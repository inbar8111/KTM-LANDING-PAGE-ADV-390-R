# KTM Israel — Design System

Brand & UI system for **KTM Israel** marketing surfaces — currently the **ADV 390 R** lead-capture landing page and the agency-side lead-notification email. Everything in this repo is derived from a real, shipping Next.js codebase and the official KTM "Ready to Race" logo provided by the client.

---

## Sources

| Source | Path / Location | Notes |
|---|---|---|
| Codebase | `דף נחיתהADV 390/` (locally-mounted) | Next 16 + React 19 + Tailwind v4 RTL Hebrew landing page for ADV 390 R |
| Brand mark | `uploads/347773548_3503163139966089_8062529241926366253_n.png` | Orange-on-orange "KTM" badge — KTM Israel Instagram/Facebook avatar |
| Hero photography | `דף נחיתהADV 390/public/hero-bike.jpg` | KTM ADV 390 R, off-road environment, available light |
| KTM corp logo | `דף נחיתהADV 390/public/ktm-logo.png` | Black "Ready to Race" wordmark |
| Email template | `דף נחיתהADV 390/email-template.html` | Lead notification, light theme |

> KTM Israel runs as an importer/dealer network. Distinctive customer-facing copy is in **Hebrew, RTL**. Product names ("ADV 390 R", "WP APEX", "TFT") stay in English and tend to read LTR even when wrapped in RTL containers.

## Products represented

1. **ADV 390 R Landing Page** — a single-page lead-capture site. Mobile-first scroll experience (video → offer → form); desktop is a single-viewport split layout with the hero photo full-bleed and the form pinned to the bottom strip.
2. **Lead notification email** — internal-facing, light theme, agency-distribution. Reuses brand orange and Hebrew copy patterns.

There is no consumer app, no docs site, no broader marketing site in scope yet.

---

## Index

```
README.md                  ← you are here
SKILL.md                   ← Agent-Skills shim so this folder works in Claude Code
colors_and_type.css        ← all design tokens as CSS custom properties
assets/                    ← logos, hero photography
preview/                   ← Design-System tab cards (typography, color, components)
ui_kits/
  adv-390-landing/         ← interactive recreation of the landing page
    index.html             ← desktop split-layout view (interactive)
    README.md
    components/*.jsx       ← Hero, LeadForm, MobileOffer, PriceBadge, etc
```

---

## Content Fundamentals

KTM Israel's voice is **direct, present-tense, plural-imperative**, with English product names threaded through a Hebrew sentence.

**Voice — who's talking to whom**
- The brand addresses readers as **אתם / you (plural masculine)** — "השאירו פרטים", "מלאו את הפרטים", "צפו בסרטון". Never the formal "אתה" or "את".
- KTM never says "I". The brand is a "we" that mostly disappears — most copy is imperative or descriptive.
- It's not chummy. It's clipped, confident, slightly aggressive. Like a sales floor at a motorcycle shop.

**Voice — what it sounds like**
- **Short sentences. Two- or three-word fragments are normal.** Hero copy is built from chunks: *"יש כאלה שרוכבים בכביש / ויש כאלה שרוכבים על / ADV 390 R"*.
- **Numbers do the heavy lifting.** "1,958 ₪/חודש", "24 תשלומים", "ריבית 0%", "45 כ״ס | 37 ניוטון-מטר". Specifics > adjectives.
- **No emoji in the public-facing landing page.** Emoji appear only in the internal lead-notification email (🏍️ 👤 📞 ✉️ 📍 🕐 🌐 ⚡ 📞 💬) where they act as quick scan-aids for the dealer reading the email, not as brand voice.
- **No exclamation points** in marketing copy on the landing page. The only "!" in the codebase is `תודה!` in the success modal — gratitude, not excitement.

