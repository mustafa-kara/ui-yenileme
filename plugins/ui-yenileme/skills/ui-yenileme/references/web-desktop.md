# Masaüstü web: ayrı kompozisyon kuralları

Herkese açık bir web sitesini ya da web uygulamasını yenilerken bu dosyayı oku. Admin panelleri için de geçerli; oradaki fark §6'da.

Bu dosya bir geri bildirimden doğdu: skill'in mobil tasarımı beğenildi, masaüstü tasarımı beğenilmedi. Masaüstü sayfa, mobil yapının 1440 px'e yayılmış hâliydi:
- üstte fotoğraf ve arama;
- ardından art arda üç tane eşit 4'lü kart satırı;
- sağ yarısı boş bir üst alan;
- aramanın sonucunu yanında değil "aşağıda" gösteren bir düzen.

Sadeleştirme dar ekranda kazanç sağlıyor, geniş ekranda ise sayfayı boş ve sıradan gösteriyor. Mobil önce tasarlanabilir, ama masaüstü onun geniş hâli değildir (NN/g, "Mobile-First Is NOT Mobile-Only").

## 1. Masaüstü ve mobil iki ayrı kompozisyon

- Her bölüm için "geniş ekranda ne kazanıyoruz?" sorusunu yaz ve cevabını çiz. Cevap yoksa o bölüm masaüstünde gereksiz olabilir.
- Duyarlı (responsive) aynı DOM yeterli değilse masaüstünde farklı bir yerleşim öner, ör.:
  - mobilde alt alta duran arama ve sonuçlar → masaüstünde yan yana;
  - mobilde yatay kaydırılan kart şeridi → masaüstünde ızgara ya da liste ve detay.
- Genişlik sınıflarını kaynak al (Material 3 window size classes): compact < 600, medium 600–839, expanded 840–1199, large 1200–1599, extra-large ≥ 1600. Çizimde en az iki masaüstü genişliğine bak: 1440 ve 1280.
- Material 3'ün "canonical layouts"u masaüstü için iyi bir başlangıç listesidir:
  - **liste–detay:** seçilen öğe sağda açılır, liste kaybolmaz;
  - **destek paneli:** ana içerik + yan bilgi;
  - **akış:** çok sütunlu kart ızgarası.

## 2. Hiyerarşi: her bölüm aynı ağırlıkta olmasın

- Sayfada tek bir birincil iş olsun. Pazar yeri ve arama sitelerinde bu iş genellikle aramadır. Birincil iş en çok alanı ve en güçlü görsel ağırlığı alır.
- Art arda aynı biçimde bölüm koyma (başlık + "Tümü" + 4 eş kart, üç kez). Bölümleri ritimle ayır:
  - bir geniş öne çıkan blok;
  - iki sütunlu bir düzen (ör. sol liste, sağ harita ya da özet);
  - yoğun bir liste;
  - dar bir bilgi şeridi.
- Göz F biçiminde tarar (NN/g F-shaped pattern). Kararı belirleyen bilgi (fiyat, puan, konum, uygunluk) satırların başında ve sol sütunda olsun; dekoratif fotoğraf bu alanı yemesin.
- Üst alanda (hero) masaüstünün sağ yarısını boş fotoğrafa bırakma. Ya arama ve önizleme sonuçları, ya bir harita, ya canlı içerik (öne çıkan ilan, yaklaşan etkinlik), ya da açıkça seçilmiş tek güçlü görsel.

## 3. Bilgi yoğunluğu ve karşılaştırma

- Masaüstü kullanıcısı çoğu zaman karşılaştırır. Kartlar ya da liste satırları karar için gereken alanları taşısın: fiyat ve birimi, puan ve yorum sayısı, konum ve mesafe, tür ya da kategori, uygunluk. Mobilde kesilen alanlar masaüstünde geri gelir.
- Çok sonuç varsa ızgara yerine ya da yanında liste görünümü ve sıralama sun. Liste mi ızgara mı sorusu ürüne göre değişir: görselin karar verdiği ürünlerde ızgara, özelliklerin karar verdiği ürünlerde liste (Baymard ürün listesi araştırmaları).
- Filtreler masaüstünde sol sütunda sürekli görünür (Baymard). Uygulanan filtreler sonuçların üstünde kaldırılabilir etiketlerle gösterilir. Mobilde aynı filtreler alt sayfaya taşınır.
- Metin satırı 50–75 karakter (Baymard ve tipografi kaynakları). Uzun metin bloklarını tam genişliğe yayma; geniş alanı sütunlarla kullan.

