# Factory images

## 1.2.0 (current)

Full 16 MB images (bootloader, partition table, OTA data, application, assets). Write at offset `0x0`;
a full image erases NVS (Wi-Fi, settings, server activation). Choose the image by board and amplifier:
later OTA updates keep the same board and amplifier variant.

| File | Device | Size | SHA-256 |
|---|---|---|---|
| `FNK0104S_1.2.0_external_amp_full_0x0.bin` | FNK0104S, внешний усилитель (external_amp) | 11232544 | `efcd25422ad89f9b2b5867305da36c6f66e0fb96ffb8fc4668cc2b4ae90e1386` |
| `FNK0104S_1.2.0_internal_amp_full_0x0.bin` | FNK0104S, встроенный усилитель (internal_amp) | 11232544 | `d8500cf1a1d5fbeaf75e53adb61224ff70674b83d9feb1ae73ec5b8279fe38fc` |
| `FNK0104B_1.2.0_internal_amp_full_0x0.bin` | FNK0104B, встроенный усилитель (internal_amp) | 10831032 | `ce9b2443fd5e9d6d1c05f147a647e2fefdce181f6b1f403d59d1f33e8120c522` |
| `FNK0104B_1.2.0_external_amp_full_0x0.bin` | FNK0104B, внешний усилитель (external_amp) | 10831032 | `9fc2c7bd789ddfc0640168642f0c38e7c6873451336c3e01204ec9a8a9d3d48e` |

```text
esptool.py --chip esp32s3 --before default-reset --after hard-reset write-flash 0x0 <file>
```

## Older images

Earlier full images (1.1.15, 1.1.26) remain in this directory for rollback.
