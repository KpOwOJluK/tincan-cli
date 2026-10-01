# Tincan — модифицированный fork для FakeDiscord

Это **не чистое зеркало upstream**. Репозиторий является настоящим fork проекта [bilalyazicioglu/tincan-cli](https://github.com/bilalyazicioglu/tincan-cli), поверх которого находятся изменения, необходимые для **FakeDiscord**.

Версия fork: **0.3.2-fd14**.

## Что изменено

### Приватный сервер
- постоянная identity координатора;
- одноразовые invite-коды;
- allowlist авторизованных устройств;
- список и отзыв устройств;
- host-only команды больше не могут уронить control task.

### Передача файлов
- отдельный `tincan/file/1` протокол;
- прямая P2P-передача по iroh/QUIC;
- публичные и recipient-only предложения;
- streaming download;
- BLAKE2s-256 проверка целостности;
- `.part` + atomic rename;
- защита от перезаписи;
- предпросмотр изображений;
- `/send`, `/sendto`, `/files`, `/get` и completion.

### PTT и звук
- настраиваемая клавиша PTT;
- корректные press/release события;
- поддержка F1-F12, букв, цифр, Space и CapsLock;
- глобальный read-only evdev listener на Linux;
- звуки фактического открытия/закрытия микрофона.

## Совместимость

Fork использует изменённый control protocol `tincan/control/4` и file protocol `tincan/file/1`, поэтому он не гарантирует полную protocol-совместимость с чистым upstream Tincan.

Полный desktop-проект находится здесь:

**https://github.com/KpOwOJluK/FakeDiscord**

## Разработка с ChatGPT

Модификации этого fork реализованы с существенной помощью **ChatGPT от OpenAI** под руководством и с проверкой владельца репозитория.

Подробный список отличий: [FORK_CHANGES.md](FORK_CHANGES.md).

Upstream README сохранён в [README_UPSTREAM.md](README_UPSTREAM.md).

Лицензия upstream — MIT, файл [LICENSE](LICENSE) сохранён.
