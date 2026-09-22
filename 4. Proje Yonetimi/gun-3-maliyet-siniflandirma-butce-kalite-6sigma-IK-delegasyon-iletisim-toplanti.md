# Proje Yönetimi — Gün 3: Maliyet Sınıflandırma, Bütçe Uygulaması, Kalite Yönetimi (6 Sigma, FMEA), Proje İK, Delegasyon, İletişim ve Toplantı Yönetimi

Eğitmen: Tuğçe Hanım

## Maliyet Sınıflandırma

Maliyetler 2 eksende sınıflandırılır:

1. **Sabit vs Değişken**
   - **Sabit**: belli dönemde, faaliyet/büyüklük düzeyine göre değişmeyen maliyet (ör. ofis kirası, araç kirası — üretim miktarından bağımsız).
   - **Değişken**: üretim/kullanım miktarına göre artan/azalan maliyet (ör. malzeme maliyeti).

2. **Doğrudan vs Dolaylı**
   - **Doğrudan**: projenin ürün/hizmetiyle doğrudan ilgili, belirli bir iş paketine doğrudan yüklenebilen maliyet (işçilik, proje için satın alınan eğitim/teçhizat) — proje yöneticisi bunu **kontrol edebilir**.
   - **Dolaylı**: tek bir projeye bağlı değil, birden fazla projeye paylaştırılan maliyet (ör. birden fazla projeye bakan genel müdürün maaşı, tüm projelerde kullanılan Asana lisansı) — muhasebe prosedürüyle projelere dağıtılır, proje yöneticisinin kontrolü **sınırlı**.

## Bütçe Tablosu Uygulaması (Şablon)

**Sütunlar**: Proje adı/no, Proje Yöneticisi, Kategori, Öge, Maliyet, Miktar, Tahmini Gider, Fiili Gider, Tahmini Gelir, Fiili Gelir, Kaynak, Faaliyet, Tür.

