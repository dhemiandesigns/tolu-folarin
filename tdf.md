# TDF — Betrayal Care by Tolu Folarin — Build Log

## Mandatory continuity rule

**Every person or AI agent who changes any part of this website must update
this `tdf.md` file in the same work session.** This includes changes to copy,
design, layout, assets, interactions, forms, analytics, configuration, GitHub,
Vercel, domains, DNS, or deployment settings. Do not consider a change
finished until the corresponding handoff note has been added here.

Each update must record:

- the date and a concise description of what changed;
- the files, services, or settings affected;
- important decisions, assumptions, and client instructions;
- verification performed and its result;
- anything incomplete, blocked, or requiring follow-up; and
- any new instructions the next person needs to continue safely.

Never write passwords, access tokens, verification codes, private keys, or
other secrets in this file. Commit and push the `tdf.md` update together with
the related website changes so the repository always contains the latest
handoff state.

## Project goal
High-conversion marketing website for Tolu Folarin's counselling practice
(infidelity / betrayal trauma / relationship therapy), built to receive paid
ad traffic. Primary conversion goals: (1) book a free 15-minute consultation,
(2) check insurance coverage (direct billing lead capture). Site must feel
calm, editorial, and trauma-informed — minimal copy, generous whitespace,
soft motion — not a typical "salesy" landing page.

## Source material
- `websirw.png` — client-approved hero mockup (teal / cream / peach palette).
- `tdf 2.png` — cutout portrait of Tolu (transparent background), copied to
  `assets/tolu-portrait.png` and reused in both the hero and About section.
- Full copy brief supplied by the user (see conversation) — based on a review
  of the live site at tolufolarin.ca and her Psychology Today profile.

## What's built (v1 — static site)
Plain HTML/CSS/JS, no build step, no framework, so any developer can pick it
up immediately.

```
index.html        — full single-page site, all sections in copy brief
css/style.css     — design system (CSS variables), layout, responsive rules
js/main.js        — scroll-reveal animation, mobile nav, coverage-form modal
assets/tolu-portrait.png — cutout portrait (hero + About)
```

### Sections implemented (in order)
1. Announcement bar — direct billing callout
2. Sticky header/nav (About, How I Help, Insurance, FAQs, Book CTA)
3. Hero — matches the approved mockup almost exactly (teal field, portrait
   right, peach primary CTA, pill badge, trust line)
4. "You may be here because…" — 3-path visitor identification cards
   (discovered betrayal / broke the trust / rebuilding together)
5. Insurance / direct billing conversion block with checklist + disclaimer
6. Specialized care section (EFT + EMDR bullet outcomes) — dark teal to
   break up the page rhythm
7. 3-step process ("Starting therapy can be simple")
8. About Tolu (credentials, trust points)
9. Testimonials (3 short quotes — placeholders, see below)
10. FAQ (accordion via native `<details>`, no JS needed)
11. Final CTA (dark teal, mirrors hero energy)
12. Footer

### Interactions
- Scroll-reveal fade/slide-up on all major blocks via `IntersectionObserver`
  (respects `prefers-reduced-motion`).
- "Check My Coverage" (hero, insurance section, final CTA) opens a modal with
  a short lead form: name, email, phone, insurance provider, therapy type,
  preferred contact method. **Deliberately does not ask for policy numbers**
  per the brief's privacy guidance.
- Form submit currently just swaps to a static success message client-side —
  **it is not wired to a CRM/email/intake endpoint yet.** See TODO below.
- Mobile hamburger nav below 980px.

## v2 update — verified against real sources (2026-09-09)
The client flagged that the original location/phone copy might misrepresent
the practice, and pointed at **tolufolarin.ca** as the source of truth. That
site is a half-built GoDaddy site (its browser tab literally still reads
"VOTE Tolu Folarin FOR RPSB TRUSTEE" — an old campaign site title left over
from a previous use of the domain), but its `/about` and `/contact` pages
have real, current content, and it links out to Tolu's verified Psychology
Today profile, which has the richest confirmed detail. Both were fetched
directly and cross-checked before writing anything down. Everything below
is sourced from those two places, not invented:

- **Locations**: In-person in **Calgary, AB** and **Edmonton, AB**; secure
  online sessions across **Alberta and Ontario** (per her Psychology Today
  "Practice at a Glance": Calgary AB T3C + Edmonton AB T5J, online across
  Alberta and Ontario). Earlier drafts guessed "Regina" from a garbled voice
  note — that did not check out against either real source, so it was
  removed everywhere (hero, FAQ, footer).
- **Phone**: (587) 324-7624 — confirmed as the "Betrayal Care" practice line
  on Psychology Today (matches what was already in the copy brief). Note:
  tolufolarin.ca's own contact form lists a different personal number,
  (639) 571-2516, and a personal email, tolu.folarintherapy@gmail.com —
  those were left out of the marketing site in favor of the practice line,
  but flag this discrepancy to Tolu in case she wants the personal
  email/line used for the "Contact" flow instead.
- **Booking**: real Calendly link wired up everywhere a "Book a
  Consultation" CTA appears: https://calendly.com/toluladefolarin (pulled
  from the "BOOK A SESSION" button on tolufolarin.ca's homepage).
- **Credentials**: Tolu Folarin, MSW, BSW, RSW. BSW from University of
  Regina (2019), MSW from University of Toronto (2024), in practice 7
  years — "Practising since 2019" trust point is accurate as written.
  Modalities: EFT + EMDR (kept as the headline pair for simplicity), though
  her full PT/about listing also mentions ART (Accelerated Resolution
  Therapy) and CBT-informed work — worth a mention if Tolu wants a fuller
  modalities list later.
- **Insurance**: added a real, representative accepted-provider line to the
  insurance section (Alberta Blue Cross, Canada Life, Manulife, Sun Life,
  Green Shield Canada, Desjardins, Equitable Life, iA Financial Group,
  Johnston Group, Medavie Blue Cross, "and more") — cross-referencing both
  her Psychology Today insurer list and tolufolarin.ca's longer list.
- **Testimonials**: replaced the placeholder client quotes (which were
  invented and risked misrepresenting the practice) with 3 real,
  attributed professional endorsements pulled from her public Psychology
  Today profile (17 endorsements listed there — Elliott Kemmet RSW, Joanna
  He Registered Provisional Psychologist, Rita Onwunali RSW were used). A
  small note under the section heading discloses these are colleague
  endorsements shared on Psychology Today, not client reviews — this
  matters for accuracy/compliance. **Still no real client testimonials
  exist anywhere public** — get permissioned ones from Tolu before this
  section should claim to represent clients.
- **Footer**: added real social links (Instagram @tolu_folarin, LinkedIn,
  Facebook) and made the phone number a clickable `tel:` link.
- **"Learn More About Tolu"** now links to her real Psychology Today
  profile instead of a dead `#` anchor.

## v3 update — conversion/layout pass (2026-09-09)
Client feedback: the page felt too wordy/"worthy" for someone in pain, wasn't
responsive well, the hero image/text balance was off vs. the reference
mockup, and NIHB/insurance (a major differentiator) needed more prominence.
Also: the homepage "About" teaser should stay brief — a fuller bio belongs
on a dedicated About page later — and the site must NOT list Tolu's other
(non-betrayal) counselling services, since Betrayal Care exists specifically
to give her a niche; that decision waits until a meeting with Tolu
identifies her highest-ticket offering to fold in.

- **Hero rebuilt for full-bleed image balance**: `.hero-media` is no longer
  a flex/grid column — it's now an absolutely-positioned element pinned to
  the right edge of the `.hero` section (`right:0`, full height), sized at
  46% width (40% under 1240px), so the portrait bleeds to the screen edge
  and fills the section height like the reference mockup. `.hero-copy` is
  a normal-flow column with `max-width: 600px` on the left. Below 980px it
  reverts to a simple stacked layout (image on top, static position) — see
  the `@media (max-width: 980px)` block in `css/style.css`.
