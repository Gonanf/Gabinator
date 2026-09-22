<p align="center">
  <img src="assets/banner.png" alt="Gabinator" width="100%">
</p>

<h1 align="center">Gabinator</h1>

<p align="center"><b>Screen sharing from Windows/Linux desktop to Android over USB or TCP.</b></p>

<p align="center">
  <img alt="estado" src="https://img.shields.io/badge/estado-prototipo-blue">
  <img alt="lenguaje" src="https://img.shields.io/badge/HTML-4-blue">
  <img alt="licencia" src="https://img.shields.io/badge/licencia-privado-lightgrey">
  <img alt="última actividad" src="https://img.shields.io/badge/ultima_actividad-2024--11-lightgrey">
</p>

---

## What it is

Gabinator is a screen sharing tool that mirrors a Windows or Linux desktop screen to an Android device. The desktop app captures, compresses, and sends frames; the Android app receives and displays them.

Two connection modes:

- **USB** — uses Android Open Accessory (AOA) protocol for low-latency direct connection.
- **TCP** — standard network connection over Wi-Fi.

**In one sentence:** Gabinator lets you view your desktop screen on your Android phone via USB or TCP.

## State

| | |
|---|---|
| **Status** | Prototype |
| **Last activity** | 2024-11 |
| **Usable today** | Yes, but alpha — expect rough edges |
| **What's missing** | Formal packaging (installers), documentation, tests |
| **Known risks** | Alpha builds only; no CI/CD; no automated testing |

## Why it exists

Student project for screen mirroring without relying on existing solutions like scrcpy. Built as a two-component system (desktop server + Android client) with AOA and TCP transport.

## Demo

No demo available in this repo. The actual components are in separate repos:

- [Gabinator Android](https://github.com/Gonanf/gabinator_android_remaster/releases/tag/alpha-v0.1.0)
- [Gabinator Desktop](https://github.com/Gonanf/gabinator_desktop_remaster/releases/tag/alpha-v0.1.0)

## Installation and usage

This repo is a documentation site (Jekyll/GitHub Pages). To run locally:

```bash
cd Gabinator
bundle install
bundle exec jekyll serve
```

Then open `http://localhost:4000`.

### Using Gabinator

**USB mode:**

1. Install ADB drivers on your desktop ([Google guide](https://developer.android.com/studio/run/win-usb)).
2. Install Gabinator Android and run it.
3. Install Gabinator Desktop, then:
   ```bash
   gabinator_desktop_r -M AOA -G        # list compatible devices
   gabinator_desktop_r -M AOA -P <PID> -V <VID> -C  # connect
   ```
4. On Android, tap USB and accept permissions.

**TCP mode:**

1. Install Gabinator Android and run it.
2. Install Gabinator Desktop, then:
   ```bash
   gabinator_desktop_r -M TCP -C
   ```
3. On Android, tap TCP, enter the IP shown on desktop, connect.

## Stack

- **Languages:** HTML, SCSS
- **Framework:** Jekyll (GitHub Pages)
- **Theme:** Hacker theme (customized)
- **Infra:** GitHub Pages for this docs site

## Architecture

This repo is the documentation landing page. The actual screen sharing system has two components:

```
gabinator_desktop  →  USB/TCP  →  gabinator_android
(server)                          (client)
```

- **Desktop** captures frames, compresses, sends via AOA or TCP.
- **Android** receives frames and displays them in real time.

## Repo structure

```
_layouts/       # Jekyll layout templates
_includes/      # Head customization (analytics, theme colors)
_sass/          # SCSS styles (Hacker theme)
assets/         # Static assets (CSS, images)
index.html      # Main landing page with usage instructions
docs/           # Additional documentation
```

## Roadmap

- [ ] Publish installers for desktop (Windows/Linux packages)
- [ ] Add proper documentation (setup guide, troubleshooting)
- [ ] Add automated tests
- [ ] Improve frame compression/performance

## Notes and decisions

- Split into two repos (desktop + Android) for independent development.
- AOA chosen for USB mode to avoid requiring root/ADB on the Android side.
- TCP mode added as fallback for devices without USB support.
- The project is marked "Terminado" (finished) in git, but is alpha quality — no formal release process.

## License

Private — no license file. Not open source.

---

*This README replaces the auto-generated one. Based on the actual repo contents and project page.*
