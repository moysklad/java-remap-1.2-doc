## Внутренний заказ
Средствами JSON API можно создавать и обновлять сведения о Внутренних заказах, запрашивать списки Внутренних заказов и сведения по отдельным Внутренним заказам. Позициями Внутренних заказов можно управлять как в составе отдельного заказа, так и с помощью специальных ресурсов для управления позициями. Кодом сущности для Внутреннего заказа в составе JSON API является ключевое слово **internalorder**.

### Внутренние заказы 
#### Атрибуты сущности

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные Внутреннего заказа|Только для чтения|да
|**id**                 |UUID|ID Внутреннего заказа|Только для чтения|да
|**accountId**          |UUID| ID учетной записи|Только для чтения|да
|**syncId**             |UUID|ID синхронизации. После заполнения недоступен для изменения|Только для чтения|нет
|**updated**            |DateTime|Момент последнего обновления Внутреннего заказа|Только для чтения|да
|**deleted**            |DateTime|Момент последнего удаления Внутреннего заказа|Только для чтения|да
|**name**               |String(255)|Наименование Внутреннего заказа|Необходимое при создании|да
|**description**        |String(4096)|Комментарий Внутреннего заказа|&mdash;|нет
|**externalCode**       |String(255)|Внешний код Внутреннего заказа|Только для чтения| да
|**moment**             |DateTime|Дата смены|Только для чтения|да
|**applicable**         |Boolean|Отметка о проведении|&mdash;|да
|**vatEnabled**         |Boolean|Учитывается ли НДС|&mdash;|да
|**vatIncluded**        |Boolean| Включен ли НДС в цену|&mdash;|нет
|**project**            |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные проекта|&mdash;|нет
|**sum**                |Int|Сумма Внутреннего заказа в копейках|Только для чтения|да
|**rate**               |Object|Валюта. [Подробнее тут](../documents/#dokumenty-obschie-swedeniq-valuta-w-dokumentah)|&mdash;|да
|**owner**              |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Владелец (Сотрудник)|&mdash;|да
|**shared**             |Boolean|Общий доступ|Только для чтения|да
|**group**              |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Отдел сотрудника|&mdash;|да
|**organization**       |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные юрлица|Необходимое при создании|да
|**store**              |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные склада|&mdash;|да
|**state**              |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные статуса Внутреннего заказа|&mdash;|нет
|**attributes**         |Array(Object)|Коллекция метаданных доп. полей. [Поля объекта](../#mojsklad-json-api-obschie-swedeniq-rabota-s-dopolnitel-nymi-polqmi) |Только для чтения|нет
|**files**              |MetaArray|Массив метаданных [Файлов](../dictionaries/#suschnosti-fajly) (Максимальное количество файлов - 100)|&mdash;|да
|**created**            |DateTime|Дата создания|Только для чтения|да
|**printed**            |Boolean|Напечатан ли документ|Только для чтения|да
|**published**          |Boolean|Опубликован ли документ|Только для чтения|да
|**vatSum**                |Float|Сумма включая НДС|Только для чтения|да
|**positions**        |MetaArray|Метаданные позиций Внутреннего заказа|Только для чтения|да
|**deliveryPlannedMoment**            |DateTime|Планируемая дата приемки|&mdash;|нет
|**purchaseOrders**         |Array(Object)| Коллекция метаданных на связанные заказы поставщику|&mdash;|да
|**moves**          |Array(Object)|Коллекция метаданных на связанные заказы перемещения|&mdash;|да

#### Позиции Внутреннего заказа
Позиции Внутреннего заказа - это список товаров/услуг/модификаций/серий.
Объект позиции Внутреннего заказа содержит следующие поля:

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**id**                 |UUID|ID позиции|Только для чтения|да
|**accountId**          |UUID| ID учетной записи|Только для чтения|да
|**quantity**          |Int|Количество товаров/услуг данного вида в позиции. Если позиция - товар, у которого включен учет по серийным номерам, то значение в этом поле всегда будет равно количеству серийных номеров для данной позиции в документе.|&mdash;|да
|**price**          |Float|Цена товара/услуги в копейках|&mdash;|да
|**vat**        |Int|НДС, которым облагается текущая позиция|&mdash;|да
|**vatEnabled**     |Boolean|Включен ли НДС для позиции. С помощью этого флага для позиции можно выставлять НДС = 0 или НДС = "без НДС". (vat = 0, vatEnabled = false) -> vat = "без НДС", (vat = 0, vatEnabled = true) -> vat = 0%.|&mdash;|да
|**assortment**              |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные товара/услуги/серии/модификации, которую представляет собой позиция|&mdash;|да
|**pack**            |String(255)|Упаковка товара|&mdash;|нет

С позициями можно работать с помощью [специальных ресурсов для управления позициями Внутреннего заказа](../documents/#dokumenty-vnutrennij-zakaz-pozicii-wnutrennego-zakaza),
а также в составе отдельного Внутреннего заказа. При работе в составе отдельного Внутреннего заказа,
вы можете отправлять запросы на создание отдельного Внутреннего заказа с включенным в тело запроса
массивом позиций Внутреннего заказа. Если количество позиций превышает максимально допустимое, то для
дальнейшего пополнения позиций нужно будет работать со специальным ресурсом "Позиции Внутреннего заказа".
Также, при работе в составе отдельного Внутреннего заказа, можно отправлять запросы на обновление списка позиций
с включенным в тело запроса массивом позиций Внутреннего заказа. При этом важно помнить, что коллекция позиций будет
восприниматься как "все позиции Внутреннего заказа" и полностью заменит уже существующую коллекцию при обновлении объекта - лишние
позиции будут удалены, новые добавлены, существующие - изменены.

О работе с доп. полями Внутренних заказов можно прочитать [здесь](../#mojsklad-json-api-obschie-swedeniq-rabota-s-dopolnitel-nymi-polqmi)


### Получить Внутренние заказы 

**Параметры**

| Параметр                | Описание  |
| ------------------------------ |:---------------------------|
|**limit** |  `number` (optional) **Default: 1000** *Example: 1000* Максимальное количество сущностей для извлечения.`Допустимые значения 1 - 1000`.|
|**offset** |  `number` (optional) **Default: 0** *Example: 40* Отступ в выдаваемом списке сущностей.|
|**search** |  `string` (optional) *Example: 0001* Фильтр документов по указанной поисковой строке.

> Получить Внутренние заказы

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/internalorder"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление списка Внутренних заказов.

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
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/metadata",
    "type": "internalorder",
    "mediaType": "application/json",
    "size": 2,
    "limit": 1000,
    "offset": 0
  },
  "rows": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/31d58bde-b2fd-11e6-8a84-bae500000068",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/metadata",
        "type": "internalorder",
        "mediaType": "application/json"
      },
      "id": "31d58bde-b2fd-11e6-8a84-bae500000068",
      "accountId": "b8b74698-9128-11e6-8a84-bae500000001",
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
      "updated": "2016-11-25 13:52:01",
      "name": "00002",
      "description": "Комментарий",
      "externalCode": "00KNqzWbjDRhZ1A0411hS2",
      "moment": "2016-11-25 13:50:00",
      "applicable": true,
      "printed": true,
      "published": true,
      "rate": {
        "currency": {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/b942e6f2-9128-11e6-8a84-bae500000058",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
            "type": "currency",
            "mediaType": "application/json"
          }
        },
        "value": 1
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
      "state": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/metadata/states/f804ff3d-b2fc-11e6-8a84-bae500000065",
          "type": "state",
          "mediaType": "application/json"
        }
      },
      "positions": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/31d58bde-b2fd-11e6-8a84-bae500000068/positions",
          "type": "internalorderposition",
          "mediaType": "application/json",
          "size": 2,
          "limit": 1000,
          "offset": 0
        }
      },
      "vatEnabled": true,
      "vatIncluded": true,
      "vatSum": 0,
      "deliveryPlannedMoment": "2016-11-30 13:50:00"
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/64e426af-b0d8-11e6-8a84-bae500000064",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/metadata",
        "type": "internalorder",
        "mediaType": "application/json"
      },
      "id": "64e426af-b0d8-11e6-8a84-bae500000064",
      "accountId": "b8b74698-9128-11e6-8a84-bae500000001",
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
      "updated": "2016-11-22 21:04:24",
      "name": "00001",
      "externalCode": "80QQopc4h8yBc0LnmTPpT3",
      "moment": "2016-11-22 20:23:00",
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
      "positions": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/64e426af-b0d8-11e6-8a84-bae500000064/positions",
          "type": "internalorderposition",
          "mediaType": "application/json",
          "size": 5,
          "limit": 1000,
          "offset": 0
        }
      },
      "vatEnabled": true,
      "vatIncluded": true,
      "vatSum": 0,
      "moves": [
        {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/move/a3b68a79-b0dc-11e6-8a84-bae5000000cd",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/move/metadata",
            "type": "move",
            "mediaType": "application/json"
          }
        }
      ]
    }
  ]
}
```

### Создать Внутренний заказ 
Запрос на создание нового Внутреннего заказа.
Обязательные для создания поля:

+ **name** - номер Внутреннего заказа
+ **organization** - Ссылка на ваше юрлицо в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye)

> Пример создания нового Внутреннего заказа.

```shell
  curl -X POST
    "https://online.moysklad.ru/api/remap/1.2/entity/internalorder"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
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
            "name": "000222",
            "description": "Мой Комментарий",
            "externalCode": "00KNqzWbjDRhZ1A0411ss1231hS2",
            "moment": "2016-11-25 13:52:00",
            "applicable": true,
            "rate": {
              "currency": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/b942e6f2-9128-11e6-8a84-bae500000058",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
                  "type": "currency",
                  "mediaType": "application/json"
                }
              },
              "value": 1
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
            "state": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/metadata/states/f804ff3d-b2fc-11e6-8a84-bae500000065",
                "type": "state",
                "mediaType": "application/json"
              }
            },
            "positions": [
              {
                "quantity": 1,
                "price": 0,
                "discount": 0,
                "vat": 0,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/variant/fc635ded-acf7-11e6-8a84-bae500000075",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/variant/metadata",
                    "type": "variant",
                    "mediaType": "application/json"
                  }
                }
              },
              {
                "quantity": 1,
                "price": 0,
                "discount": 0,
                "vat": 0,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/f4ac4460-acf7-11e6-8a84-bae500000068",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                    "type": "product",
                    "mediaType": "application/json"
                  }
                }
              }
            ],
            "vatEnabled": true,
            "vatIncluded": true,
            "vatSum": 0,
            "deliveryPlannedMoment": "2016-11-30 13:50:00"
          }'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление созданного Внутреннего заказа.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/eb75f6b8-b2ff-11e6-8a84-bae500000000",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/metadata",
    "type": "internalorder",
    "mediaType": "application/json"
  },
  "id": "eb75f6b8-b2ff-11e6-8a84-bae500000000",
  "accountId": "b8b74698-9128-11e6-8a84-bae500000001",
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
  "updated": "2016-11-25 14:11:31",
  "name": "000222",
  "description": "Мой Комментарий",
  "externalCode": "00KNqzWbjDRhZ1A0411ss1231hS2",
  "moment": "2016-11-25 13:52:00",
  "applicable": true,
  "rate": {
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/b942e6f2-9128-11e6-8a84-bae500000058",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json"
      }
    },
    "value": 63.45
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
  "state": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/metadata/states/f804ff3d-b2fc-11e6-8a84-bae500000065",
      "type": "state",
      "mediaType": "application/json"
    }
  },
  "created": "2007-02-07 17:16:41",
  "printed": true,
  "published": true,
  "positions": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/eb75f6b8-b2ff-11e6-8a84-bae500000000/positions",
      "type": "internalorderposition",
      "mediaType": "application/json",
      "size": 2,
      "limit": 1000,
      "offset": 0
    }
  },
  "vatEnabled": true,
  "vatIncluded": true,
  "vatSum": 0,
  "deliveryPlannedMoment": "2016-11-30 13:50:00"
}
```

### Шаблон Внутреннего заказа 

### Шаблон Внутреннего заказа 
Запрос на получение шаблона Внутреннего заказа.

> Пример создания нового Внутреннего заказа.

```shell
  curl -X PUT
    "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/new"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d ''  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление предзаполненного шаблона Внутреннего заказа.

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
  "moment": "2016-11-25 14:59:18",
  "applicable": true,
  "printed": true,
  "published": true,
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
  "organization": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/b9324d71-9128-11e6-8a84-bae500000051",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
      "type": "organization",
      "mediaType": "application/json"
    }
  },
  "state": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/metadata/states/f804ff3d-b2fc-11e6-8a84-bae500000065",
      "type": "state",
      "mediaType": "application/json"
    }
  },
  "positions": {
    "rows": []
  },
  "vatEnabled": true,
  "vatIncluded": true
}

