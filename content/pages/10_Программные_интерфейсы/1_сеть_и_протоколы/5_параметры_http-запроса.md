---
Title: Параметры HTTP-запроса
Sort: 5
---

В прошлом уроке вы узнали о том, что заголовки и тело запроса могут содержать параметры. В этом уроке вы узнаете, что это такое параметры HTTP-запроса и какими они могут быть.

### Параметры запросов

**Параметры** — это сведения, предоставляемые запросу для его выполнения.

Запрос возвращает данные на основе входящих параметров, которые передаются при вызове метода. Параметры необходимы для того, чтобы запрос был выполнен корректно.

Параметры при запросе можно передать в URL, в заголовках и в теле запроса. Например, так выглядят параметры в теле запроса:

```JSON
PUT http://предметы-сервировки-стола.рф/бокал/для-красного-вина 
Body: {
    “volume”: “140",
    “height”: “25",
    "material": "стекло" 
} 
```

Как и в прошлом уроке, в этом уроке используется стиль представления данных JSON. В этом примере передаются данные о ресурсе «бокал для красного вина», а с помощью параметров задаётся его объём (volume), высота (height) и материал (material).

### Виды параметров

Существует четыре вида параметров HTTP:
- параметры URL (URL Parameters),
- параметры запроса (Query Parameters),
- параметры формы (Form Parameters),
- параметры заголовка (Header Parameters).

Все параметры используются для того, чтобы обеспечить входные данные для запроса, но каждый из видов используется в разных случаях.

#### Параметры URL (URL Parameters)

Параметр URL— это часть самого URL, а значит, и часть идентификатора ресурса. Параметры URL ещё называют локаторами. 

В запросе ниже параметр URL — идентификатор 2.

```
GET http://предметы-сервировки-стола.рф/ложка/для_супа/2
```

Если параметр URL указан неверно, то весь URL неверный. В итоге ресурс невозможно найти, а при попытке пользователь увидит код ответа 404 (Not Found).

Параметры URL могут быть использованы в основных методах HTTP: GET, PUT, POST.

#### Параметры запроса (Query Parameters)

Параметры запроса — это параметры типа ключ-значение, которые «прикрепляются» к URL ресурса через символ «?». Если запрос подразумевает поиск по нескольким параметрам, они могут быть соединены через «&», формируя список:

```
GET http://предметы-сервировки-стола.рф/бокал/для-красного-вина?material=пластик&volume=160
```

Параметры запроса передаются в формате: **ключ=значение**. В данном случае ключами будут material (материал) и volume (объём), а их значения — «пластик» и «160».

Лучшего всего разрабатывать параметры запроса как необязательные входящие параметры запроса, чтобы каждый из параметров мог быть передан или удалён из запроса. Если параметр запроса отсутствует, метод должен выполнять запрос без этих параметров или с установленными значениями по умолчанию.

Если один из параметров передан некорректно, возвращается код 400 (Bad Request), который говорит о том, что запрос содержит ошибку. Код 404 может вернуться, только если, помимо ошибки в параметрах, не удалось найти сам ресурс.

Обычно параметры запроса применяются в методе GET.

#### Параметры формы (Form Parameters)

Параметры формы используются для передачи данных, которые были получены через пользовательский интерфейс при заполнении формы. Параметры формы используются в комбинации с методом POST.

Параметры формы передаются в теле HTTP-запроса. В отличии от параметров запроса и параметров URL, параметры формы не являются частью URL. Преимущество использования параметров формы заключается в том, что они не ограничиваются лимитами длины URL. 

Чтобы сервер понял, что запрос формируется в виде формы, в параметре Content-Type необходимо установить такое значение: application/ x-www-form-urlencoded. При передаче параметров формы заголовок «тип содержимого тела HTTP-запроса» (Content-Type) устанавливается значение: application/ x-www-form-urlencoded. Так можно «объяснить» серверу, что это именно параметры формы, а не изображение, текст или другой тип данных.

```JSON
http://предметы-сервировки-стола.рф/кофейная-пара/чашка
material=glass&volume=30
Content-Type: application/x-www-form-encoded
-> 201 Created 
```

#### Параметры заголовка (Header Parameters)

Параметры заголовка — это пары «ключ:значение», где ключ — это название HTTP-заголовка, а значение — это информация, которую нужно передать в этом заголовке. Параметры заголовка отправляются в заголовке запроса. Нужно отметить, что у ответа на запрос также есть свои заголовки.

В параметрах заголовка передаются метаданные запроса. Как вы помните, метаданные — это описание любой структуры данных, или «данные о данных». В HTTP-запросе параметры заголовка предоставляют данные о содержимом запроса и том, какие данные клиент сможет принять в ответ.

