# Design tuvali tarifi

Bu sayfa claude.ai Design tuvalinin pratik mekaniğini anlatır. Design türünün kendi talimatları (`Artifact` yanıtında gelir) her zaman önceliklidir; burada yalnız bu skill'de işe yarayan kalıplar var.

## İçindekiler
1. Tuvali açma
2. Çalışma klasörü ve görseller
3. Golden'dan telefon karesi kırpma
4. Tuval düzeni (bugün/yeni çiftleri)
5. Yazma ve yayınlama düzeni
6. Çerçeve iskeletleri (telefon, alt gezinme, seçim kartı, alt sayfa, bugünkü ekran, web sayfası)
7. Sık hatalar

## 1. Tuvali açma
- `Artifact` → `action: "quickstart"`, `intent: "design"`. Tasarım sistemi yoksa ya da kullanıcı istemediyse `design_systems: false`.
- Dönen Design `type_url` ile oluştur: `title` (kullanıcının diliyle, ör. "Kayıt Akışı Yeni Tasarım"), `auto_open: "after_first_write"`, başka bir şey yok. Yanıtta türün talimatları ve `format.md` gelir; ilk çerçeveden önce oku.
- Tuval adresini proje hafızasına ve bir not dosyasına yaz. Sonraki turlarda aynı tuvale yayınlarsın.

## 2. Çalışma klasörü ve görseller
- **Kök scratchpad'de ya da çalışma klasöründe olmalı.** Artifact aracı bunların dışındaki bir klasörden (ör. `~/.claude/...`, başka bir proje) yayın yapamaz. Çıktının başka bir yerde de durması gerekiyorsa tuvali scratchpad'de kur, yayından sonra dosyaları oraya kopyala.
- **Her tuvale kendi klasörü:** ör. `<scratchpad>/<tuval-adı>/`. Aynı oturumda başka bir ajan ya da başka bir tuval aynı scratchpad'i kullanabilir; başkasının `project/canvas.json` dosyasına yazarsan onun düzenini bozarsın.
- Klasörün altında `project/` (tuval dosyaları) ve `assets/` (yüklenecek görseller) durur.
- Görselleri ImageMagick ile hazırla:
  - **Ekran görüntüsü:** `magick in.png -resize 390x -quality 78 -strip assets/now-<ad>.jpg`
  - **Fotoğraf (4:5):** `magick p.jpg -resize 480x600^ -gravity center -extent 480x600 -quality 76 -strip assets/pNN.jpg`
  - **Logo:** `-resize 360x -quality 85`
- Yükleme: `Artifact` publish, `url` + `asset: true` + `file_paths` (en çok 25 dosya). Yanıttaki `/_blob/<id>` adreslerini **hemen** `assets/blobs.txt` dosyasına yaz (ad, id, kısa açıklama, ör. "kişi, kısa saç, dış mekân"). Bağlam sıkıştırılınca bu liste kaybolmasın.
- Gerçek kişi fotoğrafı yalnız lisansı açıksa kullanılır: projedeki mock fotoğrafların `CREDITS.md`/lisans dosyasına bak. Yoksa basit figür (daire baş + omuz yolu) çiz.

## 3. Golden'dan telefon karesi kırpma
Flutter alchemist golden'ları çoklu cihaz ızgarasıdır. Örnek: 1945×2406 = sütunlar 360 | 390 | 820 | 375 genişliğinde; üst sıra 1.0×, alt sıra 2.0×. 390×844 1.0× karesi ikinci sütunun en üstündedir:

```bash
magick golden.png -crop 390x844+360+16 +repage -quality 80 -strip assets/now-<ad>.jpg
```

Üstteki ~16 px cihaz etiketidir ("390x844 · 1.0x"). Ofseti emin değilsen önce `-crop 390x860+360+0` ile çıkarıp bak. Izgara düzeni projeye göre değişebilir: `magick identify` ile boyutu al, etiket metinlerinden sütunları çöz.

Önizleme için birkaç kareyi yan yana koyup kendin incele:
`magick \( a.png -crop … \) \( b.png -crop … \) +append -resize 1170x out.jpg`

