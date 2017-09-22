# Excel JavaScript API advanced concepts

This article builds upon the information in [Excel JavaScript API core concepts](excel-add-ins-core-concepts.md) to describe some of the more advanced concepts that are essential to building complex add-ins for Excel 2016. 

## Office.js APIs for Excel

An Excel add-in interacts with objects in Excel by using the JavaScript API for Office, which includes two JavaScript object models:

* **Excel JavaScript API**: Introduced with Office 2016, the [Excel JavaScript API](../../reference/excel/excel-add-ins-reference-overview.md?product=excel) provides strongly-typed objects that you can use to access worksheets, ranges, tables, charts, and more. 

* **Common APIs**: Introduced with Office 2013, the common APIs (also referred to as the [Shared API](../../reference/add-ins/javascript-api-for-office.md?product=excel)) can be used to access features such as UI, dialogs, and client settings that are common across multiple types of host applications such as Word, Excel, and PowerPoint.

While you'll likely use the Excel JavaScript API to develop the majority of functionality in add-ins that target Excel 2016, you'll also use objects in the Shared API. For example:

- [Context](../../reference/shared/context.md): The **Context** object represents the runtime environment of the add-in and provides access to key objects of the API. It consists of workbook configuration details such as `contentLanguage` and `officeTheme` and also provides information about the add-in's runtime environment such as `host` and `platform`. Additionally, it provides the `requirements.isSetSupported()` method, which you can use to check whether the specified requirement set is supported by the Excel application where the add-in is running. 

- [Document](../../reference/shared/document.md): The **Document** object provides the `getFileAsync()` method, which you can use to download the Excel file where the add-in is running. 

## Requirement sets

Requirement sets are named groups of API members. An Office Add-in can perform a runtime check or use requirement sets specified in the manifest to determine whether an Office host supports the APIs that the add-in needs. To identify the specific requirement sets that are available on each supported platform, see [Excel JavaScript API requirement sets](../reference/requirement-sets/excel-api-requirement-sets.md).

### Checking for requirement set support at runtime

The following code sample shows how to determine whether the host application where the add-in is running supports the specified API requirement set.

```js
if (Office.context.requirements.isSetSupported('ExcelApi', 1.3) === true) {
  /// perform actions
}
else {
  /// provide alternate flow/logic
}
```

### Defining requirement set support in the manifest

You can use the [Requirements element](../reference/manifest/requirements.md) in the add-in manifest to specify the minimal requirement sets and/or API methods that your add-in requires to activate. If the Office host or platform doesn't support the requirement sets or API methods that are specified in the **Requirements** element of the manifest, the add-in won't run in that host or platform, and won't display in the list of add-ins that are shown in **My Add-ins**. 

The following code sample shows the **Requirements** element in an add-in manifest which specifies that the add-in should load in all Office host applications that support ExcelApi requirement set version 1.3 or greater.

```xml
<Requirements>
   <Sets DefaultMinVersion="1.3">
      <Set Name="ExcelApi" MinVersion="1.3"/>
   </Sets>
</Requirements>
```

**Note**: To make your add-in available on all platforms of an Office host, such as Excel for Windows, Excel Online, and Excel for iPad, we recommend that you check for requirement support at runtime instead of defining requirement set support in the manifest.

### Requirement sets for the Office.js Common API

For information about common API requirement sets, see [Office common API requirement sets](../reference/requirement-sets/office-add-in-requirement-sets.md).

## Loading the properties of an object

The `load()` method instructs the Excel API to load the object into JavaScript memory when the `sync()` method runs. The `load` method is available on each of the Excel JavaScript objects and can be used to read scalar properties or navigation properties of an object. The `load` method accepts a string that contains comma-delimited property names or an object that specifies properties, pagination options, etc. 

**Note**: If you call the `load()` method on an object (or collection) without specifying any parameters, all scalar properties of the object (or all scalar properties of all objects in the collection) will be loaded. To reduce the amount of data transfer between the Excel host application and the add-in, you should avoid calling the `load()` method without explicitly specifying which properties to load.

### Method details

#### load(param: object)

Fills the proxy object created in JavaScript layer with property and object values specified by the parameters.

#### Syntax

```js
object.load(param);
```

#### Parameters

|**Parameter**|**Type**|**Description**|
|:------------|:-------|:----------|
|`param`|object|Optional. Accepts parameter and relationship names as comma-delimited string or an array. An object can also be passed to set the selection and navigation properties (as shown in the example below).|

#### Returns

void

#### Example

The following code sample sets the properties of one Excel range by copying the properties of another range. Note that the source object must be loaded first, before its property values can be accessed and written to the target range. This example assumes that there is data the two ranges (**B2:E2** and **B7:E7**) and that the two ranges are initially formatted differently.

```js
Excel.run(function (ctx) { 
	var sheet = ctx.workbook.worksheets.getItem("Sample");
	var sourceRange = sheet.getRange("B2:E2");
	sourceRange.load("format/fill/color, format/font/name, format/font/color");

	return ctx.sync()
		.then(function () {
			var targetRange = sheet.getRange("B7:E7");
			targetRange.set(sourceRange); 
			targetRange.format.autofitColumns();

			return ctx.sync();
		});
}).catch(function(error) {
	console.log("Error: " + error);
	if (error instanceof OfficeExtension.Error) {
		console.log("Debug info: " + JSON.stringify(error.debugInfo));
	}
});
```

### Load option properties

