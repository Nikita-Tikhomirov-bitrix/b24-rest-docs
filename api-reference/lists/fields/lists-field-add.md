# Создать поле универсального списка lists.field.add

{% note warning "Мы еще обновляем эту страницу" %}

Тут может не хватать некоторых данных — дополним в ближайшее время

{% endnote %}

{% if build == 'dev' %}

{% note alert "TO-DO _не выгружается на prod_" %}

- нужны правки под стандарт написания
- не указаны типы параметров
- отсутствуют примеры
- отсутствует ответ в случае успеха
- отсутствует ответ в случае ошибки

{% endnote %}

{% endif %}

> Scope: [`lists`](../../scopes/permissions.md)
>
> Кто может выполнять метод: любой пользователь

Метод `lists.field.add` создает поле списка. В случае успешного создания поля ответ `true`, иначе `Exception`.

## Параметры

#|
|| **Параметр** | **Описание** ||
|| **IBLOCK_TYPE_ID**^*^
[`unknown`](../../data-types.md) | `id` типа инфоблока (обязательно):
- **lists** - тип инфоблока списка
- **bitrix_processes** - тип инфоблока процессов
- **lists_socnet** - тип инфоблока списков групп ||
|| **IBLOCK_CODE/IBLOCK_ID**^*^
[`unknown`](../../data-types.md) | код или `id` инфоблока (обязательно) ||
|| **SOCNET_GROUP_ID**^*^
[`unknown`](../../data-types.md) | `id` группы (обязательно, если список создается для группы); ||
|| **FIELDS**
[`unknown`](../../data-types.md) | ключи такие же как при создании поля из интерфейса Битрикс24:
- **NAME**^*^ - название (обязательно)
- **IS_REQUIRED** - метка обязательности
- **MULTIPLE** - метка множественности
- **TYPE**^*^ - тип (обязательно), включая:
    - **S** - Строка
    - **N** - Число
    - **L** - Список
    - **F** - Файл
    - **G** - Привязка к разделам
    - **E** - Привязка к элементам
    - **S:Date** - Дата
    - **S:DateTime** - Дата/Время
    - **S:HTML** - HTML/текст
    - **E:EList** - Привязка к элементам в виде списка. При создании поля с этим типом необходимо обязательно указать `LINK_IBLOCK_ID` - `id` информационного блока, элементы которого будут отображаться в селекторе этого поля.
    - **N:Sequence** - Счетчик
    - **S:Money** - Деньги
    - **S:DiskFile** - Файл (Диск)
    - **S:map_yandex** - Привязка к Яндекс.Карте
    - **S:employee** - Привязка к сотруднику
    - **S:ECrm** - Привязка к элементам CRM
- **SORT** - сортировка
- **DEFAULT_VALUE** - значение по умолчанию
- **LIST** - может использоваться для добавления значений поля типа "Список".
- **LIST_TEXT_VALUES** - может использоваться для добавления значений поля типа "Список" с помощью строки. (Каждая уникальная строчка станет отдельным значением списка)
- **LIST_DEF** - значение по умолчанию для поля типа "Список" (Формат: массив с значением, где значение `id` пункта списка)
- **CODE**^*^ - код (обязательно, если поле является свойством инфоблока)
- **SETTINGS** - все ключи должны присутствовать, иначе будет происходить затирание значениями по умолчанию, включая:
    - **SHOW_ADD_FORM** - показывать в форме добавления
    - **SHOW_EDIT_FORM** - показывать в форме редактирования
    - **ADD_READ_ONLY_FIELD** - только для чтения (форма добавления)
    - **EDIT_READ_ONLY_FIELD** - только для чтения (форма редактирования)
    - **SHOW_FIELD_PREVIEW** - показать поле при формировании ссылки на элемент списка
- **USER_TYPE_SETTINGS** - ключ для передачи пользовательских настроек
- **ROW_COUNT/COL_COUNT** - настройка для полей textarea
- **LINK_IBLOCK_ID** - `id` привязываемого списка (раздела инфоблока) ||
|#

{% include [Сноска о параметрах](../../../_includes/required.md) %}

## Пример

{% list tabs %}

- JS

    ```js
    var params = {
        'IBLOCK_TYPE_ID': 'lists_socnet',
        'IBLOCK_CODE': 'rest_1',
        'SOCNET_GROUP_ID': '7',
        'FIELDS': {
            'NAME': 'List field',
            'IS_REQUIRED': 'Y',
            'MULTIPLE': 'N',
            'TYPE': 'L',
            'SORT': '20',
            'CODE': 'fieldList',
            'LIST_TEXT_VALUES': 'one\ntwo\nthree',
            'SETTINGS': {
                'SHOW_ADD_FORM': 'Y',
                'SHOW_EDIT_FORM': 'Y',
                'ADD_READ_ONLY_FIELD': 'N',
                'EDIT_READ_ONLY_FIELD': 'N',
                'SHOW_FIELD_PREVIEW': 'N'
            }
        }
    };
    BX24.callMethod(
        'lists.field.add',
        params,
        function(result)
        {
            if(result.error())
                alert("Error: " + result.error());
            else
                alert("Success: " + result.data());
        }
    );
    ```

{% endlist %}

{% include [Сноска о примерах](../../../_includes/examples.md) %}