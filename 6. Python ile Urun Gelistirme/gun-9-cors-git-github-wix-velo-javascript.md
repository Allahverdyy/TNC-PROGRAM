# Gün 9: CORS, Git/GitHub, Wix Velo JavaScript Temelleri

## 1. CORS Nedir — Neden Gerekli

- İki ayrı adres (örn. `salihtekin.com` ve `gitup.com`, veya bir API ile bir web sitesi) birbirleriyle haberleşmek istediğinde, karşı tarafın buna izin vermesi gerekir — tarayıcı güvenlik duvarı bu izin olmadan veri akışını engeller.
- **CORS**: Flask ile kullanılan ayrı bir kütüphane (`flask-cors`) — flask'tan bağımsız, `pip install flask-cors` ile kurulur.
- CORS eklenmezse (sunucuda hiç ayarlanmamazsa), web tarafından API'ya (örn. chatbot) istek gönderildiğinde cevap dönmez — "haberleşemedi" gibi hata mesajları alınır.

```python
from flask_cors import CORS

app = Flask(__name__)
CORS(app)  # tüm adreslere izin verir — sadece geliştirme aşamasında kullanılmalı
```

- **`CORS(app)`**: bütün adreslere izin verir. Canlıya alınacak/yayınlanacak bir üründe bu **tehlikeli** — veri çalınması, gereksiz yönlendirme riski oluşturur.
- **Belirli adreslere izin verme (production için doğru yöntem):**
```python
CORS(app, origins=["https://ornek-site.com"])
```
- `origins` listesine sadece haberleşilmesi gereken adresler yazılmalı, diğer adreslerden gelen istekler otomatik engellenir.

## 2. Fetch (JavaScript Tarafı)

- Wix/Velo tarafında (JavaScript) bir API adresinden veri çekmek veya oraya veri göndermek için **fetch** kullanılır.
- Fetch içinde belirtilmesi gerekenler: hangi adresle haberleşiliyor, hangi HTTP metodu kullanılıyor, veri hangi formatta dönecek, hangi veri gönderiliyor.
- Bu dersin konusu değil ama bilinmesi gerekiyor: fetch doğru ayarlanmazsa kod çalışmaz.

## 3. CORS Hatası Alındığında Kontrol Sırası

Yapay zeka modeliyle haberleşen bir kod yazıldığında 400'lü/500'lü hata alınırsa sırasıyla kontrol edilmesi gerekenler:
1. **API key** doğru çekiliyor mu, doğru yerden çekiliyor mu (örn. Groq API key)?
2. **CORS** doğru kurulmuş ve ayarlanmış mı?
3. **Fetch** (JavaScript tarafındaki haberleşme) doğru ayarlanmış mı?
4. (İleride) **Render** tarafındaki ayarlar doğru mu?

## 4. Git ve GitHub — Temel Kavramlar

- **Git**: bir sürüm kontrol sistemi (yazılım). **GitHub**: bu sistemin arayüzü/barındırma platformu.
- Git ile: her yeni versiyonda değişiklikleri commit'leyip saklayabilme, hata durumunda geri dönebilme (yedekleme), ayrı dallarda (branch) paralel çalışabilme sağlanır.
- **Repository (repo)**: projenin tamamını ve geçmişini tutan depo alanı.
- **Commit**: o anki değişikliğin repoya yönlendirilmesi (anlık kayıt).
- **Add**: hangi dosyaların commit'leneceğini belirleme/işaretleme işlemi.
- **Push**: lokaldeki commit'leri GitHub'a yönlendirme.
- **Pull**: GitHub'daki değişiklikleri lokale çekme.
- **Branch (dal)**: aynı projenin farklı kişiler/farklı özellikler için paralel geliştirilebildiği ayrı çalışma alanları — sonradan `merge` ile birleştirilir (çakışan noktalar **conflict** olarak ortaya çıkar, giderilmesi gerekir). Şu aşamada branch'e derinlemesine girilmedi — temel commit bilgisi yeterli.

