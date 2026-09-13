# Changelog

All notable changes to this project are documented here. The format follows
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and the project uses
[Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [0.2.0] - 2026-09-13

Makes the plugin a single answer for both per-monitor settings. 0.1.0 shipped the
per-monitor bar size, but left per-output monitor scaling to a standalone script
the user installed by hand, so the Display panel's own SCALE row still used
Omarchy's desktop-wide behaviour. The two disagreed on a per-output config: the
keybinding persisted a scale, the panel did not.

### Added

- `bin/monitor-scale` now ships **inside** the plugin, resolved relative to the
  plugin folder the same way `bin/bar-zoom` already was. Nothing to install by
  hand and nothing required on `PATH`.

### Changed

- The Display panel's **SCALE** row writes the scale onto the focused output's
  own rule in `monitors.lua`, so a per-monitor scale survives a reload the way
  BAR SIZE does. On a stock `monitors.lua`, where there is no per-output rule to
  edit, the helper hands back to `omarchy-hyprland-monitor-scaling` and the row
  behaves exactly as it did before — stock setups are unaffected.
- `GDK_SCALE` is deliberately no longer rewritten when scaling a monitor. It is a
  single global value that cannot describe two monitors at different scales, so
  whatever it is pinned to stays pinned.

### Removed

- `tools/`. Its only occupant, `monitor-scale`, is now part of the plugin.

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
- `monitor-scale`: a script that sets the Hyprland scale of the focused monitor
  and persists it per output, rather than through Omarchy's desktop-wide
  catch-all rule. Shipped alongside the plugin in this release; bundled into it
  in 0.2.0.

### Known limitations

- Zoom is a render transform, so sharpness depends on the monitor's Hyprland
  scale. See `docs/limitations.md`.
- Popup anchoring on a zoomed monitor is computed in unscaled coordinates and
  can sit slightly off.

[Unreleased]: https://github.com/jramiresbrito/omarchy-bar-zoom/compare/v0.2.0...HEAD
[0.2.0]: https://github.com/jramiresbrito/omarchy-bar-zoom/releases/tag/v0.2.0
[0.1.0]: https://github.com/jramiresbrito/omarchy-bar-zoom/releases/tag/v0.1.0
