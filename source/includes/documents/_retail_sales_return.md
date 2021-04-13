## Розничный возврат
Средствами JSON API можно создавать и обновлять сведения о Розничных возвратах, запрашивать списки Розничных возвратов и сведения по отдельным Розничным возвратам. Позициями Розничных возвратов  можно управлять как в составе отдельного Возврата, так и отдельно - с помощью специальных ресурсов для управления позициями Розничного возврата. Кодом сущности для Розничного возврата в составе JSON API является ключевое слово **retailsalesreturn**.
### Розничные возвраты 
#### Атрибуты сущности

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные Розничного возврата|&mdash;|да
|**id**                 |UUID|ID Розничного возврата|Только для чтения|да
|**accountId**          |UUID| ID учетной записи|Только для чтения|да
|**syncId**             |UUID|ID синхронизации. После заполнения недоступен для изменения|&mdash;|нет
|**updated**            |DateTime|Момент последнего обновления Розничного возврата|Только для чтения|да
|**deleted**            |DateTime|Момент последнего удаления Розничного возврата|Только для чтения|нет
|**name**               |String(255)|Наименование Розничного возврата|&mdash;|да
|**description**        |String(4096)|Комментарий Розничного возврата|&mdash;|нет
|**externalCode**       |String(255)|Внешний код Розничного возврата|&mdash;| да
|**moment**             |DateTime|Дата Счета|&mdash;|да
|**applicable**         |Boolean|Отметка о проведении|&mdash;|да
|**vatEnabled**         |Boolean|Учитывается ли НДС|&mdash;|да
|**vatIncluded**        |Boolean| Включен ли НДС в цену|&mdash;|нет
|**sum**                |Int|Сумма Розничного возврата в копейках|Только для чтения|да
|**project**            |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные проекта|&mdash;|нет
|**rate**               |Object|Валюта. [Подробнее тут](../documents/#dokumenty-obschie-swedeniq-valuta-w-dokumentah)|&mdash;|да
|**owner**              |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Владелец (Сотрудник)|&mdash;|да
|**shared**             |Boolean|Общий доступ|&mdash;|да
|**group**              |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Отдел сотрудника|&mdash;|да
|**organization**       |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные юрлица|Необходимое при создании|да
|**agent**              |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные контрагента|Необходимое при создании|да
|**store**              |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные склада|Необходимое при создании|да
|**contract**              |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные договора|&mdash;|нет
|**state**              |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные статуса Розничного возврата|&mdash;|нет
|**organizationAccount**|[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные счета юрлица|&mdash;|нет
|**agentAccount**       |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные счета контрагента|&mdash;|нет
|**attributes**         |Array(Object)|Коллекция метаданных доп. полей. [Поля объекта](../#mojsklad-json-api-obschie-swedeniq-rabota-s-dopolnitel-nymi-polqmi) |&mdash;|нет
|**created**            |DateTime|Дата создания|Только для чтения|да
|**printed**            |Boolean|Напечатан ли документ|Только для чтения|да
|**published**          |Boolean|Опубликован ли документ|Только для чтения|да
|**vatSum**                |Float|Сумма включая НДС|&mdash;|да
|**positions**          |MetaArray|Метаданные позиций Розничного возврата|&mdash;|да
|**demand**          |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные позиций Розничного возврата, по которой произошел возврат|&mdash;|нет
|**retailStore**         |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные Точки продаж|Необъодимое при создании|да
|**retailShift**        |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные Розничной смены|Необходимое при создании|да
|**cashSum**                |Float|Оплачено наличными|&mdash;|да
|**noCashSum**                |Float|Оплачено картой|&mdash;|да
|**qrSum**                |Float|Оплачено по QR-коду|&mdash;|да
|**taxSystem**         |Enum|Код системы налогообложения. [Подробнее тут](../dictionaries/#dokumenty-roznichnyj-wozwrat-roznichnye-wozwraty-atributy-suschnosti-kod-sistemy-nalogooblozheniq)|&mdash;|нет

##### Код системы налогообложения
Значения поля taxSystem.

| Значение                | Описание  |
| ------------------------------ |:---------------------------|
| **GENERAL_TAX_SYSTEM**                  | ОСН|
| **SIMPLIFIED_TAX_SYSTEM_INCOME**        | УСН. Доход|
| **SIMPLIFIED_TAX_SYSTEM_INCOME_OUTCOME**| УСН. Доход-Расход|
| **UNIFIED_AGRICULTURAL_TAX**            | ЕСХН|
| **PRESUMPTIVE_TAX_SYSTEM**              | ЕНВД|
| **PATENT_BASED**                        | Патент|

#### Позиции Розничного возврата
Позиции Розничного возврата - это список товаров/услуг/модификаций/серий.
Объект позиции Розничного возврата содержит следующие поля:

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
|**cost**          |Int|Себестоимость (только для услуг)|&mdash;|нет

С позициями можно работать с помощью специальных [ресурсов для управления позициями Розничного возврата](../documents/#dokumenty-roznichnyj-wozwrat-pozicii-roznichnogo-wozwrata),
а также в составе отдельного Розничного возврата. При работе в составе отдельного Розничного возврата,
вы можете отправлять запросы на создание отдельного Розничного возврата с включенным в тело запроса
массивом позиций Розничного возврата. Если количество позиций превышает максимально допустимое, то для
дальнейшего пополнения позиций нужно будет работать со специальным ресурсом "Позиции Розничного возврата".
Также, при работе в составе отдельного Розничного возврата, можно отправлять запросы на обновление списка позиций
с включенным в тело запроса массивом позиций Розничного возврата. При этом важно помнить, что коллекция позиций будет
восприниматься как "все позиции Розничного возврата" и полностью заменит уже существующую коллекцию при обновлении объекта - лишние
позиции будут удалены, новые добавлены, существующие - изменены.

О работе с доп. полями Розничных возвратов можно прочитать [здесь](../#mojsklad-json-api-obschie-swedeniq-rabota-s-dopolnitel-nymi-polqmi)

### Получить Розничные возвраты 
Запрос всех Розничных возвратов на данной учетной записи.
Результат: Объект JSON, включающий в себя поля:

| Название  | Тип | Описание                    |
| --------- |:----|:----------------------------|
**meta** |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные о выдаче,
**context** | [Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye) | Метаданные о сотруднике, выполнившем запрос.
**rows** |Array(Object)|Массив JSON объектов, представляющих собой Розничные возвраты.

**Параметры**

| Параметр                | Описание  |
| ------------------------------ |:---------------------------|
|**limit** |  `number` (optional) **Default: 1000** *Example: 1000* Максимальное количество сущностей для извлечения.`Допустимые значения 1 - 1000`.|
|**offset** |  `number` (optional) **Default: 0** *Example: 40* Отступ в выдаваемом списке сущностей.|

> Получить Розничные возвраты

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление списка Розничных возвратов.

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
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailSalesReturn",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailSalesReturn/metadata",
    "type": "retailsalesreturn",
    "mediaType": "application/json",
    "size": 1,
    "limit": 1000,
    "offset": 0
  },
  "rows": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/a62e39af-0c75-11e6-9464-e4de00000030",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/metadata",
        "type": "retailsalesreturn",
        "mediaType": "application/json"
      },
      "id": "a62e39af-0c75-11e6-9464-e4de00000030",
      "accountId": "84e60e93-f504-11e5-8a84-bae500000008",
      "updated": "2016-04-27 15:43:31",
      "name": "00001",
      "externalCode": "33YOoIGVhdPXFBr8QNbD50",
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
      "syncId": "eefa141e-0c65-4993-8b16-934905d47dbd",
      "moment": "2016-04-27 15:43:00",
      "applicable": true,
      "vatEnabled": true,
      "vatIncluded": true,
      "printed": true,
      "published": true,
      "sum": 14000,
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
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
          "type": "store",
          "mediaType": "application/json"
        }
      },
      "agent": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/8518d001-f504-11e5-8a84-bae50000016a",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
          "type": "counterparty",
          "mediaType": "application/json"
        }
      },
      "positions": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/a62e39af-0c75-11e6-9464-e4de00000030/positions",
          "type": "salesreturnposition",
          "mediaType": "application/json",
          "size": 3,
          "limit": 1000,
          "offset": 0
        }
      },
      "retailStore": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailstore/851f8576-f504-11e5-8a84-bae50000016c",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailstore/metadata",
          "type": "retailstore",
          "mediaType": "application/json"
        }
      },
      "demand": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/retaildemand/2ef43ba7-0c5a-11e6-9464-e4de0000000c",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retaildemand/metadata",
          "type": "retaildemand",
          "mediaType": "application/json"
        }
      },
      "retailShift": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailshift/9e46db1e-0c75-11e6-9464-e4de0000002b",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailshift/metadata",
          "type": "retailshift",
          "mediaType": "application/json"
        }
      },
      "taxSystem": "GENERAL_TAX_SYSTEM",
      "cashSum": 14000,
      "noCashSum": 0,
      "qrSum": 0
    }
  ]
}
```

### Создать Розничный возврат 
Розничная смена, на которую указывает ссылка при создании Розничного возврата обязательно должна быть активной.
При создании Розничного возврата через JSON API, дата, указанная в **moment** возврата
должна быть позже даты, указанной в **moment** активной розничной смены, иначе
произойдет ошибка.
Обязательные поля при создании нового Розничного возврата:

+ **name** - Номер возврата
+ **organization** - Ссылка на ваше юрлицо в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye)
+ **store** - Ссылка на склад в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye)
+ **demand** - Ссылка на Розничную продажу, по которой произошел возврат в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye), обязательное поле только для возврата на основании
+ **retailStore** - Ссылка на точку продаж в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye)
+ **retailShift** - Сссылка на Розничную смену, в рамках которой происходит возврат
+ **agent** - Ссылка на контрагента в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye).
Контрагент, указанный в запросе на создание возврата, должен совпадать с контрагентом, указанном в документе, по которому создается возврат.
+ **cashSum**  - Оплачено наличными. Поле является необходимым для возврата без основания
+ **noCashSum** - Оплачено картой. Поле является необходимым для возврата без основания

При создании возврата:

+ Контрагент в возврате и в документе, по которому он создается, должны совпадать
+ Валюта и юрлицо в возврате и в документе так же должны совпадать
+ При передаче коллекции **positions** в теле запроса на создание возврата, передаваемые позиции
должны соответствовать позициям в документе. Различие может быть только в количестве товара в позиции
(меньшее либо равное количеству в документе). Нельзя передать позиции, которых нет в документе.

> Пример создания новой Розничного возврата с телом запроса, содержащим только необходимые поля.

```shell
  curl -X POST
    "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "name": "123142vzvrt",
            "organization": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/107430bc-36e7-11e7-8a7f-40d000000090",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
                "type": "organization",
                "mediaType": "application/json"
              }
            },
            "store": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/1076a96a-36e7-11e7-8a7f-40d000000092",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
                "type": "store",
                "mediaType": "application/json"
              }
            },
            "retailStore": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailstore/10a79ac5-36e7-11e7-8a7f-40d00000009f",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailstore/metadata",
                "type": "retailstore",
                "mediaType": "application/json"
              }
            },
            "demand": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/retaildemand/700f8635-36f7-11e7-8a7f-40d00000011e",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retaildemand/metadata",
                "type": "retaildemand",
                "mediaType": "application/json"
              }
            },
            "retailShift": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailshift/6fe7b0da-36f7-11e7-8a7f-40d00000011c",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailshift/metadata",
                "type": "retailshift",
                "mediaType": "application/json"
              }
            }
          }'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление созданного Розничного возврата.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/80a2ea3b-3713-11e7-8a7f-40d000000003",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/metadata",
    "type": "retailsalesreturn",
    "mediaType": "application/json"
  },
  "id": "80a2ea3b-3713-11e7-8a7f-40d000000003",
  "accountId": "103bff1b-36e7-11e7-8a7f-40d000000004",
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
  "updated": "2017-05-12 16:04:15",
  "name": "123142vzvrt",
  "externalCode": "1-hpzSjAjCxS2dj55ZFeG2",
  "moment": "2017-05-12 16:04:00",
  "applicable": true,
  "rate": {
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/10772c12-36e7-11e7-8a7f-40d000000097",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json"
      }
    }
  },
  "sum": 0,
  "store": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/1076a96a-36e7-11e7-8a7f-40d000000092",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
      "type": "store",
      "mediaType": "application/json"
    }
  },
  "agent": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/109e931d-36e7-11e7-8a7f-40d00000009d",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
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
  "created": "2016-08-25 19:55:00",
  "printed": true,
  "published": true,
  "positions": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/80a2ea3b-3713-11e7-8a7f-40d000000003/positions",
      "type": "salesreturnposition",
      "mediaType": "application/json",
      "size": 0,
      "limit": 1000,
      "offset": 0
    }
  },
  "vatEnabled": true,
  "vatIncluded": true,
  "vatSum": 0,
  "demand": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/retaildemand/700f8635-36f7-11e7-8a7f-40d00000011e",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retaildemand/metadata",
      "type": "retaildemand",
      "mediaType": "application/json"
    }
  },
  "retailStore": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailstore/10a79ac5-36e7-11e7-8a7f-40d00000009f",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailstore/metadata",
      "type": "retailstore",
      "mediaType": "application/json"
    }
  },
  "retailShift": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailshift/6fe7b0da-36f7-11e7-8a7f-40d00000011c",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailshift/metadata",
      "type": "retailshift",
      "mediaType": "application/json"
    }
  },
  "cashSum": 0,
  "noCashSum": 0,
  "qrSum": 0
}
```

> Пример создания нового Розничного возврата с более насыщенным телом запроса.

```shell
  curl -X POST
    "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "name": "123142vzvrt",
            "description": "Розничный возврат по просьбе покупателя",
            "code": "303",
            "externalCode": "2250005aas-cszsz",
            "moment": "2016-05-06 14:47:47",
            "vatEnabled": true,
            "vatIncluded": true,
            "rate": {
              "currency": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/ee37a4b0-137a-11e6-9464-e4de000000e4",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
                  "type": "currency",
                  "mediaType": "application/json"
                }
              },
              "value": 71
            },
            "organization": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/30f01af0-137a-11e6-9464-e4de0000004e",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
                "type": "organization",
                "mediaType": "application/json"
              }
            },
            "store": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/30fe30a0-137a-11e6-9464-e4de00000050",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
                "type": "store",
                "mediaType": "application/json"
              }
            },
            "retailStore": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailstore/31b6349e-137a-11e6-9464-e4de0000005d",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailstore/metadata",
                "type": "retailstore",
                "mediaType": "application/json"
              }
            },
            "demand": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/retaildemand/5fa6624c-1380-11e6-9464-e4de00000205",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retaildemand/metadata",
                "type": "retaildemand",
                "mediaType": "application/json"
              }
            },
            "retailShift": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailshift/5f67a979-1380-11e6-9464-e4de00000203",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailshift/metadata",
                "type": "retailshift",
                "mediaType": "application/json"
              }
            },
            "attributes": [
              {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/metadata/attributes/0cd74e1e-2e59-11e6-8a84-bae50000008a",
                  "type": "attributemetadata",
                  "mediaType": "application/json"
                },
                "value": false
              },
              {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/metadata/attributes/0cd74e1e-2e59-11e6-8a84-bae50000008a",
                  "type": "attributemetadata",
                  "mediaType": "application/json"
                },
                "value": "3325-4214-42145-4211"
              }
            ]
          }'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление созданного Розничного возврата.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/5d6c0d07-1381-11e6-9464-e4de00000000",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/metadata",
    "type": "retailsalesreturn",
    "mediaType": "application/json"
  },
  "id": "5d6c0d07-1381-11e6-9464-e4de00000000",
  "accountId": "305f25aa-137a-11e6-9464-e4de00000001",
  "updated": "2016-05-06 14:55:01",
  "name": "123142vzvrt",
  "description": "Розничный возврат по просьбе покупателя",
  "code": "303",
  "externalCode": "2250005aas-cszsz",
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
  "moment": "2016-05-06 14:47:47",
  "applicable": true,
  "vatEnabled": true,
  "vatIncluded": true,
  "rate": {
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/ee37a4b0-137a-11e6-9464-e4de000000e4",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json"
      }
    },
    "value": 71
  },
  "sum": 0,
  "organization": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/30f01af0-137a-11e6-9464-e4de0000004e",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
      "type": "organization",
      "mediaType": "application/json"
    }
  },
  "store": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/30fe30a0-137a-11e6-9464-e4de00000050",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
      "type": "store",
      "mediaType": "application/json"
    }
  },
  "agent": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/31ace095-137a-11e6-9464-e4de0000005b",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
      "mediaType": "application/json"
    }
  },
  "attributes": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/metadata/attributes/0cd74e1e-2e59-11e6-8a84-bae50000008a",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "c72ff31e-1380-11e6-9464-e4de00000231",
      "name": "AttributeName1",
      "type": "string",
      "value": "3325-4214-42145-4211"
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/metadata/attributes/0cd74e1e-2e59-11e6-8a84-bae50000008a",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "c72ffba9-1380-11e6-9464-e4de00000232",
      "name": "AttributeName1",
      "type": "boolean",
      "value": false
    }
  ],
  "created": "2016-08-25 19:55:00",
  "printed": true,
  "published": true,
  "positions": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/5d6c0d07-1381-11e6-9464-e4de00000000/positions",
      "type": "salesreturnposition",
      "mediaType": "application/json",
      "size": 0,
      "limit": 1000,
      "offset": 0
    }
  },
  "retailStore": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailstore/31b6349e-137a-11e6-9464-e4de0000005d",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailstore/metadata",
      "type": "retailstore",
      "mediaType": "application/json"
    }
  },
  "demand": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/retaildemand/5fa6624c-1380-11e6-9464-e4de00000205",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retaildemand/metadata",
      "type": "retaildemand",
      "mediaType": "application/json"
    }
  },
  "retailShift": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailshift/5f67a979-1380-11e6-9464-e4de00000203",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailshift/metadata",
      "type": "retailshift",
      "mediaType": "application/json"
    }
  },
  "cashSum": 0,
  "noCashSum": 0,
  "qrSum": 0
}
```

> Пример запроса на создание Розничного возврата с позициями в теле запроса.

```shell
  curl -X POST
    "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "name": "123142vzvrt",
            "description": "Розничный возврат по просьбе покупателя",
            "code": "303",
            "externalCode": "2250005aas-cszsz",
            "moment": "2016-05-06 14:47:47",
            "vatEnabled": true,
            "vatIncluded": true,
            "rate": {
              "currency": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/ee37a4b0-137a-11e6-9464-e4de000000e4",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
                  "type": "currency",
                  "mediaType": "application/json"
                }
              },
              "value": 71
            },
            "organization": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/30f01af0-137a-11e6-9464-e4de0000004e",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
                "type": "organization",
                "mediaType": "application/json"
              }
            },
            "store": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/30fe30a0-137a-11e6-9464-e4de00000050",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
                "type": "store",
                "mediaType": "application/json"
              }
            },
            "retailStore": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailstore/31b6349e-137a-11e6-9464-e4de0000005d",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailstore/metadata",
                "type": "retailstore",
                "mediaType": "application/json"
              }
            },
            "demand": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/retaildemand/5fa6624c-1380-11e6-9464-e4de00000205",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retaildemand/metadata",
                "type": "retaildemand",
                "mediaType": "application/json"
              }
            },
            "retailShift": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailshift/5f67a979-1380-11e6-9464-e4de00000203",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailshift/metadata",
                "type": "retailshift",
                "mediaType": "application/json"
              }
            },
            "attributes": [
              {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/metadata/attributes/0cd74e1e-2e59-11e6-8a84-bae50000008a",
                  "type": "attributemetadata",
                  "mediaType": "application/json"
                },
                "value": false
              },
              {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/metadata/attributes/0cd74e1e-2e59-11e6-8a84-bae50000008a",
                  "type": "attributemetadata",
                  "mediaType": "application/json"
                },
                "value": "3325-4214-42145-4211"
              }
            ],
            "positions": [
              {
                "quantity": 5,
                "price": 30000,
                "discount": 0,
                "vat": 20,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/variant/0805a582-137b-11e6-9464-e4de0000010c",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/variant/metadata",
                    "type": "variant",
                    "mediaType": "application/json"
                  }
                }
              },
              {
                "quantity": 7,
                "price": 30000,
                "discount": 0,
                "vat": 20,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/variant/07fe4cad-137b-11e6-9464-e4de000000fd",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/variant/metadata",
                    "type": "variant",
                    "mediaType": "application/json"
                  }
                }
              }
            ]
          }'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление созданного Розничного возврата.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/c1ab79f5-1381-11e6-9464-e4de00000005",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/metadata",
    "type": "retailsalesreturn",
    "mediaType": "application/json"
  },
  "id": "c1ab79f5-1381-11e6-9464-e4de00000005",
  "accountId": "305f25aa-137a-11e6-9464-e4de00000001",
  "updated": "2016-05-06 14:57:50",
  "name": "123142vzvrt",
  "description": "Розничный возврат по просьбе покупателя",
  "code": "303",
  "externalCode": "2250005aas-cszsz",
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
  "moment": "2016-05-06 14:47:47",
  "applicable": true,
  "vatEnabled": true,
  "vatIncluded": true,
  "rate": {
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/ee37a4b0-137a-11e6-9464-e4de000000e4",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json"
      }
    },
    "value": 71
  },
  "sum": 360000,
  "organization": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/30f01af0-137a-11e6-9464-e4de0000004e",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
      "type": "organization",
      "mediaType": "application/json"
    }
  },
  "store": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/30fe30a0-137a-11e6-9464-e4de00000050",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
      "type": "store",
      "mediaType": "application/json"
    }
  },
  "agent": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/31ace095-137a-11e6-9464-e4de0000005b",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
      "mediaType": "application/json"
    }
  },
  "attributes": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/metadata/attributes/0cd74e1e-2e59-11e6-8a84-bae50000008a",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "c72ff31e-1380-11e6-9464-e4de00000231",
      "name": "AttributeName1",
      "type": "string",
      "value": "3325-4214-42145-4211"
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/metadata/attributes/0cd74e1e-2e59-11e6-8a84-bae50000008a",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "c72ffba9-1380-11e6-9464-e4de00000232",
      "name": "AttributeName2",
      "type": "boolean",
      "value": false
    }
  ],
  "created": "2016-08-25 19:55:00",
  "printed": true,
  "published": true,
  "positions": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/c1ab79f5-1381-11e6-9464-e4de00000005/positions",
      "type": "salesreturnposition",
      "mediaType": "application/json",
      "size": 2,
      "limit": 1000,
      "offset": 0
    }
  },
  "retailStore": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailstore/31b6349e-137a-11e6-9464-e4de0000005d",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailstore/metadata",
      "type": "retailstore",
      "mediaType": "application/json"
    }
  },
  "demand": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/retaildemand/5fa6624c-1380-11e6-9464-e4de00000205",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retaildemand/metadata",
      "type": "retaildemand",
      "mediaType": "application/json"
    }
  },
  "retailShift": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailshift/5f67a979-1380-11e6-9464-e4de00000203",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailshift/metadata",
      "type": "retailshift",
      "mediaType": "application/json"
    }
  },
  "cashSum": 360000,
  "noCashSum": 0,
  "qrSum": 0
}
```

> Пример запроса на создание Розничного возврата без основания.

```shell
  curl -X POST
    "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "name": "123142vzvrt",
            "description": "Розничный возврат по просьбе покупателя",
            "code": "303",
            "externalCode": "2250005aas-cszsz",
            "moment": "2016-05-06 14:47:47",
            "vatEnabled": true,
            "vatIncluded": true,
            "rate": {
              "currency": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/ee37a4b0-137a-11e6-9464-e4de000000e4",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
                  "type": "currency",
                  "mediaType": "application/json"
                }
              },
              "value": 71
            },
            "organization": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/30f01af0-137a-11e6-9464-e4de0000004e",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
                "type": "organization",
                "mediaType": "application/json"
              }
            },
            "store": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/30fe30a0-137a-11e6-9464-e4de00000050",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
                "type": "store",
                "mediaType": "application/json"
              }
            },
            "retailStore": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailstore/31b6349e-137a-11e6-9464-e4de0000005d",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailstore/metadata",
                "type": "retailstore",
                "mediaType": "application/json"
              }
            },
            "retailShift": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailshift/5f67a979-1380-11e6-9464-e4de00000203",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailshift/metadata",
                "type": "retailshift",
                "mediaType": "application/json"
              }
            },
            "attributes": [
              {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/metadata/attributes/0cd74e1e-2e59-11e6-8a84-bae50000008a",
                  "type": "attributemetadata",
                  "mediaType": "application/json"
                },
                "value": false
              },
              {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/metadata/attributes/0cd74e1e-2e59-11e6-8a84-bae50000008a",
                  "type": "attributemetadata",
                  "mediaType": "application/json"
                },
                "value": "3325-4214-42145-4211"
              }
            ],
            "positions": [
              {
                "quantity": 5,
                "price": 30000,
                "discount": 0,
                "vat": 20,
                "cost": 2500,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/variant/0805a582-137b-11e6-9464-e4de0000010c",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/variant/metadata",
                    "type": "variant",
                    "mediaType": "application/json"
                  }
                }
              },
              {
                "quantity": 7,
                "price": 30000,
                "discount": 0,
                "vat": 20,
                "cost": 3000,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/variant/07fe4cad-137b-11e6-9464-e4de000000fd",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/variant/metadata",
                    "type": "variant",
                    "mediaType": "application/json"
                  }
                }
              }
            ],
            "cashSum": 300000,
            "noCashSum": 60000
          }'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление созданного Розничного возврата.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/c1ab79f5-1381-11e6-9464-e4de00000005",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/metadata",
    "type": "retailsalesreturn",
    "mediaType": "application/json"
  },
  "id": "c1ab79f5-1381-11e6-9464-e4de00000005",
  "accountId": "305f25aa-137a-11e6-9464-e4de00000001",
  "updated": "2016-05-06 14:57:50",
  "name": "123142vzvrt",
  "description": "Розничный возврат по просьбе покупателя",
  "code": "303",
  "externalCode": "2250005aas-cszsz",
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
  "moment": "2016-05-06 14:47:47",
  "applicable": true,
  "vatEnabled": true,
  "vatIncluded": true,
  "rate": {
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/ee37a4b0-137a-11e6-9464-e4de000000e4",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json"
      }
    },
    "value": 71
  },
  "sum": 360000,
  "organization": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/30f01af0-137a-11e6-9464-e4de0000004e",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
      "type": "organization",
      "mediaType": "application/json"
    }
  },
  "store": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/30fe30a0-137a-11e6-9464-e4de00000050",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
      "type": "store",
      "mediaType": "application/json"
    }
  },
  "agent": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/31ace095-137a-11e6-9464-e4de0000005b",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
      "mediaType": "application/json"
    }
  },
  "attributes": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/metadata/attributes/0cd74e1e-2e59-11e6-8a84-bae50000008a",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "c72ff31e-1380-11e6-9464-e4de00000231",
      "name": "AttributeName1",
      "type": "string",
      "value": "3325-4214-42145-4211"
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/metadata/attributes/0cd74e1e-2e59-11e6-8a84-bae50000008a",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "c72ffba9-1380-11e6-9464-e4de00000232",
      "name": "AttributeName2",
      "type": "boolean",
      "value": false
    }
  ],
  "created": "2016-08-25 19:55:00",
  "printed": true,
  "published": true,
  "positions": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/c1ab79f5-1381-11e6-9464-e4de00000005/positions",
      "type": "salesreturnposition",
      "mediaType": "application/json",
      "size": 2,
      "limit": 100,
      "offset": 0
    }
  },
  "retailStore": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailstore/31b6349e-137a-11e6-9464-e4de0000005d",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailstore/metadata",
      "type": "retailstore",
      "mediaType": "application/json"
    }
  },
  "retailShift": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailshift/5f67a979-1380-11e6-9464-e4de00000203",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailshift/metadata",
      "type": "retailshift",
      "mediaType": "application/json"
    }
  },
  "cashSum": 300000,
  "noCashSum": 60000,
  "qrSum": 0
}
```

### Массовое создание и обновление Розничных возвратов 
[Массовое создание и обновление](../#mojsklad-json-api-obschie-swedeniq-sozdanie-i-obnowlenie-neskol-kih-ob-ektow) Розничных возвратов.
В теле запроса нужно передать массив, содержащий JSON представления Розничных возвратов, которые вы хотите создать или обновить.
Обновляемые Розничные возвраты должны содержать идентификатор в виде метаданных.

> Пример создания и обновления нескольких Розничных возвратов

```shell
  curl -X POST
    "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '[
            {
              "name": "123142vzvrt",
              "organization": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/107430bc-36e7-11e7-8a7f-40d000000090",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
                  "type": "organization",
                  "mediaType": "application/json"
                }
              },
              "store": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/1076a96a-36e7-11e7-8a7f-40d000000092",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
                  "type": "store",
                  "mediaType": "application/json"
                }
              },
              "retailStore": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailstore/10a79ac5-36e7-11e7-8a7f-40d00000009f",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailstore/metadata",
                  "type": "retailstore",
                  "mediaType": "application/json"
                }
              },
              "demand": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/retaildemand/700f8635-36f7-11e7-8a7f-40d00000011e",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retaildemand/metadata",
                  "type": "retaildemand",
                  "mediaType": "application/json"
                }
              },
              "retailShift": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailshift/6fe7b0da-36f7-11e7-8a7f-40d00000011c",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailshift/metadata",
                  "type": "retailshift",
                  "mediaType": "application/json"
                }
              }
            },
            {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/c1ab79f5-1381-11e6-9464-e4de00000005",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/metadata",
                "type": "retailsalesreturn",
                "mediaType": "application/json"
              },
              "vatEnabled": false,
              "vatIncluded": false,
              "name": "newName",
              "code": "3033",
              "positions": [
                {
                  "quantity": 6,
                  "price": 30000,
                  "discount": 0,
                  "vat": 20,
                  "assortment": {
                    "meta": {
                      "href": "https://online.moysklad.ru/api/remap/1.2/entity/variant/07f8fb39-137b-11e6-9464-e4de000000f3",
                      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/variant/metadata",
                      "type": "variant",
                      "mediaType": "application/json"
                    }
                  },
                  "cost": 250
                },
                {
                  "quantity": 2,
                  "price": 20000,
                  "discount": 0,
                  "vat": 0,
                  "assortment": {
                    "meta": {
                      "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/27a803bd-137b-11e6-9464-e4de0000013a",
                      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                      "type": "product",
                      "mediaType": "application/json"
                    }
                  },
                  "cost": 370
                },
                {
                  "accountId": "305f25aa-137a-11e6-9464-e4de00000001",
                  "quantity": 4,
                  "price": 40000,
                  "discount": 0,
                  "vat": 0,
                  "assortment": {
                    "meta": {
                      "href": "https://online.moysklad.ru/api/remap/1.2/entity/variant/609e36c0-137b-11e6-9464-e4de00000179",
                      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/variant/metadata",
                      "type": "variant",
                      "mediaType": "application/json"
                    }
                  },
                  "cost": 490
                },
                {
                  "quantity": 4,
                  "price": 40000,
                  "discount": 0,
                  "vat": 0,
                  "assortment": {
                    "meta": {
                      "href": "https://online.moysklad.ru/api/remap/1.2/entity/variant/609c2418-137b-11e6-9464-e4de00000174",
                      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/variant/metadata",
                      "type": "variant",
                      "mediaType": "application/json"
                    }
                  },
                  "cost": 510
                }
              ]
            }
          ]'  
