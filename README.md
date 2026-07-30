# Fix Shots - Free Online Image Tools

Privacy-first image tools. No signup, no watermarks, no image storage. Every image is processed in memory and discarded immediately.

**Live site:** [fixshots.com](https://fixshots.com)

---

## Tools

### One-Click Photo Fixer
Apply a preset style to any photo in one click - Vivid, Bright, Vintage, Black and White, or Sharp. Side-by-side preview before you download.

[Open tool](https://fixshots.com/tools/photo-fixer)

### Image Converter
Convert between JPG, PNG, WebP, AVIF, BMP, TIFF, GIF and HEIC/HEIF, with a quality slider for the lossy formats. Handles the iPhone HEIC files that Windows cannot open natively.

[Open tool](https://fixshots.com/tools/image-converter)

### Photo Privacy Cleaner
Strip GPS coordinates, camera make and model, timestamps and other EXIF metadata from a photo before you share it - and see exactly which tags were removed.

[Open tool](https://fixshots.com/tools/exif-remover)

---

## How it works

Every tool uses classical image processing via Python and Pillow. There are no AI models, no machine learning, and no third-party APIs anywhere in the pipeline.

Your image is read into memory, processed, returned to you, and discarded. Nothing is written to disk, logged, or retained in any form. There is no database, so there is nothing to breach.

## Stack

- Flask and Pillow, with pillow-heif for HEIC/HEIF support
- Vanilla JavaScript - no frameworks, no third-party CDN scripts
- Jinja2 templates on a single `base.html`
- Gunicorn behind Traefik
- GoatCounter analytics - no cookies, no personal data, GDPR compliant

---

## Links

- **Website:** [fixshots.com](https://fixshots.com)
- **Blog:** [How to Choose the Right Image Format](https://fixshots.com/blog/image-format-guide)
- **About and privacy policy:** [About Fix Shots](https://fixshots.com/about)

---

*No images stored. No accounts. No tracking. No AI.*
