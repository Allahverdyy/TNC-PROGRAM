# Gün 4: Fonksiyonlar, Lambda, Global/Lokal Değişkenler, Hata Yakalama (try/except)

## 1. Fonksiyon Kavramı — Neden Gerekli

- Bugüne kadar yazılan kodlar birbirinden bağımsız, tek seferlik çalışan parçalardı. Bir kod bloğunu tekrar tekrar farklı yerlerde kullanmak/çağırmak gerektiğinde **fonksiyon** devreye girer.
- Fonksiyon, matematikteki fonksiyon mantığıyla aynı: bir "paket" işlem, girdiye göre çıktı üreten yeniden kullanılabilir bir yapı.

### DRY Prensibi (Don't Repeat Yourself)
- Yazılımın en temel kurallarından biri: **aynı işlemi farklı yerlerde kopyala-yapıştır ile tekrar tekrar yazmayın.**
- Aynı mantığı taşıyan kod birden fazla yerde tekrarlanırsa, bir hatayı düzeltmek gerektiğinde sadece bulduğunuz kopyayı düzeltirsiniz — diğer kopyalar hatalı kalmaya devam eder.
- Sonuç: yönetilemez kod, "spagetti kod", kısalan yazılım ömrü, mimari yeniden yazma zorunluluğu.
- Çözüm: tekrar eden mantığı bir fonksiyona isim verip paketleyin, her yerde o fonksiyonu çağırın.

## 2. Fonksiyon Tanımlama (def)

```python
def merhaba():
    print("Merhaba")
    print("Sisteme hoş geldiniz")

merhaba()   # fonksiyonu çağırma — istenildiği kadar tekrar çağrılabilir
```
- Python'da fonksiyon gövdesi **girinti (indentation)** ile belirlenir — süslü parantez yok, tab/boşluk seviyesi hangi kodun fonksiyona ait olduğunu gösterir.

## 3. Parametre Alma

```python
def selamla(isim):
    print("Merhaba", isim)

selamla("Ahmet")   # Merhaba Ahmet
selamla("Ayşe")    # Merhaba Ayşe
```

### Çoklu Parametre
```python
def topla(sayi1, sayi2):
    toplam = sayi1 + sayi2
    print(toplam)

topla(10, 20)   # 30
```

## 4. return — Değeri Fonksiyon Dışına Çıkarma

- `print()` sadece terminale yazar — değeri fonksiyonun DIŞINDA kullanamazsınız.
- `return` ile fonksiyonun ürettiği değer dışarı aktarılır, başka bir değişkene atanabilir, başka fonksiyonlarda kullanılabilir.

```python
def kare_al(sayi):
    return sayi ** 2

sonuc = kare_al(5)
print(sonuc)   # 25
```

## 5. Default (Varsayılan) Parametre Değerleri

```python
def hos_geldin(isim="ziyaretçi"):
    print("Hoş geldin", isim)

hos_geldin("Ahmet")   # Hoş geldin Ahmet
hos_geldin()           # Hoş geldin ziyaretçi
```
- Bir parametrenin gelmeme ihtimali varsa, default değer atayarak fonksiyonun hata vermeden (None/null kontrolüne gerek kalmadan) çalışmasını sağlar.

## 6. Birden Fazla Değer Döndürme (return)

```python
def istatistik_hesapla(sayilar):
    toplam = sum(sayilar)
    ortalama = toplam / len(sayilar)
    maksimum = max(sayilar)
    minimum = min(sayilar)
    return toplam, ortalama, maksimum, minimum

t, o, mx, mn = istatistik_hesapla([10, 20, 30, 40])
```
- Python, virgülle ayrılmış birden fazla değeri tek `return` ile döndürebilir (arka planda tuple olarak döner).
- **Uyarı:** Çok fazla değer döndüren uzun/karmaşık fonksiyonlar hata ayıklamayı zorlaştırır. Tavsiye: fonksiyonu parça parça, ayrı fonksiyonlara bölmek — büyük bir fonksiyonda hatayı bulmak, küçük parçalanmış fonksiyonlarda hatayı bulmaktan çok daha zordur.

## 7. Esnek Argümanlar — *args ve **kwargs

### *args — Belirsiz Sayıda Pozisyonel Argüman
```python
def coklu_toplam(*sayilar):
    return sum(sayilar)

coklu_toplam(10, 20, 30)      # sayilar bir TUPLE olarak toplanır
coklu_toplam(5, 10, 15, 20)   # kaç değer gönderilirse gönderilsin çalışır
```
- `*sayilar` fonksiyona kaç argüman gönderileceği belli olmadığında kullanılır — argümanlar fonksiyon içinde **tuple** olarak toplanır.

