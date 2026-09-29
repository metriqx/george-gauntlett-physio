# George Gauntlett Physio

Static marketing site for George Gauntlett Physio, Hartley Farm, Winsley.

## Structure

One hand-authored HTML page, no build step. All CSS and JS are inline, and all
images are embedded as base64 data URIs, so the page is fully self-contained.

| File | Purpose |
| --- | --- |
| `index.html` | The whole site: hero, about, services, fees, contact, location (map), FAQs |
| `rugby-robust.html` | Rugby Robust: physio-led youth rugby robustness workshops and sessions (U13 to U16) |

`.nojekyll` stops GitHub Pages from running Jekyll over the files.

## Local preview

```bash
python3 -m http.server 4173
```

Then open http://localhost:4173.

## Deploying

The site is static, so any static host works. For GitHub Pages: push to `main`,
then Settings to Pages, source "Deploy from a branch", branch `main` / root.

For a custom domain bought at Namecheap, add the domain under Settings to Pages
to Custom domain (this writes a `CNAME` file), then in Namecheap set Advanced
DNS to:

- `A` records for `@` pointing at `185.199.108.153`, `185.199.109.153`,
  `185.199.110.153`, `185.199.111.153`
- `CNAME` record for `www` pointing at `<org-or-user>.github.io`

Wait for DNS to propagate, then tick "Enforce HTTPS".

## Editing notes

- The site mirrors the Rugby Robust page: navy `#0d1724`, pale blue `#a7d8f2`,
  tints `#eef8fd`, lines `#dbe6ed`, set as `:root` custom properties at the top
  of each page's `<style>` block (the `--green` / `--sage-*` tokens still carry
  their old names from the previous palette). Accent text and icons use a
  darker `#2b6d91` so they pass contrast on white, where Rugby Robust's own
  `#78c5eb` only works against its dark backgrounds.
- One typeface throughout, matching Rugby Robust:
  `Inter, ui-sans-serif, system-ui, …`. No webfont is loaded, so it falls back
  to the system UI font exactly as Rugby Robust does.
- There is no build step, so a colour or font change means editing every page.
- "How George can help" is the `.gg-services` block; its cards are `<details>`
  elements, so they open without JavaScript.
- "Appointments and fees" is the `.gg-fees` block: two equal `minmax(0, 1fr)`
  tracks, Health and Performance.
- Favicons are generated from `images/logo.webp`; regenerate all three sizes
  together if the logo changes.
- Booking buttons open the Splose booking form in a pop-out (`#booking-dialog`).
  The iframe is lazy: its `src` is only set from `data-src` on first open, so
  Splose is not loaded on every page view. Each button keeps the real Splose
  URL in its `href` with `target="_blank"`, so it still works without
  JavaScript. The `splose-booking-embed` script handles the iframe auto-resize
  and pushes a `splose_booking_confirmed` event to `window.dataLayer` (only
  useful if GTM or GA4 is installed).
- The clinic address (Unit 8, Hartley Farm, Winsley, BA15 2JB) appears in the
  location section, the MedicalBusiness JSON-LD and the Google Maps embed.
- Cancellation policy (48 hours) appears twice in `index.html`: the fees small
  print and the FAQ entry.
- The full top-level nav needs about 1040px; below that the header switches to
  the menu button.
