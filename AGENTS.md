# AGENTS.md

This file provides guidance to agents when working with code in this repository.

## Hard Constraints ⚠️

1. **Single-page only** — All content lives in `index.html`. No additional pages allowed.
2. **Tailwind CSS only** — No Bootstrap, custom stylesheets, or alternative CSS frameworks.
3. **No server-side code** — Static site only.
4. `main` is branch-protected — PRs required; only [@AndyYouens](https://github.com/AndyYouens) can merge.

## No Build Step

There is no `package.json`, no npm scripts, no build command. `assets/css/tailwind.css` is a **pre-compiled, committed artefact** — do not regenerate or delete it. There is no Tailwind config file.

Local preview: `npx serve .`

## Custom Tailwind Classes (defined in compiled CSS — not standard Tailwind)

| Class | Value |
|---|---|
| `text-ibm-blue` / `bg-ibm-blue` | `#0f62fe` |
| `hover:bg-ibm-blue-dark` | `#0043ce` |
| `text-ibm-carbon` / `bg-ibm-carbon` | `#393939` |
| `text-ibm-carbon-light` | `#525252` |
| `bg-ibm-gray` | `#f4f4f4` |
| `ibm-grid` | decorative grid background (hero) |
| `ibm-diagonal` | decorative diagonal overlay (hero) |
| `animate-fade-in` | `fade-in 0.6s ease-out forwards` |
| `animate-fade-up` | `fade-up 0.6s ease-out forwards` |

These are baked into `assets/css/tailwind.css`. Any new class you add to `index.html` that isn't already in the compiled file **will not render** — use only classes already present in the stylesheet.

## Navigation: Desktop + Mobile Must Stay in Sync

The desktop `<nav>` (line ~135) and `<div id="mobile-menu">` (line ~177) are **separate, independent copies** of the nav links. Adding/removing a link in one requires mirroring the change in the other.

Mobile nav links need `class="mobile-link"` — JavaScript uses this selector to close the menu on tap.

## Contact Form — Web3Forms

The form (`id="contact-form"`) POSTs to **Web3Forms** (`https://api.web3forms.com/submit`), which forwards submissions to an email address. The `access_key` field in the `fetch` body (in the `<script>` block) is a **routing key, not a secret** — it is safe to commit. Replace `YOUR_ACCESS_KEY_HERE` with the key obtained at [web3forms.com](https://web3forms.com).

## Image Naming Convention

- Photo strip (sections 1–9): `assets/images/photo1.jpeg` … `photo9.jpeg`
- Gallery section (further down page): `photo10.jpeg` – `photo12.jpeg`

Keep images under ~300 KB. JPEG format recommended.

## Page Sections Reference

| Section | id / location |
|---|---|
| Header/nav | `id="site-header"` |
| Hero | first `<section>` (no id) |
| Photo strip | second `<section>` (no id) |
| About | `id="about"` |
| Conference | `id="conference"` |
| Gallery | `id="gallery"` |
| Contact | `id="contact"` |
| Footer | `<footer>` |

## Decision Framework

| Situation | Action |
|---|---|
| Fix typo, update date/event info | ✅ Do it |
| Image updates, wording improvements | ✅ Do it |
| Fix broken styles (CSS) | ✅ Do it |
| New section, redesign, layout change | ⚠️ Draft PR / open issue first |
| Change CSS framework, add pages, server code | 🛑 Escalate to Development Director |