```

> Response 200 (application/json)
Успешный запрос. Результат - массив JSON представлений созданных и обновленных Розничных возвратов.

```json
[
  {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/80a2ea3b-3713-11e7-8a7f-40d000000003",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/metadata",
      "type": "retailsalesreturn",
      "mediaType": "application/json"
    },
    "id": "80a2ea3b-3713-11e7-8a7f-40d000000003",
    "accountId": "103bff1b-36e7-11e7-8a7f-40d000000004",
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
    "updated": "2017-05-12 16:04:15",
    "name": "123142vzvrt",
    "externalCode": "1-hpzSjAjCxS2dj55ZFeG2",
    "moment": "2017-05-12 16:04:00",
    "applicable": true,
    "rate": {
      "currency": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/10772c12-36e7-11e7-8a7f-40d000000097",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
          "type": "currency",
          "mediaType": "application/json"
        }
      }
    },
    "sum": 0,
    "store": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/1076a96a-36e7-11e7-8a7f-40d000000092",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
        "type": "store",
        "mediaType": "application/json"
      }
    },
    "agent": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/109e931d-36e7-11e7-8a7f-40d00000009d",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
        "type": "counterparty",
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
    "created": "2016-08-25 19:55:00",
    "printed": true,
    "published": true,
    "positions": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/80a2ea3b-3713-11e7-8a7f-40d000000003/positions",
        "type": "salesreturnposition",
        "mediaType": "application/json",
        "size": 0,
        "limit": 1000,
        "offset": 0
      }
    },
    "vatEnabled": true,
    "vatIncluded": true,
    "vatSum": 0,
    "demand": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/retaildemand/700f8635-36f7-11e7-8a7f-40d00000011e",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retaildemand/metadata",
        "type": "retaildemand",
        "mediaType": "application/json"
      }
    },
    "retailStore": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailstore/10a79ac5-36e7-11e7-8a7f-40d00000009f",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailstore/metadata",
        "type": "retailstore",
        "mediaType": "application/json"
      }
    },
    "retailShift": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailshift/6fe7b0da-36f7-11e7-8a7f-40d00000011c",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailshift/metadata",
        "type": "retailshift",
        "mediaType": "application/json"
      }
    },
    "cashSum": 0,
    "noCashSum": 0,
    "qrSum": 0
  },
  {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/c1ab79f5-1381-11e6-9464-e4de00000005",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/metadata",
      "type": "retailsalesreturn",
      "mediaType": "application/json"
    },
    "id": "c1ab79f5-1381-11e6-9464-e4de00000005",
    "accountId": "305f25aa-137a-11e6-9464-e4de00000001",
    "updated": "2016-05-06 15:02:27",
    "name": "newName",
    "description": "Розничный возврат по просьбе покупателя",
    "code": "3033",
    "externalCode": "2250005aas-cszsz",
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
    "moment": "2016-05-06 14:47:47",
    "applicable": true,
    "vatEnabled": false,
    "rate": {
      "currency": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/ee37a4b0-137a-11e6-9464-e4de000000e4",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
          "type": "currency",
          "mediaType": "application/json"
        }
      },
      "value": 71
    },
    "sum": 540000,
    "organization": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/30f01af0-137a-11e6-9464-e4de0000004e",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
        "type": "organization",
        "mediaType": "application/json"
      }
    },
    "store": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/30fe30a0-137a-11e6-9464-e4de00000050",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
        "type": "store",
        "mediaType": "application/json"
      }
    },
    "agent": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/31ace095-137a-11e6-9464-e4de0000005b",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
        "type": "counterparty",
        "mediaType": "application/json"
      }
    },
    "attributes": [
      {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/metadata/attributes/0cd74e1e-2e59-11e6-8a84-bae50000008a",
          "type": "attributemetadata",
          "mediaType": "application/json"
        },
        "id": "c72ff31e-1380-11e6-9464-e4de00000231",
        "name": "AttributeName1",
        "type": "string",
        "value": "3325-4214-42145-4211"
      },
      {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/metadata/attributes/0cd74e1e-2e59-11e6-8a84-bae50000008a",
          "type": "attributemetadata",
          "mediaType": "application/json"
        },
        "id": "c72ffba9-1380-11e6-9464-e4de00000232",
        "name": "AttributeName2",
        "type": "boolean",
        "value": false
      }
    ],
    "created": "2016-08-25 19:55:00",
    "printed": true,
    "published": true,
    "positions": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/c1ab79f5-1381-11e6-9464-e4de00000005/positions",
        "type": "salesreturnposition",
        "mediaType": "application/json",
        "size": 4,
        "limit": 1000,
        "offset": 0
      }
    },
    "retailStore": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailstore/31b6349e-137a-11e6-9464-e4de0000005d",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailstore/metadata",
        "type": "retailstore",
        "mediaType": "application/json"
      }
    },
    "demand": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/retaildemand/5fa6624c-1380-11e6-9464-e4de00000205",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retaildemand/metadata",
        "type": "retaildemand",
        "mediaType": "application/json"
      }
    },
    "retailShift": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailshift/5f67a979-1380-11e6-9464-e4de00000203",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailshift/metadata",
        "type": "retailshift",
        "mediaType": "application/json"
      }
    },
    "cashSum": 540000,
    "noCashSum": 0,
    "qrSum": 0
  }
]
```

### Удалить Розничный возврат

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Розничного возврата.|
 
> Запрос на удаление Розничного возврата с указанным id.

```shell
curl -X DELETE
  "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/7944ef04-f831-11e5-7a69-971500188b19"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешное удаление Розничного возврата.

