# Excel JavaScript API programming overview

This article describes how to use the [Excel JavaScript API](../../reference/excel/excel-add-ins-reference-overview.md?product=excel) to build add-ins for Excel 2016. It introduces key concepts that are fundamental to using the APIs, such as **RequestContext**, JavaScript proxy objects, **sync()**, **Excel.run()**, and **load()** and provides code examples that show how to apply the concepts.

>**Note:** When you build your add-in, if you plan to [publish](../publish/publish.md) your add-in to the Office Store, make sure that you conform to the [Office Store validation policies](https://msdn.microsoft.com/en-us/library/jj220035.aspx). For example, to pass validation, your add-in must work across all platforms that support the methods that you define (for more information, see [section 4.12](https://msdn.microsoft.com/en-us/library/jj220035.aspx#Anchor_3) and the [Office Add-in host and availability page](https://dev.office.com/add-in-availability)).

## RequestContext

The **RequestContext** object facilitates requests to the Excel application. Because the Office Add-in and the Excel application run in two different processes, the add-in requires a request context in order to be able to interact with objects in Excel such as worksheets, ranges, charts, and tables. The following snippet shows how to create a request context.

```js
const ctx = new Excel.RequestContext();
```

## Proxy objects

The Excel JavaScript objects declared and used in an add-in are proxy objects for the real objects in an Excel document. Actions taken on proxy objects are not realized in Excel, and the state of the Excel document is not realized in the proxy objects, until the document state has been synchronized. The document state is synchronized when the **sync()** method is run. (See below for details about the **sync()** method.)

For example, the following code snippet declares the local JavaScript object **selectedRange** to reference the selected range.

```js
const selectedRange = ctx.workbook.getSelectedRange();
```

The **selectedRange** object is a proxy object that can be used to queue the setting of the range's properties and invoking of the ranges methods. Any properties set or methods invoked on the **selectedRange** proxy object will not be realized in Excel until the **sync()** method is run.

## sync()

Calling the **sync()** method on the request context synchronizes the state between JavaScript proxy objects and real objects in Excel by executing any instructions that have been queued on the context and retrieving values for any properties that have been loaded for proxy objects. This method returns a promise, which is resolved when synchronization is complete. 

## Excel.run

The **Excel.run** function executes a batch script that you define to perform actions on the Excel object model. The batch script includes definitions of local JavaScript proxy objects, **sync()** methods that synchronize the state between local objects and Excel objects, and promise resolution. Calling **Excel.run** automatically creates a request context, which you can use in the batch script to interact with objects in Excel. When the batch script completes and the promise is resolved, any tracked objects that were allocated during the execution will automatically be released. While it is possible to run a batch script outside of **Excel.run**, it is not recommended, as any object references that are created outside of **Excel.run()** would need to be manually tracked and managed.

The following example shows a simple batch script executed within **Excel.run**.

```js
Excel.run(function (ctx) { 
  const selectedRange = ctx.workbook.getSelectedRange();
  selectedRange.load('address');
  return ctx.sync()
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

## load()

The **load()** method can be used to populate a proxy object that has been created in the add-in JavaScript layer, if you are intending to read back its properties. For example, if you create a proxy object to reference the selected range, and subsequently want to read the selected range's **address** property, you need to load the **address** property before you'll be able to read it. The following code snippet uses the **load()** method to load the **address** property for the selected range and then calls the **sync()** method to execute the load.

```js
const selectedRange = ctx.workbook.getSelectedRange();
selectedRange.load('address');
ctx.sync();
console.log('The selected range is: ' + selectedRange.address);
```

If you are simply calling methods on a proxy object, or setting its properties, or using the object to navigate to another object, you do not need to call the **load()** method. The **load()** method is only required when you are intending to read properties on a proxy object. You can call the **load()** method in any of the following ways, specifying the properties that you want to load when the **sync()** method is subsquently called.

_Syntax:_

```js
object.load(string: properties);
// or
object.load(array: properties);
// or
object.load({ loadOption });
```

Where:

* `properties` is the list of properties and/or relationship names to be loaded specified as comma-delimited strings or array of names. See **.load()** methods under each object for details.
* `loadOption` specifies an object that describes the selection, expansion, top, and skip options. See object load [options](../../reference/excel/loadoption.md?product=excel) for details.

## Example: Write values from an array to a range object

The following example shows how to write values from an array to a range object in an Excel worksheet.

The **Excel.run()** function contains a batch of instructions. A proxy object is created to reference a range on the active worksheet (range address = `A1:B2`) and the value of this proxy object is set locally. When `ctx.sync()` is called, the state of the proxy object is synchronized with the corresponding object in Excel. The **sync()** method returns a promise that can be used to chain it with other operations.

```js
// Run a batch operation against the Excel object model. 
// The ctx input parameter provides access to objects in the Excel document.
Excel.run(function (ctx) {
  // Create a proxy object for the sheet
  const sheet = ctx.workbook.worksheets.getActiveWorksheet();

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
  return ctx.sync()
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

## Example: Copy values from one range to another

The following example shows how to copy the values from range `A1:A2` to range `B1:B2` in the active worksheet, by using the **load()** method to retrieve the values of the first range and then using those values to populate the second range.

```js
Excel.run(function (ctx) {
  // Create a proxy object for the range and load the values property
  const range = ctx.workbook.worksheets.getActiveWorksheet().getRange('A1:A2').load('values');

  // Synchronize the state between JavaScript proxy objects and real objects in Excel 
  // by executing instructions that have been queued on the context
  return ctx.sync()
    .then(function () {
      // Assign the previously loaded values to the new range proxy object. 
      // The values will be updated once the following .then() function is invoked.
      ctx.workbook.worksheets.getActiveWorksheet().getRange('B1:B2').values = range.values;
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

## Load properties and relationships

By default, **object.load()** loads all scalar and complex properties of the object; the relationships (for example, **format** on a **Range** object) are not loaded by default. To optimize performance, you should explicitly specify the properties and relationships to be loaded when calling the **object.load()** method. For example, if you only intend to read back the **address** property of a range object, specify that property in the load call: `range.load('address')`.

The **load()** method accepts three different types of input parameter:

* Property and relationship names as a comma-separated string.
```js
object.load('var1, relation1/var2');
```

* Property and relationship names as an array of strings. 
```js
object.load(['var1', 'relation1/var2']);
```

* An object that specifies the selection, expansion, top, and skip options, as described in [Object Load Options](../../reference/excel/loadoption.md).

In the following example, only specific properties and relationships of the range are loaded. Because `format/font` is not loaded, the value of the `format.font.color` property cannot be read.

```js
Excel.run(function (ctx) {
  const sheetName = 'Sheet1';
  const rangeAddress = 'A1:B2';
  const myRange = ctx.workbook.worksheets.getItem(sheetName).getRange(rangeAddress);

  myRange.load(['address', 'format/*', 'format/fill', 'entireRow' ]);

  return ctx.sync()
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
const range = ctx.workbook.worksheets.getActiveWorksheet().getRange('A:B');
range.values = 'Due Date';
```

## Read or write to a large range

"Large range" implies a range that is too large for a single API call. Many factors such as number of cells, values, number formats, and formulas contained in a range can make the response so large that it becomes unsuitable for API interaction. The API will make a best attempt to execute the requested operation (i.e., to retrieve or write the specified data), but attempting to perform read or write operations for a large range may result in an API error due to excessive resource utilization. To avoid such errors, we recommend that you execute separate read or write operations for smaller subsets of a large range, instead of attempting to execute a single read or write operation for the large range.

## Update all cells in a range

To apply the same update to all cells in a range, (for example, to populate all cells in a range with the same value, set the same number format for all cells in a range, or populate all cells in a range with the same formula), simply set the corresponding property on **range** object to the desired (single) value.

The following example gets a range that contains 20 cells and then sets the number format for all cells in the range and populates all cells in the range with the value **3/11/2015**. 

```js
Excel.run(function (ctx) {
  const sheetName = 'Sheet1';
  const rangeAddress = 'A1:A20';
  const worksheet = ctx.workbook.worksheets.getItem(sheetName);
  
  const range = worksheet.getRange(rangeAddress);
  range.numberFormat = 'm/d/yyyy';
  range.values = '3/11/2015';
  range.load('text');

  return ctx.sync()
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

When an API error occurs, the API will return an **error** object that consists of a code and a message. The following table provides a list of errors that the API may return.

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
* [Explore snippets with Script Lab](excel-add-ins-script-lab.md?product=excel)
* [Excel add-ins code samples](http://dev.office.com/code-samples#?filters=excel,office%20add-ins)
* [Excel JavaScript API reference](../../reference/excel/excel-add-ins-reference-overview.md?product=excel)