## 4. Tuval düzeni (bugün/yeni çiftleri)
- Telefon çerçevesi 390×844, `"radius": 44`. Yeni ekranlarda `"is_interactive": true`.
- Çerçeve adları: `"Bugün · Anasayfa"` / `"Yeni · Anasayfa"`. Dosya adları: `OldMain.dc.html` / `Main.dc.html`. İlk yeni ekran `Main.dc.html` olmalı (giriş çerçevesi).
- **Çift:** bugünkü `x`, yeni `x + 430`; çift genişliği 820. Çiftler arası 140 boşluk, yani çift adımı 960. Satırda 3 çift (satır genişliği 2740).
- **Satır adımı 1184:** her satırın üstünde ≥223 px başlık alanı. Başlık notu `{"x":0,"y":<satırY-300>,"text":"1 · Ana sayfa (solda bugün, sağda yeni)","kind":"title1","maxW":2740}`.
- Web sayfası çerçevesi: `w` 1440, `"expand": "fill"`, `h` = sayfanın 1440 genişlikteki yüksekliği. Çiftler alt alta durur: bugün üstte, yeni altta.
- **Yükseklikte cömert ol.** Tuvali geri okuyup ölçmüyorsun, o yüzden yüksekliği bölümlerin toplamından tahmin et ve üstüne %20 ekle. Uzun çerçeve kesik çerçeveden iyidir; altı kesik bir sayfa kullanıcıya bozuk görünür. Telefon ekranında da içerik 844'ü aşıyorsa ya içeriği kısalt ya da "kaydırılmış" hâli ayrı bir çift olarak çiz.
- **Bugünkü ekranın görüntüsü yoksa** (ör. admin paneli, çalıştırılamayan sunucu) bugünkü sayfayı koddan sadık biçimde yeniden çiz: alanlar, düğmeler, sıralar ve metinler kaynaktaki gibi. Çerçeve adına bunu yaz: `"Bugün · Sipariş detayı (koddan yeniden çizildi)"`. Kullanıcı neyin gerçek ekran görüntüsü, neyin yeniden çizim olduğunu bilmeli.

```json
"OldMain.dc.html": {"x": 0,   "y": 0, "w": 390, "h": 844, "title": "Bugün · Anasayfa", "radius": 44},
"Main.dc.html":    {"x": 430, "y": 0, "w": 390, "h": 844, "title": "Yeni · Anasayfa", "is_interactive": true, "radius": 44},
"OldProfile.dc.html": {"x": 960, "y": 0, …}, "Profile.dc.html": {"x": 1390, "y": 0, …}
```

## 5. Yazma ve yayınlama düzeni
- **İlk çağrı:** önce `project/canvas.json` dosyası, tam hâliyle; bütün çerçeveler `boards` ve `order` içinde, `createdOnFiles` şu anki zamanla. Sonra `project/Main.dc.html`. İkisini tek publish ile gönder (`url`, `root`, `file_path` = canvas.json, `files` = Main).
- **Sonra:** her seferinde bir dosya yaz ve hemen yayınla (`file_path` = o dosya). Art arda iki Write yapma. Bu kural türün talimatından geliyor ve kısmi yayınların tutarlı kalmasını sağlıyor.
- **Küçük düzeltme:** Edit + aynı dosyanın publish'i aynı yanıtta. Read yok.
- **Düzen değişikliği:** önce `read` ile `project/canvas.json`'u yeniden oku, açıp bak. Kullanıcı çerçeveleri elle taşımış olabilir. Yalnız kendi anahtarlarını değiştir.
- **Çerçeve silme:** `files: {"project/X.dc.html": null}` ve index'ten çıkar.
- **Doğrulama:** kullanıcı istemedikçe tuvali geri okuma, ekran görüntüsü alma, tarayıcıda açma.
- **İlerleme bilgisi:** 3–4 yayında bir kullanıcıya tek cümle ver ("Kayıt ve kod ekranları hazır, sırada izin ekranları").

## 6. Çerçeve iskeletleri
Hepsinde: `<html lang="tr">` (metnin dili), kendi `<title>`, `<script src="./support.js"></script>` satırı aynen, `<helmet>` içinde Google Fonts `css2` linki ve `body{margin:0}`. Tutarlılık için stil satır içi (`style="…"`); `{{hole}}` yalnız noktalı arama, ifade değil; mantık `class Component extends DCLogic` + `renderVals()`; `data-props` tek tırnaklı JSON, `$preview` boyutu.

