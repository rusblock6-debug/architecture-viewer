# Документация - Цифровой двойник карьера

Интерактивная документация для системы имитационного моделирования карьера.

## Структура проекта

```
Tete/
├── admin.html              # Админ-панель с редактированием (локально с сервером)
├── admin_git.html          # Версия для GitHub Pages (только просмотр)
├── user.html               # Пользовательская версия (только просмотр, без кнопок редактирования)
├── data.json               # Данные карточек (обзор, инструкции, о системе)
├── directory_data.json     # Справочники (параметры системы)
├── server.js               # Node.js сервер для локальной работы
├── screenshots/            # Папка для скриншотов
└── README.md               # Этот файл
```

## Версии документации

### admin.html
Полная версия с возможностью редактирования. Работает только с локальным сервером Node.js.
Позволяет добавлять, редактировать и удалять карточки через веб-интерфейс.

### admin_git.html
Версия для размещения на GitHub Pages. Только просмотр, без возможности редактирования.
Загружает данные из data.json напрямую.

### user.html
Пользовательская версия без кнопок редактирования. Чистый интерфейс для просмотра документации.
Подходит для конечных пользователей системы.

## Запуск локально

Требования: Node.js (любая версия)

1. Перейти в папку проекта:
```bash
cd Tete
```

2. Запустить сервер:
```bash
node server.js
```

3. Открыть в браузере:
- Просмотр: http://localhost:3000
- Админка: http://localhost:3000/admin.html
- Пользовательская версия: http://localhost:3000/user.html

## Развертывание в Docker

### Простой Dockerfile

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

### Docker Compose

Создать docker-compose.yml:
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

## Размещение на GitHub Pages

1. Переименовать нужную версию в index.html:
```bash
copy admin_git.html index.html
```
или
```bash
copy user.html index.html
```

2. Загрузить в репозиторий вместе с data.json, directory_data.json и папкой screenshots

3. Включить GitHub Pages в настройках репозитория:
   - Settings → Pages
   - Source: Deploy from a branch
   - Branch: main → папка: / (root)
   - Save

Документация будет доступна по адресу: https://username.github.io/repository-name/

## Редактирование контента

### Через веб-интерфейс (локально)
1. Запустить node server.js
2. Открыть http://localhost:3000/admin.html
3. Использовать кнопку "+" для добавления карточек
4. Изменения сохраняются в data.json

### Напрямую в файлах
Редактировать data.json и directory_data.json вручную в любом текстовом редакторе.
Структура JSON интуитивно понятна.

## API сервера

- GET /api/data - получить данные
- POST /api/data - сохранить данные
- POST /api/save-image - загрузить изображение
- POST /api/delete-image - удалить изображение

## Примечания

- Папка screenshots/ создается автоматически при первом запуске
- Все изображения сохраняются в screenshots/
- Версии для GitHub Pages не поддерживают редактирование и загрузку изображений
- Пользовательская версия (user.html) не содержит кнопок редактирования для чистого интерфейса
