# Rebuilding missing or withheld components

Macross Ver.26 is being published conservatively. Some source and generated files are intentionally withheld until their redistribution rights, provenance, or vendor terms are fully resolved.

The purpose of this document is to show **what is already published, where the remaining gaps are, what each missing component does, and where a developer should look to obtain, regenerate, or replace it** without redistributing uncertain material.

This is not a substitute for each upstream license. Preserve all upstream notices and comply with the terms of the source you obtain.

## Publication rule

A file may be absent from this repository for one of four different reasons:

1. **User-supplied game data** — never distributed here.
2. **Third-party source awaiting license/provenance review** — may be publishable later once the applicable grant and modification history are confirmed.
3. **Vendor-generated FPGA/IP output** — may be better regenerated locally with the vendor toolchain than redistributed.
4. **Private engineering evidence or generated build output** — useful for preservation, but not part of the public source tree.

Do not treat an absent file as permission to copy it from an arbitrary mirror. Obtain it from the original author/vendor or implement an independently written compatible replacement.

As of the 2026-10-04 publication pass, additional cleared upstream material has been added to the repository. See [PUBLICATION-BATCH-2.md](PUBLICATION-BATCH-2.md) for the exact second-batch paths and provenance.

## Expected repository layout

Keep these relative paths when reconstructing a complete local build:

```text
rtl/
modules/
target/pocket/
platform/pocket/
projects/
pkg/pocket/
sim/
tools/
build-local.sh
package-pocket.py
```

The Quartus QSF/QIP hierarchy and build scripts depend on these relationships. Do not flatten or arbitrarily relocate dependencies.

## FX68K

**Role:** Motorola 68000-compatible CPU implementation.

**Published now:** the repository includes five upstream-cleared FX68K companion files under `modules/cpu-fx68k/`:

```text
LICENSE
fx68k.txt
microrom.mem
nanorom.mem
uaddrPla.sv
```

These files were matched exactly to the pinned upstream FX68K source by Jorge Cwik and are distributed under the applicable GPL-3.0-or-later terms.

Two files that may look like ROM data are actually part of the CPU implementation:

```text
microrom.mem
nanorom.mem
```

These are FX68K control tables, **not Macross game ROMs or firmware**. Keep them beside the FX68K source. Simulation scripts copy them into the run directory because the HDL loads them by bare filename.

Do not use a blanket `*.mem` exclusion when reconstructing the build.

**Still withheld:** the locally modified primary FX68K implementation and related files remain under review because their modification history is not yet documented accurately enough for publication. In particular:

- `modules/cpu-fx68k/fx68k.sv` contains local observer/timing and packed-typedef changes.
- `modules/cpu-fx68k/fx68kAlu.sv` contains local functional edits, including `OP_IDLE`-related changes.
- the previous local `UPSTREAM.txt` did not fully describe those modifications and is therefore not being published as authoritative provenance.

Until those edits are attributed and dated correctly, obtain pristine FX68K from the upstream project if an independent reconstruction requires it. Do not substitute the modified local files from an unreviewed copy.

## JT sound cores

**Role:** YM2203-compatible synthesis and OKI ADPCM playback.

Ver.26 uses JT-family components including:

- JT03 / JT49
- JT6295

The reviewed publication batch contains the unchanged JT HDL files and their license/provenance companions. All 51 published JT HDL files and the three included LICENSE files were independently rechecked against their recorded upstream pins during the second publication pass.

When using a different checkout, obtain the cores from their upstream project, retain their license files and notices, and keep the source paths expected by the project QIPs.

No additional unpublished JT files remain in the maintained module directories. Files in excluded upstream reference/check-out areas are not part of the published Ver.26 source tree.

## NMK004 / TLCS-90 sound controller

**Role:** reproduces the original Macross NMK004 sound-control path.

The maintained project implementation is **still withheld** pending a clear rights/contribution record and applicable licensing.

This is distinct from bootleg sound hardware. A replacement implementation must provide the same externally observed behavior expected by the Macross machine integration, including:

- reset and program execution behavior
- access to the external NMK004 program ROM supplied by the user
- access to the NMK004 internal firmware supplied by the user
- host-command and response handshakes with the 68000 side
- the observed `$FB00` / `$FC00` communication behavior used by Macross
- control of the YM2203-compatible and dual OKI audio paths
- timing sufficient to satisfy the Macross boot and sound-command sequences

Until the maintained implementation is cleared, use the surrounding public interfaces, architectural documentation, and upstream hardware references as a behavioral contract for an independently written compatible replacement. Do not copy a restricted implementation merely because its behavior is documented.

## Pocket platform and template code

**Role:** Analogue Pocket/openFPGA integration, memory glue, display processing, controls, packaging, and platform metadata.

The repository now contains both the original clearly licensed MIT/CC0 subset and an additional ten GPL-licensed Pocket platform files that were matched exactly to the pinned `plasticbugs/pocket-core-template` upstream source.

The second publication batch added:

```text
platform/pocket/audio/filters/audio_filters.sv
platform/pocket/audio/filters/audio_mix.sv
platform/pocket/audio/filters/dc_blocker.sv
platform/pocket/audio/filters/iir_filter.sv
platform/pocket/audio/filters/iir_filter_tap.sv
platform/pocket/support/hiscore.sv
platform/pocket/support/nvram.sv
platform/pocket/video/scanlines.sv
platform/pocket/video/scanlines_generator.sv
platform/pocket/video/shadowmask.sv
```

Their original GPL notices and contributor headers are retained. The preserved lineage includes plasticbugs, Marcus Andrade / OpenGateware / Raetro, Alexey Melnikov, Alan Steremberg, Jim Gregory, Till Harbaum, and other upstream contributors as named in the source files.

