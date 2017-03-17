# TableRowCollection Object (JavaScript API for OneNote)

_Applies to: OneNote Online_  


Contains a collection of TableRow objects.

## Properties

| Property	   | Type	|Description|Feedback|
|:---------------|:--------|:----------|:-------|
|count|int|Returns the number of table rows in this collection. Read-only.|[Go](https://github.com/OfficeDev/office-js-docs/issues/new?title=OneNote-tableRowCollection-count)|
|items|[TableRow[]](tablerow.md)|A collection of tableRow objects. Read-only.|[Go](https://github.com/OfficeDev/office-js-docs/issues/new?title=OneNote-tableRowCollection-items)|

_See property access [examples.](#property-access-examples)_

## Relationships
None


## Methods

| Method		   | Return Type	|Description| Feedback|
|:---------------|:--------|:----------|:-------|
|[getItem(index: number or string)](#getitemindex-number-or-string)|[TableRow](tablerow.md)|Gets a table row object by ID or by its index in the collection. Read-only.|[Go](https://github.com/OfficeDev/office-js-docs/issues/new?title=OneNote-tableRowCollection-getItem)|
|[getItemAt(index: number)](#getitematindex-number)|[TableRow](tablerow.md)|Gets a table row at its position in the collection.|[Go](https://github.com/OfficeDev/office-js-docs/issues/new?title=OneNote-tableRowCollection-getItemAt)|
|[load(param: object)](#loadparam-object)|void|Fills the proxy object created in JavaScript layer with property and object values specified in the parameter.|[Go](https://github.com/OfficeDev/office-js-docs/issues/new?title=OneNote-tableRowCollection-load)|

## Method Details


### getItem(index: number or string)
Gets a table row object by ID or by its index in the collection. Read-only.

#### Syntax
```js
tableRowCollectionObject.getItem(index);
```

#### Parameters
| Parameter	   | Type	|Description|
|:---------------|:--------|:----------|
|index|number or string|A number that identifies the index location of a table row object.|

#### Returns
[TableRow](tablerow.md)

### getItemAt(index: number)
Gets a table row at its position in the collection.

#### Syntax
```js
tableRowCollectionObject.getItemAt(index);
```

#### Parameters
| Parameter	   | Type	|Description|
|:---------------|:--------|:----------|
|index|number|Index value of the object to be retrieved. Zero-indexed.|

#### Returns
[TableRow](tablerow.md)

### load(param: object)
Fills the proxy object created in JavaScript layer with property and object values specified in the parameter.

#### Syntax
```js
object.load(param);
```

#### Parameters
| Parameter	   | Type	|Description|
|:---------------|:--------|:----------|
|param|object|Optional. Accepts parameter and relationship names as delimited string or an array. Or, provide [loadOption](loadoption.md) object.|

#### Returns
void
