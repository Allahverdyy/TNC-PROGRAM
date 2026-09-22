# Gün 1: Algoritma Mantığı, VS Code, Değişkenler, Veri Tipleri

## 1. Eğitim Süreci Hakkında

- 10 günlük Python eğitimi başlıyor — süreç yoğun geçecek, ortalarda zorlayıcı, sonlara doğru rahatlayan bir tempo planlanıyor.
- Eğitmen: savunma sanayii kökenli yazılım mühendisi, şu an kendi girişimini yürütüyor.
- Hedef: sadece Python öğretmek değil, **yazılım metodolojisi** ve **algoritma mantığı** öğretmek. Amaç 10 günde "kod yazdırmak" değil — **kodu okuyabilmeyi** öğretmek. Kod okuyabilen biri, var olan bir kodu rahatlıkla değiştirebilir.

## 2. Python Neden Tercih Ediliyor

- Değişken tanımlarken veri tipi belirtme zorunluluğu yok (dinamik tipli dil) — C#/.NET, Java gibi dillere göre daha kolay giriş.
- Sözdizimi (syntax) insan diline daha yakın — girinti (indentation) tabanlı, süslü parantez/noktalı virgül yoğunluğu daha az.
- Açık kaynak, geniş community, platform bağımsız (Windows/Linux/Ubuntu fark etmez).
- Yapay zeka, veri bilimi, istatistiksel/matematiksel işlemler için en yaygın kullanılan dil — kütüphane zenginliği diğer dillere göre yüksek.

## 3. Dilden Bağımsız Düşünme

- "Yazılım" = gerçek dünyadaki eylemlerin bilgisayar ortamına aktarılması — belirli bir dille (Python) sınırlı bir kavram değil.
- Kullanım alanına göre dil değişir: gömülü sistemler → C++; mobil uygulama → Java/Kotlin/Swift; masaüstü/web servis → .NET, Python vb.
- Temel: önce **algoritma mantığı** kurulur, sonra hangi dille yazılacağı ayrı bir tercih meselesidir.

## 4. Algoritma Mantığı — Temel Kavram

- Algoritma, soru sorarak ilerleyen bir karar ağacıdır: "TV çalışıyor mu?" → Evet/Hayır → her cevap farklı bir yola götürür → sonunda bir çıktıya (sonuca) varılır.
- Bir butona basıldığında gerçekleşecek eylem de aynı mantıkla önce algoritmaya dökülür, sonra koda çevrilir.
- Kod yazmanın zor kısmı genelde YAZMAK değil, **test etmek / hatayı bulup doğru çözmek**.

## 5. Yapay Zeka ve Yazılımcılık İlişkisi

- Yapay zeka kod yazma sürecinde büyük kolaylık sağlıyor ama **hata ayıklamada (debug)** güvenilir değil — kodu okuyup anlayamayan biri, AI'ın önerdiği "çözümün" gerçekten doğru olup olmadığını değerlendiremez.
- Sonuç: yazılımcılık bitmiyor, AI da elimizden almıyor — algoritma mantığına ve yazılım mimarisine hakim olanlar için AI hız kazandıran bir araç.
- AI'ın işi tam anlamıyla devralması için (tüm süreç otomasyonu) yüksek maliyetli altyapı (büyük cloud, database, token maliyeti) gerekir — bu da pratikte sınırlı.

## 6. VS Code (Visual Studio Code) — Geliştirme Ortamı

- Ücretsiz, Microsoft'un resmi sitesinden indirilir, kurulumu basit.
- Kod editörü olarak tercih ediliyor çünkü: klasör/proje yapısını (mimariyi) yönetmek, kütüphaneleri entegre etmek, terminal/notebook gibi araçları tek yerden kullanmak kolay.
- Alternatif olarak Anaconda/Jupyter Lab/Jupyter Notebook da kullanılabilir ama bu eğitimde VS Code tercih ediliyor (proje mimarisi ve versiyon kontrolü için daha uygun).

### Python Dosyası Oluşturma
- Yeni dosya oluşturulur, uzantı `.py` olmalı.
- **Dosya isimlendirme kuralı:** Türkçe karakter/kelime kullanılmamalı — İngilizce isimlendirme yapılmalı (aksi halde hata riski yüksek).

