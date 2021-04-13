## Товар
### Товары 
Средствами JSON API можно создавать и обновлять сведения о Товарах, запрашивать списки Товаров и сведения по отдельным Товарам.
 Кодом сущности для Товара в составе JSON API является ключевое слово **product**. Больше о Товарах и работе с ними в основном интерфейсе вы можете прочитать в нашей службе поддержки в разделе
 [Товары и склад](https://support.moysklad.ru/hc/ru/sections/200564973-%D0%A2%D0%BE%D0%B2%D0%B0%D1%80%D1%8B-%D0%B8-%D1%81%D0%BA%D0%BB%D0%B0%D0%B4).
По данной сущности можно осуществлять контекстный поиск с помощью специального параметра `search`. Подробнее можно узнать по [ссылке](../#mojsklad-json-api-obschie-swedeniq-kontextnyj-poisk).

Поиск среди объектов товаров на соответствие поисковой строке будет осуществлен по следующим полям:

+ по наименованию товара (name)
+ по коду товара (code)
+ по артикулу (article)

#### Атрибуты сущности

| Название  | Тип | Описание                    | Свойство поля в запросе | Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**meta**              |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные Товара|&mdash;|да
|**id**                |UUID|ID Товара|Только для чтения|да
|**accountId**         |UUID|ID учетной записи|Только для чтения|да
|**owner**         |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные владельца (Сотрудника)|&mdash;|да
|**shared**         |Boolean|Общий доступ|&mdash;|да
|**group**         |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные отдела сотрудника|&mdash;|да
|**syncId**                |UUID|ID синхронизации|После заполнения недоступно для изменения|нет
|**updated**         |DateTime|Момент последнего обновления сущности|Только для чтения|да
|**name**         |String(255)|Наименование Товара|Необходимое при создании|да
|**description**        |String(4096)|Описание Товара|&mdash;|нет
|**code**         |String(255)|Код Товара|&mdash;|нет
|**externalCode**         |String(255)|Внешний код Товара|&mdash;|да
|**archived**        |Boolean|Добавлен ли Товар в архив|&mdash;|да
|**pathName**         |String|Наименование группы, в которую входит Товар|Только для чтения|да
|**vat**         |Int|НДС %|&mdash;|нет
|**vatEnabled**     |Boolean|Включен ли НДС для товара. С помощью этого флага для товара можно выставлять НДС = 0 или НДС = "без НДС". (vat = 0, vatEnabled = false) -> vat = "без НДС", (vat = 0, vatEnabled = true) -> vat = 0%.|&mdash;|да
|**useParentVat**   |Boolean|Использует ли товар НДС с родительской группы|&mdash;|да
|**effectiveVat**         |Int|Реальный НДС %|Только для чтения|нет
|**productFolder**         |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные группы Товара|&mdash;|нет
|**uom**         |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Единицы измерения|&mdash;|нет
|**images**       |Array(Object)|Изображения Комплекта. Изображений у Модификации может быть не более 10. [Подробнее тут](../dictionaries/#suschnosti-towar-towary-atributy-wlozhennyh-suschnostej-izobrazhenie-struktura-i-zagruzka)|&mdash;|нет
|**minPrice**         |Object|Минимальная цена. [Подробнее тут](../dictionaries/#suschnosti-towar-towary-atributy-wlozhennyh-suschnostej-minimal-naq-cena)|&mdash;|нет
|**salePrices**         |Array(Object)|Цены продажи. [Подробнее тут](../dictionaries/#suschnosti-towar-towary-atributy-wlozhennyh-suschnostej-ceny-prodazhi)|&mdash;|нет
|**buyPrice**         |Object|Закупочная цена. [Подробнее тут](../dictionaries/#suschnosti-towar-towary-atributy-wlozhennyh-suschnostej-zakupochnaq-cena)|&mdash;|нет
|**supplier**         |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные контрагента-поставщика|&mdash;|нет
|**attributes**         |Array(Object)|Коллекция доп. полей|&mdash;|нет
|**country**         |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные Страны|&mdash;|нет
|**article**         |String(255)|Артикул|&mdash;|нет
|**weight**         |Int|Вес|&mdash;|нет
|**volume**         |Int|Объем|&mdash;|нет
|**packs**         |Array(Object)|Упаковки Товара. [Подробнее тут](../dictionaries/#suschnosti-towar-towary-atributy-wlozhennyh-suschnostej-upakowki-towara)|&mdash;|нет
|**alcoholic**         |Object|Объект, содержащий поля алкогольной продукции. [Подробнее тут](../dictionaries/#suschnosti-towar-towary-atributy-wlozhennyh-suschnostej-ob-ekt-soderzhaschij-polq-alkogol-noj-produkcii)|&mdash;|нет
|**variantsCount**         |Int|Количество модификаций у данного товара|Только для чтения|да
|**minimumBalance**         |Int|Неснижаемый остаток|&mdash;|да
|**isSerialTrackable**         |Boolean|Учет по серийным номерам. Не может быть указан вместе с **alcoholic** и **weighed**|&mdash;|нет
|**things**       |Array(String)|Серийные номера|&mdash;|нет
|**barcodes**         |Array(Object)|Штрихкоды Комплекта. [Подробнее тут](../dictionaries/#suschnosti-towar-towary-atributy-wlozhennyh-suschnostej-shtrihkody)|&mdash;|нет
|**discountProhibited**        |Boolean|Признак запрета скидок|&mdash;|да
|**tnved**         |String(255)|Код ТН ВЭД|&mdash;|нет
|**partialDisposal**         |Boolean|Управление состоянием частичного выбытия маркированного товара. «true» - возможность включена.|&mdash;|нет
|**trackingType**         |Enum|Тип маркируемой продукции. [Подробнее тут](../dictionaries/#suschnosti-towar-towary-atributy-suschnosti-tip-markiruemoj-produkcii)|&mdash;|нет
|**paymentItemType**         |Enum|Признак предмета расчета. [Подробнее тут](../dictionaries/#suschnosti-towar-towary-atributy-suschnosti-priznak-predmeta-rascheta)|&mdash;|нет
|**taxSystem**         |Enum|Код системы налогообложения. [Подробнее тут](../dictionaries/#suschnosti-towar-towary-atributy-suschnosti-kod-sistemy-nalogooblozheniq)|&mdash;|нет
|**ppeType**        |Enum|Код вида номенклатурной классификации медицинских средств индивидуальной защиты (EAN-13). [Подробнее тут](../dictionaries/#suschnosti-towar-towary-atributy-suschnosti-kod-wida-nomenklaturnoj-klassifikacii-medicinskih-sredstw-indiwidual-noj-zaschity)|&mdash;|нет
|**files**              |MetaArray|Массив метаданных [Файлов](../dictionaries/#suschnosti-fajly) (Максимальное количество файлов - 100)|&mdash;|нет|

Атрибут **pathName** сам по себе является атрибутом только для чтения, однако его можно изменить
с помощью обновления атрибута **productFolder**.

##### Тип маркируемой продукции
Значения поля trackingType.

| Значение                | Описание  |
| ------------------------------ |:---------------------------|
| **NOT_TRACKED**           | Без маркировки|
| **TOBACCO**                 |Тип маркировки "Табак"|
| **SHOES**        |Тип маркировки "Обувь"|
| **LP_CLOTHES**        |Тип маркировки "Одежда"|
| **LP_LINENS**        |Тип маркировки "Постельное белье"|
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

##### Код вида номенклатурной классификации медицинских средств индивидуальной защиты
Значения поля ppeType.

| Значение                | Описание  |
| ------------------------------ |:---------------------------|
|**2400001323807** | маска лицевая для защиты дыхательных путей, многоразового использования            
|**2400003675805** | маска лицевая для защиты дыхательных путей, одноразового использования             
|**2400001807703** | респиратор общего применения	                                                     
|**2400001818303** | респиратор хирургический                                                           
|**2400002186203** | респиратор хирургический антибактериальный	                                     
|**2400001368105** | средство назальное для защиты от загрязненного воздуха, местного действия          
|**2400001225408** | перчатки смотровые (процедурные) из латекса гевеи, неопудренные, нестерильные      
|**2400001225606** | перчатки смотровые (процедурные) из латекса гевеи, опудренные                      
|**2400001226108** | перчатки смотровые (процедурные) из латекса гевеи, неопудренные, стерильные	     
|**2400001393503** | перчатки смотровые (процедурные) из полихлоропрена, неопудренные                   
|**2400001858309** | перчатки смотровые (процедурные) нитриловые, неопудренные, нестерильные	         
|**2400001858507** | перчатки смотровые (процедурные) нитриловые, опудренные	                         
|**2400002052805** | перчатки смотровые (процедурные) виниловые, неопудренные                           
|**2400002052904** | перчатки смотровые (процедурные) виниловые, опудренные	                         
|**2400002984502** | перчатки смотровые (процедурные) из гваюлового латекса, неопудренные	             
|**2400003117107** | перчатки смотровые (процедурные) из этиленвинилацетата, неопудренные, стерильные   
|**2400003117206** | перчатки смотровые (процедурные) из этиленвинилацетата, неопудренные, нестерильные 
|**2400003207907** | перчатки смотровые (процедурные) нитриловые, неопудренные, антибактериальные	     
|**2400003215308** | перчатки смотровые (процедурные) полиизопреновые, неопудренные	                 
|**2400003297700** | перчатки смотровые (процедурные) нитриловые, неопудренные, стерильные	             
|**2400003356704** | перчатки смотровые (процедурные) виниловые, неопудренные, стерильные	             
|**2400003356803** | перчатки смотровые (процедурные) виниловые, опудренные, стерильные	             
|**2400003433108** | перчатки смотровые (процедурные) из латекса гевеи, опудренные, стерильные	         
|**2400003492303** | перчатки смотровые (процедурные) полиизопреновые, опудренные	                     
|**2400003495700** | перчатки смотровые (процедурные) из полихлоропрена, неопудренные, стерильные	     
|**2400003495809** | перчатки смотровые (процедурные) из полихлоропрена, неопудренные, стерильные	     
|**2400003495908** | перчатки смотровые (процедурные) нитриловые, опудренные, стерильные	             
|**2400003496004** | перчатки смотровые (процедурные) полиизопреновые, неопудренные, стерильные	     
|**2400003496103** | перчатки смотровые (процедурные) полиизопреновые, опудренные, стерильные	         
|**2400001226306** | перчатки хирургические из латекса гевеи, неопудренные	                             
|**2400001226405** | перчатки хирургические из латекса гевеи, опудренные	                             
|**2400001393107** | перчатки хирургические из полихлоропрена, неопудренные	                         
|**2400001393602** | перчатки смотровые (процедурные) из полихлоропрена, опудренные	                 
|**2400001565306** | перчатки хирургические из блоксополимера стирола, неопудренные, антибактериальные	 
|**2400001857203** | перчатки хирургические нитриловые, опудренные	                                     
|**2400001857005** | перчатки хирургические нитриловые, неопудренные	                                 
|**2400002015909** | перчатки хирургические полиизопреновые, неопудренные	                             
|**2400002016005** | перчатки хирургические полиизопреновые, неопудренные, антибактериальные            
|**2400002016104** | перчатки хирургические полиизопреновые, опудренные	                             
|**2400003161209** | перчатки хирургические из блоксополимера стирола, неопудренные	                 
|**2400003227806** | перчатки хирургические полимерно-композитные, неопудренные	                     
|**2400003237409** | перчатки хирургические полимерно-композитные, неопудренные	                     
|**2400003263408** | перчатки хирургические из латекса гевеи, неопудренные, антибактериальные	         
|**2400003356902** | перчатки хирургические из гваюлового латекса, неопудренные	                     
|**2400003356902** | перчатки хирургические из полихлоропрена, опудренные	                             
|**2400002886806** | набор гигиенической одежды для посетителей	                                     
|**2400002886707** | комбинезон гигиенический для посетителей	                

#### Атрибуты вложенных сущностей
##### Упаковки Товара:

| Название  | Тип | Описание                    | Свойство поля в запросе | Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:---------
|**id**             |UUID|ID упаковки товара|Только для чтения|да
|**uom**             |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные единиц измерения|&mdash;|да
|**quantity**            |Float|Количество Товаров в упаковке данного вида|Необходимое при создании|да
|**barcodes**         |Array(String)|Массив штрихкодов упаковок товаров. Данный массив может содержать не более одного штрихкода. Если штрихкод в массиве отсутствует, то данное поле не выводится|&mdash;|нет

В версии API 1.2 был удален отдельный ресурс для работы с упаковками товаров. Теперь упаковки - вложенная коллекция.
Для того, чтобы создать новую упаковку для данного товара, нужно в запросе на обновление товара указать ее как элемент
поля **packs**, а в ее составе указать ссылку в формате meta на единицу измерения и количество товаров в упаковке.
Для упаковки товара нельзя указать ссылку на единицу измерения, совпадающую с единицей измерения товара, иначе возникнет ошибка.
При обновлении штрихкодов упаковки в рамках обновления товара, переданная коллекция штрихкодов упаковки полностью заменяет имеющуюся до этого 
коллекцию.
Для обновления списка упаковок товара, необходимо в рамках обновления товара передать новую коллекцию упаковок. Новая коллекия упаковок товара
 полностью заменит старую коллекцию.

##### Метаданные Товаров
Метаданные Товаров содержат информацию о дополнительных полях.

Посмотреть все созданные в основном интерфейсе доп. поля Товаров,
а также все типы цен можно с помощью запроса на получение метаданных Товаров.
Ответ - объект, со следующей структурой:

| Название  | Тип | Описание                    | Обязательное при ответе|
| --------- |:----|:----------------------------|:---------
| **meta**         | Meta        | Метаданные                                                                                                               | да |
| **attributes**   | Array(Object) | Коллекция всех существующих доп. полей Товаров в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye) | да |
| **createShared** | Boolean     | Создавать новые Товары с меткой "Общий"                                                                                  | да |

Структуры объектов отдельных коллекций:

##### Штрихкоды:
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

О работе с доп. полями Товаров можно прочитать [здесь](../#mojsklad-json-api-obschie-swedeniq-rabota-s-dopolnitel-nymi-polqmi)

##### Объект, содержащий поля алкогольной продукции

 Название  | Тип | Описание                    | Свойство поля в запросе | Обязательное при ответе|
| --------- |:----|:----------------------------|:----------------|:------------------------|
|**excise**              |Boolean|Содержит акцизную марку|&mdash;|нет
|**type**              |Int|Код вида продукции|&mdash;|нет
|**strength**              |Float| Крепость|&mdash;|нет
|**volume**              |Float|Объём тары|&mdash;|нет

##### Поставщик Товара:

| Название  | Тип | Описание                    | Свойство поля в запросе | Обязательное при ответе|
| --------- |:----|:----------------------------|:---------------|:-----------------------|
| **meta**  |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)| Метаданные, содержащие ссылку на группу поставщика.|&mdash;| да

Тип поставщика - Контрагент. Описание сущности Контрагент вы можете посмотреть [здесь](../dictionaries/#suschnosti-kontragent)

##### Цены продажи

| Название  | Тип | Описание                    | Свойство поля в запросе | Обязательное при ответе|
| --------- |:----|:----------------------------|:---------------|:-----------------------|
|**value**   |Float|Значение цены| &mdash; | да
|**currency**|[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)| Ссылка на валюту в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye)| &mdash; | да
|**priceType**   |Object|Тип цены| &mdash; | да


##### Закупочная цена

| Название  | Тип | Описание                    | Свойство поля в запросе | Обязательное при ответе|
| --------- |:----|:----------------------------|:---------------|:-----------------------|
**value**   |Float|Значение цены| &mdash; | да
**currency**|[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Ссылка на валюту в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye)| &mdash; | да

##### Минимальная цена

| Название  | Тип | Описание                    | Свойство поля в запросе | Обязательное при ответе|
| --------- |:----|:----------------------------|:---------------|:-----------------------|
**value**   |Float|Значение цены| &mdash; | да
**currency**|[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Ссылка на валюту в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye)| &mdash; | да

##### Изображение: структура и загрузка.
При запросе Товара с изображениями будет выведено json представление этого Товара, содержащее поле **images**. Данное поле является 
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
Для загрузки изображений нужно в теле запроса на [создание](../dictionaries/#suschnosti-towar-sozdat-towar) или [обновление](../dictionaries/#suschnosti-towar-izmenit-towar) товара
указать поле **images** со списком элементов, имеющих следующие атрибуты:

| Название                | Описание  |
| ------------------------------ |:---------------------------|
|**filename** | имя файла с расширением. Например - "банан.png"|
| **content** | Изображение, закодированное в формате Base64.|

Если в запросе на обновление **images** будет содержать пустой массив элементов, то все Изображения у Товара будут удалены, 
т.к. сервер посчитает, что пользователь хочет обновить список Изображений Товара.

Документация API по работе с Изображениями приведена в главе [Изображение](../dictionaries/#suschnosti-izobrazhenie).

##### Группа Товара

| Название  | Тип | Описание                    | Свойство поля в запросе | Обязательное при ответе|
| --------- |:----|:----------------------------|:---------------|:-----------------------|
| **meta**  |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)| Метаданные, содержащие ссылку на группу Товара.|&mdash;| да

Описание сущности Группа вы можете посмотреть [здесь](../dictionaries/#suschnosti-gruppa-towarow)
Обновление этого атрибута также обновит атрибут **pathName**.

##### Весовой товар

| Название  | Тип | Описание                    | Свойство поля в запросе | Обязательное при ответе|
| --------- |:----|:----------------------------|:---------------|:-----------------------|
| **weighed**  |Boolean|Поле, показывающее является ли товар весовым. Если его значение false - поле не отображается.|&mdash;| да

Если в основном интерфейсе у товара стоит отметка об учете его по серийным номерам, выставить значение данного поля на true невозможно.

##### Особенности фильтрации поля archived
Если одновременно осуществляется фильтрация по полям **id** и **archived**, то фильтрация по полю **archived** не учитывается.


### Получить список Товаров 
Запрос на получение всех Товаров для данной учетной записи.
Результат: Объект JSON, включающий в себя поля:

| Название  | Тип | Описание                    |
| --------- |:----|:----------------------------|
**meta** |[Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye)|Метаданные о выдаче,
**context** | [Meta](../#mojsklad-json-api-obschie-swedeniq-metadannye) | Метаданные о сотруднике, выполнившем запрос.
**rows** |Array(Object)|Массив JSON объектов, представляющих собой Товаров.

**Параметры**

| Параметр                | Описание  |
| ------------------------------ |:---------------------------|
|**limit** |  `number` (optional) **Default: 1000** *Example: 1000* Максимальное количество сущностей для извлечения.`Допустимые значения 1 - 1000`.|
|**offset** |  `number` (optional) **Default: 0** *Example: 40* Отступ в выдаваемом списке сущностей.|

> Получить список Товаров

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/product"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление списка Товаров.
  
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
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
    "type": "product",
    "mediaType": "application/json",
    "size": 5,
    "limit": 1000,
    "offset": 0
  },
  "rows": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/26b36824-2c83-11e6-8a84-bae50000001b",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
        "type": "product",
        "mediaType": "application/json"
      },
      "id": "26b36824-2c83-11e6-8a84-bae50000001b",
      "accountId": "6270cd18-2c7f-11e6-8a84-bae500000001",
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
      "updated": "2016-06-07 10:40:48",
      "name": "Тыква",
      "description": "Тыква, Германия",
      "code": "pumpkin1",
      "externalCode": "456pumpkin",
      "archived": false,
      "pathName": "",
      "vat": 18,
      "vatEnabled": true,
      "useParentVat": false,
      "effectiveVat": 18,
      "discountProhibited": false,
      "uom": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/uom/19f1edc0-fc42-4001-94cb-c9ec9c62ec10",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/uom/metadata",
          "type": "uom",
          "mediaType": "application/json"
        }
      },
      "images": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/26b36824-2c83-11e6-8a84-bae50000001b/images",
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
          "value": 3353,
          "currency": {
            "meta": {
              "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/6314188d-2c7f-11e6-8a84-bae500000055",
              "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
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
        },
        {
          "value": 3253,
          "currency": {
            "meta": {
              "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/6314188d-2c7f-11e6-8a84-bae500000055",
              "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
              "type": "currency",
              "mediaType": "application/json"
            }
          },
          "priceType": {
            "meta": {
              "href": "https://online.moysklad.ru/api/remap/1.2/context/companysettings/pricetype/672559f1-cbf3-11e1-9eb9-889ffa6f2222",
              "type": "pricetype",
              "mediaType": "application/json"
            },
            "id": "672559f1-cbf3-11e1-9eb9-889ffa6f2222",
            "name": "Цена для друзей",
            "externalCode": "cbcf493b-55bc-11d9-848a-00112f432222"
          }
        }
      ],
      "supplier": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/6313d1e7-2c7f-11e6-8a84-bae500000051",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
          "type": "counterparty",
          "mediaType": "application/json"
        }
      },
      "attributes": [
        {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata/attributes/0c2e54cd-2c80-11e6-8a84-bae50000009c",
            "type": "attributemetadata",
            "mediaType": "application/json"
          },
          "id": "0c2e54cd-2c80-11e6-8a84-bae50000009c",
          "name": "Экспорт",
          "type": "boolean",
          "value": true
        },
        {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata/attributes/0c2e5dc5-2c80-11e6-8a84-bae50000009d",
            "type": "attributemetadata",
            "mediaType": "application/json"
          },
          "id": "0c2e5dc5-2c80-11e6-8a84-bae50000009d",
          "name": "Изготовитель",
          "type": "string",
          "value": "фермерское хозяйство \"Петрович\""
        }
      ],
      "buyPrice": {
        "value": 54,
        "currency": {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/6314188d-2c7f-11e6-8a84-bae500000055",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
            "type": "currency",
            "mediaType": "application/json"
          }
        }
      },
      "article": "Ar23",
      "weight": 200,
      "volume": 300,
      "variantsCount": 0,
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
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/d950551c-2c7f-11e6-8a84-bae50000000b",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
        "type": "product",
        "mediaType": "application/json"
      },
      "id": "d950551c-2c7f-11e6-8a84-bae50000000b",
      "accountId": "6270cd18-2c7f-11e6-8a84-bae500000001",
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
      "updated": "2016-06-07 10:45:16",
      "name": "Бананы",
      "description": "Бананы, Африка",
      "code": "one1",
      "externalCode": "456",
      "archived": false,
      "pathName": "",
      "vat": 18,
      "vatEnabled": true,
      "useParentVat": false,
      "effectiveVat": 18,
      "discountProhibited": false,
      "uom": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/uom/19f1edc0-fc42-4001-94cb-c9ec9c62ec10",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/uom/metadata",
          "type": "uom",
          "mediaType": "application/json"
        }
      },
      "images": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/d950551c-2c7f-11e6-8a84-bae50000000b/images",
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
          "value": 346347237000,
          "currency": {
            "meta": {
              "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/6314188d-2c7f-11e6-8a84-bae500000055",
              "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
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
        },
        {
          "value": 100,
          "currency": {
            "meta": {
              "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/6314188d-2c7f-11e6-8a84-bae500000055",
              "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
              "type": "currency",
              "mediaType": "application/json"
            }
          },
          "priceType": {
            "meta": {
              "href": "https://online.moysklad.ru/api/remap/1.2/context/companysettings/pricetype/672559f1-cbf3-11e1-9eb9-889ffa6f2222",
              "type": "pricetype",
              "mediaType": "application/json"
            },
            "id": "672559f1-cbf3-11e1-9eb9-889ffa6f2222",
            "name": "Цена для друзей",
            "externalCode": "cbcf493b-55bc-11d9-848a-00112f432222"
          }
        }
      ],
      "supplier": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/6313d1e7-2c7f-11e6-8a84-bae500000051",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
          "type": "counterparty",
          "mediaType": "application/json"
        }
      },
      "attributes": [
        {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata/attributes/0c2e54cd-2c80-11e6-8a84-bae50000009c",
            "type": "attributemetadata",
            "mediaType": "application/json"
          },
          "id": "0c2e54cd-2c80-11e6-8a84-bae50000009c",
          "name": "Экспорт",
          "type": "boolean",
          "value": false
        }
      ],
      "buyPrice": {
        "value": 23553000,
        "currency": {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/6314188d-2c7f-11e6-8a84-bae500000055",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
            "type": "currency",
            "mediaType": "application/json"
          }
        }
      },
      "article": "Ar23",
      "weight": 200,
      "volume": 300,
      "packs": [
        {
          "id": "c6bdee6f-2c83-11e6-8a84-bae5000000a4",
          "uom": {
            "meta": {
              "href": "https://online.moysklad.ru/api/remap/1.2/entity/uom/c6b91d63-2c83-11e6-8a84-bae5000000a1",
              "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/uom/metadata",
              "type": "uom",
              "mediaType": "application/json"
            }
          },
          "quantity": 35
        },
        {
          "id": "c6bdf693-2c83-11e6-8a84-bae5000000a5",
          "uom": {
            "meta": {
              "href": "https://online.moysklad.ru/api/remap/1.2/entity/uom/c6bc9273-2c83-11e6-8a84-bae5000000a3",
              "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/uom/metadata",
              "type": "uom",
              "mediaType": "application/json"
            }
          },
          "quantity": 2000
        }
      ],
      "variantsCount": 0,
      "isSerialTrackable": true,
      "things": [
        "F564X056",
        "F564X057"
      ],
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
      "trackingType": "NOT_TRACKED",
      "taxSystem": "GENERAL_TAX_SYSTEM"
    },
{
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/26b36824-2c83-11e6-8a84-bae50000031b",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
        "type": "product",
        "mediaType": "application/json"
      },
      "id": "26b36824-2c83-11e6-8a84-bae50000031b",
      "accountId": "6270cd18-2c7f-11e6-8a84-bae500000001",
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
      "updated": "2016-06-07 10:40:48",
      "name": "Маска",
      "description": "Маска, Гигиеническая",
      "code": "mask1",
      "externalCode": "mask4433",
      "archived": false,
      "pathName": "",
      "vat": 20,
      "vatEnabled": true,
      "useParentVat": false,
      "effectiveVat": 20,
      "discountProhibited": false,
      "uom": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/uom/19f1edc0-fc42-4001-94cb-c9ec9c62ec10",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/uom/metadata",
          "type": "uom",
          "mediaType": "application/json"
        }
      },
      "salePrices": [
        {
          "value": 2600,
          "currency": {
            "meta": {
              "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/6314188d-2c7f-11e6-8a84-bae500000255",
              "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
              "type": "currency",
              "mediaType": "application/json"
            }
          },
          "priceType": {
            "meta": {
              "href": "https://online.moysklad.ru/api/remap/1.2/context/companysettings/pricetype/672559f1-cbf3-11e1-9eb9-889ffa6f23fd",
              "type": "pricetype",
              "mediaType": "application/json"
            },
            "id": "672559f1-cbf3-11e1-9eb9-889ffa6f23fd",
            "name": "Цена продажи",
            "externalCode": "cbcf493b-55bc-11d9-848a-00113333529a"
          }
        }
      ],
      "buyPrice": {
        "value": 12,
        "currency": {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/6314188d-2c7f-11e6-8a84-bae500002255",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
            "type": "currency",
            "mediaType": "application/json"
          }
        }
      },
      "article": "kk212k",
      "weight": 1,
      "volume": 1,
      "variantsCount": 0,
      "barcodes": [
        {
          "ean13": "2000000000000"
        }
      ],
      "ppeType" : "2400001323807"
    }
  ]
}
```

### Создать Товар 
Создать новый Товар.
#### Описание
Товар создается на основе переданного объекта JSON,
который содержит представление нового Товара.
Результат - JSON представление созданного Товара. Для создания нового Товара,
необходимо и достаточно указать в переданном объекте не пустое поле `name`.
Если вы хотите создать алкогольный товар, то в теле запроса, нужно передать
объект **alcoholic**, у которого как минимум одна из нижеперечисленных характеристик будет передана с значением. 
Иначе, при передаче пустого объекта **alcoholic**, он будет проигнорирован,и товар создастся без пометки "Алкогольная продукция".

| Название                | Описание  |
| ------------------------------ |:---------------------------|
|**excise** | Содержит акцизную марку
| **type**  | Код вида продукции
| **strength** | Крепость
| **volume** | Объем тары

Будет передана с значением. Иначе, при передаче пустого объекта **alcoholic**,
он будет проигнорирован, и товар создастся без пометки "Алкогольная продукция".

При создании Товара с указанным массивом штрихкодов для каждого штрихкода требуется указать к какому типу относится штрихкод. 
Например, чтобы создать штрихкод с типом Code 128, в массив штрихкодов должен быть добавлен JSON-объект с полем code128 со значением штрихкода.

> Пример наиболее полного по количеству полей запроса.
  
  ```shell
  curl -X POST
    "https://online.moysklad.ru/api/remap/1.2/entity/product"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "name": "Бананы",
            "code": "one1",
            "externalCode": "456",
            "description": "Бананы, Африка",
            "vat": 18,
            "effectiveVat": 18,
            "discountProhibited": false,
            "uom": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/uom/19f1edc0-fc42-4001-94cb-c9ec9c62ec10",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/uom/metadata",
                "type": "uom",
                "mediaType": "application/json"
              }
            },
            "supplier": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/2b5095a4-296b-11e6-8a84-bae500000051",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
                "type": "counterparty",
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
            "buyPrice": {
              "value": 23553000,
              "currency": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/2b50da23-296b-11e6-8a84-bae500000055",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
                  "type": "currency",
                  "mediaType": "application/json"
                }
              }
            },
            "salePrices": [
              {
                "value": 346347237000,
                "currency": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/2b50da23-296b-11e6-8a84-bae500000055",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
                    "type": "currency",
                    "mediaType": "application/json"
                  }
                },
                "priceType": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/context/companysettings/pricetype/672559f1-cbf3-11e1-9eb9-889ffa6f49fd",
                    "type": "pricetype",
                    "mediaType": "application/json"
                  }
                }
              },
              {
                "value": 100,
                "currency": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/2b50da23-296b-11e6-8a84-bae500000055",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
                    "type": "currency",
                    "mediaType": "application/json"
                  }
                },
                "priceType": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/context/companysettings/pricetype/672559f1-cbf3-11e1-9eb9-889ffa6f2222",
                    "type": "pricetype",
                    "mediaType": "application/json"
                  }
                }
              }
            ],
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
            "article": "Ar23",
            "weight": 200,
            "volume": 300,
            "packs": [
              {
                "uom": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/uom/2ec1170c-3f69-4409-87bb-c68e0011b275",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/uom/metadata",
                    "type": "uom",
                    "mediaType": "application/json"
                  }
                },
                "quantity": 2
              }
            ],
            "isSerialTrackable": false,
            "trackingType": "NOT_TRACKED"
          }'  
  ```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление созданного Товара.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/a355f431-29a1-11e6-8a84-bae500000009",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
    "type": "product",
    "mediaType": "application/json"
  },
  "id": "a355f431-29a1-11e6-8a84-bae500000009",
  "accountId": "2aa3f5df-296b-11e6-8a84-bae500000001",
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
  "updated": "2016-06-03 18:41:28",
  "name": "Бананы",
  "description": "Бананы, Африка",
  "code": "one1",
  "externalCode": "456",
  "archived": false,
  "pathName": "",
  "vat": 18,
  "vatEnabled": true,
  "useParentVat": false,
  "effectiveVat": 18,
  "discountProhibited": false,
  "uom": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/uom/19f1edc0-fc42-4001-94cb-c9ec9c62ec10",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/uom/metadata",
      "type": "uom",
      "mediaType": "application/json"
    }
  },
  "images": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/a355f431-29a1-11e6-8a84-bae500000009/images",
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
      "value": 346347237000,
      "currency": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/2b50da23-296b-11e6-8a84-bae500000055",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
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
    },
    {
      "value": 100,
      "currency": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/2b50da23-296b-11e6-8a84-bae500000055",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
          "type": "currency",
          "mediaType": "application/json"
        }
      },
      "priceType": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/context/companysettings/pricetype/672559f1-cbf3-11e1-9eb9-889ffa6f2222",
          "type": "pricetype",
          "mediaType": "application/json"
        },
        "id": "672559f1-cbf3-11e1-9eb9-889ffa6f2222",
        "name": "Цена для друзей",
        "externalCode": "cbcf493b-55bc-11d9-848a-00112f432222"
      }
    }
  ],
  "supplier": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/2b5095a4-296b-11e6-8a84-bae500000051",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
      "mediaType": "application/json"
    }
  },
  "buyPrice": {
    "value": 23553000,
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/2b50da23-296b-11e6-8a84-bae500000055",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json"
      }
    }
  },
  "article": "Ar23",
  "weight": 200,
  "volume": 300,
  "packs": [
    {
      "id": "a97af44b-8b46-11e8-56c0-00080000000d",
      "uom": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/uom/2ec1170c-3f69-4409-87bb-c68e0011b275",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/uom/metadata",
          "type": "uom",
          "mediaType": "application/json"
        }
      },
      "quantity": 2
    }
  ],
  "isSerialTrackable": false,
  "trackingType": "NOT_TRACKED"
}
```

