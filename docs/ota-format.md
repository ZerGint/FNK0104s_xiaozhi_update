# OTA manifest format

The FNK0104S custom firmware reads a small channel manifest from this repository and downloads the referenced firmware from a GitHub Release asset.

## Channel manifests

Stable channel:

`ota/stable.json`

Beta channel:

`ota/beta.json`

An empty channel uses:

```json
{
  "schema": 1,
  "channel": "stable",
  "firmware": null
}
```

A populated channel should use this shape:

```json
{
  "schema": 1,
  "channel": "stable",
  "firmware": {
    "version": "2.5.0",
    "build": "git-sha-or-build-id",
    "board": "freenove-fnk0104s",
    "chip": "esp32s3",
    "size": 3809296,
    "sha256": "64-lowercase-hex-characters",
    "url": "https://github.com/ZerGint/FNK0104s_xiaozhi_update/releases/download/v2.5.0/fnk0104s-firmware.bin"
  }
}
```

## Required firmware fields

- `version` — semantic firmware version shown to the device/user.
- `build` — source commit or build identifier.
- `board` — must be `freenove-fnk0104s`.
- `chip` — must be `esp32s3`.
- `size` — exact firmware binary size in bytes.
- `sha256` — SHA-256 of the exact release asset, encoded as 64 lowercase hexadecimal characters.
- `url` — immutable URL to the firmware asset for that release/tag.

## Release convention

Recommended tag:

`v<version>`

Recommended binary asset name:

`fnk0104s-firmware.bin`

Example:

`v2.5.0 / fnk0104s-firmware.bin`

Do not commit firmware binaries to the repository history. Store binaries as GitHub Release assets and keep only small manifests in Git.

## Update safety model

The intended firmware behavior is:

1. Download a candidate image to SD as a temporary file.
2. Verify transport completion and exact file size.
3. Calculate SHA-256 and compare it with the manifest.
4. Verify ESP image/chip/project metadata where supported.
5. Atomically promote the temporary file to a staged image.
6. Ask for local installation approval.
7. Reboot into a minimal installer.
8. Recompute SHA-256 before writing the inactive OTA partition.
9. Use ESP-IDF OTA validation and rollback for the first boot of the new app.

The channel manifest is metadata, not a substitute for ESP-IDF image validation or rollback.
