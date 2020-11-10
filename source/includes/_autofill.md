## Автозаполнение

Средствами JSON API можно рассчитать значение скидок, цен и ндс для позиций следующих документов:

- [Оприходование](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-oprihodowanie)
- [Заказ покупателя](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-zakaz-pokupatelq)
- [Заказ поставщику](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-zakaz-postawschiku)
- [Счет покупателю](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-schet-pokupatelu)
- [Счет поставщику](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-schet-postawschika)
- [Отгрузка](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-otgruzka)
- [Приемка](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-priemka)
- [Списание](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-spisanie)
- [Перемещение](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-peremeschenie)
- [Розничная продажа](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-roznichnaq-prodazha)
- [Розничный возврат](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-roznichnyj-wozwrat)
- [Возврат покупателя](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-vozwrat-pokupatelq)
- [Возврат поставщику](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-vozwrat-postawschiku)
- [Инвентаризация](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-inwentarizaciq)
- [Полученный отчет комиссионера](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-poluchennyj-otchet-komissionera)
- [Выданный отчет комиссионера](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-vydannyj-otchet-komissionera)
- [Внутренний заказ](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-vnutrennij-zakaz)

Заполнение скидок не поддерживает следующие типы:

- [Инвентаризация](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-inwentarizaciq)
- [Перемещение](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-peremeschenie)
- [Внутренний заказ](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-vnutrennij-zakaz)
- [Оприходование](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-oprihodowanie)
- [Списание](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-spisanie)

Заполнение цен не поддерживает [Инвентаризация](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-inwentarizaciq)


### Шаблон автозаполнения

#### Атрибуты сущности

Атрибуты сущности нужно передавать в зависимости от типа документа, для которого будет выполнено автозаполнение. В 
соответствие с типом, будут обрабатываться соответствующие поля.

Ниже приводятся поля, которые влияют на заполнение скидок, цен и ндс.

+ **organization** - Ссылка на юрлицо в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye). Обязателен со значением `evaluate_vat` параметра `action`
+ **agent** - Ссылка на контрагента в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye). 
Обязателен со значениями `evaluate_price`, `evaluate_discount` параметра `action`
+ **vatEnabled** - Учитывается ли НДС
+ **vatIncluded** - Включен ли НДС в цену
+ **rate** - Валюта. Если не передано, заполняется валютой учета
+ **positions** - Позиции документа

При этом, если помимо вышеперечисленных полей были добавлены другие, не влияющие на заполнение, то они будут присутствовать в
ответе в том же порядке и с теми же значениями.

**Примечание**

Если в документе не используется поле `agent`, то для расчета цен `evaluate_price` и скидок `evaluate_discount` 
используется значение поля `organization`.

#### Позиции документа

Позиции в шаблоне - это список товаров/услуг/модификаций/серий/комплектов.
Объект позиции содержит следующие поля:

+ **quantity** - Количество товаров/услуг данного вида в позиции. Если позиция - товар, у которого включен учет по серийным номерам, то значение в этом поле всегда будет равно количеству серийных номеров для данной позиции в документе.
+ **price** - Цена товара/услуги в копейках.
+ **discount** - Процент скидки или наценки.
+ **vat** - НДС, которым облагается текущая позиция.
+ **assortment** - Ссылка на товар/услугу/серию/модификацию/комплект, которую представляет собой позиция, в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye)
+ **discountedPrice** - Цена товара/услуги с учетом скидок и ндс в копейках.
+ **sum** - Общая сумма с учетом скидки за указанное количество товара в позиции в копейках.

### Запрос автозаполения

Запрос заполения полей шаблона.
Результат: Объект JSON, с заполненным шаблоном.

**Параметры**

| Параметр | Описание | 
| --------- |:----|
| action | `enum` (optional) *Example: evaluate_discount, evaluate_price, evaluate_discount* Определяет какую информацию нужно заполнить: цены (evaluate_price), ндс (evaluate_vat) или скидки (evaluate_discount). `Допустимые значения: evaluate_price, evaluate_discount, evaluate_vat`. |

### Запрос автозаполения цен

Запрос автозаполения с параметром `action` со значением `evaluate_price`. Требуется заполнение поля **agent**. 
Заполняет поле цены товара **price** (если явно не передано) ценой переданного в поле **agent** контрагента, 
а также поле **discountedPrice**, с учетом рассчитанной или переданной скидки **discount** 
(принимается за 0, если значение отсутствует) и НДС **vat** (не учитывается, если пустое, поле **vatEnabled** 
имеет значение `false` или **vatIncluded** имеет значение `true`). Если передано поле **quantity**, 
то будет рассчитано поле **sum**.

