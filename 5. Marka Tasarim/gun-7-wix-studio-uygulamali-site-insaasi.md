# Gün 7: Wix Studio Uygulamalı Site İnşası

## 1. Zorunlu Sayfa/Bölüm Akışı — Netleştirme

- **Ana sayfa:** Kullanıcıyı karşılayan ilk yüz.
- **Hakkımızda:** Markanın yazınsal anlatımı (marka değeri, kapsamı, hangi soruna çözüm olarak doğduğu).
- **Ürünler/Hizmetler/Çözümler:** Yapılan işi SOMUT gösteren bölüm — kullanıcının web sitesinde "ikna olacağı" kısım. Sektöre göre içeriği değişir (ürün markası → "Ürünlerimiz", hizmet markası → "Hizmetlerimiz", dijital marka → "Çözümlerimiz").
- **Chatbot:** Her sayfada bulunmalı (ana sayfa istisna olabilir — bkz. aşağı), açılıp kapanabilir ya da sürekli açık (pin'li) olabilir. HTML gömülerek veya Wix'in kendi araçlarıyla yapılabilir.
- **Yönetim Paneli (Dashboard):** Form/chatbot'tan gelen verilerin (Repeater ile) düştüğü sayfa — zorunlu, olmadan olmaz.
- **KVKK metni:** Mutlaka bir yere iliştirilmeli (Hakkımızda altına, footer'a tıklanır link olarak vb.) — nerede olduğu serbest, olması zorunlu.

### Chatbot Yerleşim Esnekliği
- Eğer ana sayfaya sürekli açık (daimi/pin'li) bir chat alanı yapılırsa, o sayfada ayrıca tıkla-aç/kapa chatbot'a gerek yok — aynı işi görüyorlar, tekrar gereksiz.
- Diğer sayfalarda tıkla-aç/kapa chatbot kullanılabilir.
- Bilgi toplama (dashboard'a veri çeken input alanı) "Bize Ulaşın" sayfasında, ana sayfanın altında bir bölüm olarak, veya ayrı bir "karşılama sayfası" olarak yapılabilir — tasarımcının tercihi, hepsi kabul.

## 2. Sunum Akışı Örneği (Next Play Üzerinden)

Jüri sunumunda izlenecek sıra örneği:
1. Ana sayfa tanıtımı (marka odağı, multistate box gibi bileşenler)
2. Chatbot gösterimi
3. Hakkımızda (marka hikayesi)
4. Hizmet/Çözüm sayfası
5. Dashboard (form doldurma → panele düşme testi canlı gösterilir)
6. KVKK metni gösterimi

## 3. Tasarım Değerlendirme Kriterleri (Mentör Gözünden)

- Kullanıcıyı net yönlendiren, "bet sitesi" gibi olmayan profesyonel akış.
- Buton boyutlarının okunabilir olması.
- Marka renklerinin siteye (Site Style) kayıtlı olup olmadığı.
- Responsive ayarların (ekran küçülüp büyüdüğünde bozulmama) doğru çalışması.
- Koyu arka planlarda buton/metinlerin okunabilir kalması — projeksiyona yansıtıldığında da test edilir.
- Tutarlılık: tüm başlıkların aynı font ailesinden, logonun her sayfada entegre ve okunaklı olması.

## 4. Site Renklerini Kaydetme — Stüdyo

### Yöntem
1. **6013-benzeri renk üretici site** (60-30-10 Color Generator) kullanılarak marka renginden uyumlu palet üretilir.
2. Wix Studio'da **Site Style (Theme)** paneline gidilir:
   - **Birincil renk (Color 1):** Genelde arka plan/en baskın kullanılan renk.
   - **İkincil renk:** Kartların arka planı için.
   - **Buton renkleri (Color 6/7 vb.):** Marka renginden (örn. logo moru).
   - **Text color(ler):** Ana metin rengi + gerekirse ikinci bir text rengi (koyu arka planlarda okunabilirlik için).
   - Renk tramlarından (ton varyasyonları) buton "hover" (üzerine gelme) durumunda kullanılacak renk de eklenir.
3. Bir kez kaydedilen renkler, sonradan çağrılan her şablon bölümünde OTOMATİK uygulanır — manuel renk değiştirmeye gerek kalmaz.

### Editor'de Aynı İşlem
- Editor'de "Site Design → Color Theme" bölümünden Base Color (arka plan) ve Accent Colors (buton/vurgu renkleri) eklenir — mantık aynı, arayüz farklı.

## 5. UI Prensibi — Primary Button Tutarlılığı

- Bir web sitesinde EN önemli aksiyon butonuna "primary button" denir (örn. "Devam Et", "Sepete Ekle").
- Kural: primary button HER SAYFADA aynı renk, aynı boyut, aynı biçimde olmalı (Amazon örneği: "Devam Et", "Alışverişe Başla", "Sepete Ekle" hep aynı turuncu/boyut).
- Hover durumundaki renk de tüm sayfalarda tutarlı olmalı.

## 6. Fontları Kaydetme — Type Scale ile

### Stüdyo Akışı
1. Site Style → Typography bölümünde iki font slotu var (Heading fontu + Paragraph fontu).
2. Kurumsal kimlikte belirlenen fontlar (örn. Geist = başlık, Space Grotesk = paragraf) buraya yüklenir.
3. **Type Scale (type-scale.com)** aracı kullanılarak H1'den H6'ya kadar piksel boyutları ve satır yüksekliği (line-height, genelde 1.5) hesaplanır.
4. Her başlık seviyesine (H1-H6) ayrı ayrı: font ağırlığı (Extra Bold/Bold/Semibold/Medium), boyut, satır yüksekliği, renk atanır — büyük başlıktan küçüğe inildikçe ağırlık da genelde azaltılır (H1: Extra Bold → H6: Medium).
5. Paragraf metinleri (Paragraph 1/2, Quote, Description) için de benzer şekilde: 16px/14px/12px, Regular ağırlık.
6. Bir kez tanımlandıktan sonra, sayfaya eklenen her H1/H2/paragraf elementi otomatik doğru font+boyut+renk ile gelir — manuel ayar gerekmez.

### Editor'de Aynı İşlem
- "Customize Heading Style" ve "Customize Paragraph Style" panelleriyle aynı mantıkla H1-H6 ve Paragraph 1/2 tanımlanır.

## 7. Şablon (Template) Kullanımı — Pratik Uygulama

- Boş sayfaya (kendi site renginiz/fontunuz kayıtlıyken) başka bir şablondan bölüm kopyalanıp yapıştırıldığında (Ctrl+X / Paste), o bölüm OTOMATİK marka renklerine ve fontlarına uyarlanır.
- Bu sayede farklı şablonlardan beğenilen bölümler bir araya getirilip özgün bir site oluşturulabilir — "tasarım bulamıyorum" sorunu bu şekilde aşılabilir.

## 8. Section (Bölüm) Mantığı — Kritik Kural

- **Her yeni içerik alanı için AYRI bir section açılmalı.** Tüm sayfayı tek bir dev section içine sığdırmak (örn. tek section'ı 1200px+ genişletip her şeyi içine tıkıştırmak) işleri çok zorlaştırır, hata riski artırır.
- Bir section'a tıklandığında mavi renkte gösterilir (hem Editor hem Studio'da).
- Section içinde "Section Layout" ile istenen düzene (2'li, 3'lü, 4'lü grid vb.) bölünebilir.
- Yanlış giden bir bölüm silinip yeniden yapılabilir — üstteki/alttaki section'lara zarar vermez (her section bağımsız).

## 9. Fit to Screen (Ekrana Yayma)

- Bir görsel/video'nun tam ekranı kaplaması isteniyorsa, önce SECTION "Fit to Screen" yapılır (section'ı %100 ekran yüksekliğine sabitler).
- Ardından içindeki medya elementi "Stretch" ile section'a yayılır.
- Video/görsel için "Focal Point" (odak noktası) belirlenir — kırpıldığında hangi kısmın öncelikli görüneceğini belirler.

## 10. Konteyner (Container) Kullanım Kuralları

- **Gereksiz iç içe konteyner atmayın** — kod bağlantısı karışır, silme/düzenleme zorlaşır.
- Bir elemente kod bağlandıktan sonra silinirse kod bağlantısı kopar (dün öğrenilen kural, tekrar vurgulandı).
- Metin/görsel eklerken önce konteyner eklenir, içine padding (iç boşluk) verilir, SONRA içerik (Add Media/Text) eklenir — bu sıra taşma/bozulma sorunlarını önler.
- Hangi katmanda olduğunuzu anlamak için: elemente tıklarken ekranın alt köşesindeki breadcrumb (Section > Cell > Container > Text) takip edilir.
- Bir elementi taşırken göründüğü MAVİ ÇİZGİLER, nereye ekleneceğini gösterir — bu çizgileri takip ederek doğru konuma bırakılır.

## 11. Padding / Margin / Scale Proportionality — Responsive'in Temeli

- **Padding (iç boşluk):** Bir konteyner/hücrenin kendi içindeki kenar boşluğu — içerik konteynerin sınırına yapışmasın diye.
- **Margin (kenar boşluğu / mesafe):** Elementin sayfanın kenarına veya diğer elementlere olan mesafesi.
- **Scale Proportionality vs Fixed:** Elementler (görsel, buton, text) FIXED (sabit) yerine SCALE PROPORTIONALITY (orantılı ölçeklenen) olarak ayarlanmalı — aksi halde ekran boyutu değiştiğinde (tablet/mobil/farklı monitör) yapı bozulur.
- **Test yöntemi:** Tarayıcı penceresini fare ile küçültüp büyüterek yapının bozulup bozulmadığı sürekli kontrol edilmeli ("responsive test" — her element için ayrı ayrı yapılmalı).
- Header yüksekliği genelde 90-120px arası tutulur ve sabitlenir.

## 12. Stack (Oto-Layout Benzeri Yapı)

- Figma'daki "Auto Layout"un Wix karşılığı **Stack**'tir.
- Birbirine bağlı/aynı hizada kalması gereken elementler (örn. başlık + alt başlık + buton) seçilip "Stack" yapılır — aralarındaki boşluk (spacing) piksel olarak sabitlenir, elementler otomatik hizalanır.
- Stack sonradan bozulabilir ("Unstack" / "Yığını Dağıt") ama genel kural: mümkün olduğunca stack kullanmak, sürükle-bırak ile serbest konumlandırmaktan kaçınmak.

## 13. Grid Layout (Hücre Sistemi)

- Section içinde "Grid Layout" ile hazır düzenler (2'li/3'lü/4'lü sütun vb.) seçilebilir.
- Hücreler birleştirilebilir (Shift ile seçip "Merge") veya bölünebilir (Split Horizontal/Vertical) — hazır grid şablonlarına bağlı kalmak zorunlu değil, özgün düzen kurgulanabilir.
- Her hücreye ayrı padding verilerek kartlar arasında tutarlı boşluk bırakılır (örn. 24px tüm kenarlardan).

## 14. Menü (Navigation) Oluşturma

1. Header'a "Menu" elementi eklenir — dikey/yatay/hamburger/ankor gibi tipler mevcut, web'de klasik yatay menü öneriliyor.
2. Sayfalar önce "Manage Pages" ile oluşturulur (Ana Sayfa, Hakkımızda, Hizmetlerimiz ve Çözümlerimiz, Bize Ulaşın vb.).
3. **Kritik:** Sayfalar menüye OTOMATİK eklenmez — menü üstüne tıklanıp "Manage Menu → Add Item" ile her sayfa manuel eklenmeli.
4. Menü item'ların "Regular" ve "Hover" durumdaki renkleri ayrı ayrı ayarlanabilir (Site Style'da kayıtlı renklerden seçilerek).
5. **Set Homepage:** Sitenin açılış sayfası mutlaka "Ana Sayfa" olarak ayarlanmalı (ev ikonu ana sayfanın yanında görünmeli) — yanlışlıkla başka bir sayfa ana sayfa yapılmışsa link paylaşıldığında kullanıcı yanlış sayfadan başlar.
6. Logoya tıklanınca ana sayfaya dönmesi için logo elementine "Link → Page → Home" bağlanabilir (zorunlu değil ama önerilir).

## 15. Input (Girdi) Alanları

- Form/arama input'ları Wix'in hazır "Input" elementiyle eklenir, Settings'ten placeholder metni değiştirilir.
- Genelde input ve buton yüksekliği 48px tercih edilir.
- Input da diğer elementler gibi Scale Proportionality ve padding/margin kurallarına tabi.

## 16. Video/Görsel Ekleme ve Düzenleme

- **Video ekleme:** Add → Media → Video Box/Video Player, ardından "Upload Media → From Computer" ile video yüklenir, section'a "Add to Page" ile eklenir, Stretch ile tam ekrana yayılır, Focal Point ile odak noktası belirlenir.
- **Görsel ekleme:** Add Media → Upload from Computer veya Wix'in kendi stok görsel kütüphanesi / Unsplash eklentisi kullanılabilir.
- **Adjust (Ayarla) paneli:** Yüklenen görselin parlaklık/kontrast/doygunluk (saturation) değerleri değiştirilebilir — Saturation'ı sıfırlamak görseli siyah-beyaz yapar.
- Video, tıklanınca durdurulabilir (pause) — bu davranış hem editörde hem yayınlanan sitede aynı şekilde çalışır.

## 17. Dönen Görsel/Logo Şeridi (Pro Gallery / Slider)

1. Add → Media → **Pro Gallery** eklenir.
2. Pro Gallery üstüne tıklanıp Settings açılır.
3. **Layout → Slider** seçilir.
4. "Customize Layout" içinde **Loop** (otomatik sürekli döngü) açılır, hız ayarlanır, "Pause on Hover" isteğe bağlı işaretlenir, "Spacing" sıfırlanabilir (boşluksuz şerit görünümü için).
5. Görseller manuel değiştirilebilir (Manage Media → Select All → Delete → yeni görseller/video eklenir).
6. Bu yöntem hem görsel şeridi hem logo/marka şeridi (logo carousel) yapmak için kullanılabilir.

## 18. Footer (Alt Bilgi) Oluşturma

- Section paneline gidilip hazır bir footer düzeni seçilebilir, logo/renk/yazı markaya göre özelleştirilir.
- **Herhangi bir section'ı Footer yapmak için:** Section'a sağ tıklanır → "Set as Global Footer" seçilir — bölüm yeşil çerçeveli olur ve her sayfada otomatik görünür hale gelir.
- Aynı mantıkla bir section "Global Header" da yapılabilir.

## 19. Animasyonlar (Studio)

- Element seçilip "Animation" panelinden giriş animasyonu (Slide, Float vb.) eklenir; süre (örn. 1.5 saniye) ve gecikme (örn. 0.3 saniye) ayarlanabilir.
- Her element (başlık, alt başlık, buton, kart, konteyner) ayrı ayrı animasyonlandırılabilir — tutarlı bir "giriş" hissi için genelde hepsine benzer animasyon (Slide/Float) uygulanır.
- Buton hover animasyonları da (üzerine gelince büyüme/renk değişimi) kodsuz eklenebilir.

## 20. Anchor (Sayfa İçi Bağlantı)

- Bir butona (örn. "Daha Fazlası") tıklandığında aynı sayfanın belirli bir bölümüne (section) kaydırma yapılabilmesi için "Link → Anchor" ile ilgili section'a bağlanır — sayfa değiştirmeden akıcı gezinme sağlar.

## 21. Genel Çalışma Önerisi

- Her sayfa/bölüm bitirildikçe "Publish" edip test etmek, tüm işi bitirdikten sonra tek seferde kontrol etmekten çok daha güvenli — hata kaynağını hatırlamak/bulmak kolaylaşıyor.
- Ekran boyutunu manuel küçültüp büyüterek yapılan "responsive test" her önemli düzenlemeden sonra tekrarlanmalı.
- Wix Studio, Editor'e göre daha güçlü ama öğrenme eğrisi biraz daha uzun — sağ paneli (padding/margin/scale/stack) doğru kullanmayı öğrenmek anahtar.

## 22. Sonraki Gün İçin
- Editor'de örnek sayfa yapımı.
- Yönetim panelleri ve chatbot'ların detaylı kurulumu.
- Buton/element tutarlılığının pratikleri devam edecek.
