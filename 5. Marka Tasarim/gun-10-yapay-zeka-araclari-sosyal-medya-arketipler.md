# Gün 10 (Son Gün): Wix Kapanış, AI Görsel Araçları, Sosyal Medya Stratejisi, Marka Arketipleri

## 1. Wix Kapanış Notları — Şablon Entegrasyonu ve Chatbot Uyarısı

- Farklı şablonlardan alınan bölümler (Ctrl+X → başka şablona yapıştırma) otomatik olarak hedef şablonun renk/tipografi temasına uyarlanır — bu yüzden site renkleri/fontları en başta kaydedilmeli.
- **Kritik uyarı:** Bazı Wix şablonlarında hazır gelen "Let's Chat" gibi bir chatbot widget'ı, Wix'in KENDİ otomatik AI chatbot sistemidir — eğitim kapsamında KULLANILMIYOR. Şablon kullanırken bu widget fark edilirse silinmeli; kendi tasarlanan/kodlanan chatbot kullanılmalı.

## 2. Editor'de Chatbot Yapımı — Stüdyoda Olmayan İki Fark

### Fark 1: Scroll (Kayan İçerik)
- Editor'de Studio'daki gibi "Overflow Content → Scroll" seçeneği YOK.
- Çözüm: **HTML** elementi eklenip, bir yapay zeka aracına ("bu kayan mesaj alanını nasıl yaparım" şeklinde) sorularak basit bir HTML/CSS kod parçası alınıp o HTML kutusuna yapıştırılır — kod bilgisi gerektirmez, kopyala-yapıştır yeterlidir.

### Fark 2: Tıklayınca Açılıp Kapanma Animasyonu
- Editor'de Studio'daki gibi kodsuz "Click Animation" YOK.
- Çözüm: Yine HTML/kod ile (ekran görüntüsü + AI aracına sorarak) çözülebilir.

### Ortak Kalan Kısım
- Buton pinleme (sağ tık → "Pin to Screen"), konteyner içine konteyner mantığı, input/buton ekleme, Scale Proportionality, Stack benzeri hizalama ihtiyacı (Editor'de padding/margin kavramı sınırlı olsa da mesafeler manuel ayarlanmalı) — hepsi aynı mantıkla devam ediyor.
- Editor'de de metinler mutlaka İÇ konteynere bağlanmalı, dış konteynere değil (aynı taşma sorunu geçerli).

## 3. Yönetim Paneli — Bölümleme Kuralının Tekrarı

Next Play örneği üzerinden dört bölüm netleştirildi:
1. Üst bilgi (logo, başlık).
2. Menü/buton alanı (arama, yenile vb.).
3. İstatistik kartları.
4. Repeater (müşteri adayları tablosu).

Her biri AYRI section/hücre olarak yapılmalı, tek bir dev alana sıkıştırılmamalı. Container → Repeater → Text sırası korunmalı; bir text repeater'a eklendiğinde otomatik tüm tekrarlanan öğelere yansır (repeater'ın temel mantığı budur).

## 4. Form Elementi Yerine Input Kullanımı — Son Hatırlatma
- Wix'in "Form" elementi KESİNLİKLE kullanılmıyor — yazılım/kod bağlantısında sorun çıkarıyor. Tüm iletişim/veri toplama alanları manuel Input elementleriyle kuruluyor.

## 5. Studio'da İleri Seviye Animasyon — Çoklu Katmanlı Animasyon

- Her bir görsel/karta AYRI hover animasyonu (büyüme, dönme, çarpıtma, opaklık değişimi — Custom Animation ile) verilebilir.
- Aynı zamanda bu elementler bir arada **Stack** yapılıp GRUBA da ayrı bir animasyon (Translate/kayma, opaklık, renk değişimi) eklenebilir — hem tekil hem toplu animasyon birlikte çalışabilir (parallax benzeri efektler).
- Bu tür efektler YouTube'da "Wix Studio hover animation" gibi aramalarla daha da geliştirilebilir.

