# Gün 8: Chatbot, Yönetim Paneli, Input Alanları (Wix Uygulamalı)

## 1. Logo Minimum Boyut Testi — Tekrar/Netleştirme

- Sabit bir "maksimum" değer yok — sadece **minimum boyut** kavramı var, logoya göre değişken.
- Yöntem: Figma'da ekran görünümü **%100'de** tutulur. Logo yavaşça küçültülür. Ekran hep %100'de kalır (yakınlaştırma yapılmaz). En küçük detayın (nokta, ince çizgi vb.) okunamaz/seçilemez hale geldiği nokta = logonun minimum kullanılabilir boyutu.
- Bu değer logonun formuna göre değişir; ince çizgili/çok detaylı logolarda minimum boyut daha büyük olur.

## 2. Şerit / Dönen Logo Galerisi (Pro Gallery — Detaylandırma)

1. Yeni bir **section** açılır, **Fit to Screen** yapılır, sonra istenen yüksekliğe (örn. 240px) küçültülür.
2. **Add → Media → Pro Gallery** eklenir, section'a **Stretch** ile tam genişliğe yayılır.
3. Pro Gallery'nin **Settings → Layout → Slider** seçilir.
4. **Manage Media → Select All → Delete** ile varsayılan görseller silinir, kendi logo/görsel setiniz yüklenir.
5. **Customize Layout:** Loop (sürekli döngü) açılır, hız ayarlanır, "Pause on Hover" istenirse işaretlenir, Spacing sıfırlanabilir (boşluksuz şerit için).
6. Bu yöntemle iş ortağı logoları, marka görselleri veya herhangi bir içerik şerit halinde döndürülebilir.

## 3. KVKK Metni Ekleme — Alt Sayfa Olarak

1. Yeni sayfa açılır (KVKK).
2. Menüye eklenir (**Manage Menu → Add Item**).
3. Menüde KVKK item'ı, "Hakkımızda" item'ının üzerine sürüklenip sağa kaydırılarak onun **alt sayfası (sub-page)** haline getirilir.
4. Yayınlanıp kontrol edilir; bozulmalar varsa (stack/scale proportionality) düzeltilir.

## 4. Chatbot Tasarımı — Adım Adım (Açılır/Kapanır Buton Tipi)

### Buton Hazırlığı
1. Bir **buton** eklenir ("AI Asistan" vb.), **Scale Proportionality** yapılır (Fixed değil).
2. Boyut ayarlanır (örn. 48px yükseklik, 180px genişlik).
3. Buton **sayfaya pinlenir**: `Position → Position Type → Pin → Page`.
4. Pin sonrası kenar mesafeleri (margin) sıfırdan girilir (örn. sağdan 24px, üstten/alttan 24px) — göz kararı sürükleme yapılmaz.

### Chat Paneli Yapısı (İç İçe Konteyner Mantığı)
1. **Dış konteyner** eklenir (örn. 320x400px) — chat panelinin tüm alanı.
2. İçine **padding** verilir (örn. 28px her yönden).
3. İçine bir **başlık konteyneri** eklenir (üstte sabit, "AI Asistan" yazısı + opsiyonel SVG ikon).
4. **Kritik kural: Kod SADECE İÇ konteynere bağlanmalı, dış konteynere değil.** Dış konteynere kod bağlanırsa yazılar taşar ve tasarım bozulur.
5. Yazışmaların akacağı **iç konteyner** eklenir — buraya **Overflow Content → Scroll** ayarı verilir (taşan içerik kaydırılabilir olur, sabit alanı bozmaz).
6. Altına **Input** (mesaj yazma alanı, 48px, Scale Proportionality) ve **Buton** (gönder, sağa-alta sabitlenmiş) eklenir.
7. Tüm elementler birbirine **Stack** ile bağlanır (aralarındaki mesafe piksel olarak sabitlenir).
8. **Chatbot rengi/görünümü:** Glass effect (camsı/buzlu cam görünümü) ve corner radius ile modern bir görünüm verilebilir.