```

### Массовое создание и обновление Внутренних заказов 
[Массовое создание и обновление](../#mojsklad-json-api-obschie-swedeniq-sozdanie-i-obnowlenie-neskol-kih-ob-ektow) Внутренних заказов.
В теле запроса нужно передать массив, содержащий JSON представления Внутренних заказов, которые вы хотите создать или обновить.
Обновляемые Внутренние заказы должны содержать идентификатор в виде метаданных.

> Пример создания и обновления нескольких Внутренних заказов

```shell
  curl -X POST
    "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/new"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '[
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
              "name": "000222",
              "description": "Мой Комментарий",
              "externalCode": "00KNqzWbjDRhZ1A0411ss1231hS2",
              "moment": "2016-11-25 13:52:00",
              "applicable": true,
              "rate": {
                "currency": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/b942e6f2-9128-11e6-8a84-bae500000058",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
                    "type": "currency",
                    "mediaType": "application/json"
                  }
                },
                "value": 1
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
              "state": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/metadata/states/f804ff3d-b2fc-11e6-8a84-bae500000065",
                  "type": "state",
                  "mediaType": "application/json"
                }
              },
              "positions": [
                {
                  "quantity": 1,
                  "price": 0,
                  "discount": 0,
                  "vat": 0,
                  "assortment": {
                    "meta": {
                      "href": "https://online.moysklad.ru/api/remap/1.2/entity/variant/fc635ded-acf7-11e6-8a84-bae500000075",
                      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/variant/metadata",
                      "type": "variant",
                      "mediaType": "application/json"
                    }
                  }
                },
                {
                  "quantity": 1,
                  "price": 0,
                  "discount": 0,
                  "vat": 0,
                  "assortment": {
                    "meta": {
                      "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/f4ac4460-acf7-11e6-8a84-bae500000068",
                      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                      "type": "product",
                      "mediaType": "application/json"
                    }
                  }
                }
              ],
              "vatEnabled": true,
              "vatIncluded": true,
              "vatSum": 0,
              "deliveryPlannedMoment": "2016-11-30 13:50:00"
            },
            {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/64e426af-b0d8-11e6-8a84-bae500000064",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/metadata",
                "type": "internalorder",
                "mediaType": "application/json"
              },
              "owner": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/b905bfb0-9128-11e6-8a84-bae50000002a",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
                  "type": "employee",
                  "mediaType": "application/json"
                }
              },
              "shared": true,
              "group": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/group/b8ba0d3f-9128-11e6-8a84-bae500000002",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/group/metadata",
                  "type": "group",
                  "mediaType": "application/json"
                }
              },
              "name": "700222",
              "description": "Мой обновленный Комментарий",
              "externalCode": "00KNqzWbjDRhZ1A0411ss1231hS2",
              "moment": "2016-11-25 13:52:00",
              "applicable": true,
              "rate": {
                "currency": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/b942e6f2-9128-11e6-8a84-bae500000058",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
                    "type": "currency",
                    "mediaType": "application/json"
                  }
                },
                "value": 1
              },
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
              "state": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/metadata/states/f804ff3d-b2fc-11e6-8a84-bae500000065",
                  "type": "state",
                  "mediaType": "application/json"
                }
              },
              "positions": [
                {
                  "quantity": 1,
                  "price": 2230,
                  "discount": 0,
                  "vat": 0,
                  "assortment": {
                    "meta": {
                      "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/f4ac4460-acf7-11e6-8a84-bae500000068",
                      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                      "type": "product",
                      "mediaType": "application/json"
                    }
                  }
                }
              ],
              "vatEnabled": true,
              "vatIncluded": true,
              "vatSum": 0,
              "deliveryPlannedMoment": "2016-12-30 13:52:00"
            }
          ]'  