Параметры заголовка иногда называют полями HTTP-заголовка (HTTP Headers Fields) или просто HTTP-заголовками (HTTP Headers).

Выделяют типовые и пользовательские заголовки. Большая часть заголовков является типовыми, пользовательские заголовки встречаются гораздо реже. Узнать о необходимости использования дополнительных пользовательских заголовков можно из документации сервиса.

Предполагается, что клиенты, как и веб-серверы, должны уметь работать с типовыми (стандартными) HTTP-заголовками, однако если вы отправляете пользовательский заголовок, то получатель не сможет обработать его корректно (если только этот пользовательский заголовок не предусмотрен в сервисе-получателе). Также выделяются заголовки запроса и заголовки ответа. Подробнее о HTTP-ответах вы узнаете в следующем уроке.

#### Параметры типовых заголовков (Generic Header Parameters)

Типовые (Generic) заголовки могут быть использованы как в запросах, так и ответах. Вот некоторые типовые заголовки:

Заголовок|	Назначение
--| --
Content-Type:|	Тип содержимого определяет синтаксис и семантику тела HTTP запроса. Ингода вместо заголовка Content-type используют заголовки media-type или MIME-type.<br> Например, заголовок `Content-Type:text/plain` говорит о том, что в запросе или ответе содержится обычный текст, не требующий редактирования.
Content-Length:|	Определяет длину содержимого запроса в байтах. При чтении помогает определить, было ли прочитано содержимое целиком.<br> `Content-Length:2875`
Content-Language:|	Определяет язык представления текстовых данных, используя одно- или двухбуквенный числовой код.<br> `Content-Language: de, gu`
Content-Location:|	Определяет адрес, по которому контент тела HTTP может быть получен, используя `GET`. <br>Параметр сообщает, что содержимое тела запроса содержит копию ресурса, адрес которого указан в заголовке `Content-Location:` <br>`Content-Location: http://предметы-сервировки-стола.рф`
Content-Encoding:|	Определяет использованный способ сжатия данных.<br>Возможные варианты:<br>- gzip (используется алгоритм LZ77)<br>- compress (используется алгоритм LZW)<br>- deflate (используется алгоритм deflate)<br>`Content-Encoding:gzip`
Date:|	Указывает дату и время отправления запроса<br> `Date:Tue, 17 Dec 2021 17:40:50 GMT`
Host:|	Определяет сервер, к которому необходимо выполнить запрос<br> `Host: www.practicum.yandex.ru`

#### Параметры заголовков запроса

В дополнение к типовым заголовкам в запросах часто используются специализированные заголовки, применяемые только в запросах. Вот некоторые из них:

Заголовок | Назначение
--|--
User-Agent:|	Идентифицирует клиента (агента). Строка содержит данные об устройстве клиента (операционная система, модель, производитель), настройках устройства(язык), используемый браузер и т.д.
Referer:|	Определяет URL, с которого получен запрос.<br> Например, если я зашел на домашнюю страницу пред + и нажал ссылку на каталог бокалов, этот header будет отправлен в браузер:<br>`Referer: http://предметы-сервировки-стола.рф/`
From:|	e-mail пользователя, который отправляет запрос
Accept:|	Определяет список типов данных, которые клиент может обработать при получении ответа: <br>Например:<br> `Accept: text/html`<br> `Accept: image/gif`
Accept-Encoding:|	Определяет виды кодировки, которые клиент может обработать при получении ответа<br> Например:<br>`Accept-Encoding: gzip`<br>`Accept-Encoding: compress`<br>`Accept-Encoding: deflate`<br> `Accept-Encoding: * - поддерживаются все виды корректировки`
Accept-Language:|	Определяет языки, которые клиент принимает в ответе<br> `Accept-Language: gu`
MIME-Version:|	Определяет используемую версию MIME протокола (протокол используется для передачи данных по почте)<br> `MIME-Version:1.1`
If-Modified-Since:|	Используется для запросов с условием, значение заголовка содержит дату и время, для определения актуальности ресурса. Сервис возвращает положительный ответ, если ресурс был изменен после указанной даты и времени.<br> `If-Modified-Since:Tue, 17 Dec 2021 17:40:50 GMT`
If-Unmodified-Since|	Используется для запросов с условием, значение заголовка содержит дату и время, для определения актуальности ресурса. Сервис возвращает положительный ответ, если ресурс не был изменен после указанной даты и времени<br> Если веб-документ уже сохранен в кеше в браузере и вы посещаете его снова, ваш браузер может проверить, был ли документ обновлён.<br> `If-Unmodified-Since:Tue, 17 Dec 2021 17:40:50 GMT`
Authorization:|	Передает информацию о пользователе (логин, пароль), чтобы подтвердить, что запрос пришел от авторизованного пользователя<br> Данные об авторизации пользователя передаются в зашифрованном виде и записывается в формате `Authorization: <auth-scheme> <authorization-parameters>` где, < auth-scheme> - схема, по которой зашифрованы параметры авторизации (логин, пароль и тд.) < authorization-parameters> - зашифрованные параметры `Authorization: Basic YWxhZGRpbjpvcGVuc2VzYW1l`

