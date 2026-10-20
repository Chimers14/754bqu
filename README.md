# MIXUP ARCHIVE — reading-first rebuild

## Test in VS Code
Open the project folder in VS Code, then run:

```bash
python build_sources.py
python -m http.server 8000
```

Visit **http://localhost:8000**. Do not open index.html with `file://` because fetch/PDF operations may fail.

## Add your books and sources
Use the top-level **`sources/`** folder. For your book, put numbered images inside **`sources/flash-of-the-spirit/`** (`001.png` through `355.png`). Other books can have their own subfolders; individual PDF, TXT, PNG, JPG, GIF, WebP, BMP, AVIF, TIFF or SVG files can go directly inside `sources/`. Run `python build_sources.py` again each time you change the folder. It rebuilds `sources/manifest.json`. Source folders become selectable tabs in READ. Browser + ADD FILE is temporary for the current session and doesn't write to your local project folder.

## Reading interaction
Tap a single word in extracted text for a dictionary lookup. Drag the word away from the document (at least 12 pixels) to create a separate bouncing, rotating word object in the lower playground. For image pages, press **RECOGNIZE IMAGE TEXT** first. The OCR result is a selectable transcript, not a perfectly positioned text layer on top of the scan. PDF text layers are supported, though complex typography can have imperfect hitboxes. The OCR engine, PDF.js and dictionary services need internet access. Dictionary entries and etymologies are not guaranteed for all languages or Afro-Caribbean cultural terms.

## WORDS
Type one word and press Enter. Words fall, collide, rotate and can be dragged/thrown. The screen includes full interaction instructions and a dictionary-language selector. This is lightweight 2D collision physics, not the Happy Wheels engine; rotating rectangles use approximate collision boxes.

## Videos
VIDEO picks randomly from your five supplied YouTube links and immediately displays the video without a separate menu. It requests fullscreen and landscape when browser APIs permit. **iOS Safari and some Android browsers do not allow a site to force orientation or fullscreen on an iframe.** The portrait CSS rotates the video surface where possible, but for reliable horizontal viewing users may still need to rotate their device and enable fullscreen in the player. YouTube playback/autoplay is subject to browser and embed restrictions.

## Privacy / metadata
Install Pillow and pypdf with `python -m pip install pillow pypdf`, then run `python privacy_clean.py sources/flash-of-the-spirit/` and inspect the `clean_output/` folder. This creates copies; it does **not** guarantee complete PDF sanitization. Check document content, hidden attachments, OCR layers, watermarks, copyright and other identifying details before publishing. Browser uploads are **not** scrubbed automatically.

## Missing original game assets
`game.js` and `server.js` were not included in the supplied files. MIXUP is clearly marked **WORK IN PROGRESS**; to restore the original game, add its existing `game.js` (and server files if using multiplayer). The reading and word features do not require the game.

## Rights
The local `file:///G:/...` path cannot be read by visitors or ChatGPT. Add your book locally, and confirm you have permission to publicly host or distribute copyrighted book scans.


## Flash of the Spirit setup (updated)
Copy your 355 PNGs into `sources/flash-of-the-spirit/` (for example `001.png` ... `355.png`). Run `python build_sources.py`, then `python -m http.server 8000`. The first source is selected automatically and its drawer remains collapsed until opened. Browser uploads remain separate underneath.

The VIDEO overlay has a top-right MENU control and supports browser Back after entering a video. OCR text supports double-click/double-tap dropping and drag-to-drop.

## Rigid-body update
READ and WORDS now share one rigid-rectangle physics implementation. Grab any part of a word to dangle it by that point; release to bounce, tumble, and settle with friction. No automatic angle snapping. The READ transcript supports dragging directly into the playground. This is a custom JavaScript solver; it has not been browser-tested here.

## READ physics parity
READ loose words now use the same `createWordPhysics` rigid-body solver and the same `word-chip-inner` visual geometry as WORDS. READ retains its document, definitions, and OCR controls. Dragging a document word spawns a loose body; after it is loose, grab any edge and swing or throw it like on WORDS. The READ playground has been enlarged. WORDS files and behavior were not modified.

## READ panel resizing
Drag the three-line divider immediately beneath the book viewer up or down to allocate screen space between the document and the loose-word playground. Double-click the divider to restore the default split. Keyboard: focus divider, use Up/Down arrows (Shift for larger steps), or Home to reset. This resizes the panel, not the PNG/PDF/text zoom. WORDS and the physics solver were not changed.
