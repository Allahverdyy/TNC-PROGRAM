# Gün 8: Flask Web Framework, API Oluşturma, Chatbot'u Web Servisine Dönüştürme

## 1. Flask Nedir — Neden Kullanılıyor

- **Flask**: Python için web servisleri/API'ler oluşturmayı sağlayan, hafif (micro) bir web framework kütüphanesi.
- Alternatif: **FastAPI** — daha modern, asenkron çalışıyor. Flask senkron çalışıyor.
- **Asenkron çalışma neden daha sağlıklı:** Bir noktada hata/gecikme olsa bile, diğer bağımsız işlemler bloklanmadan devam edebilir — bu backend/frontend haberleşmesinde daha esnek/dayanıklı bir yapı sağlar.
- Bu eğitimde Flask kullanılıyor çünkü öğrenmesi kolay, ihtiyaçları karşılamaya yetiyor.

## 2. Flask Kurulumu ve İlk Uygulama

```bash
pip install flask
```

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def ana_sayfa():
    return "Merhaba Flask çalışıyor"

@app.route("/hakkinda")
def hakkinda():
    return "Bu bir sade sitedir"

if __name__ == "__main__":
    app.run(debug=True)
```
- `@app.route("/")`: Ana sayfa (kök adres) — hiçbir uzantı verilmediğinde açılacak sayfa.
- `@app.route("/hakkinda")`: Farklı bir URL uzantısı (path) tanımlar — aynı domain altında farklı sayfalar oluşturmak için kullanılır.
- `app.run(debug=True)`: Sunucuyu ayağa kaldırır. **debug=True** ile, kod değiştirilip kaydedildiğinde (Ctrl+S) sunucu YENİDEN BAŞLATILMADAN otomatik olarak güncel hali yansıtılır — geliştirme sürecini hızlandırır.
- Kütüphane VS Code içinde tanınmıyorsa (kırmızı/turuncu alt çizgi), terminalden (CMD/PowerShell) doğrudan çalıştırılabilir — Visual Studio'nun Python entegrasyonu farklı bir ortamı görüyor olabilir.

## 3. URL'den Veri Alma (Route Parametreleri)

```python
@app.route("/selam/<isim>")
def selamla(isim):
    return f"Selam {isim}"
```
- URL'in bir parçası dinamik olarak alınabilir (örn. `/selam/Ahmet` → "Selam Ahmet").
- Kullanım örneği: LinkedIn gibi sitelerde kullanıcı adının URL'de görünmesi bu mantığa benzer.

## 4. GET ve POST Metotlarını Birlikte Yönetme

```python
from flask import request

@app.route("/veri", methods=["GET", "POST"])
def veri():
    if request.method == "POST":
        gelen = request.get_json()
        return {"mesaj": "Veri alındı", "gelen": gelen}
    else:
        return "GET isteği ile geldiniz"
```
- Bir route (adres) hem GET hem POST metodunu kabul edecek şekilde tanımlanabilir; `request.method` ile hangi metodun kullanıldığı kontrol edilir.
- **Ara katman (middleware) mantığı:** Genelde 2 API söz konusu olur — biri dış kaynak (örn. yapay zeka API'sı), diğeri sizin backend'iniz (Flask). Backend, dış API'dan veri çeker (GET), sonra bu veriyi frontend'e (Wix/arayüz) yönlendirir (POST/response) — Flask bu "orta katman" görevini görür.

## 5. Jinja Şablon (Template) ile HTML Sunma

### Proje Yapısı
```
proje/
├── app.py
└── templates/
    └── index.html
```

```python
from flask import render_template

@app.route("/")
def ana_sayfa():
    isim = "Ahmet"
    return render_template("index.html", isim=isim)
```

```html
<!-- templates/index.html -->
<header>
    <h1>Merhaba {{ isim }}</h1>
</header>
```
- HTML dosyaları **mutlaka `templates/` klasörü içinde olmalı** — Flask bu klasörden otomatik olarak şablon arar.
- Değişkenler HTML içinde `{{ değişken_adı }}` şeklinde (Jinja template dili) çağrılır.
- HTML/CSS içeriğini elle yazmak zorunlu değil — bu kodlar AI ile hızlıca üretilip Flask'e entegre edilebilir.

## 6. Query Parametreleri (Sorgu Parametreleri)

```python
from flask import request

@app.route("/ara")
def ara():
    sorgu = request.args.get("q")
    return f"Aranan: {sorgu}"
```
- URL'in sonuna `?parametre=değer` şeklinde eklenen kısımlar (query string) `request.args.get()` ile okunur.

## 7. Flask Proje Mimarisi — Standart Klasör Yapısı

```
proje/
├── app.py                # Flask ana dosyası, route'ların bulunduğu yer
├── venv/                 # Sanal ortam
├── .env                  # Gizli API key'ler
├── .gitignore             # .env ve venv/ gibi klasörlerin GitHub'a gitmesini engeller
├── requirements.txt       # Bağımlılık listesi
└── templates/
    └── index.html
```
- `venv/`: farklı projelerin farklı kütüphane versiyonlarını izole tutması için.
- `requirements.txt`: kütüphanelerin kendisini değil, sadece isim/versiyon listesini commit etmek için — kod başka bir ortama taşındığında `pip install -r requirements.txt` ile tüm bağımlılıklar hızlıca kurulur.
- `.env`: API key gibi gizli bilgiler — asla commit edilmemeli.

## 8. Chatbot'u Flask API'sine Dönüştürme (Ana Yapı)

### Tam Kod Şablonu
```python
from flask import Flask, request, jsonify
from groq import Groq
from dotenv import load_dotenv
import os

load_dotenv()

