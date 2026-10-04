# Rebuilding missing or withheld components

Macross Ver.26 is being published conservatively. Some source and generated files are intentionally withheld until their redistribution rights, provenance, or vendor terms are fully resolved.

The purpose of this document is to show **where the gaps are, what each missing component does, and where a developer should look to obtain, regenerate, or replace it** without redistributing uncertain material.

This is not a substitute for each upstream license. Preserve all upstream notices and comply with the terms of the source you obtain.

## Publication rule

A file may be absent from this repository for one of four different reasons:

1. **User-supplied game data** — never distributed here.
2. **Third-party source awaiting license/provenance review** — may be publishable later once the applicable grant and modification history are confirmed.
3. **Vendor-generated FPGA/IP output** — may be better regenerated locally with the vendor toolchain than redistributed.
4. **Private engineering evidence or generated build output** — useful for preservation, but not part of the public source tree.

Do not treat an absent file as permission to copy it from an arbitrary mirror. Obtain it from the original author/vendor or implement an independently written compatible replacement.

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

**Expected area:** `modules/` under the existing FX68K layout.

**Where to look:** the upstream FX68K project by Jorge Cwik.

The maintained Ver.26 tree contains a local change to the primary FX68K source involving packed typedef handling. The exact upstream revision and the date/provenance of that local change must be recorded before the modified source is redistributed.

Two files that may look like ROM data are actually part of the CPU implementation:

```text
microrom.mem
nanorom.mem
```

These are FX68K control tables, **not Macross game ROMs or firmware**. Keep them beside the FX68K source. Simulation scripts copy them into the run directory because the HDL loads them by bare filename.

Do not use a blanket `*.mem` exclusion when reconstructing the build.

## JT sound cores

**Role:** YM2203-compatible synthesis and OKI ADPCM playback.

Ver.26 uses JT-family components including:

- JT03 / JT49
- JT6295

The reviewed publication batch contains the unchanged JT HDL files and their license/provenance companions. When using a different checkout, obtain the cores from their upstream project, retain their license files and notices, and keep the source paths expected by the project QIPs.

The publication review verified that the retained JT HDL matched the local upstream reference copies byte-for-byte. Exact upstream commit pins should remain documented in the repository provenance records.

## NMK004 / TLCS-90 sound controller

**Role:** reproduces the original Macross NMK004 sound-control path.

This is distinct from bootleg sound hardware. A replacement implementation must provide the same externally observed behavior expected by the Macross machine integration, including:

- reset and program execution behavior
- access to the external NMK004 program ROM supplied by the user
- access to the NMK004 internal firmware supplied by the user
- host-command and response handshakes with the 68000 side
- the observed `$FB00` / `$FC00` communication behavior used by Macross
- control of the YM2203-compatible and dual OKI audio paths
- timing sufficient to satisfy the Macross boot and sound-command sequences

If the maintained project implementation is still withheld, use the surrounding public RTL, simulation interfaces, architectural documentation, and MAME/NMK hardware documentation as an interface contract for an independently written replacement. Do not copy a restricted implementation merely because its behavior is documented.

## Pocket platform and template code

**Role:** Analogue Pocket/openFPGA integration, memory glue, display processing, controls, packaging, and platform metadata.

The first publication batch includes platform files whose MIT/CC0 status was clear. Other inherited template/platform files remain on hold where their exact contribution scope, modification status, or license obligations need confirmation.

When reconstructing locally:

- obtain the corresponding Pocket/openFPGA template/platform sources from their upstream project
- preserve all license and copyright notices
- keep the original relative paths
- compare against the Ver.26 QSF/QIP references before substituting newer platform code

A newer Pocket template may not be a drop-in replacement for the frozen Ver.26 build.

## Intel / Altera generated IP and PLL files

**Role:** Pocket target clocks and FPGA megafunction/IP integration.

Some required PLL/IP wrappers and QIP files remain under review because they were generated by Intel/Altera tooling or are associated with restricted-license source material.

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

Some Macross-specific RTL, simulation files, scripts, and configuration material remain under review because a clear rights-holder/license record still has to be attached to them.

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

## Game ROMs and firmware

Game data is never supplied by this repository.

Users provide their own lawfully obtained source archives and build:

```text
Assets/mycore/common/macross.rom
```

The ROM-assembly README and helper document the exact member checks, concatenation recipe, final size, and SHA-256 without distributing copyrighted ROM contents.

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
