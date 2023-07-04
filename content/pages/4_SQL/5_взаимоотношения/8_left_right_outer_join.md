---
Title: Операторы LEFT OUTER JOIN и RIGHT OUTER JOIN
Sort: 8
---

С операторами LEFT OUTER JOIN и RIGHT OUTER JOIN вы уже знакомы. Напомним: оператор LEFT OUTER JOIN предполагает, что в результат слияния обязательно войдут все записи из левой таблицы. Записи из правой таблицы сохранятся только в том случае, если значения в поле, по которому происходит объединение, совпадают со значениями в левой таблице. Оператор RIGHT OUTER JOIN устроен аналогичным образом, но бóльшим приоритетом обладает правая таблица. 

Сразу перейдём к практике. Что нужно сделать: 

Объединить данные таблиц artist и album и вывести всех исполнителей, добавив информацию о музыкальных альбомах, которые они выпустили.

Таблица artist хранит информацию об исполнителях и содержит поле artist_id с идентификатором и поле name с именем исполнителя. Таблица album содержит данные о музыкальных альбомах и включает в себя поля album_id и title с идентификатором альбома и его названием соответственно, а также поле artist_id с идентификатором исполнителя.

### Выбираем тип объединения

Таблицы artist и album связаны по ключу artist_id, и связь между ними — «один ко многим», ведь одному исполнителю может соответствовать несколько музыкальных альбомов.

Раз нужно вывести данные обо всех исполнителях, оператор INNER JOIN не подойдёт: в таком случае исполнители без альбома в итоговую таблицу не попадут. Если использовать оператор LEFT OUTER JOIN, все исполнители попадут в выдачу. 

### Соединяем таблицы

Чтобы объединить таблицы, нужно указать подходящий оператор: LEFT OUTER JOIN или сокращённую версию LEFT JOIN. 

```SQL
SELECT art.name,
       alb.title
FROM artist AS art
LEFT OUTER JOIN album AS alb ON art.artist_id = alb.artist_id
LIMIT 10; 
```

Таблицы artist и album объединены по ключу artist_id, и благодаря оператору LEFT OUTER JOIN все значения из поля name таблицы artist попадут в итоговую таблицу. Если для какого-то исполнителя не найдётся альбома, на этом месте в поле title появится значение NULL.

name|	title
--|--
AC/DC|	For Those About To Rock We Salute You
AC/DC|	Let There Be Rock
Accept|	Balls to the Wall
Accept|	Restless and Wild
Aerosmith|	Big Ones
Alanis Morisette|	Jagged Little Pill
Alice in Chains|	Facelift
Antônio Carlos Jobim|	Warner 25 Anos
Antônio Carlos Jobim|	Chill: Brazil (Disc 2)
Apocalyptica|	Plays Metallica By Four Cellos
<br>

Получить такую же таблицу можно и другим запросом. 

```SQL
SELECT art.name,
       alb.title
FROM album AS alb
RIGHT OUTER JOIN artist AS art ON art.artist_id = alb.artist_id
LIMIT 10; 
```

name|	title
--|--
AC/DC|	For Those About To Rock We Salute You
AC/DC|	Let There Be Rock
Accept|	Balls to the Wall
Accept|	Restless and Wild
Aerosmith|	Big Ones
Alanis Morisette|	Jagged Little Pill
Alice in Chains|	Facelift
Antônio Carlos Jobim|	Warner 25 Anos
Antônio Carlos Jobim|	Chill: Brazil (Disc 2)
Apocalyptica|	Plays Metallica By Four Cellos
<br>

Результат не поменялся. Это связано с тем, что LEFT OUTER JOIN и RIGHT OUTER JOIN в большинстве случаев взаимозаменяемы. Достаточно просто поменять местами таблицы в запросе. В некоторых СУБД оператор RIGHT OUTER JOIN совсем не используют, потому что получить нужный результат можно, меняя таблицы местами.

### Агрегируем и сортируем

Получившуюся таблицу можно обновить, посчитав, сколько приходится альбомов на одного исполнителя. Поле с количеством альбомов лучше переименовать. 

```SQL
SELECT art.name,
       COUNT(alb.title) AS total_album
FROM artist AS art
LEFT OUTER JOIN album AS alb ON art.artist_id = alb.artist_id
GROUP BY art.name
ORDER BY total_album DESC
LIMIT 10; 
```

name|	total_album
--|--
Iron Maiden	|21
Led Zeppelin|	14
Deep Purple	|11
Metallica|	10
U2|	10
Ozzy Osbourne|	6
Pearl Jam|	5
Faith No More|	4
Foo Fighters|	4
Various Artists	|4
<br>

Так выглядит топ-10 исполнителей по количеству альбомов. Неудивительно, что Iron Maiden на первом месте, — они играют ещё с начала восьмидесятых!