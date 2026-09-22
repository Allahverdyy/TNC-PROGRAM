# Gün 9: Açık Chat Paneli Derinleştirme, Editor vs Studio Karşılaştırması, Genel Özet

## 1. Açık Chat Paneli — Tam Yapım Süreci (Ana Sayfa/Bölüm İçi)

Dıştan içe katman sırası:

1. **Dış konteyner** — tüm paneli kapsayan ana kutu. Renk, corner radius (örn. 8px) verilir.
2. **Başlık konteyneri** — dış konteynerin üst kısmına ayrı bir konteyner eklenir (genişliği dış konteynerle aynı, örn. 72px yükseklik, glass effect, corner radius). İçine padding + başlık text (Heading 5, Hug → Scale Proportionality) + opsiyonel SVG ikon eklenir, ikon ve yazı Stack ile birleştirilir.
3. **Yazışma alanı konteyneri** — dış konteynerin ortasına, başlığın altına ikinci bir konteyner eklenir (biraz daha dar, örn. dış konteynerden 8px içeride, ayrı bir corner radius ve glass effect ile). **Kod SADECE bu konteynere bağlanır** — dış konteynere değil.
4. **Overflow Content → Scroll** bu yazışma konteynerine verilir — mesajlar uzadıkça kayar, input/butonun üstüne taşmaz.
5. **Input** (mesaj yazma alanı) — dış konteynerin alt kısmına, 52px yükseklik, Scale Proportionality, sol/alt kenara sabitlenir.
6. **Gönder butonu** — input ile aynı yükseklikte (52px), sağ/alt kenara sabitlenir, input ile Stack'lenir.
7. Tüm katmanlar tek tek Scale Proportionality kontrolünden geçirilir, responsive test (ekranı büyültüp-küçültme) her adımdan sonra tekrarlanır.

### Sık Karşılaşılan Hata ve Çözümü
- Elementler stack'lenmeden/yüzdeye çevrilmeden bırakılırsa yayınlandığında kayma/iç içe geçme oluşur.
- Çözüm: boyut ayarlarında "gelişmiş ayarlar" açılıp otomatik (auto) yerine **yüzde (%)** bazlı boyutlandırmaya geçilmesi bozulmaları düzeltebilir.
- Bazı durumlarda Wix bir section'ı düzgün algılamayabilir (ör. Anchor bağlarken section görünmemesi) — bu durumda ilgili yapı yeni bir section'a taşınarak sorun çözülür.

## 2. Geniş Input Formu Örneği (İsim, Soyisim, Email, Telefon, Not, Tarih)