## 6. AI Görsel Üretim Araçları — Kapsamlı Liste

### Genel İlke
- AI, marka stratejisini kurmaz, metin/tutarlılık sorununu tek başına çözmez — sadece görsel üretim, logo konsepti, renk paleti önerisi gibi noktalarda YARDIMCI araçtır. Marka başlatma belgesine AI çıktısı kontrolsüz kopyalanmamalı (parantez içi boşluk bırakılmış placeholder metinlere dikkat edilmeli).
- Proje Uzmanı Yetiştirme Programı online eğitim dosyasında, Marka Tasarımı bölümünün altında paylaşılan bir "Görsel Prompt Üretim Rehberi" mevcut — örnek doğru/yanlış promptlar içeriyor.

### Araç Karşılaştırması

| Araç | Kullanım Alanı | Notlar |
|---|---|---|
| **Midjourney** | En yüksek estetik kalite | Ücretli, alternatiflere göre daha az tercih ediliyor bu dönem |
| **ChatGPT (DALL·E entegre görsel üretimi)** | Detaylı, konuşma diliyle revize edilebilir görseller | Prompt'lar insanla konuşur gibi uzun/detaylı yazılmalı ("arka planı yeşil yap, 3cm sağa kaydır" gibi revize talepleri işe yarıyor) |
| **Adobe Firefly** | Ticari kullanım için EN GÜVENLİ seçenek | Lisanslı içerik — telif riski taşımaz, Photoshop/Illustrator entegrasyonu var, eğitmenin en çok önerdiği araç |
| **Canva AI (Magic Studio)** | Ürün/mekan görselleri, marka logosuyla orantılı görsel üretimi | Üretilen görseller Canva içinde düzenlenebilir, marka kitine entegre edilebilir |
| **Ideogram** | Poster/görsel İÇİNDE metin (tipografi) bozulmadan üretme | Font, renk, layout detaylandırıldıkça daha gerçekçi sonuç veriyor; günlük ücretsiz kredi hakkı var |
| **Recraft** | Vektörel çıktı, 3D logo görselleştirme, izometrik logo | Düzenlenebilir vektör üretir — her parçaya ayrı ayrı müdahale edilebilir, logo tasarımında zorlananlar için özellikle öneriliyor |

### Prompt Yazma İlkeleri
- Stil belirtilmeli (flat vector, clean lines, 3D typography, high contrast, black and white vb.).
- Sektöre özgü terimler kullanılmalı (teknoloji → minimal/futuristic; moda → elegant/script font/luxury/serif typography).
- Marka teması belirtilmeli (playful, professional vb.).
- Renkler mümkünse Hex kodu ile verilmeli.
- Üretilen görsel Wix'e normal "Add Media → Upload" yoluyla aktarılır.

## 7. Sosyal Medya ve Dijital Pazarlama — Temel Kavramlar

### Dijital vs Geleneksel Pazarlama
- Geleneksel: TV, radyo, gazete, dergi.
- Dijital: web sitesi, e-posta, arama motorları, sosyal medya — eğitimin odağı burası.

### Dijital/Sosyal Medya Okuryazarlığı
- Kişisel veri koruması, web sitesi güvenliği, doğruluğu kanıtlanmamış bilgi paylaşmama, başka markadan doğrudan kopyalama yapmama (ilham almak farklı, kopyalamak farklı).

### Algı Yönetimi ile Web Sitesi Kalitesinin İlişkisi
- Web sitesindeki tutarlılık (logo, renk paleti, dil, görsel bütünlük, hizalamalar, okunabilirlik) doğrudan kullanıcı algısını ve markaya duyulan güveni etkiler — bozuk/parça parça görünen bir site olumsuz algı yaratır.
- Hedef kitleye uygun içerik türü seçimi önemli: eğitici, eğlendirici, ilham verici, duyuru odaklı — marka konumlandırmasına göre belirlenir (örnek: Odak markası eğitici içerik ağırlıklı olabilir).