### Açılıp Kapanma Animasyonu (Kodsuz)
1. Butona tıklanır → sağ panelde **Animation (şimşek ikonu) → Click (Tıklama) animasyonu** seçilir.
2. **Animated Element** olarak iç panel konteyneri seçilir (`Choose on Canvas` ile mavi çerçeveden doğru elementi bulmak gerekir).
3. Efekt olarak **Fade (Belirip Kaybolma)** seçilir — Gizle/Göster mantığı.
4. Publish edilip test edilir: butona tıklayınca panel açılır/kapanır.

### Test Kriterleri
- Ekran küçültülüp büyütülerek (responsive test) chatbot'un pozisyonunun her boyutta doğru kalması kontrol edilir — mobilde, tablette, web'de aynı davranış beklenir.

## 5. "Bir Konteyner İçine Bir Konteyner Daha Atmayın" Kuralı — Pekiştirme

- Chatbot'un iç panelini oluştururken sadece TEK konteyner kullanılmalı (üstüne bir konteyner daha eklenmemeli) — aksi halde kod bağlantısı iki ayrı katmana bölünür, hangi katmanın neyi taşıdığı karışır, silme/düzenleme sırasında hatalar oluşur.

## 6. Ana Sayfada Chatbot mı, Açık Chat Paneli mi?

- Eğer ana sayfaya (veya herhangi bir sayfaya) **sürekli açık (pinlenmemiş, sabit görünür) bir chat paneli** yapılırsa, o sayfaya ayrıca açılır-kapanır chatbot butonu koymaya gerek yok — ikisi aynı işi görür.
- Açık chat paneli olmayan TÜM diğer sayfalarda chatbot (açılır/kapanır buton) bulunmalı.
- Bir elementi (chatbot butonu gibi) başka bir sayfaya kopyaladığınızda **pin ayarları sıfırlanır** — Position/Pin ayarlarını yeni sayfada yeniden yapmak gerekir.

## 7. Yönetim Paneline Veri Toplama — Form Elementi KULLANMAYIN

### Neden Wix'in Hazır "Form" Elementi Kullanılmaz?
- Wix'in kendi "Form" bileşeni eklenip veri girildiğinde, bu veriler kodlanan yönetim paneline DEĞİL, Wix hesabına kayıtlı e-posta adresine düşer — bu eğitim kapsamındaki amaca (kendi kodlanan dashboard'a veri akışı) hizmet etmez.
- Bu yüzden "Form" yerine **manuel Input elementleri** kullanılarak kendi form yapınız kurulur.

### Manuel Form Oluşturma Adımları
1. Her alan için ayrı **Input** elementi eklenir (İsim Soyisim, E-posta, Telefon Numarası, Mesaj/Not vb.) — her biri farklı input tipinden kopyalanıp **Settings**'ten placeholder metni değiştirilir.
2. Her input **Scale Proportionality** yapılır, boyutu (48px), yerleşimi (sola/yukarı sabitleme) ayarlanır.
3. Tüm input'lar **Stack** ile birbirine bağlanır, aralarındaki mesafe (örn. 20-28px) sabitlenir.
4. Sonuna bir **Gönder/Demo Talep Et** butonu eklenir — o da Scale Proportionality, boyutu diğer inputlarla uyumlu, stack'e dahil.
5. Tüm form bir hücrenin içine padding ile yerleştirilir, taşma önlenir.
6. Yayınlanıp test edilir — bozulma varsa scale/stack ayarları tekrar gözden geçirilir.

## 8. Yönetim Paneli (Dashboard) Sayfası — Yapı

### Genel İskelet
- Üst bilgi (header benzeri) bölümü: logo + sayfa başlığı ("Müşteri Adayı Yönetim Paneli") + arama input'u + buton(lar) (Yenile, Karşılama Sayfası vb.) — her biri ayrı stack ile hizalanır.
- Alt bölüm iki hücreye ayrılır (Grid Layout): sol/geniş hücre = **müşteri adayları tablosu (Repeater)**, gerekiyorsa üstte özet kartlar (toplam lead, bugünkü lead vb.).

