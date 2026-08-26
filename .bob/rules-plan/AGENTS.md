# Project Architecture Rules (Non-Obvious Only)

- **Single HTML file, no build pipeline** — The entire site is `index.html` + pre-compiled CSS. Any plan involving a build step, framework, or additional pages requires Development Director approval and is effectively a new tech stack decision.
- **CSS is frozen** — `assets/css/tailwind.css` cannot be extended without a Tailwind build environment (none exists in this repo). Any plan that requires new CSS classes beyond what's already compiled is blocked unless the CSS file is regenerated — which itself requires a new toolchain.
- **JS is a single inline block** — All interactivity lives in one `<script>` tag at the bottom of `index.html`. There are no modules, imports, or external scripts. Plans for new JS features should treat this as the only JS surface area.
- **Contact form has no backend** — Any plan to make the form functional requires both a backend endpoint and a rewrite of the frontend `setTimeout` simulation in the inline `<script>`.
- **Azure deployment is zero-config** — The CI/CD pipeline (`app_location: "/"`, `output_location: "."`) serves files as-is with no build step. Adding a build step would require changes to the workflow YAML and approval.
- **Two nav copies are structurally coupled** — Any plan that changes navigation must account for the fact that desktop and mobile navs are independent HTML blocks that must always match.
