## Отгрузка
Средствами JSON API можно создавать и обновлять сведения об Отгрузках, запрашивать списки Отгрузок и сведения по отдельным Отгрузкам. Позициями Отгрузок можно управлять как в составе отдельной Отгрузки, так и отдельно - с помощью специальных ресурсов для управления позициями Отгрузки. Кодом сущности для Отгрузки в составе JSON API является ключевое слово **demand**. Больше об Отгрузках и работе с ними в основном интерфейсе вы можете прочитать в нашей службе поддержки по  [этой ссылке](https://support.moysklad.ru/hc/ru/articles/203325463-%D0%9E%D1%82%D0%B3%D1%80%D1%83%D0%B7%D0%BA%D0%B0-%D1%82%D0%BE%D0%B2%D0%B0%D1%80%D0%BE%D0%B2).
### Отгрузки 
#### Атрибуты сущности

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные Отгрузки|&mdash;|да
|**id**                 |UUID|ID Отгрузки|Только для чтения|да
|**accountId**          |UUID| ID учетной записи|Только для чтения|да
|**syncId**             |UUID|ID синхронизации. После заполнения недоступен для изменения|&mdash;|нет
|**updated**            |DateTime|Момент последнего обновления Отгрузки|Только для чтения|да
|**deleted**            |DateTime|Момент последнего удаления Отгрузки|Только для чтения|нет
|**name**               |String(255)|Наименование Отгрузки|&mdash;|да
|**description**        |String(4096)|Комментарий Отгрузки|&mdash;|нет
|**externalCode**       |String(255)|Внешний код Отгрузки|&mdash;| да
|**moment**             |DateTime|Дата Счета|&mdash;|да
|**applicable**         |Boolean|Отметка о проведении|&mdash;|да
|**vatEnabled**         |Boolean|Учитывается ли НДС|&mdash;|да
|**vatIncluded**        |Boolean| Включен ли НДС в цену|&mdash;|нет
|**sum**                |Int|Сумма Отгрузки в копейках|Только для чтения|да
|**project**            |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные проекта|&mdash;|нет
|**rate**               |Object|Валюта. [Подробнее тут](../documents/#dokumenty-obschie-swedeniq-valuta-w-dokumentah)|&mdash;|да
|**owner**              |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Владелец (Сотрудник)|&mdash;|да
|**shared**             |Boolean|Общий доступ|&mdash;|да
|**group**              |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Отдел сотрудника|&mdash;|да
|**organization**       |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные юрлица|Необходимое при создании|да
|**agent**              |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные контрагента|Необходимое при создании|да
|**store**              |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные склада|Необходимое при создании|да
|**contract**              |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные договора|&mdash;|нет
|**state**              |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные статуса Отгрузки|&mdash;|нет
|**organizationAccount**|[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные счета юрлица|&mdash;|нет
|**agentAccount**       |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные счета контрагента|&mdash;|нет
|**attributes**         |Array(Object)|Коллекция метаданных доп. полей. [Поля объекта](../#mojsklad-json-api-obschie-swedeniq-rabota-s-dopolnitel-nymi-polqmi) |&mdash;|нет
|**files**              |MetaArray|Массив метаданных [Файлов](../dictionaries/#suschnosti-fajly) (Максимальное количество файлов - 100)|&mdash;|да
|**created**            |DateTime|Дата создания|Только для чтения|да
|**printed**            |Boolean|Напечатан ли документ|Только для чтения|да
|**published**          |Boolean|Опубликован ли документ|Только для чтения|да
|**vatSum**                |Float|Сумма включая НДС|&mdash;|да
|**positions**          |MetaArray|Метаданные позиций Отгрузки|&mdash;|да
|**overhead**           |Object|Накладные расходы. [Подробнее тут](../dictionaries/#dokumenty-otgruzka-otgruzki-nakladnye-rashody). Если Позиции Отгрузки не заданы, то накладные расходы нельзя задать|&mdash;|нет
|**payedSum**            |Float|Сумма входящих платежей по Отгрузке |Только для чтения|да

#### Накладные расходы
Описание полей overhead

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**sum**                |Int|Сумма Оприходования в копейках|&mdash;|да
|**distribution**                |Enum|Распределение накладных расходов `[weight, volume, price]` -> `[по весу, по объему, по цене]`|&mdash;|да

#### Связи с другими документами
|Название          | Описание  |
| ------------------------------ |:---------------------------|
|**customerOrder** | Ссылка на Заказ Покупателя, с которым связана эта Отгрузка в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye)
| **factureOut** | Ссылка на Счет-фактуру выданный, с которым связана эта Отгрузка в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye)
| **returns** | Массив ссылок на связанные возвраты в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye)
| **payments** |Массив ссылок на связанные платежи в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye)
| **invoicesOut** | Массив ссылок на связанные счета покупателям в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye)

####  Другие поля 
| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**consignee**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные грузополучателя (контрагент или юрлицо)|&mdash;|нет
|**transportFacilityNumber**              |String(255)|Номер автомобиля|&mdash;|нет
|**shippingInstructions**               |String(255)|Указания грузоотправителя|&mdash;|нет
|**cargoName**              |String(255)|Наименование груза|&mdash;|нет
|**transportFacility**               |String(255)|Транспортное средство|&mdash;|нет
|**goodPackQuantity**               |String(255)|Всего мест|&mdash;|нет
|**carrier**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные перевозчика (контрагент или юрлицо)|&mdash;|нет
|**stateContractId**              |String(255)|Идентификатор государственного контракта, договора (соглашения)|&mdash;|нет

#### Позиции Отгрузки
Позиции Отгрузки - это список товаров/услуг/модификаций/серий.
Объект позиции Отгрузки содержит следующие поля:

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**id**                 |UUID|ID позиции|Только для чтения|да
|**accountId**          |UUID| ID учетной записи|Только для чтения|да
|**quantity**          |Int|Количество товаров/услуг данного вида в позиции. Если позиция - товар, у которого включен учет по серийным номерам, то значение в этом поле всегда будет равно количеству серийных номеров для данной позиции в документе.|&mdash;|да
|**price**          |Float|Цена товара/услуги в копейках|&mdash;|да
|**discount**          |Int|Процент скидки или наценки. Наценка указывается отрицательным числом, т.е. -10 создаст наценку в 10%|&mdash;|да
|**vat**        |Int|НДС, которым облагается текущая позиция|&mdash;|да
|**vatEnabled**     |Boolean|Включен ли НДС для позиции. С помощью этого флага для позиции можно выставлять НДС = 0 или НДС = "без НДС". (vat = 0, vatEnabled = false) -> vat = "без НДС", (vat = 0, vatEnabled = true) -> vat = 0%.|&mdash;|да
|**assortment**              |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные товара/услуги/серии/модификации, которую представляет собой позиция|&mdash;|да
|**pack**            |String(255)|Упаковка товара|&mdash;|нет
|**things**            |Array(String)|Серийные номера. Значение данного атрибута игнорируется, если товар позиции не находится на серийном учете. В ином случае количество товаров в позиции будет равно количеству серийных номеров, переданных в значении атрибута.|&mdash;|нет
|**trackingCodes**          |Array(Object)|Коды маркировки товаров и транспортных упаковок. [Подробнее тут](../documents/#dokumenty-otgruzka-otgruzki-kody-markirowki-towarow-i-transportnyh-upakowok)|&mdash;|нет
|**cost**          |Int|Себестоимость (только для услуг)|&mdash;|нет

С позициями можно работать с помощью [специальных ресурсов для управления позициями Отгрузки](../documents/#dokumenty-otgruzka-pozicii-otgruzki),
а также в составе отдельной Отгрузки. При работе в составе отдельной Отгрузки,
вы можете отправлять запросы на создание отдельной Отгрузки с включенным в тело запроса
массивом позиций Отгрузки. Если количество позиций превышает максимально допустимое, то для
дальнейшего пополнения позиций нужно будет работать со специальным ресурсом "Позиции Отгрузки".
Также, при работе в составе отдельной Отгрузки, можно отправлять запросы на обновление списка позиций
с включенным в тело запроса массивом позиций Отгрузки. При этом важно помнить, что коллекция позиций будет
восприниматься как "все позиции Отгрузки" и полностью заменит уже существующую коллекцию при обновлении объекта - лишние
позиции будут удалены, новые добавлены, существующие - изменены.

О работе с доп. полями Отгрузок можно прочитать [здесь](../#mojsklad-json-api-obschie-swedeniq-rabota-s-dopolnitel-nymi-polqmi)

#### Коды маркировки товаров и транспортных упаковок
Поддержаны в виде иерархической структуры JSON. 

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**cis**           |String|Значение кода маркировки|Необходимое при создании|да
|**type**          |Enum|Тип кода маркировки. Возможные значения: `trackingcode`, `consumerpack`, `transportpack`|Необходимое при создании|да
|**trackingCodes** |Array(Object)|Массив вложенных кодов маркировки. Может присутствовать, только если **type** имеет значения `consumerpack` или `transportpack`|&mdash;|нет

Значение кода указывается в атрибуте **cis**. 
Для каждого кода указывается тип **type**: `trackingcode` (код маркировки товара), `consumerpack` (код маркировки потребительской упаковки) или `transportpack` (код транспортной упаковки). 
Допустима вложенность кодов маркировки товаров в транспортные упаковки. Транспортные упаковки не могут иметь вложенных упаковок. 
Коды упаковок могут отсутствовать - в этом случае структура не будет вложенной. 
Если продукция не является маркированной, то коды маркировки для позиции не будут сохранены. 
Количество кодов маркировки может отличаться от фактического количества единиц продукции.

#### Особенности работы с кодами маркировки и серийными номерами для позиции документа

При работе с позицией Отгрузки следует учитывать следующие особенности.

+ Количество кодов маркировки **trackingCodes** в позиции документа не влияет на количество единиц **quantity** в позиции.
+ Количество серийных номеров **things** в позиции документа строго соответствует количеству единиц **quantity** в позиции. 
  Изменение **quantity** на значение, не соответствующее количеству серийных номеров, недопустимо. 
+ Для обновления списка кодов маркировки **trackingCodes** и списка серийных номеров **things** позиции Отгрузки, 
  необходимо передавать их полный список, включающий как старые, так и новые значения. Отсутствующие значения при обновлении будут удалены.
  
Недопустимо сохранение дублирующихся кодов маркировки и серийных номеров внутри документа Отгрузки. 


### Получить список Отгрузок 
Запрос всех Отгрузок на данной учетной записи.
Результат: Объект JSON, включающий в себя поля:

| Название  | Тип | Описание                    |
| --------- |:----|:----------------------------|
**meta** |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные о выдаче,
**context** | [Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye) | Метаданные о сотруднике, выполнившем запрос.
**rows** |Array(Object)|Массив JSON объектов, представляющих собой Отгрузки.

**Параметры**

| Параметр                | Описание  |
| ------------------------------ |:---------------------------|
|**limit** |  `number` (optional) **Default: 1000** *Example: 1000* Максимальное количество сущностей для извлечения.`Допустимые значения 1 - 1000`.|
|**offset** |  `number` (optional) **Default: 0** *Example: 40* Отступ в выдаваемом списке сущностей.|
|**search** |  `string` (optional) *Example: 0001* Фильтр документов по указанной поисковой строке.|

> Получить список Отгрузок

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/demand"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление списка Отгрузок.

```json
{
  "context": {
    "employee": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/context/employee",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
        "type": "employee",
        "mediaType": "application/json"
      }
    }
  },
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/?limit=2",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
    "type": "demand",
    "mediaType": "application/json",
    "size": 13,
    "limit": 2,
    "offset": 0
  },
  "rows": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/0ee24723-f640-11e5-8a84-bae500000065",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
        "type": "demand",
        "mediaType": "application/json"
      },
      "id": "0ee24723-f640-11e5-8a84-bae500000065",
      "accountId": "84e60e93-f504-11e5-8a84-bae500000008",
      "syncId": "734a9e26-45a2-4ead-849c-e144daeb854d",
      "updated": "2016-03-30 09:24:29",
      "name": "00001",
      "externalCode": "1SB6iRE9imMFJDMlab7Nk0",
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
      "moment": "2016-03-30 09:24:00",
      "applicable": true,
      "vatEnabled": true,
      "vatIncluded": true,
      "printed": true,
      "published": true,
      "sum": 123000,
      "rate": {
        "currency": {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/baac25f0-50ac-11e5-300d-c79b00000055",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
            "type": "currency",
            "mediaType": "application/json"
          }
        }
      },
      "organization": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/850c8195-f504-11e5-8a84-bae50000015e",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
          "type": "organization",
          "mediaType": "application/json"
        }
      },
      "store": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/850ee995-f504-11e5-8a84-bae500000160",
          "type": "store",
          "mediaType": "application/json"
        }
      },
      "agent": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/850efc5f-f504-11e5-8a84-bae500000161",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
          "type": "counterparty",
          "mediaType": "application/json"
        }
      },
      "organizationAccount": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/850c8195-f504-11e5-8a84-bae50000015e/accounts/850c8af2-f504-11e5-8a84-bae50000015f",
          "type": "account",
          "mediaType": "application/json"
        }
      },
      "agentAccount": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/850efc5f-f504-11e5-8a84-bae500000161/accounts/850f0617-f504-11e5-8a84-bae500000162",
          "type": "account",
          "mediaType": "application/json"
        }
      },
      "positions": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/0ee24723-f640-11e5-8a84-bae500000065/positions",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
          "type": "demandposition",
          "mediaType": "application/json",
          "size": 1,
          "limit": 1000,
          "offset": 0
        }
      },
      "payedSum": 0,
      "consignee": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/869d7628-6396-11e6-8a84-bae50000000a",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
          "type": "counterparty",
          "mediaType": "application/json"
        }
      },
      "transportFacilityNumber": "лb777m",
      "shippingInstructions": "Беречь от воздействия солнца",
      "cargoName": "Овощи",
      "transportFacility": "Mercedes benz",
      "carrier": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/cffd2c81-62b4-11e6-8a84-bae500000053",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
          "type": "counterparty",
          "mediaType": "application/json"
        }
      },
      "overhead": {
        "sum": 200,
        "distribution": "price"
      }
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/b44f220c-f64e-11e5-8a84-bae500000068",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
        "type": "demand",
        "mediaType": "application/json"
      },
      "id": "b44f220c-f64e-11e5-8a84-bae500000068",
      "accountId": "84e60e93-f504-11e5-8a84-bae500000008",
      "syncId": "734a9e26-45a2-4ead-849c-e144daeb854d",
      "updated": "2016-04-01 10:37:29",
      "name": "00002",
      "externalCode": "btlob8zrgFoJoxXLNyxBi3",
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
      "moment": "2016-03-30 11:08:00",
      "applicable": false,
      "vatEnabled": true,
      "vatIncluded": true,
      "printed": true,
      "published": true,
      "sum": 123000,
      "rate": {
        "currency": {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/baac25f0-50ac-11e5-300d-c79b00000055",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
            "type": "currency",
            "mediaType": "application/json"
          }
        }
      },
      "organization": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/850c8195-f504-11e5-8a84-bae50000015e",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
          "type": "organization",
          "mediaType": "application/json"
        }
      },
      "store": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/850ee995-f504-11e5-8a84-bae500000160",
          "type": "store",
          "mediaType": "application/json"
        }
      },
      "agent": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/850f1667-f504-11e5-8a84-bae500000163",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
          "type": "counterparty",
          "mediaType": "application/json"
        }
      },
      "organizationAccount": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/850c8195-f504-11e5-8a84-bae50000015e/accounts/850c8af2-f504-11e5-8a84-bae50000015f",
          "type": "account",
          "mediaType": "application/json"
        }
      },
      "agentAccount": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/850f1667-f504-11e5-8a84-bae500000163/accounts/850f1eab-f504-11e5-8a84-bae500000164",
          "type": "account",
          "mediaType": "application/json"
        }
      },
      "positions": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/b44f220c-f64e-11e5-8a84-bae500000068/positions",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
          "type": "demandposition",
          "mediaType": "application/json",
          "size": 3,
          "limit": 1000,
          "offset": 0
        }
      },
      "payedSum": 0,
      "overhead": {
        "sum": 300,
        "distribution": "weight"
      }
    }
  ]
}
```

### Создать Отгрузку
Запрос на создание новой Отгрузки.
Обязательные для создания поля:

| Параметр                | Описание  |
| ------------------------------ |:---------------------------|
| **name** | номер Отгрузки
| **organization** | Ссылка на ваше юрлицо в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye)
| **agent** | Ссылка на контрагента в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye)
| **store** | Ссылка на склад в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye)

> Пример создания новой Отгрузки с телом запроса, содержащим только необходимые поля.

```shell
  curl -X POST
    "https://online.moysklad.ru/api/remap/1.2/entity/demand"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "name": "888",
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
          }
'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление созданной Отгрузки.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/2464c97a-030a-11e6-9464-e4de00000000",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
    "type": "demand",
    "mediaType": "application/json"
  },
  "id": "2464c97a-030a-11e6-9464-e4de00000000",
  "accountId": "84e60e93-f504-11e5-8a84-bae500000008",
  "syncId": "734a9e26-45a2-4ead-849c-e144daeb854d",
  "updated": "2016-04-15 16:01:17",
  "name": "888",
  "externalCode": "Dt7BqCkBhCxUMXayh4NfA2",
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
  "moment": "2016-04-15 16:01:17",
  "applicable": true,
  "vatEnabled": true,
  "vatIncluded": true,
  "sum": 0,
  "rate": {
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/baac25f0-50ac-11e5-300d-c79b00000055",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json"
      }
    }
  },
  "organization": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/850c8195-f504-11e5-8a84-bae50000015e",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
      "type": "organization",
      "mediaType": "application/json"
    }
  },
  "store": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/850ee995-f504-11e5-8a84-bae500000160",
      "type": "store",
      "mediaType": "application/json"
    }
  },
  "agent": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/9794d400-f689-11e5-8a84-bae500000078",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
      "mediaType": "application/json"
    }
  },
  "organizationAccount": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/850c8195-f504-11e5-8a84-bae50000015e/accounts/3a30e844-016f-11e6-9464-e4de00000068",
      "type": "account",
      "mediaType": "application/json"
    }
  },
  "agentAccount": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/9794d400-f689-11e5-8a84-bae500000078/accounts/9794f7a0-f689-11e5-8a84-bae500000079",
      "type": "account",
      "mediaType": "application/json"
    }
  },
  "created": "2016-08-25 19:55:00",
  "printed": true,
  "published": true,
  "positions": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/2464c97a-030a-11e6-9464-e4de00000000/positions",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
      "type": "demandposition",
      "mediaType": "application/json",
      "size": 0,
      "limit": 1000,
      "offset": 0
    }
  },
  "payedSum": 0
}
```

> Пример создания новой Отгрузки с более насыщенным телом запроса.

```shell
  curl -X POST
    "https://online.moysklad.ru/api/remap/1.2/entity/demand"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "name": "888",
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
            },
            "code": "1243521",
            "moment": "2016-04-19 13:50:24",
            "applicable": false,
            "vatEnabled": true,
            "vatIncluded": true,
            "customerOrder": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/customerorder/c49e83b3-01af-11e6-9464-e4de00000026",
                "type": "customerorder",
                "mediaType": "application/json"
              }
            },
            "consignee": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/869d7628-6396-11e6-8a84-bae50000000a",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
                "type": "counterparty",
                "mediaType": "application/json"
              }
            },
            "transportFacilityNumber": "МК2142",
            "shippingInstructions": "Огнеопасно",
            "cargoName": "масло",
            "transportFacility": "Камаз 2007",
            "carrier": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/cffd2c81-62b4-11e6-8a84-bae500000053",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
                "type": "counterparty",
                "mediaType": "application/json"
              }
            },
            "stateContractId": "s11233dsasd233"
          }
'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление созданной Отгрузки.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/c2a04da5-030a-11e6-9464-e4de00000005",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
    "type": "demand",
    "mediaType": "application/json"
  },
  "id": "c2a04da5-030a-11e6-9464-e4de00000005",
  "accountId": "84e60e93-f504-11e5-8a84-bae500000008",
  "syncId": "734a9e26-45a2-4ead-849c-e144daeb854d",
  "updated": "2016-04-15 16:05:43",
  "name": "888",
  "code": "1243521",
  "externalCode": "p7TPtR1hgOBjUev7rJLmo1",
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
  "moment": "2016-04-19 13:50:24",
  "applicable": false,
  "vatEnabled": true,
  "vatIncluded": true,
  "sum": 0,
  "rate": {
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/baac25f0-50ac-11e5-300d-c79b00000055",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json"
      }
    }
  },
  "organization": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/850c8195-f504-11e5-8a84-bae50000015e",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
      "type": "organization",
      "mediaType": "application/json"
    }
  },
  "store": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/850ee995-f504-11e5-8a84-bae500000160",
      "type": "store",
      "mediaType": "application/json"
    }
  },
  "agent": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/9794d400-f689-11e5-8a84-bae500000078",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
      "mediaType": "application/json"
    }
  },
  "organizationAccount": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/850c8195-f504-11e5-8a84-bae50000015e/accounts/3a30e844-016f-11e6-9464-e4de00000068",
      "type": "account",
      "mediaType": "application/json"
    }
  },
  "agentAccount": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/9794d400-f689-11e5-8a84-bae500000078/accounts/9794f7a0-f689-11e5-8a84-bae500000079",
      "type": "account",
      "mediaType": "application/json"
    }
  },
  "created": "2016-08-25 19:55:00",
  "printed": true,
  "published": true,
  "positions": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/c2a04da5-030a-11e6-9464-e4de00000005/positions",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
      "type": "demandposition",
      "mediaType": "application/json",
      "size": 0,
      "limit": 1000,
      "offset": 0
    }
  },
  "payedSum": 0,
  "stateContractId": "s11233dsasd233"
}
```

> Пример запроса на создание Отгрузки с доп. полями.

```shell
  curl -X POST
    "https://online.moysklad.ru/api/remap/1.2/entity/demand"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "name": "888",
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
            },
            "code": "1243521",
            "moment": "2016-04-19 13:50:24",
            "applicable": false,
            "vatEnabled": true,
            "vatIncluded": true,
            "customerOrder": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/customerorder/c49e83b3-01af-11e6-9464-e4de00000026",
                "type": "customerorder",
                "mediaType": "application/json"
              }
            },
            "attributes": [
              {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/attributes/0cd74e1e-2e59-11e6-8a84-bae50000008a",
                  "type": "attributemetadata",
                  "mediaType": "application/json"
                },
                "value": "AttributeValue1"
              }
            ]
          }'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление созданной Отгрузки.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/c2a04da5-030a-11e6-9464-e4de00000005",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
    "type": "demand",
    "mediaType": "application/json"
  },
  "id": "c2a04da5-030a-11e6-9464-e4de00000005",
  "accountId": "84e60e93-f504-11e5-8a84-bae500000008",
  "syncId": "734a9e26-45a2-4ead-849c-e144daeb854d",
  "updated": "2016-04-15 16:05:43",
  "name": "888",
  "code": "1243521",
  "externalCode": "p7TPtR1hgOBjUev7rJLmo1",
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
  "moment": "2016-04-19 13:50:24",
  "applicable": false,
  "vatEnabled": true,
  "vatIncluded": true,
  "sum": 0,
  "rate": {
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/baac25f0-50ac-11e5-300d-c79b00000055",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json"
      }
    }
  },
  "organization": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/850c8195-f504-11e5-8a84-bae50000015e",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
      "type": "organization",
      "mediaType": "application/json"
    }
  },
  "store": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/850ee995-f504-11e5-8a84-bae500000160",
      "type": "store",
      "mediaType": "application/json"
    }
  },
  "agent": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/9794d400-f689-11e5-8a84-bae500000078",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
      "mediaType": "application/json"
    }
  },
  "organizationAccount": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/850c8195-f504-11e5-8a84-bae50000015e/accounts/3a30e844-016f-11e6-9464-e4de00000068",
      "type": "account",
      "mediaType": "application/json"
    }
  },
  "agentAccount": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/9794d400-f689-11e5-8a84-bae500000078/accounts/9794f7a0-f689-11e5-8a84-bae500000079",
      "type": "account",
      "mediaType": "application/json"
    }
  },
  "attributes": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/attributes/0cd74e1e-2e59-11e6-8a84-bae50000008a",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "23d3965d-0313-11e6-9464-e4de00000097",
      "name": "AttributeName1",
      "type": "string",
      "value": "AttributeValue1"
    }
  ],
  "created": "2016-08-25 19:55:00",
  "printed": true,
  "published": true,
  "positions": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/c2a04da5-030a-11e6-9464-e4de00000005/positions",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
      "type": "demandposition",
      "mediaType": "application/json",
      "size": 0,
      "limit": 1000,
      "offset": 0
    }
  },
  "payedSum": 0
}
```

> Пример запроса на создание Отгрузки с позициями в теле запроса.

```shell
  curl -X POST
    "https://online.moysklad.ru/api/remap/1.2/entity/demand"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "name": "888",
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
            },
            "code": "1243521",
            "moment": "2016-04-19 13:50:24",
            "applicable": false,
            "vatEnabled": true,
            "vatIncluded": true,
            "positions": [
              {
                "quantity": 10,
                "price": 100,
                "discount": 0,
                "vat": 0,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/8b382799-f7d2-11e5-8a84-bae5000003a5",
                    "type": "product",
                    "mediaType": "application/json"
                  }
                },
               "trackingCodes": [
                {
                  "cis": "012345678912345672",
                  "type": "transportpack",
                    "trackingCodes": [
                     {
                      "cis": "010463003759026521uHpIIf2111114",
                      "type": "trackingcode"
                      },
                      {
                       "cis": "010463003759026521uHpIIf2111111",
                       "type": "trackingcode"
                      }
                    ]
                  }
                ],
                "reserve": 10,
                "overhead": 20
              },
              {
                "quantity": 20,
                "price": 200,
                "discount": 0,
                "vat": 21,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/be903062-f504-11e5-8a84-bae50000019a",
                    "type": "product",
                    "mediaType": "application/json"
                  }
                },
                "reserve": 20,
                "overhead": 20
              },
              {
                "quantity": 30,
                "price": 300,
                "discount": 0,
                "vat": 7,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/service/c02e3a5c-007e-11e6-9464-e4de00000006",
                    "type": "service",
                    "mediaType": "application/json"
                  }
                },
                "pack": {
                  "id": "1bf22e62-8b47-11e8-56c0-000800000006"
                },
                "reserve": 30,
                "overhead": 20,
                "cost": 47
              }
            ]
          }'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление созданной Отгрузки.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/c2a04da5-030a-11e6-9464-e4de00000005",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
    "type": "demand",
    "mediaType": "application/json"
  },
  "id": "c2a04da5-030a-11e6-9464-e4de00000005",
  "accountId": "84e60e93-f504-11e5-8a84-bae500000008",
  "syncId": "734a9e26-45a2-4ead-849c-e144daeb854d",
  "updated": "2016-04-15 16:05:43",
  "name": "888",
  "code": "1243521",
  "externalCode": "p7TPtR1hgOBjUev7rJLmo1",
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
  "moment": "2016-04-19 13:50:24",
  "applicable": false,
  "vatEnabled": true,
  "vatIncluded": true,
  "sum": 0,
  "rate": {
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/baac25f0-50ac-11e5-300d-c79b00000055",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json"
      }
    }
  },
  "organization": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/850c8195-f504-11e5-8a84-bae50000015e",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
      "type": "organization",
      "mediaType": "application/json"
    }
  },
  "store": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/850ee995-f504-11e5-8a84-bae500000160",
      "type": "store",
      "mediaType": "application/json"
    }
  },
  "agent": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/9794d400-f689-11e5-8a84-bae500000078",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
      "mediaType": "application/json"
    }
  },
  "organizationAccount": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/850c8195-f504-11e5-8a84-bae50000015e/accounts/3a30e844-016f-11e6-9464-e4de00000068",
      "type": "account",
      "mediaType": "application/json"
    }
  },
  "agentAccount": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/9794d400-f689-11e5-8a84-bae500000078/accounts/9794f7a0-f689-11e5-8a84-bae500000079",
      "type": "account",
      "mediaType": "application/json"
    }
  },
  "created": "2016-08-25 19:55:00",
  "printed": true,
  "published": true,
  "positions": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/c2a04da5-030a-11e6-9464-e4de00000005/positions",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
      "type": "demandposition",
      "mediaType": "application/json",
      "size": 3,
      "limit": 1000,
      "offset": 0
    }
  },
  "payedSum": 0,
  "overhead": {
    "sum": 60,
    "distribution": "price"
  }
}
```

### Массовое создание и обновление Отгрузок 
[Массовое создание и обновление](../#mojsklad-json-api-obschie-swedeniq-sozdanie-i-obnowlenie-neskol-kih-ob-ektow) Отгрузок.
В теле запроса нужно передать массив, содержащий JSON представления Отгрузок, которые вы хотите создать или обновить.
Обновляемые Отгрузки должны содержать идентификатор в виде метаданных.

> Пример создания и обновления нескольких Отгрузок

```shell
  curl -X POST
    "https://online.moysklad.ru/api/remap/1.2/entity/demand"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '[
            {
              "name": "888",
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
            },
            {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/405f69c0-019e-11e6-9464-e4de00000085",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
                "type": "demand",
                "mediaType": "application/json"
              },
              "name": "887",
              "moment": "2004-01-14 19:03:00",
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
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/86c857d6-0302-11e6-9464-e4de00000072",
                  "type": "store",
                  "mediaType": "application/json"
                }
              },
              "code": "666",
              "applicable": false,
              "vatEnabled": true,
              "vatIncluded": true,
              "customerOrder": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/customerorder/c49e83b3-01af-11e6-9464-e4de00000026",
                  "type": "customerorder",
                  "mediaType": "application/json"
                }
              },
              "stateContractId": "s11233dsasd233"
            }
          ]'  
```

> Response 200 (application/json)
Успешный запрос. Результат - массив JSON представлений созданных и обновленных Отгрузок.

```json
[
  {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/2464c97a-030a-11e6-9464-e4de00000000",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
      "type": "demand",
      "mediaType": "application/json"
    },
    "id": "2464c97a-030a-11e6-9464-e4de00000000",
    "accountId": "84e60e93-f504-11e5-8a84-bae500000008",
    "syncId": "734a9e26-45a2-4ead-849c-e144daeb854d",
    "updated": "2016-04-15 16:01:17",
    "name": "888",
    "externalCode": "Dt7BqCkBhCxUMXayh4NfA2",
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
    "moment": "2016-04-15 16:01:17",
    "applicable": true,
    "vatEnabled": true,
    "vatIncluded": true,
    "sum": 0,
    "rate": {
      "currency": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/baac25f0-50ac-11e5-300d-c79b00000055",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
          "type": "currency",
          "mediaType": "application/json"
        }
      }
    },
    "organization": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/850c8195-f504-11e5-8a84-bae50000015e",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
        "type": "organization",
        "mediaType": "application/json"
      }
    },
    "store": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/850ee995-f504-11e5-8a84-bae500000160",
        "type": "store",
        "mediaType": "application/json"
      }
    },
    "agent": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/9794d400-f689-11e5-8a84-bae500000078",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
        "type": "counterparty",
        "mediaType": "application/json"
      }
    },
    "organizationAccount": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/850c8195-f504-11e5-8a84-bae50000015e/accounts/3a30e844-016f-11e6-9464-e4de00000068",
        "type": "account",
        "mediaType": "application/json"
      }
    },
    "agentAccount": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/9794d400-f689-11e5-8a84-bae500000078/accounts/9794f7a0-f689-11e5-8a84-bae500000079",
        "type": "account",
        "mediaType": "application/json"
      }
    },
    "created": "2016-08-25 19:55:00",
    "printed": true,
    "published": true,
    "positions": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/2464c97a-030a-11e6-9464-e4de00000000/positions",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
        "type": "demandposition",
        "mediaType": "application/json",
        "size": 0,
        "limit": 1000,
        "offset": 0
      }
    },
    "payedSum": 0
  },
  {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/405f69c0-019e-11e6-9464-e4de00000085",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
      "type": "demand",
      "mediaType": "application/json"
    },
    "id": "405f69c0-019e-11e6-9464-e4de00000085",
    "accountId": "84e60e93-f504-11e5-8a84-bae500000008",
    "syncId": "734a9e26-45a2-4ead-849c-e144daeb854d",
    "updated": "2016-04-15 16:26:20",
    "name": "887",
    "code": "666",
    "externalCode": "ibWbdtWWhXiIwfZVEal6z2",
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
    "moment": "2004-01-14 19:03:00",
    "applicable": false,
    "vatEnabled": true,
    "vatIncluded": true,
    "sum": 346389501420,
    "rate": {
      "currency": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/baac25f0-50ac-11e5-300d-c79b00000055",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
          "type": "currency",
          "mediaType": "application/json"
        }
      }
    },
    "organization": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/850c8195-f504-11e5-8a84-bae50000015e",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
        "type": "organization",
        "mediaType": "application/json"
      }
    },
    "store": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/86c857d6-0302-11e6-9464-e4de00000072",
        "type": "store",
        "mediaType": "application/json"
      }
    },
    "contract": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/contract/8ce3c179-015e-11e6-9464-e4de0000007a",
        "type": "contract",
        "mediaType": "application/json"
      }
    },
    "project": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/project/51f263f9-0307-11e6-9464-e4de0000007c",
        "type": "project",
        "mediaType": "application/json"
      }
    },
    "agent": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/9794d400-f689-11e5-8a84-bae500000078",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
        "type": "counterparty",
        "mediaType": "application/json"
      }
    },
    "state": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/states/fb56c504-2e58-11e6-8a84-bae500000069",
        "type": "state",
        "mediaType": "application/json"
      }
    },
    "organizationAccount": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/850c8195-f504-11e5-8a84-bae50000015e/accounts/850c8af2-f504-11e5-8a84-bae50000015f",
        "type": "account",
        "mediaType": "application/json"
      }
    },
    "agentAccount": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/9794d400-f689-11e5-8a84-bae500000078/accounts/9794f7a0-f689-11e5-8a84-bae500000079",
        "type": "account",
        "mediaType": "application/json"
      }
    },
    "created": "2016-08-25 19:55:00",
    "printed": true,
    "published": true,
    "positions": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/405f69c0-019e-11e6-9464-e4de00000085/positions",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
        "type": "demandposition",
        "mediaType": "application/json",
        "size": 4,
        "limit": 1000,
        "offset": 0
      }
    },
    "payedSum": 365939611804,
    "customerOrder": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/customerorder/34efe2ee-015e-11e6-9464-e4de0000006b",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/customerOrder/metadata",
        "type": "customerorder",
        "mediaType": "application/json"
      }
    },
    "stateContractId": "s11233dsasd233"
  }
]
```

### Удалить Отгрузку

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Отгрузки.|

> Запрос на удаление Отгрузки с указанным id.

```shell
curl -X DELETE
  "https://online.moysklad.ru/api/remap/1.2/entity/demand/7944ef04-f831-11e5-7a69-971500188b19"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешное удаление Отгрузки.

### Массовое удаление Отгрузок

В теле запроса нужно передать массив, содержащий JSON метаданных Отгрузок, которые вы хотите удалить.


> Запрос на массовое удаление Отгрузок. 

```shell
curl -X POST
  "https://online.moysklad.ru/api/remap/1.2/entity/demand/delete"
  -H "Authorization: Basic <Credentials>"
  -H "Content-Type: application/json"
  -d '[
        {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/7944ef04-f831-11e5-7a69-971500188b1",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
            "type": "demand",
            "mediaType": "application/json"
        },
        {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/7944ef04-f831-11e5-7a69-971500188b2",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
            "type": "demand",
            "mediaType": "application/json"
        }
      ]'
```        

> Успешный запрос. Результат - JSON информация об удалении Отгрузок.

```json
[
  {
    "info":"Сущность 'demand' с UUID: 7944ef04-f831-11e5-7a69-971500188b1 успешно удалена"
  },
  {
    "info":"Сущность 'demand' с UUID: 7944ef04-f831-11e5-7a69-971500188b2 успешно удалена"
  }
]
``` 

### Метаданные Отгрузок 
#### Метаданные Отгрузок 
Запрос на получение метаданных Отгрузок. Результат - объект JSON, включающий в себя:

| Параметр                | Описание  |
| ------------------------------ |:---------------------------|
| **meta**         | Ссылка на метаданные Отгрузок|
| **attributes**   | Массив объектов доп. полей Отгрузок в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye)|
| **states**       | Массив статусов Отгрузок|
| **createShared** | создавать новые Отгрузки  с меткой "Общий"|

Структура отдельного объекта, представляющего доп. поле подробно описана в разделе [Работа с дополнительными полями](../#mojsklad-json-api-obschie-swedeniq-rabota-s-dopolnitel-nymi-polqmi).

> Метаданные Отгрузок

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление доп. полей Отгрузок.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
    "mediaType": "application/json"
  },
  "attributes": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/attributes/23d3965d-0313-11e6-9464-e4de00000097",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "23d3965d-0313-11e6-9464-e4de00000097",
      "name": "AttributeName1",
      "type": "boolean",
      "required": false
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/attributes/5290a290-0313-11e6-9464-e4de00000020",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "5290a290-0313-11e6-9464-e4de00000020",
      "name": "AttributeName2",
      "type": "boolean",
      "required": false
    }
  ],
  "states": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/states/fb56c504-2e58-11e6-8a84-bae500000069",
        "type": "state",
        "mediaType": "application/json"
      },
      "id": "fb56c504-2e58-11e6-8a84-bae500000069",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "name": "Новый",
      "color": 15106326,
      "stateType": "Regular",
      "entityType": "demand"
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/states/fb56cae3-2e58-11e6-8a84-bae50000006a",
        "type": "state",
        "mediaType": "application/json"
      },
      "id": "fb56cae3-2e58-11e6-8a84-bae50000006a",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "name": "Подтвержден",
      "color": 40931,
      "stateType": "Regular",
      "entityType": "demand"
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/states/fb56cf4f-2e58-11e6-8a84-bae50000006b",
        "type": "state",
        "mediaType": "application/json"
      },
      "id": "fb56cf4f-2e58-11e6-8a84-bae50000006b",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "name": "Собран",
      "color": 8767198,
      "stateType": "Regular",
      "entityType": "demand"
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/states/fb56d433-2e58-11e6-8a84-bae50000006c",
        "type": "state",
        "mediaType": "application/json"
      },
      "id": "fb56d433-2e58-11e6-8a84-bae50000006c",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "name": "Отгружен",
      "color": 10774205,
      "stateType": "Regular",
      "entityType": "demand"
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/states/fb56d92f-2e58-11e6-8a84-bae50000006d",
        "type": "state",
        "mediaType": "application/json"
      },
      "id": "fb56d92f-2e58-11e6-8a84-bae50000006d",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "name": "Доставлен",
      "color": 8825440,
      "stateType": "Successful",
      "entityType": "demand"
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/states/fb56de0a-2e58-11e6-8a84-bae50000006e",
        "type": "state",
        "mediaType": "application/json"
      },
      "id": "fb56de0a-2e58-11e6-8a84-bae50000006e",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "name": "Возврат",
      "color": 15280409,
      "stateType": "Unsuccessful",
      "entityType": "demand"
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/states/fb56e2b4-2e58-11e6-8a84-bae50000006f",
        "type": "state",
        "mediaType": "application/json"
      },
      "id": "fb56e2b4-2e58-11e6-8a84-bae50000006f",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "name": "Отменен",
      "color": 15280409,
      "stateType": "Unsuccessful",
      "entityType": "demand"
    }
  ],
  "createShared": false
}
```

### Отдельное доп. поле



**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Доп. поля.|
 
> Запрос на получение информации по отдельному дополнительному полю.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/attributes/7944ef04-f831-11e5-7a69-971500188b19"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление отдельного доп. поля.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/attributes/127d484e-3f81-11e6-8a84-bae5000000cb",
    "type": "attributemetadata",
    "mediaType": "application/json"
  },
  "id": "127d484e-3f81-11e6-8a84-bae5000000cb",
  "name": "AttributeName1",
  "type": "boolean",
  "required": false
}

