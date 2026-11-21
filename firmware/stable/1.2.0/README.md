# FNK0104S custom firmware release 1.2.0

- fnk0104s-firmware-external-i2s.bin — external I2S amplifier (external_amp).
- fnk0104s-firmware-internal.bin — built-in ES8311/FM8002E amplifier (internal_amp).

The device selects the matching image from ota/stable.json using its compiled audio-output variant.
The internal-amp image is built from the same commit with `CONFIG_FNK_EXTERNAL_I2S_SPEAKER`
disabled for the build (hence `dirty_worktree`).

Changes since 1.1.28:

- Settings menu (gear button under the navigation column): Network (Wi-Fi status, network, signal,
  IP address, Home Assistant portal), Screen (brightness, screensaver, avatar), Sound (volume,
  microphone level meter), System (board, firmware, free memory, clock correction, OTA slot, update).
  Quick Settings now holds only the volume.
- Avatar choice: Anime or Robo eyes (applied after a restart, with a confirmation).
- Screensaver replaces auto dimming: large clock, date, weather and the playing source, drifting
  slowly against burn-in; optional screen off after a minute.
- Status bar: time and date centred; the IP address moved to Settings > Network.
- Navigation icons: AI shows idle / listening / speaking; radio, music and generated-music icons
  turn green while their source plays.
- Music: "Artist - Title" from ID3 tags (cleaned file names otherwise), the playing item is
  highlighted, the player title no longer changes when browsing tabs; radio list favorites filter.
- Weather widget: wind arrow, weekdays on the forecast, "обн. HH:MM".
- Fix: on built-in-amplifier boards the assistant's speech could stay silent until the volume was
  changed.
- FNK0104B: new external-amplifier variant (external_amp, I2S on GPIO2/21/14, like FNK0104S).
