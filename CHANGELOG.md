# Changelog

All notable changes to JankMark are documented here. This project follows
[Semantic Versioning](https://semver.org/) (MAJOR.MINOR.PATCH).

## [0.2.0-beta] — 2026-06-20

First public beta release.

### Added

- **5% Low, 1% Low, 0.1% Low FPS** — three low-percentile stats derived from
  frame-interval percentiles (p95/p99/p99.9). All three are shown on the live
  dashboard and in session reports.
- **GPU frequency telemetry** — avg and peak GPU clock speed (MHz) in reports,
  alongside the existing CPU frequency stats. Shown when the device exposes the
  reading; unavailable values are omitted cleanly rather than shown as errors.
- **Branded onboarding screen** — JankMark logo and tagline on the connection
  screen; USB and Wi-Fi tiles with illustrated glyphs; animated spinner during
  device search; collapsible "How to enable USB debugging" guide inline.
- **Four-state session machine** — Idle → Connecting → Recording → Stopped, each
  with a distinct visual state so the app never looks broken between actions.
- Recording indicator: blinking red dot, REC label, and live elapsed mm:ss timer.
- Over-budget shading in the frame-time chart — semi-transparent red fill above
  the 16.67 ms (60 FPS) threshold line; updates if the FPS target changes.
- Live pulse dot on the FPS and frame-time plots — a sine-eased breathing
  marker at the current leading edge.
- Help menu: **Open Log Folder** and **Report an Issue**.
- Keyboard shortcuts: Space → Start/Stop, C → Clear, Esc → Stop.

### Changed

- **Zero-setup ADB**: bundled `adb.exe` is used automatically — no manual PATH
  configuration needed.
- Report charts now rendered with pyqtgraph (already bundled) instead of
  matplotlib, removing ~40 MB from the installed size.
- Installer size reduced from ~173 MB to ~141 MB.
- RAM stat card and RAM chart are linked: clicking the card toggles the chart
  between MB and % view with no separate in-graph button.
- Crosshair value label now snaps to the nearest recorded data point (instead
  of the raw pointer Y position) and flips below the crosshair line when the
  data point is near the top of the plot to prevent clipping.

### Fixed

- PausedOverlay (game not in foreground) text was clipping on the second line —
  now renders correctly at any window size.
- RAM chart was starting at a 0–1 pyqtgraph default range instead of the
  device's actual RAM ceiling.

---

## [0.1.0] — 2025 (internal only)

Initial working prototype. Not released publicly.
