# Araştırma alt ajanı için brief şablonu

Bu brief'i genel amaçlı alt ajana arka planda (`run_in_background: true`) ver. Köşeli parantezli yerleri doldur. Rapor İngilizce gelir, kullanıcıya özetlerken kullanıcının diline çevir. Alt ajan web'de araştırır ve kod yazmaz.

Kişisel veri (kullanıcının adı, e-postası, proje sahibinin kimliği) brief'e girmez. Ürünü genel tarif et ("Türkiye'de küçük işletmeler için randevu uygulaması" gibi tek bir cümle yeterli).

---

```
You are researching [mobile | web | admin-panel] UX for [one-line product description, market, language, platform/framework, brand notes such as "<brand color> accent, <font> font, light theme only"].

Context: [what the team already did, e.g. "basic form hygiene is done: labels above fields, placeholders only as examples, validate on blur, primary button always tappable". The owner says that was only polish and wants a substantially better experience.] Your job is to find what authoritative sources and best-in-class products do, so we can design a big redesign of [scope, e.g. "the registration flow only" / "the main tabs: home, search, orders, messages, profile, settings"].

Product model (fixed by the client, do NOT propose changing it): [rules such as "payment only on delivery; guests can browse but not order"; approved decisions like "the product image ratio is approved and must stay"].

Current flow / screens (in order): [screen → screen → …, with what each one asks or shows].

Research, citing sources with URLs:
1. Authoritative guidance: Nielsen Norman Group, Baymard Institute, GOV.UK Design System, Apple Human Interface Guidelines, Material Design 3, WCAG 2.2 [add domain-specific ones: e.g. KVKK/GDPR for consent, PCI for payments, Android/Apple onboarding guidance]. Extract concrete, actionable rules (what to do and why), with numbers where available.
2. Best-in-class product patterns in this domain: [the 3–5 best products in this domain and adjacent apps; widely praised onboarding: Duolingo, Headspace, Airbnb]. Describe patterns (layout, progress, choice controls, empty states, celebratory moments, safety affordances, sensitive questions). Prefer official help centers; mark secondary write-ups as such and company-reported numbers as "company-reported".
3. Specific evidence on: [the open design questions, e.g. "one-question-per-screen vs grouped", "progress indicators", "estimated time", "skip affordances", "gamification and harm", "when to ask for notification permission"].
4. Accessibility points for these screens (WCAG 2.2: 2.4.3 focus order, 2.4.11 focus not obscured, 2.5.7 dragging, 2.5.8 target size, 3.2.2 on input, 3.3.7 redundant entry, 3.3.8 accessible authentication, 1.4.3 contrast over photos, 4.1.3 status messages — pick the relevant ones).

Deliver a concise report in English (max ~1000 words):
(a) 12–15 concrete design rules for these screens, each with a one-line rationale and source URL;
(b) patterns from comparable products worth adopting (patterns only, no copying of branding or visuals);
(c) evidence AGAINST popular patterns or things to avoid (dark patterns, gamification harms, over-badging, overdoing one-question-per-screen), so we don't overdo it.
Do not write code. Do not include any personal data. Say which sources you could not verify.
```

---

## Platforma göre ek kaynaklar

- **Mobil uygulama:** Apple HIG (tab bars, onboarding, sheets), Material 3 (navigation bar, badges, onboarding), Android onboarding rehberi.
- **Web/admin paneli:** NN/g (data tables, filters, bulk actions, dashboards), GOV.UK (task list, check answers, confirmation pages), Baymard (form ve tablo kalıpları), WCAG 2.2 tablo ve klavye erişimi. Admin araçları için "moderation queue" ve "case management" örnekleri (Trust & Safety araçları yazıları).
- **Ödeme/sepet:** Baymard checkout araştırmaları, PSD2/3DS akış yönergeleri.
- **Rıza ve yasal:** ilgili yasa ve kurul kararları (KVKK, GDPR), "just-in-time consent" kalıbı. Hukuk onayı gerektiğini rapora yazdır.