### **kwargs — Belirsiz Sayıda İsimli (Keyword) Argüman
```python
def kullanici_bilgisi(**bilgiler):
    return bilgiler

kullanici_bilgisi(ad="Ahmet", yas=25, sehir="İstanbul")
# {"ad": "Ahmet", "yas": 25, "sehir": "İstanbul"} — DICTIONARY olarak döner
```
- `**bilgiler` ile gönderilen `isim=deger` çiftleri fonksiyon içinde **dictionary** olarak toplanır.
- Kural: `*args` → tuple sonucu, `**kwargs` → dictionary sonucu.

## 8. Tip Belirtme (Type Hinting) — Opsiyonel

```python
def kullanici_kaydi(isim: str, soyisim: str, yas: int):
    return f"{isim} {soyisim}, {yas}"
```
- Python'da zorunlu değil (dinamik tipli dil) ama gelen parametrenin hangi tipte olması gerektiğini belgelemek/okunabilirliği artırmak için kullanılabilir.
- .NET, Java, C++ gibi dillerde tip belirtme zorunlu; Python'da bu daha çok isteğe bağlı bir dokümantasyon aracı olarak kullanılıyor, çok yaygın bir kullanım değil.

## 9. Lambda (Anonim Fonksiyonlar)

- Kısa, tek satırlık, isimlendirilmemiş fonksiyonlar için kullanılır.

```python
kare_al = lambda x: x ** 2
print(kare_al(5))   # 25

toplam = lambda x, y: x + y
print(toplam(10, 20))   # 30
```
- Amaç: kısa fonksiyonları uzun `def` bloğu yazmadan tek satırda tanımlamak — kodun daha derli toplu, okunabilir olmasını sağlar.
- Özellikle küçük yardımcı kütüphane fonksiyonları (matematik işlemleri gibi) için pratik.
- **Not:** Kod yazım standardı önemli — kurumsal şirketlerde genelde bir "kod yazım dokümanı" olur, ekip bu standarda uymak zorundadır; standartlara uymayan kod hem okunmaz hem hata ayıklamada sorun çıkarır.

## 10. map() ve filter() — Fonksiyonel Programlama Araçları

```python
sayilar = [1, 2, 3, 4, 5]

kareler = list(map(lambda x: x ** 2, sayilar))
# [1, 4, 9, 16, 25]

ciftler = list(filter(lambda x: x % 2 == 0, sayilar))
# çift olanları filtreler
```
- `map()`: listedeki her elemana bir fonksiyon uygular, tek satırda for döngüsünün yaptığını yapar.
- `filter()`: listeden belirli koşulu sağlayan elemanları seçer.
- Python'ın gömülü (built-in) kütüphane fonksiyonları olduğu için genelde manuel for döngüsünden daha hızlı çalışır ve kod satırını kısaltır.

## 11. Global ve Lokal Değişkenler — KRİTİK KONU

### Temel Fark
```python
mesaj = "Merhaba"   # GLOBAL değişken

def fonksiyon():
    isim = "Ahmet"   # LOKAL değişken — sadece bu fonksiyonun içinde geçerli
    print(mesaj)      # global değişkene erişilebilir
```
- **Global** değişken: tüm fonksiyonlar içinden erişilebilir/kullanılabilir.
- **Lokal** değişken: sadece tanımlandığı fonksiyonun içinde var olur, dışarıdan erişilemez.

### Hafıza Yönetimi Uyarısı
- Bir Python dosyasını çalıştırmak, o dosyadaki fonksiyonları OTOMATİK çalıştırmaz — fonksiyon çağrılmadığı sürece içindeki kod çalışmaz.
- Ancak **globalde tanımlanan değişkenler dosya çalıştığı anda hafızada (RAM) yer tutar** — fonksiyon hiç çağrılmasa bile.
- Büyük projelerde, çok sayıda sınıf/dosya ayağa kalktığında, gereksiz global değişken tanımları hafızayı gereksiz yere şişirir — "stack overflow" gibi hatalara, sistemin yavaşlamasına yol açabilir.
- **Kural:** Gereksiz yere global değişken tanımlamayın; gerçekten birden fazla fonksiyon tarafından paylaşılması gereken veriler için global kullanın.

### Fonksiyon İçinde Global Değeri Değiştirme
```python
puan = 85   # global

def puan_artir():
    puan = 500   # bu sadece LOKAL bir değişken oluşturur, global'i DEĞİŞTİRMEZ!
    print(puan)  # 500 yazar ama global puan hâlâ 85

def puan_artir_dogru():
    global puan          # global anahtar kelimesi ile global'e erişim sağlanır
    puan = 500            # artık GERÇEKTEN global puan değişir
```
- `global` anahtar kelimesi kullanılmadan bir fonksiyon içinde aynı isimde değişken atanırsa, bu YENİ bir lokal değişken oluşturur — global değeri etkilemez (sessizce, hata vermeden!).
- **Uyarı:** Global bir değeri değiştirmeden önce, o değişkenin başka hangi fonksiyonlarda/nerede kullanıldığını bilmek gerekir — kontrolsüz değişiklik, diğer fonksiyonların sonuçlarını bozabilir, bu da testte veya production'da sessiz/bulunması zor hatalara yol açar.
- Sorumluluk uyarısı: bir global değişkeni değiştirdiğinizde, o değişikliğin yol açtığı her türlü hatadan (başka fonksiyonlardaki dahil) siz sorumlu olursunuz.

