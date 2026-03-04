# ICDC Website Review — Changes Made (Round 2)

Below is a complete list of changes made in response to each item in the second round of Notre Dame DIY website review feedback.

---

## 1. Buttons: Matching NDT4 Button Styles

**Feedback:** Button styles still not matching NDT4. Border weight should not exceed 1px; gold text and gold borders are not allowed for buttons in dark mode.

**Resolution:** All button variants have been reworked to match the NDT4 reference styles from `webtheme.nd.edu`:

- **`.btn-outline` border reduced from 2px to 1px.** The border now uses `light-dark(rgba(0,0,0,.12), rgba(193,205,221,0.25))` — a subtle translucent border matching NDT4's default `--border-primary` token, with no gold in either mode.

- **Gold completely removed from all buttons in dark mode.** The `.btn-outline` now uses `color: light-dark(#0c2340, #ffffff)` — navy text in light mode, white text in dark mode. No gold text or gold borders appear on any button in dark mode.

- **`.btn-primary` updated to match NDT4 CTA pattern.** In dark mode the primary button now uses a white background with navy text (`light-dark(#0c2340, #ffffff)` / `light-dark(#ffffff, #0c2340)`), matching NDT4's `.btn--cta` dark-mode inversion pattern. This also fixes a previous contrast issue where the navy-on-navy button was barely visible in dark mode.

- **Hover behavior updated to match NDT4.** All buttons now use `transform: scale(1.06)` on hover instead of the previous `translateY(-2px)`, consistent with NDT4's `.btn:hover` behavior.

- **Link pills (Try Sway / ThinkerAnalytix) also updated.** These button-like elements now follow the same NDT4 pattern: transparent background, subtle translucent border, navy/white text by mode, with no gold in dark mode.

---

## 2. Cards: Border Removal Where Backgrounds Differ

**Feedback:** Borders should only be used on cards if background is transparent and visible separation is required. White background cards over warm-white sections should have borders removed.

**Resolution:** Card borders are now conditionally applied based on whether the card background matches the section background:

