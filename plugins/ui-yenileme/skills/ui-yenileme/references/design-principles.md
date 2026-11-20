# Damıtılmış tasarım kuralları (önceki iki araştırma turundan)

Kaynak: Kasım 2026'da bir sosyal mobil uygulamanın (1) kayıt/onboarding akışı ve (2) ana sekmeleri için yapılan iki araştırma turu. Her projede araştırmayı yeniden yaptır. Bu liste başlangıç noktası ve kontrol listesidir; şirket beyanı sayılar "şirket beyanı" diye işaretli.

## Akış ve formlar
1. **Ekran başına bir karar, alan başına bir ekran değil.** Birbirine bağlı alanlar aynı ekranda kalır. Soru büyük başlıkta, başlık alanın etiketi. (GOV.UK question pages; Android onboarding "don't overdo one input per screen"; NN/g progressive disclosure)
2. **Önce soruları azalt, sonra böl.** Tek soruluk ekranlar çok soruyu gizlemek için kullanılmaz (GDS). Couper vd. 2001: tek soruluk ekranlar biraz daha yavaş ama boş bırakılan alan daha az.
3. **Ana düğme hep basılabilir.** Basınca hata alanın altında görünür, odak ilk hataya gider. Doğrulama alandan çıkınca yapılır; hata düzelince hemen kalkar. Placeholder yalnız "örn." ile örnek olabilir. (NN/g Forms, Baymard inline validation, Axess Lab disabled buttons)
4. **Bölümlü ilerleme çubuğu, "3/23" değil.** Biten bölümler dolu görünür. Hızlı ekranlar başa konur. Eşit hızda ilerleyen çubuk tek başına terk oranını düşürmez; yavaş başlayan çubuk artırır (City Univ. meta-analizi). "Hazır doldurulmuş ilerleme" etkisi gerekçe ister (Nunes & Drèze).
5. **Ölçülmemiş süre vaat etme** ("2 dakika"). Vaadi aşmak terki artırır.
6. **İsteğe bağlı adımlarda görünür "Şimdilik geç"** ve her adımda kayıt + kaldığı yerden devam (NN/g, Android).
7. **Seçim kartları otomatik ilerlemez** (WCAG 3.2.2 On Input). 2–4 seçenek için tam genişlikte radyo kartları kullanılır.
8. **Onay penceresi yalnız ciddi ve geri dönüşsüz yerde.** Sonucu yazar; düğmeler sonucu adlandırır ("Evet, doğru" / "Düzelt"), varsayılan seçili düğme olmaz. (NN/g confirmation dialogs)
9. **Rıza tam ihtiyaç anında istenir.** Örnek: özel nitelikli veri izni ilgili sorudan hemen önce gelir. Bilgi eksilmez; reddetme yolu tasarlanır. Hukuk onayı gerekir.
10. **Kod ekranı:** tek alan altı kutu görünümünde; tam kod yapıştırma ve OS otomatik doldurma açık; e-posta + "Değiştir" görünür; yeniden gönderme sayacı bitince gerçek düğme olur (WCAG 3.3.8). "Mail uygulamasını aç" yaygın bir kalıp ama otorite kaynağı yok.
11. **Önceki cevap tekrar sorulmaz** (WCAG 3.3.7): okul e-postadan geliyorsa tekrar sorma.
12. **Karşılama:** tek değer ekranı, carousel değil (NN/g mobile onboarding). Kaydı biraz geciktirmek bazı ürünlerde etkinliği artırdı (Duolingo, şirket beyanı).
13. **Sonda önizleme ve kısa bir başarı anı.** Önizlemedeki alana dokununca o adıma gidilip geri dönülür (GOV.UK check answers, Android "sense of accomplishment").

