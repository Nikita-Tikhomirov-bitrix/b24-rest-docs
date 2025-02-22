# Завершить звонок и зафиксировать его в статистике telephony.externalcall.finish

{% note warning "Мы еще обновляем эту страницу" %}

Тут может не хватать некоторых данных — дополним в ближайшее время

{% endnote %}

{% if build == 'dev' %}

{% note alert "TO-DO _не выгружается на prod_" %}

- отсутствуют примеры
- отсутствует ответ в случае ошибки

{% endnote %}

{% endif %}

{% include notitle [Скоуп telephony all](./_includes/scope-telephony-all.md) %}

Метод `telephony.externalcall.finish` завершает звонок, фиксирует его в статистике, скрывает у пользователя карточку звонка.

#|
|| **Параметр** / **Тип** | **Описание** ||
|| **CALL_ID**^*^ 
[`string`](../data-types.md) | Идентификатор звонка из метода [telephony.externalcall.register](telephony-external-call-register.md). ||
|| **USER_ID**^*^ 
[`int`](../data-types.md) | Идентификатор пользователя. Ответственный в лиде будет изменен на переданный USER_ID. Ответственный будет меняться только для лида, созданного автоматически при вызове метода [telephony.externalcall.register](telephony-external-call-register.md). Для существующего лида ответственный не меняется. ||
|| **DURATION**^*^ 
[`int`](../data-types.md) | Длительность в сек. ||
|| **COST** 
[`double`](../data-types.md) | Стоимость звонка. ||
|| **COST_CURRENCY** 
[`string`](../data-types.md) | Валюта, в которой указана стоимость звонка. Список валют можно получить методом `crm.currency.list`. ||
|| **STATUS_CODE** 
[`string`](../data-types.md) | Код вызова (смотрите [таблицу кодов вызова](#call-failed-code)) ||
|| **FAILED_REASON** 
[`string`](../data-types.md) | Причина несостоявшегося звонка. ||
|| **RECORD_URL** 
[`string`](../data-types.md) | URL файла (желательно mp3, возможен flac) с записью звонка.
Портал осуществит две попытки скачать запись по указанному адресу. В случае неудачи, запись приложена не будет и никакого уведомления об ошибке отправлено не будет.

{% note info %}

Данный параметр является устаревшим и оставлен исключительно для обратной совместимости. Использовать его крайне не рекомендуется. Для загрузки записи звонка используйте метод [telephony.externalCall.attachRecord](telephony-external-call-attach-record.md).

{% endnote %}
||
|| **VOTE** 
[`int`](../data-types.md) | Оценка звонка пользователем (если АТС поддерживает функционал оценки разговора). ||
|| **ADD_TO_CHAT** 
[`int`](../data-types.md) | Добавлять ли сообщение о совершенном звонке сотруднику Б24 в чат (Возможные значения 0 или 1, по умолчанию 0). ||
|#

{% include [Сноска о параметрах](../../_includes/required.md) %}

{% note info %}

Вместо USER_ID также может принимать USER_PHONE_INNER.

{% endnote %}

## Таблица кодов вызова (CALL_FAILED_CODE) {#call-failed-code}

#|
|| **Код** | **Описание** ||
|| `$MESS["VI_STATUS_200"]` | Успешный звонок ||
|| `$MESS["VI_STATUS_304"]` | Пропущенный звонок ||
|| `$MESS["VI_STATUS_603"]` | Отклонено ||
|| `$MESS["VI_STATUS_603-S"]` | Вызов отменен ||
|| `$MESS["VI_STATUS_403"]` | Запрещено ||
|| `$MESS["VI_STATUS_404"]` | Неверный номер ||
|| `$MESS["VI_STATUS_486"]` | Занято ||
|| `$MESS["VI_STATUS_484"]` | Данное направление недоступно ||
|| `$MESS["VI_STATUS_503"]` | Данное направление недоступно ||
|| `$MESS["VI_STATUS_480"]` | Временно недоступен ||
|| `$MESS["VI_STATUS_402"]` | Недостаточно средств на счету ||
|| `$MESS["VI_STATUS_423"]` | Заблокировано ||
|| `$MESS["VI_STATUS_OTHER"]` | Не определен ||
|#

## Ответ в случае успеха

Метод возвращает массив, аналогичный методу [voximplant.statistic.get](voximplant-statistic-get.md).