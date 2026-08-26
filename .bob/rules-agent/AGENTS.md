# Project Coding Rules (Non-Obvious Only)

- **No build step** — `assets/css/tailwind.css` is pre-compiled and committed. Never run a Tailwind build or regenerate it; there is no config file to run it with anyway.
- **Tailwind class scope** — Only classes already present in `assets/css/tailwind.css` will render. If you add a new Tailwind utility not seen elsewhere in `index.html`, it will silently have no effect. Verify with `grep` against the CSS file before using unfamiliar utilities.
- **Custom color tokens** — `text-ibm-blue`, `bg-ibm-blue`, `hover:bg-ibm-blue-dark`, `text-ibm-carbon`, `text-ibm-carbon-light`, `bg-ibm-gray`, `bg-ibm-carbon` are custom extensions. These are NOT standard Tailwind colors.
- **Dual-nav rule** — Desktop `<nav>` (~line 135) and mobile `<div id="mobile-menu">` (~line 177) are separate HTML blocks. Any nav link change must be applied to both. Mobile links also require `class="mobile-link"` for the JS close-on-tap behavior.
- **Contact form is fake** — `id="contact-form"` has no real backend; the submit handler uses `setTimeout` to simulate success. Do not add a real `action` attribute to the form without replacing the JS handler too.
- **Photo numbering split** — `photo1.jpeg`–`photo9.jpeg` belong to the photo strip; `photo10.jpeg`–`photo12.jpeg` belong to the gallery section. Do not mix them up when adding images.
- **Inline JS only** — All JavaScript lives in a single `<script>` block at the bottom of `index.html`. No external JS files.
- **PR required** — Never push directly to `main`. All changes go through a PR reviewed by [@AndyYouens](https://github.com/AndyYouens).
