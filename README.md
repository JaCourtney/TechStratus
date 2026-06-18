# TechStratus

Marketing website for **TechStratus** — friendly technology support for seniors,
families, home offices, and small businesses in Missoula, Montana.

Plain static site (HTML / CSS / JS). No build step. Hosted on **Cloudflare Pages**,
source on **GitHub**.

## Structure

```
.
├── index.html        # the whole page
├── css/styles.css    # all styles (brand colors live in :root at the top)
├── js/main.js         # mobile nav, scroll effects, contact form
├── assets/            # logo + hero video
└── _headers           # Cloudflare caching/security headers
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

- [ ] **Connect the contact form.** It currently shows a placeholder message.
      Easiest option: [Formspree](https://formspree.io) — create a form, then set
      `<form action="https://formspree.io/f/XXXX" method="POST">` in `index.html`
      and remove the `e.preventDefault()` handling in `js/main.js`.
- [ ] Point the `techstratus.com` domain at the Cloudflare Pages project.
- [ ] Add real photos to replace the logo placeholder in the "About" section.

## Contact info on the site

- Phone: 406-284-5523
- Email: jacob@techstratus.com
- Location: Missoula, MT