- Birden fazla input yan yana/alt alta dizilirken her biri ayrı ayrı Scale Proportionality yapılıp sonra Stack ile gruplanır (örn. isim+soyisim bir stack, email+telefon başka bir stack, ardından bu gruplar birbirleriyle tekrar stack'lenir).
- Geniş bir "mesaj/not" input'u eklenirken genişliği **Relative Width** yapılırsa diğer elementlerle birlikte orantılı büyüyüp küçülür.
- Tarih seçici (date picker) input'u da aynı mantıkla eklenebilir.
- Form en sonunda tek bir buton (Demo Talep Et / İletişime Geç) ile kapatılır, o da diğer inputlarla stack'lenir.
- Test: ekran genişliği 1000px, 1650px gibi farklı değerlere çekilerek bozulma olup olmadığı kontrol edilir.

## 3. Anchor (Buton → Sayfa İçi Bölüme Yönlendirme) — Pratik Sorun ve Çözüm

- Bir buton "Link → Anchor → [Sayfa] → [Section]" ile ilgili bölüme bağlanabilir.
- Bazen Wix doğru section'ı listede göstermeyebilir — bu durumda mevcut yapı silinip yeniden aynı bölüme (farklı bir section numarasıyla) taşınarak veya sayfa yeniden kontrol edilerek çözülür; birkaç deneme gerekebilir.
- Anchor çalıştığında butona tıklanınca sayfa otomatik olarak ilgili bölüme kaydırılır (chat/form alanına yönlendirme için sık kullanılır).

## 4. Yönetim Paneli Sayfası — Genişletilmiş Yapı

### Üst Bilgi (Header) Bölümü
- Logo + sayfa başlığı ("Müşteri Yönetim Paneli") + arama input'u + buton(lar) (Yenile, Verileri İndir, Ana Sayfaya Dön vb.) — hepsi stack ile hizalanır, glass effect ile tasarlanabilir.

### İstatistik Kartları (Opsiyonel)
- Toplam Lead, Bu Ay, Günlük Veri gibi kartlar konteyner içine stack'lenerek dizilir — kod bağlanmazsa statik/temsili gösterilebilir.

### Müşteri Adayları Tablosu (Repeater)
- Alt bölüm bir hücreye ayrılır, içine önce padding verilen bir konteyner, onun içine **Repeater** (yatay) eklenir.
- Repeater içine Müşteri/Mesaj/Tarih/Durum gibi text alanları eklenir — her biri kod tarafından doldurulacak alan tanımı olarak işlev görür.
- Başlık ("Müşteri Adayları Tablosu") repeaterın üstüne ayrı bir hücrede, Heading 5-6 boyutunda eklenir.

### Bağlantı Tasarımı Notu
- Chat/form alanı ayrı bir sayfa (Karşılama Sayfası) olarak yapılmışsa, Yönetim Paneline "Karşılama Sayfasına Dön" butonu eklenmelidir.
- Chat/form alanı bir sayfanın bölümü olarak yapılmışsa (ör. Ana Sayfa veya Hakkımızda sonu), Yönetim Paneline doğrudan o bölüme (anchor ile) veya o sayfaya (link ile) dönen bir buton eklenebilir.

## 5. Ders İçi Öz-Değerlendirme (Öğrenci Özetleri — Doğrulandı)

Öğrencilerin kendi notlarından derlenen ve eğitmen tarafından onaylanan kritik kurallar listesi:
- Sitede olması gereken sayfalar: Ana Sayfa, Hakkımızda, Hizmetlerimiz/Çözümlerimiz (ayrı sayfalar, bölüm değil).
- Hakkımızda altına KVKK metni alt sayfa olarak eklenebilir.
- Chatbot her sayfada görünür, açılıp kapanır olmalı.
- İletişim/form alanı: chatbot'a yazılan bilgilerin yönetim paneline aktarılması sisteminin kurgulanması gerekiyor.
- Chat, ayrı bir sayfada veya ana sayfaya gömülü bir bölüm olarak konumlandırılabilir — biri "açık" ise diğerine (açılır/kapanır chatbot) gerek kalmaz.
- Stüdyoda TÜM işlemler sağ panelden yapılmalı (orantısız büyütüp publish etmek kaymalara yol açar); Editor'de manuel sürükleme daha kabul edilebilir ama yine de dikkatli olunmalı.
- Üst üste konteyner atılmamalı.
- Bir elemente kod bağlandıktan sonra silinirse kod bağlantısı bozulur — büyütme/küçültme serbest, silme değil.
- Görsel eklerken: bir kez tıklama = konteynere, iki kez tıklama = görselin kendisine ulaşır.

## 6. Logo Serbest Alan — Soru-Cevap Netleştirmesi

**Soru:** Logo sola yaslandığında logo ile kenar arasında beklenenden fazla boşluk oluşuyor, neden?

**Cevap:** Bu boşluk, logonun İÇİNDE tanımlanmış olan **serbest alan** (clear space) değeridir — logo dosyasının kendi sınırları içine dahil edilmiş bir güvenlik payıdır. Logo tasarlanırken şekil bozulmasın diye bilinçli bırakılan bu boşluk korunmalıdır, kaldırılmamalıdır. Padding değeri sıfır olsa bile logo görselinin kendi içindeki bu pay görünmeye devam eder — bu normal ve doğru bir davranıştır.

## 7. Editor vs Studio — Kapsamlı Karşılaştırma

### Ortak Noktalar
- İkisinde de şablon veya boş sayfa seçeneği var.
- İkisinde de Header/Footer, Menu, Input, Button, Image, Gallery, Strip gibi temel elementler mevcut.
- İkisinde de Site Style (renk teması + tipografi teması) kaydedilebiliyor — Color Theme ve Text Theme ile başlıklar/paragraflar tek seferde tanımlanıp tüm şablona otomatik uygulanıyor.
- İkisinde de logo/element **Pin** edilebiliyor (Editor'de sağ tık → "Pin to Screen"; Studio'da Position → Pin → Page/Section).
- İkisinde de Anchor linki (buton → sayfa içi bölüm) çalışıyor.
- İkisinde de görsel/köşe yuvarlatma (corner radius) hem konteynere hem içindeki görsele AYRI AYRI verilmeli — sadece konteynere corner verip içine görsel eklenirse köşe yuvarlaklığı kaybolur, görsele de ayrıca corner radius verilmesi gerekir.

### Farklar
| Özellik | Editor | Studio |
|---|---|---|
| Konumlandırma | Sürükle-bırak (manuel), padding/margin kavramı sınırlı | Sağ panelden piksel bazlı, padding/margin/stack tam kontrol |
| Header/Section boyutlandırma | Manuel sürükleme ile | Sayısal değerlerle, Fit to Screen gibi araçlarla |
| Animasyon çeşitliliği | Sınırlı (birkaç hazır animasyon), üst üste animasyon zor | Çok daha zengin (Custom Animation ile özel büyüme/dönme/renk değişimi tanımlanabilir), birden fazla animasyon üst üste (element bazlı + toplu section bazlı) verilebilir |
| Chatbot açılıp-kapanma animasyonu | Kodsuz yapılamaz — HTML/kod gerekir | Kodsuz, Click Animasyonu ile yapılabilir (Fade Show/Hide) |
| Özel etkileşim elementi | **HoverBox** (Tool panelinden) — Regular/Hover iki durumlu, görsel/renk/metin/efekt her durum için ayrı tanımlanabilen hazır kutu | Böyle özel bir "HoverBox" aracı yok, benzer etki manuel animasyon kombinasyonlarıyla elde edilir |
| Responsive (tablet/mobil) | Ayrı görünüm düzenleme sınırlı | Tam responsive kontrol, her ekran boyutu ayrı ayrı test edilip düzenlenebilir |

### Değerlendirme Notu
- Her iki araç da eşit değerlendiriliyor — hangisi kullanılırsa kullanılsın önemli olan doğru/tutarlı uygulama.
- Eğitmen kişisel tercih olarak Studio'yu öneriyor (daha "keyifli" ve kontrol edilebilir bulunuyor) ama zorunluluk yok.

## 8. Custom Animation (Studio) — Detaylı Örnek

1. Bir görsel/kart seçilir, **Hover → Custom Animation** eklenir (örn. %110 büyüme, 0.5 saniye).
2. Birden fazla element seçilip **Stack** yapıldıktan sonra, TÜM GRUBA ayrı bir animasyon (scroll, mouse-follow, hover, renk değişimi) verilebilir — hem tek tek elementlerin hem grubun kendi animasyonu aynı anda çalışabilir.
3. Farklı animasyon türleri (Loop, Mouse Effect, dönme, kayma) denenip publish edilerek test edilir.

## 9. Şablon Sayfasını Değiştirme (Pratik Örnek)

- Bir sayfa (örn. hazır şablonun "Hakkımızda" sayfası) çok karmaşık/beğenilmediyse: **Manage Pages'ten o sayfa silinir + menüden otomatik kalkar → yeni bir boş veya farklı şablondan sayfa eklenir → Manage Menu'den yeniden menüye bağlanır.** Bu şekilde şablonlar karışık kullanılabilir, istenmeyen karmaşık sayfalar sadeleştirilebilir.

## 10. Marka Başlatma Belgesi — Genel Akış Hatırlatması (Kapanış Özeti)

Sıra: İsim/sektör/hizmet tanımı → Görsel kimlik tercihleri → Tipografi (font pairing araçlarıyla, örn. Fontpair.co üzerinden Montserrat'a uygun font bulma) → Kurumsal kimlik kılavuzu (açılış sayfası → renkler → logo orijinal/negatif kullanım → serbest alan → minimum boyut testi → tipografi kaydı → antetli kağıt + kartvizit) → Wix (Editor veya Studio, Harmony DEĞİL) → site (Ana Sayfa, Hakkımızda, Hizmetlerimiz, Bize Ulaşın + Chatbot + Yönetim Paneli).

## 11. Sonraki Gün İçin
- Eğitimin son günü — kalan iki konu başlığı işlenecek.
- Öğrencilerden gün boyunca takıldıkları/unuttukları noktaları mail ile iletmeleri istendi; son gün açılışında toplu tekrar yapılacak.