```

### Шаблон Отгрузки 
#### Шаблон Отгрузки 
> Запрос на получение предзаполненого стандартными значениями шаблона отгрузки без связи с каким-либо документом.

```shell
  curl -X PUT
    "https://online.moysklad.ru/api/remap/1.2/entity/demand/new"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d ''  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление предзаполненной отгрузки.

```json
{
  "owner": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/105a788e-36e7-11e7-8a7f-40d000000069",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
      "type": "employee",
      "mediaType": "application/json"
    }
  },
  "shared": false,
  "group": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/group/103cca6f-36e7-11e7-8a7f-40d000000005",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/group/metadata",
      "type": "group",
      "mediaType": "application/json"
    }
  },
  "moment": "2017-05-12 15:31:10",
  "applicable": true,
  "sum": 0,
  "store": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/1076a96a-36e7-11e7-8a7f-40d000000092",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
      "type": "store",
      "mediaType": "application/json"
    }
  },
  "organization": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/107430bc-36e7-11e7-8a7f-40d000000090",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
      "type": "organization",
      "mediaType": "application/json"
    }
  },
  "positions": {
    "rows": []
  },
  "vatEnabled": true,
  "vatIncluded": true,
  "payedSum": 0
}
```

### Шаблон Отгрузки на основе 
Запрос на получение шаблона отгрузки на основе заказа покупателя или счета покупателю.
В результате запроса, будет создан предзаполненный шаблон отгрузки на основе переданного
документа.

