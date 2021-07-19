# МойСклад JSON API
## Общие Сведения
### Аутентификация

Для того чтобы успешно взаимодействовать с JSON API онлайн-сервиса МойСклад, необходимо аутентифицироваться
 в системе. МойСклад поддерживает аутентификацию по протоколу Basic Auth и с использованием токена доступа. 
 
 * При аутентификации по протоколу Basic Auth вместе с запросом
 передается заголовок `Authorization` со значением пары `логин:пароль`, закодированным в варианте RFC2045-MIME стандарта Base64.
 * При аутентификации с использованием токена доступа вместе с запросом передается заголовок `Authorization` со значением `Bearer <Access-Token>`.
 
 Аутентификация по протоколу Basic Auth с автоматической генерацией соответствующего
 заголовка и возможность указать заголовок для аутентификации по токену поддерживается во многих HTTP-клиентах, таких как Postman, curl и т.п.

#### Получение нового токена
Запрос на получение нового токена. Как и в других запросах, в заголовке `Authorization` пара `логин:пароль` указывается закодированной в варианте RFC2045-MIME стандарта Base64. 
При генерации нового токена доступа сгенерированные до этого токены пользователя будут отозваны.

* **access_token** - токен для доступа

> Пример запроса на получение нового токена

```shell
curl -X POST
  "https://online.moysklad.ru/api/remap/1.2/security/token"
  -H "Authorization: Basic <Credentials>"
``` 

> Response 200 (application/json) Успешный запрос. Результат JSON объект, содержащий токен

```json
{
  "access_token": "0cbfc512618efa7d5fa306250bca064c1169b37c"
}
```

### Замечания по разработке клиентских приложений
При разработке клиентского приложения необходимо учитывать следующие моменты:

  + Структура ответов и типы полей поддерживаются нами неизменными
  + Может быть добавлено новое поле без нарушения структуры ответа
  + Может быть добавлен новый ресурс

### Ограничения

