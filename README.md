# Linux on Huawei MateBook 13 (2019)

> Brain dump: MateBook 13 (Wright-W19) running Debian heavily inspired by [lidel's documentation of running Linux on MateBook X](https://github.com/lidel/linux-on-huawei-matebook-x-2017).

## Background

Huawei MateBook 13, released in 2019, has at least two modifications (different CPUs, integrated vs. dedicated graphics). Both come with Microsoft Windows 10 and there initially was no information at all concerning Linux support.

I am running Debian on the more simple MateBook 13 variant, model Wright-W19. This repository documents what works and what does not.

## Linux Support Matrix

| Device | Model |  Works | Notes |
| --- | --- |  :---: | --- |
| Processor | Intel Core i5-8265U | ✔ Yes | 8 cores, power states etc seem to work out of the box|
| Graphics | Intel UHD Graphics 620 | ✔ Yes | via standard kernel driver |
| Memory | 8192 MB | ✔ Yes |  |
| Display | 13 inch 2:3, 2160x1440 (2K) | ✔ Yes | resolution is correctly detected by `xrandr`, backlight control works via native function keys and can be controlled by KDE settings |
| Storage | Samsung SSD, 256 GB | ✔ Yes | via standard kernel driver |
| Wifi | Intel Cannon Point Wireless-AC 8265 (a/b/g/n/ac) | ✔ Yes | requires kernel 4.14 and firmware (`firmware-iwlwifi` non-free package) |
| Bluetooth | Intel Bluetooth 5.0| ❓ Not tested |  |
| Airplane Mode | Wifi+Bluetooth | ❓ Not tested |  |
| Soundcard  | Intel Cannon Point-LP High Definition Audio | ✔ Yes  | via standard kernel driver, works fine with `pulseaudio` |
| Speakers  |  | ✔ Yes |  |
| Microphone | | ✔ Yes | out of the box |
| Webcam | HD Camera (13D3:56C6) | ✔ Yes | works out of the box, indicating light too |
| Ports | 2 × USB-C | ✔ Yes | charging works only via left port, external display only via right one, but it is a known hardware limitation of the laptop |
| Power button |  | ✔ Yes | needs to be pressed for at least a second to generate event |
| Fingerprint Reader | some proprietary sensor | ❌ No | located on the power button  |
| Battery | Dynapack 42 Wh Lithium-Polymer | ✔ Yes | everything works: current status, chargin/discharging rate and remaining battery time estimates |
| Lid | ACPI-compliant |  ✔ Yes | works as expected, though ACPI complains in logs |
| Power management | | ✔ Yes | works, [see below](#power-management) for details |
| Keyboard |  | ❕ Mostly | backlight and backlight control work, Fn+Key combinations work (including non-documented Fn+Up/Down = PgUp/PgDn, Fn+Left/Right = Home/End), volume control works, microphone switch doesn't, display switch works, Wifi switch doesn't, Huawei key doesn't; those that don't generate nothing in ACPI logs or `xev` |
| Touchpad | ELAN962C:00 04F3:30D0 | ⁉ Kinda | touchpad is detected and works in KDE (though not in Debian installer), but almost all options are greyed out; double- and three-finger clicks work, so does double-finger scrolling, multi-touch gestures can not be set up; upon every touch floods system logs with error messages (`incomplete report (14/65535)`) - up to the point where rubbing your finger against touchpad produces 15% CPU usage by syslog |
| Port Extender | MateDock 2 dongle included with laptop | ✅ Partly tested | full-size HDMI and D-SUB not tested, USB-C and USB-A work as expected |

## Power Management

Suspend to S3 state works out of the box. For hibernation to work `Secure boot` must be disabled in BIOS. Laptop seems to wake up without any issues.