```

> Response 200 (application/json)
Успешный запрос. Результат - массив JSON представлений созданных и обновленных Внутренних заказов.

```json
[
  {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/eb75f6b8-b2ff-11e6-8a84-bae500000000",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/metadata",
      "type": "internalorder",
      "mediaType": "application/json"
    },
    "id": "eb75f6b8-b2ff-11e6-8a84-bae500000000",
    "accountId": "b8b74698-9128-11e6-8a84-bae500000001",
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
    "updated": "2016-11-25 14:11:31",
    "name": "000222",
    "description": "Мой Комментарий",
    "externalCode": "00KNqzWbjDRhZ1A0411ss1231hS2",
    "moment": "2016-11-25 13:52:00",
    "applicable": true,
    "rate": {
      "currency": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/b942e6f2-9128-11e6-8a84-bae500000058",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
          "type": "currency",
          "mediaType": "application/json"
        }
      },
      "value": 63.45
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
    "state": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/metadata/states/f804ff3d-b2fc-11e6-8a84-bae500000065",
        "type": "state",
        "mediaType": "application/json"
      }
    },
    "created": "2007-02-07 17:16:41",
    "printed": true,
    "published": true,
    "positions": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/eb75f6b8-b2ff-11e6-8a84-bae500000000/positions",
        "type": "internalorderposition",
        "mediaType": "application/json",
        "size": 2,
        "limit": 1000,
        "offset": 0
      }
    },
    "vatEnabled": true,
    "vatIncluded": true,
    "vatSum": 0,
    "deliveryPlannedMoment": "2016-11-30 13:50:00"
  },
  {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/64e426af-b0d8-11e6-8a84-bae500000064",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/metadata",
      "type": "internalorder",
      "mediaType": "application/json"
    },
    "id": "64e426af-b0d8-11e6-8a84-bae500000064",
    "accountId": "b8b74698-9128-11e6-8a84-bae500000001",
    "owner": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/b905bfb0-9128-11e6-8a84-bae50000002a",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
        "type": "employee",
        "mediaType": "application/json"
      }
    },
    "shared": true,
    "group": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/group/b8ba0d3f-9128-11e6-8a84-bae500000002",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/group/metadata",
        "type": "group",
        "mediaType": "application/json"
      }
    },
    "updated": "2016-11-25 14:48:02",
    "name": "700222",
    "description": "Мой обновленный Комментарий",
    "externalCode": "00KNqzWbjDRhZ1A0411ss1231hS2",
    "moment": "2016-11-25 13:52:00",
    "applicable": true,
    "rate": {
      "currency": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/b942e6f2-9128-11e6-8a84-bae500000058",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
          "type": "currency",
          "mediaType": "application/json"
        }
      },
      "value": 63.45
    },
    "sum": 2230,
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
    "state": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/metadata/states/f804ff3d-b2fc-11e6-8a84-bae500000065",
        "type": "state",
        "mediaType": "application/json"
      }
    },
    "created": "2007-02-07 17:16:41",
    "printed": true,
    "published": true,
    "positions": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/64e426af-b0d8-11e6-8a84-bae500000064/positions",
        "type": "internalorderposition",
        "mediaType": "application/json",
        "size": 1,
        "limit": 1000,
        "offset": 0
      }
    },
    "vatEnabled": true,
    "vatIncluded": true,
    "vatSum": 0,
    "deliveryPlannedMoment": "2016-12-30 13:52:00",
    "moves": [
      {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/move/a3b68a79-b0dc-11e6-8a84-bae5000000cd",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/move/metadata",
          "type": "move",
          "mediaType": "application/json"
        }
      }
    ]
  }
]
```

### Удалить Внутренний заказ

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Внутреннего заказа.|
 
> Запрос на удаление Внутреннего заказа с указанным id.

```shell
curl -X DELETE
  "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/7944ef04-f831-11e5-7a69-971500188b1"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешное удаление Внутреннего заказа.

