### Валюта
Поле **rate** - объект, содержащий в себе следующие атрибуты:

+ currency - Ссылка на валюту в формате [Метаданных](/api/remap/1.2/doc/index.html#header-метаданные)
+ value - Текущий курс валюты (выдается, если значение курса отлично от 1)

Вместо ссылки на валюту можно получить объект валюты целиком с помощью параметра запроса `?expand=rate.currency`.