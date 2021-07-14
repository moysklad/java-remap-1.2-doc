## Отчет Обороты
Средствами JSON API можно запросить отчет "Обороты" по всем товарам и модификациям. Для доступа к отчету через API требуется право на просмотр отчета *Обороты*.
О том, что представляет собой отчет "Обороты" вы можете прочитать по [этой ссылке](https://support.moysklad.ru/hc/ru/articles/203396063-%D0%9E%D0%B1%D0%BE%D1%80%D0%BE%D1%82%D1%8B).

### Обороты по товарам
Общий отчет по оборотам товаров и модификаций без детализации по складам. 

#### Атрибуты объекта отчета

| Название  | Тип | Описание                    | Обязательное при ответе|
| --------- |:----|:----------------------------|:------------------------|
|**assortment**        |Object|Краткое представление Товара или Модификации в отчете. [Подробнее тут](#otchety-otchet-oboroty-oboroty-po-towaram-struktura-ob-ekta-assortment)|да
|**onPeriodStart**     |Object|Показатели на начало периода. [Подробнее тут](#otchety-otchet-oboroty-oboroty-po-towaram-struktura-ob-ekta-pokazateli-onperiodstart-onperiodend-income-outcome)|да
|**onPeriodEnd**       |Object|Показатели на конец периода. [Подробнее тут](#otchety-otchet-oboroty-oboroty-po-towaram-struktura-ob-ekta-pokazateli-onperiodstart-onperiodend-income-outcome)|да
|**income**            |Object|Показатели прихода в течение периода отчета. [Подробнее тут](#otchety-otchet-oboroty-oboroty-po-towaram-struktura-ob-ekta-pokazateli-onperiodstart-onperiodend-income-outcome)|да
|**outcome**           |Object|Показатели расхода в течение периода отчета. [Подробнее тут](#otchety-otchet-oboroty-oboroty-po-towaram-struktura-ob-ekta-pokazateli-onperiodstart-onperiodend-income-outcome)|да

#### Структура объекта assortment

| Название  | Тип | Описание                    | Обязательное при ответе|
| --------- |:----|:----------------------------|:------------------------|
|**meta**           |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные Товара или Модификации|да
|**name**           |String(255)|Наименование Товара или Модификации|да
|**code**           |String(255)|Код Товара|нет
|**article**        |String(255)|Артикул Товара|нет
|**productFolder**  |Object|Группа Товара или Модификации|нет
|**uom**            |Object|Единица измерения|нет
|**image**          |Object|Первое изображение Товара или Модификации|нет

#### Структура объекта показатели (onPeriodStart, onPeriodEnd, income, outcome)

| Название  | Тип | Описание                    | Обязательное при ответе|
| --------- |:----|:----------------------------|:------------------------|
|**sum**        |Float|Сумма себестоимости|да
|**quantity**   |Float|Количество единиц товара|да

#### Атрибуты доступные для фильтрации

Результаты отчета можно отфильтровать, используя параметр filter. Для каждого параметра можно указать только одно значение. Нельзя указывать пустые значения. Поддерживается фильтрация только на равенство.

| Название               | Описание  |
| ------------------------------ |:---------------------------|
|**agent** | ссылка на контрагента, по которому нужно произвести фильтрацию.
|**product** | ссылка на товар, по которому нужно произвести фильтрацию. В выдаче будет товар вместе с его модификациями при `groupBy=variant`.
|**variant** | ссылка на модификацию, по которой нужно произвести фильтрацию.
|**organization** | ссылка на юрлицо, по которому нужно произвести фильтрацию.
|**project** | ссылка на проект, по которому нужно произвести фильтрацию.
|**contract** | ссылка на договор, по которому нужно произвести фильтрацию.
|**store** | ссылка на склад, по которому нужно произвести фильтрацию.
|**retailStore** | ссылка на точку продаж, по которой нужно произвести фильтрацию.
|**agentTag** | строка с названием группы контрагентов, по которой нужно произвести фильтрацию.
|**withoutturnover** | параметр для фильтрации "Показывать товары без движения". Возможные значения: true, false.
|**type** | строка с названием типа документа, по который нужно произвести фильтрацию. Возможные значения supply, purchasereturn, demand, salesreturn, loss, enter, move, processing, retaildemand, retailsalesreturn.


Примеры фильтрации:

- `filter=agent=https://online.moysklad.ru/api/remap/1.2/entity/counterparty/f8f729a5-a784-11e9-ac12-000800000000`
- `filter=product=https://online.moysklad.ru/api/remap/1.2/entity/product/f8f729a5-a784-11e9-ac12-000800000000`
- `filter=organization=https://online.moysklad.ru/api/remap/1.2/entity/organization/0347beb0-a785-11e9-ac12-000800000003`
- `filter=store=https://online.moysklad.ru/api/remap/1.2/entity/store/656c4032-8667-11e6-8a84-bae500003321`
- `filter=project=https://online.moysklad.ru/api/remap/1.2/entity/project/7a5f0ed5-8552-11e6-8a84-bae500000046`
- `filter=contract=https://online.moysklad.ru/api/remap/1.2/entity/contract/7a5f0ed5-8552-11e6-8a84-bae500085742`
- `filter=retailStore=https://online.moysklad.ru/api/remap/1.2/entity/retailstore/9ca74859-85c7-11e9-ac12-000d00000030`
- `filter=agentTag=favorites`
- `filter=withoutturnover=true`
- `filter=type=supply`

### Получить Обороты по товарам

Запрос на получение отчета Обороты по товарам.

**Параметры**

| Параметр                | Описание  |
| ------------------------------ |:---------------------------|
|**limit** |  `number` (optional) **Default: 1000** *Example: 1000* Максимальное количество сущностей для извлечения.`Допустимые значения 1 - 1000`.|
|**offset** |  `number` (optional) **Default: 0** *Example: 40* Отступ в выдаваемом списке сущностей.|
|**momentFrom** |  `date` (optional) *Example: 2018-09-01 00:00:00* Начало периода отчета|
|**momentTo** |  `date` (optional) *Example: 2018-10-01 00:00:00* Конец периода отчета|
|**groupBy**|  `string` (optional) тип, по которому нужно сгруппировать выдачу. По умолчанию параметр **groupBy** имеет значение `product`. Если вы хотите увидеть только объекты типа product, необходимо выставить соответствующее значение параметра. <ul><li>groupBy=product - только товары</li><li>groupBy=variant - товары и модификации</li></ul>|

**Заголовки**

| Заголовок                | Описание  |
| ------------------------------ |:---------------------------|
|**X-Lognex-Accept-Timezone** | Опциональный заголовок, в котором указана текущая дата на клиенте в RFC 3522. Таймзону обязательно указывать в формате знак и 4 символа (не в Obsolete Date and Time). Пример даты: `Wed, 16 Aug 2017 23:07:01 +0700`. При подсчете показателей даты операций смещаются в таймзону клиента.|
|**X-Lognex-Content-Timezone** | Заголовок ответа. В нем указывается (как думает сервер) текущая дата на клиенте в RFC 3522.|


> Запрос на получение отчета "Обороты по товарам".

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/report/turnover/all"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление отчета.

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
    "href": "https://online.moysklad.ru/api/remap/1.2/report/turnover/all",
    "type": "turnover",
    "mediaType": "application/json",
    "size": 3,
    "limit": 1000,
    "offset": 0
  },
  "rows": [
    {
      "assortment": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/66990dc7-bdfe-11eb-c0a8-800c00000016",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
          "type": "product",
          "mediaType": "application/json",
          "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=66989c14-bdfe-11eb-c0a8-800c00000014"
        },
        "name": "товар 2"
      },
      "onPeriodStart": {
        "quantity": 0.0,
        "sum": 0.0
      },
      "onPeriodEnd": {
        "quantity": 1.0,
        "sum": 0.0
      },
      "income": {
        "quantity": 3.0,
        "sum": 0.0
      },
      "outcome": {
        "quantity": 2.0,
        "sum": 0.0
      }
    },
    {
      "assortment": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/variant/3e32ef51-c1f1-11eb-c0a8-800c00000003",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/variant/metadata",
          "type": "variant",
          "mediaType": "application/json",
          "uuidHref": "https://online.moysklad.ru/app/#feature/edit?id=3e3278e5-c1f1-11eb-c0a8-800c00000001"
        },
        "name": "2 (char)"
      },
      "onPeriodStart": {
        "quantity": 0.0,
        "sum": 0.0
      },
      "onPeriodEnd": {
        "quantity": 2.0,
        "sum": 20000.0
      },
      "income": {
        "quantity": 3.0,
        "sum": 30000.0
      },
      "outcome": {
        "quantity": 1.0,
        "sum": 10000.0
      }
    },
    {
      "assortment": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/b008915c-b977-11eb-c0a8-800a00000008",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
          "type": "product",
          "mediaType": "application/json",
          "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=b0078621-b977-11eb-c0a8-800a00000006"
        },
        "name": "товар 1",
        "code": "00001",
        "article": "123",
        "uom": {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/uom/19f1edc0-fc42-4001-94cb-c9ec9c62ec10",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/uom/metadata",
            "type": "uom",
            "mediaType": "application/json"
          },
          "name": "шт"
        },
        "productFolder": {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/productfolder/e229bb59-c202-11eb-c0a8-800b00000002",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/productfolder/metadata",
            "type": "productfolder",
            "mediaType": "application/json",
            "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=e229bb59-c202-11eb-c0a8-800b00000002"
          },
          "name": "группа"
        }
      },
      "onPeriodStart": {
        "quantity": 0.0,
        "sum": 0.0
      },
      "onPeriodEnd": {
        "quantity": 2.0,
        "sum": 4400.0
      },
      "income": {
        "quantity": 3.0,
        "sum": 6600.0
      },
      "outcome": {
        "quantity": 1.0,
        "sum": 2200.0
      }
    }
  ]
}
```

### Обороты по товару с детализацией по складам
Отчет обороты по товару и его модификациям с детализацией по складам. 

#### Атрибуты объекта отчета

| Название  | Тип | Описание                    | Обязательное при ответе|
| --------- |:----|:----------------------------|:------------------------|
|**assortment**        |Object|Краткое представление Товара или Модификации в отчете. [Подробнее тут](#otchety-otchet-oboroty-oboroty-po-towaru-s-detalizaciej-po-skladam-struktura-ob-ekta-assortment)|да
|**stockByStore**      |Object|Детализация оборотов по складам. [Подробнее тут](#otchety-otchet-oboroty-oboroty-po-towaru-s-detalizaciej-po-skladam-struktura-ob-ekta-detalizaciq-oborotow-po-skladam)|да

#### Структура объекта assortment

| Название  | Тип | Описание                    | Обязательное при ответе|
| --------- |:----|:----------------------------|:------------------------|
|**meta**           |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные Товара или Модификации|да
|**name**           |String(255)|Наименование Товара или Модификации|да
|**code**           |String(255)|Код Товара|нет
|**article**        |String(255)|Артикул Товара|нет
|**productFolder**  |Object|Группа Товара или Модификации|нет
|**uom**            |Object|Единица измерения|нет
|**image**          |Object|Первое изображение Товара или Модификации|нет

#### Структура объекта детализация оборотов по складам

| Название  | Тип | Описание                    | Обязательное при ответе|
| --------- |:----|:----------------------------|:------------------------|
|**store**             |Object|Склад.|да
|**onPeriodStart**     |Object|Показатели на начало периода. [Подробнее тут](#otchety-otchet-oboroty-oboroty-po-towaru-s-detalizaciej-po-skladam-struktura-ob-ekta-pokazateli-onperiodstart-onperiodend-income-outcome)|да
|**onPeriodEnd**       |Object|Показатели на конец периода. [Подробнее тут](#otchety-otchet-oboroty-oboroty-po-towaru-s-detalizaciej-po-skladam-struktura-ob-ekta-pokazateli-onperiodstart-onperiodend-income-outcome)|да
|**income**            |Object|Показатели прихода в течение периода отчета. [Подробнее тут](#otchety-otchet-oboroty-oboroty-po-towaru-s-detalizaciej-po-skladam-struktura-ob-ekta-pokazateli-onperiodstart-onperiodend-income-outcome)|да
|**outcome**           |Object|Показатели расхода в течение периода отчета. [Подробнее тут](#otchety-otchet-oboroty-oboroty-po-towaru-s-detalizaciej-po-skladam-struktura-ob-ekta-pokazateli-onperiodstart-onperiodend-income-outcome)|да

#### Структура объекта показатели (onPeriodStart, onPeriodEnd, income, outcome)

| Название  | Тип | Описание                    | Обязательное при ответе|
| --------- |:----|:----------------------------|:------------------------|
|**sum**        |Float|Сумма себестоимости|да
|**quantity**   |Float|Количество единиц товара|да

#### Атрибуты доступные для фильтрации

Результаты отчета можно отфильтровать, используя параметр filter. Для каждого параметра можно указать только одно значение. Нельзя указывать пустые значения. Поддерживается фильтрация только на равенство.

Является обязательным указание одного из параметров фильтрации **product** или **variant**.

| Название               | Описание  |
| ------------------------------ |:---------------------------|
|**agent** | ссылка на контрагента, по которому нужно произвести фильтрацию.
|**product** | ссылка на товар, по которому нужно произвести фильтрацию. В выдаче будет товар вместе с его модификациями.
|**variant** | ссылка на модификацию, по которой нужно произвести фильтрацию.
|**organization** | ссылка на юрлицо, по которому нужно произвести фильтрацию.
|**project** | ссылка на проект, по которому нужно произвести фильтрацию.
|**contract** | ссылка на договор, по которому нужно произвести фильтрацию.
|**store** | ссылка на склад, по которому нужно произвести фильтрацию.
|**retailStore** | ссылка на точку продаж, по которой нужно произвести фильтрацию.
|**agentTag** | строка с названием группы контрагентов, по которой нужно произвести фильтрацию.

Примеры фильтрации:

- `filter=agent=https://online.moysklad.ru/api/remap/1.2/entity/counterparty/f8f729a5-a784-11e9-ac12-000800000000`
- `filter=product=https://online.moysklad.ru/api/remap/1.2/entity/product/f8f729a5-a784-11e9-ac12-000800000000`
- `filter=organization=https://online.moysklad.ru/api/remap/1.2/entity/organization/0347beb0-a785-11e9-ac12-000800000003`
- `filter=store=https://online.moysklad.ru/api/remap/1.2/entity/store/656c4032-8667-11e6-8a84-bae500003321`
- `filter=project=https://online.moysklad.ru/api/remap/1.2/entity/project/7a5f0ed5-8552-11e6-8a84-bae500000046`
- `filter=contract=https://online.moysklad.ru/api/remap/1.2/entity/contract/7a5f0ed5-8552-11e6-8a84-bae500085742`
- `filter=retailStore=https://online.moysklad.ru/api/remap/1.2/entity/retailstore/9ca74859-85c7-11e9-ac12-000d00000030`
- `filter=agentTag=favorites`

