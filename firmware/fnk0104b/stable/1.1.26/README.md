# FNK0104B custom firmware release 1.1.26

- fnk0104b-firmware.bin — FNK0104B (2.8-inch ILI9341, onboard amplifier, internal_amp).

Listed in ota/stable-fnk0104b.json.

Changes since 1.1.25:

- More free internal RAM (LVGL in PSRAM): fixes reboots while playing HTTPS radio.
- Weather where Open-Meteo is blocked: fixes reboots after switching to MET Norway, the widget is
  updated again and the working source is remembered across reboots.
- City search falls back to OpenStreetMap Nominatim when the Open-Meteo geocoder is unreachable.