### Kod Çalıştırma Yöntemleri
1. VS Code içinden **F5** veya "Run" ile çalıştırma.
2. VS Code'un kendi entegre terminalinden `python dosya_adi.py` komutuyla çalıştırma.
3. Harici terminal (PowerShell/CMD) açıp `cd` ile klasöre gidip `python dosya_adi.py` çalıştırma (Tab tuşu ile otomatik tamamlama kullanılabilir).
- **Önemli:** Kodda değişiklik yaptıktan sonra terminalden çalıştırmadan önce dosyayı **Ctrl+S ile kaydetmek** gerekir — aksi halde eski (kayıtsız) hali çalışır.

## 7. İlk Kod — print()

```python
print("Merhaba Dünya")
```

- Geleneksel olarak ilk yazılan kod budur.
- `print()` sadece ekrana yazı bastırma değil — **debug (hata ayıklama) için en pratik araçtır**. Kodun hangi satırda takıldığını, ara değerlerin ne olduğunu görmek için sık kullanılır.

### Tırnak İşareti Farkı
- `print("2012")` → string (metin) değer, karakter karakter tutulur.
- `print(2012)` → sayısal (integer) değer.
- Bu ayrım, verinin hafızada nasıl tutulacağını ve hangi işlemlere tabi tutulabileceğini belirler.

### separator (sep) ve end Parametreleri
```python
print("14", "05", "2026", sep="/")   # 14/05/2026
print("Merhaba", end=" ")            # satır sonuna gitmeden devam eder
```
- `sep`: değerler arasına eklenecek ayraç (örn. tarih formatı için "/").
- `end`: normalde print sonrası satır atlar; `end` ile bu davranış değiştirilir (örn. boşlukla devam ettirmek).

### Yorum Satırı
- `Ctrl+K, Ctrl+C` → seçili satır(lar)ı yorum satırına çevirir (kod çalışmaz hale gelir).
- `Ctrl+K, Ctrl+U` → yorum satırını geri açar.
- Yorum satırları kodun ne yaptığını açıklamak için önemli — "bugün yazdığınız kodu bir hafta sonra unutacaksınız" prensibiyle mutlaka kullanılmalı.

## 8. Değişkenler (Variables)

- Python'da değişken tanımlarken veri tipi belirtme zorunluluğu yoktur — Python, atanan değere bakarak tipini otomatik belirler (dinamik tipleme).
- String değerler hafızada sayısal değerlere göre çok daha fazla yer kaplar (her karakterin kendi ikili/binary karşılığı ayrı ayrı tutulur) — gereksiz yere string kullanmaktan kaçınılmalı.

