# Proje Yönetimi — Gün 2: Ekip Oluşturma/Yönetme, Zaman Yönetimi (AON/CPM/PERT), Gantt Uygulaması, Maliyet Tahmini

Eğitmen: Tuğçe Hanım

## Kolb Öğrenme Stilleri (Ekip Çeşitliliği)

Ekipte farklı düşünce tarzları istememizin arkasındaki teorik temel — 4 öğrenme stili:

1. **Somut yaşantı**: hislerine dayalı değerlendirir, keşfederek öğrenir, ekip çalışmasına yatkın, duygusal zekası yüksek.
2. **Yansıtıcı gözlem**: önce durur, dikkatle gözlemler, sessizce dinler, sabırlı/tarafsız değerlendirir, kök nedene iner — isabet oranı yüksek kararlar.
3. **Soyut kavramsallaştırma**: duyguları bir kenara bırakır, bilimsel yöntem/analiz/kaynak taraması kullanır, mantıksal analiz gerektiren konularda başarılı.
4. **Aktif yaşantı**: hemen dener, pratik uygulamayla öğrenir, "yaparak öğrenme" — hızlı ama derin problemlerde yetersiz kalabilir.

### Vaka: Ömer (aktif yaşantı) vs Mehmet (soyut kavramsallaştırma)

- Ömer: dökümhane ustabaşı, deneyime dayalı hızlı çözüm üretir, çoğu problemi hızlı çözer ama bazı derin problemlerde tıkanır.
- Mehmet: mühendis, kitap/makale araştırıp yavaş ama sağlam çözüm üretir.
- **Sonuç**: Sadece Ömer türü ekip → hızlı çözer ama derin problemde tıkanır. Sadece Mehmet türü → yavaş, küçük problemlerde bile aksama. **İkisi bir arada olursa** küçük problem Ömer'e, derin problem Mehmet'e yönlendirilir — dengeli ekip en yüksek verimi sağlar.
- **Prensip**: proje ekibini tek bir öğrenme stiline sahip kişilerle kurmak riskli — dengeli dağılım şart.

## Ekibi Yönetme

### Yetki ve Sorumluluk
- Yetki ve sorumluluk **birlikte** bulunmalı — biri olmadan diğeri anlamsız.
- **Kritik zorluk**: ekip üyeleri genelde kendi departman yöneticilerine de bağlı (proje yöneticisine değil) — bu çatışma/yetki karmaşası yaratır.
- Çözüm: ekip üyesinin bağlı olduğu **bölüm yöneticisiyle iyi ilişki** kurmak zorunlu — bu ilişki doğrudan ekip üyesine yansır.
- Başarı ölçütü: **KPI (kilit performans göstergeleri)** ile karar verilir (ör. test uzmanı için dokümantasyonun tam/zamanında yapılması).

### Çatışma Yönetimi
- Çatışma projelerde kaçınılmaz — sebepleri: farklı tutum/davranışlar, yetersiz kaynak, önceliklendirme değişiklikleri.
- Doğru yönetilen çatışma **üretkenliği artırabilir** (araştırma/fikir üretimini tetikler).
- Teknik seçimi şuna bağlı: çatışmanın yoğunluğu/önemi, çözecek zaman var mı, tarafların statüsü (iç/dış kaynak), kısa/uzun vade çözüm isteği.

**Kullanılan teknikler:**
- **Kaçınma/geri çekilme**: yoğunluk düşükse, faaliyetleri etkilemiyorsa.
- **Yumuşatma**: ortak noktaları öne çıkarma.
- **Uzlaşma**: her iki tarafın kısmen tatmin olacağı, fedakarlık gerektiren çözüm.
- **Zorlama**: süre kısıtı varsa, çok mecbur kalmadıkça başvurulmaz ("yönetici olarak çözüm bulmalısınız" demek).
- **Yüzleştirme/tartışma**: açık görüşlü ekipte farklı perspektifler tartışılıp nihai karara varılır.
- **Tarafsız arabulucu**: proje yöneticisi çatışmada taraflı görünebilecekse (ör. iki farklı departmandan kişiler arası çatışma), tarafsız üçüncü kişi devreye girer.

