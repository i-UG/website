# UK IBM i User Group Website

![i-UG Website](/assets/logo/logo.png)

The official website for the UK IBM i User Group.<br><br>
A single-page informational site covering events, news & how to get in touch.

**Live site:** [i-ug.co.uk](https://i-ug.co.uk)

## Tech stack

- **Static, one-page site** — no database, no server-side code, no CMS
- **Tailwind CSS** for all styling
- **Hosted on Azure Static Web Apps** (Free tier)
- **Deployed automatically via GitHub Actions** whenever changes are merged into `main`
- **Contact form** powered by [Formspree](https://formspree.io) (free tier) — submissions are emailed directly to the configured inbox with no backend required.  Currently, the email addresses Andy.Youens@i-ug.co.uk & saroj.bains@i-ug.co.uk are the recipients. If this needs to change, a issue needs to be raised on gitHub.

> ⚠️ **Please don't deviate from this technical foundation.** No additional pages, no alternative CSS frameworks (Bootstrap, custom stylesheets, etc.), no CMS or page builders. Any proposed change to this foundation should go through the Development Director first, separately from routine content edits.

## Project structure

```text
├── .git/                         # Git version control - do not edit!
├── .github/
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.md         # Bug report issue template
│   │   ├── config.yml            # Issue template chooser config
│   │   ├── feature_request.md    # Feature request issue template
│   │   └── issue.md              # General issue template
│   ├── workflows/
│   │   └── azure-static-web-apps-yellow-bay-013bff303.yml  # Azure deployment workflow
│   └── PULL_REQUEST_TEMPLATE.md  # PR description template
├── index.html                    # The single page — all content lives here
├── announcements.json            # Announcement cards data — edit this to update the announcements section
├── /assets/css                   # Tailwind stylesheets
├── /assets/images                # Images
├── /assets/logo                  # Logos
├── website_update_guide.pdf      # Images
└── README.md                     # this bumph
```

## How changes get published....

Changes will only be made that have a GitHub issue raised [here](https://github.com/i-UG/website/issues).  **NO other changes will be considered or worked on.**

Nobody edits the live site directly. Every change goes through a review step:

1. Open the relevant file on GitHub and make your edit (small text/content changes can be done directly in the GitHub web interface — no coding tools required).
2. This automatically creates a branch and a **pull request** — a request for the change to be reviewed.
3. The **Development Director** reviews the change, leaving comments if anything needs adjusting.
4. Once approved, the Director **merges** the pull request. This is the only step that can publish a change — only the Development Director can merge into `main`.
5. Azure automatically rebuilds and republishes the site, usually within a minute or two. No manual deployment step is ever needed.

See the **Website Update Guide** [Found here](./Website-Update-Guide.pdf), for the full walkthrough.

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

## Announcements

The **Announcements** section (displayed below the hero banner) is driven entirely by [`announcements.json`](./announcements.json) in the repo root — no code changes are needed to add, edit, or remove announcements.

### Format

```json
[
  {
    "text": "Your announcement text here",
    "icon": "🔔",
    "url": "https://link-to-more-info"
  }
]
```

| Field | Required | Notes |
|---|---|---|
| `text` | ✅ Yes | The announcement message displayed on the card |
| `icon` | No | Any single emoji — shown to the left of the text |
| `url` | No | If provided, a "Find out more →" link is added to the card (opens in a new tab) |

### How to add or remove an announcement

1. Edit [`announcements.json`](./announcements.json) directly in GitHub (or via a branch/PR).
2. Add a new JSON object to the array for a new announcement, or delete an object to remove one.
3. There is no limit on the number of announcements — cards wrap into a responsive grid (1 col → 2 col → 3 col).
4. To hide the section entirely, return an empty array `[]`.

> The announcements section uses **Google Sans** font and matches the IBM carbon design language of the rest of the site.

---

## Contact form

The **Contact Us** form on the page submits to [Formspree](https://formspree.io) via a `fetch()` POST. No server-side code is involved.

| Detail | Value |
|---|---|
| Formspree endpoint | `https://formspree.io/f/mvkopbno` |
| Fields submitted | `name`, `email`, `message` |
| Success / error handling | Handled in the `contactForm` submit listener in `index.html` |

**To change the destination email address:** log in to [formspree.io](https://formspree.io), open the form, and update the email under Settings — no code change required.

**To view or export past submissions:** log in to Formspree and open the Submissions tab for the form.

**Allowed origins:** if the form stops working after a domain change, update the allowed origins in the Formspree dashboard under Settings → Allowed Origins.

## Branch protection

- `main` is protected: no direct pushes, pull requests required & only the Development Director can approve and merge.
- Committee members have **Write** access, which allows branches and pull requests but not direct merges to `main`.

## Maintainer

**Development Director:**   [![GitHub: AndyYouens](https://img.shields.io/badge/GitHub-AndyYouens-blue?logo=github)](https://github.com/AndyYouens)

## License

This project is licensed under a proprietary license. All rights reserved by FormaServe Systems Ltd. Unauthorized copying, distribution, or modification of this code is strictly prohibited without prior written consent from FormaServe Systems Ltd.
