# 📚 Документация Forelka Userbot

> **Forelka** — мощный и гибкий Telegram userbot на базе Telethon с модульной архитектурой, поддержкой инлайн-бота и расширенной системой конфигурации.

---

## 📋 Содержание

1. [Обзор проекта](#обзор-проекта)
2. [Архитектура](#архитектура)
3. [Требования](#требования)
4. [Установка](#установка)
5. [Быстрый старт](#быстрый-старт)
6. [Конфигурация](#конфигурация)
7. [Основные компоненты](#основные-компоненты)
8. [Система модулей](#система-модулей)
9. [Команды](#команды)
10. [Инлайн-бот](#инлайн-бот)
11. [API Reference](#api-reference)
12. [Примеры использования](#примеры-использования)
13. [Troubleshooting](#troubleshooting)
14. [Безопасность](#безопасность)

---

## 📖 Обзор проекта

**Forelka Userbot** — это многофункциональный Telegram userbot, разработанный для автоматизации задач и расширения возможностей Telegram. Проект построен на асинхронной библиотеке **Telethon** и поддерживает:

- ✅ **Модульную архитектуру** — загрузка модулей из папок `modules/` и `loaded_modules/`
- ✅ **Инлайн-бота** — встроенный Telegram bot для интерактивного управления
- ✅ **Management Group** — группа с топиками для логов, команд, бекапов
- ✅ **Гибкую конфигурацию** — per-account конфиги с поддержкой алиасов
- ✅ **Систему овнеров** — управление правами доступа
- ✅ **Обратную связь** — пользователи могут отправлять сообщения через бота
- ✅ **Автоматическую установку зависимостей** — pip-пакеты для модулей
- ✅ **Веб-интерфейс авторизации** — HTML-страница для входа в Telegram
- ✅ **Туннелирование** — публичный доступ через localhost.run

### Версия
- **Текущая версия:** 1.0.0
- **Фреймворк:** Telethon
- **Язык:** Python 3.7+

---

## 🏗 Архитектура

```
forelka-userbot-telethon/
├── main.py                 # Точка входа, инициализация клиента
├── kernel.py               # Ядро системы, управление ботами
├── loader.py               # Загрузчик модулей, команды управления
├── database.py             # Работа с SQLite базой
├── inline_bot.py           # Инлайн-бот функциональность
├── meta_lib.py             # Утилиты для метаданных модулей
├── webapp.py               # Веб-интерфейс авторизации
├── tunnel.py               # Туннелирование через localhost.run
├── Updater.py              # Автообновление и рестарт
├── utils.py                # Вспомогательные утилиты
│
├── modules/                # Системные модули
│   ├── ping.py             # Проверка задержки
│   ├── help.py             # Справка по командам
│   ├── config.py           # Конфигурация через инлайн
│   ├── backup.py           # Бекап и восстановление
│   ├── feedback.py         # Обратная связь
│   ├── owner.py            # Управление овнерами
│   ├── logs.py             # Просмотр логов
│   ├── aliases.py          # Алиасы команд
│   ├── calculator.py       # Калькулятор
│   ├── prefix.py           # Смена префикса
│   ├── accounts.py         # Управление аккаунтами
│   ├── restart.py          # Перезапуск
│   ├── terminal.py         # Выполнение команд
│   └── info.py             # Информация о системе
│
├── loaded_modules/         # Пользовательские модули
│   ├── neofetch.py         # Системная информация
│   ├── ollama_ai.py        # AI интеграция
│   ├── autoreply.py        # Автоответы
│   └── image_processor.py  # Обработка изображений
│
├── config-<user_id>.json   # Конфигурация аккаунта
├── kernel_config-<user_id>.json  # Конфигурация ядра
├── repos.json              # Список репозиториев модулей
├── forelka_config.db       # SQLite база конфигураций
└── forelka.log             # Лог-файл
```

### Поток выполнения

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│   main.py   │────▶│  kernel.py  │────▶│ inline_bot.py│
└─────────────┘     └─────────────┘     └─────────────┘
       │                   │                     │
       ▼                   ▼                     ▼
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│  loader.py  │────▶│  modules/   │     │   database  │
└─────────────┘     └─────────────┘     └─────────────┘
```

---

## 📦 Требования

### Минимальные требования
- **Python:** 3.7 или выше
- **ОС:** Linux, macOS, Windows, Android (Termux)
- **Память:** 100+ MB RAM
- **Место:** 50+ MB свободного места

### Зависимости

Основные пакеты устанавливаются автоматически:

```bash
pip install telethon aiosqlite flask pyrogram requests aiohttp
```

### Для Termux (Android)

```bash
pkg update && pkg upgrade
pkg install python git openssh neofetch
pip install telethon aiosqlite flask pyrogram requests aiohttp
```

---

## ⚙️ Установка

### 1. Клонирование репозитория

```bash
git clone https://github.com/kirillusha/forelka-userbot-telethon.git
cd forelka-userbot-telethon
```

### 2. Установка зависимостей

```bash
pip install -r requirements.txt
```

Если файла `requirements.txt` нет, установите вручную:

```bash
pip install telethon aiosqlite flask pyrogram requests aiohttp
```

### 3. Получение API ключей

1. Перейдите на [my.telegram.org](https://my.telegram.org)
2. Авторизуйтесь по номеру телефона
3. Перейдите в **API development tools**
4. Создайте новое приложение
5. Скопируйте **API ID** и **API HASH**

---

## 🚀 Быстрый старт

### Запуск бота

```bash
python main.py
```

### Первый запуск

При первом запуске вам будет предложено выбрать способ авторизации:

```
No session found.
Choose login method:
  1) Terminal (API ID/HASH + phone in terminal)
  2) Web panel (HTML login page)
  3) Web + tunnel (HTML + public localhost.run URL)
> 
```

#### Способ 1: Terminal (рекомендуется для локального использования)

```bash
> 1
API ID: 12345678
API HASH: abcdef0123456789
```

Введите номер телефона и код из Telegram.

#### Способ 2: Web panel

```bash
> 2
Web panel: http://127.0.0.1:8000
```

Откройте в браузере `http://127.0.0.1:8000` и пройдите авторизацию.

#### Способ 3: Web + Tunnel

```bash
> 3
Web panel: http://127.0.0.1:8000
Public URL: https://abc123.localhost.run
```

Откройте публичный URL для авторизации с любого устройства.

### После авторизации

Бот автоматически:
1. Создаст сессию `forelka-<user_id>.session`
2. Сохранит API ключи в `telegram_api-<user_id>.json`
3. Создаст Management Group с топиками
4. Настроит инлайн-бота

---

## 🔧 Конфигурация

### Файлы конфигурации

#### 1. `config-<user_id>.json` — Конфигурация аккаунта

```json
{
    "management_group_id": -1001234567890,
    "management_topics": {
        "Логи": 2,
        "Команды": 3,
        "Бекапы": 4,
        "Мусорка": 5
    },
    "owners": [YOUR_USER_ID_HERE],
    "aliases": {
        "p": "ping"
    },
    "prefix": "."
}
```

| Параметр | Тип | Описание |
|----------|-----|----------|
| `management_group_id` | integer | ID группы управления |
| `management_topics` | object | ID топиков для разных целей |
| `owners` | array | Список ID владельцев |
| `aliases` | object | Алиасы команд |
| `prefix` | string | Префикс команд (по умолчанию `.`) |

#### 2. `kernel_config-<user_id>.json` — Конфигурация ядра

```json
{
    "inline_bot_token": "YOUR_BOT_TOKEN_HERE",
    "inline_bot_username": "your_bot_username",
    "api_id": 12345678,
    "api_hash": "your_api_hash_here"
}
```

| Параметр | Тип | Описание |
|----------|-----|----------|
| `inline_bot_token` | string | Токен инлайн-бота |
| `inline_bot_username` | string | Username инлайн-бота |
| `api_id` | integer | API ID Telegram |
| `api_hash` | string | API HASH Telegram |

#### 3. `repos.json` — Репозитории модулей

```json
[
    "https://github.com/kirillusha/forelka-userbot-modules",
    "https://raw.githubusercontent.com/Kirillusha/forelka-userbot-modules/refs/heads/main"
]
```

#### 4. `forelka_config.db` — База данных конфигураций

SQLite база для хранения настроек модулей.

---

### Управление конфигурацией

#### Смена префикса

```bash
.prefix !
# Теперь команды: !help, !ping, и т.д.
```

#### Создание алиаса

```bash
.alias p ping
# Теперь .p работает как .ping
```

#### Удаление алиаса

```bash
.delalias p
```

#### Список алиасов

```bash
.aliases
```

---

## 🧩 Основные компоненты

### 1. Kernel (`kernel.py`)

**Kernel** — центральное ядро системы, управляющее всеми компонентами.

#### Основные методы:

| Метод | Описание |
|-------|----------|
| `bind_client(client)` | Привязывает Telegram клиент |
| `setup_inline_bot()` | Настраивает инлайн-бота |
| `register_bot_command(cmd, handler)` | Регистрирует команду бота |
| `register_inline_handler(handler)` | Регистрирует инлайн-обработчик |
| `register_callback_handler(handler)` | Регистрирует обработчик кнопок |
| `send_to_topic(topic_name, text)` | Отправляет сообщение в топик |
| `get_module_config(module_name)` | Получает конфиг модуля |
| `stop()` | Останавливает все компоненты |

#### Пример использования:

```python
kernel = Kernel()
kernel.bind_client(client)
await kernel.setup_inline_bot()
kernel.register_bot_command("ping", ping_handler)
```

---

### 2. Loader (`loader.py`)

**Loader** — система загрузки и управления модулями.

#### Команды loader:

| Команда | Описание |
|---------|----------|
| `.dlm <module>` | Скачать модуль из репозитория |
| `.lm` | Загрузить модуль из файла (ответом) |
| `.ulm <name>` | Удалить модуль |
| `.ml <name>` | Отправить файл модуля |
| `.addrepo <url>` | Добавить репозиторий |
| `.pip install <pkg>` | Установить pip пакет |
| `.pip uninstall <pkg>` | Удалить pip пакет |
| `.pip list` | Список установленных пакетов |
| `.pip show <pkg>` | Информация о пакете |

#### Примеры:

```bash
# Добавить репозиторий
.addrepo https://github.com/user/repo

# Скачать модуль
.dlm weather

# Скачать по прямой ссылке
.dlm https://raw.githubusercontent.com/user/repo/main/weather.py

# Загрузить из файла (ответом на .py файл)
.lm

# Установить зависимость
.pip install pillow

# Удалить модуль
.ulm weather
```

---

### 3. Inline Bot (`inline_bot.py`)

**InlineBot** — встроенный Telegram bot для интерактивного управления.

#### Возможности:

- ✅ Команды бота (`/ping`, `/calc`, `/feedback`)
- ✅ Инлайн-запросы (`@bot ping`, `@bot calc 2+2`)
- ✅ Интерактивные кнопки
- ✅ Обратная связь от пользователей
- ✅ Отправка сообщений в топики

#### Настройка бота:

При первом запуске:

```
1. Автоматически создать бота
2. Ввести токен вручную
Выберите (1/2): 
```

**Автоматическое создание:**
- Бот создаётся через @BotFather
- Токен сохраняется в конфиг

**Ручная настройка:**
- Введите существующий токен бота
- Введите username бота

---

### 4. Database (`database.py`)

**Database** — работа с SQLite базой данных.

#### Методы:

| Метод | Описание |
|-------|----------|
| `set(key, value)` | Установить значение |
| `get(key, default)` | Получить значение |
| `close()` | Закрыть соединение |

---

### 5. Meta Library (`meta_lib.py`)

**Meta Library** — утилиты для работы с метаданными модулей.

#### Функции:

| Функция | Описание |
|---------|----------|
| `read_module_meta(module, name, commands)` | Читает метаданные модуля |
| `extract_command_descriptions(meta)` | Извлекает описания команд |
| `build_meta(...)` | Создаёт структуру метаданных |

#### Формат метаданных модуля:

```python
__meta__ = {
    "name": "Weather",
    "version": "1.0.0",
    "author": "Author Name",
    "description": "Модуль для прогноза погоды",
    "commands": ["weather", "forecast"],
    "requires": ["aiohttp", "pillow>=1.0"]
}
```

---

## 📚 Система модулей

### Структура модуля

```python
from telethon.tl.custom import Message

# Метаданные (опционально)
__meta__ = {
    "name": "MyModule",
    "version": "1.0.0",
    "author": "Author",
    "description": "Описание модуля",
    "commands": ["cmd1", "cmd2"]
}

# Команда
async def cmd1_cmd(client, message, args):
    """Описание команды"""
    await message.edit("Hello!")

# Регистрация
def register(app, commands, module_name, kernel=None):
    commands["cmd1"] = {"func": cmd1_cmd, "module": module_name}
```

### Типы register функций

Модуль может иметь разные сигнатуры `register`:

```python
# 4 параметра (полная)
def register(app, commands, module_name, kernel):
    ...

# 3 параметра
def register(app, commands, module_name):
    ...

# 2 параметра
def register(app, commands):
    ...

# 1 параметр
def register(app):
    ...

# Без параметров
def register():
    ...
```

### Папки модулей

| Папка | Описание |
|-------|----------|
| `modules/` | Системные модули (защищены от удаления) |
| `loaded_modules/` | Пользовательские модули |

### Зависимости модулей

Модуль может указать зависимости:

```python
# Вариант 1: В __meta__
__meta__ = {
    "requires": ["aiohttp", "pillow>=1.0"]
}

# Вариант 2: Отдельная переменная
__requires__ = ["aiohttp", "pillow"]

# Вариант 3: Строка
__requires__ = "aiohttp, pillow"
```

Зависимости устанавливаются автоматически при загрузке модуля.

---

## 🎮 Команды

### Системные команды

| Команда | Описание | Пример |
|---------|----------|--------|
| `.help` | Показать список модулей | `.help`, `.help ping` |
| `.ping` | Проверить задержку | `.ping` |
| `.prefix` | Сменить префикс | `.prefix !` |
| `.restart` | Перезапустить бота | `.restart` |
| `.update` | Обновить из git | `.update` |
| `.log` | Отправить логи | `.log` |
| `.backup` | Создать бекап | `.backup` |
| `.restore` | Восстановить из бекапа | (ответом на ZIP) |

### Управление овнерами

| Команда | Описание | Пример |
|---------|----------|--------|
| `.owners` | Список овнеров | `.owners` |
| `.addowner` | Добавить овнера | `.addowner 123456` |
| `.delowner` | Удалить овнера | `.delowner 123456` |

### Модули

| Команда | Описание | Пример |
|---------|----------|--------|
| `.calc` | Калькулятор | `.calc 2 + 2 * 5` |
| `.alias` | Создать алиас | `.alias p ping` |
| `.delalias` | Удалить алиас | `.delalias p` |
| `.aliases` | Список алиасов | `.aliases` |
| `.config` | Конфигурация (инлайн) | `.config` |
| `.feedback` | Режим обратной связи | `/feedback` (в боте) |
| `.neofetch` | Системная информация | `.neofetch` |

### Загрузчик модулей

| Команда | Описание | Пример |
|---------|----------|--------|
| `.dlm` | Скачать модуль | `.dlm weather` |
| `.lm` | Загрузить из файла | (ответом на .py) |
| `.ulm` | Удалить модуль | `.ulm weather` |
| `.ml` | Отправить модуль | `.ml weather` |
| `.addrepo` | Добавить репозиторий | `.addrepo https://...` |
| `.pip` | Управление pip | `.pip install aiohttp` |

---

## 🤖 Инлайн-бот

### Команды бота

| Команда | Описание | Пример |
|---------|----------|--------|
| `/start` | Приветственное меню | `/start` |
| `/ping` | Проверка задержки | `/ping` |
| `/calc` | Калькулятор | `/calc 2+2` |
| `/feedback` | Режим обратной связи | `/feedback` |

### Инлайн-запросы

Используйте `@username_bot` в любом чате:

```
@your_bot_username ping
@your_bot_username calc 2+2*5
@your_bot_username config
```

### Интерактивная конфигурация

Команда `.config` открывает инлайн-меню для настройки модулей:

```
⚙️ Панель конфигурации
├── 🧩 Модули
│   └── [список модулей с настройками]
└── 🌐 Общие
```

---

## 📖 API Reference

### Класс `Kernel`

```python
class Kernel:
    def __init__(self):
        """Инициализация ядра"""
        
    def bind_client(self, client: TelegramClient):
        """Привязка клиента"""
        
    async def setup_inline_bot(self):
        """Настройка инлайн-бота"""
        
    def register_bot_command(self, command: str, handler):
        """Регистрация команды бота"""
        
    def register_inline_handler(self, handler):
        """Регистрация инлайн-обработчика"""
        
    def register_callback_handler(self, handler):
        """Регистрация обработчика кнопок"""
        
    async def send_to_topic(self, topic_name: str, text: str):
        """Отправка в топик management-группы"""
        
    async def get_module_config(self, module_name: str) -> dict:
        """Получение конфигурации модуля"""
        
    async def stop(self):
        """Остановка ядра"""
```

### Класс `InlineBot`

```python
class InlineBot:
    def __init__(self, kernel: Kernel):
        """Инициализация инлайн-бота"""
        
    async def setup(self):
        """Настройка бота"""
        
    async def start_bot(self):
        """Запуск бота"""
        
    async def stop_bot(self):
        """Остановка бота"""
```

### Формат команды

```python
commands = {
    "command_name": {
        "func": async_function,      # Функция обработчика
        "module": "module_name",     # Название модуля
        "description": "Описание"    # Описание (опционально)
    }
}
```

### Сигнатура обработчика команды

```python
async def command_handler(
    client: TelegramClient,
    message: Message,
    args: List[str]
):
    """
    client — клиент Telethon
    message — сообщение команды
    args — аргументы после команды
    """
    await message.edit("Response")
```

---

## 💡 Примеры использования

### 1. Создание собственного модуля

Создайте файл `loaded_modules/hello.py`:

```python
__meta__ = {
    "name": "Hello",
    "version": "1.0.0",
    "author": "Your Name",
    "description": "Приветственный модуль",
    "commands": ["hello", "greet"]
}

async def hello_cmd(client, message, args):
    """Отправить приветствие"""
    name = " ".join(args) if args else "мир"
    await message.edit(f"👋 Привет, {name}!")

async def greet_cmd(client, message, args):
    """Альтернативное приветствие"""
    await message.edit("🌟 Добро пожаловать!")

def register(app, commands, module_name):
    commands["hello"] = {"func": hello_cmd, "module": module_name}
    commands["greet"] = {"func": greet_cmd, "module": module_name}
```

Загрузите модуль:

```bash
.lm (ответом на файл hello.py)
# или
.dlm hello (если есть в репозитории)
```

### 2. Модуль с зависимостями

```python
__meta__ = {
    "name": "ImageProcessor",
    "requires": ["pillow>=9.0", "numpy"]
}

from PIL import Image

async def process_cmd(client, message, args):
    # Обработка изображений
    pass

def register(app, commands, module_name):
    commands["process"] = {"func": process_cmd, "module": module_name}
```

### 3. Модуль с конфигурацией

```python
__meta__ = {
    "name": "AutoReply",
    "description": "Автоматические ответы"
}

async def get_config(kernel, module_name):
    return {
        "enabled": {
            "name": "Включено",
            "type": "bool",
            "default": True,
            "description": "Включить автоответы"
        },
        "delay": {
            "name": "Задержка",
            "type": "int",
            "default": 5,
            "description": "Задержка в секундах"
        }
    }

def register(app, commands, module_name, kernel):
    if kernel:
        kernel.module_configs[module_name] = get_config
```

### 4. Использование инлайн-бота в модуле

```python
async def inline_handler(event):
    query = event.text
    builder = event.builder
    result = builder.article(
        title="Результат",
        text=f"Вы запросили: {query}"
    )
    await event.answer([result])

def register(app, commands, module_name, kernel):
    if kernel:
        kernel.register_inline_handler(inline_handler)
```

---

## 🔧 Troubleshooting

### Ошибки при запуске

#### `ModuleNotFoundError: No module named 'telethon'`

```bash
pip install telethon
```

#### `Session file not found`

Удалите повреждённые сессии:

```bash
rm forelka-*.session
python main.py
```

#### `API ID/HASH не найдены`

Проверьте файлы:
- `telegram_api-<user_id>.json`
- `kernel_config-<user_id>.json`

### Ошибки модулей

#### Модуль не загружается

Проверьте:
1. Наличие функции `register`
2. Правильную сигнатуру `register`
3. Отсутсвие синтаксических ошибок

```bash
python -m py_compile loaded_modules/module.py
```

#### Зависимости не устанавливаются

```bash
.pip install <package>
# или вручную
pip install <package>
```

### Ошибки инлайн-бота

#### Бот не отвечает

1. Проверьте токен в `kernel_config-<user_id>.json`
2. Убедитесь, что бот добавлен в овнеры
3. Перезапустите бота: `.restart`

#### Ошибка "Доступ запрещен"

Добавьте себя в овнеры:

```bash
.addowner <ваш_id>
```

### Проблемы с туннелем

#### `ssh не найден`

```bash
# Termux
pkg install openssh

# Ubuntu/Debian
sudo apt install openssh-client
```

#### Туннель не создаётся

Проверьте переменные окружения:

```bash
export FORELKA_LHR_USER=nokey
export FORELKA_TUNNEL_VERBOSE=1
```

---

## 🔒 Безопасность

### Овнеры

Только овнеры могут:
- Использовать команды управления
- Получать доступ к логам
- Изменять конфигурацию
- Получать сообщения фидбека

### Защита сессий

- Файлы `.session` содержат чувствительные данные
- Не передавайте файлы сессий
- Используйте `.backup` для безопасного резервирования

### API ключи

- Храните `telegram_api-*.json` в секрете
- Не коммитьте в git
- При компрометации — отзовите на my.telegram.org

### Рекомендации

1. **Регулярные бекапы:** `.backup`
2. **Ограниченный доступ:** добавляйте только доверенных овнеров
3. **Обновления:** `.update` для получения исправлений безопасности
4. **Логи:** проверяйте `.log` на подозрительную активность

---

## 📄 Лицензия

Проект распространяется без явной лицензии. Все права защищены.

---

## 👥 Поддержка

- **GitHub:** [kirillusha/forelka-userbot-telethon](https://github.com/kirillusha/forelka-userbot-telethon)
- **Репозиторий модулей:** [kirillusha/forelka-userbot-modules](https://github.com/kirillusha/forelka-userbot-modules)

---

## 📝 Changelog

### Version 1.0.0

- ✅ Первая стабильная версия
- ✅ Модульная архитектура
- ✅ Инлайн-бот
- ✅ Management Group с топиками
- ✅ Система овнеров
- ✅ Обратная связь
- ✅ Веб-авторизация
- ✅ Туннелирование
- ✅ Автоустановка зависимостей

---

*Документация создана для Forelka Userbot v1.0.0*
