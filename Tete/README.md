# Документация - Цифровой двойник карьера

Интерактивная документация для системы имитационного моделирования карьера.

## Структура проекта

```
Tete/
├── admin.html              # Админ-панель для редактирования (локально)
├── admin_git.html          # Версия для GitHub Pages (только просмотр)
├── data.json               # Данные карточек (обзор, инструкции, о системе)
├── directory_data.json     # Справочники (параметры системы)
├── server.js               # Node.js сервер для локальной работы
├── screenshots/            # Папка для скриншотов
└── README.md               # Этот файл
```

## Быстрый старт (локально)

### Требования
- Node.js (любая версия)

### Запуск

1. Перейдите в папку проекта:
```bash
cd Tete
```

2. Запустите сервер:
```bash
node server.js
```

3. Откройте в браузере:
- **Просмотр**: http://localhost:3000
- **Редактирование**: http://localhost:3000/admin.html

## Развертывание в Docker

### Вариант 1: Простой Dockerfile

Создайте `Dockerfile`:
```dockerfile
FROM node:alpine
WORKDIR /app
COPY . .
EXPOSE 3000
CMD ["node", "server.js"]
```

Запуск:
```bash
docker build -t docs-app .
docker run -p 3000:3000 docs-app
```

### Вариант 2: Docker Compose

Создайте `docker-compose.yml`:
```yaml
version: '3.8'
services:
  docs:
    image: node:alpine
    working_dir: /app
    volumes:
      - .:/app
    ports:
      - "3000:3000"
    command: node server.js
```

Запуск:
```bash
docker-compose up
```

## GitHub Pages (только просмотр)

Для публикации на GitHub Pages используйте файл `admin_git.html`:

1. Переименуйте `admin_git.html` в `index.html`
2. Загрузите в репозиторий вместе с `data.json` и `directory_data.json`
3. Включите GitHub Pages в настройках репозитория

## Редактирование контента

### Локально (с сервером)
1. Запустите `node server.js`
2. Откройте http://localhost:3000/admin.html
3. Редактируйте карточки через интерфейс
4. Изменения сохраняются в `data.json`

### Справочники
Файл `directory_data.json` содержит параметры системы. Редактируйте его напрямую или через интерфейс.

## API сервера

- `GET /api/data` - получить данные
- `POST /api/data` - сохранить данные
- `POST /api/save-image` - загрузить изображение
- `POST /api/delete-image` - удалить изображение

## Примечания

- Папка `screenshots/` создается автоматически при первом запуске
- Все изображения сохраняются в `screenshots/`
- Версия для GitHub Pages не поддерживает редактирование и загрузку изображений
