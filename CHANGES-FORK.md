# Changes in this fork

Upstream: https://github.com/rolanddd-hu/HDR_DNG_Merger, tag `v1.0.0` (commit `008819e`).
This fork is distributed under the same license, GPL-3.0-or-later (see `LICENSE`).

## 2026-11-20 — no magenta in thin highlights (`src/core/MergeEngine.cpp`)

Feathering the per-quad weights (radius 8 quads) spreads a brighter frame's weight into quads where that
frame is clipped: thin bright lines such as mortar joints, boards, or sky between branches. A clipped green
photosite next to unclipped red and blue renders as magenta. After feathering, every frame except the
darkest now gets weight 0 in any quad where it is itself clipped (`vMax > clipThreshold`), before the
weights are normalized. Measured on 66 Sony A7S III brackets: 45–85 % fewer magenta pixels; the result
then matches Lightroom's own merge.

## 2026-11-21 — release packaging (`.github/workflows/release.yml`)

- Tags may carry a suffix (`v1.0.0-reok.1`): the check compares only the `1.0.0` part with `CMakeLists.txt`.
- The zip adds `licenses/` (each vcpkg dependency's copyright file), `CHANGES-FORK.md`, and `SOURCE.txt`
  (the repository URL and the exact commit the binaries were built from).
