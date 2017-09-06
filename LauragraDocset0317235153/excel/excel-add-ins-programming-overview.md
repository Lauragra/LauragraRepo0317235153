# Excel JavaScript API programming overview

This article describes how to use the [Excel JavaScript API](../../reference/excel/excel-add-ins-reference-overview.md?product=excel) to build add-ins for Excel 2016. It introduces key concepts that are fundamental to using the API and provides code samples that show how to apply the concepts. It also provides guidance about specific scenarios such as reading or writing to a large range, updating all cells in range, and more.

## Excel.run

The **Excel.run** function executes a batch function that you define to execute actions on the Excel object model. Calling **Excel.run** automatically creates a *request context* that is passed into the batch function, where you can use it to interact with Excel objects such as worksheets, ranges, charts, and tables. 

>**Note**: Because an Excel add-in and the Excel application run in two different processes, the add-in requires a request context in order to interact with Excel.

Using **Excel.run** is advantageous not only because it automatically creates a request context, but also because when the batch function completes and the promise is resolved, any tracked objects that were allocated during the execution are automatically released. 

The following example shows a simple batch function that is executed using **Excel.run**. It includes a single **catch** statement at the end of **Excel.run** to catch and log any errors that may occur within the batch function.

```js
Excel.run(function (context) { 
  // You can use the Excel JavaScript API here in the batch function
  // to execute actions on the Excel object model.
  console.log('Your code goes here.');
}).catch(function (error) {
  console.log('error: ' + error);
  if (error instanceof OfficeExtension.Error) {
    console.log('Debug info: ' + JSON.stringify(error.debugInfo));
  }
});
```

## Proxy objects and the asynchronous programming model

The Excel JavaScript objects that you declare and use in an add-in are proxy objects which represent elements that may or may not yet exist in the Excel document. Any methods that you invoke or properties that you set or load on proxy objects are simply added to a queue of pending changes, to be dispatched to the Excel application as a batch of instructions the next time you call the **sync()** method on the request context. 

For example, the following code snippet declares the local JavaScript object **selectedRange** to reference the selected range in the Excel document and then sets some properties on that object. Because the **selectedRange** object is simply a proxy object, none of the properties set or methods invoked on that object will be dispatched to Excel until **context.sync()** is called.

```js
const selectedRange = context.workbook.getSelectedRange();
selectedRange.format.fill.color = "#4472C4";
selectedRange.format.font.color = "white";
selectedRange.format.autofitColumns();
```

The Excel JavaScript API is fundamentally batch-centric. You can queue up as many changes as you wish on the request context, and then call the **sync()** method to execute the batch of queued instructions when necessary. To optimize performance, you should queue up as many changes as possible before calling **sync()** and minimize the number of times you call **sync()**. 

### sync()

Calling the **sync()** method on the request context synchronizes the state between JavaScript proxy objects and objects in the Excel document by executing any instructions that have been queued on the request context and retrieving values for any properties that have been requested to be loaded for proxy objects. The **sync()** method executes asynchronously and returns a promise, which is resolved when synchronization is complete. 

>**Note**: In the Excel JavaScript API, **sync()** is the only asynchronous operation.

Because **sync()** is an asynchronous operation that returns a promise, you should always **return** the promise (in JavaScript) or **await** the promise (in TypeScript). Doing so will ensure that the **sync()** operation completes before execution continues. 

The following example shows a batch function that defines a local JavaScript proxy object (**selectedRange**), loads a property of that object, and then uses the JavaScript Promises pattern to call **context.sync()** to synchronize the state between local proxy objects and objects in the Excel document. 

```js
Excel.run(function (context) { 
  const selectedRange = context.workbook.getSelectedRange();
  selectedRange.load('address');
  return context.sync()
    .then(function () {
      console.log('The selected range is: ' + selectedRange.address);
  });
}).catch(function (error) {
  console.log('error: ' + error);
  if (error instanceof OfficeExtension.Error) {
    console.log('Debug info: ' + JSON.stringify(error.debugInfo));
  }
});
```

### load()

Before you can read the properties of a proxy object, you must explicitly load the properties to populate the proxy object with data from the Excel document. For example, if you create a proxy object to reference the selected range, and subsequently want to read the selected range's **address** property, you need to load the **address** property before you'll be able to read it. To request that properties of a proxy object be loaded, call the **load()** method on the object to specify those properties.  

>**Note**: If you are simply calling methods on a proxy object, or setting its properties, or using the object to navigate to another object, you do not need to call the **load()** method. The **load()** method is only required when you are intending to read properties on a proxy object. 

Just like requests to set properties or invoke methods on proxy objects, requests to load properties on proxy objects get added to the queue of pending requests on the request context, to be do be dispatched to the Excel application as a batch of instructions the next time you call the **sync()** method on the request context. Therefore, you can queue up as many **load()** calls on the request context as you need to, and they will all be executed with any other queued up instructions the next time you call **sync()**. 

In the following example, only specific properties and relationships of the range are loaded. Because `format/font` is not loaded, the value of the `format.font.color` property cannot be read.

