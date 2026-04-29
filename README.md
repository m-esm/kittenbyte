# KittenByte landing page

Static marketing page for **KittenByte**, a Tinder-style photo cleanup app for iOS and Android. Live at [m-esm.github.io/kittenbyte](https://m-esm.github.io/kittenbyte/).

The app source lives in a separate repo. This repo only hosts the marketing site.

## Stack

Plain HTML + CSS + a few lines of JS, no build step. Everything lives in `index.html` with embedded styles. Screenshots are stored as both PNG and WebP under `screenshots/`; the page serves WebP first via `<picture>` and falls back to PNG.

## Local preview

```bash
# any static server works
python3 -m http.server 8000
# → http://localhost:8000
```

## Updating screenshots

Screenshots are captured from the iOS simulator running the KittenByte app, then resized to 540px wide with rounded corners. The pipeline (in the app repo):

1. Boot a paired iPhone simulator and run the app.
2. Drive it to the desired state, then `xcrun simctl io booted screenshot <name>.png`.
3. Resize + round-corners with PIL, scale to 540px wide, save as PNG.
4. Convert to WebP with `quality=82, method=6` (icon uses 90).
5. Copy `<name>-web.png` and `<name>-web.webp` into this repo's `screenshots/`.

The OG share image (`screenshots/og-image.png`, 1200x630) is composed from the hero and delete-queue screenshots over a peach radial gradient.

## Deployment

GitHub Pages is configured to serve from the `main` branch root. A `.nojekyll` file disables Jekyll processing so dotfiles and `_`-prefixed paths pass through unchanged.

Push to `main` and the page redeploys.

## License

MIT. See [LICENSE](LICENSE).
