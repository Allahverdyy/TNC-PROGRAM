# Gün 7: POST İsteği, LLM (Grok/OpenAI/Gemini) Entegrasyonu, Chatbot Döngüsü, Proje Mimarisi

## 1. POST İsteği ile Sunucuya Veri Gönderme

```python
import requests

url = "https://jsonplaceholder.typicode.com/posts"
yeni_veri = {
    "title": "Python öğreniyorum",
    "body": "Model o kadar da harika değil",
    "userId": 1
}

cevap = requests.post(url, json=yeni_veri)
print(cevap.status_code)   # 201 = başarıyla oluşturuldu

sonuc = cevap.json()
print(sonuc["id"])
```
- GET'te sadece veri çekilir; POST'ta önce gönderilecek veri bir **dictionary** olarak hazırlanır, sonra `requests.post(url, json=veri)` ile gönderilir.
- Başarılı POST isteği genelde **201** (Created) durum kodu döndürür.

## 2. CORS Mantığı (Kısa Değinme)

- Bazı API'ler/domainler dışarıdan gelen isteklere varsayılan olarak kapalıdır — haberleşmenin çalışması için karşı tarafın izin vermesi (CORS ayarı) gerekir.
- Özellikle Wix gibi platformlarla haberleşirken bu kısıtlamalarla karşılaşılabilir — hangi kaynaklardan (origin) gelen isteklere izin verileceği CORS mantığıyla yönetilir.

## 3. API Key ile Parametreli İstek

- Bazı API'ler (özellikle yapay zeka modelleri) her istekte bir **API anahtarı (key)** talep eder — bu anahtar, isteğin kimden geldiğini doğrular ve ücretlendirme/yetkilendirme için kullanılır.
- Anahtar genelde `params` veya header içinde gönderilir.

## 4. "Kodculuk mu Ölüyor?" — Sektör Değerlendirmesi

- Yeni nesil AI modelleri (bahsedilen dönemde yeni çıkan bir GPT modeli) kısa/orta ölçekli görevlerde artık %90-99 doğrulukla kod üretebiliyor.
- Eğitmenin görüşü: **"Koderlik ölüyor olabilir ama yazılımcılık ölmüyor."** Fark:
  - Kod YAZMAK artık büyük ölçüde AI'ın işi.
  - Kodu OKUYABİLMEK, hatayı bulup doğru/verimli şekilde (az token ile) düzelttirebilmek, mimariyi doğru kurabilmek hâlâ insan mühendisin işi.
- AI'a "bir sistem oluştur" dendiğinde otomatik olarak eksiksiz bir hata yönetimi listesi oluşturmayacaktır — bunu mühendisin talep etmesi/tanımlaması gerekir.
- Sektörün yöneldiği yön: iyi kod yazmak değil, **iyi sistem/mimari tasarlamak ve doğru hata yönetimi kurmak.**

## 5. Grok API Key Alma (Pratik Adımlar)

1. `console.groq.com` (Grok Cloud) adresine Google/GitHub hesabıyla giriş yapılır.
2. **"Create API Key"** ile yeni bir anahtar oluşturulur, bir isim verilir (workspace adı gibi).
3. Oluşturulan key **HEMEN kopyalanıp güvenli bir yere kaydedilmelidir** — pencere kapatıldıktan sonra bir daha görüntülenemez, sadece silinip yeniden oluşturulabilir.
- OpenAI ve Gemini'de de aynı mantık: "Create New Key" → hemen kopyala → kaydet.
- Grok tercih edilme nedeni: ücretsiz kotası OpenAI/Gemini'ye göre daha geniş — test/öğrenme aşaması için daha kullanışlı.

## 6. .env Dosyası ile API Key Saklama

### .env Dosyası Oluşturma
- Not Defteri'nde dosya oluşturulup uzantısı `.env` olarak değiştirilir (isim vermeden).
- İçine: `GROQ_API_KEY=xxxxxxxxxxxx` şeklinde yazılır.

### python-dotenv Kütüphanesi ile Okuma
```bash
pip install python-dotenv
```

