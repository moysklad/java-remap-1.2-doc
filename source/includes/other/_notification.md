# Уведомления

## Лента уведомлений
### Общие атрибуты уведомлений

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта. Содержит тип конкретного уведомления|&mdash;да
|**id**                 |UUID|ID Уведомления|Только для чтения|да
|**accountId**          |UUID| ID учетной записи|Только для чтения|да
|**created**            |DateTime|Дата и время формирования Уведомления|Только для чтения|да
|**read**        |Boolean|Признак того, было ли Уведомление прочитано|&mdash;|да
|**title**       |String(255)|Краткий текст уведомления|Только для чтения| да
|**description**       |String(4096)|Описание уведомления|Только для чтения| да

### Получить ленту Уведомлений
Запрос на получение ленты Уведомлений.
Результат: Объект JSON, включающий в себя поля:

| Название  | Тип | Описание                    |
| --------- |:----|:----------------------------|
**meta** |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные о выдаче,
**context** | [Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye) | Метаданные о сотруднике, выполнившем запрос.
**rows** |Array(Object)|Массив JSON объектов, представляющих собой [Уведомления](../other/#uwedomleniq-lenta-uwedomlenij).

**Параметры**

| Параметр                | Описание  |
| ------------------------------ |:---------------------------|
|**limit** |  `number` (optional) **Default: 1000** *Example: 1000* Максимальное количество сущностей для извлечения.`Допустимые значения 1 - 1000`.|
|**offset** |  `number` (optional) **Default: 0** *Example: 40* Отступ в выдаваемом списке сущностей.|

> Получить ленту уведомлений

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/notification"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление списка Уведомлений.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/notification",
    "type": "notification",
    "mediaType": "application/json",
    "size": 3,
    "limit": 1000,
    "offset": 0
  },
  "rows": [
    {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/notification/32f118d3-5b8f-11e9-9bea-3ff700000070",
      "type": "NotificationGoodCountTooLow",
      "mediaType": "application/json"
    },
    "id": "32f118d3-5b8f-11e9-9bea-3ff700000070",
    "accountId": "45b76d0a-5aa2-11e9-727d-307300000002",
    "created": "2019-04-10 15:50:20.271",
    "read": true,
    "title": "Заканчивается товар Картофель (да)",
    "description": "Остаток ниже 1",
    "good": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/0daf8e9a-5b7a-11e9-727d-307300000007",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
        "type": "product",
        "mediaType": "application/json"
      },
      "id": "0daf8e9a-5b7a-11e9-727d-307300000007",
      "name": "Картофель (да)"
    },
    "actualBalance": 0,
    "minimumBalance": 1
    },
    {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/notification/0f423542-5b7a-11e9-9bea-3ff70000000f",
      "type": "NotificationImportCompleted",
      "mediaType": "application/json"
    },
    "id": "0f423542-5b7a-11e9-9bea-3ff70000000f",
    "accountId": "45b76d0a-5aa2-11e9-727d-307300000002",
    "created": "2019-04-10 13:19:01.123",
    "read": true,
    "title": "Импорт завершен",
    "description": "Товары и остатки (Excel). Оприходование 00002 создано. Обработано 7 строк, создано 7 элементов, обновлено 0 элементов",
    "message": "Обработано 7 строк, создано 7 элементов, обновлено 0 элементов",
    "taskType": "importer_good",
    "taskState": "completed",
    "createdDocumentName": "00002"
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/notification/a805beb5-5adf-11e9-9bea-3ff700000025",
        "type": "NotificationTaskChanged",
        "mediaType": "application/json"
      },
      "id": "a805beb5-5adf-11e9-9bea-3ff700000025",
      "accountId": "45b76d0a-5aa2-11e9-727d-307300000002",
      "created": "2019-04-09 18:53:45.314",
      "read": true,
      "title": "Задача изменена: Новое описание задачи",
      "description": "admin изменил задачу",
      "performedBy": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/188cb787-5aa5-11e9-727d-30730000009c",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
          "type": "employee",
          "mediaType": "application/json"
        },
        "id": "188cb787-5aa5-11e9-727d-30730000009c",
        "name": "admin"
      },
      "task": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/task/14ac66b6-5add-11e9-727d-30730000002f",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/task/metadata",
          "type": "task",
          "mediaType": "application/json"
        },
        "id": "14ac66b6-5add-11e9-727d-30730000002f",
        "name": "Новое описание задачи",
        "deadline": "2019-04-02 18:53:00.000"
      },
      "diff": {
        "description": {
          "oldValue": "Старое описание задачи",
          "newValue": "Новое описание задачи"
        },
        "deadline": {
          "newValue": "2019-04-02 18:53:00.000"
        }
      }
    }
  ]
}
```

## Уведомление

### Получить Уведомление

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Уведомления.|

> Запрос на получение Уведомления с указанным id.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/notification/7944ef04-f831-11e5-7a69-971500188b19"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление Уведомления.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/notification/bcd815b9-56ca-11e9-c0a8-100b00000001",
    "type": "NotificationTaskAssigned",
    "mediaType": "application/json"
  },
  "id": "bcd815b9-56ca-11e9-c0a8-100b00000001",
  "accountId": "c45c23d5-5640-11e9-c0a8-100a00000001",
  "created": "2019-04-04 14:13:56.000",
  "read": false,
  "title": "Новая задача: Задача",
  "description": "Администратор назначил вам задачу Задача",
  "performedBy": {
    "id": "c461170f-5640-11e9-c0a8-100a00000003",
    "name": "Администратор"
  },
  "task": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/task/8413bfc3-56ca-11e9-c0a8-100a00000000",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/task/metadata",
      "type": "task",
      "mediaType": "application/json"
    },
    "id": "8413bfc3-56ca-11e9-c0a8-100a00000000",
    "name": "Задача"
  }
}
```

### Удалить Уведомление
Запрос на удаление Уведомления. Возможно удаление только Уведомлений текущего пользователя.

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Уведомления.|

> Запрос на удаление Уведомления с указанным id.

```shell
curl -X DELETE
  "https://online.moysklad.ru/api/remap/1.2/notification/7944ef04-f831-11e5-7a69-971500188b19"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешное удаление Уведомления.


### Отметить Уведомление как прочитанное
Отметить конкретное уведомление, как прочитанное. Можно отмечать только Уведомления текущего пользователя.

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Уведомления.|

> Отметить конкретное уведомление, как прочитанное.

```shell
curl -X PUT
  "https://online.moysklad.ru/api/remap/1.2/notification/7944ef04-f831-11e5-7a69-971500188b19/markasread"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешное проставление признака "прочитано".

### Отметить все Уведомления как прочитанные
Отметить все Уведомления текущего пользователя как прочитанные.

> Отметить все Уведомления текущего пользователя как прочитанные

