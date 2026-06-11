# KPV Parameter Editor

A browser-based SysEx parameter editor for the **KORG KAOSS PAD V**.  
No installation required — open `index.html` in any modern browser with Web MIDI support (Chrome recommended).

> **Disclaimer:** This is an unofficial, community-developed tool and is not affiliated with or endorsed by KORG Inc.  
> Use at your own risk. The author assumes no responsibility for any damage to your device or data loss resulting from the use of this software.

## Features

- **FX** — Edit parameters for all 5 FX slots. Each slot remembers its algorithm independently.
- **LFO / EG / EF** — Full parameter control for all modulation units.
- **Mixer** — Level and routing parameters for all 5 FX slots.
- **VP (Virtual Patch)** — 32-patch modulation routing with source, destination, intensity, and polarity.
- **VP Curve (Mapper)** — Graphical editor for the VP Mapper curve. Click to add points, drag to move, right-click to delete.
- **Librarian** — Import `.preset` files, browse loaded presets, and send them to the device.
- **DSP Usage meter** — Real-time DSP load bar in the header. Algorithms that would exceed 101% are dimmed and disabled.
- **Send All / Send 1 Tab** — Send all edited parameters at once, or only the current tab.

## Requirements

- Chrome (or any Chromium-based browser) with Web MIDI API enabled
- KORG KAOSS PAD V connected via USB MIDI

## Usage

1. Connect your KAOSS PAD V via USB.
2. Open `index.html` in Chrome.
3. Select the MIDI output port for your device.
4. Edit parameters — changes are sent to the device in real time via SysEx.

To load a preset: go to the **Lib** tab, click **Import**, select a `.preset` file, then click **Load**.

## SysEx Protocol

| Message | Format |
|---------|--------|
| VE Parameter Change (Func 71) | `F0 42 3g 00 01 79 71 <idx×3> <float×5> F7` |
| VE Mapper Change (Func 72) | `F0 42 3g 00 01 79 72 <mode> <mapperIdx> <pointIdx> <inVal×5> <outVal×5> F7` |

- `3g` = Global Channel byte (g = 0-based channel number)
- Float encoding: IEEE 754 big-endian split into 7-bit × 5 bytes
- Mapper modes: `00`=Remove, `01`=Move, `02`=RemoveAll, `03`=Init, `7F`=Add

## Release Notes

### v0.1.2 — 2026-06-11
- Removed Google Analytics to improve privacy and eliminate third-party data collection

### v0.1.1 — 2026-06-11
- Fixed: DSP usage limit check now correctly blocks combinations at exactly 101% (was allowing 101%)

### v0.1.0 — 2026-06-11
- Initial public release
- Full parameter editing for FX / LFO / EG / EF / Mixer / Virtual Patch
- Virtual Patch Curve (Mapper) GUI
- `.preset` file import and send (Librarian)
- DSP Usage display and algorithm selection restriction

## License

MIT