> Запрос на создание отгрузки на основе заказа покупателя.

```shell
  curl -X PUT
    "https://online.moysklad.ru/api/remap/1.2/entity/demand/new"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "customerOrder": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/customerorder/451cb4c0-3d1d-11e6-8a84-bae500000004",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/customerorder/metadata",
                "type": "customerorder",
                "mediaType": "application/json"
              }
            }
          }'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление предзаполненной отгрузки.

```json
{
  "owner": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/b905bfb0-9128-11e6-8a84-bae50000002a",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
      "type": "employee",
      "mediaType": "application/json"
    }
  },
  "shared": false,
  "group": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/group/b8ba0d3f-9128-11e6-8a84-bae500000002",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/group/metadata",
      "type": "group",
      "mediaType": "application/json"
    }
  },
  "moment": "2016-11-25 18:02:21",
  "applicable": true,
  "rate": {
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/baac25f0-50ac-11e5-300d-c79b00000055",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json"
      }
    }
  },
  "sum": 0,
  "store": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/b942743c-9128-11e6-8a84-bae500000053",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
      "type": "store",
      "mediaType": "application/json"
    }
  },
  "agent": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/b9324d71-9128-11e6-8a84-bae500000051",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
      "type": "organization",
      "mediaType": "application/json"
    }
  },
  "organization": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/b9324d71-9128-11e6-8a84-bae500000051",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
      "type": "organization",
      "mediaType": "application/json"
    }
  },
  "agentAccount": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/b9324d71-9128-11e6-8a84-bae500000051/accounts/b932bc5b-9128-11e6-8a84-bae500000052",
      "type": "account",
      "mediaType": "application/json"
    }
  },
  "organizationAccount": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/b9324d71-9128-11e6-8a84-bae500000051/accounts/b932bc5b-9128-11e6-8a84-bae500000052",
      "type": "account",
      "mediaType": "application/json"
    }
  },
  "created": "2016-08-25 19:55:00",
  "printed": true,
  "published": true,
  "positions": {
    "rows": [
      {
        "quantity": 1,
        "price": 0,
        "discount": 0,
        "vat": 0,
        "vatEnabled": false,
        "assortment": {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/c55b5e7c-9128-11e6-8a84-bae500000087",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
            "type": "product",
            "mediaType": "application/json",
            "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=392c045c-2842-11e9-ac12-000a00000002"
          }
        },
        "overhead": 0
      }
    ]
  },
  "vatEnabled": true,
  "vatIncluded": true,
  "payedSum": 0,
  "customerOrder": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/customerorder/559adab5-915c-11e6-8a84-bae500000014",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/customerorder/metadata",
      "type": "customerorder",
      "mediaType": "application/json"
    }
  }
}
```

> Запрос на создание отгрузки на основе счета покупателя.

```shell
  curl -X PUT
    "https://online.moysklad.ru/api/remap/1.2/entity/demand/new"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "invoicesOut": [
              {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/invoiceout/1571eb25-d03d-11e7-6a80-332a00000002",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/invoiceout/metadata",
                  "type": "invoiceout",
                  "mediaType": "application/json",
                  "uuidHref": "https://online.moysklad.ru/app/#invoiceout/edit?id=1571eb25-d03d-11e7-6a80-332a00000002"
                }
              }
            ]
          }'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление предзаполненной отгрузки.

