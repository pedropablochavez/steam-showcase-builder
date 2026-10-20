# Steam Showcase Builder

A free tool for creating **animated showcases for your Steam profile** (split GIFs that line up perfectly with each other), right in your browser. No account, no tokens, no watermarks, and your files are never uploaded to any server.

## What is it for?

On Steam, the Artwork and Workshop showcases display **several separate images side by side**. If you want them to look like one continuous image, each piece has to be the exact width and the gap Steam leaves between them has to be cut out. Otherwise the narrow strip ends up "shifted" and doesn't line up with the big one.

This tool lets you build everything on a single canvas, add layers (background, character, text, frame, effects), and when you export it automatically cuts it into the GIFs Steam needs, already aligned.

## Showcase types

| Tab       | Files it generates    | Size                                         |
|-----------|-----------------------|----------------------------------------------|
| Featured  | 1 GIF                 | 630 px wide                                  |
| Artwork   | 2 GIFs (main + strip) | 506 px + 100 px (9 px hidden gap in between) |
| Workshop  | 5 GIFs                | 5 × 122 px (4 px hidden gap between each)    |
| Adaptive  | 1 GIF                 | 630 px, height follows the background        |
| Avatar    | 1 image               | 512 × 512 px                                 |

You choose the height (824 px by default).

## Features

- **Background:** image, animated GIF, WebP or video (MP4/WEBM). Cover/fit options, plus **"Align with profile"**: scales a 1920 px profile background and crops it at the exact position of the showcase so it blends into your Steam background. Brightness, contrast, saturation, hue and blur.
- **Characters (multiple):** remove the background three ways — quick (corner color), chroma key (also works on GIFs and video), or **AI that runs on your own PC** ([@imgly/background-removal](https://github.com/imgly/background-removal-js)). Scale, rotation, flip, 10 animations (breathing, wave, float, sway, pulse, shake, 3D spin, zoom, glitch…), light, glow, sticker, echo and shadow effects, "blend into background" and color correction.
- **Text (multiple):** 38 fonts, horizontal / stacked / sideways orientation, gradient, outline, shadow and 26 animations (Glow, Tube Charge, Holo Foil, Chrome Neon, Embers, Molten Gold, Glitch, typewriter, letter wave…).
- **Frames:** 18 styles (classic, neon, HUD, film, rainbow, glitch, thorns…), animated or static. Each piece of the showcase gets its own frame.
- **Effects (multiple, stackable):** 75 seamlessly looping effects in 5 categories, plus a global Glitch. Drag any effect in the preview to place it and use the mouse wheel to resize it.
  - **Particles:** Matrix, Sakura, snow, rain, sparks, fireflies, hyperspace, network…
  - **Occult / Satanic:** pentagram, inverted pentagram, inverted cross, 666, ritual candles, hell portal, hellfire, blood drip…
  - **Horror / Jumpscare:** jumpscare face, demon eyes, creepy eye, shadow figure, spiders, bats, ghosts, heartbeat, TV static…
  - **Memes / Troll:** skull rain 💀, emoji rain, MLG, Deal With It, bouncing text, Vine Boom, censored bar, error popups, fake loading, Wasted, To Be Continued, Deep Fried, Bass Boosted, RGB Gamer…
  - **Filters:** earthquake, invert flash, lens flare, VHS, film grain, vignette… (filters affect every layer below them)
  - Some effects have editable text (666, Bouncing Text, Wasted, Censored, Emoji Rain…).
- **Export:** loop duration, FPS and colors. If a GIF goes over the limit (5 MB by default) it is **optimized automatically**. Includes the hex trick, ZIP download and static PNG.
- **GIF optimizer:** shrink any GIF (colors, scale, frame skipping) or let auto mode bring it under the limit.
- **Hex patcher:** changes the last byte of your GIFs from `0x3B` to `0x21`.
- **Profile mockup**, **save/open project** (.json) and a **step-by-step guide** for uploading to Steam with the console commands.

- **English / Spanish:** switch the interface language with the **EN / ES** buttons at the top right. Your choice is remembered.

## How to use it

**Online, nothing to download:** <https://pedropablochavez.github.io/steam-showcase-builder/>

Or download `index.html` and open it in Chrome, Brave or Edge (double-click). It only needs internet to load fonts and libraries.

1. Pick the showcase type at the top (for example **Artwork**).
2. Add a background, character, text, frame and effects from the left panel. Drag in the preview to move the selected layer and use the mouse wheel to scale it.
3. Click **Download GIFs**.
4. Follow the **How to upload** tab.

## Uploading to Steam (summary)

1. Go to <https://steamcommunity.com/sharedfiles/edititem/767/3/> (upload artwork).
2. Choose the file and paste the invisible character `⠀` (U+2800) in the title so no text shows under the showcase.
3. Open the console (F12 → Console), paste the command and press Enter:
   - Artwork / Featured:
     ```js
     $J('#image_width').val(1000).attr('id',''),$J('#image_height').val(1).attr('id','');
     ```
   - Screenshots:
     ```js
     $J('#image_width').val(1000).attr('id',''),$J('#image_height').val(1).attr('id','');$J('[name=file_type]').val(5);
     ```
   - Workshop (upload the 5 parts in order):
     ```js
     $J('[name=consumer_app_id]').val(480);$J('[name=file_type]').val(0);$J('[name=visibility]').val(0);
     ```
4. Tick the authorship checkbox, save, and repeat for each part.
5. **Edit Profile → Featured Showcase** and pick the artwork for each slot.

> Showcases unlock at Steam level 10 (one more every 10 levels). The console commands and the hex trick are community tricks, not official Steam features, so they may stop working if Steam changes something.

## Tech

A single HTML file with plain JavaScript. It uses [gifenc](https://github.com/mattdesl/gifenc) to create the GIFs, [fflate](https://github.com/101arrowz/fflate) for the ZIP, the browser's `ImageDecoder` to read animated GIFs, and Google Fonts for the fonts.

---

Not affiliated with Valve or Steam.
