# Получить список чат-ботов imbot.bot.list

{% note warning "Мы еще обновляем эту страницу" %}

Тут может не хватать некоторых данных — дополним в ближайшее время

{% endnote %}

{% if build == 'dev' %}

{% note alert "TO-DO _не выгружается на prod_" %}

- нужны правки под стандарт написания
- отсутствуют примеры
- отсутствует ответ в случае успеха
- отсутствует ответ в случае ошибки

{% endnote %}

{% endif %}

> Scope: [`imbot`](../scopes/permissions.md)
>
> Кто может выполнять метод: любой пользователь

Метод `imbot.bot.list` получает список доступных чат-ботов.

Без параметров.

## Примеры

{% include [Пояснение о restCommand](./_includes/rest-command.md) %}

{% list tabs %}

- PHP

    ```php
    $result = restCommand(
        'imbot.bot.list',
        Array(),
        $_REQUEST[
            "auth"
        ]
    );
    ```

{% endlist %}

{% include [Сноска о примерах](../../_includes/examples.md) %}

### Ответ в случае успеха

Массив массивов, содержащий данные по чат-ботам:

- **ID** - идентификатор бота.
- **NAME** - имя чат-бота.
- **CODE** - внутренний код.
- **OPENLINE** - поддерживает Открытые линии или нет.