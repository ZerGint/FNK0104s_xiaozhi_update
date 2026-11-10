# FNK0104S custom firmware release 1.1.22

Two stable images are published for the board audio variants:

- fnk0104s-firmware-external-i2s.bin — external I2S amplifier (external_amp).
- fnk0104s-firmware-internal.bin — built-in ES8311/FM8002E amplifier (internal_amp).

The device selects the matching image from ota/stable.json using its compiled audio-output variant.
Bootloader, partition table and assets are unchanged since 1.1.18; the application image is the
complete update. The internal-amp image is built from the same commit with
`CONFIG_FNK_EXTERNAL_I2S_SPEAKER` disabled for the build (hence `dirty_worktree`).

Changes since 1.1.21:

- Quick Settings header: clock correction from -2 to +2 hours, saved on the device. It shifts
  the clock, the weather date and the weather update time when the server time zone differs
  from the user's location.
- The clock is redrawn once a minute instead of four times a second, and the weather date
  changes at midnight without waiting for the next weather update.
