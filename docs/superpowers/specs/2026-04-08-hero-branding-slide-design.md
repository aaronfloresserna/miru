# Hero Branding Slide — Design Spec
**Date:** 2026-04-08
**Status:** Approved

---

## Overview

Replace the existing hero headline ("Your company's intelligence, automated.") with the Miru brand tagline "See your AI future clearly." Add a kanji identity line above the h1 and a supporting subtitle below it. No new section is added — all changes are contained within the existing `#hero` section.

---

## Goals

- Establish the Miru brand positioning ("See your AI future clearly") as the first thing visitors read.
- Surface the Miru etymology (見る = "to see") as a visual brand marker.
- Add a one-sentence description of what Miru does, drawn directly from the brand copy.

---

## What Changes

### HTML — `#hero` section

**Remove** the existing h1 element:
```html
<h1 class="reveal from-bottom d2" data-i18n="hero.h1">Your company's<br>intelligence,<br><span class="grad-text">automated.</span></h1>
```

**Replace with** these three elements in order:
```html
<p class="hero-kanji reveal from-bottom">見る · Miru · "To see"</p>
<h1 class="reveal from-bottom" data-i18n="hero.h1">See your AI future <span class="grad-text">clearly.</span></h1>
<p class="hero-sub reveal from-bottom" data-i18n="hero.sub">We help companies understand where AI, data, and automation should go and how to implement them successfully.</p>
```

Note: `d1`–`d5` delay classes are **not** used on hero elements. The hero stagger is driven by DOM order — the JS at `#hero` startup does:
```js
document.querySelectorAll('#hero .reveal').forEach((el, i) => {
  setTimeout(() => el.classList.add('in'), 100 + i * 200);
});
```
Adding kanji and subtitle as `.reveal` elements automatically extends the stagger sequence. No JS changes are needed.

The `data-i18n` attribute fallback text inside the h1 element is overwritten at runtime by `applyLang()` — it exists only as a non-JS fallback. The authoritative copy lives in the `T` object (see below).

**Buttons:** no class change needed. DOM order places them after the new elements, so the stagger index shifts naturally.

---

### New CSS

Add near the `.hero-sub` rule in the existing style block:

```css
.hero-kanji {
  font-size: 11px;
  font-weight: 700;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: var(--accent);
  margin-bottom: 10px;
}
```

`.hero-sub` is already defined — no new rule needed.

**Mobile:** `.hero-kanji` is already small (11px) and contains only brand language. No mobile override is needed — the existing font size works at all breakpoints. Confirm visually after implementation.

**Note on `.hero-kanji` language:** This element is intentionally hardcoded with no `data-i18n` attribute. The kanji line is brand identity and is the same in both EN and ES. Do not add an i18n key for it.

---

### i18n Updates — `T` object in `index.html`

**`hero.h1`** — replace the existing value in both `T.en` and `T.es`. Do not add a duplicate key; replace the existing one.

```js
// T.en
'hero.h1': 'See your AI future <span class="grad-text">clearly.</span>',

// T.es
'hero.h1': 'Ve con claridad tu futuro<br>con <span class="grad-text">IA.</span>',
```

**`hero.sub`** — this is a **new key** that does not exist yet. Add it in both `T.en` and `T.es`:

```js
// T.en
'hero.sub': 'We help companies understand where AI, data, and automation should go and how to implement them successfully.',

// T.es
'hero.sub': 'Ayudamos a las empresas a entender adónde debe ir la IA, los datos y la automatización y cómo implementarlos.',
```

---

## Element Order in DOM (final)

| # | Element | Class | Note |
|---|---|---|---|
| 1 | Badge | `reveal from-bottom` | No change |
| 2 | Kanji line | `reveal from-bottom` | New element, no i18n |
| 3 | H1 | `reveal from-bottom` | Updated copy |
| 4 | Subtitle | `reveal from-bottom` | New element, new i18n key |
| 5 | Buttons | `reveal from-bottom` | No change, index shifts naturally |

---

## Out of Scope

- No changes to the canvas animation.
- No changes to any other section.
- No new sections added.

---

## Files Affected

| File | Change |
|---|---|
| `index.html` (HTML) | Remove old h1, add kanji `<p>`, new h1, subtitle `<p>` |
| `index.html` (CSS) | Add `.hero-kanji` rule |
| `index.html` (JS/i18n) | Replace `hero.h1` in T.en and T.es; add new `hero.sub` key in both |
