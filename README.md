# TWRP device tree for Xiaomi SM8750

## Devices

One image serves the whole family. `variant-script.sh` reads
`ro.boot.hardware.sku` and sets the per-device properties from there; the
WLAN chip is read from the kernel's cnss device tree node instead.

| SKU | Device | Weaver | WLAN |
| --- | --- | --- | --- |
| `dada` | Xiaomi 15 | Thales eSE | peach_v2 |
| `haotian` | Xiaomi 15 Pro | Thales eSE | peach_v2 |
| `xuanyuan` | Xiaomi 15 Ultra | Thales eSE | peach_v2 |
| `warsaw` | REDMI K90 Ultra | NXP eSE | kiwi_v2 |
| `annibale` | REDMI K90 / POCO F8 Pro | NXP eSE | kiwi_v2 |
| `miro` | REDMI K80 Pro / POCO F7 Ultra | NXP eSE | detected |
| `piano` | Xiaomi Pad 8 Pro | TEE (miweaver) | peach_v2 |

`piano` has no secure element: no eSE node in its device tree, so the eSE HAL
never finds one and nothing can reach an applet. Its weaver slots live in the
TEE and Xiaomi's own `android.hardware.weaver` is the service that reads them.

Tested on hardware: `warsaw`, `piano`.

`piano` has a landscape panel, so init sets persist.twrp.rotation for it and
TWRP scales the portrait theme onto the rotated canvas. TW_ROTATION is only
the compile time default; the property overrides it per device.

## Features

- [X] ADB
- [X] Decryption
- [X] Display
- [X] Fasbootd
- [X] Flashing
- [X] MTP
- [X] Sideload
- [X] USB-OTG
- [X] Vibrator
- [X] WLAN

## Build it yourself
* [TWRP-Test/platform_manifest_twrp_aosp](https://github.com/TWRP-Test/platform_manifest_twrp_aosp)
