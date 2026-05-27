# Mac Framez v2.0

**Mac Framez** is a fast, native macOS app for AI-powered slow motion video interpolation. Built on RIFE and FFmpeg, it turns any video into buttery smooth slow motion — up to 8x frame interpolation, batch queue, two complete UI themes, After Effects integration, and a full setup wizard. Built by [@MythVfxx](https://x.com/MythVfxx).

---

## What's New in v2.0

### 🎬 Rendering
- **8x interpolation** — added a third RIFE pass for extreme slow motion on top of 2x and 4x
- **Queue drag reorder fixed** — render order now actually respects the order you set
- **Metadata loading fixed** — background thread loading, format-level duration fallback, no more "Error loading metadata" on MKV or certain MP4s

### 🧙 Onboarding & Setup
- **Setup wizard** — 5-page first-run guide with download buttons, copy-able terminal commands, RIFE binary picker built in, and a live dependency checker with green/red status per item
- **RIFE path picker** — browse and validate your RIFE binary in Settings → RIFE Engine
- **Dependency health check** — runs silently every launch and logs warnings if anything is missing

### 💥 Crash Logging
- Unhandled exceptions caught and written to `~/Library/Logs/MacFramez/crash.log`
- User-facing dialog shows the error and log path when a crash happens
- Log auto-rotates at 512KB
- Settings → Crash Log → Open log folder / Clear log

### 🎨 UI & Themes
- **Nova theme** — default dark animated gradient, refined and optimised
- **Forge theme** — completely separate UI layout: warm industrial browns, monospace typography, table-style queue, tabbed right panel. Built in `ui_frame.py` — not just a recolor
- **Theme switcher** — Settings → Preferences → UI Theme → Nova or Forge, restart to apply
- **Performance** — background animation cut from 62fps to 20fps, orb count 5→3, shadow blur halved. Much lighter at idle

### ⏰ Scheduling
- **At specific time** — hour/minute/AM PM picker with live countdown
- **When CPU is idle** — pick a threshold (15–50%) and sustained duration (30 sec to 5 min) with live CPU indicator

### 📦 Presets
- **Import/export** — share presets as `.macframez_preset` JSON files
- Overwrites warning when importing over an existing preset

---

## After Effects Bridge

The AE bridge has been completely rebuilt in v2.0. Two versions are included in the `AE_Bridge/` folder.

### What it does
Send footage directly from After Effects → Mac Framez renders it → auto-imports the result back into your AE project. No manual file management.

### Option A — CEP HTML Panel (recommended)
A proper docked panel inside After Effects with the full Mac Framez dark UI. Always available in Window → Extensions → Mac Framez Bridge.

**Install:**
```bash
cp -r AE_Bridge/CEP_Panel ~/Library/Application\ Support/Adobe/CEP/extensions/MacFramez_Bridge
defaults write com.adobe.CSXS.11 PlayerDebugMode 1
# AE 2025+: use CSXS.12 instead
```
Restart After Effects → Window → Extensions → Mac Framez Bridge.

### Option B — JSX Script
A `.jsx` script that runs from File → Scripts. Same features, native AE dialog styling. Good if you don't want to install a CEP extension.

**Install:** Copy `AE_Bridge/mac_framez_bridge.jsx` to:
```
/Applications/Adobe After Effects [version]/Scripts/
```

### Bridge Features (v2.0)
- **MacFramez folder picker** — browse once, saved to preferences permanently
- **3-way source mode** — Active comp / Pick specific layer / Browse for file
- **Layer picker** — dropdown lists all footage layers in the comp by index and name
- **Work area / in-out range** — send only the comp work area instead of the full clip
- **Render settings** — set multiplier (2x/4x/8x), slow motion mode, and format right in the bridge
- **Preset picker** — reads your `presets.json` and lets you pick a saved preset before sending
- **Place in comp** — auto-places the result back in the original comp at the source timecode after import
- **Live progress** — shows render stage and percentage while Mac Framez is running
- **All settings persist** — everything saves between sessions

### How to use the bridge
1. Set your **MacFramez folder path** (browse to `rife_app_full`)
2. Choose your **source** — active comp, specific layer, or browse for a file
3. Set **multiplier**, **slowmo**, and **format**
4. Optionally pick a **preset**
5. Hit **Send to Mac Framez →**
6. Mac Framez opens, renders, and auto-imports the result back

---

## Features

| Feature | Description |
|---------|-------------|
| 2x / 4x / 8x RIFE | Three-pass AI frame interpolation |
| Batch queue | Drag & drop multiple files or folders |
| Per-file settings | Right-click any queue item to override settings |
| Slowmo modes | Normal, 2x, 4x, 8x |
| Output formats | MP4, MKV, MOV, AVI, WebM, ProRes, PNG/JPG Sequence |
| Hardware accel | Apple VideoToolbox |
| Presets | Save, load, import, export |
| Scheduling | By time or CPU idle |
| History | SQLite DB, search, re-run |
| AE Bridge | Full round-trip CEP panel + JSX script |
| Two themes | Nova (dark) + Forge (industrial) |
| Crash logging | Auto-saved to ~/Library/Logs/MacFramez/ |
| Auto-updater | Checks GitHub releases on launch |

---

## Installation

### DMG (recommended)
1. Download `MacFramez_v2.0.dmg`
2. Drag **Mac Framez** to Applications
3. Open — the setup wizard guides you through the rest
4. Only thing needed separately: the **RIFE binary** (wizard links directly to it)

### From source
```bash
# 1. Homebrew (if needed)
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# 2. ffmpeg
brew install ffmpeg

# 3. Python packages
pip3 install PySide6 psutil --break-system-packages

# 4. RIFE binary — https://github.com/nihui/rife-ncnn-vulkan/releases
# Download macOS build, unzip anywhere, set path in Settings → RIFE Engine

# 5. Run
python3 main.py
```

---

## Themes

| Theme | Look |
|-------|------|
| **✦ Nova** | Dark animated gradient, purple accent, glowing cards |
| **⬛ Forge** | Industrial browns, monospace, table queue, tabbed panels |

Switch in **Settings → Preferences → UI Theme**, restart to apply.

---

## Crash Reporting

Log location: `~/Library/Logs/MacFramez/crash.log`
Also: **Settings → Crash Log → Open log folder**

Report bugs to [@MythVfxx on X](https://x.com/MythVfxx) with the crash log attached.

---

## Credits

- **RIFE** — Zhewei Hu et al., ncnn Vulkan port by [nihui](https://github.com/nihui/rife-ncnn-vulkan) — MIT License
- **FFmpeg** — https://ffmpeg.org — LGPL/GPL
- **PySide6** — Qt for Python — LGPL

---

Built by **[@MythVfxx](https://x.com/MythVfxx)** — follow for updates.

*Mac Framez is free and not affiliated with Adobe, RIFE, or FFmpeg.*
