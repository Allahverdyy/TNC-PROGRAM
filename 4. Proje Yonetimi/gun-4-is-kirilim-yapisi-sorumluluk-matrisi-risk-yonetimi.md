# Proje Yönetimi — Gün 4: İş Kırılım Yapısı (WBS), Sorumluluk Matrisi (RACI), Risk Yönetimi

Eğitmen: Tuğçe Hanım

## İş Kırılım Yapısı (WBS)

- Amaç: proje bütününü/ana faaliyetlerini yönetmek, maliyet tahmin etmek zor olduğu için işleri **küçük, yapılabilir parçalara (lokmalara)** bölmek.
- **Ekiple birlikte yapılır** (A diyagramı gibi tek başına değil) — fiziksel/sanal ortamda ekip bir araya gelip post-it'lere görevleri yazar, sınıflandırılır.

### Kurallar

1. En üst kutucuğa **projenin temel çıktısı** yazılır.
2. Bir alt seviyeye **ana faaliyetler** yan yana yerleştirilir.
3. Her ana faaliyet detaylandırılarak aşağı inilir — seviyeler **içerik/detay bakımından** dengeli olmalı (bir dalda çok detaya inip diğerinde genel bırakmak yanlış).
4. Yeterli ayrıntıya ulaşana kadar bölme devam eder.
5. Etiketleme: 1, 1.1, 1.2 şeklinde numaralandırma.
6. Bazen bir dalın diğerlerinden daha fazla detay gerektirdiği durumlarda **çıkıntılı ek seviye** (ör. 1.2.n1) eklenebilir — ayrıntı seviyesi tutmuyorsa yan sütunlara yazılmaz, ayrı bir dal olarak gösterilir.

### Proje Tipine Göre Farklılık

- **C/D tipi büyük projeler**: detaylı, çok seviyeli WBS gerekir.
- **A/B tipi küçük projeler**: daha az ana faaliyet, daha sığ WBS yeterli.
- **Çok büyük/uzun projelerde**: WBS'i proje fazlarına (girişim, uygulama, kapanış) göre ayrı ayrı hazırlamak mantıklı olabilir — her fazı ayrı bir "mini proje" gibi ele alıp kendi WBS'ini çıkarmak.

## Sorumluluk Matrisi (RACI)

- Ekipteki kişilerin roller/sorumluluklarını, kime bağlı/kime hesap verildiğini netleştiren tablo — iletişimi güçlendirir, sınırları çizer.

### RACI Harfleri

- **R (Responsible/Sorumlu)**: görevi fiilen yapan, aktif rol alan kişi. Soru: "Görevi kim yapacak?"
- **A (Accountable/Hesap Veren)**: görevin sonucundan hesap veren kişi (genelde yönetici) — doğrudan uygulama sorumluluğu yok ama nihai sonuçtan sorumlu. Soru: "İşler ters giderse kime hesap sorulur? Karar yetkisi kimde?"
- **C (Consulted/Danışılan)**: görevle ilgili bilgi/uzmanlık sağlayan, karar aşamasında danışılan kişi.
- **I (Informed/Bilgilendirilen)**: görevin durumu hakkında bilgilendirilmesi gereken ama aktif rolü olmayan kişi.
- (Bazı organizasyonlarda ek olarak **S (Support/Destekleyen)** de kullanılabilir — az görülür.)

### Uygulama Notu

- Bir görevde birden fazla kişiye **R** (birlikte sorumlu/çalışan) verilebilir ama genelde **A (hesap veren)** tek kişi olmalı.
- Bazen kişi kendine A + C (hem hesap veren hem danışılan) verebilir — görev proje yöneticisinden bağımsız ilerleyen bir süreçse.

---

## Örnek Uygulama: İK-Ekip Yönetimi ve İletişim Planı

Belgrad'da teslim edilecek bir belge. Yapı:

1. **Personel kaynağı ve yetenekleri** — her rol için (proje yöneticisi, geliştirici, test uzmanı vb.) gereken yetkinlikler alt madde madde açıklanır (liderlik yetenekleri, yönetim yetenekleri, teknolojik yetenekler, ekip koordinasyon yetenekleri).
2. **Ekip dinamikleri**:
   - **İletişim stilleri** — her rolün iletişim tarzı tanımlanır (ör. proje yöneticisi = açık/doğrudan iletişimci, geliştirici = teknik terimleri sadeleştiren, test uzmanı = detaylı/sistematik).
   - **İletişim engelleri ve çözüm önerileri** — (ör. teknik jargon anlaşılmaması → basitleştirme + eğitim).
   - **Çatışma yönetimi** — olası çatışma noktaları (hedef yanlış anlaşılması, görev dağılımı adaletsizliği) + çözüm stratejileri (düzenli toplantı, açık geri bildirim kültürü, performansa dayalı ödül).
   - **Motivasyon ve işbirliği** — başarıların tanınması, mesleki gelişim fırsatları, sosyal etkinlikler, ortak hedef belirleme.
   - **Esneklik ve adaptasyon** — alternatif planlar/kriz yönetimi, ekibi değişim sürecine dahil etme.
3. **Toplantılar ve iletişim kanalları** — haftalık durum toplantıları, aylık strateji toplantıları, kanal seçimi (email, Slack, Trello).
4. **Hedef belirleme ve takip** — periyodik performans değerlendirme (ör. 360 derece geri bildirim), gelişim planı bağlantısı.
5. **Ekip gelişimi** — eğitim programları (yazılım geliştirme teknikleri, veri analizi, iletişim, çatışma çözümü — atölye/workshop şeklinde), mentorluk (deneyimli-yeni ekip üyesi eşleştirme, koçluk seansları, performansa dayalı gelişim planı).

---

## Örnek Uygulama: Risk Analizi ve Yönetim Formu

### Bölüm 1: Risk Faktörleri Listesi

- Serbest listeleme — her biri **bir olasılık** olmalı, kesinlik içeren durumlar risk sayılmaz.
- Örnek (yazılım projesi): teknik yetersizlik, zamanında teslim edilmeme, bütçe aşımı, güvenlik açıkları, yazılım hataları, ekip üyesi değişikliği, müşteri beklenti değişimi, teknolojik değişiklik, yetersiz test süreçleri, kapsam değişikliği.

### Bölüm 2: Risk Değerleme Matrisi (Nicel)

Sütunlar: Risk No, Risk Faktörü, **Olasılık** (1-5), **Etki** (1-5), **Önem Düzeyi** (= Olasılık × Etki).

- Önem düzeyi en yüksek olan riskler önceliklendirilir.
- Eşit skorlarda ek kriter kullanılır: düşük olasılık + yüksek etki olan riskler yakından izlenmeli (olasılık artışına karşı); benzer skorlarda müşteri etkisi büyük olan öncelikli alınır.

### Bölüm 3: Tepki Planı

Her risk faktörü için **birden fazla önlem/çözüm** yazılır (tek çözüm yetmez).

### Bölüm 4: Detaylı Tehlike-Önlem Tablosu

Sütunlar: Faaliyet/Risk, **Olası Tehlike**, **Var Olan Önlem**, **Önlemin Zaafı**, **Önlem Sonrası Risk Düzeyi** (düşük/orta/yüksek), **Riskin Oluşması Durumunda Yapılacak Faaliyet** (yedek plan).

- Her önlemin kendi zayıf noktası (zaafı) olduğu kabul edilir ve ayrıca not edilir — bu, çok katmanlı risk yönetiminin özü.

---

## Risk Yönetimi (Kavramsal Çerçeve)

### Risk Tanımı

- Risk = bir **olasılık**. Gerçekleşeceğinden emin olunan bir durum risk sayılmaz, risk yönetimi kapsamına girmez.
- Olumlu da olabilir (fırsat), olumsuz da (tehdit) — "krizi fırsata çevirmek" mantığı.

