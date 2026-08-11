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
- **Business Solutions** (`business-solutions.html`) — ✅ (overview page; 2 subpages still blank)
  - Business IT Services (`business-it-services.html`) — ✅
  - Digital Presence (`digital-presence.html`) — ✅
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
- [ ] Business Solutions's remaining 2 subpages (AI & Automation,
      Technology Consulting)
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
      (1.6 MB), `assets/business-solutions-hero.png` (2.0 MB),
      `assets/business-it-services-hero.png` (2.1 MB),
      `assets/digital-presence-hero.png` (1.7 MB). Worth a batch
      pass to shrink these (WebP/optimized MP4) for page speed.
- [ ] **Duplicate image files**: `assets/Business-IT-services-image.png`
      and `assets/Digital-Presence-image.png` (the original, mixed-case
      files the user placed in the project) are still sitting untracked
      in `assets/` — their content was copied to `business-it-services-hero.png`
      and `digital-presence-hero.png` (lowercase, matching the site's naming
      convention), which are what the pages actually use. The originals are
      unused; ask before deleting them since they weren't created this session.
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

- Made Digital Presence's 3 stacked flip-cards span the full content
  width (`.container`, ~1116px) instead of the default 486px, so
  they're wider than tall (landscape) rather than the other way
  around. `.flip-grid-stacked` now clears its own max-width and forces
  `flex-basis: 100%` on the cards. At that width the front paragraph
  text was hitting ~117 characters per line (unreadable), so
  constrained the inner text/checklist to a 640px centered reading
  column via `.flip-grid-stacked .flip-card-front-content` and
  `.flip-grid-stacked .flip-card-back > *` — the visible white card
  stays full width, only the text column inside is narrower. Confirmed
  zero overflow on all 3 cards at desktop width; the mobile overflow
  that shows up at 375px is pre-existing (mobile card width was
  already governed by the unrelated `flex-basis:100%` responsive rule,
  unchanged by this edit) and matches the same graceful internal-
  scroll behavior already present on Senior Support and Business IT
  Services' mobile flip-cards.
- Restored the tagline sub-headings ("A Better Home for Your Business
  Online," etc.) on Digital Presence's 3 flip-card fronts, under each
  h3. Added `.card-tagline` styling scoped to `.flip-card-front-content`
  (reusing the existing `.card-tagline` class name, since the original
  rule required a `.card` ancestor that doesn't exist here) plus a
  `.section-blue` override so it stays blue rather than picking up the
  section's white/slate text-color rules. Re-verified all 3 cards still
  fit exactly at 560px with zero overflow after adding the extra line.
- Consolidated Digital Presence's three separate service sections
  (Website Design & Development, Branding & Identity, Social Media &
  Digital Marketing — previously full alternating-background sections
  with their own headings and buttons) into one `.flip-grid` section,
  matching Business IT Services' card mechanism exactly (hover-to-flip
  on desktop, tap-to-focus on mobile, same 486x560 card size via
  `.flip-grid-tall`). Added a new `.flip-grid-stacked` modifier
  (`max-width: 486px`) so the 3 cards stack in a single column instead
  of wrapping 2-per-row, per the request. Dropped the "Explore ...
  Services" buttons and the tagline sub-headings (e.g. "A Better Home
  for Your Business Online"), since the Business IT Services card
  format doesn't have either — flagged this to the user rather than
  silently cutting content. Kept all three intro paragraphs on Social
  Media & Digital Marketing's front (didn't preemptively trim, per
  earlier feedback); verified zero overflow on all 3 cards without any
  text changes needed this time.
- Added the 8-item FAQ to Digital Presence, right before the CTA,
  matching the FAQ-before-CTA convention used on Senior Support and
  Business IT Services. Since FAQ is always `.section-blue` sitewide
  and "One Partner for Your Digital Presence" (the section right
  before it) was already blue, inserting FAQ there would have created
  two blue sections in a row. Changed "One Partner" to a plain white
  section instead (removing `section-blue`) so the rhythm reads
  white -> white -> blue(FAQ) -> white(CTA) — one intentional
  white/white adjacency, same precedent already used on Business
  Solutions between its Why and CTA sections.