```json
{
  "owner": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/46073d61-ca1f-11e7-6a80-332a0000002a",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
      "type": "employee",
      "mediaType": "application/json",
      "uuidHref": "https://online.moysklad.ru/app/#employee/edit?id=46073d61-ca1f-11e7-6a80-332a0000002a"
    }
  },
  "shared": false,
  "group": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/group/452fb22f-ca1f-11e7-6a80-332a00000002",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/group/metadata",
      "type": "group",
      "mediaType": "application/json"
    }
  },
  "name": "",
  "moment": "2017-11-23 13:59:29",
  "applicable": true,
  "rate": {
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/464062ac-ca1f-11e7-6a80-332a00000058",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json",
        "uuidHref": "https://online.moysklad.ru/app/#currency/edit?id=464062ac-ca1f-11e7-6a80-332a00000058"
      }
    }
  },
  "sum": 0,
  "store": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/463f8970-ca1f-11e7-6a80-332a00000053",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
      "type": "store",
      "mediaType": "application/json",
      "uuidHref": "https://online.moysklad.ru/app/#warehouse/edit?id=463f8970-ca1f-11e7-6a80-332a00000053"
    }
  },
  "agent": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/463fe231-ca1f-11e7-6a80-332a00000056",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
      "mediaType": "application/json",
      "uuidHref": "https://online.moysklad.ru/app/#company/edit?id=463fe231-ca1f-11e7-6a80-332a00000056"
    }
  },
  "organization": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/463a706e-ca1f-11e7-6a80-332a00000051",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
      "type": "organization",
      "mediaType": "application/json",
      "uuidHref": "https://online.moysklad.ru/app/#mycompany/edit?id=463a706e-ca1f-11e7-6a80-332a00000051"
    }
  },
  "documents": {
    "rows": []
  },
  "positions": {
    "rows": [
      {
        "quantity": 1,
        "price": 100000,
        "discount": 0,
        "vat": 0,
        "vatEnabled": false,
        "assortment": {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/variant/b5d94dd1-cab0-11e7-6a80-332a00000011",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/variant/metadata",
            "type": "variant",
            "mediaType": "application/json",
            "uuidHref": "https://online.moysklad.ru/app/#feature/edit?id=3b1e1f15-2842-11e9-ac12-000c0000002f"
          }
        },
        "overhead": 0
      }
    ]
  },
  "vatEnabled": true,
  "vatIncluded": true,
  "payedSum": 0,
  "invoicesOut": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/invoiceout/1571eb25-d03d-11e7-6a80-332a00000002",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/invoiceout/metadata",
        "type": "invoiceout",
        "mediaType": "application/json",
        "uuidHref": "https://online.moysklad.ru/app/#invoiceout/edit?id=1571eb25-d03d-11e7-6a80-332a00000002"
      }
    }
  ]
}
```

