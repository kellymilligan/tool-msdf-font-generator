# MSDF Font generation

To use MSDF font's in Three.js using [`three-bmfont-text`](https://github.com/Jam3/three-bmfont-text) we need to generate an MSDF font atlas. This is a spritesheet of the font's characters with MSDF channels applied to them.

Here's some suggested [background reading](https://github.com/Jam3/three-bmfont-text/blob/master/docs/sdf.md) on this text rendering technique.

Generating font atlases is relatively easy, we're using a tool designed to work with `three-bmfont-text`: [msdf-bmfont](https://github.com/Jam3/msdf-bmfont). 

---

## Installation

Installation can be a bit fiddly (especially on Windows), make sure you've got `nodejs` and `cairo` installed in your environment. 
Cairo is required by the `node-canvas` package, and will complain during `npm install` or `yarn install` if it's not found. 

Install tool dependencies `npm install`

Then [install some system dependencies](https://github.com/Jam3/msdf-bmfont#install).

---

## Generation

1. Place your font file (must be `.ttf`, see notes below about converting other formats to ttf) into `./input/`
2. Rename the font to `font.ttf` or adjust the path in `generate.js`
3. Run the tool `npm run generate`
4. See the output `font.json` data and atlases `sheet[n].png` in `./output/`


## Tips & Notes:
- By default, it includes all standard UTF-8 characters in the `charset`, this can be adjusted in the script.
- Aim to include all glyphs within a single atlas image, as using multiple images is more complex to implement.
    - `fontSize`, `textureWidth`, `textureHeight` values can be adjusted to fit glyphs into a single image
    - Texture size should be a power of two (is loaded to the GPU)
    - Texture size shouldn't need to be large (>2048x2048px), quality improvement will be small, but it will increase memory usage and filesize. Try bringing the `fontSize` down to make it fit
- Each different font-face will need it's own atlas
- Font's can be converted from other formats (e.g. the common `.otf`) to `.ttf` using [FontForge](https://fontforge.github.io/en-US/). Open the font in FontForge, then go to `File > Generate Fonts...` and follow the prompts. Don't worry about "Em-Size power of 2" or "Missing Points at Extrema" errors.