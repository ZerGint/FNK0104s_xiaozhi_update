# FNK0104S custom firmware release 1.1.20

Two stable images are published for the board audio variants:

- fnk0104s-firmware-external-i2s.bin — external I2S amplifier (external_amp).
- fnk0104s-firmware-internal.bin — built-in ES8311/FM8002E amplifier (internal_amp).

The device selects the matching image from ota/stable.json using its compiled audio-output variant.

Bootloader, partition table and the assets partition are unchanged since
1.1.18, so the application image is the complete update for devices on 1.1.18.
The internal-amp image is built from the same commit with
`CONFIG_FNK_EXTERNAL_I2S_SPEAKER` disabled for the build (hence
`dirty_worktree`), as for earlier releases.

Changes since 1.1.18 (radio, player and assistant interaction):

- Stopping media no longer flushes queued TTS or the wake popup.
- Media is paused for server notifications and server-initiated speech.
- Media starts never close a newer voice session; resume after a conversation runs in place.
- Assistant-initiated media lets the spoken acknowledgement finish.
- Blocking MCP tools (Radio Browser, music bridge, Home Assistant, SD scans) run on a background worker.
- Explicit media.pause / new media.resume; next/previous keep a parked radio station.
- Radio: startup timeout, reconnect backoff with Wi-Fi wait, PSRAM buffers.
- SD player: bounded skipping of unplayable files, no lost track changes.
- Thread-safety fixes, 64 KiB Radio Browser response cap, no SD scan on the LVGL task,
  wake word stays enabled during a music download.
