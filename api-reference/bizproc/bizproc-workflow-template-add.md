# Добавить шаблон бизнес-процесса bizproc.workflow.template.add

{% note warning "Мы еще обновляем эту страницу" %}

Тут может не хватать некоторых данных — дополним в ближайшее время

{% endnote %}

{% if build == 'dev' %}

{% note alert "TO-DO _не выгружается на prod_" %}

- нужны правки под стандарт написания
- не указаны типы параметров
- не указана обязательность параметров
- отсутствуют примеры
- отсутствует ответ в случае успеха
- отсутствует ответ в случае ошибки
- не прописаны ссылки на несозданные ещё страницы.
- нужны параметры и описания параметров
- не хватает примеров
- нет стандартных блоков

{% endnote %}

{% endif %}

> Scope: [`bizproc`](../scopes/permissions.md)
>
> Кто может выполнять метод: администратор

Метод добавляет шаблон Бизнес-процесса из сохраненного файла. Иными словами, сначала нужный бизнес-процесс целиком и полностью настраивается на конкретном Битрикс24, затем этот бизнес-процесс экспортируется в bpt-файл с помощью соответствующего пользовательского инструмента (тут нужна ссылка!), а затем этот файл может быть использован для добавления этого же бизнес-процесса в качестве шаблона на нужный Битрикс24 с помощью метода `bizproc.workflow.template.add`.

#|
|| **Параметр** | **Описание**||
|| **DOCUMENT_TYPE**
[`array`](../data-types.md) | Тип документа - массив из 3 строковых элементов, которые определяют, к какому типу объектов будет прикреплен новый шаблон бизнес-процесса. Описание значений см. в стаблице ниже||
|| **NAME**
[`string`](../data-types.md) | Название шаблона ||
|| **DESCRIPTION**
[`string`](../data-types.md) | Описание шаблона. ||
|| **TEMPLATE_DATA**
[`file`](../data-types.md) | Передается контент файла с шаблоном бизнес-процесса *.bpt. См. [{#T}](../how-to-call-rest-api/how-to-upload-files.md) ||
|| **AUTO_EXECUTE**
[`integer`](../data-types.md) | Флаг автозапуска, может быть:

- `0` (без автозапуска),
- `1` (запуск на создание),
- `2` (запуск на изменение),
- `3` (запуск и на создание, и на изменение) ||
|#

## DOCUMENT_TYPE

Параметр `DOCUMENT_TYPE` всегда представляет собой массив из трех элементов. Например, ['crm', 'CCrmDocumentLead', 'LEAD'] и т.д. Значения в этих элементах являются взаимозависимыми. Иными словами, выбрав значение 'crm' для первого элемента массива, остальные значения, которые можно использовать, являются не произвольными, а конкретными и должны быть связаны с crm. Необходимо внимательно следить за их правильностью.

#|
|| **Элемент** | **Описание** ||
|| **id модуля** | Фактически, здесь указывается область привязки шаблона бизнес-процесса. В Битрикс24 на текущий момент бизнес-процессы используются в объектах CRM, живой ленте, универсальных списках, проектах и Битрикс Диск. Следовательно, возможные значения:

- crm
- livestream?
- lists
- tasks
- disk
  
||
|| **Тип объекта / сущность** | Тип документа представляет собой конкретный объект в рамках указанного модуля/сущности. Например, если в качестве модуля мы указали CRM, то в качестве типа документа можно указать CCrmDocumentLead, чтобы привязать шаблон бизнес-процесса к лидам. Возможные значения:

- для crm: CCrmDocumentLead, CCrmDocumentDeal, CCrmDocumentCompany, CCrmDocumentContact
- для livestream ... ??
- для lists: BizprocDocument, ??
- tasks: Bitrix\Tasks\Integration\Bizproc\Document\Task, ??
- disk: Bitrix\Disk\BizProcDocument, ??
 ||

|| **Тип документа / конкретный объект** | После указания типа объекта или сущности, необходимо уточнение в виде привязки к конкретному типу документа или лаже конкретному объекту, если это возможно в конкретном случае. Например, в случае привязки шаблона бизнес-процесса к задачам, необходимо указать идентификатор конкретной рабочей группы (проекта). Возможные значения:

- для CCrmDocumentLead: 'LEAD'
- для CCrmDocumentDeal: 'DEAL'
- для CCrmDocumentCompany: 'COMPANY'
- для CCrmDocumentContact: 'CONTACT'
- для BizprocDocument: 'iblock_22' (привязка к конкретному универсальному списку с id 22)
- для Bitrix\Disk\BizProcDocument: 'STORAGE_490' (привязка к конкретному хранилищу файлов с id 490)
- для Bitrix\Tasks\Integration\Bizproc\Document\Task: 'TASK_PROJECT_13' (привязка к конкретной рабочей группе с id 13)
||
|#

## Пример

{% list tabs %}

- JS

	```javascript
	function addTemplate()
	{
		BX24.callMethod(
			'bizproc.workflow.template.add',
			{
				DOCUMENT_TYPE: ['crm', 'CCrmDocumentLead', 'LEAD'],
				NAME: 'App template',
				DESCRIPTION: 'Template was generated by rest application.',
				AUTO_EXECUTE: 1,
				TEMPLATE_DATA: document.getElementById('tpl_file')
			},
			function(result)
			{
				if(result.error())
					alert("Error: " + result.error());
				console.log(result);
			}
		);
	}
	```

{% endlist %}

{% include [Сноска о примерах](../../_includes/examples.md) %}