### Массовое удаление Внутренних заказов

В теле запроса нужно передать массив, содержащий JSON метаданных Внутренних заказов, которые вы хотите удалить.


> Запрос на массовое удаление Внутренних заказов. 

```shell
curl -X POST
  "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/delete"
  -H "Authorization: Basic <Credentials>"
  -H "Content-Type: application/json"
  -d '[
        {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/7944ef04-f831-11e5-7a69-971500188b1",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/metadata",
            "type": "internalorder",
            "mediaType": "application/json"
        },
        {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/7944ef04-f831-11e5-7a69-971500188b2",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/metadata",
            "type": "internalorder",
            "mediaType": "application/json"
        }
      ]'
```        

> Успешный запрос. Результат - JSON информация об удалении Внутренних заказов.

```json
[
  {
    "info":"Сущность 'internalorder' с UUID: 7944ef04-f831-11e5-7a69-971500188b1 успешно удалена"
  },
  {
    "info":"Сущность 'internalorder' с UUID: 7944ef04-f831-11e5-7a69-971500188b2 успешно удалена"
  }
]
``` 

### Метаданные Внутренних заказов 
#### Метаданные Внутренних заказов 
Запрос на получение метаданных Внутренних заказов. Результат - объект JSON, включающий в себя:

| Параметр                | Описание  |
| ------------------------------ |:---------------------------|
| **meta**         | Ссылка на метаданные Внутренних заказов|
| **attributes**   | Массив объектов доп. полей Внутренних заказов в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye)|
| **states**       | Массив статусов Внутренних заказов|
| **createShared** | создавать новые Внутренние заказы с меткой "Общий"|