## 12. Hata Yakalama — try / except / else / finally

### Neden Önemli
- Yapay zekaya "hatayı ve tüm kodu yapıştırıp çözdürmek" doğru bir yöntem değil — özellikle web servis gibi bağımsız modüllerin birbirine bağlandığı sistemlerde, hata farklı bir modülde olabilir; AI'a topluca kod göndermek hem token israfı hem yanlış/gereksiz "düzeltmelerle" kodu daha da bozma riski taşır.
- Doğru yöntem: hatayı bulun, hangi fonksiyon/satırda olduğunu belirleyin, sadece o parçayı analiz ettirin.

### Temel Yapı
```python
try:
    yas = int(input("Yaşınızı girin: "))
    print("Yaşınız:", yas)
except:
    print("Geçersiz bir yaş girdiniz")
```
- `try` bloğunda hata oluşursa, program ÇÖKMEZ — `except` bloğuna atlar ve devam eder.
- `try` bloğu olmadan hata oluşsaydı, program o satırda tamamen dururdu (crash).

### Spesifik Hata Türlerini Yakalama
```python
try:
    sayi1 = int(input("1. sayı: "))
    sayi2 = int(input("2. sayı: "))
    sonuc = sayi1 / sayi2
except ValueError:
    print("Geçersiz bir sayı girdiniz")
except ZeroDivisionError:
    print("İkinci sayı 0 olamaz")
except Exception as hata:
    print("Beklenmedik bir hata oluştu:", hata)
```
- Farklı hata tiplerini ayrı ayrı yakalayarak, her biri için özel/anlamlı mesaj verilebilir.

### else ve finally
```python
try:
    hesap = 10 / 2
except ZeroDivisionError:
    print("Sıfıra bölme hatası")
else:
    print("Hata oluşmadı")   # try bloğu hatasız tamamlanırsa çalışır
finally:
    print("Dosya kapatılıyor")   # hata olsun olmasın HER ZAMAN çalışır
```
- `else`: try bloğu hatasız tamamlanırsa çalışır.
- `finally`: hata olsun olmasın, HER DURUMDA çalışır (kaynak kapatma, temizlik işlemleri için kullanılır).

### Kendi Hatanızı Fırlatma (raise)
```python
def kayit_yap(yas):
    if yas < 18:
        raise ValueError("18 yaşından küçük olamaz")
    return "Kayıt işlemi tamamlandı"

try:
    sonuc = kayit_yap(16)
    print(sonuc)
except ValueError as hata:
    print("Hata var:", hata)
```
- `raise`, sistemsel bir hata olmasa bile, kendi iş mantığınıza göre "bu durum hata sayılmalı" dediğiniz senaryolarda özel hata fırlatmanızı sağlar (örn. yaş kısıtlaması, iş kuralı ihlalleri).
- Bu sayede kodun neyi "hata" olarak kabul edeceğini kendiniz tanımlarsınız.

## 13. Debug (Hata Ayıklama) — VS Code Pratikleri

- **Breakpoint (kesme noktası):** Kod satırının solundaki boşluğa tıklanarak konur — F5 ile debug modda çalıştırıldığında program o satırda durur.
- **F11:** Kodu adım adım (satır satır) ilerletir — her adımda değişkenlerin durumu izlenebilir.
- **print() ile manuel debug:** Kodun hangi satıra kadar çalıştığını görmek için stratejik noktalara `print()` eklemek pratik bir yöntem — hangi print'in yazdırılıp hangisinin yazdırılmadığına bakarak hatanın nerede olduğu anlaşılabilir.
- **Önemli:** Debug amaçlı eklenen `print()` satırları, kod tamamlandıktan sonra MUTLAKA silinmeli — production kodunda kalmamalı.

## 14. Genel Prensip — Tekrar Vurgu

- Kod yazmak artık büyük ölçüde AI'ın işi haline geldi ama **kodu yönetmek, hatayı bulmak, tokenleri verimli kullanmak hâlâ yazılımcının sorumluluğu.**
- Global/lokal değişken yönetimi, hata yakalama gibi konular "kod çalışsın yeter" mantığıyla değil, **sürdürülebilir, okunabilir, ekip tarafından anlaşılabilir** kod yazma disipliniyle ele alınmalı.

## 15. Ödev / Pratik
- Bugün işlenen konuların (fonksiyon, lambda, global/lokal, try/except) ekran görüntülerini alıp kendi ortamında tekrar denemek istendi — zorunlu değil ama pekiştirme için önerildi.

## 16. Sonraki Gün İçin
- Bu derste değinilmeyen konular (nesne yönelimli programlama / class yapıları gibi) muhtemelen ileride işlenecek.