### Метаданные Розничных возвратов 
#### Метаданные Розничных возвратов 
Запрос на получение метаданных Розничных возвратов. Результат - объект JSON, включающий в себя:

| Параметр                | Описание  |
| ------------------------------ |:---------------------------|
| **meta**         | Ссылка на метаданные Розничных возвратов|
| **attributes**   | Массив объектов доп. полей Розничных возвратов в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye)|
| **states**       | Массив статусов Розничных возвратов|
| **createShared** | создавать новые Розничные возвраты с меткой "Общий"|

Структура отдельного объекта, представляющего доп. поле подробно описана в разделе [Работа с дополнительными полями](../#mojsklad-json-api-obschie-swedeniq-rabota-s-dopolnitel-nymi-polqmi).

> Метаданные Розничных возвратов

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/metadata"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление доп. полей Розничных возвратов.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/metadata",
    "mediaType": "application/json"
  },
  "attributes": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/metadata/attributes/c72ff31e-1380-11e6-9464-e4de00000231",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "c72ff31e-1380-11e6-9464-e4de00000231",
      "name": "AttributeName1",
      "type": "string",
      "required": false
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/metadata/attributes/c72ffba9-1380-11e6-9464-e4de00000232",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "c72ffba9-1380-11e6-9464-e4de00000232",
      "name": "AttributeName2",
      "type": "boolean",
      "required": false
    }
  ],
  "states": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/metadata/states/fb56c504-2e58-11e6-8a84-bae500000069",
        "type": "state",
        "mediaType": "application/json"
      },
      "id": "fb56c504-2e58-11e6-8a84-bae500000069",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "name": "Новый",
      "color": 15106326,
      "stateType": "Regular",
      "entityType": "retailsalesreturn"
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/metadata/states/fb56cae3-2e58-11e6-8a84-bae50000006a",
        "type": "state",
        "mediaType": "application/json"
      },
      "id": "fb56cae3-2e58-11e6-8a84-bae50000006a",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "name": "Подтвержден",
      "color": 40931,
      "stateType": "Regular",
      "entityType": "retailsalesreturn"
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/metadata/states/fb56cf4f-2e58-11e6-8a84-bae50000006b",
        "type": "state",
        "mediaType": "application/json"
      },
      "id": "fb56cf4f-2e58-11e6-8a84-bae50000006b",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "name": "Собран",
      "color": 8767198,
      "stateType": "Regular",
      "entityType": "retailsalesreturn"
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/metadata/states/fb56d433-2e58-11e6-8a84-bae50000006c",
        "type": "state",
        "mediaType": "application/json"
      },
      "id": "fb56d433-2e58-11e6-8a84-bae50000006c",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "name": "Отгружен",
      "color": 10774205,
      "stateType": "Regular",
      "entityType": "retailsalesreturn"
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/metadata/states/fb56d92f-2e58-11e6-8a84-bae50000006d",
        "type": "state",
        "mediaType": "application/json"
      },
      "id": "fb56d92f-2e58-11e6-8a84-bae50000006d",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "name": "Доставлен",
      "color": 8825440,
      "stateType": "Successful",
      "entityType": "retailsalesreturn"
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/metadata/states/fb56de0a-2e58-11e6-8a84-bae50000006e",
        "type": "state",
        "mediaType": "application/json"
      },
      "id": "fb56de0a-2e58-11e6-8a84-bae50000006e",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "name": "Возврат",
      "color": 15280409,
      "stateType": "Unsuccessful",
      "entityType": "retailsalesreturn"
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/metadata/states/fb56e2b4-2e58-11e6-8a84-bae50000006f",
        "type": "state",
        "mediaType": "application/json"
      },
      "id": "fb56e2b4-2e58-11e6-8a84-bae50000006f",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "name": "Отменен",
      "color": 15280409,
      "stateType": "Unsuccessful",
      "entityType": "retailsalesreturn"
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
  "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/metadata/attributes/7944ef04-f831-11e5-7a69-971500188b19"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление отдельного доп. поля.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/metadata/attributes/9b0c8d28-558c-11e6-8a84-bae50000008a",
    "type": "attributemetadata",
    "mediaType": "application/json"
  },
  "id": "9b0c8d28-558c-11e6-8a84-bae50000008a",
  "name": "AttributeName1",
  "type": "time",
  "required": false
}
```

### Шаблон Розничного возврата 
#### Шаблон Розничного возврата на основе 
Запрос на получение предзаполненого стандартными значениями
шаблона розничного возврата на основе других документов.
Шаблон розничного возврата можно получить на основе:

+ Розничной смены
+ Розничной продажи

При запросе шаблона только с розничной сменой в результате получиться шаблон возврата без основания.
При запросе шаблона с указанием розничной продажи, розничная смена может быть заполнена из нее.

> Пример запроса на создание шаблона розничного возврата на основе смены.

```shell
  curl -X PUT
    "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/new"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "retailShift": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailshift/ed8de012-479b-11e8-7ae5-8ba2000000ce",
                "type": "retailshift",
                "mediaType": "application/json"
              }
            }
          }'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление предзаполненного розничного возврата.

