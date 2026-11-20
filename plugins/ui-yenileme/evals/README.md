# Değerlendirme senaryoları

İki örnek senaryo skill'in uçtan uca davranışını ölçer: araştırma, bugün/yeni çiftleriyle Design tuvali, karar listesi ve depoya dokunmama.

- `hesap-silme-bildirim-ayarlari`: mobil uygulamada hesap silme ve bildirim ayarları ekranları.
- `admin-sikayet-inceleme`: web admin panelinde şikayet (moderasyon) inceleme sayfası.

Senaryolar bu ekranlara sahip bir projenin kök dizininde çalıştırılmak içindir:

```
claude plugin eval ui-yenileme@ui-yenileme
```

Kendi projene uymuyorsa `prompt.md` metnini ve `graders/` ölçütlerini projenin ekranlarına göre değiştir.
