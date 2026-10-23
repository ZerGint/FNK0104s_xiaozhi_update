# Формат OTA-манифеста FNK0104S

Устройство читает `ota/stable.json` и выбирает запись по встроенному варианту аудиовыхода. Поддерживаются `external_amp` и `internal_amp`. Все URL прошивок должны быть HTTPS.

## Схема 2

Текущий стабильный канал использует одну запись на каждый вариант усилителя:

```json
{
  "schema": 2,
  "channel": "stable",
  "board": "freenove-fnk0104s",
  "chip": "esp32s3",
  "variants": {
    "external_amp": {
      "variant": "external_amp",
      "release_id": "1.1.17_external_amp",
      "version": "1.1.17",
      "build": "git-sha-or-build-id",
      "board": "freenove-fnk0104s",
      "chip": "esp32s3",
      "size": 4062576,
      "sha256": "64-lowercase-hex-characters",
      "url": "https://raw.githubusercontent.com/.../fnk0104s-firmware-external-i2s.bin"
    },
    "internal_amp": {
      "variant": "internal_amp",
      "release_id": "1.1.17_internal_amp",
      "version": "1.1.17",
      "build": "git-sha-or-build-id",
      "board": "freenove-fnk0104s",
      "chip": "esp32s3",
      "size": 4059488,
      "sha256": "64-lowercase-hex-characters",
      "url": "https://raw.githubusercontent.com/.../fnk0104s-firmware-internal.bin"
    }
  }
}
```

Устройство выбирает `external_amp` для сборки с внешним I2S-усилителем и `internal_amp` для сборки со встроенным усилителем. Несовместимый образ не скачивается и не устанавливается.

Каждая запись обязана содержать `variant`, `release_id`, числовую версию `version`, `build`, `board`, `chip`, точный `size`, SHA-256 и HTTPS `url`. Поле `variant` должно совпадать с ключом и с вариантом, скомпилированным в устройстве.

## Схема 1 (legacy)

Старые каналы могут использовать объект `firmware` вместо `variants`:

```json
{
  "schema": 1,
  "channel": "stable",
  "firmware": null
}
```

Для заполненного legacy-манифеста сохраняются поля `version`, `build`, `board`, `chip`, `size`, `sha256` и `url`.

## Текущий layout

- `ota/stable.json` — единый манифест стабильного канала, схема 2.
- `firmware/stable/1.1.17/fnk0104s-firmware-external-i2s.bin` — OTA для внешнего усилителя.
- `firmware/stable/1.1.17/fnk0104s-firmware-internal.bin` — OTA для внутреннего усилителя.
- `factory_setup/factory_bin/` — полные образы для заводской прошивки.

Для новых выпусков предпочтительны GitHub Release assets. Если бинарники хранятся в `firmware/`, URL, размер и SHA-256 в манифесте должны в точности соответствовать файлам.

## Проверка безопасности

Прошивка скачивает файл во временный путь на SD, проверяет размер и SHA-256, проверяет метаданные образа, атомарно переводит файл в staging, а минимальный установщик повторяет проверку перед записью неактивного OTA-раздела. После первого запуска ESP-IDF подтверждает или откатывает образ.