### Отгрузка
 
### Получить Отгрузку

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Отгрузки.|
 
> Запрос на получение отдельной Отгрузки с указанным id.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/demand/7944ef04-f831-11e5-7a69-971500188b19"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление Отгрузки.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/405f69c0-019e-11e6-9464-e4de00000085",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
    "type": "demand",
    "mediaType": "application/json"
  },
  "id": "405f69c0-019e-11e6-9464-e4de00000085",
  "accountId": "84e60e93-f504-11e5-8a84-bae500000008",
  "syncId": "734a9e26-45a2-4ead-849c-e144daeb854d",
  "updated": "2016-04-15 15:48:46",
  "name": "24124",
  "externalCode": "ibWbdtWWhXiIwfZVEal6z2",
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
  "moment": "2016-04-14 11:03:00",
  "applicable": true,
  "vatEnabled": true,
  "vatIncluded": true,
  "sum": 346389501420,
  "rate": {
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/bc1b4fde-019a-11e6-9464-e4de00000073",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json"
      }
    },
    "value": 214
  },
  "organization": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/850c8195-f504-11e5-8a84-bae50000015e",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
      "type": "organization",
      "mediaType": "application/json"
    }
  },
  "store": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/850ee995-f504-11e5-8a84-bae500000160",
      "type": "store",
      "mediaType": "application/json"
    }
  },
  "contract": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/contract/8ce3c179-015e-11e6-9464-e4de0000007a",
      "type": "contract",
      "mediaType": "application/json"
    }
  },
  "project": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/project/51f263f9-0307-11e6-9464-e4de0000007c",
      "type": "project",
      "mediaType": "application/json"
    }
  },
  "agent": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/9794d400-f689-11e5-8a84-bae500000078",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
      "mediaType": "application/json"
    }
  },
  "state": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/states/fb56c504-2e58-11e6-8a84-bae500000069",
      "type": "state",
      "mediaType": "application/json"
    }
  },
  "organizationAccount": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/850c8195-f504-11e5-8a84-bae50000015e/accounts/850c8af2-f504-11e5-8a84-bae50000015f",
      "type": "account",
      "mediaType": "application/json"
    }
  },
  "agentAccount": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/9794d400-f689-11e5-8a84-bae500000078/accounts/9794f7a0-f689-11e5-8a84-bae500000079",
      "type": "account",
      "mediaType": "application/json"
    }
  },
  "positions": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/405f69c0-019e-11e6-9464-e4de00000085/positions",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
      "type": "demandposition",
      "mediaType": "application/json",
      "size": 4,
      "limit": 1000,
      "offset": 0
    }
  },
  "payedSum": 365939611804,
  "customerOrder": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/customerorder/34efe2ee-015e-11e6-9464-e4de0000006b",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/customerOrder/metadata",
      "type": "customerorder",
      "mediaType": "application/json"
    }
  },
  "consignee": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/869d7628-6396-11e6-8a84-bae50000000a",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
      "mediaType": "application/json"
    }
  },
  "transportFacilityNumber": "ло777v",
  "shippingInstructions": "Беречь от воздействия солнца",
  "cargoName": "Овощи",
  "transportFacility": "Mercedes benz",
  "goodPackQuantity": 500,
  "carrier": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/cffd2c81-62b4-11e6-8a84-bae500000053",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
      "mediaType": "application/json"
    }
  },
  "overhead": {
    "sum": 200,
    "distribution": "price"
  }
}
```

### Изменить Отгрузку 
Запрос на обновление Отгрузки с указанным id.
В теле запроса можно указать только те поля, которые необходимо изменить у Отгрузки, кроме тех, что
помечены `Только для чтения` в описании [атрибутов Отгрузки](../documents/#dokumenty-otgruzka).
При обновлении полей **organization** и **agent** нужно также обновить поля **organizationAccount** и
**agentAccount** соответственно, иначе произойдет ошибка.

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Отгрузки.|

> Пример запроса на обновление отдельной Отгрузки.

```shell
  curl -X PUT
    "https://online.moysklad.ru/api/remap/1.2/entity/demand/7944ef04-f831-11e5-7a69-971500188b19"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "name": "887",
            "moment": "2004-01-14 19:03:00",
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
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/86c857d6-0302-11e6-9464-e4de00000072",
                "type": "store",
                "mediaType": "application/json"
              }
            },
            "code": "666",
            "applicable": false,
            "vatEnabled": true,
            "vatIncluded": true,
            "customerOrder": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/customerorder/c49e83b3-01af-11e6-9464-e4de00000026",
                "type": "customerorder",
                "mediaType": "application/json"
              }
            },
            "stateContractId": "s11233dsasd233"
          }'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление обновленной Отгрузки.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/405f69c0-019e-11e6-9464-e4de00000085",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
    "type": "demand",
    "mediaType": "application/json"
  },
  "id": "405f69c0-019e-11e6-9464-e4de00000085",
  "accountId": "84e60e93-f504-11e5-8a84-bae500000008",
  "syncId": "734a9e26-45a2-4ead-849c-e144daeb854d",
  "updated": "2016-04-15 16:26:20",
  "name": "887",
  "code": "666",
  "externalCode": "ibWbdtWWhXiIwfZVEal6z2",
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
  "moment": "2004-01-14 19:03:00",
  "applicable": false,
  "vatEnabled": true,
  "vatIncluded": true,
  "sum": 346389501420,
  "rate": {
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/baac25f0-50ac-11e5-300d-c79b00000055",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json"
      }
    }
  },
  "organization": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/850c8195-f504-11e5-8a84-bae50000015e",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
      "type": "organization",
      "mediaType": "application/json"
    }
  },
  "store": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/86c857d6-0302-11e6-9464-e4de00000072",
      "type": "store",
      "mediaType": "application/json"
    }
  },
  "contract": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/contract/8ce3c179-015e-11e6-9464-e4de0000007a",
      "type": "contract",
      "mediaType": "application/json"
    }
  },
  "project": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/project/51f263f9-0307-11e6-9464-e4de0000007c",
      "type": "project",
      "mediaType": "application/json"
    }
  },
  "agent": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/9794d400-f689-11e5-8a84-bae500000078",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
      "mediaType": "application/json"
    }
  },
  "state": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/states/fb56c504-2e58-11e6-8a84-bae500000069",
      "type": "state",
      "mediaType": "application/json"
    }
  },
  "organizationAccount": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/850c8195-f504-11e5-8a84-bae50000015e/accounts/850c8af2-f504-11e5-8a84-bae50000015f",
      "type": "account",
      "mediaType": "application/json"
    }
  },
  "agentAccount": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/9794d400-f689-11e5-8a84-bae500000078/accounts/9794f7a0-f689-11e5-8a84-bae500000079",
      "type": "account",
      "mediaType": "application/json"
    }
  },
  "created": "2016-08-25 19:55:00",
  "printed": true,
  "published": true,
  "positions": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/405f69c0-019e-11e6-9464-e4de00000085/positions",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
      "type": "demandposition",
      "mediaType": "application/json",
      "size": 4,
      "limit": 1000,
      "offset": 0
    }
  },
  "payedSum": 365939611804,
  "customerOrder": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/customerorder/34efe2ee-015e-11e6-9464-e4de0000006b",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/customerOrder/metadata",
      "type": "customerorder",
      "mediaType": "application/json"
    }
  },
  "stateContractId": "s11233dsasd233"
}
```

> Пример запроса на изменение Отгрузки с дополнительными полями.

```shell
  curl -X PUT
    "https://online.moysklad.ru/api/remap/1.2/entity/demand/7944ef04-f831-11e5-7a69-971500188b19"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "name": "887",
            "moment": "2004-01-14 19:03:00",
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
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/86c857d6-0302-11e6-9464-e4de00000072",
                "type": "store",
                "mediaType": "application/json"
              }
            },
            "code": "666",
            "applicable": false,
            "vatEnabled": true,
            "vatIncluded": true,
            "customerOrder": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/customerorder/c49e83b3-01af-11e6-9464-e4de00000026",
                "type": "customerorder",
                "mediaType": "application/json"
              }
            },
            "attributes": [
              {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/attributes/0cd74e1e-2e59-11e6-8a84-bae50000008a",
                  "type": "attributemetadata",
                  "mediaType": "application/json"
                },
                "name": "AttributeName1",
                "type": "boolean",
                "value": true
              }
            ],
            "consignee": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/869d7628-6396-11e6-8a84-bae50000000a",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
                "type": "counterparty",
                "mediaType": "application/json"
              }
            },
            "transportFacilityNumber": "МК2142",
            "shippingInstructions": "Огнеопасно",
            "cargoName": "масло",
            "transportFacility": "Камаз 2007",
            "carrier": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/cffd2c81-62b4-11e6-8a84-bae500000053",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
                "type": "counterparty",
                "mediaType": "application/json"
              }
            },
            "overhead": {
              "sum": 990,
              "distribution": "price"
            }
          }'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление обновленной Отгрузки.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/405f69c0-019e-11e6-9464-e4de00000085",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
    "type": "demand",
    "mediaType": "application/json"
  },
  "id": "405f69c0-019e-11e6-9464-e4de00000085",
  "accountId": "84e60e93-f504-11e5-8a84-bae500000008",
  "syncId": "734a9e26-45a2-4ead-849c-e144daeb854d",
  "updated": "2016-04-15 16:26:20",
  "name": "887",
  "code": "666",
  "externalCode": "ibWbdtWWhXiIwfZVEal6z2",
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
  "moment": "2004-01-14 19:03:00",
  "applicable": false,
  "vatEnabled": true,
  "vatIncluded": true,
  "sum": 346389501420,
  "rate": {
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/baac25f0-50ac-11e5-300d-c79b00000055",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json"
      }
    }
  },
  "organization": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/850c8195-f504-11e5-8a84-bae50000015e",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
      "type": "organization",
      "mediaType": "application/json"
    }
  },
  "store": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/86c857d6-0302-11e6-9464-e4de00000072",
      "type": "store",
      "mediaType": "application/json"
    }
  },
  "contract": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/contract/8ce3c179-015e-11e6-9464-e4de0000007a",
      "type": "contract",
      "mediaType": "application/json"
    }
  },
  "project": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/project/51f263f9-0307-11e6-9464-e4de0000007c",
      "type": "project",
      "mediaType": "application/json"
    }
  },
  "agent": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/9794d400-f689-11e5-8a84-bae500000078",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
      "mediaType": "application/json"
    }
  },
  "state": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/states/fb56c504-2e58-11e6-8a84-bae500000069",
      "type": "state",
      "mediaType": "application/json"
    }
  },
  "organizationAccount": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/850c8195-f504-11e5-8a84-bae50000015e/accounts/850c8af2-f504-11e5-8a84-bae50000015f",
      "type": "account",
      "mediaType": "application/json"
    }
  },
  "agentAccount": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/9794d400-f689-11e5-8a84-bae500000078/accounts/9794f7a0-f689-11e5-8a84-bae500000079",
      "type": "account",
      "mediaType": "application/json"
    }
  },
  "attributes": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/attributes/0cd74e1e-2e59-11e6-8a84-bae50000008a",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "23d3965d-0313-11e6-9464-e4de00000097",
      "name": "AttributeName1",
      "type": "boolean",
      "value": true
    }
  ],
  "created": "2016-08-25 19:55:00",
  "printed": true,
  "published": true,
  "positions": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/405f69c0-019e-11e6-9464-e4de00000085/positions",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
      "type": "demandposition",
      "mediaType": "application/json",
      "size": 4,
      "limit": 1000,
      "offset": 0
    }
  },
  "payedSum": 365939611804,
  "customerOrder": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/customerorder/34efe2ee-015e-11e6-9464-e4de0000006b",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/customerOrder/metadata",
      "type": "customerorder",
      "mediaType": "application/json"
    }
  },
  "consignee": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/869d7628-6396-11e6-8a84-bae50000000a",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
      "mediaType": "application/json"
    }
  },
  "transportFacilityNumber": "МК2142",
  "shippingInstructions": "Огнеопасно",
  "cargoName": "масло",
  "transportFacility": "Камаз 2007",
  "carrier": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/cffd2c81-62b4-11e6-8a84-bae500000053",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
      "mediaType": "application/json"
    }
  },
  "overhead": {
    "sum": 990,
    "distribution": "price"
  }
}
```

> Пример запроса на обновление Отгрузки с позициями в теле запроса.

```shell
  curl -X PUT
    "https://online.moysklad.ru/api/remap/1.2/entity/demand/7944ef04-f831-11e5-7a69-971500188b19"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "name": "887",
            "moment": "2004-01-14 19:03:00",
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
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/86c857d6-0302-11e6-9464-e4de00000072",
                "type": "store",
                "mediaType": "application/json"
              }
            },
            "code": "666",
            "applicable": false,
            "vatEnabled": true,
            "vatIncluded": true,
            "customerOrder": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/customerorder/c49e83b3-01af-11e6-9464-e4de00000026",
                "type": "customerorder",
                "mediaType": "application/json"
              }
            },
            "positions": [
              {
                "id": "34f6344f-015e-11e6-9464-e4de0000006c",
                "quantity": 10,
                "price": 100,
                "discount": 0,
                "vat": 0,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/8b382799-f7d2-11e5-8a84-bae5000003a5",
                    "type": "product",
                    "mediaType": "application/json"
                  }
                },
                "reserve": 10
              },
              {
                "id": "34f6344f-015e-11e6-9464-e4de0000006d",
                "quantity": 20,
                "price": 200,
                "discount": 0,
                "vat": 21,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/be903062-f504-11e5-8a84-bae50000019a",
                    "type": "product",
                    "mediaType": "application/json"
                  }
                },
                "reserve": 20
              },
              {
                "id": "34f6344f-015e-11e6-9464-e4de0000006e",
                "quantity": 30,
                "price": 300,
                "discount": 0,
                "vat": 7,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/c02e3a5c-007e-11e6-9464-e4de00000006",
                    "type": "product",
                    "mediaType": "application/json"
                  }
                },
                "reserve": 30
              }
            ],
            "overhead": {
              "sum": 1000,
              "distribution": "weight"
            }
          }