### Platforma Göre Marka Dili (Ton Değişir, Ses Değişmez)
| Platform | Karakteristik |
|---|---|
| Instagram | Görsel, estetik, hikaye anlatımı, ilham |
| TikTok | Eğlenceli, enerjik, samimi, trend/akım odaklı |
| LinkedIn | B2B, network, ciddi/kanıta dayalı, kısa açıklayıcı |

- **Hook First (Kanca Cümle):** Postlarda ve web sitesi ana sayfasında dikkat çeken kısa bir açılış cümlesi/slogan kullanımı önemli.

### Platform Seçimi
- Hedef kitlenin yaş/meslek/davranış profiline göre belirlenir — marka başlatma belgesindeki hedef kitle tanımıyla birebir örtüşmeli.

### Trend Takibi — Soru-Cevap Sonucu
**Soru:** Her trend her marka tarafından uygulanmalı mı?
**Cevap (doğrulandı):** Hayır — sadece marka kimliği, sesi ve tonuyla örtüşen trendlere katılınmalı. Marka sınırlarının dışına çıkan trend katılımı kısa vadede görünürlük sağlasa da uzun vadede marka algısını olumsuz etkileyebilir. Kural: "Trende gir ama marka sınırlarını aşma."

## 8. Markalaşma Süreci — Adımlar

1. **Keşif ve Araştırma** — fikir, hizmet sektörü belirleme.
2. **Marka Temellerini Kurma** — hedef kitle ve persona oluşturma.
3. **Arketip Seçimi** — bkz. aşağıdaki bölüm.
4. **İçerik Stratejisi** — platform, içerik türü, ton belirleme.
5. **Konumlandırma** — Gün 2-3'te işlenen konumlandırma stratejileriyle birleşiyor.

## 9. Marka Arketipleri (Carl Jung — Kolektif Bilinçdışı Teorisine Dayalı)

12 arketip, 4 grup halinde, her grupta 3 arketip. Markalar genelde bir ANA arketip + bir YARDIMCI (destekleyici) arketip seçer.

### Grup A — Düzen ve Kontrol Arayanlar
| Arketip | Temel Arzu | Örnek Markalar |
|---|---|---|
| **The Ruler (Yönetici)** | Güç, kontrol, liderlik, düzen yaratmak | Rolex, Apple, Mercedes |
| **The Creator (Yaratıcı)** | Kalıcı, özgün, yenilikçi bir şey yaratmak, öncü olmak | Adobe, Figma, Pixar, Lego |
| **The Caregiver (Bakıcı/Şefkatli)** | Yardım etmek, beslemek, korumak | Volvo (aile koruması teması) |

### Grup B — Bağ Kurmak ve Ait Olmak İsteyenler
| Arketip | Temel Arzu | Örnek Markalar |
|---|---|---|
| **The Everyman (Sıradan Dost)** | Herkesle bağ kurmak, ulaşılabilir olmak | IKEA ("evinizin her şeyi"), Volkswagen |
| **The Lover (Sevgili/Aşık)** | Samimiyet, haz, güzellik, yakınlık, tutku | Magnum, Chanel, Victoria's Secret |
| **The Jester (Palyaço)** | Eğlence, mizah, dürtüsellik, ironi | M&M's, Old Spice, Doritos, Fanta |

### Grup C — Değişim, Risk, Etki Yaratmak İsteyenler
| Arketip | Temel Arzu | Örnek Markalar |
|---|---|---|
| **The Hero (Kahraman)** | Cesareti/gücü kanıtlamak, sınırları zorlamak | Nike ("Just Do It"), BMW, FedEx, Adidas |
| **The Outlaw (Asi)** | Kuralları yıkmak, farklı olmak, toplumsal normlara meydan okumak | Harley-Davidson, Red Bull |
| **The Magician (Sihirbaz)** | İnovasyon, dönüşüm yaratmak, daha önce yapılmamışı yapmak | Disney, Tesla, Dyson |

