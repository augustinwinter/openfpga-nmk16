# Build and reproduction

## Maintained entry points

```sh
sh build-local.sh map
sh build-local.sh
```

The full build performs the timing gate and packages the Pocket release tree.

`python3 package-pocket.py` can package an already fitted build; it is not a substitute for recompiling after HDL or constraint changes.

## Toolchain used for Ver.26

- Quartus Prime Lite **25.1std.0 Build 1129**
- Docker image tag: `openfpgaos-quartus-full:latest`
- Verilator **5.052**
- C++ compiler/toolchain
- Make
- Python 3 for packaging/validation helpers

The local Docker image was verified during project consolidation, but a fully pinned public image digest and public reconstruction recipe still need publication review.

## ROM-free validation

The repository should support source-only syntax, structural, and regression checks without redistributing game content. Tests requiring private ROM data or reference captures must remain outside the public repository unless replaced with lawful synthetic fixtures.

## Reproducibility status

The frozen Ver.26 bitstream and package hashes are historical authorities. A fresh public checkout should not be described as bit-for-bit reproducible until the source snapshot, exact toolchain, build environment, and packaging metadata have all been pinned and independently rebuilt.
