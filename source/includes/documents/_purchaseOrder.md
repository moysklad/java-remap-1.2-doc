## Заказ поставщику
### Заказы Поставщикам 
Средствами JSON API можно создавать и обновлять сведения о Заказах поставщику, запрашивать списки Заказов и сведения по отдельным Заказам Поставщикам. Позициями Заказов можно управлять как в составе отдельного Заказа поставщику, так и отдельно - с помощью специальных ресурсов для управления позициями Заказа. Кодом сущности для Заказа поставщику в составе JSON API является ключевое слово **purchaseorder**. Больше о Заказах Поставщикам и работе с ними в основном интерфейсе вы можете прочитать в нашей службе поддержки по [этой ссылке](https://support.moysklad.ru/hc/ru/articles/202984676-%D0%97%D0%B0%D0%BA%D0%B0%D0%B7%D1%8B-%D0%BF%D0%BE%D1%81%D1%82%D0%B0%D0%B2%D1%89%D0%B8%D0%BA%D0%B0%D0%BC).

#### Атрибуты сущности

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные Заказа поставщику|&mdash;|да
|**id**                 |UUID|ID Заказа поставщику|Только для чтения|да
|**accountId**          |UUID| ID учетной записи|Только для чтения|да
|**syncId**             |UUID|ID синхронизации. После заполнения недоступен для изменения|&mdash;|нет
|**updated**            |DateTime|Момент последнего обновления Заказа поставщику|Только для чтения|да
|**deleted**            |DateTime|Момент последнего удаления Заказа поставщику|Только для чтения|нет
|**name**               |String(255)|Наименование Заказа поставщику|&mdash;|да
|**description**        |String(4096)|Комментарий Заказа поставщику|&mdash;|нет
|**externalCode**       |String(255)|Внешний код Заказа поставщику|&mdash;| да
|**moment**             |DateTime|Дата Заказа|&mdash;|да
|**applicable**         |Boolean|Отметка о проведении|&mdash;|да
|**vatEnabled**         |Boolean|Учитывается ли НДС|&mdash;|да
|**vatIncluded**        |Boolean| Включен ли НДС в цену|&mdash;|нет
|**sum**                |Int|Сумма Заказа поставщику в установленной валюте|Только для чтения|да
|**rate**               |Object|Валюта. [Подробнее тут](../documents/#dokumenty-obschie-swedeniq-valuta-w-dokumentah)|&mdash;|да
|**owner**              |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Владелец (Сотрудник)|&mdash;|да
|**shared**             |Boolean|Общий доступ|&mdash;|да
|**group**              |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Отдел сотрудника|&mdash;|да
|**organization**       |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные юрлица|Необходимое при создании|да
|**agent**              |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные контрагента|Необходимое при создании|да
|**store**              |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные склада|&mdash;|да
|**contract**              |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные договора|&mdash;|нет
|**state**              |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные статуса заказа|&mdash;|нет
|**organizationAccount**|[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные счета юрлица|&mdash;|нет
|**agentAccount**       |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные счета контрагента|&mdash;|нет
|**attributes**         |Array(Object)|Коллекция метаданных доп. полей. [Поля объекта](../#mojsklad-json-api-obschie-swedeniq-rabota-s-dopolnitel-nymi-polqmi) |&mdash;|нет
|**files**              |MetaArray|Массив метаданных [Файлов](../dictionaries/#suschnosti-fajly) (Максимальное количество файлов - 100)|&mdash;|да|
|**created**            |DateTime|Дата создания|Только для чтения|да
|**printed**            |Boolean|Напечатан ли документ|Только для чтения|да
|**published**          |Boolean|Опубликован ли документ|Только для чтения|да
|**vatSum**             |Float|Сумма НДС |Только для чтения|да
|**positions**          |MetaArray|Метаданные позиций Заказа поставщику|&mdash;|да
|**deliveryPlannedMoment**          |DateTime|Планируемая дата отгрузки|&mdash;|нет
|**payedSum**            |Float|Сумма входящих платежей по Заказу |Только для чтения|да
|**shippedSum**             |Float|Сумма отгруженного |Только для чтения|да
|**invoicedSum**            |Float|Сумма счетов поставщику |Только для чтения|да
|**project**            |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные проекта|&mdash;|нет
|**waitSum**            |Float|Сумма товаров в пути|&mdash;|да

#### Связи с другими документами

|Название          | Описание  |
| ------------------------------ |:---------------------------|
| **customerOrders** | Массив ссылок на связанные заказы покупателей в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye)
| **invoicesIn** | Массив ссылок на связанные счета поставщиков в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye)
| **payments** | Массив ссылок на связанные платежи в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye)
| **supplies** | Массив ссылок на связанные приемки в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye)
| **internalOrder** | Внутренний заказ, связанный с заказом поставщику, в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye)

#### Позиции Заказа поставщику
Позиции Заказа - это список товаров/услуг/модификаций/серий.
Объект позиции Заказа содержит следующие поля:

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
|**shipped**        |Int|Принято|&mdash;|да
|**wait**        |Boolean|Ожидается данной позиции|&mdash;|нет

С позициями можно работать с помощью специальных ресурсов для управления позициями Заказа,
а также в составе отдельного Заказа поставщику. При работе в составе отдельного Заказа поставщику,
вы можете отправлять запросы на создание отдельного Заказа поставщику с включенным в тело запроса
массивом позиций Заказа. Если количество позиций превышает максимально допустимое, то для
дальнейшего пополнения позиций нужно будет работать со специальным ресурсом "Позиции Заказа поставщику".
Также, при работе в составе отдельного Заказа поставщику, можно отправлять запросы на обновление списка позиций
с включенным в тело запроса массивом позиций Заказа. При этом важно помнить, что коллекция позиций будет
восприниматься как "все позиции Заказа" и полностью заменит уже существующую коллекцию при обновлении объекта - лишние
позиции будут удалены, новые добавлены, существующие - изменены.