> Пример запроса на создание Товара с единственным необходимым полем.
  
  ```shell
  curl -X POST
    "https://online.moysklad.ru/api/remap/1.2/entity/product"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "name": "Мандарины"
          }'  
  ```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление созданного Товара.
  
  ```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/04996e84-29a1-11e6-8a84-bae500000002",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
    "type": "product",
    "mediaType": "application/json"
  },
  "id": "04996e84-29a1-11e6-8a84-bae500000002",
  "accountId": "2aa3f5df-296b-11e6-8a84-bae500000001",
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
  "images": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/04996e84-29a1-11e6-8a84-bae500000002/images",
      "type": "image",
      "mediaType": "application/json",
      "size": 0,
      "limit": 1000,
      "offset": 0
    }
  },
  "salePrices": [
    {
      "value": 346347237000,
      "currency": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/2b50da23-296b-11e6-8a84-bae500000055",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
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
    },
    {
      "value": 100,
      "currency": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/2b50da23-296b-11e6-8a84-bae500000055",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
          "type": "currency",
          "mediaType": "application/json"
        }
      },
      "priceType": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/context/companysettings/pricetype/672559f1-cbf3-11e1-9eb9-889ffa6f2222",
          "type": "pricetype",
          "mediaType": "application/json"
        },
        "id": "672559f1-cbf3-11e1-9eb9-889ffa6f2222",
        "name": "Цена для друзей",
        "externalCode": "cbcf493b-55bc-11d9-848a-00112f432222"
      }
    }
  ],
  "updated": "2016-06-03 18:37:02",
  "name": "Мандарины",
  "code": "00003",
  "externalCode": "Cf0ehavIglre6sMX-J2rR2",
  "archived": false,
  "pathName": "",
  "weight": 0,
  "volume": 0,
  "isSerialTrackable": false,
  "trackingType": "NOT_TRACKED",
  "vatEnabled": false,
  "useParentVat": true
}
```

