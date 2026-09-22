# Gün 2: Operatörler, Koşullu Yapılar (if/elif/else), Döngüler (for/while)

## 1. Aritmetik Operatörler

| Operatör | İşlem | Örnek |
|---|---|---|
| `+` | Toplama | `5 + 3` |
| `-` | Çıkarma | `5 - 3` |
| `*` | Çarpma | `5 * 3` |
| `/` | Bölme (ondalıklı sonuç) | `10 / 3 → 3.33` |
| `//` | Tam bölme (ondalık kısmı atar, sadece tam sayı kısmı) | `10 // 3 → 3` |
| `%` | Mod (kalan bulma) | `10 % 3 → 1` |
| `**` | Üs alma | `x ** y` = x'in y. kuvveti |

### Kullanım Örneği — Para Üstü / Kaç Adet Hesabı
```python
sayi = 17
kalan = sayi % 3      # kalan bulma
yeni_sayi = sayi - kalan

adet = 137 // 20       # 137 içinde kaç tane 20 var
```
- `//` operatörü özellikle "kaç adet/kaç tane var" hesaplarında (örn. kaç adet 20'lik banknot) kullanılır.
- Bu operatörler oyun programlama, fizik motoru hesaplamaları, indeks/döngü kontrolü gibi alanlarda yoğun kullanılır.

### VS Code'da Kaydetmeden Çalıştırma Farkı
- Terminalden doğrudan Python derleyicisiyle (interaktif mod) çalıştırırken `Ctrl+S` ile kaydetmeye gerek yok — dinamik olarak anlık çalışır.
- `.py` dosyasını çalıştırırken ise mutlaka önce kaydetmek (`Ctrl+S`) gerekir, aksi halde eski hali çalışır.

## 2. Atama (Assignment) Operatörleri

```python
skor = 85
skor += 15    # skor = skor + 15 ile aynı, tek satırda
skor -= 10    # skor = skor - 10
```
- İki değişken kullanıp (`skor2 = skor + 15`, sonra `skor = skor2`) sonucu tekrar atamak yerine `+=` kullanmak: hafızada gereksiz değişken oluşturmayı önler, kod okunabilirliğini artırır.
- Özellikle for döngülerinde artan/azalan sayaç değerleri oluştururken sık kullanılır (`sayac += 1` gibi).

## 3. Karşılaştırma (Mantık) Operatörleri

| Operatör | Anlamı |
|---|---|
| `==` | Eşit mi |
| `!=` | Eşit değil mi |
| `>` | Büyük mü |
| `<` | Küçük mü |
| `>=` | Büyük eşit mi |
| `<=` | Küçük eşit mi |

- Sonuç her zaman `True`/`False` (boolean) döner.
- **Büyük/küçük harf farkı önemli:** `"a" == "A"` → `False` — çünkü hafızada farklı ikili (binary) değerlere sahiptirler.
- Basit şifre kontrolü örneği:
```python
gercek_sifre = "1234"
girilen = input("Şifreyi girin: ")
print(girilen == gercek_sifre)   # True/False
```
(Not: bu sadece öğretim amaçlı basit bir örnek — gerçek uygulamalarda şifreler token/hash gibi güvenli yöntemlerle saklanmalı, düz metin karşılaştırma kullanılmamalı.)

### Aralık Kontrolü
```python
yas = 24
print(18 <= yas <= 30)   # yaş 18-30 arasında mı
```

## 4. Mantıksal Operatörler (and / or / not)

```python
kullanici_adi = "admin"
sifre = "1234"

if kullanici_adi == "admin" and sifre == "1234":
    print("Giriş izni verildi")

puan = 40
vip_uye = True
print(puan > 50 or vip_uye)   # OR: ikisinden biri True ise True

print(not True)   # False — sonucu tersine çevirir
```
- `and`: her iki koşul da doğruysa `True`.
- `or`: koşullardan biri doğruysa `True`.
- `not`: sonucu tersine çevirir.

## 5. Koşullu Yapılar (if / elif / else)

### Temel Yapı
```python
sicaklik = 34
if sicaklik > 30:
    print("Hava çok sıcak")
else:
    print("Hava sıcak değil")
```
- **Girinti (indentation) kritik önemde** — Python'da hangi kod bloğunun hangi koşula ait olduğunu girinti belirler.

### Metin İçinde Arama (in)
```python
mesaj = "hava çok güzel bugün"
if "hava" in mesaj:
    print("Mesajda hava kelimesi geçiyor")
```

### Çift Sayı/Tek Sayı Kontrolü
```python
sayi = 7
if sayi % 2 == 0:
    print("Çift sayı")
else:
    print("Tek sayı")
```

### Çoklu Koşul — elif
```python
puan = 85
if puan >= 90:
    print("AA")
elif puan >= 80:
    print("BA")
elif puan >= 70:
    print("BB")
elif puan >= 60:
    print("CB")
else:
    print("FF")
```
- `elif` = "else if" kısaltması — birden fazla olası durum varsa zincirleme koşul yapısı kurulur.
- Koşullar sırayla kontrol edilir, ilk uyan koşul çalışır, diğerlerine bakılmaz.

### Pratik Örnek — Kargo Ücreti
```python
sepet_tutari = 450
vip_uye = True

if sepet_tutari > 500 or vip_uye:
    kargo = 0
    print("Kargo ücretsiz")
else:
    kargo = 50
    print("Kargo ücreti 50 TL")
```

## 6. İç İçe (Nested) if Yapıları — Uyarı

- İç içe if kullanmak **yasak değil**, sabit/basit/az tekrar eden yapılarda sorun yok.
- **Ama döngü içinde binlerce kez çalışacak iç içe if yapıları performans ve HATA AYIKLAMA açısından ciddi sorun yaratır** — hangi seviyedeki if'te hatanın olduğunu bulmak zorlaşır, debug süreci uzar.
- Tavsiye: gerektiğinde kullanılabilir ama aşırısından kaçınılmalı; `and`/`or` ile birleştirilmiş tek seviyeli koşullar genelde daha okunabilir ve yönetilebilir.
- Yapay zekaya kod optimizasyonu sordurmak (kodu inceleyip iç içe yapıyı sadeleştirmesini istemek) meşru bir kullanım — önemli olan geliştiricinin kodu anlayıp doğru yönlendirebilmesi.

## 7. Döngüler — for

### Liste Üzerinde Döngü
```python
meyveler = ["elma", "armut", "muz", "kivi"]
for meyve in meyveler:
    print(meyve)
```

### String (Karakter) Üzerinde Döngü
```python
kelime = "Python"
for harf in kelime:
    print(harf)
```

### range() ile Sayısal Döngü
```python
for sayi in range(6):        # 0'dan 5'e kadar (6 dahil değil)
    print(sayi)

for sayi in range(2, 5):     # 2'den 4'e kadar
    print(sayi)

for sayi in range(0, 10, 2): # 0'dan 10'a ikişer atlayarak
    print(sayi)
```

### for İçinde if — Pratik Örnek (Satış Analizi)
```python
satislar = [150, 300, 450, 500, 200]
toplam_ciro = 0
buyuk_satis_adedi = 0

for satis in satislar:
    toplam_ciro += satis
    if satis > 300:
        buyuk_satis_adedi += 1

print(toplam_ciro)
print(buyuk_satis_adedi)
```
- for döngüsü içinde if kullanmak çok yaygın bir kalıp — döngüyle veri setinde gezinip, her elemanı koşulla filtreleme/toplama işlemi.

## 8. Döngüler — while

### Temel Yapı
```python
sayac = 1
while sayac <= 5:
    print(sayac)
    sayac += 1
print("Döngü tamamlandı")
```
- `while` koşulu `True` olduğu sürece döngü devam eder, `False` olunca çıkar.
- **KRİTİK UYARI: Sonsuz döngüden (infinite loop) kaçının.** Sayaç/koşul güncellenmezse program takılır kalır (`Ctrl+C` ile zorla kesilebilir).

### Şifre Deneme Örneği (while ile)
```python
dogru_sifre = "Python123"
girilen_sifre = ""

while girilen_sifre != dogru_sifre:
    girilen_sifre = input("Şifrenizi girin: ")
    if girilen_sifre != dogru_sifre:
        print("Hatalı şifre, tekrar deneyin")

print("Giriş başarılı")
```

### Deneme Hakkı Sınırlama (break ile)
```python
giris_hakki = 3
while True:
    girilen_sifre = input("Şifrenizi girin: ")
    if girilen_sifre == dogru_sifre:
        print("Giriş başarılı")
        break
    else:
        giris_hakki -= 1
        print("Hatalı şifre")
        if giris_hakki == 0:
            print("Giriş hakkı bitti")
            break
```

## 9. break ve continue

- **`break`**: döngüden tamamen çıkar (döngüyü sonlandırır).
- **`continue`**: mevcut döngü adımının kalan kısmını atlar, döngünün altındaki kodu çalıştırmadan bir sonraki adıma geçer (döngü devam eder, sadece o adım kesilir).

### Hata Mesajlarını Okuma — Pratik Not
- Sonsuz döngüye girildiğinde `Ctrl+C` ile kesilir, hata mesajı hangi satırda sorun olduğunu gösterir (örn. "line 225") ama bu satır her zaman gerçek sorunun kaynağı olmayabilir (örn. hata `print` satırında gösterilse de asıl sorun döngü koşulunun kendisinde olabilir).
- **Kodu okuyamıyorsanız/anlamıyorsanız hatayı bulamazsınız** — bu yüzden yapay zekaya "tüm kodu düzelt" demek yerine, önce kodu küçük parçalara bölüp anlamaya, sonra parça parça düzeltmeye çalışmak öneriliyor.

## 10. Yapay Zeka Kullanımı Hakkında — Tekrar Vurgu

- Kod optimizasyonu, hata düzeltme gibi konularda AI'a danışmak meşru ama **kod okuma/anlama becerisi olmadan AI'ın verdiği çözümü kontrol edemezsiniz.**
- AI, karmaşık/büyük iç içe yapılarda hatalı veya optimize edilmemiş öneriler verebilir — geliştiricinin ne istediğini bilmesi ve AI'ın çıktısını değerlendirebilmesi gerekiyor.
- Gereksiz yere büyük kod bloklarını AI'a yapıştırmak hem token israfı hem hatalı/gereksiz değişikliklere yol açma riski taşır.

## 11. Markdown (Ertelendi)

- Dokümantasyon (Markdown) konusu bu derste işlenmedi — 10 günlük eğitimin sonunda, tüm konular tamamlandıktan sonra anlatılacak.

## 12. Belgrad Süreci Hakkında Soru-Cevap

**Soru:** Belgrad'da (yüz yüze eğitim döneminde) eğitmen yanımızda olacak mı, chatbot/yazılım atölyesi nasıl ilerleyecek?

**Cevap:**
- Belgrad'a gelmeden önce belirli bir envanter teslimi yapılması gerekiyor (bildirilmiş durumda).
- Belgrad'da hem **atölye süreçleri** (eğitmenin gelip konu anlatacağı/destek olacağı saatler) hem **mentörlük süreçleri** (birebir görüşmelerle sorunların çözüldüğü) olacak.
- **Önemli:** Eğitmen kod YAZMAYACAK — katılımcı kodu kendisi yazacak, eğitmen yönlendirecek/destek olacak.

## 13. Sonraki Gün İçin
- Bu derste işlenmeyen konular: liste (list) oluşturma detayları, fonksiyonlar (function) — bir sonraki derslerde işlenecek.
- Fonksiyon kavramı bu derste kısaca değinildi: "bir kod bloğunun isimlendirilip tekrar tekrar çağrılabilir hale getirilmesi" olarak tanımlandı, detayı ileride işlenecek.
