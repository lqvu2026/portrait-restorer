# Portrait Restorer

A single-file web app that cleans up old photos in the browser and crops them to 4:5 with a studio gray backdrop. It also includes a copy-ready prompt for restoring photos with an AI image model.

Photos never leave your device. All processing runs locally in the page.

## Run it

Open `index.html` in a browser, or upload it to any static host (GitHub Pages, Netlify, and similar). There is no build step and no dependencies. The only outside request is for the Google Fonts (Bricolage Grotesque, IBM Plex Sans, IBM Plex Mono). If they fail to load, the page falls back to system fonts.

## Restore tab

1. Choose a photo, drop one onto the picture, or start from the built-in sample.
2. Pick a starting point (Gentle, Faded print, Grainy scan) and adjust.
3. Drag across the picture to compare the original and restored versions.
4. Pick a size and format, then choose Render full size and Save image.

| Group | Controls |
| --- | --- |
| Frame (4:5) | Zoom, move left / right, move up / down |
| Clean | Dust and scratches, grain and noise |
| Colour and tone | Remove colour cast, auto levels, brightness, contrast, saturation, warmth, black and white |
| Detail | Sharpen |
| Studio backdrop | Replace on/off, backdrop match, edge softness, gray tone |

Export sizes are 1080 × 1350, 1620 × 2025 and 2160 × 2700 px, as PNG or JPG.

### How it works

- Dust and scratches: a 3×3 median filter replaces pixels that differ sharply from their neighbours.
- Grain and noise: an edge-preserving bilateral filter.
- Colour cast: gray-world white balance, then percentile-based levels and a tone curve.
- Backdrop: a flood fill from the photo edges finds the background, which is then replaced with a soft studio gray.
- Upscaling: stepwise 2× resizing, then an unsharp mask on luminance.

## AI prompt tab

Your original prompt, with the camera, aspect ratio and background editable. Copy it and use it with an image model that accepts a photo and returns an edited image. Check the eyes, nose, mouth and jawline against the original before using the result.

## Limits

- This is classic image cleanup, not generative restoration. It cannot redraw detail that the photo has lost, and it does not colorize.
- The backdrop replacement works best on plain backgrounds. Turn it off if the edges look wrong.
- The preview is rendered at about 900 px wide, and the export at up to 1600 px before upscaling. Very large exports can take a few seconds.
- Source images over 4000 px on the long side are scaled down on load.
- The sample image is synthetic and is not a real person.

## Files

- `index.html`: the whole app (HTML, CSS and JavaScript).
- `README.md`: this file.