```shell
curl -X PUT
  "https://online.moysklad.ru/api/remap/1.2/notification/markasreadall"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешное проставление признака "прочитано" всем непрочитанным Уведомлениям.

## Типы уведомлений
### Форматы полей
#### Формат измененного поля
Формат измененного поля содержит в себе старое и новое значение:

|**oldValue**       |String(255)|Значение атрибута до удаления|Только для чтения|да
|**newValue**       |String(255)|Значение атрибута после обновления|Только для чтения|да

Формат oldValue и newValue совпадает с форматом поля, изменение которого отображается. Одно из полей может быть не заполнено.

#### Возможные значения типа экспорта
+ **export_csv_good**
+ **export_csv_agent**
+ **export_ms_xml**
+ **export_1c_v2_xml**
+ **export_unisender**
+ **export_1c_v3_xml**
+ **export_subscribepro**
+ **export_1c_client_bank**
+ **export_alfa_payments**
+ **export_tochka_payments**
+ **export_modulbank_payments**
+ **export_1c_enterprise_data**
+ **export_tinkoff_payments**
+ **export_good**
+ **export_custom_entity**

#### Возможные значения типа импорта
+ **importer_csv**
+ **importer_yml**
+ **importer_csv_agent**
+ **importer_csv_customerorder**
+ **importer_csv_purchaseorder**
+ **importer_csv_pricelist**
+ **importer_ms_xml**
+ **importer_1c_client_bank**
+ **import_alfa_payments**
+ **import_alfa_payments_request**
+ **import_alfa_payments_save**
+ **import_tochka_payments**
+ **import_modulbank_payments**
+ **import_tochka_payments_save**
+ **import_modulbank_payments_save**
+ **import_tinkoff_payments**
+ **import_tinkoff_payments_save**
+ **importer_good**
+ **importer_good_in_doc**
+ **import_edo_supply**
+ **import_union_company**
+ **import_sberbank_payments_request**
+ **import_sberbank_payments_save**
+ **import_update_vat_to_20_percents**
+ **import_custom_entity**


### Сводная таблица типов уведомлений
| Тип уведомления                     | Группа               | О чем уведомление            |
|-------------------------------------|----------------------|-------------------------------|
| **NotificationOrderNew**		            | Заказ покупателя   	| Новый заказа покупателя |
| **NotificationOrderOverdue**		    | Заказ покупателя		| Просрочен заказ |
| **NotificationInvoiceOutOverdue**		| Счет		            | Просрочен счёт, который не оплатил или не полностью оплатил покупатель |
| **NotificationGoodCountTooLow**		    | Остатки	        	| Снижение количества товара до неснижаемого остатка |
| **NotificationTaskAssigned**	    	| Задача	        	| Задача назначена |
| **NotificationTaskUnassigned**	    	| Задача		        | Задача снята |
| **NotificationTaskOverdue**		        | Задача		        | Задача просрочена |
| **NotificationTaskCompleted**	        | Задача		        | Задача выполнена |
| **NotificationTaskReopened**	    	| Задача		        | Задача переоткрыта |
| **NotificationTaskNewComment**		    | Задача	        	| У задачи появился новый комментарий |
| **NotificationTaskChanged**	    	    | Задача	        	| Задача поменялась |
| **NotificationTaskDeleted**		        | Задача	        	| Задача удалена |
| **NotificationTaskCommentDeleted**	    | Задача	        	| Комментарий у задачи был удален |
| **NotificationTaskCommentChanged**	    | Задача	        	| Комментарий у задачи был изменен |
| **NotificationImportCompleted**		    | Обмен данными	    	| Импорт выполнен |
| **NotificationExportCompleted**		    | Обмен данными	    	| Экспорт выполнен |
| **NotificationSubscribeExpired**        | Биллинг               | Окончание подписки |
| **NotificationSubscribeTermsExpired**   | Биллинг               | Истекают условия подписки |
| **NotificationRetailShiftOpened**       | Розничная торговля    | Открыта смена |
| **NotificationRetailShiftClosed**       | Розничная торговля    | Закрыта смена |
| **NotificationScript**       | Сценарии    | Уведомление из сценария |
| **FacebookTokenExpirationNotification** | Интернет-магазины     | О скором окончании действия доступа к аккаунту Facebook |

## Подробное описание типов уведомлений

### Завершение экспорта
#### Тип уведомления
NotificationExportCompleted - завершение экспорта
#### Атрибуты уведомления

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта|Необходимое при создании|да
|**id**                 |UUID|ID Уведомления|Необходимое при создании|да
|**accountId**          |UUID| ID учетной записи|Необходимое при создании|да
|**created**            |DateTime|Дата и время формирования Уведомления|Необходимое при создании|да
|**read**        |Boolean|Признак того, было ли Уведомление прочитано|Необходимое при создании|да
|**title**       |String(255)|Краткий текст уведомления|Необходимое при создании| да
|**description**       |String(4096)|Описание уведомления|Необходимое при создании| да
|**message**      |String(255)|Сообщение о завершении экспорта|&mdash;|нет
|**errorMessage**      |String(255)|Сообщение об ошибке|&mdash;|нет
|**createdDocumentName**      |String(255)|Имя экспортированного документа|&mdash;|нет
|**taskType**                 |Object|[Тип экспорта](../other/#uwedomleniq-tipy-uwedomlenij-formaty-polej-vozmozhnye-znacheniq-tipa-axporta)|Необходимое при создании|да
|**taskState**                 |Object|Статус завершения. Может принимать значения `completed`, `interrupted`, `interrupted_by_user`, `interrupted_by_timeout`, `interrupted_by_system`|Необходимое при создании|да

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id**  |  `string` (required) *Example: 02950e3c-35f2-11e9-9ff4-34e8000799c0* id Уведомления.|

> Запрос на получение Уведомления с указанным id.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/notification/02950e3c-35f2-11e9-9ff4-34e8000799c0"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление Уведомления.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/notification/02950e3c-35f2-11e9-9ff4-34e8000799c0",
    "type": "NotificationExportCompleted",
    "mediaType": "application/json"
  },
  "id": "02950e3c-35f2-11e9-9ff4-34e8000799c0",
  "accountId": "45eb22e0-0e7b-11e2-1c31-3c4a92f3a0a7",
  "created": "2019-02-21 19:01:55.277",
  "read": true,
  "title": "Экспорт завершен",
  "description": "Экспорт товаров (Excel). Экспортировано 43465 товаров и 2080 модификаций",
  "message": "Экспортировано 43465 товаров и 2080 модификаций",
  "taskType": "export_good",
  "taskState": "completed"
}
```

### Завершение импорта
#### Тип уведомления
NotificationImportCompleted - завершение импорта
#### Атрибуты уведомления

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта|Необходимое при создании|да
|**id**                 |UUID|ID Уведомления|Необходимое при создании|да
|**accountId**          |UUID| ID учетной записи|Необходимое при создании|да
|**created**            |DateTime|Дата и время формирования Уведомления|Необходимое при создании|да
|**read**        |Boolean|Признак того, было ли Уведомление прочитано|Необходимое при создании|да
|**title**       |String(255)|Краткий текст уведомления|Необходимое при создании| да
|**description**       |String(4096)|Описание уведомления|Необходимое при создании| да
|**message**      |String(255)|Сообщение о завершении экспорта|&mdash;|нет
|**errorMessage**      |String(255)|Сообщение об ошибке|&mdash;|нет
|**createdDocumentName**      |String(255)|Имя экспортированного документа|&mdash;|нет
|**taskType**                 |Object|[Тип экспорта](../other/#uwedomleniq-tipy-uwedomlenij-formaty-polej-vozmozhnye-znacheniq-tipa-axporta)|Необходимое при создании|да
|**taskState**                 |Object|Статус завершения. Может принимать значения `completed`, `interrupted`, `interrupted_by_user`, `interrupted_by_timeout`, `interrupted_by_system`|Необходимое при создании|да

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 02950e31-35f2-11e9-9ff4-34e8000799c0* id Уведомления.|

> Запрос на получение Уведомления с указанным id.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/notification/02950e31-35f2-11e9-9ff4-34e8000799c0"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление Уведомления.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/notification/02950e31-35f2-11e9-9ff4-34e8000799c0",
    "type": "NotificationImportCompleted",
    "mediaType": "application/json"
  },
  "id": "02950e31-35f2-11e9-9ff4-34e8000799c0",
  "accountId": "45eb22e0-0e7b-11e2-1c31-3c4a92f3a0a7",
  "created": "2019-02-21 19:01:55.277",
  "read": true,
  "title": "Импорт завершен",
  "description": "Импорт контрагентов (Excel). Обработано 3 строки, создано 0 контрагентов, обновлено 0 контрагентов.",
  "message": "Обработано 3 строки, создано 0 контрагентов, обновлено 0 контрагентов.",
  "taskType": "importer_csv_agent",
  "taskState": "completed"
}
```

### Снижение остатка товара ниже неснижаемого
#### Тип уведомления
NotificationGoodCountTooLow - снижение остатка товара ниже неснижаемого
#### Атрибуты уведомления

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта|Необходимое при создании|да
|**id**                 |UUID|ID Уведомления|Необходимое при создании|да
|**accountId**          |UUID| ID учетной записи|Необходимое при создании|да
|**created**            |DateTime|Дата и время формирования Уведомления|Необходимое при создании|да
|**read**        |Boolean|Признак того, было ли Уведомление прочитано|Необходимое при создании|да
|**title**       |String(255)|Краткий текст уведомления|Необходимое при создании| да
|**description**       |String(4096)|Описание уведомления|Необходимое при создании| да
|**actualBalance**                |Int|Остаток товара|Необходимое при создании|да
|**minimumBalance**                |Int|Неснижаемый остаток товара|Необходимое при создании|да
|**good**              |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные товара|Необходимое при создании|да

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 9338c8bd-56e5-11e9-c0a8-100b00000023* id Уведомления.|

> Запрос на получение Уведомления с указанным id.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/notification/9338c8bd-56e5-11e9-c0a8-100b00000023"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление Уведомления.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/notification/9338c8bd-56e5-11e9-c0a8-100b00000023",
    "type": "NotificationGoodCountTooLow",
    "mediaType": "application/json"
  },
  "id": "9338c8bd-56e5-11e9-c0a8-100b00000023",
  "accountId": "c45c23d5-5640-11e9-c0a8-100a00000001",
  "created": "2019-04-04 17:26:02.000",
  "read": false,
  "title": "Заканчивается товар 1",
  "description": "Остаток ниже 200",
  "good": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/bdca925e-56e1-11e9-c0a8-100a00000016",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
      "type": "product",
      "mediaType": "application/json"
    },
    "id": "bdca925e-56e1-11e9-c0a8-100a00000016",
    "name": "1"
  },
  "actualBalance": 180.0,
  "minimumBalance": 200.0
}
```

