# Work with Worksheets using the Excel JavaScript API

This article...

```js
Excel.run(function (context) {
    var range = context.workbook.getSelectedRange();
    range.format.fill.color = "yellow";
    range.load("address");
    return context.sync()
        .then(function() {
            console.log("The range address was \"" + range.address + "\".");
        });
}).catch(errorHandler);

Excel.run(function (ctx) {
    var chart = ctx.workbook.worksheets.getItem("Sample").charts.getItem("Chart1");
    chart.load('title/text');
    
    return ctx.sync()
        .then(function () {
            console.log("Chart title is '" + chart.title.text + "'");
        })
}).catch(errorHandler);
```

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

## Get and set the active worksheet

...


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

The following example gets a reference to the worksheet that follows the active worksheet. If there is no worksheet after the active worksheet, this method will throw an **ItemNotFound** error.

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

The following example gets the worksheet that precedes the active worksheet. If there is no worksheet before the active worksheet, this method will throw an **ItemNotFound** error.

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

...

## Hide and unhide a worksheet

...

## Get a range or cell in a worksheet

...