Для JSON API установлены следующие ограничения:

  + Не более 45 запросов за 3 секундный период от аккаунта
  + Не более 5 параллельных запросов от одного пользователя
  + Не более 20 параллельных запросов от аккаунта
  + Не более 20 Мб данных в одном запросе, отправляемом на сервер
  + Не более 4 [асинхронных задач](#mojsklad-json-api-asinhronnyj-obmen) в очереди на аккаунт

Также накладывается ограничение на максимальное число объектов (позиций, материалов, продуктов), передаваемых в одном массиве в запросе - не более 1000 элементов.
В случае, если количество элементов коллекции превышает максимально допустимое, произойдет ошибка со статусом 413.
Если количество позиций превышает максимально допустимое, то для дальнейшего пополнения позиций нужно будет работать со специальным ресурсом,
описание которого приведено в конкретной сущности.

### Типы данных

|Название| Описание|
| -------|:--------|
**String(MaxLength)**|Представляет текстовые данные в виде последовательности символов UTF-8. MaxLength - максимальная длина строки для конкретного поля. Пример значения: `"Москва"`.
**URL**|Соответствующая стандартам FRC 3986 и RFC 3987 строка URI. Пример значения: `"https://online.moysklad.ru/api/remap/1.2/entity/counterparty"`.
**UUID**|Предствляет строку в формате UUID. Пример значения: `"12a8b923-692c-11e6-8a84-bae500000053"`.
**Boolean**|Представляет значение `true` или `false`.
**Int**|Представляет целое числовое значение в диапазоне -2^31 – 2^31. Пример значения: `200`.
**Long**|Представляет целое числовое значение в диапазоне -2^63 – 2^63. Пример значения: `1613766951558`.
**Float**|Представляет дробное числовое значение. Пример значения: `200.8`.
**DateTime**|Представляет строку в формате "гггг-мм-дд чч-мм-сс". Пример значения: `"2016-08-23 15:21:09"`. [Подробнее тут](#mojsklad-json-api-obschie-swedeniq-format-daty-i-wremeni)
**Object**|Представляет сущность с вложенными полями.
**Meta**|Представляет объект в формате [Метаданных](#mojsklad-json-api-obschie-swedeniq-metadannye).
**Array(Type)**|Массив объектов/значений. Type - тип элементов массива.
**MetaArray**|Объект с полями **meta** и **rows**, где **rows** - массив объектов. Элементы массива **rows** можно запросить, используя [параметр запроса expand](#mojsklad-json-api-obschie-swedeniq-zamena-ssylok-ob-ektami-s-pomosch-u-expand) соответствующего поля.
**Enum**|Представляет строку, принимающую константное множество значений.

### Метаданные

В JSON есть несколько видов Метаданных. Один из них - поле **meta**, которое фигурирует в большинстве
JSON представлений объектов, и содержит информацию об объекте или о выдаче, а также может использоваться в качестве ссылки
на другой объект. Поле **meta** представляет собой объект со следующими атрибутами:

| Название  | Тип | Описание                    | 
| --------- |:----|:----------------------------|
|**href**|URL|Ссылка на объект|
|**metadataHref**|URL|Ссылка на метаданные сущности (Другой вид метаданных. Присутствует не во всех сущностях)
|**type**|String(255)|Тип объекта|
|**mediaType**|String(255)|Тип данных, которые приходят в ответ от сервиса, либо отправляются в теле запроса. В рамках данного  API всегда равен `application/json`|
|**uuidHref**|URL|Ссылка на объект на UI. Присутствует не во всех сущностях. Может быть использована для получения uuid|
|**downloadHref**|URL|Ссылка на скачивание Изображения. Данный параметр указывается только в **meta** для Изображения у Товара или Комплекта.|

###### Атрибуты расширенного объекта meta

Следующие атрибуты объекта **meta** появляются, как правило, в методах выдачи списка сущностей/строк отчета.
В них содержится информация о выдаче, пришедшей в ответ. В объектах **meta**, содержащих
данные лишь об одном объекте (например поле **meta** в объекте **context**) нижеперечисленные атрибуты не фигурируют.  

| Название  | Тип | Описание                    | 
| --------- |:----|:----------------------------|
|**size**|Int|Размер выданного списка|
|**limit**|Int|Максимальное количество элементов в выданном списке. Максимальное количество элементов в списке равно 1000.|
|**offset**|Int|Отступ в выданном списке|

###### Метаданные сущности

Другой вид Метаданных. Представляет собой отдельный ресурс, содержащий информацию обо всех объектах сущностей данного типа.
**Есть не у каждой сущности.** Присутствует лишь у тех сущностей, у которых в данной документации описан ресурс "Метаданные <наименование_сущности>".
Как правило содержит информацию о вложенных сущностях, коллекциях и дополнительных полях.

JSON API позволяет получить метаданные всех сущностей с помощью метода `/entity/metadata`. Также можно ограничить
выборку, указав в фильтре **type** только необходимые сущности.

> Пример запроса на получение метаданных с помощью GET:

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/metadata?filter=type=product;type=service;type=demand"
  -H "Authorization: Bearer <Access-Token>"
```

> Пример тела запроса:

```json
{
  "service": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
      "mediaType": "application/json"
    }
  },
  "product": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
      "mediaType": "application/json"
    }
  },
  "demand": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
      "mediaType": "application/json"
    }
  }
}
```

###### Мета коллекций

**meta** коллекций содержит все те же атрибуты, что и **meta** сущностей, однако, если в списке появляется больше
позиций, чем умещается на одной странице (size > limit) в объект **meta** добавляются след. поля:

| Название  | Тип | Описание                    | 
| --------- |:----|:----------------------------|
|**nextHref**|URL|Ссылка на следующую страницу сущностей.|
|**previousHref**|URL|Ссылка на предыдущую страницу сущностей.

**meta** с такими полями можно встретить при выполнении запросов на получение всех объектов определенного типа
 на учетной записи (например запрос всех отгрузок), а также при запросе всех позиций отдельного документа.

### Обработка ошибок
###### СТРУКТУРА ОШИБОК

Ошибка в данном API представляет собой массив **errors**, содержащий объекты **error**, каждый из которых описывает отдельную ошибку.

###### СТРУКТУРА ОБЪЕКТА error

| Название  | Тип | Описание                    | Свойство поля в запросе | Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**error**               |String(255)|Заголовок ошибки|&mdash;|да
|**parameter**               |String(255)|Параметр, на котором произошла ошибка|&mdash;|нет
|**code**              |Int|Код ошибки (Если поле ничего не содержит, смотрите HTTP status code)|&mdash;|нет
|**error_message**               |String(255)|Сообщение, прилагаемое к ошибке.|&mdash;|нет

###### Возвращаемые HTTP статусы ошибок и их значения:

| HTTP status code | Значение                                                                                                                                            |
| :--------------|:----------------------------------------------------------------------------------------------------------------------------------------------------|
| **301**              | Запрашиваемый ресурс находится по другому URL.                                                                                                      |
| **303**              | Запрашиваемый ресурс может быть найден по другому URI и должен быть найден с использоваием GET запроса                                              |
| **400**              | Ошибка в структуре JSON передаваемого запроса                                                                                                       |
| **401**              | Имя и/или пароль пользователя указаны неверно или заблокированы пользователь или аккаунт                                                            |
| **403**              | У вас нет прав на просмотр данного объекта                                                                                                          |
| **404**              | Запрошенный ресурс не существует                                                                                                                    |
| **405**              | http-метод указан неверно для запрошенного ресурса                                                                                                  |
| **409**              | Указанный объект используется и не может быть удален                                                                                                |
| **410**              | Версия API больше не поддерживается                                                                                                                 |
| **412**              | Не указан обязательный параметр строки запроса или поле структуры JSON                                                                              |
| **413**              | Размер запроса или количество элементов запроса превышает лимит (например, количество позиций, передаваемых в массиве **positions**, превышает 1000)|
| **429**              | Превышен лимит количества запросов                                                                                                                  |
| **500**              | При обработке запроса возникла непредвиденная ошибка                                                                                                |
| **502**              | Сервис временно недоступен                                                                                                                          |
| **503**              | Сервис временно отключен                                                                                                                            |
| **504**              | Превышен таймаут обращения к сервису, повторите попытку позднее                                                                                     |

Также, вместе с телом ответа ошибки, вам могут прийти следующие заголовки (Headers):

+ X-Lognex-Auth - расширенный код ошибки аутентификации
+ X-Lognex-Auth-Message - сообщение об ошибке.
+ X-Lognex-API-Version-Deprecated - дата отключения запрошенной версии API.
+ Location - URL по которому доступен запрашиваемый ресурс (в случае ответа с кодом 301 или кодом 303)

Вы можете узнать лимит оставшихся запросов с помощью следующих заголовков

+ X-RateLimit-Limit - количество запросов, которые равномерно можно сделать в течение интервала до появления 429 ошибки
+ X-Lognex-Retry-TimeInterval - интервал в миллисекундах, в течение которого можно сделать эти запросы
+ X-RateLimit-Remaining - Число запросов, которые можно отправить до получения 429 ошибки
+ X-Lognex-Reset - время до сброса ограничения в миллисекундах. Равно нулю, если ограничение не установлено
+ X-Lognex-Retry-After - время до сброса ограничения в миллисекундах.


### Работа с дополнительными полями

Дополнительные поля позволяют расширить набор свойств некоторых сущностей путем добавления собственных типизированных полей.
JSON API позволяет создавать, обновлять и удалять дополнительные поля и их значения.  

Список сущностей, у которых есть доп. поля:

+ [Договор](dictionaries/#suschnosti-dogowor)
+ [Контрагент](dictionaries/#suschnosti-kontragent)
+ [Юрлицо](dictionaries/#suschnosti-jurlico)
+ [Проект](dictionaries/#suschnosti-proekt)
+ [Склад](dictionaries/#suschnosti-sklad)
+ [Сотрудник](dictionaries/#suschnosti-sotrudnik)
+ [Товар](dictionaries/#suschnosti-towar)
+ [Услуга](dictionaries/#suschnosti-usluga) (располагаются в метаданных Товаров)
+ [Комплект](dictionaries/#suschnosti-komplekt) (располагаются в метаданных Товаров)
+ [Серия](dictionaries/#suschnosti-seriq)
+ Все документы:
  - [Возврат покупателя](documents/#dokumenty-vozwrat-pokupatelq)
  - [Возврат поставщику](documents/#dokumenty-vozwrat-postawschiku)
  - [Входящий платеж](documents/#dokumenty-vhodqschij-platezh)
  - [Заказ покупателя](documents/#dokumenty-zakaz-pokupatelq)
  - [Заказ поставщику](documents/#dokumenty-zakaz-postawschiku)
  - [Исходящий платеж](documents/#dokumenty-ishodqschij-platezh)
  - [Оприходование](documents/#dokumenty-oprihodowanie)
  - [Отгрузка](documents/#dokumenty-otgruzka)
  - [Перемещение](documents/#dokumenty-peremeschenie)
  - [Приемка](documents/#dokumenty-priemka)
  - [Приходный ордер](documents/#dokumenty-prihodnyj-order)
  - [Расходный ордер](documents/#dokumenty-rashodnyj-order)
  - [Розничная продажа](documents/#dokumenty-roznichnaq-prodazha)
  - [Розничная смена](documents/#dokumenty-roznichnaq-smena)
  - [Розничный возврат](documents/#dokumenty-roznichnyj-wozwrat)
  - [Списание](documents/#dokumenty-spisanie)
  - [Инвентаризация](documents/#dokumenty-inwentarizaciq)
  - [Счет покупателю](documents/#dokumenty-schet-pokupatelu)
  - [Счет поставщика](documents/#dokumenty-schet-postawschika)
  - [Счет-фактура выданный](documents/#dokumenty-schet-faktura-wydannyj)
  - [Счет-фактура полученный](documents/#dokumenty-schet-faktura-poluchennyj)
  - [Прайс-лист](documents/#dokumenty-prajs-list)
  - [Внутренний заказ](documents/#dokumenty-vnutrennij-zakaz)
  - [Заказ на производство](documents/#dokumenty-zakaz-na-proizwodstwo)
  - [Тех. операция](documents/#dokumenty-teh-operaciq)
  - [Полученный отчет комиссионера](documents/#dokumenty-poluchennyj-otchet-komissionera)
  - [Выданный отчет комиссионера](documents/#dokumenty-vydannyj-otchet-komissionera)

Посмотреть все созданные доп. поля можно с помощью запроса на получение метаданных сущности.
Ответ будет содержать описание доп. полей в виде коллекции **attributes**, если указанная сущность поддерживает работу с доп. полями.

#### Атрибуты описания доп. поля

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**|[Meta](#mojsklad-json-api-obschie-swedeniq-metadannye)|Ссылка на метаданные доп. поля|&mdash;|да
|**id** |UUID|ID доп. поля|Только для чтения|да
|**name**|String(255)|Наименование доп. поля|Необходимое при создании|да
|**type**|Enum|Тип доп. поля|Необходимое при создании. После заполнения недоступен для изменения|да
|**required**|Boolean|Является ли доп. поле обязательным|&mdash;|да
|**description**|String(4096)|Описание доп. поля|&mdash;|нет

Дополнительные поля конкретной сущности - внутренняя коллекция **attributes**, которая
представлена в виде массива объектов доп. полей со значениями.

#### Атрибуты доп. поля со значением

| Название  | Тип | Описание                    | 
| --------- |:----|:----------------------------|
|**meta**|[Meta](#mojsklad-json-api-obschie-swedeniq-metadannye)|Ссылка на метаданные доп. поля|
|**id** |UUID|ID соответствующего доп. поля|
|**name**|String(255)|Наименование доп. поля|
|**value**|Зависит от типа, см. ниже|Значение, указанное в доп. поле|

Возможные значения типа доп. поля (поле **type**) и соответствующие им значения типа в JSON, а также
типы атрибута **value** в JSON объекта доп поля при соответствующем type:

| Тип атрибута        | Значение поля type в JSON        | Тип поля value в JSON |
| ------------------- |:---------------------------------| --------------------- |
| Строка              | string                           | string                |
| Число целое         | long                             | number                |
| Дата                | time                             | string                |
| Справочник          | {entityType}                     | object **             |
| Файл                | file                             | string                |
| Число дробное       | double                           | number                |
| Флажок              | boolean                          | boolean               |
| Текст               | text                             | string                |
| Ссылка              | link                             | string                |

При передаче значения `null` в поле **value** значение соответствующего доп. поля сбрасывается. 

#### Дополнительные поля типа справочник

Отдельного упоминания заслуживает тип доп. поля "справочник". Значение **type** в представлении
объекта доп. поля будет разным в зависимости от того, справочник каких сущностей был
выбран при создании доп. поля. Ниже представлена таблица, в которой при выбранном типе доп. поля
"справочник" показаны значения поля **type** в зависимости от выбранного типа сущностей в справочнике.

#### Примеры значения **type** у доп. поля типа справочник   

| Тип сущностей справочника | Значение поля type в JSON (entityType) |
| ------------------------- |:---------------------------------------|
| [Контрагент]              | counterparty                           |
| [Товар]                   | product                                |
| [Склад]                   | store                                  |
| [Проект]                  | project                                |
| [Договор]                 | contract                               |
| [Сотрудник]               | employee                               |
| Имя_пользовательского справочника| customentity                    |

Если в качестве типа доп. поля выбран [Пользовательский справочник](dictionaries/#suschnosti-pol-zowatel-skij-sprawochnik), то в составе объекта данного
доп. поля появится новый атрибут **customEntityMeta** являющийся ссылкой на метаданные этого справочника.
Полный набор атрибутов доп. поля будет выглядеть следующим образом:

| Название  | Тип | Описание                    | 
| --------- |:----|:----------------------------|
|**meta**|[Meta](#mojsklad-json-api-obschie-swedeniq-metadannye)|Ссылка на метаданные доп. поля|
|**customEntityMeta** |[Meta](#mojsklad-json-api-obschie-swedeniq-metadannye)|Ссылка на метаданные пользовательского справочника|
|**id** |UUID|ID доп. поля|
|**name**|String(255)|Наименование доп. поля|
|**type**|Enum|Тип доп. поля|
|**required**|Boolean|Является ли доп. поле обязательным|
|**description**|String(4096)|Описание доп. поля|

При выбранном типе доп. поля "справочник" атрибут **value** будет объектом со следующими свойствами:

| Название  | Тип | Описание                    | 
| --------- |:----|:----------------------------|
|**meta**|[Meta](#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные сущности соответствующего справочника|
|**name**|String(255)|Наименование соответствующей сущности|

Обнуление доп. поля типа "справочник" происходит так же, как и при работе с другими доп. полями.
В запросе на обновление в коллекции **attributes** следует указать объект с **id** данного поля, а в качестве **value** передать `null`.

С коллекцией доп. полей можно работать только в контексте отдельной сущности. Доп. поля и их значения
можно передать в коллекции **attributes** в теле запроса как на создание, так и на обновление сущности.
В качестве указания доп. поля нужно использовать поле **meta**.
В переданном массиве объектов можно указать не все доп. поля - проинициализируются/обновятся только указанные.

#### Дополнительные поля типа файл

Для загрузки значения для доп. поля типа файл нужно в JSON при создании или обновлении для значения поля указать объект следующей структуры:

| Название  | Тип | Описание                    | Свойство поля в запросе | Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**filename**              |String(255)|Имя файла|Необходимое при создании|да
|**content**              |String|Байты файла, закодированные в base64|Необходимое при создании|да

Пример указания значения для доп. поля типа файл есть в секции [создания товара](dictionaries/#suschnosti-towar-sozdat-towar)

### Дополнительные поля сущностей
Запрос на получение дополнительных полей сущности.
Список доступных типов сущностей перечислен [тут](#mojsklad-json-api-obschie-swedeniq-rabota-s-dopolnitel-nymi-polqmi).

Структура объекта доп. поля подробно описана в секции [Работа с дополнительными полями](#mojsklad-json-api-obschie-swedeniq-rabota-s-dopolnitel-nymi-polqmi).

**Параметры**

| Параметр                | Описание  |
| ------------------------------ |:---------------------------|
|**limit** |  `number` (optional) **Default: 1000** *Example: 1000* Максимальное количество сущностей для извлечения.`Допустимые значения 1 - 1000`.|
|**offset** |  `number` (optional) **Default: 0** *Example: 40* Отступ в выдаваемом списке сущностей.|
|**entityType** |  `string` *Example: demand* тип сущностей, для которых осуществляется управление доп. полями.|

#### Получить все дополнительные поля для указанного типа
Запрос всех доп. полей для переданного типа сущностей.
Результат: Объект JSON, включающий в себя поля:

| Название               |Тип| Описание  |
| ------------------------------ |---|:---------------------------|
|**meta** |[Meta](#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные о выдаче|
|**rows** |Array(Object)| Массив JSON объектов, представляющих собой доп. поля.|

> Получить доп поля отгрузок

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/attributes"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление списка доп. полей отгрузок.

```json
{
  "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/attributes",
      "mediaType": "application/json"
  },
  "rows": [
    {
      "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/attributes/9862d46e-6500-11e8-9464-e4de00000045",
          "type": "attributemetadata",
          "mediaType": "application/json"
      },
      "id": "9862d46e-6500-11e8-9464-e4de00000045",
      "name": "Строковое",
      "type": "string",
      "required": false,
      "description": "Поле-строка"
    },
    {
      "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/attributes/98630aee-6500-11e8-9464-e4de00000046",
          "type": "attributemetadata",
          "mediaType": "application/json"
      },
      "id": "98630aee-6500-11e8-9464-e4de00000046",
      "name": "Целочисленное",
      "type": "long",
      "required": true
    },
    {
      "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/attributes/98630f62-6500-11e8-9464-e4de00000047",
          "type": "attributemetadata",
          "mediaType": "application/json"
      },
      "id": "98630f62-6500-11e8-9464-e4de00000047",
      "name": "Поле-дата",
      "type": "time",
      "required": false
    },
    {
      "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/attributes/986314b4-6500-11e8-9464-e4de00000048",
          "type": "attributemetadata",
          "mediaType": "application/json"
      },
      "id": "986314b4-6500-11e8-9464-e4de00000048",
      "name": "Справочник-товар",
      "type": "productfolder",
      "required": true
    },
    {
      "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/attributes/986318cd-6500-11e8-9464-e4de00000049",
          "type": "attributemetadata",
          "mediaType": "application/json"
      },
      "id": "986318cd-6500-11e8-9464-e4de00000049",
      "name": "Файловое",
      "type": "file",
      "required": false
    },
    {
      "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/attributes/98631cbf-6500-11e8-9464-e4de0000004a",
          "type": "attributemetadata",
          "mediaType": "application/json"
      },
      "id": "98631cbf-6500-11e8-9464-e4de0000004a",
      "name": "Дробное число",
      "type": "double",
      "required": true,
      "description": "Поле-дробное"
    },
    {
      "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/attributes/986320d6-6500-11e8-9464-e4de0000004b",
          "type": "attributemetadata",
          "mediaType": "application/json"
      },
      "id": "986320d6-6500-11e8-9464-e4de0000004b",
      "name": "Булиновое",
      "type": "boolean",
      "required": false
    },
    {
      "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/attributes/98632583-6500-11e8-9464-e4de0000004c",
          "type": "attributemetadata",
          "mediaType": "application/json"
      },
      "id": "98632583-6500-11e8-9464-e4de0000004c",
      "name": "Текстовое",
      "type": "text",
      "required": true
    },
    {
      "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/attributes/98632a03-6500-11e8-9464-e4de0000004d",
          "type": "attributemetadata",
          "mediaType": "application/json"
      },
      "id": "98632a03-6500-11e8-9464-e4de0000004d",
      "name": "Ссылочное",
      "type": "link",
      "required": false
    }
  ]
}
```

#### Создать дополнительные поля
Действие доступно только для пользователя с правами администратора.<br>
Запрос на создание нового доп. поля для указанного типа сущностей.

> Создание двух новых доп. полей для отгрузок.

```shell
curl -X POST
  "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/attributes"
  -H "Authorization: Basic <Credentials>"
  -H 'Content-Type: application/json' \
  -d '[
        {
          "name": "Строковое",
          "type": "string",
          "required": false,
          "description": "Поле-строка"
        },
        {
          "name": "Целочисленное",
          "type": "long",
          "required": true
        }
      ]'
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление созданных доп. полей.