### Случаи использования параметров

Существует несколько случаев, в которых необходимо передать параметры в запросе:
- создание или обновление ресурса (Resource Creation and Update);
- поиск ресурса: фильтрация и сортировка (Resource Retrieval: Filters and Sorting);
- поиск ресурса: локатор (Resource Retrieval: Locators);
- поиск ресурсов: проекция (Resource Retrieval: Projections);
- передача метаданных (Metadata).

### Создание или обновление ресурса

Если ресурс создается методом POST, информация о создаваемом ресурсе передаётся как параметры формы (Form Parameters).

Например, нужно создать новый бокал красного вина с объемом 140 мл и высотой 25 см, материал — стекло. Тогда запрос будет выглядеть так:

```JSON
POST http://предметы-сервировки-стола.рф/бокал/для-красного-вина
volume=140&height=25&material=стекло 
```

Если ресурс создаётся или обновляется методом PUT, входящие параметры отправляются в теле запроса.

```JSON
PUT http://предметы-сервировки-стола.рф/бокал/для-красного-вина` 
Body: {
“volume”: “140",
“height”: “25",
"material": "стекло" 
} 
```

Если ресурс обновляется с использованием метода PATCH, в данных в теле запроса передаются только параметры, которые нужно изменить.

Например, нужно изменить объем с 140 мл до 160 мл:

```JSON
PATCH http://предметы-сервировки-стола.рф/бокал/для-красного-вина` 
Body: {
“volume”: “160"
} 
```

### Поиск ресурса: фильтрация и сортировка

Коллекции ресурсов — это список ресурсов, которые хранятся на сервере. 

Например, если нужно выполнить запрос `GET http://предметы-сервировки-стола.рф/бокал/для-красного-вина`, в ответ мы можем получить несколько бокалов с разными характеристиками. Это и есть коллекция ресурсов.

Сервер может хранить большие коллекции ресурсов, однако пользователи могут быть заинтересованы лишь в небольшой части этой коллекции. По этой причине методы могут искать, фильтровать и сортировать ресурсы. 

Фильтры в HTTP-запросах реализуются с использованием критериев фильтрации. Сортировка требует указания конкретного критерия и порядка сортировки. Критерии обычно указываются как параметры запроса.

Критерии указываются в формате «критерий=значение» в конце URL запроса, после символа «?».

Критерий поиска задаётся с помощью параметра Search. Его называют строка запроса (Query String). Например, нам нужно найти в коллекции бокалов для красного вина все ресурсы, которые содержат слово «пластик». Оно может быть найдено среди всех значений параметра "материал", и даже среди значений параметров "ширина" и "высота".

`GET http://предметы-сервировки-стола.рф/бокал/для-красного-вина?search=пластик`

Однако такой запрос выдаст в ответ все возможные бокалы для красного вина со словом «пластик», включая и другие характеристики, например высоту и ширину.

Но все же при составлении запроса нужно найти все бокалы для красного вина, у которых материал пластик, потому можно уточнить  запрос и выполнять поиск только по критерию «материал». То есть нам нужно найти все ресурсы, у которых в значении параметра material (материал) будет слово «пластик». Этот запрос будет выглядеть так:

`http://предметы-сервировки-стола.рф/бокал/для-красного-вина?material=пластик`

Теперь из всех полученных пластиковых бокалов необходимо выбрать самый объёмный. Для этого нужно воспользоваться сортировкой. Сортировка выполняется с помощью параметра Sort.  

`http://предметы-сервировки-стола.рф/бокал/для-красного-вина?material=пластик&sort=volume&sortOrder=desc`

### Поиск ресурса: локатор (Resource Retrieval: Locators)

URL позволяет однозначно определить адрес ресурса на сервере. В запросе расположение ресурса выражается параметрами URL, это следует из его названия — Uniform Resource Locator (унифицированный указатель ресурса).

К коллекции ресурсов можно применить как фильтры, так и локатор. Разница между ними в том, что локатор определяет один элемент в коллекции ресурсов, в то время как фильтры могут возвращать несколько коллекций, состоящих из нескольких элементов.

Представьте, что в коллекции есть три ложки для супа, они сделаны из разных материалов (material): серебра, меди, латуни. Эти ложки имеют разную длину (length): 21 см, 22 см и 21 см, соответственно. Чтобы у нас была возможность определить каждую ложку с помощью локатора, присвоим им идентификатор (id).

