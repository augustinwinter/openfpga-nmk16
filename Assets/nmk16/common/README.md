# Macross Ver.26 — ROM assembly

Macross Ver.26 requires a single `macross.rom` at:

```text
Assets/nmk16/common/macross.rom
```

This package includes no game ROM or NMK004 firmware. Supply your own lawfully obtained archives. The project does not distribute or link to copyrighted ROM archives.

## Inputs

Use Python 3 and the accompanying `build_macross_rom.py` helper.

Required archives:

- `macross.zip`: MAME `macross` set for **Super Spacefortress Macross (1992)**
- `nmk004.zip`: NMK004 device firmware archive containing `nmk004.bin`

Archive names are conventional; the helper validates exact member names, sizes and CRC32 values. Additional ZIP members are ignored.

## Build

```sh
python3 build_macross_rom.py "/path/to/macross.zip" "/path/to/nmk004.zip" --output macross.rom
```

On Windows, use `py -3` instead of `python3`.

A verified output is:

```text
5,980,704 bytes (0x5B4220)
SHA-256 209700c2b4d0722e39eb2c395f13fe08903aaf315e1cbac3fab78ddd3c903e59
```

Use `--check-only` to validate the source archives without writing an output file.

## Exact concatenation order

No byte swapping, interleaving, graphics decoding, header, padding or duplication is applied. Concatenate the members exactly as stored in the source ZIPs:

| Offset | Archive | Member | Length | CRC32 |
|---:|---|---|---:|---|
| `0x000000` | `macross.zip` | `921a03` | `0x080000` | `33318d55` |
| `0x080000` | `macross.zip` | `921a02` | `0x010000` | `77c082c7` |
| `0x090000` | `macross.zip` | `921a01` | `0x020000` | `bbd8242d` |
| `0x0B0000` | `macross.zip` | `nmk-215.bin` | `0x002000` | `d355a06f` |
| `0x0B2000` | `macross.zip` | `921a04` | `0x200000` | `4002e4bb` |
| `0x2B2000` | `macross.zip` | `921a07` | `0x200000` | `7d2bf112` |
| `0x4B2000` | `macross.zip` | `921a05` | `0x080000` | `d5a1eddd` |
| `0x532000` | `macross.zip` | `921a06` | `0x080000` | `89461d0f` |
| `0x5B2000` | `macross.zip` | `921a08` | `0x000100` | `cfdbb86c` |
| `0x5B2100` | `macross.zip` | `921a09` | `0x000100` | `633ab1c9` |
| `0x5B2200` | `macross.zip` | `921a10` | `0x000020` | `8371e42d` |
| `0x5B2220` | `nmk004.zip` | `nmk004.bin` | `0x002000` | `8ae61a09` |

Keep `921a03` and `921a07` exactly as stored in the ZIP even though MAME describes their loading with `ROM_LOAD16_WORD_SWAP`. Ver.26 expects the physical-ROM byte contract and does not pre-apply MAME region transforms.

## Install

Copy the verified result to:

```text
Assets/nmk16/common/macross.rom
```

The Pocket loads the assembled image; it does not run the Python helper or unpack ZIPs.

## Provenance

This recipe was verified against the preserved Ver.26 ROM reconstruction tooling and canonical aggregate image. The unfinished historical MRA template is not used as the assembly recipe.

