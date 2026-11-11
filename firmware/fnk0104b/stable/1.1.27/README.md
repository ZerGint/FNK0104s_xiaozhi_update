# FNK0104B custom firmware release 1.1.27

- fnk0104b-firmware.bin — FNK0104B (2.8-inch ILI9341, onboard amplifier, internal_amp).

Listed in ota/stable-fnk0104b.json.

Changes since 1.1.26:

- When the assistant starts radio or SD music, the conversation is closed first and then the source
  starts (as before 1.1.20). Fixes the AI hanging after "play radio" with the radio silent and the
  station missing from the local list.
- The radio, the AI and weather updates no longer use the network at the same time.
- Reconnects automatically when the server stops answering a new conversation.
