# Hero Branding Slide Implementation Plan

> **For agentic workers:** REQUIRED: Use superpowers:subagent-driven-development (if subagents available) or superpowers:executing-plans to implement this plan. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Replace the hero h1 with "See your AI future clearly", add a 見る kanji identity line above it, and a supporting subtitle below — all within the existing `#hero` section of `index.html`.

**Architecture:** Three isolated edits to the same file (`index.html`): (1) add a CSS rule, (2) swap HTML elements in the hero, (3) update i18n string values. No new files. No JS changes.

**Tech Stack:** Vanilla HTML/CSS/JS, inline i18n via `T = { en, es }` object, `applyLang()` function.

**Spec:** `docs/superpowers/specs/2026-04-08-hero-branding-slide-design.md`

---

## Chunk 1: All Three Edits

### Task 1: Add `.hero-kanji` CSS rule

**Files:**
- Modify: `index.html` — CSS block, near line 211 (after `.hero-sub` rule)

- [ ] **Step 1: Add the CSS rule**

In `index.html`, locate the `.hero-sub` rule (around line 211):
```css
.hero-sub {
  font-size: 18px; font-weight: 400;
  color: var(--text-light);
  line-height: 1.7; max-width: 600px;
  margin: 0 auto 48px;
}
```

Insert the following block **immediately after** it:
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

---

### Task 2: Replace hero HTML elements

**Files:**
- Modify: `index.html` — `#hero` section, around line 829

- [ ] **Step 2: Swap the hero h1 and add kanji + subtitle**

Locate this block in `index.html` (inside `<div class="hero-inner">`):
```html
<h1 class="reveal from-bottom d2" data-i18n="hero.h1">Your company's<br>intelligence,<br><span class="grad-text">automated.</span></h1>
```

Replace it with these three elements:
```html
<p class="hero-kanji reveal from-bottom">見る · Miru · "To see"</p>
<h1 class="reveal from-bottom" data-i18n="hero.h1">See your AI future <span class="grad-text">clearly.</span></h1>
<p class="hero-sub reveal from-bottom" data-i18n="hero.sub">We help companies understand where AI, data, and automation should go and how to implement them successfully.</p>
```

**Notes:**
- Do not add `d1`–`d5` delay classes — hero stagger is driven by JS DOM index, not these classes.
- The `hero-kanji` element has no `data-i18n` — it is intentionally hardcoded (brand identity, same in both languages).
- The `hero-btns` div that follows remains unchanged.

---

### Task 3: Update i18n — `T` object

**Files:**
- Modify: `index.html` — JS block, `T` object, around lines 1831 and 1872

- [ ] **Step 3: Replace `hero.h1` and add `hero.sub` in T.en**

Locate in `T.en` (around line 1831):
```js
'hero.h1':'Your company\'s<br>intelligence,<br><span class="grad-text">automated.</span>',
```

Replace that line with:
```js
'hero.h1':'See your AI future <span class="grad-text">clearly.</span>',
'hero.sub':'We help companies understand where AI, data, and automation should go and how to implement them successfully.',
```

- [ ] **Step 4: Replace `hero.h1` and add `hero.sub` in T.es**

Locate in `T.es` (around line 1872):
```js
'hero.h1':'La inteligencia<br>de tu empresa,<br><span class="grad-text">automatizada.</span>',
```

Replace that line with:
```js
'hero.h1':'Ve con claridad tu futuro<br>con <span class="grad-text">IA.</span>',
'hero.sub':'Ayudamos a las empresas a entender adónde debe ir la IA, los datos y la automatización y cómo implementarlos.',
```

---

### Task 4: Verify and commit

- [ ] **Step 5: Open the site in a browser and verify**

Open `index.html` directly in a browser (or use a local server). Check:
- [ ] Kanji line `見る · Miru · "To see"` appears above the headline in blue
- [ ] Headline reads "See your AI future clearly." with "clearly." in animated blue gradient
- [ ] Subtitle appears below the headline in muted color
- [ ] All three elements animate in with stagger (badge → kanji → h1 → subtitle → buttons)
- [ ] Toggle language to ES — headline reads "Ve con claridad tu futuro con IA." and subtitle updates in Spanish
- [ ] Mobile: open at narrow viewport, verify kanji and subtitle are readable and don't overflow

- [ ] **Step 6: Commit**

```bash
git add index.html
git commit -m "feat: replace hero headline with 'See your AI future clearly' branding

- Add 見る kanji identity line above h1
- New headline: 'See your AI future clearly'
- New subtitle from brand copy (EN + ES)
- Add .hero-kanji CSS rule

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>"
```