app = Flask(__name__)
client = Groq(api_key=os.getenv("GROQ_API_KEY"))

@app.route("/chatbot", methods=["POST"])
def chatbot():
    veri = request.get_json()
    soru = veri.get("soru")

    if not soru:
        return jsonify({"hata": "Soru bulunamadı"}), 400

    try:
        cevap = client.chat.completions.create(
            model="llama-3.3-70b-versatile",
            messages=[{"role": "user", "content": soru}]
        )
        mesaj = cevap.choices[0].message.content
        return jsonify({"cevap": mesaj})
    except Exception as hata:
        return jsonify({"hata": str(hata)}), 500

if __name__ == "__main__":
    app.run(debug=True)
```

### Adım Adım Mantık (Katman Katman)
1. Flask entegre edilir, `app` nesnesi oluşturulur.
2. Yapay zeka API'sı (Grok/OpenAI/Gemini) entegre edilir, `.env`'den API key çekilir.
3. `client` nesnesi (AI bağlantısı) ayağa kaldırılır.
4. Route (`/chatbot`) tanımlanır — hangi adrese istek atıldığında bu fonksiyonun çalışacağı belirlenir.
5. Gelen JSON veriden `soru` çekilir — **veri kontrolü (if not soru)** yapılır, boş/eksik veri varsa hata döndürülür (crash önlenir).
6. Soru varsa AI modeline yönlendirilir, cevap alınır, JSON olarak geri döndürülür.
7. Hata durumunda `try/except` ile yakalanıp anlamlı bir hata mesajı JSON formatında döndürülür.

## 9. API'yi Test Etme — İki Yöntem

### Yöntem 1: Terminalden CURL/Request ile
```python
# test.py
import requests

url = "http://127.0.0.1:5000/chatbot"
veri = {"soru": "Merhaba nasılsın?"}

cevap = requests.post(url, json=veri)
print(cevap.status_code)
print(cevap.json())
```
- Bu test kodu ÇALIŞIRKEN, Flask sunucusunun (chatbot dosyası) da ayrı bir terminalde/pencerede AKTİF ÇALIŞIR halde olması gerekir — iki ayrı işlem eş zamanlı çalışmalı.

### Yöntem 2: Terminal (curl komutu) ile Doğrudan
- Sunucu ayağa kaldırıldıktan sonra terminalden bir `curl` isteği ile de POST gönderilip sonuç doğrudan terminalde görülebilir.

## 10. Durum Kodlarına Göre Hata Teşhisi

| Kod | Anlamı |
|---|---|
| 200 | Başarılı |
| 201 | Oluşturuldu (Created) |
| 400 | İstemci hatası (eksik/hatalı veri) |
| 401 | Yetkisiz |
| 404 | Bulunamadı |
| 405 | Metot izin verilmiyor (örn. GET yerine POST beklenirken GET gönderilmiş) |
| 500 | Sunucu hatası |

- Ders sırasında canlı olarak 405 hatası ile karşılaşıldı — sebebi route'un sadece belirli bir metodu (`methods=[...]`) kabul etmesiydi, test isteği yanlış metotla gönderilmişti. Bu tür hataları çözmek için durum kodunu okumak ilk adımdır.

## 11. RESTful API Mimarisi Kavramı

- **RESTful API özel bir komut seti değildir — bir MİMARİ/tasarım prensibidir.**
- Fikir: aynı kaynak/domain üzerinde farklı HTTP metotlarını (GET, POST, PUT, DELETE) kullanarak organize, tutarlı bir haberleşme yapısı kurmak.
- Benzetme: "garson-müşteri ilişkisi" — her isteği ayrı ayrı, dağınık şekilde göndermek yerine, düzenli/organize bir sırayla ve mantıklı gruplamayla istek yapmak.
- Bugüne kadar yazılan API yapıları (route + metot ayrımı + JSON response) aslında basit birer RESTful API örneğiydi.

## 12. API Tasarım İlkeleri

1. **Anlamlı isimlendirme:** Route/adres isimleri, o adresin yaptığı işi net şekilde yansıtmalı (`/kullanicilar`, `/urunler`, `/software` gibi) — özellikle bu API başka bir yerden (örn. Wix'ten) çağrıldığında, hata durumunda isimlendirme sayesinde hatanın kaynağı hızlıca anlaşılır.
2. **Veri doğrulama:** Gelen her veri kontrol edilmeli — eksik/hatalı veri varsa (`if not veri`) uygun hata döndürülmeli, işlem sessizce yanlış sonuç üretmemeli.
3. **Tutarlı JSON yapısı:** Her zaman aynı formatta yanıt dönmeli (örn. her hata `{"hata": "..."}`, her başarı `{"sonuc": "..."}` gibi sabit bir şablonla) — öngörülebilirlik sağlar.
4. **Hata yönetimi (try/except):** Her haberleşme kodu mutlaka try/except içinde olmalı.

## 13. Genel Hata Ayıklama Felsefesi (Tekrar Vurgu)

- Kod yazmak/çalıştırmak nispeten kolay; **hatayı ÇÖZMEK** daha zor ve zaman alıcı olan kısım.
- Küçük syntax hataları (unutulan virgül, nokta, eksik import) saatler harcatabilir — bu normal, cesaret kırılmamalı.
- Haberleşme kodu yazarken:
  - try/except ZORUNLU.
  - Her adım tutarlı ve öngörülebilir olmalı.
  - Adres/route isimlendirmesi anlamlı olmalı.
  - Veri doğrulaması atlanmamalı.

## 14. Sonraki Gün İçin
- CORS mantığı detaylandırılacak.
- GitHub'a yönlendirme/commit işlemleri işlenecek.
