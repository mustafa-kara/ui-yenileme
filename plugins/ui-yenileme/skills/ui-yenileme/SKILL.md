---
name: ui-yenileme
description: Bir uygulamanın ekranlarını ya da bir akışını (kayıt, onboarding, anasayfa, profil, mesajlar, ayarlar, ödeme, admin paneli…) araştırmaya dayalı olarak baştan tasarlar. Bugünkü ekranları inceler, otoritelerden (NN/g, GOV.UK, Baymard, WCAG 2.2, Apple HIG, Material 3, uygulama yardım merkezleri) kurallar toplar, claude.ai Design tuvalinde tıklanabilir yeni ekranlar çizer ve her yeni ekranı bugünkü hâliyle yan yana koyar. Davranış değiştiren kararları kullanıcıya ayrıca sorar. Kullanıcı "ekranları yenile", "UI/UX'i daha iyi yap", "bu akış çok kötü, baştan tasarla", "büyük bir değişim istiyorum", "formlar kötü, otoritelerden araştır", "tasarım önerisi göster", "önce/sonra karşılaştır", "redesign", "revamp the UI", "make the onboarding better" gibi bir şey dediğinde kullan. Ekran adı vermese ya da "tuval" kelimesini kullanmasa da kullan. Rötuş isteklerinde değil (tek bir düğmenin rengi, tek hata düzeltmesi), kapsamlı yenilemede kullan. Mobil ve web için geçerli; uygulama (kod) aşaması bu skill'in dışında.
---

# UI yenileme: araştırma → tasarım tuvali → karşılaştırma

Bu skill bir ekran grubunu ya da akışı **görülür biçimde daha iyi** hâle getiren bir tasarım önerisi üretir. Çıktı bir claude.ai Design tuvalidir: telefon ya da web boyutunda tıklanabilir yeni ekranlar, her birinin solunda bugünkü ekranın görüntüsü. Yanında kullanıcıya kısa bir özet ve karar listesi verilir. Kod yazılmaz; uygulama kullanıcı onaylayınca ayrı bir iş olarak yapılır.

Kullanıcının beklediği şey rötuş değil. Bu skill'in çıkış noktası şu tür bir geri bildirimdir: "İyileştirmeydi ama beklediğim büyük değişim değildi." Bu yüzden:
- düzeni, ekran başına soru sayısını ve akış sırasını sorgula;
- duygusal anları (kutlama, önizleme) ve güveni artıran öğeleri ekle;
- her kararı bir kaynağa ya da bugünkü bir soruna bağla. İnce detaylar bu işin değerini belirler.

Kullanıcıya giden her metin kullanıcının dilinde olsun, ara durum mesajları dahil. Uzun tuval yazımı sırasında birkaç adımda bir tek cümlelik durum ver; kullanıcı ne olduğunu bilmek istiyor.

## 1. Kapsamı netleştir

Konuşmadan şunları çıkar; yalnız gerçekten belirsiz olanı sor:
- **Hangi ekranlar ya da akış?** Kullanıcı "yalnız kayıt, diğer alanlara dokunma" dediyse kapsam dışı ekranları çizme.
- **Platform:** mobil (390×844 telefon çerçevesi) ya da web/admin (1440 genişlikte sayfa).
- **Değişim düzeyi:** büyük yenileme mi, belirli bir sorun mu? Belirtilmemişse büyük yenileme varsay.

## 2. Bugünü topla (araştırmayla paralel)

Araştırma alt ajanını (adım 3) hemen başlat; bu adımı o çalışırken yap.

1. **Bugünkü ekran görüntüleri.** Sırasıyla bak:
   - konuşmada ya da çalışma klasöründe daha önce çekilmiş ekran görüntüleri;
   - projenin golden/snapshot testleri (Flutter alchemist golden'ları çoklu cihaz ızgarasıdır; telefon karesini kırpma tarifi `references/canvas-recipe.md`'de);
   - gerekiyorsa uygulamayı çalıştırıp çekmek (simülatör, emülatör, tarayıcı). Bunu ancak ortam uygunsa ve başka bir süreci (ör. başka bir ajanın simülatörünü) bozmayacaksa yap;
   - hiçbiri yoksa bugünkü ekranı koddan sadık biçimde yeniden çizersin. Çerçeve adına "(koddan yeniden çizildi)" yaz (`references/canvas-recipe.md` §4).

   Görüntüleri yan yana bir montajda (ImageMagick `+append`) birleştirip kendin incele. Neyin kötü olduğunu somut yaz: "her ekran aynı form", "yeni kullanıcı 'Tekrar hoş geldin' görüyor", "iki ayrı ilerleme göstergesi", "boş kutular rehbersiz" gibi.
