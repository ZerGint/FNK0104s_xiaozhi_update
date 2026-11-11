# Waveshare ESP32-P4 4.3" custom firmware release 1.0.2

- RU/p4-4.3-firmware.bin — Waveshare ESP32-P4-WIFI6-Touch-LCD-4.3 (Rev3.x, Multi-OTA layout),
  Russian build. Application image only, installed into the inactive XiaoZhi slot (OTA0/OTA1).

Listed in ota/stable-p4-4.3.json under the `RU` key.

Changes since 1.0.1:

- Fixes a crash (blue screen and reboot) when pressing "Обновить" or a slot button in
  Settings → System: confirmation and progress dialogs used a font freed after the theme
  was reloaded. 1.0.0 and 1.0.1 cannot start an update from the UI because of this; they
  need one USB flash of 1.0.2 or later.
