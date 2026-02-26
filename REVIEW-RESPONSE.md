# ICDC Website Review — Changes Made

Below is a complete list of changes made in response to each item in the Notre Dame DIY website review.

---

## General

### 1. Global Menu/Search button in header does not work

**Resolution:** Removed the global menu/search button and associated dialog entirely. The button triggered an unstyled native `<dialog>` that did not integrate with the NDT4 theme's expected markup, resulting in a broken UI. Since site-level search is not a requirement for this project site, the button has been removed for a clean header.

### 2. Button styles do not match webtheme.nd.edu styling

**Resolution:** All four requested changes have been made:

- Removed all `box-shadow` properties from `.btn-primary` and `.btn-primary:hover`
- Changed `border-radius` from `10px` to `2rem`
- Changed `font-weight` from `600` to `300`
- Fixed dark-mode contrast: the primary button now uses a navy background (`#0c2340`) with white text in dark mode, instead of gold with white text, to meet minimum contrast requirements

### 3. Card styles do not match webtheme.nd.edu styling

**Resolution:** All five requested changes have been made across every card type (feature cards, goal cards, tool cards, partner cards, study cards, timeline cards, stat cards, CTA box):

- Removed all `box-shadow` properties from cards and their hover states
- Changed `border-radius` from `20px`/`16px`/`14px`/`24px` to `4px` on all cards
- Changed card title `font-family` from the serif heading font to `'GP', 'Helvetica Neue', Helvetica, Arial, Verdana, sans-serif`
- Added a `border-bottom` rule below card titles where cards contain summary/long-form text
- All cards now use a `1px solid` border using the theme border color, ensuring visibility in both light and dark modes (where card and section backgrounds can match)

### 4. Section labels do not match webtheme.nd.edu styling

**Resolution:** All three requested changes have been made:

- Changed `font-weight` from `600` to `300`
- Changed `color` from the primary/gold color to the standard page text color (`--icdc-text`)
- Gold text has been reserved exclusively for links and stat numbers throughout the site

### 5. In dark mode, base text color should be white (#fff)

**Resolution:** Changed the dark-mode value of `--icdc-text` from `#f8f4ec` (warm white) to `#ffffff` (pure white).

### 6. Cards should not have a hover style if they are not actionable links

**Resolution:** Removed all hover effects (`:hover` styles including `border-color`, `box-shadow`, `transform`) from every card type: feature cards, goal cards, tool cards, partner cards, study cards, timeline cards, and stat cards.

### 7. All rounded corners (except buttons and input fields) should be 4px

**Resolution:** Changed `border-radius` to `4px` on all non-button elements: feature cards, goal cards, tool cards, partner cards, study cards, timeline content cards, stat cards, study group boxes, CTA box, highlight box, feature icons, and goal number badges. Buttons retain `2rem` as specified in item 2.

### 8. Site is missing sticky navigation when scrolling down the page

**Resolution:** Added `position: sticky; top: 0; z-index: 100` to the `.site-header` element, making the header and navigation bar stick to the top of the viewport when scrolling.

### 9. Background color consistency

**Resolution:** Updated the color scheme to use a consistent base + highlight pattern:

- Base background changed from warm beige (`#f8f4ec`) to white (`#ffffff`) in light mode
- Dark-mode base background set to `#091b34` as specified
- Alternating/highlight sections now consistently use warm white (`#f8f4ec`) — sky blue is no longer used anywhere as a section background

### 10. Correct heading orders for all sections

**Resolution:** Fixed the heading hierarchy throughout:

- Hero heading changed from `<h1>` to `<h2>` (the site-title `<h1>` in the NDT4 header is the single `<h1>` on the page)
- Goal card headings changed from `<h3>` to `<h4>` (they are children of the `<h3>` "Project Goals" heading)
- "Study Groups" heading changed from `<h4>` to `<h3>` (it is a sibling of the `<h3>` "Project Timeline" heading, both under the `<h2>` section title)

### 11. Fix accessibility issues

**Resolution:** Added `aria-labelledby` attributes to all `<section>` elements, pointing to their corresponding `<h2>` section titles (which were given `id` attributes). This allows screen readers to announce the section name when navigating by landmark.

### 12. Add " | University of Notre Dame" to end of `<title>`

**Resolution:** Changed the page title from:
> `ICDC — Integrating Civil Discourse into the Curriculum`

to:
> `ICDC — Integrating Civil Discourse into the Curriculum | University of Notre Dame`

---

## Hero

### 13. In dark mode, gold text should only be reserved for links and stats

**Resolution:** Two changes made in the hero section:

- The `<em>` text ("Civil Discourse") no longer uses gold in dark mode — it now uses the standard text color
- The hero tagline ("A FIPSE-FUNDED NATIONAL INITIATIVE") changed from gold to the standard text color, with `font-weight` also updated from `600` to `300`

Additionally, gold was removed from non-link/non-stat elements site-wide: tool taglines, tool card checkmarks, partner roles, timeline dates, study group headings, and partner category titles.

---

## Technology

### 14. Remove background gradient from thinkARGUMENTS + Sway card

**Resolution:** Removed the `linear-gradient` background and the `2px solid` gold border from the `.tool-combined` card. It now uses the same plain card background and standard border as the other tool cards.

---

## Collaboration

### 15. "Civic Institute Partner", "University Partners", etc. should be headings (h3)

**Resolution:** Changed all three partner category titles from `<div>` elements to `<h3>` elements:

- "Civic Institute Partner" → `<h3>`
- "University Partners" → `<h3>`
- "Nonprofit Partners" → `<h3>`

Their styling was also updated to use a standard heading appearance (normal weight, standard text color) rather than the previous uppercase gold label style.

---

## Research

### 16. Timeline styles do not match webtheme.nd.edu styling

**Resolution:** All three requested changes have been made:

- **Diamond marker overlapping timeline bar:** The square timeline markers have been replaced with diamond-shaped CSS pseudo-elements (`::before` with `transform: rotate(45deg)`) that overlap the vertical timeline bar
- **Y1/Y2/Y3 incorporated into cards:** The year markers (Y1, Y2, Y3, Y4) have been moved from standalone markers beside the timeline bar to inline badge elements inside each timeline card, similar to the study group card style above
- **Dark mode extra stroke fixed:** The timeline card border that created a double-stroke appearance in dark mode has been resolved — cards now use the standard theme border color consistently

### 17. Use proper heading styles for "Study Group" and "Project Timeline"

**Resolution:** Both headings now use the correct `font-family` (`'GP', 'Helvetica Neue', Helvetica, Arial, Verdana, sans-serif`) and appropriate sizing. "Study Groups" was also corrected from `<h4>` to `<h3>` to match the heading hierarchy (see item 10).
