# Changelog

This file follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/) and
[Semantic Versioning](https://semver.org/spec/v2.0.0.html). Release tags must
match a section heading exactly (for example `v1.0.0`).

When you cut a release:

1. Move items from `[Unreleased]` into a new `## [vX.Y.Z] - YYYY-MM-DD` section.
2. Commit the changelog update.
3. Push the tag: `git tag vX.Y.Z && git push origin vX.Y.Z`

CI reads the matching section and uses it as the GitHub Release notes. The tag
is also used in staged asset names (`<binary>-<tag>.bin`, `<binary>-<tag>.zip`).

## [v0.0.4] - 2026-09-13

### Changed

- Publish conservative runtime save and savestate support metadata for LFS sizing.

## [v0.0.3] - 2026-09-12

### Fixed

- The RetroFab licence now travels with the release. `assets/license.txt` is
  CC-BY-NC-ND and clause (g) requires the document be retained in its entirety
  when the work is redistributed, but v0.0.2 shipped `homebrews/Cupcake.bin`
  alone. It is now in the install zip as `Cupcake-license.txt` and attached to
  the release, through the shared `REDIST_DOCS` mechanism.
- The offline bundle carries every file the manifest names. `make_bundle.py`
  kept its own copy of the file list and had not learned about shipped games;
  nothing here ships one, so this release is unaffected in content.

## [v0.0.2] - 2026-09-11

### Added

- The project adopts the [GWRG distribution model](https://github.com/slash-proc/gwrg-dist-spec).
  A tagged release now carries a `manifest.json` describing what it installs
  and where, an offline bundle holding every file that manifest names, and a
  GitHub Pages mirror a web installer can fetch across origins.
- The shared dist scripts, taken verbatim from the canonical set:
  `make_manifest.py`, `build_dist.py`, `make_bundle.py` and `stage_release.py`.
  They read every project-specific value out of the Makefile, so they stay
  byte-identical across projects and a fix lands everywhere at once.
- `print-SIDECARS` and `print-RO_BIN`, which the staging step reads to find any
  extra device file installed beside the binary. This project has none; the
  targets exist so the shared script needs no per-project variant.
- `print-COVER_FULL`, so the unscaled `assets/screen.jpg` is published beside
  the release next to the 128x96 copy packed into the binary. A cover browser
  can then show art that is not limited to what fits in the header.

## [v0.0.1]

### Added

- Port Cupcake Crisis as a GWHB homebrew on the Retro-Go SD template
  (ABI v2 / `gw_core_bridge`, embedded RGB565 art + ADPCM audio).

### Changed

- Package layout: single `/homebrews/Cupcake.bin` (audio embedded; no
  `cupcake_assets.dat` sidecar).
- Draw directly into the LCD buffer and play ADPCM from the embedded
  archive so the audio blob fits in RAM_EMU.

### Install

- Unzip the release archive onto the SD card root (`homebrews/Cupcake.bin`).
- Requires firmware whose ABI matches `SDK_VERSION` in this repository.