'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление обновленной Отгрузки.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/405f69c0-019e-11e6-9464-e4de00000085",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
    "type": "demand",
    "mediaType": "application/json"
  },
  "id": "405f69c0-019e-11e6-9464-e4de00000085",
  "accountId": "84e60e93-f504-11e5-8a84-bae500000008",
  "syncId": "734a9e26-45a2-4ead-849c-e144daeb854d",
  "updated": "2016-04-15 16:26:20",
  "name": "887",
  "code": "666",
  "externalCode": "ibWbdtWWhXiIwfZVEal6z2",
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
  "moment": "2004-01-14 19:03:00",
  "applicable": false,
  "vatEnabled": true,
  "vatIncluded": true,
  "sum": 346389501420,
  "rate": {
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/baac25f0-50ac-11e5-300d-c79b00000055",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json"
      }
    }
  },
  "organization": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/850c8195-f504-11e5-8a84-bae50000015e",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
      "type": "organization",
      "mediaType": "application/json"
    }
  },
  "store": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/86c857d6-0302-11e6-9464-e4de00000072",
      "type": "store",
      "mediaType": "application/json"
    }
  },
  "contract": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/contract/8ce3c179-015e-11e6-9464-e4de0000007a",
      "type": "contract",
      "mediaType": "application/json"
    }
  },
  "project": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/project/51f263f9-0307-11e6-9464-e4de0000007c",
      "type": "project",
      "mediaType": "application/json"
    }
  },
  "agent": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/9794d400-f689-11e5-8a84-bae500000078",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
      "mediaType": "application/json"
    }
  },
  "state": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata/states/fb56c504-2e58-11e6-8a84-bae500000069",
      "type": "state",
      "mediaType": "application/json"
    }
  },
  "organizationAccount": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/850c8195-f504-11e5-8a84-bae50000015e/accounts/850c8af2-f504-11e5-8a84-bae50000015f",
      "type": "account",
      "mediaType": "application/json"
    }
  },
  "agentAccount": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/9794d400-f689-11e5-8a84-bae500000078/accounts/9794f7a0-f689-11e5-8a84-bae500000079",
      "type": "account",
      "mediaType": "application/json"
    }
  },
  "created": "2016-08-25 19:55:00",
  "printed": true,
  "published": true,
  "positions": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/405f69c0-019e-11e6-9464-e4de00000085/positions",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
      "type": "demandposition",
      "mediaType": "application/json",
      "size": 4,
      "limit": 1000,
      "offset": 0
    }
  },
  "payedSum": 365939611804,
  "customerOrder": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/customerorder/34efe2ee-015e-11e6-9464-e4de0000006b",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/customerOrder/metadata",
      "type": "customerorder",
      "mediaType": "application/json"
    }
  },
  "stateContractId": "s11233dsasd233"
}
```

### Позиции Отгрузки 
Отдельный ресурс для управления позициями Отгрузки. С его помощью вы можете управлять позициями большого документа, количество строк в котором превышает лимит на количество строк, сохраняемых вместе с документом. Этот лимит равен 1000. Более подробно о лимитах на количество строк документа и работе с большими документами можно прочитать [тут](../#mojsklad-json-api-obschie-swedeniq-rabota-s-poziciqmi-dokumentow).

### Получить позиции Отгрузки 
Запрос на получение списка всех позиций данной Отгрузки.

| Название  | Тип | Описание                    |
| --------- |:----|:----------------------------|
**meta** |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные о выдаче,
**context** | [Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye) | Метаданные о сотруднике, выполнившем запрос.
**rows** |Array(Object)|Массив JSON объектов, представляющих собой позиции Отгрузки.

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Отгрузки.|
|**limit** |  `number` (optional) **Default: 1000** *Example: 1000* Максимальное количество сущностей для извлечения.`Допустимые значения 1 - 1000`.|
|**offset** |  `number` (optional) **Default: 0** *Example: 40* Отступ в выдаваемом списке сущностей.|

> Получить позиции Отгрузки

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/demand/7944ef04-f831-11e5-7a69-971500188b19/positions"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление списка позиций отдельной Отгрузки.

```json
{
  "context": {
    "employee": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/context/employee",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
        "type": "employee",
        "mediaType": "application/json"
      }
    }
  },
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/7944ef04-f831-11e5-7a69-971500188b19/positions",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
    "type": "demandposition",
    "mediaType": "application/json",
    "size": 4,
    "limit": 1000,
    "offset": 0
  },
  "rows": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/7944ef04-f831-11e5-7a69-971500188b19/positions/40603fbd-019e-11e6-9464-e4de00000086",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
        "type": "demandposition",
        "mediaType": "application/json"
      },
      "id": "40603fbd-019e-11e6-9464-e4de00000086",
      "accountId": "84e60e93-f504-11e5-8a84-bae500000008",
      "quantity": 1,
      "sum": 123050,
      "discount": 0,
      "vat": 18,
      "vatEnabled": true,
      "assortment": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/66ccbc9f-f7d2-11e5-8a84-bae500000076",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
          "type": "product",
          "mediaType": "application/json",
          "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=63b1e1f15-2842-11e9-ac12-000c0000002f"
        }
      }
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/7944ef04-f831-11e5-7a69-971500188b19/positions/40604612-019e-11e6-9464-e4de00000087",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
        "type": "demandposition",
        "mediaType": "application/json"
      },
      "id": "40604612-019e-11e6-9464-e4de00000087",
      "accountId": "84e60e93-f504-11e5-8a84-bae500000008",
      "quantity": 1,
      "sum": 214,
      "discount": 0,
      "vat": 18,
      "vatEnabled": true,
      "assortment": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/service/60fc3826-00d7-11e6-9464-e4de00000097",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/service/metadata",
          "type": "service",
          "mediaType": "application/json",
          "uuidHref": "https://online.moysklad.ru/app/#service/edit?id=e64d0a86-2a99-11e9-ac12-000c00000041"
        }
      },
      "cost": 34
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/7944ef04-f831-11e5-7a69-971500188b19/positions/40604a79-019e-11e6-9464-e4de00000088",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
        "type": "demandposition",
        "mediaType": "application/json"
      },
      "id": "40604a79-019e-11e6-9464-e4de00000088",
      "accountId": "84e60e93-f504-11e5-8a84-bae500000008",
      "quantity": 1,
      "sum": 346347237062,
      "discount": 0,
      "vat": 18,
      "vatEnabled": true,
      "assortment": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/56c73633-ffe4-11e5-9464-e4de000000c6",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/variant/metadata",
          "type": "variant",
          "mediaType": "application/json",
          "uuidHref": "https://online.moysklad.ru/app/#feature/edit?id=392c045c-2842-11e9-ac12-000a00000002"
        }
      },
      "country": {
        "name": "Германия"
      }
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/7944ef04-f831-11e5-7a69-971500188b19/positions/406055cb-019e-11e6-9464-e4de00000089",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
        "type": "demandposition",
        "mediaType": "application/json"
      },
      "id": "406055cb-019e-11e6-9464-e4de00000089",
      "accountId": "84e60e93-f504-11e5-8a84-bae500000008",
      "quantity": 1,
      "sum": 42141094,
      "discount": 0,
      "vat": 18,
      "vatEnabled": true,
      "assortment": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/66cc36dc-f7d2-11e5-8a84-bae500000074",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/variant/metadata",
          "type": "variant",
          "mediaType": "application/json",
          "uuidHref": "https://online.moysklad.ru/app/#feature/edit?id=3bb1af6c-2842-11e9-ac12-000c00000061"
        }
      }
    }
  ]
}
```

> Пример с кодами маркировки

```shell
curl --location --request GET 'https://online.moysklad.ru/api/remap/1.2/entity/demand/8830a022-8a03-11ea-0a80-01cb00000040/positions' \
--header 'Authorization: Basic <Credentials>'
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление списка позиций отдельной Отгрузки.