О работе с доп. полями Заказов поставщикам можно прочитать [здесь](../#mojsklad-json-api-obschie-swedeniq-rabota-s-dopolnitel-nymi-polqmi)

### Получить список Заказов Поставщикам 
Запрос всех Заказов Поставщикам на данной учетной записи.
Результат: Объект JSON, включающий в себя поля:

| Название  | Тип | Описание                    |
| --------- |:----|:----------------------------|
**meta** |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные о выдаче,
**context** | [Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye) | Метаданные о сотруднике, выполнившем запрос.
**rows** |Array(Object)|Массив JSON объектов, представляющих собой Заказы Поставщикам.

**Параметры**

| Параметр                | Описание  |
| ------------------------------ |:---------------------------|
|**limit** |  `number` (optional) **Default: 1000** *Example: 1000* Максимальное количество сущностей для извлечения.`Допустимые значения 1 - 1000`.|
|**offset** |  `number` (optional) **Default: 0** *Example: 40* Отступ в выдаваемом списке сущностей.|
|**search** |  `string` (optional) *Example: 0001* Фильтр документов по указанной поисковой строке.

> Получить список Заказов Поставщикам

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление списка Заказов Поставщикам.

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
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata",
    "type": "purchaseorder",
    "mediaType": "application/json",
    "size": 2,
    "limit": 1000,
    "offset": 0
  },
  "rows": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/172fb2f6-3f70-11e6-8a84-bae50000008e",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata",
        "type": "purchaseorder",
        "mediaType": "application/json"
      },
      "id": "172fb2f6-3f70-11e6-8a84-bae50000008e",
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
      "updated": "2016-07-01 12:42:13",
      "name": "00002",
      "description": "Описание заказа",
      "externalCode": "FfSmVuSKi7h8L-jLADHV80",
      "moment": "2016-07-01 12:40:00",
      "applicable": true,
      "printed": true,
      "published": true,
      "rate": {
        "currency": {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/faf45b9a-2e58-11e6-8a84-bae500000055",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
            "type": "currency",
            "mediaType": "application/json"
          }
        }
      },
      "sum": 5900,
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
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/contract/e105a2e7-3f6f-11e6-8a84-bae500000087",
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
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/14ae5431-32ca-11e6-8a84-bae50000002d",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
          "type": "counterparty",
          "mediaType": "application/json"
        }
      },
      "state": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/states/11f5becd-3f70-11e6-8a84-bae50000008b",
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
      "vatEnabled": true,
      "vatIncluded": true,
      "positions": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/172fb2f6-3f70-11e6-8a84-bae50000008e/positions",
          "type": "purchaseorderposition",
          "mediaType": "application/json",
          "size": 5,
          "limit": 1000,
          "offset": 0
        }
      },
      "deliveryPlannedMoment": "2016-07-15 12:40:00",
      "payedSum": 0,
      "shippedSum": 0,
      "invoicedSum": 0,
      "waitSum": 5900
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/403e7ea0-2e63-11e6-8a84-bae500000131",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata",
        "type": "purchaseorder",
        "mediaType": "application/json"
      },
      "id": "403e7ea0-2e63-11e6-8a84-bae500000131",
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
      "updated": "2016-06-10 10:06:46",
      "name": "00001",
      "externalCode": "pk6fh0NthbBSgrqI931uA0",
      "moment": "2016-06-10 10:06:00",
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
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/403e7ea0-2e63-11e6-8a84-bae500000131/positions",
          "type": "purchaseorderposition",
          "mediaType": "application/json",
          "size": 2,
          "limit": 1000,
          "offset": 0
        }
      },
      "deliveryPlannedMoment": "2016-06-11 10:06:00",
      "payedSum": 0,
      "shippedSum": 0,
      "invoicedSum": 0,
      "waitSum": 0
    }
  ]
}
```
        
### Создать Заказ поставщику 
Запрос на создание нового Заказа поставщику.
Обязательные для создания поля:

| Параметр                | Описание  |
| ------------------------------ |:---------------------------|
|**name** | номер Заказа поставщику
| **organization** | Ссылка на ваше юрлицо в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye)
| **agent** | Ссылка на контрагента (поставщику) в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye)

> Пример создания нового Заказа.

```shell
  curl -X POST
    "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "name": "103034",
            "description": "Типичный заказ поставщику",
            "organization": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
                "type": "organization",
                "mediaType": "application/json"
              }
            },
            "code": "404",
            "moment": "2016-12-05 15:30:14",
            "applicable": true,
            "vatEnabled": true,
            "vatIncluded": true,
            "agent": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/1483952f-32ca-11e6-8a84-bae500000007",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
                "type": "counterparty",
                "mediaType": "application/json"
              }
            },
            "state": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/states/11f5becd-3f70-11e6-8a84-bae50000008b",
                "type": "state",
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
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/contract/e105a2e7-3f6f-11e6-8a84-bae500000087",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/contract/metadata",
                "type": "contract",
                "mediaType": "application/json"
              }
            },
            "rate": {
              "currency": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/cdbc62de-3f68-11e6-8a84-bae500000050",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
                  "type": "currency",
                  "mediaType": "application/json"
                }
              }
            },
            "deliveryPlannedMoment": "2015-02-15 14:12:19",
            "attributes": [
              {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/attributes/6a885b1b-3f70-11e6-8a84-bae50000009d",
                  "type": "attributemetadata",
                  "mediaType": "application/json"
                },
                "value": "Черный"
              },
              {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/attributes/6a88619c-3f70-11e6-8a84-bae50000009e",
                  "type": "attributemetadata",
                  "mediaType": "application/json"
                },
                "value": 0.4
              },
              {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/attributes/6a886744-3f70-11e6-8a84-bae50000009f",
                  "type": "attributemetadata",
                  "mediaType": "application/json"
                },
                "value": true
              }
            ]
          }'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление созданного Заказа поставщику.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/22b4caaa-3f74-11e6-8a84-bae500000069",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata",
    "type": "purchaseorder",
    "mediaType": "application/json"
  },
  "id": "22b4caaa-3f74-11e6-8a84-bae500000069",
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
  "updated": "2016-07-01 13:11:11",
  "name": "103034",
  "description": "Типичный заказ поставщику",
  "code": "404",
  "externalCode": "s30P0zlwg-1qxSZnRVONF0",
  "moment": "2016-12-05 15:30:14",
  "applicable": true,
  "rate": {
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/cdbc62de-3f68-11e6-8a84-bae500000050",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json"
      }
    },
    "value": 63
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
  "contract": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/contract/e105a2e7-3f6f-11e6-8a84-bae500000087",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/contract/metadata",
      "type": "contract",
      "mediaType": "application/json"
    }
  },
  "agent": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/1483952f-32ca-11e6-8a84-bae500000007",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
      "mediaType": "application/json"
    }
  },
  "state": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/states/11f5becd-3f70-11e6-8a84-bae50000008b",
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
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/1483952f-32ca-11e6-8a84-bae500000007/accounts/1483a4fa-32ca-11e6-8a84-bae500000008",
      "type": "account",
      "mediaType": "application/json"
    }
  },
  "attributes": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/attributes/6a885b1b-3f70-11e6-8a84-bae50000009d",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "6a885b1b-3f70-11e6-8a84-bae50000009d",
      "name": "AttributeName1",
      "type": "string",
      "value": "Черный"
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/attributes/6a88619c-3f70-11e6-8a84-bae50000009e",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "6a88619c-3f70-11e6-8a84-bae50000009e",
      "name": "AttributeName2",
      "type": "double",
      "value": 0.4
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/attributes/6a886744-3f70-11e6-8a84-bae50000009f",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "6a886744-3f70-11e6-8a84-bae50000009f",
      "name": "AttributeName3",
      "type": "boolean",
      "value": true
    }
  ],
  "vatEnabled": true,
  "vatIncluded": true,
  "created": "2016-08-25 19:55:00",
  "printed": true,
  "published": true,
  "positions": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/22b4caaa-3f74-11e6-8a84-bae500000069/positions",
      "type": "purchaseorderposition",
      "mediaType": "application/json",
      "size": 0,
      "limit": 1000,
      "offset": 0
    }
  },
  "deliveryPlannedMoment": "2015-02-15 14:12:19",
  "payedSum": 0,
  "shippedSum": 0,
  "invoicedSum": 0,
  "waitSum": 0
}
```

> Пример запроса на создание Заказа поставщику с позициями в теле запроса.

```shell
  curl -X POST
    "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "name": "777",
            "description": "Типичный заказ поставщику",
            "organization": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
                "type": "organization",
                "mediaType": "application/json"
              }
            },
            "code": "404",
            "moment": "2016-12-05 15:30:14",
            "applicable": true,
            "vatEnabled": true,
            "vatIncluded": true,
            "agent": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/1483952f-32ca-11e6-8a84-bae500000007",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
                "type": "counterparty",
                "mediaType": "application/json"
              }
            },
            "state": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/states/11f5becd-3f70-11e6-8a84-bae50000008b",
                "type": "state",
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
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/contract/e105a2e7-3f6f-11e6-8a84-bae500000087",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/contract/metadata",
                "type": "contract",
                "mediaType": "application/json"
              }
            },
            "rate": {
              "currency": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/cdbc62de-3f68-11e6-8a84-bae500000050",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
                  "type": "currency",
                  "mediaType": "application/json"
                }
              }
            },
            "deliveryPlannedMoment": "2015-02-15 14:12:19",
            "attributes": [
              {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/attributes/6a885b1b-3f70-11e6-8a84-bae50000009d",
                  "type": "attributemetadata",
                  "mediaType": "application/json"
                },
                "value": "Черный"
              },
              {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/attributes/6a88619c-3f70-11e6-8a84-bae50000009e",
                  "type": "attributemetadata",
                  "mediaType": "application/json"
                },
                "value": 0.4
              },
              {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/attributes/6a886744-3f70-11e6-8a84-bae50000009f",
                  "type": "attributemetadata",
                  "mediaType": "application/json"
                },
                "value": true
              }
            ],
            "positions": [
              {
                "quantity": 12,
                "price": 300,
                "vat": 0,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/variant/7a81082f-3c64-11e6-8a84-bae50000000e",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/variant/metadata",
                    "type": "variant",
                    "mediaType": "application/json"
                  }
                },
                "inTransit": 11
              },
              {
                "quantity": 3,
                "price": 1000,
                "discount": 0,
                "vat": 10,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/7a6f697f-3c64-11e6-8a84-bae500000006",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                    "type": "product",
                    "mediaType": "application/json"
                  }
                },
                "inTransit": 1
              },
              {
                "quantity": 404,
                "price": 454,
                "discount": 200,
                "vat": 21,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/variant/7a83c422-3c64-11e6-8a84-bae500000012",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/variant/metadata",
                    "type": "variant",
                    "mediaType": "application/json"
                  }
                },
                "inTransit": 216
              }
            ]
          }'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление созданного Заказа поставщику.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/ae7fa9fb-3f74-11e6-8a84-bae500000070",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata",
    "type": "purchaseorder",
    "mediaType": "application/json"
  },
  "id": "ae7fa9fb-3f74-11e6-8a84-bae500000070",
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
  "updated": "2016-07-01 13:15:05",
  "name": "777",
  "description": "Типичный заказ поставщику",
  "code": "404",
  "externalCode": "37KNBm71gw7Zm00T5JdAt0",
  "moment": "2016-12-05 15:30:14",
  "applicable": true,
  "printed": true,
  "published": true,
  "rate": {
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/cdbc62de-3f68-11e6-8a84-bae500000050",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json"
      }
    },
    "value": 63
  },
  "sum": 176816,
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
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/contract/e105a2e7-3f6f-11e6-8a84-bae500000087",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/contract/metadata",
      "type": "contract",
      "mediaType": "application/json"
    }
  },
  "agent": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/1483952f-32ca-11e6-8a84-bae500000007",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
      "mediaType": "application/json"
    }
  },
  "state": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/states/11f5becd-3f70-11e6-8a84-bae50000008b",
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
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/1483952f-32ca-11e6-8a84-bae500000007/accounts/1483a4fa-32ca-11e6-8a84-bae500000008",
      "type": "account",
      "mediaType": "application/json"
    }
  },
  "attributes": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/attributes/6a885b1b-3f70-11e6-8a84-bae50000009d",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "6a885b1b-3f70-11e6-8a84-bae50000009d",
      "name": "AttributeName1",
      "type": "string",
      "value": "Черный"
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/attributes/6a88619c-3f70-11e6-8a84-bae50000009e",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "6a88619c-3f70-11e6-8a84-bae50000009e",
      "name": "AttributeName2",
      "type": "double",
      "value": 0.4
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/attributes/6a886744-3f70-11e6-8a84-bae50000009f",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "6a886744-3f70-11e6-8a84-bae50000009f",
      "name": "AttributeName3",
      "type": "boolean",
      "value": true
    }
  ],
  "vatEnabled": true,
  "vatIncluded": true,
  "created": "2016-08-25 19:55:00",
  "printed": true,
  "published": true,
  "positions": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/ae7fa9fb-3f74-11e6-8a84-bae500000070/positions",
      "type": "purchaseorderposition",
      "mediaType": "application/json",
      "size": 3,
      "limit": 1000,
      "offset": 0
    }
  },
  "deliveryPlannedMoment": "2015-02-15 14:12:19",
  "payedSum": 0,
  "shippedSum": 0,
  "invoicedSum": 0,
  "waitSum": 5907132
}
```

### Массовое создание и обновление Заказов поставщику 
[Массовое создание и обновление](../#mojsklad-json-api-obschie-swedeniq-sozdanie-i-obnowlenie-neskol-kih-ob-ektow) Заказов поставщику.
В теле запроса нужно передать массив, содержащий JSON представления Заказов поставщику, которые вы хотите создать или обновить.
Обновляемые Заказы поставщику должны содержать идентификатор в виде метаданных.

> Пример создания и обновления нескольких Заказов поставщику

```shell
  curl -X POST
    "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '[
            {
              "name": "103034",
              "description": "Типичный заказ поставщику",
              "organization": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
                  "type": "organization",
                  "mediaType": "application/json"
                }
              },
              "code": "404",
              "moment": "2016-12-05 15:30:14",
              "applicable": true,
              "vatEnabled": true,
              "vatIncluded": true,
              "agent": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/1483952f-32ca-11e6-8a84-bae500000007",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
                  "type": "counterparty",
                  "mediaType": "application/json"
                }
              },
              "state": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/states/11f5becd-3f70-11e6-8a84-bae50000008b",
                  "type": "state",
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
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/contract/e105a2e7-3f6f-11e6-8a84-bae500000087",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/contract/metadata",
                  "type": "contract",
                  "mediaType": "application/json"
                }
              },
              "rate": {
                "currency": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/cdbc62de-3f68-11e6-8a84-bae500000050",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
                    "type": "currency",
                    "mediaType": "application/json"
                  }
                }
              },
              "deliveryPlannedMoment": "2015-02-15 14:12:19",
              "attributes": [
                {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/attributes/6a885b1b-3f70-11e6-8a84-bae50000009d",
                    "type": "attributemetadata",
                    "mediaType": "application/json"
                  },
                  "value": "Черный"
                },
                {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/attributes/6a88619c-3f70-11e6-8a84-bae50000009e",
                    "type": "attributemetadata",
                    "mediaType": "application/json"
                  },
                  "value": 0.4
                },
                {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/attributes/6a886744-3f70-11e6-8a84-bae50000009f",
                    "type": "attributemetadata",
                    "mediaType": "application/json"
                  },
                  "value": true
                }
              ]
            },
            {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/ae7fa9fb-3f74-11e6-8a84-bae500000070",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata",
                "type": "purchaseorder",
                "mediaType": "application/json"
              },
              "updated": "2016-07-01 13:15:05",
              "name": "777",
              "description": "Типичный заказ поставщику, с договором, другой валютой",
              "code": "404",
              "externalCode": "37KNBm7ф1gw7Zm00T5JdAt0",
              "moment": "2016-12-05 15:30:14",
              "applicable": false,
              "rate": {
                "currency": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/faf45b9a-2e58-11e6-8a84-bae500000055",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
                    "type": "currency",
                    "mediaType": "application/json"
                  }
                }
              },
              "contract": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/contract/e105a2e7-3f6f-11e6-8a84-bae500000087",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/contract/metadata",
                  "type": "contract",
                  "mediaType": "application/json"
                }
              },
              "agent": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/1485d676-32ca-11e6-8a84-bae500000009",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
                  "type": "counterparty",
                  "mediaType": "application/json"
                }
              },
              "state": null,
              "organizationAccount": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e/accounts/fae39d66-2e58-11e6-8a84-bae50000004f",
                  "type": "account",
                  "mediaType": "application/json"
                }
              },
              "attributes": [
                {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/attributes/6a885b1b-3f70-11e6-8a84-bae50000009d",
                    "type": "attributemetadata",
                    "mediaType": "application/json"
                  },
                  "value": "AttributeValue1"
                },
                {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/attributes/6a88619c-3f70-11e6-8a84-bae50000009e",
                    "type": "attributemetadata",
                    "mediaType": "application/json"
                  },
                  "value": 0.99
                },
                {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/attributes/6a886744-3f70-11e6-8a84-bae50000009f",
                    "type": "attributemetadata",
                    "mediaType": "application/json"
                  },
                  "value": true
                }
              ],
              "vatEnabled": true,
              "vatIncluded": false,
              "positions": [],
              "deliveryPlannedMoment": "2016-02-15 14:12:19"
            }
          ]'  