### Motivasyon

- **İç kaynaklı motivasyon**: projeden keyif alma, kişisel tatmin — daha sürdürülebilir.
- **Dış kaynaklı motivasyon**: departman yöneticisi baskısı, terfi/ödül/zam beklentisi — ödül gelmezse veya bağlı olduğu kişi ayrılırsa motivasyon çöker.
- Proje yöneticisi bu ayrımı **gözlemleyerek** yapmalı — dış kaynaklı motive olanlar genelde sadece "görünür" işleri yapar, arka plana destek olmaz, bu çatışma yaratabilir; bu kişilerin performansı daha yakından izlenmeli, gerekirse daha sıkı denetlenmeli.
- Motivasyon kaynağı maddi olmak zorunda değil: sosyal faaliyetler, birlikte gelecek planlama, ait olma hissi, başarının görülmesi/takdir edilmesi.
- **Uyarı**: yöneticinin sadece "uygun ortam sağlayıp motive olmasını ummak" sürdürülebilir değil — kısa vadede kolay görünür ama uzun vadede düşük performans/proje riski yaratır.

---

## Zaman Yönetimi

- Etkili zaman yönetimi = kaynakların optimum kullanımı, risklerin erken tespiti, müşteri memnuniyeti/güveni (zaman sapması tazminat/proje iptaline kadar gidebilir).

### AON (Activity-on-Node) Diyagramı — Temel Kurallar

1. **Soldan sağa** akış — yukarıdan aşağı olmaz.
2. Bir faaliyet **öncül faaliyeti tamamlanmadan** başlayamaz.
3. Oklar **çaprazlayabilir**, ama **döngüye izin yok** (geri dönüş yasak).
4. **Koşullu dallanma yok** — "X başarılıysa Y gerçekleşsin" gibi bir kural konamaz.
5. Diyagramın **net bir başlangıç ve net bir bitiş** noktası olmalı.

### Üç Temel İlişki (Soru-Cevap Yöntemiyle Bulunur)

1. **Öncül**: "Bu faaliyetten önce hangi faaliyet tamamlanmalı?"
2. **Ardıl**: "Bu faaliyeti hangi faaliyet izlemeli?"
3. **Paralel**: "Bu faaliyetle aynı anda hangi faaliyetleri eş zamanlı yürütebilirim?" — paralel iş toplam proje süresini kısaltır, mümkün olan her yerde tercih edilir.

### CPM (Critical Path Method / Kritik Yol Yöntemi)

- Amaç: projenin en uzun süren, bitiş tarihini belirleyen **kritik yolunu** bulmak.
- Adımlar: faaliyetleri tanımla → öncül/ardıl/paralel ilişkileri belirle → en erken/en geç başlama-bitiş sürelerini hesapla → kritik yol ortaya çıkar.

**Kutucuk formatı:**
- Kutu içi: faaliyet adı + süresi (gün).
- Sol üst: **EBAT** (Erken Başlama Tarihi)
- Sağ üst: **EBİT** (Erken Bitiş Tarihi) = EBAT + süre
- Sol alt: **GBT** (Geç Başlama Tarihi) = GTT − süre
- Sağ alt: **GTT** (Geç Tamamlanma Tarihi)

**Hesaplama yöntemi (İleri geçiş — erken tarihler):**
- Başlangıç faaliyetlerinin EBAT'ı = 0.
- EBİT = EBAT + süre.
- Birden fazla öncülü olan faaliyette, öncüllerin **en geç biten EBİT'i** esas alınır.

