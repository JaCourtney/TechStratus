# TechStratus — project notes for Claude

## What this is
A plain **static website** (HTML/CSS/JS, no build step, no framework) for TechStratus,
a technology-support business in Missoula, MT. Source on GitHub, hosted on Cloudflare Pages.

## Working on it
- The entire page is `index.html` (single-page site with anchor sections).
- All styling is `css/styles.css`. **Brand colors are CSS variables in `:root`** at the top —
  change them there, not scattered through the file.
- Behavior is `js/main.js` (vanilla JS, no dependencies).
- Keep it dependency-free and buildless. Don't introduce a framework or bundler unless asked.

## Brand (official — from "TechStratus Brand & Marketing Overview")
- **TechStratus Blue `#2070AF`** — primary: headings, buttons, links, CTAs.
- **Sky Blue `#78C9DB`** — highlights & accents.
- **Slate `#355063`** — body text, dark areas (nav, footer).
- **White `#FFFFFF`** — used generously; keep designs open and uncluttered.
- Colors live as CSS variables in `:root` (`--blue`, `--sky`, `--slate`).
- **Hexagons are the primary visual motif** (pointy-top, matching the logo). Used as icon
  frames via `clip-path`. Keep them supportive, not dense — no glow, no circuit-board look.
- Voice: calm, direct, encouraging. No hype ("skyrocket", "transform overnight", "guaranteed").
- Headings use Inter; body falls back to the system stack.
- Logo: `assets/logo-color.png` (light bg), `assets/logo-white.png` (dark bg).

## Deploy
- Cloudflare Pages auto-deploys on every push to `main`. No build command; output dir is the repo root.
- Manual: `npx wrangler pages deploy . --project-name techstratus`.

## Open items
- Contact form is not wired to a backend yet (see README "To do").
- Domain `techstratus.com` still needs to be pointed at the Pages project.
