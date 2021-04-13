## Возврат поставщику
Средствами JSON API можно создавать и обновлять сведения о Возвратах поставщикам, запрашивать списки Возвратов поставщикам и сведения по отдельным Возвратам поставщикам. Позициями Возвратов поставщикам можно управлять как в составе отдельного Возврата, так и отдельно - с помощью специальных ресурсов для управления позициями Возврата поставщику. Кодом сущности для Возврата поставщику в составе JSON API является ключевое слово **purchasereturn**.
### Возвраты поставщикам 
#### Атрибуты сущности

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные Возврата поставщику|&mdash;|да
|**id**                 |UUID|ID Возврата поставщику|Только для чтения|да
|**accountId**          |UUID| ID учетной записи|Только для чтения|да
|**syncId**             |UUID|ID синхронизации. После заполнения недоступен для изменения|&mdash;|нет
|**updated**            |DateTime|Момент последнего обновления Возврата поставщику|Только для чтения|да
|**deleted**            |DateTime|Момент последнего удаления Возврата поставщику|Только для чтения|нет
|**name**               |String(255)|Наименование Возврата поставщику|&mdash;|да
|**description**        |String(4096)|Комментарий Возврата поставщику |&mdash;|нет
|**externalCode**       |String(255)|Внешний код Возврата поставщику |&mdash;| да
|**moment**             |DateTime|Дата Счета|&mdash;|да
|**applicable**         |Boolean|Отметка о проведении|&mdash;|да
|**vatEnabled**         |Boolean|Учитывается ли НДС|&mdash;|да
|**vatIncluded**        |Boolean| Включен ли НДС в цену|&mdash;|нет
|**sum**                |Int|Сумма Возврата поставщику в копейках|Только для чтения|да
|**project**            |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные проекта|&mdash;|нет
|**rate**               |Object|Валюта. [Подробнее тут](../documents/#dokumenty-obschie-swedeniq-valuta-w-dokumentah)|&mdash;|да
|**owner**              |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Владелец (Сотрудник)|&mdash;|да
|**shared**             |Boolean|Общий доступ|&mdash;|да
|**group**              |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Отдел сотрудника|&mdash;|да
|**organization**       |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные юрлица|&mdash;|да
|**agent**              |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные контрагента|Необходимое при создании|да
|**store**              |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные склада|Необходимое при создании|да
|**contract**              |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные договора|&mdash;|нет
|**state**              |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные статуса Возврата поставщику |&mdash;|нет
|**organizationAccount**|[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные счета юрлица|&mdash;|нет
|**agentAccount**       |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные счета контрагента|&mdash;|нет
|**attributes**         |Array(Object)|Коллекция метаданных доп. полей. [Поля объекта](../#mojsklad-json-api-obschie-swedeniq-rabota-s-dopolnitel-nymi-polqmi) |&mdash;|нет
|**files**              |MetaArray|Массив метаданных [Файлов](../dictionaries/#suschnosti-fajly) (Максимальное количество файлов - 100)|&mdash;|да
|**created**            |DateTime|Дата создания|Только для чтения|да
|**printed**            |Boolean|Напечатан ли документ|Только для чтения|да
|**published**          |Boolean|Опубликован ли документ|Только для чтения|да
|**vatSum**                |Float|Сумма включая НДС|&mdash;|да

#### Связи с другими документами
|Название          | Описание  |
| ------------------------------ |:---------------------------|
|**positions** |Ссылка на позиции Возврата поставщику в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye)
|**supply** | Ссылка на приемку, по которой произошел возврат в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye) Поле является необходимым для возврата с основанием.
|**factureOut** | Ссылка на Счет-фактуру выданный в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye)
|**factureIn** | Ссылка на Счет-фактуру полученный в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye)
|**payedSum** | Сумма входящих платежей по возврату поставщику
|**payments** | Массив ссылок на связанные платежи в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye)

#### Позиции Возврата поставщику
Позиции Возврата поставщику - это список товаров/услуг/модификаций/серий.
Объект позиции Возврата поставщику содержит следующие поля:

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

Значение данного атрибута игнорируется, если товар позиции не находится на серийном учете.
В ином случае количество товаров в позиции будет равно количеству серийных номеров, переданных в значении атрибута.

