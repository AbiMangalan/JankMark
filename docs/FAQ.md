# FAQ

**Is JankMark really free?**
Yes. No paywall, no subscription. Supporting development is optional.

**Is it open source?**
No. JankMark is closed source but free to use. This repo holds the
documentation and the release downloads, not the source code.

**Does it put an overlay on my phone or change my device?**
No. JankMark reads telemetry over ADB from your PC. Nothing is drawn on the
phone and nothing is written to the device.

**Does it collect or upload my data?**
No. Profiling happens locally between your PC and your own device.

**Which platforms are supported?**
Windows today. Linux and macOS support is planned.

**Why do I need USB debugging?**
That's the standard, accurate way to read frame-timing data from Android.
See [CONNECTING.md](CONNECTING.md).

**Why is GPU usage / GPU frequency blank?**
GPU telemetry comes from vendor-specific kernel files that many phones only
expose to rooted devices. FPS, frame-time, CPU, RAM, and temperature work
everywhere; GPU values show only when your device makes them readable.

**How do I report a bug or request a feature?**
Open an issue from the
[Issues](https://github.com/AbiMangalan/JankMark/issues) tab, or start a
[Discussion](https://github.com/AbiMangalan/JankMark/discussions).
