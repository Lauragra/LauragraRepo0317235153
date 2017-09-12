# Work with Worksheets using the Excel JavaScript API

This article provides code samples that show how to perform common tasks with worksheets using the Excel JavaScript API. For the complete list of properties and methods that the **Worksheet** object supports, see [Worksheet Object (JavaScript API for Excel)](../../reference/excel/worksheet.md).

**Note**: [TODO: add note to indicate that the information in this article applies only to the "worksheet" type of worksheet; the JavaScript Excel APIs do not apply to "chart" type of sheet and the "macro" type of sheet. https://excel.tips.net/T002538_Detecting_Types_of_Sheets_in_VBA.html]

## List worksheets

The following example lists the worksheets in a workbook.

```js
Excel.run(function (context) {
    var sheets = context.workbook.worksheets;
    sheets.load("items/name");

    return context.sync()
        .then(function () {
            if (sheets.items.length > 1) {
                console.log(`There are ${sheets.items.length} worksheets in the workbook:`);
            } else {
                console.log(`There is one worksheet in the workbook:`);
            }
            for (var i in sheets.items) {
                console.log(sheets.items[i].name);
            }
        });
});
```

**Note**: [TODO: add note about the **id** property being handled differently on Mac.] Returns a value that uniquely identifies the worksheet in a given workbook. The value of the identifier remains the same even when the worksheet is renamed or moved.]

## Get and set the active worksheet

The following examples show how to get and set the active worksheet.

### Get the active worksheet

The following example gets the active worksheet.

```js
Excel.run(function (context) {
    var sheet = context.workbook.worksheets.getActiveWorksheet();
    sheet.load("name");
    
    return context.sync()
        .then(function () {
            console.log(`The active worksheet is "${sheet.name}"`);
        });
});
```

### Set the active worksheet

The following example sets the active worksheet to the worksheet named **My Sheet**. If there is no worksheet with that name, the **activate()** method will throw an **ItemNotFound** error.

```js
Excel.run(function (context) {
    var sheet = context.workbook.worksheets.getItem("My Sheet");
    sheet.activate();
    sheet.load("name");

    return context.sync()
        .then(function () {
            console.log(`The active worksheet is "${sheet.name}"`);
        });
});
```

## Reference worksheets by relative position

The following examples show how to get a reference to a worksheet by using its relative position.

### Get the first worksheet

The following example gets a reference to the first worksheet in a workbook.

```js
Excel.run(function (context) {
    var firstSheet = context.workbook.worksheets.getFirst();
    firstSheet.load("name");

    return context.sync()
        .then(function () {
            console.log(`The name of the first worksheet is "${firstSheet.name}"`);
        });
});
```

### Get the last worksheet

The following example gets a reference to the last worksheet in a workbook.

```js
Excel.run(function (context) {
    var lastSheet = context.workbook.worksheets.getLast();
    lastSheet.load("name");

    return context.sync()
        .then(function () {
            console.log(`The name of the last worksheet is "${lastSheet.name}"`);
        });
});
```

### Get the next worksheet

The following example gets a reference to the worksheet that follows the active worksheet. If there is no worksheet after the active worksheet, the **getNext()** method will throw an **ItemNotFound** error.

```js
 Excel.run(function (context) {
    var currentSheet = context.workbook.worksheets.getActiveWorksheet();
    var nextSheet = currentSheet.getNext();
    nextSheet.load("name");

    return context.sync()
        .then(function () {
            console.log(`The name of the sheet that follows the active worksheet is "${nextSheet.name}"`);
        });
});
```

### Get the previous worksheet

The following example gets the worksheet that precedes the active worksheet. If there is no worksheet before the active worksheet, the **getPrevious()** method will throw an **ItemNotFound** error.

```js
Excel.run(function (context) {
    var currentSheet = context.workbook.worksheets.getActiveWorksheet();
    var previousSheet = currentSheet.getPrevious();
    previousSheet.load("name");

    return context.sync()
        .then(function () {
            console.log(`The name of the sheet that precedes the active worksheet is "${previousSheet.name}"`);
        });
});
```

## Add, delete, rename and move a worksheet

The following examples show how to get add, delete, rename, and move a worksheet.

### Add a worksheet

The following example . a worksheet.

```js
```

### Delete a worksheet

The following example . a worksheet.

```js
```

### Rename a worksheet

The following example . a worksheet.

```js
```

### Move a worksheet

The following example . a worksheet.

```js
```





## Hide and unhide a worksheet

...

## Get a range or cell in a worksheet

...

## Additional resources

- [Worksheet Object (JavaScript API for Excel)](../../reference/excel/worksheet.md)