С позициями можно работать с помощью специальных [ресурсов для управления позициями Возврата поставщику](../documents/#dokumenty-vozwrat-postawschiku-pozicii-vozwrata-postawschiku),
а также в составе отдельного Возврата поставщику. При работе в составе отдельного Возврата поставщику,
вы можете отправлять запросы на создание отдельного Возврата поставщику с включенным в тело запроса
массивом позиций Возврата поставщику. Если количество позиций превышает максимально допустимое, то для
дальнейшего пополнения позиций нужно будет работать со специальным ресурсом "Позиции Возврата поставщику".
Также, при работе в составе отдельного Возврата поставщику, можно отправлять запросы на обновление списка позиций
с включенным в тело запроса массивом позиций Возврата поставщику. При этом важно помнить, что коллекция позиций будет
восприниматься как "все позиции Возврата поставщику" и полностью заменит уже существующую коллекцию при обновлении объекта - лишние
позиции будут удалены, новые добавлены, существующие - изменены.

О работе с доп. полями Возвратов поставщикамых возвратов можно прочитать [здесь](../#mojsklad-json-api-obschie-swedeniq-rabota-s-dopolnitel-nymi-polqmi)

### Получить Возвраты поставщикам 
Запрос всех Возвратов поставщикам на данной учетной записи.
Результат: Объект JSON, включающий в себя поля:

| Название  | Тип | Описание                    |
| --------- |:----|:----------------------------|
**meta** |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные о выдаче,
**context** | [Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye) | Метаданные о сотруднике, выполнившем запрос.
**rows** |Array(Object)|Массив JSON объектов, представляющих собой Возвраты поставщикам.

**Параметры**

| Параметр                | Описание  |
| ------------------------------ |:---------------------------|
|**limit** |  `number` (optional) **Default: 1000** *Example: 1000* Максимальное количество сущностей для извлечения.`Допустимые значения 1 - 1000`.|
|**offset** |  `number` (optional) **Default: 0** *Example: 40* Отступ в выдаваемом списке сущностей.|

> Получить Возвраты поставщикам

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление списка Возвратов поставщикам.

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
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata",
    "type": "purchasereturn",
    "mediaType": "application/json",
    "size": 4,
    "limit": 1000,
    "offset": 0
  },
  "rows": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/b875cc8f-313f-11e6-8a84-bae500000093",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata",
        "type": "purchasereturn",
        "mediaType": "application/json"
      },
      "id": "b875cc8f-313f-11e6-8a84-bae500000093",
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
      "updated": "2016-06-13 11:20:55",
      "name": "00001",
      "externalCode": "E4l6sMtVixklOjgfK6VQt3",
      "moment": "2016-06-13 11:20:00",
      "applicable": true,
      "printed": true,
      "published": true,
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
      "organization": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
          "type": "organization",
          "mediaType": "application/json"
        }
      },
      "store": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/faf3ff5b-2e58-11e6-8a84-bae500000050",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
          "type": "store",
          "mediaType": "application/json"
        }
      },
      "agent": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/faf44002-2e58-11e6-8a84-bae500000053",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
          "type": "counterparty",
          "mediaType": "application/json"
        }
      },
      "organizationAccount": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e/accounts/fae39d66-2e58-11e6-8a84-bae50000004f",
          "type": "account",
          "mediaType": "application/json"
        }
      },
      "vatEnabled": true,
      "vatIncluded": true,
      "positions": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/b875cc8f-313f-11e6-8a84-bae500000093/positions",
          "type": "purchasereturnposition",
          "mediaType": "application/json",
          "size": 1,
          "limit": 1000,
          "offset": 0
        }
      },
      "supply": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/supply/b1008773-313f-11e6-8a84-bae500000089",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/supply/metadata",
          "type": "supply",
          "mediaType": "application/json"
        }
      },
      "payedSum": 0
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/d43161ea-3140-11e6-8a84-bae5000000c6",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata",
        "type": "purchasereturn",
        "mediaType": "application/json"
      },
      "id": "d43161ea-3140-11e6-8a84-bae5000000c6",
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
      "updated": "2016-06-13 11:28:34",
      "name": "00002",
      "externalCode": "-5xto6PjiGhuL8RAky-9c3",
      "moment": "2016-06-13 11:22:00",
      "applicable": true,
      "printed": true,
      "published": true,
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
      "sum": 273000,
      "organization": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
          "type": "organization",
          "mediaType": "application/json"
        }
      },
      "store": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/faf3ff5b-2e58-11e6-8a84-bae500000050",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
          "type": "store",
          "mediaType": "application/json"
        }
      },
      "agent": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/faf44002-2e58-11e6-8a84-bae500000053",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
          "type": "counterparty",
          "mediaType": "application/json"
        }
      },
      "organizationAccount": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e/accounts/fae39d66-2e58-11e6-8a84-bae50000004f",
          "type": "account",
          "mediaType": "application/json"
        }
      },
      "vatEnabled": true,
      "vatIncluded": true,
      "positions": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/d43161ea-3140-11e6-8a84-bae5000000c6/positions",
          "type": "purchasereturnposition",
          "mediaType": "application/json",
          "size": 2,
          "limit": 1000,
          "offset": 0
        }
      },
      "supply": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/supply/f39a60f5-313f-11e6-8a84-bae5000000b4",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/supply/metadata",
          "type": "supply",
          "mediaType": "application/json"
        }
      },
      "payedSum": 0
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/dc194230-41bd-11e6-8a84-bae5000000a9",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata",
        "type": "purchasereturn",
        "mediaType": "application/json"
      },
      "id": "dc194230-41bd-11e6-8a84-bae5000000a9",
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
      "updated": "2016-07-04 11:03:57",
      "name": "00003",
      "externalCode": "-SmYzmhBjSFQBveIJQ6uV0",
      "moment": "2016-07-04 11:03:00",
      "applicable": true,
      "printed": true,
      "published": true,
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
      "sum": 28000,
      "organization": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
          "type": "organization",
          "mediaType": "application/json"
        }
      },
      "store": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/faf3ff5b-2e58-11e6-8a84-bae500000050",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
          "type": "store",
          "mediaType": "application/json"
        }
      },
      "contract": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/contract/2b34d43f-3f52-11e6-8a84-bae500000066",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/contract/metadata",
          "type": "contract",
          "mediaType": "application/json"
        }
      },
      "project": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/project/722e39f0-313e-11e6-8a84-bae500000008",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/project/metadata",
          "type": "project",
          "mediaType": "application/json"
        }
      },
      "agent": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/1489a08d-32ca-11e6-8a84-bae50000000d",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
          "type": "counterparty",
          "mediaType": "application/json"
        }
      },
      "organizationAccount": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e/accounts/fae39d66-2e58-11e6-8a84-bae50000004f",
          "type": "account",
          "mediaType": "application/json"
        }
      },
      "agentAccount": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/1489a08d-32ca-11e6-8a84-bae50000000d/accounts/1489ad8d-32ca-11e6-8a84-bae50000000e",
          "type": "account",
          "mediaType": "application/json"
        }
      },
      "vatEnabled": true,
      "vatIncluded": true,
      "positions": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/dc194230-41bd-11e6-8a84-bae5000000a9/positions",
          "type": "purchasereturnposition",
          "mediaType": "application/json",
          "size": 7,
          "limit": 1000,
          "offset": 0
        }
      },
      "supply": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/supply/ceec2ca6-41bd-11e6-8a84-bae500000097",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/supply/metadata",
          "type": "supply",
          "mediaType": "application/json"
        }
      },
      "payedSum": 0
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/e699b298-41bd-11e6-8a84-bae5000000ba",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata",
        "type": "purchasereturn",
        "mediaType": "application/json"
      },
      "id": "e699b298-41bd-11e6-8a84-bae5000000ba",
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
      "updated": "2016-07-04 11:04:15",
      "name": "00004",
      "externalCode": "tBSZzXSgggWNL5MZ7IrYE2",
      "moment": "2016-07-04 11:04:00",
      "applicable": true,
      "printed": true,
      "published": true,
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
      "sum": 43156000,
      "organization": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
          "type": "organization",
          "mediaType": "application/json"
        }
      },
      "store": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/faf3ff5b-2e58-11e6-8a84-bae500000050",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
          "type": "store",
          "mediaType": "application/json"
        }
      },
      "contract": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/contract/91287d9a-41bc-11e6-8a84-bae500000082",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/contract/metadata",
          "type": "contract",
          "mediaType": "application/json"
        }
      },
      "project": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/project/722e39f0-313e-11e6-8a84-bae500000008",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/project/metadata",
          "type": "project",
          "mediaType": "application/json"
        }
      },
      "agent": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/14bfc067-32ca-11e6-8a84-bae50000003f",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
          "type": "counterparty",
          "mediaType": "application/json"
        }
      },
      "organizationAccount": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e/accounts/fae39d66-2e58-11e6-8a84-bae50000004f",
          "type": "account",
          "mediaType": "application/json"
        }
      },
      "vatEnabled": true,
      "vatIncluded": true,
      "positions": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/e699b298-41bd-11e6-8a84-bae5000000ba/positions",
          "type": "purchasereturnposition",
          "mediaType": "application/json",
          "size": 7,
          "limit": 1000,
          "offset": 0
        }
      },
      "supply": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/supply/80d04ebc-41bd-11e6-8a84-bae500000085",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/supply/metadata",
          "type": "supply",
          "mediaType": "application/json"
        }
      },
      "payedSum": 0
    }
  ]
}
```

### Создать Возврат поставщику 
Обязательные поля при создании нового Возврата поставщику:

+ **name** - Номер возврата
+ **organization** - Ссылка на ваше юрлицо в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye)
+ **store** - Ссылка на склад в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye)
+ **supply** - Ссылка на приемку, по которой произошел возврат в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye), обязательное поле только для возврата по основанию
+ **agent** - Ссылка на контрагента в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye)
Контрагент, указанный в запросе на создание возврата, должен совпадать с контрагентом, указанном в документе,
по которому создается возврат.

При создании возврата:

+ При создании возврата без основания поле **supply** указывать не нужно
+ Контрагент в возврате и в документе, по которому он создается, должны совпадать
+ Валюта и юрлицо в возврате и в документе так же должны совпадать
+ При передаче коллекции **positions** в теле запроса на создание возврата, передаваемые позиции
должны соответствовать позициям в документе. Различие может быть только в количестве товара в позиции
(меньшее либо равное количеству в документе). Нельзя передать позиции, которых нет в документе.

> Пример создания нового Возврата поставщику на основании приемки.

```shell
  curl -X POST
    "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "name": "77887",
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
            "description": "Возврат поставщику созданный через API",
            "code": "8865255398",
            "externalCode": "fruitsareawesome124",
            "moment": "2016-11-21 14:37:00",
            "applicable": true,
            "organization": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
                "type": "organization",
                "mediaType": "application/json"
              }
            },
            "agent": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/147c1f1b-32ca-11e6-8a84-bae500000004",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
                "type": "counterparty",
                "mediaType": "application/json"
              }
            },
            "store": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/faf3ff5b-2e58-11e6-8a84-bae500000050",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
                "type": "store",
                "mediaType": "application/json"
              }
            },
            "attributes": [
              {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/attributes/4fc7e124-41be-11e6-8a84-bae5000000cb",
                  "type": "attributemetadata",
                  "mediaType": "application/json"
                },
                "value": "деталь"
              },
              {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/attributes/4fc7e7e7-41be-11e6-8a84-bae5000000cc",
                  "type": "attributemetadata",
                  "mediaType": "application/json"
                },
                "value": false
              }
            ],
            "positions": [
              {
                "quantity": 1,
                "price": 1241200,
                "discount": 0,
                "vat": 0,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/e6447ee7-3303-11e6-8a84-bae5000149c2",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                    "type": "product",
                    "mediaType": "application/json"
                  }
                }
              },
              {
                "quantity": 1,
                "price": 24100,
                "discount": 0,
                "vat": 0,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/e8517bc4-3303-11e6-8a84-bae500014de1",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                    "type": "product",
                    "mediaType": "application/json"
                  }
                }
              },
              {
                "quantity": 1,
                "price": 421000,
                "discount": 0,
                "vat": 0,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/service/6767bc73-3d19-11e6-8a84-bae500000002",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/service/metadata",
                    "type": "service",
                    "mediaType": "application/json"
                  }
                }
              },
              {
                "quantity": 1,
                "price": 2421000,
                "discount": 0,
                "vat": 0,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/e8563cc5-3303-11e6-8a84-bae500014df0",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                    "type": "product",
                    "mediaType": "application/json"
                  }
                }
              }
            ],
            "supply": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/supply/7585391b-41c0-11e6-8a84-bae5000000de",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/supply/metadata",
                "type": "supply",
                "mediaType": "application/json"
              }
            }
          }'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление созданного Возврата поставщику.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/6d5371fc-41c1-11e6-8a84-bae50000001c",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata",
    "type": "purchasereturn",
    "mediaType": "application/json"
  },
  "id": "6d5371fc-41c1-11e6-8a84-bae50000001c",
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
  "updated": "2016-07-04 11:29:29",
  "name": "77887",
  "description": "Возврат поставщику созданный через API",
  "code": "8865255398",
  "externalCode": "fruitsareawesome124",
  "moment": "2016-11-21 14:37:00",
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
  "sum": 4107300,
  "organization": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
      "type": "organization",
      "mediaType": "application/json"
    }
  },
  "store": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/faf3ff5b-2e58-11e6-8a84-bae500000050",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
      "type": "store",
      "mediaType": "application/json"
    }
  },
  "agent": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/147c1f1b-32ca-11e6-8a84-bae500000004",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
      "mediaType": "application/json"
    }
  },
  "organizationAccount": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e/accounts/fae39d66-2e58-11e6-8a84-bae50000004f",
      "type": "account",
      "mediaType": "application/json"
    }
  },
  "agentAccount": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/147c1f1b-32ca-11e6-8a84-bae500000004/accounts/147c3231-32ca-11e6-8a84-bae500000005",
      "type": "account",
      "mediaType": "application/json"
    }
  },
  "attributes": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/attributes/4fc7e124-41be-11e6-8a84-bae5000000cb",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "4fc7e124-41be-11e6-8a84-bae5000000cb",
      "name": "AttributeName1",
      "type": "boolean",
      "value": false
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/attributes/4fc7e7e7-41be-11e6-8a84-bae5000000cc",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "4fc7e7e7-41be-11e6-8a84-bae5000000cc",
      "name": "AttributeName2",
      "type": "text",
      "value": "деталь"
    }
  ],
  "vatEnabled": true,
  "vatIncluded": true,
  "created": "2007-02-07 17:16:41",
  "printed": true,
  "published": true,
  "positions": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/6d5371fc-41c1-11e6-8a84-bae50000001c/positions",
      "type": "purchasereturnposition",
      "mediaType": "application/json",
      "size": 4,
      "limit": 1000,
      "offset": 0
    }
  },
  "supply": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/supply/7585391b-41c0-11e6-8a84-bae5000000de",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/supply/metadata",
      "type": "supply",
      "mediaType": "application/json"
    }
  },
  "payedSum": 0
}
```

> Пример создания нового Возврата поставщику без основания.

```shell
  curl -X POST
    "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "name": "77887",
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
            "description": "Возврат поставщику созданный через API",
            "code": "8865255398",
            "externalCode": "fruitsareawesome124",
            "moment": "2016-11-21 14:37:00",
            "applicable": true,
            "organization": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
                "type": "organization",
                "mediaType": "application/json"
              }
            },
            "agent": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/147c1f1b-32ca-11e6-8a84-bae500000004",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
                "type": "counterparty",
                "mediaType": "application/json"
              }
            },
            "store": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/faf3ff5b-2e58-11e6-8a84-bae500000050",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
                "type": "store",
                "mediaType": "application/json"
              }
            },
            "attributes": [
              {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/attributes/4fc7e124-41be-11e6-8a84-bae5000000cb",
                  "type": "attributemetadata",
                  "mediaType": "application/json"
                },
                "value": "деталь"
              },
              {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/attributes/4fc7e7e7-41be-11e6-8a84-bae5000000cc",
                  "type": "attributemetadata",
                  "mediaType": "application/json"
                },
                "value": false
              }
            ],
            "positions": [
              {
                "quantity": 1,
                "price": 1241200,
                "discount": 0,
                "vat": 0,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/e6447ee7-3303-11e6-8a84-bae5000149c2",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                    "type": "product",
                    "mediaType": "application/json"
                  }
                }
              },
              {
                "quantity": 1,
                "price": 24100,
                "discount": 0,
                "vat": 0,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/e8517bc4-3303-11e6-8a84-bae500014de1",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                    "type": "product",
                    "mediaType": "application/json"
                  }
                }
              },
              {
                "quantity": 1,
                "price": 421000,
                "discount": 0,
                "vat": 0,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/service/6767bc73-3d19-11e6-8a84-bae500000002",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/service/metadata",
                    "type": "service",
                    "mediaType": "application/json"
                  }
                }
              },
              {
                "quantity": 1,
                "price": 2421000,
                "discount": 0,
                "vat": 0,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/e8563cc5-3303-11e6-8a84-bae500014df0",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                    "type": "product",
                    "mediaType": "application/json"
                  }
                }
              }
            ]
          }'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление созданного Возврата поставщику.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/6d5371fc-41c1-11e6-8a84-bae50000001c",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata",
    "type": "purchasereturn",
    "mediaType": "application/json"
  },
  "id": "6d5371fc-41c1-11e6-8a84-bae50000001c",
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
  "updated": "2016-07-04 11:29:29",
  "name": "77887",
  "description": "Возврат поставщику созданный через API",
  "code": "8865255398",
  "externalCode": "fruitsareawesome124",
  "moment": "2016-11-21 14:37:00",
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
  "sum": 4107300,
  "organization": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
      "type": "organization",
      "mediaType": "application/json"
    }
  },
  "store": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/faf3ff5b-2e58-11e6-8a84-bae500000050",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
      "type": "store",
      "mediaType": "application/json"
    }
  },
  "agent": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/147c1f1b-32ca-11e6-8a84-bae500000004",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
      "mediaType": "application/json"
    }
  },
  "organizationAccount": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e/accounts/fae39d66-2e58-11e6-8a84-bae50000004f",
      "type": "account",
      "mediaType": "application/json"
    }
  },
  "agentAccount": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/147c1f1b-32ca-11e6-8a84-bae500000004/accounts/147c3231-32ca-11e6-8a84-bae500000005",
      "type": "account",
      "mediaType": "application/json"
    }
  },
  "attributes": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/attributes/4fc7e124-41be-11e6-8a84-bae5000000cb",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "4fc7e124-41be-11e6-8a84-bae5000000cb",
      "name": "AttributeName1",
      "type": "boolean",
      "value": false
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/attributes/4fc7e7e7-41be-11e6-8a84-bae5000000cc",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "4fc7e7e7-41be-11e6-8a84-bae5000000cc",
      "name": "AttributeName2",
      "type": "text",
      "value": "деталь"
    }
  ],
  "vatEnabled": true,
  "vatIncluded": true,
  "created": "2007-02-07 17:16:41",
  "printed": true,
  "published": true,
  "positions": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/6d5371fc-41c1-11e6-8a84-bae50000001c/positions",
      "type": "purchasereturnposition",
      "mediaType": "application/json",
      "size": 4,
      "limit": 100,
      "offset": 0
    }
  },
  "payedSum": 0
}
```

### Массовое создание и обновление Возвратов поставщику 
[Массовое создание и обновление](../#mojsklad-json-api-obschie-swedeniq-sozdanie-i-obnowlenie-neskol-kih-ob-ektow) Возвратов поставщику.
В теле запроса нужно передать массив, содержащий JSON представления Возвратов поставщику, которые вы хотите создать или обновить.
Обновляемые Возвраты поставщику должны содержать идентификатор в виде метаданных.

> Пример создания и обновления нескольких Возвратов поставщику

```shell
  curl -X POST
    "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '[
            {
              "name": "77887",
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
              "description": "Возврат поставщику созданный через API",
              "code": "8865255398",
              "externalCode": "fruitsareawesome124",
              "moment": "2016-11-21 14:37:00",
              "applicable": true,
              "organization": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
                  "type": "organization",
                  "mediaType": "application/json"
                }
              },
              "agent": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/147c1f1b-32ca-11e6-8a84-bae500000004",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
                  "type": "counterparty",
                  "mediaType": "application/json"
                }
              },
              "store": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/faf3ff5b-2e58-11e6-8a84-bae500000050",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
                  "type": "store",
                  "mediaType": "application/json"
                }
              },
              "attributes": [
                {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/attributes/4fc7e124-41be-11e6-8a84-bae5000000cb",
                    "type": "attributemetadata",
                    "mediaType": "application/json"
                  },
                  "value": "деталь"
                },
                {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/attributes/4fc7e7e7-41be-11e6-8a84-bae5000000cc",
                    "type": "attributemetadata",
                    "mediaType": "application/json"
                  },
                  "value": false
                }
              ],
              "positions": [
                {
                  "quantity": 1,
                  "price": 1241200,
                  "discount": 0,
                  "vat": 0,
                  "assortment": {
                    "meta": {
                      "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/e6447ee7-3303-11e6-8a84-bae5000149c2",
                      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                      "type": "product",
                      "mediaType": "application/json"
                    }
                  }
                },
                {
                  "quantity": 1,
                  "price": 24100,
                  "discount": 0,
                  "vat": 0,
                  "assortment": {
                    "meta": {
                      "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/e8517bc4-3303-11e6-8a84-bae500014de1",
                      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                      "type": "product",
                      "mediaType": "application/json"
                    }
                  }
                },
                {
                  "quantity": 1,
                  "price": 421000,
                  "discount": 0,
                  "vat": 0,
                  "assortment": {
                    "meta": {
                      "href": "https://online.moysklad.ru/api/remap/1.2/entity/service/6767bc73-3d19-11e6-8a84-bae500000002",
                      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/service/metadata",
                      "type": "service",
                      "mediaType": "application/json"
                    }
                  }
                },
                {
                  "quantity": 1,
                  "price": 2421000,
                  "discount": 0,
                  "vat": 0,
                  "assortment": {
                    "meta": {
                      "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/e8563cc5-3303-11e6-8a84-bae500014df0",
                      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                      "type": "product",
                      "mediaType": "application/json"
                    }
                  }
                }
              ],
              "supply": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/supply/7585391b-41c0-11e6-8a84-bae5000000de",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/supply/metadata",
                  "type": "supply",
                  "mediaType": "application/json"
                }
              }
            },
            {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/6d5371fc-41c1-11e6-8a84-bae50000001c",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata",
                "type": "purchasereturn",
                "mediaType": "application/json"
              },
              "name": "763457",
              "owner": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/1205364b-7f01-455a-a1b5-4ba0988c8308",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
                  "type": "employee",
                  "mediaType": "application/json"
                }
              },
              "shared": true,
              "group": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/group/348d910b-6dc0-483f-b916-2237bc54a04e",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/group/metadata",
                  "type": "group",
                  "mediaType": "application/json"
                }
              },
              "description": "Возврат поставщику созданный и обновленный через API",
              "code": "8865255398",
              "externalCode": "fruitsareawesome!!!",
              "moment": "2016-11-21 14:27:00",
              "applicable": false,
              "state": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/states/69e39d04-41be-11e6-8a84-bae5000000d2",
                  "type": "state",
                  "mediaType": "application/json"
                }
              },
              "attributes": [
                {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/attributes/4fc7e124-41be-11e6-8a84-bae5000000cb",
                    "type": "attributemetadata",
                    "mediaType": "application/json"
                  },
                  "value": true
                }
              ],
              "positions": [
                {
                  "quantity": 1,
                  "price": 1241200,
                  "discount": 0,
                  "vat": 0,
                  "assortment": {
                    "meta": {
                      "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/e6447ee7-3303-11e6-8a84-bae5000149c2",
                      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                      "type": "product",
                      "mediaType": "application/json"
                    }
                  }
                },
                {
                  "quantity": 1,
                  "price": 24100,
                  "discount": 0,
                  "vat": 0,
                  "assortment": {
                    "meta": {
                      "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/e8517bc4-3303-11e6-8a84-bae500014de1",
                      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                      "type": "product",
                      "mediaType": "application/json"
                    }
                  }
                },
                {
                  "quantity": 1,
                  "price": 421000,
                  "discount": 0,
                  "vat": 0,
                  "assortment": {
                    "meta": {
                      "href": "https://online.moysklad.ru/api/remap/1.2/entity/service/6767bc73-3d19-11e6-8a84-bae500000002",
                      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/service/metadata",
                      "type": "service",
                      "mediaType": "application/json"
                    }
                  }
                },
                {
                  "quantity": 1,
                  "price": 2421000,
                  "discount": 0,
                  "vat": 0,
                  "assortment": {
                    "meta": {
                      "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/e8563cc5-3303-11e6-8a84-bae500014df0",
                      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                      "type": "product",
                      "mediaType": "application/json"
                    }
                  }
                },
                {
                  "quantity": 1,
                  "price": 263000,
                  "discount": 0,
                  "vat": 0,
                  "assortment": {
                    "meta": {
                      "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/20485cfd-2e62-11e6-8a84-bae500000112",
                      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                      "type": "product",
                      "mediaType": "application/json"
                    }
                  }
                }
              ]
            }
          ]'  
