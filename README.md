Запуск локальной версии документации
------------

_Чтобы локально развернуть копию документации:_

1. Установить docker CE и docker-compose, следуя инструкциям на https://docs.docker.com/ для своей ОС
2. Склонировать репозиторий `https://github.com/moysklad/doc.git`
3. В командной строке, перейдите в папку репозитория.
4. Выполните команду `docker-compose up`

Локальная версия документации будет доступна по адресу `http://localhost:4567`

Основная версия документации доступна по адресу https://moysklad.github.io/doc/api/remap/1.2/ru/

## Описание репозитория и структуры документации

В ветке `master` находится версия документации, развёрнутая на продуктовом сервере. После мерджа измений в мастер необходимо запустить скрипт `deploy.sh`, чтобы сделанные изменения стали доступны пользователям.

В папке `source/includes` находятся .md-файлы документации.

## Оформление нового раздела

Для добавления нового раздела необходимо создать .md-файл в папке `source/includes`. Имя файла должно начинаться с `_`. Для отображения нового раздела в боковом меню в `source/index.html.md` в раздел `includes` нужно прописать название нового раздела (должно совпадать с названием .md-файла).

Пример разметки страницы:
```
## Заголовок раздела

### Название сущности
Описание сущности

#### Атрибуты сущности
Описание аттрибутов сущности
+ **attribute** - описание аттрибута

#### Атрибуты доступные для фильтрации
При необходимости

#### Атрибуты доступные для сортировки
При необходимости

### Получить Сущности

**Параметры**

| Параметр                | Описание  |
| ------------------------------ |:---------------------------|
|parameter |  Описание параметра |

> Получить Сущности 

curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/some_entity"
  -H "Authorization: Basic <Access-Token>"


> Response 200 (application/json)
Успешный запрос. Результат - JSON представление списка Сущностей

JSON ответа от сервера

```
