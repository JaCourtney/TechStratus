# TechStratus

Marketing website for **TechStratus** — friendly technology support for seniors,
families, home offices, and small businesses in Missoula, Montana.

Plain static site (HTML / CSS / JS). No build step. Hosted on **Cloudflare Pages**,
source on **GitHub**.

## Structure

Multi-page static site. Each page is a standalone `.html` file with the same
header/footer copied in (no build step, so shared markup is duplicated across
files, not templated).

```
.
├── index.html          # Home (full content)
├── personal-technology.html, senior-support.html, family-support.html,
│   home-office-support.html                        # Personal Technology + subpages
├── business-solutions.html, business-it-services.html, digital-presence.html,
│   ai-automation.html, technology-consulting.html   # Business Solutions + subpages
├── about.html, contact.html
├── resources.html, faq.html, technology-guides.html,
│   blog.html, support-resources.html                # Resources + subpages
├── css/styles.css      # all styles (brand colors live in :root at the top)
├── js/main.js          # mobile nav, scroll effects, contact form
├── assets/             # logos, hero video/photos
└── _headers            # Cloudflare caching/security headers
```

## Editing & previewing locally

Open `index.html` in a browser, or run a tiny local server (nicer for video/paths):

```bash
npx serve .
# or
python -m http.server 8000
```

## Deploying

Cloudflare Pages is connected to this GitHub repo. **Any push to `main`
automatically publishes the live site** — no manual deploy needed.

Manual deploy (optional, uses the Wrangler CLI):

```bash
npx wrangler pages deploy . --project-name techstratus
```

## To do

See **[PROJECT-PLAN.md](PROJECT-PLAN.md)** — the full site map (which pages are
built vs. still blank) and the running punch list live there now, not here.

## Contact info on the site

- Phone: 406-284-5523
- Email: jacob@techstratus.com
- Location: Missoula, MT
