# FNK0104S XiaoZhi OTA

Репозиторий содержит OTA-обновления FNK0104S с раздельными каналами для усилителей. Устройство автоматически выбирает запись `external_amp` или `internal_amp` из `ota/stable.json` по скомпилированному варианту аудиовыхода.

- Манифест: `ota/stable.json` (схема 2).
- OTA release 1.1.17: `firmware/stable/1.1.17/` (external and internal amplifier images).
- Полные заводские образы: `factory_setup/factory_bin/`.

Подробности формата и жизненного цикла обновления: [`docs/ota-format.md`](docs/ota-format.md).
