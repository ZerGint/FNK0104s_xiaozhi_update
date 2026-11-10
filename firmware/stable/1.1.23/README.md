# FNK0104S custom firmware release 1.1.23

Two stable images are published for the board audio variants:

- fnk0104s-firmware-external-i2s.bin — external I2S amplifier (external_amp).
- fnk0104s-firmware-internal.bin — built-in ES8311/FM8002E amplifier (internal_amp).

The device selects the matching image from ota/stable.json using its compiled audio-output variant.
Bootloader, partition table and assets are unchanged since 1.1.18; the application image is the
complete update. The internal-amp image is built from the same commit with
`CONFIG_FNK_EXTERNAL_I2S_SPEAKER` disabled for the build (hence `dirty_worktree`).

Changes since 1.1.22:

- Weather works where Open-Meteo is unreachable: MET Norway (api.met.no) is used as a fallback.
  The working source is remembered across reboots and the other one is tried if it fails.
  If both fail, the weather widget shows "Сервер недоступен" and keeps the last data.
  With met.no the forecast card shows the expected precipitation amount instead of a probability.
