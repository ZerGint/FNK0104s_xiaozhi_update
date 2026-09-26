# FNK0104S XiaoZhi Update Repository

This repository hosts OTA update metadata for the custom FNK0104S XiaoZhi firmware.

## Layout

- `ota/stable.json` — stable-channel manifest used by the device.
- `ota/beta.json` — optional beta-channel manifest.
- `docs/ota-format.md` — manifest schema and release conventions.

Firmware binaries should be attached to GitHub Releases rather than committed to this repository.

Recommended release asset name:

`fnk0104s-firmware.bin`

Intended device flow:

1. Fetch a channel manifest.
2. Compare the offered version with the installed firmware.
3. Download the firmware asset to SD staging.
4. Verify size, SHA-256, chip/project metadata.
5. Ask the user for installation approval.
6. Reboot into a minimal installer mode.
7. Re-verify and write to the inactive OTA partition.
8. Reboot into the new firmware and validate/rollback as needed.
