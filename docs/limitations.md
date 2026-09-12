# Limitations

## Zoom sharpness depends on the monitor's scale

This plugin magnifies the bar at render time rather than laying it out at a larger
font size. How sharp the result looks therefore depends on how many real pixels
the monitor gives the bar surface to begin with.

| Hyprland scale | Bar is rasterised at | Zoomed to 1.4x |
|---|---|---|
| 2 | 2x device pixels | ~1.43x more real pixels than the layout needs — stays crisp |
| 1 | 1x device pixels | nothing spare, pixels are interpolated — text softens |

A monitor at scale 2 is already drawn at double resolution, so magnifying the
bar eats into that surplus without exhausting it. A monitor at scale 1 is drawn
at exactly its display size, so zooming is the same operation as enlarging a
photograph.

**In practice:** zoom HiDPI monitors, leave scale-1 monitors at `1.0`. That is
usually what you want anyway — a scale-1 monitor is typically the one whose bar
already looks right.

Making the bar genuinely sharp at any scale would mean the bar widgets laying
text out at a larger font size rather than being magnified. Since `Style` is a
singleton, that requires a per-screen font size threaded through every bar
widget — roughly ten plugins, each then forked. That trade was not worth it here.

## Popup anchoring on a zoomed monitor

Tooltip and popup anchor positions are computed in unscaled item coordinates, so
on a zoomed monitor they can sit slightly off. Nothing is unusable, but it is a
known rough edge.

## Forks, not extensions

Omarchy's plugin system loads a whole bar or widget from a plugin folder; there
is no hook to patch one property of a built-in. This plugin is therefore a fork of two
Omarchy 4.0.3 components. While it is enabled, upstream changes to the bar and
the Display panel do not reach you.

The diffs are kept as small as possible so rebasing onto a newer Omarchy is
mostly a matter of re-applying them:

- **Bar.qml** — a `barScaleFor(screen)` lookup, a wrapper item with a `Scale`
  transform, and the panel's `implicitWidth`/`implicitHeight`.
- **Panel.qml** — a `barZoomValues` list, section plumbing for a `barzoom`
  section, a `BarZoomPill` component, the UI block, and two `Process` items to
  read and write the value.