```

> Response 200 (application/json)
Успешный запрос. Результат - массив JSON представлений созданных и обновленных Заказов поставщику.

```json
[
  {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/22b4caaa-3f74-11e6-8a84-bae500000069",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata",
      "type": "purchaseorder",
      "mediaType": "application/json"
    },
    "id": "22b4caaa-3f74-11e6-8a84-bae500000069",
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
    "updated": "2016-07-01 13:11:11",
    "name": "103034",
    "description": "Типичный заказ поставщику",
    "code": "404",
    "externalCode": "s30P0zlwg-1qxSZnRVONF0",
    "moment": "2016-12-05 15:30:14",
    "applicable": true,
    "rate": {
      "currency": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/cdbc62de-3f68-11e6-8a84-bae500000050",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
          "type": "currency",
          "mediaType": "application/json"
        }
      },
      "value": 63
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
    "contract": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/contract/e105a2e7-3f6f-11e6-8a84-bae500000087",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/contract/metadata",
        "type": "contract",
        "mediaType": "application/json"
      }
    },
    "agent": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/1483952f-32ca-11e6-8a84-bae500000007",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
        "type": "counterparty",
        "mediaType": "application/json"
      }
    },
    "state": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/states/11f5becd-3f70-11e6-8a84-bae50000008b",
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
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/1483952f-32ca-11e6-8a84-bae500000007/accounts/1483a4fa-32ca-11e6-8a84-bae500000008",
        "type": "account",
        "mediaType": "application/json"
      }
    },
    "attributes": [
      {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/attributes/6a885b1b-3f70-11e6-8a84-bae50000009d",
          "type": "attributemetadata",
          "mediaType": "application/json"
        },
        "id": "6a885b1b-3f70-11e6-8a84-bae50000009d",
        "name": "AttributeName1",
        "type": "string",
        "value": "AttributeValue1"
      },
      {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/attributes/6a88619c-3f70-11e6-8a84-bae50000009e",
          "type": "attributemetadata",
          "mediaType": "application/json"
        },
        "id": "6a88619c-3f70-11e6-8a84-bae50000009e",
        "name": "AttributeName2",
        "type": "double",
        "value": 0.4
      },
      {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/attributes/6a886744-3f70-11e6-8a84-bae50000009f",
          "type": "attributemetadata",
          "mediaType": "application/json"
        },
        "id": "6a886744-3f70-11e6-8a84-bae50000009f",
        "name": "AttributeName1",
        "type": "boolean",
        "value": true
      }
    ],
    "vatEnabled": true,
    "vatIncluded": true,
    "created": "2016-08-25 19:55:00",
    "printed": true,
    "published": true,
    "positions": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/22b4caaa-3f74-11e6-8a84-bae500000069/positions",
        "type": "purchaseorderposition",
        "mediaType": "application/json",
        "size": 0,
        "limit": 1000,
        "offset": 0
      }
    },
    "deliveryPlannedMoment": "2015-02-15 14:12:19",
    "payedSum": 0,
    "shippedSum": 0,
    "invoicedSum": 0,
    "waitSum": 0
  },
  {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/ae7fa9fb-3f74-11e6-8a84-bae500000070",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata",
      "type": "purchaseorder",
      "mediaType": "application/json"
    },
    "id": "ae7fa9fb-3f74-11e6-8a84-bae500000070",
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
    "updated": "2016-07-01 13:23:26",
    "name": "777",
    "description": "Типичный заказ поставщику, с договором, другой валютой",
    "code": "404",
    "externalCode": "37KNBm7ф1gw7Zm00T5JdAt0",
    "moment": "2016-12-05 15:30:14",
    "applicable": false,
    "rate": {
      "currency": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/faf45b9a-2e58-11e6-8a84-bae500000055",
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
    "contract": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/contract/e105a2e7-3f6f-11e6-8a84-bae500000087",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/contract/metadata",
        "type": "contract",
        "mediaType": "application/json"
      }
    },
    "agent": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/1485d676-32ca-11e6-8a84-bae500000009",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
        "type": "counterparty",
        "mediaType": "application/json"
      }
    },
    "state": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/states/11f5becd-3f70-11e6-8a84-bae50000008b",
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
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/1485d676-32ca-11e6-8a84-bae500000009/accounts/1485e43e-32ca-11e6-8a84-bae50000000a",
        "type": "account",
        "mediaType": "application/json"
      }
    },
    "attributes": [
      {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/attributes/6a885b1b-3f70-11e6-8a84-bae50000009d",
          "type": "attributemetadata",
          "mediaType": "application/json"
        },
        "id": "6a885b1b-3f70-11e6-8a84-bae50000009d",
        "name": "AttributeName1",
        "type": "string",
        "value": "AttributeValue1"
      },
      {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/attributes/6a88619c-3f70-11e6-8a84-bae50000009e",
          "type": "attributemetadata",
          "mediaType": "application/json"
        },
        "id": "6a88619c-3f70-11e6-8a84-bae50000009e",
        "name": "AttributeName2",
        "type": "double",
        "value": 0.99
      },
      {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/attributes/6a886744-3f70-11e6-8a84-bae50000009f",
          "type": "attributemetadata",
          "mediaType": "application/json"
        },
        "id": "6a886744-3f70-11e6-8a84-bae50000009f",
        "name": "AttributeName3",
        "type": "boolean",
        "value": true
      }
    ],
    "vatEnabled": true,
    "vatIncluded": false,
    "created": "2016-08-25 19:55:00",
    "printed": true,
    "published": true,
    "positions": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/ae7fa9fb-3f74-11e6-8a84-bae500000070/positions",
        "type": "purchaseorderposition",
        "mediaType": "application/json",
        "size": 0,
        "limit": 1000,
        "offset": 0
      }
    },
    "deliveryPlannedMoment": "2016-02-15 14:12:19",
    "payedSum": 0,
    "shippedSum": 0,
    "invoicedSum": 0,
    "waitSum": 0
  }
]
```

### Удалить Заказ поставщику

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Заказа поставщику.|

> Запрос на удаление Заказа поставщику с указанным id.

```shell
curl -X DELETE
  "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/7944ef04-f831-11e5-7a69-971500188b19"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешное удаление Заказа поставщику.

