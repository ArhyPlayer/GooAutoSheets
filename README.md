# GooAutoSheets

Инструменты для работы с Google Таблицами через API: CRUD-клиент и генератор отчётов с графическим интерфейсом.

## Установка

```bash
python -m venv .venv
.venv\Scripts\activate   # Windows
pip install -r requirements.txt
```

## Настройка

1. Скопируйте `env-example` в `.env`:
   ```bash
   copy env-example .env
   ```

2. Укажите в `.env`:
   - `GOOGLE_CREDENTIALS_PATH` — путь к JSON-ключу сервисного аккаунта (например, `excel-factory-488906-cd544edd406e.json`)
   - `GOOGLE_SPREADSHEET_ID` — ID таблицы из URL (часть между `/d/` и `/edit`)

3. Создайте сервисный аккаунт в [Google Cloud Console](https://console.cloud.google.com/), скачайте JSON-ключ и добавьте его email как редактора в вашу Google Таблицу.

## Использование

### Генератор отчётов (GUI)

```bash
python report_app.py
```

Приложение позволяет сформировать случайный отчёт (продажи, производство, персонал) и сохранить его в Google Таблицу в виде оформленного документа.

### CRUD-клиент (модуль)

```python
from google_sheets_client import GoogleSheetsClient

client = GoogleSheetsClient(
    spreadsheet_id="your_spreadsheet_id",
    credentials_path="excel-factory-488906-cd544edd406e.json",
)

# Чтение
rows = client.read_all()
rows = client.read_range("A1:D10")

# Запись
client.write_range("A1", [["Заголовок"], ["Строка 1"]])
client.append_rows([["Новая строка"]])
client.update_cell("B2", "Значение")

# Очистка
client.clear_range("A1:Z100")

# Метаданные
sheet_names = client.get_sheet_names()
```

### Проверка подключения

```bash
python google_sheets_client.py
```

Выведет список листов и содержимое первого листа.

## Структура проекта

| Файл | Описание |
|------|----------|
| `google_sheets_client.py` | CRUD-клиент для Google Sheets API v4 |
| `report_app.py` | Tkinter-приложение для генерации отчётов |
| `env-example` | Пример переменных окружения |
| `requirements.txt` | Зависимости Python |

## Требования

- Python 3.10+
- Сервисный аккаунт Google Cloud с доступом к Google Sheets API
