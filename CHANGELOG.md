# Changelog

All notable changes to JankMark are documented here. This project follows
[Semantic Versioning](https://semver.org/) (MAJOR.MINOR.PATCH).

## [0.2.0-beta] — 2026-06-21

First public beta release.

### Added

- **Session library** — every completed session is auto-saved to
  `%USERPROFILE%\.jankmark\sessions\`. Access via **File → Sessions** to browse,
  open past sessions with full interactive charts, rename, or delete them.
- **Screenshot export** — "Screenshot" button in the report dialog captures the
  entire report to a PNG via a system file picker.
- **Power consumption** stat card and live chart (Watts, computed from battery
  voltage × current).
- **Battery percentage** live chart.
- **Battery voltage** live chart (3.0–4.5 V range) — useful for spotting voltage
  sag under sustained gaming load.
- **Current draw** live chart (0–5 A) — shows instantaneous amp draw in real time.
- Power section in session reports: average power, peak power, average battery %,
  average/minimum voltage, average/peak current.
- **5% Low, 1% Low, and 0.1% Low FPS** — three low-percentile stats derived from
  frame-interval percentiles (p95/p99/p99.9), shown on the live dashboard and in
  session reports.
- **GPU frequency telemetry** — avg and peak GPU clock speed (MHz) in reports,
  alongside CPU frequency stats.
- **CPU and GPU clock-frequency gauge toggles** — click the unit label ("%" or
  "GHz") on either the CPU or GPU circular gauge to toggle between usage percentage
  and live clock speed. Useful for spotting thermal throttling at a glance.
- **Branded onboarding screen** — logo and tagline on the connection screen; USB
  and Wi-Fi tiles with illustrated glyphs; animated spinner during device search;
  inline "How to enable USB debugging" guide.
- **Four-state session machine** — Idle → Connecting → Recording → Stopped, each
  with a distinct visual state.
- Recording indicator: blinking red dot, REC label, and live elapsed mm:ss timer.
- Over-budget shading in the frame-time chart — semi-transparent red fill above
  the 16.67 ms threshold line.
- Live pulse dot on FPS and frame-time plots at the current leading edge.
- Help menu: **Open Log Folder** and **Report an Issue**.
- Keyboard shortcuts: Space → Start/Stop, C → Clear, Esc → Stop.
- Clean uninstall prompt in the uninstaller to permanently remove
  `%USERPROFILE%\.jankmark\` (settings, sessions, logs).

### Changed

- **Zero-setup ADB**: bundled `adb.exe` is used automatically — no manual PATH
  configuration or separate ADB install needed.
- **CPU usage accuracy**: switched from `dumpsys cpuinfo` (unreliable on Android
  8+) to `/proc/stat` jiffies-delta, the standard Linux method.
- Report charts use pyqtgraph (already bundled) instead of matplotlib, removing
  ~40 MB from the installed size.
- RAM stat card and RAM chart are linked: clicking the card toggles the chart
  between MB and % view.
- Crosshair value label snaps to the nearest recorded data point and flips below
  the crosshair line near the top of a plot to prevent clipping.
- Installer size ~141 MB (down from ~173 MB).

### Fixed

- PausedOverlay (app not in foreground) text was clipping on the second line.
- RAM chart was starting at a 0–1 default range instead of the device's actual
  RAM ceiling.

---

## [0.1.0] — 2025 (internal only)

Initial working prototype. Not released publicly.
