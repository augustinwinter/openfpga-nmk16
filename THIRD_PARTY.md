# Third-party components and provenance

This file records component publication decisions. No project-wide license has been adopted; original per-file licenses remain authoritative.

## Known upstream components

| Component | Role | Upstream / author | Publication status |
|---|---|---|---|
| FX68K companions | 68000-compatible CPU support | Jorge Cwik, ijor/fx68k | five exact pinned upstream files published under GPL-3.0-or-later; modified fx68k.sv, fx68kAlu.sv and inaccurate UPSTREAM.txt remain held |
| JT03 / JT49 | YM2203-compatible audio | Jose Tejada Gomez | first source batch published under GPL-3.0-or-later; all HDL independently matched to recorded upstream pins in this review |
| JT6295 | OKI ADPCM audio | Jose Tejada Gomez | first source batch published under GPL-3.0-or-later; HDL matched to upstream pin; INTERPOL=0 |
| Pocket licensed subset | Pocket integration | plasticbugs template lineage; Marcus Andrade, OpenGateware / Raetro and original named contributors | 39 MIT/CC0 files previously published; ten GPL files now matched exactly to pinned public template, with headers retained |
| Remaining template / APF / vendor IP | Pocket integration and build glue | plasticbugs, Analogue, Intel/Altera and other contributors | held; public repository presence alone does not establish a redistribution grant |
| Pristine MAME tool-source selection | emulator source reference | original authors named in source headers | four exact pinned files published under BSD-3-Clause with full terms; modified observer sources and bundled runtimes held/excluded |

## Project-authored areas

The Macross-specific machine integration, NMK004/TLCS-90 work, renderers, temporal presenters, diagnostics, build glue, and verification tooling require file-by-file provenance confirmation before a project-wide license is applied.

## Publication rule

Do not remove or replace inherited copyright headers or license files. Do not assume that a repository-level license overrides third-party file licenses.

See [docs/LICENSING.md](docs/LICENSING.md).

Exact pins, selected paths, licensing evidence and the FX68K correction are recorded in [docs/PUBLICATION-BATCH-2.md](docs/PUBLICATION-BATCH-2.md). The full GPLv3 text is retained in [modules/cpu-fx68k/LICENSE](modules/cpu-fx68k/LICENSE), alongside the component grant in [fx68k.txt](modules/cpu-fx68k/fx68k.txt).

The separately cleared MAME source selection and its exact hashes are documented in [tools/mame/source/upstream/UPSTREAM.md](tools/mame/source/upstream/UPSTREAM.md).