### Массовое удаление Заказов Поставщикам

В теле запроса нужно передать массив, содержащий JSON метаданных Заказов Поставщикам, которые вы хотите удалить.


> Запрос на массовое удаление Заказов Поставщикам. 

```shell
curl -X POST
  "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/delete"
  -H "Authorization: Basic <Credentials>"
  -H "Content-Type: application/json"
  -d '[
        {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/7944ef04-f831-11e5-7a69-971500188b1",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata",
            "type": "purchaseorder",
            "mediaType": "application/json"
        },
        {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/7944ef04-f831-11e5-7a69-971500188b2",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata",
            "type": "purchaseorder",
            "mediaType": "application/json"
        }
      ]'
```        

> Успешный запрос. Результат - JSON информация об удалении Заказов Поставщикам.

```json
[
  {
    "info":"Сущность 'purchaseorder' с UUID: 7944ef04-f831-11e5-7a69-971500188b1 успешно удалена"
  },
  {
    "info":"Сущность 'purchaseorder' с UUID: 7944ef04-f831-11e5-7a69-971500188b2 успешно удалена"
  }
]
``` 

### Метаданные Заказов Поставщикам 
#### Метаданные Заказов Поставщикам 
Запрос на получение метаданных Заказов поставщикам. Результат - объект JSON, включающий в себя:

| Параметр                | Описание  |
| ------------------------------ |:---------------------------|
| **meta**         | Ссылка на метаданные Заказов поставщикам|
| **attributes**   | Массив объектов доп. полей Заказов поставщикам в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye)|
| **states**       | Массив статусов Заказов поставщикам|
| **createShared** | создавать новые Заказы поставщикам с меткой "Общий"|


Структура отдельного объекта, представляющего доп. поле подробно описана в разделе [Работа с дополнительными полями](../#mojsklad-json-api-obschie-swedeniq-rabota-s-dopolnitel-nymi-polqmi).

> Метаданные Заказов Поставщикам

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление доп. полей Заказов поставщикам.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata",
    "mediaType": "application/json"
  },
  "attributes": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/attributes/6a885b1b-3f70-11e6-8a84-bae50000009d",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "6a885b1b-3f70-11e6-8a84-bae50000009d",
      "name": "AttributeName1",
      "type": "string",
      "required": false
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/attributes/6a88619c-3f70-11e6-8a84-bae50000009e",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "6a88619c-3f70-11e6-8a84-bae50000009e",
      "name": "AttributeName2",
      "type": "double",
      "required": false
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/attributes/6a886744-3f70-11e6-8a84-bae50000009f",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "6a886744-3f70-11e6-8a84-bae50000009f",
      "name": "AttributeName3",
      "type": "boolean",
      "required": false
    }
  ],
  "states": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/states/11f5becd-3f70-11e6-8a84-bae50000008b",
        "type": "state",
        "mediaType": "application/json"
      },
      "id": "11f5becd-3f70-11e6-8a84-bae50000008b",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "name": "Ожидает отправки",
      "color": 10066329,
      "stateType": "Regular",
      "entityType": "purchaseorder"
    }
  ],
  "createShared": false
}
```

### Отдельное доп. поле

#### Отдельное доп. поле

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Доп. поля.|
 
> Запрос на получение информации по отдельному дополнительному полю.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/attributes/7944ef04-f831-11e5-7a69-971500188b19"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление отдельного доп. поля.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/attributes/6a88619c-3f70-11e6-8a84-bae50000009e",
    "type": "attributemetadata",
    "mediaType": "application/json"
  },
  "id": "6a88619c-3f70-11e6-8a84-bae50000009e",
  "name": "AttributeName3",
  "type": "double",
  "required": false
}
```

### Шаблон Заказа поставщику 
#### Шаблон Заказа поставщику 
Запрос на получение предзаполненого стандартными значениями шаблона заказа поставщику без связи с каким-либо документом.

> Шаблон заказа поставщику

```shell
  curl -X PUT
    "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/new
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d ''  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление предзаполненного заказа поставщику.

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
  "moment": "2016-11-25 17:33:33",
  "applicable": true,
  "sum": 0,
  "store": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/b942743c-9128-11e6-8a84-bae500000053",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
      "type": "store",
      "mediaType": "application/json"
    }
  },
  "project": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/project/6c6dd3f9-97a1-11e6-8a84-bae500000002",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/project/metadata",
      "type": "project",
      "mediaType": "application/json"
    }
  },
  "agent": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/b942953e-9128-11e6-8a84-bae500000054",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
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
  "organizationAccount": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/b9324d71-9128-11e6-8a84-bae500000051/accounts/b932bc5b-9128-11e6-8a84-bae500000052",
      "type": "account",
      "mediaType": "application/json"
    }
  },
  "positions": {
    "rows": []
  },
  "vatEnabled": true,
  "vatIncluded": true,
  "printed": true,
  "published": true,
  "payedSum": 0,
  "shippedSum": 0,
  "invoicedSum": 0
}
```

### Шаблон Заказа поставщику на основе 
Запрос на получение предзаполненного шаблона заказа поставщику на основе внутреннего заказа или заказа покупателя.
В ответ на запрос вернется предзаполненный шаблон заказа поставщику, который
затем можно будет использовать для создания нового заказа с помощью POST запроса.

> Пример запроса на получение шаблона заказа поставщику на основе внутреннего заказа.

```shell
  curl -X PUT
    "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/new"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "internalOrder": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/64e426af-b0d8-11e6-8a84-bae500000064",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/metadata",
                "type": "internalorder",
                "mediaType": "application/json"
              }
            }
          }'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление предзаполненного заказа поставщику.

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
  "moment": "2016-11-25 17:34:37",
  "applicable": true,
  "rate": {
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/b942e6f2-9128-11e6-8a84-bae500000058",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json"
      }
    }
  },
  "sum": 9910,
  "store": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/b942743c-9128-11e6-8a84-bae500000053",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
      "type": "store",
      "mediaType": "application/json"
    }
  },
  "project": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/project/6c6dd3f9-97a1-11e6-8a84-bae500000002",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/project/metadata",
      "type": "project",
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
  "created": "2016-08-25 19:55:00",
  "printed": true,
  "published": true,
  "positions": {
    "rows": [
      {
        "quantity": 1,
        "price": 2230,
        "discount": 0,
        "vat": 0,
        "vatEnabled": false,
        "assortment": {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/f4ac4460-acf7-11e6-8a84-bae500000068",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
            "type": "product",
            "mediaType": "application/json",
            "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=3b1e1f15-2842-11e9-ac12-000c0000002f"
          }
        },
        "shipped": 0,
        "inTransit": 0
      },
      {
        "quantity": 1,
        "price": 100,
        "discount": 10,
        "vat": 10,
        "vatEnabled": true,
        "assortment": {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/f4ac4460-acf7-11e6-8a84-bae500000068",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
            "type": "product",
            "mediaType": "application/json",
            "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=e64d0a86-2a99-11e9-ac12-000c00000041"
          }
        },
        "shipped": 0,
        "inTransit": 0
      },
      {
        "quantity": 2,
        "price": 500,
        "discount": 10,
        "vat": 18,
        "vatEnabled": true,
        "assortment": {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/f4ac4460-acf7-11e6-8a84-bae500000068",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
            "type": "product",
            "mediaType": "application/json",
            "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=392c045c-2842-11e9-ac12-000a00000002"
          }
        },
        "shipped": 0,
        "inTransit": 0
      },
      {
        "quantity": 3,
        "price": 2230,
        "discount": 0,
        "vat": 0,
        "vatEnabled": false,
        "assortment": {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/f4ac4460-acf7-11e6-8a84-bae500000068",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
            "type": "product",
            "mediaType": "application/json",
            "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=3bb1af6c-2842-11e9-ac12-000c00000061"
          }
        },
        "shipped": 0,
        "inTransit": 0
      }
    ]
  },
  "vatEnabled": true,
  "vatIncluded": true,
  "payedSum": 0,
  "shippedSum": 0,
  "invoicedSum": 0,
  "internalOrder": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/64e426af-b0d8-11e6-8a84-bae500000064",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/metadata",
      "type": "internalorder",
      "mediaType": "application/json"
    }
  }
}
```

> Пример запроса на получение шаблона заказа поставщику на основе заказа покупателя.

