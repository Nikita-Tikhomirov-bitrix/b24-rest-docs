# Получить статус участия текущего пользователя в событии calendar.meeting.status.get

{% note warning "Мы еще обновляем эту страницу" %}

Тут может не хватать некоторых данных — дополним в ближайшее время

{% endnote %}

{% if build == 'dev' %}

{% note alert "TO-DO _не выгружается на prod_" %}

- не указаны типы параметров
- отсутствуют примеры
- отсутствует ответ в случае ошибки

{% endnote %}

{% endif %}

> Scope: [`calendar`](../scopes/permissions.md)
>
> Кто может выполнять метод: любой пользователь

Метод `calendar.meeting.status.get` возвращает статус участия текущего пользователя в событии.

#|
|| **Параметр** | **Описание** ||
|| **eventId**^*^ | Идентификатор события. ||
|#

{% include [Сноска о параметрах](../../_includes/required.md) %}

## Пример

{% list tabs %}

- JS

    ```js
    BX24.callMethod("calendar.meeting.status.get",
        {
            eventId: '651'
        }
    );
    ```

{% endlist %}

{% include [Сноска о примерах](../../_includes/examples.md) %}

## Ответ в случае успеха

Возвращает статус ("Y", "N", "Q").