```json
[
  {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/attributes/7bc578d8-6501-11e8-9464-e4de00000004",
      "type": "attributemetadata",
      "mediaType": "application/json"
    },
    "id": "7bc578d8-6501-11e8-9464-e4de00000004",
    "name": "Строковое",
    "type": "string",
    "required": false,
    "description": "Поле-строка"
  },
  {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/attributes/7bd3d688-6501-11e8-9464-e4de00000005",
      "type": "attributemetadata",
      "mediaType": "application/json"
    },
    "id": "7bd3d688-6501-11e8-9464-e4de00000005",
    "name": "Целочисленное",
    "type": "long",
    "required": true
  }
]
```

> Пример создания нового доп. поля Отгрузок и обновления существующего одним запросом.

```shell
curl -X POST
  "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/attributes"
  -H "Authorization: Basic <Credentials>"
  -H 'Content-Type: application/json' \
  -d '[
        {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/attributes/7bc578d8-6501-11e8-9464-e4de00000004",
            "type": "attributemetadata",
            "mediaType": "application/json"
          },
          "name": "Строковое поле",
          "required": true,
          "description": "Поле-строка"
        },
        {
          "name": "Целочисленное2",
          "type": "long",
          "required": true
        }
      ]'
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление созданного и обновленного доп. полей.

```json
[
  {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/attributes/7bc578d8-6501-11e8-9464-e4de00000004",
      "type": "attributemetadata",
      "mediaType": "application/json"
    },
    "id": "7bc578d8-6501-11e8-9464-e4de00000004",
    "name": "Строковое поле",
    "type": "string",
    "required": true,
    "description": "Поле-строка"
  },
  {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/attributes/c66edb30-6501-11e8-9464-e4de00000008",
      "type": "attributemetadata",
      "mediaType": "application/json"
    },
    "id": "c66edb30-6501-11e8-9464-e4de00000008",
    "name": "Целочисленное2",
    "type": "long",
    "required": true
  }
]
```

> Пример создания дополнительного поля типа пользовательский справочник.

```shell
curl -X POST
  "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/attributes"
  -H "Authorization: Basic <Credentials>"
  -H 'Content-Type: application/json' \
  -d '{
        "customEntityMeta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/context/companysettings/metadata/customEntities/0347beb0-a785-11e9-ac12-000800000003",
          "type": "customentitymetadata",
          "mediaType": "application/json"
        },
        "name": "Доп поле типа пользовательский справочник",
        "type": "customentity",
        "required": false
      }'
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление созданного доп. поля.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/attributes/53eb36a5-a78a-11e9-ac12-000c00000000",
    "type": "attributemetadata",
    "mediaType": "application/json"
  },
  "customEntityMeta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/context/companysettings/metadata/customEntities/0347beb0-a785-11e9-ac12-000800000003",
    "type": "customentitymetadata",
    "mediaType": "application/json"
  },
  "id": "53eb36a5-a78a-11e9-ac12-000c00000000",
  "name": "Доп поле типа пользовательский справочник",
  "type": "customentity",
  "required": false
}
```

#### Удалить дополнительные поля
Действие доступно только для пользователя с правами администратора.<br>
Запрос на удаление нескольких доп. полей отгрузок.

> Удаление двух доп полей одним запросом

```shell
curl -X POST
  "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/attributes/delete"
  -H "Authorization: Basic <Credentials>"
  -H 'Content-Type: application/json' \
  -d '[
        {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/attributes/986318cd-6500-11e8-9464-e4de00000049",
            "type": "attributemetadata",
            "mediaType": "application/json"
          }
        },
        {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/attributes/98631cbf-6500-11e8-9464-e4de0000004a",
            "type": "attributemetadata",
            "mediaType": "application/json"
          }
        }
      ]'