### Получить Обороты по товару

Запрос на получение отчета Обороты по товару.

Для успешного выполнения запроса необходимо указание одного из параметров фильтрации **product** или **variant**. 

**Параметры**

| Параметр                | Описание  |
| ------------------------------ |:---------------------------|
|**momentFrom** |  `date` (optional) *Example: 2018-09-01 00:00:00* Начало периода отчета|
|**momentTo** |  `date` (optional) *Example: 2018-10-01 00:00:00* Конец периода отчета|

**Заголовки**

| Заголовок                | Описание  |
| ------------------------------ |:---------------------------|
|**X-Lognex-Accept-Timezone** | Опциональный заголовок, в котором указана текущая дата на клиенте в RFC 3522. Таймзону обязательно указывать в формате знак и 4 символа (не в Obsolete Date and Time). Пример даты: `Wed, 16 Aug 2017 23:07:01 +0700`. При подсчете показателей даты операций смещаются в таймзону клиента.|
|**X-Lognex-Content-Timezone** | Заголовок ответа. В нем указывается (как думает сервер) текущая дата на клиенте в RFC 3522.|


> Запрос на получение отчета "Обороты по товару" с указанным id товара.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/report/turnover/bystore?filter=product=https://online.moysklad.ru/api/remap/1.2/entity/product/66990dc7-bdfe-11eb-c0a8-800c00000016"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление отчета.

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
    "href": "https://online.moysklad.ru/api/remap/1.2/report/turnover/bystore?filter=product=https://online.moysklad.ru/api/remap/1.2/entity/product/66990dc7-bdfe-11eb-c0a8-800c00000016",
    "type": "turnoverbystore",
    "mediaType": "application/json",
    "size": 2,
    "limit": 1000,
    "offset": 0
  },
  "rows": [
    {
      "assortment": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/66990dc7-bdfe-11eb-c0a8-800c00000016",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
          "type": "product",
          "mediaType": "application/json",
          "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=66989c14-bdfe-11eb-c0a8-800c00000014"
        },
        "name": "товар 2",
        "uom": {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/uom/af3b8110-5a23-4839-b3f7-a486f771a315",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/uom/metadata",
            "type": "uom",
            "mediaType": "application/json"
          },
          "name": "10^6 м3"
        }
      },
      "stockByStore": [
        {
          "store": {
            "meta": {
              "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/9238b396-b719-11eb-c0a8-800c00000074",
              "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
              "type": "store",
              "mediaType": "application/json",
              "uuidHref": "https://online.moysklad.ru/app/#warehouse/edit?id=9238b396-b719-11eb-c0a8-800c00000074"
            },
            "name": "Основной склад"
          },
          "onPeriodStart": {
            "quantity": 0.0,
            "sum": 0.0
          },
          "onPeriodEnd": {
            "quantity": 1.0,
            "sum": 0.0
          },
          "income": {
            "quantity": 3.0,
            "sum": 0.0
          },
          "outcome": {
            "quantity": 2.0,
            "sum": 0.0
          }
        }
      ]
    },
    {
      "assortment": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/variant/3e32ef51-c1f1-11eb-c0a8-800c00000003",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/variant/metadata",
          "type": "variant",
          "mediaType": "application/json",
          "uuidHref": "https://online.moysklad.ru/app/#feature/edit?id=3e3278e5-c1f1-11eb-c0a8-800c00000001"
        },
        "name": "товар 2 (красный)",
        "uom": {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/uom/af3b8110-5a23-4839-b3f7-a486f771a315",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/uom/metadata",
            "type": "uom",
            "mediaType": "application/json"
          },
          "name": "10^6 м3"
        }
      },
      "stockByStore": [
        {
          "store": {
            "meta": {
              "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/9238b396-b719-11eb-c0a8-800c00000074",
              "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
              "type": "store",
              "mediaType": "application/json",
              "uuidHref": "https://online.moysklad.ru/app/#warehouse/edit?id=9238b396-b719-11eb-c0a8-800c00000074"
            },
            "name": "Основной склад"
          },
          "onPeriodStart": {
            "quantity": 0.0,
            "sum": 0.0
          },
          "onPeriodEnd": {
            "quantity": 2.0,
            "sum": 20000.0
          },
          "income": {
            "quantity": 3.0,
            "sum": 30000.0
          },
          "outcome": {
            "quantity": 1.0,
            "sum": 10000.0
          }
        },
        {
          "store": {
            "meta": {
              "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/8d3d4ad8-be02-11eb-c0a8-800c00000025",
              "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
              "type": "store",
              "mediaType": "application/json",
              "uuidHref": "https://online.moysklad.ru/app/#warehouse/edit?id=8d3d4ad8-be02-11eb-c0a8-800c00000025"
            },
            "name": "склад 2"
          },
          "onPeriodStart": {
            "quantity": 0.0,
            "sum": 0.0
          },
          "onPeriodEnd": {
            "quantity": -5.0,
            "sum": 0.0
          },
          "income": {
            "quantity": 0.0,
            "sum": 0.0
          },
          "outcome": {
            "quantity": 5.0,
            "sum": 0.0
          }
        }
      ]
    }
  ]
}
```