## 5. Git Kurulumu ve İlk Ayarlar

- git-scm.com üzerinden "Install for Windows" ile indirilir, kurulum adımları sabit (varsayılanlarla ilerlenebilir).
- GitHub'da hesap oluşturulur (dashboard: repolar, profil, commit geçmişi buradan yönetilir).

```bash
git config --global user.name "Kullanıcı Adı"
git config --global user.email "email@adres.com"
```
- Username: genelde gerçek isim. Email: kullanılan GitHub email adresi.
- **`git config --list`**: mevcut ayarları (username, email, bağlı repo, default branch vb.) listeler.
- **`git --version`**: kurulu Git versiyonunu gösterir.
- Varsayılan ana dal adı **main** olarak ayarlanmalı (yaygın kullanım).

## 6. .gitignore Dosyası

- Proje klasöründe `.gitignore` adlı bir dosya oluşturulur.
- İçine, commit'lenmemesi gereken dosya/klasör uzantıları yazılır (örn. `.env`, `venv/`) — özellikle **gizli bilgiler** (API key gibi) asla GitHub'a commit'lenmemeli.
- Git, `.gitignore` içindeki değerleri görmezden gelerek diğer tüm dosyaları commit'e dahil eder.

## 7. GitHub'da Repo Oluşturma

- GitHub → Repositories → **New** ile yeni repo açılır.
- Repo adı verilir (örn. `test1`), isteğe bağlı açıklama girilir.
- **Public**: herkese açık. **Private**: sadece izin verilenler görebilir.
- **README** ve **.gitignore** dosyaları GitHub tarafında oluşturulmamalı — bunlar lokalde oluşturulup commit'lenecek.
- **Lisans**: seçmek zorunlu değil; seçilecekse **MIT** (ücretsiz, açık kaynak) yaygın tercih.
- Repo oluşturulduktan sonra GitHub, ilk commit için kullanılacak komutları otomatik gösterir — ancak **"add README" seçeneğini kullanmayın**, çünkü bu sadece README dosyasını commit'ler; bunun yerine `.` (nokta) ile tüm proje dosyalarının commit'lenmesi sağlanmalı.

## 8. Temel Git Komut Akışı

```bash
git init                          # proje klasöründe git deposu başlatma (.git klasörü oluşur)
git add .                         # tüm dosyaları commit'e hazırlama
git commit -m "anlamlı mesaj"     # değişikliği kaydetme
git remote add origin <repo-url>  # lokal depoyu GitHub reposuna bağlama
git branch -M main                # ana dalı ayarlama
git push -u origin main           # GitHub'a gönderme
```

- **Farklı bir repoya zaten bağlıysa** (örn. proje klasörü daha önce başka bir `.git` içeriyorsa) hata alınabilir — bu durumda mevcut `.git` bağlantısının koparılması/silinmesi ve yeniden `git init` yapılması gerekir.
- Sonraki commit'lerde tekrar aynı sıra: `git add .` → `git commit -m "..."` → `git push`.

## 9. Commit Mesajı Kuralları

1. **Açık ve net olsun** — o commit'in neyi değiştirdiğini/düzelttiğini anlatsın. Gereksiz uzun hikaye yazılmamalı ama iş net anlatılmalı, gerekirse madde madde.
2. **Emir kipi kullanılabilir** (kaldır, düzelt, ekle gibi) — zorunlu değil ama tercih edilir.
3. **Sık commit atın** — büyük bir işi tek seferde commit'lemek yerine, her küçük görevi/fonksiyonu tamamladıkça (1-3 satırlık değişiklik bile olsa) ayrı commit atılmalı. Böylece bir hata çıktığında hangi commit'in sebep olduğu kolayca bulunur; tek büyük commit'te hatanın kaynağını bulmak zaman kaybettirir.
4. Yanlış/eksik commit mesajları iş ortamında (test ekibi, senior) geri dönüşe (code review feedback) sebep olur — bu yüzden mesajlar özenli yazılmalı.

## 10. README Dosyası