```shell
  curl -X PUT
    "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/new"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "customerOrders": [
              {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/customerorder/e9350b05-5751-11e8-9109-f8fc0010fba3",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/customerorder/metadata",
                  "type": "customerorder",
                  "mediaType": "application/json"
                }
              }
            ]
          }'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление предзаполненного заказа поставщику.

```json
{
  "owner": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/8187b9ca-5751-11e8-9107-504800110aa3",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
      "type": "employee",
      "mediaType": "application/json"
    }
  },
  "shared": false,
  "group": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/group/816f2c7e-5751-11e8-9109-f8fc0000534e",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/group/metadata",
      "type": "group",
      "mediaType": "application/json"
    }
  },
  "name": "",
  "moment": "2018-05-14 11:39:50",
  "applicable": true,
  "rate": {
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/819ac910-5751-11e8-9107-504800110ad2",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json"
      }
    }
  },
  "sum": 10000,
  "store": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/819ab5e8-5751-11e8-9107-504800110acd",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
      "type": "store",
      "mediaType": "application/json"
    }
  },
  "organization": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/81995e7d-5751-11e8-9107-504800110acb",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
      "type": "organization",
      "mediaType": "application/json"
    }
  },
  "positions": {
    "rows": [
      {
        "quantity": 20,
        "price": 500,
        "discount": 0,
        "vat": 18,
        "vatEnabled": true,
        "assortment": {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/cbe0b7bc-5751-11e8-9ff4-31500010c0aa",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
            "type": "product",
            "mediaType": "application/json",
            "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=3bb1af6c-2842-11e9-ac12-000c00000061"
          }
        },
        "shipped": 0,
        "inTransit": 0
      }
    ]
  },
  "vatEnabled": true,
  "vatIncluded": true,
  "printed": true,
  "published": true,
  "payedSum": 0,
  "shippedSum": 0,
  "invoicedSum": 0,
  "waitSum": 0,
  "customerOrders": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/customerorder/e9350b05-5751-11e8-9109-f8fc0010fba3",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/customerorder/metadata",
        "type": "customerorder",
        "mediaType": "application/json"
      }
    }
  ]
}

```

### Заказ поставщику

### Получить Заказ поставщику

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Заказа поставщику.|
 
> Запрос на получение отдельного Заказа поставщику с указанным id.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/7944ef04-f831-11e5-7a69-971500188b19"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление Заказа поставщику.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/172fb2f6-3f70-11e6-8a84-bae50000008e",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata",
    "type": "purchaseorder",
    "mediaType": "application/json"
  },
  "id": "172fb2f6-3f70-11e6-8a84-bae50000008e",
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
  "updated": "2016-07-01 12:42:13",
  "name": "00002",
  "description": "Описание заказа",
  "externalCode": "FfSmVuSKi7h8L-jLADHV80",
  "moment": "2016-07-01 12:40:00",
  "applicable": true,
  "rate": {
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/faf45b9a-2e58-11e6-8a84-bae500000055",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json"
      }
    }
  },
  "sum": 5900,
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
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/contract/e105a2e7-3f6f-11e6-8a84-bae500000087",
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
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/14ae5431-32ca-11e6-8a84-bae50000002d",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
      "mediaType": "application/json"
    }
  },
  "state": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/states/11f5becd-3f70-11e6-8a84-bae50000008b",
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
  "vatEnabled": true,
  "vatIncluded": true,
  "printed": true,
  "published": true,
  "positions": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/172fb2f6-3f70-11e6-8a84-bae50000008e/positions",
      "type": "purchaseorderposition",
      "mediaType": "application/json",
      "size": 5,
      "limit": 1000,
      "offset": 0
    }
  },
  "deliveryPlannedMoment": "2016-07-15 12:40:00",
  "payedSum": 0,
  "shippedSum": 0,
  "invoicedSum": 0,
  "waitSum": 5900
}
```

