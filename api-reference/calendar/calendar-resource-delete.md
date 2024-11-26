# Удалить ресурс calendar.resource.delete

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

Метод `calendar.resource.delete` удаляет ресурс.

#|
|| **Параметр** | **Описание** ||
|| **resourceId**^*^ | Идентификатор ресурса. ||
|#

{% include [Сноска о параметрах](../../_includes/required.md) %}

## Пример

{% list tabs %}

- JS

    ```js
    BX24.callMethod("calendar.resource.delete",
        {
            resourceId: 521
        }
    );
    ```

{% endlist %}

{% include [Сноска о примерах](../../_includes/examples.md) %}

## Ответ в случае успеха

Возвращает true, если удаление успешно.