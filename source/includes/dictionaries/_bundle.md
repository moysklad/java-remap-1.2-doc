## Комплект
### Комплекты

Средствами JSON API можно создавать и обновлять сведения о Комплектах, запрашивать списки Комплектов и сведения по отдельным Комплектам. Кодом сущности для Комплекта в составе JSON API является ключевое слово **bundle**.

#### Атрибуты сущности

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**              |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные Комплекта|&mdash;|да
|**id**                |UUID|ID Комплекта|Только для чтения|да
|**accountId**         |UUID|ID учетной записи|Только для чтения|да
|**owner**         |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные владельца (Сотрудника)|&mdash;|да
|**shared**         |Boolean|Общий доступ|&mdash;|да
|**group**         |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные отдела сотрудника|&mdash;|да
|**syncId**                |UUID|ID синхронизации|После заполнения недоступно для изменения|нет
|**updated**         |DateTime|Момент последнего обновления сущности|Только для чтения|да
|**name**         |String(255)|Наименование Комплекта|Необходимое при создании|да
|**description**        |String(4096)|Описание Комплекта|&mdash;|нет
|**code**         |String(255)|Код Комплекта|&mdash;|нет
|**externalCode**         |String(255)|Внешний код Комплекта|&mdash;|да
|**archived**        |Boolean|Добавлен ли Комплект в архив|&mdash;|да
|**pathName**         |String|Наименование группы, в которую входит Комплект|Только для чтения|да
|**vat**         |Int|НДС %|&mdash;|нет
|**vatEnabled**     |Boolean|Включен ли НДС для товара. С помощью этого флага для товара можно выставлять НДС = 0 или НДС = "без НДС". (vat = 0, vatEnabled = false) -> vat = "без НДС", (vat = 0, vatEnabled = true) -> vat = 0%.|&mdash;|да
|**useParentVat**   |Boolean|Использует ли товар НДС с родительской группы|&mdash;|да
|**effectiveVat**         |Int|Реальный НДС %|Только для чтения|нет
|**productFolder**         |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные группы Комплекта|&mdash;|нет
|**uom**         |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Единицы измерения|&mdash;|нет
|**images**       |Array(Object)|Изображения Комплекта. Изображений у Модификации может быть не более 10. [Подробнее тут](../dictionaries/#suschnosti-komplekt-komplekty-komponenty-komplekta-izobrazhenie-struktura-i-zagruzka)|&mdash;|нет
|**minPrice**         |Object|Минимальная цена. [Подробнее тут](../dictionaries/#suschnosti-komplekt-komplekty-atributy-wlozhennyh-suschnostej-minimal-naq-cena)|&mdash;|нет
|**salePrices**         |Array(Object)|Цены продажи|&mdash;|нет
|**attributes**         |Array(Object)|Коллекция доп. полей|&mdash;|нет
|**country**            |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные Страны|&mdash;|нет
|**article**         |String(255)|Артикул|&mdash;|нет
|**weight**         |Int|Вес|&mdash;|нет
|**volume**         |Int|Объем|&mdash;|нет
|**barcodes**         |Array(Object)|Штрихкоды Комплекта. [Подробнее тут](../dictionaries/#suschnosti-komplekt-komplekty-komponenty-komplekta-shtrih-kody)|&mdash;|нет
|**discountProhibited**        |Boolean|Признак запрета скидок|&mdash;|да
|**overhead**         |Object|Дополнительные расходы. [Подробнее тут](../dictionaries/#suschnosti-komplekt-komplekty-atributy-wlozhennyh-suschnostej-dopolnitel-nye-rashody)|&mdash;|нет
|**components**         |Array(Object)|Компоненты Комплекта. [Подробнее тут](../dictionaries/#suschnosti-komplekt-komplekty-komponenty-komplekta)|&mdash;|нет
|**trackingType**         |Enum|Тип маркируемой продукции. [Подробнее тут](../dictionaries/#suschnosti-komplekt-komplekty-atributy-suschnosti-tip-markiruemoj-produkcii)|&mdash;|нет
|**tnved**         |String(255)|Код ТН ВЭД|&mdash;|нет
|**partialDisposal**         |Boolean|Управление состоянием частичного выбытия маркированного товара. «true» - возможность включена.|&mdash;|нет
|**paymentItemType**         |Enum|Признак предмета расчета. [Подробнее тут](../dictionaries/#suschnosti-komplekt-komplekty-atributy-suschnosti-priznak-predmeta-rascheta)|&mdash;|нет
|**taxSystem**         |Enum|Код системы налогообложения. [Подробнее тут](../dictionaries/#suschnosti-komplekt-komplekty-atributy-suschnosti-kod-sistemy-nalogooblozheniq)|&mdash;|нет
|**files**              |MetaArray|Массив метаданных [Файлов](../dictionaries/#suschnosti-fajly) (Максимальное количество файлов - 100)|&mdash;|нет|

##### Тип маркируемой продукции
Значения поля trackingType.

| Значение                | Описание  |
| ------------------------------ |:---------------------------|
| **NOT_TRACKED**           | Без маркировки|
| **TOBACCO**                 |Тип маркировки "Табак"|
| **SHOES**        |Тип маркировки "Обувь"|
| **LP_CLOTHES**        |Тип маркировки "Одежда"|
| **LP_LINENS**         |Тип маркировки "Постельное белье"|
| **PERFUMERY**         |Духи и туалетная вода|
| **ELECTRONICS**       |Фотокамеры и лампы-вспышки|
| **TIRES**       |Шины и покрышки|
| **OTP**       |Альтернативная табачная продукция|

##### Признак предмета расчета
Значения поля paymentItemType.

| Значение                | Описание  |
| ------------------------------ |:---------------------------|
| **GOOD**                        | Товар|
| **EXCISABLE_GOOD**               |Подакцизный товар|
| **COMPOUND_PAYMENT_ITEM**       |Составной предмет расчета|
| **ANOTHER_PAYMENT_ITEM**        |Иной предмет расчета|

##### Код системы налогообложения
Значения поля taxSystem.

| Значение                | Описание  |
| ------------------------------ |:---------------------------|
| **TAX_SYSTEM_SAME_AS_GROUP**            | Совпадает с группой|
| **GENERAL_TAX_SYSTEM**                  | ОСН|
| **SIMPLIFIED_TAX_SYSTEM_INCOME**        | УСН. Доход|
| **SIMPLIFIED_TAX_SYSTEM_INCOME_OUTCOME**| УСН. Доход-Расход|
| **UNIFIED_AGRICULTURAL_TAX**            | ЕСХН|
| **PRESUMPTIVE_TAX_SYSTEM**              | ЕНВД|
| **PATENT_BASED**                        | Патент|

#### Комплект как позиция документа
Комплект может выступать в роли позиции документа. Он также как и товары, услуги и модификации может быть передан в составе позиции в формате метаданных.<br>
Вот некоторые ограничения, связанные с использованием комплектов как позиций:

+ Количество комплектов должно быть целым числом
+ Комплекты не могут быть позициями в следующих типах документов:
  - Заказы поставщикам
  - Счета поставщиков
  - Приемки
  - Возвраты поставщикам
  - Выданные отчеты комиссионера
  - Списания
  - Оприходования
  - Перемещения
  - Инвентаризации
  - Тех. карты
  - Тех. операции
  - Внутренние заказы
+ Комплект не может быть позицией отгрузки по комиссионному договору:
  - нельзя добавить комплект в отгрузку по комиссионному договору
  - нельзя установить комиссионный договор в отгрузке с комплектами
  - нельзя изменить договор на комиссионный, если по нему есть отгрузки с комплектами


#### Атрибуты вложенных сущностей
##### Дополнительные расходы
Структура объекта overhead.

| Название  | Тип | Описание                    | Свойство поля в запросе | Обязательное при ответе|
| --------- |:----|:----------------------------|:---------------|:-----------------------|
**value**   |Float|Значение цены| &mdash; | да
**currency**|[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Ссылка на валюту в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye)| &mdash; | да

##### Минимальная цена
Структура объекта minPrice.

| Название  | Тип | Описание                    | Свойство поля в запросе | Обязательное при ответе|
| --------- |:----|:----------------------------|:---------------|:-----------------------|
**value**   |Float|Значение цены| &mdash; | да
**currency**|[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Ссылка на валюту в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye)| &mdash; | да

#### Компоненты Комплекта
Компоненты Комплекта - это список товаров/услуг/модификаций, который входят в состав комплекта. Компонентов у комплекта может быть от 1 до 50.
Объект компонента Комплекта содержит следующие поля:

| Название  | Тип | Описание                    | Свойство поля в запросе | Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**id**                |UUID|ID компонента|Только для чтения|да
|**accountId**         |UUID|ID учетной записи|Только для чтения|да
|**quantity**         |Int|Количество товаров/услуг данного вида в компоненте|Только для чтения|да
|**assortment**             |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные товара/услуги/серии, которую представляет собой компонент|&mdash;|да

##### Метаданные Комплектов
Метаданные Комплектов содержат информацию о дополнительных полях.

Посмотреть все созданные в основном интерфейсе доп. поля Комплектов,
а также все типы цен можно с помощью запроса на получение метаданных Комплектов.
Ответ - объект, со следующей структурой:

| Название  | Тип | Описание                    | Свойство поля в запросе | Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**              |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные |&mdash;|да
|**attributes**        |Array(Object)|коллекция всех существующих доп. полей Комплектов|&mdash;|да


Структуры объектов отдельных коллекций:

##### Штрих коды:
При создании штрихкода требуется описать объект с полем, являющимся форматом представления штрихкода в нижнем регистре, со строковым значением самого штрихкода. Наименование полей отдельного объекта, представляющего штрихкод:

|Название|Описание|
|--------------|-----------------------------------|
| **ean13**          | штрихкод в формате EAN13, если требуется создать штрихкод в формате EAN13           |
| **ean8**           | штрихкод в формате EAN8, если требуется создать штрихкод в формате EAN8             |
| **code128**        | штрихкод в формате Code128, если требуется создать штрихкод в формате Code128       |
| **gtin**           | штрихкод в формате GTIN, если требуется создать штрихкод в формате GTIN. Валидируется на соответствие формату GS1|

Для обновления списка штрихкодов необходимо передавать их полный список, включающий как старые, так и новые значения. 
Отсутствующие значения штрихкодов при обновлении будут удалены. При обновлении списка штрихкодов валидируются только новые значения. 
Ранее сохраненные штрихкоды не валидируются. То есть, если один из старых штрихкодов не соответствует требованиям к валидации, то ошибки при обновлении списка не будет. 
Если на вход передан пустой список штрихкодов или список из пустых значений, то ранее созданные штрихкоды будут удалены.

Особенности создания списка штрихкодов при создании комплекта:

+ Если передать список штрихкодов на вход, то полученные значения штрихкодов сохраняются, а пустые значения игнорируются.
+ Если передать список из пустых значений штрихкодов на вход, то для продукции не будет создано ни одного штрихкода.
+ Если не передать на вход атрибут barcodes или передать пустой список в нем, то по умолчанию будет создан один случайный штрихкод типа EAN13 для продукции.

О работе с доп. полями Комплектов можно прочитать [здесь](../#mojsklad-json-api-obschie-swedeniq-rabota-s-dopolnitel-nymi-polqmi)

##### Изображение: структура и загрузка.
При запросе Комплекта с изображениями будет выведено json представление этого Комплекта, содержащее поле **images**. Данное поле является 
массивом элементов. Элементы поля **images** имеют поля:

| Название  | Тип | Описание                    | Свойство поля в запросе | Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта|&mdash;|да
|**title**               |String(255)|Название Изображения|&mdash;|да
|**filename**               |String(255)|Имя файла|&mdash;|да
|**size**               |Int|Размер файла в байтах|&mdash;|да
|**updated**               |DateTime|Время загрузки файла на сервер|&mdash;|да
|**miniature**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные миниатюры изображения|&mdash;|да
|**tiny**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные уменьшенного изображения|&mdash;|да

<h4>Загрузка</h4>
Для загрузки изображения нужно в теле запроса на [создание](../dictionaries/#suschnosti-komplekt-sozdat-komplekt) или [обновление](../dictionaries/#suschnosti-komplekt-izmenit-komplekt) Комплекта
указать поле **images**  со списком элементов, имеющих следующие атрибуты:

| Название                | Описание  |
| ------------------------------ |:---------------------------|
|**filename** | имя файла с расширением. Например - "банан.png"|
| **content** | Изображение, закодированное в формате Base64.|

Если в запросе на обновление **images** будет содержать пустой массив элементов, то все Изображения у Комплекта будут удалены, 
т.к. сервер посчитает, что пользователь хочет обновить список Изображений Комплекта.

Документация API по работе с Изображениями приведена в главе [Изображение](../dictionaries/#suschnosti-izobrazhenie).

О работе с доп. полями Комплектов можно прочитать [здесь](../#mojsklad-json-api-obschie-swedeniq-rabota-s-dopolnitel-nymi-polqmi)

### Получить список комплектов
Запрос на получение всех комплектов для данной учетной записи.
Результат: Объект JSON, включающий в себя поля:

| Название  | Тип | Описание                    |
| --------- |:----|:----------------------------|
**meta** |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные о выдаче,
**context** | [Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye) | Метаданные о сотруднике, выполнившем запрос.
**rows** |Array(Object)| Массив JSON объектов, представляющих собой комплекты.

**Параметры**

| Параметр                | Описание  |
| ------------------------------ |:---------------------------|
|**limit** |  `number` (optional) **Default: 1000** *Example: 1000* Максимальное количество сущностей для извлечения.`Допустимые значения 1 - 1000`.|
|**offset** |  `number` (optional) **Default: 0** *Example: 40* Отступ в выдаваемом списке сущностей.|

> Получить список комплектов

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/bundle"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление списка комплектов.

```json
{
  "context": {
    "employee": {
      "meta": {
        "href": "http://online.moysklad.ru/api/remap/1.2/context/employee",
        "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
        "type": "employee",
        "mediaType": "application/json"
      }
    }
  },
  "meta": {
    "href": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/",
    "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/metadata",
    "type": "bundle",
    "mediaType": "application/json",
    "size": 1,
    "limit": 1000,
    "offset": 0
  },
  "rows": [
    {
      "meta": {
        "href": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/c21646cf-ee08-11e6-8af5-581e00000023",
        "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/metadata",
        "type": "bundle",
        "mediaType": "application/json"
      },
      "id": "c21646cf-ee08-11e6-8af5-581e00000023",
      "accountId": "badae4a0-ee05-11e6-8af5-581e00000001",
      "owner": {
        "meta": {
          "href": "http://online.moysklad.ru/api/remap/1.2/entity/employee/bb430a4e-ee05-11e6-8af5-581e0000002a",
          "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
          "type": "employee",
          "mediaType": "application/json"
        }
      },
      "shared": true,
      "group": {
        "meta": {
          "href": "http://online.moysklad.ru/api/remap/1.2/entity/group/bade121f-ee05-11e6-8af5-581e00000002",
          "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/group/metadata",
          "type": "group",
          "mediaType": "application/json"
        }
      },
      "updated": "2017-02-08 17:13:26",
      "name": "Комплект с товаром и услугой",
      "code": "00003",
      "externalCode": "iOzqxcTCiAK1-6-eAjVR12",
      "archived": false,
      "pathName": "",
      "discountProhibited": false,
      "uom": {
        "meta": {
          "href": "http://online.moysklad.ru/api/remap/1.2/entity/uom/19f1edc0-fc42-4001-94cb-c9ec9c62ec10",
          "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/uom/metadata",
          "type": "uom",
          "mediaType": "application/json"
        }
      },
      "images": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/bundle/c21646cf-ee08-11e6-8af5-581e00000023/images",
          "type": "image",
          "mediaType": "application/json",
          "size": 0,
          "limit": 1000,
          "offset": 0
        }
      },      
      "minPrice": {
        "value": 500,
        "currency": {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/10772c12-36e7-11e7-8a7f-40d000000097",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
            "type": "currency",
            "mediaType": "application/json"
          }
        }
      },
      "salePrices": [
        {
          "value": 0,
          "currency": {
            "meta": {
              "href": "http://online.moysklad.ru/api/remap/1.2/entity/currency/bb724075-ee05-11e6-8af5-581e00000058",
              "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
              "type": "currency",
              "mediaType": "application/json"
            }
          },
          "priceType": {
            "meta": {
              "href": "https://online.moysklad.ru/api/remap/1.2/context/companysettings/pricetype/672559f1-cbf3-11e1-9eb9-889ffa6f49fd",
              "type": "pricetype",
              "mediaType": "application/json"
            },
            "id": "672559f1-cbf3-11e1-9eb9-889ffa6f49fd",
            "name": "Цена продажи",
            "externalCode": "cbcf493b-55bc-11d9-848a-00112f43529a"
          }
        }
      ],
      "weight": 0,
      "volume": 0,
      "trackingType": "NOT_TRACKED",
      "barcodes": [
        {
          "ean13": "2000000000039"
        }
      ],
      "vatEnabled": false,
      "useParentVat": true,
      "components": {
        "meta": {
          "href": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/c21646cf-ee08-11e6-8af5-581e00000023/components",
          "type": "bundlecomponent",
          "mediaType": "application/json",
          "size": 2,
          "limit": 1000,
          "offset": 0
        }
      }
    }
  ],
  "taxSystem": "GENERAL_TAX_SYSTEM"
}
```

### Создать Комплект

Создать новый комплект.

#### Описание

Комплект создается на основе переданного объекта JSON,
который содержит представление нового Комплекта.
Результат - JSON представление созданного Комплекта. Для создания нового Комплекта
необходимо и достаточно указать в переданном объекте не пустое поле `name` и не пустое множество компонентов `components`.
Максимальное число компонентов в Комплекте - 50.

> Пример наиболее полного по количеству полей запроса.

```shell
  curl -X POST
    "https://online.moysklad.ru/api/remap/1.2/entity/bundle"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "name": "Комплект с товаром и еще одним товаром",
            "code": "00003",
            "externalCode": "iOzqxcTCiAK1-6-eAjVR12",
            "archived": false,
            "pathName": "",
            "discountProhibited": false,
            "uom": {
              "meta": {
                "href": "http://online.moysklad.ru/api/remap/1.2/entity/uom/19f1edc0-fc42-4001-94cb-c9ec9c62ec10",
                "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/uom/metadata",
                "type": "uom",
                "mediaType": "application/json"
              }
            },
            "minPrice": {
              "value": 500,
              "currency": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/10772c12-36e7-11e7-8a7f-40d000000097",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
                  "type": "currency",
                  "mediaType": "application/json"
                }
              }
            },
            "salePrices": [
              {
                "value": 20,
                "currency": {
                  "meta": {
                    "href": "http://online.moysklad.ru/api/remap/1.2/entity/currency/bb724075-ee05-11e6-8af5-581e00000058",
                    "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
                    "type": "currency",
                    "mediaType": "application/json"
                  }
                },
                "priceType": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/context/companysettings/pricetype/672559f1-cbf3-11e1-9eb9-889ffa6f49fd",
                    "type": "pricetype",
                    "mediaType": "application/json"
                  },
                  "id": "672559f1-cbf3-11e1-9eb9-889ffa6f49fd",
                  "name": "Цена продажи",
                  "externalCode": "cbcf493b-55bc-11d9-848a-00112f43529a"
                }
              }
            ],
            "weight": 0,
            "volume": 0,
            "trackingType": "NOT_TRACKED",
            "barcodes": [
              {
                "ean8": "20000000"
              },
              {
                "ean13": "2000000000000"
              },
              {
                "code128": "code128 barcode"
              },
              {
                "gtin": "00000000000130"
              }
            ],
            "vat": 20,
            "useParentVat": false,
            "components": [
              {
                "assortment": {
                  "meta": {
                    "href": "http://online.moysklad.ru/api/remap/1.2/entity/product/010afdea-ea40-11e6-5bed-427b000000b8",
                    "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                    "type": "product",
                    "mediaType": "application/json"
                  }
                },
                "quantity": 1
              },
              {
                "assortment": {
                  "meta": {
                    "href": "http://online.moysklad.ru/api/remap/1.2/entity/product/010afdea-ea40-11e6-5bed-427b000000b9",
                    "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                    "type": "product",
                    "mediaType": "application/json"
                  }
                },
                "quantity": 1
              }
            ]
          }'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление созданного Комплекта.

```json
{
  "meta": {
    "href": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/c21646cf-ee08-11e6-8af5-581e00000023",
    "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/metadata",
    "type": "bundle",
    "mediaType": "application/json"
  },
  "id": "c21646cf-ee08-11e6-8af5-581e00000023",
  "accountId": "badae4a0-ee05-11e6-8af5-581e00000001",
  "owner": {
    "meta": {
      "href": "http://online.moysklad.ru/api/remap/1.2/entity/employee/bb430a4e-ee05-11e6-8af5-581e0000002a",
      "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
      "type": "employee",
      "mediaType": "application/json"
    }
  },
  "shared": true,
  "group": {
    "meta": {
      "href": "http://online.moysklad.ru/api/remap/1.2/entity/group/bade121f-ee05-11e6-8af5-581e00000002",
      "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/group/metadata",
      "type": "group",
      "mediaType": "application/json"
    }
  },
  "updated": "2017-02-08 17:13:26",
  "name": "Комплект с товаром и еще одним товаром",
  "code": "00003",
  "externalCode": "iOzqxcTCiAK1-6-eAjVR12",
  "archived": false,
  "pathName": "",
  "discountProhibited": false,
  "uom": {
    "meta": {
      "href": "http://online.moysklad.ru/api/remap/1.2/entity/uom/19f1edc0-fc42-4001-94cb-c9ec9c62ec10",
      "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/uom/metadata",
      "type": "uom",
      "mediaType": "application/json"
    }
  },
  "images": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/bundle/c21646cf-ee08-11e6-8af5-581e00000023/images",
      "type": "image",
      "mediaType": "application/json",
      "size": 0,
      "limit": 1000,
      "offset": 0
    }
  },  
  "minPrice": {
    "value": 500,
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/10772c12-36e7-11e7-8a7f-40d000000097",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json"
      }
    }
  },
  "salePrices": [
    {
      "value": 20,
      "currency": {
        "meta": {
          "href": "http://online.moysklad.ru/api/remap/1.2/entity/currency/bb724075-ee05-11e6-8af5-581e00000058",
          "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
          "type": "currency",
          "mediaType": "application/json"
        }
      },
      "priceType": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/context/companysettings/pricetype/672559f1-cbf3-11e1-9eb9-889ffa6f49fd",
          "type": "pricetype",
          "mediaType": "application/json"
        },
        "id": "672559f1-cbf3-11e1-9eb9-889ffa6f49fd",
        "name": "Цена продажи",
        "externalCode": "cbcf493b-55bc-11d9-848a-00112f43529a"
      }
    }
  ],
  "weight": 0,
  "volume": 0,
  "trackingType": "NOT_TRACKED",
  "barcodes": [
    {
      "ean8": "20000000"
    },
    {
      "ean13": "2000000000000"
    },
    {
      "code128": "code128 barcode"
    },
    {
      "gtin": "00000000000130"
    }
  ],
  "vat": 20,
  "useParentVat": false,
  "vatEnabled": true,
  "components": {
    "meta": {
      "href": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/c21646cf-ee08-11e6-8af5-581e00000023/components",
      "type": "bundlecomponent",
      "mediaType": "application/json",
      "size": 2,
      "limit": 1000,
      "offset": 0
    },
    "rows": [
      {
        "meta": {
          "href": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/c21646cf-ee08-11e6-8af5-581e00000023/components/9404273f-eeb6-11e6-5bed-427b0000000c",
          "type": "bundlecomponent",
          "mediaType": "application/json"
        },
        "id": "9404273f-eeb6-11e6-5bed-427b0000000c",
        "accountId": "903083d9-d973-11e6-5bed-427b00000001",
        "assortment": {
          "meta": {
            "href": "http://online.moysklad.ru/api/remap/1.2/entity/product/010afdea-ea40-11e6-5bed-427b000000b8",
            "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
            "type": "product",
            "mediaType": "application/json"
          }
        },
        "quantity": 1
      },
      {
        "meta": {
          "href": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/c21646cf-ee08-11e6-8af5-581e00000023/components/9404273f-eeb6-11e6-5bed-427b0000000d",
          "type": "bundlecomponent",
          "mediaType": "application/json"
        },
        "id": "9404273f-eeb6-11e6-5bed-427b0000000d",
        "accountId": "903083d9-d973-11e6-5bed-427b00000001",
        "assortment": {
          "meta": {
            "href": "http://online.moysklad.ru/api/remap/1.2/entity/product/010afdea-ea40-11e6-5bed-427b000000b9",
            "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
            "type": "product",
            "mediaType": "application/json"
          }
        },
        "quantity": 1
      }
    ]
  }
}
```

> Пример запроса на создание Комплекта с загрузкой изображения

```shell
  curl -X POST
    "https://online.moysklad.ru/api/remap/1.2/entity/bundle"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "name": "Комплект с изображением",
            "images": [
              {
                "filename": "birdimage.png",
                "content": "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"
              }
            ],
            "components": [
              {
                "assortment": {
                  "meta": {
                    "href": "http://online.moysklad.ru/api/remap/1.2/entity/product/010afdea-ea40-11e6-5bed-427b000000b8",
                    "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                    "type": "product",
                    "mediaType": "application/json"
                  }
                },
                "quantity": 1
              }
            ]
          }'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление созданного Комплекта.

```json
{
  "meta": {
    "href": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/c21646cf-ee08-11e6-8af5-581e00000023",
    "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/metadata",
    "type": "bundle",
    "mediaType": "application/json"
  },
  "id": "c21646cf-ee08-11e6-8af5-581e00000023",
  "accountId": "badae4a0-ee05-11e6-8af5-581e00000001",
  "owner": {
    "meta": {
      "href": "http://online.moysklad.ru/api/remap/1.2/entity/employee/bb430a4e-ee05-11e6-8af5-581e0000002a",
      "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
      "type": "employee",
      "mediaType": "application/json"
    }
  },
  "shared": true,
  "group": {
    "meta": {
      "href": "http://online.moysklad.ru/api/remap/1.2/entity/group/bade121f-ee05-11e6-8af5-581e00000002",
      "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/group/metadata",
      "type": "group",
      "mediaType": "application/json"
    }
  },
  "updated": "2017-02-08 17:13:26",
  "name": "Комплект с картинкой",
  "code": "00003",
  "externalCode": "iOzqxcTCiAK1-6-eAjVR12",
  "archived": false,
  "pathName": "",
  "discountProhibited": false,
  "uom": {
    "meta": {
      "href": "http://online.moysklad.ru/api/remap/1.2/entity/uom/19f1edc0-fc42-4001-94cb-c9ec9c62ec10",
      "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/uom/metadata",
      "type": "uom",
      "mediaType": "application/json"
    }
  },
  "images": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/bundle/c21646cf-ee08-11e6-8af5-581e00000023/images",
      "type": "image",
      "mediaType": "application/json",
      "size": 1,
      "limit": 1000,
      "offset": 0
    },
    "updated": "2017-01-11 14:54:10",
    "title": "birdimage.png",
    "filename": "birdimage.png",
    "size": 14052,
    "miniature": {
      "href": "https://online.moysklad.ru/api/remap/1.2/download/bd159783-95ee-11e6-8a84-bae500000001?miniature=true",
      "mediaType": "image/png"
    },
    "tiny": {
      "href": "https://online.moysklad.ru/app/download/bd14f0b6-95ee-11e6-8a84-bae500000000.png",
      "mediaType": "image/png"
    }
  },  
  "minPrice": {
    "value": 500,
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/10772c12-36e7-11e7-8a7f-40d000000097",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json"
      }
    }
  },
  "salePrices": [
    {
      "value": 20,
      "currency": {
        "meta": {
          "href": "http://online.moysklad.ru/api/remap/1.2/entity/currency/bb724075-ee05-11e6-8af5-581e00000058",
          "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
          "type": "currency",
          "mediaType": "application/json"
        }
      },
      "priceType": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/context/companysettings/pricetype/672559f1-cbf3-11e1-9eb9-889ffa6f49fd",
          "type": "pricetype",
          "mediaType": "application/json"
        },
        "id": "672559f1-cbf3-11e1-9eb9-889ffa6f49fd",
        "name": "Цена продажи",
        "externalCode": "cbcf493b-55bc-11d9-848a-00112f43529a"
      }
    }
  ],
  "weight": 0,
  "volume": 0,
  "trackingType": "NOT_TRACKED",
  "barcodes": [
    {
      "ean13": "2000000000039"
    }
  ],
  "useParentVat": true,
  "vatEnabled": false,
  "components": {
    "meta": {
      "href": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/c21646cf-ee08-11e6-8af5-581e00000023/components",
      "type": "bundlecomponent",
      "mediaType": "application/json",
      "size": 2,
      "limit": 1000,
      "offset": 0
    },
    "rows": [
      {
        "meta": {
          "href": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/c21646cf-ee08-11e6-8af5-581e00000023/components/9404273f-eeb6-11e6-5bed-427b0000000c",
          "type": "bundlecomponent",
          "mediaType": "application/json"
        },
        "id": "9404273f-eeb6-11e6-5bed-427b0000000c",
        "accountId": "903083d9-d973-11e6-5bed-427b00000001",
        "assortment": {
          "meta": {
            "href": "http://online.moysklad.ru/api/remap/1.2/entity/product/010afdea-ea40-11e6-5bed-427b000000b8",
            "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
            "type": "product",
            "mediaType": "application/json"
          }
        },
        "quantity": 1
      },
      {
        "meta": {
          "href": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/c21646cf-ee08-11e6-8af5-581e00000023/components/9404273f-eeb6-11e6-5bed-427b0000000d",
          "type": "bundlecomponent",
          "mediaType": "application/json"
        },
        "id": "9404273f-eeb6-11e6-5bed-427b0000000d",
        "accountId": "903083d9-d973-11e6-5bed-427b00000001",
        "assortment": {
          "meta": {
            "href": "http://online.moysklad.ru/api/remap/1.2/entity/product/010afdea-ea40-11e6-5bed-427b000000b9",
            "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
            "type": "product",
            "mediaType": "application/json"
          }
        },
        "quantity": 1
      }
    ]
  }
}
```

### Массовое создание и обновление Комплектов
[Массовое создание и обновление](../#mojsklad-json-api-obschie-swedeniq-sozdanie-i-obnowlenie-neskol-kih-ob-ektow) Комплектов.
В теле запроса нужно передать массив, содержащий JSON представления Комплектов, которые вы хотите создать или обновить.
Обновляемые Комплекты должны содержать идентификатор в виде метаданных.

> Пример создания и обновления нескольких Комплектов

  ```shell
    curl -X POST
      "https://online.moysklad.ru/api/remap/1.2/entity/bundle"
      -H "Authorization: Basic <Credentials>"
      -H "Content-Type: application/json"
        -d '[
              {
                "name": "Комплект с товаром и еще одним товаром",
                "code": "00003",
                "externalCode": "iOzqxcTCiAK1-6-eAjVR12",
                "archived": false,
                "pathName": "",
                "uom": {
                  "meta": {
                    "href": "http://online.moysklad.ru/api/remap/1.2/entity/uom/19f1edc0-fc42-4001-94cb-c9ec9c62ec10",
                    "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/uom/metadata",
                    "type": "uom",
                    "mediaType": "application/json"
                  }
                },
                "minPrice": {
                  "value": 500,
                  "currency": {
                    "meta": {
                      "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/10772c12-36e7-11e7-8a7f-40d000000097",
                      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
                      "type": "currency",
                      "mediaType": "application/json"
                    }
                  }
                },
                "salePrices": [
                  {
                    "value": 20,
                    "currency": {
                      "meta": {
                        "href": "http://online.moysklad.ru/api/remap/1.2/entity/currency/bb724075-ee05-11e6-8af5-581e00000058",
                        "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
                        "type": "currency",
                        "mediaType": "application/json"
                      }
                    },
                    "priceType": {
                      "meta": {
                        "href": "https://online.moysklad.ru/api/remap/1.2/context/companysettings/pricetype/672559f1-cbf3-11e1-9eb9-889ffa6f49fd",
                        "type": "pricetype",
                        "mediaType": "application/json"
                      },
                      "id": "672559f1-cbf3-11e1-9eb9-889ffa6f49fd",
                      "name": "Цена продажи",
                      "externalCode": "cbcf493b-55bc-11d9-848a-00112f43529a"
                    }
                  }
                ],
                "weight": 0,
                "volume": 0,
                "trackingType": "NOT_TRACKED",
                "barcodes": [
                  {
                    "ean8": "20000000"
                  },
                  {
                    "ean13": "2000000000000"
                  },
                  {
                    "code128": "code128 barcode"
                  },
                  {
                    "gtin": "00000000000130"
                  }
                ],
                "components": [
                  {
                    "assortment": {
                      "meta": {
                        "href": "http://online.moysklad.ru/api/remap/1.2/entity/product/010afdea-ea40-11e6-5bed-427b000000b8",
                        "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                        "type": "product",
                        "mediaType": "application/json"
                      }
                    },
                    "quantity": 1
                  },
                  {
                    "assortment": {
                      "meta": {
                        "href": "http://online.moysklad.ru/api/remap/1.2/entity/product/010afdea-ea40-11e6-5bed-427b000000b9",
                        "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                        "type": "product",
                        "mediaType": "application/json"
                      }
                    },
                    "quantity": 1
                  }
                ]
              },
              {
                "meta": {
                  "href": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/c21646cf-ee08-11e6-8af5-581e00000023",
                  "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/metadata",
                  "type": "bundle",
                  "mediaType": "application/json"
                },
                "name": "Новое наименование",
                "barcodes": [
                  {
                    "ean8": "20000000"
                  },
                  {
                    "ean13": "2000000000000"
                  },
                  {
                    "code128": "code128 barcode"
                  },
                  {
                    "gtin": "00000000000130"
                  }
                ]
              }
            ]'  
  ```
> Response 200 (application/json)
Успешный запрос. Результат - массив JSON представлений созданных и обновленных Комплектов.
  
  ```json
  [
    {
      "meta": {
        "href": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/c21646cf-ee08-11e6-8af5-581e00000023",
        "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/metadata",
        "type": "bundle",
        "mediaType": "application/json"
      },
      "id": "c21646cf-ee08-11e6-8af5-581e00000023",
      "accountId": "badae4a0-ee05-11e6-8af5-581e00000001",
      "owner": {
        "meta": {
          "href": "http://online.moysklad.ru/api/remap/1.2/entity/employee/bb430a4e-ee05-11e6-8af5-581e0000002a",
          "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
          "type": "employee",
          "mediaType": "application/json"
        }
      },
      "shared": true,
      "group": {
        "meta": {
          "href": "http://online.moysklad.ru/api/remap/1.2/entity/group/bade121f-ee05-11e6-8af5-581e00000002",
          "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/group/metadata",
          "type": "group",
          "mediaType": "application/json"
        }
      },
      "updated": "2017-02-08 17:13:26",
      "name": "Комплект с товаром и еще одним товаром",
      "code": "00003",
      "externalCode": "iOzqxcTCiAK1-6-eAjVR12",
      "archived": false,
      "pathName": "",
      "discountProhibited": false,
      "uom": {
        "meta": {
          "href": "http://online.moysklad.ru/api/remap/1.2/entity/uom/19f1edc0-fc42-4001-94cb-c9ec9c62ec10",
          "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/uom/metadata",
          "type": "uom",
          "mediaType": "application/json"
        }
      },
      "images": {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/bundle/c21646cf-ee08-11e6-8af5-581e00000023/images",
            "type": "image",
            "mediaType": "application/json",
            "size": 0,
            "limit": 1000,
            "offset": 0
          }
      },  
      "minPrice": {
        "value": 500,
        "currency": {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/10772c12-36e7-11e7-8a7f-40d000000097",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
            "type": "currency",
            "mediaType": "application/json"
          }
        }
      },
      "salePrices": [
        {
          "value": 20,
          "currency": {
            "meta": {
              "href": "http://online.moysklad.ru/api/remap/1.2/entity/currency/bb724075-ee05-11e6-8af5-581e00000058",
              "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
              "type": "currency",
              "mediaType": "application/json"
            }
          },
          "priceType": {
            "meta": {
              "href": "https://online.moysklad.ru/api/remap/1.2/context/companysettings/pricetype/672559f1-cbf3-11e1-9eb9-889ffa6f49fd",
              "type": "pricetype",
              "mediaType": "application/json"
            },
            "id": "672559f1-cbf3-11e1-9eb9-889ffa6f49fd",
            "name": "Цена продажи",
            "externalCode": "cbcf493b-55bc-11d9-848a-00112f43529a"
          }
        }
      ],
      "weight": 0,
      "volume": 0,
      "trackingType": "NOT_TRACKED",
      "barcodes": [
        {
          "ean8": "20000000"
        },
        {
          "ean13": "2000000000000"
        },
        {
          "code128": "code128 barcode"
        },
        {
          "gtin": "00000000000130"
        }
      ],
      "useParentVat": true,
      "vatEnabled": false,
      "components": {
        "meta": {
          "href": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/c21646cf-ee08-11e6-8af5-581e00000023/components",
          "type": "bundlecomponent",
          "mediaType": "application/json",
          "size": 2,
          "limit": 1000,
          "offset": 0
        },
        "rows": [
          {
            "meta": {
              "href": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/c21646cf-ee08-11e6-8af5-581e00000023/components/9404273f-eeb6-11e6-5bed-427b0000000c",
              "type": "bundlecomponent",
              "mediaType": "application/json"
            },
            "id": "9404273f-eeb6-11e6-5bed-427b0000000c",
            "accountId": "903083d9-d973-11e6-5bed-427b00000001",
            "assortment": {
              "meta": {
                "href": "http://online.moysklad.ru/api/remap/1.2/entity/product/010afdea-ea40-11e6-5bed-427b000000b8",
                "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                "type": "product",
                "mediaType": "application/json"
              }
            },
            "quantity": 1
          },
          {
            "meta": {
              "href": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/c21646cf-ee08-11e6-8af5-581e00000023/components/9404273f-eeb6-11e6-5bed-427b0000000d",
              "type": "bundlecomponent",
              "mediaType": "application/json"
            },
            "id": "9404273f-eeb6-11e6-5bed-427b0000000d",
            "accountId": "903083d9-d973-11e6-5bed-427b00000001",
            "assortment": {
              "meta": {
                "href": "http://online.moysklad.ru/api/remap/1.2/entity/product/010afdea-ea40-11e6-5bed-427b000000b9",
                "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                "type": "product",
                "mediaType": "application/json"
              }
            },
            "quantity": 1
          }
        ]
      }
    },
    {
      "meta": {
        "href": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/c21646cf-ee08-11e6-8af5-581e00000023",
        "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/metadata",
        "type": "bundle",
        "mediaType": "application/json"
      },
      "id": "c21646cf-ee08-11e6-8af5-581e00000023",
      "accountId": "badae4a0-ee05-11e6-8af5-581e00000001",
      "owner": {
        "meta": {
          "href": "http://online.moysklad.ru/api/remap/1.2/entity/employee/bb430a4e-ee05-11e6-8af5-581e0000002a",
          "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
          "type": "employee",
          "mediaType": "application/json"
        }
      },
      "shared": true,
      "group": {
        "meta": {
          "href": "http://online.moysklad.ru/api/remap/1.2/entity/group/bade121f-ee05-11e6-8af5-581e00000002",
          "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/group/metadata",
          "type": "group",
          "mediaType": "application/json"
        }
      },
      "updated": "2017-02-08 17:13:26",
      "name": "Новое наименование",
      "code": "00003",
      "externalCode": "iOzqxcTCiAK1-6-eAjVR12",
      "archived": false,
      "pathName": "",
      "discountProhibited": false,
      "uom": {
        "meta": {
          "href": "http://online.moysklad.ru/api/remap/1.2/entity/uom/19f1edc0-fc42-4001-94cb-c9ec9c62ec10",
          "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/uom/metadata",
          "type": "uom",
          "mediaType": "application/json"
        }
      },
     "images": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/bundle/c21646cf-ee08-11e6-8af5-581e00000023/images",
          "type": "image",
          "mediaType": "application/json",
          "size": 0,
          "limit": 1000,
          "offset": 0
        }
      },      
      "minPrice": {
        "value": 500,
        "currency": {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/10772c12-36e7-11e7-8a7f-40d000000097",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
            "type": "currency",
            "mediaType": "application/json"
          }
        }
      },
      "salePrices": [
        {
          "value": 20,
          "currency": {
            "meta": {
              "href": "http://online.moysklad.ru/api/remap/1.2/entity/currency/bb724075-ee05-11e6-8af5-581e00000058",
              "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
              "type": "currency",
              "mediaType": "application/json"
            }
          },
          "priceType": {
            "meta": {
              "href": "https://online.moysklad.ru/api/remap/1.2/context/companysettings/pricetype/672559f1-cbf3-11e1-9eb9-889ffa6f49fd",
              "type": "pricetype",
              "mediaType": "application/json"
            },
            "id": "672559f1-cbf3-11e1-9eb9-889ffa6f49fd",
            "name": "Цена продажи",
            "externalCode": "cbcf493b-55bc-11d9-848a-00112f43529a"
          }
        }
      ],
      "weight": 0,
      "volume": 0,
      "trackingType": "NOT_TRACKED",
      "barcodes": [
        {
          "ean8": "20000000"
        },
        {
          "ean13": "2000000000000"
        },
        {
          "code128": "code128 barcode"
        },
        {
          "gtin": "00000000000130"
        }
      ],
      "useParentVat": true,
      "vatEnabled": false,
      "components": {
        "meta": {
          "href": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/c21646cf-ee08-11e6-8af5-581e00000023/components",
          "type": "bundlecomponent",
          "mediaType": "application/json",
          "size": 2,
          "limit": 1000,
          "offset": 0
        },
        "rows": [
          {
            "meta": {
              "href": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/c21646cf-ee08-11e6-8af5-581e00000023/components/9404273f-eeb6-11e6-5bed-427b0000000c",
              "type": "bundlecomponent",
              "mediaType": "application/json"
            },
            "id": "9404273f-eeb6-11e6-5bed-427b0000000c",
            "accountId": "903083d9-d973-11e6-5bed-427b00000001",
            "assortment": {
              "meta": {
                "href": "http://online.moysklad.ru/api/remap/1.2/entity/product/010afdea-ea40-11e6-5bed-427b000000b8",
                "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                "type": "product",
                "mediaType": "application/json"
              }
            },
            "quantity": 1
          },
          {
            "meta": {
              "href": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/c21646cf-ee08-11e6-8af5-581e00000023/components/9404273f-eeb6-11e6-5bed-427b0000000d",
              "type": "bundlecomponent",
              "mediaType": "application/json"
            },
            "id": "9404273f-eeb6-11e6-5bed-427b0000000d",
            "accountId": "903083d9-d973-11e6-5bed-427b00000001",
            "assortment": {
              "meta": {
                "href": "http://online.moysklad.ru/api/remap/1.2/entity/product/010afdea-ea40-11e6-5bed-427b000000b9",
                "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                "type": "product",
                "mediaType": "application/json"
              }
            },
            "quantity": 1
          }
        ]
      }
    }
  ]
  ```
  
### Метаданные Комплектов
#### Метаданные Комплектов
Запрос на получение метаданных Комплектов. Результат - объект JSON, включающий в себя:

| Название  | Тип | Описание                    | Свойство поля в запросе | Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**              |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные |&mdash;|да
|**attributes**        |Array(Object)|Коллекция всех существующих доп. полей Комплектов|&mdash;|да

Структура отдельного объекта, представляющего доп. поле подробно описана в разделе [Работа с дополнительными полями](../#mojsklad-json-api-obschie-swedeniq-rabota-s-dopolnitel-nymi-polqmi).

> Получить метаданные комплектов

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/bundle/metadata"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление доп. полей Комплектов.

```json
{
  "meta": {
    "href": "http://online.moysklad.ru/api/remap/1.2/entity/bundle",
    "mediaType": "application/json"
  },
  "attributes": [
    {
      "meta": {
        "href": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/metadata/attributes/5a374c72-ee21-11e6-8af5-581e00000003",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "5a374c72-ee21-11e6-8af5-581e00000003",
      "name": "доп строка",
      "type": "string",
      "required": false
    }
  ]
}
```

### Отдельное доп. поле

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Доп. поля.|

#### Отдельное доп. поле

> Запрос на получение информации по отдельному дополнительному полю.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/bundle/metadata/attributes/7944ef04-f831-11e5-7a69-971500188b19"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление отдельного доп. поля.

```json
{
  "meta": {
    "href": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/metadata/attributes/5a374c72-ee21-11e6-8af5-581e00000003",
    "type": "attributemetadata",
    "mediaType": "application/json"
  },
  "id": "5a374c72-ee21-11e6-8af5-581e00000003",
  "name": "доп строка",
  "type": "string",
  "required": false
}
```

### Комплект

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Комплекта.|

### Получить Комплект

> Запрос на получение комплекта с указанным id.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/bundle/7944ef04-f831-11e5-7a69-971500188b19"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление комплекта.

```json
{
  "meta": {
    "href": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/c21646cf-ee08-11e6-8af5-581e00000023",
    "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/metadata",
    "type": "bundle",
    "mediaType": "application/json"
  },
  "id": "c21646cf-ee08-11e6-8af5-581e00000023",
  "accountId": "badae4a0-ee05-11e6-8af5-581e00000001",
  "owner": {
    "meta": {
      "href": "http://online.moysklad.ru/api/remap/1.2/entity/employee/bb430a4e-ee05-11e6-8af5-581e0000002a",
      "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
      "type": "employee",
      "mediaType": "application/json"
    }
  },
  "shared": true,
  "group": {
    "meta": {
      "href": "http://online.moysklad.ru/api/remap/1.2/entity/group/bade121f-ee05-11e6-8af5-581e00000002",
      "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/group/metadata",
      "type": "group",
      "mediaType": "application/json"
    }
  },
  "updated": "2017-02-08 17:13:26",
  "name": "Комплект с товаром и услугой",
  "code": "00003",
  "externalCode": "iOzqxcTCiAK1-6-eAjVR12",
  "archived": false,
  "pathName": "",
  "discountProhibited": false,
  "uom": {
    "meta": {
      "href": "http://online.moysklad.ru/api/remap/1.2/entity/uom/19f1edc0-fc42-4001-94cb-c9ec9c62ec10",
      "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/uom/metadata",
      "type": "uom",
      "mediaType": "application/json"
    }
  },
  "images": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/bundle/c21646cf-ee08-11e6-8af5-581e00000023/images",
      "type": "image",
      "mediaType": "application/json",
      "size": 0,
      "limit": 1000,
      "offset": 0
    }
  },  
  "minPrice": {
    "value": 500,
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/10772c12-36e7-11e7-8a7f-40d000000097",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json"
      }
    }
  },
  "salePrices": [
    {
      "value": 0,
      "currency": {
        "meta": {
          "href": "http://online.moysklad.ru/api/remap/1.2/entity/currency/bb724075-ee05-11e6-8af5-581e00000058",
          "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
          "type": "currency",
          "mediaType": "application/json"
        }
      },
      "priceType": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/context/companysettings/pricetype/672559f1-cbf3-11e1-9eb9-889ffa6f49fd",
          "type": "pricetype",
          "mediaType": "application/json"
        },
        "id": "672559f1-cbf3-11e1-9eb9-889ffa6f49fd",
        "name": "Цена продажи",
        "externalCode": "cbcf493b-55bc-11d9-848a-00112f43529a"
      }
    }
  ],
  "weight": 0,
  "volume": 0,
  "trackingType": "NOT_TRACKED",
  "barcodes": [
    {
      "ean13": "2000000000039"
    }
  ],
  "useParentVat": true,
  "vatEnabled": false,
  "components": {
    "meta": {
      "href": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/c21646cf-ee08-11e6-8af5-581e00000023/components",
      "type": "bundlecomponent",
      "mediaType": "application/json",
      "size": 2,
      "limit": 1000,
      "offset": 0
    }
  }
}
```

### Изменить Комплект

Запрос на обновление существующего Комплекта.
Типы цен в ценах продаж, дополнительные поля и компоненты обновляются как элементы вложенных коллекций:

+ Если в текущем объекте у какого-то из доп. полей / типов цен / компонентов нет значения,
а в переданной коллекции оно есть - значение записывается в доп. поле / тип цены / компонент.
+ Если же у данного атрибута значение уже присутствует - оно перезаписывается на переданное.
+ Если у данного атрибута в составе объекта значение присутствует, однако оно отсутствует
в передаваемой в теле запроса коллекции (не передается совсем), то значение атрибута объекта не изменяется.

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Комплекта.|

> Пример запроса на обновление Комплекта
 
 ```shell
   curl -X PUT
     "https://online.moysklad.ru/api/remap/1.2/entity/bundle/7944ef04-f831-11e5-7a69-971500188b19"
     -H "Authorization: Basic <Credentials>"
     -H "Content-Type: application/json"
       -d '{
             "name": "Новое наименование",
             "barcodes": [
               {
                 "ean8": "20000000"
               },
               {
                 "ean13": "2000000000000"
               },
               {
                 "code128": "code128 barcode"
               },
               {
                 "gtin": "00000000000130"
               }
             ],
           }'  
 ```
 
>  Response 200 (application/json)
Успешный запрос. Результат - JSON представление обновленного Комплекта.
 
 ```json
{
  "meta": {
    "href": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/c21646cf-ee08-11e6-8af5-581e00000023",
    "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/metadata",
    "type": "bundle",
    "mediaType": "application/json"
  },
  "id": "c21646cf-ee08-11e6-8af5-581e00000023",
  "accountId": "badae4a0-ee05-11e6-8af5-581e00000001",
  "owner": {
    "meta": {
      "href": "http://online.moysklad.ru/api/remap/1.2/entity/employee/bb430a4e-ee05-11e6-8af5-581e0000002a",
      "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
      "type": "employee",
      "mediaType": "application/json"
    }
  },
  "shared": true,
  "group": {
    "meta": {
      "href": "http://online.moysklad.ru/api/remap/1.2/entity/group/bade121f-ee05-11e6-8af5-581e00000002",
      "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/group/metadata",
      "type": "group",
      "mediaType": "application/json"
    }
  },
  "updated": "2017-02-08 17:13:26",
  "name": "Новое наименование",
  "code": "00003",
  "externalCode": "iOzqxcTCiAK1-6-eAjVR12",
  "archived": false,
  "pathName": "",
  "discountProhibited": false,
  "uom": {
    "meta": {
      "href": "http://online.moysklad.ru/api/remap/1.2/entity/uom/19f1edc0-fc42-4001-94cb-c9ec9c62ec10",
      "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/uom/metadata",
      "type": "uom",
      "mediaType": "application/json"
    }
  },
  "images": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/bundle/c21646cf-ee08-11e6-8af5-581e00000023/images",
      "type": "image",
      "mediaType": "application/json",
      "size": 0,
      "limit": 1000,
      "offset": 0
    }
  },  
  "minPrice": {
    "value": 500,
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/10772c12-36e7-11e7-8a7f-40d000000097",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json"
      }
    }
  },
  "salePrices": [
    {
      "value": 20,
      "currency": {
        "meta": {
          "href": "http://online.moysklad.ru/api/remap/1.2/entity/currency/bb724075-ee05-11e6-8af5-581e00000058",
          "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
          "type": "currency",
          "mediaType": "application/json"
        }
      },
      "priceType": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/context/companysettings/pricetype/672559f1-cbf3-11e1-9eb9-889ffa6f49fd",
          "type": "pricetype",
          "mediaType": "application/json"
        },
        "id": "672559f1-cbf3-11e1-9eb9-889ffa6f49fd",
        "name": "Цена продажи",
        "externalCode": "cbcf493b-55bc-11d9-848a-00112f43529a"
      }
    }
  ],
  "weight": 0,
  "volume": 0,
  "trackingType": "NOT_TRACKED",
  "barcodes": [
    {
      "ean8": "20000000"
    },
    {
      "ean13": "2000000000000"
    },
    {
      "code128": "code128 barcode"
    },
    {
      "gtin": "00000000000130"
    }
  ],
  "useParentVat": true,
  "vatEnabled": false,
  "components": {
    "meta": {
      "href": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/c21646cf-ee08-11e6-8af5-581e00000023/components",
      "type": "bundlecomponent",
      "mediaType": "application/json",
      "size": 2,
      "limit": 1000,
      "offset": 0
    },
    "rows": [
      {
        "meta": {
          "href": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/c21646cf-ee08-11e6-8af5-581e00000023/components/9404273f-eeb6-11e6-5bed-427b0000000c",
          "type": "bundlecomponent",
          "mediaType": "application/json"
        },
        "id": "9404273f-eeb6-11e6-5bed-427b0000000c",
        "accountId": "903083d9-d973-11e6-5bed-427b00000001",
        "assortment": {
          "meta": {
            "href": "http://online.moysklad.ru/api/remap/1.2/entity/product/010afdea-ea40-11e6-5bed-427b000000b8",
            "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
            "type": "product",
            "mediaType": "application/json"
          }
        },
        "quantity": 1
      },
      {
        "meta": {
          "href": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/c21646cf-ee08-11e6-8af5-581e00000023/components/9404273f-eeb6-11e6-5bed-427b0000000d",
          "type": "bundlecomponent",
          "mediaType": "application/json"
        },
        "id": "9404273f-eeb6-11e6-5bed-427b0000000d",
        "accountId": "903083d9-d973-11e6-5bed-427b00000001",
        "assortment": {
          "meta": {
            "href": "http://online.moysklad.ru/api/remap/1.2/entity/product/010afdea-ea40-11e6-5bed-427b000000b9",
            "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
            "type": "product",
            "mediaType": "application/json"
          }
        },
        "quantity": 1
      }
    ]
  }
} 
 ``` 
  
### Удалить Комплект

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Комплекта.|

> Запрос на удаление Комплекта с указанным id.

```shell
curl -X DELETE
  "https://online.moysklad.ru/api/remap/1.2/entity/bundle/7944ef04-f831-11e5-7a69-971500188b19"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешное удаление Комплекта.

### Массовое удаление Комплектов

В теле запроса нужно передать массив, содержащий JSON метаданных Комплектов, которые вы хотите удалить.


> Запрос на массовое удаление Комплектов. 

```shell
curl -X POST
  "https://online.moysklad.ru/api/remap/1.2/entity/bundle/delete"
  -H "Authorization: Basic <Credentials>"
  -H "Content-Type: application/json"
  -d '[
        {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/bundle/7944ef04-f831-11e5-7a69-971500188b1",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/bundle/metadata",
            "type": "bundle",
            "mediaType": "application/json"
        },
        {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/bundle/7944ef04-f831-11e5-7a69-971500188b2",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/bundle/metadata",
            "type": "bundle",
            "mediaType": "application/json"
        }
      ]'
```        

> Успешный запрос. Результат - JSON информация об удалении Комплектов.

```json
[
  {
    "info":"Сущность 'bundle' с UUID: 7944ef04-f831-11e5-7a69-971500188b1 успешно удалена"
  },
  {
    "info":"Сущность 'bundle' с UUID: 7944ef04-f831-11e5-7a69-971500188b2 успешно удалена"
  }
]
```  

### Компоненты Комплекта

Отдельный ресурс для управления компонентами Комплекта.

### Получить компоненты Комплекта
Запрос на получение списка всех компонентов данного Комплекта.

| Название  | Тип | Описание                    |
| --------- |:----|:----------------------------|
**meta** |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные о выдаче,
**context** | [Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye) | Метаданные о сотруднике, выполнившем запрос.
**rows** |Array(Object)|Массив JSON объектов, представляющих собой Комплекта.

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Комплекта.|
|**limit** |  `number` (optional) **Default: 1000** *Example: 1000* Максимальное количество сущностей для извлечения.`Допустимые значения 1 - 1000`.|
|**offset** |  `number` (optional) **Default: 0** *Example: 40* Отступ в выдаваемом списке сущностей.|

> Получить компоненты Комплекса

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/bundle/7944ef04-f831-11e5-7a69-971500188b19/components"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление списка компонентов отдельного Комплекта.

```json
{
  "context": {
    "employee": {
      "meta": {
        "href": "http://online.moysklad.ru/api/remap/1.2/context/employee",
        "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
        "type": "employee",
        "mediaType": "application/json"
      }
    }
  },
  "meta": {
    "href": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/c21646cf-ee08-11e6-8af5-581e00000023/components",
    "type": "bundlecomponent",
    "mediaType": "application/json",
    "size": 2,
    "limit": 1000,
    "offset": 0
  },
  "rows": [
    {
      "meta": {
        "href": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/c21646cf-ee08-11e6-8af5-581e00000023/components/c21661f2-ee08-11e6-8af5-581e00000026",
        "type": "bundlecomponent",
        "mediaType": "application/json"
      },
      "id": "c21661f2-ee08-11e6-8af5-581e00000026",
      "accountId": "badae4a0-ee05-11e6-8af5-581e00000001",
      "assortment": {
        "meta": {
          "href": "http://online.moysklad.ru/api/remap/1.2/entity/service/b3d8d132-ee08-11e6-8af5-581e00000013",
          "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/service/metadata",
          "type": "service",
          "mediaType": "application/json"
        }
      },
      "quantity": 1
    },
    {
      "meta": {
        "href": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/c21646cf-ee08-11e6-8af5-581e00000023/components/c21668eb-ee08-11e6-8af5-581e00000027",
        "type": "bundlecomponent",
        "mediaType": "application/json"
      },
      "id": "c21668eb-ee08-11e6-8af5-581e00000027",
      "accountId": "badae4a0-ee05-11e6-8af5-581e00000001",
      "assortment": {
        "meta": {
          "href": "http://online.moysklad.ru/api/remap/1.2/entity/product/b01e8dfd-ee08-11e6-8af5-581e00000005",
          "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
          "type": "product",
          "mediaType": "application/json"
        }
      },
      "quantity": 1
    }
  ]
}
```

### Добавить компонент Комплекта

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Комплекта.|

> Запрос на добавление компонента Комплекта.

```shell
  curl -X POST
    "https://online.moysklad.ru/api/remap/1.2/entity/bundle/7944ef04-f831-11e5-7a69-971500188b19/components"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "assortment": {
              "meta": {
                "href": "http://online.moysklad.ru/api/remap/1.2/entity/product/010afdea-ea40-11e6-5bed-427b000000b8",
                "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                "type": "product",
                "mediaType": "application/json"
              }
            },
            "quantity": 1
          }'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление добавленного компонента.

```json
{
  "meta": {
    "href": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/c21646cf-ee08-11e6-8af5-581e00000023/components/9404273f-eeb6-11e6-5bed-427b0000000c",
    "type": "bundlecomponent",
    "mediaType": "application/json"
  },
  "id": "9404273f-eeb6-11e6-5bed-427b0000000c",
  "accountId": "903083d9-d973-11e6-5bed-427b00000001",
  "assortment": {
    "meta": {
      "href": "http://online.moysklad.ru/api/remap/1.2/entity/product/010afdea-ea40-11e6-5bed-427b000000b8",
      "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
      "type": "product",
      "mediaType": "application/json"
    }
  },
  "quantity": 1
}
```


### Компонент Комплекта

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Комплекта.|
|**id** |  `string` (required) *Example: 34f6344f-015e-11e6-9464-e4de0000006c* id компонента Комплекта.|

### Получить компонент

> Запрос на получение отдельного компонента Комплекта с указанным id.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/bundle/7944ef04-f831-11e5-7a69-971500188b19/components/34f6344f-015e-11e6-9464-e4de0000006c"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление отдельного компонента Комплекта.

```json
{
  "meta": {
    "href": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/c21646cf-ee08-11e6-8af5-581e00000023/components/9404273f-eeb6-11e6-5bed-427b0000000c",
    "type": "bundlecomponent",
    "mediaType": "application/json"
  },
  "id": "9404273f-eeb6-11e6-5bed-427b0000000c",
  "accountId": "903083d9-d973-11e6-5bed-427b00000001",
  "assortment": {
    "meta": {
      "href": "http://online.moysklad.ru/api/remap/1.2/entity/product/010afdea-ea40-11e6-5bed-427b000000b8",
      "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
      "type": "product",
      "mediaType": "application/json"
    }
  },
  "quantity": 1
}
```

### Изменить компонент

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Комплекта.|
|**id** |  `string` (required) *Example: 34f6344f-015e-11e6-9464-e4de0000006c* id компонента Комплекта.|

Запрос на изменение отдельного компонента Комплекта с указанным id.

> Пример запроса на изменение компонента Комплекта

```shell
  curl -X PUT
    "https://online.moysklad.ru/api/remap/1.2/entity/bundle/7944ef04-f831-11e5-7a69-971500188b19/components/34f6344f-015e-11e6-9464-e4de0000006c
"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "quantity": 50
          }'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление отдельного компонента Комплекта.

```json
{
  "meta": {
    "href": "http://online.moysklad.ru/api/remap/1.2/entity/bundle/c21646cf-ee08-11e6-8af5-581e00000023/components/9404273f-eeb6-11e6-5bed-427b0000000c",
    "type": "bundlecomponent",
    "mediaType": "application/json"
  },
  "id": "9404273f-eeb6-11e6-5bed-427b0000000c",
  "accountId": "903083d9-d973-11e6-5bed-427b00000001",
  "assortment": {
    "meta": {
      "href": "http://online.moysklad.ru/api/remap/1.2/entity/product/010afdea-ea40-11e6-5bed-427b000000b8",
      "metadataHref": "http://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
      "type": "product",
      "mediaType": "application/json"
    }
  },
  "quantity": 50
}
```

### Удалить компонент

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Комплекта.|
|**id** |  `string` (required) *Example: 34f6344f-015e-11e6-9464-e4de0000006c* id компонента Комплекта.|

> Запрос на удаление отдельного компонента Комплекта с указанным id.

```shell
curl -X DELETE
  "https://online.moysklad.ru/api/remap/1.2/entity/bundle/7944ef04-f831-11e5-7a69-971500188b19/components/34f6344f-015e-11e6-9464-e4de0000006c"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешное удаление компонента Комплекта.
