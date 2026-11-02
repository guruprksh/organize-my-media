# Architecture

One file, `index.html`: HTML, CSS and JavaScript, no dependencies. The only external resource is the Google Fonts stylesheet.

## Pipeline

1. **Scan.** Files are read from the folder handle (File System Access API) or from a file input. Photos and videos are detected by MIME type or extension. Up to 500 files are drawn as particles; all files are counted and sorted.
2. **Look.** Each file is decoded (`createImageBitmap` for photos, a seeked `<video>` frame for videos) and drawn to a 24 px thumbnail, a 280 px preview and, when Claude vision is on, a 512 px JPEG.
   - Without Claude: screenshots (file name or tall PNG), documents (bright, low saturation), videos by duration, photos by month.
   - With Claude: (a) a few batches of sample images are sent and Claude proposes 4 to 8 folder names each; the lists are merged to 8 to 12 names plus "Other". (b) Every image is classified in batches of up to 8 with its file name and date. (c) Items still unassigned get a second pass in batches of 3, then fall into "Other".
3. **Match.** A SHA-256 of the first 256 KB plus the last 64 KB plus the file size. Repeats are flagged as duplicates and kept in `Duplicates (review)`.
4. **File.** Labels are laid out on an ellipse around the vortex. Particles launch along quadratic Bezier paths and land in a phyllotaxis pile next to their label.

## Applying

`dest(item)` returns `['Sorted', optional 'YYYY-MM', folder]`. In copy mode each file is streamed to the destination (`file.stream().pipeTo(writable)`). In move mode the source is removed only after the copy succeeds. A journal enables undo.

## Rendering

A single `<canvas>` with a `requestAnimationFrame` loop draws the vortex, particles, trails and sparks. Labels, the gallery and the apply panel are DOM. `prefers-reduced-motion` slows the vortex and disables sparks and shortened flights.

## Claude API use

`apiShim(key)` calls `POST https://api.anthropic.com/v1/messages` with images as base64 and the browser-access header. Inside claude.ai the page uses the host's sampling capability instead and the key box stays hidden.
