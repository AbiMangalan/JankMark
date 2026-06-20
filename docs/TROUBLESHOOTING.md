# JankMark Troubleshooting

Common issues encountered during beta and how to resolve them.

---

## Wireless ADB: "failed to connect" / cannot reach device over Wi-Fi

**Symptom:** JankMark says the device is unavailable, or `adb connect` returns
`failed to connect to 192.168.x.x:xxxxx: Connection refused`.

**Root cause:** Android's wireless debugging uses *two separate ports*:
- A **pairing port** (changes every session) — used once with `adb pair` to
  exchange a certificate.
- A **debugging port** (you set it; persists) — used with `adb connect` for
  every subsequent connection.

If you deleted the JankMark/PC certificate from your tablet's
*Settings → Developer Options → Wireless debugging → Paired devices*, the device
no longer trusts this PC and `adb connect` will be refused.

**Fix — re-pair the device:**

1. On the tablet, go to **Settings → Developer Options → Wireless debugging**.
2. Tap **Pair device with pairing code**.
3. Note the **IP address**, **pairing port** (e.g. `192.168.1.5:37853`), and the
   6-digit code shown on screen.
4. In a terminal on the PC run:
   ```
   adb pair 192.168.1.5:37853
   ```
   Enter the 6-digit code when prompted.
5. Once pairing succeeds, tap back to the main Wireless debugging screen and note
   the **port** shown next to "IP address & Port" (this is the *debugging* port,
   different from the pairing port).
6. Connect:
   ```
   adb connect 192.168.1.5:5555
   ```
   (Use the debugging port from step 5, not the pairing port.)
7. Re-launch JankMark and tap **Disconnect → Reconnect** to re-run onboarding.

> **Tip:** JankMark bundles its own `adb` binary. If you run these commands in
> the terminal, make sure you're using the same `adb` the app uses (bundled in the
> installation folder) or that your system `adb` version matches.

---

## No device detected on USB

- **USB debugging not enabled:** Go to *Settings → About phone*, tap *Build
  number* seven times to unlock Developer Options, then enable *USB debugging*.
- **Cable is charge-only:** Use a data-capable USB cable (many budget cables
  only carry power). Try the cable that came with the device.
- **Windows driver missing (Android phones):** Install the OEM USB driver or
  the generic Android ADB driver via Device Manager.
- **"Unauthorised" in JankMark:** Unlock the device and accept the "Allow USB
  debugging?" prompt. Check "Always allow from this computer".

---

## Connection drops mid-session

- **Screen times out:** Keep the screen on during profiling. Go to *Developer
  Options → Stay awake* to prevent the display from sleeping while charging.
- **USB power saving:** Some PCs suspend USB ports after idle. Disable USB
  selective suspend in Windows power settings.
- **Wireless signal loss:** Ensure the tablet and PC are on the same Wi-Fi
  network and within range. Avoid switching between 2.4 GHz and 5 GHz bands
  during a session.

---

## Collecting logs for a bug report

JankMark writes detailed diagnostic logs during every session.

**Log location:** `%USERPROFILE%\.jankmark\logs\jankmark.log`
(e.g. `C:\Users\YourName\.jankmark\logs\jankmark.log`)

**Easiest way to open the folder:** In JankMark, go to **Help → Open Log Folder**.
This opens the log directory in Windows Explorer.

**What to include in a GitHub issue:**

1. Steps to reproduce the problem.
2. The full `jankmark.log` file (or the relevant section if it's large).
3. Your device model, Android version, and connection method (USB / wireless).
4. Screenshots if the issue is visual.

Open issues at: **https://github.com/AbiMangalan/JankMark/issues**

> **Note for beta users:** Beta builds (`0.x.x-beta`) log at DEBUG level, which
> captures ADB exchanges, frame counts, and hardware poll results. This extra
> detail is invaluable when diagnosing connection or parsing issues. Final release
> builds log at INFO level (quieter).
