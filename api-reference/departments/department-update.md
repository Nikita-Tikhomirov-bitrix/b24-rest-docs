# Изменить подразделение department.update

{% note warning "Мы еще обновляем эту страницу" %}

Тут может не хватать некоторых данных — дополним в ближайшее время

{% endnote %}

{% if build == 'dev' %}

{% note alert "TO-DO _не выгружается на prod_" %}

- не указаны типы параметров
- отсутствует ответ в случае ошибки
- нет примеров
  
{% endnote %}

{% endif %}

> Scope: [`department`](../scopes/permissions.md)
>
> Кто может выполнять метод: пользователь с правами на изменение структуры

Метод изменяет указанное подразделение

#|
|| **Параметр** | **Описание** ||
|| **ID^*^** | идентификатор подразделения ||
|| **NAME^*^** | наименование подразделения ||
|| **SORT** | параметр сортировки подразделения ||
|| **PARENT** | идентификатор родительского подразделения ||
|| **UF_HEAD** | идентификатор руководителя подразделения ||
|#

{% include [Сноска о параметрах](../../_includes/required.md) %}

## Примеры кода

{% list tabs %}

- JS

    ```js
    BX24.callMethod(
        'department.update',
        {
            "ID": 222,
            "NAME": "Старое подразделение",
            "PARENT": 114,
            "UF_HEAD": 11
        },
        function(result) {
            if (result.error()) {
                console.error(result.error());
            } else {
                console.info(result.data());
            }
        }
    );
    ```

{% endlist %}

## Запрос

```
https://my.bitrix24.ru/rest/department.update.json?ID=222&NAME=Старое подразделение&PARENT=114&UF_HEAD=11&auth=2577a0459ed8f183c996f44f0995ebe5
```

## Ответ

> 200 OK

```json
{"result":true}
```