## 4. Gezinme ve masaüstü davranışları

- Çok kategorili sitelerde üst menüde açılır menü ya da mega menü değerlendir (NN/g mega menus). Kategoriler gruplu, metinle ve tıklanınca açılsın. Yalnız fareyle üzerine gelince açılan menü klavye ve dokunmatik ekranlı dizüstüler için yetmez.
- Fareyle üzerine gelince ek bilgi verilebilir, ama aynı bilgi tıklama ya da odakla da erişilebilir olmalı. Hover içeriği kapatılabilir, üzerine gelinebilir ve kalıcı olmalı (WCAG 1.4.13).
- Klavye: görünür odak halkası (WCAG 2.4.7, 2.4.11), mantıklı sekme sırası, "içeriğe atla" bağlantısı.
- Bölümler arası atlama için sayfa içi bağlantılar ya da yapışkan (sticky) bir alt menü uzun sayfalarda işe yarar. Yapışkan öğe odaktaki içeriği örtmesin.

## 5. Mobil kompozisyon (aynı sayfanın dar hâli)

- Arama ve birincil iş ilk ekranda.
- Uzun kart listeleri yatay kaydırılan şeritlere ya da "Tümü" bağlantısına iner.
- Filtreler alt sayfada.
- Tablo yerine kart.
- Metin ve dokunma hedefi ölçüleri mobil kurallarla aynı (≥ 44 pt, WCAG 2.5.8).
- WCAG 1.4.10 (reflow): 320 CSS px genişlikte yatay kaydırma olmadan okunabilmeli.

## 6. Admin panelleri

Admin ekranları çoğu zaman yalnız masaüstündür. Kurallar:
- yoğun tablo;
- kalıcı filtre sütunu;
- liste–detay ya da sayfa içi karar paneli;
- toplu işlem;
- klavye kısayolları.

Mobil kompozisyon istenmedikçe çizilmez, ama 1280 genişlikte kırılmamalı.

## 7. Tuvalde

- Herkese açık web sayfası için iki satır çiz:
  - "Masaüstü — solda bugün, sağda yeni" (1440);
  - "Mobil — solda bugün, sağda yeni" (390).

  Masaüstü çerçevesini 1280'de de kontrol et. Mümkünse ikinci bir masaüstü çerçevesi koy ya da çerçeve notuna "1280'de de kırılmadan çalışır" diye yaz.
- Masaüstü ve mobil aynı örnek veriyle çizilsin: biri boş durum, öteki dolu liste gösteriyorsa karşılaştırma yanıltır. Boş durum gerekiyorsa ayrı bir çerçevede göster.
- Sayfanın her bölümünü çiz. Footer gibi değişmeyen bölümleri "değişmedi" yazılı boş bir şeritle bırakma; bugünkünü taşı. Yarım görünen tuval tasarımı olduğundan kötü gösterir.
- Kullanıcıya sunarken masaüstü için ayrıca "geniş ekranda ne kazandık" maddesi yaz: 2–3 somut fark, ör. "arama sonuçları üst alanda haritayla yan yana", "filtreler sol sütunda sabit", "kartlarda fiyat ve mesafe".

## Kendi kendine kontrol (masaüstü çerçevesini yayınlamadan önce)
- [ ] Masaüstü düzen, mobil düzenin genişletilmiş hâli değil; en az iki bölüm masaüstünde farklı yerleşiyor.
- [ ] Üst alanın her iki yarısı da işe yarıyor.
- [ ] Art arda aynı biçimde üç bölüm yok.
- [ ] Kartlar ya da satırlar karşılaştırma için gereken alanları taşıyor.
- [ ] Filtre ve sıralama (varsa) masaüstünde sürekli görünür.
- [ ] Hover'a bağlı bilgi tıklama ve odakla da erişilebilir.
- [ ] Masaüstü ve mobil aynı örnek veriyi gösteriyor; footer dahil hiçbir bölüm "değişmedi" şeridi değil.