> Пример запроса на создание Товара с доп. полями.
  
  ```shell
  curl -X POST
    "https://online.moysklad.ru/api/remap/1.2/entity/product"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "name": "Тыква",
            "code": "pumpkin1",
            "externalCode": "456pumpkin",
            "description": "Тыква, Германия",
            "vat": 18,
            "effectiveVat": 18,
            "uom": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/uom/19f1edc0-fc42-4001-94cb-c9ec9c62ec10",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/uom/metadata",
                "type": "uom",
                "mediaType": "application/json"
              }
            },
            "supplier": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/6313d1e7-2c7f-11e6-8a84-bae500000051",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
                "type": "counterparty",
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
            "buyPrice": {
              "value": 54,
              "currency": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/6314188d-2c7f-11e6-8a84-bae500000055",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
                  "type": "currency",
                  "mediaType": "application/json"
                }
              }
            },
            "salePrices": [
              {
                "value": 3353,
                "currency": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/6314188d-2c7f-11e6-8a84-bae500000055",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
                    "type": "currency",
                    "mediaType": "application/json"
                  }
                },
                "priceType": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/context/companysettings/pricetype/672559f1-cbf3-11e1-9eb9-889ffa6f49fd",
                    "type": "pricetype",
                    "mediaType": "application/json"
                  }
                }
              },
              {
                "value": 3253,
                "currency": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/6314188d-2c7f-11e6-8a84-bae500000055",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
                    "type": "currency",
                    "mediaType": "application/json"
                  }
                },
                "priceType": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/context/companysettings/pricetype/672559f1-cbf3-11e1-9eb9-889ffa6f2222",
                    "type": "pricetype",
                    "mediaType": "application/json"
                  }
                }
              }
            ],
            "article": "Ar23",
            "weight": 200,
            "volume": 300,
            "attributes": [
              {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata/attributes/0c2e54cd-2c80-11e6-8a84-bae50000009c",
                  "type": "attributemetadata",
                  "mediaType": "application/json"
                },
                "name": "Экспорт",
                "value": true
              },
              {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata/attributes/0c2e5dc5-2c80-11e6-8a84-bae50000009d",
                  "type": "attributemetadata",
                  "mediaType": "application/json"
                },
                "name": "Изготовитель",
                "value": "фермерское хозяйство \"Петрович\" "
              },
              {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata/attributes/0f1e750e-e1b2-11e7-9464-e4de00000003",
                  "type": "attributemetadata",
                  "mediaType": "application/json"
                },
                "name": "not strange attribute name",
                "type": "file",
                "file": {
                  "filename": "filename",
                  "content": "5cYwMpOmNk5kSVr4YgZGKtXJb/7KpHVLDUawyZrD5Nf0WDhB7mS1I77VcAMqYQ8DkP/1wDLhb0X6b2JO4pdpKA=="
                }
              }
            ]
          }'  
  ```
  