### Telefon ekranı (soru ekranı)
```html
<div style="width: 390px; height: 844px; position: relative; overflow: hidden; background: <canvas>; font-family: <Font>, system-ui, sans-serif; color: <ink>">
  <!-- Üst satır: geri + yolculuk çubuğu + sağ eylem (Geç / ⋯) -->
  <div style="position: absolute; left: 0; right: 0; top: 50px; padding: 0 16px 0 8px; display: flex; align-items: center; gap: 8px">
    <a href="Prev.dc.html" aria-label="Geri" style="width: 44px; height: 44px; display: flex; align-items: center; justify-content: center">…chevron svg…</a>
    <div style="flex: 1; display: flex; flex-direction: column; gap: 6px; padding-top: 12px">
      <div style="display: flex; gap: 6px">
        <div style="flex: 1; height: 6px; border-radius: 3px; background: <primary>"></div>
        <div style="flex: 1; height: 6px; border-radius: 3px; background: <track>"><div style="width: 50%; height: 6px; border-radius: 3px; background: <primary>"></div></div>
        <div style="flex: 1; height: 6px; border-radius: 3px; background: <track>"></div>
      </div>
      <div style="display: flex; gap: 6px; font-size: 12px; font-weight: 600"><span style="flex: 1">Hesap ✓</span><span style="flex: 1; color: <primaryStrong>">Bilgiler</span><span style="flex: 1">Tercihler</span></div>
    </div>
    <span style="width: 44px"></span>
  </div>
  <!-- Başlık ve açıklama -->
  <div style="position: absolute; left: 24px; right: 24px; top: 140px; display: flex; flex-direction: column; gap: 10px">
    <h1 style="margin: 0; font-size: 32px; line-height: 38px; font-weight: 800; letter-spacing: -0.02em">Adın ne?</h1>
    <p style="margin: 0; font-size: 16px; line-height: 24px; color: <inkSecondary>">Profilinde böyle görünecek.</p>
    <!-- büyük alt çizgili alan: border-bottom 2px primary, 22–30px yazı -->
  </div>
  <!-- Klavyeye yaslanan CTA + klavye yer tutucusu -->
  <div style="position: absolute; left: 24px; right: 24px; bottom: 312px"><a href="Next.dc.html" style="height: 56px; border-radius: 28px; background: <primary>; color: #fff; display: flex; align-items: center; justify-content: center; font-weight: 700; text-decoration: none">Devam</a></div>
  <div style="position: absolute; left: 0; right: 0; bottom: 0; height: 296px; background: #E6E1E3; display: flex; align-items: center; justify-content: center; font-size: 13px">Klavye</div>
</div>
```
Klavye kapalı ekranlarda CTA `bottom: 34px` olur.

### Alt gezinme (sekme kökleri)
`<nav aria-label="Ana gezinme">`, 84 px yüksek, beyaz, üstte 1 px kenar, 5 eşit `<a>`. Etkin sekmede ikonun arkasında 56×30 hap (`primaryContainer`), dolu ikon, kalın etiket ve `aria-current="page"`. Sayılı rozet yalnız mesajlarda; sekme `aria-label="Mesajlar, 3 okunmamış"`.

### Seçim kartı (state ile)
```js
renderVals() {
  const opts = [{ id: 'p', label: 'Bireysel' }, { id: 'c', label: 'Kurumsal' }];
  return { options: opts.map((o) => { const on = this.state.picked === o.id; return {
    label: o.label, checked: on ? 'true' : 'false', pick: () => this.setState({ picked: o.id }),
    style: '… height: 64px; border-radius: 16px; ' + (on ? 'background: <blush>; border: 2px solid <primary>;' : 'background: #fff; border: 1.5px solid <borderStrong>;'),
  }; }) };
}
```
Şablonda `<button type="button" role="radio" aria-checked="{{o.checked}}" onClick="{{o.pick}}" style="{{o.style}}">`, sarmalayıcıda `role="radiogroup"`.

### Alt sayfa / onay
`<sc-if value="{{sheet}}" hint-placeholder-val="{{ true }}">` içinde tam ekran yarı saydam zemin + alttan `border-radius: 28px 28px 0 0` beyaz panel, `role="dialog" aria-modal="true"`. Tuvalde açık görünsün diye başlangıç state'i açık; "Düzelt" kapatır.

### Bugünkü ekran çerçevesi
```html
<div style="width: 390px; height: 844px; overflow: hidden; background: <canvas>">
  <img src="/_blob/<id>" alt="Bugünkü <ad> ekranı" style="width: 390px; height: 844px; object-fit: cover; object-position: top; display: block">
</div>
```

### Web sayfası
Çerçeve `"expand": "fill"`. Kökte px genişlik yok: `max-width` kapsayıcı, `%`/`fr`. Yan menü + içerik `flex-wrap: wrap` satırı, içerik `flex: 999 1 560px; min-width: 0`. Geniş tablo `overflow-x: auto` kutuda. Dar ekranda menü üstte yığılır.

## 7. Sık hatalar
- **Uydurma:** ürün iddiası, davranış ("engellenen kişiye bildirim gitmez"), sayı. Emin değilsen o cümleyi çıkar.
- **Sabit liste değişikliği:** şikayet nedenlerinden birini düşürmek ya da "Başka bir şey" eklemek gibi. Bugünkü listeyi birebir kullan.
- **Sunucuda olmayan ayar:** bir anahtar çizmeden önce API alanını ara.
- **Fotoğraf üstünde zeminsiz yazı:** alttan koyulaşan zemin kullan, en parlak fotoğrafla dene.
- **Sabit alanın arkasında kalan son öğe:** gövdenin altına boşluk bırak; kayan gövde altta görünür biçimde kesilmesin.