```json
{
  "owner": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/e346e355-2780-11e8-0532-9eed0000002a",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
      "type": "employee",
      "mediaType": "application/json",
      "uuidHref": "https://online.moysklad.ru/app/#employee/edit?id=e346e355-2780-11e8-0532-9eed0000002a"
    }
  },
  "shared": true,
  "group": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/group/e29e01d3-2780-11e8-0532-9eed00000002",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/group/metadata",
      "type": "group",
      "mediaType": "application/json"
    }
  },
  "name": "",
  "moment": "2018-05-08 13:00:00",
  "applicable": true,
  "rate": {
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/e37f9321-2780-11e8-0532-9eed00000058",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json",
        "uuidHref": "https://online.moysklad.ru/app/#currency/edit?id=e37f9321-2780-11e8-0532-9eed00000058"
      }
    }
  },
  "sum": 0,
  "store": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/e37edd82-2780-11e8-0532-9eed00000053",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
      "type": "store",
      "mediaType": "application/json",
      "uuidHref": "https://online.moysklad.ru/app/#warehouse/edit?id=e37edd82-2780-11e8-0532-9eed00000053"
    }
  },
  "agent": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/030a5127-3663-11e8-56c0-000800000000",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
      "mediaType": "application/json",
      "uuidHref": "https://online.moysklad.ru/app/#company/edit?id=030a5127-3663-11e8-56c0-000800000000"
    }
  },
  "organization": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/e37a6d1c-2780-11e8-0532-9eed00000051",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
      "type": "organization",
      "mediaType": "application/json",
      "uuidHref": "https://online.moysklad.ru/app/#mycompany/edit?id=e37a6d1c-2780-11e8-0532-9eed00000051"
    }
  },
  "documents": {
    "rows": []
  },
  "positions": {
    "rows": []
  },
  "vatEnabled": true,
  "vatIncluded": true,
  "retailShift": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailshift/ed8de012-479b-11e8-7ae5-8ba2000000ce",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailshift/metadata",
      "type": "retailshift",
      "mediaType": "application/json",
      "uuidHref": "https://online.moysklad.ru/app/#retailshift/edit?id=ed8de012-479b-11e8-7ae5-8ba2000000ce"
    }
  },
  "cashSum": 0,
  "noCashSum": 0,
  "qrSum": 0
}
```