### Изменить Заказ поставщику 
Запрос на обновление Заказа поставщику с указанным id.
В теле запроса можно указать только те поля, которые необходимо изменить у Заказа поставщику, кроме тех, что
помечены `Только для чтения` в описании [атрибутов Заказа поставщику](../documents/#dokumenty-zakaz-postawschiku).
При обновлении полей **organization** и **agent** нужно также обновить поля **organizationAccount** и
**agentAccount** соответственно, иначе произойдет ошибка.

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Заказа поставщику.|

> Пример запроса на обновление отдельного Заказа поставщику.

```shell
  curl -X PUT
    "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/7944ef04-f831-11e5-7a69-971500188b19"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "updated": "2016-07-01 13:15:05",
            "name": "777",
            "description": "Типичный заказ поставщику, с договором, другой валютой",
            "code": "404",
            "externalCode": "37KNBm7ф1gw7Zm00T5JdAt0",
            "moment": "2016-12-05 15:30:14",
            "applicable": false,
            "rate": {
              "currency": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/faf45b9a-2e58-11e6-8a84-bae500000055",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
                  "type": "currency",
                  "mediaType": "application/json"
                }
              }
            },
            "contract": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/contract/e105a2e7-3f6f-11e6-8a84-bae500000087",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/contract/metadata",
                "type": "contract",
                "mediaType": "application/json"
              }
            },
            "agent": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/1485d676-32ca-11e6-8a84-bae500000009",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
                "type": "counterparty",
                "mediaType": "application/json"
              }
            },
            "state": null,
            "organizationAccount": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e/accounts/fae39d66-2e58-11e6-8a84-bae50000004f",
                "type": "account",
                "mediaType": "application/json"
              }
            },
            "attributes": [
              {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/attributes/6a885b1b-3f70-11e6-8a84-bae50000009d",
                  "type": "attributemetadata",
                  "mediaType": "application/json"
                },
                "value": "AttributeValue1"
              },
              {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/attributes/6a88619c-3f70-11e6-8a84-bae50000009e",
                  "type": "attributemetadata",
                  "mediaType": "application/json"
                },
                "value": 0.99
              },
              {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/attributes/6a886744-3f70-11e6-8a84-bae50000009f",
                  "type": "attributemetadata",
                  "mediaType": "application/json"
                },
                "value": true
              }
            ],
            "vatEnabled": true,
            "vatIncluded": false,
            "positions": [],
            "deliveryPlannedMoment": "2016-02-15 14:12:19"
          }'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление обновленного Заказа поставщику.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/ae7fa9fb-3f74-11e6-8a84-bae500000070",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata",
    "type": "purchaseorder",
    "mediaType": "application/json"
  },
  "id": "ae7fa9fb-3f74-11e6-8a84-bae500000070",
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
  "updated": "2016-07-01 13:23:26",
  "name": "777",
  "description": "Типичный заказ поставщику, с договором, другой валютой",
  "code": "404",
  "externalCode": "37KNBm7ф1gw7Zm00T5JdAt0",
  "moment": "2016-12-05 15:30:14",
  "applicable": false,
  "rate": {
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/faf45b9a-2e58-11e6-8a84-bae500000055",
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
  "contract": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/contract/e105a2e7-3f6f-11e6-8a84-bae500000087",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/contract/metadata",
      "type": "contract",
      "mediaType": "application/json"
    }
  },
  "agent": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/1485d676-32ca-11e6-8a84-bae500000009",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
      "mediaType": "application/json"
    }
  },
  "state": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/states/11f5becd-3f70-11e6-8a84-bae50000008b",
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
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/1485d676-32ca-11e6-8a84-bae500000009/accounts/1485e43e-32ca-11e6-8a84-bae50000000a",
      "type": "account",
      "mediaType": "application/json"
    }
  },
  "attributes": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/attributes/6a885b1b-3f70-11e6-8a84-bae50000009d",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "6a885b1b-3f70-11e6-8a84-bae50000009d",
      "name": "AttributeName1",
      "type": "string",
      "value": "AttributeValue1"
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/attributes/6a88619c-3f70-11e6-8a84-bae50000009e",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "6a88619c-3f70-11e6-8a84-bae50000009e",
      "name": "AttributeName2",
      "type": "double",
      "value": 0.99
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata/attributes/6a886744-3f70-11e6-8a84-bae50000009f",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "6a886744-3f70-11e6-8a84-bae50000009f",
      "name": "AttributeName3",
      "type": "boolean",
      "value": true
    }
  ],
  "vatEnabled": true,
  "vatIncluded": false,
  "created": "2016-08-25 19:55:00",
  "printed": true,
  "published": true,
  "positions": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/ae7fa9fb-3f74-11e6-8a84-bae500000070/positions",
      "type": "purchaseorderposition",
      "mediaType": "application/json",
      "size": 0,
      "limit": 1000,
      "offset": 0
    }
  },
  "deliveryPlannedMoment": "2016-02-15 14:12:19",
  "payedSum": 0,
  "shippedSum": 0,
  "invoicedSum": 0,
  "waitSum": 0
}
```

### Позиции Заказа поставщику 
Отдельный ресурс для управления позициями Заказа поставщику. С его помощью вы можете управлять позициями большого документа, количество строк в котором превышает лимит на количество строк, сохраняемых вместе с документом. Этот лимит равен 1000. Более подробно о лимитах на количество строк документа и работе с большими документами можно прочитать [тут](../#mojsklad-json-api-obschie-swedeniq-rabota-s-poziciqmi-dokumentow).

### Получить позиции Заказа поставщику 
Запрос на получение списка всех позиций данного Заказа поставщику.


| Название  | Тип | Описание                    |
| --------- |:----|:----------------------------|
**meta** |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные о выдаче,
**context** | [Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye) | Метаданные о сотруднике, выполнившем запрос.
**rows** |Array(Object)|Массив JSON объектов, представляющих собой позиции Заказа поставщику.

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Заказа поставщику.|
|**limit** |  `number` (optional) **Default: 1000** *Example: 1000* Максимальное количество сущностей для извлечения.`Допустимые значения 1 - 1000`.|
|**offset** |  `number` (optional) **Default: 0** *Example: 40* Отступ в выдаваемом списке сущностей.|

> Получить позиции Заказа поставщику

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/purchaseOrder/7944ef04-f831-11e5-7a69-971500188b19/positions"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление списка позиций отдельного Заказа поставщику.

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
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/7944ef04-f831-11e5-7a69-971500188b19/positions/",
    "type": "purchaseorderposition",
    "mediaType": "application/json",
    "size": 5,
    "limit": 1000,
    "offset": 0
  },
  "rows": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/7944ef04-f831-11e5-7a69-971500188b19/positions/17307520-3f70-11e6-8a84-bae50000008f",
        "type": "purchaseorderposition",
        "mediaType": "application/json"
      },
      "id": "17307520-3f70-11e6-8a84-bae50000008f",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "quantity": 1,
      "price": 4300,
      "discount": 0,
      "vat": 0,
      "vatEnabled": false,
      "assortment": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/0a89c6f1-3303-11e6-8a84-bae500000cda",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
          "type": "product",
          "mediaType": "application/json",
          "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=3bb1af6c-2842-11e9-ac12-000c00000061"
        }
      },
      "shipped": 0,
      "inTransit": 1
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/7944ef04-f831-11e5-7a69-971500188b19/positions/17308a33-3f70-11e6-8a84-bae500000090",
        "type": "purchaseorderposition",
        "mediaType": "application/json"
      },
      "id": "17308a33-3f70-11e6-8a84-bae500000090",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "quantity": 1,
      "price": 600,
      "discount": 0,
      "vat": 0,
      "vatEnabled": false,
      "assortment": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/0163030c-3303-11e6-8a84-bae5000004de",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
          "type": "product",
          "mediaType": "application/json",
          "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=392c045c-2842-11e9-ac12-000a00000002"
        }
      },
      "shipped": 0,
      "inTransit": 1
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/7944ef04-f831-11e5-7a69-971500188b19/positions/17309bf8-3f70-11e6-8a84-bae500000091",
        "type": "purchaseorderposition",
        "mediaType": "application/json"
      },
      "id": "17309bf8-3f70-11e6-8a84-bae500000091",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "quantity": 1,
      "price": 0,
      "discount": 0,
      "vat": 0,
      "vatEnabled": false,
      "assortment": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/4f918196-3304-11e6-8a84-bae50001c6d2",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
          "type": "product",
          "mediaType": "application/json",
          "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=3b1e1f15-2842-11e9-ac12-000c0000002f"
        }
      },
      "shipped": 0,
      "inTransit": 1
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/7944ef04-f831-11e5-7a69-971500188b19/positions/1730ac60-3f70-11e6-8a84-bae500000092",
        "type": "purchaseorderposition",
        "mediaType": "application/json"
      },
      "id": "1730ac60-3f70-11e6-8a84-bae500000092",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "quantity": 1,
      "price": 0,
      "discount": 0,
      "vat": 0,
      "vatEnabled": false,
      "assortment": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/4f785efd-3304-11e6-8a84-bae50001c6c4",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
          "type": "product",
          "mediaType": "application/json",
          "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=e64d0a86-2a99-11e9-ac12-000c00000041"
        }
      },
      "shipped": 0,
      "inTransit": 1
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/7944ef04-f831-11e5-7a69-971500188b19/positions/1730bb31-3f70-11e6-8a84-bae500000093",
        "type": "purchaseorderposition",
        "mediaType": "application/json"
      },
      "id": "1730bb31-3f70-11e6-8a84-bae500000093",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "quantity": 1,
      "price": 1000,
      "discount": 0,
      "vat": 0,
      "vatEnabled": false,
      "assortment": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/7b37adef-3303-11e6-8a84-bae50000bbf7",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
          "type": "product",
          "mediaType": "application/json",
          "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=3c3c1618-2842-11e9-ac12-000c0000006f"
        }
      },
      "shipped": 0,
      "inTransit": 1
    }
  ]
}
```

### Создать позицию Заказа поставщику 
Запрос на создание новой позиции в Заказе поставщику.
Для успешного создания необходимо в теле запроса указать следующие поля:

+ **assortment** - Ссылка на товар/услугу/серию/модификацию, которую представляет собой позиция.
Также можно указать поле с именем **service**, **consignment**, **variant** в соответствии с тем,
чем является указанная позиция. Подробнее об этом поле можно прочитать в описании [позиции Заказа](../documents/#dokumenty-zakaz-postawschiku-zakazy-postawschikam-pozicii-zakaza-postawschiku)
+ **quantity** - Количество указанной позиции. Должно быть положительным, иначе возникнет ошибка.

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Заказа поставщику.|

> Пример создания одной позиции в Заказе поставщику.

```shell
  curl -X POST
    "https://online.moysklad.ru/api/remap/1.2/entity/purchaseOrder/7944ef04-f831-11e5-7a69-971500188b19/positions"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "quantity": 49,
            "price": 451,
            "discount": 0,
            "vat": 10,
            "assortment": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/variant/7a7daa6b-3c64-11e6-8a84-bae50000000a",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/variant/metadata",
                "type": "variant",
                "mediaType": "application/json"
              }
            },
            "shipped": 20,
            "inTransit": 19
          }'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление созданной позиции отдельного Заказа поставщику.

