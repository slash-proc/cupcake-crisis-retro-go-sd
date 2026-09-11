# Changelog

This file follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/) and
[Semantic Versioning](https://semver.org/spec/v2.0.0.html). Release tags must
match a section heading exactly (for example `v1.0.0`).

When you cut a release:

1. Move items from `[Unreleased]` into a new `## [vX.Y.Z] - YYYY-MM-DD` section.
2. Commit the changelog update.
3. Push the tag: `git tag vX.Y.Z && git push origin vX.Y.Z`

CI reads the matching section and uses it as the GitHub Release notes. Assets
attached to the release:

- `<binary>-<tag>.zip` — SD layout (`homebrews/Cupcake.bin` + `cupcake_assets.dat`)
- `<binary>-<tag>-debug.zip` — ELF + linker map

## [Unreleased]

### Added

- Port Cupcake Crisis as a GWHB homebrew on the Retro-Go SD template
  (ABI v2 / `gw_core_bridge`, embedded RGB565 art + ADPCM audio).

### Changed

- Package layout: single `/homebrews/Cupcake.bin` (audio embedded; no
  `cupcake_assets.dat` sidecar).
- Draw directly into the LCD buffer and play ADPCM from the embedded
  archive so the audio blob fits in RAM_EMU.