### Grup Egzersizi: Risk Örnekleri (Katılımcı Yanıtları)

- Zamanında yetiştirememe, müşterinin projeyi beğenmemesi, önceden alınmayan önlemler nedeniyle sonradan fark edilen hatalar, ekip içi çözülemeyen anlaşmazlıklar, yeni teknoloji benimseme riski (hem olumlu hem olumsuz olabilir), bütçe aşımı, kritik roldeki kişiyi kaybetme, sapmalardan kaynaklı bilgi sızması/rakibin fikri çalması, üçlü kısıtın (zaman-maliyet-kapsam-kalite) olumlu/olumsuz yönde oynaması, projenin toplum/hedef kitleyle uyumsuzluğu.
- Eğitmen sentezi: hepsi geçerli — kritik olan hepsinin **olasılık** olduğunu bilmek, kesinlik ile karıştırmamak.

### Risk Yönetimi Neden Sürekli Bir Süreç?

- Proje planlama aşamasından itibaren başlar, proje boyunca **sürekli güncellenir** — bütçe gibi (önce tahmin, sonra fiili güncelleme).
- Bir faaliyetteki gecikme yeni risk doğurabilir, bazı riskler kendiliğinden ortadan kalkabilir.
- Tüm bilgi alanlarıyla bağlantılı, her birinden etkilenir.

### Risk Yönetim Süreçleri

1. **Risk Planlama**: proje risk yönetim faaliyetlerinin nasıl yürütüleceğine karar verme.
2. **Risk Belirleme**: "projede neler ters gidebilir?" — ekiple beyin fırtınası, SWOT analizi, fishbone diyagramı kullanılabilir. Risk kaynağı **iç (proje içi)** veya **dış (proje dışı — enflasyon, döviz kuru)** olarak ayrılır.
3. **Nitel/Nicel Risk Analizi**: risklerin önceliklendirilmesi.
4. **Risk Tepki Planlama**: belirlenen risklere nasıl cevap verileceği.
5. **İzleme ve Kontrol**: sürekli döngü, durum toplantılarında yeniden değerlendirme, trend analizi.

### Girdi

- Kapsam belgesi, kurumsal süreç varlıkları, çevresel işletme faktörleri (dış çevre analizi); ilerleyen aşamalarda bütçe, iş takvimi, WBS, sorumluluk matrisi, ekip planı, tedarikçi anlaşmaları da girdi olarak kullanılır.

### Risk Kategorileri (4 Ana Grup)

1. **Teknik riskler**: yeni teknoloji benimseme zorlukları, teknik karmaşıklık/uyumsuzluk, yazılım/donanım hataları, geliştirme araçlarının verimsiz kullanımı.
2. **Proje yönetim riskleri**: planlama hataları, iletişim eksikliği, kaynak yönetim eksikliği, ekip becerisi/motivasyon eksikliği.
3. **Kurumsal riskler**: iş süreci etkinliği, finansal yönetim eksikliği, kaynak yetersizliği, strateji uyumsuzluğu.
4. **Dışsal riskler**: ekonomik dalgalanma/döviz kuru, doğal afetler, tedarik zinciri kesintileri, pazar değişiklikleri/rekabet.

### Risk Belirleme ve Değerleme Formu (Kategori Bazlı)

- Her kategori için: kapsamı, zamanı, maliyeti, kaliteyi, kaynakları nasıl etkiler — 1-10 arası puanlanır.
- Bu değerlendirmeye göre projenin risk yönetimini hangi boyutta (basit liste mi, çok katılımcılı toplantı mı) yapılacağına karar verilir. C/D tipi projelerde kapsamlı risk planlama toplantısı (ekip, ekip liderleri, kilit paydaşlar) gerekir.

### Nicel vs Nitel Risk Analizi

