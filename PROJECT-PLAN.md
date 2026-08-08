# TechStratus — Project Plan

Living tracker for the site build. Update this as pages get built out or
priorities change — it's the one place to check "where are we" without
digging through chat history.

## Site map & status

Legend: ✅ built out · ⬜ blank stub (title only)

- **Home** (`index.html`) — ✅
- **Personal Technology** (`personal-technology.html`) — ✅
  - Senior Tech Support (`senior-support.html`) — ✅
  - Family Tech Support (`family-support.html`) — ✅
  - Home Office Support (`home-office-support.html`) — ✅
- **Business Solutions** (`business-solutions.html`) — ⬜
  - Business IT Services (`business-it-services.html`) — ⬜
  - Digital Presence (`digital-presence.html`) — ⬜
  - AI & Automation (`ai-automation.html`) — ⬜
  - Technology Consulting (`technology-consulting.html`) — ⬜
- **About** (`about.html`) — ⬜
- **Resources** (`resources.html`) — ⬜
  - Frequently Asked Questions (`faq.html`) — ⬜
  - Technology Guides (`technology-guides.html`) — ⬜
  - Blog (`blog.html`) — ⬜
  - Support Resources (`support-resources.html`) — ⬜
- **Contact** (`contact.html`) — ⬜ (title only; the real contact info/form still lives on Home)

## Open items

### Blocking / functional
- [ ] **Connect the contact form.** It currently shows a placeholder message
      instead of actually sending anything. Easiest option:
      [Formspree](https://formspree.io) — create a form, then set
      `<form action="https://formspree.io/f/XXXX" method="POST">` in
      `contact.html` and remove the `e.preventDefault()` handling in `js/main.js`.
- [ ] **Point `techstratus.com` at Cloudflare Pages.** Still on the old
      WordPress host. Need to confirm whether the domain's DNS is already on
      Cloudflare or managed elsewhere (e.g. Hostinger) before doing this.

### Content still needed
- [ ] Business Solutions overview + its 4 subpages
- [ ] About
- [ ] Contact (decide whether the contact info/form moves here from Home)
- [ ] Resources overview + its 4 subpages
- [ ] **Blog specifically**: once there's more than one post, hand-coded HTML
      pages get tedious to maintain — worth a simpler approach (templating or
      a lightweight generator) before writing much content there.

### Polish / cleanup
- [ ] **Compress images/video** — several assets are large for the web:
      `assets/Stock.png` (~2.9 MB), `assets/hero-video.mp4` (2.4 MB),
      `assets/home-tech.png` (1.7 MB), `assets/senior-support-hero.png` (1.9 MB),
      `assets/family-support-hero.png` (1.8 MB), `assets/home-office-support-hero.png`
      (1.6 MB). Worth a batch pass to shrink these (WebP/optimized MP4) for
      page speed.
- [ ] **Favicon visibility** — `assets/logo-white.png` is set as the browser-tab
      icon, but it's a white shape on a transparent background, so it may be
      invisible on light-colored tabs. Consider the colored logo instead, or a
      white logo on a small blue background tile.
- [ ] "Smart-Home Support" tile icon (Personal Technology page) is a generic
      house icon since no dedicated smart-home icon existed; swap for something
      more distinctive if desired.
- [ ] Unused CSS: the old homepage "How It Works" step styles are still in
      `styles.css` even though that section was removed from `index.html`.
      Harmless, but could be deleted for a tidier file.

### Decisions made along the way (revisit if wrong)
- All "Request Support / Schedule a Consultation / Contact TechStratus"-style
  buttons on Personal Technology, Senior Tech Support, and Family Tech Support currently
  point to `contact.html` — there's no separate booking/request system yet.
- Family Tech Support has "Home Network and Wi-Fi Support" as both a short card
  (Services Offered) and its own deeper section later — kept exactly as
  written since the source content repeated it, but flagging in case it was
  meant to be one or the other.
- Family Tech Support's hero now uses the same looping video as Home (was briefly
  a static photo of a teenager on a phone). That photo is now used instead
  in the "Common Challenges Families Face" section (image + text/checklist
  side by side) as an experiment — was a fairly full section already, so
  worth a look to see if it feels too dense.

## Change log

- Built out Home Office Support (last of the 3 Personal Technology
  subpages) in the now-established pattern: video hero with blue title +
  subheadline + narrative, Common Challenges with the supplied photo
  (`home-office-support-hero.png`) side-by-side with the checklist, 5-card
  Services Offered, 5 deep-dive sections merged into flip cards (Workspace
  Optimization, Networking and Connectivity, Data Protection and Backup,
  Security and Account Management, Remote Work Support), 3-card Appointment
  Options, 5-item FAQ, closing CTA. Restore point tagged:
  `home-office-support-before-build`. This completes all 3 Personal
  Technology subpages.
- Fixed a sitewide bug: the "Get Started" nav button's text turned blue on
  hover (against its blue gradient background, effectively invisible)
  because the generic `.nav-menu a:hover` rule was more specific than the
  button's own hover color. Added a more specific override
  (`.nav-menu .nav-cta a:hover`) so it stays white. Affects every page
  (shared header).
- Family Tech Support flip-card order and copy: shortened the Child and
  Teen Online Safety narrative to two tight sentences; reordered the cards
  to Child and Teen Online Safety, Support for Parents, Device and Account
  Organization, Home Network and Wi-Fi Support, Family Technology
  Education.
- Family Tech Support tweaks: swapped the Services Offered "Home Network
  and Wi-Fi Support" card icon from the reused check-circle placeholder to
  an actual Wi-Fi icon (scoped to just this card; Senior Support's "Home
  Wi-Fi Support" and Personal Technology's "Wi-Fi Support" tile still use
  the check-circle and weren't touched). Removed the first of three
  paragraphs from the Child and Teen Online Safety flip card's front (down
  to 2, matching the other cards). Swapped the flip-card order so Family
  Technology Education comes before Child and Teen Online Safety.