- Projenin temel tanıtım dosyası — Markdown (`.md`) formatında yazılır.
- Markdown yazım kuralları ayrı bir başlıkta ele alınacak (bu derste detaya girilmedi).

## 11. Wix Studio / Velo — Developer Moduna Giriş

- Wix Studio'da yeni site oluşturulurken **boş şablon** ile başlanabilir.
- Tasarım (UI) katmanı: buton, input alanı, text alanı gibi bileşenler sürükle-bırak ile eklenir — bu, kullanıcıya gösterilen "vitrin" kısmıdır ve önemi büyüktür (yazılım bilenler yazılımı, herkes tasarımı değerlendirebilir).
- **"Kodlamaya başla"** seçeneğiyle Developer Mode açılır — burada JavaScript (Velo) kodları yazılır.
- Wix'in sağladığı temel kolaylık: sunucu, hosting, SSL gibi teknik altyapı işlerini Wix hallediyor; geliştirici sadece koda odaklanıyor.

## 12. ID Kavramı — Tasarımla Değil ID'lerle Çalışma

- Kod tarafında UI bileşenleriyle (buton, input, text vb.) çalışabilmek için her bileşenin **ID**'si kullanılır — tasarımın kendisiyle değil, ID'lerle iş yapılır.
- Bir bileşen seçildiğinde, özellikler panelinden ID değiştirilebilir/isimlendirilebilir.

### ID İsimlendirme Kuralları
1. **Anlamlı olmalı** — hangi bileşene ait olduğunu ve ne işe yaradığını açıkça belirtmeli (örn. `inputSoru`, `sonucText`, `gonderButonu`).
2. **camelCase** kullanılmalı — birden fazla kelime birleştirildiğinde ilk kelime küçük harfle, sonraki her kelimenin ilk harfi büyük harfle başlamalı (örn. `inputSoru`, `cevapText`). Bu zorunlu değil ama yaygın standart — kodun okunabilirliğini ve globaldeki diğer kodlarla tutarlılığını sağlar.
3. **Boşluk kullanılmamalı.**
4. **Sayısal karakterle başlanmamalı.**
5. **Özel karakter / Türkçe karakter kullanılmamalı** — sistem yükü ve kod hatası riski yaratır; İngilizce harflerle yazılmalı.
6. İsteğe bağlı olarak bileşenin bulunduğu sayfa da isimlendirmeye dahil edilebilir (örn. `sayfa1InputSoru`).

## 13. Velo (JavaScript) Kod Yapısı — `$w.onReady`

