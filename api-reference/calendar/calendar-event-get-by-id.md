# Просмотреть событие календаря по идентификатору calendar.event.getbyid

{% note warning "Мы еще обновляем эту страницу" %}

Тут может не хватать некоторых данных — дополним в ближайшее время

{% endnote %}

{% if build == 'dev' %}

{% note alert "TO-DO _не выгружается на prod_" %}

- не указаны типы параметров
- отсутствуют примеры
- отсутствует ответ в случае успеха
- отсутствует ответ в случае ошибки

{% endnote %}

{% endif %}

> Scope: [`calendar`](../scopes/permissions.md)
>
> Кто может выполнять метод: любой пользователь

Метод `calendar.event.getbyid` возвращает событие календаря по идентификатору.

#|
|| **Параметр** | **Описание** ||
|| **id**^*^ | Число. Возвращает массив с полями сущности события или `null`. ||
|#

{% include [Сноска о параметрах](../../_includes/required.md) %}

## Пример

{% list tabs %}

- JS

    ```js
    BX24.callMethod("calendar.event.getbyid", {id: 324});
    /*
        * Returns event by its id
        *
        * @param array $params - incoming params:
        * $params['id'] - int, (required) calendar event id
        * @return event or null
        * @throws \Bitrix\Rest\RestException
        *
        * @example (Javascript)
        * BX24.callMethod("calendar.event.getbyid",
        * {
        *     id: 324
        * });
        *
        */
    ```

{% endlist %}

{% include [Сноска о примерах](../../_includes/examples.md) %}