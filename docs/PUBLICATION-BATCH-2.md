# Publication batch 2: verified dependency companions

Reviewed 2026-10-04 against the maintained Macross Ver.26 tree and the prior publication inventory. Each of these 15 files preserves its exact relative path, bytes and original notices. No game payload is included. This remains an incomplete source publication, not a buildable integrated core or a project-wide license adoption.

## FX68K: five files

[ijor/fx68k at 0602ee4627b10f301298f2673d826cdd6baa9327](https://github.com/ijor/fx68k/tree/0602ee4627b10f301298f2673d826cdd6baa9327). All five files match the authoritative Git blob hashes. Jorge Cwik's complete GPL-3.0-or-later grant is retained in fx68k.txt; LICENSE supplies the full GPLv3 terms. microrom.mem and nanorom.mem are licensed CPU control tables, not arcade ROM or MCU firmware dumps.

## Pocket: ten files

[plasticbugs/pocket-core-template at c77563fa84bcc5754d5f1f6ba51168e8849f0e1d](https://github.com/plasticbugs/pocket-core-template/tree/c77563fa84bcc5754d5f1f6ba51168e8849f0e1d). All ten files match public upstream Git blob hashes exactly, resolving the prior local modification-lineage hold. Their original GPL grants/SPDX labels and copyright notices remain intact. SPDX labels say GPL-3.0-or-later; some video boilerplate explicitly says version 3. This publication is permitted under version 3 in either case, and does not rewrite that wording.

The template README and CREDITS identify OpenGateware's gateman-pocket lineage, Marcus Andrade and Raetro. The exact matching snapshot is the plasticbugs template; current opengateware/gateman-pocket main has an older layout and is not claimed as the byte-identical origin. The template and Time Pilot '84 credits corroborate platform authorship; they do not confer a blanket license on unheadered files. Preserve Marcus Andrade, OpenGateware authors/contributors, Alexey Melnikov, Alan Steremberg, Jim Gregory and Till Harbaum as named in each file. The full GPLv3 terms accompany this distribution in ../modules/cpu-fx68k/LICENSE and the existing JT component LICENSE files.

## Exact added source paths and hashes

| Path | SHA-256 | Git blob SHA-1 |
|---|---|---|
| `modules/cpu-fx68k/LICENSE` | `3972dc9744f6499f0f9b2dbf76696f2ae7ad8af9b23dde66d6af86c9dfb36986` | `f288702d2fa16d3cdf0035b15a9fcbc552cd88e7` |
| `modules/cpu-fx68k/fx68k.txt` | `2a7d451e8f7ae8683e4ec4f40a9b3adf91fb5c8b5d569c0f4cdb2b5de090811d` | `b9c3c5a4dced49ff317d05736176fa4bf2632f2d` |
| `modules/cpu-fx68k/microrom.mem` | `9d13082be0cf4b04bff887e6da23de84f9f2ee4321f3a2576b4f9540615dece6` | `22558e867b7b1665a5e605ce1b53c5cdf392d5d3` |
| `modules/cpu-fx68k/nanorom.mem` | `b3998009fb10605e8468cddf22fdd799a9792ba86f449de2e30615cfcefbeece` | `df7d74d970220878da97d5082590999cc2d171b2` |
| `modules/cpu-fx68k/uaddrPla.sv` | `07ceb3b1fbbd74f255c2a909151fe5efd38a575ba4f6aa47c6208050d2e27326` | `e24e951e3fb643a1894f278237aec2bc5b281375` |
| `platform/pocket/audio/filters/audio_filters.sv` | `156fc93a1c6a32dd42c3bd4af6da03323b7768eb422d22e3d21957a8bb12c57d` | `bcdbf6614d97caaa1c27d5175b4ca5ce3399355f` |
| `platform/pocket/audio/filters/audio_mix.sv` | `a97061c1b859a99e526563b3f70d72d0dcd51161f1f260e3e7ce6d30ea17d1d1` | `6b70b7dc0d80267cef4f7b30efe43b755b20f00d` |
| `platform/pocket/audio/filters/dc_blocker.sv` | `636dbda82fc0679320cb8b77d8df8bf5dac48b117eacea3be73d00f4a9d1411c` | `30cc92d6412d683c74bf9d82bb7edee7e1140413` |
| `platform/pocket/audio/filters/iir_filter.sv` | `384a7698bdf72529a039467c91004f51c1d9d94c8e760f706a9c531d06a35624` | `81e4b60ec225ff5a315200d621001412d07da53a` |
| `platform/pocket/audio/filters/iir_filter_tap.sv` | `69a6aaf626eeebe78e4612046ae116ea1a6b39243e96116bb12b30a396cf805e` | `7e9ca2353b192b17bbcc7532784538622ffadabc` |
| `platform/pocket/support/hiscore.sv` | `cd6f2beda8d189bf60043f610216d0a7dc68593affbb75cbd1aa07484f93261d` | `36979ac7ff47413d555573d6b72121b78c04e7e9` |
| `platform/pocket/support/nvram.sv` | `6d648b2049e57677bc94c79a395dd2eaa57ac6b8d93a8653995d1e1303907d8c` | `ee128c0c256f1386d719810e078b7001661528e3` |
| `platform/pocket/video/scanlines.sv` | `365c719ae09e4b7d7abd6181744c6a562582525812470158fff46bbc7ad44490` | `390c19797af24df4779e9106c94c6350d427dec6` |
| `platform/pocket/video/scanlines_generator.sv` | `39400cb09d4fee03014e8b58188369681e3214c3f932e25358c3b796a34a12eb` | `94a6536479f65af1f2b092f1121b0f9f218a99c3` |
| `platform/pocket/video/shadowmask.sv` | `b1738986d0f2a8d9fbba4528908ef73a3411e257808614b661cd37d9225056c4` | `e062b2db48114fc8591379721aed25cdec5b16fb` |

## Correction to prior FX68K clearance

The local fx68kAlu.sv is not pristine upstream. Besides line-ending changes, it adds OP_IDLE and two idle-column cases. It lacks a dated modification notice and a confirmed contribution record, so the earlier PUBLIC_OK classification is superseded by NEEDS_LICENSE_REVIEW. fx68k.sv also differs from upstream and stays held. UPSTREAM.txt says the only changes are three packed typedefs, which fails to describe the ALU edits; that inaccurate notice is held pending correction. None of these three files is silently replaced, modified or uploaded.

## Other holds

Unheadered template documents/tools/configuration/package metadata stay held despite exact public-template matches: the template has no root LICENSE and its README's general invitation to use files does not supply clear redistribution terms for each unheadered item. Macross-specific RTL, NMK004/TLCS-90, adapted source and local tools still need authorship/contribution grants. Analogue APF and Intel/Altera IP remain separately restricted or unresolved. ROMs, firmware dumps, private captures/media, private research and generated build products remain excluded.

## Existing JT companions

All 51 previously published HDL files and their three LICENSE files match their recorded authoritative upstream pins: jt12 dc9be7c1ff75d5b9a7f9d89da1b7fba212af1257; jt49 7f6abfd08a2af9a92dbd5b32c71ea773248a77e2; jt6295 7d76b0be8cd8f85f3ae741178c9830b20e2071a1. Their local UPSTREAM notices identify the same pins. The maintained modules contain no additional unpublished JT companions. Excluded ref/ material is not republished.
