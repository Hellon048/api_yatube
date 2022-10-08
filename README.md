# API YaMDb
***
<details>
    <summary style="font-size: 16pt; font-weight: bold">Описание</summary>

Проект YaMDb собирает отзывы пользователей на произведения. Произведения делятся на категории: «Книги», «Фильмы», «Музыка». Список категорий может быть расширен администратором.
Сами произведения в YaMDb не хранятся, здесь нельзя посмотреть фильм или послушать музыку.
Произведению может быть присвоен жанр из списка предустановленных. Новые жанры может создавать только администратор.
Благодарные или возмущённые пользователи оставляют к произведениям текстовые отзывы и ставят произведению оценку. Из пользовательских оценок формируется рейтинг.

</details>

***
<details>
    <summary style="font-size: 16pt; font-weight: bold">Технологии</summary>

* Python 3.9
* Django 2.2.16
* djangorestframework 3.12.4
* Docker 20.10.17
* Postgres:13.0-alpine
* Nginx:1.21.3-alpine


С полным списком технологий можно ознакомиться в файле requirements.txt
</details>

***

<details>
    <summary style="font-size: 16pt; font-weight: bold">Запуск проекта</summary>


Запуск проекта:
```
docker-compose up -d --build
```

Сделать миграции внутри web контейнера:
```
docker-compose exec web python manage.py migrate
```
Создать SuperUser'а:
```
docker-compose exec web python manage.py createsuperuser

```
Подгрузить статику в контейнер:
```
docker-compose exec web python manage.py collectstatic --no-input
```

</details>

***
<details>
     <summary style="font-size: 16pt; font-weight: bold">Документация</summary>

С документацией проекта можно ознакомиться по [ссылке](http://127.0.0.1:8000/redoc/) после запуска проекта.
</details>


***
<details>
    <summary style="font-size: 16pt; font-weight: bold">Management-command</summary>

Если у Вас есть чем наполнить базу данных, а именно у Вас имеется *.csv файл,
то management-command fill_db Вам облегчит жизнь. Для того чтобы
воспользоваться ею, необходимо прописать в командной строке вашего проекта следующее:
```
docker-compose exec web python manage.py fill_db -m [Model] -f [file]
```
Важно отметить, что название модели нужно вводить строго
с заглавной буквы. Так же для заполнения БД необходимо по следующем критериям:
1. Первым делом заполнить модель User;
2. Заполнить модели Category / Genre;
3. Заполнить модель Title;
4. Заполнить модель GenreTitle;
5. Последующие модели.
Если не учесть данную последовательность, то возникнет ошибка,
т.к. все модели с полями ForeignKey / ManyToManyField ожидают
экземпляр класса связующей ею моделью.

Просьба - учесть данный факт!

### Пример команды
```
python manage.py fill_db -m Category -f category
```
Для подробной информации используйте:
```
python manage.py fill_db -h
```
</details>

***
<details>
    <summary style="font-size: 16pt; font-weight: bold">Автор</summary>

* [Вячеслав Наприенко](https://github.com/Hellon048)

</details>

***