```python
from dotenv import load_dotenv
import os

load_dotenv()   # .env dosyasını yükler
api_key = os.getenv("GROQ_API_KEY")
print(api_key)
```
- **Kritik:** `.env` dosyası düzenlendikten sonra mutlaka **Ctrl+S ile kaydedilmelidir** — kaydedilmezse `load_dotenv()` boş/None değer döndürür.
- **Neden .env kullanılır:** API key'ler kod içine doğrudan yazılıp GitHub'a commit edilirse, üçüncü şahıslar tarafından görülür ve kötüye kullanılabilir. `.env` dosyası `.gitignore`'a eklenerek asla commit edilmez — sadece key'in İSMİ kod içinde geçer, değeri asla.

## 7. Grok/LLM API'sine İlk İstek

### Kurulum
```bash
pip install groq
```

### Basit Soru-Cevap
```python
from groq import Groq
from dotenv import load_dotenv
import os

load_dotenv()
api_key = os.getenv("GROQ_API_KEY")

client = Groq(api_key=api_key)

cevap = client.chat.completions.create(
    model="llama-3.3-70b-versatile",   # dokümantasyondan alınan model adı
    messages=[
        {"role": "user", "content": "Merhaba nasılsın?"}
    ]
)

mesaj = cevap.choices[0].message.content
print(mesaj)
```
- **API key'i doğrudan kod içine yazmak (test amaçlı bile olsa) TAVSİYE EDİLMEZ** — commit edildiğinde üçüncü şahıslar görebilir. Her zaman `.env` üzerinden çekilmeli.

## 8. Roller (Roles) — Rol Yönetimi

| Rol | Anlamı |
|---|---|
| `system` | Modele KİŞİLİK/TALİMAT verir — "sen şu şekilde davranmalısın" |
| `user` | Kullanıcının gönderdiği mesaj/soru |
| `assistant` | Modelin önceki cevaplarını hatırlatmak/geçmiş sohbeti yönetmek için kullanılır |

### Modele Kişilik Verme Örneği
```python
messages = [
    {"role": "system", "content": "Sen bir Python eğitmenisin. Cevapların kısa, net ve örnekli olsun."},
    {"role": "user", "content": "Liste nedir?"}
]
```
- `system` mesajı, modelin "kim olduğunu" ve nasıl cevap vereceğini tanımlar — bu, bir chatbot'a **iş bağlamı (business context)** verme yöntemidir; siteye gömülecek bir chatbot'a marka/hizmet kişiliği bu şekilde atanır.

## 9. Token ve Parametre Yönetimi

```python
cevap = client.chat.completions.create(
    model="llama-3.3-70b-versatile",
    messages=[...],
    temperature=0.2,      # tutarlılık/yaratıcılık oranı (0=tutarlı, 1=yaratıcı)
    max_tokens=150         # maksimum yanıt uzunluğu (token cinsinden)
)
```
- `temperature`: Düşük değer (örn. 0.2) daha tutarlı/öngörülebilir cevaplar; yüksek değer daha "yaratıcı"/rastgele cevaplar verir.
- `max_tokens`: Yanıtın maksimum uzunluğunu (dolayısıyla maliyetini) sınırlar.

### Token Kullanımını Görüntüleme
```python
kullanim = cevap.usage
print(kullanim.prompt_tokens)       # gönderilen (soru) token sayısı
print(kullanim.completion_tokens)   # alınan (cevap) token sayısı
print(kullanim.total_tokens)        # toplam
```

## 10. Hata Yönetimi (try/except) — LLM API'sinde

```python
try:
    cevap = client.chat.completions.create(
        model="llama-3.3-70b-versatile",
        messages=messages
    )
except Exception as hata:
    print("API isteği başarısız oldu:", hata)
```
- **Kritik prensip:** Hata mesajının BİLGİLENDİRİCİ olması gerekiyor — "hata oluştu" gibi genel bir mesaj yerine, hangi sayfada/hangi try bloğunda hatanın oluştuğunu belirten kodlanmış bir hata takip sistemi (örn. blok numaralandırma) kurulması öneriliyor — büyük projelerde hatanın kaynağını hızlı tespit için önemli.
- AI (yapay zeka) sizin için otomatik olarak eksiksiz bir hata tablosu oluşturmaz — bu mimariyi geliştiricinin tanımlaması gerekir.

