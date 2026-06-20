# Understanding JankMark Metrics

This guide explains every number JankMark shows you, what it measures, and how
to interpret it when reviewing a session.

---

## How a session works

1. Connect your device (see [CONNECTING.md](CONNECTING.md)).
2. Select the game or app you want to profile from the package dropdown.
3. Click **Start** (or press **Space**). JankMark begins reading frame data over
   ADB and streaming it to the live dashboard.
4. Play the game for as long as you need — the longer the session, the more
   meaningful the low-percentile stats.
5. Click **Stop** (or press **Space** again).
6. Click **View Report** to open the full session summary, or export it as HTML
   or Markdown.

---

## Live dashboard panels

### FPS (frames per second)

The large number in the top-left stat card is the **instantaneous FPS** —
measured over the last one-second rolling window. It reflects what is happening
right now, so it moves with the game's current load.

| Range | What it means |
|---|---|
| ~60 | Hitting the 60 FPS target (standard for most games) |
| 45–59 | Occasional load spikes or a demanding scene |
| < 30 | Sustained performance issue or thermal throttling |
| 90 / 120 | High-refresh-rate device, game running at elevated target |

### Avg FPS

The session average FPS computed from the total elapsed time since recording
began. More stable than the instantaneous FPS and a good headline number for
comparisons across devices or settings.

### 5% Low FPS

The frame rate at the **95th percentile of frame intervals** — that is, 95% of
frames were rendered faster than this. A 5% Low of 40 FPS means the slowest 5%
of your frames were slower than 25 ms each.

A healthy 5% Low is close to your Avg FPS. A large gap (e.g. Avg 58, 5% Low 32)
means the game has frequent but mild hitches even when the average looks fine.

> Requires at least ~20 frames of data. Shows "—" until that threshold is met.

### 1% Low FPS

The frame rate at the **99th percentile of frame intervals**. Captures the
worst 1% of frames — those that cause visible micro-stutters and feel "janky"
even when the average FPS is high.

This is the most widely quoted low-percentile metric in smartphone benchmark
reviews. A 1% Low close to the average means consistent frame delivery; a large
drop means the game regularly produces bad frames even when it is otherwise
smooth.

> Requires at least 100 frames of data.

### 0.1% Low FPS

The frame rate at the **99.9th percentile** — the very worst frames in the
entire session. Highlights extreme outliers such as shader compilation hitches,
garbage collection pauses, or thermal throttle events.

> Requires at least 1,000 frames of data (~17 minutes at 60 FPS). Shows "—"
> until that threshold is met; this is normal for shorter sessions.

### Frame Time (ms)

How long the most recently rendered frame took to produce, in milliseconds.
The live value updates each polling cycle.

The frame-time **chart** shows the full time series. The red dashed line marks
the **frame budget** (default: 16.67 ms for a 60 FPS target — one second
divided by 60). Any bar above this line is a jank frame.

### Jank %

The percentage of total frames that exceeded the frame-time budget. A jank frame
is one that caused the device to miss its vsync deadline, producing a visible
dropped frame or stutter.

| Value | Interpretation |
|---|---|
| < 1% | Excellent — imperceptible to almost all players |
| 1–5% | Acceptable — occasional minor stutters |
| 5–15% | Noticeable — frequent hitches during demanding scenes |
| > 15% | Poor — game is struggling to maintain its frame rate |

### CPU %

Average utilisation across all CPU cores, reported by the device kernel. A
sustained CPU % near 100% indicates a CPU-bound workload; if FPS is also low,
the CPU is the bottleneck.

### GPU %

GPU engine utilisation, where available. Many Android devices restrict this
reading to rooted access — if your device does not expose it, this card shows
"—".

A GPU % near 100% with normal CPU % indicates a GPU-bound workload.

### RAM (MB / %)

App RAM usage. Click the card to toggle between the absolute value (MB) and
percentage of total device RAM. The chart also switches view when you click the
card.

This is the working-set memory consumed by the profiled app, not total system
RAM. A steadily rising value during a session can indicate a memory leak.

### Temp (°C)

Device skin temperature, typically from the battery or SoC thermal zone,
depending on the device. Temperatures above ~45 °C typically trigger Android's
thermal throttle, which can cause sudden FPS drops.

---

## CPU and GPU frequency plots

The **CPU Freq** and **GPU Freq** plots show clock speeds in MHz over time.
A sustained drop in clock speed while FPS also drops confirms that the device
is thermally throttling — the SoC is slowing itself down to shed heat.

Normal patterns:
- Frequency ramps up at the start of a demanding scene and stabilises.
- Brief drops between scenes or in menus are expected.
- A sustained low frequency mid-session = throttle.

---

## Session report

### Hero strip (top of report)

The four headline numbers: **Avg FPS**, **5% Low FPS**, **1% Low FPS**,
**Jank %**, and **Avg Frame Time**. These are the first things to compare
across devices or sessions.

### Frame rate card

- **Avg / Min / Max FPS** — overall range of FPS during the session.
- **5% / 1% / 0.1% Low FPS** — low-percentile performance. Compare 1% Low
  to Avg FPS; the smaller the gap, the smoother the session.
- **Stability** — percentage of FPS samples within ±5 of the average. A higher
  value means more consistent frame delivery.

### Jank card

- **Jank frames** — absolute count of frames that missed the budget.
- **Jank %** — fraction of total frames that janked.
- **Worst frame** — the single slowest frame time in the session (ms).

### Frame time card

- **Average** — mean render latency across the session.
- **P95 / P99** — 95th and 99th percentile frame times. P95 maps directly to
  the 5% Low FPS; P99 maps to the 1% Low FPS.
- **Frames > budget** — count and percentage of frames that exceeded the budget
  line.

### Hardware card

| Row | What it means |
|---|---|
| Avg / Max CPU | Mean and peak CPU utilisation over the session |
| Avg / Max GPU | Mean and peak GPU utilisation (if readable) |
| CPU Freq avg / peak | Mean and maximum CPU clock speed |
| GPU Freq avg / peak | Mean and maximum GPU clock speed (if readable) |
| Peak RAM | Highest app memory reading during the session |
| Max Temp | Highest temperature reading |
| Throttle events | Number of samples at or above 45 °C |

---

## Tips for meaningful sessions

- **Record for at least 5 minutes** in a representative game scenario (not just
  the menu) to build enough interval samples for meaningful 1% Low values.
- **Reproduce the same scenario** across devices (same map, same settings) for
  fair comparisons.
- **Watch for thermal patterns** — many devices show their best performance in
  the first 2–3 minutes before heat builds. A second 5-minute run often gives a
  more realistic thermal picture.
- **Use the crosshair** — hover over any chart to see the exact value at that
  moment. The crosshair syncs across all charts so you can correlate an FPS dip
  with a temperature spike or CPU frequency drop at the same timestamp.