- **Cards in `.icdc-section-alt` sections** (The Challenge, Technology, The Study, Get Involved) — which have a warm-white background (#f8f4ec) in light mode — now have `border-color: light-dark(transparent, var(--icdc-border))`. This removes borders in light mode (where the white card on warm-white section is already visually distinct) while preserving borders in dark mode (where card and section backgrounds match at #0f1d30).

- **Stat cards** have `border: none` in all modes, since their background (`--icdc-stat-bg: #edf2f9` / `#0c1a2e`) is always visually distinct from both the base and alternate section backgrounds.

- **Cards on white-background sections** (Our Approach, Partners) retain their borders, since the white card background matches the white section background and a border is needed for visible separation.

---

## 3. Inline Navigation

**Feedback:** Consider making the navigation inline when space allows by adding `header-group--inline-xl` to the header group class.

**Resolution:** Added the `header-group--inline-lg` class to the `<div class="header-group">` element. The `--inline-lg` variant (activating at `min-width: 80em` / 1280px) was chosen over `--inline-xl` (1440px) because the XL breakpoint did not activate on common laptop displays such as a 16" MacBook Pro. At LG breakpoints and above, the NDT4 framework renders the site title/mark and navigation on the same horizontal line using a 3-column CSS grid, with the nav right-aligned via `margin-left: auto`. On narrower screens, the layout gracefully falls back to stacked (title above nav).

---

## 4. Sticky Navigation (Not Whole Header)

**Feedback:** The whole site header should not be sticky when scrolling. Only the navigation should be sticky. Refer to careers.nd.edu, fightingfor.nd.edu for examples.

**Resolution:** The previous implementation made the entire `.site-header` sticky, which consumed excessive vertical space. This has been replaced with a JavaScript-based approach that matches the NDT4 reference site behavior (careers.nd.edu, fightingfor.nd.edu):

- **Removed `position: sticky`** from `.site-header` entirely.

- **Added an IntersectionObserver** that watches the `.header-title` element. When the user scrolls past the header title/mark area, the `.header-nav` element receives `nav-fixed` and `active` classes.

- **Fixed nav styling matches NDT4's `.header-nav-fixed` pattern exactly:**
  - Navy background (`#0c2340` / `var(--brand-blue)`)
  - Gold accent line at top (`border-top: 3px solid #ae9142` / `var(--brand-gold)`)
  - Soft depth shadow (`box-shadow: 0 0 4rem rgba(0,0,0,0.3)`) — no bottom border
  - Full viewport width with `padding: 1rem 5vw`
  - `z-index: 999`
  - White nav link text, with gold underline on the active link
  - Nav links right-aligned via `justify-content: flex-end`

- **Slide-down entrance animation** via `opacity` and `translateY(-100%)` transition (0.3s ease), triggered by adding the `.active` class on the next animation frame after `.nav-fixed` is applied. This matches NDT4's `.header-nav-fixed.active` reveal pattern.

- **A `paddingBottom` spacer** is dynamically added to the header group to prevent a layout jump when the nav leaves the normal document flow.

- **Desktop only (min-width: 60em / 960px):** All fixed nav styles are wrapped in a media query matching NDT4's desktop nav breakpoint. On mobile, the fixed nav is not activated since the nav links are hidden by the NDT4 theme's responsive layout (no empty bar appears).

- **On scroll-back**, the observer removes both classes and the padding, instantly restoring the nav to its normal position within the header.

The result matches the NDT4 reference sites: the full header (mark + title + nav) is visible at the top of the page; as the user scrolls, the mark/title scrolls away and a compact navy navigation bar with a gold top accent slides down from the top of the viewport.

---

## 5. Dark Mode Body Text Color

**Feedback:** In dark mode, the body text is still not rendering as white text. `var(--icdc-text-secondary)` should be `#ffffff` in dark mode.

**Resolution:** Changed `--icdc-text-secondary` from `light-dark(#3a4d63, #b8c4d4)` to `light-dark(#3a4d63, #ffffff)`. All body text, section descriptions, card paragraphs, taglines, and other secondary-text elements now render as pure white (#ffffff) in dark mode.

---

## 6. Timeline: Diamond Markers Overlapping the Bar

**Feedback:** Diamond markers are still not overlapping the left rule. Reference: webtheme.nd.edu timeline component docs.

**Resolution:** The entire timeline component has been restyled to match the NDT4 reference implementation exactly:

- **Timeline bar:** Changed from 2px wide at `left: 11px` to **1px wide at `left: 1px`**, with colors matching NDT4's tokens: `light-dark(#e9ebee, #1e3a5f)`.

- **Timeline items:** Now use `margin-inline-start: 1.7rem` (matching NDT4's offset from the bar), replacing the previous `padding-left: 24px` on the container.

- **Diamond markers:** Resized from 12px to **0.75rem** and repositioned to `left: -2rem` from the item edge. This centers the diamond directly over the 1px vertical bar line, matching NDT4's overlap geometry. The diamond color is now the NDT4 brand gold `#ae9142` (previously it used `var(--icdc-primary)` which resolved differently by mode).

- **Dark mode extra stroke fixed:** Timeline card borders (`.timeline-content`) are now set to `border-color: transparent` in both modes, eliminating the double-stroke appearance that was previously visible in dark mode.

- **Timeline marker badges (Y1–Y4) contrast fixed:** The badge background is now `light-dark(var(--icdc-primary), #0c2340)` — navy in dark mode instead of gold, giving white-on-navy contrast of ~16:1 (previously white-on-gold was ~2.4:1, failing WCAG AA).

---

## 7. Hero: Vertical Negative Space

**Feedback:** Consider giving the hero more vertical negative space on desktop. It currently feels tight for NDT4 and the down arrow gets close to text.

**Resolution:** Multiple spacing improvements have been made:

- **Base padding increased** from `3rem 0 5rem` to `5rem 0 8rem`.

- **Viewport-filling min-height added:** The hero now uses `min-height: calc(100dvh - var(--header-h, 120px))`, where `--header-h` is measured via JavaScript at page load. This ensures the hero section fills the full visible viewport below the header on all display sizes, with the scroll-down chevron sitting comfortably at the bottom of the viewport and the next section starting just out of view.

- **Scroll chevron offset increased** from `bottom: 2.5rem` to `bottom: 3rem`.

- **CTA button row** now has `margin-bottom: 2rem` to create additional separation between the buttons and the scroll chevron.

- **Mobile padding preserved:** The `@media (max-width: 768px)` override continues to use `padding: 40px 0 60px` for appropriate mobile spacing.

---

## 8. Muted Color Contrast (WCAG AA)

**Feedback:** `var(--icdc-muted)` does not meet WCAG AA contrast requirements in dark mode.

**Resolution:** Changed `--icdc-muted` from `light-dark(#5a6a7e, #7a8a9e)` to `light-dark(#5a6a7e, #94a3b8)`.

- **Previous dark-mode value:** #7a8a9e on #091b34 = ~4.1:1 contrast ratio (fails WCAG AA's 4.5:1 minimum for normal text).
- **New dark-mode value:** #94a3b8 on #091b34 = **~6.6:1 contrast ratio** (exceeds WCAG AA for both normal and large text).

This affects the scroll chevron color, contact line text, and partner card personnel names — all of which are now accessible in dark mode.

---

## Items Confirmed Still Passing from Round 1

The following items from the original review were addressed in Round 1 and remain correctly implemented:

| Item | Status |
|---|---|
| Global Menu/Search button removed | Confirmed — no search button in header |
| Card box-shadows removed | Confirmed — no `box-shadow` on any card |
| Card border-radius 4px | Confirmed — all cards use `border-radius: 4px` |
| Card title font-family GP/Helvetica | Confirmed — all card headings use GP sans-serif |
| Card title bottom rules | Confirmed — `border-bottom: 1px solid` on card headings with body text |
| No card hover effects on non-link cards | Confirmed — comment at end of stylesheet, no `:hover` on cards |
| Section labels: weight 300, body text color, no gold | Confirmed — `font-weight: 300; color: var(--icdc-text)` |
| All rounded corners 4px (except buttons) | Confirmed |
| Background color consistency (white base + warm-white highlight only) | Confirmed — no sky-blue section backgrounds |
| Correct heading order (h1 → h2 → h3 → h4) | Confirmed |
| Accessibility: `aria-labelledby` on all sections | Confirmed |
| Title tag includes " \| University of Notre Dame" | Confirmed |
| Hero dark mode: no gold text on non-link/non-stat elements | Confirmed |
| Technology: no gradient on thinkARGUMENTS + Sway card | Confirmed |
| Collaboration: partner categories as `<h3>` | Confirmed |
| Y1–Y4 markers inside timeline cards | Confirmed |
| Study Groups / Project Timeline heading styles | Confirmed |
