# Optional tools

Not part of either plugin, and not installed by `omarchy plugin add`. These are
standalone scripts kept here because they solve neighbouring problems on the same
mixed-DPI setup.

## `monitor-scale`

Sets the Hyprland scale of the **focused** monitor and makes it persist, one
output at a time.

Omarchy's own `omarchy-hyprland-monitor-scaling` applies a scale at runtime and
then persists it by rewriting the catch-all rule (`output = ""`) in
`monitors.lua` — a rule that governs every monitor at once. So changing one
display moves the other, and if you have replaced that catch-all with per-output
rules, there is nothing for it to write and the change rolls back on the next
reload.

`monitor-scale` writes the scale onto the focused output's own rule instead.

**Requires** `~/.config/hypr/monitors.lua` to carry one `hl.monitor` rule per
output, each on a single line:

```lua
hl.monitor({ output = "eDP-1", mode = "3840x2400@59.994", position = "auto", scale = 2 })
hl.monitor({ output = "DP-7", mode = "1920x1080@165.00301", position = "auto", scale = 1 })
```

**Install**

```bash
install -Dm755 tools/monitor-scale ~/.local/bin/monitor-scale
```

**Use**

```bash
monitor-scale up      # next preset (1, 1.25, 1.6, 2, 3, 4)
monitor-scale down
monitor-scale 1.6     # exact factor, rounded to one Hyprland accepts
```

Bind it over Omarchy's own scaling keys in `~/.config/hypr/bindings.lua` if you
want them to persist per output:

```lua
hl.unbind("SUPER + SLASH")
hl.unbind("SUPER + ALT + SLASH")
o.bind("SUPER + SLASH", "Monitor scaling up", "monitor-scale up")
o.bind("SUPER + ALT + SLASH", "Monitor scaling down", "monitor-scale down")
```
