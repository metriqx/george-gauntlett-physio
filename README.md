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

- Brand colours are the `:root` custom properties at the top of each page's
  `<style>` block: navy `#123d7a`, teal `#138a85` (the `--green` / `--sage-*`
  tokens still carry their old names), pale teal `#e6f2f2`. There is no build
  step, so a colour change means editing every page.
- "How George can help" is the `.gg-services` block; its cards are `<details>`
  elements, so they open without JavaScript.
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
