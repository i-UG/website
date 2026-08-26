# Project Documentation Context (Non-Obvious Only)

- The `Website_Update_Guide.pdf` in the project root is the contributor reference doc (not in `public/docs/` as the old AGENTS.md stated — it lives at the root).
- `assets/css/tailwind.css` looks like a standard compiled Tailwind file but contains **custom IBM brand color tokens** (`ibm-blue`, `ibm-carbon`, etc.) and **custom utility classes** (`ibm-grid`, `ibm-diagonal`, `animate-fade-in`, `animate-fade-up`) that are not part of standard Tailwind. There is no `tailwind.config.js` to reference these from — the compiled CSS is the source of truth.
- The contact form appears functional (has validation, submit handler, status messaging) but does **not** call any real endpoint — it is entirely client-side simulation.
- Page sections are found by searching for their `id=` attribute (e.g. `id="conference"`); the hero and photo strip sections have **no `id`**, making them harder to locate — they are the first and second `<section>` elements in `<main>`.
- Navigation links in the HTML appear twice: once for desktop, once for mobile — always check both when answering questions about nav structure.
