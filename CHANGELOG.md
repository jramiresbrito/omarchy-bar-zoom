# Changelog

All notable changes to this project are documented here. The format follows
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and the project uses
[Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [0.1.0] - 2026-09-13

Initial release, developed against Omarchy 4.0.3-1.

### Added

- A replacement bar that renders at a per-monitor zoom factor, read from
  `bar.scaleByMonitor` in `shell.json`. The bar is laid out at its natural size
  and the whole panel is scaled, so glyphs and icons magnify together rather
  than the bar only gaining padding.
- A **BAR SIZE** row on Omarchy's Display panel that sets the zoom for the
  focused monitor, with mouse and keyboard navigation and the active factor read
  back from `shell.json`. Shipped in the same plugin, which declares both the
  `bar` and `bar-widget` kinds, so one install covers both halves.
- `tools/monitor-scale`: an optional script that sets the Hyprland scale of the
  focused monitor and persists it per output, rather than through Omarchy's
  desktop-wide catch-all rule.

### Known limitations

- Zoom is a render transform, so sharpness depends on the monitor's Hyprland
  scale. See `docs/limitations.md`.
- Popup anchoring on a zoomed monitor is computed in unscaled coordinates and
  can sit slightly off.

[Unreleased]: https://github.com/jramiresbrito/omarchy-bar-zoom/compare/v0.1.0...HEAD
[0.1.0]: https://github.com/jramiresbrito/omarchy-bar-zoom/releases/tag/v0.1.0
