# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A single-file [sunsetr](https://github.com/psi4j/sunsetr) configuration (`sunsetr.toml`)
checked out **directly into `~/.config/sunsetr`**. The repo root *is* the live config directory,
so editing `sunsetr.toml` here edits the running config. Docs:
https://github.com/psi4j/sunsetr/blob/main/docs/src/SUMMARY.md

sunsetr is the blue-light filter on this machine, used **instead of Omarchy's hyprsunset**. It is
started by the Hyprland config (`~/.config/hypr/autostart.lua`, in the
[hypr repo](https://github.com/anwarahmed/hypr)), not by this repo. Omarchy ships no sunsetr
config, so nothing overwrites this file on `omarchy-update`.

## Commands

```sh
sunsetr status                 # current runtime state (period, temperature, gamma)
sunsetr get night_temp         # read a field
sunsetr set night_temp=3500    # write a field to sunsetr.toml (rewrites the file)
sunsetr test 3500 90           # preview a temperature and gamma without saving
sunsetr restart                # reload: stop and start a fresh instance
sunsetr --simulate <start> <end> [mult]   # dry-run a transition with simulated time
sunsetr geo                    # pick a location and write latitude/longitude
```

`sunsetr set` and `sunsetr geo` rewrite `sunsetr.toml`, so check `git diff` afterwards. The
file's inline comments carry each field's valid range. Keep them when editing.

## Settings that matter

- `transition_mode = "geo"`: sunset and sunrise come from `latitude`/`longitude` (Toronto). The
  `[Manual transitions]` times and the `[Static config]` values are ignored in this mode.
- `night_temp` and `day_temp` are deliberately warmer than sunsetr's defaults (the comment on
  `night_temp` records the default). Gamma was changed and reverted once (#4, #5), so
  `night_gamma = 90` is a settled choice.