```

> Response 200 (application/json)
Успешное удаление доп. полей.

### Дополнительное поле
**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7bc578d8-6501-11e8-9464-e4de00000004* id доп. поля.|

#### Получить дополнительное поле
Запрос на получение отдельного доп. поля отгрузок с указанным id.


> Запрос на получение отдельного доп. поля отгрузки

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/attributes/7bc578d8-6501-11e8-9464-e4de00000004"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление доп. поля отгрузки.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/attributes/7bc578d8-6501-11e8-9464-e4de00000004",
    "type": "attributemetadata",
    "mediaType": "application/json"
  },
  "id": "7bc578d8-6501-11e8-9464-e4de00000004",
  "name": "Строковое поле",
  "type": "string",
  "required": true,
  "description": "Поле-строка"
}
```

#### Изменить дополнительное поле
Действие доступно только для пользователя с правами администратора.<br>
Запрос на обновление отдельного доп. поля для переданного типа сущностей.

> Запрос на обновление доп. поля отгрузки

```shell
curl -X PUT
  "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/attributes/7bc578d8-6501-11e8-9464-e4de00000004"
  -H "Authorization: Basic <Credentials>"
  -H 'Content-Type: application/json' \
  -d '{
        "name": "обновленное Строковое поле",
        "required": false,
        "description": "Обновленное поле-строка"
      }'
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление доп. поля отгрузки.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/attributes/7bc578d8-6501-11e8-9464-e4de00000004",
    "type": "attributemetadata",
    "mediaType": "application/json"
  },
  "id": "7bc578d8-6501-11e8-9464-e4de00000004",
  "name": "обновленное Строковое поле",
  "type": "string",
  "required": false,
	"description": "Обновленное поле-строка"
}
```

#### Удалить дополнительное поле
Действие доступно только для пользователя с правами администратора.<br>
Запрос на удаление доп. поля отгрузок с указанным id.

> Запрос на удаление доп. поля отгрузки

```shell
curl -X DELETE
  "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/attributes/7bc578d8-6501-11e8-9464-e4de00000004"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешное удаление доп. поля.

### Обновление значений дополнительных полей
Запрос на обновление коллекции доп. полей конкретной сущности.

> Запрос на обновление доп. полей отгрузки

```shell
curl -X PUT
  "https://online.moysklad.ru/api/remap/1.2/entity/demand/7bc578d8-6501-11e8-9464-e4de00000001"
  -H "Authorization: Basic <Credentials>"
  -H 'Content-Type: application/json' \
  -d '{
        "attributes": [
          {
            "meta": {
              "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/attributes/986314b4-6500-11e8-9464-e4de00000048",
              "type": "attributemetadata",
              "mediaType": "application/json"
            },
            "value": "new string"
          }
        ]
      }'
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление отгрузки с обновленными доп. полями.

```json
{
...
  "attributes": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/attributes/986314b4-6500-11e8-9464-e4de00000048",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "986314b4-6500-11e8-9464-e4de00000048",
      "name": "Строковое поле",
      "type": "string",
      "value": "new string"
    }
  ]
...
}
```

### Работа с позициями документов