```json
{
   "context":{
      "employee":{
         "meta":{
            "href":"https://online.moysklad.ru/api/remap/1.2/context/employee",
            "metadataHref":"https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
            "type":"employee",
            "mediaType":"application/json"
         }
      }
   },
   "meta":{
      "href":"https://online.moysklad.ru/api/remap/1.2/entity/demand/8830a022-8a03-11ea-0a80-01cb00000040/positions",
      "type":"demandposition",
      "mediaType":"application/json",
      "size":2,
      "limit":1000,
      "offset":0
   },
   "rows":[
      {
         "meta":{
            "href":"https://online.moysklad.ru/api/remap/1.2/entity/demand/8830a022-8a03-11ea-0a80-01cb00000040/positions/8830b0fe-8a03-11ea-0a80-01cb00000041",
            "type":"demandposition",
            "mediaType":"application/json"
         },
         "id":"8830b0fe-8a03-11ea-0a80-01cb00000041",
         "accountId":"de6b5113-8491-11ea-0a80-134500000014",
         "quantity":20.0,
         "price":200.0,
         "discount":0.0,
         "vat":21,
         "vatEnabled": true,
         "assortment":{
            "meta":{
               "href":"https://online.moysklad.ru/api/remap/1.2/entity/product/aa1b1814-8493-11ea-0a80-037a00000307",
               "metadataHref":"https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
               "type":"product",
               "mediaType":"application/json",
               "uuidHref":"https://online.moysklad.ru/app/#good/edit?id=aa1b0d42-8493-11ea-0a80-037a00000305"
            }
         },
         "trackingCodes":[
            {
               "cis":"012345678912345672",
               "type":"transportpack",
               "trackingCodes":[
                  {
                     "cis":"010463003759026521uHpIIf2111111",
                     "type":"trackingcode"
                  },
                  {
                     "cis":"010463003759026521uHpIIf2111114",
                     "type":"trackingcode"
                  }
               ]
            }
         ],
         "overhead":0.0
      },
      {
         "meta":{
            "href":"https://online.moysklad.ru/api/remap/1.2/entity/demand/8830a022-8a03-11ea-0a80-01cb00000040/positions/770f45b4-8a04-11ea-0a80-01cb00000060",
            "type":"demandposition",
            "mediaType":"application/json"
         },
         "id":"770f45b4-8a04-11ea-0a80-01cb00000060",
         "accountId":"de6b5113-8491-11ea-0a80-134500000014",
         "quantity":10.0,
         "price":0.0,
         "discount":0.0,
         "vat":0,
         "vatEnabled": false,
         "assortment":{
            "meta":{
               "href":"https://online.moysklad.ru/api/remap/1.2/entity/product/b20184da-8493-11ea-0a80-037a00000314",
               "metadataHref":"https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
               "type":"product",
               "mediaType":"application/json",
               "uuidHref":"https://online.moysklad.ru/app/#good/edit?id=b20178fb-8493-11ea-0a80-037a00000312"
            }
         },
         "trackingCodes":[
            {
               "cis":"010463003759026521uHpIIf-nXIH>1",
               "type":"trackingcode"
            },
            {
               "cis":"012345678912345671",
               "type":"transportpack"
            },
            {
               "cis":"012345678912345678",
               "type":"transportpack",
               "trackingCodes":[
                  {
                     "cis":"010463003759026521uHpIIf-nXIH>0",
                     "type":"trackingcode"
                  },
                  {
                     "cis":"010463003759026521uHpIIf-nXIH>4",
                     "type":"trackingcode"
                  },
                  {
                     "cis":"010463003759026521uHpIIf-111114",
                     "type":"trackingcode"
                  }
               ]
            },
            {
               "cis":"010463003759026521uHpIIf-111122",
               "type":"trackingcode"
            },
            {
               "cis":"010463003759026521uHpIIf-nXIH>2",
               "type":"trackingcode"
            }
         ],
         "overhead":0.0
      }
   ]
}
```

### Создать позицию Отгрузки 
Запрос на создание новой позиции в Отгрузке.
Для успешного создания необходимо в теле запроса указать следующие поля:

+ **assortment** - Ссылка на товар/услугу/серию/модификацию, которую представляет собой позиция.
Также можно указать поле с именем **service**, **consignment**, **variant** в соответствии с тем,
чем является указанная позиция. Подробнее об этом поле можно прочитать в описании [позиции Отгрузки](../documents/#dokumenty-otgruzka-otgruzki-pozicii-otgruzki)
+ **quantity** - Количество указанной позиции. Должно быть положительным, иначе возникнет ошибка.
Одновременно можно создать как одну так и несколько позиций Отгрузки. Все созданные данным запросом позиции
будут добавлены к уже существующим.

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Отгрузки.|

> Пример создания одной позиции в Отгрузке.

```shell
  curl -X POST
    "https://online.moysklad.ru/api/remap/1.2/entity/demand/7944ef04-f831-11e5-7a69-971500188b19/positions"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "quantity": 4,
            "price": 12345,
            "discount": 0,
            "vat": 0,
            "assortment": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/66ccbc9f-f7d2-11e5-8a84-bae500000076",
                "type": "product",
                "mediaType": "application/json"
              }
            }
          }'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление созданной позиции отдельной Отгрузки.

```json
[
  {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/7944ef04-f831-11e5-7a69-971500188b19/positions/3bf025cc-0310-11e6-9464-e4de0000000e",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
      "type": "demandposition",
      "mediaType": "application/json"
    },
    "id": "3bf025cc-0310-11e6-9464-e4de0000000e",
    "accountId": "84e60e93-f504-11e5-8a84-bae500000008",
    "quantity": 4,
    "price": 12345,
    "discount": 0,
    "vat": 0,
    "vatEnabled": false,
    "assortment": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/66ccbc9f-f7d2-11e5-8a84-bae500000076",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
        "type": "product",
        "mediaType": "application/json",
        "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=3bb1af6c-2842-11e9-ac12-000c00000061"
      }
    }
  }
]
```

> Пример создания сразу нескольких позиций в Отгрузке.

```shell
  curl -X POST
    "https://online.moysklad.ru/api/remap/1.2/entity/demand/7944ef04-f831-11e5-7a69-971500188b19/positions"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '[
            {
              "quantity": 103,
              "price": 1002,
              "discount": 0,
              "vat": 0,
              "assortment": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/8b382799-f7d2-11e5-8a84-bae5000003a5",
                  "type": "product",
                  "mediaType": "application/json"
                }
              }
            },
            {
              "quantity": 21,
              "price": 2300,
              "discount": 0,
              "vat": 21,
              "assortment": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/be903062-f504-11e5-8a84-bae50000019a",
                  "type": "product",
                  "mediaType": "application/json"
                }
              }
            },
            {
              "quantity": 3,
              "price": 3500,
              "discount": 0,
              "vat": 7,
              "assortment": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/service/c02e3a5c-007e-11e6-9464-e4de00000006",
                  "type": "service",
                  "mediaType": "application/json"
                }
              },
              "pack": {
                "id": "1bf22e62-8b47-11e8-56c0-000800000006"
              },
              "cost": 47
            }
          ]'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление списка созданных позиций отдельной Отгрузки.