## Akış içi ekranlar (feed, profil, mesaj, ayarlar)
Bu bölümdeki örnekler sosyal bir uygulamadan; başka alanlarda (e-ticaret, randevu, içerik) karşılığını bul.
14. **Kart hiyerarşisi:** fotoğraf → ad, yaş, doğrulama rozeti → okul → tek kısa öneri. Kartın her yerine dokununca detay açılır; beğeni ayrı bir kontroldür. (NN/g cards)
15. **Fotoğraf üstü yazı yalnız alttan koyulaşan zemin üzerinde** ve en parlak fotoğrafla test edilir (NN/g text over images, WCAG 1.4.3).
16. **Akışın bir sonu olsun** ("Bugünlük yeni profil kalmadı" + filtre değiştir). Dönüşte kaydırma konumu korunur. Çok profil değerlendirmek reddetme eğilimini artırır (SPPS 2019).
17. **Detayda sabit eylem çubuğu**, son içeriğin ve odaktaki öğenin altında boşlukla (WCAG 2.4.11, F110).
18. **Beğeni ≥44 pt.** Beğenilmiş durum ikon + metinle gösterilir ("Beğenildi"), yalnız renkle değil; sonuç durum mesajı olarak duyurulur (WCAG 2.5.8, 1.4.1, 4.1.3).
19. **Sıralama:** ilk N kişi sıcak bir dille gösterilir. Kullanıcıya düşük sırası ya da sıfır sayısı gösterilmez. Haftalık sıfırlama görünür; "sıralamada görünme" seçeneği düşünülür. (Emerald 2022; Instagram like gizleme)
20. **Boş durum:** neden boş olduğunu söyler ve tek sonraki adım verir. İskelet yükleme yalnız ~1 sn'den uzun tam ekran yüklemelerde kullanılır (NN/g).
21. **Mesaj istekleri** ayrı bölümde, sayıyla. "Kabul et", "Sil" ve "Engelle ve bildir" eşit görünürlükte. Kabulden önce okundu bilgisi gitmez (Instagram/Meta yardım).
22. **İlk mesaj:** karşı tarafın sorularından 2–3 başlangıç önerisi ve görünür karakter sınırı (Bumble Opening Moves). Gönderim öncesi kibar "emin misin?" uyarısı (Tinder, şirket beyanı).
23. **Engelle ve bildir en fazla iki dokunuş uzakta**, sohbet menüsünden ve profilden, her yerde aynı etiketle. Bildirimin gizli kaldığı söylenir.
24. **Şikayet akışı:**
    - ekran başına bir soru;
    - önce "ne oldu" nedenleri;
    - ayrıntı isteğe bağlı;
    - sonda ne olacağını anlatan onay ekranı ve engelle seçeneği;
    - durum şikayet geçmişinde görünür (Twitter semptom-önce: şikayet edilebilir rapor +%50, şirket beyanı; GOV.UK confirmation pages).
25. **Ayarlar:** özgül grup başlıkları ("Genel" değil), ekran başına ≤10–15 öğe, her satırda şu anki değer. Bu boyutta arama gerekmez (Android settings guidelines).
26. **Yıkıcı eylemler en sonda ve ayrı:**
    - onay sonuçları ve bekleme süresini listeler;
    - düğme eylemi adlandırır;
    - hesap silme uygulama içinden başlatılabilir (Apple hesap silme şartı).
27. **Alt gezinme:** 5 etiketli sekme, sabit sıra. Sayılı rozet yalnız mesajlarda; ziyaret edilince temizlenir (Apple HIG tab bars, M3 badges).
28. **Büyük başlık yalnız sekme köklerinde**, açılan sayfalarda küçük başlık (yaygın uygulama).
29. **Profil tamamlama göstergesi:**
    - adlandırılmış seviye ve tek somut sonraki adım;
    - tamamlanınca kaybolur;
    - görünürlüğü yüzdeye bağlamaz (LinkedIn).
30. **Düzenlerken "başkaları nasıl görüyor" geçişi** (Hinge).

## Kaçınılacaklar
- Bulanık "seni beğenenler" teaser'ı, tekrar eden yükseltme/bildirim istekleri, hesap silmede suçluluk dili.
- Düşük sıradakilere kesin sayı, "sıralamada düştün" bildirimi, arkadaşla kıyas.
- Seri (streak), giriş ödülü, her beğenide konfeti. Kutlama nadir, kısa ve azaltılmış harekete saygılı olmalı.
- Her sekmede rozet, pazarlama rozeti, sonsuza dek dürten tamamlama göstergesi.
- İstekte "görüldü" baskısı.
- Şikayeti ikiden çok dokunuş derine gömmek, zorunlu uzun metin, şikayet edeni açığa çıkarmak.