> Response 200 (application/json)
Успешный запрос. Результат - JSON представление созданного Товара.
 
```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/26b36824-2c83-11e6-8a84-bae50000001b",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
    "type": "product",
    "mediaType": "application/json"
  },
  "id": "26b36824-2c83-11e6-8a84-bae50000001b",
  "accountId": "6270cd18-2c7f-11e6-8a84-bae500000001",
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
  "updated": "2016-06-07 10:40:48",
  "name": "Тыква",
  "description": "Тыква, Германия",
  "code": "pumpkin1",
  "externalCode": "456pumpkin",
  "archived": false,
  "pathName": "",
  "vat": 18,
  "vatEnabled": true,
  "useParentVat": false,
  "effectiveVat": 18,
  "discountProhibited": false,
  "uom": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/uom/19f1edc0-fc42-4001-94cb-c9ec9c62ec10",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/uom/metadata",
      "type": "uom",
      "mediaType": "application/json"
    }
  },
  "images": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/26b36824-2c83-11e6-8a84-bae50000001b/images",
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
      "value": 3353,
      "currency": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/6314188d-2c7f-11e6-8a84-bae500000055",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
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
    },
    {
      "value": 3253,
      "currency": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/6314188d-2c7f-11e6-8a84-bae500000055",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
          "type": "currency",
          "mediaType": "application/json"
        }
      },
      "priceType": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/context/companysettings/pricetype/672559f1-cbf3-11e1-9eb9-889ffa6f2222",
          "type": "pricetype",
          "mediaType": "application/json"
        },
        "id": "672559f1-cbf3-11e1-9eb9-889ffa6f2222",
        "name": "Цена для друзей",
        "externalCode": "cbcf493b-55bc-11d9-848a-00112f432222"
      }
    }
  ],
  "supplier": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/6313d1e7-2c7f-11e6-8a84-bae500000051",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
      "mediaType": "application/json"
    }
  },
  "attributes": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata/attributes/0c2e54cd-2c80-11e6-8a84-bae50000009c",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "0c2e54cd-2c80-11e6-8a84-bae50000009c",
      "name": "Экспорт",
      "type": "boolean",
      "value": true
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata/attributes/0c2e5dc5-2c80-11e6-8a84-bae50000009d",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "0c2e5dc5-2c80-11e6-8a84-bae50000009d",
      "name": "Изготовитель",
      "type": "string",
      "value": "фермерское хозяйство \"Петрович\""
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata/attributes/0f1e750e-e1b2-11e7-9464-e4de00000003",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "0f1e750e-e1b2-11e7-9464-e4de00000003",
      "name": "not strange attribute name",
      "type": "file",
      "value": "filename",
      "download": {
        "href": "https://online.moysklad.ru/api/remap/1.2/download/00664f3a-e3da-11e7-9464-e4de00000000",
        "mediaType": "application/octet-stream"
      }
    }
  ],
  "buyPrice": {
    "value": 54,
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/6314188d-2c7f-11e6-8a84-bae500000055",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json"
      }
    }
  },
  "article": "Ar23",
  "weight": 200,
  "volume": 300,
  "isSerialTrackable": false,
  "trackingType": "NOT_TRACKED"
}
```