- Built the Digital Presence subpage (second of Business Solutions'
  4 subpages), based on Business IT Services' layout family: video
  hero, a white photo+text overview section (using
  assets/digital-presence-hero.png), then three full detailed service
  sections (Website Design & Development, Branding & Identity, Social
  Media & Digital Marketing), each with its own two-tier heading
  (section-head h2 + tagline), narrative, checklist, and an "Explore
  ... Services" button linking to contact.html (no dedicated subpages
  exist for these three yet). Used plain sections rather than flip
  cards here, since each has its own heading/button unlike Business IT
  Services' 9 uniform topics. Followed by Featured Work (4-tile
  commitment grid: Websites, Brand Identities, Social Campaigns,
  Before & After), a 6-step Our Process (reused the `.steps` numbered
  component, but the shared 4-column desktop grid would strand steps
  5-6, so added `#process .steps { grid-template-columns: repeat(3,
  1fr); }` scoped to min-width:901px to leave the existing 2-col/1-col
  responsive breakpoints untouched), Flexible Ways to Work Together
  (4-card cards-2 grid, mixed content shapes — one card has no
  checklist), a closing "One Partner" narrative section, and a final
  CTA. No FAQ section, since none was supplied for this page. Verified
  all checklist item counts, section alternation (clean blue/white
  rhythm), and both grid-stranding fixes (6 steps at 3+3, 4 featured
  tiles centering their lone 4th item) in the browser.
- Corrected an overcorrection: the prior pass had consolidated the
  front and back text on all 9 Business IT Services flip-cards and
  shrunk them to 420px, but the user only wanted the one card that
  actually forced the 560px -> 640px jump (Continuous Device
  Monitoring, which has two closing-paragraph sentences) trimmed.
  Restored the original two front paragraphs and full closing text on
  the other 8 cards, consolidated only Continuous Device Monitoring's
  two closing sentences into one, restored the card height to 560px
  (`.flip-grid-tall`), and removed the padding/margin tightening added
  for the 420px squeeze (no longer needed at 560px). Kept the
  `.section-blue .flip-card-back p` color-fix from the previous pass,
  since that was a genuine bug (invisible white-on-white text) rather
  than something the user asked to revert. Verified all 9 cards fit at
  exactly 560px with zero overflow on both faces.
- Reverted Business IT Services' flip-cards to the original shared
  size (486x420, matching Senior/Family/Home Office Support) instead of
  the taller 640px variant from the previous pass. Consolidated each
  front's two intro paragraphs into one shorter paragraph, and trimmed
  each back's closing line to a short clause, to fit the restored
  height. The checklist itself (up to 10 items) was already consuming
  nearly the entire 420px budget, so text trimming alone wasn't enough
  for the denser cards — also tightened checklist/eyebrow spacing and
  back padding, scoped to `#services` only, so the other three
  flip-card pages are untouched. Verified all 9 cards fit exactly at
  420px with zero overflow on both faces. Also fixed a real bug: the
  restored closing paragraph had no `.section-blue` color override, so
  it inherited white text on top of the flip-card-back's white
  background (invisible) — added `.section-blue .flip-card-back p` to
  the existing slate-color override list.