### Grup D — Öz Gelişim ve Bağımsızlık Arayanlar
| Arketip | Temel Arzu | Örnek Markalar |
|---|---|---|
| **The Innocent (Masum)** | Mutluluk, sadelik, saflık | Coca-Cola, McDonald's |
| **The Explorer (Kaşif)** | Sınırları keşfetmek, bağımsızlık, yeni dünyalar | North Face, Jeep, Patagonia |
| **The Sage (Bilge)** | Bilgiyi bulmak, araştırmak, öz gelişim | BBC, TED, Wikipedia, Google |

### Kullanım Notu
- Marka başlatma belgesine arketip spesifik olarak yazılmıyor (zorunlu alan değil) ama marka kimliğini netleştirmek için kullanılması öneriliyor — kendi markanızı tarif edip bir AI aracına "bu marka hangi arketipe yakın?" diye sorabilirsiniz.
- Bir marka birden fazla arketipe (özellikle ana + yardımcı) yakın olabilir — sektöre ve kapsam genişlemesine göre değişebilir (örnek soru-cevapta: bir sanatçı markası hem Yaratıcı hem Kaşif/Bağımsız olabilir).

## 10. Kriz ve İtibar Yönetimi

### Takipçi Satın Alma Sorusu — Sınıf Tartışması Sonucu
**Soru:** Yeni kurulan bir markanın sosyal medyada büyümesi için takipçi satın almak mantıklı mı?
**Sonuç (doğrulandı):** HAYIR. Bot/satın alınmış takipçi:
- Kullanıcılar tarafından fark edilebilir, güven kaybına yol açar.
- Marka algısını "takipçi kasan" konumuna düşürür.
- Organik büyüme (tutarlı, düzenli, eğitici/değerli içerik üretimi — özellikle Reels gibi formatlar) uzun vadede daha sağlıklı sonuç verir.

### Riskli Promosyon Stratejisi Örneği (Tartışıldı)
- "Bizi takip et, kanıtla, %10 indirim al" gibi agresif takipçi kazanma taktikleri kısa vadede işe yarasa da marka güvenilirliğini zedeleyebilir — "muhtemelen batar" şeklinde değerlendirildi.

### Kriz Yönetiminin Amacı
- Amaç krizi anında bastırmak değil, markayı krizden DAHA GÜÇLÜ ve güvenilir çıkarmaktır.
- Bir marka bir olayla eleştirildiğinde, eleştiren herkesin markanın hedef kitlesi olmadığı unutulmamalı — markanın "herkesi memnun etmeye" çalışarak asıl hedef kitlesinden uzaklaşması riski var.
- Doğru yaklaşım: soğukkanlılık, tutarlılık, hızlı ama hesaplı reaksiyon, hedef kitleye sadık kalma.
- Doğru yönetilen kriz, zamanla markanın güvenilirliğini artırabilir.

## 11. Kapanış — Süreç Özeti

- Marka başlatma belgesi (kopyası alınıp doldurulur, PDF olarak iletilir).
- Logo, Belgrad'a gelmeden tamamlanmalı.
- Kurumsal kimlik kılavuzu sayfaları elden geldiğince önceden hazırlanmalı.
- Belgrad 3. gün 23:59'da kurumsal kimlik kılavuzu son teslimi var.
- Wix çalışması Belgrad süreci boyunca devam eder, ilerledikçe eğitmenle paylaşılıp revize alınabilir.
- Eğitim boyunca işlenen tüm konular (marka temelleri, hedef kitle/persona, isimlendirme, logo, renk, tipografi, kurumsal kimlik kılavuzu, Wix Editor/Studio, chatbot/yönetim paneli, AI araçları, sosyal medya, arketipler) 10 günlük Marka Tasarımı eğitiminin tamamını oluşturuyor — bundan sonrası Belgrad'daki yüz yüze atölye süreci ve yazılım eğitimiyle devam ediyor.
