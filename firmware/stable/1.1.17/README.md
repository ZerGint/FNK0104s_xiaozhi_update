# FNK0104S custom firmware release 1.1.17

Two stable images are published for the board audio variants:

- fnk0104s-firmware-external-i2s.bin — external I2S amplifier (`external_amp`).
- fnk0104s-firmware-internal.bin — built-in ES8311/FM8002E amplifier (`internal_amp`).

The device selects the matching image from ota/stable.json using its compiled audio-output variant.