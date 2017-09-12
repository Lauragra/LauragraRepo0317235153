# Work with Worksheets using the Excel JavaScript API

This article provides code samples that show how to perform common tasks with worksheets using the Excel JavaScript API. For the complete list of properties and methods that the **Worksheet** object supports, see [Worksheet Object (JavaScript API for Excel)](../../reference/excel/worksheet.md).

**Note**: The information in this article applies only to regular worksheets; it does not apply to "chart" sheets or "macro" sheets.

## Get worksheets

The following code sample gets the collection of worksheets, loads the **name** property of each worksheet, and writes a message to the console.

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

**Note**: The **id** property of a worksheet uniquely identifies the worksheet in a given workbook and its value will remain the same even when the worksheet is renamed or moved. When a worksheet is deleted from a workbook in Excel for Mac, the **id** of the deleted worksheet may be reassigned to a new worksheet that is subsequently created.

## Get and set the active worksheet

These examples show how to get and set the active worksheet.

### Get the active worksheet

The following code sample gets the active worksheet, loads its **name** property, and writes a message to the console.

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

The following code sample sets the active worksheet to the worksheet named **My Sheet**, loads its **name** property, and writes a message to the console. If there is no worksheet with that name, the **activate()** method will throw an **ItemNotFound** error.

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

These examples show how to get a reference to a worksheet by using its relative position.

### Get the first worksheet

The following code sample gets the first worksheet in the workbook, loads its **name** property, and writes a message to the console.

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

The following code sample gets the last worksheet in the workbook, loads its **name** property, and writes a message to the console.

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

The following code sample gets the worksheet that follows the active worksheet in the workbook, loads its **name** property, and writes a message to the console. If there is no worksheet after the active worksheet, the **getNext()** method will throw an **ItemNotFound** error.

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

The following code sample gets the worksheet that precedes the active worksheet in the workbook, loads its **name** property, and writes a message to the console. If there is no worksheet before the active worksheet, the **getPrevious()** method will throw an **ItemNotFound** error.

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

These examples show how to get add, delete, rename, and move a worksheet.

### Add a worksheet

The following code sample adds a new worksheet to the workbook, loads its **name** and **position** properties, and writes a message to the console. The worksheet is added after all existing worksheets.

```js
Excel.run(function (context) {
    var sheets = context.workbook.worksheets;

    var sheet = sheets.add();
    sheet.load("name, position");
    
    return context.sync()
        .then(function () {
            console.log(`Added worksheet named "${sheet.name}" in position ${sheet.position}`);
        });
});
```

### Delete a worksheet

The following code sample deletes the final worksheet in the workbook (as long as it's not the only sheet in the workbook) and writes a message to the console.

```js
Excel.run(function (context) {
    var sheets = context.workbook.worksheets;
    sheets.load("items/name");

    return context.sync()
        .then(function () {
            if (sheets.items.length === 1) {
                console.log("Unable to delete the only worksheet in the workbook");
            } else {
                var lastSheet = sheets.items[sheets.items.length - 1];

                console.log(`Deleting worksheet named "${lastSheet.name}"`);
                lastSheet.delete();

                return context.sync();
            };
        });
});
```

### Rename a worksheet

The following code sample changes the name of the active worksheet to **New Name**.

```js
Excel.run(function (context) {
    var currentSheet = context.workbook.worksheets.getActiveWorksheet();
    currentSheet.name = "New Name";

    return context.sync();
});
```

### Move a worksheet

The following code sample moves a worksheet from the last position in the workbook to the first position in the workbook.

```js
Excel.run(function (context) {
    var sheets = context.workbook.worksheets;
    sheets.load("items");

    return context.sync()
        .then(function () {
            var lastSheet = sheets.items[sheets.items.length - 1];
            lastSheet.position = 0;

            return context.sync();
        });
});
```

## Set worksheet visibility

These examples show how to set the visibility of a worksheet.

### Hide a worksheet

The following code sample sets the visibility of worksheet named **Sample** to hidden, loads its **name** property, and writes a message to the console.

```js
Excel.run(function (context) {

    var sheet = context.workbook.worksheets.getItem("Sample");
    sheet.visibility = Excel.SheetVisibility.hidden;
    sheet.load("name");

    return context.sync()
        .then(function () {
            console.log(`Worksheet with name "${sheet.name}" is hidden`);
        });
});
```

### Unhide a worksheet

The following code sample sets the visibility of worksheet named **Sample** to visible, loads its **name** property, and writes a message to the console.

```js
Excel.run(function (context) {

    var sheet = context.workbook.worksheets.getItem("Sample");
    sheet.visibility = Excel.SheetVisibility.visible;
    sheet.load("name");

    return context.sync()
        .then(function () {
            console.log(`Worksheet with name "${sheet.name}" is visible`);
        });
});
```

## Get a cell within a worksheet

The following code sample gets the cell that is located in row 2, column 5 of the worksheet named **Sample**, loads its **address** and **values** properties, and writes a message to the console. The values that are passed into the **getCell(row: number, column:number)** method are the zero-indexed row number and column number for the cell that is being retrieved.

```js
Excel.run(function (context) {
    var sheet = context.workbook.worksheets.getItem("Sample");
    var cell = sheet.getCell(1, 4);
    cell.load("address, values");
    
    return context.sync()
        .then(function() {
            console.log(`The value of the cell in row 2, column 5 is "${cell.values[0][0]}" and the address of that cell is "${cell.address}"`);
        })
});
```

## Get a range within a worksheet

These examples show different ways to get a reference to a range within a worksheet.

### Get range by address

The following code sample gets the range with address **B2:B5** from the worksheet named **Sample**, loads its **address** property, and writes a message to the console.

```js
Excel.run(function (context) {
    var sheet = context.workbook.worksheets.getItem("Sample");
    var range = sheet.getRange("B2:C5");
    range.load("address");

    return context.sync()
        .then(function () {
            console.log(`The address of the range B2:C5 is "${range.address}"`);
        });
});
```

### Get range by name

The following code sample gets the range named **MyRange** from the worksheet named **Sample**, loads its **address** property, and writes a message to the console.

```js
Excel.run(function (context) {
    var sheet = context.workbook.worksheets.getItem("Sample");
    var range = sheet.getRange("MyRange");
    range.load("address");

    return context.sync()
        .then(function () {
            console.log(`The address of the range "MyRange" is "${range.address}"`);
        });
});
```

### Get used range

The following code sample gets the used range from the worksheet named **Sample**, loads its **address** property, and writes a message to the console. The used range is the smallest range that encompasses any cells in the worksheet that have a value or formatting assigned to them. If the entire worksheet is blank, the **getUsedRange()** function will return a range that consists of only the top left cell in the worksheet.

```js
Excel.run(function (context) {
    var sheet = context.workbook.worksheets.getItem("Sample");
    var range = sheet.getUsedRange();
    range.load("address");

    return context.sync()
        .then(function () {
            console.log(`The address of the used range in the worksheet is "${range.address}"`);
        });
});
```

### Get entire range

The following code sample gets the entire worksheet range from the worksheet named **Sample**, loads its **address** property, and writes a message to the console.

```js
Excel.run(function (context) {
    var sheet = context.workbook.worksheets.getItem("Sample");
    var range = sheet.getRange();
    range.load("address");

    return context.sync()
        .then(function () {
            console.log(`The address of the entire worksheet range is "${range.address}"`);
        });
});
```

## Additional resources

- [Excel JavaScript API core concepts](excel-add-ins-core-concepts.md)
- [Worksheet Object (JavaScript API for Excel)](../../reference/excel/worksheet.md)