### Просрочен счет покупателя
#### Тип уведомления
NotificationInvoiceOutOverdue - просрочен счет покупателя
#### Атрибуты уведомления

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта|Необходимое при создании|да
|**id**                 |UUID|ID Уведомления|Необходимое при создании|да
|**accountId**          |UUID| ID учетной записи|Необходимое при создании|да
|**created**            |DateTime|Дата и время формирования Уведомления|Необходимое при создании|да
|**read**        |Boolean|Признак того, было ли Уведомление прочитано|Необходимое при создании|да
|**title**       |String(255)|Краткий текст уведомления|Необходимое при создании| да
|**description**       |String(4096)|Описание уведомления|Необходимое при создании| да
|**invoice**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные счета|Необходимое при создании|да
|**paymentPlannedMoment**           |DateTime|Запланированная дата оплаты|&mdash;|да
|**sum**           |Int|Сумма счета|&mdash;|да
|**agentName*           |String(255)|Имя контрагента|&mdash;|да

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 572d1dd9-56fc-11e9-c0a8-100b00000006* id Уведомления.|

> Запрос на получение Уведомления с указанным id.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/notification/572d1dd9-56fc-11e9-c0a8-100b00000006"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление Уведомления.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/notification/572d1dd9-56fc-11e9-c0a8-100b00000006",
    "type": "NotificationInvoiceOutOverdue",
    "mediaType": "application/json"
  },
  "id": "572d1dd9-56fc-11e9-c0a8-100b00000006",
  "accountId": "c45c23d5-5640-11e9-c0a8-100a00000001",
  "created": "2019-04-04 20:09:00.000",
  "read": false,
  "title": "Счет покупателю №00003 просрочен",
  "description": "Дата оплаты: 01.04.2019 20:08. Сумма: 500,00. Покупатель: Розничный покупатель.",
  "invoice": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/invoiceout/571b1ac4-56fc-11e9-c0a8-100e0000002b",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/invoiceout/metadata",
      "type": "invoiceout",
      "mediaType": "application/json"
    },
    "id": "571b1ac4-56fc-11e9-c0a8-100e0000002b",
    "name": "00003",
    "paymentPlannedMoment": "2019-04-01 20:08:00.000",
    "sum": 50000,
    "customerName": "Розничный покупатель"
  }
}
```

### Новый заказ
#### Тип уведомления
NotificationOrderNew - новый заказ
#### Атрибуты уведомления

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта|Необходимое при создании|да
|**id**                 |UUID|ID Уведомления|Необходимое при создании|да
|**accountId**          |UUID| ID учетной записи|Необходимое при создании|да
|**created**            |DateTime|Дата и время формирования Уведомления|Необходимое при создании|да
|**read**        |Boolean|Признак того, было ли Уведомление прочитано|Необходимое при создании|да
|**title**       |String(255)|Краткий текст уведомления|Необходимое при создании| да
|**description**       |String(4096)|Описание уведомления|Необходимое при создании| да
|**order**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные заказа|Необходимое при создании|да
|**deliveryPlannedMoment**           |DateTime|Планируемое время отгрузки|&mdash;|да
|**sum**           |Int|Сумма счета|&mdash;|да
|**agentName*           |String(255)|Имя контрагента|&mdash;|да

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: c6082a9e-56e1-11e9-c0a8-100b00000011* id Уведомления.|

> Запрос на получение Уведомления с указанным id.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/notification/c6082a9e-56e1-11e9-c0a8-100b00000011"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление Уведомления.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/notification/c6082a9e-56e1-11e9-c0a8-100b00000011",
    "type": "NotificationOrderNew",
    "mediaType": "application/json"
  },
  "id": "c6082a9e-56e1-11e9-c0a8-100b00000011",
  "accountId": "c45c23d5-5640-11e9-c0a8-100a00000001",
  "created": "2019-04-04 16:58:50.000",
  "read": false,
  "title": "Новый заказ покупателя № 00001",
  "description": "Сумма: 499.99. Покупатель: Розничный покупатель.",
  "order": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/customerorder/c5ab5d93-56e1-11e9-c0a8-100a0000001d",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/customerorder/metadata",
      "type": "customerorder",
      "mediaType": "application/json"
    },
    "id": "c5ab5d93-56e1-11e9-c0a8-100a0000001d",
    "name": "00001",
    "sum": 49999,
    "agentName": "Розничный покупатель"
  }
}
```

### Просроченный заказ
#### Тип уведомления
NotificationOrderOverdue - просроченный заказ
#### Атрибуты уведомления

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта|Необходимое при создании|да
|**id**                 |UUID|ID Уведомления|Необходимое при создании|да
|**accountId**          |UUID| ID учетной записи|Необходимое при создании|да
|**created**            |DateTime|Дата и время формирования Уведомления|Необходимое при создании|да
|**read**        |Boolean|Признак того, было ли Уведомление прочитано|Необходимое при создании|да
|**title**       |String(255)|Краткий текст уведомления|Необходимое при создании| да
|**description**       |String(4096)|Описание уведомления|Необходимое при создании| да
|**order**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные заказа|Необходимое при создании|да
|**deliveryPlannedMoment**           |DateTime|Планируемое время отгрузки|&mdash;|да
|**sum**           |Int|Сумма счета|&mdash;|да
|**agentName*           |String(255)|Имя контрагента|&mdash;|да

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: c6082a9e-56e1-11e9-c0a8-100b00000011* id Уведомления.|

> Запрос на получение Уведомления с указанным id.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/notification/c6082a9e-56e1-11e9-c0a8-100b00000011"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление Уведомления.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/notification/c6082a9e-56e1-11e9-c0a8-100b00000011",
    "type": "NotificationOrderOverdue",
    "mediaType": "application/json"
  },
  "id": "c6082a9e-56e1-11e9-c0a8-100b00000011",
  "accountId": "c45c23d5-5640-11e9-c0a8-100a00000001",
  "created": "2019-04-04 16:58:50.000",
  "read": false,
  "title": "Просрочен заказ покупателя № 00001",
  "description": "Просрочен заказ покупателя № 00001 Сумма: 300.00. Покупатель: Розничный покупатель.",
  "order": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/customerorder/c5ab5d93-56e1-11e9-c0a8-100a0000001d",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/customerorder/metadata",
      "type": "customerorder",
      "mediaType": "application/json"
    },
    "id": "c5ab5d93-56e1-11e9-c0a8-100a0000001d",
    "name": "00001",
    "sum": 30000,
    "agentName": "Розничный покупатель"
  }
}
```


### Окончание подписки
#### Тип уведомления
NotificationSubscribeExpired - окончание подписки
#### Атрибуты уведомления

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта|Необходимое при создании|да
|**id**                 |UUID|ID Уведомления|Необходимое при создании|да
|**accountId**          |UUID| ID учетной записи|Необходимое при создании|да
|**created**            |DateTime|Дата и время формирования Уведомления|Необходимое при создании|да
|**read**        |Boolean|Признак того, было ли Уведомление прочитано|Необходимое при создании|да
|**title**       |String(255)|Краткий текст уведомления|Необходимое при создании| да
|**description**       |String(4096)|Описание уведомления|Необходимое при создании| да

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: c2582a9e-56e1-11e9-c0a8-100b00000123* id Уведомления.|

> Запрос на получение Уведомления с указанным id.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/notification/c2582a9e-56e1-11e9-c0a8-100b00000123"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление Уведомления.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/notification/c2582a9e-56e1-11e9-c0a8-100b00000123",
    "type": "NotificationOrderOverdue",
    "mediaType": "application/json"
  },
  "id": "c2582a9e-56e1-11e9-c0a8-100b00000123",
  "accountId": "c45c23d5-5640-11e9-c0a8-100a00000001",
  "created": "2019-04-04 16:58:50.000",
  "read": false,
  "title": "Окончание подписки",
  "description": "Подписка на аккаунте AccountName окончена. Вы по-прежнему можете работать, используя бесплатный тарифный план. Подписка возобновится при пополнении баланса."
}
```

### Условия подписки истекают
#### Тип уведомления
NotificationSubscribeTermsExpired - условия подписки истекают
#### Атрибуты 

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта|Необходимое при создании|да
|**id**                 |UUID|ID Уведомления|Необходимое при создании|да
|**accountId**          |UUID| ID учетной записи|Необходимое при создании|да
|**created**            |DateTime|Дата и время формирования Уведомления|Необходимое при создании|да
|**read**        |Boolean|Признак того, было ли Уведомление прочитано|Необходимое при создании|да
|**title**       |String(255)|Краткий текст уведомления|Необходимое при создании| да
|**description**       |String(4096)|Описание уведомления|Необходимое при создании| да
|**daysLeft**                 |Int|Количество оставшихся дней подписки|Необходимое при создании|да

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: c2582a9e-56e1-11e9-c0a8-100b00000125* id Уведомления.|

