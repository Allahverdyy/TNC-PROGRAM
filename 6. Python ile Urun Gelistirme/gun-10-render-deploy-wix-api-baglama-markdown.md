# Gün 10: Render'da Deploy, Wix-API Bağlantısı, Hata Yönetimi, Markdown (Eğitimin Son Günü)

## 1. Render.com — API'yi Canlıya Alma (Deploy)

- **Render**: yazdığımız Flask API'sini ayağa kaldırıp yayınlamak (deploy etmek) için kullanılan araç/platform.
- Render'a kaydolurken **GitHub hesabıyla** bağlanılmalı (Google/Gmail ile değil) — çünkü yayınlanan tüm repolar GitHub üzerinden buraya bağlanacak.
- **Dashboard**: mevcut projelerin ve bunların çalışır durumda olup olmadığının görüldüğü ekran.

### Yeni Web Servisi Oluşturma Adımları
1. **New → Web Service** seçilir.
2. Bağlanacak GitHub reposu seçilir (örn. proje reposu).
3. **Build Command**: `pip install -r requirements.txt` — bu alana dokunulmamalı, olduğu gibi bırakılmalı. Bu komut, web servis ayağa kalkarken hangi kütüphanelerin (`requirements.txt` içindeki) sunucu tarafında (ayrılan CPU alanında) kurulacağını belirtir.
4. **Start Command**: `gunicorn app:app` — Render, Flask'ı doğrudan `python app.py` ile değil **gunicorn** (production-grade WSGI sunucusu) ile başlatıyor. `app:app` ifadesindeki ilk `app`, dosya adını (`app.py`), ikinci `app` ise o dosya içindeki Flask nesnesinin adını (`app = Flask(__name__)`) belirtir. Bu isim değiştirilmemeli, genel kullanım budur.
5. **Instance Type / RAM**: ücretsiz (0 dolar) seçenek test/geliştirme için yeterli. Web servis ileride büyük ölçekli bir ürüne dönüşürse, daha yüksek RAM/ücretli paketler seçilebilir (aylık farklı fiyatlandırma seçenekleri mevcut).

