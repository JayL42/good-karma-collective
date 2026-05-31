# Good Karma Collective — Project Log

Append-only action log for this project. Follows the workspace `log.md` action vocabulary: `ingest · query · lint · update · file-back · cleanup · init · link · scope-change · dedupe · correction`.

Scope: `project: good-karma-collective` / `context_domain: personal`.

---

## [2026-04-24] init | Project scaffolded — README, CLAUDE.md, source-artifacts/brief.md, outputs/ tree

Kickoff. Seeded from handoff brief at `assets/good-karma-collective-claude-brief.md` (canonical copy preserved; working copy at `source-artifacts/brief.md`). Project-local CLAUDE.md establishes `context_domain: personal` — loads workspace filing discipline, explicitly excludes Returnalyze shared context, TPx plans, and Returnalyze-scoped skills. GitHub connector flagged as anticipated tooling for the code phase; not yet installed.

Pre-kickoff state: no design direction, site structure, or copy decisions. Bethany runs design/copy exploration in a separate Claude chat seeded from the brief; this workspace context handles technical/hosting/deploy concerns.

## [2026-05-31] file-back | outputs/design/GoodKarmaCollective WebsiteBrief.md — complete design + copy brief from Bethany

Bethany's parallel Claude chat produced a finalized brief covering: tagline ("Wellness for Body, Mind & Life"), brand palette (deep teal #1a5c56 / gold #c9a84c / warm cream BG), 5-page site structure (Home / About / Massage Services / Health Coaching / Book Now), full approved copy for every page, and pricing tables for all 6 massage services + 3 coaching package tiers. Outstanding: final pricing review, policies confirmation, photos, MassageBook gift cert setup verification. Project transitions from pre-kickoff to design-approved, build-ready.

## [2026-05-31] correction | Booking platform: Vagaro → MassageBook — propagated across README.md, CLAUDE.md, and brief frontmatter

Original handoff brief listed Vagaro as the booking platform. Bethany confirmed MassageBook (paired with Square reader for in-person payments) when filing the design brief. MassageBook URL: https://www.massagebook.com/biz/good-karma-collective. Gift certificates also routed through MassageBook. Note: MassageBook's *own* site builder doesn't allow custom code, which reinforces the original "host elsewhere" decision (Netlify). Booking integration on our site is either an embedded widget or a "Book Now" link-out — final choice pending the code phase.

## [2026-05-31] update | source-artifacts/brief.md + /assets/good-karma-collective-claude-brief.md marked superseded

Both handoff brief copies (project-local + canonical /assets/) annotated with status: superseded, pointer to the new design brief, and the known-inaccuracies list (Vagaro→MassageBook, phone TBD→confirmed). Bodies preserved unedited as historical record. Going forward, outputs/design/GoodKarmaCollective WebsiteBrief.md is the authoritative spec.

## [2026-05-31] file-back | outputs/specs/2026-05-31-booking-integration.md — MassageBook widget options + hybrid integration decision

Spec captures the three MassageBook widget flavors (booking button link-out, booking iframe embed, reviews button/page, gift cert button) with literal snippets from MB's Website Integration screen. Decided: hybrid — branded link-out "Book Now" buttons on Home/About/Services pages, full iframe embed on the dedicated Book Now page, same shape for gift certs. Flagged blockers: MB's button PNGs are served over http:// (mixed-content blocker on HTTPS Netlify — build our own buttons); URL slug duality (/biz/ vs /therapists/ — verify pre-launch); iframe height is fixed 1000px (mobile responsiveness test needed); no brand theming exposed in widgets (wrap iframe in a styled container). Open items captured at the end of the spec.

## [2026-05-31] update | URL slug confirmed, Google links + asset inventory added, IMG_1051 ext fix

Booking spec: `/biz/good-karma-collective` confirmed as a 301 redirect to `/therapists/good-karma-collective` — open item closed. README: added External Profiles section with Google Business Profile URL (https://share.google/3BNZRZ391JrKIH8xJ) and Google leave-a-review link (https://g.page/r/CZ2MSft7QnSpEBM/review). README: added Assets inventory section listing the logo SVG (with teal background rect that can be removed for transparent variants), IMG_1051.PNG (Bethany portrait), and four interior/storefront jpegs (need categorization + responsive resizing — raw files are 2–4 MB). Design brief: IMG_1051.jpg → IMG_1051.PNG ext correction.

## [2026-05-31] init | git repo initialized at projects/good-karma-collective/

`git init -b main` + `.gitignore` (macOS, editor, node, build, env, netlify). Matches workspace convention — whole project folder is the repo. No commits made from this session; sandbox lacks Jay's git author identity and GitHub credentials. Repo will be private — folder contains internal process notes (CLAUDE.md exclusion lists, log entries about Bethany's separate chat) that aren't for public consumption. GH remote creation + first push pending Jay's terminal:

```bash
cd ~/Development/projects/good-karma-collective
git add -A
git commit -m "Initial scaffold: brief, design output, booking spec, project meta"
# With gh CLI (preferred):
gh repo create good-karma-collective --private --source=. --push
# Or via github.com web UI: create empty private repo named "good-karma-collective" (do NOT init README/license), then:
# git remote add origin git@github.com:jayl42/good-karma-collective.git
# git push -u origin main
```

## [2026-05-31] update | Repo pushed to github.com/JayL42/good-karma-collective (private)

First commit `683331b` — 13 files, 3215 insertions, ~13.35 MiB. `main` branch tracking `origin/main`. Note for future cleanup: raw photo files (~13 MiB across 4 jpegs + IMG_1051.PNG) currently committed to the repo. Working call for now since the deployable site will need them anyway; once we have an optimized-assets pipeline (responsive resizing for web), revisit whether to keep raw photos in the repo or move them to git-lfs / out-of-repo storage. Commented hooks for raw-photo exclusion already in `.gitignore`.

## [2026-05-31] file-back | index.html + styles.css — Home page mockup v1 (plain HTML+CSS)

First visual mockup. Plain HTML+CSS per stack decision. Home page only per scope decision. Brand tokens land as CSS custom properties (teal-900/700/500, gold-600/500/200, cream/paper, plus terracotta/sage/amber accents reserved for later sections). Typography: Playfair Display (serif heads) + Inter (body) via Google Fonts CDN. No images in v1 — typographic hero, type-driven service cards, "" decorative quote mark in vision section — lets Bethany react to color + type + rhythm before we add photos. Sections: sticky header w/ brand circle mark "GKC" placeholder + nav + Book Now CTA chip; hero (eyebrow / headline / lede / dual CTA / tagline); vision quote on deep-teal block w/ ghosted curly quote; two service cards on light bg w/ gold accent dots, hover lift, bordered detail rows; closing CTA; full footer (brand block / visit / book / explore / copyright). Booking links target the actual MassageBook URL pattern from the integration spec, including `?src=external` attribution param.

Open items for v2 once Bethany reacts: swap "GKC" circle for the real logo (need transparent-bg variant from the SVG — strip the `rgb(3,75,90)` rect); pick which photo lands in the hero vs. about-page-feature vs. service-page background; categorize IMG_2900/2921/3060/3063 (interior vs. storefront); validate type scale on real content with prices/long copy on services + coaching pages.

## [2026-05-31] update | Home page mockup v2 — logo integrated, color vibrancy bumped, tagline scaled

Per Jay reaction to v1: (1) Integrated the horizontal logo lockup (tree + stylized wordmark) — `assets/logo-small.svg` is the small SVG with the teal background rect stripped (transparent variant for use on the cream header). Header `<span class="brand-mark">GKC</span>` placeholder + brand name span replaced with a single `<img class="brand-logo">`. (2) Color tokens bumped for vibrancy: `--teal-700` #1a5c56 → #0e6e60 (more chroma); `--gold-500` #c9a84c → #d4a932 (richer); `--teal-900` deepened to #0a3631; cream slightly warmer to #faf4e3. (3) Hero tagline ("Wellness for Body, Mind & Life") scaled from 1rem ink-faint → clamp(1.35rem, 2.2vw, 1.7rem) in teal-900 with thin gold rules flanking it as ornament. (4) Section-title underline upgraded from 60×2 solid gold → 80×3 gold-700/300/700 horizontal gradient. The brief's baseline #1a5c56 / #c9a84c are preserved in comments so we can revert if Bethany prefers the original spec.

## [2026-05-31] update | Home page mockup v3 — golden bg + "more joyful" pass

Combined two pieces of feedback: (1) Jay — try `#ffd20094` for the primary BG and shift/scale the logo for optical balance. (2) Bethany — needs to be more joyful, less serene.