> Пример запроса на создание Товара с загрузкой изображения.
  
  ```shell
  curl -X POST
    "https://online.moysklad.ru/api/remap/1.2/entity/product"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "name": "testimage",
            "images": [
              {
                "filename": "birdimage.png",
                "content": "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"
              }
            ]
          }'  
  ```
  
> Response 200 (application/json)
Успешный запрос. Результат - JSON представление созданного Товара с изображением.
  
  ```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/bd1c0a3e-95ee-11e6-8a84-bae500000004",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
    "type": "product",
    "mediaType": "application/json"
  },
  "id": "bd1c0a3e-95ee-11e6-8a84-bae500000004",
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
  "updated": "2016-10-19 14:25:28",
  "name": "testimage",
  "code": "00006",
  "externalCode": "0bmPIvHxgEDlNIZrZ6GLt2",
  "archived": false,
  "pathName": "",
  "images": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/bd1c0a3e-95ee-11e6-8a84-bae500000004/images",
      "type": "image",
      "mediaType": "application/json",
      "size": 1,
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
  "buyPrice": {
    "value": 0
  },
  "weight": 0,
  "volume": 0,
  "barcodes": [
    {
      "ean13": "2000000000107"
    }
  ],
  "variantsCount": 0,
  "isSerialTrackable": false,
  "trackingType": "NOT_TRACKED",
  "vatEnabled": false,
  "useParentVat": true,
}
```

### Массовое создание и обновление товаров 
[Массовое создание и обновление](../#mojsklad-json-api-obschie-swedeniq-sozdanie-i-obnowlenie-neskol-kih-ob-ektow) товаров.
В теле запроса нужно передать массив, содержащий JSON представления товаров, которые вы хотите создать или обновить.
Обновляемые товары должны содержать идентификатор в виде метаданных.

> Пример создания и обновления нескольких товаров
  
```shell
  curl -X POST
    "https://online.moysklad.ru/api/remap/1.2/entity/product
"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '[
            {
              "name": "Мандарины"
            },
            {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/26b36824-2c83-11e6-8a84-bae50000001b",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                "type": "product",
                "mediaType": "application/json"
              },
              "name": "Брюква",
              "description": "Брюква, Брюссель"
            }
          ]'  
  ```

> Response 200 (application/json)
Успешный запрос. Результат - массив JSON представлений созданных и обновленных товаров.

```json
[
  {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/04996e84-29a1-11e6-8a84-bae500000002",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
      "type": "product",
      "mediaType": "application/json"
    },
    "id": "04996e84-29a1-11e6-8a84-bae500000002",
    "accountId": "2aa3f5df-296b-11e6-8a84-bae500000001",
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
    
    "salePrices": [
      {
        "value": 346347237000,
        "currency": {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/2b50da23-296b-11e6-8a84-bae500000055",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
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
      },
      {
        "value": 100,
        "currency": {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/2b50da23-296b-11e6-8a84-bae500000055",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
            "type": "currency",
            "mediaType": "application/json"
          }
        },
        "priceType": {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/context/companysettings/pricetype/672559f1-cbf3-11e1-9eb9-889ffa6f2222",
            "type": "pricetype",
            "mediaType": "application/json"
          },
          "id": "672559f1-cbf3-11e1-9eb9-889ffa6f2222",
          "name": "Цена для друзей",
          "externalCode": "cbcf493b-55bc-11d9-848a-00112f432222"
        }
      }
    ],
    "updated": "2016-06-03 18:37:02",
    "name": "Мандарины",
    "code": "00003",
    "externalCode": "Cf0ehavIglre6sMX-J2rR2",
    "archived": false,
    "pathName": "",
    "images": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/04996e84-29a1-11e6-8a84-bae500000002/images",
        "type": "image",
        "mediaType": "application/json",
        "size": 0,
        "limit": 1000,
        "offset": 0
      }
    },  
    "weight": 0,
    "volume": 0,
    "isSerialTrackable": false,
    "trackingType": "NOT_TRACKED",
    "vatEnabled": false,
    "useParentVat": true,
  },
  {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/26b36824-2c83-11e6-8a84-bae50000001b",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
      "type": "product",
      "mediaType": "application/json"
    },
    "id": "26b36824-2c83-11e6-8a84-bae50000001b",
    "accountId": "6270cd18-2c7f-11e6-8a84-bae500000001",
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
    "updated": "2016-06-07 11:00:37",
    "name": "Брюква",
    "description": "Брюква, Брюссель",
    "code": "pumpkin1",
    "externalCode": "456pumpkin",
    "archived": false,
    "pathName": "",
    "vat": 3,
    "vatEnabled": true,
    "useParentVat": false,
    "effectiveVat": 3,
    "discountProhibited": false,
    "uom": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/uom/19f1edc0-fc42-4001-94cb-c9ec9c62ec10",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/uom/metadata",
        "type": "uom",
        "mediaType": "application/json"
      }
    },
    "images": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/26b36824-2c83-11e6-8a84-bae50000001b/images",
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
        "value": 3753,
        "currency": {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/6314188d-2c7f-11e6-8a84-bae500000055",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
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
      },
      {
        "value": 3653,
        "currency": {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/6314188d-2c7f-11e6-8a84-bae500000055",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
            "type": "currency",
            "mediaType": "application/json"
          }
        },
        "priceType": {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/context/companysettings/pricetype/672559f1-cbf3-11e1-9eb9-889ffa6f2222",
            "type": "pricetype",
            "mediaType": "application/json"
          },
          "id": "672559f1-cbf3-11e1-9eb9-889ffa6f2222",
          "name": "Цена для друзей",
          "externalCode": "cbcf493b-55bc-11d9-848a-00112f432222"
        }
      }
    ],
    "supplier": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/6313f1eb-2c7f-11e6-8a84-bae500000053",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
        "type": "counterparty",
        "mediaType": "application/json"
      }
    },
    "attributes": [
      {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata/attributes/0c2e54cd-2c80-11e6-8a84-bae50000009c",
          "type": "attributemetadata",
          "mediaType": "application/json"
        },
        "id": "0c2e54cd-2c80-11e6-8a84-bae50000009c",
        "name": "Экспорт",
        "type": "boolean",
        "value": false
      },
      {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata/attributes/0c2e5dc5-2c80-11e6-8a84-bae50000009d",
          "type": "attributemetadata",
          "mediaType": "application/json"
        },
        "id": "0c2e5dc5-2c80-11e6-8a84-bae50000009d",
        "name": "Изготовитель",
        "type": "string",
        "value": "Колхоз \"Иваново\""
      }
    ],
    "country": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/country/0238a888-c602-4e78-a199-d8f49c4d6c18",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/country/metadata",
        "type": "country",
        "mediaType": "application/json"
      }
    },
    "buyPrice": {
      "value": 54,
      "currency": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/6314188d-2c7f-11e6-8a84-bae500000055",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
          "type": "currency",
          "mediaType": "application/json"
        }
      }
    },
    "article": "Ar23",
    "weight": 100,
    "volume": 400,
    "packs": [
      {
        "id": "354ba98c-2cb9-11e6-8a84-bae5000000e3",
        "uom": {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/uom/2d1fdd55-d935-4d55-80d4-f6904b62ff46",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/uom/metadata",
            "type": "uom",
            "mediaType": "application/json"
          }
        },
        "quantity": 40
      },
      {
        "id": "354ba98c-2cb9-11e6-8a84-bae5000004e3",
        "uom": {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/uom/0dd4fe8b-e59e-486e-bde5-b52fe0e25415",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/uom/metadata",
            "type": "uom",
            "mediaType": "application/json"
          }
        },
        "quantity": 101
      }
    ],
    "barcodes": [
      {
        "code128": "code128barcode"
      }
    ],
    "alcoholic": {
      "excise": true,
      "type": 3100,
      "strength": 0.6,
      "volume": 1.5
    },
    "isSerialTrackable": false,
    "trackingType": "NOT_TRACKED"
  }
]

```


### Удалить Товар

**Параметры**

|Параметр   | Описание  | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Товара.|
 
> Запрос на удаление Товара с указанным id.

```shell
curl -X DELETE
  "https://online.moysklad.ru/api/remap/1.2/entity/product/7944ef04-f831-11e5-7a69-971500188b19"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешное удаление Товара.

### Массовое удаление Товаров

В теле запроса нужно передать массив, содержащий JSON метаданных Товаров, которые вы хотите удалить.


> Запрос на массовое удаление Товаров. 

```shell
curl -X POST
  "https://online.moysklad.ru/api/remap/1.2/entity/product/delete"
  -H "Authorization: Basic <Credentials>"
  -H "Content-Type: application/json"
  -d '[
        {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/7944ef04-f831-11e5-7a69-971500188b1",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
            "type": "product",
            "mediaType": "application/json"
        },
        {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/7944ef04-f831-11e5-7a69-971500188b2",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
            "type": "product",
            "mediaType": "application/json"
        }
      ]'
