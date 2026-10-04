# ROM contract

Game ROM data is not distributed with this project.

The user supplies a lawfully obtained assembled input file named:

```text
macross.rom
```

Expected size:

```text
5,980,704 bytes
```

Expected SHA-256 for the frozen Ver.26 baseline:

```text
209700c2b4d0722e39eb2c395f13fe08903aaf315e1cbac3fab78ddd3c903e59
```

Expected Pocket SD-card path:

```text
Assets/mycore/common/macross.rom
```

## Byte layout

| Offset | Size | Content |
|---:|---:|---|
| 0x000000 | 0x80000 | 68000 program |
| 0x080000 | 0x10000 | NMK004 external program |
| 0x090000 | 0x20000 | text graphics |
| 0x0B0000 | 0x2000 | NMK215 / protection data |
| 0x0B2000 | 0x200000 | background graphics |
| 0x2B2000 | 0x200000 | sprite graphics |
| 0x4B2000 | 0x80000 | OKI sample bank 1 |
| 0x532000 | 0x80000 | OKI sample bank 2 |
| 0x5B2000 | 0x100 | horizontal timing PROM |
| 0x5B2100 | 0x100 | vertical / IRQ timing PROM |
| 0x5B2200 | 0x20 | color PROM |
| 0x5B2220 | 0x2000 | NMK004 internal ROM |

The inherited `mycore.mra` is an unfinished template and is **not** an authoritative Macross ROM assembly recipe.

A public reconstruction tool or fully reviewed recipe may be added later. Until then, this document describes the frozen input contract only.
