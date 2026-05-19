# MiniRGBDisplayOTA

Signed firmware releases for the MINI RGB DISPLAY ESP32 firmware.

The device polls `ota-manifest.json` every ~24h. When the manifest's `version`
is newer than what's running, the device shows an **Install Update** button
in its dashboard. Click it and the device downloads the `.bin`, verifies the
RSA signature against the public key baked in at build time, then flashes
itself and reboots.

## Layout

- `ota-manifest.json` — the manifest the device fetches. One entry per
  hardware variant. Current variants: `mini-rgb-display-esp32-v1`.
- `firmware-X.Y.Z.bin` — signed firmware images.
- `firmware-X.Y.Z.bin.sig` — RSA-2048 detached signatures.

## Releasing

From the firmware project folder (`MINI_RGB_DISPLAY_2026_v3.1`):

```powershell
.\release.bat 3.1.2          # bump version in source
# Arduino IDE -> Sketch -> Export Compiled Binary
.\release.bat 3.1.2 sign     # signs and prints manifest snippet
```

Then copy the produced `firmware-3.1.2.bin` + `firmware-3.1.2.bin.sig` here,
replace `ota-manifest.json` with the printed snippet, and `git push`.