> Запрос автозаполения цен

```shell
  curl -X POST
    "https://online.moysklad.ru/api/remap/1.2/wizard/demand?action=evaluate_price"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '
{
   "agent":{
      "meta":{
         "href":"https://online.moysklad.ru/api/remap/1.2/entity/counterparty/eff93a94-c03a-11ea-c0a8-f00c0000001f",
         "metadataHref":"https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
         "type":"counterparty",
         "mediaType":"application/json",
         "uuidHref":"https://online.moysklad.ru/app/#company/edit?id=eff93a94-c03a-11ea-c0a8-f00c0000001f"
      }
   },
   "positions":[
      {
         "assortment":{
            "meta":{
               "href":"https://online.moysklad.ru/api/remap/1.2/entity/product/46628fb5-c1c8-11ea-c0a8-f00c0000001a",
               "metadataHref":"https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
               "type":"product",
               "mediaType":"application/json",
               "uuidHref":"https://online.moysklad.ru/app/#good/edit?id=46628fb5-c1c8-11ea-c0a8-f00c00000018"
            }
         },
         "quantity":12
      },
      {
         "assortment":{
            "meta":{
               "href":"https://online.moysklad.ru/api/remap/1.2/entity/product/bb989405-bf9e-11ea-c0a8-f0100000000e",
               "metadataHref":"https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
               "type":"product",
               "mediaType":"application/json",
               "uuidHref":"https://online.moysklad.ru/app/#good/edit?id=bb96904c-bf9e-11ea-c0a8-f0100000000c"
            }
         },
         "discount":20
      }
   ]
}'  
```

> Response 200 (application/json)
> Успешный запрос. Результат - JSON представление заполненного шаблона документа.

```json
{
  "agent": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/eff93a94-c03a-11ea-c0a8-f00c0000001f",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
      "mediaType": "application/json",
      "uuidHref": "https://online.moysklad.ru/app/#company/edit?id=eff93a94-c03a-11ea-c0a8-f00c0000001f"
    }
  },
  "rate": {
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/44126ea6-bf76-11ea-c0a8-f01000000077",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json",
        "uuidHref": "https://online.moysklad.ru/app/#currency/edit?id=44126ea6-bf76-11ea-c0a8-f01000000077"
      }
    }
  },
  "positions": [
    {
      "price": 3300.0,
      "discountedPrice": 3300.0,
      "quantity": 12.0,
      "sum": 39600.0,
      "assortment": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/46628fb5-c1c8-11ea-c0a8-f00c0000001a",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
          "type": "product",
          "mediaType": "application/json",
          "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=46628fb5-c1c8-11ea-c0a8-f00c00000018"
        }
      }
    },
    {
      "price": 3300.0,
      "discountedPrice": 2640.0,
      "discount": 20.0,
      "assortment": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/bb989405-bf9e-11ea-c0a8-f0100000000e",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
          "type": "product",
          "mediaType": "application/json",
          "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=bb96904c-bf9e-11ea-c0a8-f0100000000c"
        }
      }
    }
  ]
}
```

### Запрос автозаполения скидок

Запрос автозаполения с параметром `action` со значением `evaluate_discount`. Требуется заполнение поля **agent**. 
Заполняет поле скидки **discount** (если явно не передано) суммой применимых к данному товару активных скидок 
переданного в поле **agent** контрагента.

> Запрос автозаполения скидок

```shell
  curl -X POST
    "https://online.moysklad.ru/api/remap/1.2/wizard/demand?action=evaluate_discount"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '
{
   "agent":{
      "meta":{
         "href":"https://online.moysklad.ru/api/remap/1.2/entity/counterparty/eff93a94-c03a-11ea-c0a8-f00c0000001f",
         "metadataHref":"https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
         "type":"counterparty",
         "mediaType":"application/json",
         "uuidHref":"https://online.moysklad.ru/app/#company/edit?id=eff93a94-c03a-11ea-c0a8-f00c0000001f"
      }
   },
   "positions":[
      {
         "assortment":{
            "meta":{
               "href":"https://online.moysklad.ru/api/remap/1.2/entity/product/46628fb5-c1c8-11ea-c0a8-f00c0000001a",
               "metadataHref":"https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
               "type":"product",
               "mediaType":"application/json",
               "uuidHref":"https://online.moysklad.ru/app/#good/edit?id=46628fb5-c1c8-11ea-c0a8-f00c00000018"
            }
         },
         "quantity":12
      },
      {
         "assortment":{
            "meta":{
               "href":"https://online.moysklad.ru/api/remap/1.2/entity/product/bb989405-bf9e-11ea-c0a8-f0100000000e",
               "metadataHref":"https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
               "type":"product",
               "mediaType":"application/json",
               "uuidHref":"https://online.moysklad.ru/app/#good/edit?id=bb96904c-bf9e-11ea-c0a8-f0100000000c"
            }
         }
      }
   ]
}'  
```

