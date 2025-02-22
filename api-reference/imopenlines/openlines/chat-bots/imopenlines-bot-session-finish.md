# Завершить диалог imopenlines.bot.session.finish

{% note warning "Мы еще обновляем эту страницу" %}

Тут может не хватать некоторых данных — дополним в ближайшее время

{% endnote %}

{% if build == 'dev' %}

{% note alert "TO-DO _не выгружается на prod_" %}

- отсутствуют примеры

{% endnote %}

{% endif %}

> Scope: [`imopenlines, imbot`](../../../scopes/permissions.md)
>
> Кто может выполнять метод: любой пользователь

Метод завершает текущую сессию.

## Параметры метода

{% include [Сноска о параметрах](../../../../_includes/required.md) %}

#|
|| **Название**
`Тип` | **Пример** | **Описание** | **Ревизия** ||
|| **CHAT_ID^*^**
[`integer`](../../../data-types.md) | `112` | Идентификатор чата | 1 ||
|#

## Примеры

{% include [Пояснение о restCommand](../../../chat-bots/_includes/rest-command.md) %}

{% list tabs %}

- PHP

    ```php
    $result = restCommand(
        'imopenlines.bot.session.finish',
        Array(
            'CHAT_ID' => 112
        ),
        $_REQUEST["auth"]
    );
    ```

{% endlist %}

{% include [Сноска о примерах](../../../../_includes/examples.md) %}

## Ответ в случае успеха

```json
{
    "result": true
}
```

## Ответ в случае ошибки

```json
{
    "error": "CHAT_ID_EMPTY",
    "error_description": "Не передан идентификатор чата"
}
```

### Описание ключей

- `error` — код возникшей ошибки
- `error_description` — краткое описание возникшей ошибки

### Возможные коды ошибок

#|
|| **Код** | **Описание** ||
|| **CHAT_ID_EMPTY** | Не передан идентификатор чата ||
|| **BOT_ID_ERROR** | Неправильный идентификатор чат-бота ||
|#