```javascript
$w.onReady(function () {
    console.log("Merhaba Vix");

    function selamVer() {
        console.log("Ayrı fonksiyon");
    }
    selamVer();
});
```
- **`$w.onReady(...)`**: sayfa/kod çalıştırıldığı anda içindeki tüm kodun aktifleşmesini sağlayan ana fonksiyon.
- **`console.log(...)`**: Python'daki `print()` karşılığı — konsol ekranında (Visual Studio'daki terminale benzer) çıktı gösterir; hata ayıklamada kullanılır.
- `onReady` içinde tanımlanan fonksiyonlar çağrılarak çalıştırılabilir.
- Değişken tanımlama: `let` komutu kullanılır (Python'da karşılığı yok).
```javascript
let selam = "Selam verildi";
console.log(selam);
```
- JavaScript sözdizimi (fonksiyon tanımlama, koşullu yapılar, değişken/print mantığı) Python'a büyük ölçüde benziyor.

## 14. Elementlere Erişim — `$w("#id")`

```javascript
let girisKutusu = $w("#girisKutusu");
let gonderButonu = $w("#gonderButonu");
let cevapAlani = $w("#cevapAlani");
```
- `$w("#id")` ile ID'si belirtilen bileşene erişilir; erişilen bileşenin türüne göre farklı özellik/metodlar (`.value`, `.text`, `.label`, `.show()`, `.hide()`, `.enable()`, `.disable()` vb.) kullanılabilir.

### Sık Kullanılan Özellikler
| Özellik | Ne için |
|---|---|
| `.value` | Input/checkbox gibi bileşenlerin değerini okur/yazar |
| `.text` | Text elementinin içindeki metni okur/yazar |
| `.label` | Buton üzerindeki yazıyı değiştirir |
| `.show()` / `.hide()` | Bir elementi görünür yapar / gizler |
| `.enable()` / `.disable()` | Bir butonu aktif/inaktif hale getirir |
| `.checked` | Checkbox'ın işaretli olup olmadığını verir |

## 15. Event (Olay) Mantığı

- Her bileşenin kendine özgü event'leri vardır: `onClick`, `onChange`, `onBlur`, `onDblClick`, `onFocus`, `onInput`, `onKeyPress` vb.
- Bir event'in içine yazılan kod, o olay tetiklendiğinde (örn. butona tıklanınca) çalışır.

### Örnek: Buton Click ile Soru-Cevap Akışı
```javascript
$w("#cevapAlani").hide();

$w("#gonderButonu").onClick(() => {
    let soru = $w("#girisKutusu").value;

    if (soru === "") {
        $w("#cevapAlani").text = "Lütfen bir mesaj giriniz";
        return;
    }

    $w("#cevapAlani").show();
    $w("#cevapAlani").text = soru;
});
```
- Akış: cevap alanı başta gizli → butona tıklanınca input'taki değer okunur → boşsa uyarı yazılıp fonksiyon durdurulur (`return`) → doluysa cevap alanı gösterilir ve içeriği güncellenir.
- **Boşluk da bir değerdir** — sadece space girilmiş bir input, boş (`""`) sayılmaz; bu yüzden veri doğrulamasında dikkat edilmeli.

### Enter Tuşu ile Aynı İşlemi Tetikleme
```javascript
$w("#girisKutusu").onKeyPress((event) => {
    if (event.key === "Enter") {
        // gönder butonunun yaptığı işlemi burada da çalıştır
    }
});
```
- `onKeyPress`: herhangi bir tuşa basıldığında tetiklenir; içeride `event.key === "Enter"` kontrolüyle sadece Enter tuşuna özel davranış tanımlanır.
- Pratikte hem `onClick` hem `onKeyPress` (Enter) aynı işlemi tetikleyecek şekilde birlikte kullanılması önerilir.

### Temizleme (Reset) Örneği
```javascript
$w("#temizleButonu").onClick(() => {
    $w("#girisKutusu").value = "";
    $w("#cevapAlani").text = "";
    console.log("Temizlendi");
});
```
- Birden fazla butona farklı event'ler bağlanabilir; her buton kendi işlevine göre ayrı `onClick` tanımına sahip olabilir.

## 16. Sık Kullanılan Velo Modülleri

- **`wix-fetch`**: HTTP istekleri (GET/POST) için — API ile haberleşmede **mutlaka kullanılması gereken** modül, kolayca unutulabiliyor.
- **`wix-data`**: Wix veri tabanıyla çalışma (kayıt ekleme, sorgulama).
- **`wix-location`**: sayfa yönlendirme / farklı sayfalara geçiş.
- Bu derste yalnızca `wix-fetch` öncelikli olarak vurgulandı; API haberleşmesi bir sonraki derste detaylandırılacak.

## 17. Genel Yaklaşım — Kod Yazımı vs. Kod Okuma

- JavaScript kodlarının tamamını ezbere yazabilmek zorunlu değil — yapay zekadan hızlıca üretilip kullanılabilir.
- **Ancak üretilen kodun mantığını satır satır anlamak zorunlu** — her satırın ne işe yaradığı bilinmeli, çünkü hata ayıklama ancak kodu anlayarak yapılabilir.
- Python ile JavaScript'in temel yapıları (fonksiyon tanımlama, koşullu yapılar, print/console.log) birbirine oldukça benziyor.

## 18. Sonraki Gün İçin
- API çağrısının (fetch ile) Wix/Velo tarafında detaylı kurulumu.
- API'nin render edilmesi (deploy/canlıya alma) süreci.
