# Управление карточками контактов: обзор методов

Группа методов crm.contact.details.configuration.* управляет настройками карточки для двух представлений:

* «Общий вид» — вид карточки для всех сотрудников
* «Мой вид» — личная настройка карточки сотрудника

Для каждого вида карточки можно настроить секции, внутри секции — перечень полей. Например создать секцию «Контактные данные» и вывести в ней поля «Телефон» и «Почта». Для полей, которые не относятся к контактным данным, создать другую секцию.

> Быстрый переход: [все методы](#all-methods) 
> 
> Пользовательская документация: [Представления CRM](https://helpdesk.bitrix24.ru/open/17914816/)

## Связь карточки контактов с другими объектами

**Пользователь.** Идентификатор пользователя `userId` используется при установке личных настроек карточки. Получить идентификатор пользователя можно с помощью метода [user.get](../../../user/user-get.md).

**Поля контакта.** Идентификаторы полей используются при установке видимых полей в секции карточки. Получить идентификаторы системных и пользовательских полей контакта можно с помощью метода [crm.contact.fields](../crm-contact-fields.md).

## Универсальные методы для управления карточками

Наравне с методами crm.contact.details.configuration.* для настройки карточки контакта можно использовать группу универсальных методов [crm.item.details.configuration.*](../../universal/item-details-configuration/index.md). Возможности методов одинаковые, отличие может быть во времени выполнения запроса.

Методы [crm.item.details.configuration.*](../../universal/item-details-configuration/index.md) имеют дополнительный параметр `entityTypeId` — ID типа объекта. Параметр `entityTypeId` позволяет применять универсальные методы к любому объекту CRM. Для управления карточкой контакта через универсальный метод передавайте `entityTypeId` = `3`. 

## Обзор методов {#all-methods}

> Scope: [`crm`](../../../scopes/permissions.md)
>
> Кто может выполнять методы: любой пользователь

#|
|| **Метод** | **Описание** ||
|| [crm.contact.details.configuration.get](./crm-contact-details-configuration-get.md) | Получает параметры карточки контакта  ||
|| [crm.contact.details.configuration.set](./crm-contact-details-configuration-set.md) | Устанавливает параметры индивидуальной карточки  ||
|| [crm.contact.details.configuration.forceCommonScopeForAll](./crm-contact-details-configuration-force-common-scope-for-all.md) | Устанавливает общую карточку для всех пользователей  ||
|| [crm.contact.details.configuration.reset](./crm-contact-details-configuration-reset.md) | Сбрасывает параметры карточки  ||
|#
