# Contributing

Thanks for taking a look. This is a small project with a narrow purpose, so the
bar for changes is mostly: does it keep the forks minimal, and does it still
validate?

## Before you open a pull request

Both plugin folders must pass Omarchy's own validator, which mirrors the checks
the running shell enforces:

```bash
omarchy plugin validate .
```

The repository also has a validator that runs without Omarchy installed, and is
what CI runs:

```bash
./scripts/check
```

## Testing a change locally

Install from your working copy rather than from git, so you can iterate:

```bash
cp -r . ~/.config/omarchy/plugins/io.github.jramiresbrito.bar-zoom
omarchy plugin enable io.github.jramiresbrito.bar-zoom
```

Saving a file under `~/.config/omarchy/plugins/` reloads plugin code
automatically. QML changes to an already-loaded plugin sometimes need a full
restart:

```bash
omarchy restart shell
```

Check the journal for QML errors after a change — they do not always surface on
screen:

```bash
journalctl --user --since "1 minute ago" | grep -iE "\.qml:|error"
```

## Keeping the forks small

The plugin is a fork of two Omarchy components, which is the part that ages badly.
Every line that differs from upstream is a line to re-apply when Omarchy moves,
so please keep additions surgical and comment *why* rather than *what* — the
surrounding code is someone else's and the reader needs to know which parts are
ours.

`docs/limitations.md` lists the current diff against upstream. Update it if your
change adds to that surface.

## Style

`.editorconfig` covers whitespace. Otherwise match the surrounding Omarchy code:
two-space indentation in QML and shell, comments that explain the reasoning, and
no trailing whitespace.
