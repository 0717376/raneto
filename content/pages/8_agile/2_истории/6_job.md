---
Title: Job Story
Sort: 6
---

В некоторых случаях техника пользовательских историй (User Stories) не подходит для описания требований, тогда используются Job Stories. В этом уроке вы узнаете, что это такое, чем Job Story отличается от пользовательской истории и в каких случаях используются Job Stories.

### Что такое Job Story

**Job Story** — это техника описания функций ПО, которые позволяют решить проблему пользователя в определённой ситуации.

Job Story акцентирует внимание на ситуации (причина), из-за которой нужно воспользоваться определённой функцией ПО.

Название Job Story придумал Алан Клемент, один из авторов техники JTBD (Job to be Done — «работа, которая должна быть сделана»). Job Stories основаны на JTBD, но это не одна и та же техника. JTBD предполагает, что мы покупаем товары и услуги для выполнения определённой работы, а Job Story описывает, какую именно работу будет выполнять ПО. Здесь и далее речь идёт именно о Job Story. JTBD в этом спринте не рассматривается.

### Шаблон Job Story

Шаблон Job Story — это описание мотивации пользователя применять ПО для достижения желанного результата в определённой ситуации. Системный аналитик пишет шаблон Job Story от первого лица так:
- Когда (ситуация),
- я хочу (мотивация),
- чтобы (ожидаемый результат).

<img src="%base_url%/images/S7-T2-L5-01_1669994673.png"/>
<br><br>

В оригинале шаблон выглядит так:

<img src="%base_url%/images/S7-T2-L5-02_1669994680.png"/>
<br><br>

### Ситуация

Ситуация описывает, в каких обстоятельствах находится пользователь, что стало причиной, которая толкнула его воспользоваться функцией ПО. Важно описать не проблему пользователя, а именно ситуацию, которая порождает проблему.

Разобраться с этим поможет пример с Job Story для картографического сервиса. Важная функция такого сервиса — возможность смотреть сохранённые на устройстве участки карты без соединения с интернетом. Эта история будет называться «Карты в режиме офлайн».

Ситуацию, которая легла в основу этой истории, правильно записывать так: «Когда путешествую в новой стране без доступа к интернету». Нужно избегать формулировки «когда потерялся». Слово «потерялся» указывает на описание проблемы, формулировка «когда потерялся» не даёт понять, что случилось с пользователем, в каких обстоятельствах это произошло. Вариант «путешествую в новой стране без доступа к интернету» указывает на то, что пользователь оказался в незнакомой ему стране и у него пока нет доступа к интернету. Это значит, что есть некоторое затруднение, которое может привести к проблеме — пользователь может потеряться.

### Мотивация (изменение)

В этой части шаблона системный аналитик описывает, какое действие пользователь совершает, чтобы изменить ситуацию и решить проблему.

Как пользователь, который оказался в новой стране без доступа к интернету, может изменить ситуацию? Скорее всего, он хочет открыть на смартфоне карту, которая будет отображаться в офлайн-режиме. 

Слово «хочу» в этой части истории можно заменить на «могу», «должен», «обязан» и другие глаголы, которые выражают отношение пользователя к изменениям. 

Как и в пользовательских историях, в этой части шаблона не нужно упоминать элементы интерфейса. Проблемы пользователя решают не кнопки, а функции ПО.

### Ожидаемый результат

В этой части шаблона нужно указать, что пользователь получит, когда ситуация изменится.

Чтобы сформулировать ожидаемый результат, нужно задаться вопросом: «Для чего?» Формулировки должны давать понимание, к какому результату придёт пользователь: например, сможет добраться из аэропорта до гостиницы.

Нужно избегать абстрактных формулировок ожидаемого результата. Они не позволяют понять, какую проблему пользователю удалось решить и какого результата он смог достичь. «Чтобы не теряться» — как раз абстрактная формулировка, которая не даёт понять, к какому результату пришёл пользователь.

В итоге Job Story «Карты в режиме офлайн» будет сформулирована так:

Когда путешествую в новой стране без доступа к интернету, я хочу открыть на смартфоне карту, доступную в режиме офлайн, чтобы добраться из аэропорта до гостиницы.

<img src="%base_url%/images/S7-T2-L5-03_a_1669994710.png"/>
<br><br>

### Чем схожи Job Story и пользовательская история

#### Одинаковые составляющие

Job Story так же, как и пользовательская история, состоит из 3C:
- Card (карточка).
- Conversation (обсуждение).
- Confirmation (подтверждение).

