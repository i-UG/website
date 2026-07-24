# UK IBM i User Group Website

The official website for the UK IBM i User Group — a single-page informational site covering events, news, and how to get in touch.

**Live site:** _add your Azure Static Web Apps URL / custom domain here_

## Tech stack

- **Static, one-page site** — no database, no server-side code, no CMS
- **Tailwind CSS** for all styling
- **Hosted on Azure Static Web Apps** (Free tier)
- **Deployed automatically via GitHub Actions** whenever changes are merged into `main`

> ⚠️ **Please don't deviate from this technical foundation.** No additional pages, no alternative CSS frameworks (Bootstrap, custom stylesheets, etc.), no CMS or page builders. Any proposed change to this foundation should go through the Development Director first, separately from routine content edits.

## Project structure

```text
├── index.html          # The single page — all content lives here
├── /assets             # Images, icons, etc.
├── /css                # Tailwind stylesheets
└── README.md
```

## How changes get published

Nobody edits the live site directly. Every change goes through a review step:

1. Open the relevant file on GitHub and make your edit (small text/content changes can be done directly in the GitHub web interface — no coding tools required).
2. This automatically creates a branch and a **pull request** — a request for the change to be reviewed.
3. The **Development Director** reviews the change, leaving comments if anything needs adjusting.
4. Once approved, the Director **merges** the pull request. This is the only step that can publish a change — only the Development Director can merge into `main`.
5. Azure automatically rebuilds and republishes the site, usually within a minute or two. No manual deployment step is ever needed.

See the **Website Update Guide** (shared with the committee) for the full walkthrough.

## Contributing (Committee members)

- Stick to minor content updates: event details, contact info, dates, small wording fixes.
- Keep to the one-page, Tailwind-only technical foundation described above.
- Anything involving new design, layout, or page structure should be discussed with the Development Director first.
- If you're not sure whether a change is in scope, open the pull request anyway and leave a comment — it's easy to discuss before anything goes live.

## Local development

```bash
# Clone the repo
git clone https://github.com/i-UG/website
cd website

# Open index.html in a browser or use a local server, e.g.:
npx serve .
```

## Branch protection

- `main` is protected: no direct pushes, pull requests required, and only the Development Director can approve and merge.
- Committee members have **Write** access, which allows branches and pull requests but not direct merges to `main`.

## Maintainer

**Development Director:** @AndyYouens