**Bg**: `--cream` token swapped to `#ffd20094` (semi-transparent golden over the white html root — renders as a warm golden cream ~`#ffe56b`). `--paper` warmed to `#fffaea` so service cards harmonize with the new ground. Sticky header gets a translucent golden cream backdrop (`rgba(255, 234, 130, 0.85)`) instead of the old cream alpha.

**Accent rebalance** for the new bg (gold-on-gold disappears): added `--accent-warm` (#b85a30 deeper terracotta) for type accents and `--accent-rule` (#c97a4a) for hairlines/ornaments. Swapped hero-eyebrow, service-card-eyebrow, and closing-eyebrow from gold-600 → accent-warm. Service-card hover border goes from translucent gold → terracotta. Gold is preserved on the dark sections (vision + footer) where contrast still works.

**Logo balance**: `.brand-logo` height 44→62px, max-width 240→320px, plus `transform: translateY(-3px) scale(1.04)` with `transform-origin: left center` — the small SVG's tree element sits low in its bounding box because of a lightweight top circle. The Y nudge + slight scale visually centers it without modifying the SVG geometry. Surgical SVG-level rebalance (inline + per-group transform) is a follow-up if the optical fix isn't enough.

**"More joyful" treatments**:
- Vision section bg lightened from `--teal-900` to `--teal-700` with warm gold + terracotta radial-gradient washes — less monolithic-contemplative, more inviting. Doubled the giant curly-quote ornament's opacity (0.08 → 0.18) and added a small `✦` flourish in the lower-right.
- Hero eyebrow ("Welcome home.") scaled from 1.15rem → `clamp(1.2rem, 2vw, 1.5rem)` in terracotta — pops as a warm invitation.
- Hero-tagline rules: thin gold bars replaced with `✦` star ornaments in terracotta — playful instead of architectural.
- Section-title underline: solid gold gradient bar replaced with a `✦ · ✦ · ✦` typographic ornament in terracotta — looser and more decorative.
- Closing CTA: warm radial gradients (terracotta from bottom, gold from top) over the golden cream — feels celebratory. Lone `✦` ornament at the top of the section as a section opener.
- Service card hover lift bumped from -3px to -4px with a slightly stronger shadow — a touch more bounce.

Brand identity drift to flag for Bethany: original brief was teal + gold + cream. v3 introduces terracotta as a secondary accent (only on light sections). The brief's "leaf accent tones: terracotta, sage, amber for subtle pops" is explicit permission for terracotta — so we're inside the brief, just leaning into it. Easy to dial back if it reads as too warm/golden.

## [2026-05-31] update | Home page mockup v3.5 — soft bg + cream header + vibrant teal + larger logo

Targeted feedback from Jay (with Bethany's mockup screenshot for reference) — v3 went too saturated, dial back.

**Bg**: `--cream` `#ffd20094` → `#fff6ce4a` — much softer yellow wash (alpha drops from 0.58 to 0.29). Reads as a barely-warm cream instead of full golden. The "joy" of v3 was overcooked; v3.5 gets warmth from sections + ornaments, not the body.

**Header restored to cream**: new `--header-cream` token (`#faf4e3` — v2's cream) for the sticky header background. Solid (not translucent) so it contrasts cleanly against the soft yellow body. Removed the translucent-gold backdrop from v3.

**Teal shift to `#137466`** for primary buttons + dark sections — matches Bethany's reference exactly. `--teal-700` now `#137466` (was `#0e6e60`), `--teal-900` set to `#0d5a4e` (slight depth for footer). Button hover stays slightly deeper for visual feedback. Text-on-teal contrast (`--paper` body, `--gold-200` highlights) unchanged — both pop well on `#137466`.

**Hero eyebrow contrast**: `--accent-warm` `#b85a30` → `#9c4824` — deeper terracotta for the "Welcome home." line. Reads with more bite on the paler bg.

**Logo push**: height 62→80, max-width 320→380, transform translateY(-6) scale(1.1) (was -3/1.04). The tree now visually leads the wordmark and bleeds up slightly into the header's top padding — net effect is the tree appearing larger AND set higher than the wordmark baseline, optically correcting the SVG's low-sitting tree. Mobile-scaled proportionally (height 56, max-w 260, same transform ratios). If the optical fix still isn't enough, next step is the surgical SVG fix: inline the logo as `<svg>` and apply a transform to the tree's path group specifically — needs identifying which paths form the tree (probably by X-bound clustering since the SVG has no per-element IDs).

Closing CTA `::before` ✦ star kept — not flagged, can drop if it reads as one ornament too many.

## [2026-05-31] update | Home page mockup v4 — new wellness palette + logo CSS reverted

Bethany sourced a 5-color wellness palette (Deep Teal #0E6E7F · Brushed Gold #C7A64A · Warm Ivory #F7F4EA · Soft Sage #A8C9B5 · Charcoal #353335). Jay also dropped in a refreshed `Good Karma Logo Small.svg` that self-corrects the tree positioning — no more CSS optical fix needed. Mandate: swap palette, don't change the design.

**Logo**: stripped the new SVG's bg rect → `assets/logo-small.svg` (same procedure). `.brand-logo` reverted to baseline: height 44px, max-width 240px, no transform. v3/v3.5 scale + translateY transforms removed. Mobile: 36px height. SVG now does its own balance work.

**Palette swap** (token-level — visual structure untouched):
- Body bg `--cream` → `#f7f4ea` (Warm Ivory, solid — replaces the v3.5 soft yellow wash)
- Header bg `--header-cream` → `#f1ecdf` (subtle differentiation from body)
- Card bg `--paper` → `#ffffff` (clean white pops against ivory)
- Body text `--ink` → `#353335` (Charcoal)
- Primary teal `--teal-700` → `#0e6e7f` (Deep Teal — was `#137466`)
- Primary gold `--gold-500` → `#c7a64a` (Brushed Gold — was `#d4a932`)
- Added `--sage-300/500/700` tokens + `--charcoal/-80` tokens for future use
- Removed `--accent-warm` (deep terracotta) + `--accent-rule` (terracotta) tokens

**Accent rebalance**: every `var(--accent-warm)` (hero/service-card/closing eyebrows + section-title ornament + closing-cta ✦) → `var(--gold-600)`. Every `var(--accent-rule)` (hero tagline stars + service-card hover border) → `var(--gold-500)`. The terracotta radial-gradient stops in vision section and closing-cta were swapped to Soft Sage rgba — gives those sections a "natural, grounding" wash instead of warm terracotta, matching the palette's intent.

Net effect: same layout, same ornament structure, same sections — just the wellness palette throughout. Per Jay's note on the reference site he attached: "use the palette, don't change the design — example is too busy." No new components or busy patterns introduced.

Charcoal currently appears only as body text (`--ink`). If Bethany wants Charcoal more present as a structural color (e.g., footer bg), easy swap — footer is currently `var(--teal-900)` = `#084a55`. Sage similarly is only present as gradient washes; available as `--sage-500` for any spot that wants a sage chip/bg.

## [2026-05-31] update | Home page mockup v4.1 — sage surfaced, header contrast, logo source fixed

Three things landed this pass:

**Logo source fix**: Jay had placed the previous "updated" Good Karma Logo Small.svg in the wrong folder — the source under `outputs/design/` hadn't actually changed until now. Confirmed the new file is in place (2026-05-31 20:26, 307,913 bytes) and structurally different from the older one: the new SVG has no leading teal-bg rect to strip, just `<g id="Good-Karma-Coll---Drop">` at line 4. `assets/logo-small.svg` regenerated as a clean copy (no sed). Tags balanced (650 open `<g>`, 650 close). Earlier blind sed run had broken the XML — that mistake is the artifact you'd have seen if you tested before this update. Also filed: `outputs/design/color palate.png` (1.9 MB) — the ChatGPT palette reference image, preserved for posterity.

**Header contrast**: `--header-cream` `#f1ecdf` (a hair off-cream — invisible against the Warm Ivory body) → renamed to `--header-bg` `#dde9e0` light sage. Sticky header now reads as a clearly defined band against the body. Border-bottom switched to sage-tinted (`rgba(108, 157, 126, 0.30)`) so the band's edge is harmonized with the sage fill rather than ghosted teal.

**Sage surfaced**: previously sage existed only as low-opacity radial-gradient stops in the vision + closing-cta sections (0.18 / 0.22 alpha) and was effectively invisible. Now sage shows up in three legible places:

1. **Header band** — sage fill, sage-tinted border bottom
2. **Service card hover** — border swaps gold → sage-700 (`#6c9d7e`), card bg gets a subtle bottom-up sage wash (`rgba(168, 201, 181, 0.18)`) so hovering feels like the card greens slightly. Shadow tinted teal instead of teal-900 for hue consistency.
3. **Radial washes bumped** — vision section sage stop 0.18 → 0.32, closing-cta sage stop 0.22 → 0.38. Both noticeably visible now.

Net: sage is present in the header (constant), the service-card hover (interactive), and the soft section washes (atmospheric). Three different roles, none overpowering — matches "subtle pops" from the original brief while making the palette actually use all 5 colors.

Charcoal still appears only as body text (`--ink`). If Bethany wants Charcoal more present too, footer is the obvious candidate (currently `--teal-900` `#084a55`).

## [2026-05-31] update | Logo dimensions bumped per Jay dev-tools sizing — 44→66px / 240→340px max

Sized to Jay's tested values from Chrome inspector. Mobile breakpoint scaled proportionally: 36→54 / 180→260. With the new self-balanced SVG, pure dimensional scale is enough — no transforms.

## [2026-05-31] file-back | index2.html + assets/logo-large.svg — ghosted-tree backdrop variant

index2.html is a parallel mockup for Bethany comparison — same content as index.html (so the v4.1 baseline is preserved for show-and-tell) plus a fixed, ghosted tree visible behind the hero. `assets/logo-large.svg` was stripped from `outputs/design/Good Karma Logo.svg` (had the same leading teal bg rect at lines 4-6 as the original small logo).

**Implementation**:
- New `<div class="tree-backdrop">` as the first child of body, holding the large logo `<img>`.
- Scoped `<style>` block in `<head>` (doesn't touch shared styles.css — index.html is unaffected).
- `.tree-backdrop`: position fixed inset 0, z-index 0, pointer-events none, image opacity 0.18, `clip-path: inset(0 0 38% 0)` to hide the wordmark portion of the SVG (only the tree shows). `transform: translateY(2vh)` nudges the trunk down so it doesn't crowd the header.
- `.site-header`, `main`, `.site-footer` get `position: relative; z-index: 2` so all real content stacks above the backdrop.
- `.hero` background overridden to transparent so the tree shows through it. Hero's warm radial-gradient glow preserved as a `::before` pseudo-element so we don't lose v4 atmosphere.
- Vision section + footer keep their solid bgs → cover the fixed tree once user scrolls past. Effect: tree visible while reading the hero; recedes behind opaque sections during deeper scroll; reappears if user scrolls back up.

Open knob if Bethany wants more/less: tweak `.tree-backdrop img { opacity }` (0.18 currently) and `width` (`min(720px, 82vw)` currently). Clip-path inset can be reduced to 0 to show the wordmark too (currently 38% to hide it).

## [2026-05-31] update | index2 tree backdrop — pinned strictly to viewport center, no scroll drift

Jay reported the tree shifted slightly on scroll before hitting its limit. Root cause: my v1 backdrop used `display: grid; place-items: center` + `transform: translateY(2vh)` on the img — the 2vh nudge recomputed when the viewport height changed (URL bar showing/hiding on mobile, elastic-bounce on macOS Safari overscroll), and grid placement is sensitive to wrapper-size shifts.

Fix: switched to absolute centering inside the fixed wrapper — `position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%)`. No vh-based motion, no grid recalc. Wrapper goes back to plain `top: 0; left: 0; width: 100%; height: 100%` (semantically identical to `inset: 0` but more obvious about what's happening). Tree now strictly pinned to viewport center across scroll, resize, and macOS rubber-band.

## [2026-05-31] update | index2 promoted to index.html + service-card stretched-link

Tree-backdrop variant won the comparison — index.html now contains what index2.html was (same 8662-byte file). Variant-specific styles still live in an inline `<style>` block inside index.html since they're tightly coupled to the tree-backdrop div; the broader page styles stay in styles.css. Title corrected back to the production "Wellness for Body, Mind & Life" (had carried over from the variant). **Action for Jay**: sandbox can't unlink files; run `rm index2.html` in your terminal to clean up the now-redundant copy.

**Stretched-link pattern** applied to service cards (`.service-card-link::after { position: absolute; inset: 0 }` with `.service-card { position: relative }`) — clicking anywhere on a service card navigates to its respective href, while the visible "Explore services →" / "Learn more →" link stays as the affordance. Standard pattern (used by Bootstrap, Stripe docs, etc.) — semantic HTML preserved, no JS, no nested-`<a>` issues. Added `.service-card:hover { cursor: pointer }` so the whole card signals interactivity.

## [2026-05-31] file-back | 4 new pages (about/massage/coaching/book) + reusable styles

Built the four inner pages to match Bethany's design brief. All share the same header/footer pattern from index.html (logo + 5-item nav + sticky sage band, footer brand/visit/book/explore grid). Nav-cta "Book Now" updated across all pages to land on `book.html` (the iframe-embed page) rather than direct link-out — body CTAs ("Book a session" etc.) keep the direct MassageBook link per the booking integration spec.

**about.html** — page-hero with eyebrow + "27 years of healing hands. One exciting new chapter." headline. Two-column grid: portrait (IMG_1051.PNG with deep teal vignette + radial mask fading edges) + bio prose (drop-cap first letter in gold). Credentials block in a sage-tinted chip below the bio. Closes with CTA to book.

**massage.html** — page-hero intro + Book Now button. Six service blocks (Relaxation / Deep Tissue+Sports / Prenatal / Aches & Pains / Lomi Lomi / Hot Stone), each with descriptive copy on the left and a pricing table on the right (stacked on mobile). Pricing tables get a sage caption strip, tabular-nums for price column, alternating row borders. Pricing note flagged for Bethany's final review. Closes with CTA.

**coaching.html** — page-hero with two paragraphs of intro (whole-person framing). Three-package grid (Single $50 / 4-pack $200 / 6-pack $300), each with hover lift + sage border. 4-session minimum note as a serif italic block. Free 20-min Discovery CTA in a contact-cta block (phone + email channels + scheduling button → mailto with prefilled subject). Closes with a cross-link to massage.

**book.html** — page-hero. MassageBook iframe embed (`widget/services` URL, 100% × 1000px, lazy-loaded, in a styled wrapper with rounded border + teal-shadow). Phone fallback + gift cert link-out below. Closes with policy block (24h cancel + 10-min early arrival).

**styles.css additions** (~180 lines): `.page-hero`, `.about-grid`/`.portrait-wrap`/`.about-bio` (with `mask-image: radial-gradient` for the portrait vignette and `::first-letter` drop cap), `.credentials` (sage chip), `.service-block`/`.service-block-inner` (responsive 1.4fr/1fr columns), `.pricing-table` (caption strip + tabular-nums), `.packages`/`.package` (3-col grid, hover), `.coaching-note` (serif italic), `.contact-cta`/`.contact-cta-channels`, `.booking-wrap`/`.booking-frame` (iframe container).

**Brand link consistency fix**: brand wrapper and Home nav item changed from `href="/"` to `href="index.html"` — root path was triggering Python http.server's directory listing on local preview.

Outstanding for next session: photo categorization (which IMG_xxxx jpegs are storefront vs treatment rooms — likely candidates for About page background or homepage hero alternative); decide whether tree backdrop should appear on About/Coaching for atmospheric consistency; mobile pass on the booking iframe (1000px fixed height is a known concern from the integration spec).

## [2026-05-31] update | Hero eyebrow "Welcome home." — promoted to teal bold for legibility against tree backdrop

Jay dev-tools tested. Three changes to `.hero-eyebrow`: font-size clamp floor raised from 1.2rem → 1.5rem (now effectively pinned at 1.5rem); `font-weight: bold` added; color `--gold-600` → `--teal-700`. The gold was getting lost in the multicolored leaves of the ghosted tree backdrop; the deeper teal pops cleanly. Italic preserved via `<em>` wrapping in the HTML. Inner pages still use gold for `.page-hero-eyebrow` since those don't have the tree backdrop to compete with.

## [2026-05-31] update | About bio greeting — "Hi" now rendered as a unit, not a 1-char drop cap

Fix: `::first-letter` was grabbing only "H", leaving "i" tiny next to a giant H. Replaced with a `<span class="greeting">Hi</span>` wrapper in the bio markup and updated the CSS to target the span. Floated like before so the body text wraps around — magazine "letter from Bethany" feel. Size 3.6rem, weight 500, gold-600, negative letter-spacing to keep "Hi" feeling tight as a two-letter unit.

## [2026-05-31] update | index.html service-card links — leading-slash → relative

Missed two spots when I swept paths on the home-link fix earlier. `.service-card-link` for Massage Therapy and Health & Wellness Coaching still had `href="/massage.html"` and `href="/coaching.html"` — same file:// breakage class as the brand link bug. Both now `href="massage.html"` / `href="coaching.html"`. Confirmed via grep across all five active pages: no remaining leading-slash internal hrefs.
