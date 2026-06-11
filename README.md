# Dither Boy — local edition

A self-contained, **in-browser** dithering studio inspired by
[Studio AAA's Dither Boy](https://studioaaa.com/product/dither-boy/).
Upload an image, tweak the dither, download a PNG. Everything runs locally —
your images never leave your machine and there is no install or build step.

## Run it

**Option A — just open it.** Double-click `index.html`. It works straight from
`file://` (no server needed).

**Option B — serve it** (recommended; enables "Copy to clipboard" in some
browsers and avoids any local-file quirks):

```bash
# from inside the ditherboy/ folder
python -m http.server 8000
# then open http://localhost:8000
```

## Features

**Input** — drag & drop, file picker, or paste from clipboard (Ctrl/Cmd+V).

**18 dithering algorithms**
- *Error diffusion:* Floyd–Steinberg, False Floyd–Steinberg, Jarvis–Judice–Ninke,
  Stucki, Atkinson, Burkes, Sierra (3-row), Two-Row Sierra, Sierra Lite, Stevenson–Arce
- *Ordered:* Bayer 2×2 / 4×4 / 8×8, Clustered-dot 4×4 / 8×8
- *Pattern:* Halftone dots, Random noise, Threshold (no dither)

**Color**
- Black & White (1-bit) with custom ink/paper colors
- Grayscale / Duotone with an adjustable number of levels (2–32) and tinting
- Color palettes: Game Boy, Game Boy Pocket, CGA, Commodore 64, PICO-8,
  ZX Spectrum, CMYK, Sepia, and more
- Build a **custom palette** by hand, or **extract** a palette from the image
  (median-cut, 2–32 colors)

**Adjustments (pre-dither)** — brightness, contrast, midtones (gamma),
saturation, hue shift, invert.

**Controls** — resolution / pixelation, dither amount (error scale / threshold
spread), serpentine scan, halftone dot size.

**Post effects** — scanlines, noise, chromatic aberration.

**Export** — download PNG at 1× / 2× / 4× / 8× (crisp nearest-neighbour upscale),
or copy straight to the clipboard. Live preview updates as you drag sliders.

**Animated GIF** — load an animated GIF and every frame is re-dithered with your
current settings, then exported as a new looping GIF (original frame delays
preserved). Or turn a *still* image into an animated GIF: the "shimmer" generator
renders N frames with a moving/boiling dither pattern at an adjustable frame rate
— echoing the original's "temporal" effects. GIF encoding and decoding are both
implemented from scratch (no libraries).

**Batch processing** — queue any number of images, dither them all with the
current settings, and download the results as a single `.zip` (also written from
scratch, no libraries).

## Files

| file | purpose |
|------|---------|
| `index.html` | layout & controls |
| `style.css`  | styling |
| `dither.js`  | the processing engine (algorithms, palettes, effects) |
| `codec.js`   | animated GIF encoder/decoder + ZIP writer (all from scratch) |
| `app.js`     | UI wiring & render pipeline |

## Notes & differences from the original

This is an image-focused homage. The commercial Dither Boy additionally offers
full video dithering with a timeline, a much larger effect library (~63),
stackable reorderable effect layers, and vector/embroidery export — those are out
of scope here (animated GIF in/out is supported, but not video formats).
Everything above is implemented from scratch in vanilla JS on the Canvas API.
