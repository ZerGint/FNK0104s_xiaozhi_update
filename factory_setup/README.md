# FNK0104S factory setup

This directory contains the files needed for a fresh FNK0104S setup.

- `FNKMusicBridge-1.1.6.zip` вЂ” latest packaged FNKMusicBridge archive available in the workspace.
- `factory_bin/fnk0104s-factory-1.1.15-merged.bin` вЂ” complete 16 MB factory image containing the bootloader, partition table, OTA data, application, and assets.

The bridge archive is stored with Git LFS. A direct download is available at:

`https://media.githubusercontent.com/media/ZerGint/FNK0104s_xiaozhi_update/main/factory_setup/FNKMusicBridge-1.1.6.zip`

The merged image is written at flash offset `0x0`:

```text
esptool.py --chip esp32s3 --before default-reset --after hard-reset write-flash 0x0 factory_bin/fnk0104s-factory-1.1.15-merged.bin
```

After a full factory flash, configure Wi-Fi and the device settings again. The image does not preserve the device's private NVS data.