As an alternative to passing a comma-delimited string or array when you call the `load()` method, you can pass an object that contains the following properties. 

|**Property**|**Type**|**Description**|
|:-----------|:-------|:----------|
|`select`|object|Contains a comma-delimited list or an array of parameter/relationship names. Optional.|
|`expand`|object|Contains a comma-delimited list or an array of relationship names. Optional.|
|`top`|int| Specifies the maximum number of collection items that can be included in the result. Optional. You can only use this option when you use the object notation option.|
|`skip`|int|Specify the number of items in the collection that are to be skipped and not included in the result. If `top` is specified, the result set will start after skipping the specified number of items. Optional. You can only use this option when you use the object notation option.|

The following code sample loads a workskeet collection by selecting the `name` property and the `address` of the used range for each worksheet in the collection. It also specifies that only the top five worksheets in the collection should be loaded. You could process the next set of five worksheets by specifying `top: 10` and `skip: 5` as attribute values. 

```js 
myWorksheets.load({
	select: 'name, userRange/address',
	expand: 'tables',
	top: 5,
	skip: 0
});
```

## Scalar and navigation properties 

In the Excel JavaScript API reference documentation, you may notice that object members are grouped into two categories: **properties** and **relationships**. A property of an object is a scalar member such as a string, an integer, or a boolean value, while a relationship of an object (also known as a navigation property) is a member that is either an object or collection of objects. For example, `name` and `position` members on the [Worksheet](../reference/excel/worksheet.md) object are scalar properties, whereas `protection` and `tables` are relationships (navigation properties). 

### Loading properties of an object

Calling the `object.load()` method with no parameters specified will not load the navigation properties of the object. Only the scalar properties of the object will be loaded. Additionally, navigation properties cannot be loaded directly. Instead, you should use the `load()` method to reference individual scalar properties within the desired navigation property. For example, to load the font name for a range, you must specify the **format** and **font** navigation properties as the path to the **name** property:

```js
someRange.load("format/font/name")
```

You can use the Excel JavaScript API to set scalar properties of a navigation property by traversing the path. For instance, the scalar property `someRange.format.font.size` could be directly set without loading it first. 

## Setting properties of an object

Setting properties on an object with nested navigation properties can be cumbersome. Instead of setting individual properties and nested statements, developers can use `set` method available on all of Excel's objects. This method sets multiple properties of an object at once by passing either another object of the same Office type or a JavaScript object with properties that are structured isomorphically to the properties of the object on which the method is called.

- **Note**: This method is implemented only on the objects of the host-specific Office JavaScript APIs, such as Excel JavaScript objects. The method is not supported on the sommon APIs. 

### set (properties: object, options: object)

The *non-read-only* properties of the object on which the method is called are set to the same values as the corresponding properties of the passed-in object.
If the `properties` parameter is a JavaScript object, then properties in the passed-in object that correspond to a read-only property in the object on which the method is called are either ignored or cause an exception, depending on the `options` parameter.

#### Syntax

```js
object.set(properties[, options]);
```

#### Parameters

|**Parameter**|**Type**|**Description**|
|:------------|:--------|:----------|
|`properties`|object|Either an object *of the same Office type* on which the method is called, or a JavaScript object of property names and values that mirrors the structure of the properties of the object type on which the method is called.|
|`options`|object|Optional. Can only be passed when the first parameter is a JavaScript object. The object can contain the following property: `throwOnReadOnly?: boolean` (Default is `true`: throw an error if the passed in JavaScript object includes read-only properties.)|

#### Returns

void    

#### Examples

The following example sets several Excel format properties with a JavaScript object. The example assumes that there is data in range **B2:E2**.

```js
Excel.run(function (ctx) { 
	var sheet = ctx.workbook.worksheets.getItem("Sample");
	var range = sheet.getRange("B2:E2");
	range.set({
		format: {
			fill: {
				color: '#4472C4'
			},
			font: {
				name: 'Verdana',
				color: 'white'
			}
		}
	})
	range.format.autofitColumns();
	return ctx.sync(); 
}).catch(function(error) {
	console.log("Error: " + error);
	if (error instanceof OfficeExtension.Error) {
		console.log("Debug info: " + JSON.stringify(error.debugInfo));
	}
});
```
## &#42;OrNull objects

Many of the APIs returns exception when the condition of the API is not met. For example, if you attempt to get a worksheet based on the name that doesn't exist, the API returns `ItemNotFound` exception. If the scenario is to create a worksheet only if the worksheet doesn't exist, then the structure of the code can be complex as the business logic now needs to be handleded through exception handling functions. In order to make the code flow better, some of the Excel JavaScript APIs contain `OrNullObject` varient that returns a null object (not the JavaScript `null`). Common example is `getItemOrNullObject` on various collections such as `worksheets` collection. 

The null object is returned consists of `isNullObject` boolean property that can be checked to see if the object exists or not.

```js
let dataSheet = context.workbook.worksheets.getItemOrNullObject("Data"); 
if (dataSheet.isNullObject) { 
    // Create the sheet
}

dataSheet.position = 1;
//...
```

## Additional resources
 
* [Excel JavaScript API core concepts](excel-add-ins-core-concepts.md?product=excel)
* [Excel add-ins code samples](http://dev.office.com/code-samples#?filters=excel,office%20add-ins)
* [Excel JavaScript API reference](../../reference/excel/excel-add-ins-reference-overview.md?product=excel)
