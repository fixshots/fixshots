# Fix Shots - Free Online Image Tools

Privacy-first image tools. No signup, no watermarks, no image storage. Every image is processed in memory and discarded immediately.

**Live site:** [fixshots.com](https://fixshots.com)

---

## Engineering notes

Write-ups of the parts that were not obvious to build. Runnable code, real measurements, and the things I got wrong first.

- **[Compressing a JPEG to an exact file size in Python](https://fixshots.com/blog/compress-jpeg-exact-file-size-python)** - binary search on the quality dial, when to shed pixels instead, and measurements across four 12.5 MP camera originals showing what `optimize=True` on every encode actually buys. Includes a benchmark script so you can run it on your own photos.

---

## Tools

### Signature Extractor
Pull a signature off a phone photo of paper. Estimates the local background with a morphological closing, so uneven lighting and paper texture come out clean rather than blotchy. One extraction, two outputs: a JPG at exact pixel dimensions inside a min/max KB window for upload forms, or a transparent PNG in a chosen ink colour for signing documents.

[Open tool](https://fixshots.com/tools/signature-extractor)

### Watermark & Credit
Stamp your name or logo on a photo before you publish it, and sign it in the metadata. Tiled or single placement, with EXIF Artist and Copyright fields written alongside the visible mark.

[Open tool](https://fixshots.com/tools/watermark)

### Compress to Exact Size
Hit a hard file size limit - 20 KB, 50 KB, 100 KB, or any target from 5 KB to 5000 KB. Built for the upload forms that reject a photo for being a few kilobytes too large. Finds the highest JPEG quality that still fits, and only reduces the pixel dimensions when no quality setting is small enough.

[Open tool](https://fixshots.com/tools/compress-to-size) · [How it works](https://fixshots.com/blog/compress-jpeg-exact-file-size-python)

Size-specific pages: [20 KB](https://fixshots.com/compress/20kb) · [50 KB](https://fixshots.com/compress/50kb) · [100 KB](https://fixshots.com/compress/100kb)

### One-Click Photo Fixer
Apply a preset style to any photo in one click - Vivid, Bright, Vintage, Black and White, or Sharp. Side-by-side preview before you download.

[Open tool](https://fixshots.com/tools/photo-fixer)

### Image Converter
Convert between JPG, PNG, WebP, AVIF, BMP, TIFF, GIF and HEIC/HEIF, with a quality slider for the lossy formats. Handles the iPhone HEIC files that Windows cannot open natively.

[Open tool](https://fixshots.com/tools/image-converter) · [HEIC to JPG](https://fixshots.com/convert/heic-to-jpg)

### Photo Privacy Cleaner
Strip GPS coordinates, camera make and model, timestamps and other EXIF metadata from a photo before you share it - and see exactly which tags were removed.

[Open tool](https://fixshots.com/tools/exif-remover)

---

## How it works

Every tool uses classical image processing via Python and Pillow. There are no AI models, no machine learning, and no third-party APIs anywhere in the pipeline. Nothing here needs a GPU, an API key, or a paid tier to run.

Your image is read into memory, processed, returned to you, and discarded. Nothing is written to disk, logged, or retained in any form. There is no database, so there is nothing to breach.

Because every tool rebuilds the output from the image pixels alone, EXIF metadata is dropped as a side effect. A converted or compressed file does not carry your GPS coordinates into whatever you upload it to.

If you are reading the source, the two least obvious pieces are `compress_to_target()`, which searches JPEG quality by bisection and falls back to pixel reduction only when the quality floor still overshoots, and the signature extraction path, which estimates a per-pixel background level rather than thresholding against a global constant.

## Stack

- Flask and Pillow, with pillow-heif for HEIC/HEIF support
- Vanilla JavaScript - no frameworks, no third-party CDN scripts
- Jinja2 templates on a single `base.html`
- Gunicorn behind Traefik
- GoatCounter analytics - no cookies, no personal data, GDPR compliant

The tool list in `main.py` drives the navigation dropdown, the homepage grid and the ticker. Adding or reordering a tool needs no template changes.

---

## Links

- **Website:** [fixshots.com](https://fixshots.com)
- **Blog:** [All articles](https://fixshots.com/blog)
- **About and privacy policy:** [About Fix Shots](https://fixshots.com/about)

---

*No images stored. No accounts. No tracking. No AI.*