```

> Response 200 (application/json)
Успешный запрос. Результат - массив JSON представлений созданных и обновленных Возвратов поставщику.

```json
[
  {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/6d5371fc-41c1-11e6-8a84-bae50000001c",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata",
      "type": "purchasereturn",
      "mediaType": "application/json"
    },
    "id": "6d5371fc-41c1-11e6-8a84-bae50000001c",
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
    "updated": "2016-07-04 11:29:29",
    "name": "77887",
    "description": "Возврат поставщику созданный через API",
    "code": "8865255398",
    "externalCode": "fruitsareawesome124",
    "moment": "2016-11-21 14:37:00",
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
    "sum": 4107300,
    "organization": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
        "type": "organization",
        "mediaType": "application/json"
      }
    },
    "store": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/faf3ff5b-2e58-11e6-8a84-bae500000050",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
        "type": "store",
        "mediaType": "application/json"
      }
    },
    "agent": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/147c1f1b-32ca-11e6-8a84-bae500000004",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
        "type": "counterparty",
        "mediaType": "application/json"
      }
    },
    "organizationAccount": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e/accounts/fae39d66-2e58-11e6-8a84-bae50000004f",
        "type": "account",
        "mediaType": "application/json"
      }
    },
    "agentAccount": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/147c1f1b-32ca-11e6-8a84-bae500000004/accounts/147c3231-32ca-11e6-8a84-bae500000005",
        "type": "account",
        "mediaType": "application/json"
      }
    },
    "attributes": [
      {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/attributes/4fc7e124-41be-11e6-8a84-bae5000000cb",
          "type": "attributemetadata",
          "mediaType": "application/json"
        },
        "id": "4fc7e124-41be-11e6-8a84-bae5000000cb",
        "name": "AttributeName1",
        "type": "boolean",
        "value": false
      },
      {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/attributes/4fc7e7e7-41be-11e6-8a84-bae5000000cc",
          "type": "attributemetadata",
          "mediaType": "application/json"
        },
        "id": "4fc7e7e7-41be-11e6-8a84-bae5000000cc",
        "name": "AttributeName2",
        "type": "text",
        "value": "деталь"
      }
    ],
    "vatEnabled": true,
    "vatIncluded": true,
    "created": "2007-02-07 17:16:41",
    "printed": true,
    "published": true,
    "positions": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/6d5371fc-41c1-11e6-8a84-bae50000001c/positions",
        "type": "purchasereturnposition",
        "mediaType": "application/json",
        "size": 4,
        "limit": 1000,
        "offset": 0
      }
    },
    "supply": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/supply/7585391b-41c0-11e6-8a84-bae5000000de",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/supply/metadata",
        "type": "supply",
        "mediaType": "application/json"
      }
    },
    "payedSum": 0
  },
  {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/6d5371fc-41c1-11e6-8a84-bae50000001c",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata",
      "type": "purchasereturn",
      "mediaType": "application/json"
    },
    "id": "6d5371fc-41c1-11e6-8a84-bae50000001c",
    "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
    "owner": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/1205364b-7f01-455a-a1b5-4ba0988c8308",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
        "type": "employee",
        "mediaType": "application/json"
      }
    },
    "shared": true,
    "group": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/group/348d910b-6dc0-483f-b916-2237bc54a04e",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/group/metadata",
        "type": "group",
        "mediaType": "application/json"
      }
    },
    "updated": "2016-07-04 11:35:26",
    "name": "763457",
    "description": "Возврат поставщику созданный и обновленный через API",
    "code": "8865255398",
    "externalCode": "fruitsareawesome!!!",
    "moment": "2016-11-21 14:27:00",
    "applicable": false,
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
    "sum": 4370300,
    "organization": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
        "type": "organization",
        "mediaType": "application/json"
      }
    },
    "store": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/faf3ff5b-2e58-11e6-8a84-bae500000050",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
        "type": "store",
        "mediaType": "application/json"
      }
    },
    "agent": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/147c1f1b-32ca-11e6-8a84-bae500000004",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
        "type": "counterparty",
        "mediaType": "application/json"
      }
    },
    "state": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/states/69e39d04-41be-11e6-8a84-bae5000000d2",
        "type": "state",
        "mediaType": "application/json"
      }
    },
    "organizationAccount": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e/accounts/fae39d66-2e58-11e6-8a84-bae50000004f",
        "type": "account",
        "mediaType": "application/json"
      }
    },
    "agentAccount": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/147c1f1b-32ca-11e6-8a84-bae500000004/accounts/147c3231-32ca-11e6-8a84-bae500000005",
        "type": "account",
        "mediaType": "application/json"
      }
    },
    "attributes": [
      {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/attributes/4fc7e124-41be-11e6-8a84-bae5000000cb",
          "type": "attributemetadata",
          "mediaType": "application/json"
        },
        "id": "4fc7e124-41be-11e6-8a84-bae5000000cb",
        "name": "AttributeName1",
        "type": "boolean",
        "value": true
      },
      {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/attributes/4fc7e7e7-41be-11e6-8a84-bae5000000cc",
          "type": "attributemetadata",
          "mediaType": "application/json"
        },
        "id": "4fc7e7e7-41be-11e6-8a84-bae5000000cc",
        "name": "AttributeName2",
        "type": "text",
        "value": "деталь"
      }
    ],
    "vatEnabled": true,
    "vatIncluded": true,
    "created": "2007-02-07 17:16:41",
    "printed": true,
    "published": true,
    "positions": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/6d5371fc-41c1-11e6-8a84-bae50000001c/positions",
        "type": "purchasereturnposition",
        "mediaType": "application/json",
        "size": 5,
        "limit": 1000,
        "offset": 0
      }
    },
    "supply": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/supply/7585391b-41c0-11e6-8a84-bae5000000de",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/supply/metadata",
        "type": "supply",
        "mediaType": "application/json"
      }
    },
    "payedSum": 0
  }
]
```

### Удалить Возврат поставщику

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Возврата поставщику.|
 
> Запрос на удаление Возврата поставщику с указанным id.

```shell
curl -X DELETE
  "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/7944ef04-f831-11e5-7a69-971500188b19"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешное удаление Возврата поставщику.

