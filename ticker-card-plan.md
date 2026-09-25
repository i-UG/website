# Plan: Rotating Ticker Card — Issue #29

## Overview

Add a rotating "ticker card" announcement widget to `index.html`. The card displays one message at a time, fading between messages every 4 seconds. Each message can carry an emoji/SVG icon, plain text, and an optional URL. The component is dependency-free (plain HTML/CSS/JS) and lives entirely within `index.html`.

**Placement:** Between the hero section (`<!-- END HERO SECTION -->`, line 307) and the photo-strip `<section>` (line 309). This puts the ticker immediately below the hero fold where it will catch every visitor's eye without disrupting the hero layout. This is the starting position — can be moved later if needed.

**Constraints:**
- No new CSS classes may be added to `assets/css/tailwind.css` (pre-compiled artefact, no build tooling).
- All styling must use classes already compiled into `tailwind.css` (see AGENTS.md) plus any necessary inline `style=""` attributes for values not available as utilities (e.g. `opacity` transitions).
- All JavaScript must go in the single existing `<script>` block at the bottom of the file.

---

## Sub-Tasks

---

### Sub-Task 1 — Add ticker HTML markup

**Intent:** Insert the static HTML shell for the ticker card between the hero section and the photo strip. The card's content slot will be populated and swapped by JavaScript; here we only define the structural container and first visible state.

**Expected Outcomes:**
- A slim, visually cohesive card appears below the hero before any JavaScript runs.
- The card has a container element the JS can target by `id`.
- The icon slot and text/link slot are identifiable via `id` attributes.
- Accessibility: `aria-live="polite"` is set so screen readers announce each new message.

**Todo List:**
1. After `<!-- END HERO SECTION -->` (line 307), insert a new `<section>` element containing:
   - Outer wrapper: `bg-ibm-gray border-b border-gray-200 py-3`
   - Inner centred row: `mx-auto flex max-w-6xl items-center gap-3 px-6 lg:px-8`
   - Icon span: `id="ticker-icon"` — `text-xl` for emoji sizing
   - Text/link slot: `id="ticker-text"` — `text-sm font-medium text-ibm-carbon` wrapping either a plain `<span>` or an `<a>` depending on whether a URL is present (the JS will swap this)
   - A label badge on the left: small `bg-ibm-blue text-white text-xs font-semibold px-2 py-0.5 rounded` reading "Latest"
2. Set `aria-live="polite"` and `aria-atomic="true"` on the text slot so assistive tech announces the swap.
3. Wrap the icon + text row in a `<div id="ticker-card">` which the JS will control opacity on during transitions. Apply `transition-opacity duration-500` via a `style` attribute since `transition-opacity` is already present in the compiled CSS.

**Relevant Context:**
- Insertion point: [`index.html`](index.html:307) — after `<!-- END HERO SECTION -->`
- Existing card styling reference: gallery cards at line ~784 use `border border-gray-200 bg-white shadow-sm`
- IBM blue badge pattern: hero eyebrow label at line ~275 uses `text-ibm-blue` with tracking — replicate the brand feel
- `bg-ibm-gray` is a custom compiled class (confirmed in AGENTS.md)

**Status:** [ ] pending

---

### Sub-Task 2 — Add ticker JavaScript logic

**Intent:** Add a self-contained ticker function inside the existing `<script>` block that populates the messages array, sets initial content, and starts the rotation interval.

**Expected Outcomes:**
- The ticker card shows the first message immediately on page load.
- Every 4 seconds the card fades out (`opacity: 0`), the content swaps, then fades back in (`opacity: 1`).
- If a message has a `url`, the text renders as an `<a href="...">` with appropriate hover styling; if not, it renders as a plain `<span>`.
- If a message has an `icon`, it appears in the icon slot; if not, the icon slot is empty/hidden.
- Messages loop (index wraps with `% messages.length`).
- No dependencies on any external library.

