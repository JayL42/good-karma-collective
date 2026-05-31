---
title: Good Karma Collective — Website Project
created: 2026-04-24
author: Jay LaBelle
scope:
  project: good-karma-collective
  context_domain: personal
status: active
aliases: [gkc, good-karma]
---

# Good Karma Collective

Website build for Bethany LaBelle's new solo wellness practice (massage therapy + functional medicine health coaching). Independent personal project — Jay handles hosting/tech, Bethany drives design/copy decisions in a separate Claude context seeded from `source-artifacts/brief.md`.

## Status

**Phase**: Design approved, ready to build. As of 2026-05-31, Bethany has filed the complete website brief at `outputs/design/GoodKarmaCollective WebsiteBrief.md` — finalized copy, brand palette (deep teal + gold), tagline, 5-page structure, and pricing for all services. Next step is the code/hosting build.

## Roles

- **Bethany LaBelle** — owner, LMT + FMHC. Drives brand voice, service copy, visual direction. Works with Claude in a separate chat seeded from `source-artifacts/brief.md`.
- **Jay LaBelle** — technical owner. Handles hosting (Netlify), domain, Vagaro widget embed, deployment, site updates. Uses this project folder + Claude on the Development workspace.

## Stack (current)

- **Hosting**: Netlify (free tier)
- **Domain**: TBD (~$15/year)
- **Booking**: **MassageBook** — `https://www.massagebook.com/biz/good-karma-collective`. **Hybrid approach** (decided 2026-05-31): every page has a branded "Book Now" button that link-outs to MassageBook; the dedicated `Book Now` page embeds the full booking iframe so users can complete in-place. See [`outputs/specs/2026-05-31-booking-integration.md`](./outputs/specs/2026-05-31-booking-integration.md) for the full integration spec, widget snippets, and gotchas (mixed-content on MB's button PNGs, mobile responsiveness pending test). Bethany has Square reader paired with MassageBook for in-person payments. Gift certificates also routed through MassageBook.
- **Build**: Custom site — not a site builder. Static or light framework (likely 11ty / Astro / hand-rolled HTML+CSS — decision pending). MassageBook's own site builder is *not* viable because it doesn't allow custom code, which is why we host elsewhere.
- **Source control**: GitHub (connector needed when we start writing code — see `CLAUDE.md`). No repo exists yet.

## Brand (from Bethany's filed design brief)

- **Tagline**: *Wellness for Body, Mind & Life*
- **Primary background**: Deep teal `#1a5c56`
- **Gold accent**: `#c9a84c`
- **Website background**: Warm cream / soft white
- **Leaf accent tones**: Terracotta, sage, amber for subtle pops
- **Typography**: Serif headings (small-caps feel matching logo), clean readable body

## Site Structure

5 pages + a Gift Certificates link:

1. **Home** — hero, vision, service preview blocks
2. **About** — Bethany's bio (27+ years), credentials block
3. **Massage Services** — 6 services with pricing tables
4. **Health Coaching** — packages + free 20-min discovery call CTA
5. **Book Now** — MassageBook widget or link-out

Full copy lives in `outputs/design/GoodKarmaCollective WebsiteBrief.md`.

## Key Decisions Made

- Custom build, not Wix/Squarespace — annual cost ~$15 vs. $200-400+
- Name: *Good Karma Collective* — signals community + growth vs. solo spa
- Booking via **MassageBook** (corrected from Vagaro in original brief)
- Two service lines: massage (book via MassageBook) + health coaching (free 20-min discovery call, no direct booking)
- Brand palette + tagline approved (see Brand section above)
- All copy approved by Bethany

## Resolved HIL Items

- ✅ Phone: **978-857-7842** (carries from Serenity, confirmed for GKC)
- ✅ Email: **BethanyLaBelle.lmt.hc@gmail.com**
- ✅ Hot Stone certification: listed in services
- ✅ Booking platform: MassageBook (not Vagaro)

## Open HIL Checkpoints (from Bethany's filed brief)

- Final review of all massage prices before launch
- Final review of coaching package prices before launch
- Confirm policies are accurate for GKC
- ~~Provide photos for the site~~ ✅ (delivered 2026-05-31 — see Assets below)
- Confirm MassageBook gift certificate setup is active

## External Profiles & Links

- **GitHub repo** (private): `https://github.com/JayL42/good-karma-collective`
- **MassageBook profile**: `https://www.massagebook.com/biz/good-karma-collective` (redirects to `/therapists/good-karma-collective`)
- **Google Business Profile**: `https://share.google/3BNZRZ391JrKIH8xJ`
- **Google review link** (for asking happy clients to leave reviews): `https://g.page/r/CZ2MSft7QnSpEBM/review`

## Assets

All in `outputs/design/`:

- `Good Karma Logo.svg` — primary logo. Has a deep-teal background rect baked in (`rgb(3,75,90)` ≈ `#034b5a`). Drop the rect element for a transparent-background variant, or crop the raster for shaped placements (circle, badge).
- `IMG_1051.PNG` — Bethany portrait (head & shoulders, portrait orientation). Featured on About page per the design brief.
- `IMG_2900.jpeg`, `IMG_2921.jpeg`, `IMG_3060.jpeg`, `IMG_3063.jpeg` — interior space + storefront photos. Need to be categorized (which is which) before placement decisions. Several are 3–4 MB raw — will need responsive resizing for the site (~120–250 KB per image at common hero sizes).

## File Layout

```
good-karma-collective/
├── CLAUDE.md               # Project-local context gate — loads frameworks, excludes Returnalyze
├── README.md               # This file
├── log.md                  # Project-local append-only log
├── .gitignore              # macOS, editor, node, build, env, netlify
│
├── index.html              # ⭐ Home — hero, vision, service preview, fixed ghosted tree backdrop
├── about.html              # About Bethany — portrait, bio, credentials
├── massage.html            # 6 services + pricing tables
├── coaching.html           # Coaching packages + free 20-min discovery CTA
├── book.html               # MassageBook iframe embed + gift cert link-out
├── styles.css              # All shared styles — tokens, header/footer, page patterns
│
├── assets/
│   ├── logo-small.svg      # Horizontal lockup, transparent bg — header logo
│   └── logo-large.svg      # Vertical lockup, transparent bg — used by ghosted backdrop on index
│
├── source-artifacts/
│   └── brief.md            # Original handoff brief — superseded by outputs/design/ brief
└── outputs/
    ├── analyses/           # Filed analyses (brand direction eval, competitor scan, etc.)
    ├── design/             # Mockups, wireframes, color/type specs
    │   ├── GoodKarmaCollective WebsiteBrief.md  # ⭐ canonical brief — all copy + brand approved
    │   ├── Good Karma Logo.svg / Logo Small.svg
    │   ├── color palate.png                     # Wellness palette reference (ChatGPT-sourced)
    │   └── IMG_*.PNG / IMG_*.jpeg               # photos (portrait + space + storefront)
    └── specs/              # Technical specs (hosting plan, deploy pipeline, etc.)
        └── 2026-05-31-booking-integration.md    # MassageBook widget options + hybrid approach
```

## Viewing the mockup

```bash
cd ~/Development/projects/good-karma-collective
python3 -m http.server 8000
# then open http://localhost:8000 in a browser
```

Or just open `index.html` directly — Google Fonts CDN works either way; some hover/sticky behaviors are easier to evaluate via the local server.

## Related

- `projects/README.md` — workspace project registry
- `assets/good-karma-collective-claude-brief.md` — original handoff brief (canonical copy is in `source-artifacts/`)