Структура отдельного объекта, представляющего доп. поле подробно описана в разделе [Работа с дополнительными полями](../#mojsklad-json-api-obschie-swedeniq-rabota-s-dopolnitel-nymi-polqmi).

> Метаданные Внутренних заказов

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/metadata"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление метаданных Внутренних заказов.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/metadata",
    "mediaType": "application/json"
  },
  "attributes": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/metadata/attributes/68d142e7-b300-11e6-8a84-bae50000008b",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "68d142e7-b300-11e6-8a84-bae50000008b",
      "name": "Доп поле внут заказа",
      "type": "string",
      "required": false
    }
  ],
  "states": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/metadata/states/f804ff3d-b2fc-11e6-8a84-bae500000065",
        "type": "state",
        "mediaType": "application/json"
      },
      "id": "f804ff3d-b2fc-11e6-8a84-bae500000065",
      "accountId": "b8b74698-9128-11e6-8a84-bae500000001",
      "name": "OMG",
      "color": 10066329,
      "stateType": "Regular",
      "entityType": "internalorder"
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
  "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/metadata/attributes/7944ef04-f831-11e5-7a69-971500188b19"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление отдельного доп. поля.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/metadata/attributes/68d142e7-b300-11e6-8a84-bae50000008b",
    "type": "attributemetadata",
    "mediaType": "application/json"
  },
  "id": "68d142e7-b300-11e6-8a84-bae50000008b",
  "name": "Доп поле внут заказа",
  "type": "string",
  "required": false
}
```

### Внутренний заказ 

### Получить Внутренний заказ

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Внутреннего заказа.|
 
> Запрос на получение отдельного Внутреннего заказа с указанным id.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/7944ef04-f831-11e5-7a69-971500188b19"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление Внутреннего заказа.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/31d58bde-b2fd-11e6-8a84-bae500000068",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/metadata",
    "type": "internalorder",
    "mediaType": "application/json"
  },
  "id": "31d58bde-b2fd-11e6-8a84-bae500000068",
  "accountId": "b8b74698-9128-11e6-8a84-bae500000001",
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
  "updated": "2016-11-25 13:52:01",
  "name": "00002",
  "description": "Комментарий",
  "externalCode": "00KNqzWbjDRhZ1A0411hS2",
  "moment": "2016-11-25 13:50:00",
  "applicable": true,
  "printed": true,
  "published": true,
  "rate": {
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/b942e6f2-9128-11e6-8a84-bae500000058",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json"
      }
    },
    "value": 1
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
  "state": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/metadata/states/f804ff3d-b2fc-11e6-8a84-bae500000065",
      "type": "state",
      "mediaType": "application/json"
    }
  },
  "positions": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/31d58bde-b2fd-11e6-8a84-bae500000068/positions",
      "type": "internalorderposition",
      "mediaType": "application/json",
      "size": 2,
      "limit": 1000,
      "offset": 0
    }
  },
  "vatEnabled": true,
  "vatIncluded": true,
  "vatSum": 0,
  "deliveryPlannedMoment": "2016-11-30 13:50:00",
  "moves": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/move/3aa6f577-b2ff-11e6-8a84-bae500000070",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/move/metadata",
        "type": "move",
        "mediaType": "application/json"
      }
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/move/3fe38e12-b2ff-11e6-8a84-bae500000077",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/move/metadata",
        "type": "move",
        "mediaType": "application/json"
      }
    }
  ],
  "purchaseOrders": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/4a29b74e-b2ff-11e6-8a84-bae500000084",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata",
        "type": "purchaseorder",
        "mediaType": "application/json"
      }
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/45353c47-b2ff-11e6-8a84-bae50000007e",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/purchaseorder/metadata",
        "type": "purchaseorder",
        "mediaType": "application/json"
      }
    }
  ]
}
```