> Пример запроса на создание шаблона розничного возврата на основе розничной продажи.

```shell
  curl -X PUT
    "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/new"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "demand": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/retaildemand/e806748e-9639-41da-8f2e-5e197312eac2",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retaildemand/metadata",
                "type": "retaildemand",
                "mediaType": "application/json"
              }
            }
          }'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление предзаполненного розничного возврата.

```json
{
  "owner": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/e346e355-2780-11e8-0532-9eed0000002a",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
      "type": "employee",
      "mediaType": "application/json",
      "uuidHref": "https://online.moysklad.ru/app/#employee/edit?id=e346e355-2780-11e8-0532-9eed0000002a"
    }
  },
  "shared": true,
  "group": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/group/e29e01d3-2780-11e8-0532-9eed00000002",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/group/metadata",
      "type": "group",
      "mediaType": "application/json"
    }
  },
  "name": "",
  "moment": "2018-05-08 13:00:00",
  "applicable": true,
  "rate": {
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/e37f9321-2780-11e8-0532-9eed00000058",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json",
        "uuidHref": "https://online.moysklad.ru/app/#currency/edit?id=e37f9321-2780-11e8-0532-9eed00000058"
      }
    }
  },
  "sum": 0,
  "store": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/e37edd82-2780-11e8-0532-9eed00000053",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
      "type": "store",
      "mediaType": "application/json",
      "uuidHref": "https://online.moysklad.ru/app/#warehouse/edit?id=e37edd82-2780-11e8-0532-9eed00000053"
    }
  },
  "agent": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/030a5127-3663-11e8-56c0-000800000000",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
      "mediaType": "application/json",
      "uuidHref": "https://online.moysklad.ru/app/#company/edit?id=030a5127-3663-11e8-56c0-000800000000"
    }
  },
  "organization": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/e37a6d1c-2780-11e8-0532-9eed00000051",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
      "type": "organization",
      "mediaType": "application/json",
      "uuidHref": "https://online.moysklad.ru/app/#mycompany/edit?id=e37a6d1c-2780-11e8-0532-9eed00000051"
    }
  },
  "documents": {
    "rows": []
  },
  "positions": {
    "rows": [
      {
        "quantity": 1,
        "price": 16000,
        "discount": 10,
        "vat": 0,
        "vatEnabled": false,
        "assortment": {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/03216395-3663-11e8-56c0-000800000004",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
            "type": "product",
            "mediaType": "application/json",
            "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=3b1e1f15-2842-11e9-ac12-000c0000002f"
          }
        }
      }
    ]
  },
  "vatEnabled": true,
  "vatIncluded": true,
  "demand": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/retaildemand/e806748e-9639-41da-8f2e-5e197312eac2",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retaildemand/metadata",
      "type": "retaildemand",
      "mediaType": "application/json",
      "uuidHref": "https://online.moysklad.ru/app/#retaildemand/edit?id=e806748e-9639-41da-8f2e-5e197312eac2"
    }
  },
  "retailShift": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailshift/ed8de012-479b-11e8-7ae5-8ba2000000ce",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailshift/metadata",
      "type": "retailshift",
      "mediaType": "application/json",
      "uuidHref": "https://online.moysklad.ru/app/#retailshift/edit?id=ed8de012-479b-11e8-7ae5-8ba2000000ce"
    }
  },
  "cashSum": 0,
  "noCashSum": 0,
  "qrSum": 0
}
```

### Розничный возврат
   
### Получить Розничный возврат

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Розничного возврата.|
 
> Запрос на получение отдельного Розничного возврата с указанным id.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/7944ef04-f831-11e5-7a69-971500188b19"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление Розничного возврата с указанным id.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/a62e39af-0c75-11e6-9464-e4de00000030",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/metadata",
    "type": "retailsalesreturn",
    "mediaType": "application/json"
  },
  "id": "a62e39af-0c75-11e6-9464-e4de00000030",
  "accountId": "84e60e93-f504-11e5-8a84-bae500000008",
  "updated": "2016-04-27 15:43:31",
  "name": "00001",
  "externalCode": "33YOoIGVhdPXFBr8QNbD50",
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
  "syncId": "eefa141e-0c65-4993-8b16-934905d47dbd",
  "moment": "2016-04-27 15:43:00",
  "applicable": true,
  "vatEnabled": true,
  "vatIncluded": true,
  "sum": 14000,
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
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
      "type": "store",
      "mediaType": "application/json"
    }
  },
  "agent": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/8518d001-f504-11e5-8a84-bae50000016a",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
      "mediaType": "application/json"
    }
  },
  "positions": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/a62e39af-0c75-11e6-9464-e4de00000030/positions",
      "type": "salesreturnposition",
      "mediaType": "application/json",
      "size": 3,
      "limit": 1000,
      "offset": 0
    }
  },
  "retailStore": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailstore/851f8576-f504-11e5-8a84-bae50000016c",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailstore/metadata",
      "type": "retailstore",
      "mediaType": "application/json"
    }
  },
  "demand": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/retaildemand/2ef43ba7-0c5a-11e6-9464-e4de0000000c",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retaildemand/metadata",
      "type": "retaildemand",
      "mediaType": "application/json"
    }
  },
  "retailShift": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailshift/9e46db1e-0c75-11e6-9464-e4de0000002b",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailshift/metadata",
      "type": "retailshift",
      "mediaType": "application/json"
    }
  },
  "cashSum": 14000,
  "noCashSum": 0,
  "qrSum": 0
}
```

