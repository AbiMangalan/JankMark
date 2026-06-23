# Changelog

All notable changes to JankMark are documented here. This project follows
[Semantic Versioning](https://semver.org/) (MAJOR.MINOR.PATCH).

## [0.2.1-beta] — 2026-06-23

### Added

- **Searchable app picker** — the package selector is now type-to-search
  (case-insensitive, matches anywhere in the name/package), so you no longer
  scroll a long list to find your game.
- **Auto-detect the running app** — a **Detect** button selects whatever app is
  currently open on your device; while recording, JankMark also flags when the
  profiled app leaves the foreground with an "App not in foreground" overlay.
- **Separate CPU, GPU & battery temperatures** — the Temperature chart now plots
  all three as their own lines instead of a single combined reading.
- **Hover "?" badges** on every metric explaining what it means.
- **"What's New"** dialog shown once after each update.
- **"Not supported on this device" overlays** — when a phone can't expose a metric
  (e.g. GPU usage on some Pixels), the chart now says so with a "?" that explains
  why, instead of leaving an empty graph.
- **Frame-time graph explainer** — a "?" on the Frame Time chart (live and in
  reports) explains why a phone's frame time steps up and down: phones refresh on a
  fixed beat and mostly lack desktop-style variable refresh (VRR / G-Sync /
  FreeSync), so normal vsync pacing isn't mistaken for stutter.

### Improved

- **Frame time reflects what's on screen** — JankMark now shows the real on-screen
  frame interval (120 FPS ≈ 8.3 ms, 60 FPS ≈ 16.7 ms), like desktop frame-time
  tools, with a **cadence indicator** (Even / Fractional / Uneven) that explains
  the pattern. On a 120 Hz screen, frame rates that don't divide evenly (e.g. 90)
  naturally step between 8.3 and 16.7 ms — that's vsync ("Fractional"), not stutter.
- **Gauges auto-pick the mode that has data** — on devices where only GPU usage or
  only GPU clock is readable, the gauge now starts on whichever one your phone
  actually reports instead of showing a blank "N/A" (you can still click to switch).
- **Temperature gauge cycles sensors** — click the °C on the Temperature gauge to
  cycle Max → CPU → GPU → Battery (skipping any sensor your device doesn't expose).
- **Clearer temperature graph hover** — hovering the Temperature chart now snaps to
  the line nearest your cursor and names it (e.g. "GPU 50 °C"); hovering another
  chart shows all three temperatures at once.
- **Scrollable, zoomable report timeline** — long sessions open at a readable
  window; drag to pan through the timeline and scroll to zoom, with every chart
  staying time-aligned.
- **Wider GPU support** — reads GPU usage without root on more devices (including
  via the Adreno busy counter); when a device blocks GPU stats, the gauge explains
  why instead of showing a blank.
- **Smarter graph scaling** — the FPS and frame-time charts scale to the bulk of
  the data, so a single spike no longer flattens everything; faint 30 / 60 / 90 /
  120 guide lines on the FPS chart.
- **Sharper app icon** that fills the tile properly — on the taskbar, in shortcuts,
  and in the installer.
- **Cleaner installer** — closes a running JankMark before upgrading and removes
  old files on reinstall.

### Fixed

- Recording no longer starts until real frames arrive — no more empty sessions if
  you press Start before the game finishes loading.
- A clear "check your phone for a USB authorisation prompt" message when the ADB
  connection drops mid-session.
- The Wi-Fi connection error no longer overlaps the IP field, and the duplicated
  help/links at the bottom of the connect screen are gone.
- Chart hover tooltips no longer get clipped at the edges of a graph.

---

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