**Casing & punctuation**
- **English product names stay UPPERCASE**: KTM, ADV 390 R, ABS, TCS, TFT, WP APEX, GPS.
- **Eyebrow labels are UPPERCASE-equivalent in Hebrew** by using massive letter-spacing (0.3em) on short labels like *"ההצעה"*, *"הטכנולוגיה"*. Hebrew doesn't have case, so wide tracking is how KTM signals "this is a label, not a sentence".
- **Currency**: numeral first, then ₪. *"1,958 ₪"* — not "₪1,958".
- **Slash separates spec values**: *"45 כ״ס | 37 ניוטון-מטר"*. Pipe with space on both sides.
- **English-Hebrew bilingual lines stay LTR for the English bit**: phone numbers and emails use `direction: ltr; text-align: right;` so the digits read naturally inside an RTL paragraph.

**Vibe**
Adventure, capability, no-nonsense ownership. Buying a KTM is framed as a decision a confident person makes; the copy never sells *to* you, it sells *with* you. The countdown timer, the "24 תשלומים ללא ריבית" stamp, and the "מבצע למלאי קיים" disclaimer create urgency without pleading.

**Examples of brand copy (verbatim from the codebase)**
- Hero: *"יש כאלה שרוכבים בכביש ויש כאלה שרוכבים על ADV 390 R"*
- Offer eyebrow: *"ההצעה"* / *"שלא מחכה"*
- CTA primary: *"השאר פרטים"* / *"אני רוצה לרכוש"*
- CTA secondary: *"צפה בסרטון"* / *"לרכיבת מבחן חינם"*
- Success: *"תודה! קיבלנו את פרטיך ונחזור אליך בהקדם לתאום רכיבת מבחן על ה-KTM ADV 390 R."*
- Disclaimer: *"ההצעה כפופה לתנאי חברת האשראי. 24 תשלומים שווים בכרטיס אשראי, ריבית 0%. המחיר הסופי ומפרט הרכב עשויים להשתנות."*

---

## Visual Foundations

### Colors
Three hard primaries, full stop: **orange `#ff6600`**, **black `#0a0a0a`**, **off-white `#e8e8e8`**. Pure white `#ffffff` is reserved for high-contrast text on dark imagery. WhatsApp green `#25D366` shows up exactly once (the success-state CTA) and is borrowed from WhatsApp's brand, not part of the KTM palette.

Neutrals are a tight gray scale: `#0a0a0a → #1a1a1a → #1e1e1e → #2a2a2a → #333 → #444 → #555`. Use them by *step*, not by hand-tuned shade — the codebase already has them indexed.

### Type
**Heebo, single family, all weights.** Display work runs at **900 (Black)**, body at 400. The brand voice IS the weight contrast — there's no serif, no monospace, no display alternate. Headlines are tightly tracked (`-0.02em` to `-0.04em`); labels & eyebrows use very wide tracking (`0.2em` – `0.3em`) and uppercase or its Hebrew equivalent (no case + wide track).

### Backgrounds
- **Full-bleed photography** is the hero treatment. The bike sits in a real environment (mountains, dust, gray sky) and is overlaid with a **left-to-right black gradient** (`from-black/30 via-black/55 to-black/80`) to push the photo back and make the right-side text panel readable. The gradient lifts toward content, not toward the bike.
- **Pure `#0a0a0a` flat** is the section background everywhere else.
- **Orange radial glows** — soft blurred orange circles (`bg-[#ff6600]/20 blur-[120px]`) — are used sparingly to charge an otherwise-flat black section with energy. Top-center for hero, bottom-right for accent.
- **No gradients other than the photo overlay and the success-modal backdrop.** No mesh, no rainbow, no purple/blue.

### Typography in use
Hero number: 900, ~96px, tabular-nums, orange. Section eyebrow: 700, 14px, `tracking-widest`, orange. Section title: 900, 48px, white. Feature subtitle: 700, 14px, orange. Body: 400, 16px, `text-60` (60% opacity of off-white). Disclaimer: 400, 12px, `text-40`.

