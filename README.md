# mnshot.ai

Marketing site for **mnshot** — a boutique AI research lab delivering frontier solutions to frontier science-based problems.

Single-file static site (`index.html`). No build step. Deployed via Cloudflare Pages.

## Structure

- `index.html` — the entire site (HTML + inline CSS + inline JS + Google Fonts + Unsplash imagery).

## Local preview

```bash
open index.html        # macOS — opens in your default browser
# or
python3 -m http.server 8080
# then visit http://localhost:8080
```

## Deployment

1. Push this repo to GitHub.
2. In Cloudflare Pages, create a new project from this repo. No build command, output directory `/` (root).
3. Point `mnshot.ai` at Cloudflare (nameservers on Namecheap → Cloudflare) and add the custom domain in Pages.

## Stack

- Fraunces (display) + Inter (body), served from Google Fonts.
- Palette: warm ivory base, pale blue-horizon mist, muted aged-gold accent.
- Project thumbnails sourced from Unsplash and filtered/toned in CSS to match the palette.
