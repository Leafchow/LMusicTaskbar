# LMusicTaskbar

A lightweight [Windhawk](https://windhawk.net) mod that docks a native-style music controller directly onto your Windows 11 taskbar. No extra windows, no system tray icon — just the controls you need, right where you already look.

---

## Features

- **Album art** with rounded corners, pulled from the active media session
- **Prev / Play-Pause / Next** buttons with hover highlight and scale support
- **Volume slider** — drag to set system volume, or use the scroll wheel anywhere on the panel
- **Scrolling ticker** for long track and artist names
- **Acrylic blur** background that follows your Windows light/dark theme automatically
- **Idle hide** — panel disappears after playback has been paused for a configurable number of seconds
- **Fullscreen hide** — hides automatically when a fullscreen or Direct3D app is detected

---

## Requirements

- Windows 11
- [Windhawk](https://windhawk.net) v1.4 or later

---

## Installation

1. Open Windhawk and go to **Explore**.
2. Search for **LMusicTaskbar** and click **Install**, or
3. Click **Create new mod**, paste the contents of `lmusictb.wh.cpp`, and click **Compile**.

---

## Settings

| Setting | Default | Description |
|---|---|---|
| Panel Width | `300` | Width of the panel in pixels |
| Panel Height | `48` | Height of the panel in pixels (minimum 24) |
| Font Size | `11` | Track and artist text size in pixels |
| Button Scale | `1.0` | Scale factor for media buttons (0.5 – 4.0) |
| Horizontal Offset | `12` | Distance from the left edge of the taskbar |
| Vertical Offset | `0` | Fine-tune vertical centering relative to the taskbar |
| Auto Theme | `true` | Follow Windows light/dark mode for text and background |
| Text Color | `FFFFFF` | Manual hex RGB color — only used when Auto Theme is off |
| Background Opacity | `0` | Tint strength 0–255 — only used when Auto Theme is off |
| Hide in Fullscreen | `false` | Hide when a fullscreen or D3D app is detected |
| Idle Hide Timeout | `0` | Seconds paused before auto-hiding. `0` = never hide |

---

## Usage

| Action | Result |
|---|---|
| Click **⏮ / ⏯ / ⏭** | Previous / Play-Pause / Next |
| **Scroll wheel** over panel | Adjust system volume ±5% |
| **Drag** the volume slider | Set system volume precisely |
| Change settings in Windhawk | Panel updates immediately |

---

## How it works

LMusicTaskbar creates a transparent layered window (`WS_EX_LAYERED`) pinned at `ZBID_IMMERSIVE_NOTIFICATION` band level so it sits above the taskbar without stealing focus. It polls the [Global System Media Transport Controls](https://learn.microsoft.com/en-us/uwp/api/windows.media.control.globalsystemmediatransportcontrolssessionmanager) (GSMTC) API once per second to get the current session, track info, and album art. Volume is read and written through the Core Audio `IAudioEndpointVolume` interface. The panel hooks `EVENT_OBJECT_LOCATIONCHANGE` on the taskbar process so it repositions instantly when the taskbar moves or resizes.

---

## License

MIT