```json
[
  {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/7944ef04-f831-11e5-7a69-971500188b19/positions/574b6485-3f71-11e6-8a84-bae50000005b",
      "type": "purchaseorderposition",
      "mediaType": "application/json"
    },
    "id": "574b6485-3f71-11e6-8a84-bae50000005b",
    "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
    "quantity": 49,
    "price": 451,
    "discount": 0,
    "vat": 10,
    "vatEnabled": true,
    "assortment": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/variant/7a7daa6b-3c64-11e6-8a84-bae50000000a",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/variant/metadata",
        "type": "variant",
        "mediaType": "application/json",
        "uuidHref": "https://online.moysklad.ru/app/#feature/edit?id=3c3c1618-2842-11e9-ac12-000c0000006f"
      }
    },
    "shipped": 0,
    "inTransit": 19
  }
]
```

> Пример создания сразу нескольких позиций в Заказе поставщику.

```shell
  curl -X POST
    "https://online.moysklad.ru/api/remap/1.2/entity/purchaseOrder/7944ef04-f831-11e5-7a69-971500188b19/positions"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '[
            {
              "quantity": 12,
              "price": 300,
              "vat": 0,
              "assortment": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/variant/7a81082f-3c64-11e6-8a84-bae50000000e",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/variant/metadata",
                  "type": "variant",
                  "mediaType": "application/json"
                }
              },
              "inTransit": 11
            },
            {
              "quantity": 3,
              "price": 1000,
              "discount": 0,
              "vat": 10,
              "assortment": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/7a6f697f-3c64-11e6-8a84-bae500000006",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                  "type": "product",
                  "mediaType": "application/json"
                }
              },
              "inTransit": 1
            },
            {
              "quantity": 404,
              "price": 454,
              "discount": 200,
              "vat": 21,
              "assortment": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/variant/7a83c422-3c64-11e6-8a84-bae500000012",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/variant/metadata",
                  "type": "variant",
                  "mediaType": "application/json"
                }
              },
              "inTransit": 216
            }
          ]'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление списка созданных позиций отдельного Заказа поставщику.

```json
[
  {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/7944ef04-f831-11e5-7a69-971500188b19/positions/f389488d-3f71-11e6-8a84-bae50000005f",
      "type": "purchaseorderposition",
      "mediaType": "application/json"
    },
    "id": "f389488d-3f71-11e6-8a84-bae50000005f",
    "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
    "quantity": 12,
    "price": 300,
    "discount": 0,
    "vat": 0,
    "vatEnabled": false,
    "assortment": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/variant/7a81082f-3c64-11e6-8a84-bae50000000e",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/variant/metadata",
        "type": "variant",
        "mediaType": "application/json",
        "uuidHref": "https://online.moysklad.ru/app/#feature/edit?id=3c3c1618-2842-11e9-ac12-000c0000006f"
      }
    },
    "shipped": 0,
    "inTransit": 11
  },
  {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/7944ef04-f831-11e5-7a69-971500188b19/positions/f389521b-3f71-11e6-8a84-bae500000060",
      "type": "purchaseorderposition",
      "mediaType": "application/json"
    },
    "id": "f389521b-3f71-11e6-8a84-bae500000060",
    "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
    "quantity": 3,
    "price": 1000,
    "discount": 0,
    "vat": 10,
    "vatEnabled": true,
    "assortment": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/7a6f697f-3c64-11e6-8a84-bae500000006",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
        "type": "product",
        "mediaType": "application/json",
        "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=e64d0a86-2a99-11e9-ac12-000c00000041"
      }
    },
    "shipped": 0,
    "inTransit": 1
  },
  {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/7944ef04-f831-11e5-7a69-971500188b19/positions/f3895aa1-3f71-11e6-8a84-bae500000061",
      "type": "purchaseorderposition",
      "mediaType": "application/json"
    },
    "id": "f3895aa1-3f71-11e6-8a84-bae500000061",
    "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
    "quantity": 404,
    "price": 454,
    "discount": 200,
    "vat": 21,
    "vatEnabled": true,
    "assortment": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/variant/7a83c422-3c64-11e6-8a84-bae500000012",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/variant/metadata",
        "type": "variant",
        "mediaType": "application/json",
        "uuidHref": "https://online.moysklad.ru/app/#feature/edit?id=3b1e1f15-2842-11e9-ac12-000c0000002f"
      }
    },
    "shipped": 0,
    "inTransit": 216
  }
]
```

### Позиция Заказа 
Отдельная позиция Заказа с указанным id позиции.

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Заказа поставщику.|
|**positionID**|  `string` (required) *Example: 34f6344f-015e-11e6-9464-e4de0000006c* id позиции Заказа поставщику.|

### Получить позицию Заказа 
> Запрос на получение отдельной позиции Заказа с указанным id.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/7944ef04-f831-11e5-7a69-971500188b19/positions/34f6344f-015e-11e6-9464-e4de0000006c"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление отдельной позиции Заказа поставщику.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/7944ef04-f831-11e5-7a69-971500188b19/positions/34f6344f-015e-11e6-9464-e4de0000006c",
    "type": "purchaseorderposition",
    "mediaType": "application/json"
  },
  "id": "34f6344f-015e-11e6-9464-e4de0000006c",
  "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
  "quantity": 1,
  "price": 1000,
  "discount": 0,
  "vat": 0,
  "vatEnabled": false,
  "assortment": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/7b37adef-3303-11e6-8a84-bae50000bbf7",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
      "type": "product",
      "mediaType": "application/json",
      "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=3b1e1f15-2842-11e9-ac12-000c0000002f"
    }
  },
  "shipped": 0,
  "inTransit": 1
}
```

### Изменить позицию Заказа 
Запрос на обновление отдельной позиции Заказа. Для обновления позиции нет каких-либо
 обязательных для указания в теле запроса полей. Только те, что вы желаете обновить.
 
 **Параметры**
 
|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Заказа поставщику.|
|**positionID**|  `string` (required) *Example: 34f6344f-015e-11e6-9464-e4de0000006c* id позиции Заказа поставщику.|

> Пример запроса на обновление отдельной позиции в Заказе поставщику.

```shell
  curl -X PUT
    "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/7944ef04-f831-11e5-7a69-971500188b19/positions/34f6344f-015e-11e6-9464-e4de0000006c"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "quantity": 44,
            "price": 4540,
            "discount": 150,
            "vat": 10,
            "assortment": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/variant/7a83c422-3c64-11e6-8a84-bae500000012",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/variant/metadata",
                "type": "variant",
                "mediaType": "application/json"
              }
            },
            "shipped": 10,
            "inTransit": 200
          }'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление обновленной позиции Заказа поставщику.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/7944ef04-f831-11e5-7a69-971500188b19/positions/34f6344f-015e-11e6-9464-e4de0000006c",
    "type": "purchaseorderposition",
    "mediaType": "application/json"
  },
  "id": "34f6344f-015e-11e6-9464-e4de0000006c",
  "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
  "quantity": 44,
  "price": 4540,
  "discount": 150,
  "vat": 10,
  "vatEnabled": true,
  "assortment": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/variant/7a83c422-3c64-11e6-8a84-bae500000012",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/variant/metadata",
      "type": "variant",
      "mediaType": "application/json",
      "uuidHref": "https://online.moysklad.ru/app/#feature/edit?id=3b1e1f15-2842-11e9-ac12-000c0000002f"
    }
  },
  "shipped": 0,
  "inTransit": 200
}
```

### Удалить позицию

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Заказа поставщику.|
|**positionID**|  `string` (required) *Example: 34f6344f-015e-11e6-9464-e4de0000006c* id позиции Заказа поставщику.|
 
> Запрос на удаление отдельной позиции Заказа с указанным id.

```shell
curl -X DELETE
  "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/7944ef04-f831-11e5-7a69-971500188b19/positions/34f6344f-015e-11e6-9464-e4de0000006c"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешное удаление позиции Заказа.