### Spacing & layout
- **Container max widths**: `max-w-5xl` (cards grid), `max-w-4xl` (hero), `max-w-3xl` (offer block). Centered, with generous side padding (`px-6` on mobile, more on desktop).
- **Section vertical rhythm**: `py-20` (80px) for marketing sections is the default. Hero is full viewport (`h-dvh`).
- **Grid gaps are 1px** in the feature grid — cards sit on a `bg-[#2a2a2a]` parent so the 1px gap reads as a hairline rule, not whitespace.

### Backgrounds — imagery vibe
**Warm-but-overcast.** The hero photography is shot in moody natural light: gray sky, dry-grass foreground, the bike's orange popping as the only saturated color in frame. Never studio-clean, never sunset-warm. The bike feels *used* — about to be ridden, not on display.

### Animation
- **Easing**: default browser easing on color transitions (`transition-colors duration-200`). No custom cubic-béziers.
- **Bounces & shakes**: exactly one — the `animate-bounce` down-arrow at the bottom of the hero. Telegraphs "scroll".
- **Fades**: success-modal backdrop fades in via `backdrop-blur-sm` + `bg-black/75`. The modal itself just snaps in.
- **No scroll-driven animation, no parallax, no GSAP.** The page is static. The video carries the motion.

### Hover & press states
- **Primary CTA (orange)**: `bg-[#ff6600]` → `hover:bg-[#cc5200]`. Darker orange, not lighter. No scale, no shadow change.
- **Outline CTA (white border)**: `border-white` → `hover:border-[#ff6600] hover:text-[#ff6600]`. Adopts the orange.
- **Cards**: `bg-[#1a1a1a]` → `hover:bg-[#222222]`. Just one shade up.
- **Disabled**: `disabled:opacity-40 disabled:cursor-not-allowed`. Strong opacity drop — KTM doesn't soft-disable.
- **No press / active styles** beyond browser defaults.

### Borders
- Outline buttons: **2px**, full color.
- Form fields: **1px**, three states — neutral `#333`, error `red-500`, valid `green-600`. Border changes color on validate; field stays the same gray.
- Decorative borders: 1px in `--ktm-orange-20` to `--ktm-orange-40` (transparent orange) — used on the offer card and the form strip's top edge.

### Shadows
**Almost none.** KTM's dark UI uses **orange glow** (huge blur radius, low opacity, on `#ff6600`) instead of drop shadows. The one exception is the success modal: `shadow-2xl`. The email template (light theme) uses a subtle `0 4px 24px rgba(0,0,0,0.10)` card shadow.

### Layout rules
- **Sticky / fixed elements**: a **bottom sticky bar** on mobile (`StickyBar.tsx`) holds the price + "השאר פרטים" CTA. Desktop has no fixed chrome.
- **RTL**: the entire `<html>` is `dir="rtl"`. `me-2` / `ms-2` (Tailwind logical props) are used so layouts flip cleanly. Number-heavy spans use `direction: ltr` islands inside an RTL parent so 1,958 ₪ reads correctly.

### Transparency & blur
Used only twice. Success-modal backdrop (`bg-black/75 backdrop-blur-sm`) and the desktop hero's gradient overlay. Never on cards, never on buttons.

### Corner radii — sharp vs round, by intent
KTM's radii are **schizophrenic on purpose**, and that's the design.
- **Hard 0px corners** = "industrial, motorcycle-spec" — primary marketing CTAs, the dividing accent bar, feature-grid cells.
- **`rounded-xl` (12px)** = "modern, app-like" — form fields, primary submit button, mobile sticky CTA.
- **`rounded-2xl` (16-24px)** = "soft surface" — mobile offer card, success modal, video frame.
The contrast — hard CTA above a soft offer card — is the brand's visual signature. Don't smooth this out.

