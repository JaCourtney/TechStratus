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

## Brand
- Primary blue `#046bd2`, deeper blue `#045cb4`, footer blue `#206fb0`, cyan accent `#78c9db`.
- Headings use Inter; body falls back to the system stack.
- Logo: `assets/logo-color.png` (for light bg), `assets/logo-white.png` (for dark bg).

## Deploy
- Cloudflare Pages auto-deploys on every push to `main`. No build command; output dir is the repo root.
- Manual: `npx wrangler pages deploy . --project-name techstratus`.

## Open items
- Contact form is not wired to a backend yet (see README "To do").
- Domain `techstratus.com` still needs to be pointed at the Pages project.