- Restored the closing paragraph on each Business IT Services flip-card
  back (removed in the prior pass, added back per follow-up request).
  Continuous Device Monitoring has two closing paragraphs, same as the
  original plain-card version. This pushed 1 of the 9 cards (the one
  with two closing paragraphs) past the 560px flip-card height set in
  the last pass, so bumped `.flip-grid-tall .flip-card` to 640px and
  re-verified all 9 cards for overflow on both faces (none). Also added
  a new white "A Complete IT Partner for Your Organization" overview
  section right after the hero (photo + text, `.section.about` /
  `.about-grid`, matching Business Solutions' overview section pattern)
  using `assets/business-it-services-hero.png` (copied from the user's
  `Business-IT-services-image.png`, lowercase-hyphenated per site
  convention) with new summary copy synthesized from the 9 services
  below it (not verbatim user copy, since none was given for this
  section).
- Converted the Business IT Services "Our Services" grid from plain
  cards to flip cards (hover on desktop, tap/focus on mobile), matching
  Senior/Family/Home Office Support's flip-card pattern. Front now
  shows icon + title + the two intro paragraphs + "Click to See How We
  Help" hint; back shows the eyebrow + checklist. Dropped the closing
  paragraph that followed each list (per instruction). Added the icon
  to the front for the first time in this component (existing flip
  cards elsewhere have no icon) via a new `.flip-card-front-content
  .card-icon { margin: 0 auto 1.25rem; }` rule. Also discovered the
  shared 420px `min-height` was too short once an icon and two full
  paragraphs were added — every card overflowed on both faces. Fixed
  with a page-scoped `.flip-grid-tall` modifier (560px min-height)
  rather than changing the shared 420px default used by the other
  three flip-card pages.
- Built the Business IT Services subpage (first of Business Solutions'
  4 subpages), following the same layout family as the Personal
  Technology subpages: video hero (title, subheadline, 3 paragraphs,
  2 buttons), a 9-card "Our Services" grid (3x3, `.cards-3`, on
  `.section-blue`, plain non-flipping cards since the content per
  topic was too dense for the flip-card format used on Senior/Family/
  Home Office Support), a 3-tier "Managed Service Plans" card grid
  (Essential/Managed/Complete), a 7-item FAQ accordion, and a closing
  CTA. Single-column checklists throughout (matching the established
  cards-3 width convention) rather than the 2-column variant used in
  wider cards elsewhere. All 9 service topics and 3 plan tiers came
  from the user's supplied copy verbatim; icons reused from the
  existing icon library rather than hand-authoring new SVG paths.
- Who These Services Are For (Business Solutions): 10 tiles in a
  4-column grid stranded the last row (2 tiles) on the left. Switched
  `.tile-grid` from CSS Grid to flexbox with `justify-content: center`
  (same fix pattern as `.why-grid`/`.flip-grid`), so the short last row
  centers itself. Also fixed a specificity bug where `.section-head p`'s
  `margin: 0` was crushing the "These services are especially valuable
  for" eyebrow line up against the paragraph above it with no gap;
  added `.section-head .eyebrow` to restore its intended top margin.
- Business Solutions polish: removed the four narrative paragraphs
  from the hero (kept subheadline + buttons); added "Google Workspace
  Administration" to the Business IT Services checklist next to
  Microsoft 365 administration; swapped "Cybersecurity improvements"
  and "Managed IT services" in that same checklist; capped the
  Business Solution Categories card grid at a 920px max-width so it's
  centered instead of stretching edge-to-edge. Also fixed a real CSS
  specificity bug: Engagement Options' `.commitment` cards have white
  backgrounds sitting on the blue `.section-blue` section, and
  `.section-blue p` (white text) was tying in specificity with
  `.commitment p` (muted grey text) and winning on source order,
  making the descriptor paragraphs invisible (white on white). Added
  `.section-blue .commitment p { color: var(--slate); }` to fix it,
  matching the existing `.card` override pattern. Worth checking any
  future `.commitment`-in-`.section-blue` combination for the same
  issue (index.html and personal-technology.html's commitment cards
  are currently in white, non-blue sections, so unaffected).
- Removed the "Home" and "Contact" text links from the top nav menu
  (`.nav-menu`) across all 17 pages. The logo already links home, and
  the "Get Started" button already links to contact.html, so both
  links were redundant. Footer nav (`.footer-nav`) still has both,
  untouched, since the user's request was scoped to the top menu only.
- Built the Business Solutions overview page, following Personal
  Technology's layout: video hero (blue title, grey subheadline, 4
  narrative paragraphs), Business Technology Overview (photo + text,
  blue h2), Business Solution Categories (4 cards in a 2x2 grid — Business
  IT Services, Digital Presence, AI and Automation, Technology Consulting —
  each linking to its subpage), Who These Services Are For (10-tile grid),
  Engagement Options (5 cards) and Why Work With TechStratus? (6 cards, its
  existing "Why" pattern), closing CTA. One deliberate repeated white
  section (Why -> CTA) to keep the CTA contrasting against the always-blue
  footer, same as the precedent set on Senior Support. Restore point
  tagged: `business-solutions-before-build`.
- Personal Technology page: hero switched from the text-only gradient
  ("mini-hero") to the same looping video used everywhere else. "Personal
  Technology Support" (h1) is now blue via the shared `.hero-title-accent`
  class; "Patient and Practical" (subheadline) uses the shared `.hero-sub`
  default color (slate/grey), matching Senior/Family's subheadlines. Added
  a new small `.text-blue` utility and applied it to "Technology should
  work for you" in the intro section. Removed the now-unused
  `.mini-hero`/`.mini-hero-sub` CSS (no other page referenced them).
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