### İsimlendirme Kuralları
1. Değişken ismi, tuttuğu değeri **anlamlı şekilde tarif etmeli** (örn. `x = 25` değil, `yas = 25`).
2. Birleşik isimler için **snake_case** kullanılır (Python'da yaygın): `ogrenci_yasi`.
3. Diğer dillerde (Python'da daha az yaygın) **camelCase** de görülebilir: `ogrenciYasi`.
4. Rakamla başlanamaz.
5. İsimler arasında boşluk bırakılamaz.
6. Python'ın ayrılmış (reserved) kelimeleri (`if`, `else`, `for`, `print`, `tuple`, `dictionary` vb.) değişken ismi olarak kullanılamaz.
7. **Türkçe karakter kesinlikle kullanılmamalı** (ğ, ş, ı, ö, ü, ç) — değişken/dosya isimlerinde mutlaka İngilizce karakterler kullanılmalı. (String içeriğinde, yani print edilen metinlerde Türkçe karakter kullanmak sorun değildir — sadece tanımlayıcı isimlerde yasak.)

### Örnek
```python
isim = "Ahmet"
yas = 25
puan = 85.5

print(isim)
print(yas)

yas = 26              # değer güncelleme
yedek_isim = isim     # bir değişkenin değerini başka değişkene atama
print(yedek_isim)
```

## 9. Temel Veri Tipleri

| Tip | Açıklama | Örnek |
|---|---|---|
| **string (str)** | Metin, tırnak içinde tanımlanır | `"Ahmet"` |
| **integer (int)** | Virgülsüz tam sayı | `25` |
| **float** | Virgüllü (ondalıklı) sayı | `85.5` |
| **boolean (bool)** | Sadece `True`/`False` (1/0) | `True` |

- Python'da tip belirtme gerekmez — atanan değere göre otomatik belirlenir.
- `type(degisken)` ile bir değişkenin tipi kontrol edilebilir.

## 10. String İşlemleri

### Birleştirme (Concatenation)
```python
ad = "Python"
soyad = "Yazılım"
tam_isim = ad + " " + soyad   # "Python Yazılım"
```
- Boşluk (`" "`) da bir karakterdir — hafızada yer kaplar, gereksiz boşluklardan kaçınılmalı.

### Çarpma (Tekrarlama)
```python
gulumse = "salih"
print(gulumse * 5)   # salihsalihsalihsalihsalih
```

### String + String ≠ Toplama
```python
sayi1 = "10"
sayi2 = "5"
print(sayi1 + sayi2)   # "105" (string birleştirme, TOPLAMA DEĞİL)
```
- String olarak tanımlanmış sayısal değerler `+` ile birleştirilir, toplanmaz. Gerçek toplama için `int()` ile dönüştürme gerekir.

### String Metotları
```python
mesaj = "merhaba dünya"
print(mesaj.upper())      # tamamı büyük harf
print(mesaj.lower())      # tamamı küçük harf
uzunluk = len(mesaj)      # karakter sayısı (boşluk dahil!)
yeni_mesaj = mesaj.replace("dünya", "Python")   # değiştirme
```
- `len()` boşlukları da sayar — "merhaba dünya" 13 karakterdir (boşluk dahil).

### İndeksleme (Indexing) — KRİTİK KURAL
- **İndeksler 0'dan başlar.** Bu, tüm veri yapılarında (string, list, tuple vb.) geçerli evrensel bir kuraldır.
```python
mesaj = "merhaba dünya"
print(mesaj[3])        # 4. karakter (0'dan sayınca)
print(mesaj[0:3])      # 0,1,2. karakterler (3 dahil değil)
print(mesaj[3:])       # 3. karakterden sona kadar
print(mesaj[0:7:2])    # 0'dan 7'ye ikişer atlayarak
print(mesaj[::-1])     # tersten yazdırma
```

## 11. Sayısal Tip İşlemleri

```python
dogum_yili = 1995          # int
kredi_borcu = -1500.0      # float
puan = 32.45                # float

sonuc = dogum_yili + 0.5   # int + float = float (otomatik tip yükseltme)
print(sonuc, type(sonuc))
```

- Python'da int ile float doğrudan toplanabilir — sonuç otomatik float'a yükseltilir (diğer dillerde tip dönüşümü elle yapılması gerekebilir).

### Yuvarlama ve Mutlak Değer
```python
fatura = 245.78
print(round(fatura))        # en yakın tam sayıya yuvarlama
print(round(fatura, 1))     # virgülden sonra 1 haneye yuvarlama
print(abs(-12))             # mutlak değer → 12
```

## 12. Boolean (Bool) Tipi

- Sadece `True` ve `False` değerlerini alır (1 ve 0).
- Karşılaştırma işlemleri boolean sonuç döndürür:
```python
sonuc = 10 > 5
print(sonuc)   # True
```
- **Önemli kural:** `0` her zaman `False`'a eşdeğerdir; `0` dışındaki her sayısal değer `True`'ya eşdeğerdir.
- Boş string (`""`) → `False`; içinde karakter olan string → `True`.
- Pratik kullanım örneği: 0'a bölme kontrolü (bir sayı 0 ise `False`, matematiksel hata önlenir — if/else ile ileride detaylandırılacak).

## 13. Tip Dönüşümü (Type Casting)

- Özellikle haberleşme/veri aktarımında (örn. JSON verisi) tüm veriler string olarak gelir — sayısal işlem yapmak için dönüştürülmesi gerekir.

```python
girdi = input("Doğum yılınızı girin: ")   # input() HER ZAMAN string döndürür
dogum_yili = int(girdi)                    # string → int dönüşümü
yas = 2026 - dogum_yili
print(yas)
```

- `input()` fonksiyonunun döndürdüğü değer HER ZAMAN string'dir — sayısal işlem yapılacaksa mutlaka `int()` veya `float()` ile dönüştürülmelidir. Dönüştürülmeden doğrudan işlem yapılırsa hata (`TypeError`) alınır.
- Pratik kısayol: `yas = int(input("Doğum yılınızı girin: "))` — girdiyi doğrudan int'e çevirerek tek satırda alma.

## 14. Genel Öğrenci Notları
- Sınıfta hem tecrübeli yazılımcılar hem hiç kod yazmamış katılımcılar var — eğitmen her seviyeye uygun ilerlemeyi hedefliyor.
- Dersleri kaçırmamak kritik — Belgrad'daki uygulamalı süreçte geride kalmamak için günü gününe takip önemli.
- Yapay zeka kullanımı serbest ama üretilen kodun mantığını açıklayabilmek bekleniyor.

## 15. Sonraki Gün İçin
- Tip dönüşümleri konusuna devam edilecek, ardından muhtemelen if/else (karar yapıları) ve döngüler işlenecek.
