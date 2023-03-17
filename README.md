# Проект API_YAMDB собирает отзывы пользователей на различные произведения.
Проект создавали:
* ### Андрей Мельников
  * система регистрации и аутентификации,
  * права доступа,
  * работа с токеном,
  * система подтверждения через e-mail.
* ### Клавдия Дунаева
  Пишет модели, view и эндпойнты для:
  * произведений,
  * категорий,
  * жанров;
* ### Николай Артемьев
  Пишет модели, view и эндпойнты для:
  * отзывов,
  * комментариев,
  * рейтинг произведений.
  
  Упаковывает приложение в контейнер

В данном проекте использованы технологии:
Docker, Python, Django, DRF, Api, Postman
## Как запустить проект:

Клонировать репозиторий и перейти в него в командной строке:

```
git clone https://git@github.com:Nikolay-ar/infra_sp2.git
```

Создать и активировать виртуальное окружение:

```
python3 -m venv env
```

* Если у вас Linux/macOS

    ```
    source env/bin/activate
    ```

* Если у вас windows

    ```
    source env/scripts/activate
    ```

Обновить pip:

```
python3 -m pip install --upgrade pip
```

Установить зависимости из файла requirements.txt:

```
pip install -r requirements.txt
```

Перейти в папку infra:

```
cd infra
```

Запустить docker-compose:

```
docker-compose up -d --build
```

Выполнить миграции:

```
docker-compose exec web python manage.py migrate
```

Собрать статику:

```
docker-compose exec web python manage.py collectstatic --no-input
```

Теперь проект доступен по адресу http://localhost/

## Примеры запросов: ##
Вход в админ панель:
>**POST** http://localhost/admin/
> 
Регистрация нового пользователя:
>**POST** http://localhost/api/v1/signup/

Для получения токена отправьте логин и код, который пришел вам на электронную почту:
>**POST** http://localhost/api/v1/auth/token/

Получение списка произведений:
>**GET** http://localhost/api/v1/titles/

Создание публикации (только администратор):
>**POST** http://localhost/api/v1/titles/
> 
```
{
"name": "string",
"year": 0,
"description": "string",
"genre": [
"string"
],
"category": "string"
}
```

Получение списка категорий:
>**GET** http://localhost/api/v1/categories/

Получение списка жанров:
>**GET** http://localhost/api/v1/genre/

Просмотр отзывов на произведение:
>**GET** http://localhost/api/v1/titles/{title_id}/reviews/

Создание отзывов на произведение:
>**POST** http://localhost/api/v1/titles/{title_id}/reviews/
```
{
"text": "string",
"score": 1
}
```

Просмотр комментариев к отзыву:
>**GET** http://localhost/api/v1/titles/{title_id}/reviews/{review_id}/commenta/

Создание комментария к отзыву:
>**Post** http://localhost/api/v1/titles/{title_id}/reviews/{review_id}/commenta/
```
{
"text": "string"
}
```
Остальные запросы можно посмотреть в документации для API Yamdb:
> http://localhost/redoc/