### Изменить Розничный возврат 
Запрос на обновление Розничного возврата с указанным id.
В теле запроса можно указать только те поля, которые необходимо изменить у Розничного возврата, кроме тех, что
помечены `Только для чтения` в описании [атрибутов Розничного возврата](../documents/#dokumenty-roznichnyj-wozwrat).
При обновлении поля **organization** нужно также обновить поле **organizationAccount** иначе произойдет ошибка.

Контрагент должен совпадать с контрагентом, указанным в документе, по которому создается возврат.

При обновлении возврата:

+ Нельзя изменять следующие поля: **agentAccount**, **agent**, **demand**
+ Нельзя выставить валюту отличную от валюты в документе
+ Нельзя добавить позиции, отсутствующие среди позиций документа.

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Розничного возврата.|

> Пример запроса на обновление Розничного возврата.

```shell
  curl -X PUT
    "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/7944ef04-f831-11e5-7a69-971500188b19"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "vatEnabled": false,
            "vatIncluded": false,
            "name": "newName",
            "code": "3033",
            "positions": [
              {
                "quantity": 6,
                "price": 30000,
                "discount": 0,
                "vat": 20,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/variant/07f8fb39-137b-11e6-9464-e4de000000f3",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/variant/metadata",
                    "type": "variant",
                    "mediaType": "application/json"
                  }
                },
                "cost": 250
              },
              {
                "quantity": 2,
                "price": 20000,
                "discount": 0,
                "vat": 0,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/27a803bd-137b-11e6-9464-e4de0000013a",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                    "type": "product",
                    "mediaType": "application/json"
                  }
                },
                "cost": 370
              },
              {
                "accountId": "305f25aa-137a-11e6-9464-e4de00000001",
                "quantity": 4,
                "price": 40000,
                "discount": 0,
                "vat": 0,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/variant/609e36c0-137b-11e6-9464-e4de00000179",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/variant/metadata",
                    "type": "variant",
                    "mediaType": "application/json"
                  }
                },
                "cost": 490
              },
              {
                "quantity": 4,
                "price": 40000,
                "discount": 0,
                "vat": 0,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/variant/609c2418-137b-11e6-9464-e4de00000174",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/variant/metadata",
                    "type": "variant",
                    "mediaType": "application/json"
                  }
                },
                "cost": 510
              }
            ]
          }'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление обновленного Розничного возврата.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/c1ab79f5-1381-11e6-9464-e4de00000005",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/metadata",
    "type": "retailsalesreturn",
    "mediaType": "application/json"
  },
  "id": "c1ab79f5-1381-11e6-9464-e4de00000005",
  "accountId": "305f25aa-137a-11e6-9464-e4de00000001",
  "updated": "2016-05-06 15:02:27",
  "name": "newName",
  "description": "Розничный возврат по просьбе покупателя",
  "code": "3033",
  "externalCode": "2250005aas-cszsz",
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
  "moment": "2016-05-06 14:47:47",
  "applicable": true,
  "vatEnabled": false,
  "rate": {
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/ee37a4b0-137a-11e6-9464-e4de000000e4",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json"
      }
    },
    "value": 71
  },
  "sum": 540000,
  "organization": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/30f01af0-137a-11e6-9464-e4de0000004e",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
      "type": "organization",
      "mediaType": "application/json"
    }
  },
  "store": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/30fe30a0-137a-11e6-9464-e4de00000050",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
      "type": "store",
      "mediaType": "application/json"
    }
  },
  "agent": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/31ace095-137a-11e6-9464-e4de0000005b",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
      "mediaType": "application/json"
    }
  },
  "attributes": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/metadata/attributes/0cd74e1e-2e59-11e6-8a84-bae50000008a",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "c72ff31e-1380-11e6-9464-e4de00000231",
      "name": "AttributeName1",
      "type": "string",
      "value": "3325-4214-42145-4211"
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/metadata/attributes/0cd74e1e-2e59-11e6-8a84-bae50000008a",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "c72ffba9-1380-11e6-9464-e4de00000232",
      "name": "AttributeName2",
      "type": "boolean",
      "value": false
    }
  ],
  "created": "2016-08-25 19:55:00",
  "printed": true,
  "published": true,
  "positions": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/c1ab79f5-1381-11e6-9464-e4de00000005/positions",
      "type": "salesreturnposition",
      "mediaType": "application/json",
      "size": 4,
      "limit": 1000,
      "offset": 0
    }
  },
  "retailStore": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailstore/31b6349e-137a-11e6-9464-e4de0000005d",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailstore/metadata",
      "type": "retailstore",
      "mediaType": "application/json"
    }
  },
  "demand": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/retaildemand/5fa6624c-1380-11e6-9464-e4de00000205",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retaildemand/metadata",
      "type": "retaildemand",
      "mediaType": "application/json"
    }
  },
  "retailShift": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailshift/5f67a979-1380-11e6-9464-e4de00000203",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailshift/metadata",
      "type": "retailshift",
      "mediaType": "application/json"
    }
  },
  "cashSum": 540000,
  "noCashSum": 0,
  "qrSum": 0
}

```
 
### Позиции Розничного возврата 
Отдельный ресурс для управления позициями Розничного возврата. С его помощью вы можете управлять позициями большого документа, количество строк в котором превышает лимит на количество строк, сохраняемых вместе с документом. Этот лимит равен 1000. Более подробно о лимитах на количество строк документа и работе с большими документами можно прочитать [тут](../#mojsklad-json-api-obschie-swedeniq-rabota-s-poziciqmi-dokumentow).

### Получить позиции 
Запрос на получение списка всех позиций данной Розничного возврата.

| Название  | Тип | Описание                    |
| --------- |:----|:----------------------------|
**meta** |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные о выдаче,
**context** | [Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye) | Метаданные о сотруднике, выполнившем запрос.
**rows** |Array(Object)|Массив JSON объектов, представляющих собой позиции Розничного возврата.

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Розничного возврата.|
|**limit** |  `number` (optional) **Default: 1000** *Example: 1000* Максимальное количество сущностей для извлечения.`Допустимые значения 1 - 1000`.|
|**offset** |  `number` (optional) **Default: 0** *Example: 40* Отступ в выдаваемом списке сущностей.|

> Получить позиции 

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/7944ef04-f831-11e5-7a69-971500188b19/positions"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление списка позиций Розничного возврата.

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
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/7944ef04-f831-11e5-7a69-971500188b19/positions",
    "type": "salesreturnposition",
    "mediaType": "application/json",
    "size": 4,
    "limit": 1000,
    "offset": 0
  },
  "rows": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/7944ef04-f831-11e5-7a69-971500188b19/positions/6702da17-1382-11e6-9464-e4de0000000e",
        "type": "salesreturnposition",
        "mediaType": "application/json"
      },
      "id": "6702da17-1382-11e6-9464-e4de0000000e",
      "accountId": "305f25aa-137a-11e6-9464-e4de00000001",
      "quantity": 6,
      "price": 30000,
      "discount": 0,
      "vat": 0,
      "vatEnabled": false,
      "assortment": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/variant/07f8fb39-137b-11e6-9464-e4de000000f3",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/variant/metadata",
          "type": "variant",
          "mediaType": "application/json",
          "uuidHref": "https://online.moysklad.ru/app/#feature/edit?id=e64d0a86-2a99-11e9-ac12-000c00000041"
        }
      },
      "cost": 25
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/7944ef04-f831-11e5-7a69-971500188b19/positions/6702ecc7-1382-11e6-9464-e4de0000000f",
        "type": "salesreturnposition",
        "mediaType": "application/json"
      },
      "id": "6702ecc7-1382-11e6-9464-e4de0000000f",
      "accountId": "305f25aa-137a-11e6-9464-e4de00000001",
      "quantity": 2,
      "price": 20000,
      "discount": 0,
      "vat": 0,
      "vatEnabled": false,
      "assortment": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/27a803bd-137b-11e6-9464-e4de0000013a",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
          "type": "product",
          "mediaType": "application/json",
          "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=3b1e1f15-2842-11e9-ac12-000c0000002f"
        }
      },
      "cost": 37
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/7944ef04-f831-11e5-7a69-971500188b19/positions/6703f8ae-1382-11e6-9464-e4de00000010",
        "type": "salesreturnposition",
        "mediaType": "application/json"
      },
      "id": "6703f8ae-1382-11e6-9464-e4de00000010",
      "accountId": "305f25aa-137a-11e6-9464-e4de00000001",
      "quantity": 4,
      "price": 40000,
      "discount": 0,
      "vat": 0,
      "vatEnabled": false,
      "assortment": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/variant/609e36c0-137b-11e6-9464-e4de00000179",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/variant/metadata",
          "type": "variant",
          "mediaType": "application/json",
          "uuidHref": "https://online.moysklad.ru/app/#feature/edit?id=392c045c-2842-11e9-ac12-000a00000002"
        }
      },
      "cost": 49
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/7944ef04-f831-11e5-7a69-971500188b19/positions/67040794-1382-11e6-9464-e4de00000011",
        "type": "salesreturnposition",
        "mediaType": "application/json"
      },
      "id": "67040794-1382-11e6-9464-e4de00000011",
      "accountId": "305f25aa-137a-11e6-9464-e4de00000001",
      "quantity": 4,
      "price": 40000,
      "discount": 0,
      "vat": 0,
      "vatEnabled": false,
      "assortment": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/variant/609c2418-137b-11e6-9464-e4de00000174",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/variant/metadata",
          "type": "variant",
          "mediaType": "application/json",
          "uuidHref": "https://online.moysklad.ru/app/#feature/edit?id=3bb1af6c-2842-11e9-ac12-000c00000061"
        }
      },
      "cost": 51
    }
  ]
}
```

### Создать позицию 
Запрос на создание новой позиции в Розничном возврате.
Для успешного создания необходимо в теле запроса указать следующие поля:

+ **assortment** - Ссылка на товар/услугу/серию/модификацию, которую представляет собой позиция.
Также можно указать поле с именем **service**, **consignment**, **variant** в соответствии с тем,
чем является указанная позиция. Подробнее об этом поле можно прочитать в описании [позиции Розничного возврата](../documents/#dokumenty-roznichnyj-wozwrat-roznichnye-wozwraty-pozicii-roznichnogo-wozwrata).
+ **quantity** - Количество указанной позиции. Должно быть положительным, иначе возникнет ошибка.
Одновременно можно создать как одну так и несколько позиций Розничного возврата. Все созданные данным запросом позиции
будут добавлены к уже существующим.
Нельзя создавать позиции, отличные от позиций в документе, по которому создается возврат. Допустимо только
отличие в **quantity** позиций (количество в позиции в возврате м.б. меньше или равно количеству в позиции в документе).

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Розничного возврата.|

> Пример запроса на создание позиций в Розничном возврате.

```shell
  curl -X POST
    "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/7944ef04-f831-11e5-7a69-971500188b19/positions"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '[
            {
              "quantity": 103,
              "price": 999,
              "discount": 0,
              "vat": 0,
              "assortment": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/variant/609e36c0-137b-11e6-9464-e4de00000179",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/variant/metadata",
                  "type": "variant",
                  "mediaType": "application/json"
                }
              },
              "cost": 25
            },
            {
              "quantity": 21,
              "price": 100,
              "discount": 0,
              "vat": 21,
              "assortment": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/variant/07f8fb39-137b-11e6-9464-e4de000000f3",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/variant/metadata",
                  "type": "variant",
                  "mediaType": "application/json"
                }
              },
              "cost": 37
            },
            {
              "quantity": 3,
              "price": 35300,
              "discount": 0,
              "vat": 7,
              "assortment": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/variant/609e36c0-137b-11e6-9464-e4de00000179",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/variant/metadata",
                  "type": "variant",
                  "mediaType": "application/json"
                }
              },
              "cost": 49
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
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/7944ef04-f831-11e5-7a69-971500188b19/positions/13982b01-138a-11e6-9464-e4de00000018",
      "type": "salesreturnposition",
      "mediaType": "application/json"
    },
    "id": "13982b01-138a-11e6-9464-e4de00000018",
    "accountId": "305f25aa-137a-11e6-9464-e4de00000001",
    "quantity": 103,
    "price": 999,
    "discount": 0,
    "vat": 0,
    "vatEnabled": false,
    "variant": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/variant/609e36c0-137b-11e6-9464-e4de00000179",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/variant/metadata",
        "type": "variant",
        "mediaType": "application/json",
        "uuidHref": "https://online.moysklad.ru/app/#feature/edit?id=609e36c0-137b-11e6-9464-e4de00000179"
      }
    },
    "cost": 25
  },
  {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/7944ef04-f831-11e5-7a69-971500188b19/positions/13998a65-138a-11e6-9464-e4de00000019",
      "type": "salesreturnposition",
      "mediaType": "application/json"
    },
    "id": "13998a65-138a-11e6-9464-e4de00000019",
    "accountId": "305f25aa-137a-11e6-9464-e4de00000001",
    "quantity": 21,
    "price": 100,
    "discount": 0,
    "vat": 0,
    "vatEnabled": false,
    "variant": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/variant/07f8fb39-137b-11e6-9464-e4de000000f3",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/variant/metadata",
        "type": "variant",
        "mediaType": "application/json",
        "uuidHref": "https://online.moysklad.ru/app/#feature/edit?id=07f8fb39-137b-11e6-9464-e4de000000f3"
      }
    },
    "cost": 37
  },
  {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/7944ef04-f831-11e5-7a69-971500188b19/positions/13999856-138a-11e6-9464-e4de0000001a",
      "type": "salesreturnposition",
      "mediaType": "application/json"
    },
    "id": "13999856-138a-11e6-9464-e4de0000001a",
    "accountId": "305f25aa-137a-11e6-9464-e4de00000001",
    "quantity": 3,
    "price": 35300,
    "discount": 0,
    "vat": 0,
    "vatEnabled": false,
    "variant": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/variant/609e36c0-137b-11e6-9464-e4de00000179",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/variant/metadata",
        "type": "variant",
        "mediaType": "application/json",
        "uuidHref": "https://online.moysklad.ru/app/#feature/edit?id=609e36c0-137b-11e6-9464-e4de00000179"
      }
    },
    "cost": 49
  }
]
```

### Позиция Розничного возврата
   
### Получить позицию

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Розничного возврата.|
|**positionID** |  `string` (required) *Example: 34f6344f-015e-11e6-9464-e4de0000006c* id позиции Розничного возврата.|
 
> Запрос на получение отдельной позиции Розничного возврата с указанным id.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/7944ef04-f831-11e5-7a69-971500188b19/positions/34f6344f-015e-11e6-9464-e4de0000006c"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление отдельной позиции Розничного возврата.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/7944ef04-f831-11e5-7a69-971500188b19/positions/34f6344f-015e-11e6-9464-e4de0000006c",
    "type": "salesreturnposition",
    "mediaType": "application/json"
  },
  "id": "34f6344f-015e-11e6-9464-e4de0000006c",
  "accountId": "305f25aa-137a-11e6-9464-e4de00000001",
  "quantity": 103,
  "price": 999,
  "discount": 0,
  "vat": 0,
  "vatEnabled": false,
  "assortment": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/variant/609e36c0-137b-11e6-9464-e4de00000179",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/variant/metadata",
      "type": "variant",
      "mediaType": "application/json",
      "uuidHref": "https://online.moysklad.ru/app/#feature/edit?id=3bb1af6c-2842-11e9-ac12-000c00000061"
    }
  },
  "cost": 25
}
```
        
