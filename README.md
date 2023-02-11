# Проект **YaMDb** 

Api собирает отзывы пользователей на различные произведения.

# Как запустить проект чeрез Docker:
Должен быть уставлен Docker https://www.docker.com

Клонируем репозиторий и переходим в него:

```
git clone https://github.com/Nemets87/infra_sp2

```

Перейти в папку infra

```
cd infra
```

Создать файл ".env"

```
DB_ENGINE=django.db.backends.postgresql = указываем, что работаем с postgresql
DB_NAME=postgres = имя базы данных
POSTGRES_USER=postgres = логин для подключения к базе данных
POSTGRES_PASSWORD=postgres = пароль для подключения к БД (установите свой)
DB_HOST=db = название сервиса (контейнера)
DB_PORT=5432 = порт для подключения к БД 
```
Работать мы будем в linux и все команды начинаются со слова sudo
P.S в Windows sudo не нужно  
```
sudo su root дает возможность избежать слово sudo,но под рутом сидеть опасно 
```
Собрать проект (в папке с файлом docker-compose.yaml:)
```
sudo docker-compose up -d --build
```

Cделать миграции, создать суперпользователя и собрать статику 

```
sudo docker-compose exec web python manage.py makemigrations reviews
sudo docker-compose exec web python manage.py migrate 
sudo docker-compose exec web python manage.py createsuperuser 
sudo docker-compose exec web python manage.py collectstatic --no-input 
```
Создаем дамп базы данных (нет их сейчас,но будут):
```
sudo docker-compose exec web python manage.py dumpdata > dumpPostrgeSQL.json
```
Останавливаем контейнеры:

```
sudo docker-compose down -v
```

проект доступен по адресу 

```
http://localhost/api/v1/
```


# Регистрация нового пользователя
```
POST http://localhost/api/v1/auth/signup/

{
  "email": "string",
  "username": "string"
}
```

**Редактирование, удаление и создание категорий жанров и произведений доступно только Администратору**
# Примеры запросов
## Получение списка всех категорий

```
GET http://localhost/api/v1/categories/
```
## Добавление новой категории

```
POST http://localhost/api/v1/categories/

{
  "name": "string",
  "slug": "string"
}
```


### **Авторы:**
- [Sergey Fedorov + Power 45 Team ](https://github.com/Nemets87)