### Массовое удаление Возвратов поставщикам

В теле запроса нужно передать массив, содержащий JSON метаданных Возвратов поставщикам, которые вы хотите удалить.


> Запрос на массовое удаление Возвратов поставщикам. 

```shell
curl -X POST
  "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/delete"
  -H "Authorization: Basic <Credentials>"
  -H "Content-Type: application/json"
  -d '[
        {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/7944ef04-f831-11e5-7a69-971500188b1",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata",
            "type": "purchasereturn",
            "mediaType": "application/json"
        },
        {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/7944ef04-f831-11e5-7a69-971500188b2",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata",
            "type": "purchasereturn",
            "mediaType": "application/json"
        }
      ]'
```        

> Успешный запрос. Результат - JSON информация об удалении Возвратов поставщикам.

```json
[
  {
    "info":"Сущность 'purchasereturn' с UUID: 7944ef04-f831-11e5-7a69-971500188b1 успешно удалена"
  },
  {
    "info":"Сущность 'purchasereturn' с UUID: 7944ef04-f831-11e5-7a69-971500188b2 успешно удалена"
  }
]
``` 

### Метаданные Возвратов поставщикам 
#### Метаданные Возвратов поставщикам 
Запрос на получение метаданных Возвратов поставщикам. Результат - объект JSON, включающий в себя:

| Параметр                | Описание  |
| ------------------------------ |:---------------------------|
| **meta**         | Ссылка на метаданные Возвратов поставщикам|
| **attributes**   | Массив объектов доп. полей Возвратов поставщикам в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye)|
| **states**       | Массив статусов Возвратов поставщикам|
| **createShared** | создавать новые Возвраты поставщикам с меткой "Общий"|

Структура отдельного объекта, представляющего доп. поле подробно описана в разделе [Работа с дополнительными полями](../#mojsklad-json-api-obschie-swedeniq-rabota-s-dopolnitel-nymi-polqmi).

> Метаданные Возвратов поставщикам

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление доп. полей Возвратов поставщикам.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata",
    "mediaType": "application/json"
  },
  "attributes": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/attributes/4fc7e124-41be-11e6-8a84-bae5000000cb",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "4fc7e124-41be-11e6-8a84-bae5000000cb",
      "name": "AttributeName1",
      "type": "boolean",
      "required": false
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/attributes/4fc7e7e7-41be-11e6-8a84-bae5000000cc",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "4fc7e7e7-41be-11e6-8a84-bae5000000cc",
      "name": "AttributeName2",
      "type": "text",
      "required": false
    }
  ],
  "states": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/states/69e394ff-41be-11e6-8a84-bae5000000d0",
        "type": "state",
        "mediaType": "application/json"
      },
      "id": "69e394ff-41be-11e6-8a84-bae5000000d0",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "name": "Оформлен",
      "color": 9245744,
      "stateType": "Regular",
      "entityType": "purchasereturn"
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/states/69e39958-41be-11e6-8a84-bae5000000d1",
        "type": "state",
        "mediaType": "application/json"
      },
      "id": "69e39958-41be-11e6-8a84-bae5000000d1",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "name": "Произведен частично",
      "color": 4354177,
      "stateType": "Regular",
      "entityType": "purchasereturn"
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/states/69e39d04-41be-11e6-8a84-bae5000000d2",
        "type": "state",
        "mediaType": "application/json"
      },
      "id": "69e39d04-41be-11e6-8a84-bae5000000d2",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "name": "Произведен",
      "color": 8825440,
      "stateType": "Regular",
      "entityType": "purchasereturn"
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
  "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/attributes/7944ef04-f831-11e5-7a69-971500188b19"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление отдельного доп. поля.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/attributes/4fc7e7e7-41be-11e6-8a84-bae5000000cc",
    "type": "attributemetadata",
    "mediaType": "application/json"
  },
  "id": "4fc7e7e7-41be-11e6-8a84-bae5000000cc",
  "name": "AttributeName1",
  "type": "text",
  "required": false
}
```

### Шаблон Возврата поставщику 
#### Шаблон Возврата поставщику 
Запрос на получение предзаполненого стандартными значениями шаблона возврата поставщику без связи с каким-либо документом.

> Создание шаблона возврата поставщику с пустым телом запроса

```shell
  curl -X PUT
    "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/new"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d ''  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление предзаполненного Возврата поставщику.