```js
Excel.run(function (context) {
  const sheetName = 'Sheet1';
  const rangeAddress = 'A1:B2';
  const myRange = context.workbook.worksheets.getItem(sheetName).getRange(rangeAddress);

  myRange.load(['address', 'format/*', 'format/fill', 'entireRow' ]);

  return context.sync()
    .then(function () {
      console.log (myRange.address);              // ok
      console.log (myRange.format.wrapText);      // ok
      console.log (myRange.format.fill.color);    // ok
      //console.log (myRange.format.font.color);  // not ok as it was not loaded
  });
}).then(function () {
  console.log('done');
}).catch(function (error) {
  console.log('Error: ' + error);
  if (error instanceof OfficeExtension.Error) {
    console.log('Debug info: ' + JSON.stringify(error.debugInfo));
  }
});
```

By default, **object.load()** loads all scalar and complex properties of the object; the relationships (for example, **format** on a **Range** object) are not loaded by default. To optimize performance, you should explicitly specify the properties and relationships to be loaded when calling the **object.load()** method. For example, if you only intend to read back the **address** property of a range object, specify only that property when you call **object.load**: 

```js
range.load('address');
```

You can call **object.load()** in any of the following ways:

_Syntax:_

```js
object.load(string: properties);
// or
object.load(array: properties);
// or
object.load({ loadOption });
```

_Where:_

* `properties` is the list of properties and/or relationship names to be loaded specified as comma-delimited strings or array of names. See **.load()** methods under each object for details.
* `loadOption` specifies an object that describes the selection, expansion, top, and skip options. See object load [options](../../reference/excel/loadoption.md?product=excel) for details.

## Examples

The following two examples demonstrate the concepts that have been discussed in this article thus far.

### Write values from an array to a range object

The following example shows how to write values from an array to a range object in an Excel worksheet.

The **Excel.run** function contains a batch of instructions. A proxy object is created to reference a range on the active worksheet (range address = `A1:B2`) and the value of this proxy object is set locally. When `context.sync()` is called, the state of the proxy object is synchronized with the corresponding object in Excel. The **sync()** method returns a promise that can be used to chain it with other operations.

```js
// Run a batch operation against the Excel object model. 
// The context input parameter provides access to objects in the Excel document.
Excel.run(function (context) {
  // Create a proxy object for the sheet
  const sheet = context.workbook.worksheets.getActiveWorksheet();

  // Specify values
  const values = [
    ['Type', 'Estimate'],
    ['Transportation', 1670]
  ];

  // Create a proxy object for the range
  const range = sheet.getRange('A1:B2');

  // Set the proxy object's values property to the array of values defined earlier
  range.values = values;

  // Synchronize the state between JavaScript proxy objects and real objects in Excel 
  // by executing instructions that have been queued on the context
  return context.sync()
    .then(function () {
      console.log('Done');
  });
}).catch(function (error) {
  console.log('error: ' + error);
  if (error instanceof OfficeExtension.Error) {
    console.log('Debug info: ' + JSON.stringify(error.debugInfo));
  }
});
```

### Copy values from one range to another

The following example shows how to copy the values from range `A1:A2` to range `B1:B2` in the active worksheet, by using the **load()** method to retrieve the values of the first range and then using those values to populate the second range.

```js
Excel.run(function (context) {
  // Create a proxy object for the range and load the values property
  const range = context.workbook.worksheets.getActiveWorksheet().getRange('A1:A2').load('values');

  // Synchronize the state between JavaScript proxy objects and real objects in Excel 
  // by executing instructions that have been queued on the context
  return context.sync()
    .then(function () {
      // Assign the previously loaded values to the new range proxy object. 
      // The values will be updated once the following .then() function is invoked.
      context.workbook.worksheets.getActiveWorksheet().getRange('B1:B2').values = range.values;
  });
}).then(function () {
  console.log('done');
}).catch(function (error) {
  console.log('Error: ' + error);
  if (error instanceof OfficeExtension.Error) {
    console.log('Debug info: ' + JSON.stringify(error.debugInfo));
  }
});
```

## `null` or blank property values

### `null` input in 2-D Array

`null` input inside two-dimensional array (for values, number format, formula) is ignored by the update API. No update will take place to the intended target when `null` input is specified for values or number format or formula.

For example, to update the number format for only one cell within a range, and retain the existing number format for all other cells in the range, specify the new number format for the cell to update, and specify `null` for all other cells. The following code snippet sets a new number format for the fourth cell in the range, and leaves the number format unchanged for the first three cells in the range.

```js
range.values = [['Eurasia', '29.96', '0.25', '15-Feb' ]];
range.numberFormat = [[null, null, null, 'm/d/yyyy;@']];
```

### `null` input for a property

`null` is not a valid input for single property. For example, the following code snippet is not valid, as the **values** property of the range cannot be set to `null`.

```js
range.values = null;
```

Likewise, the following code snippet is not valid, as `null` is not a valid value for the **color** property.

```js
range.format.fill.color =  null;
```

### `null` property values in the response

Formatting properties such as `size` and `color` will contain `null` values in the response when non-uniform values exist throughout the specified range. For example, if you retrieve a range and load its `format.font.color` property:

* If all cells in the range have the same font color, `range.format.font.color` specifies that color.
* If multiple font colors are present within the range, `range.format.font.color` is `null`.

### Blank input for a property

A blank value (i.e., two quotation marks with no space in-between `''`) in an update request is interpreted as an instruction to clear or reset the respective property. For example: 

* If you specify a blank value for the `values` property of a range, the content of the range is cleared. This is the same as clearing the content of the range in the application.

* If you specify a blank value for the `numberFormat` property, the number format is reset to `General`.

* If you specify a blank value for the `formula` property and `formulaLocale` property, the formula values are cleared.

### Blank property values in the response

For read operations, a blank property value in the response (i.e., two quotation marks with no space in-between `''`) indicates that cell contains no data or value. In the first example below, the first and last cell in the range contain no data. In the second example, the first two cells in the range do not contain a formula.

```js
range.values = [['', 'some', 'data', 'in', 'other', 'cells', '']];
```

```js
range.formula = [['', '', '=Rand()']];
```

## Read or write to an unbounded range

### Read an unbounded range

An unbounded range address specifies only column identifiers or only row identifiers. For example:

* Addresses that specify only column identifers: `C:C`, `A:F`, `A:XFD`
* Addresses that specify only row identifers: `2:2`, `1:4`, `1:1048546`

When the API makes a request to retrieve an unbounded range (e.g., `getRange('C:C')`), the response will contain `null` values for cell-level properties such as `values`, `text`, `numberFormat`, and `formula`. Other properties of the range, such as `address` and `cellCount`, will contain valid values for the unbounded range.

### Write to an unbounded range

Setting cell-level properties such as `values`, `numberFormat`, and `formula` on unbounded range is **prohibited**, as the input request might be too large to handle. For example, the following code snippet is not valid because it attempts to specify `values` for an unbounded range. The API will return an error if you attempt to set cell-level properties for an unbounded range.

```js
const range = context.workbook.worksheets.getActiveWorksheet().getRange('A:B');
range.values = 'Due Date';
```

## Read or write to a large range

If a range contains a large number of cells, values, number formats, and/or formulas, it may not be possible to successfully execute API operations for the range. The API will always make a best attempt to execute the requested operation on a range (i.e., to retrieve or write the specified data), but attempting to perform read or write operations for a large range may result in an API error due to excessive resource utilization. To avoid such errors, we recommend that you execute separate read or write operations for smaller subsets of a large range, instead of attempting to execute a single read or write operation for the large range.

## Update all cells in a range

To apply the same update to all cells in a range, (for example, to populate all cells in a range with the same value, set the same number format for all cells in a range, or populate all cells in a range with the same formula), set the corresponding property on **range** object to the desired (single) value.

The following example gets a range that contains 20 cells and then sets the number format for all cells in the range and populates all cells in the range with the value **3/11/2015**. 

```js
Excel.run(function (context) {
  const sheetName = 'Sheet1';
  const rangeAddress = 'A1:A20';
  const worksheet = context.workbook.worksheets.getItem(sheetName);
  
  const range = worksheet.getRange(rangeAddress);
  range.numberFormat = 'm/d/yyyy';
  range.values = '3/11/2015';
  range.load('text');

  return context.sync()
    .then(function () {
      console.log(range.text);
  });
}).catch(function (error) {
  console.log('Error: ' + error);
  if (error instanceof OfficeExtension.Error) {
    console.log('Debug info: ' + JSON.stringify(error.debugInfo));
  }
});
```

## Error messages

When an API error occurs, the API will return an **error** object that contains a code and a message. The following table defines a list of errors that the API may return.

|error.code | error.message |
|:----------|:--------------|
|InvalidArgument |The argument is invalid or missing or has an incorrect format.|
|InvalidRequest  |Cannot process the request.|
|InvalidReference|This reference is not valid for the current operation.|
|InvalidBinding  |This object binding is no longer valid due to previous updates.|
|InvalidSelection|The current selection is invalid for this operation.|
|Unauthenticated |Required authentication information is either missing or invalid.|
|AccessDenied	|You cannot perform the requested operation.|
|ItemNotFound	|The requested resource doesn't exist.|
|ActivityLimitReached|Activity limit has been reached.|
|GeneralException|There was an internal error while processing the request.|
|NotImplemented  |The requested feature isn't implemented.|
|ServiceNotAvailable|The service is unavailable.|
|Conflict	|Request could not be processed because of a conflict.|
|ItemAlreadyExists|The resource being created already exists.|
|UnsupportedOperation|The operation being attempted is not supported.|
|RequestAborted|The request was aborted during run time.|
|ApiNotAvailable|The requested API is not available.|
|InsertDeleteConflict|The insert or delete operation attempted resulted in a conflict.|
|InvalidOperation|The operation attempted is invalid on the object.|

## Additional resources

* [Get started with Excel add-ins](excel-add-ins-get-started-overview.md?product=excel)
* [Excel add-ins code samples](http://dev.office.com/code-samples#?filters=excel,office%20add-ins)
* [Excel JavaScript API reference](../../reference/excel/excel-add-ins-reference-overview.md?product=excel)