## 11. Model Karşılaştırması (Eğitmen Görüşü, Dönemsel)

- Kod yazımında (bahsedilen dönemde) Claude ve yeni GPT modelleri öne çıkıyor; GPT'nin son modelinin kendi gereksinimlerini belirleyebilme, hata yönetimi yapabilme konusunda daha ileri gittiği belirtildi.
- Gemini'nin bu alanda (dönemsel olarak) biraz geride kaldığı değerlendirmesi yapıldı — bu tamamen dönemsel bir gözlem, sürekli değişebilir.

## 12. Prompt Mühendisliği — Temel Kurallar

1. **Net ve spesifik olun** — belirsiz/açık uçlu talimatlar, modelin sizden bağımsız, istenmeyen kararlar almasına yol açar.
2. **Parça parça (adım adım) isteyin** — büyük, karmaşık bir yapıyı tek seferde istemek hem çok token harcar hem hata riskini artırır (güvenlik açıkları dahil). Büyük projeler küçük parçalara bölünerek geliştirilmeli.
3. **Bağlam (context) verin** — modele bir rol/bağlam vererek cevabın kalitesini artırın (genel cevap yerine, o role özgü cevap).
4. **Örnek gösterin.**

## 13. Model Seçimi — Maliyet-Fayda Dengesi

- Test/geliştirme aşamasında **en ucuz/yeterli model** tercih edilmeli — henüz production'a geçmemiş bir projede pahalı/yüksek seviyeli model kullanmanın anlamı yok.
- Ürünleşme aşamasında (gerçek kullanıma geçince) daha güçlü/ücretli modellere (örn. Grok'tan OpenAI'a) geçiş düşünülebilir — cevap kalitesi modelin gücüne göre değişir.
- Gereksiz yüksek maliyetli model seçmek, basit bir chatbot görevini yerine getirmek için mantıksız bir harcamadır.

## 14. Chatbot Döngüsü (while ile Sürekli Sohbet)

```python
from groq import Groq
from dotenv import load_dotenv
import os

load_dotenv()
client = Groq(api_key=os.getenv("GROQ_API_KEY"))

print("Chatbot'a hoş geldiniz. Çıkmak için 'q' yazın.\n")

while True:
    soru = input("Siz: ").lower()

    if soru in ["q", "çık", "exit"]:
        print("Görüşmek üzere")
        break

    cevap = client.chat.completions.create(
        model="llama-3.3-70b-versatile",
        messages=[{"role": "user", "content": soru}]
    )

    mesaj = cevap.choices[0].message.content
    print("Bot:", mesaj)
```
- `.lower()` kullanımı — kullanıcı "Q", "q", "EXIT" gibi büyük/küçük harf karışık yazsa bile kontrol edilebilmesi için.
- `client` nesnesinin `while` döngüsünün DIŞINDA bir kez oluşturulması yeterli — her döngü adımında yeniden oluşturmak gereksiz kaynak israfı.

### Bilinen Sınırlama: Hafızasızlık
- Bu basit chatbot yapısı **hiçbir şeyi hatırlamaz** — her yeni soru bağımsız bir istek olarak gönderilir, önceki konuşma geçmişi model tarafından bilinmez.
- Gerçek "hafızalı" bir sohbet için: tüm konuşma geçmişi bir **liste** içinde tutulmalı ve her istekte bu liste tekrar gönderilmelidir.

```python
gecmis = [{"role": "system", "content": "Sen yardımsever bir asistansın."}]

while True:
    soru = input("Siz: ")
    if soru.lower() in ["q", "exit"]:
        break
    gecmis.append({"role": "user", "content": soru})

    cevap = client.chat.completions.create(
        model="llama-3.3-70b-versatile",
        messages=gecmis
    )
    yanit = cevap.choices[0].message.content
    print("Bot:", yanit)
    gecmis.append({"role": "assistant", "content": yanit})
```
- **Uyarı:** Her seferinde TÜM geçmişi tekrar göndermek çok fazla token tüketir — ücretsiz kotalarla bu sürdürülemez. Pratik çözüm: sadece kritik/özet bilgileri tutmak, gereksiz detayları biriktirmemek; gerçek üretimde geçmiş konuşmalar veritabanında/cloud'da saklanıp gerektiğinde özetlenerek modele verilmelidir.