- **Removed the redundant hero pill** ("NIHB-Approved · Direct Billing
  Available" badge) per follow-up feedback — it duplicated the announcement
  bar directly above it. The `.pill` CSS was deleted since nothing
  references it now.
- **NIHB/insurance emphasis increased**: the announcement bar now leads
  with "NIHB-approved · direct insurance billing available" in bold: this
  is the very first thing a visitor reads. The dedicated Insurance section
  is still the second section on the page (right after the "You may be
  here because…" identification cards), so the financial-friction objection
  gets addressed early, before any deeper pitch.
- **Copy trimmed throughout** — this was a working site copy for a page for
  people in acute distress, not a brochure. Cut: the hero's second
  sub-paragraph (kept only the one-line lede), the identify-card
  descriptions (down to short phrases), the insurance section's
  paragraph/insurer-list/disclaimer (shorter, sharper), the specialized-care
  section's two intro paragraphs merged into one line, and the About
  section's two-paragraph bio collapsed into one sentence (full bio belongs
  on a future dedicated About page, not this homepage teaser). CTA button
  labels shortened ("Book a Free 15-Minute Consultation" → "Book a Free
  Consultation") to reduce visual weight and give hero buttons room to sit
  on one line.
- **Responsiveness audited** at 375px (mobile), 769px (tablet), and 1400px
  (desktop) — hero, identify cards, insurance checklist, specialized
  section, process steps, mobile hamburger nav, and footer all confirmed
  working correctly at each size. No real bugs found; note for whoever
  continues this — this session's screenshot tool has a recurring
  compositing-lag quirk where a screenshot taken immediately after a JS
  scroll/DOM change renders blank/stale, even though the underlying DOM and
  computed styles are correct. Waiting ~1-2s before re-screenshotting (or
  checking computed styles directly) always resolved it. Don't mistake that
  for a real rendering bug in the site itself.
- **Confirmed**: the site does not and should not list Tolu's broader
  service catalogue (youth counselling, parenting/family counselling,
  perinatal/postpartum counselling, or the long general "areas of
  expertise" list like anxiety/depression/grief from her Psychology Today
  profile). Betrayal Care is intentionally narrow. Revisit this only after
  the planned meeting with Tolu identifies her highest-ticket service to
  potentially feature.

## v4 update — hero rebuild for bold image + real bug fix (2026-09-09)
Client sent a mobile reference screenshot (their brand guideline, not a
suggestion) showing the portrait as a bold, full-bleed banner between the
headline and body copy on mobile — not a small cutout floating in a sea of
teal, which is what v3's mobile hero looked like ("sitting in the void").
Direction given explicitly: "the use of image needs to feel bold — what
we're selling is the person, not just text."

- **Hero markup restructured** into three siblings inside `.hero`:
  `.hero-top` (headline), `.hero-media` (portrait), `.hero-bottom` (lede,
  CTAs, trust line). On desktop, `.hero-media` is absolutely positioned
  full-height against the right edge exactly as before — `.hero-top` and
  `.hero-bottom` stack normally in the left column since the absolutely
  positioned image doesn't affect their flow. On mobile (`≤980px`),
  `.hero-media` drops into normal flow **between** the headline and body
  copy, full-width, `object-fit: cover` at a generous fixed height
  (`clamp(360px, 82vw, 560px)`) — so it reads as a bold, edge-to-edge photo
  banner, not a floating cutout. This matches the reference exactly.
- **Real bug found and fixed**: putting a smaller `max-width` directly on
  an element that also has the `.container` class (which centers itself
  via `margin: 0 auto`) centers that narrower box in the middle of the
  section instead of keeping it left-aligned — this caused the hero
  headline and image to overlap at common desktop widths (confirmed via
  `getBoundingClientRect()`, not just a screenshot glitch). Fixed by
  keeping `.hero-top`/`.hero-bottom` at the standard container width and
  constraining line length on the text elements themselves (`.hero h1`,
  `.trust-line` get `max-width: 560px`, dialed to `460px` under 1240px)
  instead. Worth remembering for any future section that nests a narrower
  column inside `.container`.
- **Pill removed again**: it was reinstated this round to match the
  reference images (which do show it), then the client asked a second time
  to remove it — final call is **no pill in the hero**, the announcement
  bar above carries that message instead. The `.pill` CSS was deleted.
  Don't re-add it without an explicit ask, since this has flip-flopped
  twice now.
- Confirmed at 375px, and 1440px that there is no image/text overlap and
  the portrait reads as bold/dominant at both sizes.

### Note on this session's screenshot tool
Repeatedly, a screenshot taken immediately after a scroll, viewport resize,
or DOM change came back blank or showing stale content, even though
`getBoundingClientRect()` / `getComputedStyle()` confirmed the real DOM was
correct. Waiting ~1-2 seconds and retaking the screenshot always resolved
it. When something looks broken in a screenshot, verify with JS rects
before assuming it's a real layout bug — but the max-width/container
overlap bug above was real precisely because the JS rects (not just the
screenshot) showed the overlap.

## v5 update — hero layout correction, real bugs fixed (2026-09-09)
Client feedback: too much empty space, portrait too small/too low on
desktop, mobile cropped her hair, and mobile felt like the image was
"floating" in flat teal instead of landing at a section boundary. Treated
as a layout-correction pass — copy/typography/palette/asset untouched
except for cropping the asset's own transparent margins (see below).

### Asset change
`assets/tolu-portrait.png` had ~210px of fully transparent canvas above her
head (no transparent margin below — the chair already touched the bottom
edge). Auto-cropped to the tight content bounding box (+12px pad) with
Pillow, from 2006×2211 down to 1816×2013. This directly helps both
requirements: less dead space above her head, and a tighter fit against the
mobile background seam. Client also mentioned a replacement/second image is
coming for possible use on a future About page — not yet added.

### Desktop
Old model stretched `.hero-media` `top:0;bottom:0` to match a `.hero-bottom`
that had `padding-bottom: 260px` purely to reserve vertical space — exactly
the anti-pattern the client called out ("moving the image up alone won't
fix it if the container still reserves the original space"). Replaced with:
- `.hero` now sets `--media-h` (a clamped, viewport-relative height) and
  derives its own `min-height` from that *same* variable
  (`calc(var(--media-h) + 60px)`) — one source of truth, no space reserved
  separately from the image's actual size.
- `.hero-media` is `position: absolute; bottom: 0; right: 0; height: var(--media-h); width: auto;` — sized by height only, so width/proportions stay
  intrinsic (never stretched or squished), anchored to the bottom, and its
  height directly controls both her prominence and how close her head sits
  to the headline (no separate "top" positioning to fight with).
- Nav-to-headline clearance tightened from 56px to 36px padding-top.

### Mobile and tablet (shared rules, ≤980px — not just a shrunk desktop)
- `.hero-media` switches to normal flow, `width:100%; height:auto;`, image
  `object-fit:contain` — sized purely by the asset's own aspect ratio, so
  her full face and hair are mathematically guaranteed to never crop at any
  width in this range.
- `.hero-bottom` (lede, buttons, trust line) gets its own background,
  `var(--teal-700)`, starting immediately where `.hero-media` ends — the
  color seam lands exactly at the image's bottom edge with zero gap,
  "grounding" it at a section boundary instead of floating in the same flat
  teal as the headline above it.

### Two real bugs found and fixed (not screenshot artifacts — confirmed via
`getBoundingClientRect()`/`getComputedStyle()`)
1. **3-value padding shorthand silently zeroing horizontal gutters.**
   `padding: 36px 0 0` (intended as "top only") actually sets
   top/right/bottom/left = 36/0/0/0 — wiping out the `.container` class's
   own left/right padding on any element that carries both classes. Hit
   this twice (`.hero-top`/`.hero-bottom` on desktop, then again in their
   mobile overrides). Fixed by always using explicit `padding-top` /
   `padding-bottom` longhand when only touching one axis on a `.container`
   element — never the 2-3 value shorthand.
2. **Equal-specificity cascade collision.** A later, more general
   `@media (max-width: 600px) { .container { padding: 0 22px; } }` rule
   was clobbering the mobile hero's `padding-top`/`padding-bottom` (set on
   `.hero-bottom`, which also carries the `.container` class) purely
   because it appeared later in the file with equal specificity — nothing
   to do with `.hero-bottom` being "more specific" by name. Fixed by making
   that rule (and the base `.container` rule itself, proactively) use
   longhand `padding-left`/`padding-right` only, so it can never again
   silently reset an unrelated element's vertical padding just because it
   shares the `.container` class.
   **Lesson for future edits**: never mix `.container` with a second class
   that sets its own vertical padding unless every padding declaration
   touching either class uses longhand properties. Shorthand `padding: a b`
   (or `a b c`) always sets all four sides — there is no such thing as a
   "partial" padding shorthand.

Verified via `getBoundingClientRect()` (not just visual screenshots) at
1440px, 1200px, 1100px, 1000px, 960px (tablet-stacked), and 375px (mobile)
— no image/text overlap, no clipped face/hair, no horizontal scroll, and
the mobile color seam lands with a 0px gap once the scroll-reveal animation
settles (a `reveal` element mid-transition briefly shows a ~24px offset
from its `translateY` entrance animation — not a layout bug, confirmed by
re-checking after the transition completes).

## v6 update — second image used in About section (2026-09-09)
Client added a second asset, originally `assets/tdf about.png` (a
full-length standing portrait, transparent background, same shoot/outfit as
the seated hero photo) and asked where it landed. Used it exactly where
flagged as likely: the About section, replacing the reused seated hero
photo that was a placeholder there.

- Renamed to `assets/tolu-about-standing.png` (spaces in filenames are
  fragile in URLs/build tools) and auto-cropped its transparent margins
  with Pillow the same way as the hero asset (1024×1536 → tight bbox →
  382×1355 with a 10px pad) — same rationale as before: less dead space to
  fight with in layout math.
- This image is very tall and narrow (~0.28 aspect ratio) — a normal
  width-driven grid column would have forced it to some absurd height (a
  0.8fr column at desktop widths would have rendered it over 1500px tall).
  Rewrote `.about-media` to be height-driven instead
  (`height: clamp(480px, 44vw, 680px)` desktop, `clamp(380px, 78vw, 520px)`
  mobile), same technique as the hero fix from the previous round — size by
  the constrained axis, let the other axis stay intrinsic via
  `object-fit: contain` + `width: auto`.
- Dropped the old blush-card treatment (`border-radius` + background chip)
  that was designed for the previous square-ish seated-photo crop — a
  full-length standing cutout floats directly on the section background
  instead, the same way the hero photo floats on teal. Narrowed the
  `.about-inner` grid column from `0.8fr` to `minmax(200px, 300px)` to match
  the image's natural narrow footprint instead of leaving dead space beside
  it.
- Verified at ~1300px desktop and 375px mobile — natural proportions, no
  stretching, no excess dead space beside the image column.

## v7 update — desktop headline pushed down one line (2026-09-09)
Client request (desktop only): push the whole hero headline down so the
first line ("When trust breaks, you") starts where the second line
("don't have to face what") used to sit — i.e. shift the headline down by
exactly one line of its own text.

- Added `margin-top: 1.15em` to `.hero h1` (matches the site's global
  `h1,h2,h3 { line-height: 1.15 }`, so the shift is always exactly one
  line regardless of the headline's `clamp()`-driven font size at any
  desktop width). Reset to `margin-top: 0` inside the
  `@media (max-width: 980px)` block so mobile/tablet are unaffected, per
  "on the desktop version" in the request.
- Verified via `getBoundingClientRect()` at 1440px: h1 top moved from
  186.5px to 245.4px (a 58.88px shift = the computed line-height at that
  width, confirmed via `getComputedStyle`), with no overlap into the
  portrait or overflow past the hero's bottom edge (trust-line/location
  content still ends well before `.hero`'s own bottom). Confirmed
  `margin-top: 0px` still holds at 375px (mobile) — no regression there.

### Git / deployment note
Earlier in this session, `git push origin main` failed:
```
remote: Permission to dhemiandesigns/tolu-folarin.git denied to cstlelivn.
```
The osxkeychain-cached GitHub credential on this machine belonged to a
different account (`cstlelivn`) without write access to
`dhemiandesigns/tolu-folarin`. That got resolved outside this change (the
`463996e` "Document deployment and handoff workflow" commit landed on
`origin/main` in the meantime, confirming push access now works). The v6
(About portrait) and v7 (headline push) commits above were made on a
throwaway local branch while push was still blocked and have since been
folded onto `main` on top of `463996e` and pushed — see commit history for
the exact SHAs.

## v8 update — reverted About section back to seated portrait (2026-09-09)
Client feedback: the full-length standing portrait (`tolu-about-standing.png`)
didn't look good on tablet/mobile in the About section. Decision: pull it
back out of the About section entirely for now — "hold it, we'll find
another place to use it" — rather than try to fix its sizing there further.

- `index.html`: About section image reverted from
  `assets/tolu-about-standing.png` back to `assets/tolu-portrait.png` (the
  seated photo, same one used in the hero).
- `css/style.css`: `.about-inner`/`.about-media` reverted to the pre-v6
  treatment — `grid-template-columns: 0.8fr 1.2fr`, `align-items: center`,
  and the rounded blush-card image treatment
  (`border-radius: var(--radius-lg); background: var(--blush-200);`) —
  undoing the height-driven/no-card sizing that v6 introduced specifically
  for the standing portrait's tall proportions. Mobile override reverted
  from the `height: clamp(...)` rule back to `max-width: 320px; margin: 0
  auto;`.
- **`assets/tolu-about-standing.png` is kept in the repo, just unused** —
  client wants to place it elsewhere later (a full-length shot is a strong
  candidate for a future dedicated About page, or a testimonials/trust
  section). Don't delete this asset.
- Verified at ~1300px desktop and ~800px tablet: About section is back to
  the balanced two-column card layout with no stretching or cropping
  issues.

## v9 update — site expanded to multiple pages (2026-09-09)
Client direction: Betrayal Care stays the flagship/homepage specialty (no
change there), but Tolu also offers the full range of services already
listed on tolufolarin.ca (couples/infidelity, individual, parenting &
family, youth, perinatal & postpartum counselling) plus separate consulting
work (community engagement/outreach strategy, grant writing/funding
strategy, staff training, social program design, policy development &
advocacy — she ran for trustee on the Regina Public Schools Board,
Subdivision 4, in 2024). The insurance section needed to become a real
landing page with the full accepted-insurer list in a multi-column layout
instead of one long column. Asked first whether "Betrayal Care" (possibly
already used by a partner company) needed to change — client chose to
**keep the name as-is for now**, so no renaming was done anywhere.

**Site is now multi-page** (previously a single `index.html` with anchors):
- `about.html` — full bio, pulled from tolufolarin.ca/about (re-fetched
  live to confirm current wording): "Can we actually recover from this?"
  narrative, credentials (BSW University of Regina, MSW University of
  Toronto), approach (EFT + EMDR-informed + ART + CBT), and a specialties/
  expertise grid (top specialties, betrayal-focused expertise, broader
  clinical support).
- `services.html` — Betrayal Care featured as the flagship offering in a
  dark highlighted card (links back to `index.html`), followed by a grid of
  the other five services (couples/relationship, individual, parenting &
  family, youth, perinatal & postpartum), each with its own booking link.
- `insurance.html` — dedicated landing page: NIHB/direct-billing checklist,
  then the full 29-provider accepted-insurer list in a responsive grid
  (`.insurer-grid`: 4 columns desktop, 2 columns tablet/mobile) instead of
  one long list, plus the coverage-check modal (reused from the homepage).
- `consulting.html` — kept deliberately low-key per "don't want it to
  overshadow the counselling": **not in the main nav**, linked only from
  the footer (`Consulting`) on every page. Covers the four consulting
  service areas plus a policy/advocacy callout (Regina Public Schools Board
  run, Zao Innovation Hub link).

**Second portrait now used**: `assets/tolu-about-standing.png` (pulled from
the About section back in v8 for looking bad on tablet/mobile there) is now
used in `consulting.html`'s intro band — a two-column layout pairing the
copy with the standing portrait, sized the same way as the hero fix
(`height: clamp(...)`, `object-fit: contain`, `width: auto` — intrinsic
proportions, no cropping) and switching to a stacked, centered layout with
`order: -1` (image above text) under 980px. Chosen because a full-length
formal shot suits a "consulting" context better than the tighter About-page
card layout it didn't work in.

**Homepage (`index.html`) updates**:
- Nav simplified to About / Services / Insurance / FAQs (dropped the
  "How I Help" nav item now that Services covers that ground more fully;
  the `#how-i-help` anchor and its content are untouched — the "Find the
  Right Support" button still scrolls to it).
- "Learn More About Tolu" now links to `about.html` instead of sending
  traffic out to Psychology Today.
- Insurance section's insurer-list line now links to `insurance.html`
  ("see the full list") instead of just naming a few providers with no
  follow-through.
- Footer links expanded: About, Services, Insurance and Fees, Consulting,
  Book a Consultation, Privacy Policy, Terms — same footer copied onto
  every new page for consistency.

**New shared CSS** (in `css/style.css`, before the Responsive section):
`.page-intro` (shared light-hero band for interior pages), `.service-
featured` / `.service-grid` / `.service-card` (Services page), `.insurer-
grid` (Insurance page), `.consulting-grid` / `.consulting-advocacy` /
`.consulting-intro-*` (Consulting page). Responsive collapse rules added
for all of these in the existing `@media (max-width: 980px)` and
`(max-width: 600px)` blocks — no new breakpoints introduced.

Verified: all five pages return HTTP 200 locally, nav/footer links resolve
correctly across pages, the coverage-check modal works from both
`index.html` and the new `insurance.html`, and the consulting intro image
was checked at ~1300px (two-column, no overlap) and mobile/tablet pane
width (stacked, full figure visible, no cropping).

### Still open from this round
- An extra untracked image, currently `assets/tolu-portrait 2.png` (this
  filename has already changed once this session — it briefly appeared as
  `assets/tdf 2Jjpg.jpg` — so don't be surprised if it changes again),
  showed up in the assets folder mid-session. It has not been reviewed or
  used anywhere yet. Left uncommitted/untracked intentionally until someone
  looks at it and decides where (if anywhere) it belongs.
- Consulting page CTA uses a plain `mailto:tolu.folarintherapy@gmail.com`
  link (no form) — fine for now given it's a low-traffic page, but revisit
  if consulting inquiries pick up.
- The Services page's five secondary service cards (couples, individual,
  family, youth, perinatal) all use generic descriptive copy written for
  this build, not pulled from any client-approved source — worth a
  copy-accuracy pass with Tolu before this goes live, the way the
  Betrayal Care homepage copy already was.

## Still placeholder / needs Tolu's input
- **"Privacy Policy" / "Terms"** footer links are still `#` — no dedicated
  pages built.
- The coverage-check modal still only shows a client-side success message —
  not wired to a real inbox/CRM yet (see below).
- Old tolufolarin.ca's stray "Vote Tolu Folarin for RPSB Trustee" browser-tab
  title issue does not apply to this build — it ships its own clean
  `<title>` and meta description from scratch.

## Not yet built (intentionally out of scope for v1)
- Backend / form submission wiring (email notification, CRM, or scheduling
  API integration for the coverage-check modal).
- Dedicated "How I Help," "About," "Insurance & Fees," "Privacy," and
  "Terms" sub-pages — everything currently lives as anchors on one page,
  per the brief's minimalism direction. Revisit if Tolu wants deeper pages
  for SEO (e.g. a dedicated infidelity-therapy landing page for ad traffic
  matching).
- Analytics / conversion tracking (GA4, Meta Pixel, conversion events on
  button clicks) — needed before running paid ads, since the stated goal is
  ad-driven lead capture.
- A/B test variants of the hero headline/CTA copy.

## Design system reference (for whoever continues this)
Colors (see `:root` in `css/style.css`):
- `--teal-900 / --teal-800 / --teal-700` — primary brand teal (hero, dark
  sections, header/footer)
- `--cream-050 / --cream-100` — page background + light text on dark teal
- `--blush-200 / --blush-300` — soft dusty-pink section backgrounds (used to
  break up rhythm between teal/cream sections, taken directly from the
  mockup's bottom band)
- `--peach-400 / --peach-500` — primary CTA color + accent dots/checks

Typography: `Playfair Display` (serif, headings) + `Inter` (sans, body/UI)
via Google Fonts. (v1 used Fraunces; swapped to Playfair Display per Tolu's
feedback that Fraunces read as too playful for the subject matter.)

Primary brand teal is pinned to Tolu's exact requested hex, `#006075`
(`--teal-800`), with `--teal-900` (#004a56) and `--teal-700` (#0d7690) as
manually-tuned darker/lighter companions for depth and hover states.

## How to preview locally
No build step required — just open `index.html` in a browser, or serve the
folder with any static server, e.g.:

```bash
cd "/Users/demidhemian/Documents/STUDIO/TDF"
python3 -m http.server 8080
```

Then visit `http://localhost:8080`.

## GitHub and Vercel deployment handoff (2026-09-09)

### Canonical repository

- GitHub owner: `dhemiandesigns` (DHEMIAN agency account)
- Repository: `https://github.com/dhemiandesigns/tolu-folarin`
- Visibility: public
- Production branch: `main`
- Local remote: `origin`
- Initial website commit: `1c15687` (`Initial Tolu Folarin website`)

This GitHub repository is the source of truth. Make changes in this working
copy, verify them, update this file, commit both the site changes and handoff
notes, and push to `origin/main`.

### Vercel production deployment

- Vercel scope/team: `dhemian` (DHEMIAN)
- Vercel project: `tolu-folarin`
- Project dashboard: `https://vercel.com/dhemian/tolu-folarin`
- Stable production URL: `https://tolu-folarin.vercel.app`
- Framework: none; this is a plain static HTML/CSS/JavaScript site
- Build step: none required
- Output directory: repository root (`.`)
- Root directory: repository root

The production URL was deployed and verified on 2026-09-09 with an HTTP 200
response. The live page title was also confirmed in Chrome as “Betrayal Care
by Tolu Folarin | Infidelity & Betrayal Trauma Therapy.”

The GitHub repository is connected to the Vercel project. A push to `main`
creates a production deployment automatically. Pull-request and non-production
branch changes may create preview deployments. After every push, confirm the
Vercel deployment succeeds and visually check the stable production URL before
calling the work complete.

Vercel's GitHub App currently has access only to the
`dhemiandesigns/tolu-folarin` repository. Do not broaden that access without an
explicit DHEMIAN decision.

The local folder is linked to this Vercel project through the ignored
`.vercel/` directory. Do not commit `.vercel/`, Vercel credentials, or other
machine-specific authentication files.

### Account and ownership decisions

- DHEMIAN is the agency and owns/manages the GitHub repository and Vercel
  project.
- Do not create a separate Vercel account for Tolu as part of the current
  workflow. A client account is only needed later if DHEMIAN explicitly decides
  to transfer ownership.
- Other DHEMIAN and client websites should be separate Vercel projects, each
  connected to its own Git repository and respective domain.
- The current Vercel workspace is on the Hobby plan. It technically supports up
  to 200 projects and 50 domains per project, but Vercel describes Hobby as
  personal/non-commercial. DHEMIAN should use Pro for ongoing commercial client
  hosting.

### Domain status

No custom domain has been connected yet. The agreed next session task is to
connect the client's primary domain after confirming the exact domain and
current DNS provider/settings. Until that is completed and verified, use
`https://tolu-folarin.vercel.app` as the canonical live link. Do not change DNS
records without first inspecting the existing records and confirming the exact
domain target.

### Standard continuation workflow

1. Run `git status` before editing and preserve unrelated user changes.
2. Pull or otherwise confirm `main` is current before starting new work.
3. Make and locally verify the requested website change.
4. Update the relevant existing section of `tdf.md` or add a new dated update.
5. Review `git diff`, commit the website and `tdf.md` changes together, and push
   to `origin/main`.
6. Wait for the connected Vercel production deployment to finish.
7. Verify `https://tolu-folarin.vercel.app` loads successfully and visually
   inspect the changed area at relevant desktop and mobile sizes.
8. Record deployment or verification problems in `tdf.md` before handing off.

If a change should not go live immediately, work on a separate branch and use a
Vercel preview deployment; do not merge or push that work to `main` until it is
approved for production.

## Next steps (suggested priority order)
1. Get Tolu's sign-off on copy edits (if any) and confirmed location/phone.
2. Choose and wire up a real scheduling tool for all "Book a Consultation"
   CTAs.
3. Wire the coverage-check modal to a real destination (email service, CRM,
   or intake form provider) instead of the client-side stub in `main.js`.
4. Swap placeholder testimonials for real, permissioned client quotes.
5. Add analytics + conversion tracking before launching paid ads.
6. Mobile QA pass on real devices (this was built and reasoned about
   responsively, but not yet tested on physical hardware).
