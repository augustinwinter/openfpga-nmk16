<img width="522" height="165" alt="macross_arcade_banner" src="https://github.com/user-attachments/assets/a1944921-5a7d-4cf0-869f-b8f9744e9509" />

## Why this project exists

This started as an experiment in learning how to use ChatGPT and Codex as practical tools over a long, complicated technical project.

I wanted to do more than ask questions or generate bits of code. I wanted to see how far these tools could be pushed, where they would fail, and what kind of working method would make them genuinely useful. Recreating **Super Spacefortress Macross** on the Analogue Pocket turned out to be a very effective stress test.

Along the way, I learned that the hardest part was not necessarily raw technical capability. It was continuity, verification, context, and knowing when not to trust a plausible answer. We made bad assumptions, chased the wrong problems, rediscovered things we had already found, and occasionally came close to "fixing" something that was already working.

<img width="224" height="320" alt="20261005_225144" src="https://github.com/user-attachments/assets/3f0bf82d-bbed-414a-b35c-faba0f3395ce" />

The project eventually settled on a simple rule:

**OBSERVE → PROVE → EXPLAIN → CHANGE → RETEST**

I also learned that prompt wording worked best when it enforced process rather than asked for clever answers. Phrases like **“One terminal command at a time,” “Preserve the evidence,” “Do not reopen a closed checkpoint without contrary evidence,”** and especially **“Continue your work in an active window”** became part of the workflow.

<img width="224" height="320" alt="20261005_225150" src="https://github.com/user-attachments/assets/fb9bdfaf-d8e6-478c-9c51-cb805ecbbc2d" />

For continuity, ChatGPT became **Doctor Lucy van Pelt**, while Codex became **Jordan**. The names were partly a joke, but the roles helped create a nominal sense of accountability over a project that eventually spanned many conversations, migrations, checkpoints, and handoffs.

The full story, including the mistakes, workflow changes, context problems, migration packages, and what I learned about using AI as a technical collaborator, is here:

[Read the full project story](https://github.com/augustinwinter/openfpga-nmk16/blob/codex/publication-bootstrap/docs/PROJECT-STORY.md)

## Macross Ver.26 — Analogue Pocket release

Download [Macross-Ver26-Pocket.zip](https://github.com/augustinwinter/openfpga-nmk16/releases/download/0.26.0/Macross-Ver26-Pocket.zip) from the [0.26.0 release](https://github.com/augustinwinter/openfpga-nmk16/releases/tag/0.26.0). Copy `Cores/`, `Platforms/`, and `Assets/` from its enclosing `Macross-Ver26-Pocket/` folder to the SD-card root.

The Pocket platform ID is `mycore`: `Platforms/mycore.json`, `Platforms/_images/mycore.bin`, and `Assets/mycore/common/macross.rom`. ROM assembly instructions are in `Assets/mycore/common/README.txt`. For an existing installation, back up the card and Settings, install `Cores/August.Macross/`, and move the assembled ROM to the path above if needed. Remove superseded Macross core folders from active `Cores/` to avoid stale identities. Settings may be copied to `Settings/August.Macross/` after retaining a backup. Eject the card and check Arcade on the Pocket; rescan in Pocket Sync if used.

The game/core remains **Macross Ver.26**, with core folder `Cores/August.Macross/` and version `0.26.0`. Authorship and credits remain **August Wong / Doctor Lucy van Pelt / Codex Jordan**. The Pocket-tested identity is author `August`, shortname `Macross`, folder `August.Macross`, and platform ID `mycore`. This correction preserves version `0.26.0`, the ROM, banner, bitstream, controls, and audio/video metadata byte-for-byte; all Mac resource sidecars are omitted.

Current ZIP SHA-256: `e21c140ca7dbb03d8950d209a89a05e9e3b483c2a1ffd2d066367ac1e510c06b`. The release includes `Macross-Ver26-Pocket.zip.sha256` for verification. Bitstream SHA-256 remains `e71cdf822157772146f96bee032b1411cfb4b7e7051093ae2e346b91ed37513c`.