> Запрос на получение Уведомления с указанным id.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/notification/c2582a9e-56e1-11e9-c0a8-100b00000125"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление Уведомления.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/notification/c2582a9e-56e1-11e9-c0a8-100b00000125",
    "type": "NotificationOrderOverdue",
    "mediaType": "application/json"
  },
  "id": "c2582a9e-56e1-11e9-c0a8-100b00000125",
  "accountId": "c45c23d5-5640-11e9-c0a8-100a00000001",
  "created": "2019-04-04 16:58:50.000",
  "read": false,
  "title": "До окончания подписки 5 дней",
  "description": "До окончания подписки на аккаунте AccountName осталось 3 дней. Рекомендуем заранее пополнить баланс.",
  "daysLeft": 5
}
```

### Задача назначена
#### Тип уведомления
NotificationTaskAssigned - задача назначена
#### Атрибуты уведомления

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта|Необходимое при создании|да
|**id**                 |UUID|ID Уведомления|Необходимое при создании|да
|**accountId**          |UUID| ID учетной записи|Необходимое при создании|да
|**created**            |DateTime|Дата и время формирования Уведомления|Необходимое при создании|да
|**read**        |Boolean|Признак того, было ли Уведомление прочитано|Необходимое при создании|да
|**title**       |String(255)|Краткий текст уведомления|Необходимое при создании| да
|**description**       |String(4096)|Описание уведомления|Необходимое при создании| да
|**performedBy**                 |Object|Сотрудник, выполнивший изменение. [Подробнее тут](../dictionaries/#suschnosti-kontragent-kontragenty-attributy-suschnosti-adres)|Необходимое при создании|да
|**task**                 |Object|Задача|Необходимое при создании. [Подробнее тут](../dictionaries/#suschnosti-kontragent-kontragenty-attributy-suschnosti-adres)|да

#### Атрибуты вложенных сущностей
##### Сотрудник, выполнивший изменение

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта|&mdash;|да
|**id**                 |UUID|ID Уведомления|&mdash;|да
|**name**               |String(255)|Наименование Контрагента|&mdash;|да

##### Задача

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта|&mdash;|да
|**id**                 |UUID|ID Уведомления|&mdash;|да
|**name**               |String(255)|Наименование Контрагента|&mdash;|да
|**deadline**                |DateTime|Планируемая дата завершения задачи|&mdash;|да


**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: bcd815b9-56ca-11e9-c0a8-100b00000001* id Уведомления.|

> Запрос на получение Уведомления с указанным id.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/notification/bcd815b9-56ca-11e9-c0a8-100b00000001"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление Уведомления.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/notification/bcd815b9-56ca-11e9-c0a8-100b00000001",
    "type": "NotificationTaskAssigned",
    "mediaType": "application/json"
  },
  "id": "bcd815b9-56ca-11e9-c0a8-100b00000001",
  "accountId": "c45c23d5-5640-11e9-c0a8-100a00000001",
  "created": "2019-04-04 14:13:56.000",
  "read": false,
  "title": "Новая задача: Текст задачи 1",
  "description": "ntest1 назначил вам задачу Текст задачи 1",
  "performedBy": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/c4e1397b-807c-11e9-9ff4-31500025d4ed",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
      "type": "employee",
      "mediaType": "application/json"
    },
    "id": "c4e1397b-807c-11e9-9ff4-31500025d4ed",
    "name": "ntest1"
  },
  "task": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/task/91d6e8a5-807d-11e9-9109-f8fc0024968d",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/task/metadata",
      "type": "task",
      "mediaType": "application/json"
    },
    "id": "91d6e8a5-807d-11e9-9109-f8fc0024968d",
    "name": "Текст задачи 1"
  }
}
```

### Задача снята
#### Тип уведомления
NotificationTaskUnassigned - задача снята
#### Атрибуты уведомления

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта|Необходимое при создании|да
|**id**                 |UUID|ID Уведомления|Необходимое при создании|да
|**accountId**          |UUID| ID учетной записи|Необходимое при создании|да
|**created**            |DateTime|Дата и время формирования Уведомления|Необходимое при создании|да
|**read**        |Boolean|Признак того, было ли Уведомление прочитано|Необходимое при создании|да
|**title**       |String(255)|Краткий текст уведомления|Необходимое при создании| да
|**description**       |String(4096)|Описание уведомления|Необходимое при создании| да
|**performedBy**                 |Object|Сотрудник, выполнивший изменение. [Подробнее тут](../dictionaries/#suschnosti-kontragent-kontragenty-attributy-suschnosti-adres)|Необходимое при создании|да
|**task**                 |Object|Задача|Необходимое при создании. [Подробнее тут](../dictionaries/#suschnosti-kontragent-kontragenty-attributy-suschnosti-adres)|да

#### Атрибуты вложенных сущностей
##### Сотрудник, выполнивший изменение

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта|&mdash;|да
|**id**                 |UUID|ID Уведомления|&mdash;|да
|**name**               |String(255)|Наименование Контрагента|&mdash;|да

##### Задача

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта|&mdash;|да
|**id**                 |UUID|ID Уведомления|&mdash;|да
|**name**               |String(255)|Наименование Контрагента|&mdash;|да
|**deadline**                |DateTime|Планируемая дата завершения задачи|&mdash;|да

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 80c8a58b-56cb-11e9-c0a8-100b00000009* id Уведомления.|

> Запрос на получение Уведомления с указанным id.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/notification/80c8a58b-56cb-11e9-c0a8-100b00000009"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление Уведомления.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/notification/80c8a58b-56cb-11e9-c0a8-100b00000009",
    "type": "NotificationTaskUnassigned",
    "mediaType": "application/json"
  },
  "id": "80c8a58b-56cb-11e9-c0a8-100b00000009",
  "accountId": "c45c23d5-5640-11e9-c0a8-100a00000001",
  "created": "2019-04-04 14:19:25.000",
  "read": false,
  "title": "Задача снята: Новый текст задачи 1",
  "description": "ntest1 снял с вас задачу",
  "performedBy": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/c4e1397b-807c-11e9-9ff4-31500025d4ed",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
      "type": "employee",
      "mediaType": "application/json"
    },
    "id": "c4e1397b-807c-11e9-9ff4-31500025d4ed",
    "name": "ntest1"
  },
  "task": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/task/91d6e8a5-807d-11e9-9109-f8fc0024968d",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/task/metadata",
      "type": "task",
      "mediaType": "application/json"
    },
    "id": "91d6e8a5-807d-11e9-9109-f8fc0024968d",
    "name": "Новый текст задачи 1",
    "deadline": "2019-05-27 15:49:00.000"
  }
}
```

### Задача изменена
#### Тип уведомления
NotificationTaskChanged - задача изменена
#### Атрибуты уведомления

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта|Необходимое при создании|да
|**id**                 |UUID|ID Уведомления|Необходимое при создании|да
|**accountId**          |UUID| ID учетной записи|Необходимое при создании|да
|**created**            |DateTime|Дата и время формирования Уведомления|Необходимое при создании|да
|**read**        |Boolean|Признак того, было ли Уведомление прочитано|Необходимое при создании|да
|**title**       |String(255)|Краткий текст уведомления|Необходимое при создании| да
|**description**       |String(4096)|Описание уведомления|Необходимое при создании| да
|**performedBy**                 |Object|Сотрудник, выполнивший изменение. [Подробнее тут](../dictionaries/#suschnosti-kontragent-kontragenty-attributy-suschnosti-adres)|Необходимое при создании|да
|**diff**                 |Object|Задача|Измененные поля. [Подробнее тут](../dictionaries/#suschnosti-kontragent-kontragenty-attributy-suschnosti-adres)|да
|**task**                 |Object|Задача|Необходимое при создании. [Подробнее тут](../dictionaries/#suschnosti-kontragent-kontragenty-attributy-suschnosti-adres)|да

#### Атрибуты вложенных сущностей
##### Сотрудник, выполнивший изменение

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта|&mdash;|да
|**id**                 |UUID|ID Уведомления|&mdash;|да
|**name**               |String(255)|Наименование Контрагента|&mdash;|да

##### Измененные поля

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**description**               |String(255)|Изменение описания задачи в [формате изменения поля](../other/#uwedomleniq-tipy-uwedomlenij-formaty-polej-format-izmenennogo-polq)|&mdash;|да
|**deadline**              |String(255)|Изменение планируемой даты завершения задачи в [формате изменения поля](../other/#uwedomleniq-tipy-uwedomlenij-formaty-polej-format-izmenennogo-polq)|&mdash;|да
|**agentLink**               |String(255)|Изменение контрагента в [формате изменения поля](../other/#uwedomleniq-tipy-uwedomlenij-formaty-polej-format-izmenennogo-polq)|&mdash;|да
|**documentLink**               |String(255)|Изменение связанного документа в [формате изменения поля](../other/#uwedomleniq-tipy-uwedomlenij-formaty-polej-format-izmenennogo-polq)|&mdash;|да
|**assignee**              |String(255)|Изменение исполнителя в [формате изменения поля](../other/#uwedomleniq-tipy-uwedomlenij-formaty-polej-format-izmenennogo-polq)|&mdash;|да

##### Задача

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта|&mdash;|да
|**id**                 |UUID|ID Уведомления|&mdash;|да
|**name**               |String(255)|Наименование Контрагента|&mdash;|да
|**deadline**                |DateTime|Планируемая дата завершения задачи|&mdash;|да

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: bd0dbccf-56ca-11e9-c0a8-100b00000003* id Уведомления.|

> Запрос на получение Уведомления с указанным id.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/notification/bd0dbccf-56ca-11e9-c0a8-100b00000003"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление Уведомления.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/notification/bd0dbccf-56ca-11e9-c0a8-100b00000003",
    "type": "NotificationTaskChanged",
    "mediaType": "application/json"
  },
  "id": "bd0dbccf-56ca-11e9-c0a8-100b00000003",
  "accountId": "c45c23d5-5640-11e9-c0a8-100a00000001",
  "created": "2019-04-04 14:13:56.000",
  "read": false,
  "title": "Задача изменена: Новый текст задачи 1",
  "description": "ntest1 изменил задачу",
  "performedBy": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/c4e1397b-807c-11e9-9ff4-31500025d4ed",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
      "type": "employee",
      "mediaType": "application/json"
    },
    "id": "c4e1397b-807c-11e9-9ff4-31500025d4ed",
    "name": "ntest1"
  },
  "task": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/task/91d6e8a5-807d-11e9-9109-f8fc0024968d",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/task/metadata",
      "type": "task",
      "mediaType": "application/json"
    },
    "id": "91d6e8a5-807d-11e9-9109-f8fc0024968d",
    "name": "Новый текст задачи 1",
    "deadline": "2019-05-27 15:49:00.000"
  },
  "diff": {
    "deadline": {
      "oldValue": "2019-05-29 15:47:00.000",
      "newValue": "2019-05-27 15:49:00.000"
    }
  }
}
```

