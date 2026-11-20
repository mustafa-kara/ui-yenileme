# ui-yenileme

Claude Code için bir skill: bir uygulamanın ekranlarını ya da bir akışını (kayıt, onboarding, anasayfa, profil, mesajlar, ayarlar, ödeme, admin paneli…) araştırmaya dayalı olarak baştan tasarlar.

1. Bugünkü ekranları inceler (ekran görüntüleri, golden/snapshot testleri ya da kod).
2. Arka planda otoritelerden kural toplatır: NN/g, GOV.UK Design System, Baymard, WCAG 2.2, Apple HIG, Material 3, ürünlerin yardım merkezleri.
3. claude.ai **Design tuvalinde** tıklanabilir yeni ekranlar çizer; her yeni ekranın solunda bugünkü hâli durur.
4. Kısa bir özet ve davranış değiştiren kararların numaralı listesini verir.

Kod yazmaz; uygulama, tasarım onaylandıktan sonra ayrı bir iştir. Skill metni ve kullanıcıyla konuşması Türkçedir.

## Kurulum

Bu depo özel (private). Kurmak için depoya erişimin olmalı ve git'in GitHub'a giriş yapabilmesi gerekir (ör. `gh auth login`).

```
claude plugin marketplace add mustafa-kara/ui-yenileme
claude plugin install ui-yenileme@ui-yenileme
```

Claude Code oturumunun içinden aynı işi `/plugin marketplace add mustafa-kara/ui-yenileme` ve `/plugin install ui-yenileme@ui-yenileme` yapar. Güncellemek için: `claude plugin marketplace update ui-yenileme`.

## Gereksinimler

Tasarım tuvali claude.ai'nin Artifact aracıyla yayımlanır. Bunun için:

- Pro, Max, Team ya da Enterprise planı,
- Claude Code'a claude.ai hesabıyla `/login` ile girilmiş olması (API anahtarı, Bedrock, Vertex ya da gateway ile değil),
- güncel bir Claude Code sürümü.

Bunlar yoksa tuval yayımlanamaz; araştırma ve karar listesi yine çıkar.

İsteğe bağlı: ekran görüntülerini birleştirmek ve kırpmak için ImageMagick (`magick`).

## Kullanım

Skill kendiliğinden devreye girer. Örnek istekler:

- "Kayıt akışı çok kötü, baştan tasarla."
- "Ayarlar ekranlarını yenileyelim, otoritelerden araştır, önce/sonra göster."
- "Admin panelindeki sipariş sayfası karışık, daha iyi bir tasarım öner."

Doğrudan çağırmak için: `/ui-yenileme:ui-yenileme`.

## İçerik

```
plugins/ui-yenileme/
├── .claude-plugin/plugin.json
├── skills/ui-yenileme/
│   ├── SKILL.md                    iş akışı
│   └── references/
│       ├── research-brief.md       araştırma alt ajanının brief şablonu
│       ├── design-principles.md    önceki araştırmalardan damıtılmış kurallar
│       └── canvas-recipe.md        Design tuvali mekaniği ve çerçeve iskeletleri
└── evals/                          iki örnek değerlendirme senaryosu
```