2. **Akış ve kod:** rota sırası, durum makinesi, ekranların hangi API çağrısını yaptığı. Bir soruyu başka ekrana taşımak ya da bölmek mümkün mü, bunu buradan anlarsın.
3. **Marka ve tasarım sistemi:** renk token'ları, yazı tipi, köşe yarıçapları, ikon dili, logo dosyası. Yeni tasarım bu token'larla çizilir. Büyük değişim düzende ve etkileşimde olur, markayı değiştirmek gerekmez.
4. **Ürün kararları ve kısıtlar:** proje hafızası, plan/tasarım dokümanları, AGENTS.md/CLAUDE.md. Özellikle bak:
   - **Kullanıcının reddettiği öneriler:** tekrar önerme. Örnek: kullanıcının onayladığı bir oranı, rengi ya da akış sırasını yeniden değiştirmeyi önermek.
   - **Ürün modeli:** ör. "ödeme yalnız kapıda", "mesajlaşma yalnız iki taraf onaylayınca".
   - **Yasal metinler ve rıza akışları:** içerik eksilmez, yalnız düzen değişir.
   - **Sabit listeler:** şikayet nedenleri, seçenek değerleri.
   - **Veri yerelliği ve yeni dış hizmet yasakları.**
5. **Gerçek metinler:** l10n/ARB dosyalarından bugünkü metinleri al. Yeni metin yazarken bugünkü anlamı ve yasal içeriği koru.

## 3. Araştır (arka plan alt ajanı)

`references/research-brief.md`'deki şablonla bir genel amaçlı alt ajanı arka planda başlat. Şablonda ürün modelini, bugünkü akışı, ekip tarafından zaten yapılmış iyileştirmeleri ve kapsamı doldur. Alt ajan rapor dönene kadar adım 2 ve 4'ü sürdür; sonucu tahmin etme.

`references/design-principles.md` daha önceki iki araştırma turunun damıtılmış kurallarını içerir. Hem başlangıç noktası hem kontrol listesi olarak kullan, ama her projede araştırmayı yine yaptır: ürün ve platform farkı kuralları değiştirir.

Raporda özellikle iki şeye dikkat et:
- **Aleyhteki kanıtlar:** ör. "ekran başına tek alan bazen yavaşlatır", "otomatik ilerleme WCAG 3.2.2'ye aykırı", "ölçülmemiş süre vaadi yapma". Bunlar tasarımı aşırıya kaçmaktan korur.
- **Şirket beyanı ve ikincil kaynak etiketleri:** sayıları kullanıcıya aktarırken bu ayrımı koru.

## 4. Konsepti kur

Her bugünkü sorunu bir değişikliğe bağlayan kısa bir eşleme çıkar; ilk taslağı araştırma gelmeden yapabilirsin. Araştırmanın "büyük değişim" kaldıraçları:
- **Ekran başına bir karar:** soru büyük başlıkta, başlık aynı zamanda alanın etiketi. Birbirine bağlı alanlar (il/ilçe/adres ya da kart numarası/son kullanma/CVC gibi) aynı ekranda kalır.
- **Tek yolculuk çubuğu:** "Adım 3/23" yerine 2–4 bölümlü bir çubuk. Biten bölüm dolu ve ✓ ile gösterilir.
- **Seçim kartları:** 2–4 seçenek için büyük, dokunması kolay kartlar. Otomatik ilerleme yok.
- **Değer ve güven:** ilk ekranda bir karşılama sayfası (değer önerisi + güven maddeleri), carousel değil.
- **Duygusal anlar:** doğrulama sonrası kısa kutlama + yol haritası; sonda "başkaları seni böyle görecek" önizlemesi. Bunları seyrek tut.
- **Koçluk:** fotoğraf ipuçları, ilk mesaj için başlangıç önerileri, boş durumlarda tek sonraki adım.
- **Güvenlik:** şikayet ve engelleme en fazla iki dokunuş uzakta, kapatılabilir güvenlik ipucu.

