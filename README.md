# Kittygram Final

[![Kittygram workflow](https://github.com/amosova-elena/kittygram_final/actions/workflows/main.yml/badge.svg)](https://github.com/amosova-elena/kittygram_final/actions/workflows/main.yml)

Учебный проект, выполненный в рамках курса «Python-разработчик» Яндекс Практикума.

## Описание проекта

Kittygram — это веб-приложение, в котором пользователи могут публиковать фотографии своих котиков, указывать их имя, год рождения, цвет и достижения.

В данном репозитории реализована контейнеризация приложения с помощью Docker и автоматизирован процесс тестирования и деплоя с использованием GitHub Actions.

Проект разворачивается на удалённом сервере в виде набора Docker-контейнеров:

- backend (Django + Django REST Framework);
- frontend (React);
- gateway (Nginx);
- PostgreSQL.

При каждом пуше в ветку `main` GitHub Actions автоматически:

- запускает тесты бэкенда и фронтенда;
- проверяет код на соответствие PEP8;
- собирает Docker-образы;
- отправляет их в Docker Hub;
- обновляет контейнеры на сервере;
- выполняет миграции и сборку статики;
- отправляет уведомление об успешном деплое в Telegram.

---

## Использованные технологии

- Python 3.12
- Django
- Django REST Framework
- PostgreSQL
- React
- Docker
- Docker Compose
- Nginx
- GitHub Actions

---

## Установка и запуск проекта

### Клонирование репозитория

```bash
git clone git@github.com:<ваш_логин>/kittygram_final.git
cd kittygram_final
```

### Настройка переменных окружения

В корне проекта находится файл `.env.example`, содержащий пример переменных окружения.

Перед запуском проекта создайте на его основе файл `.env`:

```bash
cp .env.example .env
```

Пользователи Windows могут просто скопировать файл `.env.example` и переименовать его в `.env`.

При необходимости измените значения переменных окружения в файле `.env`.

### Запуск проекта

```bash
docker compose up -d
```

После запуска выполните миграции:

```bash
docker compose exec backend python manage.py migrate
```

Соберите статические файлы:

```bash
docker compose exec backend python manage.py collectstatic --noinput
```

---

## Примеры запросов к API

### Получить список котиков

```
GET /api/cats/
```

Ответ:

```json
[
  {
    "id": 1,
    "name": "Барсик",
    "birth_year": 2022,
    "color": "black"
  }
]
```

---

### Добавить котика

```
POST /api/cats/
```

Тело запроса:

```json
{
  "name": "Мурзик",
  "birth_year": 2023,
  "color": "white",
  "achievements": ["Поймал мышку"]
}
```

---

### Получить информацию о пользователе

```
GET /api/users/me/
```

---

## Автор

**Елена Амосова**

GitHub: https://github.com/amosova-elena