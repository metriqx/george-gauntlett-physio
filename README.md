# George Gauntlett Physio

Static marketing site for George Gauntlett Physio, Church Street Practice,
Bradford-on-Avon.

## Structure

Two hand-authored HTML pages, no build step. All CSS and JS are inline, and all
images are embedded as base64 data URIs, so the pages are fully self-contained.

| File | Purpose |
| --- | --- |
| `index.html` | Single-page main site: hero, about, services, the 3 R's, fees, contact, location, FAQs |
| `conditions-treated.html` | Interactive body map of conditions treated |

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

- The 3 R's section uses `.section-approach-light`; its light styling overrides
  live in the `<style>` block near the "Light treatment for the 3 R's section"
  comment in `index.html`.
- Navigation and footer links are duplicated in both pages; change both.
- Cancellation policy (48 hours) appears twice in `index.html`: the fees small
  print and the FAQ entry.
