---
Title: Специальное значение NULL
Sort: 8
---

Таблица `client` хранит информацию о покупателях и содержит поле `fax` с номерами факсов. Посмотрите на первые десять записей этого поля:

```SQL
SELECT fax
FROM client
LIMIT 10; 
```

fax|
--|
+55 (12) 3923-5566
[null]
[null]
[null]
+420 2 4172 5555
[null]
[null]
[null]
[null]
+55 (11) 3033-4564

Не во всех ячейках есть данные с номерами факсов. В них находится что-то странное. Может, всё дело в том, что никто больше не использует факс?

Специальное значение `NULL` обозначает отсутствие данных. Основная особенность `NULL` в том, что это значение не равно ничему. С `NULL` нельзя сравнить какое-либо значение с помощью любых операторов: `=`, `<`, `>`, `LIKE`. 

Если выгрузить из таблицы `client` все строки, в которых в номерах факса указано значение `NULL`, на экране появится пустая таблица.

```SQL
SELECT *
FROM client
WHERE fax = NULL; 
```

Для работы со специальными значениями используют отдельные операторы — `IS NULL` и `IS NOT NULL`. Оператор `IS NULL` при встрече с `NULL` вернёт `TRUE`, а оператор `IS NOT NULL` наоборот: вернёт `TRUE`, если значение не равно `NULL`.

Операторы `IS NULL` и `IS NOT NULL` можно применять в условиях, чтобы фильтровать данные. В запросе можно задать условие с оператором `IS NULL`, чтобы выгрузить записи, в которых есть пропуски. Такой запрос выгрузит из таблицы `client` поле с адресами электронной почты и поле с номерами факсов, в котором все значения — пропуски:

```SQL
SELECT email,
         fax
FROM client
WHERE fax IS NULL
LIMIT 5; 
```

email|	fax
--|--
leonekohler@surfeu.de|	[null]
ftremblay@gmail.com|	[null]
bjorn.hansen@yahoo.no|	[null]
hholy@gmail.com|	[null]
astrid.gruber@apple.at|	[null]

Если заменить оператор на IS NOT NULL, можно выгрузить записи без пропусков:

```SQL
SELECT email,
         fax
FROM client
WHERE fax IS NOT NULL
LIMIT 5; 
```

email|	fax
--|--
luisg@embraer.com.br|	+55 (12) 3923-5566
frantisekw@jetbrains.com|	+420 2 4172 5555
eduardo@woodstock.com.br|	+55 (11) 3033-4564
alero@uol.com.br|	+55 (11) 3055-8131
roberto.almeida@riotur.gov.br|	+55 (21) 2271-7070

Зачем вообще нужны инструменты, которые убирают или, наоборот, выводят пропуски? Пропущенные значения — чаще всего аномалии. Специалистам приходится решать, что с ними делать. Пропуски можно отобрать и обработать отдельно или вообще исключить из выдачи.