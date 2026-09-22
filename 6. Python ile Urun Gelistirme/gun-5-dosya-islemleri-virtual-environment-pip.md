# Gün 5: Dosya İşlemleri (Okuma/Yazma), Virtual Environment, pip Paket Yönetimi

## 1. Dosya İşlemlerine Giriş — Neden Gerekli

- Bugüne kadar yazılan kodlarda hiçbir veri kalıcı olarak saklanmadı — hepsi RAM'de (geçici hafızada) çalıştı, program kapanınca kayboldu.
- Kalıcı saklama veya haberleşme için farklı dosya türleri kullanılır: **TXT**, **JSON**, **SQL** (veritabanı) vb. Bu derste TXT üzerinden dosya okuma/yazma işlendi.

## 2. Dosya Açma Modları (open() Operatörleri)

| Mod | Anlamı | Dosya Yoksa | Dosya Varsa |
|---|---|---|---|
| `r` | Read (okuma) | Hata verir | Okur |
| `w` | Write (yazma) | Oluşturur | **İçeriği tamamen siler, sıfırdan yazar** |
| `a` | Append (ekleme) | Oluşturur | Sonuna ekler, mevcut veriyi SİLMEZ |
| `x` | Create (oluşturma) | Oluşturur | Hata verir (zaten var) |
| `r+` | Okuma + yazma | Hata verir | Dosyanın var olması şart |
| `b` (binary) | İkili mod | — | Resim/video gibi binary dosyalar için |

**KRİTİK UYARI:** `w` (write) modu, dosya zaten varsa içeriğini SİLER ve sıfırdan yazar — kalıcı/önemli veri kaybına yol açabilir. Bunu kasıtlı bilerek (örn. geçici log dosyası) mı kullanıyorsunuz yoksa yanlışlıkla mı veri kaybediyorsunuz, buna dikkat edilmeli.

## 3. Temel Yazma İşlemi

```python
dosya = open("notlar.txt", "w")
dosya.write("Python öğreniyorum\n")
dosya.write("Dosya işlemleri çok kolay\n")
dosya.close()   # MUTLAKA kapatılmalı
```
- `\n` satır sonu karakteri — eklenmezse tüm veriler yan yana (aynı satırda) yazılır.
- **`.close()` unutulursa** veri kaybı, dosya bozulması gibi sorunlar oluşabilir — yapılan yazma işlemi garanti altına alınmamış olur.

## 4. Okuma İşlemleri

```python
dosya = open("notlar.txt", "r")
icerik = dosya.read()        # tüm dosyayı TEK STRING olarak alır
dosya.close()

dosya = open("notlar.txt", "r")
satirlar = dosya.readlines()  # her satırı ayrı elemanlı LİSTE olarak alır
dosya.close()

dosya = open("notlar.txt", "r")
ilk_satir = dosya.readline()  # sadece BİR satır okur (tekrar çağrılırsa bir sonraki satır)
dosya.close()
```

### Büyük Dosyalarda Satır Satır Okuma (Hafıza Dostu Yöntem)
```python
dosya = open("veri.txt", "r")
satir_no = 1
for satir in dosya:
    print(satir_no, satir.strip())
    satir_no += 1
dosya.close()
```
- Milyon satırlık bir dosyanın tamamını `.read()` ile tek seferde belleğe (RAM) çekmek gereksiz yüksek hafıza kullanımına ve hafıza hatalarına yol açabilir.
- Bu yüzden büyük veri setlerinde (örn. bir yapay zeka modelinin eğitim verisi) dosya **satır satır** (döngüyle) okunmalı.

## 5. Append (Ekleme) Modu — Veri Kaybını Önleme

```python
dosya = open("gunluk.txt", "a")
dosya.write("2. gün devam ediyorum\n")
dosya.close()
```
- `w` moduna göre GÜVENLİ — mevcut veriyi silmeden sonuna ekler.
- Log dosyaları için kullanım örneği: bazı senaryolarda hata logları silinmemeli, hep ARKA arkaya eklenmeli (append); bazı senaryolarda ise (geçici/tekrar eden log) her seferinde sıfırlanabilir (write) — hangisinin doğru olduğu ihtiyaca göre belirlenir.

## 6. with Bloğu — .close() Unutma Riskini Ortadan Kaldırma

