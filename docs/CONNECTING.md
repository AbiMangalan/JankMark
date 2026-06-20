# Connecting your device

JankMark reads performance data from your phone over **ADB** (Android Debug
Bridge). You can connect by USB (recommended) or Wi-Fi.

## 1. Enable Developer Options
1. On your phone: **Settings → About phone**.
2. Tap **Build number** seven times until it says "You are now a developer."
3. Go back to **Settings → System → Developer options**.

## 2. Connect by USB (recommended — lowest latency)
1. In Developer options, turn on **USB debugging**.
2. Plug your phone into your PC with a USB cable.
3. On the phone, tap **Allow** when asked to authorize USB debugging.
4. Open JankMark — it should detect your device automatically.

## 3. Connect by Wi-Fi (wireless debugging)
1. In Developer options, turn on **Wireless debugging**.
2. Tap **Wireless debugging → IP address & Port** to see something like
   `192.168.1.50:43210`.
3. In JankMark, choose **Wireless** and enter that IP and port.

> Phone and PC must be on the same network. USB is more reliable for accurate
> frame timing.
>
> The Wi-Fi **port changes every time** you toggle Wireless debugging — always
> read the current IP:port off that screen rather than reusing an old one.

## Troubleshooting
- **No device found:** re-check USB debugging is on and you tapped **Allow** on
  the phone. Try a different cable/port (some cables are charge-only).
- **"Device found but not authorized":** unlock the phone and accept the
  authorization prompt (tick "Always allow from this computer").
- **More than one device:** JankMark shows a picker so you can choose which
  device to profile.
- **Wi-Fi won't connect:** confirm the IP:port are current, the phone is on the
  same network, and no other `adb` instance is running and fighting JankMark's.
