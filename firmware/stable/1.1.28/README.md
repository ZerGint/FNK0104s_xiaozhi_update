# FNK0104S custom firmware release 1.1.28

- fnk0104s-firmware-external-i2s.bin — external I2S amplifier (external_amp).
- fnk0104s-firmware-internal.bin — built-in ES8311/FM8002E amplifier (internal_amp).

The device selects the matching image from ota/stable.json using its compiled audio-output variant.
The internal-amp image is built from the same commit with `CONFIG_FNK_EXTERNAL_I2S_SPEAKER`
disabled for the build (hence `dirty_worktree`).

Changes since 1.1.27:

- New assistant tool music.play_online: finds one song in an online catalog by title and artist and
  plays it ("Музыка online" on the media screen, title and artist shown, next/previous disabled).
- The song continues from where it was heard after a conversation or a pause, and stops at its end.
- Online songs are not added to the radio list or favorites.