### Repeater Kullanımı
- **Repeater**, kod tarafından tekrar eden verilerin (her bir müşteri kaydı gibi) görüntülendiği ana bileşendir.
- Repeater bir konteynerin içine yerleştirilir, konteynere padding verilir, corner radius eklenebilir.
- İstatistik kartları da benzer mantıkla: konteyner içine stack'lenmiş küçük kartlar (örn. "Toplam Lead: 0", "Bu Ay: 0") — kod bağlanmadıysa temsili/statik gösterilebilir.

### Karşılama Sayfası Bağlantısı — İki Yaklaşım
- **Ayrı sayfa yaklaşımı** (Next Play örneğindeki gibi): Chat + veri toplama formu ayrı bir "Karşılama Sayfası" olarak yapılır. Bu durumda Yönetim Paneli sayfasına "Karşılama Sayfasına Dön" butonu eklenmesi gerekir.
- **Bölüm (section) yaklaşımı:** Chat + form, ana sayfanın bir bölümü olarak eklenir. Bu durumda ayrı buton gerekmez ama Yönetim Paneline erişim için ayrı, görünür bir buton (menüye eklenmeden) konabilir.

### Anchor (Sayfa İçi Yönlendirme) ile Buton Bağlama
- Bir buton, aynı sayfadaki belirli bir section'a **Link → Anchor** ile bağlanabilir — tıklanınca sayfa o bölüme otomatik kayar (örn. "Daha Fazlası" butonu chat/form bölümüne kaydırır).
- Yönetim Paneline giden bir buton da benzer şekilde **Link → Page → Yönetim Paneli** olarak bağlanır — sunumda jüriye canlı gösterim için pratiktir (normal kullanıcı akışında bu buton gizlenebilir/kaldırılabilir).

## 9. Genel Test Akışı (Sunum Provası)

Örnek uçtan uca akış:
1. Ana sayfa açılır, menü test edilir (Hakkımızda, Hizmetler/Çözümler).
2. Chatbot açılıp kapatılır (diğer sayfalarda).
3. Sayfa içinde bir butona tıklanır → anchor ile ilgili bölüme (chat/form alanı) kayar.
4. Form alanına bilgiler girilir, chat'te bir soru sorulur (yapay zeka cevap verir — kod bağlıysa).
5. "Yönetim Paneli" butonuna tıklanır → panel sayfası açılır.
6. Girilen bilgilerin panelde (Repeater'da) göründüğü kontrol edilir.
7. Bu akış eksiksiz çalışıyorsa jüri sunumu için temel yapı tamamlanmış sayılır.

## 10. Genel Prensip — Tekrar Vurgulanan Kurallar

- **Hiçbir şeyi elle/göz kararı sürüklemeyin** — her zaman sağ paneldeki sayısal değerlerle (padding, margin, boyut) çalışın.
- **Her yeni bölüm için ayrı section/hücre** açın, birbirine karışmasın.
- **Scale Proportionality** her element için kontrol edilmeli (Fixed unutulmuş elementler responsive testte bozulmanın en sık nedeni).
- **Stack** kullanarak elementleri gruplayın — böylece aralarındaki mesafe her ekran boyutunda korunur.
- Her önemli adımdan sonra **Publish edip test edin** — biriktirmeyin, hatanın kaynağını unutmayın.
- Kendi kendine bir sayfa + chatbot yapısı üzerinde pratik yapmak, Belgrad'daki yoğun günlerde büyük kolaylık sağlıyor (önceki dönemlerin geri bildirimi).

## 11. Sonraki Gün İçin
- Editor'de çalışma devam edecek.
- Eklenmesi gereken ek detaylar konuşulacak.
- Ardından eğitimin son gününe geçiş yapılacak.