**Hesaplama yöntemi (Geri geçiş — geç tarihler):**
- Son faaliyet(ler)in GTT'si = kendi EBİT'i (proje bitiş süresi).
- GBT = GTT − süre.
- Bir önceki faaliyetin GTT'si = sonraki faaliyetin GBT'si (birden fazla ardılı varsa **en erken** GBT esas alınır).

### Kritik Yol ve Sarkma Süresi

- **Kritik yol**: en geç tamamlanan seri faaliyetlerden oluşan yol — bu faaliyetlerde gecikme = toplam proje süresinde gecikme (gecikme toleransı sıfır).
- **Sarkma süresi (float)**: kritik yol dışındaki faaliyetlerin, toplam proje süresini etkilemeden geciktirilebileceği süre.
- **Formül**: GBT − EBAT = GTT − EBİT (kritik yol üzerindeki faaliyetlerde bu fark her zaman 0'dır).
- Sarkma süresi hesaplarken 2 varsayım: (1) başka hiçbir faaliyette sarkma kullanılmayacak, (2) projenin kritik süresi gerçek bitiş tarihidir.
- **Kaynak aktarımı**: bir faaliyette gecikme yaşanırsa, sarkma süresi olan faaliyetlerden kaynak (iş gücü vb.) aktarılarak toplam süre korunabilir.
- **Tampon payı ("küçük hile")**: 50 günlük proje müşteriye 60 gün olarak sunulursa, 10 günlük tampon kritik yoldaki herhangi bir faaliyette kullanılabilir.

### AON/PERT (Program Evaluation and Review Technique)

- Belirsizlik/karmaşıklık çok yüksekse (genelde D tipi projede) kullanılır — CPM'den daha az yaygın, daha maliyetli (çok veri/katılımcı gerektirir).
- Her faaliyet için **3 zaman tahmini**: iyimser, kötümser, en olası — tahmini **o faaliyeti yapacak kişi** yapmalı (en isabetli tahmin).
- **3 bağıntı türü** (öncül/ardıl/paralel yerine):
  1. **Zorunlu bağıntı**: değiştirilemez (ör. müşteri onayı almadan canlıya alamama).
  2. **İsteğe bağlı bağıntı**: proje yöneticisinin tercihine bağlı, değişebilir.
  3. **Dış bağıntı**: proje yöneticisinin kontrolünde değil (ör. o alanda uzmanlığı olmayan proje yöneticisi, teknik süreyi belirleyemez — bu, o alanın uzmanına bağlıdır).
- **Kesikli çizgi (sanal ilişki)**: gerçek bir öncüllük/ardıllık göstermez — bir faaliyeti doğrudan bitişe bağlayamadığımızda kullanılan gösterim aracı.

## Soru-Cevap: Zaman Yönetimi

**S (Semiha) — Süreçler sıralı mı yürütülür?**
- (Önceki gün ele alındı) — paralel yürütülür, kesin sıralama yok.

**S (Pınar/Bilge) — GBT/GTT hesaplamasını Gantt'a yansıtıyor muyuz?**
- Hayır. Gantt şeması, ekipteki personelin takip ettiği bir araç. En geç tarihler personele gösterilmez — çünkü gösterirsek muhtemelen en geç tarihe göre çalışırlar. AON hesaplaması proje yöneticisinin arka planda tuttuğu bir çalışma.

---

## Gantt Şeması Hazırlama (Uygulamalı Örnek)

- Araçlar: Microsoft Project, Asana, Excel/Google E-Tablo, Trello (görev panosu için daha çok kullanılır) — mantık hepsinde aynı.

### Örnek Süreç (Yazılım Projesi, 11 Faaliyet)

1. Proje başlangıç toplantısı
2. İhtiyaç analizi
3. Sistem gereksinimleri belirleme
4. Yazılım mimarisi tasarımı (paralel + sıralı — ihtiyaç analizine bağımlı)
5. Veri tabanı tasarımı
6. Test plan hazırlığı
7. Birim testleri
8. Entegrasyon testleri
9. Kullanıcı kabul testleri
10. Projenin canlıya alınması
11. Proje sonu değerlendirme

**Tablo sütunları**: Faaliyet No, Faaliyet Adı, Süre (gün), Tip (S=Sıralı, P=Paralel, SP=her ikisi), Bağımlı Olduğu Faaliyet, Başlangıç Tarihi, Bitiş Tarihi, Kaynak (kim yapacak).

**İş günü notu**: Süreler genelde iş günü üzerinden hesaplanır (hafta sonları hariç) — ama firmaya/endüstriye göre değişebilir (cumartesi mesaisi varsa dahil edilir).

### Gantt Çizim Adımları

1. Tarih aralığını (gün/hafta bazında) tabloya yatay eksen olarak aç, üst satırda ay, alt satırda gün gösterecek şekilde hücreleri birleştir.
2. Her faaliyet için, o faaliyetin sürdüğü tarih aralığındaki hücreleri birleştir ve **dolgu rengi** ver.
3. **Aynı kaynağı (kişi/ekip) kullanan faaliyetlere aynı renk** ver — böylece kim hangi tarihlerde çalışıyor, ne zaman boşta, görsel olarak net görülür.
4. Paralel faaliyetler birebir aynı tarihte başlayıp bitmek zorunda değil — bir arada, örtüşerek de ilerleyebilir; Gantt'ta bu görsel olarak yakalanır.

## Soru-Cevap: Gantt Uygulaması

**S (Pınar) — Aynı tarihte başlayan iki faaliyetten birine "paralel-sıralı" diğerine sadece "sıralı" yazılmasının sebebi?**
- Birlikte ilerletilebilen tüm faaliyet çiftlerine tek tek "paralel" yazmak yerine, Gantt'ta tarihler zaten paralelliği gösterdiği için tek bir yerde belirtmek yeterli.

**S (Gülçay) — Aynı tarihte çalışan farklı roller (yazılım ekibi + analist) birlikte mi çalışıyor demektir?**
- Aynı faaliyet üzerinde birlikte yazıldılarsa, bilgi alışverişiyle **birlikte** çalışacakları anlamına gelir (paralel/sıralı fark etmez, faaliyet ortaksa birlikte yürütülür).

---

## Maliyet Yönetimi

- **Sorumluluk proje yöneticisindedir** — mali işler departmanının değil. Proje yöneticisi şirketin maliyet/dağıtım esaslarını bile bilmeli (ör. bütçe %25 ilk ay, %75 sonraki ay gibi dağıtılabiliyorsa buna göre tedarik/personel planı yapılmalı).
- Maliyet yönetimi diğer tüm bilgi alanlarıyla (kapsam, zaman, İK vb.) yakından bağlantılı.
- Girdi: proje başlatma belgesi (dün görülen), süreç ilerledikçe iş takvimi, risk listesi, iş kırılım yapısı da girdi olabilir; ayrıca kurumsal süreç varlıkları (şirket bütçe kaynağı, müşteri/sponsor bütçesi).
- Proje tipine göre maliyet yönetiminin kapsamı değişir (A tipi basit takvim, D tipi detaylı iş kırılım yapısı gerektirir).

### Kaynak Listesi

- Maliyet tahmininden önce, projeyi tamamlamak için gerekli **tüm kaynakların listesi** çıkarılır (insan kaynağı, malzeme, yazılım, lisans, ekipman).
- Bu listeyi genelde **ekip birlikte** hazırlar — proje yöneticisi her alanda uzman olmadığından, teknik kaynağı en iyi o işi yapan kişi bilir.
- Proje ilerledikçe ek kaynak ihtiyacı çıkabilir — bu normal, ek rezervden karşılanır.

### Üç Temel Maliyet Tahmin Türü

| Tür | Ne Zaman | Sapma Aralığı | Not |
|---|---|---|---|
| **Kabaca Tahmin** | Proje çok başında, kapsam belgesi hazırlanırken | −%50 / +%100 | Finansal yapılabilirlik değerlendirmesi için; proje seçiminde kullanılır. Belgrad'daki bütçe teslim ödevi bu yöntemle yapılıyor — temeli iyi oturtmak için tercih edilir. |
| **Bütçesel Tahmin** ("Yukarıdan Aşağı") | Planlama aşamasında, geçmiş benzer proje verisiyle | −%10 / +%25 | Üst yönetimden başlayıp aşağı doğru tahmin toplanır, deneyime dayalı. |
| **Kesin Tahmin** ("Aşağıdan Yukarı") | Projeye yakın zamanda, iş kırılım yapısı hazır olduğunda | −%5 / +%10 | En doğru ama en uzun zaman alan/en maliyetli yöntem — küçük iş paketleri tek tek tahmin edilip toplanır. |

*(Örnek: gerçek maliyet 100.000 TL ise → kabaca tahmin 50.000–200.000 TL; bütçesel 90.000–125.000 TL; kesin 95.000–110.000 TL aralığında olur.)*

### Destekleyici Tahmin Teknikleri

1. **Ortak görüş / uzman görüşü**: üst düzey yöneticiler veya uzmanlar bir araya gelip işçilik, malzeme, enflasyon, risk faktörlerini tartışıp ortak tahmine varır.
2. **Örneksel (analojik) tahmin**: geçmiş benzer projenin kapsam/süre/maliyeti referans alınır — A/B tipi standart küçük projeler için uygun.
3. **Ayrıntılı (bottom-up) tahmin**: iş kırılım yapısındaki her iş paketinden sorumlu kişiye süre/maliyet sorulur, en güvenilir yöntem (proje yönetiminde zaman/maliyet tahmininin en güvenli yolu genelde budur).
4. **Üç nokta tahmini (PERT mantığı)**: her faaliyet için en olası, iyimser, kötümser maliyet tahmini yapılır.
5. **Aşamalar için tahminleme**: yüksek belirsizlikte proje fazlara bölünüp her faz ayrı tahminlenir (nihai ürün tam kestirilemiyorsa).
6. **Yedek faaliyet analizi (ek rezerv / risk fonu / ihtiyat yedeği)**: beklenmedik durum bütçesi — kullanmak zorunlu değil ama gerektiğinde başvurulur. Genel kural: toplam proje bütçesinin **A tipi ~%5, B tipi ~%10, D tipi %20'ye kadar** ayrılabilir.
7. **Tedarikçi fiyat teklifi analizi**: gerekli koşulları sağlayan tedarikçi tekliflerine göre ön maliyet tahmini yapılır.

## Soru-Cevap: Maliyet Tahmini

**S (Bilge) — Kolb öğrenme stilleri proje yöneticisinin kendisine nasıl etki eder, hangisi daha avantajlı?**
- Hiçbiri tek başına "daha avantajlı" değil — probleme göre değişir. Proje yöneticisinin zorluğu: **her stili duruma göre uygulayabilmek** (bazen hızlı deneyimsel karar, bazen derin sistematik analiz) — objektif kalmayı öğrenmek gerekiyor.

**S (Semiha) — Kabaca tahmin aralığını (ör. 100.000–200.000) aşan bir maliyet çıkarsa (ör. 300.000) ne yapılır?**
- Öncelik: elde kaynak varsa **kaynak aktarımı**. Yoksa mevcut kaynaklara göre kısıtlama değerlendirilir. En kötü senaryoda **ek rezerv** kullanılır. Ayrıca proje sonunda mutlaka not düşülmeli: tahmin neden saptı (piyasa araştırması yetersiz miydi, hangi analiz hatalıydı) — gelecekteki projeler için ders çıkarılmalı.

---
*Not: Yarın (3. gün) maliyet yönetimi devam edecek — bir bütçe uygulaması yapılacak, ardından diğer bilgi alanlarına geçilecek.*