Системный аналитик записывает Job Story на карточке и обсуждает её детали с членами команды разработки и пользователями. На карточке Job Story тоже записывают примечания, критерии и сценарии приёмки, которые формулируются в ходе обсуждения. После чего системный аналитик фиксирует договорённости (подтверждение).

Полная карточка Job Story картографического сервиса будет выглядеть так:

<img src="%base_url%/images/S7-T2-L5-05_1669994891.png"/>
<br><br>

#### Одинаковые преимущества

Job Stories так же, как и пользовательские истории:
- понятны как пользователю, так и членам команды;
- определяют объёмы работы над функциональностью и сроки реализации;
- используются для формирования бэклога продукта и итераций при работе в гибкой модели;
- переносят акцент с документирования требований на их устное обсуждение;
- помогают достичь единого понимания требований как со стороны пользователей, так и со стороны команды разработки.

#### Job Story даёт дополнительный контекст

Представьте Job Story «Карты в режиме офлайн» в виде пользовательской истории:

Как путешественник, я хочу просматривать карты в режиме офлайн, чтобы добраться из аэропорта до гостиницы.

В этой истории недостаточно контекста: неясно, зачем пользователю понадобились офлайн-карты, почему он не может использовать онлайн-карты. 

Можно переписать историю так:

Как путешественник, я хочу просматривать карты в режиме офлайн, чтобы пользоваться картами без подключения к интернету.

Стало понятнее, но если вспомнить шаблон записи пользовательской истории, получится, что «пользоваться картами» — конечная цель путешественника, хотя это не так. Его цель — добраться из аэропорта до гостиницы. 

Job Story даёт дополнительную информацию о ситуации и отвечает на вопрос: «Когда пользователю требуется функция?» Например, она может потребоваться:
- когда нет доступа к интернету;
- когда пользователь просматривает корзину;
- когда пользователь сделал заказ.

#### Job Story не содержит информации о пользователе

Пользовательская история должна начинаться с записи класса пользователя или персоны — «Как [кто?]». 

Словосочетание «как путешественник» не даёт дополнительной полезной информации о пользователе. Путешественником может быть кто угодно, это слишком общее понятие. Для Job Story не так важно, какая персона или какой класс пользователя будет использовать функционал, поскольку офлайн-карты пригодятся любому пользователю, который оказался без доступа к интернету. Неважно, сколько ему лет, кем он работает и какие у него привычки.

Таким образом, Job Story смещает фокус с особенностей конкретного пользователя, на ситуацию, в которой этот пользователь находится.

### Когда СА использует Job Story

Job Story нужно использовать, если:
- **Пользователи продукта однородны.**
      Пользователи продукта однородны, если среди них нельзя выделить специальные группы, имеющие специфические требования. Если при составлении бэклога все пользовательские истории начинаются с «Как пользователь, я…», стоит использовать Job Story, чтобы избежать постоянного дублирования неважной информации и добавить данных о контексте.
- **Требование актуально для всех групп пользователей.**
      Job Story можно применить для описания требований, если описываемая функция актуальна для всех пользователей. Даже если для ПО выделили несколько целевых групп пользователей или несколько персон.
- **Ситуация важнее класса пользователя.**
      Использование Job Story добавляет ситуации, в которой находится пользователь, контекст. Если информация о том, при каких условиях произойдёт история, важнее, чем информация о том, с кем она произойдёт, нужно использовать Job Story.


### Подведём итоги

В этом уроке вы познакомились с Job Story. Эта техника позволяет записывать пользовательские требования. Она описывает функциональность продукта с точки зрения того, как пользователь применяет эту функциональность в конкретной ситуации.

Как и пользовательские истории, Job Story записывают на индексных карточках, детали истории обсуждаются с пользователями и командой разработки, а договорённости фиксируются в подтверждении.

Шаблон для карточки Job Story состоит из таких элементов:
- Когда (ситуация),
- я хочу (мотивация),
- чтобы (ожидаемый результат).

Использовать Job Story для описания требований нужно, если:
- пользователи продукта однородны, среди них нельзя выделить группы со специальными требованиями;
- требование актуально для всех групп пользователей;
- ситуация, в которой находится пользователь (контекст), важнее класса пользователя.

Job Story позволяет команде, работающей в гибкой модели, определить объёмы работы над функциональностью и сроки реализации, а также сформировать бэклог продукта и итерации.