### Environment (Ortam Değişkenleri) — Kritik Adım
- **`.env` dosyası asla GitHub'a commit edilmemeli** — bu yüzden Render'da projeyi ayağa kaldırabilmek için gizli değerler (API key'ler) Render panelindeki **Environment** bölümüne elle girilmelidir.
- Lokaldeki `.env` dosyasında ne varsa (örn. `GROQ_API_KEY`), aynı isim ve değer Render'ın Environment alanına tek tek eklenmelidir.
- Toplu dosya yükleme seçeneği (`.env` dosyasını sürükleyip ekleme) de mevcuttur ancak **tavsiye edilen yöntem tek tek elle girmek** — toplu yüklemede yanlış/hatalı değer girme riski daha yüksek.
- **Environment eksik/yanlışsa deploy hatası oluşur** — API key alanı boş bırakılırsa web servis ayağa kalkmaz, hata verir.

### Deploy Sonrası
- **Deploy Web Service** butonuna basıldığında build işlemi başlar; hata yoksa yeşil bir gösterge ile başarı bildirilir. Hata varsa terminal ekranında hangi satırda, hangi sebepten hata oluştuğu gösterilir.
- Deploy sonrası GitHub'da yapılan değişiklik bazen otomatik yansımayabilir — bu durumda **Clear Build & Deploy** (temiz build) ile yeniden başlatılabilir.
- Başarılı deploy sonrası proje için bir **canlı adres/URL** oluşur — bu adres artık API'nin gerçek, kullanılabilir haberleşme noktasıdır; front-end (Wix) tarafında bu adres kullanılacaktır.
- **Ücretsiz plan sınırlaması**: 15 dakika boyunca istek gelmezse servis "uyku moduna" geçer; yeniden istek geldiğinde servisin tekrar ayağa kalkması biraz zaman alır (ilk istek gecikmeli cevap dönebilir).

## 2. Kullanılacak Yapay Zeka Modeli — Güncel Model Seçimi

- Kullanılan yapay zeka modelleri zamanla **kullanımdan kaldırılabiliyor (deprecated)** — örn. dersin başında kullanılan bir Groq modeli ~3-4 hafta içinde kapatıldı.
- Bu yüzden model ismi kodda güncel/çalışır bir modelle değiştirilmeli — güncel model adı, ilgili sağlayıcının (Groq, OpenAI vb.) dokümantasyon sayfasından kontrol edilmeli.
- Groq üzerinden hem kendi modelleri hem de OpenAI destekli modeller kullanılabiliyor; dokümantasyondaki örnek kod/model adı doğrudan projeye entegre edilebilir.

## 3. Backend (Render) — Route Yapısı Hatırlatması

- Python/Flask tarafında her bir işlev için ayrı **route** (yol) tanımlanır (örn. `/chatbot`).
- **Sayfalar (HTML/frontend test amaçlı)** ile **API (asıl haberleşme uç noktaları)** ayrı ayrı tutulmalı — ikisi karıştırılırsa (`/sohbet` gibi tek bir adrese hem sayfa hem API mantığı yüklenirse) haberleşme başarısız olur.
- **Öneri:** her yapay zeka sağlayıcısı (Groq, Gemini vb.) için haberleşme kodu ayrı bir modülde/dosyada tutulmalı — hepsini tek bir route içine yazmak karmaşıklığa ve yanlış veri çekmeye yol açar.
- API adresine istek atarken **doğru path'in (`/api/...` gibi) belirtilmesi zorunlu** — sadece ana render adresine (kök adres) istek atmak, doğrudan bir sayfa/HTML açmaya çalışmak anlamına gelir; API endpoint'ine ulaşmaz.

## 4. Wix Tarafında API'ye Bağlanma (Fetch)

```javascript
import { fetch } from "wix-fetch";

$w.onReady(function () {
    $w("#gonderButonu").onClick(() => soruyuGonder());
    $w("#girisKutusu").onKeyPress((event) => {
        if (event.key === "Enter") {
            soruyuGonder();
        }
    });

    async function soruyuGonder() {
        let soru = $w("#girisKutusu").value;

        if (!soru) {
            $w("#cevapAlani").text = "Lütfen bir soru yazın";
            return;
        }

        $w("#cevapAlani").text = "Düşünüyorum...";
        $w("#girisKutusu").value = "";

        try {
            let response = await fetch("https://render-adresiniz.onrender.com/api/chatbot", {
                method: "post",
                headers: { "Content-Type": "application/json" },
                body: JSON.stringify({ mesaj: soru })
            });

            if (response.ok) {
                let data = await response.json();
                $w("#cevapAlani").text = data.cevap;
            } else {
                console.log(response.status);
                $w("#cevapAlani").text = "Bir hata oluştu";
            }
        } catch (error) {
            console.log(error);
            $w("#cevapAlani").text = "Bağlantı hatası oluştu";
        }
    }
});
```

### Kod Akışının Açıklaması
1. **`import { fetch } from "wix-fetch";`** — unutulmaması gereken zorunlu modül; HTTP isteklerini (GET/POST) yönetir.
2. **`onClick`** ve **`onKeyPress`** (Enter tuşu) aynı fonksiyonu (`soruyuGonder`) tetikler — hem butona tıklayarak hem Enter'a basarak istek gönderilebilir.
3. **`async function`**: haberleşme sırasında bekleme (asenkron) durumunu yönetmek için kullanılır — cevap gelene kadar kod diğer işlemleri bloklamadan bekler.
4. Giriş kutusundan alınan `soru` değeri boşsa (`if (!soru)`), kullanıcıya uyarı gösterilip fonksiyon `return` ile sonlandırılır.
5. Boş değilse: kullanıcıya bekleme mesajı ("Düşünüyorum...") gösterilir, giriş kutusu temizlenir.
6. **`try` bloğunda**: `fetch` ile API adresine POST isteği gönderilir — `method`, `headers` (Content-Type: application/json) ve `body` (JSON.stringify ile gönderilecek veri) belirtilir.
7. **JSON key ismi tutarlılığı kritik** — backend'de (Flask) hangi key adı bekleniyorsa (`mesaj`, `soru` vb.), frontend'de (Wix) gönderilen JSON'da da **birebir aynı key adı** kullanılmalı; aksi halde cevap dönmez.
8. **`response.ok`** — `true`/`false` döner; `true` ise haberleşme başarılı (200'lü kod), `false` ise başarısız (400'lü/500'lü kod). Bu değer `if/else` ile kontrol edilerek akış yönetilir.
9. Başarılıysa `response.json()` ile veri (`data`) alınır, `data.cevap` metin alanına yazdırılır.
10. Başarısızsa `response.status` (hata kodu) konsola yazdırılarak hatanın sebebine dair ipucu elde edilir.
11. **`catch` bloğu**: try içindeki kodlardan herhangi biri patlarsa (network hatası, syntax hatası vb.) buraya düşer — hata konsola loglanır ve kullanıcıya genel bir hata mesajı gösterilir.

## 4b. Ekranda Gösterilen Resmî Slaytlar — Wix ↔ Python İstek-Cevap Akışı (Tam Kod)

**Gerçek proje referansı:** Salih Tekin'in örnek "Akıllı Satış Asistanı" (Smart Lead AI) reposu — `https://github.com/salihtekin/smartlead_ai`. Repo içinde `app/`, `docs/`, `static/`, `uygulama/` klasörleri ve `ayarlar.py`, `baslat.py`, `config.py`, `gerekinimler.txt`/`requirements.txt`, `run.py`, `test_arayuz.html` dosyaları var. `.env.example` şablonu şu yapıyı gösteriyor:

```
# Flask Ortamı
FLASK_ENV=development

# Güvenlik
SECRET_KEY=cok-gizli-bir-anahtar-buraya-yazin

# AI Sağlayıcı: "gemini" veya "openai"
AI_PROVIDER=gemini

# Google Gemini API Key (https://aistudio.google.com/app/apikey)
GEMINI_API_KEY=GCP_API_ANAHTARI_BURAYA_YAZILACAK

# OpenAI API Key (https://platform.openai.com/api-keys)
OPENAI_API_KEY=sk-...buraya-openai-key-yazin

# İşletme Tanımı
BUSINESS_NAME=TechDrone Systems
BUSINESS_CONTEXT=Sen TechDrone Systems şirketinin profesyonel B2B satış asistanısın. Şirket; savunma, lojistik ve tarım sektörlerine yönelik otonom insansız hava a...

# CORS (Production'da kendi Wix domain'inizi yazın)
CORS_ORIGINS=*
```
- `.env.example` dosyası kopyalanıp `.env` yapılır (`cp .env.example .env`), gerçek `.env` dosyası **asla Git'e commit edilmez** (`.gitignore`'a eklenir).
- `AI_PROVIDER` ile Gemini veya OpenAI arasında seçim yapılabiliyor — proje iki sağlayıcıyı da destekleyecek şekilde tasarlanmış.
- `BUSINESS_CONTEXT`, chatbot'un LLM'e gönderdiği sistem promptunun/iş tanımının bir parçası — işletmenin ne iş yaptığını modele anlatan metin.

**Adım 1: wix-fetch Modülünü İçe Aktarmak**
```javascript
// Kodun EN ÜSTÜNE yazılır (onReady'den önce)
import { fetch } from 'wix-fetch';

$w.onReady(function () {
  $w("#gonderButonu").onClick(function () {
    // Artık fetch fonksiyonunu burada kullanabiliriz
    console.log("fetch hazır!");
  });
});
// Not: Wix bazı sürümlerde 'wix-fetch' modülünü farklı isimlendirebilir;
// dokümantasyondan kontrol edin. Modern Velo'da 'wix-fetch' yerleşik gelir; kurulum gerekmez.
```

**Adım 2: POST İsteği Göndermek**
```javascript
import { fetch } from 'wix-fetch';

function soruyuGonder() {
  let soru = $w("#girisKutusu").value;

  // API'ye POST isteği gönder
  fetch("https://benim-api.com/sohbet", {
    method: "POST",
    headers: {
      "Content-Type": "application/json"
    },
    body: JSON.stringify({ soru: soru })
  })
  .then(function (response) {
    // Cevabı JSON'a çevir
    return response.json();
  })
  .then(function (data) {
    // Gelen AI cevabını ekrana yaz
    $w("#cevapAlani").text = data.cevap;
  });
}
```
- `fetch`'e URL ve ayarları (`method`, `headers`, `body`) veririz.
- `method: 'POST'` → veri gönderiyoruz.
- `headers` → JSON gönderdiğimizi belirtir.
- `body` → `JSON.stringify` ile soruyu paketleriz.
- `.then()` ile cevabı yakalarız (zincir halinde birden fazla `.then` kullanılabilir).

**Hatırlatma: Python (Flask) API Tarafı — Canlıda Çalışan Kod**
```python
from flask import Flask, request, jsonify
from flask_cors import CORS
from openai import OpenAI

app = Flask(__name__)
CORS(app)                     # Wix'in erişmesi için ŞART!
client = OpenAI()

@app.route("/sohbet", methods=["POST"])
def sohbet():
    veri = request.get_json()
    soru = veri.get("soru")   # Wix'ten gelen soru

    cevap = client.chat.completions.create(
        model="gpt-4o-mini",
        messages=[{"role": "user", "content": soru}]
    )
    ai_cevap = cevap.choices[0].message.content
    return jsonify({"cevap": ai_cevap})   # Wix'e dön
```
- Wix'in gönderdiği isteği karşılayan Python API'miz hazır olmalı.
- **CORS ayarı KESİNLİKLE açık olmalı** (Wix farklı bir origin'den geldiği için).
- API soruyu alır, LLM'e sorar, cevabı JSON döner.

**Modern Yöntem: async/await (`.then()` Zincirine Alternatif)**
```javascript
import { fetch } from 'wix-fetch';

// Fonksiyonu 'async' yap
async function soruyuGonder() {
  let soru = $w("#girisKutusu").value;

  // İsteği gönder ve cevabı BEKLE (await)
  let response = await fetch("https://benim-api.com/sohbet", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({ soru: soru })
  });

  // Cevabı JSON'a çevir (yine await)
  let data = await response.json();

  // AI cevabını ekrana yaz
  $w("#cevapAlani").text = data.cevap;
}
```
- `.then()` zinciri yerine `async`/`await` daha okunaklıdır.
- Fonksiyonu `async` ile işaretleriz.
- `await` ile cevabı bekleriz (kod sırayla akar, callback karmaşası olmaz).
- Hataları `try-catch` ile yakalarız (aşağıda).

**Wix → Python İstek-Cevap Akışı (4 Adım Diyagramı)**
1. **Wix (Tarayıcı)** — Kullanıcı soru yazar, butona tıklar. `wix-fetch` POST isteği hazırlar.
2. **POST İsteği → İnternet** — `body: {"soru": "Python nedir?"}` JSON formatında API'ye gider.
3. **Python API (Sunucu)** — Soruyu alır, LLM'e sorar, AI cevabını üretir.
4. **JSON Cevap → Wix** — `{"cevap": "..."}` geri döner, text alanına yazılır.

**İstekte Hata Yönetimi (try-catch)**
```javascript
async function soruyuGonder() {
  let soru = $w("#girisKutusu").value;

  try {
    // Riskli işlem: API isteği
    let response = await fetch("https://benim-api.com/sohbet", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({ soru: soru })
    });
    let data = await response.json();
    $w("#cevapAlani").text = data.cevap;
  } catch (error) {
    // Hata olursa burası çalışır
    console.log("Hata:", error);
    $w("#cevapAlani").text = "Bağlantı hatası!";
  }
}
```
- İnternet kesintisi veya sunucu hatası isteği başarısız kılabilir.
- `fetch` çağrısını `try-catch` içine alırız.
- Hata olursa kullanıcıya bilgi verir, kod çökmez.
- `finally` bloğu, başarılı/başarısız her durumda çalışır (istenirse eklenebilir).

**Bonus: GET İsteği ile Veri Çekmek**
```javascript
import { fetch } from 'wix-fetch';

async function ornekSorulariGetir() {
  // GET isteği (method belirtilmezse varsayılan GET'tir)
  let response = await fetch("https://benim-api.com/ornekler");

  let data = await response.json();
  console.log("Örnek sorular:", data);

  // Gelen veriyi kullan (örn. bir listede göster)
  // data.sorular.forEach(...)
}

// Sayfa açılınca örnekleri yükle
$w.onReady(function () {
  ornekSorulariGetir();
});
```
- Bazen API'den sadece veri okumak isteriz (POST değil).
- **GET isteğinde `body` olmaz** — veri URL'de gönderilir.
- `method` belirtmezsek varsayılan **GET**'tir.
- Örnek kullanım: hazır soru listesi veya geçmiş sohbetleri çekmek.

## 5. Response Durumu — `response.ok` ve `response.status`

- `response.ok`: boolean (`true`/`false`) — haberleşmenin başarılı olup olmadığını gösterir.
- `response.status`: sayısal HTTP durum kodu (200, 400, 401, 404, 500 vb.) — hatanın **nereden kaynaklandığını** anlamak için konsola loglanmalı.
- Boş veri gönderildiğinde (`soru` boşsa ve backend bunu reddediyorsa) `response.ok` **false** döner — bu, hem frontend hem backend tarafında veri doğrulamasının birlikte çalıştığını gösterir.

## 6. Haberleşme Sorunu Yaşandığında Kontrol Sırası (Özet)

1. **API adresi doğru mu?** — Render'dan alınan adres + doğru path (`/api/...`) birebir doğru yazılmış mı?
2. **JSON key isimleri tutarlı mı?** — frontend'in gönderdiği key ile backend'in beklediği key aynı mı?
3. **CORS ayarlanmış mı?** — ayarlanmazsa kesinlikle 400 hatası alınır, bunun "kaçarı yoktur."
4. Yukarıdakilerin hepsi doğruysa: **`console.log` ile debug** yapılmalı.

## 7. Debug Yöntemi — Adım Adım console.log

- Hata hangi satırda oluştuğu net anlaşılamıyorsa, kodun şüpheli görülen her adımına ayrı `console.log("test1")`, `console.log("test2")` gibi işaretleyici loglar konularak, **hangi log'un konsolda görünmediği** tespit edilir — kod o noktada "patlamış" demektir.
- Bu, JavaScript tarafında satır satır hata ayıklamanın en pratik yöntemi.

## 8. Genel Hata Ayıklama Disiplini (Eğitim Boyunca Vurgulanan Ana Tema)

- **Kodunuza hakim olun** — yapay zekadan kod üretilmiş olsa bile, her satırın ne işe yaradığı bilinmeli. Hata oluştuğunda kodu bilmeyen biri (eğitmen dahil) o kodu "tersine mühendislik" yaparak çözmek zorunda kalır — bu zaman kaybettirir.
- **Kopyala-yapıştır dikkatsizliği** ciddi hatalara yol açar — örn. aynı fonksiyonun yanlışlıkla iki kez tanımlanması gibi yapısal hatalar, "syntax hatası" gibi görünüp aslında kod yapısından kaynaklanabilir; hatayı çözmeden önce kodu **okumak** şart.
- Yapay zeka ile "kavga etmek" yerine, doğru ve net soru/prompt yazmak önemli — yapay zeka doğru bilgi verir, sorunun kalitesi cevabın kalitesini belirler.
- **Araştırma becerisi** temel yetkinlik — bir konuyu bilmemek sorun değil, o konuyu doğru şekilde araştırıp uygulayabilmek asıl beceridir.

## 9. Markdown (README / Dokümantasyon) Yazımı

- Proje dokümantasyonu (`README.md` veya başka `.md` dosyaları) ile kodun mimarisi, kullanılan route'lar, haberleşme metotları, klasör yapısı açıklanır.
- Markdown, GitHub, GitLab, Word, VS Code gibi birçok platformda standart olarak desteklenir.

### Temel Markdown Sözdizimi
```markdown
# Ana Başlık
## Alt Başlık
### Daha Alt Başlık

Normal paragraf metni buraya yazılır.

**Kalın yazı** için çift yıldız kullanılır.

- Madde işaretli liste öğesi
- Başka bir öğe

1. Numaralı liste öğesi
2. İkinci öğe

- [ ] İşaretlenebilir (checkbox) liste öğesi

`tek backtick` ile satır içi kod gösterilir.

​```
çoklu backtick ile kod bloğu oluşturulur
​```

[Site adı](https://ornek-site.com)  → link oluşturma

| Başlık 1 | Başlık 2 |
|---|---|
| Değer 1  | Değer 2  |
```
- Bu yapılar ezberlenmek zorunda değil — ihtiyaç duyulduğunda yapay zekadan veya dokümantasyondan öğrenilip kullanılabilir; önemli olan kendi projenizin mimarisini bu şekilde **anlaşılır şekilde belgeleyebilmek**.

## 10. Eğitim Sonu — Sırbistan Öncesi Beklenen Teslimler (Envanter)

Eğitmenin Sırbistan'a (yüz yüze eğitim/atölye) gelmeden önce tamamlanmasını istediği maddeler:
1. **Proje mimarisi/dokümantasyonu** — klasör yapısının oluşturulması ve açıklanması.
2. **Render tarafının ayağa kaldırılması** — API'nin deploy edilip canlı bir mesaj/cevap döndürebilir halde olması (HTML ile de test edilebilir, Wix'e bağlanması tercih sebebi ama zorunlu değil).
3. **GitHub'a tüm proje/klasör yapısının commit'lenmesi.**
4. **Chatbot ve dashboard kısımlarının** büyük oranda bu süreçte tamamlanması beklenir (yüz yüze eğitimde daha ileri/zorlayıcı görevler verilecek).
5. Takıntılı/sözdizimsel (syntax) hatalarda değil, ancak **kavramsal** noktalarda soru sorulabilir — dersin öncesinde e-posta yoluyla iletişim mümkün.

## 11. Kapanış Notları

- Eğitim boyunca hedef: yazılım geçmişi olan/olmayan herkesin, yapay zeka destekli olsa dahi **kendi kodunun mantığına hakim olarak** bir web servisi + chatbot + Wix arayüzü ortaya çıkarabilmesi.
- JavaScript tarafında da (Python'daki gibi) kod satır satır okunabilir olmalı; yazamasanız da neyin ne işe yaradığını anlatabilmelisiniz.
- Sonraki adım: yüz yüze eğitim (Belgrad/Sırbistan) — orada bireysel destek ve ek zorlayıcı görevler verilecek.