API сервиса МойСклад позволяет оперировать с такими документами как [Отгрузка](documents/#dokumenty-otgruzka), [Заказ покупателя](documents/#dokumenty-zakaz-pokupatelq), [Счет покупателю](documents/#dokumenty-schet-pokupatelu),
[Розничная продажа](documents/#dokumenty-roznichnaq-prodazha), [Полученный отчет комиссионера](documents/#dokumenty-poluchennyj-otchet-komissionera), [Выданный отчет комиссионера](documents/#dokumenty-vydannyj-otchet-komissionera), [Оприходование](documents/#dokumenty-oprihodowanie),
[Внутренний заказ](documents/#dokumenty-vnutrennij-zakaz), [Инвентаризация](documents/#dokumenty-inwentarizaciq), [Списание](documents/#dokumenty-spisanie), [Перемещение](documents/#dokumenty-peremeschenie), [Прайс-лист](documents/#dokumenty-prajs-list),
[Заказ на производство](documents/#dokumenty-zakaz-na-proizwodstwo), [Возврат поставщику](documents/#dokumenty-vozwrat-postawschiku), [Заказ поставщику](documents/#dokumenty-zakaz-postawschiku),
[Розничный возврат](documents/#dokumenty-roznichnyj-wozwrat), [Возврат покупателя](documents/#dokumenty-vozwrat-pokupatelq), [Приемка](documents/#dokumenty-priemka), [Счет поставщика](documents/#dokumenty-schet-postawschika). Перечисленные документы содержат позиции, работать с которыми можно как в составе отдельного документа,
так и с помощью специальных ресурсов для управления позициями документа.

######  Работа с позициями в рамках отдельного документа

При работе с позициями в рамках отдельного документа, их можно передавать как поле **positions**, представляющее собой массив позиций документа, в составе объекта, использующегося
в запросе на изменение или создание документа. В таком случае, массив позиций воспринимается как множество всех позиций документа
и полностью заменяет (в случае запроса на обновление) все уже существующие позиции в документе. В случае запроса на обновление, все позиции, которые существовали ранее в документе,
но не были переданы в теле запроса на обновление, будут удалены, все существующие позиции, id которых совпал с id передаваемых позиций в теле запроса, будут обновлены,
а новые позиции, которых ранее не было среди существующих позиций документа, будут добавлены в список позиций.

######  Работа с позициями документов с помощью специальных ресурсов

В JSON API предусмотрены специальные ресурсы для управления позициями документов. Эти ресурсы как правило доступны по следующему URI и с помощью них вы сможете удалять позиции из документа, сделав запрос с методом DELETE по URL соответствующего ресурса с указание id позиции:

+ `/{код сущности документа, в составе JSON API}/{id отдельного документа}/positions/{id отдельной позиции}`

> Пример URL для запроса на удаление с помощью DELETE:

```shell
curl -X DELETE 
  "https://online.moysklad.ru/api/remap/1.2/{код сущности документа, в составе JSON API}/{id отдельного документа}/positions/179dd832-960c-11e6-8a84-bae5000000dc
  -H "Authorization: Bearer <Access-Token>"
```


При работе со специальными ресурсами можно запрашивать список всех позиций документа, создавать новые позиции, а также обновлять существующие. При создании новых позиций с помощью данных ресурсов, можно обходить ограничение в 1000 позиций на документ. Также, используя данный ресурс, можно управлять массовым обновлением позиций. Для изменения сведений по отдельным позициям необходимо использовать ресурсы управления отдельными позициями документа, которые доступны по URI:

+ `/{код сущности документа, в составе JSON API}/{id отдельного документа}/positions/{id отдельной позиции}`

Оба способа работы с позициями также описаны в документации по каждому из документов.

Также возможно массовое удаление позиций документа, используя метод POST по URL соответствующего ресурса. В теле запроса необходимо указать массив удаляемых позиций, указав поле meta у каждой из позиций.

> Пример URL для запроса на массовое удаление позиций с помощью POST:

```shell
curl -X POST
  "https://online.moysklad.ru/api/remap/1.2/{код сущности документа, в составе JSON API}/{id отдельного документа}/positions/delete
  -H "Authorization: Bearer <Access-Token>"
```

> Пример тела запроса:

```json
[
  {
    "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/405f69c0-019e-11e6-9464-e4de00000085/positions/727cf336-0310-11e6-9464-e4de00000013",
        "type": "demandposition",
        "mediaType": "application/json"
    }
  },
  {
    "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/405f69c0-019e-11e6-9464-e4de00000085/positions/727cfce0-0310-11e6-9464-e4de00000014",
        "type": "demandposition",
        "mediaType": "application/json"
    }
  },
  {
    "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/405f69c0-019e-11e6-9464-e4de00000085/positions/727d057f-0310-11e6-9464-e4de00000015",
        "type": "demandposition",
        "mediaType": "application/json"
    }
  }
]
```

### Остатки в позициях документов

> Представление остатков в составе позиции

```json
"stock": {
    "cost": 5000,
    "quantity": 999,
    "reserve": 90,
    "intransit": 9,
    "available": 918
}
```

При запросе и обновлении документов есть возможность получать остатки позиций этих документов.
Для получения остатков в позициях документа в запросе нужно передать дополнительный параметр `fields=stock`.
Например,

+ `/customerorder/{id документа}?fields=stock&expand=positions`

Остатки можно получить по следующим документам: `[Отгрузка, Заказ Покупателя, Розничная продажа, Счет покупателя, Заказ поставщика, Счет поставщика, Приемка, Возврат поставщику, Возврат покупателя, Розничный возврат]`

Остатки для документов **Отгрузка**, **Розничная продажа**, **Приемка**, **Возврат поставщику**, **Возврат покупателя**, **Розничный возврат** расчитываются на момент поля **moment** в данных документах.
Для **Заказа покупателя**, **Счета покупателя**, **Заказа поставщика**, **Счета поставщика** остатки рассчитываются на текущий момент времени.

Получить остатки можно для следующих запросов:

+ Получения списка операций
+ Получение отдельной операции
+ Получение позиций операции
+ Получение отдельной позиции операции
+ Обновление операции
+ Обновление позиции

При составлении запроса на получение списка операций нужно дополнительно передать параметр `limit` со значением, не превышающем 100.
Например,

+ `/customerorder?fields=stock&expand=positions&limit=100`                                                                                                                                     

Для возврата покупателя без основания и розничного возврата без основания поле `cost` будет отсутствовать в составе `stock`.


### Назначение поля syncId

Сущностям, у которых среди атрибутов присутствует поле **syncId**, оно необходимо для того, чтобы в случае сбоя
при повторной отправке запроса на создание новой сущности не происходило дублирование объектов. Если в теле запроса
на создание сущности указать сгенерированный на клиенте syncId, то при повторной отправке этого же запроса (с тем же syncId) вместо создания
сущности с идентичными полями в ответ придет ранее созданная сущность.
Сущности, поддерживающие поле **syncId**, можно удалить, используя url типа `/entity/{type}/syncid/{id}`.

### Создание и обновление объекта

При создании объекта достаточно заполнить только поля, помеченные `Необходимое`. Данные поля используются только при создании, при обновлении они не требуются.
Поля, помеченные `Только для чтения`, игнорируются при создании/обновлении объекта.

### Создание и обновление нескольких объектов

При использовании метода POST вы можете указать в теле запроса вместо одной -
массив сущностей. Для этого, вам нужно передать массив (начать тело запроса с `[` и закончить `]`), который будет содержать JSON представления
объектов, которые вы хотите создать или обновить. Обновляемые сущности должны содержать идентификатор в виде метаданных.
Если при обновлении сущность не найдена, она будет создана.

Также возможно произвести массовое удаление сущностей, если при использовании метода POST указать url вида `/entity/{type}/delete`.

Лимит на создание, обновление и удаление объектов списком - 1000

### Поддержка null

В рамках JSON API можно удалить значение из поля типа объект (если это поле не является обязательным, или же если данное поле в
основном интерфейсе может содержать пустое значение). Например: поле Договор(**contract**) в любом из документов. Сделать это можно передав в
запросе на обновление сущносте в данное поле null. Например: `{  "contract": null  }`.
Удаление валюты из документов (`{rate: null}`) равносильно изменению валюты документа на валюту по умолчанию. В результате все
цены и суммы будут пересчитаны. Накладные расходы также будут пересчитаны, если они не были указаны явно.

### Пустые поля

Если какое-то из полей сущности не было заполнено и, при этом оно не является обязательным, оно не будет выдано в JSON представлении этой сущности.

### Формат даты и времени

В JSON API поля типа дата-время (момент времени) - это строка в формате:

+ Без миллисекунд: `ГГГГ-ММ-ДД ЧЧ:мм:сс`
+ С миллисекундами: `ГГГГ-ММ-ДД ЧЧ:мм:сс.ммм` В этом формате возвращаются поля типа дата-время в ответах на запросы.
+ Без секунд: `ГГГГ-ММ-ДД ЧЧ:мм` Только для параметров фильтрации.

Следующие поля устанавливаются и выводятся в JSON API с точностью до минут, а именно со значением секунд и миллисекунд равным `00`:

+ **incomingDate**
+ **commisionPeriodStart**
+ **commisionPeriodEnd**
+ **certificateDate**
+ **moment**
+ **deliveryPlannedMoment**
+ **paymentPlannedMoment**
+ **firstDemandDate**
+ **lastDemandDate**
+ дополнительное поле с типом **Дата**

### Сортировка объектов

Для сортировки списка объектов можно использовать url параметр `order`.
Значение этого параметра - **urlencoded** строка с условиями сортировки, перечисленными через `;`. (Все примеры ниже указаны без urlencoded для лучшей читаемости)
Каждое условие сортировки- это сочетание названия поля, запятой (опционально, если указывается направление сортировки), направления сортировки (опционально; может принимать значения  `asc` и `desc`. Значение по умолчанию - `asc`).

Сортировка поддерживается для следующих типов полей: числовой, строковый, дата-время, логический и uuid.

Примеры запросов с сортировкой:

+ https://online.moysklad.ru/api/remap/1.2/entity/supply?order=name
+ https://online.moysklad.ru/api/remap/1.2/entity/product?order=code,desc
+ https://online.moysklad.ru/api/remap/1.2/entity/product?order=name;code,desc
+ https://online.moysklad.ru/api/remap/1.2/entity/product?order=name,desc;code,asc

### Фильтрация выборки с помощью параметра filter

Для фильтрации выборки по нескольким полям можно использовать url параметр `filter`.
Значение этого параметра - **urlencoded** строка с поисковыми условиями, перечисленными через `;`. Для использования самого символа `;` 
в текстовых фильтрах необходимо указывать два символа `\;`.
(Все примеры ниже указаны без urlencoded для лучшей читаемости)
Каждое поисковое условие - это сочетание названия поля, оператора и константы.
Фильтровать можно по всем полям, значения которых являются примитивными типами. Т.е. нельзя фильтровать поля-объекты и поля-массивы,
все остальные поля могут быть использованы в параметре `filter`.

+ Допустимые операторы: `['=', '>', '<', '>=', '<=', '!=', '~', '~=', '=~']`

Если в поисковом запросе несколько раз встречается условие типа "равенство" `=` примененное к одному и тому же полю,
то такое условие интерпретируется как совокупность условий, разделенных логическим оператором `ИЛИ`.

+ Например условие `filter=sum=100;sum=150` будет интерпретировано как `sum=100 ИЛИ sum=150`
или же `sum in (100, 150)`

Если же встречается несколько условий вида "не равно" `!=`, наложенных на одну и ту же переменную, то они интерпретируются как совокупность
условий разделенных логическим оператором `И`.

+ Например условие `filter=name!=0001;name!=0002` будет эквивалентно следующим (взаимно эквивалентным) условиям :
`name != 0001 И name != 0002` или `name not in (0001, 0002)`

Если на одно из полей наложено ограничение типа "равенство", а затем на него накладывается ограничение типа неравенство - в таком случае произойдет ошибка.

+ Например условие `filter=sum=100;sum>99` вызовет ошибку.

Допускается использование одновременно нескольких одинаковых операторов сравнения `['>', '<', '>=', '<=']` для одного поля. При этом будет использовано лишь первое значение.

+ Например условие `filter=sum>99;sum>100` будет аналогично условию `filter=sum>99`.
В будущих версиях такое условие будет вызывать ошибку.

Фильтры, примененные к разным полям объединяются через логическое `И`, т.е. в запросе вида:

+ `filter=sum=100;moment>2016-10-11 12:00:00` выборка будет отфильтрована и по сумме и по дате.

######  Проверка на пустое значение

Если в строке фильтрации указать конструкцию вида: `<имя_поля>=;` то в выборку попадут только объекты, где
данное поле равно null (т.е. отсутствует значение), а если тип поля - строковое, то будет также выполнена проверка на пустую строку, т.е. поле=''.
Конструкция `<имя_поля>!=;` выполнит проверку на присутствие значения. С помощью данной конструкции можно проверить наличие значения в ссылочном поле.

###### Фильтрация документов

Для фильтрации выборки **документов** можно использовать параметр **isDeleted**. Принимает значения `true` и `false`.

+ При указании значения `true` вернутся все документы данного типа, находящиеся в корзине.
+ При указании значения `false` вернутся только неудаленные документы.
+ Можно вывести все документы: и удаленные, и нет, указав в запросе оба значения данного параметра: `filter=isDeleted=true;isDeleted=false`.

Для фильтрации выборки напечатанных **документов** используется параметр **printed**. Принимает значения `true` и `false`.

Для фильтрации выборки отправленных **документов** используется параметр **published**. Принимает значения `true` и `false`.


###### Фильтрация сущностей

Для фильтрации выборки **сущностей** следует использовать параметр **archived**. Данный параметр принимает значения `true` и `false`.

+ При указании значения `true` вернутся все сущности данного типа, находящиеся в архиве.
+ При указании значения `false` вернутся только не архивные сущности.
+ Можно вывести все сущности: и архивные, и нет, указав в запросе оба значения данного параметра: `filter=archived=true;archived=false`.
Фильтровать по параметру archived можно только те сущности, у которых данный параметр присутствует в списке полей.

###### Фильтрация ссылочных полей

С помощью filter можно фильтровать ссылочные поля. Если в сущности присутствует ссылочное поле в виде метаданных,
можно использовать следующую конструкцию для того чтобы отфильтровать по этому полю выборку:

+ `filter=<имя_поля>=<ссылка>`

Пример ссылки:

+ `http://online.moysklad.ru/api/remap/1.2/entity/<type>/<id>`

Вот несколько примеров:

+ `filter=agent=http://online.moysklad.ru/api/remap/1.2/entity/counterparty/<id>`
+ `filter=ownAgent=http://online.moysklad.ru/api/remap/1.2/entity/organization/<id>`

Ссылочные поля, доступные для фильтрации:

+ agent
+ ownAgent
+ owner
+ group
+ parent
+ contract
+ project
+ organization
+ store
+ agentStore
+ supplier

Для розничных операций ("Розничная смена", "Розничная продажа", "Розничный возврат", "Внесение денег", "Выплата денег") также доступна фильтрация по:

+ retailstore

Примеры запросов для фильтрации :

+ `https://online.moysklad.ru/api/remap/1.2/entity/demand?filter=moment>2016-10-11 12:00:00;moment<2016-10-11 13:00:00;sum=100;name=0010;name=0011`
+ `https://online.moysklad.ru/api/remap/1.2/entity/counterparty?filter=name=Иван;phone=89269269222;email=vanyan@mail.krut`

###### Фильтрация по полям типа ID

С помощью filter можно фильтровать поля типа ID.

+ `filter=<имя_поля>=<ID>`

Пример ID:

+ `94975104-3cad-11e8-1e44-bd4d00000084`

Например:

+ `filter=productid=94975104-3cad-11e8-1e44-bd4d00000084`

###### Фильтрация по дополнительным полям

С помощью filter можно фильтровать по дополнительным полям. Список дополнительных полей сущности указан в ее метаданных

`https://online.moysklad.ru/api/remap/1.2/entity/product/metadata`

Можно использовать следующую конструкцию для того чтобы отфильтровать по дополнительному полю выборку:

+ `filter=<ссылка на доп.поле>=<значение>`

для доп.полей типа справочник:

+ `filter=<ссылка на доп.поле>=<ссылка на сущность>`

Пример ссылки на доп.поле

+ `http://online.moysklad.ru/api/remap/1.2/entity/<type>/metadata/attributes/<id>`

Пример ссылки на сущность:

+ `http://online.moysklad.ru/api/remap/1.2/entity/<type>/<id>`

для доп.полей типа пользовательский справочник

+ `http://online.moysklad.ru/api/remap/1.2/entity/customentity/<customentity_id>/<id>`

Примеры фильтра:

+ `filter=https://online.moysklad.ru/api/remap/1.2/entity/<type>/metadata/attributes/<id>
=42`

+ `filter=https://online.moysklad.ru/api/remap/1.2/entity/<type>/metadata/attributes/<id>
=http://online.moysklad.ru/api/remap/1.2/entity/<type>/<id>`

###### Дополнительные фильтры

С помощью filter=state.name=<ИмяСтатуса> можно фильтровать документы по имени статуса. 
state.name Параметр строкового типа. В отфильтрованную выборку попадут все документы данного типа, на которые выставлен статус с указанным именем.

Пример запроса с использованием фильтра state.name:

`https://online.moysklad.ru/api/remap/1.2/entity/customerOrder?filter=state.name=Новый;state.name=Принят`

Фильтр filter=assortment=<href сущности> позволяет фильтровать документы по наличию позиций с указанными сущностями ассортимента.
assortment - параметр, принимающий href ассортимента или группы товаров. Допустимые типы сущностей: Товар, Услуга, Модификация, Комплект, Группа товаров. 
В выборку попадут те документы, которые содержат указанные сущности в числе позиций, или, в случае указания Групп товаров, одну из сущностей из указанных Групп товаров.

Пример запроса с использованием фильтра assortment:

`https://online.moysklad.ru/api/remap/1.2/entity/demand?filter=assortment=https://online.moysklad.ru/api/remap/1.2/entity/product/166909e6-4a99-11e6-8a84-bae500000089`

### Фильтрация по сущностям, на которые нет права просмотра

При фильтрации по сущности, на которую у текущего пользователя нет прав на просмотр в ответе придет пустой список.
Например, при фильтрации задач (**task**) по автору (**author**), который является сотрудником, которого не может просматривать текущий пользователь,
в ответ вернется пустой список задач.

### Контекстный поиск

В JSON API можно осуществлять контекстный поиск среди списка сущностей определенного типа по их строковым полям. Для этого
используется URI параметр фильтрации **search**

+ **search**
  Параметр фильтрации, с помощью которого можно осуществить поиск в списке сущностей. Поиск происходит по основным строковым полям сущностей данного
    типа. Результатом поиска будет отсортированный по релевантности список сущностей данного типа, прошедших фильтрацию по переданной поисковой строке. В отличии от фильтрации выборки
    с помощью параметра **filter**, при которой значения проверяются на точное совпадение указанным, при контекстном поиске проверка на совпадение не строгая.
    Таким образом, если осуществлять фильтрацию вида `../entity/<entity_type>?filter=name=120` в отфильтрованную выборку попадут только те сущности, поле **name**
    у которых имеет значение `120` и никакие другие. При контекстном поиске вида `../entity/<entity_type>?search=120` будут выведены как сущности с **name** равным
    `120`, так и сущности, в имени (или в другом строковом поле) которых `120` является началом какого-то слова, например `12003`, `пазл детский 1200 штук` и т.п.
    Причем, если ввести несколько слов `../entity/<entity_type>?search=120 возврат` и поиск идет по полям **name** и **description**, то будут выведены как сущности с **name** равным `1200` и с **description**
    равным `возврат из-за деффекта`, так и сущности с именем `777` с описанием `розничный возврат на улице 120 летия`.

  + Примеры запросов контекстного поиска (значения должны быть urlencoded):
    - `https://online.moysklad.ru/api/remap/1.2/entity/project?search=реструктуризация`
    - `https://online.moysklad.ru/api/remap/1.2/entity/move?search=ул.Вавилова`
    - `https://online.moysklad.ru/api/remap/1.2/entity/counterparty?search=петров`



### Оператор фильтрации "подобие"

В JSON API для <u>строковых</u> полей есть специальный оператор фильтрации "подобие".

+ `~`  обычное подобие. Ищет любое вхождение подстроки, следующей после оператора, в значении поля. Например, `?filter=code~ms` найдет все сущности, у которых в коде встречается подстрока "ms".
+ `~=` левое подобие. Ищет соответствие по префиксу значения. Например `?filter=code~=ms` найдет все сущности, у которых код начинается на "ms".
+ `=~` правое подобие. Ищет соответствие по постфиксу. Например `?filter=code=~ms` найдет все сущности, у которых код оканчивается на "ms".

Операторы подобия работают исключительно с полями строкового типа и не учитывают регистр. К полям типа uuid и дата-время они неприменимы.

### Ссылки на файлы

В JSON API для скачивания файла формируется редирект на временный URL файла (конечную ссылку). Для корректной работы необходимо поддерживать обработку редиректов. 
По умолчанию время жизни конечной ссылки равно одной минуте.

Можно задать время жизни конечной ссылки на скачивание файла, указав количество секунд в специальном заголовке `X-Lognex-Download-Expiration-Seconds`.
Заголовок принимает целое положительное число не больше 86400 (24 часа).

### Замена ссылок объектами с помощью expand 

В JSON API, в составе сущностей можно встретить ссылки на связанные объекты.
Ссылки выводятся в формате [Метаданных](#mojsklad-json-api-obschie-swedeniq-metadannye). Для того, чтобы вместо ссылок получить связанные объекты,
не обязательно делать отдельные запросы для каждого из них. Вместо этого, вместе с запросом на получение сущности, нужно передать параметр **expand**.
В качестве значения данного параметра нужно перечислить через запятую все необходимые поля-ссылки,
на месте которых вы бы хотели видеть связанные объекты.
В результате запроса с таким параметром, в ответе вы получите объект с развернутыми вложенными объектами вместо ссылок.
К примеру, в документах, имеющих в составе поле **agent**, вместо ссылки на
контрагента будет выведен объект со всеми полями сущности "Контрагент", описанными [тут](dictionaries/#suschnosti-kontragent).
Максимальный уровень вложенности **expand** : 3.
Expand разрешен только на размере выборки не более 100. Если указан больший лимит, но указан expand, то данный параметр будет игнорироваться.

Также **expand** можно применять для результатов операций создания и обновления.

+ Ниже показаны примеры использования **expand** на [Возврате покупателя](documents/#dokumenty-vozwrat-pokupatelq). В примерах представлены только поля **meta** и **demand**.

### Возврат без expand 

> Пример запроса возврата без expand

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/salesreturn/166909e6-4a99-11e6-8a84-bae500000089"
  -H "Authorization: Basic <Credentials>"
```

> Объект возврата покупателя в его обычном представлении, имеющий ссылку на отгрузку

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/salesreturn/166909e6-4a99-11e6-8a84-bae500000089",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/salesreturn/metadata",
    "type": "salesreturn",
    "mediaType": "application/json"
  },
  ...
  "demand": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/f99544d7-4a98-11e6-8a84-bae50000007f",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
      "type": "demand",
      "mediaType": "application/json"
    }
  }
}
```

### Возврат с expand отгрузки 

> Пример запроса возврата с expand отгрузки
Передаем параметр **expand**=demand.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/salesreturn/166909e6-4a99-11e6-8a84-bae500000089?expand=demand"
  -H "Authorization: Basic <Credentials>"
```

> В ответ придет возврат покупателя, у которого вместо ссылки на отгрузку, по которой производится возврат, будет вложенный объект со всеми полями данной отгрузки.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/salesreturn/166909e6-4a99-11e6-8a84-bae500000089?expand=demand",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/salesreturn/metadata",
    "type": "salesreturn",
    "mediaType": "application/json"
  },
  ...
  "demand": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/f99544d7-4a98-11e6-8a84-bae50000007f",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
      "type": "demand",
      "mediaType": "application/json"
    },
    "id": "f99544d7-4a98-11e6-8a84-bae50000007f",
    "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
    "owner": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/faba7f37-2e58-11e6-8a84-bae500000028",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
        "type": "employee",
        "mediaType": "application/json"
      }
    },
    "shared": false,
    "group": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/group/f97aa1fb-2e58-11e6-8a84-bae500000002",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/group/metadata",
        "type": "group",
        "mediaType": "application/json"
      }
    },
    ...
    "positions": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/f99544d7-4a98-11e6-8a84-bae50000007f/positions",
        "type": "demandposition",
        "mediaType": "application/json",
        "size": 2,
        "limit": 1000,
        "offset": 0
      }
    },
    "vatEnabled": true,
    "vatIncluded": true,
    "payedSum": 0,
    "returns": [
      {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/salesreturn/166909e6-4a99-11e6-8a84-bae500000089",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/salesreturn/metadata",
          "type": "salesreturn",
          "mediaType": "application/json"
        }
      }
    ]
  }
}
```

### Expand с глубиной 2 

> Пример запроса возврата c expand с глубиной 2 
Теперь развернем поле **agent** у вложенной в возврат отгрузки (**demand**).
В ответ придет возврат покупателя с развернутой отгрузкой (**demand**), внутри которой
будет развернутый объект контрагента (**agent**). <br>В данном запросе продемонстрирован уровень вложенности
параметра **expand** равный двум.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/salesreturn/166909e6-4a99-11e6-8a84-bae500000089?expand=demand,demand.agent"
  -H "Authorization: Basic <Credentials>"
```

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/salesreturn/166909e6-4a99-11e6-8a84-bae500000089?expand=demand,demand.agent",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/salesreturn/metadata",
    "type": "salesreturn",
    "mediaType": "application/json"
  },
  ...
  "demand": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/f99544d7-4a98-11e6-8a84-bae50000007f?expand=agent",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
      "type": "demand",
      "mediaType": "application/json"
    },
    ...
    "agent": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/147c1f1b-32ca-11e6-8a84-bae500000004",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
        "type": "counterparty",
        "mediaType": "application/json"
      },
      ...
      "name": "Агент1",
      "code": "УТ0003074",
      "externalCode": "kAgs4Xbhiz2Sp5oP2OCaB2",
      "archived": false,
      "legalTitle": "Общество с ограниченной ответственностью «Агент1»",
      "legalAddress": "107023, г. Москва, Барабанный переулок, дом № 42, строение 2",
      "inn": "7719864242",
      "kpp": "771901001",
      ...
    },
    ...
    "positions": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/f99544d7-4a98-11e6-8a84-bae50000007f/positions",
        "type": "demandposition",
        "mediaType": "application/json",
        "size": 2,
        "limit": 1000,
        "offset": 0
      }
    },
    "vatEnabled": true,
    "vatIncluded": true,
    "payedSum": 0,
    "returns": [
      {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/salesreturn/166909e6-4a99-11e6-8a84-bae500000089",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/salesreturn/metadata",
          "type": "salesreturn",
          "mediaType": "application/json"
        }
      }
    ]
  }
  ...
}
```

### Создание отгрузки с expand 

> Развернем поле **agent** у создаваемой отгрузки.

```shell
curl -X POST
  "https://online.moysklad.ru/api/remap/1.2/entity/demand?expand=agent"
  -H "Authorization: Basic <Credentials>"
  -H 'Content-Type: application/json' \
  -d '{
  "name": "0001",
  "organization": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/850c8195-f504-11e5-8a84-bae50000015e",
      "type": "organization",
      "mediaType": "application/json"
    }
  },
  "agent": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/9794d400-f689-11e5-8a84-bae500000078",
      "type": "counterparty",
      "mediaType": "application/json"
    }
  },
  "store": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/850ee995-f504-11e5-8a84-bae500000160",
      "type": "store",
      "mediaType": "application/json"
    }
  }
}'
```

> В ответ придет созданная отгрузка с развернутым объектом контрагента (**agent**).

```json
{
    "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/1c3f30d2-88b9-11e7-9464-e4de00000000",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
        "type": "demand",
        "mediaType": "application/json",
        "uuidHref": "https://online.moysklad.ru/app/#demand/edit?id=1c3f30d2-88b9-11e7-9464-e4de00000000"
    },
    "id": "1c3f30d2-88b9-11e7-9464-e4de00000000",
    "accountId": "d8a2e973-6703-11e7-9464-e4de00000001",
    "owner": {
        "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/d9335bf2-6703-11e7-9464-e4de0000002a",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
            "type": "employee",
            "mediaType": "application/json",
            "uuidHref": "https://online.moysklad.ru/app/#employee/edit?id=d9335bf2-6703-11e7-9464-e4de0000002a"
        }
    },
    "shared": false,
    "group": {
        "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/group/d8a5d385-6703-11e7-9464-e4de00000002",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/group/metadata",
            "type": "group",
            "mediaType": "application/json"
        }
    },
    "updated": "2017-08-24 13:43:47",
    "name": "0001",
    "externalCode": "UoaXR1oZhS9LOHzdUi42R1",
    "moment": "2017-08-24 13:43:00",
    "applicable": true,
    "rate": {
        "currency": {
            "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/d959dce8-6703-11e7-9464-e4de00000058",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
                "type": "currency",
                "mediaType": "application/json",
                "uuidHref": "https://online.moysklad.ru/app/#currency/edit?id=d959dce8-6703-11e7-9464-e4de00000058"
            }
        }
    },
    "sum": 0,
    "store": {
        "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/d95915ff-6703-11e7-9464-e4de00000053",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
            "type": "store",
            "mediaType": "application/json",
            "uuidHref": "https://online.moysklad.ru/app/#warehouse/edit?id=d95915ff-6703-11e7-9464-e4de00000053"
        }
    },
    "agent": {
        "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/d9593e70-6703-11e7-9464-e4de00000054",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
            "type": "counterparty",
            "mediaType": "application/json",
            "uuidHref": "https://online.moysklad.ru/app/#company/edit?id=d9593e70-6703-11e7-9464-e4de00000054"
        },
        "id": "d9593e70-6703-11e7-9464-e4de00000054",
        "accountId": "d8a2e973-6703-11e7-9464-e4de00000001",
        "owner": {
            "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/d9335bf2-6703-11e7-9464-e4de0000002a",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
                "type": "employee",
                "mediaType": "application/json",
                "uuidHref": "https://online.moysklad.ru/app/#employee/edit?id=d9335bf2-6703-11e7-9464-e4de0000002a"
            }
        },
        "shared": false,
        "group": {
            "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/group/d8a5d385-6703-11e7-9464-e4de00000002",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/group/metadata",
                "type": "group",
                "mediaType": "application/json"
            }
        },
        "updated": "2017-08-18 17:49:23",
        "name": "ООО \"Поставщик\"",
        "externalCode": "YWKWXePEi9jBAmxriBpc93",
        "archived": false,
        "created": "2017-07-12 16:13:08",
        "companyType": "legal",
        "legalTitle": "Общество с ограниченной ответственностью \"Поставщик\"",
        "legalAddress": "г.Москва, ул.Строителей, д.12",
        "inn": "7736570901",
        "kpp": "773601001",
        "accounts": {
            "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/d9593e70-6703-11e7-9464-e4de00000054/accounts",
                "type": "account",
                "mediaType": "application/json",
                "size": 0,
                "limit": 1000,
                "offset": 0
            }
        },
        "tags": [
            "bbbvcc",
            "ss"
        ],
        "contactpersons": {
            "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/d9593e70-6703-11e7-9464-e4de00000054/contactpersons",
                "type": "contactperson",
                "mediaType": "application/json",
                "size": 0,
                "limit": 1000,
                "offset": 0
            }
        },
        "notes": {
            "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/d9593e70-6703-11e7-9464-e4de00000054/notes",
                "type": "note",
                "mediaType": "application/json",
                "size": 0,
                "limit": 1000,
                "offset": 0
            }
        },
        "state": {
            "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata/states/d9efdc3b-6703-11e7-9464-e4de00000066",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
                "type": "state",
                "mediaType": "application/json"
            }
        },
        "salesAmount": 4500
    },
    "organization": {
        "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/d955aa70-6703-11e7-9464-e4de00000051",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
            "type": "organization",
            "mediaType": "application/json",
            "uuidHref": "https://online.moysklad.ru/app/#mycompany/edit?id=d955aa70-6703-11e7-9464-e4de00000051"
        }
    },
    "created": "2017-08-24 13:43:48",
    "positions": {
        "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/1c3f30d2-88b9-11e7-9464-e4de00000000/positions",
            "type": "demandposition",
            "mediaType": "application/json",
            "size": 0,
            "limit": 1000,
            "offset": 0
        }
    },
    "vatEnabled": true,
    "vatIncluded": true,
    "vatSum": 0,
    "payedSum": 0
}
```

### Редактирование отгрузки с expand 

> Теперь обновим эту отгрузку и развернем у нее поля **agent** и **organization**.
В ответ придет измененная отгрузка с развернутым объектом контрагента (**agent**) и развернутым объектом юрлица (**organization**).

```shell
curl -X PUT
  "https://online.moysklad.ru/api/remap/1.2/entity/demand/1c3f30d2-88b9-11e7-9464-e4de00000000?expand=agent,organization"
  -H "Authorization: Basic <Credentials>"
  -H 'Content-Type: application/json' \
  -d '{
  "name": "3738"
}`
```

> Response 200 (application/json)

```json
{
    "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/1c3f30d2-88b9-11e7-9464-e4de00000000?expand=agent,organization",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
        "type": "demand",
        "mediaType": "application/json",
        "uuidHref": "https://online.moysklad.ru/app/#demand/edit?id=1c3f30d2-88b9-11e7-9464-e4de00000000"
    },
    "id": "1c3f30d2-88b9-11e7-9464-e4de00000000",
    "accountId": "d8a2e973-6703-11e7-9464-e4de00000001",
    "owner": {
        "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/d9335bf2-6703-11e7-9464-e4de0000002a",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
            "type": "employee",
            "mediaType": "application/json",
            "uuidHref": "https://online.moysklad.ru/app/#employee/edit?id=d9335bf2-6703-11e7-9464-e4de0000002a"
        }
    },
    "shared": false,
    "group": {
        "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/group/d8a5d385-6703-11e7-9464-e4de00000002",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/group/metadata",
            "type": "group",
            "mediaType": "application/json"
        }
    },
    "updated": "2017-08-24 13:53:07",
    "name": "3738",
    "externalCode": "UoaXR1oZhS9LOHzdUi42R1",
    "moment": "2017-08-24 13:43:00",
    "applicable": true,
    "rate": {
        "currency": {
            "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/d959dce8-6703-11e7-9464-e4de00000058",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
                "type": "currency",
                "mediaType": "application/json",
                "uuidHref": "https://online.moysklad.ru/app/#currency/edit?id=d959dce8-6703-11e7-9464-e4de00000058"
            }
        }
    },
    "sum": 0,
    "store": {
        "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/d95915ff-6703-11e7-9464-e4de00000053",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
            "type": "store",
            "mediaType": "application/json",
            "uuidHref": "https://online.moysklad.ru/app/#warehouse/edit?id=d95915ff-6703-11e7-9464-e4de00000053"
        }
    },
    "agent": {
        "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/d9593e70-6703-11e7-9464-e4de00000054",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
            "type": "counterparty",
            "mediaType": "application/json",
            "uuidHref": "https://online.moysklad.ru/app/#company/edit?id=d9593e70-6703-11e7-9464-e4de00000054"
        },
        "id": "d9593e70-6703-11e7-9464-e4de00000054",
        "accountId": "d8a2e973-6703-11e7-9464-e4de00000001",
        "owner": {
            "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/d9335bf2-6703-11e7-9464-e4de0000002a",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
                "type": "employee",
                "mediaType": "application/json",
                "uuidHref": "https://online.moysklad.ru/app/#employee/edit?id=d9335bf2-6703-11e7-9464-e4de0000002a"
            }
        },
        "shared": false,
        "group": {
            "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/group/d8a5d385-6703-11e7-9464-e4de00000002",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/group/metadata",
                "type": "group",
                "mediaType": "application/json"
            }
        },
        "updated": "2017-08-18 17:49:23",
        "name": "ООО \"Поставщик\"",
        "externalCode": "YWKWXePEi9jBAmxriBpc93",
        "archived": false,
        "created": "2017-07-12 16:13:08",
        "companyType": "legal",
        "legalTitle": "Общество с ограниченной ответственностью \"Поставщик\"",
        "legalAddress": "г.Москва, ул.Строителей, д.12",
        "inn": "7736570901",
        "kpp": "773601001",
        "accounts": {
            "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/d9593e70-6703-11e7-9464-e4de00000054/accounts",
                "type": "account",
                "mediaType": "application/json",
                "size": 0,
                "limit": 1000,
                "offset": 0
            }
        },
        "tags": [
            "bbbvcc",
            "ss"
        ],
        "contactpersons": {
            "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/d9593e70-6703-11e7-9464-e4de00000054/contactpersons",
                "type": "contactperson",
                "mediaType": "application/json",
                "size": 0,
                "limit": 1000,
                "offset": 0
            }
        },
        "notes": {
            "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/d9593e70-6703-11e7-9464-e4de00000054/notes",
                "type": "note",
                "mediaType": "application/json",
                "size": 0,
                "limit": 1000,
                "offset": 0
            }
        },
        "state": {
            "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata/states/d9efdc3b-6703-11e7-9464-e4de00000066",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
                "type": "state",
                "mediaType": "application/json"
            }
        },
        "salesAmount": 4500
    },
    "organization": {
        "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/d955aa70-6703-11e7-9464-e4de00000051",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
            "type": "organization",
            "mediaType": "application/json",
            "uuidHref": "https://online.moysklad.ru/app/#mycompany/edit?id=d955aa70-6703-11e7-9464-e4de00000051"
        },
        "id": "d955aa70-6703-11e7-9464-e4de00000051",
        "accountId": "d8a2e973-6703-11e7-9464-e4de00000001",
        "owner": {
            "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/d9335bf2-6703-11e7-9464-e4de0000002a",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
                "type": "employee",
                "mediaType": "application/json",
                "uuidHref": "https://online.moysklad.ru/app/#employee/edit?id=d9335bf2-6703-11e7-9464-e4de0000002a"
            }
        },
        "shared": true,
        "group": {
            "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/group/d8a5d385-6703-11e7-9464-e4de00000002",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/group/metadata",
                "type": "group",
                "mediaType": "application/json"
            }
        },
        "updated": "2017-07-12 16:13:09",
        "name": "reqwy",
        "externalCode": "PRLKDfmQgwj7TGtiYWrrZ3",
        "archived": false,
        "created": "2017-07-12 16:13:08",
        "companyType": "legal",
        "legalTitle": "reqwy",
        "email": "erqw@ss.ru",
        "accounts": {
            "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/d955aa70-6703-11e7-9464-e4de00000051/accounts",
                "type": "account",
                "mediaType": "application/json",
                "size": 0,
                "limit": 1000,
                "offset": 0
            }
        },
        "isEgaisEnable": false,
        "payerVat": true,
        "director": "Администратор",
        "chiefAccountant": "Администратор"
    },
    "created": "2017-08-24 13:43:48",
    "positions": {
        "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/1c3f30d2-88b9-11e7-9464-e4de00000000/positions",
            "type": "demandposition",
            "mediaType": "application/json",
            "size": 0,
            "limit": 1000,
            "offset": 0
        }
    },
    "vatEnabled": true,
    "vatIncluded": true,
    "vatSum": 0,
    "payedSum": 0
}
```

### Серверные приложения
Для доступа к API может быть использован токен выданный Вендору при установке Серверного приложения пользователем МоегоСклада.

#### Получение контекста приложения
Возвращает параметры приложения, в рамках которого присходит запрос (по аналогии с контекстом Сотрудника).

> Пример запроса на получение контекста приложения

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/context/application"
  -H "Authorization: Bearer <Access-Token>"
``` 

