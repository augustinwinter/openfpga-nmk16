# Architecture overview

Macross Ver.26 models the NMK-derived arcade hardware used by Super Spacefortress Macross and adapts it to the Analogue Pocket/openFPGA environment.

## Major blocks

- **68000 main CPU** — FX68K
- **NMK004 sound controller** — project TLCS-90/NMK004 implementation
- **YM2203-compatible audio** — JT03/JT49
- **ADPCM audio** — two JT6295 instances
- **Background renderer**
- **Sprite renderer**
- **Text renderer**
- **Palette and presentation pipeline**
- **Pocket memory / loading / input / display / audio glue**

## Timing and presentation

A major part of the final engineering work was preserving the original machine's temporal behavior when crossing into the Pocket display domain.

The late verification stages focused on:

- Stage23 — scroll-domain snapshotting
- Stage24 — sprite-frame coherency
- Stage25 — palette timeline coherency
- Stage26 — text and background temporal coherency

These mechanisms exist because a visually plausible frame can still be wrong if state from different native raster times is mixed into one output frame.

## Native behavior and Pocket presentation

The arcade machine and Pocket display do not share the same refresh cadence. Ver.26 therefore separates native game-state timing from Pocket presentation timing and intentionally accepts refresh-conversion repeats where required instead of altering native motion to hide them.

The final physical motion review classified the remaining foreground judder as refresh-conversion behavior rather than a renderer defect.