### Изменить Внутренний заказ 
Запрос на обновление Внутреннего заказа с указанным id.

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Внутреннего заказа.|

> Пример запроса на обновление отдельного Внутреннего заказа.

```shell
  curl -X PUT
    "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/7944ef04-f831-11e5-7a69-971500188b19"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "owner": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/b905bfb0-9128-11e6-8a84-bae50000002a",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
                "type": "employee",
                "mediaType": "application/json"
              }
            },
            "shared": true,
            "group": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/group/b8ba0d3f-9128-11e6-8a84-bae500000002",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/group/metadata",
                "type": "group",
                "mediaType": "application/json"
              }
            },
            "name": "700222",
            "description": "Мой обновленный Комментарий",
            "externalCode": "00KNqzWbjDRhZ1A0411ss1231hS2",
            "moment": "2016-11-25 13:52:00",
            "applicable": true,
            "rate": {
              "currency": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/b942e6f2-9128-11e6-8a84-bae500000058",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
                  "type": "currency",
                  "mediaType": "application/json"
                }
              },
              "value": 1
            },
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
            "state": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/metadata/states/f804ff3d-b2fc-11e6-8a84-bae500000065",
                "type": "state",
                "mediaType": "application/json"
              }
            },
            "positions": [
              {
                "quantity": 1,
                "price": 2230,
                "discount": 0,
                "vat": 0,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/f4ac4460-acf7-11e6-8a84-bae500000068",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                    "type": "product",
                    "mediaType": "application/json"
                  }
                }
              }
            ],
            "vatEnabled": true,
            "vatIncluded": true,
            "vatSum": 0,
            "deliveryPlannedMoment": "2016-12-30 13:52:00"
          }'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление обновленного Внутреннего заказа.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/64e426af-b0d8-11e6-8a84-bae500000064",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/metadata",
    "type": "internalorder",
    "mediaType": "application/json"
  },
  "id": "64e426af-b0d8-11e6-8a84-bae500000064",
  "accountId": "b8b74698-9128-11e6-8a84-bae500000001",
  "owner": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/b905bfb0-9128-11e6-8a84-bae50000002a",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
      "type": "employee",
      "mediaType": "application/json"
    }
  },
  "shared": true,
  "group": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/group/b8ba0d3f-9128-11e6-8a84-bae500000002",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/group/metadata",
      "type": "group",
      "mediaType": "application/json"
    }
  },
  "updated": "2016-11-25 14:48:02",
  "name": "700222",
  "description": "Мой обновленный Комментарий",
  "externalCode": "00KNqzWbjDRhZ1A0411ss1231hS2",
  "moment": "2016-11-25 13:52:00",
  "applicable": true,
  "rate": {
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/b942e6f2-9128-11e6-8a84-bae500000058",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json"
      }
    },
    "value": 63.45
  },
  "sum": 2230,
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
  "state": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/metadata/states/f804ff3d-b2fc-11e6-8a84-bae500000065",
      "type": "state",
      "mediaType": "application/json"
    }
  },
  "created": "2007-02-07 17:16:41",
  "printed": true,
  "published": true,
  "positions": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/64e426af-b0d8-11e6-8a84-bae500000064/positions",
      "type": "internalorderposition",
      "mediaType": "application/json",
      "size": 1,
      "limit": 1000,
      "offset": 0
    }
  },
  "vatEnabled": true,
  "vatIncluded": true,
  "vatSum": 0,
  "deliveryPlannedMoment": "2016-12-30 13:52:00",
  "moves": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/move/a3b68a79-b0dc-11e6-8a84-bae5000000cd",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/move/metadata",
        "type": "move",
        "mediaType": "application/json"
      }
    }
  ]
}
```