**Still withheld:** unheadered or otherwise unresolved template documentation, tools, configuration, package files, APF files governed by Analogue-specific terms, and any inherited file whose exact redistribution grant remains unclear.

When reconstructing locally:

- use the in-repository cleared Pocket files where present
- obtain any still-missing corresponding Pocket/openFPGA sources from their authoritative upstream project
- preserve all license and copyright notices
- keep the original relative paths
- compare against the Ver.26 QSF/QIP references before substituting newer platform code

A newer Pocket template may not be a drop-in replacement for the frozen Ver.26 build.

## MAME source references

**Role:** source-level behavioral reference for NMK16 hardware, ROM descriptors, device relationships, video behavior, and emulator-side machine structure.

The repository now includes four pristine MAME source files under `tools/mame/source/upstream/src/mame/nmk/`:

```text
nmk16.cpp
nmk16.h
nmk16_v.cpp
nmk214.h
```

These files were matched exactly to the pinned MAME upstream commit and retain their original BSD-3-Clause headers. The full BSD-3-Clause text and an upstream provenance note are included under:

```text
tools/mame/source/upstream/LICENSE-BSD-3-Clause
tools/mame/source/upstream/UPSTREAM.md
```

These are source-code references only. They are **not** game ROMs, firmware dumps, private captures, or MAME runtime binaries.

Adapted local MAME observer/debug source remains withheld until its authorship/modification provenance is documented separately.

## Intel / Altera generated IP and PLL files

**Role:** Pocket target clocks and FPGA megafunction/IP integration.

Required PLL/IP wrappers, QIP files, and related vendor-generated companions remain under review because their redistribution terms have not yet been established clearly enough for publication.

The preferred public reconstruction path is:

1. install the documented Quartus toolchain
2. recreate the required IP from its source parameters/configuration where those parameters can be distributed
3. regenerate the vendor output locally
4. place the resulting files at the exact paths referenced by the project QIPs

The frozen development environment used:

```text
Quartus Prime Shell 25.1std.0 Build 1129
```

The project used a local Docker image tagged:

```text
openfpgaos-quartus-full:latest
```

That tag alone is not a reproducible environment specification. A public container recipe or equivalent pinned toolchain description is still needed.

Do not assume that a generated `.qip`, `.v`, `.sv`, `.mif`, `.ppf`, or other vendor product is automatically redistributable merely because Quartus created it.

## build_id.mif

`target/pocket/build_id.mif` is generated build identity/timestamp data.

It is intentionally not source-controlled as a normal source dependency. Pocket pre-flow/checkBuildID tooling regenerates it. The frozen Stage26 integrity manifest may still record the historical file hash because it authenticates the saved production build.

A fresh build is expected to produce a different build identity.

## Project RTL and configuration

Macross-specific RTL, simulation files, scripts, configuration material, custom tools, and some adapted reference code remain under review because a clear rights-holder/contribution record still has to be attached to them.

For an independent NMK16 implementation, the useful public documentation is the behavioral contract rather than any withheld source text:

- 68000 address map and reset behavior
- graphics ROM regions and transform expectations
- background, sprite, text, and palette interfaces
- native timing and IRQ behavior
- NMK004 host protocol
- SDRAM/SRAM ownership and arbitration requirements
- Pocket presentation requirements
- verified Stage23–26 temporal-coherency behavior

The project documentation should be used as a reference for compatible behavior, not as a license to reproduce code that has not been cleared for redistribution.

## Current publication gap

The second publication pass cleared 14 previously held files: ten Pocket GPL files and four pristine MAME files. Five additional FX68K companion files that were already candidates for publication were also added with their license material.

A substantial portion of the complete Ver.26 maintained tree is still intentionally absent. The remaining held set includes project RTL, NMK004/TLCS-90 implementation, modified FX68K sources, unresolved template/APF material, Intel/Altera-generated IP, simulations, custom tooling, and other files whose grant or contribution history has not yet been established.

The public repository therefore remains **incomplete and not yet independently buildable** from source alone.

## Game ROMs and firmware

Game data is never supplied by this repository.

Users provide their own lawfully obtained source archives and build:

```text
Assets/mycore/common/macross.rom
```

The ROM-assembly README documents the exact member checks, concatenation recipe, final size, and SHA-256 without distributing copyrighted ROM contents.

Expected final image:

```text
5,980,704 bytes (0x5B4220)
SHA-256 209700c2b4d0722e39eb2c395f13fe08903aaf315e1cbac3fab78ddd3c903e59
```

## Verifying a reconstructed tree

Before treating a locally reconstructed tree as equivalent to Ver.26:

1. confirm every QSF/QIP referenced path resolves
2. preserve the frozen directory relationships
3. verify dependency versions and notices
4. regenerate vendor IP using the documented Quartus version
5. build the project rather than packaging stale fitted outputs
6. run the ROM-independent simulations/checks first
7. run ROM-dependent verification only with a user-supplied verified `macross.rom`
8. compare resulting behavior against the documented Stage23–26 validation record
9. do not claim bit-for-bit reproducibility unless the complete toolchain and generated-IP inputs are pinned

## For other NMK16 projects

This repository should be treated as a **hardware-family reference developed around Macross**, not as proof that every NMK16 title shares an identical machine.

When adapting it to another NMK16 game, establish that game's own:

- CPU and clock configuration
- memory map
- sound subsystem
- graphics layout and protection/decode path
- tile/sprite/text geometry
- palette organization
- IRQ/raster timing
- ROM map
- input map
- Pocket presentation requirements

Reuse interfaces and infrastructure where the hardware evidence supports it; do not assume Macross-specific behavior is universal across NMK16.

