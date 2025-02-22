# Получить отчет о выявленных отсутствиях timeman.timecontrol.reports.get

{% note warning "Мы еще обновляем эту страницу" %}

Тут может не хватать некоторых данных — дополним в ближайшее время

{% endnote %}

{% if build == 'dev' %}

{% note alert "TO-DO _не выгружается на prod_" %}

- нужны правки под стандарт написания
- не указаны типы параметров
- отсутствуют примеры

{% endnote %}

{% endif %}

> Scope: [`timeman`](../../scopes/permissions.md)
>
> Кто может выполнять метод: любой пользователь

Метод `timeman.timecontrol.reports.get` для получения отчёта о выявленных отсутствиях.

### Параметры

#|
|| **Параметр** | **Пример** | **Обязательный** | **Описание** ||
|| **USER_ID**^*^
[`unknown`](../../data-types.md) | 2 | Да | Идентификатор пользователя. ||
|| **YEAR**^*^
[`unknown`](../../data-types.md) | 2018 | Да | Год для формирования отчета. ||
|| **MONTH**^*^
[`unknown`](../../data-types.md) | 8 | Да | Месяц для формирования отчета. ||
|| **WORKDAY_HOURS**^**^
[`unknown`](../../data-types.md) | 8 | Нет | Необходимая продолжительность рабочего дня в часах (по-умолчанию 8 часов). ||
|| **IDLE_MINUTES**
[`unknown`](../../data-types.md) | 15 | Нет | Максимальное время отсутствия на рабочем месте, которое не будет учитываться как отсутствие. ||
|#

{% include [Сноска о параметрах](../../../_includes/required.md) %}

^**^ – Параметр `IDLE_MINUTES` доступен только, если вы руководитель или администратор. Если не указывать, время автоматически берется из настроек модуля.

## Пример вызова

{% list tabs %}

- JS

    ```js
    BX24.callMethod('timeman.timecontrol.reports.get', {
        user_id: 2,
        year: 2018,
        month: 8,
        workday_hours: 8,
        idle_minutes: 15
    }, function(result){
        if(result.error())
        {
            console.error(result.error().ex);
        }
        else
        {
            console.log(result.data());
        }
    });
    ```

- PHP

    ```php
    $result = restCommand('timeman.timecontrol.reports.get', Array(
        'USER_ID' => 2,
        'YEAR' => 2018,
        'MONTH' => 8,
        'WORKDAY_HOURS' => 8,
        'IDLE_MINUTES' => 15
    ), $_REQUEST["auth"]);
    ```

{% endlist %}

{% include [Сноска о примерах](../../../_includes/examples.md) %}

## Ответ в случае успеха

> 200 OK
```json
{
    "result": {
        "report": {
            "month_title": "Август",
            "date_start": "2018-08-01T00:00:00+03:00",
            "date_finish": "2018-08-31T23:59:59+03:00",
            "days": [
                {
                    "index": "20180816",
                    "day_title": "16.08.2018",
                    "workday_complete": false,
                    "workday_date_start": "2018-08-16T14:08:35+03:00",
                    "workday_date_finish": "2018-08-16T11:20:00+03:00",
                    "workday_duration": 10115,
                    "workday_duration_config": 28800,
                    "workday_duration_final": 6914,
                    "workday_time_leaks_user": 0,
                    "workday_time_leaks_real": 3201,
                    "workday_time_leaks_final": 21886,
                    "reports": [
                        {
                            "id": 459,
                            "type": "TM_START",
                            "date_start": "2018-08-16T14:08:35+03:00",
                            "date_finish": "2018-08-16T14:08:35+03:00",
                            "duration": 0,
                            "active": false,
                            "entry_id": 35,
                            "report_type": "NONE",
                            "report_text": null,
                            "system_text": "",
                            "source_start": "TM_EVENT",
                            "source_finish": "TM_EVENT",
                            "ip_start": "93.60.295.11",
                            "ip_finish": "10.10.255.255",
                            "ip_start_network": false,
                            "ip_finish_network": {
                                "ip": "10.10.255.255",
                                "range": "10.0.0.0-10.255.255.255",
                                "name": "Офисная сеть 10.x.x.x"
                            }
                        }
                    ]
                }
            ]
        },
        "user": {
            "id": 2,
            "name": "Мария Ившина",
            "first_name": "Мария",
            "last_name": "Ившина",
            "work_position": "IT-специалист",
            "avatar": "http://test.bitrix24.com/upload/resize_cache/main/072/100_100_2/42-17948709.gif",
            "last_activity_date": "2018-08-15T16:25:34+03:00"
        }
    }
}
```

### Описание ключей