- **Nicel**: sayısal olasılık/etki değerlendirmesi, beklenen zarar hesaplanır (olasılık × etki). Riskten kaçınmanın maliyeti beklenen zarardan büyükse **risk göz ardı edilebilir** (ör. önlemek 1000 TL, gerçekleşirse kayıp 100 TL → önlem alınmaz).
- **Nitel**: güvenilir sayısal veri yoksa, veri elde etme maliyeti yüksekse veya ekipte sayısal analiz uzmanı yoksa kullanılır. "Çok düşük, düşük, orta, yüksek, çok yüksek" gibi niteleyici terimlerle değerlendirilir — çalıştay, anket, mülakat, odak grup gibi nitel yöntemlerle veri toplanır.

### Nitel Risk Matrisi Örneği (3x3)

- Sütun: gerçekleşme olasılığı (düşük/orta/yüksek); Satır: gerçekleşirse etki (düşük/orta/yüksek).
- Kesişim hücreleri: **göz ardı et / önemse / önlem al** şeklinde önerilen tutumu gösterir.

### Risk Değerleme Tablosu (Süreç × Risk Faktörü Matrisi)

- Sütunlar risk faktörleri (A=en olası...J=en az olası), satırlar proje faaliyetleri/süreç adımları.
- Her hücreye 1(düşük)/2(orta)/3(yüksek) puan verilir, satır ve sütun toplamları alınır.
- **En yüksek sütun toplamı**: birkaç faaliyeti etkileyen risk faktörünü gösterir — bu faktörlere odaklanılır.
- **En yüksek satır toplamı**: birkaç risk faktöründen etkilenen süreci gösterir — bu süreç özellikle iyileştirilmeli.

## Soru-Cevap: Risk Analizi

**S (İrem) — Riskler ne zaman müşteri/işverenle paylaşılır?**
- Proje şirket içiyse müşteri zaten süreci takip eder, durum/tespit raporları isteyebilir, risk değerlendirme toplantılarına katılabilir. Sponsor da önemli bir paydaş, kritik kararlarda dahil olabilir. Tedarikçiyle ilgili spesifik risklerde ilgili tedarikçi de sürece dahil edilir (yedek anlaşma gerekebilir). Durum değişkendir.

### Risk Tepki Stratejileri (5 Temel Yaklaşım)

1. **Kabullenme (Accept)**: riske karşı eylemin maliyeti beklenen zarardan büyükse — proje yönetim planı değiştirilmez. (Uygun yanıt bulunamadığında da kullanılabilir.)
2. **Kaçınma (Avoid)**: proje yönetim planını, riski tamamen dışarıda bırakacak şekilde değiştirmek — riski oluşturan faaliyeti yapmamayı seçmek.
3. **Azaltma (Mitigate)**: olasılık ve/veya etkiyi kabul edilebilir sınırlara çekmeye çalışmak (ör. büyük ölçeğe geçmeden önce prototip geliştirme).
4. **Aktarma (Transfer)**: riskin etkisini kısmen/tamamen üçüncü tarafa (sigorta, dış kaynak kullanımı) aktarmak — risk ortadan kalkmaz, sadece yönetim sorumluluğu ve bir bedel karşılığında devredilir.
5. **Plan değişikliği**: tehdidi ortadan kaldırmak için proje planında değişiklik (süre uzatma, sigorta sözleşmesi, teminat isteme, ortak girişim kurma).

### Ek Güvenlik Katmanları

- Her öncelikli strateji için **yedek strateji** olmalı; o da yetersizse **en kötü durum senaryosu (geri çekilme planı)**.
- Zaman çizelgesinde ve bütçede **ek rezerv** (dün konuşulan risk fonu) mutlaka bulundurulmalı.

---
*Not: Yarın (5. gün, son gün) — Tedarik Planı, Sözleşme, nihai rapor/proje kapanışı ve çevik (agile) proje yönetimi metodolojileriyle hafta tamamlanacak. Fishbone/balık kılçığı diyagramı (kök neden analizi) da işlenecek — şube sayısı (4, 6 vb.) probleme göre değişir, sabit bir kural yok.*
