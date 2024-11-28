# Получить доступные для перевода языки catalog.priceTypeLang.getLanguages

{% note warning "Мы еще обновляем эту страницу" %}

Тут может не хватать некоторых данных — дополним в ближайшее время

{% endnote %}

{% if build == 'dev' %}

{% note alert "TO-DO _не выгружается на prod_" %}

- не указана обязательность параметров
- отсутствует ответ в случае ошибки 
- нет примеров на др. языках
  
{% endnote %}

{% endif %}

> Scope: [`catalog`](../../../scopes/permissions.md)
>
> Кто может выполнять метод: любой пользователь

```http
catalog.priceTypeLang.getLanguages()
```

Метод возвращает доступные для перевода языки.

## Параметры

Без параметров.

## Примеры

{% list tabs %}

- JS

    ```js
    BX24.callMethod(
        'catalog.priceTypeLang.getLanguages',
        {},
        function(result)
        {
            if(result.error())
                console.error(result.error().ex);
            else
                console.log(result.data());
        }
    );
    ```

{% endlist %}


{% include [Сноска о примерах](../../../../_includes/examples.md) %}