### Изменить позицию 
Запрос на обновление отдельной позиции Розничного возврата.
При обновлении отдельной позиции в возврате можно только изменить количество данной позиции.
Причем это количество должно быть в пределах , где n - кол-во данной позиции в документе, по которому создан возврат.

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Розничного возврата.|
|**positionID** |  `string` (required) *Example: 34f6344f-015e-11e6-9464-e4de0000006c* id позиции Розничного возврата.|

> Пример запроса на обновление отдельной позиции в Розничном возврате.

```shell
  curl -X PUT
    "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/7944ef04-f831-11e5-7a69-971500188b19/positions/34f6344f-015e-11e6-9464-e4de0000006c"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "quantity": 10,
            "price": 3000,
            "discount": 15,
            "vat": 10,
            "cost": 250
          }'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление обновленной позиции Розничного возврата.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/7944ef04-f831-11e5-7a69-971500188b19/positions/34f6344f-015e-11e6-9464-e4de0000006c",
    "type": "salesreturnposition",
    "mediaType": "application/json"
  },
  "id": "34f6344f-015e-11e6-9464-e4de0000006c",
  "accountId": "305f25aa-137a-11e6-9464-e4de00000001",
  "quantity": 10,
  "price": 3000,
  "discount": 15,
  "vat": 0,
  "assortment": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/variant/609e36c0-137b-11e6-9464-e4de00000179",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/variant/metadata",
      "type": "variant",
      "mediaType": "application/json",
      "uuidHref": "https://online.moysklad.ru/app/#feature/edit?id=3bb1af6c-2842-11e9-ac12-000c00000061"
    }
  },
  "cost": 250
}

```

### Удалить позицию

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Розничного возврата.|
|**positionID** |  `string` (required) *Example: 34f6344f-015e-11e6-9464-e4de0000006c* id позиции Розничного возврата.|
 
> Запрос на удаление отдельной позиции Розничного возврата с указанным id.

```shell
curl -X DELETE
  "https://online.moysklad.ru/api/remap/1.2/entity/retailsalesreturn/7944ef04-f831-11e5-7a69-971500188b19/positions/34f6344f-015e-11e6-9464-e4de0000006c"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешное удаление позиции Розничного возврата.
