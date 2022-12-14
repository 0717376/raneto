---
Title: Оператор WHERE. Операторы сравнения
Sort: 3
---

Выгрузить конкретные поля — ещё полдела. Чаще всего данные нужно как-то ограничить: выгрузить информацию за конкретный период или с конкретным условием. Например, получить названия всех треков в жанре рок. 

Для таких задач в SQL используют условный оператор `WHERE`. Его указывают после оператора `FROM`:

```SQL
SELECT track_id, -- поля для выгрузки
       album_id 
       ...
FROM track -- таблица, из которой выгружают данные
WHERE track_id = 5; -- условие для среза данных 
```

Задавать условия можно с помощью операторов сравнения. Равенство значений указывают знаком `=`, неравенство — знаками `<>`. Вариант для обозначения неравенства `!=`, который используется во многих языках программирования, в PostgreSQL тоже сработает. Остальные операторы сравнения выглядят так: 
- `>` — больше;
- `<` — меньше;
- `>=` — больше или равно;
- `<=` — меньше или равно.

Сравнение с числом записывают просто: `WHERE поле < 5`. Но если значение сравнивают с символьным типом, набор символов нужно взять в одинарные кавычки: WHERE поле = 'Иванов'. Это правило также касается даты и времени: `WHERE поле = '2013-07-01'`.

Покажем, как это выглядит на практике. Нужно выгрузить данные о заказах на сумму больше или равно 1.2. Информацию о счетах хранит таблица `invoice`, а поле `total` в таблице содержит данные о сумме заказа. Такой запрос отфильтрует необходимую информацию:

```SQL
SELECT *
/* Нужно выгрузить всю информацию о заказах,
поэтому поля можно не указывать*/
FROM invoice
WHERE total >= 1.2; 
```