```json
[
  {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/7944ef04-f831-11e5-7a69-971500188b19/positions/727cf336-0310-11e6-9464-e4de00000013",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
      "type": "demandposition",
      "mediaType": "application/json"
    },
    "id": "727cf336-0310-11e6-9464-e4de00000013",
    "accountId": "84e60e93-f504-11e5-8a84-bae500000008",
    "quantity": 10,
    "price": 100,
    "discount": 0,
    "vat": 0,
    "vatEnabled": false,
    "assortment": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/8b382799-f7d2-11e5-8a84-bae5000003a5",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
        "type": "product",
        "mediaType": "application/json",
        "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=3bb1af6c-2842-11e9-ac12-000c00000061"
      }
    }
  },
  {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/7944ef04-f831-11e5-7a69-971500188b19/positions/727cfce0-0310-11e6-9464-e4de00000014",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
      "type": "demandposition",
      "mediaType": "application/json"
    },
    "id": "727cfce0-0310-11e6-9464-e4de00000014",
    "accountId": "84e60e93-f504-11e5-8a84-bae500000008",
    "quantity": 20,
    "price": 200,
    "discount": 0,
    "vat": 21,
    "vatEnabled": true,
    "assortment": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/be903062-f504-11e5-8a84-bae50000019a",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
        "type": "product",
        "mediaType": "application/json",
        "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=392c045c-2842-11e9-ac12-000a00000002"
      }
    }
  },
  {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/7944ef04-f831-11e5-7a69-971500188b19/positions/727d057f-0310-11e6-9464-e4de00000015",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
      "type": "demandposition",
      "mediaType": "application/json"
    },
    "id": "727d057f-0310-11e6-9464-e4de00000015",
    "accountId": "84e60e93-f504-11e5-8a84-bae500000008",
    "quantity": 30,
    "price": 300,
    "discount": 0,
    "vat": 7,
    "vatEnabled": true,
    "assortment": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/service/c02e3a5c-007e-11e6-9464-e4de00000006",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/service/metadata",
        "type": "service",
        "mediaType": "application/json",
        "uuidHref": "https://online.moysklad.ru/app/#service/edit?id=3b1e1f15-2842-11e9-ac12-000c0000002f"
      }
    },
    "pack": {
      "id": "1bf22e62-8b47-11e8-56c0-000800000006",
      "uom": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/uom/2ec1170c-3f69-4409-87bb-c68e0011b275",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/uom/metadata",
          "type": "uom",
          "mediaType": "application/json"
        }
      },
      "quantity": 2
    },
    "cost": 47
  }
]
```

> Пример с кодами маркировки.

```shell
curl --location --request POST 'https://online.moysklad.ru/api/remap/1.2/entity/demand/8830a022-8a03-11ea-0a80-01cb00000040/positions' \
--header 'Authorization: Basic <Credentials>' \
--header 'Content-Type: application/json' \
--data-raw '{
   "quantity":10.0,
   "price":100.0,
   "discount":0.0,
   "vat":0,
   "assortment":{
      "meta":{
         "href":"https://online.moysklad.ru/api/remap/1.2/entity/product/b20184da-8493-11ea-0a80-037a00000314",
         "metadataHref":"https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
         "type":"product",
         "mediaType":"application/json",
         "uuidHref":"https://online.moysklad.ru/app/#good/edit?id=b20178fb-8493-11ea-0a80-037a00000312"
      }
   },
   "trackingCodes":[
      {
         "cis":"010463003759026521uHpIIf-111122",
         "type":"trackingcode"
      },
      {
         "cis":"012345678912345671",
         "type":"transportpack"
      },
      {
         "cis":"010463003759026521uHpIIf-nXIH>1",
         "type":"trackingcode"
      },
      {
         "cis":"012345678912345678",
         "type":"transportpack",
         "trackingCodes":[
            {
               "cis":"010463003759026521uHpIIf-111114",
               "type":"trackingcode"
            },
            {
               "cis":"010463003759026521uHpIIf-nXIH>4",
               "type":"trackingcode"
            },
            {
               "cis":"010463003759026521uHpIIf-nXIH>0",
               "type":"trackingcode"
            }
         ]
      },
      {
         "cis":"010463003759026521uHpIIf-nXIH>2",
         "type":"trackingcode"
      }
   ],
   "overhead":0.0
}'
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление созданной позиции отдельной Отгрузки.

```json
[
   {
      "meta":{
         "href":"https://online.moysklad.ru/api/remap/1.2/entity/demand/8830a022-8a03-11ea-0a80-01cb00000040/positions/770f45b4-8a04-11ea-0a80-01cb00000060",
         "type":"demandposition",
         "mediaType":"application/json"
      },
      "id":"770f45b4-8a04-11ea-0a80-01cb00000060",
      "accountId":"de6b5113-8491-11ea-0a80-134500000014",
      "quantity":10.0,
      "price":100.0,
      "discount":0.0,
      "vat":0,
      "vatEnabled": false,
      "assortment":{
         "meta":{
            "href":"https://online.moysklad.ru/api/remap/1.2/entity/product/b20184da-8493-11ea-0a80-037a00000314",
            "metadataHref":"https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
            "type":"product",
            "mediaType":"application/json",
            "uuidHref":"https://online.moysklad.ru/app/#good/edit?id=b20178fb-8493-11ea-0a80-037a00000312"
         }
      },
      "trackingCodes":[
         {
            "cis":"010463003759026521uHpIIf-111122",
            "type":"trackingcode"
         },
         {
            "cis":"012345678912345671",
            "type":"transportpack"
         },
         {
            "cis":"010463003759026521uHpIIf-nXIH>1",
            "type":"trackingcode"
         },
         {
            "cis":"012345678912345678",
            "type":"transportpack",
            "trackingCodes":[
               {
                  "cis":"010463003759026521uHpIIf-111114",
                  "type":"trackingcode"
               },
               {
                  "cis":"010463003759026521uHpIIf-nXIH>4",
                  "type":"trackingcode"
               },
               {
                  "cis":"010463003759026521uHpIIf-nXIH>0",
                  "type":"trackingcode"
               }
            ]
         },
         {
            "cis":"010463003759026521uHpIIf-nXIH>2",
            "type":"trackingcode"
         }
      ],
      "overhead":0.0
   }
]
```

### Позиция Отгрузки
 
### Получить позицию

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Отгрузки.|
|**positionID**|  `string` (required) *Example: 34f6344f-015e-11e6-9464-e4de0000006c* id позиции Отгрузки.|
 
> Запрос на получение отдельной позиции Отгрузки с указанным id.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/demand/7944ef04-f831-11e5-7a69-971500188b19/positions/34f6344f-015e-11e6-9464-e4de0000006c"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление отдельной позиции Отгрузки.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/7944ef04-f831-11e5-7a69-971500188b19/positions/34f6344f-015e-11e6-9464-e4de0000006c",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
    "type": "demandposition",
    "mediaType": "application/json"
  },
  "id": "34f6344f-015e-11e6-9464-e4de0000006c",
  "accountId": "84e60e93-f504-11e5-8a84-bae500000008",
  "quantity": 20,
  "sum": 200,
  "discount": 0,
  "vat": 21,
  "vatEnabled": true,
  "assortment": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/be903062-f504-11e5-8a84-bae50000019a",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
      "type": "product",
      "mediaType": "application/json",
      "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=e64d0a86-2a99-11e9-ac12-000c00000041"
    }
  }
}
```

### Изменить позицию 
Запрос на обновление отдельной позиции Отгрузки. Для обновления позиции нет каких-либо
 обязательных для указания в теле запроса полей. Только те, что вы желаете обновить.
 
При обновлении списка кодов маркировки учитывать, что их количество может отличаться от фактического количества единиц продукции. 
 Для изменения количества единиц продукции необходимо использовать параметр **quantity**.

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Отгрузки.|
|**positionID**|  `string` (required) *Example: 34f6344f-015e-11e6-9464-e4de0000006c* id позиции Отгрузки.|
 
> Пример запроса на обновление отдельной позиции в Отгрузке.

```shell
  curl -X PUT
    "https://online.moysklad.ru/api/remap/1.2/entity/demand/7944ef04-f831-11e5-7a69-971500188b19/positions/34f6344f-015e-11e6-9464-e4de0000006c"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "quantity": 111,
            "price": 26332700,
            "discount": 0,
            "vat": 18,
            "assortment": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/eeef177f-f648-11e5-8a84-bae50000007a",
                "type": "product",
                "mediaType": "application/json"
              }
            }
          }'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление обновленной позиции Отгрузки.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/demand/7944ef04-f831-11e5-7a69-971500188b19/positions/34f6344f-015e-11e6-9464-e4de0000006c",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/demand/metadata",
    "type": "demandposition",
    "mediaType": "application/json"
  },
  "id": "34f6344f-015e-11e6-9464-e4de0000006c",
  "accountId": "84e60e93-f504-11e5-8a84-bae500000008",
  "quantity": 111,
  "price": 26332700,
  "discount": 0,
  "vat": 18,
  "vatEnabled": true,
  "assortment": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/eeef177f-f648-11e5-8a84-bae50000007a",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
      "type": "product",
      "mediaType": "application/json",
      "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=e64d0a86-2a99-11e9-ac12-000c00000041"
    }
  }
}
```

### Удалить позицию 

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Отгрузки.|
|**positionID**|  `string` (required) *Example: 34f6344f-015e-11e6-9464-e4de0000006c* id позиции Отгрузки.|

> Запрос на удаление отдельной позиции Отгрузки с указанным id.

```shell
curl -X DELETE
  "https://online.moysklad.ru/api/remap/1.2/entity/demand/7944ef04-f831-11e5-7a69-971500188b19/positions/34f6344f-015e-11e6-9464-e4de0000006c"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешное удаление позиции Отгрузки.
