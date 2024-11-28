# Создать подразделение department.add

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

Метод создает подразделение

#|
|| **Параметр** | **Описание** ||
|| **NAME^*^** | наименование подразделения ||
|| **SORT** | параметр сортировки подразделения ||
|| **PARENT** | идентификатор родительского подразделения. ||
|| **UF_HEAD** | идентификатор руководителя подразделения ||
|#

{% include [Сноска о параметрах](../../_includes/required.md) %}

## Примеры кода

{% list tabs %}

- JS

    ```js
    BX24.callMethod(
        'department.add',
        {
            "NAME": "Подразделение",
            "PARENT": 155,
            "UF_HEAD": 1
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
https://my.bitrix24.ru/rest/department.add.json?NAME=Подразделение&PARENT=155&UF_HEAD=1&auth=1b2234a7412080205f4318e42c7298dc
```

## Ответ

> 200 OK

```json
{"result":222}
```