```        

> Успешный запрос. Результат - JSON информация об удалении Товаров.

```json
[
  {
    "info":"Сущность 'product' с UUID: 7944ef04-f831-11e5-7a69-971500188b1 успешно удалена"
  },
  {
    "info":"Сущность 'product' с UUID: 7944ef04-f831-11e5-7a69-971500188b2 успешно удалена"
  }
]
```  


### Метаданные Товаров 
#### Метаданные Товаров 
Запрос на получение метаданных Товаров. Результат - объект JSON, включающий в себя:

|Название|Описание| 
|:----|:----|
|**meta**   |Метаданные   |
|**attributes**   |коллекция всех существующих доп. полей Товаров в формате [Метаданных](../#mojsklad-json-api-obschie-swedeniq-metadannye)   |
|**createShared**   |создавать новые комплекты с меткой "Общий"   |

Структура отдельного объекта, представляющего доп. поле подробно описана в разделе [Работа с дополнительными полями](../#mojsklad-json-api-obschie-swedeniq-rabota-s-dopolnitel-nymi-polqmi).

> Метаданные Товаров

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление доп. полей Товаров.
  
```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/product",
    "mediaType": "application/json"
  },
  "attributes": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata/attributes/0c2e54cd-2c80-11e6-8a84-bae50000009c",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "0c2e54cd-2c80-11e6-8a84-bae50000009c",
      "name": "Экспорт",
      "type": "boolean",
      "required": false
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata/attributes/0c2e5dc5-2c80-11e6-8a84-bae50000009d",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "0c2e5dc5-2c80-11e6-8a84-bae50000009d",
      "name": "Изготовитель",
      "type": "string",
      "required": false
    }
  ],
  "createShared": true
}
```

### Отдельное доп. поле

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id**   |`7944ef04-f831-11e5-7a69-971500188b19` (required, string) - id Доп. поля   |

#### Отдельное доп. поле
> Запрос на получение информации по отдельному дополнительному полю.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata/attributes/7944ef04-f831-11e5-7a69-971500188b19"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление отдельного доп. поля.  
  
```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata/attributes/3cd83619-5585-11e6-8a84-bae500000069",
    "type": "attributemetadata",
    "mediaType": "application/json"
  },
  "customEntityMeta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/context/companysettings/metadata/customEntities/a27aa372-5311-11e6-8a84-bae500000001",
    "type": "customentitymetadata",
    "mediaType": "application/json"
  },
  "id": "3cd83619-5585-11e6-8a84-bae500000069",
  "name": "Связанная сущность",
  "type": "customentity",
  "required": false
}
```

### Товар 
Товар, обращение к которому происходит по значению его id.

### Получить Товар

**Параметры**

|Параметр   |Описание   | 
|:----|:----|
|**id** |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Товара.|

> Запрос на получение Товара с указанным id.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/product/7944ef04-f831-11e5-7a69-971500188b19"
  -H "Authorization: Basic <Credentials>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление Товара.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/d950551c-2c7f-11e6-8a84-bae50000000b",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
    "type": "product",
    "mediaType": "application/json"
  },
  "id": "d950551c-2c7f-11e6-8a84-bae50000000b",
  "accountId": "6270cd18-2c7f-11e6-8a84-bae500000001",
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
  "updated": "2016-06-07 10:45:16",
  "name": "Бананы",
  "description": "Бананы, Африка",
  "code": "one1",
  "externalCode": "456",
  "archived": false,
  "pathName": "",
  "vat": 18,
  "vatEnabled": true,
  "useParentVat": false,
  "effectiveVat": 18,
  "discountProhibited": false,
  "uom": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/uom/19f1edc0-fc42-4001-94cb-c9ec9c62ec10",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/uom/metadata",
      "type": "uom",
      "mediaType": "application/json"
    }
  },
  "images": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/d950551c-2c7f-11e6-8a84-bae50000000b/images",
      "type": "image",
      "mediaType": "application/json",
      "size": 0,
      "limit": 1000,
      "offset": 0
    }
  },  
  "minPrice": {
    "value": 532000,
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
      "value": 346347237000,
      "currency": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/6314188d-2c7f-11e6-8a84-bae500000055",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
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
    },
    {
      "value": 100,
      "currency": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/6314188d-2c7f-11e6-8a84-bae500000055",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
          "type": "currency",
          "mediaType": "application/json"
        }
      },
      "priceType": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/context/companysettings/pricetype/672559f1-cbf3-11e1-9eb9-889ffa6f2222",
          "type": "pricetype",
          "mediaType": "application/json"
        },
        "id": "672559f1-cbf3-11e1-9eb9-889ffa6f2222",
        "name": "Цена для друзей",
        "externalCode": "cbcf493b-55bc-11d9-848a-00112f432222"
      }
    }
  ],
  "supplier": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/6313d1e7-2c7f-11e6-8a84-bae500000051",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
      "mediaType": "application/json"
    }
  },
  "attributes": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata/attributes/0c2e54cd-2c80-11e6-8a84-bae50000009c",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "0c2e54cd-2c80-11e6-8a84-bae50000009c",
      "name": "Экспорт",
      "type": "boolean",
      "value": false
    }
  ],
  "buyPrice": {
    "value": 23553000,
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/6314188d-2c7f-11e6-8a84-bae500000055",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json"
      }
    }
  },
  "article": "Ar23",
  "weight": 200,
  "volume": 300,
  "packs": [
    {
      "id": "c6bdee6f-2c83-11e6-8a84-bae5000000a4",
      "uom": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/uom/c6b91d63-2c83-11e6-8a84-bae5000000a1",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/uom/metadata",
          "type": "uom",
          "mediaType": "application/json"
        }
      },
      "quantity": 35
    },
    {
      "id": "c6bdf693-2c83-11e6-8a84-bae5000000a5",
      "uom": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/uom/c6bc9273-2c83-11e6-8a84-bae5000000a3",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/uom/metadata",
          "type": "uom",
          "mediaType": "application/json"
        }
      },
      "quantity": 2000
    }
  ],
  "variantsCount": 0,
  "isSerialTrackable": true,
  "trackingType": "NOT_TRACKED",
  "things": [
    "F564X056",
    "F564X057"
  ],
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
```