**Todo List:**
1. At the end of the existing `<script>` block (before the closing `</script>` tag), add a `messages` array following the data structure from the issue:
   ```
   { text, url (optional), icon (optional) }
   ```
   Seed it with 3 placeholder messages matching the issue examples (Registration open, Call for speakers, New workshop). Add a prominent `/* ===== TICKER MESSAGES — edit here ===== */` comment block immediately above the array so content editors can locate and update the messages easily in the future without reading the rest of the JS.
2. Write a `renderTicker(index)` helper that:
   - Reads `messages[index]`
   - Sets `ticker-icon` `textContent` to `icon` (or clears it)
   - Builds either an `<a>` or `<span>` for the text, sets it as the content of `ticker-text`
   - Applies `cursor-pointer` class and `target="_blank" rel="noopener noreferrer"` on the `<a>` if URL present (opens in a new tab)
3. Call `renderTicker(0)` immediately to show the first message without waiting for the first interval.
4. Set up `setInterval` (4000 ms) that:
   a. Fades the `ticker-card` div to `opacity: 0` (set `style.opacity = '0'`)
   b. After 500 ms (`setTimeout`) swaps content via `renderTicker(nextIndex)`
   c. Fades back to `opacity: 1`
5. Guard the whole block with a check that `document.getElementById('ticker-card')` exists, so the script doesn't throw if the HTML is ever removed.

**Relevant Context:**
- Existing `<script>` block: [`index.html`](index.html:1798) — append inside this block before `</script>`
- Pattern to follow: the sticky-header scroll handler already uses `style.*` manipulation for opacity (`opacity-0` / `opacity-100` toggled on hamburger lines ~1853–1864)
- `transition-opacity duration-500` will make the CSS engine interpolate the opacity change smoothly — no need for JS animation libraries
- The `transition` property on `#ticker-card` must be set in the HTML (`style="transition: opacity 0.5s"`) so the CSS transition fires when JS changes `style.opacity`

**Status:** [ ] pending

---

### Sub-Task 3 — Verify styling uses only compiled classes

**Intent:** Do a final audit to confirm every Tailwind class added in Sub-Task 1 is present in `assets/css/tailwind.css`. Any class not present in the compiled file must be replaced with an inline `style=""` equivalent.

**Expected Outcomes:**
- No new utility classes appear in `index.html` that are absent from `assets/css/tailwind.css`.
- The ticker renders correctly without missing styles (no invisible or mis-styled elements).

**Todo List:**
1. Grep `assets/css/tailwind.css` for each class applied in the ticker HTML:
   - `bg-ibm-gray` — confirmed in AGENTS.md ✓
   - `text-ibm-blue`, `bg-ibm-blue`, `text-ibm-carbon` — confirmed in AGENTS.md ✓
   - `transition-opacity`, `duration-500` — confirmed present (used on hamburger line ~194 and gallery ~792)
   - `border-b`, `border-gray-200`, `py-3`, `px-6`, `gap-3`, `text-sm`, `font-medium`, `text-xl`, `text-xs`, `rounded`, `font-semibold` — standard Tailwind utilities, verify presence
2. For any class not found in the compiled file, substitute with an equivalent inline style.
3. Confirm the "News" badge colour — `bg-ibm-blue text-white` — renders (both confirmed in AGENTS.md).

**Relevant Context:**
- [`assets/css/tailwind.css`](assets/css/tailwind.css) — grep target
- AGENTS.md custom class table — reference for confirmed custom classes

**Status:** [ ] pending

---

## Implementation Notes

- The ticker section sits outside of any named section `id`, consistent with the photo-strip and media-partner sections which also have no `id`.
- The messages array is intentionally hardcoded for now. A future enhancement could externalise it to a JSON file, but that is out of scope for this issue.
- Desktop and mobile nav do **not** need changes — the ticker is a page-body element, not a navigation element.