## 15. Streaming (Akan Yanıt) Yapısı

```python
akis = client.chat.completions.create(
    model="llama-3.3-70b-versatile",
    messages=messages,
    stream=True
)

for parca in akis:
    icerik = parca.choices[0].delta.content
    if icerik:
        print(icerik, end="")
```
- ChatGPT/Gemini arayüzlerinde gördüğümüz "yazı yazılıyormuş gibi" akan cevap efekti bu yapıyla elde edilir — yanıt parça parça (chunk chunk) geldikçe ekrana basılır.
- Bu da ezberlenecek bir yapı değil — gerektiğinde dokümantasyondan/AI'dan bulunup entegre edilecek bir kalıp.

## 16. Maliyet ve Token Yönetimi — Genel Tavsiye

- Chatbot'ta token/maliyet yönetimini doğru yapmak kritik — ücretsiz kotalar (günlük/saatlik mesaj sınırı gibi) hızla tükenebilir.
- Gereksiz yüksek token harcayan yapılar (örn. her seferde tüm geçmişi gönderme) modelin/API'ın kotasını erken tüketir.
- Model seçiminde "yeterli olan en ucuz" prensibi maliyet analizinde kritik.

## 17. Proje Mimarisi — Klasör Yapısı Tavsiyesi (Öğrenci Sorusu Üzerine)

**Soru:** Her yeni kod parçası için yeni bir `.py` dosyası mı açmalıyız?

**Cevap:**
- Evet ama **rastgele değil, GÖREVE göre** — her Python dosyası tek bir işleve/konuya hizmet etmeli (modülerlik prensibi, DRY ile bağlantılı).
- Örnek klasör yapısı:
```
proje/
├── app/
│   ├── database.py       # veritabanı işlemleri
│   ├── routes.py         # rota/endpoint tanımları
│   ├── services/
│   │   └── ai_service.py # yapay zeka haberleşme kodları
│   └── main.py           # başlatma dosyası
```
- Türkçe klasör/dosya isimleri kullanılabilir ama İngilizce isimlendirme daha sağlıklı çalışır (uyumluluk, karakter sorunları).
- **Kural:** Haberleşme kodu, test kodu, veritabanı kodu — hepsi AYNI dosyada olmamalı. Her biri kendi görevine özel dosyada tutulmalı.

## 18. Belgrad Öncesi Yapılması Gerekenler (Soru-Cevap)

**Sorular:** Database kısmı ne kadar ilerletilmeli? Belgrad'a kadar ne bitmeli?

**Cevap:**
- Belgrad'a gelmeden önce:
  1. **Proje mimarisi** (klasör yapısı) net şekilde oluşturulmuş olmalı.
  2. **GitHub'a kod commit edilmiş** olmalı.
  3. Haberleşmenin (API, chatbot) **çalıştığı test edilmiş** olmalı.
- Wix tarafına bağlama veya tüm chat kodlarını tam bitirme zorunluluğu YOK — bunlar Belgrad'da ekiple birlikte tamamlanabilir.
- Beklenen genel akış: Lead (potansiyel müşteri) kaydı → İki sayfa: (1) Chatbot sayfası, (2) Dashboard sayfası. Chatbot'tan alınan isim/soyisim/email gibi veriler Dashboard'a (veritabanına) yönlendirilir.
- Veritabanı tarafı için elle tablo oluşturmaya gerek yok — hazır kütüphaneler/ORM'lerle (örn. SQLite ile) bu iş kolayca halledilebilir.

## 19. Sonraki Gün İçin
- Web/premium tarafıyla entegrasyon (chatbot'un web sitesine/Wix'e nasıl bağlanacağı) işlenecek.