Önermeden önce her fikri kontrol et:
- **Sunucuda karşılığı var mı?** Bir anahtar ya da ayar öneriyorsan API/modelde alanını ara. Yoksa çizme ya da açıkça "sunucuda ek gerekir" diye işaretle. Örnek: tasarımda çizilen bir "profilimde göster" anahtarının sunucuda alanı yoksa, uygulamaya geçerken çıkarmak gerekir.
- **Bugünkü bir seçeneği kaldırıyor mu?** Gizlilik ve güvenlik seçeneklerini kaldırma, taşı (ör. alt sayfaya).
- **Uydurma var mı?** Uydurma ürün iddiası ("bu seçenek seni öne çıkarır"), uydurma davranış ("karşı tarafa bildirim gitmez") ya da uydurma istatistik yazma. Emin değilsen o cümleyi çıkar.
- **Sıra değişikliği izin/yasal akışı etkiliyor mu?** Örnek: hassas veri izni ilgili sorudan hemen önce gelsin diye soruların sırasını değiştirmek. Bu çoğu zaman sunucu değişikliği gerektirmez.

## 5. Tuvali çiz

Ayrıntılı mekanik `references/canvas-recipe.md`'de; tuvale başlamadan önce oku. Özet:
- **Tuvali aç:** `Artifact` aracıyla `action: "quickstart"`, `intent: "design"` → Design türüyle tuvali oluştur (`type_url`, `title`, `auto_open: "after_first_write"`) → türün talimatlarını izle.
- **Klasör:** tuvalin dosyalarını scratchpad'de, yalnız bu tuvale ait bir klasörde tut. Artifact aracı scratchpad ve çalışma klasörü dışından yayın yapamaz; başka bir tuvalin klasörüne yazmak da onun düzenini bozar.
- **Yükseklik:** çerçeveleri cömert yükseklikte aç. Ölçüp düzeltemeyeceğin için uzun çerçeve, altı kesik çerçeveden iyidir.
- **Düzen:** her akış bir satır, satırın üstünde başlık notu. **Her yeni ekranın soluna bugünkü ekranı koy**: çerçeve adları "Bugün · X" ve "Yeni · X". Kullanıcılar karşılaştırmayı böyle çok daha iyi anlıyor; ayrı bir "bugün" satırı yetmiyor. Bugünkü karşılığı olmayan yeni ekranlarda solu boş bırak ya da en yakın bugünkü ekranı koy ve adında belirt.
- **Ekran içeriği:**
  - gerçek metin, marka token'ları ve gerçek ikon dili;
  - fotoğraf gerekiyorsa projedeki lisanslı deneme fotoğrafları (lisans dosyasını kontrol et), yoksa figür;
  - klavye açık ekranlarda gri "Klavye" bloğu;
  - sahte durum çubuğu yok.
- **Etkileşim:** seçimler, anahtarlar, alt sayfalar ve sekmeler state ile çalışsın; ekranlar arası `<a href="X.dc.html">` ile Play akışı kurulsun.
- **Yazım düzeni:** her dosyayı yaz ve hemen yayınla. Kullanıcı istemedikçe tuvali geri okuyup "doğrulama" yapma.
- **Erişilebilirlik çizimde de geçerli:** gerçek `<button>`/`<a>`/`<input>`, ikon düğmelerde `aria-label`, ≥44 pt hedef, kontrast ≥4.5:1, renk tek başına anlam taşımaz.

## 6. Kullanıcıya sun

Tuval linkiyle birlikte şu yapıda kısa bir mesaj yaz:
1. **Bir cümle:** ne hazırlandı, kod değişmedi, nasıl gezilir (Play).
2. **Link.**
3. **Bugüne göre büyük farklar:** bölüm başına 1–2 madde, somut.
4. **Araştırmanın getirdikleri:** 1–3 madde, kaynak adlarıyla.
5. **Senin kararını isteyenler (davranış değiştiriyor):** numaralı liste. Sıra değişikliği, varsayılan değer, kaldırılan/taşınan seçenek, sunucu eki gerektiren özellik, eşik değeri ("ilk 50 kayıt", "en fazla 3 deneme") gibi. Bunları görsel değişikliklerden ayırmak kullanıcının hızlı karar vermesini sağlar.
6. **Çizilmeyenler** ve bir sonraki adım: onaylarsa uygulama planı.

Kullanıcı bir ekranı reddederse ya da değişiklik isterse yalnız o çerçeveleri düzenle ve yeniden yayınla. Reddedilen öneriyi proje hafızasına "tekrar önerme" diye not et.

## Sınırlar

- Bu skill kod yazmaz, commit atmaz, derleme almaz. Uygulama kullanıcı onayından sonra ayrı bir iştir; orada da bu tuval ve karar listesi kaynak olur.
- Başka bir şirketin özgün tasarımını kopyalama; kalıp (pattern) almak serbest.
- Kullanıcının kişisel verisini (e-posta, ad) tuvale ya da dış araştırma isteklerine koyma; örnek kişiler uydurma ve genel olsun.
