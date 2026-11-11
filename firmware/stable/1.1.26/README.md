# FNK0104S custom firmware release 1.1.26

Two stable images are published for the board audio variants:

- fnk0104s-firmware-external-i2s.bin — external I2S amplifier (external_amp).
- fnk0104s-firmware-internal.bin — built-in ES8311/FM8002E amplifier (internal_amp).

The device selects the matching image from ota/stable.json using its compiled audio-output variant.
The internal-amp image is built from the same commit with `CONFIG_FNK_EXTERNAL_I2S_SPEAKER`
disabled for the build (hence `dirty_worktree`).

Changes since 1.1.25:

- More free internal RAM (LVGL in PSRAM): fixes reboots while playing HTTPS radio.
- Weather where Open-Meteo is blocked: fixes reboots after switching to MET Norway, the widget is
  updated again and the working source is remembered across reboots.
- City search falls back to OpenStreetMap Nominatim when the Open-Meteo geocoder is unreachable.