### Задача выполнена
#### Тип уведомления
NotificationTaskCompleted - задача выполнена
#### Атрибуты уведомления

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта|Необходимое при создании|да
|**id**                 |UUID|ID Уведомления|Необходимое при создании|да
|**accountId**          |UUID| ID учетной записи|Необходимое при создании|да
|**created**            |DateTime|Дата и время формирования Уведомления|Необходимое при создании|да
|**read**        |Boolean|Признак того, было ли Уведомление прочитано|Необходимое при создании|да
|**title**       |String(255)|Краткий текст уведомления|Необходимое при создании| да
|**description**       |String(4096)|Описание уведомления|Необходимое при создании| да
|**performedBy**                 |Object|Сотрудник, выполнивший изменение. [Подробнее тут](../dictionaries/#suschnosti-kontragent-kontragenty-attributy-suschnosti-adres)|Необходимое при создании|да
|**task**                 |Object|Задача|Необходимое при создании. [Подробнее тут](../dictionaries/#suschnosti-kontragent-kontragenty-attributy-suschnosti-adres)|да

#### Атрибуты вложенных сущностей
##### Сотрудник, выполнивший изменение

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта|&mdash;|да
|**id**                 |UUID|ID Уведомления|&mdash;|да
|**name**               |String(255)|Наименование Контрагента|&mdash;|да

##### Задача

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта|&mdash;|да
|**id**                 |UUID|ID Уведомления|&mdash;|да
|**name**               |String(255)|Наименование Контрагента|&mdash;|да
|**deadline**                |DateTime|Планируемая дата завершения задачи|&mdash;|да

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7945a089-56fd-11e9-c0a8-100b00000008* id Уведомления.|

> Запрос на получение Уведомления с указанным id.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/notification/7945a089-56fd-11e9-c0a8-100b00000008"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление Уведомления.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/notification/7945a089-56fd-11e9-c0a8-100b00000008",
    "type": "NotificationTaskCompleted",
    "mediaType": "application/json"
  },
  "id": "7945a089-56fd-11e9-c0a8-100b00000008",
  "accountId": "45eb22e0-0e7b-11e2-1c31-3c4a92f3a0a7",
  "created": "2019-05-27 15:47:47.000",
  "read": false,
  "title": "Задача выполнена: Новый текст задачи 1",
  "description": "ntest1 выполнил задачу Новый текст задачи 1 Срок: 29.05.2019 15:47",
  "performedBy": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/c4e1397b-807c-11e9-9ff4-31500025d4ed",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
      "type": "employee",
      "mediaType": "application/json"
    },
    "id": "c4e1397b-807c-11e9-9ff4-31500025d4ed",
    "name": "ntest1"
  },
  "task": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/task/91d6e8a5-807d-11e9-9109-f8fc0024968d",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/task/metadata",
      "type": "task",
      "mediaType": "application/json"
    },
    "id": "91d6e8a5-807d-11e9-9109-f8fc0024968d",
    "name": "Новый текст задачи 1",
    "deadline": "2019-05-29 15:47:00.000"
  }
}
```

### Задача удалена
#### Тип уведомления
NotificationTaskDeleted - задача удалена
#### Атрибуты уведомления

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта|Необходимое при создании|да
|**id**                 |UUID|ID Уведомления|Необходимое при создании|да
|**accountId**          |UUID| ID учетной записи|Необходимое при создании|да
|**created**            |DateTime|Дата и время формирования Уведомления|Необходимое при создании|да
|**read**        |Boolean|Признак того, было ли Уведомление прочитано|Необходимое при создании|да
|**title**       |String(255)|Краткий текст уведомления|Необходимое при создании| да
|**description**       |String(4096)|Описание уведомления|Необходимое при создании| да
|**performedBy**                 |Object|Сотрудник, выполнивший изменение. [Подробнее тут](../dictionaries/#suschnosti-kontragent-kontragenty-attributy-suschnosti-adres)|Необходимое при создании|да
|**task**                 |Object|Задача|Необходимое при создании. [Подробнее тут](../dictionaries/#suschnosti-kontragent-kontragenty-attributy-suschnosti-adres)|да

#### Атрибуты вложенных сущностей
##### Сотрудник, выполнивший изменение

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта|&mdash;|да
|**id**                 |UUID|ID Уведомления|&mdash;|да
|**name**               |String(255)|Наименование Контрагента|&mdash;|да

##### Задача

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**name**               |String(255)|Наименование Контрагента|&mdash;|да

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 8d07388c-56cb-11e9-c0a8-100b0000000d* id Уведомления.|

> Запрос на получение Уведомления с указанным id.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/notification/8d07388c-56cb-11e9-c0a8-100b0000000d"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление Уведомления.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/notification/8d07388c-56cb-11e9-c0a8-100b0000000d",
    "type": "NotificationTaskDeleted",
    "mediaType": "application/json"
  },
  "id": "8d07388c-56cb-11e9-c0a8-100b0000000d",
  "accountId": "45eb22e0-0e7b-11e2-1c31-3c4a92f3a0a7",
  "created": "2019-05-27 15:58:45.000",
  "read": false,
  "title": "Задача удалена: Текст задачи 2",
  "description": "ntest1 удалил задачу Текст задачи 2",
  "task": {
    "name": "Текст задачи 2"
  },
  "performedBy": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/c4e1397b-807c-11e9-9ff4-31500025d4ed",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
      "type": "employee",
      "mediaType": "application/json"
    },
    "id": "c4e1397b-807c-11e9-9ff4-31500025d4ed",
    "name": "ntest1"
  }
}
```

