# Формат OTA-манифеста FNK0104S

Устройство читает `ota/stable.json` и выбирает запись по встроенному варианту аудиовыхода. Поддерживаются `external_amp` и `internal_amp`.

## Схема 2

```json
{
  "schema": 2,
  "channel": "stable",
  "board": "freenove-fnk0104s",
  "chip": "esp32s3",
  "variants": {
    "external_amp": {
      "variant": "external_amp",
      "release_id": "1.1.16_external_amp",
      "version": "1.1.16",
      "build": "git-sha-or-build-id",
      "board": "freenove-fnk0104s",
      "chip": "esp32s3",
      "size": 4036816,
      "sha256": "64-lowercase-hex-characters",
      "url": "https://raw.githubusercontent.com/.../fnk0104s-firmware.bin"
    },
    "internal_amp": { }
  }
}
```

Каждая запись в `variants` обязана содержать `variant`, `release_id`, числовую версию `version`, `build`, `board`, `chip`, точный `size`, SHA-256 и HTTPS `url`. Поле `variant` должно совпадать с ключом и с вариантом, скомпилированным в устройство. Несовместимый образ не скачивается и не устанавливается.

## Текущий layout

- `ota/stable.json` — единый манифест схемы 2.
- `firmware/stable/1.1.16_external_amp/fnk0104s-firmware.bin` — OTA для внешнего усилителя.
- `firmware/stable/1.1.16_internal_amp/fnk0104s-firmware.bin` — OTA для внутреннего усилителя.
- `factory_setup/factory_bin/` — полные образы для заводской прошивки, включая варианты 1.1.15.

## Проверка безопасности

Прошивка скачивает файл во временный путь на SD, проверяет размер и SHA-256, проверяет метаданные образа, атомарно переводит файл в staging, а минимальный установщик повторяет проверку перед записью неактивного OTA-раздела. После первого запуска ESP-IDF подтверждает или откатывает образ.
