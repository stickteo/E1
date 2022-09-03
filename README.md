# E1
Tool for converting Jetters Tile and Map data into a BMP.

Used for extracting graphics from Jetters to allow easy image editing.

Usage: E1 pal.bin map.bin tile.bin out.bmp [meta.txt]

## pal.bin
GBA palette file where each entry is 2 bytes.

(Either dump from ROM or copy the bytes from mGBA's memory viewer)

## map.bin
Jetters specific format.

Each entry is a typical map entry.

However with 2 special commands:
- 0xFFFE indicates newline.
- 0xFFFF indicates end of map.

The tool is meant to bulk process multiple maps, so there can be multiple 0xFFFF commands.

It's done this way to:
1) Avoid multiple BMP files from being generated.
2) A tileset can correspond to many small maps. (Maps can be buttons, title banners, GUI elements, etc)
3) There's just too many maps... In particular, a set can be 99 maps!

## tile.bin
Typical GBA tileset where each entry is 32 bytes. The tool only supports 4bpp (for now).

(Can be dumped from ROM via GBAmdc since the tile sets are LZSS compressed)

## out.bmp
Output image.

The BMP is specifically formatted to contain the palette (and keep them in the correct order).

This means a tool like Usenti can edit the BMP and preserve the palette.

More importantly, this means we can preserve the palette when we generate a new tile set and maps.

## meta.txt
Metainfo about the maps.

Each map will correspond to a region indicated by X, Y, W, and H (in units of tiles).

This will be used by another tool to generate a new map.bin.
