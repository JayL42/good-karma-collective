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
