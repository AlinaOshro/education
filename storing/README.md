# Хранение 

[Здесь](https://github.com/zbze-org/zbze_crawler/tree/main/data) данные хранятся в формате
```JSON 
{
  "url": "https://apkbr.ru/node/9529",
  "title": "Лъэмыжыр къызэIуахыжащ",
  "publication_date": "2023-12-19T13:05:57+00:00",
  "content": "«Кавказ» зи фIэщыгъэ Р-217 къэралпсо автомашинэ гъуэгум хыхьэ ...",
  "author": "ШУРДЫМ Динэ."
}
```
Вариант использования связей:
1. Таблица "Источники"
2. Таблица "Предложения" (текст, ссылку на Источник)
3. Таблица "Слова"
4. Таблица-связь "Слова" и "Предложения"
7. Таблица-связь "Слова" и "Источники". Добавить поле "Количество слова в источнике"

To-Do:
- Взять текст из нескольких книг и разложить в БД
- Почитать про индексы для полнотекстного поиска и создать для таблицы предложений чтобы поиск был эффективным

# PostgreSQL 
- [Подсказки по MarkDown1](https://skillbox.ru/media/code/yazyk-razmetki-markdown-shpargalka-po-sintaksisu-s-primerami/#stk-18)
- [Подсказки по MarkDown2](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
- [JSON в Postgres](https://www.postgresql.org/docs/current/functions-json.html)

Преимущество Postgres – специальные типы данных, позволяющие хранить JSON и индексировать значения для ускорения выборки 
JSONB – бинарный формат, котрый эффективнее JSON-а хранит данные и позволяет создавать индексы на разичные часи JSON

## Создание JSON с помощью SQL-запросов 
```SQL
SELECT json_build_object('name', 'Ivan', 'age', 24); 
```

## Преобразование JSON в JSONB 
```SQL
SELECT json_build_object('name', 'Ivan', 'age', 24)::jsonb->'age' as age; 
```

 где `::` – преобразует json в jsonb

`->` – позволяет обратиться к конкретному полю 

`as age` – уставливает название колонки 

`->>` – позволяет получить текстовое представление поля 