```json
{
  "applicable": false,
  "sum": 0,
  "organization": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
      "type": "organization",
      "mediaType": "application/json"
    }
  },
  "store": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/faf3ff5b-2e58-11e6-8a84-bae500000050",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
      "type": "store",
      "mediaType": "application/json"
    }
  },
  "created": "2007-02-07 17:16:41",
  "printed": true,
  "published": true,
  "positions": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2",
      "type": "purchasereturnposition",
      "mediaType": "application/json",
      "size": 0,
      "limit": 1000,
      "offset": 0
    },
    "rows": []
  },
  "vatEnabled": true,
  "vatIncluded": true,
  "payedSum": 0
}
```

### Шаблон Возврата поставщику на основе 
Запрос на получение предзаполненного шаблона возврата поставщику на основе переданной приемки.
В ответ на запрос вернется предзаполненный шаблон возврата поставщику, который
затем можно будет использовать для создания нового возврата с помощью POST запроса.

> Пример запроса на создание шаблона возврата поставщику на основе приемки.

```shell
  curl -X PUT
    "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/new"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "supply": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/supply/373d2925-4a98-11e6-8a84-bae500000069",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/supply/metadata",
                "type": "supply",
                "mediaType": "application/json"
              }
            }
          }'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление предзаполненного Возврата поставщику.

```json
{
  "applicable": false,
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
  "organization": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/1485d676-32ca-11e6-8a84-bae500000009",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
      "mediaType": "application/json"
    }
  },
  "store": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/faf3ff5b-2e58-11e6-8a84-bae500000050",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
      "type": "store",
      "mediaType": "application/json"
    }
  },
  "agent": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
      "type": "organization",
      "mediaType": "application/json"
    }
  },
  "organizationAccount": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e/accounts/fae39d66-2e58-11e6-8a84-bae50000004f",
      "type": "account",
      "mediaType": "application/json"
    }
  },
  "agentAccount": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/1485d676-32ca-11e6-8a84-bae500000009/accounts/1485e43e-32ca-11e6-8a84-bae50000000a",
      "type": "account",
      "mediaType": "application/json"
    }
  },
  "created": "2007-02-07 17:16:41",
  "printed": true,
  "published": true,
  "positions": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2",
      "type": "purchasereturnposition",
      "mediaType": "application/json",
      "size": 0,
      "limit": 1000,
      "offset": 0
    },
    "rows": []
  },
  "vatEnabled": true,
  "vatIncluded": true,
  "supply": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/supply/373d2925-4a98-11e6-8a84-bae500000069",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/supply/metadata",
      "type": "supply",
      "mediaType": "application/json"
    }
  },
  "payedSum": 0
}
```

### Возврат поставщику
 
### Получить Возврат поставщику

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Возврата поставщику.|
 
> Запрос на получение отдельного Возврата поставщику с указанным id.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/7944ef04-f831-11e5-7a69-971500188b19"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление Возврата поставщику с указанным id.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/e699b298-41bd-11e6-8a84-bae5000000ba",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata",
    "type": "purchasereturn",
    "mediaType": "application/json"
  },
  "id": "e699b298-41bd-11e6-8a84-bae5000000ba",
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
  "updated": "2016-07-04 11:04:15",
  "name": "00004",
  "externalCode": "tBSZzXSgggWNL5MZ7IrYE2",
  "moment": "2016-07-04 11:04:00",
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
  "sum": 43156000,
  "organization": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
      "type": "organization",
      "mediaType": "application/json"
    }
  },
  "store": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/faf3ff5b-2e58-11e6-8a84-bae500000050",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
      "type": "store",
      "mediaType": "application/json"
    }
  },
  "contract": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/contract/91287d9a-41bc-11e6-8a84-bae500000082",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/contract/metadata",
      "type": "contract",
      "mediaType": "application/json"
    }
  },
  "project": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/project/722e39f0-313e-11e6-8a84-bae500000008",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/project/metadata",
      "type": "project",
      "mediaType": "application/json"
    }
  },
  "agent": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/14bfc067-32ca-11e6-8a84-bae50000003f",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
      "mediaType": "application/json"
    }
  },
  "organizationAccount": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e/accounts/fae39d66-2e58-11e6-8a84-bae50000004f",
      "type": "account",
      "mediaType": "application/json"
    }
  },
  "vatEnabled": true,
  "vatIncluded": true,
  "positions": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/e699b298-41bd-11e6-8a84-bae5000000ba/positions",
      "type": "purchasereturnposition",
      "mediaType": "application/json",
      "size": 7,
      "limit": 1000,
      "offset": 0
    }
  },
  "supply": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/supply/80d04ebc-41bd-11e6-8a84-bae500000085",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/supply/metadata",
      "type": "supply",
      "mediaType": "application/json"
    }
  },
  "payedSum": 0
}
```