### Изменить Товар 
Запрос на обновление существующего Товара.
Типы цен в ценах продаж и дополнительные поля обновляются как элементы вложенных коллекций:

+ Если в текущем объекте у какого-то из доп. полей / типов цен нет значения,
а в переданной коллекции оно есть - значение записывается в доп. поле / тип цены.
+ Если же у данного атрибута значение уже присутствует - оно перезаписывается на переданное.
+ Если у данного атрибута в составе объекта значение присутствует, однако оно отсутствует
в передаваемой в теле запроса коллекции (не передается совсем), то значение атрибута объекта не изменяется.

Для обновленя полей алкогольной продукции в теле запроса на обновление товара должен присутствовать объект **alcoholic**,
с вложенными в него полями, отражающими свойства алкогольной продукции:

| Название                | Описание  |
| ------------------------------ |:---------------------------|
|**excise** | Содержит акцизную марку
| **type**  | Код вида продукции
| **strength** | Крепость
| **volume** | Объем тары

Если в запросе на обновление товара, являющегося алкогольной продукцией, передать пустой объект **alcoholic**, с данного объекта
снимется отметка "Алкогольная продукция". Для того чтобы сделать товар, не являющийся алкогольной продукцией алкогольным, нужно в теле запроса
передать объект **alcoholic**, у которого хотя бы одно из свойств будет иметь значение.

При обновлении Товара с указанным массивом штрихкодов для каждого штрихкода требуется указать к какому типу относится штрихкод. 
Например, чтобы создать штрихкод с типом Code 128, в массив штрихкодов должен быть добавлен JSON-объект с полем code128 со значением штрихкода.

При включенном в основном интерфейсе серийном учете товаров, в запросе на обновление нельзя передать значение true полю **weighed**,
иначе возникнет ошибка, т.к. невозможен серийный учет весовых товаров.

> Пример запроса на обновление Товара
  
```shell
  curl -X PUT
    "https://online.moysklad.ru/api/remap/1.2/entity/product/7944ef04-f831-11e5-7a69-971500188b19"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "name": "Тыква",
            "code": "pumpkin1",
            "externalCode": "456pumpkin",
            "description": "Тыква, Германия",
            "vat": 3,
            "effectiveVat": 3,
            "uom": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/uom/19f1edc0-fc42-4001-94cb-c9ec9c62ec10",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/uom/metadata",
                "type": "uom",
                "mediaType": "application/json"
              }
            },
            "supplier": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/6313f1eb-2c7f-11e6-8a84-bae500000053",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
                "type": "counterparty",
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
            "buyPrice": {
              "value": 54,
              "currency": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/6314188d-2c7f-11e6-8a84-bae500000055",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
                  "type": "currency",
                  "mediaType": "application/json"
                }
              }
            },
            "salePrices": [
              {
                "value": 3753,
                "currency": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/6314188d-2c7f-11e6-8a84-bae500000055",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
                    "type": "currency",
                    "mediaType": "application/json"
                  }
                },
                "priceType": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/context/companysettings/pricetype/672559f1-cbf3-11e1-9eb9-889ffa6f49fd",
                    "type": "pricetype",
                    "mediaType": "application/json"
                  }
                }
              },
              {
                "value": 3653,
                "currency": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/6314188d-2c7f-11e6-8a84-bae500000055",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
                    "type": "currency",
                    "mediaType": "application/json"
                  }
                },
                "priceType": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/context/companysettings/pricetype/672559f1-cbf3-11e1-9eb9-889ffa6f2222",
                    "type": "pricetype",
                    "mediaType": "application/json"
                  }
                }
              }
            ],
            "country": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/country/0238a888-c602-4e78-a199-d8f49c4d6c18",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/country/metadata",
                "type": "country",
                "mediaType": "application/json"
              }
            },
            "article": "Ar23",
            "weight": 100,
            "volume": 400,
            "packs": [
              {
                "id": "354ba98c-2cb9-11e6-8a84-bae5000000e3",
                "uom": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/uom/2d1fdd55-d935-4d55-80d4-f6904b62ff46",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/uom/metadata",
                    "type": "uom",
                    "mediaType": "application/json"
                  }
                },
                "quantity": 40
              },
              {
                "uom": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/uom/0dd4fe8b-e59e-486e-bde5-b52fe0e25415",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/uom/metadata",
                    "type": "uom",
                    "mediaType": "application/json"
                  }
                },
                "quantity": 101
              }
            ],
            "images": [
              {
                "filename":"birdimageNew.png",
                "content":"iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAIAAACQd1PeAAAAA3NCSVQICAjb4U/gAAAAEHRFWHRTb2Z0d2FyZQBTaHV0dGVyY4LQCQAAAAxJREFUCNdj+PePAQAE+gH90KA5ZAAAAABJRU5ErkJggg=="
              }
             ],
            "alcoholic": {
              "excise": true,
              "type": 3100,
              "strength": 0.6,
              "volume": 1.5
            },
            "barcodes": [
              {
                "code128": "code128barcode"
              }
            ]
          }'  
```  
  
> Response 200 (application/json)
Успешный запрос. Результат - JSON представление обновленного Товара.
  
```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/26b36824-2c83-11e6-8a84-bae50000001b",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
    "type": "product",
    "mediaType": "application/json"
  },
  "id": "26b36824-2c83-11e6-8a84-bae50000001b",
  "accountId": "6270cd18-2c7f-11e6-8a84-bae500000001",
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
  "updated": "2016-06-07 11:00:37",
  "name": "Тыква",
  "description": "Тыква, Германия",
  "code": "pumpkin1",
  "externalCode": "456pumpkin",
  "archived": false,
  "pathName": "",
  "vat": 3,
  "vatEnabled": true,
  "useParentVat": false,
  "effectiveVat": 3,
  "discountProhibited": false,
  "uom": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/uom/19f1edc0-fc42-4001-94cb-c9ec9c62ec10",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/uom/metadata",
      "type": "uom",
      "mediaType": "application/json"
    }
  },
  "images": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/26b36824-2c83-11e6-8a84-bae50000001b/images",
      "type": "image",
      "mediaType": "application/json",
      "size": 1,
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
      "value": 3753,
      "currency": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/6314188d-2c7f-11e6-8a84-bae500000055",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
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
    },
    {
      "value": 3653,
      "currency": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/6314188d-2c7f-11e6-8a84-bae500000055",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
          "type": "currency",
          "mediaType": "application/json"
        }
      },
      "priceType": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/context/companysettings/pricetype/672559f1-cbf3-11e1-9eb9-889ffa6f2222",
          "type": "pricetype",
          "mediaType": "application/json"
        },
        "id": "672559f1-cbf3-11e1-9eb9-889ffa6f2222",
        "name": "Цена для друзей",
        "externalCode": "cbcf493b-55bc-11d9-848a-00112f432222"
      }
    }
  ],
  "supplier": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/6313f1eb-2c7f-11e6-8a84-bae500000053",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
      "mediaType": "application/json"
    }
  },
  "attributes": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata/attributes/0c2e54cd-2c80-11e6-8a84-bae50000009c",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "0c2e54cd-2c80-11e6-8a84-bae50000009c",
      "name": "Экспорт",
      "type": "boolean",
      "value": false
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata/attributes/0c2e5dc5-2c80-11e6-8a84-bae50000009d",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "0c2e5dc5-2c80-11e6-8a84-bae50000009d",
      "name": "Изготовитель",
      "type": "string",
      "value": "Колхоз \"Иваново\""
    }
  ],
  "country": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/country/0238a888-c602-4e78-a199-d8f49c4d6c18",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/country/metadata",
      "type": "country",
      "mediaType": "application/json"
    }
  },
  "buyPrice": {
    "value": 54,
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/6314188d-2c7f-11e6-8a84-bae500000055",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json"
      }
    }
  },
  "article": "Ar23",
  "weight": 100,
  "volume": 400,
  "packs": [
    {
      "id": "354ba98c-2cb9-11e6-8a84-bae5000000e3",
      "uom": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/uom/2d1fdd55-d935-4d55-80d4-f6904b62ff46",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/uom/metadata",
          "type": "uom",
          "mediaType": "application/json"
        }
      },
      "quantity": 40
    },
    {
      "id": "354ba98c-2cb9-11e6-8a84-bae5000004e3",
      "uom": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/uom/0dd4fe8b-e59e-486e-bde5-b52fe0e25415",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/uom/metadata",
          "type": "uom",
          "mediaType": "application/json"
        }
      },
      "quantity": 101
    }
  ],
  "barcodes": [
    {
      "code128": "code128barcode"
    }
  ],
  "alcoholic": {
    "excise": true,
    "type": 3100,
    "strength": 0.6,
    "volume": 1.5
  },
  "isSerialTrackable": false,
  "trackingType": "NOT_TRACKED"
}
```

> Пример запроса на изменение Товара с дополнительными полями.
  
