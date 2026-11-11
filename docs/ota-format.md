# Формат OTA-манифестов FNK0104S и FNK0104B

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

## Манифест FNK0104B

FNK0104B читает отдельный файл `ota/stable-fnk0104b.json` той же схемы 2. В нём одна запись
`internal_amp` (у B нет внешнего усилителя) с `"board": "freenove-fnk0104b"`. Устройство B
принимает образ только при совпадении `board` и `variant` в манифесте, в запросе на установку и в
метаданных загруженного образа. Образ S не может быть установлен на B и наоборот.
`ota/stable.json` остаётся манифестом FNK0104S, чтобы не затронуть уже выпущенные устройства.

## Манифест Waveshare ESP32-P4 4.3"

P4 читает `ota/stable-p4-4.3.json` (схема 2, `"board": "waveshare-p4-4.3"`, `"chip": "esp32p4"`).
Ключ в `variants` — язык сборки (`RU`, в будущем `EN` и т. д.), и в записи то же значение в поле
`language`. Устройство берёт только запись своего языка, поэтому не может установить сборку на
другом языке. Образ — только приложение (`build/xiaozhi.bin`, не merged), путь
`firmware/p4-4.3/stable/<версия>/<язык>/p4-4.3-firmware.bin`. Образ пишется в неактивный раздел
XiaoZhi (OTA0/OTA1); игровые разделы P4 не затрагиваются. Метаданные выпуска:
`firmware/p4-4.3/stable/<версия>/firmware-info-<язык>.json`.

## Текущий layout

- `ota/stable.json` — манифест стабильного канала FNK0104S, схема 2.
- `ota/stable-fnk0104b.json` — манифест стабильного канала FNK0104B, схема 2.
- `firmware/fnk0104b/stable/1.1.26/fnk0104b-firmware.bin` — OTA для FNK0104B.
- `firmware/stable/1.1.26/fnk0104s-firmware-external-i2s.bin` — OTA для внешнего усилителя.
- `firmware/stable/1.1.26/fnk0104s-firmware-internal.bin` — OTA для внутреннего усилителя.
- `factory_setup/factory_bin/` — полные образы для заводской прошивки.

Для новых выпусков предпочтительны GitHub Release assets. Если бинарники хранятся в `firmware/`, URL, размер и SHA-256 в манифесте должны в точности соответствовать файлам.

## Проверка безопасности

Прошивка скачивает файл во временный путь на SD, проверяет размер и SHA-256, проверяет метаданные образа, атомарно переводит файл в staging, а минимальный установщик повторяет проверку перед записью неактивного OTA-раздела. После первого запуска ESP-IDF подтверждает или откатывает образ.