### Изменить Возврат поставщику 
Запрос на обновление Возврата поставщику с указанным id.
В теле запроса можно указать только те поля, которые необходимо изменить у Возврата поставщику, кроме тех, что
помечены `Только для чтения` в описании [атрибутов Возврата поставщику](../documents/#dokumenty-vozwrat-postawschiku).
При обновлении полей **organization** и **agent** нужно также обновить поля **organizationAccount** и
**agentAccount** соответственно, иначе произойдет ошибка.
Контрагент должен совпадать с контрагентом, указанным в документе, по которому создается возврат.

При обновлении возврата:

+ Нельзя изменять следующие поля: **agentAccount**, **agent**, **supply**
+ Нельзя выставить валюту отличную от валюты в документе
+ Нельзя добавить позиции, отсутствующие среди позиций документа.

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Возврата поставщику.|

> Пример запроса на обновление Возврата поставщику.

```shell
  curl -X PUT
    "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/7944ef04-f831-11e5-7a69-971500188b19"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "name": "763457",
            "owner": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/1205364b-7f01-455a-a1b5-4ba0988c8308",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
                "type": "employee",
                "mediaType": "application/json"
              }
            },
            "shared": true,
            "group": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/group/348d910b-6dc0-483f-b916-2237bc54a04e",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/group/metadata",
                "type": "group",
                "mediaType": "application/json"
              }
            },
            "description": "Возврат поставщику созданный и обновленный через API",
            "code": "8865255398",
            "externalCode": "fruitsareawesome!!!",
            "moment": "2016-11-21 14:27:00",
            "applicable": false,
            "state": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/states/69e39d04-41be-11e6-8a84-bae5000000d2",
                "type": "state",
                "mediaType": "application/json"
              }
            },
            "attributes": [
              {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/attributes/4fc7e124-41be-11e6-8a84-bae5000000cb",
                  "type": "attributemetadata",
                  "mediaType": "application/json"
                },
                "value": true
              }
            ],
            "positions": [
              {
                "quantity": 1,
                "price": 1241200,
                "discount": 0,
                "vat": 0,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/e6447ee7-3303-11e6-8a84-bae5000149c2",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                    "type": "product",
                    "mediaType": "application/json"
                  }
                }
              },
              {
                "quantity": 1,
                "price": 24100,
                "discount": 0,
                "vat": 0,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/e8517bc4-3303-11e6-8a84-bae500014de1",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                    "type": "product",
                    "mediaType": "application/json"
                  }
                }
              },
              {
                "quantity": 1,
                "price": 421000,
                "discount": 0,
                "vat": 0,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/service/6767bc73-3d19-11e6-8a84-bae500000002",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/service/metadata",
                    "type": "service",
                    "mediaType": "application/json"
                  }
                }
              },
              {
                "quantity": 1,
                "price": 2421000,
                "discount": 0,
                "vat": 0,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/e8563cc5-3303-11e6-8a84-bae500014df0",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                    "type": "product",
                    "mediaType": "application/json"
                  }
                }
              },
              {
                "quantity": 1,
                "price": 263000,
                "discount": 0,
                "vat": 0,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/20485cfd-2e62-11e6-8a84-bae500000112",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                    "type": "product",
                    "mediaType": "application/json"
                  }
                }
              }
            ]
          }'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление обновленного Возврата поставщику.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/6d5371fc-41c1-11e6-8a84-bae50000001c",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata",
    "type": "purchasereturn",
    "mediaType": "application/json"
  },
  "id": "6d5371fc-41c1-11e6-8a84-bae50000001c",
  "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
  "owner": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/1205364b-7f01-455a-a1b5-4ba0988c8308",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
      "type": "employee",
      "mediaType": "application/json"
    }
  },
  "shared": true,
  "group": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/group/348d910b-6dc0-483f-b916-2237bc54a04e",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/group/metadata",
      "type": "group",
      "mediaType": "application/json"
    }
  },
  "updated": "2016-07-04 11:35:26",
  "name": "763457",
  "description": "Возврат поставщику созданный и обновленный через API",
  "code": "8865255398",
  "externalCode": "fruitsareawesome!!!",
  "moment": "2016-11-21 14:27:00",
  "applicable": false,
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
  "sum": 4370300,
  "organization": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
      "type": "organization",
      "mediaType": "application/json"
    }
  },
  "store": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/faf3ff5b-2e58-11e6-8a84-bae500000050",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
      "type": "store",
      "mediaType": "application/json"
    }
  },
  "agent": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/147c1f1b-32ca-11e6-8a84-bae500000004",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
      "mediaType": "application/json"
    }
  },
  "state": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/states/69e39d04-41be-11e6-8a84-bae5000000d2",
      "type": "state",
      "mediaType": "application/json"
    }
  },
  "organizationAccount": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e/accounts/fae39d66-2e58-11e6-8a84-bae50000004f",
      "type": "account",
      "mediaType": "application/json"
    }
  },
  "agentAccount": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/147c1f1b-32ca-11e6-8a84-bae500000004/accounts/147c3231-32ca-11e6-8a84-bae500000005",
      "type": "account",
      "mediaType": "application/json"
    }
  },
  "attributes": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/attributes/4fc7e124-41be-11e6-8a84-bae5000000cb",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "4fc7e124-41be-11e6-8a84-bae5000000cb",
      "name": "AttributeName1",
      "type": "boolean",
      "value": true
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/attributes/4fc7e7e7-41be-11e6-8a84-bae5000000cc",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "4fc7e7e7-41be-11e6-8a84-bae5000000cc",
      "name": "AttributeName1",
      "type": "text",
      "value": "деталь"
    }
  ],
  "vatEnabled": true,
  "vatIncluded": true,
  "created": "2007-02-07 17:16:41",
  "printed": true,
  "published": true,
  "positions": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/6d5371fc-41c1-11e6-8a84-bae50000001c/positions",
      "type": "purchasereturnposition",
      "mediaType": "application/json",
      "size": 5,
      "limit": 1000,
      "offset": 0
    }
  },
  "supply": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/supply/7585391b-41c0-11e6-8a84-bae5000000de",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/supply/metadata",
      "type": "supply",
      "mediaType": "application/json"
    }
  },
  "payedSum": 0
}
```

### Позиции Возврата поставщику 
Отдельный ресурс для управления позициями Возврата поставщику. С его помощью вы можете управлять позициями большого документа, количество строк в котором превышает лимит на количество строк, сохраняемых вместе с документом. Этот лимит равен 1000. Более подробно о лимитах на количество строк документа и работе с большими документами можно прочитать [тут](../#mojsklad-json-api-obschie-swedeniq-rabota-s-poziciqmi-dokumentow).

### Получить Позиции 
Запрос на получение списка всех позиций данной Возврата поставщику.

| Название  | Тип | Описание                    |
| --------- |:----|:----------------------------|
**meta** |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные о выдаче,
**context** | [Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye) | Метаданные о сотруднике, выполнившем запрос.
**rows** |Array(Object)|Массив JSON объектов, представляющих собой позиции Возврата поставщику.

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Возврата поставщику.|
|**limit** |  `number` (optional) **Default: 1000** *Example: 1000* Максимальное количество сущностей для извлечения.`Допустимые значения 1 - 1000`.|
|**offset** |  `number` (optional) **Default: 0** *Example: 40* Отступ в выдаваемом списке сущностей.|

> Получить Позиции

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/7944ef04-f831-11e5-7a69-971500188b19/positions"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление списка позиций Возврата поставщику.

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
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/7944ef04-f831-11e5-7a69-971500188b19/positions",
    "type": "purchasereturnposition",
    "mediaType": "application/json",
    "size": 7,
    "limit": 1000,
    "offset": 0
  },
  "rows": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/7944ef04-f831-11e5-7a69-971500188b19/positions/e699bc75-41bd-11e6-8a84-bae5000000bb",
        "type": "purchasereturnposition",
        "mediaType": "application/json"
      },
      "id": "e699bc75-41bd-11e6-8a84-bae5000000bb",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "quantity": 40,
      "price": 34400,
      "discount": 0,
      "vat": 0,
      "vatEnabled": false,
      "assortment": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/a69fe5c3-3303-11e6-8a84-bae50000dfab",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
          "type": "product",
          "mediaType": "application/json",
          "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=e64d0a86-2a99-11e9-ac12-000c00000041"
        }
      }
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/7944ef04-f831-11e5-7a69-971500188b19/positions/e699c2b5-41bd-11e6-8a84-bae5000000bc",
        "type": "purchasereturnposition",
        "mediaType": "application/json"
      },
      "id": "e699c2b5-41bd-11e6-8a84-bae5000000bc",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "quantity": 52,
      "price": 556000,
      "discount": 0,
      "vat": 0,
      "vatEnabled": false,
      "assortment": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/0464a192-3304-11e6-8a84-bae500017f51",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
          "type": "product",
          "mediaType": "application/json",
          "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=3b1e1f15-2842-11e9-ac12-000c0000002f"
        }
      }
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/7944ef04-f831-11e5-7a69-971500188b19/positions/e699c804-41bd-11e6-8a84-bae5000000bd",
        "type": "purchasereturnposition",
        "mediaType": "application/json"
      },
      "id": "e699c804-41bd-11e6-8a84-bae5000000bd",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "quantity": 32,
      "price": 200000,
      "discount": 0,
      "vat": 0,
      "vatEnabled": false,
      "assortment": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/044e812a-3304-11e6-8a84-bae500017f34",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
          "type": "product",
          "mediaType": "application/json",
          "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=392c045c-2842-11e9-ac12-000a00000002"
        }
      }
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/7944ef04-f831-11e5-7a69-971500188b19/positions/e699cd72-41bd-11e6-8a84-bae5000000be",
        "type": "purchasereturnposition",
        "mediaType": "application/json"
      },
      "id": "e699cd72-41bd-11e6-8a84-bae5000000be",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "quantity": 112,
      "price": 34000,
      "discount": 0,
      "vat": 0,
      "vatEnabled": false,
      "assortment": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/048b1a8b-3304-11e6-8a84-bae500017f84",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
          "type": "product",
          "mediaType": "application/json",
          "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=3bb1af6c-2842-11e9-ac12-000c00000061"
        }
      }
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/7944ef04-f831-11e5-7a69-971500188b19/positions/e699d288-41bd-11e6-8a84-bae5000000bf",
        "type": "purchasereturnposition",
        "mediaType": "application/json"
      },
      "id": "e699d288-41bd-11e6-8a84-bae5000000bf",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "quantity": 76,
      "price": 35000,
      "discount": 0,
      "vat": 0,
      "vatEnabled": false,
      "assortment": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/27eba7b5-3303-11e6-8a84-bae500002b72",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
          "type": "product",
          "mediaType": "application/json",
          "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=3bad99f1-2842-11e9-ac12-000c0000005c"
        }
      }
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/7944ef04-f831-11e5-7a69-971500188b19/positions/e699d76d-41bd-11e6-8a84-bae5000000c0",
        "type": "purchasereturnposition",
        "mediaType": "application/json"
      },
      "id": "e699d76d-41bd-11e6-8a84-bae5000000c0",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "quantity": 6000,
      "price": 0,
      "discount": 0,
      "vat": 0,
      "vatEnabled": false,
      "assortment": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/130a02d7-3303-11e6-8a84-bae500001887",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
          "type": "product",
          "mediaType": "application/json",
          "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=3c3c1618-2842-11e9-ac12-000c0000006f"
        }
      }
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/7944ef04-f831-11e5-7a69-971500188b19/positions/e699dcb4-41bd-11e6-8a84-bae5000000c1",
        "type": "purchasereturnposition",
        "mediaType": "application/json"
      },
      "id": "e699dcb4-41bd-11e6-8a84-bae5000000c1",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "quantity": 75,
      "price": 0,
      "discount": 0,
      "vat": 0,
      "vatEnabled": false,
      "assortment": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/3b9a7d0c-2842-11e9-ac12-000c0000005a",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
          "type": "product",
          "mediaType": "application/json",
          "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=0475cacb-3303-11e6-8a84-bae500000765"
        }
      }
    }
  ]
}

