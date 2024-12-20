# Добавить новый календарь calendar.section.add

> Scope: [`calendar`](../scopes/permissions.md)
>
> Кто может выполнять метод: любой пользователь

Метод `calendar.section.add` добавляет новый календарь. Здесь и в дальнейшем section будет именоваться как "календарь".

{% note info %}

На текущий момент метод добавляет новый календарь только для пользователя, от которого выполняется метод calendar.section.add. В будущем это ограничение будет снято.

{% endnote %}

## Параметры метода

{% include [Сноска об обязательных параметрах](../../_includes/required.md) %}

#|
|| **Параметр** | **Описание** ||
|| **type***
[`string`](../data-types.md) | Тип календаря: 
- user; 
- group. ||
|| **ownerId***
[`integer`](../data-types.md) | Идентификатор владельца календаря. Если не передан, то для type == 'user' будет установлен автоматически на текущего пользователя ||
|| **name***
[`string`](../data-types.md) | Название календаря ||
|| **description**
[`string`](../data-types.md) | Описание календаря ||
|| **color**
[`string`](../data-types.md) | Цвет календаря ||
|| **text_color**
[`string`](../data-types.md) | Цвет текста в календаре ||
|| **export**
[`object`](../data-types.md) | Список параметров экспорта календаря: 
- ALLOW [`boolean`](../data-types.md) - разрешить экспорт календаря; 
- SET [`string`](../data-types.md) - устанавливается период, за который производить экспорт ('all', '3_9', '6_12')
  - all - за весь период;
  - 3_9 - 3 месяца до и 9 после;
  - 6_12 - 6 месяцев до и 12 после.
||
|#

## Примеры кода

{% include [Сноска о примерах](../../_includes/examples.md) %}

{% list tabs %}

- JS

    ```js
    BX24.callMethod(
        'calendar.section.add',
        {
            type: 'user',
            ownerId: 2,
            name: 'New Section',
            description: 'Description for section',
            color: '#9cbeee',
            text_color: '#283000',
            export: {ALLOW: false, SET: '3_9'}
        }
    );
    ```

{% endlist %}

{% include [Сноска о примерах](../../_includes/examples.md) %}

## Обработка ответа

HTTP-статус: **200**

```json
{
  "result": 190,
  "time": {
    "start": 1733812564.64201,
    "finish": 1733812565.71673,
    "duration": 1.0747201442718506,
    "processing": 0.05963897705078125,
    "date_start": "2024-12-08T06:36:04+00:00",
    "date_finish": "2024-12-08T06:36:05+00:00"
  }
}
```

### Возвращаемые данные

#|
|| **Название**
`тип` | **Описание** ||
|| **result**
[`integer`](../data-types.md) | Идентификатор созданного календаря ||
|#

## Обработка ошибок

HTTP-статус: **400**

```json
{
  "error": "",
  "error_description": "Не задан обязательный параметр \"type\" для метода \"calendar.section.add\""
}
```

{% include notitle [обработка ошибок](../../_includes/error-info.md) %}

### Возможные коды ошибок

#|
|| **Код** | **Сообщение об ошибке** | **Описание** ||
|| Пустая строка | Не задан обязательный параметр "type" для метода "calendar.section.add" | Не передан обязательный параметр `type` ||
|| Пустая строка | Не задан обязательный параметр "ownerId" для метода "calendar.section.add" | Не передан обязательный параметр `ownerId` и параметр `type` не равен 'user' ||
|| Пустая строка | Недопустимое значение параметра "name" | Передан неверный формат данных в поле `name` ||
|| Пустая строка | Недопустимое значение параметра "description" | Передан неверный формат данных в поле `description` ||
|| Пустая строка | Доступ запрещен | Нет прав для создания календаря с переданным `type` ||
|| Пустая строка | При создании секции произошла ошибка | Другая ошибка ||
|#

{% include [системные ошибки](../../_includes/system-errors.md) %}