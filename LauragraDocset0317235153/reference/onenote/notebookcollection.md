# NotebookCollection Object (JavaScript API for OneNote)

_Applies to: OneNote Online_  


Represents a collection of notebooks.

## Properties

| Property	   | Type	|Description|Feedback|
|:---------------|:--------|:----------|:-------|
|count|int|Returns the number of notebooks in the collection. Read-only.|[Go](https://github.com/OfficeDev/office-js-docs/issues/new?title=OneNote-notebookCollection-count)|
|items|[Notebook[]](notebook.md)|A collection of notebook objects. Read-only.|[Go](https://github.com/OfficeDev/office-js-docs/issues/new?title=OneNote-notebookCollection-items)|

_See property access [examples.](#property-access-examples)_

## Relationships
None


## Methods

| Method		   | Return Type	|Description| Feedback|
|:---------------|:--------|:----------|:-------|
|[getByName(name: string)](#getbynamename-string)|[NotebookCollection](notebookcollection.md)|Gets the collection of notebooks with the specified name that are open in the application instance.|[Go](https://github.com/OfficeDev/office-js-docs/issues/new?title=OneNote-notebookCollection-getByName)|
|[getItem(index: number or string)](#getitemindex-number-or-string)|[Notebook](notebook.md)|Gets a notebook by ID or by its index in the collection. Read-only.|[Go](https://github.com/OfficeDev/office-js-docs/issues/new?title=OneNote-notebookCollection-getItem)|
|[getItemAt(index: number)](#getitematindex-number)|[Notebook](notebook.md)|Gets a notebook on its position in the collection.|[Go](https://github.com/OfficeDev/office-js-docs/issues/new?title=OneNote-notebookCollection-getItemAt)|
|[load(param: object)](#loadparam-object)|void|Fills the proxy object created in JavaScript layer with property and object values specified in the parameter.|[Go](https://github.com/OfficeDev/office-js-docs/issues/new?title=OneNote-notebookCollection-load)|

## Method Details


### getByName(name: string)
Gets the collection of notebooks with the specified name that are open in the application instance.

#### Syntax
```js
notebookCollectionObject.getByName(name);
```

#### Parameters
| Parameter	   | Type	|Description|
|:---------------|:--------|:----------|
|name|string|The name of the notebook.|

#### Returns
[NotebookCollection](notebookcollection.md)

#### Examples
```js
OneNote.run(function (context) {

    // Get the notebooks that are open in the application instance and have the specified name.
    var notebooks = context.application.notebooks.getByName("Homework");

    // Queue a command to load the notebooks. 
    // For best performance, request specific properties.           
    notebooks.load("id,name");

    // Run the queued commands, and return a promise to indicate task completion.
    return context.sync()
        .then(function () {

            // Iterate through the collection or access items individually by index, for example: notebooks.items[0]
            if (notebooks.items.length > 0) {
                console.log("Notebook name: " + notebooks.items[0].name);
                console.log("Notebook ID: " + notebooks.items[0].id);
            }
                
        });
})
.catch(function(error) {
	console.log("Error: " + error);
	if (error instanceof OfficeExtension.Error) {
		console.log("Debug info: " + JSON.stringify(error.debugInfo));
	}
});
```

### getItem(index: number or string)
Gets a notebook by ID or by its index in the collection. Read-only.

#### Syntax
```js
notebookCollectionObject.getItem(index);
```

#### Parameters
| Parameter	   | Type	|Description|
|:---------------|:--------|:----------|
|index|number or string|The ID of the notebook, or the index location of the notebook in the collection.|

#### Returns
[Notebook](notebook.md)

### getItemAt(index: number)
Gets a notebook on its position in the collection.

#### Syntax
```js
notebookCollectionObject.getItemAt(index);
```

#### Parameters
| Parameter	   | Type	|Description|
|:---------------|:--------|:----------|
|index|number|Index value of the object to be retrieved. Zero-indexed.|

#### Returns
[Notebook](notebook.md)

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
### Property access examples

**items**
```js
OneNote.run(function (context) {

    // Get the notebooks that are open in the application instance and have the specified name.
    var notebooks = context.application.notebooks.getByName("Homework");

    // Queue a command to load the notebooks. 
    // For best performance, request specific properties.           
    notebooks.load("id");

    // Run the queued commands, and return a promise to indicate task completion.
    return context.sync()
        .then(function () {

            // Iterate through the collection or access items individually by index, for example: notebooks.items[0]
            $.each(notebooks.items, function(index, notebook) {
                notebook.addSection("Biology");
                notebook.addSection("Spanish");
                notebook.addSection("Computer Science");
            });
            
            return context.sync();
        });
})
.catch(function(error) {
	console.log("Error: " + error);
	if (error instanceof OfficeExtension.Error) {
		console.log("Debug info: " + JSON.stringify(error.debugInfo));
	}
});
```