### Задача просрочена
#### Тип уведомления
NotificationTaskOverdue - задача просрочена
#### Атрибуты уведомления

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта|Необходимое при создании|да
|**id**                 |UUID|ID Уведомления|Необходимое при создании|да
|**accountId**          |UUID| ID учетной записи|Необходимое при создании|да
|**created**            |DateTime|Дата и время формирования Уведомления|Необходимое при создании|да
|**read**        |Boolean|Признак того, было ли Уведомление прочитано|Необходимое при создании|да
|**title**       |String(255)|Краткий текст уведомления|Необходимое при создании| да
|**description**       |String(4096)|Описание уведомления|Необходимое при создании| да
|**task**                 |Object|Задача|Необходимое при создании. [Подробнее тут](../dictionaries/#suschnosti-kontragent-kontragenty-attributy-suschnosti-adres)|да

#### Атрибуты вложенных сущностей
##### Сотрудник, выполнивший изменение

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта|&mdash;|да
|**id**                 |UUID|ID Уведомления|&mdash;|да
|**name**               |String(255)|Наименование Контрагента|&mdash;|да

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 51a5b0a3-56e4-11e9-c0a8-100b00000014* id Уведомления.|

> Запрос на получение Уведомления с указанным id.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/notification/51a5b0a3-56e4-11e9-c0a8-100b00000014"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление Уведомления.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/notification/51a5b0a3-56e4-11e9-c0a8-100b00000014",
    "type": "NotificationTaskOverdue",
    "mediaType": "application/json"
  },
  "id": "51a5b0a3-56e4-11e9-c0a8-100b00000014",
  "accountId": "45eb22e0-0e7b-11e2-1c31-3c4a92f3a0a7",
  "created": "2019-05-27 15:49:01.000",
  "read": false,
  "title": "Просрочена задача: Новый текст задачи 1",
  "description": "Задача просрочена Новый текст задачи 1 Срок: 27.05.2019 15:49",
  "task": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/task/91d6e8a5-807d-11e9-9109-f8fc0024968d",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/task/metadata",
      "type": "task",
      "mediaType": "application/json"
    },
    "id": "91d6e8a5-807d-11e9-9109-f8fc0024968d",
    "name": "Новый текст задачи 1",
    "deadline": "2019-05-27 15:49:00.000"
  }
}
```

### Задача переоткрыта
#### Тип уведомления
NotificationTaskReopened - задача переоткрыта
#### Атрибуты уведомления

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта|Необходимое при создании|да
|**id**                 |UUID|ID Уведомления|Необходимое при создании|да
|**accountId**          |UUID| ID учетной записи|Необходимое при создании|да
|**created**            |DateTime|Дата и время формирования Уведомления|Необходимое при создании|да
|**read**        |Boolean|Признак того, было ли Уведомление прочитано|Необходимое при создании|да
|**title**       |String(255)|Краткий текст уведомления|Необходимое при создании| да
|**description**       |String(4096)|Описание уведомления|Необходимое при создании| да
|**performedBy**                 |Object|Сотрудник, выполнивший изменение. [Подробнее тут](../dictionaries/#suschnosti-kontragent-kontragenty-attributy-suschnosti-adres)|Необходимое при создании|да
|**task**                 |Object|Задача|Необходимое при создании. [Подробнее тут](../dictionaries/#suschnosti-kontragent-kontragenty-attributy-suschnosti-adres)|да

#### Атрибуты вложенных сущностей
##### Сотрудник, выполнивший изменение

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта|&mdash;|да
|**id**                 |UUID|ID Уведомления|&mdash;|да
|**name**               |String(255)|Наименование Контрагента|&mdash;|да

##### Задача

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта|&mdash;|да
|**id**                 |UUID|ID Уведомления|&mdash;|да
|**name**               |String(255)|Наименование Контрагента|&mdash;|да
|**deadline**                |DateTime|Планируемая дата завершения задачи|&mdash;|да

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: df0c3e22-56fd-11e9-c0a8-100b0000000a* id Уведомления.|

> Запрос на получение Уведомления с указанным id.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/notification/df0c3e22-56fd-11e9-c0a8-100b0000000a"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление Уведомления.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/notification/df0c3e22-56fd-11e9-c0a8-100b0000000a",
    "type": "NotificationTaskReopened",
    "mediaType": "application/json"
  },
  "id": "df0c3e22-56fd-11e9-c0a8-100b0000000a",
  "accountId": "45eb22e0-0e7b-11e2-1c31-3c4a92f3a0a7",
  "created": "2019-05-27 15:48:06.000",
  "read": false,
  "title": "Задача открыта: Новый текст задачи 1",
  "description": "ntest1 открыл задачу Новый текст задачи 1 Срок: 29.05.2019 15:47",
  "performedBy": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/c4e1397b-807c-11e9-9ff4-31500025d4ed",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
      "type": "employee",
      "mediaType": "application/json"
    },
    "id": "c4e1397b-807c-11e9-9ff4-31500025d4ed",
    "name": "ntest1"
  },
  "task": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/task/91d6e8a5-807d-11e9-9109-f8fc0024968d",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/task/metadata",
      "type": "task",
      "mediaType": "application/json"
    },
    "id": "91d6e8a5-807d-11e9-9109-f8fc0024968d",
    "name": "Новый текст задачи 1",
    "deadline": "2019-05-29 15:47:00.000"
  }
}
```

### Новый комментарий к задаче
#### Тип уведомления
NotificationTaskNewComment - новый комментарий к задаче
#### Атрибуты уведомления

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта|Необходимое при создании|да
|**id**                 |UUID|ID Уведомления|Необходимое при создании|да
|**accountId**          |UUID| ID учетной записи|Необходимое при создании|да
|**created**            |DateTime|Дата и время формирования Уведомления|Необходимое при создании|да
|**read**        |Boolean|Признак того, было ли Уведомление прочитано|Необходимое при создании|да
|**title**       |String(255)|Краткий текст уведомления|Необходимое при создании| да
|**description**       |String(4096)|Описание уведомления|Необходимое при создании| да
|**performedBy**                 |Object|Сотрудник, выполнивший изменение. [Подробнее тут](../dictionaries/#suschnosti-kontragent-kontragenty-attributy-suschnosti-adres)|Необходимое при создании|да
|**task**                 |Object|Задача|Необходимое при создании. [Подробнее тут](../dictionaries/#suschnosti-kontragent-kontragenty-attributy-suschnosti-adres)|да
|**noteContent**      |String(4096)|Содержимое комментария|Необходимое при создании| да

#### Атрибуты вложенных сущностей
##### Сотрудник, выполнивший изменение

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта|&mdash;|да
|**id**                 |UUID|ID Уведомления|&mdash;|да
|**name**               |String(255)|Наименование Контрагента|&mdash;|да

##### Задача

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта|&mdash;|да
|**id**                 |UUID|ID Уведомления|&mdash;|да
|**name**               |String(255)|Наименование Контрагента|&mdash;|да
|**deadline**                |DateTime|Планируемая дата завершения задачи|&mdash;|да

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 240706df-5704-11e9-c0a8-100b00000003* id Уведомления.|

> Запрос на получение Уведомления с указанным id.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/notification/240706df-5704-11e9-c0a8-100b00000003"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление Уведомления.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/notification/240706df-5704-11e9-c0a8-100b00000003",
    "type": "NotificationTaskNewComment",
    "mediaType": "application/json"
  },
  "id": "240706df-5704-11e9-c0a8-100b00000003",
  "accountId": "45eb22e0-0e7b-11e2-1c31-3c4a92f3a0a7",
  "created": "2019-05-27 15:50:16.000",
  "read": false,
  "title": "Новый комментарий: Новый текст задачи 1",
  "description": "ntest1 добавил комментарий Комментарий 1",
  "performedBy": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/c4e1397b-807c-11e9-9ff4-31500025d4ed",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
      "type": "employee",
      "mediaType": "application/json"
    },
    "id": "c4e1397b-807c-11e9-9ff4-31500025d4ed",
    "name": "ntest1"
  },
  "task": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/task/91d6e8a5-807d-11e9-9109-f8fc0024968d",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/task/metadata",
      "type": "task",
      "mediaType": "application/json"
    },
    "id": "91d6e8a5-807d-11e9-9109-f8fc0024968d",
    "name": "Новый текст задачи 1",
    "deadline": "2019-05-27 15:49:00.000"
  },
  "noteContent": "Комментарий 1"
}
```


### Изменен комментарий к задаче
#### Тип уведомления
NotificationTaskCommentChanged - изменен комментарий к задаче
#### Атрибуты уведомления

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта|Необходимое при создании|да
|**id**                 |UUID|ID Уведомления|Необходимое при создании|да
|**accountId**          |UUID| ID учетной записи|Необходимое при создании|да
|**created**            |DateTime|Дата и время формирования Уведомления|Необходимое при создании|да
|**read**        |Boolean|Признак того, было ли Уведомление прочитано|Необходимое при создании|да
|**title**       |String(255)|Краткий текст уведомления|Необходимое при создании| да
|**description**       |String(4096)|Описание уведомления|Необходимое при создании| да
|**performedBy**                 |Object|Сотрудник, выполнивший изменение. [Подробнее тут](../dictionaries/#suschnosti-kontragent-kontragenty-attributy-suschnosti-adres)|Необходимое при создании|да
|**task**                 |Object|Задача|Необходимое при создании. [Подробнее тут](../dictionaries/#suschnosti-kontragent-kontragenty-attributy-suschnosti-adres)|да
|**noteContent**      |String(4096)|Содержимое комментария|Необходимое при создании| да
|**diff**      |String(255)|Изменения комментария в [формате изменения поля](../other/#uwedomleniq-tipy-uwedomlenij-formaty-polej-format-izmenennogo-polq)|Необходимое при создании| да

#### Атрибуты вложенных сущностей
##### Сотрудник, выполнивший изменение

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта|&mdash;|да
|**id**                 |UUID|ID Уведомления|&mdash;|да
|**name**               |String(255)|Наименование Контрагента|&mdash;|да

##### Задача

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта|&mdash;|да
|**id**                 |UUID|ID Уведомления|&mdash;|да
|**name**               |String(255)|Наименование Контрагента|&mdash;|да
|**deadline**                |DateTime|Планируемая дата завершения задачи|&mdash;|да

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 3d3423ee-5704-11e9-c0a8-100b00000007* id Уведомления.|

> Запрос на получение Уведомления с указанным id.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/notification/3d3423ee-5704-11e9-c0a8-100b00000007"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление Уведомления.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/notification/3d3423ee-5704-11e9-c0a8-100b00000007",
    "type": "NotificationTaskCommentChanged",
    "mediaType": "application/json"
  },
  "id": "3d3423ee-5704-11e9-c0a8-100b00000007",
  "accountId": "45eb22e0-0e7b-11e2-1c31-3c4a92f3a0a7",
  "created": "2019-05-27 15:50:53.000",
  "read": false,
  "title": "Комментарий изменен: Новый текст задачи 1",
  "description": "ntest1 изменил комментарий Новый текст комментария 1, Комментарий 1",
  "performedBy": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/c4e1397b-807c-11e9-9ff4-31500025d4ed",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
      "type": "employee",
      "mediaType": "application/json"
    },
    "id": "c4e1397b-807c-11e9-9ff4-31500025d4ed",
    "name": "ntest1"
  },
  "task": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/task/91d6e8a5-807d-11e9-9109-f8fc0024968d",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/task/metadata",
      "type": "task",
      "mediaType": "application/json"
    },
    "id": "91d6e8a5-807d-11e9-9109-f8fc0024968d",
    "name": "Новый текст задачи 1",
    "deadline": "2019-05-27 15:49:00.000"
  },
  "diff": {
    "noteContent": {
      "oldValue": "Комментарий 1",
      "newValue": "Новый текст комментария 1"
    }
  }
}
```

