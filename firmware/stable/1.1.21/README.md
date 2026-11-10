# FNK0104S custom firmware release 1.1.21

Two stable images are published for the board audio variants:

- fnk0104s-firmware-external-i2s.bin — external I2S amplifier (external_amp).
- fnk0104s-firmware-internal.bin — built-in ES8311/FM8002E amplifier (internal_amp).

The device selects the matching image from ota/stable.json using its compiled audio-output variant.
Bootloader, partition table and assets are unchanged since 1.1.18; the application image is the
complete update. The internal-amp image is built from the same commit with
`CONFIG_FNK_EXTERNAL_I2S_SPEAKER` disabled for the build (hence `dirty_worktree`).

Changes since 1.1.20:

- Higher microphone sensitivity: ES8311 digital ADC gain 30 -> 36 dB plus a 3 dB fine boost,
  and automatic gain control on the audio sent to the server (up to 18 dB). Wake word and
  phrases are recognized from 1.5-3 m at normal speaking volume, and short pauses no longer
  end a quiet phrase as easily.
