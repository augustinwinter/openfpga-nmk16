# Licensing and publication review

This repository is being prepared for public release, but the source snapshot must be reviewed before a project-wide license is applied.

## Current rule

- Preserve every inherited copyright and license notice.
- Do not publish game ROMs, firmware dumps, decoded game assets, reference media, save states, or private preservation material.
- Do not infer ownership from the fact that a file is present in the maintained development tree.
- Treat copied or adapted upstream HDL according to its original license.
- Record provenance for project-authored or substantially modified files.

## Candidate project license

**GPL-3.0-or-later** is a practical candidate for project-owned integrated gateware because GPL components are present in the dependency graph, but this is not yet a final determination.

A repository-level license should be added only after confirming that:

1. every published source file has an identified origin,
2. required upstream notices are retained,
3. all included third-party licenses are compatible with the intended distribution,
4. project-authored files can legitimately be offered under the chosen license.

## Game content

The code license will not grant rights to Super Spacefortress Macross ROMs, graphics, audio, trademarks, or other original game content.

See [THIRD_PARTY.md](../THIRD_PARTY.md) for the working component map.
