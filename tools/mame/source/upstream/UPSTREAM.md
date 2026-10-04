# Pristine MAME tool-source selection

Reviewed and published 2026-10-04. These four files match [mamedev/mame at f34f02505e32c1993c6a782b6814232cbfc74e36](https://github.com/mamedev/mame/tree/f34f02505e32c1993c6a782b6814232cbfc74e36) exactly. Local paths under tools/mame/source/upstream/src/mame/nmk/ are preserved. No source from excluded ref/ or private bundles is copied.

Each file carries its original BSD-3-Clause identifier and copyright-holders line. The accompanying [LICENSE-BSD-3-Clause](LICENSE-BSD-3-Clause) is an exact copy of that upstream commit's docs/legal/BSD-3-Clause, Git blob cc9ab753198e41128dc651e0adb4f5e8c1be932a. Its generic placeholder refers to the actual rights holders recorded in the unchanged source headers, reproduced below for convenience.

- nmk16.cpp, nmk16.h, nmk16_v.cpp: Mirko Buffoni, Nicola Salmoria, Bryan McPhail, David Haywood, R. Belmont, Alex Marshall, Angelo Salese, Luca Elia; thanks to Richard Bush.
- nmk214.h: Sergio Galiano.

These are emulator source files, not executable distributions, firmware or ROM dumps. ROM_LOAD entries describe external file identities and checksums; small MCU-response/bit-permutation tables express emulator behavior. No game payload, capture or private witness accompanies them. This selection does not build MAME independently: obtain the rest of MAME from the pinned upstream repository.

The corresponding files under ../modified/, observer.patch, build/launcher recipes and local provenance documents remain held for contribution/license records or private-path review. This publication does not imply that a fresh MAME build was performed or clear the bundled runtime.

| Local source path | Upstream path | SHA-256 | Git blob SHA-1 |
|---|---|---|---|
| `tools/mame/source/upstream/src/mame/nmk/nmk16.cpp` | `src/mame/nmk/nmk16.cpp` | `3996a3d59d138c9db8c3b4ec44ac102cc446e835d9c61ad0a2ac29db8c9bc5f9` | `9d06ff164499d1c47462bb081ab6b2a2da1a4b60` |
| `tools/mame/source/upstream/src/mame/nmk/nmk16.h` | `src/mame/nmk/nmk16.h` | `b67d2548cf5761b90bc0992e925d18e19f25119206cc532aa5d2064b966a56b9` | `bf7138bafbea61bd98d2181b02674b46f3f655a7` |
| `tools/mame/source/upstream/src/mame/nmk/nmk16_v.cpp` | `src/mame/nmk/nmk16_v.cpp` | `467d82ae5cd65334ee4c1f5aa20632bdcf2b598a9ce5f84dfeff8adeee7be17f` | `ed83e81e1e5f7ef4892b19a5970e16575347f1cd` |
| `tools/mame/source/upstream/src/mame/nmk/nmk214.h` | `src/mame/nmk/nmk214.h` | `8d073bc0564d7b3a497425f78d30444ffc9ce4f812a95ae0d7934209baecc06d` | `4a105bf029e9a362f0ba43191dd06e0fcb3e1c29` |