> Response 200 (application/json)
> Успешный запрос. Результат - JSON представление заполненного шаблона документа.

```json
{
  "agent": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/eff93a94-c03a-11ea-c0a8-f00c0000001f",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
      "mediaType": "application/json",
      "uuidHref": "https://online.moysklad.ru/app/#company/edit?id=eff93a94-c03a-11ea-c0a8-f00c0000001f"
    }
  },
  "rate": {
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/44126ea6-bf76-11ea-c0a8-f01000000077",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json",
        "uuidHref": "https://online.moysklad.ru/app/#currency/edit?id=44126ea6-bf76-11ea-c0a8-f01000000077"
      }
    }
  },
  "positions": [
    {
      "discount": 65.0,
      "assortment": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/46628fb5-c1c8-11ea-c0a8-f00c0000001a",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
          "type": "product",
          "mediaType": "application/json",
          "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=46628fb5-c1c8-11ea-c0a8-f00c00000018"
        }
      },
      "quantity": 12.0
    },
    {
      "discount": 40.0,
      "assortment": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/bb989405-bf9e-11ea-c0a8-f0100000000e",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
          "type": "product",
          "mediaType": "application/json",
          "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=bb96904c-bf9e-11ea-c0a8-f0100000000c"
        }
      }
    }
  ]
}
```

### Запрос автозаполения НДС

Запрос автозаполения с параметром `action` со значением `evaluate_vat`. Требуется заполнение поля **organization**. 
Заполняет поле **vatEnabled** на основе того, является ли переданная в поле **organization** организация плательщиком 
НДС и поля **vat** у позиций значением из карточки товара, если организация - плательщик НДС.

> Запрос автозаполения НДС

```shell
  curl -X POST
    "https://online.moysklad.ru/api/remap/1.2/wizard/demand?action=evaluate_vat"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '
{
    "organization": {
        "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/44055d92-bf76-11ea-c0a8-f01000000070",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
            "type": "organization",
            "mediaType": "application/json",
            "uuidHref": "https://online.moysklad.ru/app/#mycompany/edit?id=44055d92-bf76-11ea-c0a8-f01000000070"
        }
    },
    "vatEnabled": "true",
    "rate": {
        "currency": {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/44126ea6-bf76-11ea-c0a8-f01000000077",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
            "type": "currency",
            "mediaType": "application/json",
            "uuidHref": "https://online.moysklad.ru/app/#currency/edit?id=44126ea6-bf76-11ea-c0a8-f01000000077"
          }
        }
    },
    "positions": [
        {
            "assortment": {
                "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/46628fb5-c1c8-11ea-c0a8-f00c0000001a",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                    "type": "product",
                    "mediaType": "application/json",
                    "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=466222d6-c1c8-11ea-c0a8-f00c00000018"
                }
            },
            "quantity": 12
        },
        {
            "assortment": {
                "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/bb989405-bf9e-11ea-c0a8-f0100000000e",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                    "type": "product",
                    "mediaType": "application/json",
                    "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=bb96904c-bf9e-11ea-c0a8-f0100000000c"
                }
            }
        }
    ]
}'  
```

> Response 200 (application/json)
> Успешный запрос. Результат - JSON представление заполненного шаблона документа.

```json
{
  "organization": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/44055d92-bf76-11ea-c0a8-f01000000070",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
      "type": "organization",
      "mediaType": "application/json",
      "uuidHref": "https://online.moysklad.ru/app/#mycompany/edit?id=44055d92-bf76-11ea-c0a8-f01000000070"
    }
  },
  "vatEnabled": true,
  "rate": {
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/44126ea6-bf76-11ea-c0a8-f01000000077",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json",
        "uuidHref": "https://online.moysklad.ru/app/#currency/edit?id=44126ea6-bf76-11ea-c0a8-f01000000077"
      }
    }
  },
  "positions": [
    {
      "assortment": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/46628fb5-c1c8-11ea-c0a8-f00c0000001a",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
          "type": "product",
          "mediaType": "application/json",
          "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=466222d6-c1c8-11ea-c0a8-f00c00000018"
        }
      },
      "quantity": 12.0,
      "vat": 10
    },
    {
      "vat": 18,
      "assortment": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/bb989405-bf9e-11ea-c0a8-f0100000000e",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
          "type": "product",
          "mediaType": "application/json",
          "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=bb96904c-bf9e-11ea-c0a8-f0100000000c"
        }
      }
    }
  ]
}
```