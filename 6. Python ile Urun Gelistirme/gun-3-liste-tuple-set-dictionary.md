# Gün 3: Veri Yapıları — List, Tuple, Set, Dictionary

## 1. Genel Bakış — Toplu Veri Tutma Yöntemleri

Python'da (ve çoğu dilde benzer şekilde) birden fazla veriyi bir arada tutmak için 4 temel yapı var:

| Yapı | Söz Dizimi (Syntax) | Değiştirilebilir mi | İndeksli mi |
|---|---|---|---|
| **list** | `[ ]` köşeli parantez | Evet | Evet (0'dan başlar) |
| **tuple** | `( )` normal parantez | Hayır (değiştirilemez) | Evet (0'dan başlar) |
| **set (küme)** | `{ }` süslü parantez | Evet | Hayır (indekssiz, sırasız, tekrarsız) |
| **dictionary (sözlük)** | `{ key: value }` süslü parantez, iki değer | Evet | Hayır (key/value ile erişilir) |

## 2. List (Liste)

### Oluşturma
```python
meyveler = ["elma", "armut", "muz", "kivi"]
karisik = ["metin", True, 3.14]   # farklı veri tipleri aynı listede tutulabilir
```
- Python'a özgü esneklik: aynı liste içinde string, bool, float, int karışık tutulabilir.
- **Tavsiye edilmez / dikkatli kullanılmalı:** Farklı tipte çok sayıda veriyi karışık listede tutmak karışıklığa yol açar — sadece sınırlı/kontrollü durumlarda kullanılmalı.

### İndeksleme (Tekrar — Kritik Kural)
```python
meyveler[0]     # elma (baştan)
meyveler[-1]    # kiraz (sondan)
meyveler[1:4]   # aralık: 1'den 4'e kadar (4 dahil değil)
```

### Değer Güncelleme
```python
meyveler[1] = "portakal"   # indeksteki değeri değiştirir
```

### Ekleme / Çıkarma
```python
diller = ["Python", "Java", "C++"]
diller.append("JavaScript")       # sona ekler
diller.insert(1, "C#")            # belirli indekse ekler, sonrasını kaydırır
diller.remove("Java")             # değere göre siler
diller.pop()                      # sondan siler
```

**Uyarı:** Bir listenin ortasına `insert` ile veri eklemek, o listeyi kullanan başka fonksiyonların indeks varsayımlarını bozabilir — listede değişiklik yapmadan önce o listenin başka nerelerde/nasıl kullanıldığını kontrol etmek gerekir. AI bu tür yan etkileri göremeyebilir, geliştiricinin bilmesi gerekiyor.

### Sıralama ve Arama
```python
notlar = [78, 90, 65, 90, 40]
notlar.sort()                    # küçükten büyüğe
notlar.sort(reverse=True)        # büyükten küçüğe
notlar.count(90)                 # kaç tane 90 var
notlar.index(40)                 # 40'ın indeksi
len(notlar)                      # eleman sayısı
```
- Sıralama, koordinat/vektör hareketleri, robotik hareket algoritmaları gibi alanlarda kritik — sıralı olmayan veri, beklenmedik/saçma hareketlere yol açabilir.

### for Döngüsüyle Liste İşleme (Pratik Kalıp)
```python
sepet = [400, 100, 500, 300, 200]
toplam = 0
kargo_bedava = []

for urun in sepet:
    toplam += urun
    if urun > 300:
        kargo_bedava.append(urun)
```

### KRİTİK: Referans vs Kopya Sorunu
```python
liste_a = ["elma", "muz"]
liste_b = liste_a          # bu REFERANS atamasıdır, kopya DEĞİL
liste_b[0] = "armut"
# liste_a da değişir! ["armut", "muz"]

liste_c = liste_a.copy()   # gerçek kopya — bağımsız
liste_c[1] = "portakal"
# liste_a etkilenmez
```
- **Bu Python'a özgü değil — çoğu dilde geçerli evrensel bir davranış.**
- `liste_b = liste_a` yazıldığında iki isim aynı hafıza alanını (referansı) paylaşır — birinde yapılan değişiklik diğerini de etkiler.
- Bu, farkında olunmadığında ciddi hatalara yol açar: bir listeyi birden fazla fonksiyonda kullanıyorsanız ve birinde değişiklik yaparsanız, diğerlerindeki sonuçlar da sessizce (hata vermeden) bozulur — sonuç yanlış çıkar ama neden belli olmaz.
- Kural: bir listeyi bağımsız olarak değiştirmek istiyorsanız mutlaka `.copy()` kullanın.

### İç İçe (Nested) Listeler — Uyarı
```python
sinif = [
    ["Ahmet", 25, "erkek"],
    ["Ayşe", 22, "kadın"]
]
sinif[0][0]   # "Ahmet"
```
- İç içe liste teknik olarak çalışır ama **okunabilirlik açısından zayıf** — "0. öğrencinin 0. verisi" gibi indeks-içinde-indeks mantığı hata ayıklamayı zorlaştırır.
- **Tavsiye:** Bu tür durumlarda liste yerine **nesne (class/object)** veya **dictionary** kullanmak çok daha okunabilir ve yönetilebilir.
- Aşırı iç içe yapı (3-4 seviye nested for/list) performans ve okunabilirlik açısından ciddi sorun — büyük O(n²), O(n³) karmaşıklığa yol açabilir (yazılım mühendisliğinde "büyük O notasyonu" kavramına değinildi, detaya girilmedi).

### List Comprehension (Tek Satırda Liste Oluşturma)
```python
sayilar = [1, 2, 3, 4, 5]
kareler = [sayi * 2 for sayi in sayilar]   # [2, 4, 6, 8, 10]
```
- Aynı sonuca uzun bir for döngüsüyle de ulaşılabilir; list comprehension daha kısa/okunabilir ama AŞIRI karmaşık ifadeler için (çok uzun tek satır) yine okunabilirlik zarar görür — dengeli kullanılmalı.

## 3. Tuple (Değiştirilemez Liste)

### Oluşturma ve Temel Özellik
```python
renkler = ("mavi", "kırmızı")
renkler[0] = "siyah"   # HATA! Tuple değiştirilemez
```
- Tuple, verinin **kasıtlı olarak korunması** gerektiğinde kullanılır — bir fonksiyonun dışından/başka kodlardan yanlışlıkla değiştirilmesini engellemek için.

### Tek Elemanlı Tuple — Dikkat
```python
sahte_tuple = ("Ahmet")      # bu bir STRING'tir, tuple değil!
gercek_tuple = ("Ahmet",)    # virgül şart — bu bir tuple'dır
```
- Virgül olmadan tek elemanlı parantez, tuple değil normal string/değer olarak yorumlanır — `type()` ile kontrol edilebilir.

### Metotlar (Sınırlı — Sadece 2 Tane)
```python
sonuclar = (10, 20, 30, 40, 30)
sonuclar.count(30)   # kaç tane var
sonuclar.index(40)   # indeksi
```
- Liste'nin aksine tuple'da sadece `.count()` ve `.index()` var — ekleme/çıkarma/sıralama yok (değiştirilemez olduğu için).

### Unpacking (Değerleri Ayrı Değişkenlere Açma)
```python
kullanici = ("Ahmet", 25, "erkek")
ad, yas, cinsiyet = kullanici
```

### Hızlı Değişken Takası (Swap)
```python
a, b = 10, 20
b, a = a, b   # tek satırda yer değiştirme
```
- Bu yöntem olmadan geleneksel takas için üçüncü bir geçici değişken gerekirdi (`c = a; a = b; b = c`) — Python'ın tuple unpacking özelliği sayesinde tek satırda yapılabiliyor.

## 4. Set (Küme)

### Temel Özellik — Tekrarsız ve Sırasız
```python
sayilar = {10, 20, 30, 30, 30, 40, 40}
print(sayilar)   # {10, 20, 30, 40} — tekrarlar otomatik silinir
```
- **İndeks yok** — `sayilar[0]` gibi bir erişim MÜMKÜN DEĞİL.

### Ekleme / Çıkarma
```python
sayilar.add(60)
sayilar.remove(30)   # o değerin TÜM tekrarlarını (zaten tek kopya var) siler
```

### Listeden Tekrarları Temizleme (Pratik Kullanım)
```python
isimler = ["Ahmet", "Ayşe", "Mehmet", "Ayşe", "Fatma"]
temiz_liste = list(set(isimler))   # önce set'e çevir (tekrar silinir), sonra listeye geri çevir
```

### Küme İşlemleri (Matematiksel Küme Mantığı)
```python
a_grubu = {"Python", "Java", "C++"}
b_grubu = {"Python", "JavaScript", "C#"}

a_grubu | b_grubu   # birleşim (union)
a_grubu & b_grubu   # kesişim (intersection) → {"Python"}
a_grubu - b_grubu   # fark (difference) → {"Java", "C++"}
a_grubu ^ b_grubu   # simetrik fark (symmetric difference) → ortak olmayanlar
```

## 5. Dictionary (Sözlük) — Key-Value Yapısı

### Temel Mantık
- Listede veriye **indeks numarasıyla** erişilirken (`liste[0]`, `liste[1]`), dictionary'de veriye **tanımlanmış bir isimle (key)** erişilir.
- `key`: tanımlayıcı isim; `value`: o isme karşılık gelen veri.

### Oluşturma ve Erişim
```python
ogrenci = {"ad": "Ahmet", "yas": 25, "cinsiyet": "erkek"}
ogrenci["ad"]    # "Ahmet"
ogrenci["yas"]   # 25
```

### Güncelleme ve Yeni Anahtar Ekleme
```python
ogrenci["yas"] = 26          # var olan değeri günceller
ogrenci["meslek"] = "mühendis"  # yeni key-value ekler
```

### Güvenli Erişim — .get() Kullanımı
```python
ogrenci["meslek"]        # key yoksa HATA (KeyError) verir
ogrenci.get("meslek")    # key yoksa None (nal/nan) döner, program çökmez
```
- **Önemli pratik kural:** Bir dictionary'den veri çekerken, o key'in var olup olmadığından emin değilseniz `.get()` kullanmak programın çökmesini (crash) önler. Bulunamayan değer `None` döner, buna göre bir "null check" (boş kontrolü) yapılmalı.

### Key, Value ve Items ile Döngü
```python
puanlar = {"Ahmet": 85, "Ayşe": 90, "Mehmet": 70, "Fatma": 95}

for isim in puanlar.keys():
    print(isim)

for puan in puanlar.values():
    print(puan)

for isim, puan in puanlar.items():
    print(isim, puan)
```

### İç İçe Dictionary
```python
kullanicilar = {
    "kullanici1": {"ad": "Ahmet", "yas": 25},
    "kullanici2": {"ad": "Ayşe", "yas": 22}
}
kullanicilar["kullanici1"]["ad"]   # "Ahmet"
```
- Bu yapı **JSON veri formatına** çok benzer (JSON'da tüm değerler string olur, Python dictionary'de sayısal değerler de doğrudan tutulabilir).
- İç içe dictionary, iç içe listeye göre daha okunabilir çünkü her seviyede anlamlı bir key ismi var (indeks numarası değil).

## 6. Genel Tavsiyeler — Tüm Veri Yapıları İçin

- Her yapının kendine has doğru kullanım alanı var — birbirinin yerine geçmez.
- **Değişmemesi gereken veri → tuple.**
- **Tekrarsız/kümesel işlem gereken veri → set.**
- **Anlamlı isimle erişilecek, ilişkisel veri → dictionary.**
- **Sıralı, değişebilir, indeksli koleksiyon → list.**
- İç içe (nested) yapılardan mümkün olduğunca kaçının; gerekiyorsa nesne (class) tanımlamayı değerlendirin — kodun okunabilirliği ve hata ayıklama kolaylığı önceliklidir.

## 7. Öğrenci Geri Bildirimi

- Hiç kod yazmamış katılımcılar için içerik yoğun ama net bir "anlamadım" noktası olmadığı, video tekrarıyla oturacağı belirtildi.
- Eğitmen tavsiyesi: ezberlemeye çalışmayın, mantığı kavramaya odaklanın — çok fazla detay var, hepsini ezbere tutmak gerekmiyor, gerektiğinde araştırıp bulmak yeterli.

## 8. Sonraki Gün İçin
- Fonksiyonlara (function) giriş yapılacak — bu derste değinilmedi, bir sonraki derse bırakıldı.