### Позиции Внутреннего заказа 
Отдельный ресурс для управления позициями Внутреннего заказа. С его помощью вы можете управлять позициями большого документа, количество строк в котором превышает 1000. Более подробно о лимитах на количество строк документа и работе с большими документами можно прочитать [тут](../#mojsklad-json-api-obschie-swedeniq-rabota-s-poziciqmi-dokumentow).

### Получить позиции Внутреннего заказа 
Запрос на получение списка всех позиций данного Внутреннего заказа.

| Название  | Тип | Описание                    |
| --------- |:----|:----------------------------|
**meta** |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные о выдаче,
**context** | [Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye) | Метаданные о сотруднике, выполнившем запрос.
**rows** |Array(Object)|Массив JSON объектов, представляющих собой позиции Внутреннего заказа.

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Внутреннего заказа.|
|**limit** |  `number` (optional) **Default: 1000** *Example: 1000* Максимальное количество сущностей для извлечения.`Допустимые значения 1 - 1000`.|
|**offset** |  `number` (optional) **Default: 0** *Example: 40* Отступ в выдаваемом списке сущностей.|
|**search** |  `string` (optional) *Example: 0001* Фильтр документов по указанной поисковой строке.

> Получить позиции Внутреннего заказа

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/7944ef04-f831-11e5-7a69-971500188b19/positions"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление списка позиций отдельного Внутреннего заказа.

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
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/7944ef04-f831-11e5-7a69-971500188b19/positions",
    "type": "internalorderposition",
    "mediaType": "application/json",
    "size": 1,
    "limit": 1000,
    "offset": 0
  },
  "rows": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/7944ef04-f831-11e5-7a69-971500188b19/positions/05379d42-b305-11e6-8a84-bae500000008",
        "type": "internalorderposition",
        "mediaType": "application/json"
      },
      "id": "05379d42-b305-11e6-8a84-bae500000008",
      "accountId": "b8b74698-9128-11e6-8a84-bae500000001",
      "quantity": 1,
      "price": 2230,
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
      }
    }
  ]
}
```

### Создать позиции Внутреннего заказа 
Запрос на создание новой позиции во Внутреннем заказе.
Для успешного создания необходимо в теле запроса указать следующие поля:

+ **assortment** - Ссылка на товар/услугу/серию/модификацию, которую представляет собой позиция.
Также можно указать поле с именем **service**, **consignment**, **variant** в соответствии с тем,
чем является указанная позиция. Подробнее об этом поле можно прочитать в описании [позиции Внутреннего заказа](../documents/#dokumenty-vnutrennij-zakaz-vnutrennie-zakazy-pozicii-wnutrennego-zakaza)
+ **quantity** - Количество указанной позиции. Должно быть положительным, иначе возникнет ошибка.
Одновременно можно создать как одну так и несколько позиций Внутреннего заказа. Все созданные данным запросом позиции
будут добавлены к уже существующим.

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Внутреннего заказа.|

> Пример создания позиций во Внутреннем заказе.

```shell
  curl -X POST
    "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/7944ef04-f831-11e5-7a69-971500188b19/positions"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '[
            {
              "quantity": 1,
              "price": 100,
              "vat": 10,
              "assortment": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/f4ac4460-acf7-11e6-8a84-bae500000068",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                  "type": "product",
                  "mediaType": "application/json"
                }
              }
            },
            {
              "quantity": 12,
              "price": 200,
              "vat": 18,
              "assortment": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/f4ac4460-acf7-11e6-8a84-bae500000068",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                  "type": "product",
                  "mediaType": "application/json"
                }
              }
            },
            {
              "quantity": 3,
              "price": 2230,
              "vat": 0,
              "assortment": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/f4ac4460-acf7-11e6-8a84-bae500000068",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                  "type": "product",
                  "mediaType": "application/json"
                }
              }
            }
          ]'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление созданной позиции отдельного Внутреннего заказа.