- **report** - информация об отчете.
- **month_title** - название месяца.
- **date_start** - дата начала периода выборки в формате АТОМ.
- **date_finish** - дата окончания периода выборки в формате АТОМ.
- **days** - список отработанных дней.
    - **index** - индекс дня недели.
    - **day_title** - дата (в формате сайте).
    - **workday_complete** - рабочий день завершен (true / false).
    - **workday_date_start** - дата начала рабочего дня в формате АТОМ.
    - **workday_date_finish** - дата окончания рабочего дня в формате АТОМ (если `workday_complete = false`, в данном поле указывается дата на момент формирования отчета).
    - **workday_duration** - продолжительность рабочего дня по табелю в секундах (с учетом установленного пользователем перерыва).
    - **workday_duration_final** - продолжительность рабочего дня по фактической выработке в секундах (с учетом установленного пользователем перерыва, не подтвержденных отсутствий и отсутствий по личным делам).
    - **workday_duration_config** - необходимая продолжительность рабочего дня в секундах.
    - **workday_time_leaks_user** - продолжительность перерыва установленного пользователем в секундах.
    - **workday_time_leaks_real** - продолжительность перерыва установленного автоматической системой фиксации (не подтвержденные отсутствий и отсутствий по личным делам).
    - **workday_time_leaks_final** - если число положительное: количество не доработанного времени в секундах; если число отрицательное: количество времени отработанных сверх положенного времени (переработка).
    - **reports** - список записей выявленных отсутствий (значения доступны только на уровне детализации head и full).
     - **id** - идентификатор записи, необходим для использования метода `timeman.timecontrol.report.add`.
     - **type** - тип записи (справочник типов описан ниже).
     - **active** - активность записи.
     - **date_start**- дата начала фиксации в формате АТОМ.
     - **date_finish** - дата окончания фиксации в формате АТОМ (если active = true в данном поле указывается дата на момент формирования отчета).
     - **report_type** - тип отсутствия (work - по рабочим вопросам, private - личные дела, none - не задан, приравнивается к private).
     - **report_text** - описание причины отсутствия.
     - **system_text** - системное описание причины отсутствия (параметр доступен только на уровне детализации head).
     - **source_start** - поставщик данных начала записи (справочник типов описан ниже).
     - **source_finish** - поставщик данных окончания записи (справочник типов описан ниже).
     - **ip_start** - ip-адрес на момент начала записи (параметр доступен только на уровне детализации head).
     - **ip_start_network** - расшифровка ip-адреса на момент начала записи, если ip-адрес не входит в офисную сеть - false (параметр доступен только на уровне детализации head).
        - **ip** - ip-адрес на момент начала записи.
        - **range** - диапазон, в который входит указанный IP-адрес.
        - **name** - название диапазона, в который входит указанный IP-адрес.
     - **ip_finish** - ip-адрес на момент окончания записи (параметр доступен только на уровне детализации head).
     - **ip_finish_network** - расшифровка ip-адрес на момент окончания записи, если ip-адрес не входит в офисную сеть - false (параметр доступен только на уровне детализации head).
        - **ip** - ip-адрес на момент окончания записи.
        - **range** - диапазон, в который входит указанный IP-адрес.
        - **name** - название диапазона, в который входит указанный IP-адрес.

- **user** - информация о пользователе.
- **id** - идентификатор пользователя.
- **name** - имя и фамилия пользователя.
- **first_name** - имя пользователя.
- **last_name** - фамилия пользователя.
- **work_position** - должность.
- **avatar** - ссылка на аватар (если пусто, значит аватар не задан).
- **personal_gender** - пол пользователя.
- **last_activity_date** - дата последнего действия пользователя в формате АТОМ.

#### Возможные типы записей (type)

- **IDLE** - Отошел (фиксируется с помощью десктоп приложения).
- **OFFLINE** - Офлайн.
- **DESKTOP_ONLINE** - Зафиксирован запуск десктоп приложения (тип доступен только на уровне детализации head).
- **DESKTOP_OFFLINE** - Зафиксирован выключенное десктоп приложение (тип доступен только на уровне детализации head).
- **DESKTOP_START** - Зафиксирован запуск десктоп приложения (тип доступен только на уровне детализации head).
- **TM_START** - Начал рабочий день.
- **TM_PAUSE** - Ушел на перерыв.
- **TM_CONTINUE** - Продолжил день.
- **TM_END** - Завершил рабочий день.

#### Возможные источники записей (source_start, source_finish)

- **ONLINE_EVENT** - Событие авторизации пользователя.
- **OFFLINE_AGENT** - Агент проставляющий статус офлайн.
- **DESKTOP_OFFLINE_AGENT** - Агент проставляющий признак выключенного десктоп приложения.
- **DESKTOP_ONLINE_EVENT** - Событие проставляющий признак включенного десктоп приложения.
- **DESKTOP_START_EVENT** - Событие проставляющий признак включенного десктоп приложения.
- **IDLE_EVENT** - Событие изменение стаса отошел (фиксируется с помощью десктоп приложения).
- **TM_EVENT** - Событие изменения рабочего дня (начало, перерыв, окончание).

## Ответ в случае ошибки

> 200 Error, 50x Error
```json
{
    "error": "ACCESS_ERROR",
    "error_description": "You don't have access to this method"
}
```

### Описание ключей

- Ключ **error** - код возникшей ошибки.
- Ключ **error_description** - краткое описание возникшей ошибки.

### Возможные коды ошибок

#|
|| **Код** | **Описание** ||
|| **ACCESS_ERROR** | Указанный метод не доступен пользователю. ||
|| **USER_ACCESS_ERROR** | Нет доступа к указанному пользователю. ||
|#

## Если возвращает пустой days

Если возвращается пустой массив days, то сначала выставьте нужные опции, для доступа к отчету и сбору данных (необходимо быть администратором и на любой странице портала выполнить в консоли):

```js
BX24.callMethod('timeman.timecontrol.settings.set', {
    active: true,
    REPORT_SIMPLE_TYPE: 'all',
    REPORT_FULL_TYPE: 'all',
    report_request_type: 'user',
    report_request_users: [BX.message.USER_ID],
}, function(result){
    if(result.error())
    {
        console.error(result.error().ex);
    }
    else
    {
        console.log(result.data());
    }
});
```

После этого откройте или закройте рабочий день, после этого в отчете для этого пользователя будут данные:

```js
BX24.callMethod('timeman.timecontrol.reports.get', {
    user_id: BX.message.USER_ID,
    year: 2019,
    month: 1,
    workday_hours: 8,
    idle_minutes: 15
}, function(result){
    if(result.error())
    {
        console.error(result.error().ex);
    }
    else
    {
        console.log(result.data());
    }
});
```