- Brought Family Tech Support's five deep-dive sections (Child and Teen
  Online Safety, Family Technology Education, Device and Account
  Organization, Home Network and Wi-Fi Support, Support for Parents) into
  the same flip-card treatment as Senior Tech Support: merged into one blue
  section, front = title (blue, bigger) + narrative + "Click to See How We
  Help" hint, back = lead-in label + checklist (closing sentence removed).
  List items were NOT trimmed here (that was specific to Senior's cards) —
  all original checklist content kept as-is.
  `.flip-grid` switched from a fixed 2-column grid to flexbox (matching the
  `.why-grid` fix) so 5 cards wrap as a centered 2+2+1 instead of stranding
  the 5th card; Senior's 4-card 2x2 is unchanged (486px card width still
  fits exactly 2 per row). Restore point tagged:
  `family-support-before-flip-cards`.
- Fixed a scrollbar bug on the Scam and Online Safety Assistance and
  Device and Account Organization card backs: `.checklist-centered`
  (added to visually center these two trimmed lists) was narrowing an
  already-narrow 2-column layout down to ~85px of usable text per column,
  which forced heavy line-wrapping and pushed the content past the card's
  fixed 420px height. Switched `.checklist-centered` to a single centered
  column instead of a narrowed 2-column one — items get nearly the full
  card width, so there's little to no wrapping and the content fits
  without scrolling.
- Trimmed the two flip-card lists once more (Scam and Online Safety
  Assistance: 7 -> 6 items, now an even 3/3 split; Device and Account
  Organization: 8 -> 7).
- Fixed `.why-grid` (used by Senior/Family Support's "Services Offered" and
  Personal Technology's "Why TechStratus?", all 5-card sections): switched
  from CSS grid auto-fit to flexbox with a capped card width. Grid's
  auto-fit left a lone 5th card stranded on the left of an otherwise-empty
  row; flexbox centers a short last row instead, so 5 cards read as a clean
  centered 3+2 everywhere `.why-grid` is used, not just on this page.
- Trimmed two of the four flip cards further: shortened the Scam and Online
  Safety Assistance narrative; removed 2 items from its back list (9 -> 7)
  and 1 item from Device and Account Organization's (9 -> 8); both trimmed
  lists now centered as a block (new `.checklist-centered` modifier, scoped
  to just these two) rather than stretching full-width. Also trimmed a
  couple of words from Support for Adult Children Coordinating Care's two
  narrative paragraphs.
- Flip-card follow-up tweaks: card titles are bigger and blue (matching the
  hero heading); front now ends with a blue "Click to See How We Help" hint
  (reuses `.eyebrow` styling); removed the closing italic sentence from each
  back; back checklists switched from a 2-column CSS grid to a balanced
  multi-column flow so odd-numbered lists (9 items, 3 of the 4 cards) don't
  leave a gap in the last row. Note: true equal-count columns aren't
  possible for 9 items without adding/trimming a real list item — flagged
  to the user rather than done unilaterally.
- **Experiment** on Senior Tech Support: merged the four stacked sections
  (Patient Technology Instruction, Scam and Online Safety Assistance, Device
  and Account Organization, Support for Adult Children Coordinating Care)
  into one blue section with a 2x2 grid of flip cards. Front = title +
  narrative; back (on hover/focus) = the lead-in label, checklist, and
  closing italic line. New `.flip-grid`/`.flip-card` CSS.
  Saved a restore point before making this change: git tag
  `senior-support-before-flip-cards` (revert with
  `git checkout senior-support-before-flip-cards -- senior-support.html`).
  Known limitation: hover doesn't work well on touch devices (tap-to-flip
  behavior varies by mobile browser) — worth a JS fallback if this sticks.
- Worked "tech support" into both pages' meta descriptions to match the new
  naming, and trimmed the intro paragraph + "Common challenges include"
  eyebrow from the top of each Common Challenges section (goes straight from
  heading/photo to the checklist now — those sections were feeling full).
- Renamed "Senior Support" → "Senior Tech Support" and "Family Support" →
  "Family Tech Support" site-wide (nav, page titles, H1s, card labels, CTA
  buttons) for SEO. URLs (`senior-support.html` / `family-support.html`)
  were left as-is — only visible text changed; revisit if the slugs should
  match too.
- Built Home, Personal Technology, Senior Tech Support, Family Tech Support pages.
- Restructured nav into Personal Technology / Business Solutions / Resources
  dropdowns, each with subpages (all currently blank except the three above).
- Family Tech Support hero: photo → matched Home's white-overlay treatment →
  switched to Home's actual looping video background.
- Senior Tech Support hero rebuilt to match Family Tech Support's pattern: short H1
  ("Senior Tech Support") + subheadline (the old long headline) + same looping
  video background as Home/Family Tech Support. Both pages' hero H1s now use the
  same blue as "Technology" on Home's headline (new `.hero-title-accent`
  class, scoped so Home's two-tone headline is untouched).
- Moved the Senior Tech Support hero photo down into "Common Challenges Seniors
  Face" (same image + text/checklist side-by-side treatment as Family
  Support's Common Challenges section).
- Fixed a real readability bug: on blue-background sections, plain text,
  "eyebrow" labels, and checklist items that sit directly on the blue
  background (not inside a white card/FAQ box) were using their normal dark
  colors — including `.eyebrow`, which was blue-on-blue and essentially
  invisible. All of that now turns white on blue sections; text inside
  white cards/FAQ items is unaffected. Checkmark bullets unchanged.