- **Gelir kalemleri**: şirket içi kaynak, müşteri bütçesi, sponsorluk gelirleri (sponsoru detaylandırılabilir).
- Tahmini/fiili gelir-gider kabaca tahmin aralığına (−%50/+%100) uygun olmalı — bu aralığı tutturmak kritik kontrol noktası.
- **Gider kategorileri örnek**: proje araçları (yazılım lisansları — Microsoft Project, Asana, Miro), eğitim (test eğitimi, risk yönetimi eğitimi, İSG eğitimi), personel hak edişleri (test uzmanı, geliştirici, proje yöneticisi ücretleri), iletişim giderleri (Trello, Slack), tedarik (yazılım lisansı, donanım, ofis malzemesi), **risk fonu/rezerv** (toplam gelirin belirlenen yüzdesi — bkz. dün: A tipi ~%5, D tipi %20'ye kadar).
- Belge, proje boyunca **sürekli güncellenen** bir doküman — Belgrad teslimi tek seferlik hazırlanacak ama fiili gider kısmı proje ilerledikçe güncellenir (kavram olarak).
- Formül kullanımı zorunlu değil; manuel toplam da kabul edilir.

## Soru-Cevap: Bütçe

**S (Doğa) — Bir araç hem "proje aracı" hem "iletişim aracı" olabiliyorsa (ör. Asana) hangi kategoriye konur?**
- Aracın **kullanım amacına** göre karar verilir: görev panosu/Gantt takibi için kullanılıyorsa "proje araçları"; sadece iletişim/bilgi paylaşımı için kullanılıyorsa "iletişim araçları" kategorisine girer.

---

## Kalite Yönetimi

### Kalite Kavramının Değişimi

- **Eski mantık**: kaliteyi üretici belirlerdi.
- **Yeni mantık**: kaliteyi **müşteri/hedef kitle** belirliyor — proje yönetimi kalitesi biz tarafından belirlenir, ama **çıktı kalitesi müşteri tarafından belirlenir**.
- Kalite çıtası sürekli yükseliyor — teknoloji gelişimi, demografik/psikografik faktörler, veri üretim maliyetinin düşmesi bunun sebepleri.
- Müşteri beklentisi: daha yüksek performans, daha hızlı ürün, ileri teknoloji, makul fiyat.

### Kaliteyi Etkileyen Pazar Değişkenleri

- Ürünün satılabilirliği (kalite-maliyet dengesi)
- Üretilebilirlik (teknoloji/insan kaynağıyla üretilebiliyor mu, makul fiyata)
- Performans/güvenilirlik (belirli koşullarda hatasız çalışma)
- Bakım sonrası performansa dönme kapasitesi
- **Toplumsal kabul** (son yıllarda eklenen boyut): sürdürülebilirlik, etik değerler (ör. hayvan deneyi yapılmaması) ile projenin uyumu

### Kalite Yönetimi Süreci

- Girdi: kapsam belgesi, kurumsal süreç varlıkları.
- Araç-gereç: fayda-maliyet analizi, kontrol grafikleri, kıyaslama, akış şemaları, balık kılçığı (fishbone) diyagramı.
- **Kalite iki boyutlu**: (1) projenin yapılış sürecinin kalitesi, (2) süreç sonucu çıktının kalitesi.
- **Kritik uyarı**: proje yöneticisi sadece çıktıya odaklanıp süreç kalitesini (ekip iletişimi, ekibin fiziksel/motivasyonel durumu) ihmal ederse — ekip içi çatışma, motivasyon düşüşü, kilit yetkinlikli ekip üyesinin ayrılması gibi risklerle karşılaşır, bu da çıktı kalitesini de tehlikeye atar.
- Kalite maliyeti proje tipine göre değişir: A tipinde düşük, D tipinde kaçınılmaz yüksek.
- **Kıyaslama (benchmarking)**: SWOT analiziyle iç/dış çevre analiz edilir, benzer projelerle karşılaştırma yapılıp farkları ortaya çıkaran etmenler bulunur, kendi projeye iyileştirme uygulanır.

### ISO 9000 vs 6 Sigma

- **ISO 9000**: uluslararası kalite standartlarına uygunluk belgelendirmesi — bir kalite yönetim yöntemi değil, taahhüt göstergesi.
- **6 Sigma**: veri yönelimli, **müşteri odaklı**, sistematik metodoloji — müşteriden elde edilen veriyle sürekli kalite iyileştirme. Hataları azaltır, müşteri memnuniyetini artırır, süreçleri optimize eder.
  - Döngü: kaliteyi tanımla → müşteri talebini ölç/analiz et → iyileştir → kontrol et → gerektikçe geri dön (bitmeyen bir döngü, PUKÖ benzeri).
  - **Kuşak hiyerarşisi**: Beyaz kuşak (öğrenen, destek veren) → Sarı kuşak (istatistiksel araç kullanan, aktif görev alan) → Yeşil kuşak (küçük ölçekli kalite projelerini yönetebilen) → Siyah kuşak (ekip lideri, eğitim veren) → Uzman siyah kuşak (stratejik kalite politikalarını belirleyen) → Şampiyon (en tepede, genelde üst yönetimden biri).

### FMEA (Hata Türü ve Etkileri Analizi)

- Amaç: hatalar oluşmadan önce önlem almak (hata sonrası çözmek yerine).
- Süreci belirle → olası hata türlerini listele → müşteri/sistem üzerindeki etkisini değerlendir → mevcut kontrol/tespit sistemlerini incele.
- **RPN Hesabı** (Risk Priority Number): 
  - **Şiddet (S)**: hatanın etkisinin ciddiyeti, 1–10 puan.
  - **Olasılık (O)**: meydana gelme ihtimali, 1–10 puan.
  - **Tespit edilebilirlik (D)**: mevcut sistemle tespit edilebilme ihtimali, 1–10 puan (yüksek tespit kolaylığı = yüksek puan).
  - **RPN = S × O × D** — en yüksek skorlu hatalara öncelik verilir (kaynak israfını önlemek, doğru yere enerji sarf etmek için).
- Kullanım alanları: ürün tasarımı, üretim süreçleri, yazılım, bankacılık, sağlık — hemen her sektörde yaygın.

## Soru-Cevap: Kalite

**S (Aleyna vd. — grup egzersizi) — Kaliteli ürün/hizmet nasıl tarif edilir?**
- Katılımcı yanıtları: beklentiyi karşılama, standartlara uygunluk (kozmetikte içerik/üretim güvenilirliği), sektöre göre değişen kriterler (yazılımda veri güvenliği, gıdada doğallık), uzun vadeli memnuniyet, kullanım kolaylığı/düşük risk/dayanıklılık.
- Eğitmen sentezi: her birey/kültür için "kaliteli" farklı anlam taşıyabilir — proje yöneticisi kendi hedef kitlesinin beklentisine odaklanmalı, kendi görüşünü değil.

**S (Elif) — FMEA analizi proje stresini yönetmede işe yarar mı?**
- FMEA doğrudan stres yönetim aracı değil ama dolaylı katkısı var: proje yöneticisinin kendi duygusal zekasını yükseltip gerçeklere odaklanması, ekibi süreç iyileştirmelerine dahil ederek yapıcı eleştiri kültürü kurması stres yönetimine katkı sağlar.

---

## Proje İnsan Kaynakları Yönetimi

- Proje İK planı: roller, sorumluluklar, gerekli yetenekler belirlenir; ekip içi bilgi aktarımı/raporlama süreci de yönetilir.
- **Rol vs sorumluluk ayrımı**: rol = yapılacak görev, sorumluluk = o görevin sonuçlarından hesap verme yükümlülüğü.
- Süreç: personel ihtiyacı belirleme → yetenek yönetimi (mevcut/gelecek ihtiyaç) → açık tespiti → eğitim/gelişim programı → performans yönetimi (KPI, geri bildirim) → motivasyon sistemleri → yasal/etik uyum.
- Girdi: personel kayıtları, iş takvimi, kapsam belgesi, iş kırılım yapısı, maliyet tahmini/bütçe.

### İyi Bir Proje Yöneticisinin Nitelikleri (Grup Egzersizi Sonucu)

Katılımcılardan toplanan ve eğitmen tarafından teyit edilen özellikler:
- **Liderlik** — vizyon belirleme, hedefe odaklama, motivasyon koruma.
- **İletişim** — açık, düzenli, etkili konuşma; kapısı kapalı yönetici modelinin geride kaldığı vurgusu.
- **Problem çözme odaklılık** — risk yönetimi, değişime uyum, suçlamak yerine çözüm arama, baskı altında yönetme.
- **Detaycılık ve takip** — kritik yoldan sapmayı erken görmek.
- **Kararlılık** — belirlenmiş yapıyı gereksiz değişikliklere karşı korumak, net iletişim.
- **Geleceğe yatırım/mentorluk** — ekibi geliştirme, öğrenme sürecini destekleme.
- **Soğukkanlılık ve sevecenlik** — insanların gönüllü takip etmesini sağlamak, sadece yetki gücüyle değil.
- **Gelişime açıklık** — çağa ayak uydurma, ekipten de öğrenmeye açık olma (karşılıklı bilgi akışı).

### Eğitmenin Eklediği Unsurlar

- **Güven**: sorumlu kalma, rehberlik etme — güven olmadan ekip küçük problemleri saklar, problem büyür ve projeye zarar verir.
- **Açıklık/şeffaflık**: alınan kararlar, gidişat, değişiklikler ekiple paylaşılmalı.
- **Delegasyon**: yetkilendirme yoluyla motivasyon artırma.
- **Net performans beklentisi + periyodik geri bildirim.**
- **Esneklik/adaptasyon**: değişen koşullara hızlı uyum kültürü.

---

## Delegasyon (İş Devri)

### Temel İlke

- **Nihai sorumluluk asla delege edilemez** — proje yöneticisinde kalır. Kısmi görev/sorumluluk devredilebilir ama çıktıdan sorumlu olan yine proje yöneticisidir.

### Ne Zaman Delege Edilir?

Soru cevap: bu işi yapabilecek başka biri var mı? Kendim yapmam zorunlu mu? Bu, ekip üyesinin gelişimi için fırsat mı? Tekrar yapılacak bir görev mi? Etkili delege edecek zamanım var mı?

### Kime Delege Edilir?

Soru cevap: kişinin deneyimi/yeteneği uygun mu? Çalışma stili (bağımsız/talimatlı) neye uyuyor? Kişinin kariyer hedefleriyle örtüşüyor mu? Mevcut iş yükü uygun mu?

### Nasıl Delege Edilir?

1. İstenen sonucu **açıkça** ortaya koy.
2. Yetki/sorumluluk sınırlarını belirle (bağımsızlık derecesi).
3. Mümkünse kararı **çalışanla birlikte** al — sahiplenmeyi artırır.
4. Sorumlulukla **eşit oranda yetki** ver.
5. **Süreç boyunca destekle** — danışman gibi davran, ama önce kişinin çözüm önerisini dinle, sonra kendi görüşünü ekle (direkt çözüm dayatma).
6. **Sonuç odaklı** ol, "nasıl yaptığına" değil "neyi başardığına" bak — kendi yönteminin tek doğru yol olmadığını kabul et.
7. **Kontrolü asla bırakma** ama baskıyla değil — son tarih belirle, takip aralıklarını netleştir (ör. Asana üzerinden).
8. Değerlendirme sırasında **kendini de sorgula** (doğru aktarım yaptın mı), sadece kişinin hatasına odaklanma.
9. Sonucu değerlendirirken **sadece tam/iyi sonuçları kabul et** — eksik/kötü sonucu "moral bozulmasın" diye kabul etmek, kişiyi gelişim fırsatından mahrum bırakır ve projeye ek yük (yeniden yapım, zaman/kaynak kaybı) getirir.

### Mikro Yönetim (Kaçınılması Gereken)

- Delegasyondan çekinip her işi kendisi yapmaya yönelen veya baskıcı/aşırı kontrolcü şekilde devreden yöneticiye "mikro yönetici" denir.
- Belirtiler: sık taciz eden takip mailleri, küçük hatada işi geri alma, aşırı detaycılık.
- Sebepleri: güvensizlik, kötümserlik, düşük duygusal zeka, kısa vadede "kendim yaparım daha kolay/hızlı" algısı.
- **Kısa vadede kolay görünür ama uzun vadede zarar**: proje yöneticisi zihinsel eforunu küçük ayrıntılara harcar, büyük kararlara odaklanamaz; ekip gelişemez.
- **Eğer siz bir mikro yöneticiyle çalışıyorsanız**: seçenekler sınırlı — (1) İK'ya/ilgili komiteye durum bildirme (anonimlik garantisi olmayabilir, geri dönüş riski var), (2) projeden çekilme. "Kaçınma şansı çok sınırlı" — kendi tarafınızdan mikro yönetici olmamaya çalışıp örnek olmak, tek gerçekçi kontrol alanınız.

---

## İletişim Yönetimi

- Projedeki tüm paydaşları (ekip, tedarikçi, sponsor) bir arada tutan bilgi alanı — sağlıksız iletişim iklimi **doğrudan** çıktıyı olumsuz etkiler (kesin, olasılık değil).
- Soru cevap: paydaşlar kim? Bilgi ihtiyaçları ne? Nasıl ulaştırılacak? Kontrolü nasıl sağlanacak?
- A'dan D tipine gidildikçe iletişim yönetiminin önemi ve kullanılan araç/teknik karmaşıklığı artar.
- Plan aşamasında: hangi kanal (email, Trello/Asana/Slack, toplantı) kime, ne sıklıkla kullanılacak — netleştirilir ve kontrol edilir.

## Toplantı Yönetimi

### Genel İlkeler

- Toplantı sıklığı **durumsallık teorisine** göre belirlenir — projenin büyüklüğü/aşamasına göre değişir (başta sık, ortada/sonda seyrekleşebilir veya tersi).
- **Gereğinden sık toplantı = başarısızlık kaynağı** (sıkılma, verimsizlik).
- Çevik metodolojide "stand-up" toplantılar: 10-15 dakikalık haftalık kısa değerlendirmeler.

### PAT Sistemi (Amaç-Gündem-Zaman)

1. **Amaç**: toplantının amacı net belirlenmeli — katılımcı hazırlıksız gelirse toplantı verimsiz geçer.
2. **Gündem**: ana başlık alt başlıklara bölünür, her alt başlığa **sorumlu kişi** atanır (o kişi hazırlanıp gelir).
3. **Zaman**: her gündem maddesine süre sınırı konur — gereksiz detaydan kaçınmayı, öz konuşmayı teşvik eder.

### Verimli Toplantı için Diğer Kurallar

- **Doğru katılımcıları** belirle — konuyla ilgisi olmayan kişileri dahil etme (dikkat dağılır).
- Toplantıdan birkaç gün önce bilgilendirme yap.
- Geç gelen katılımcıya geçmiş konuşulanları özetleme — vakit kaybı ve kötü örnek olur, toplantı sonrası bireysel anlatılır.
- Alınan kararlar **tartışmaya açık değil** — "ekip kararı/konsensüs" vurgusu yapılmalı.
- Karar vericilerin yanı sıra **iş planında yer alacak kişiler** de dahil edilmeli.
- **Tek bir kişi not tutar** (herkesin ayrı not alması karmaşaya yol açar) — kararlar, sorumlular, deadline, kaynaklar kayıt altına alınır, ortak kanaldan (görev panosu) paylaşılır. Toplantı sonunda kararlar sesli okunup soru-cevap yapılır.
- **Kriz durumunda**: gündem/süre kısıtı bir kenara bırakılır, sorun çözülene kadar toplantı devam eder.
- **Ofis dışı toplantı** (kafe vb.): motivasyon/yaratıcılığı artıran bir yöntem, ara sıra kullanılabilir.

### Nominal Grup Tekniği (Fikir Geliştirme)

- Katılımcılara kağıt dağıtılır, fikirler **etkileşimsiz** yazılır → sesli paylaşılır (tartışma yok) → tahtaya yazılır → grup oylar (yine tartışmasız) → en yüksek puanlı fikirler (ör. ilk 3-5) tartışmaya açılır.
- Amaç: grup baskısını minimize etmek, herkesin özgürce fikir sunmasını sağlamak.
- Konu dışına çıkan/uzayan konuşmacıya: "tahtaya kalkıp göstererek anlatır mısınız" gibi yönlendirmelerle kısa/öz tutulur.

## Soru-Cevap: İK ve İletişim

**S (Ebru) — Belgrad'da hazırlanacak projeler marka başlatma belgesindeki faaliyete mi dayanacak?**
- Şu an netleştirilmemiş, bazı kısımlar önceden çerçevelenmiş bazı kısımlar serbest bırakılacak — şu an odaklanılması gereken konu proje envanterlerinin nasıl hazırlanacağını öğrenmek, Belgrad'da detaylar netleşecek.

**S (Pınar) — Belgrad öncesi envanterler üzerinde şimdiden pratik yapmak mantıklı mı?**
- Evet önerilir (hayali proje üzerinden A diyagramı/iş takvimi denemesi, nerede takıldığını görmek için) ama zorunlu değil — Belgrad'da bir proje yönetimi uzmanı destek sağlayacak, eğitmen de mail üzerinden erişilebilir olacak.

---
*Not: Yarın (4. gün) — ders envanter çalışmasıyla başlıyor (geç kalınmaması önemli). İş kırılım yapısı (WBS) ve sorumluluk matrisi işlenecek — teslim listesinde olmasa da proje yöneticisi için zorunlu bilgi. Son gün (Cuma) çevik proje yönetimi metodolojileri ele alınacak.*
