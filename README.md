# API Yatube
REST API для социальной cети Yatube.
## Технологии
Python 3.7.9,
Django REST framework 3.12.4
## Установка

Скопируйте репозиторий.
```sh
git clone https://github.com/caveinfix/api_final_yatube.git
```
Установите и активируйте виртуальное окружение.
```sh
cd api_yatube
python -m venv venv
source venv/bin/activate
python3 -m pip install --upgrade pip
```
Установите зависимости, выполните миграции и запустите сервер.

```sh
pip3 install -r requirements.txt
python3 manage.py migrate
python3 manage.py runserver
```

## Создание пользователя
```sh
python3 manage.py createsuperuser
```
Аутентификация
```sh
POST /api/v1/auth/jwt/create/
```
Тело запроса.
```sh
{
    "username": "anton",
    "password": "password"
}
```
В ответ получаем токен:
```sh
{
    "refresh": "refresh"
    "access": "access"
}
```
## Примеры запросов

#### Для взаимодействия с ресурсом настроены следующие эндпоинты:

| Эндпоинты | Запросы |
| ------ | ------ |
| api/v1/auth/jwt/create/ |(POST): передаём логин и пароль, получаем токен. |
| api/v1/posts/ |(GET, POST): получаем список всех постов или создаём новый пост. |
| api/v1/posts/{post_id}/ | (GET, PUT, PATCH, DELETE): получаем, редактируем или удаляем пост по id. |
|api/v1/groups/ | (GET): получаем список всех групп. |
| api/v1/groups/{group_id}/ |(GET): получаем информацию о группе по id. |
| api/v1/posts/{post_id}/comments/ |(GET, POST): получаем список всех комментариев поста с id=post_id или создаём новый, указав id поста, который хотим прокомментировать. |
| api/v1/posts/{post_id}/comments/{comment_id}/ |(GET, PUT, PATCH, DELETE): получаем, редактируем или удаляем комментарий по id у поста с id=post_id. |
| api/v1/posts/follow/ |(GET, POST): получаем информацию по подписчикам или создаем подписку. |

POST-запрос с токеном Антона Чехова: добавление нового поста.
```sh
POST .../api/v1/posts/
```
```sh
{
    "text": "Вечером собрались в редакции «Русской мысли», чтобы поговорить о народном театре. Проект Шехтеля всем нравится.",
    "group": 1
} 
```
Ответ:
```sh
{
    "id": 14,
    "text": "Вечером собрались в редакции «Русской мысли», чтобы поговорить о народном театре. Проект Шехтеля всем нравится.",
    "author": "anton",
    "image": null,
    "group": 1,
    "pub_date": "2021-06-01T08:47:11.084589Z"
} 
```

Пример POST-запроса с токеном Антона Чехова: отправляем новый комментарий к посту с id=14.

```sh
POST .../api/v1/posts/14/comments/
```

```sh
{
    "text": "тест тест"
} 
```
Ответ:
```sh
{
    "id": 4,
    "author": "anton",
    "post": 14,
    "text": "тест тест",
    "created": "2021-06-01T10:14:51.388932Z"
} 
```

Пример GET-запроса с токеном Антона Чехова: получаем информацию о группе.
```sh
GET .../api/v1/groups/2/
```

Ответ:
```sh
{
    "id": 2,
    "title": "Математика",
    "slug": "math",
    "description": "Посты на тему математики"
} 
```

## Автор проекта
- Автор: Филипп П. 
- e-mail: caveinfix@gmail.com