> Response 200 (application/json) Успешный запрос. Результат JSON объект, содержащий данные приложения

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/application/b58a6312-f958-11e9-ac12-000a00000020",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/application/metadata",
    "type": "application",
    "mediaType": "application/json"
  },
  "appUid": "test.moysklad@reqwy1",
  "id": "b58a6312-f958-11e9-ac12-000a00000020"
}
```

#### Получение сущности установленного приложения
Возвращает параметры установленного приложения по id установленного на аккаунте приложения. 

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: b58a6312-f958-11e9-ac12-000a00000020* id установленного на аккаунте приложения|

> Пример запроса на получение сущности установленного приложения

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/application/b58a6312-f958-11e9-ac12-000a00000020"
  -H "Authorization: Bearer <Access-Token>"
``` 

> Response 200 (application/json) Успешный запрос. Результат JSON объект, содержащий данные приложения

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/application/b58a6312-f958-11e9-ac12-000a00000020",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/application/metadata",
    "type": "application",
    "mediaType": "application/json"
  },
  "appUid": "test.moysklad@reqwy1",
  "id": "b58a6312-f958-11e9-ac12-000a00000020"
}
```

#### Фильтрация выборки с помощью параметра filter=updatedBy
Для фильтрации выборок сущностей по приложению укажите _uid_ изменившего их приложения.

Uid приложения должен быть указан в виде:
`<Application-Alias>.<Vendor-Alias>@<Account-Name>` 

Пример запроса на получение списка входящих платежей:
`https://online.moysklad.ru/api/remap/1.2/entity/paymentin?filter=updatedBy=test.moysklad@reqwy1` 

#### Фильтрация записей аудита с помощью параметра filter=uid
Для фильтрации аудита по приложению укажите _uid_ приложения, которое изменяло сущности.

Uid приложения должен быть указан в виде:
`<Application-Alias>.<Vendor-Alias>@<Account-Name>` 

Пример запроса на получение списка записей:
`https://online.moysklad.ru/api/remap/1.2/audit?filter=uid=test.moysklad@reqwy1` 

#### Фильтрация записей аудита с помощью параметра filter=application
Для фильтрации аудита по приложению укажите _href_ приложения, которое изменяло сущности.

Href приложения должен быть указан в виде:
`https://online.moysklad.ru/api/remap/1.2/entity/application/{id}`, 
где _id_ - UUID установленного на аккаунте приложения

Пример запроса на получение списка записей:
`https://online.moysklad.ru/api/remap/1.2/audit?filter=application=https://online.moysklad.ru/api/remap/1.2/entity/application/46ea8005-2965-11e9-9ff4-34e80009ac49` 

### Устаревшие версии JSON API 
Версия [API REMAP 1.1](https://dev.moysklad.ru/doc/api/remap/1.1/) устарела. Поддерживается и работает, но не развивается и не дополняется новыми возможностями.
