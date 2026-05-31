---
title: MassageBook Booking Integration — widget options, recommendation, gotchas
created: 2026-05-31
author: Jay LaBelle (with Claude)
scope:
  project: good-karma-collective
  context_domain: personal
source_artifacts:
  - MassageBook → Settings → Website Integration (screenshot in chat, 2026-05-31)
  - outputs/design/GoodKarmaCollective WebsiteBrief.md (Bethany's design brief)
status: active
resolves:
  - "Embed widget vs. link-out — pending decision (from README Stack)"
---

# MassageBook Booking Integration

What MassageBook actually exposes for embedding on our own site, what to use where, and the issues to watch.

## Confirmed: MassageBook biz slug

- **Public profile**: `https://www.massagebook.com/biz/good-karma-collective` (this is the URL Bethany has been advertising)
- **Widget URLs use `/therapists/good-karma-collective/`** as the slug path
- ✅ **Confirmed 2026-05-31**: `/biz/good-karma-collective` 301-redirects to `/therapists/good-karma-collective`. Both URLs work; we use the friendly `/biz/` URL in user-facing copy and the canonical `/therapists/` URL in widget/iframe embeds.

## The three widgets MassageBook gives us

### 1. Book Now Button (link-out)

```html
<a href="https://www.massagebook.com/therapists/good-karma-collective/widget/services?src=external">
  <img src="http://www.massagebook.com/home/img/getbutton/button-booknow.png"
       alt="Book Now on MassageBook.com!" border="0">
</a>
```

- Static `<a>` wrapping a MassageBook-hosted button image. Clicking takes the user to MassageBook to complete booking.
- **`?src=external`** appears to be an analytics attribution param. Keep it.
- ⚠️ **Mixed-content blocker**: button image is served over `http://`, not `https://`. On a Netlify HTTPS site, the browser will block the image. **Don't use the served PNG.** Either rewrite to `https://` (if it works — untested) or, better, build our own branded button with the same `href` target.

### 2. Booking Page (iframe embed)

```html
<iframe src="https://www.massagebook.com/therapists/good-karma-collective/widget/services"
        frameborder="0" width="100%" height="1000"></iframe>
```

- Full booking flow embedded directly. User never leaves the site.
- Fixed 1000px height — works fine on desktop. On mobile, 1000px is a tall viewport, and the iframe content does its own internal scrolling. ⚠️ **Mobile responsiveness needs a test pass.**
- ⚠️ **No brand theming exposed**. The widget renders in MassageBook's styles (sans-serif, MassageBook blue), which will visually clash with our deep-teal/gold/serif brand. Best wrapped in a strongly branded container header ("Book a session") so users understand the visual handoff.

### 3. Reviews Button (small iframe badge)

```html
<iframe src="https://www.massagebook.com/therapists/good-karma-collective/widget/reviews-btn"
        frameborder="0" width="165" height="100" allowtransparency="true"></iframe>
```

- Small 165×100 iframe — star rating + review count + "MassageBook Verified" badge. Good for social proof on Home or About.

### 4. Reviews Page (full iframe)

```html
<iframe src="https://www.massagebook.com/therapists/good-karma-collective/widget/reviews"
        frameborder="0" width="100%" height="1000"></iframe>
```

- Full reviews list embedded. Probably overkill for v1 — if Bethany wants reviews on-site, the small badge above is the better starting point.

### 5. Gift Certificates Button (link-out)

```html
<a href="https://www.massagebook.com/therapists/good-karma-collective/gift-certificates?src=external"
   target="_blank">
  <img src="http://www.massagebook.com/home/img/button-gift.png"
       alt="Purchase gift card on MassageBook.com!" border="0">
</a>
```

- Same shape as the Book Now button. Same mixed-content issue with the PNG. Same fix: custom-branded button with this `href`.
- `target="_blank"` opens MassageBook in a new tab — preserves the GKC session.

## Recommended Approach — Hybrid

| Page          | Booking element                                                                 | Why                                                                 |
|---------------|---------------------------------------------------------------------------------|---------------------------------------------------------------------|
| Home          | Branded **"Book Now"** button → link-out to `widget/services?src=external`     | Hero-level CTA, snappy, no embed lag                                |
| About         | Branded "Book Now" button (same target)                                         | Consistent CTA                                                      |
| Massage Services | Branded "Book Now" button (top + bottom)                                     | Conversion follows interest                                         |
| Health Coaching | "Schedule Free Consultation" → email/phone (not MassageBook — per Bethany)   | Coaching is discovery-call flow, not direct booking                 |
| Book Now      | **Iframe embed** (`widget/services`), wrapped in a brand-styled container       | Users who tap Book Now from nav land here and book in-place         |
| Gift Cert     | Branded "Purchase Gift Certificate" button → link-out to gift cert URL          | Same flow shape as Book Now                                         |

**Social proof (optional, decide with Bethany)**: drop the small Reviews Button iframe (165×100) on the Home page near the hero or on About. Visually contained, signals legitimacy.

## Implementation notes for the code phase

- **Build our own buttons**, don't use MassageBook's PNGs. Reasons: mixed-content, brand consistency, accessibility (alt text, focus styles), performance.
- **Iframe wrapper**: section title + short blurb above the iframe so the visual handoff feels intentional. Consider a `loading="lazy"` attribute on the iframe so the Book Now page isn't blocked by it on initial paint.
- **`X-Frame-Options` / CSP**: MassageBook is the iframe *parent's* problem only if we lock down our own CSP with `frame-src`. Make sure `frame-src https://www.massagebook.com` is allowlisted (or omit CSP for v1).
- **Mobile test plan**: load the embedded booking iframe on iOS Safari + Android Chrome at common viewports (375px, 414px) before launch. If the fixed 1000px height creates dead space or double-scroll weirdness, consider conditional behavior (iframe on desktop, link-out on mobile) or just go link-out everywhere.

## Open items

- [x] ~~Verify `/biz/good-karma-collective` and `/therapists/good-karma-collective/` point to the same listing~~ — confirmed redirect (2026-05-31)
- [ ] Test embedded iframe on mobile (375px / 414px viewports) — decide whether iframe or link-out wins on small screens
- [ ] Decide with Bethany: include Reviews Button on Home or About? (currently not in the design brief)
- [ ] Confirm `?src=external` analytics behavior in MassageBook's reporting before relying on it for attribution