```

### Создать Позицию 
Запрос на создание новой позиции в Возврате поставщику.
Для успешного создания необходимо в теле запроса указать следующие поля:

+ **assortment** - Ссылка на товар/услугу/серию/модификацию, которую представляет собой позиция.
Также можно указать поле с именем **service**, **consignment**, **variant** в соответствии с тем,
чем является указанная позиция. Подробнее об этом поле можно прочитать в описании [позиции Возврата поставщику](../documents/#dokumenty-vozwrat-postawschiku-vozwraty-postawschikam-pozicii-vozwrata-postawschiku).

+ **quantity** - Количество указанной позиции. Должно быть положительным, иначе возникнет ошибка.
Одновременно можно создать как одну так и несколько позиций Возврата поставщику. Все созданные данным запросом позиции
будут добавлены к уже существующим.
Нельзя создавать позиции, отличные от позиций в документе, по которому создается возврат. Допустимо только
отличие в **quantity** позиций (количество в позиции в возврате м.б. меньше или равно количеству в позиции в документе).

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Возврата поставщику.|

> Пример запроса на создание позиций в Возврате поставщику.

```shell
  curl -X POST
    "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/7944ef04-f831-11e5-7a69-971500188b19/positions"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '[
            {
              "quantity": 1,
              "price": 263000,
              "discount": 0,
              "vat": 0,
              "assortment": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/20485cfd-2e62-11e6-8a84-bae500000112",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                  "type": "product",
                  "mediaType": "application/json"
                }
              }
            },
            {
              "quantity": 1,
              "price": 10000,
              "discount": 0,
              "vat": 0,
              "assortment": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/0744d71b-2e59-11e6-8a84-bae50000007f",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                  "type": "product",
                  "mediaType": "application/json"
                }
              }
            }
          ]
'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление созданных позиций.

```json
[
  {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/7944ef04-f831-11e5-7a69-971500188b19/positions/9cfa8b56-41bf-11e6-8a84-bae500000014",
      "type": "purchasereturnposition",
      "mediaType": "application/json"
    },
    "id": "9cfa8b56-41bf-11e6-8a84-bae500000014",
    "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
    "quantity": 1,
    "price": 263000,
    "discount": 0,
    "vat": 0,
    "vatEnabled": false,
    "assortment": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/20485cfd-2e62-11e6-8a84-bae500000112",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
        "type": "product",
        "mediaType": "application/json",
        "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=e64d0a86-2a99-11e9-ac12-000c00000041"
      }
    }
  },
  {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/7944ef04-f831-11e5-7a69-971500188b19/positions/9cfa9b0e-41bf-11e6-8a84-bae500000015",
      "type": "purchasereturnposition",
      "mediaType": "application/json"
    },
    "id": "9cfa9b0e-41bf-11e6-8a84-bae500000015",
    "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
    "quantity": 1,
    "price": 10000,
    "discount": 0,
    "vat": 0,
    "vatEnabled": false,
    "assortment": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/0744d71b-2e59-11e6-8a84-bae50000007f",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
        "type": "product",
        "mediaType": "application/json",
        "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=3b1e1f15-2842-11e9-ac12-000c0000002f"
      }
    }
  }
]

```

### Позиция Возврата поставщику
 
### Получить Позицию

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Возврата поставщику.|
|**positionIDv**|  `string` (required) *Example: 34f6344f-015e-11e6-9464-e4de0000006c* id позиции Возврата поставщику.|
 
> Запрос на получение отдельной позиции Возврата поставщику с указанным id.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/7944ef04-f831-11e5-7a69-971500188b19/positions/34f6344f-015e-11e6-9464-e4de0000006c"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление отдельной позиции Возврата поставщику.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/7944ef04-f831-11e5-7a69-971500188b19/positions/34f6344f-015e-11e6-9464-e4de0000006c",
    "type": "purchasereturnposition",
    "mediaType": "application/json"
  },
  "id": "34f6344f-015e-11e6-9464-e4de0000006c",
  "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
  "quantity": 76,
  "price": 35000,
  "discount": 0,
  "vat": 0,
  "vatEnabled": false,
  "assortment": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/27eba7b5-3303-11e6-8a84-bae500002b72",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
      "type": "product",
      "mediaType": "application/json",
      "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=3b1e1f15-2842-11e9-ac12-000c0000002f"
    }
  }
}

```

### Изменить Позицию 
Запрос на обновление отдельной позиции Возврата поставщику.
При обновлении отдельной позиции в возврате можно только изменить количество данной позиции.
Причем это количество должно быть в пределах , где n - кол-во данной позиции в документе, по которому создан возврат.

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Возврата поставщику.|
|**positionID**|  `string` (required) *Example: 34f6344f-015e-11e6-9464-e4de0000006c* id позиции Возврата поставщику.|

> Пример запроса на обновление отдельной позиции в Возврате поставщику.

```shell
  curl -X PUT
    "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/7944ef04-f831-11e5-7a69-971500188b19/positions/34f6344f-015e-11e6-9464-e4de0000006c"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "quantity": 6754
          }'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление обновленной позиции Возврата поставщику.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/7944ef04-f831-11e5-7a69-971500188b19/positions/34f6344f-015e-11e6-9464-e4de0000006c",
    "type": "purchasereturnposition",
    "mediaType": "application/json"
  },
  "id": "34f6344f-015e-11e6-9464-e4de0000006c",
  "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
  "quantity": 6754,
  "price": 0,
  "discount": 0,
  "vat": 0,
  "vatEnabled": false,
  "assortment": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/130a02d7-3303-11e6-8a84-bae500001887",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
      "type": "product",
      "mediaType": "application/json",
      "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=3b1e1f15-2842-11e9-ac12-000c0000002f"
    }
  }
}
```

### Удалить позицию

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Возврата поставщику.|
|**positionID**|  `string` (required) *Example: 34f6344f-015e-11e6-9464-e4de0000006c* id позиции Возврата поставщику.|
 
> Запрос на удаление отдельной позиции Возврата поставщику с указанным id.

```shell
curl -X DELETE
  "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/7944ef04-f831-11e5-7a69-971500188b19/positions/34f6344f-015e-11e6-9464-e4de0000006c"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешное удаление позиции Возврата поставщику.
