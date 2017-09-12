# Work with Tables using the Excel JavaScript API

This article provides code samples that show how to perform common tasks with tables using the Excel JavaScript API. For the complete list of properties and methods that the the **Table** and **TableCollection** objects support, see [Table Object (JavaScript API for Excel)](../../reference/excel/table.md) and [TableCollection Object (JavaScript API for Excel)](../../reference/excel/tablecollection.md).

## Create a table

The following code sample adds a table to the worksheet named **Sample**. The table has headers and contains four columns and seven rows of data. If the Excel client where the code is running supports requirement set **ExcelApi 1.2**, the width of the columns and height of the rows are set to best fit the current data in the table.

```js
Excel.run(function (context) {
    var sheet = context.workbook.worksheets.getItem("Sample");
    var expensesTable = sheet.tables.add("A1:D1", true /*hasHeaders*/);
    expensesTable.name = "ExpensesTable";

    expensesTable.getHeaderRowRange().values = [["Date", "Merchant", "Category", "Amount"]];

    expensesTable.rows.add(null /*add rows to the end of the table*/, [
        ["1/1/2017", "The Phone Company", "Communications", "$120"],
        ["1/2/2017", "Northwind Electric Cars", "Transportation", "$142"],
        ["1/5/2017", "Best For You Organics Company", "Groceries", "$27"],
        ["1/10/2017", "Coho Vineyard", "Restaurant", "$33"],
        ["1/11/2017", "Bellows College", "Education", "$350"],
        ["1/15/2017", "Trey Research", "Other", "$135"],
        ["1/15/2017", "Best For You Organics Company", "Groceries", "$97"]
    ]);

    if (Office.context.requirements.isSetSupported("ExcelApi", 1.2)) {
        sheet.getUsedRange().format.autofitColumns();
        sheet.getUsedRange().format.autofitRows();
    }

    sheet.activate();

    return context.sync();
});
```

## Add rows and columns to a table

These examples show how to add rows and columns to a table.

### Add a row to a table

The following code sample..., loads the **name** property of each table..., and writes a message to the console.

```js
```

### Add a column to a table

The following code sample..., loads the **name** property of each table..., and writes a message to the console.

```js
```

### Add a calculated column to a table

The following code sample..., loads the **name** property of each table..., and writes a message to the console.

```js
```

## Import JSON data into a table

The following code sample..., loads the **name** property of each table..., and writes a message to the console.

```js
```

## Get data from a table

The following code sample..., loads the **name** property of each table..., and writes a message to the console.

```js
```

## Sort data in a table

The following code sample..., loads the **name** property of each table..., and writes a message to the console.

```js
```

## Filter data in a table

The following code sample..., loads the **name** property of each table..., and writes a message to the console.

```js
```

## Get the visible range from a filtered table

The following code sample..., loads the **name** property of each table..., and writes a message to the console.

```js
```

## Format a table

The following code sample..., loads the **name** property of each table..., and writes a message to the console.

```js
```

## Convert a range to a table

The following code sample..., loads the **name** property of each table..., and writes a message to the console.

```js
```















## [individual code sample]

The following code sample..., loads the **name** property of each table..., and writes a message to the console.

```js
```

## [section of samples]

These examples show how to...

### [subsection code sample]

The following code sample..., loads the **name** property of each table..., and writes a message to the console.

```js
```

