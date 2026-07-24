# AI Agent Guidelines for i-UG Website

## Project Overview

- **Type:** Single-page static informational website
- **Tech Stack:** HTML, Tailwind CSS, hosted on Azure Static Web Apps
- **Auto-deployment:** GitHub Actions → Azure (on merge to `main`)
- **Approval process:** All changes require Development Director review and approval before merge

## Hard Technical Constraints ⚠️

**Do NOT violate these. Any proposed change to these should be escalated to the Development Director.**

1. **Single-page only** — All content lives in `index.html`. No additional pages allowed.
2. **Tailwind CSS only** — No Bootstrap, custom stylesheets, or alternative CSS frameworks.
3. **No CMS, no page builders** — Keep the stack static and simple.
4. **No server-side code** — This is a static site.

## Typical Agent Tasks

### Content Updates (In Scope)

- Fix typos, update dates, event details, contact info
- Small wording improvements, clarifications
- Image updates/optimizations
- Rewording for tone or clarity

### Layout/Design Changes (Escalate to Development Director)

- New sections or layout restructuring
- Styling changes that go beyond fixing broken styles
- Adding new interactive features
- Changing the overall site structure

## Important Workflows

### Branch Protection

- `main` is protected: no direct pushes, PRs required
- Only Development Director can merge PRs
- See [README.md](./README.md#branch-protection) for full details

### Local Development

```bash
git clone https://github.com/i-UG/website
cd website
npx serve .  # Local preview
```

## File Structure

```
index.html           # The single page — edit here for content
/assets/css/         # Tailwind stylesheets (rarely modified)
/assets/images/      # Images
/assets/logo/        # Logo assets
/public/docs/        # External docs (e.g., Website-Update-Guide.pdf)
```

## Key Resources

- [Website Update Guide](./public/docs/Website-Update-Guide.pdf) — Full walkthrough for contributors
- [README.md](./README.md) — Project overview and contributor guidelines
- **Development Director:** [AndyYouens](https://github.com/AndyYouens) — Sole approver/merger for `main`

## Decision Framework for Agents

| Situation | Action |
|-----------|--------|
| Fix typo, update date/event info | ✅ Implement directly |
| Improve wording or clarity | ✅ Implement directly |
| Fix broken styles (CSS) | ✅ Implement directly |
| New section, redesign, or layout change | ⚠️ Open issue/draft PR for discussion first |
| Change to tech stack (CSS framework, new pages, etc.) | 🛑 Escalate to Development Director |
| Questions about scope or suitability | 💬 Open as discussion or comment in PR |

## Git Workflow

1. Create a feature branch from `main`
2. Make and commit changes
3. Open a pull request with clear description
4. Development Director reviews and merges
5. Azure auto-deploys on merge
