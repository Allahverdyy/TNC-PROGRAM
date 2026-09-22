# Gün 6: Modüller, HTTP Protokolü, API, JSON ile Haberleşme

## 1. Modül Kavramı

- Modül: belirli bir konu üzerinde çalışan fonksiyonların/değişkenlerin bir arada tutulduğu, entegre edilebilir dosya yapısı. Kütüphane de aynı mantığın paketlenmiş halidir.
- Modül kullanmanın amacı yine **DRY (Don't Repeat Yourself)** prensibi — aynı işlevi tekrar tekrar yazmak yerine bir modülde toplayıp her yerden çağırmak.

## 2. import — Kütüphane Entegrasyonu Yöntemleri

### Tüm Modülü İçe Aktarma
```python
import math
print(math.sqrt(4))    # 2.0
print(math.pi)          # 3.14159...
```

### Sadece Gerekeni İçe Aktarma (from ... import ...)
```python
from math import sqrt, factorial
print(sqrt(25))
print(factorial(5))
```
- Bu yöntem: gereksiz yere tüm kütüphaneyi hafızaya yüklememek, sadece ihtiyaç duyulan fonksiyonu almak için tercih edilir.

### Takma Ad (Alias) Verme
```python
import datetime as dt
simdi = dt.datetime.now()
```
- Uzun isimli modüller için kısaltma kullanmak kod okunabilirliğini artırır, kod kalabalığını azaltır.
- **Dikkat:** Takma ad verilen `datetime` ile içindeki `datetime` sınıfı (`dt.datetime`) farklı şeylerdir — karıştırılmamalı.

### `import *` — Tavsiye Edilmez
```python
from math import *   # TÜM isimleri doğrudan kullanılabilir yapar
```
- Hangi fonksiyonun hangi kütüphaneden geldiği belirsizleşir — kod okunabilirliğini ve netliğini azaltır, karmaşıklık yaratır. Tavsiye edilmiyor.

## 3. Kendi Modülünüzü Yazma

```python
# hesaplama.py
pi = 3.14159265

def topla(a, b):
    """a ve b değerinin toplam sonucunu verir."""
    return a + b

def carp(a, b):
    return a * b

def daire_alani(r):
    return pi * r * r
```

```python
# main.py
import hesaplama
print(hesaplama.topla(5, 3))
print(hesaplama.pi)
```
- **Docstring (fonksiyon açıklaması) önemli:** Her fonksiyon/sınıf, ne yaptığını açıklayan bir yorum satırıyla belgelenmelidir — hem sizin hem başkalarının kodu tekrar anlaması için kritik. Basit fonksiyonlarda gereksiz görünebilir ama karmaşık fonksiyonlarda hayati.

### Seçili İçe Aktarma (Kendi Modülünüzden)
```python
from hesaplama import topla, carp
toplam = topla(3, 5)
```

### F12 (Go to Definition) ile Modül İnceleme
- VS Code'da bir fonksiyon/modül üzerine gelip **F12** tuşuna basmak, o modülün kaynak koduna gider — hem kendi yazdığınız hem başka kütüphanelerin nasıl çalıştığını incelemek için kullanılır.

### if __name__ == "__main__": Bloğu
```python
if __name__ == "__main__":
    # test kodu buraya
    print(topla(2, 3))
```
- Bu blok, dosya DOĞRUDAN çalıştırıldığında çalışır; başka bir dosyaya `import` edildiğinde ÇALIŞMAZ.
- Amaç: bir modülü test etmek için yazılan kodların, o modül başka bir yerde import edildiğinde istenmeden tekrar çalışmasını önlemek.

## 4. Üç Tür Modül

1. **Yerleşik (built-in):** Python'ın kendi içinde gelen (`math`, `datetime`, `random`, `os` vb.).
2. **3. parti (third-party):** Dışarıdan indirilen kütüphaneler (`numpy`, `pandas`, `flask`, `django` vb.) — literatür taraması/araştırma ile bulunur, `pip install` ile yüklenir.
3. **Kendi yazdığınız:** Projeye özel, kendi tasarladığınız modüller.

## 5. random Modülü

```python
import random

zar = random.randint(1, 6)                        # 1-6 arası rastgele tam sayı
renk = random.choice(["kırmızı", "yeşil", "mavi"])  # listeden rastgele seçim
random.shuffle(liste)                              # listeyi karıştırır
cekilis = random.sample(range(1, 50), 6)           # aralıktan rastgele N eleman (piyango)
```

### ÖNEMLİ KAVRAM: Gerçek Rastgelelik Yoktur
- **Bilgisayar sistemleri hiçbir zaman gerçek anlamda "rastgele" değer üretmez** — üretilen her değer, arkada belirli bir algoritma/denkleme (sözde-rastgelelik / pseudo-random) dayanır.
- Yeterince uzun süre çalıştırıldığında (1000, 10.000 kez fark etmez), bir örüntü/tekrar ortaya çıkar. Bu, sistemin doğasında olan bir gerçektir, hata değil.

## 6. datetime Modülü — Pratik Kullanım

```python
from datetime import datetime, timedelta

simdi = datetime.now()
print(simdi.year, simdi.month, simdi.day)

yedi_gun_sonra = simdi + timedelta(days=7)
```

### Biçim Kodları (Format)
| Kod | Anlamı |
|---|---|
| `%Y` | 4 haneli yıl |
| `%y` | 2 haneli yıl |
| `%m`, `%d` | ay, gün |
| `%H`, `%M`, `%S` | saat, dakika, saniye |
| `%A`, `%B` | gün adı, ay adı |
| `%p` | AM/PM |

### Neden Önemli — Log Kayıtları
- Zaman damgası (timestamp), özellikle **log/hata kayıtlarında** kritik önem taşır — bir hatanın NE ZAMAN oluştuğunu bilmeden, o hatanın SEBEBİNİ diğer olaylarla ilişkilendirmek mümkün olmayabilir.
- Özellikle mekanik/robotik sistemlerde (gerçek zamanlı hareket kontrolü) zaman senkronizasyonu hatalıysa, hatanın kaynağını doğru tespit etmek çok zorlaşır.

### Doğum Tarihinden Yaş Hesaplama Örneği
```python
from datetime import datetime

dogum = datetime(2000, 5, 15)
bugun = datetime.now()
fark = bugun - dogum
yas = fark.days // 365
```

## 6b. Ekranda Gösterilen Resmî Slaytlar — Tam Kod (Modüller)

**import Kullanım Şekilleri**
```python
# 1) Tüm modülü içe aktar
import math
print(math.sqrt(16))   # 4.0
print(math.pi)          # 3.14159...

# 2) Sadece belirli şeyleri al
from math import sqrt, pi
print(sqrt(25))          # 5.0 (math. yazmadan)
print(pi)                # 3.14159...

# 3) Takma ad (alias) vermek
import datetime as dt
print(dt.datetime.now())

# 4) Her şeyi al (önerilmez - karışıklık)
from math import *
print(factorial(5))      # 120
```

**math Modülü: Matematiksel İşlemler**
```python
import math

# Karekök
print(math.sqrt(81))          # 9.0

# Üs alma (2 üzeri 10)
print(math.pow(2, 10))        # 1024.0

# Yukarı yuvarlama (tavan)
print(math.ceil(4.1))         # 5

# Aşağı yuvarlama (taban)
print(math.floor(4.9))        # 4

# Mutlak değer ve faktöriyel
print(math.factorial(5))      # 120

# Sabitler
print(math.pi)                # 3.141592...

# Daire alanı hesabı (pi * r^2)
r = 5
alan = math.pi * math.pow(r, 2)
print(f"Alan: {round(alan, 2)}")   # 78.54
```

**datetime Modülü: Tarih ve Saat**
```python
from datetime import datetime, timedelta

# Şu anki tarih ve saat
simdi = datetime.now()
print(simdi)                  # 2025-06-21 14:30:00

# Sadece parçalara ulaşmak
print(simdi.year)             # 2025
print(simdi.day)              # 21

# Tarihi formatlamak (strftime)
print(simdi.strftime("%d/%m/%Y"))   # 21/06/2025
print(simdi.strftime("%H:%M"))      # 14:30

# 7 gün sonrasını hesaplamak
gelecek = simdi + timedelta(days=7)
print("1 hafta sonra:", gelecek.date())
```

**strftime() Biçim Kodları — Tam Tablo**

| Kod | Anlamı |
|---|---|
| `%Y` / `%y` | 4 haneli yıl (2025) / 2 haneli yıl (25) |
| `%m` / `%d` | Ay (01-12) / Gün (01-31) |
| `%H` / `%M` / `%S` | Saat (00-23) / Dakika / Saniye |
| `%A` / `%B` | Haftanın günü adı (Monday) / Ay adı (June) |
| `%p` | AM/PM göstergesi |

**Kendi Modülümüzü Yazmak**
```python
# hesaplama.py (Modül)
PI = 3.14159

def topla(a, b):
    return a + b

def carp(a, b):
    return a * b

def daire_alani(r):
    return PI * r * r
```
```python
# main.py (Kullanan Program)
# Kendi modülümüzü import ediyoruz
import hesaplama

# İçindeki fonksiyonları çağır
s = hesaplama.topla(5, 3)
print(s)                       # 8

c = hesaplama.carp(4, 6)
print(c)                       # 24

a = hesaplama.daire_alani(5)
print(a)                       # 78.53975
```
- İki dosya da aynı klasörde olmalıdır. Dosya adı (.py uzantısı hariç) modül adı olur.

## 7. HTTP Protokolü

### Tanım
- HTTP (HyperText Transfer Protocol): iki sistemin (istemci ve sunucu) veri alışverişi yapabilmesi için kullandığı kurallar bütünü (protokol).
- Her haberleşme türünün (USB, Wi-Fi, Bluetooth vb.) kendine özgü protokolü vardır — HTTP web/API haberleşmesi için kullanılan protokoldür.

### İstemci (Client) — Sunucu (Server) İlişkisi
- **İstemci:** İsteği (request) BAŞLATAN taraf (tarayıcı, mobil uygulama).
- **Sunucu:** İsteği ALAN ve yanıt (response) döndüren taraf (veritabanı, API).
- İki API de birbiriyle haberleşebilir — sadece bir tarafın "veritabanı/sunucu" olması gerekmez; kim isteği başlatıyorsa o istemci, kim yanıtlıyorsa o sunucudur.

### HTTPS
- HTTP'nin daha güvenli, şifrelenmiş versiyonu. Günümüzde HTTP siteler yerine mutlaka HTTPS kullanılması öneriliyor.

## 8. HTTP Metotları

| Metot | Amacı |
|---|---|
| **GET** | Sunucudan veri OKUMAK/çekmek için |
| **POST** | Sunucuya YENİ veri GÖNDERMEK/oluşturmak için |
| **PUT / PATCH** | Var olan veriyi GÜNCELLEMEK için |
| **DELETE** | Sunucudan veri SİLMEK için (dikkatli kullanılmalı!) |

### DELETE Uyarısı — Veri Yedekleme
- **Kritik kural:** Veri silme işlemleri (DELETE, UPDATE) yapmadan önce mutlaka veri yedeklemesi olmalı — "veri bankadaki paradır" benzetmesi: tek bir yerde tutmak riskli, farklı noktalarda yedeklenmeli.
- Data center'lar bu güvenlik/yedekleme hizmetini bir ücret karşılığında sağlar; büyük şirketler genelde bu tür altyapılarla çalışır.

## 9. HTTP Durum Kodları (Status Codes)

| Kod Aralığı | Anlamı |
|---|---|
| 2xx | Başarılı (örn. 200 OK) |
| 4xx | İstemci hatası (örn. 401 Yetkisiz, 404 Bulunamadı) |
| 5xx | Sunucu hatası |

- **404:** Sunucu/kaynak bulunamadı — sık karşılaşılan hata, genelde yanlış URL veya kaynağın mevcut olmaması.
- **401:** Yetkisiz giriş — sunucuya erişim izniniz yok, kimlik doğrulama/token gerekiyor.
- Bu kodları okuyup anlamak, haberleşme hatalarını hızlıca teşhis etmek için kritik.

## 10. API (Application Programming Interface)

- Tanım: Yazılan tüm kodun (fonksiyonlar, kütüphaneler, haberleşme kodları) paketlenmiş, yayınlanmış, dışarıyla haberleşilebilir hale getirilmiş nihai halidir.
- URL'in bileşenleri size çok şey anlatır: protokol (https), domain (alan adı — benzersizdir), path/yol (hangi kaynağa erişiliyor), query (sorgu parametreleri).

## 11. requests Kütüphanesi ile HTTP İsteği Gönderme

### Basit GET İsteği
```python
import requests

url = "https://api.github.com"
cevap = requests.get(url)

print(cevap.status_code)   # 200, 404 vb.
print(cevap.text)           # ham metin içeriği
print(cevap.headers)        # başlık bilgileri
```

### Hata Yönetimi ile (try/except Kullanımı — ZORUNLU)
```python
try:
    cevap = requests.get(url)
    if cevap.status_code == 200:
        print("Veri başarıyla alındı")
    else:
        print("Hata:", cevap.status_code)
except Exception as hata:
    print("Bağlantı hatası:", hata)
```
- **Kritik kural:** Haberleşme kodu her zaman `try/except` içine alınmalı — aksi halde bağlantı hatası (internet kesintisi, yanlış URL, sunucu çökmesi) programın tamamen çökmesine (crash) yol açar.

## 12. JSON — Veri Formatı

### Temel Özellik
- JSON, Python'daki **dictionary** yapısına çok benzer (key-value) ama **JSON'daki TÜM değerler STRING'tir.**
- Bir JSON'dan sayı gibi görünen bir değer çekildiğinde (örn. yaş: 25), Python tarafında bu değer STRING olarak gelir — sayısal işlem yapmadan önce mutlaka `int()`/`float()` ile dönüştürülmelidir.

### API'den JSON Verisi Çekme
```python
import requests

url = "https://jsonplaceholder.typicode.com/users/1"
cevap = requests.get(url)
veri = cevap.json()   # JSON'ı Python dictionary'sine çevirir

print(veri["name"])
print(veri["username"])
print(veri["email"])
print(veri["address"]["city"])          # iç içe (nested) veri
print(veri["address"]["geo"]["lat"])    # 3 seviye iç içe
```

### Güvenli Erişim — .get() Kullanımı (Tekrar Önemli)
```python
telefon = veri.get("phone")   # key yoksa None döner, program çökmez
```
- Olmayan bir key'e doğrudan `veri["telefon"]` gibi erişilirse KeyError hatası alınır ve program çöker.
- `.get()` kullanımı bu riski ortadan kaldırır — bulunamayan alan `None` döner, program çalışmaya devam eder.

### Liste Halinde Gelen API Verisini İşleme
```python
url = "https://jsonplaceholder.typicode.com/users"
cevap = requests.get(url)

if cevap.status_code == 200:
    kullanicilar = cevap.json()   # bir LİSTE (dictionary'lerden oluşan)
    for kisi in kullanicilar:
        ad = kisi["name"]
        sehir = kisi["address"]["city"]
        print(ad, sehir)
else:
    print("Veri alınamadı, kod:", cevap.status_code)
```
- API'den gelen JSON, köşeli parantez `[ ]` ile başlıyorsa bu bir LİSTE'dir — for döngüsüyle içindeki her elemana (dictionary) tek tek erişilir.

## 13. Genel Tavsiyeler — Haberleşme Kodları İçin

- Haberleşme (network) programlama her zaman en zor/hataya açık alanlardan biridir — "mükemmel bir haberleşme yapmak neredeyse imkansız", her zaman bir yerde bir hata/gecikme/kopma olasılığı vardır. Bu normal karşılanmalı, cesaret kırılmamalı.
- Her HTTP isteği mutlaka: (1) `try/except` ile korunmalı, (2) status code kontrol edilmeli, (3) JSON'dan çekilen veriler için `.get()` kullanılmalı, (4) gerekli tip dönüşümleri (string→int/float) yapılmalı.

## 14. Sonraki Gün İçin
- POST isteği (veri gönderme) bu derste zaman kısıtından işlenemedi, ertelendi.
- Konular ağır bulundu, tekrar izleme öneriliyor — katılımcı geri bildirimiyle doğrulandı ("bilgisayar programcılığı mezunu için bile ağır" yorumu alındı).