```python
with open("veri.txt", "r", encoding="utf-8") as dosya:
    icerik = dosya.read()
    print(icerik)
# blok bittiğinde dosya OTOMATİK kapanır — close() yazmaya gerek yok
```
- **Tavsiye edilen yöntem budur.** `.close()` çağrısını unutma riskini tamamen ortadan kaldırır.
- `write`, `read`, `append` — hepsi `with` bloğu içinde aynı şekilde kullanılabilir.

### encoding="utf-8" — Türkçe Karakter Sorunu
```python
with open("gorevler.txt", "w", encoding="utf-8") as dosya:
    for gorev in gorevler:
        dosya.write(gorev + "\n")
```
- `encoding="utf-8"` belirtilmezse, Türkçe karakterler (ğ, ş, ı, ö, ü, ç) bazı ortamlarda (örn. VS Code'da dosyayı açarken) bozuk görünebilir.
- Türkçe karakterlerin doğru okunup yazılması için `encoding="utf-8"` parametresi eklenmesi öneriliyor.

## 7. .strip() — Satır Sonu Boşluğunu Temizleme

```python
satir.strip()   # \n ve baştaki/sondaki boşlukları temizler
```
- Dosyadan okunan her satırın sonunda genelde `\n` bulunur — bu boşluk da bir karakterdir, hafıza kaplar ve karşılaştırma/işlem yaparken sorun çıkarabilir. `.strip()` ile temizlenir.

## 8. os.path Modülü — Dosya Varlık Kontrolü

```python
import os

if os.path.exists("ornek.txt"):
    print("Dosya mevcuttur")
else:
    print("Dosya mevcut değildir")
```
- `import os` bir **kütüphane/modül entegrasyonudur** — F12 (Go to Definition) ile modülün kendi kaynak koduna gidip hangi fonksiyonların ne işe yaradığı incelenebilir.
- Bir dosyayı okumadan/yazmadan önce var olup olmadığını kontrol etmek, sistemin çökmeden (hata vermeden) çalışmasını sağlar.

### Dosya Boyutu Kontrolü
```python
boyut = os.path.getsize("gorevler.txt")
print(boyut, "byte")
```

### Pratik Örnek — Sayaç Uygulaması (Dosya Varlığına Göre Davranma)
```python
import os

dosya_adi = "sayac.txt"

if os.path.exists(dosya_adi):
    with open(dosya_adi, "r") as dosya:
        sayac = int(dosya.read())   # dosyadan okunan HER ŞEY STRING'tir!
else:
    sayac = 0

sayac += 1
print("Program", sayac, "kez çalıştırıldı")

with open(dosya_adi, "w") as dosya:
    dosya.write(str(sayac))
```
- **KRİTİK KURAL: Dosyadan okunan her değer STRING'tir** — sayısal işlem yapmadan önce `int()` veya `float()` ile dönüştürülmesi ZORUNLU, aksi halde string ile matematiksel işlem hatası (veya string birleştirme gibi yanlış sonuç) alınır.

## 9. Yol (Path) Hataları — Sık Karşılaşılan Sorun

- Bir Python dosyasını **F5 ile VS Code içinden** çalıştırmakla, **terminalden manuel yol vererek** çalıştırmak farklı çalışma dizinleri (working directory) kullanabilir.
- Dosya oluşturma/okuma işlemleri, kodun çalıştırıldığı dizine göre göreli (relative) yol kullanıyorsa, hangi ortamdan çalıştırıldığına göre dosyanın nerede oluştuğu/aranacağı değişir.
- Hata mesajını dikkatlice okumak (dosya bulunamadı hatası genelde yanlış yol yüzünden olur) sorunun kaynağını hızlıca gösterir — AI'a sormadan önce hatayı okuma alışkanlığı öneriliyor.

## 10. Virtual Environment (Sanal Ortam) — Neden Gerekli

### Problem
- Farklı projeler farklı kütüphane versiyonlarına ihtiyaç duyabilir — sistem genelinde (global) tek bir Python kurulumu kullanmak, projeler arasında versiyon çakışmasına yol açar.
- Kütüphaneleri doğrudan ana Python kurulumuna yüklemek, sistemi "kirletir" ve düzensiz/kontrolsüz bir yapı oluşturur.

### Çözüm — İzole Sanal Ortam
- Her proje için bağımsız, izole bir "sanal makine" benzeri ortam oluşturulur — o ortamdaki kütüphaneler sadece o projeye özgüdür, ana sisteme (lokale) dokunmaz.
- Farklı projeler farklı versiyonlarda kütüphane kullansa bile birbirini etkilemez.

### Kurulum Adımları
```bash
# 1. Proje klasörü oluştur, içine gir
cd "proje_klasoru"

# 2. Sanal ortam oluştur
python -m venv venv

# 3. Ortamı aktive et (Windows PowerShell)
venv\Scripts\Activate.ps1
# (PowerShell'de execution policy izin sorunu çıkarsa CMD kullanılabilir)

# Windows CMD için:
venv\Scripts\activate.bat
```
- Aktivasyon sonrası terminal artık sanal ortamın içinde çalışır — komut satırında bunun göstergesi görülür (örn. `(venv)` öneki).
- Mac/Linux'ta aktivasyon komutları farklıdır (araştırılarak bulunabilir, ezberlenmesi gerekmiyor).

### pip ile Paket Yönetimi
```bash
pip install requests              # paket yükle
pip install requests==2.31.0      # belirli versiyon yükle
pip install --upgrade requests    # paketi güncelle
pip uninstall requests            # paket kaldır
pip list                          # yüklü paketleri listele
pip show requests                 # paket detaylarını (versiyon, lisans vb.) göster
```

### requirements.txt — Taşınabilir Bağımlılık Listesi
```bash
pip freeze > requirements.txt
```
- Tüm yüklü kütüphaneleri ve versiyonlarını bir dosyaya kaydeder.
- Amaç: proje GitHub'a veya başka bir ortama taşındığında, kütüphanelerin kendisini taşımak yerine sadece bu listeyi taşımak — başka biri projeyi aldığında:
```bash
pip install -r requirements.txt
```
komutuyla tüm gerekli kütüphaneleri tek seferde internetten indirebilir.
- Bu dosya manuel de düzenlenebilir — her satıra `kutuphane_adi==versiyon` şeklinde yazılabilir.

## 11. .gitignore — Gizli/Gereksiz Dosyaları Git'ten Hariç Tutma

- `.gitignore` dosyası, GitHub'a (veya başka bir versiyon kontrol sistemine) commit atarken hangi dosyaların GÖRMEZDEN GELİNECEĞİNİ belirler.
- Tipik içerik: Python cache dosyaları, sanal ortam klasörü (`venv/`), ortam değişkeni dosyaları.

### .env Dosyası — Gizli Anahtarların Saklanması
- `.env` uzantılı bir dosya oluşturularak (örn. Not Defteri'nde dosya oluşturup uzantısını `.env` yapmak yeterli) API anahtarları gibi **gizli tutulması gereken bilgiler** buraya yazılır.
- **KRİTİK GÜVENLİK KURALI:** `.env` dosyası KESİNLİKLE `.gitignore`'a eklenip GitHub'a asla commit edilmemeli — API anahtarı gibi gizli bilgiler (örn. bir yapay zeka modeli API key'i) üçüncü şahıslar tarafından görülmemeli.
- Bu konu (ortam değişkenlerinin kod içinde nasıl kullanılacağı) ileride detaylı işlenecek.

## 12. Belgrad Süreci — Duman Testi ve Hedef Mimari (Soru-Cevap)

**Soru:** "Duman testi" (smoke test) ve "hedef mimari" ikisini de mi Belgrad'a gelmeden bitirmemiz gerekiyor?

**Cevap:**
- İkisi de yapılacak ama tamamı Belgrad'a gelmeden bitmek zorunda değil.
- **Hedef mimari:** Oluşturulacak proje yapısı — klasör yapısı, dosya organizasyonu — en azından bunun iskeleti Belgrad öncesi hazır olmalı.
- Belgrad'a gelmeden önce düzenli şekilde kod yazmaya devam edilmeli, ama detaylı/son hali Belgrad'da tamamlanacak.

## 13. Genel Prensip — Tekrar Vurgu

- Terminal komutları (`cd`, `venv`, `pip` vb.) ezberlenecek şeyler değil — gerektiğinde araştırılıp kullanılan pratik araçlar.
- Dosya işlemlerinde en kritik alışkanlıklar: `with` bloğu kullanmak, `encoding="utf-8"` eklemek, string→sayı dönüşümünü unutmamak, veri kaybı riskini (`w` modu) bilinçli yönetmek.

## 14. Sonraki Hafta İçin
- Hazır kütüphaneler ve modüller konusuna bu derste kısaca değinilip bırakıldı — detaylı işlenecek.
- Ortam değişkenleri (.env) ve API key kullanımı ileride detaylandırılacak.
