# Список изменений

В разделе перечислены изменения и расширения возможностей существующих эндпоинтов, а также новые эндпоинты,
 которые позволяют эффективнее работать с API МоегоСклада.

Более подробно с особенностями API МоегоСклада  можно ознакомиться в
 разделе [Workbook](https://dev.moysklad.ru/doc/api/remap/1.2/workbook/#workbook), а также по ссылкам на основные разделы данной документации.

Список изменений в версии 1.2 с момента её создания можно найти в [github репозитории](https://github.com/moysklad/api-remap-1.2-doc/blob/master/CHANGELOG.md)

## Нотификация в изменениях API
Чтобы узнавать об изменениях в документации и api, вы можете подписаться на нотификации об изменении документации в github.
Для этого:

- установите любой RSS reader (например, [RSS Feed Reader](https://chrome.google.com/webstore/detail/rss-feed-reader/pnjaodmkngahhkoihejjehlcdlnohgmp) для chromium или [FeedBro](https://addons.mozilla.org/en-US/firefox/addon/feedbroreader) для Firefox)
- добавьте https://github.com/moysklad/api-remap-1.2-doc/commits/master.atom
- при любом изменении документации придёт нотификация и можно посмотреть, что именно изменилось.

## Отличия API Remap 1.2 от API Remap 1.1
### Добавлено
- Аутентификация с использованием [токена](https://dev.moysklad.ru/doc/api/remap/1.2/#mojsklad-json-api-obschie-swedeniq-autentifikaciq)
- Работа с Изображениями
  - Изображения [Модификаций](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-modifikaciq) 
  - Работа с несколькими изображениями 
    в [Товарах](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-towar-sozdat-towar), 
    [Комплектах](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-komplekt-sozdat-komplekt), 
    [Модификациях](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-modifikaciq-massowoe-sozdanie-i-obnowlenie-modifikacij)
  - [Новый эндпоинт](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-izobrazhenie) для массового 
    создания, редактирования и удаления изображений у Товаров, Комплектов и Модификаций
- Изменения в [Вебхуках](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-veb-huki)
  - добавлена версия АПИ в теле
  - добавлено поле `accoundId`
- Существующие эндпоинты
  - Создание, обновление и удаление [Точек Продаж](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-tochka-prodazh)
  - Массовое удаление [сущностей](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti)
  - Редактирование полей [Сотрудника](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-sotrudnik), влияющих на разделение доступа: `email`, `group`, `archived`, `owner`, `shared`
  - Удаление [сущностей](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti) по `syncid`
  - Работа с публикациями для [Розничной смены](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-roznichnaq-smena), 
    [Заказа на производство](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-zakaz-na-proizwodstwo), 
    [Отчетов комиссионеров](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-poluchennyj-otchet-komissionera), 
    [Тех. Операции](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-teh-operaciq), 
    [Инвентаризации](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-inwentarizaciq)
  - Обработка `null` для поля [Алкогольной продукции](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-towar). Теперь через JSON API можно менять тип продукции с алкогольной на неалкогольную, передав `null` в поле `alcoholic`
  - Новые поля `directorPosition`, `directorSign`, `chiefAccountSign`, `stamp` в [Юрлице](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-jurlico)
- Работа с Файлами
  - Возможность работы с файлами в [Операциях](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty), [Товарах](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-towar) и [Контрагентах](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-kontragent)
  - [Новый эндпоинт](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-fajly) для работы с Файлами
- Новые эндпоинты
  - Эндпоинт управления [Типами цен](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-tipy-cen)   
  - Эндпоинт [Управления настройками справочника товаров](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-assortiment)
  - Эндпоинт [Управления настройками справочника контрагентов](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-kontragent-nastrojki-sprawochnika-kontragentow)
  - Эндпоинт [Настройка аккаунта компании](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-nastrojki-kompanii)
  - Эндпоинт [Настройки пользователя](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-nastrojki-pol-zowatelq)
  - Отчет [Показатели продаж](https://dev.moysklad.ru/doc/api/remap/1.2/reports/#otchety-pokazateli-prodazh-i-zakazow-pokazateli-prodazh)
  - Отчет [Показатели заказов](https://dev.moysklad.ru/doc/api/remap/1.2/reports/#otchety-pokazateli-prodazh-i-zakazow-pokazateli-zakazow)
  - Отчет [Обороты товаров](https://dev.moysklad.ru/doc/api/remap/1.2/reports/#otchety-otchet-oboroty)
  - Создание [характеристик Модификаций](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-harakteristiki-modifikacij)  
  - Эндпоинты [управления скидками](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-skidki)
  - Эндпоинт [Автозаполнения цен, скидок, ндс позиций](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#pereschet-raschetnogo-ostatka-w-inwentarizacii-awtozapolnenie)
  - Эндпоинты для [управления правами сотрудника](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-sotrudnik-rabota-s-prawami-sotrudnika) 
  - Эндпоинты для [доступа сотрудника к основному сервису МойСклад](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-sotrudnik-aktiwaciq-sotrudnika)
- Добавлена возможность выполнять запросы [асинхронно](https://dev.moysklad.ru/doc/api/remap/1.2/#mojsklad-json-api-asinhronnyj-obmen) 
  - Добавлена статья в [воркбук](https://dev.moysklad.ru/doc/api/remap/1.2/workbook/#workbook-rabota-s-asinhronnym-obmenom)
- Изменения формата JSON
  - Новые поля `bonusProgram` и `bonusPoints` в [Контрагентах](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-kontragent)
    и [Организациях](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-jurlico)
  - Новые поля `minionToMasterType` и `masterRetailStores` в [Точке продаж](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-tochka-prodazh)
- Фильтрация
  - Новая фильтрация в отчетах [Деньги](https://dev.moysklad.ru/doc/api/remap/1.2/reports/#otchety-otchet-den-gi), 
    [Показатели продаж](https://dev.moysklad.ru/doc/api/remap/1.2/reports/#otchety-pokazateli-prodazh-i-zakazow-pokazateli-prodazh) 
    и [Показатели заказов](https://dev.moysklad.ru/doc/api/remap/1.2/reports/#otchety-pokazateli-prodazh-i-zakazow-pokazateli-zakazow)  
  - Фильтрация и сортировки в [Отчетах Остатков](https://dev.moysklad.ru/doc/api/remap/1.2/reports/#otchety-otchet-ostatki)  
  - Фильтрация по `state.name` и `assortment` для [Документов](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#mojsklad-json-api-obschie-swedeniq-fil-traciq-wyborki-s-pomosch-u-parametra-filter-poluchenie-nowogo-tokena-dopolnitel-nye-fil-try)
  - Операторы фильтрации [Ассортимента](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-assortiment) по полю updated `<`, `>`  
  - Фильтрация по uid в запросе [Аудита](https://dev.moysklad.ru/doc/api/remap/1.2/other/#audit-audit-kontexty)
- Маркетплейс
  - Получение [контекста приложения](https://dev.moysklad.ru/doc/api/remap/1.2/#mojsklad-json-api-obschie-swedeniq-serwernye-prilozheniq). Возвращает параметры приложения, в рамках которого происходит запрос
  - [Получение сущности установленного приложения](https://dev.moysklad.ru/doc/api/remap/1.2/#mojsklad-json-api-obschie-swedeniq-serwernye-prilozheniq). Возвращает параметры установленного приложения по id установленного на аккаунте приложения  
  - [Фильтрация выборки](https://dev.moysklad.ru/doc/api/remap/1.2/#mojsklad-json-api-obschie-swedeniq-fil-traciq-wyborki-s-pomosch-u-parametra-filter) с помощью параметра `filter` по изменившему сущность приложению
- Документация
  - Информация о таймаутах и новом параметре в [Вебхуках](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-veb-huki)
  - Новый раздел [Workbook](https://dev.moysklad.ru/doc/api/remap/1.2/workbook/#workbook)
  - Формулировка об ограничении выборки в блоке [Остатки в позициях документов](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty)
  - Описание новых типов для [фильтров Аудита](https://dev.moysklad.ru/doc/api/remap/1.2/other/#audit-audit-fil-try)    
  - Описание работы с маркированными товарами в [Приемке](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-priemka) и [Отгрузке](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-otgruzka)  
  
### Изменено
- Общие изменения
  - Фильтрация только через `filter`. Раньше фильтровать некоторые сущности можно было не используя ключевое слово `filter`
  - Увеличен лимит выборки до *1000* вместо *100* для массивов: позиций, размера выборки get запроса и т.д.
  - Можно создавать не более 5 [Веб-хуков](https://dev.moysklad.ru/doc/api/remap/1.2/workbook/#workbook) одного типа на разные url, а не 1 как было ранее
- Изменения формата JSON
  - Формат [Типов цен](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-tipy-cen). Теперь тип цены отображается как объект в сущностях, а не как поле
  - Формат [Штрихкодов](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-towar-towary):
    - можно сохранять ean8 как ean13
    - можно сохранять ean13 как ean8  
    - в значение штрихкода теперь нельзя передавать `null`
    - штрихкоды без указания типа теперь игнорируются
    - штрихкоды вида `null` теперь игнорируются
  - Вывод "денежных" полей, таких как: `vatSum`, `sum`, `commitentSum`, `linkedSum`, `processingSum`, `proceedsNoCash`, `proceedsCash`, 
    `receivedNoCash`, `receivedCash`, `shippedSum`, `payedSum`, `invoicedSum`, `overhead.sum`, `checkSum` теперь в валюте (соответствует полю rate) [Документа](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-roznichnaq-smena-roznichnye-smeny)
  - В составе [Контрагента](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-kontragent) поле `groups` заменено на `tags`  
  - Переименовано поле `modificationsCount` в `variantsCount` в [Товарах](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-towar)  
  - Время в полях типа `дата-время` отображается с точностью до миллисекунд
- Поведения работы эндпоинта  
  - Нельзя добавлять пустое значение в массив тегов в [Контрагентах](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-kontragent-kontragenty),
   [Точках продаж](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-tochka-prodazh-tochki-prodazh) и т.д. Такие значения будут игнорироваться  
  - Фильтры в запросе [Ассортимента](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-assortiment)
    - все фильтры по полям, по доступно и остаток, по search и сортировки теперь могут работать вместе
  - [Дополнительные поля](https://dev.moysklad.ru/doc/api/remap/1.2/workbook/#workbook-rabota-s-dopolnitel-nymi-polqmi-cherez-json-api) у Товаров, Услуг, Модификаций и Комплектов общие и располагаются в метаданных Товаров.  
- Путь эндпоинта
  - Изменен путь к эндпоинтам [Показателям по деньгам](https://dev.moysklad.ru/doc/api/remap/1.2/reports/#otchety-pokazateli) (`report`)      
- Документация
  - Дополнена документация по [Аудиту](https://dev.moysklad.ru/doc/api/remap/1.2/other/#audit) по новым полям и сущностям
  - Название сущности в документации [Счет-фактура выданный](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-schet-faktura-wydannyj)
    ([Полученный](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-schet-faktura-poluchennyj)) приведено к общему виду (с написанием "выданный" после)
  - Описание в документации об ограничении при создании [Веб-хуков](https://dev.moysklad.ru/doc/api/remap/1.2/workbook/#workbook) на одну сущность
  - [Описание](https://dev.moysklad.ru/doc/api/remap/1.2/#mojsklad-json-api-obschie-swedeniq-ogranicheniq) ограничения по запросу на один IP
  - Исправлен ряд опечаток в примерах
  - Исправление опечатки в описании `email` в документации в разделе [Сотрудника](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-sotrudnik)
  
### Удалено
- Заголовки `If-Modified-Since`, `debug`, `X-Lognex-Format-Millisecond`
- Поле `version`
- Поле `documents` у [Документов](https://dev.moysklad.ru/doc/api/remap/1.2/#mojsklad-json-api-obschie-swedeniq-ogranicheniq)
- Передача заголовка `Accept`
- Поле `createShared` из метаданных [Товаров](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-towar), 
[Услуг](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-usluga), 
[Комплектов](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-komplekt), 
[Групп Товаров](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-gruppa-towarow)
- Возможность изменения поля `ofdEnabled` для [Точки продаж](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-tochka-prodazh). Теперь оно всегда равно true
- Описание заголовка `Lognex-Pretty-Print-JSON` в Общих сведениях
- В [Розничной смене](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-roznichnaq-smena) удалено поле `applicable` в перечислении полей

## Список последних изменений
<a name="lastchanges"></a>
Список последних изменений в API Remap 1.2

### 05-07-2021
#### Добавлено
- Новый тип уведомлений о скором окончании действия доступа к аккаунту Facebook

### 01-07-2021
#### Исправлено
- Исправлено описание обязательности полей отчета обороты при ответе

### 28-06-2021
#### Добавлено
- Пермиссии на документы маркировки в [правах сотрудника](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-sotrudnik-rabota-s-prawami-sotrudnika)

### 25-06-2021
#### Добавлено
- Новый ресурс [Отчет обороты](https://dev.moysklad.ru/doc/api/remap/1.2/reports/#otchety-otchet-oboroty)

### 10-06-2021
#### Документация
- Добавлено описание параметров фильтрации выборки `momentFrom` и `momentTo` в отчетах прибыльности

### 03-06-2021
#### Добавлено
- Возможность перехода к соответствующему разделу с описанием ошибки по ссылке в `errors.moreInfo`

### 03-06-2021
#### Документация
- Исправлено описание атрибута `pack` у позиций документов

### 01-06-2021
#### Добавлено
- Возможность получать и изменять пользовательские роли от лица приложения
- Исправлена ошибка: при изменении пермиссий у роли сотрудника, был невозможен вход в систему

### 31-05-2021
#### Добавлено
- Добавлены поля `welcomeBonusesEnabled`, `welcomeBonusesValue`, `welcomeBonusesEnabled` в [Бонусную программу](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-bonusnaq-programma)
- Возможность получать коды маркировки товаров и транспортных упаковок в формате тега 1162 (поле `trackingCodes_1162`) для документа типа [Отгрузка](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-otgruzka-otgruzki-kody-markirowki-towarow-i-transportnyh-upakowok-w-formate-tega-1162).

### 28-05-2021
#### Документация
- Добавлена колонка `Expand` в таблицы описания атрибутов сущностей в разделах: "Сущности" и "Документы"

### 27-05-2021
#### Добавлено
- Добавлены новые поля `authorizedHosts`, `authorizedIpNetwork`, `authorizedIpNetmask` для ограничения доступа по ip в [эндпоинте управления правами сотрудника](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-sotrudnik-rabota-s-prawami-sotrudnika)

### 21-05-2021
#### Документация
- Исправлено описание пермиссий при работе с пользовательскими справочниками

### 21-05-2021
#### Добавлено
- Исправлена отметка об обязательности складов для части документов
- Добавлен новый эндпоинт для системных ролей
- Добавлен новый эндпоинт (crud) для пользовательских ролей
- Новый ресурс [отмены асинхронной задачи](https://dev.moysklad.ru/doc/api/remap/1.2/#mojsklad-json-api-asinhronnyj-obmen-otmena-asinhronnoj-zadachi)
- Ошибка [61007](https://dev.moysklad.ru/doc/api/remap/1.2/#mojsklad-json-api-oshibki-kody-oshibok-dlq-asinhronnogo-obmena)

### 21-05-2021
#### Исправлено
- В примерах исправлен url получения метаданных [Комплектов](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-komplekt)
  и [Услуг](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-usluga)

### 20-05-2021
#### Добавлено
- Добавлена возможность редактировать поле discounts у контрагента
- Раскомплектовывание комплектов на составляющие компоненты при создании [шаблона заказа поставщику на основе](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-zakaz-postawschiku-shablon-zakaza-postawschiku-na-osnowe)
- Добавлена новая схема работы с ошибками и новый статус `API_ERROR` в
  [асинхронном обмене](https://dev.moysklad.ru/doc/api/remap/1.2/#mojsklad-json-api-asinhronnyj-obmen)
  
### 17-05-2021
#### Документация
- В Позиции Отгрузки добавлен список комплектов
- Исправлено описание `product.packs.barcodes`, `consignment.barcodes`, `bundle.components`, `consignment.image`
- Исправлено описание атрибута `images` в товарах, комплектах и модификациях
- Исправлено указание на обязательность в ответе полей `uom.accountId`, `uom.group`, `product.minimumBalance`, `country.accountId`, `demand.vatSum`, `counterparty.state`
- Исправлено указание на обязательность в ответе поля `owner` в сущностях

### 11-05-2021
#### Добавлено
- Возможность выполнять запрос [получения Ассортимента](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-assortiment)
 [асинхронно](https://dev.moysklad.ru/doc/api/remap/1.2/#mojsklad-json-api-asinhronnyj-obmen)

### 29-04-2021
#### Добавлено
- Поле `earnWhileRedeeming` в [Бонусную программу](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-bonusnaq-programma)

### 29-04-2021
#### Добавлено
- Возможность выполнять запрос [получения списка Контрагентов](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-kontragent-poluchit-spisok-kontragentow)
 [асинхронно](https://dev.moysklad.ru/doc/api/remap/1.2/#mojsklad-json-api-asinhronnyj-obmen)

### 28-04-2021
#### Изменено
- Для атрибутов
  AttributeMetadata.required ,
  AgentAccount.isDefault, WebHook.enabled, Product.weighed
  при передаче null значения выводится ошибка 2016

### 28-04-2021
#### Изменено
- Для документа [`Оприходования`](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-oprihodowanie)
  теперь учитывается пермиссия `Видеть себестоимость, цену закупки и прибыль товаров`. При отсутствии пермиссии в json представлении
  документа будет отсутствовать поле `sum`, а в позициях не будет поля `price`.

### 27-04-2021
#### Добавлено
- Очередь для [асинхронных задач](https://dev.moysklad.ru/doc/api/remap/1.2/#mojsklad-json-api-asinhronnyj-obmen)
- Обновлен список [ограничений](https://dev.moysklad.ru/doc/api/remap/1.2/#mojsklad-json-api-obschie-swedeniq-ogranicheniq) (добавлена информация про размер очереди асинхронных задач)
- Новый статус `PENDING` для [асинхронных задач](https://dev.moysklad.ru/doc/api/remap/1.2/#mojsklad-json-api-asinhronnyj-obmen)
- Эндпоинт получения [списка статусов асинхронных задач](https://dev.moysklad.ru/doc/api/remap/1.2/#mojsklad-json-api-asinhronnyj-obmen-statusy-asinhronnyh-zadach)
- Поле **meta** для [асинхронных задач](https://dev.moysklad.ru/doc/api/remap/1.2/#mojsklad-json-api-asinhronnyj-obmen)

### 27-04-2021
#### Добавлена
- Возможность создавать [вебхуки](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-veb-huki) для [асинхронных задач](https://dev.moysklad.ru/doc/api/remap/1.2/#mojsklad-json-api-asinhronnyj-obmen)

### 24-04-2021
#### Документация
- Добавлен новый раздел [Подписка компании](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-podpiska-kompanii)

### 24-04-2021
#### Изменено
- Исправлена работа с документом [Возврат поставщику](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-vozwrat-postawschiku): 
 добавлена проверка совпадения значения поля `vatEnabled` при создании и обновлении документа на основании [Приемки](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-priemka)

### 26-04-2021
#### Изменено
- Исправлен некорректный url в примерах json [Управления настройками справочника ассортимента](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-assortiment-poluchit-nastrojki-sprawochnika-towarow)

### 26-04-2021
#### Добавлены
- Новые поля `directorPosition`, `directorSign`, `chiefAccountSign`, `stamp` в [Юрлице](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-jurlico)

### 26-04-2021
#### Изменено
- Исправлено неточное описание привязок документов в общих сведениях

### 23-04-2021
#### Добавлено
- Добавлены поля authorApplication в [Задачи](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-zadacha) и [События Контрагента](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-kontragent-sobytiq-kontragenta)

### 22-04-2021
#### Документация
- Добавлено описание поля **code** для ряда сущностей. Где оно было, убран атрибут `Только для чтения`

### 15-04-2021
#### Добавлено
- Возможность работы с файлами, прикрепленными к [Задаче](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-zadacha)

### 13-04-2021
#### Добавлено
- Добавлена новая ошибка [17020](https://dev.moysklad.ru/doc/api/remap/1.2/#mojsklad-json-api-oshibki-kody-oshibok-dlq-dokumentow) - товар из упаковки в позиции документа не соответствует товару, указанному в данной позиции
- Добавлена валидация товара из упаковки в позиции документа

### 09-04-2021
#### Документация
- Переработан раздел [Работа с доп. полями](https://dev.moysklad.ru/doc/api/remap/1.2/#mojsklad-json-api-obschie-swedeniq-rabota-s-dopolnitel-nymi-polqmi)
- Добавлен тип MetaArray - объект с полями **meta** и **rows**
- Упоминание Array(Meta) изменено на Array(Object) или на MetaArray
- Изменен формат описания поля **trackingCodes** в Отгрузках и Приёмках
- Добавлен раздел [Валюта в документах](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-obschie-swedeniq-valuta-w-dokumentah) с описанием поля **rate**
- В описание добавлены отсутствовавшие поля **meta** в Счета и Контактные лица Контрагента
- Убрано возможное разночтение в описании поля **tags** Контрагента
- Для полей **consignee** и **carrier** в Отгрузках и Счетах-фактурах выданных добавлена пометка про тип сущностей
- Удалена пометка об обязательности поля **house** в адресах
- Исправлен тип поля **certificateNumber** у Юрлиц на корректный
#### Изменено
- Изменен регистр ключевого слова в [заказе покупателя](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-zakaz-pokupatelq)
- Изменен регистр ключевого слова в [заказе поставщику](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-zakaz-postawschiku)

### 07-04-2021
#### Добавлено
- Добавлен [пример](https://dev.moysklad.ru/doc/api/remap/1.2/reports/#otchety-otchet-ostatki-poluchit-ostatki) в отчет остатки по параметру includeRelated 

### 06-04-2021
#### Добавлено
- Добавлено [описание](https://dev.moysklad.ru/doc/api/remap/1.2/reports/#otchety-otchet-pribyl-nost-poluchit-pribyl-nost-po-towaram) отчета по прибыльности по товарам
- Добавлено [описание](https://dev.moysklad.ru/doc/api/remap/1.2/reports/#otchety-otchet-pribyl-nost-poluchit-pribyl-nost-po-modifikaciqm) отчета по прибыльности по модификациям

### 26-03-2021
#### Добавлено
- Возможность выполнять запросы [асинхронно](https://dev.moysklad.ru/doc/api/remap/1.2/#mojsklad-json-api-asinhronnyj-obmen)
- Статья в [воркбук](https://dev.moysklad.ru/doc/api/remap/1.2/workbook/#workbook-rabota-s-asinhronnym-obmenom)
- Описание ошибок [61000-61006](https://dev.moysklad.ru/doc/api/remap/1.2/#mojsklad-json-api-oshibki-kody-oshibok-dlq-asinhronnogo-obmena)  

### 23-03-2021
#### Добавлено
- Поле `postponedBonusesDelayDays` в [Бонусную программу](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-bonusnaq-programma)
- Поля `transactionStatus`, `executionDate` и `categoryType` в [Бонусные операции](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-bonusnaq-operaciq)

### 01-03-2021
#### Документация
- Исправлен запрос в примере на [массовое удаление модификаций](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-modifikaciq-massowoe-udalenie-modifikacij)

### 18-02-2021
#### Изменено
- Изменены CSS стили

### 11-02-2021
#### Изменено
- Исправлены битые ссылки в [Общих сведениях](https://dev.moysklad.ru/doc/api/remap/1.2/#mojsklad-json-api-obschie-swedeniq)
- Исправлено указание на обязательность в ответе поля `vatIncluded` в документах

### 04-02-2021
#### Изменено
- Добавлен новый тип уведомлений [Уведомление из сценария](https://dev.moysklad.ru/doc/api/remap/1.2/other/#uwedomleniq-podrobnoe-opisanie-tipow-uwedomlenij-uwedomlenie-iz-scenariq)
- Добавлена новая группа уведомлений [Сценарии](https://dev.moysklad.ru/doc/api/remap/1.2/other/#uwedomleniq-nastrojki-uwedomlenij-atributy-suschnosti)

### 02-02-2021
#### Добавлено
- Новые [эндпоинты для упралвения правами сотрудника](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-sotrudnik-rabota-s-prawami-sotrudnika) и [эндпоинты для доступа сотрудника к основному сервису 
МойСклад](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-sotrudnik-aktiwaciq-sotrudnika) в раздел [Сотрудники](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-sotrudnik)
- Новые ошибки [3023-3024](https://dev.moysklad.ru/doc/api/remap/1.2/#mojsklad-json-api-oshibki-obschie-oshibki-walidacii) и [43007-43029](https://dev.moysklad.ru/doc/api/remap/1.2/#mojsklad-json-api-oshibki-kody-oshibok-dlq-sotrudnikow)

### 27-01-2021
#### Документация
- Изменен тип поля quantity с Int на Float в разделе описания вложенной [Упаковки товара](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-towar-towary-atributy-wlozhennyh-suschnostej-upakowki-towara)
- Удалено описание полей объекта доп. полей из документов. 
  Его по-прежнему можно найти в разделе [Работа с доп. полями](https://dev.moysklad.ru/doc/api/remap/1.2/#mojsklad-json-api-obschie-swedeniq-rabota-s-dopolnitel-nymi-polqmi)
- Исправлен ряд опечаток в этом разделе

### 20-01-2021
#### Изменено
- Добавлены поля `printed` и `published` в [документах](https://dev.moysklad.ru/doc/api/remap/1.2/documents/)

### 18-01-2021
#### Изменено
- Для доступа к аудиту не нужно быть администратором

### 22-12-2020
#### Изменено
- Исправлен http метод в запросе на удаление группы товаров с GET на DELETE в [Группа товаров](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-gruppa-towarow-udalit-gruppu-towarow)
  и тип полей `minPrice`, `buyPrice` c Double на Object в [Товаре](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-towar)

### 22-12-2020
#### Документация
- Из параметров удален `states`, добавленные туда по ошибке в [метаданных Розничных смен](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-roznichnaq-smena-metadannye-roznichnyh-smen)

### 17-12-2020
#### Изменено
- Исправлен тип qrBankPercent с Int на Double в [Точке продаж](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-tochka-prodazh)

### 04-12-2020
#### Документация
- Исправлены неточности в разделе [Отчет остатки](https://dev.moysklad.ru/doc/api/remap/1.2/reports/#otchety-otchet-ostatki)

### 30-11-2020
#### Документация
- Исправлено форматирование таблицы описания полей результата запроса на [получение дополнительных полей](https://dev.moysklad.ru/doc/api/remap/1.2/#mojsklad-json-api-obschie-swedeniq-dop-polq-suschnostej-poluchit-wse-dop-polq-dlq-ukazannogo-tipa)

### 26-11-2020
#### Добавлено
- Фильтрация по `assortment` для [Документов](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#mojsklad-json-api-obschie-swedeniq-fil-traciq-wyborki-s-pomosch-u-parametra-filter-poluchenie-nowogo-tokena-dopolnitel-nye-fil-try)

### 21-11-2020
#### Изменено
- Описание ограничений в [Общих сведениях](https://dev.moysklad.ru/doc/api/remap/1.2/#mojsklad-json-api-obschie-swedeniq)

### 05-11-2020
#### Добавлено
- Эндпоинт [Управления настройками справочника контрагентов](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-kontragent-nastrojki-sprawochnika-kontragentow)

### 02-11-2020
#### Добавлено
- добавлены коды [ошибок 1083, 1084](/doc/api/remap/1.2/#mojsklad-json-api-oshibki-oshibki-formata).

### 29-10-2020
#### Добавлено
- Исправлена ошибка регистра кода сущности в  [Группе товаров](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-gruppa-towarow)

### 23-10-2020
#### Добавлено
- Поля `idQR` и `qrTerminalId` в [Точку продаж](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-tochka-prodazh)

### 21-10-2020
#### Изменено
- Описание ограничений в [Общих сведениях](https://dev.moysklad.ru/doc/api/remap/1.2/#mojsklad-json-api-obschie-swedeniq)

### 21-10-2020
#### Изменено
- Добавлена возможность создавать, изменять и удалять [Отделы](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-otdel)

### 21-10-2020
#### Добавлено
- Добавлено заполнение себестоимости в эндпоинт [Автозаполнения](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#pereschet-raschetnogo-ostatka-w-inwentarizacii-awtozapolnenie)

### 20-10-2020
#### Добавлено
- Поля `qrPayEnabled`, `qrBankPercent` и `qrAcquire` в [Точку продаж](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-tochka-prodazh)
- Поля `qrSum` и `prepaymentQrSum` в [Розничную продажу](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-roznichnaq-prodazha)
- Поле `qrSum` в [Розничный возврат](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-roznichnyj-wozwrat)
- Ошибки `18005`, `18006`, `19003` и `19004`
#### Изменено
- Описание полей `acquire` и `bankPercent` в [Точке продаж](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-tochka-prodazh)
- Описание [работы с полями оплаты розничной продажи](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-roznichnaq-prodazha-roznichnye-prodazhi-rabota-s-polqmi-oplaty-roznichnoj-prodazhi)
- Текст ошибок `18000` и `19002`

### 16-10-2020
#### Добавлено
- Эндпоинт [Автозаполнения цен, скидок, ндс позиций](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#pereschet-raschetnogo-ostatka-w-inwentarizacii-awtozapolnenie)

### 8-10-2020
#### Изменено
- Исправлены опечатки

### 22-09-2020
#### Документация
- Исправлено описание поля `productFolder` у [Групп товаров](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-gruppa-towarow)

### 20-09-2020
#### Изменено
- Изменено описание установленных ограничений в [Общих сведениях](https://dev.moysklad.ru/doc/api/remap/1.2/#mojsklad-json-api-obschie-swedeniq)

### 31-08-2020
#### Изменено
- Описание атрибута `allowCreateProducts` в [Точке продаж](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-tochka-prodazh)

### 30-07-2020
#### Изменено
[Дополнительные поля](https://dev.moysklad.ru/doc/api/remap/1.2/workbook/#workbook-rabota-s-dopolnitel-nymi-polqmi-cherez-json-api) Товаров, Услуг, Модификаций и Комплектов объединены и располагаются в метаданных Товаров.

### 28-07-2020
#### Добавлено
- Добавлена возможность изменять настройки применения скидок в [настройках компании]((https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-nastrojki-kompanii))

### 27-07-2020
#### Добавлено
 - Поля `minionToMasterType` и `masterRetailStores` в точку продаж, позволяющие указывать стратегию выбора мастер точки продаж для фискализации облачных чеков.

### 22-07-2020
#### Добавлено
- Новое поле `factureIn` в [Возврат поставщику](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-vozwrat-postawschiku)

### 15-07-2020
#### Добавлено
- Эндпоинты [управления скидками](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-skidki)

#### Документация
- Дополнен раздел [Скидки](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-skidki) новыми примерами

### 26-06-2020
#### Документация
- [Информация](https://dev.moysklad.ru/doc/api/remap/1.2/#mojsklad-json-api-obschie-swedeniq) в документацию про отзыв прошлых токенов при создании нового
- Аутентификации через токен в примерах приведена к единому виду

### 23-06-2020
#### Добавлено
- Эндпоинт [Настройки пользователя](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-nastrojki-pol-zowatelq)

### 18-06-2020
#### Добавлено
- Поля ФИО для [Юрлиц](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-jurlico) и [Контрагентов](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-kontragent) типа индивидуальный предприниматель и физическое лицо
- Возможность работы с файлами в [Операциях](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty), [Товарах](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-towar) и [Контрагентах](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-kontragent)

### 11-06-2020
#### Документация
- Добавлена информация о лимитах на число элементов в коллекциях и вложенных сущностях (1000 элементов)

### 10-06-2020
#### Добавлено
- Эндпоинт [Настройка аккаунта компании](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-nastrojki-kompanii)

### 03-06-2020
#### Добавлено
- Эндпоинт [Управления настройками справочника товаров](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-assortiment)

### 28-05-2020
#### Документация
- Добавлена информация об [ограничениях](https://dev.moysklad.ru/doc/api/remap/1.2/workbook/#workbook-chto-nuzhno-znat-dlq-nachala-raboty-s-json-api-ogranicheniq) и новом [параметре в Вебхуках](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-veb-huki)

### 28-05-2020
#### Добавлено в API Remap 1.1 и 1.2
- Для работы с маркированной продукцией добавлены поля `trackingType` - тип маркированной продукции, `tnved` - код ТНВЭД в сущности [Товар](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-towar-sozdat-towar)

#### Документация
- Добавлены описания ошибок [16102-16110](https://dev.moysklad.ru/doc/api/remap/1.2/#mojsklad-json-api-oshibki-kody-oshibok-dlq-towarow), связанных с маркированными товарами

### 15-05-2020
#### Добавлено
- Возможность изменения полей [Сотрудника](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-sotrudnik): `email`, `group`, `archived`, `owner`, `shared`

### 08-05-2020
#### Документация
- Добавлено описание по работе с маркированными товарами в [Приемке](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-priemka) и [Отгрузке](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-otgruzka)

### 06-05-2020
#### Документация
- Добавлено описание об ограничении выборки в блоке [Остатки в позициях документов](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty)

### 27-04-2020
#### Документация
- Удалено описание заголовка `Lognex-Pretty-Print-JSON` в [Общих сведениях](https://dev.moysklad.ru/doc/api/remap/1.2/#mojsklad-json-api-obschie-swedeniq)

### 26-04-2020
#### Документация
- [Изменено описание](https://dev.moysklad.ru/doc/api/remap/1.2/#mojsklad-json-api-obschie-swedeniq-ogranicheniq) ограничения по запросу на один IP

### 26-04-2020
#### Документация
- Исправление опечатки в описании `email` [Сотрудника](https://dev.moysklad.ru/doc/api/remap/1.2/dictionaries/#suschnosti-sotrudnik)

### 14-04-2020
#### Документация
- Добавлено описание новых типов для [фильтров Аудита](https://dev.moysklad.ru/doc/api/remap/1.2/other/#audit-audit-fil-try)

### 26-03-2020
#### Изменено
- В [Розничной смене](https://dev.moysklad.ru/doc/api/remap/1.2/documents/#dokumenty-roznichnaq-smena) удалено поле `applicable` в перечислении полей

### 10-03-2020
#### Добавлено
- Поля `printed` и `published` в эндпоинте `entity/operation` 

### 04-03-2020
#### Добавлено
- Поле `stockDays` - количество дней на складе в [Отчет Остатки -> Все Остатки](https://dev.moysklad.ru/doc/api/remap/1.2/reports/#otchety-otchet-ostatki-dostup-k-otchetu-ostatki)

### 04-03-2020
#### Документация
- Добавлен новый раздел [Workbook](https://dev.moysklad.ru/doc/api/remap/1.2/workbook/#workbook)

##
[Более полный список изменений](https://github.com/moysklad/api-remap-1.2-doc/blob/master/CHANGELOG.md)