### Удален комментарий к задаче
#### Тип уведомления
NotificationTaskCommentDeleted - удален комментарий к задаче
#### Атрибуты уведомления

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта|Необходимое при создании|да
|**id**                 |UUID|ID Уведомления|Необходимое при создании|да
|**accountId**          |UUID| ID учетной записи|Необходимое при создании|да
|**created**            |DateTime|Дата и время формирования Уведомления|Необходимое при создании|да
|**read**        |Boolean|Признак того, было ли Уведомление прочитано|Необходимое при создании|да
|**title**       |String(255)|Краткий текст уведомления|Необходимое при создании| да
|**description**       |String(4096)|Описание уведомления|Необходимое при создании| да
|**performedBy**                 |Object|Сотрудник, выполнивший изменение. [Подробнее тут](../dictionaries/#suschnosti-kontragent-kontragenty-attributy-suschnosti-adres)|Необходимое при создании|да
|**task**                 |Object|Задача|Необходимое при создании. [Подробнее тут](../dictionaries/#suschnosti-kontragent-kontragenty-attributy-suschnosti-adres)|да
|**noteContent**      |String(4096)|Содержимое комментария|Необходимое при создании| да

#### Атрибуты вложенных сущностей
##### Сотрудник, выполнивший изменение

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта|&mdash;|да
|**id**                 |UUID|ID Уведомления|&mdash;|да
|**name**               |String(255)|Наименование Контрагента|&mdash;|да

##### Задача

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта|&mdash;|да
|**id**                 |UUID|ID Уведомления|&mdash;|да
|**name**               |String(255)|Наименование Контрагента|&mdash;|да
|**deadline**                |DateTime|Планируемая дата завершения задачи|&mdash;|да

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 3d2abf0f-5704-11e9-c0a8-100b00000005* id Уведомления.|

> Запрос на получение Уведомления с указанным id.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/notification/3d2abf0f-5704-11e9-c0a8-100b00000005"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление Уведомления.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/notification/3d2abf0f-5704-11e9-c0a8-100b00000005",
    "type": "NotificationTaskCommentDeleted",
    "mediaType": "application/json"
  },
  "id": "3d2abf0f-5704-11e9-c0a8-100b00000005",
  "accountId": "45eb22e0-0e7b-11e2-1c31-3c4a92f3a0a7",
  "created": "2019-05-27 15:51:09.000",
  "read": false,
  "title": "Комментарий удален: Новый текст задачи 1",
  "description": "ntest1 удалил комментарий Новый текст комментария 1",
  "performedBy": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/c4e1397b-807c-11e9-9ff4-31500025d4ed",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
      "type": "employee",
      "mediaType": "application/json"
    },
    "id": "c4e1397b-807c-11e9-9ff4-31500025d4ed",
    "name": "ntest1"
  },
  "task": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/task/91d6e8a5-807d-11e9-9109-f8fc0024968d",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/task/metadata",
      "type": "task",
      "mediaType": "application/json"
    },
    "id": "91d6e8a5-807d-11e9-9109-f8fc0024968d",
    "name": "Новый текст задачи 1",
    "deadline": "2019-05-27 15:49:00.000"
  },
  "noteContent": "Новый текст комментария 1"
}
```

### Смена открыта
#### Тип уведомления
NotificationRetailShiftOpened - смена открыта
#### Атрибуты уведомления

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта|Необходимое при создании|да
|**id**                 |UUID|ID Уведомления|Необходимое при создании|да
|**accountId**          |UUID| ID учетной записи|Необходимое при создании|да
|**created**            |DateTime|Дата и время формирования Уведомления|Необходимое при создании|да
|**read**        |Boolean|Признак того, было ли Уведомление прочитано|Необходимое при создании|да
|**title**       |String(255)|Краткий текст уведомления|Необходимое при создании| да
|**description**       |String(4096)|Описание уведомления|Необходимое при создании| да
|**user**                |Object|Сотрудник|Необходимое при создании|да
|**retailStore**                |Object|Точка продаж|Необходимое при создании|да
|**retailShift**                |Object|Описание смены|Необходимое при создании|да

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 8002409b-351d-11e9-9ff4-34e80002a126* id Уведомления.|

> Запрос на получение Уведомления с указанным id.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/notification/8002409b-351d-11e9-9ff4-34e80002a126"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление Уведомления.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/notification/8002409b-351d-11e9-9ff4-34e80002a126",
    "type": "NotificationRetailShiftOpened",
    "mediaType": "application/json"
  },
  "id": "8002409b-351d-11e9-9ff4-34e80002a126",
  "accountId": "45eb22e0-0e7b-11e2-1c31-3c4a92f3a0a7",
  "created": "2019-02-20 17:40:42.000",
  "read": true,
  "title": "Открыта смена в Точка продаж",
  "description": "Кассир: Кассир Кладкин",
  "user": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/4d4ba195-0e7b-11e2-480d-3c4a92f3a0a7",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
      "type": "employee",
      "mediaType": "application/json"
    },
    "id": "4d4ba195-0e7b-11e2-480d-3c4a92f3a0a7",
    "name": "Кассир Кладкин"
  },
  "retailStore": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailstore/ffa5bbf4-351b-11e9-9ff4-34e800131be8",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailstore/metadata",
      "type": "retailstore",
      "mediaType": "application/json"
    },
    "id": "ffa5bbf4-351b-11e9-9ff4-34e800131be8",
    "name": "Точка продаж"
  },
  "retailShift": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailshift/7e41bd3c-351c-11e9-9ff4-34e80012cfc1",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailshift/metadata",
      "type": "retailshift",
      "mediaType": "application/json"
    },
    "id": "7e41bd3c-351c-11e9-9ff4-34e80012cfc1",
    "name": "00002",
    "open": "2019-02-20 17:33:00.000",
    "proceed": 3000000
  }
}
```

### Смена закрыта
#### Тип уведомления
NotificationRetailShiftClosed - смена закрыта
#### Атрибуты уведомления

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта|Необходимое при создании|да
|**id**                 |UUID|ID Уведомления|Необходимое при создании|да
|**accountId**          |UUID| ID учетной записи|Необходимое при создании|да
|**created**            |DateTime|Дата и время формирования Уведомления|Необходимое при создании|да
|**read**        |Boolean|Признак того, было ли Уведомление прочитано|Необходимое при создании|да
|**title**       |String(255)|Краткий текст уведомления|Необходимое при создании| да
|**description**       |String(4096)|Описание уведомления|Необходимое при создании| да
|**user**                |Object|Сотрудник|Необходимое при создании|да
|**retailStore**                |Object|Точка продаж|Необходимое при создании|да
|**retailShift**                |Object|Описание смены|Необходимое при создании|да
|**sales**                |Int| Количество продаж|Необходимое при создании|да
|**returns**                 |Int|Количество возвратов|Необходимое при создании|да

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 3929d717-351c-11e9-9ff4-34e800029ad4* id Уведомления.|

