<p align="center">
  <img src="assets/extension_icon.png" width="128" height="128" alt="Screen Mirror Extension Icon" />
</p>

<h1 align="center">Niri Monitors</h1>

<p align="center">
  <b>A Vicinae extension to manage connected displays on the Niri Wayland compositor.</b>
</p>

## Overview

Manage your connected displays without leaving the launcher. Turn monitors on or off, switch resolutions, adjust scale, and rotate a display — all from a single command, built for Vicinae for Niri window manager.

## Features

- See every connected monitor at a glance, with its model, resolution, refresh rate, current rotation, and scale
- Make quick, one-off changes that apply immediately and reset on restart
- Save settings that persist across restarts, written directly to your niri config
- Turn any monitor on or off
- Power off every monitor at once
- Adjust display scale, resolution and rotation
- Dedicated shortcuts for every single action
- Copy a monitor's name, model, or resolution to the clipboard

## Quick Demo
https://github.com/user-attachments/assets/6302b70b-04a1-49bf-ba45-bd890d7d7122

## Usage

Install **Niri Monitors** from Vicinae Extension Store then run **Monitor Settings** in launcher to see a list of your connected displays. Each row shows the monitor's current rotation and scale at a glance, so you can check your setup without opening the action panel.

Select a monitor to choose between two ways of changing its settings:

### Quick actions

Runtime-only changes that apply instantly via `niri msg` and reset the next time niri restarts. Good for testing a setting or a temporary change.

> **Note:** Quick actions apply directly to your active session and **take precedence over saved configuration** until you restart or reload Niri.

| Action                   | Shortcut          |
| ------------------------ | ----------------- |
| Enable / disable monitor | `Cmd + D`         |
| Set scale                | `Cmd + S`         |
| Rotate display           | `Cmd + R`         |
| Set resolution           | `Shift + R`       |
| Refresh list             | `Cmd + Shift + R` |
| Power off all monitors   | `Cmd + Shift + P` |
| Copy monitor name        | `Cmd + C`         |
| Copy model               | `Shift + C`       |
| Copy resolution          | `Cmd + Shift + C` |

> **Note** The enable/disable action only appears when more than one monitor is connected, since you can't disable your only display.

### Edit Persistent Settings

Opens a form to set resolution, scale, rotation, and (with more than one monitor connected) enabled state. Submitting asks for confirmation, then writes an `output "<name>" { ... }` block into your niri config file — creating it if one doesn't exist yet, or updating just that monitor's block if it does. Everything else in your config file is left untouched.

niri live-reloads its config on save, so the change applies immediately with no restart needed. If the write ever produced invalid config, niri keeps your last working configuration and shows its own notification rather than breaking your session.

## How it works

Quick actions run entirely through niri's IPC interface (`niri msg`). Persistent settings are written straight to your niri config file, found in the same place niri itself looks: the `$NIRI_CONFIG` environment variable if set, otherwise `$XDG_CONFIG_HOME/niri/config.kdl`, falling back to `~/.config/niri/config.kdl`.

## Development

```bash
npm install
npm run dev    # Development mode
npm run build  # Production bundle
```

## Links

- [Niri](https://github.com/YaLTeR/niri) — A scrollable Window Manager for Wayland.
- [Vicinae](https://www.vicinae.com/) — A focused Application Launcher for your Desktop.
