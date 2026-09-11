# Cupcake Crisis — Retro-Go SD GWHB homebrew

Port of [osirisad/retro-go-bart-simpsons-cupcake-crisis](https://github.com/osirisad/retro-go-bart-simpsons-cupcake-crisis)
onto the freestanding [Retro-Go SD](https://github.com/sylverb/game-and-watch-retro-go-sd)
homebrew template (`PROJECT_KIND=homebrew`, ABI v2 + `gw_core_bridge`).

Game logic and assets originate from the RetroFab simulation by Itizso
(see `assets/license.txt` / `LICENSE.CUPCAKE`).

## Install

| File | SD path |
|------|---------|
| `Cupcake.bin` | `/homebrews/Cupcake.bin` |

Graphics and audio are embedded in the `.bin` — no sidecar `.dat` needed.
Optional cover override: `/covers/homebrew/Cupcake.img`.

When redistributing builds, include `assets/license.txt` (RetroFab
CC-BY-NC-ND terms).

## Build

Requires a Retro-Go SD firmware that loads **GWHB** homebrews (ABI v2+).

```bash
make                    # PROJECT_KIND=homebrew is the default
# or without a local ARM toolchain:
make docker
```

Produces `Cupcake.bin`.

Host SDL preview (same `app_main`, embedded assets — no G&W flash cycle):

```bash
make host                       # SDL2 → ./cupcake_host
make host HOST_SDL=3            # SDL3
./cupcake_host                  # Esc / close window to quit
```

On macOS, if `pkg-config sdl2` fails:

```bash
export PKG_CONFIG_PATH="$(brew --prefix)/lib/pkgconfig:${PKG_CONFIG_PATH:-}"
```

Controls: arrows = D-pad, `Z`/`X` = B/A, Enter = Start, Shift = Select.
Scale with `HOST_SCALE=2` (default).

Optional SD session trace (bring-up only):

```bash
make CUPCAKE_TRACE_SD=1
```

## About the game

**Bart Simpson's™ Cupcake Crisis** (Acclaim Entertainment, SuperPlay model
40214, 1990). Move Bart left/right to catch cupcakes; hand them to Marge
with Action; sit on the couch when Homer appears. Three lives.

## Credit

Unofficial fan project; not affiliated with Acclaim, Fox, or the original
authors. Upstream port by osirisad; this tree packages it as a standard
GWHB binary for Retro-Go SD.