> Запрос на получение Уведомления с указанным id.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/notification/3929d717-351c-11e9-9ff4-34e800029ad4"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление Уведомления.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/notification/3929d717-351c-11e9-9ff4-34e800029ad4",
    "type": "NotificationRetailShiftClosed",
    "mediaType": "application/json"
  },
  "id": "3929d717-351c-11e9-9ff4-34e800029ad4",
  "accountId": "45eb22e0-0e7b-11e2-1c31-3c4a92f3a0a7",
  "created": "2019-02-20 17:31:34.000",
  "read": true,
  "title": "Закрыта смена в Точка продаж",
  "description": "Кассир: Кассир Кладкин. Длительность: 1 мин. Продаж: 2. Возвратов: 0. Выручка: 40000.00",
  "user": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/4d4ba195-0e7b-11e2-480d-3c4a92f3a0a7",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
      "type": "employee",
      "mediaType": "application/json"
    },
    "id": "4d4ba195-0e7b-11e2-480d-3c4a92f3a0a7",
    "name": "Кассир Кладкин"
  },
  "retailStore": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailstore/ffa5bbf4-351b-11e9-9ff4-34e800131be8",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailstore/metadata",
      "type": "retailstore",
      "mediaType": "application/json"
    },
    "id": "ffa5bbf4-351b-11e9-9ff4-34e800131be8",
    "name": "Точка продаж"
  },
  "retailShift": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/retailshift/08fd47a8-351c-11e9-9109-f8fc0013f6cd",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/retailshift/metadata",
      "type": "retailshift",
      "mediaType": "application/json"
    },
    "id": "08fd47a8-351c-11e9-9109-f8fc0013f6cd",
    "name": "00001",
    "open": "2019-02-20 17:30:00.000",
    "close": "2019-02-20 17:31:11.000",
    "proceed": 4000000
  },
  "sales": 2,
  "returns": 0
}
```

### Уведомление из сценария
#### Тип уведомления
NotificationScript - уведомление из сценария
#### Атрибуты уведомления

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта|Только для чтения|да
|**id**                 |UUID|ID Уведомления|Только для чтения|да
|**accountId**          |UUID| ID учетной записи|Только для чтения|да
|**created**            |DateTime|Дата и время формирования Уведомления|Только для чтения|да
|**read**        |Boolean|Признак того, было ли Уведомление прочитано|Только для чтения|да
|**title**       |String(255)|Краткий текст уведомления|Только для чтения| да
|**description**       |String(255)|Описание уведомления|Только для чтения| да
|**eventType**       |Событие|Тип события сценария|Только для чтения| да
|**entity**       |Объект|Ссылка на объект сценария|Только для чтения| да

#### Атрибуты вложенных сущностей
##### Событие
Тип события сценария. Возможные значения:

+ **ADD** - создан
+ **MODIFY** - изменен
+ **CHANGE_STATUS** - изменен статус

##### Объект
Объект, на который сработал сценарий.

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта|Только для чтения|да
|**id**                 |UUID|ID объекта|Только для чтения|да
|**name**               |String(255)|Наименование объекта|Только для чтения|да

Допустимые значения для **meta.type**:

+ **customerorder** - заказ покупателя
+ **invoiceout** - счет покупателю
+ **demand** - отгрузка
+ **purchaseorder** - заказ поставщику
+ **invoicein** - счет поставщика
+ **supply** - приемка

**Параметры**

| Параметр   | Описание   | 
|:---|:---|
| **id** |  `string` (required) *Example: 3929d717-351c-11e9-9ff4-34e800029ad4* id Уведомления.|

> Запрос на получение Уведомления с указанным id.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/notification/b22dc861-645b-11eb-0a80-1f8500000044"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление Уведомления.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/notification/b22dc861-645b-11eb-0a80-1f8500000044",
    "type": "NotificationScript",
    "mediaType": "application/json"
  },
  "id": "b22dc861-645b-11eb-0a80-1f8500000044",
  "accountId": "882bbcfa-645b-11eb-0a80-1f8000000016",
  "created": "2021-02-01 10:04:15.907",
  "read": false,
  "title": "тема",
  "description": "текст уведомления",
  "eventType": "MODIFY",
  "entity": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/customerorder/afa8525a-645b-11eb-0a80-2b47000003b7",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/customerorder/metadata",
      "type": "customerorder",
      "mediaType": "application/json"
    },
    "id": "afa8525a-645b-11eb-0a80-2b47000003b7",
    "name": "00001"
  }
}
```

### Предупреждение о скором окончании действия доступа к аккаунту Facebook
#### Тип уведомления
FacebookTokenExpirationNotification - предупреждение о скором окончании действия доступа к аккаунту Facebook
#### Атрибуты уведомления

| Название  | Тип | Описание                    | Свойство поля в запросе| Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**               |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные объекта|Необходимое при создании|да
|**id**                 |UUID|ID Уведомления|Необходимое при создании|да
|**accountId**          |UUID| ID учетной записи|Необходимое при создании|да
|**created**            |DateTime|Дата и время формирования Уведомления|Необходимое при создании|да
|**read**        |Boolean|Признак того, было ли Уведомление прочитано|Необходимое при создании|да
|**title**       |String(255)|Краткий текст уведомления|Необходимое при создании| да
|**description**       |String(4096)|Описание уведомления|Необходимое при создании| да
|**connectorName**       |String(4096)|Название коннектора "Instagram and Facebook"|&mdash;| да
|**daysLeftToExpiration**       |Int|Количество дней, оставшихся до окончания действия доступа к аккаунту Facebook|&mdash;| да

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 9596251d-da73-11eb-ac12-000c00000015* id Уведомления.|

> Запрос на получение Уведомления с указанным id.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/notification/9596251d-da73-11eb-ac12-000c00000015"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление Уведомления.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/notification/9596251d-da73-11eb-ac12-000c00000015",
    "type": "FacebookTokenExpirationNotification",
    "mediaType": "application/json"
  },
  "id": "9596251d-da73-11eb-ac12-000c00000015",
  "accountId": "54148a9e-d8fa-11eb-ac12-000b00000001",
  "created": "2021-07-01 16:52:33",
  "read": true,
  "title": "Обновите привязку к Facebook",
  "description": "Для правильной работы магазина Instagram shop доступ к аккаунту нужно обновлять каждые 60 дней — просто нажмите на кнопку в настройках. Дней до остановки синхронизации: 5",
  "connectorName": "Instagram shop",
  "daysLeftToExpiration": 5
}
```

## Настройки уведомлений
### Атрибуты сущности
+ **groups** - Подписка на уведомления по группам
  + ``groupName`` - Код группы уведомлений
    + **enabled**: (boolean, required) - Признак "активна" для подписки на уведомления данной группы
    + **channels**: (array[string], required) - Массив каналов. Содержит значения из списка: `email` (Email-уведомления), `push` (уведомления на мобильных устройствах)

Значения кода группы уведомлений.

| Код группы уведомлений   | Описание           |
| ------------------------ |--------------------|
| **customer_order**         | Заказы покупателей |
| **invoice**                | Счета покупателей  |
| **stock**                  | Складские остатки  |
| **retail**                 | Розничная торговля |
| **task**                   | Задачи             |
| **data_exchange**          | Обмен данными      |
| **scripts**                | Сценарии           |

### Получить настройки уведомлений
Запрос настроек Уведомлений текущего пользователя.

> Запрос настроек Уведомлений текущего пользователя.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/notification/subscription"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. JSON представление настроек уведомлений.

```json
{
  "groups" : {
    "customer_order" : {
      "enabled" : true,
      "channels" : [ "email", "push" ]
    },
    "invoice" : {
      "enabled" : true,
      "channels" : [ "email", "push" ]
    },
    "stock" : {
      "enabled" : true,
      "channels" : [ "email", "push" ]
    },
    "retail" : {
      "enabled" : true,
      "channels" : [ "email", "push" ]
    },
    "task" : {
      "enabled" : true,
      "channels" : [ "email", "push" ]
    },
    "data_exchange" : {
      "enabled" : true,
      "channels" : [ "email", "push" ]
    },
    "scripts" : {
      "enabled" : true,
      "channels" : [ "email", "push" ]
    },
    "online_stores" : {
      "enabled" : true,
      "channels" : [ "email", "push" ]
    }
  }
}
```

### Изменить настройки уведомлений
Изменение настроек Уведомлений текущего пользователя.

Отключение уведомлений из сценариев недопустимо. Параметр **enabled** игнорируется.

> Изменение настроек Уведомлений текущего пользователя.

```shell
  curl -X PUT
    "https://online.moysklad.ru/api/remap/1.2/notification/subscription"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "groups" : {
              "customer_order" : {
                "enabled" : true,
                "channels" : [ "email", "push" ]
              },
              "invoice" : {
                "enabled" : true,
                "channels" : [ "email", "push" ]
              },
              "stock" : {
                "enabled" : true,
                "channels" : [ "email", "push" ]
              },
              "retail" : {
                "enabled" : true,
                "channels" : [ "email", "push" ]
              },
              "task" : {
                "enabled" : true,
                "channels" : [ "email", "push" ]
              },
              "data_exchange" : {
                "enabled" : true,
                "channels" : [ "email", "push" ]
              },
              "scripts" : {
                "enabled" : true,
                "channels" : [ "email", "push" ]
              },
              "online_stores" : {
                "enabled" : true,
                "channels" : [ "email", "push" ]
              }
            }
          }'
```

> Response 200 (application/json)
Успешное изменение настроек уведомлений.