### Cards
Two card patterns:
1. **Dark-mode card**: `bg-[#1a1a1a]` + 1px `bg-[#2a2a2a]` grid separator OR thin orange border (`border-[#ff6600]/30`). Sharp corners.
2. **Email "lead-info" card** (light theme only): `bg-[#f8f8f8]` + `border-radius: 10px` + **4px solid `#ff6600` right-border accent** (RTL: the accent sits on the right edge, which is the "leading edge" in RTL). This is the one place the colored-accent-edge pattern is used; don't generalize it to dark UI.

### Iconography vibe
See **Iconography** below — but the short version: thin-stroke (1.5px) line icons in orange, no fills, no rounded caps that get cartoony.

---

## Iconography

KTM Israel's codebase does **not** ship an icon font or sprite. Icons are **inline SVGs**, hand-written per use, all following the same recipe:

- `viewBox="0 0 24 24"`, `fill="none"`, `stroke="currentColor"`, `strokeWidth={1.5}` to `{2.5}`.
- Stroke linecaps: `round`. Stroke linejoins: `round`.
- Color: `text-[#ff6600]` for feature/accent icons, `text-white` (full opacity) for UI controls (close X, chevron), `text-black` for icons sitting on an orange background.
- Sizes: `w-5 h-5` (20px) for inline UI, `w-6 h-6` (24px) for headers/CTAs, `w-10 h-10` (40px) for feature-card hero icons.

**The icons used in the codebase** (all hand-authored Heroicons-style SVG):

| Icon | Used for | Stroke |
|---|---|---|
| Lightning bolt | Feature: "מנוע 399cc" | 1.5 |
| Shield with check | Feature: "ABS + TCS" | 1.5 |
| Suspension/equalizer bars | Feature: "WP APEX Suspension" | 1.5 |
| Monitor (TFT screen) | Feature: "מסך TFT חכם" | 1.5 |
| Down chevron | Hero scroll indicator | 2 - 2.5 |
| Close X | Modal dismiss | 2.5 |
| Check ✓ | Success state | 3 |
| WhatsApp logo (filled, brand) | Success CTA | filled |

> **Substitution flag for the next agent**: When you need icons beyond the four feature glyphs above and you're not in the codebase, default to **Heroicons (outline, 24×24, 1.5 stroke)** — it's what the existing icons match. CDN: `https://unpkg.com/heroicons@2/24/outline/*.svg`. If you need fills, switch to **Heroicons solid** rather than mixing libraries. Don't reach for Lucide or Phosphor here — Heroicons' geometry is what the codebase already uses.

**Brand marks vs icons**:
- The **KTM "Ready to Race" wordmark** (`assets/ktm-logo.png`) lives ONLY inside an orange rectangle (`bg-[#ff6600]`) with `rounded-xl` corners and `px-5 py-2` padding. Never on white, never alone, never recolored.
- The **square Instagram/avatar lockup** (`assets/ktm-orange-square.png`) is for social/app-tile contexts.
- "ADV 390 R" is a typed wordmark, not a graphic. Set it in Heebo Black, 900 weight, white.

**Unicode characters used as icons**:
- `✓` (U+2713) — used in offer-section feature list, colored `#ff6600`.
- `·` (U+00B7) — used as a middle-dot separator between offer benefits.

**No emoji in the public-facing landing page.** Emoji appear only inside `email-template.html` as inline-image-fallback scan-aids for internal recipients.

---

## Substitutions to confirm

- **Font**: The codebase loads Heebo via `next/font/google`. The design-system CSS loads it from Google Fonts CDN. If KTM Israel has a licensed corporate font (e.g. KTM Light/Bold from KTM AG's global brand book), please send it — current files assume Heebo for both Hebrew and Latin.
- **Hero photo**: only one photo exists in the codebase. For broader UI work (model gallery, dealer pages) we'd need more imagery. The current photo is good — moody, environmental, off-road.
- **Icons**: feature icons beyond the four motorcycle-specific ones (engine, ABS, suspension, TFT) will fall back to **Heroicons outline** — flagged.