```shell
  curl -X PUT
    "https://online.moysklad.ru/api/remap/1.2/entity/product/7944ef04-f831-11e5-7a69-971500188b19"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "name": "Тыква",
            "code": "pumpkin1",
            "externalCode": "456pumpkin",
            "description": "Тыква, Германия",
            "vat": 3,
            "effectiveVat": 3,
            "uom": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/uom/19f1edc0-fc42-4001-94cb-c9ec9c62ec10",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/uom/metadata",
                "type": "uom",
                "mediaType": "application/json"
              }
            },
            "supplier": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/6313f1eb-2c7f-11e6-8a84-bae500000053",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
                "type": "counterparty",
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
            "buyPrice": {
              "value": 54,
              "currency": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/6314188d-2c7f-11e6-8a84-bae500000055",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
                  "type": "currency",
                  "mediaType": "application/json"
                }
              }
            },
            "salePrices": [
              {
                "value": 3753,
                "currency": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/6314188d-2c7f-11e6-8a84-bae500000055",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
                    "type": "currency",
                    "mediaType": "application/json"
                  }
                },
                "priceType": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/context/companysettings/pricetype/672559f1-cbf3-11e1-9eb9-889ffa6f49fd",
                    "type": "pricetype",
                    "mediaType": "application/json"
                  }
                }
              },
              {
                "value": 3653,
                "currency": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/6314188d-2c7f-11e6-8a84-bae500000055",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
                    "type": "currency",
                    "mediaType": "application/json"
                  }
                },
                "priceType": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/context/companysettings/pricetype/672559f1-cbf3-11e1-9eb9-889ffa6f2222",
                    "type": "pricetype",
                    "mediaType": "application/json"
                  }
                }
              }
            ],
            "article": "Ar23",
            "weight": 100,
            "volume": 400,
            "attributes": [
              {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata/attributes/0c2e54cd-2c80-11e6-8a84-bae50000009c",
                  "type": "attributemetadata",
                  "mediaType": "application/json"
                },
                "name": "Экспорт",
                "value": false
              },
              {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata/attributes/0c2e5dc5-2c80-11e6-8a84-bae50000009d",
                  "type": "attributemetadata",
                  "mediaType": "application/json"
                },
                "name": "Изготовитель",
                "value": "Колхоз \"Иваново\" "
              }
            ]
          }'  
```  
  
> Response 200 (application/json)
Успешный запрос. Результат - JSON представление обновленного Товара.
  
  ```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/26b36824-2c83-11e6-8a84-bae50000001b",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
    "type": "product",
    "mediaType": "application/json"
  },
  "id": "26b36824-2c83-11e6-8a84-bae50000001b",
  "accountId": "6270cd18-2c7f-11e6-8a84-bae500000001",
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
  "updated": "2016-06-07 10:52:58",
  "name": "Тыква",
  "description": "Тыква, Германия",
  "code": "pumpkin1",
  "externalCode": "456pumpkin",
  "archived": false,
  "pathName": "",
  "vat": 3,
  "vatEnabled": true,
  "useParentVat": false,
  "effectiveVat": 3,
  "discountProhibited": false,
  "uom": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/uom/19f1edc0-fc42-4001-94cb-c9ec9c62ec10",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/uom/metadata",
      "type": "uom",
      "mediaType": "application/json"
    }
  },
  "images": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/26b36824-2c83-11e6-8a84-bae50000001b/images",
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
      "value": 3753,
      "currency": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/6314188d-2c7f-11e6-8a84-bae500000055",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
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
    },
    {
      "value": 3653,
      "currency": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/6314188d-2c7f-11e6-8a84-bae500000055",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
          "type": "currency",
          "mediaType": "application/json"
        }
      },
      "priceType": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/context/companysettings/pricetype/672559f1-cbf3-11e1-9eb9-889ffa6f2222",
          "type": "pricetype",
          "mediaType": "application/json"
        },
        "id": "672559f1-cbf3-11e1-9eb9-889ffa6f2222",
        "name": "Цена для друзей",
        "externalCode": "cbcf493b-55bc-11d9-848a-00112f432222"
      }
    }
  ],
  "supplier": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/6313f1eb-2c7f-11e6-8a84-bae500000053",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
      "mediaType": "application/json"
    }
  },
  "attributes": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata/attributes/0c2e54cd-2c80-11e6-8a84-bae50000009c",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "0c2e54cd-2c80-11e6-8a84-bae50000009c",
      "name": "Экспорт",
      "type": "boolean",
      "value": false
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata/attributes/0c2e5dc5-2c80-11e6-8a84-bae50000009d",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "0c2e5dc5-2c80-11e6-8a84-bae50000009d",
      "name": "Изготовитель",
      "type": "string",
      "value": "Колхоз \"Иваново\""
    }
  ],
  "buyPrice": {
    "value": 54,
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/6314188d-2c7f-11e6-8a84-bae500000055",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json"
      }
    }
  },
  "article": "Ar23",
  "weight": 100,
  "volume": 400,
  "isSerialTrackable": false,
  "trackingType": "NOT_TRACKED"
}
```

> Пример запроса на изменение Товара с упаковками.

```shell
  curl -X PUT
    "https://online.moysklad.ru/api/remap/1.2/entity/product/7944ef04-f831-11e5-7a69-971500188b19"
    -H "Authorization: Basic <Credentials>"
    -H "Content-Type: application/json"
      -d '{
            "name": "Тыква",
            "code": "pumpkin1",
            "externalCode": "456pumpkin",
            "description": "Тыква, Германия",
            "vat": 3,
            "effectiveVat": 3,
            "uom": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/uom/19f1edc0-fc42-4001-94cb-c9ec9c62ec10",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/uom/metadata",
                "type": "uom",
                "mediaType": "application/json"
              }
            },
            "supplier": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/6313f1eb-2c7f-11e6-8a84-bae500000053",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
                "type": "counterparty",
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
            "buyPrice": {
              "value": 54,
              "currency": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/6314188d-2c7f-11e6-8a84-bae500000055",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
                  "type": "currency",
                  "mediaType": "application/json"
                }
              }
            },
            "salePrices": [
              {
                "value": 3753,
                "currency": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/6314188d-2c7f-11e6-8a84-bae500000055",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
                    "type": "currency",
                    "mediaType": "application/json"
                  }
                },
                "priceType": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/context/companysettings/pricetype/672559f1-cbf3-11e1-9eb9-889ffa6f49fd",
                    "type": "pricetype",
                    "mediaType": "application/json"
                  }
                }
              },
              {
                "value": 3653,
                "currency": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/6314188d-2c7f-11e6-8a84-bae500000055",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
                    "type": "currency",
                    "mediaType": "application/json"
                  }
                },
                "priceType": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/context/companysettings/pricetype/672559f1-cbf3-11e1-9eb9-889ffa6f2222",
                    "type": "pricetype",
                    "mediaType": "application/json"
                  }
                }
              }
            ],
            "article": "Ar23",
            "weight": 100,
            "volume": 400,
            "packs" : [
              {
                "uom": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/uom/19f1edc0-fc42-4001-94cb-c9ec9c62ec10",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/uom/metadata",
                    "type": "uom",
                    "mediaType": "application/json"
                  }
                },
                "quantity": 11,
                "barcodes": [
                  {
                    "code128": "code128barcode"
                  }
                ]
              }
            ]            
          }'  
```  
        
> Response 200 (application/json)
Успешный запрос. Результат - JSON представление обновлённого Товара.
  
  ```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/26b36824-2c83-11e6-8a84-bae50000001b",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
    "type": "product",
    "mediaType": "application/json"
  },
  "id": "26b36824-2c83-11e6-8a84-bae50000001b",
  "accountId": "6270cd18-2c7f-11e6-8a84-bae500000001",
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
  "updated": "2016-06-07 10:52:58",
  "name": "Тыква",
  "description": "Тыква, Германия",
  "code": "pumpkin1",
  "externalCode": "456pumpkin",
  "archived": false,
  "pathName": "",
  "vat": 3,
  "vatEnabled": true,
  "useParentVat": false,
  "effectiveVat": 3,
  "discountProhibited": false,
  "uom": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/uom/19f1edc0-fc42-4001-94cb-c9ec9c62ec10",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/uom/metadata",
      "type": "uom",
      "mediaType": "application/json"
    }
  },
  "images": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/26b36824-2c83-11e6-8a84-bae50000001b/images",
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
      "value": 3753,
      "currency": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/6314188d-2c7f-11e6-8a84-bae500000055",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
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
    },
    {
      "value": 3653,
      "currency": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/6314188d-2c7f-11e6-8a84-bae500000055",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
          "type": "currency",
          "mediaType": "application/json"
        }
      },
      "priceType": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/context/companysettings/pricetype/672559f1-cbf3-11e1-9eb9-889ffa6f2222",
          "type": "pricetype",
          "mediaType": "application/json"
        },
        "id": "672559f1-cbf3-11e1-9eb9-889ffa6f2222",
        "name": "Цена для друзей",
        "externalCode": "cbcf493b-55bc-11d9-848a-00112f432222"
      }
    }
  ],
  "supplier": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/6313f1eb-2c7f-11e6-8a84-bae500000053",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
      "mediaType": "application/json"
    }
  },
  "buyPrice": {
    "value": 54,
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/6314188d-2c7f-11e6-8a84-bae500000055",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json"
      }
    }
  },
  "packs" : [
    {
      "id": "6314188d-2c7f-11e6-8a84-bae500000055",
      "uom": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/uom/19f1edc0-fc42-4001-94cb-c9ec9c62ec10",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/uom/metadata",
          "type": "uom",
          "mediaType": "application/json"
        }
      },
      "quantity": 11,
      "barcodes": [
        {
          "code128": "code128barcode"
        }
      ]
    }
  ],
  "article": "Ar23",
  "weight": 100,
  "volume": 400,
  "isSerialTrackable": false,
  "trackingType": "NOT_TRACKED"
}
```  
