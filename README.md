# Скрипты для [ITD-SDK](https://github.com/firedotguy/itd-sdk)

Набор скриптов для работы с ITD (загрузка файлов и управление профилем).

## Содержание

* [Описание](#описание)
* [Установка](#установка)
* [Использование](#использование)
* [CLI скрипт изменения баннера](#cli-скрипт-изменения-баннера)
* [Переменные окружения](#переменные-окружения)
* [Примеры](#примеры)
* [Лицензия](#лицензия)

## Описание

`itd-scripts` предоставляет удобный способ:

* загружать файлы на сервер ITD,
* обновлять баннер профиля,
* управлять изображениями через CLI.

## Установка

1. Клонируем репозиторий:

```bash
git clone https://github.com/kilyabin/itd-scripts.git
cd itd-scripts
```

2. Устанавливаем зависимости:

```bash
pip install -r requirements.txt
```
или

```bash
pip install itd-sdk
```
(пока одна зависимость xD)

## Использование

Импортировать и использовать скрипты можно в своих проектах:

```python
from itd import ITDClient

client = ITDClient(None, 'YOUR_REFRESH_TOKEN')

# Загрузка файла
with open('banner.png', 'rb') as f:
    response = client.upload_file('banner.png', f)

# Обновление баннера профиля
client.update_profile(banner_id=str(response.id))
```

## CLI скрипт изменения баннера

Файл: `itd-change-banner.py`

Позволяет загружать изображение и сразу устанавливать его как баннер профиля.

### Аргументы

* `--token` — Refresh token (или через переменную окружения `ITD_TOKEN`)
* `--file` — Путь к изображению
* `--name` — Имя файла на сервере (по умолчанию используется имя локального файла)

### Пример использования

```bash
# Через переменную окружения
export ITD_TOKEN=YOUR_REFRESH_TOKEN
python itd-change-banner.py --file banner.png

# Через аргумент
python itd-change-banner.py --token YOUR_REFRESH_TOKEN --file banner.png --name new_banner.png
```

### Вывод

Скрипт выводит:

* Статус загрузки баннера
* id файла
* URL загруженного файла
* mime_type
* размер файла

## Переменные окружения

* `ITD_TOKEN` — Refresh token для работы скриптов без явного указания токена в командной строке.

## Примеры

```bash
# Загрузка файла и установка баннера через Python скрипт
python itd-change-banner.py --token $ITD_TOKEN --file /home/user/banner.jpg
```

```python
# Пример использования в коде
from itd import ITDClient

client = ITDClient(None, 'YOUR_REFRESH_TOKEN')
with open('banner.png', 'rb') as f:
    resp = client.upload_file('banner.png', f)
client.update_profile(banner_id=str(resp.id))
```

## Лицензия

MIT License. Смотрите файл `LICENSE` для подробностей.
