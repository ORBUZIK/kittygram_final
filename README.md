# Kittygram

![Main page](/assets/images/main_page.png)

**Kittygram** — платформа, на которой пользователи могут регистрироваться, публиковать фотографии своих питомцев, указывать их достижения и любоваться котиками других участников.

Проект представляет собой полноценное веб-приложение, упакованное в контейнеры и с настроенным конвейером автоматизации (CI/CD).

<br>

## Технологический стек

### Backend
- **Python 3.10**
- **Django 3.2**
- **Django REST Framework**
- **Djoser**
- **PostgreSQL**
- **Gunicorn**

### Frontend
- **React**
- **Node.js**
- **CSS Modules**

### Инфраструктура и DevOps
- **Docker & Docker Compose**
- **Nginx** (Reverse Proxy / Gateway)
- **GitHub Actions** (CI/CD: Линтинг, тесты, сборка образов)
- **Telegram Bot SDK** (Уведомления о статусе деплоя)
- **Ruff** (Линтер)

<br>

## Как запустить проект локально

### 1. Клонируйте репозиторий:
```bash
git clone https://github.com/ORBUZIK/kittygram_final.git
cd kittygram_final
```

### 2. Создайте файл .env:
В корневой директории создайте файл `.env` и заполните его по образцу:
```env
POSTGRES_DB=django
POSTGRES_USER=django
POSTGRES_PASSWORD=django
DB_HOST=db
DB_PORT=5432
SECRET_KEY=ваш_секретный_ключ_django
DEBUG=False
ALLOWED_HOSTS=127.0.0.1,localhost
```

### 3. Запустите проект через Docker Compose:
```bash
docker compose up -d --build
```

### 4. Выполните миграции и соберите статику:
```bash
docker compose exec backend python manage.py migrate
docker compose exec backend python manage.py collectstatic --no-input
```

Проект будет доступен по адресу: [http://localhost:8000](http://localhost:8000)

<br>

## CI/CD Workflow

В проекте настроена автоматизация через **GitHub Actions**. При каждом пуше в ветку `main` выполняются следующие шаги:

1.  **Линтинг и тесты бэкенда**: Проверка кода линтером `ruff` и запуск Django-тестов.
2.  **Тестирование фронтенда**: Запуск тестов React-приложения.
3.  **Сборка и публикация образов**: При успешном прохождении тестов собираются три Docker-образа (`backend`, `frontend`, `gateway`) и отправляются на **Docker Hub**.
4.  **Уведомление**: После завершения всех этапов в Telegram приходит сообщение об успешном обновлении образов.

<br>

## API Документация

Эндпоинты API:
- `/api/cats/` — получение списка котиков или создание новой записи (GET, POST).
- `/api/cats/{id}/` — просмотр, редактирование или удаление конкретного котика.
- `/api/achievements/` — список достижений.
- `/api/users/` — регистрация пользователей.
- `/api/token/login/` — получение токена авторизации.

Для доступа к админ-панели используйте адрес: `/admin/`

<br>

## Автор
**GitHub**: [@orbuzik](https://github.com/ORBUZIK)
