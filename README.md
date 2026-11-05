# esp8266-80211-poc

A collection of **proof-of-concept** firmware for the ESP8266, built to study and
demonstrate Layer-2 (802.11 / MAC-layer) weaknesses of Wi-Fi networks.

These are **educational security-research** projects. They exist to show how the
802.11 standard behaves when its management and control frames are abused, and to
document the mitigations that modern networks use against those techniques.

---

> ## ⚠️ Legal & ethical notice — read this first
>
> The firmware in these repositories transmits 802.11 frames that **disrupt wireless
> communications**. Using them against networks, devices, or radio spectrum that you
> do **not** own, or that you are **not explicitly authorized in writing** to test, is
> **illegal in virtually every jurisdiction** (unauthorized interference with
> communications, computer-misuse laws, etc.).
>
> Use them **only**:
> - on **your own** equipment, or
> - inside an **isolated / shielded lab**, or
> - within the documented scope of an **authorized penetration test**.
>
> This is also RF: your transmissions do not stop at the lab walls, so prefer a
> shielded environment and the lowest power/exposure necessary. The author provides
> this material for study only and **assumes no responsibility for any misuse**.

---

## Projects

| Project | What it demonstrates | Layer |
|---------|----------------------|-------|
| [esp8266-deauther](https://github.com/Datalux/esp8266-deauther) | Deauthentication / disassociation spoofing | 802.11 management frames |
| [SleepyFi](https://github.com/Datalux/SleepyFi) | Silent DoS via Power Save Mode (PSM) spoofing | 802.11 power-management state |
| [jymmyjammer](https://github.com/Datalux/jymmyjammer) | Channel / bandwidth occupation | 802.11 medium access (virtual carrier sense) |

## Background

All three projects target the same historical property of Wi-Fi: **management and
control frames were not authenticated**, so a third party within radio range can forge
them and influence how clients and access points behave. The projects isolate one
technique each so the underlying mechanism can be observed in a capture (e.g. with
Wireshark or a second ESP8266 in monitor mode).

They are intentionally minimal — each is a didactic example of *one* idea, not a
general-purpose tool.

## Countermeasures (the point of the exercise)

Documenting the defenses is as important as the attacks:

- **802.11w — Protected Management Frames (PMF)** authenticates management frames and
  neutralizes deauth/disassociation spoofing.
- **WPA3** makes PMF **mandatory**, so these management-frame attacks have no effect on
  a properly configured WPA3 network.
- **Control frames** (ACK/RTS/CTS) remain unauthenticated by design, so medium-access /
  NAV-based disruption is mitigated mostly at the **implementation** level (NAV capping
  and reset rules) rather than cryptographically — a good illustration of a
  *specification* weakness vs. a *practical* one.
- **Detection**: abnormal rates of management frames, or control frames carrying
  anomalous duration values, are observable signals a monitoring setup can flag.

## Hardware & build

- Any ESP8266 board (NodeMCU, Wemos D1 mini, …) — note: **2.4 GHz only**.
- Arduino IDE or PlatformIO with the ESP8266 core installed.
- See each repository's own README for its specific usage.

## Disclaimer

For **educational and authorized testing use only**. You are responsible for complying
with the laws and regulations of your jurisdiction.