```json
[
  {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/7944ef04-f831-11e5-7a69-971500188b19/positions/705ff11b-b305-11e6-8a84-bae50000000c",
      "type": "internalorderposition",
      "mediaType": "application/json"
    },
    "id": "705ff11b-b305-11e6-8a84-bae50000000c",
    "accountId": "b8b74698-9128-11e6-8a84-bae500000001",
    "quantity": 1,
    "price": 100,
    "vat": 10,
    "vatEnabled": true,
    "assortment": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/f4ac4460-acf7-11e6-8a84-bae500000068",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
        "type": "product",
        "mediaType": "application/json",
        "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=3bb1af6c-2842-11e9-ac12-000c00000061"
      }
    }
  },
  {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/7944ef04-f831-11e5-7a69-971500188b19/positions/705ffca0-b305-11e6-8a84-bae50000000d",
      "type": "internalorderposition",
      "mediaType": "application/json"
    },
    "id": "705ffca0-b305-11e6-8a84-bae50000000d",
    "accountId": "b8b74698-9128-11e6-8a84-bae500000001",
    "quantity": 12,
    "price": 200,
    "vat": 18,
    "vatEnabled": true,
    "assortment": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/f4ac4460-acf7-11e6-8a84-bae500000068",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
        "type": "product",
        "mediaType": "application/json",
        "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=e64d0a86-2a99-11e9-ac12-000c00000041"
      }
    }
  },
  {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/7944ef04-f831-11e5-7a69-971500188b19/positions/706006cd-b305-11e6-8a84-bae50000000e",
      "type": "internalorderposition",
      "mediaType": "application/json"
    },
    "id": "706006cd-b305-11e6-8a84-bae50000000e",
    "accountId": "b8b74698-9128-11e6-8a84-bae500000001",
    "quantity": 3,
    "price": 2230,
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
    }
  }
]

```

### Удалить позицию Внутреннего заказа 

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**positionID** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id позиции Внутреннего заказа.|

> Запрос на удаление позиции Внутреннего заказа с указанным id.

```shell
curl -X DELETE
  "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/positions/7944ef04-f831-11e5-7a69-971500188b19"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешное удаление позиции Внутреннего заказа.

### Позиция Внутреннего заказа 

### Получить позицию 

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Внутреннего заказа.|
|**positionID** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b20* id позиции Внутреннего заказа.|

> Запрос на получение отдельной позиции Внутреннего заказа с указанным id.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/7944ef04-f831-11e5-7a69-971500188b19/positions/7944ef04-f831-11e5-7a69-971500188b20"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление отдельной позиции Внутреннего заказа.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/7944ef04-f831-11e5-7a69-971500188b19/positions/7944ef04-f831-11e5-7a69-971500188b20",
    "type": "internalorderposition",
    "mediaType": "application/json"
  },
  "id": "7944ef04-f831-11e5-7a69-971500188b20",
  "accountId": "b8b74698-9128-11e6-8a84-bae500000001",
  "quantity": 12,
  "price": 200,
  "vat": 18,
  "vatEnabled": true,
  "assortment": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/f4ac4460-acf7-11e6-8a84-bae500000068",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
      "type": "product",
      "mediaType": "application/json",
      "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=3b1e1f15-2842-11e9-ac12-000c0000002f"
    }
  }
}
```

### Изменить позицию 
Запрос на обновление отдельной позиции Внутреннего заказа.

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Внутреннего заказа.|
|**positionID** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b20* id позиции Внутреннего заказа.|

> Пример запроса на обновление отдельной позиции во Внутреннем заказе.

```shell
  curl -X PUT
    "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/7944ef04-f831-11e5-7a69-971500188b19/positions/7944ef04-f831-11e5-7a69-971500188b20"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "quantity": 2,
            "price": 500,
            "vat": 18,
            "assortment": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/f4ac4460-acf7-11e6-8a84-bae500000068",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                "type": "product",
                "mediaType": "application/json"
              }
            }
          }'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление обновленной позиции заказа.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/internalorder/7944ef04-f831-11e5-7a69-971500188b19/positions/7944ef04-f831-11e5-7a69-971500188b20",
    "type": "internalorderposition",
    "mediaType": "application/json"
  },
  "id": "7944ef04-f831-11e5-7a69-971500188b20",
  "accountId": "b8b74698-9128-11e6-8a84-bae500000001",
  "quantity": 2,
  "price": 500,
  "vat": 18,
  "vatEnabled": true,
  "assortment": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/f4ac4460-acf7-11e6-8a84-bae500000068",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
      "type": "product",
      "mediaType": "application/json",
      "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=3b1e1f15-2842-11e9-ac12-000c0000002f"
    }
  }
}
```