<img src="%base_url%/images/CA-09-Sprint-001-16_1675156318.png"/>
<br><br>

Зная идентификатор, можно найти место хранения ресурса «ложка супа»:

`GET http://предметы-сервировки-стола.рф/ложка/для_супа/2`

Таким образом, получился один ресурс —  ложка для супа из меди, длинной 22 см.

### Поиск ресурсов: проекция (Resource Retrieval: Projections)

**Проекция ресурса** — часть данных, запрашиваемого ресурса.

Иногда ресурс содержит слишком много сущностей или полей в ответе. Не всем пользователям нужны данные из всех этих полей, потому есть смысл ограничить число возвращаемых полей теми, которые необходимы пользователю. Это требует меньшей пропускной способности и меньше вычислительных мощностей на стороне пользователя.

Для создания проекции выбирают определённые поля и включают их в запрос, проекции предоставляют только часть данных ресурса. Чтобы реализовать проекции, необходимо объявить большую часть полей необязательными. Это можно сделать с помощью схем JSON и XML. Со стилями представления данных JSON и XML, а также с JSON-схемой и XML-схемой вы познакомитесь в следующих уроках.

В HTTP-запросе есть два способа реализовать проекцию: в параметрах запроса или в параметрах URL. Проекции могут применяться как к коллекциям ресурсов, так и к отдельным экземплярам ресурсов.

### Проекция на коллекцию (Resource Retrieval: Projection on Collection)

Если нужно выбрать единственное поле из коллекции ресурсов, используются параметры запроса. Проекция задаётся с помощью параметра Fields, формате «параметр=значение».

Например: пользователь хочет получить объём всех бокалов в коллекции бокалов. 

`http://предметы-сервировки-стола.рф/бокал?fields=volume`

В случаях, когда нужно выбрать несколько полей из коллекции ресурса, также используют параметр Fields. Значения записывают через знак «,».

Например: пользователь хочет получить объём и материал всех бокалов в коллекции бокалов

`http://предметы-сервировки-стола.рф/бокал?fields=volume,material`

### Проекция на экземпляр ресурса (Projection on Instance Resources)

Если необходимо выбрать одно поле из экземпляра ресурса, используются параметры запроса, например: пользователь хочет получить материал только ложки с идентификатором 2. 

`http://предметы-сервировки-стола.рф/ложка/для_супа/2/material`

Нужно обратить внимание, что параметр «2» — это локатор, к который применяется к коллекции ложек для супа. Дальше через знак «/» указывается параметр ресурса, который необходимо получить. Этим запросом можно получить только один ресурс.

Такая запись является короткой формой, но можно реализовать такой запрос и с использованием параметра запроса Fields. В этом случае после локатора необходимо поставить символ «?», а затем параметры в формате «ключ=значение».

`http://предметы-сервировки-стола.рф/ложка/для_супа/2?fields=material`

Если нужно извлечь несколько параметров, необходимо также использовать параметры запроса. Несколько параметров необходимо писать через знак «,».

`http://предметы-сервировки-стола.рф/ложка/для_супа/2?fields=material,length`

### Передача метаданных (Metadata)

Каждому запросу требуются дополнительная информация об аутентификации, кодировке и типах передаваемых данных. Такие данные передаются в заголовке сообщения.

Метаданные запроса передаются в параметрах заголовка (Header Parameters).

Самым распространенным примером метаданных является заголовок авторизации (Authorization), который содержит в себе данные о логине и пароле пользователя, осуществляющего запрос.

```JSON
GET http://предметы-сервировки-стола.рф
Authorization: Basic FjgFIKVcGVuc5HgjTk
User-Agent: Mozilla/5.0 (Windows; U; Windows NT 6.1; en-US; rv:1.9.1.5) Gecko/20091102 Firefox/3.5.5 (.NET CLR 3.5.30729)
Accept: text/html
Accept-Language: en 
```

### Подведём итоги

В HTTP-запросе передаются параметры, необходимые для выполнения запроса.

Существует четыре вида параметров HTTP:
- параметры URL (URL Parameters);
- параметры запроса (Query Parameters);
- параметры формы (Form Parameters);
- параметры заголовка (Header Parameters).

Все параметры используются, чтобы обеспечить входные данные для запроса, но каждый из типов используется в разных случаях: 
- создание или обновление ресурса (Resource Creation and Update),
- поиск ресурса: фильтрация и сортировка (Resource Retrieval: Filters and Sorting),
- поиск ресурса: локатор (Resource Retrieval: Locators),
- поиск ресурсов: проекция (Resource Retrieval: Projections),
- передача метаданных (Metadata).

Параметры используются не только в HTTP-запросах, но и в HTTP-ответах. В следующем уроке, вы познакомитесь с ними подробнее.