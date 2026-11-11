# FNK0104S custom firmware release 1.1.27

- fnk0104s-firmware-external-i2s.bin — external I2S amplifier (external_amp).
- fnk0104s-firmware-internal.bin — built-in ES8311/FM8002E amplifier (internal_amp).

The device selects the matching image from ota/stable.json using its compiled audio-output variant.
The internal-amp image is built from the same commit with `CONFIG_FNK_EXTERNAL_I2S_SPEAKER`
disabled for the build (hence `dirty_worktree`).

Changes since 1.1.26:

- When the assistant starts radio or SD music, the conversation is closed first and then the source
  starts (as before 1.1.20). Fixes the AI hanging after "play radio" with the radio silent and the
  station missing from the local list.
- The radio, the AI and weather updates no longer use the network at the same time.
- Reconnects automatically when the server stops answering a new conversation.
