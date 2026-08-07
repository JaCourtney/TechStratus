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

### Blocking / functional
- [ ] **Connect the contact form.** It currently shows a placeholder message
      instead of actually sending anything. Easiest option:
      [Formspree](https://formspree.io) — create a form, then set
      `<form action="https://formspree.io/f/XXXX" method="POST">` in
      `contact.html` and remove the `e.preventDefault()` handling in `js/main.js`.
- [ ] **Point `techstratus.com` at Cloudflare Pages.** Still on the old
      WordPress host. Need to confirm whether the domain's DNS is already on
      Cloudflare or managed elsewhere (e.g. Hostinger) before doing this.

### Content still needed (blank pages)
- [ ] Home Office Support (last of the 3 Personal Technology subpages)
- [ ] Business Solutions overview + its 4 subpages (Business IT Services,
      Digital Presence, AI & Automation, Technology Consulting)
- [ ] About
- [ ] Contact (currently just a title band — the real contact info/form still
      lives on Home; decide whether to move it here)
- [ ] Resources overview + its 4 subpages (FAQ, Technology Guides, Blog,
      Support Resources)
- [ ] **Blog specifically**: once there's more than one post, hand-coded HTML
      pages get tedious to maintain — worth a simpler approach (templating or
      a lightweight generator) before writing much content there.

### Polish / cleanup
- [ ] **Compress images/video** — several assets are large for the web:
      `assets/Stock.png` (~2.9 MB), `assets/hero-video.mp4` (2.4 MB),
      `assets/home-tech.png` (1.7 MB), `assets/senior-support-hero.png` (1.9 MB),
      `assets/family-support-hero.png` (1.8 MB). Worth a batch pass to shrink
      these (WebP/optimized MP4) for page speed.
- [ ] **Favicon visibility** — `assets/logo-white.png` is set as the browser-tab
      icon, but it's a white shape on a transparent background, so it may be
      invisible on light-colored tabs. Consider the colored logo instead, or a
      white logo on a small blue background tile.
- [ ] Family Support hero photo is dark/warm-toned; under the white overlay it
      may read as too faded — an easy opacity tweak if so.
- [ ] "Smart-Home Support" tile icon (Personal Technology page) is a generic
      house icon since no dedicated smart-home icon existed; swap for something
      more distinctive if desired.
- [ ] Unused CSS: the old homepage "How It Works" step styles are still in
      `styles.css` even though that section was removed from `index.html`.
      Harmless, but could be deleted for a tidier file.

### Decisions made along the way (revisit if wrong)
- All "Request Support / Schedule a Consultation / Contact TechStratus"-style
  buttons on Personal Technology, Senior Support, and Family Support currently
  point to `contact.html` — there's no separate booking/request system yet.
- Family Support has "Home Network and Wi-Fi Support" as both a short card
  (Services Offered) and its own deeper section later — kept exactly as
  written since the source content repeated it, but flagging in case it was
  meant to be one or the other.

## Contact info on the site

- Phone: 406-284-5523
- Email: jacob@techstratus.com
- Location: Missoula, MT
