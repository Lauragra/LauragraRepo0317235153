# Excel JavaScript API advanced concepts

This article describes some of the advanced topics of Excel JavaScript API that are essential to building complex add-ins for Excel 2016. 

## Load method 

The `load` method instructs Excel API to load the object into JavaScript memory upon the `sync` operation. It is used to read scalar or navigation properties of the object. `load` method accepts a string with comma delimited property names or an object that specifies properties, pagination options, etc. `load` method is available on each of the Excel JavaScript objects. 

Note that an empty `load()` method will load all of the scalar properties of an object and on collections, loads all of scalar properties of individual objects in the collection. Hence, empty `load()` method should be avoided to reduce the amount of data transfer between Excel application/host and add-in. 

### Method Details

### load(param: object)
Fills the proxy object created in JavaScript layer with property and object values specified in the parameter.

#### Syntax
```js
object.load(param);
```

#### Parameters
| Parameter	   | Type	|Description|
|:---------------|:--------|:----------|
|param|object|Optional. Accepts parameter and relationship names as delimited string or an array. An object can also be passed as shown below to set the selection and navigation properties|

#### Returns
void

#### Example

The following example sets the properties of one Excel range by copying the properties of another range. Note that the source object must be loaded first. The example assumes there is data two ranges, B2:E2 and B7:E7, and that they are initially formatted differently.

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

	            return ctx.sync()        
	        })     
	}).catch(function(error) {
			console.log("Error: " + error);
			if (error instanceof OfficeExtension.Error) {
				console.log("Debug info: " + JSON.stringify(error.debugInfo));
			}
	});
```

The `load` method also accepts an object with following properties. 

### Load option properties
| Property	   | Type	|Description|
|:---------------|:--------|:----------|
|select|object|Contains a comma delimited list or an array of parameter/relationship names. Optional.|
|expand|object|Contains a comma delimited list or an array of relationship names. Optional.|
|top|int| Specifies the maximum number of collection items that can be included in the result. Optional. You can only use this option when you use the object notation option.|
|skip|int|Specify the number of items in the collection that are to be skipped and not included in the result. If `top` is specified, the result set will start after skipping the specified number of items. Optional. You can only use this option when you use the object notation option.|


The sample below loads workskeet collection by selecting (loading) name property, and address of the used range for each of the worksheet. It also specifies that the top 5 worksheets be loaded. If you wish to process the next set of 5 worksheets, use `top: 10` and `skip: 5` values. 

```js 
	myWorksheets.load({
                select: 'name, userRange/address',
		        expand: 'tables',
		        top: 5,
		        skip: 0
	        });
```


## Scalar and navigation properties 

Throughout the Excel JavaScript API reference documentation, you may notce that the object members are distinguished between properties and relationships or navigation properties. Properties are regular scalar members such as strings or integers or boolean values. The navigation properties are members that are either objects or collection of objects. For example, `name` and `position` members on `worksheet` object are scalar properties, whereas `usedRange`, `tables` are navigation properties. The key differences to note between the two are:

* The empty `load()` method by default does not load the navigation properties. 
* The navigation properties cannot be loaded directly. Instead the load method should be used to reference individual scalar properties within the desired navigation property. Example: `someRange.load("address, format/font/name")`

Excel JavaScript allows setting scalar properties of a navigation property by traversing the path. For instance, `someRange.format.font.size` scalar property could be directly set without loading it first. 


## object.set method

Setting properties on an object with nested navigation properties can be cumbersome. Instead of setting individual properties and nested statements, developers can use `set` method available on all of Excel's objects. This method sets multiple properties of an object at once by passing either another object of the same Office type or a JavaScript object with properties that are structured isomorphically to the properties of the object on which the method is called.

> Note: This method is implemented only on the objects of the host-specific Office JavaScript APIs, such as Excel JavaScript objects. The method is not supported on the sommon APIs. 

### set (properties: object, options: object)
The *non-read-only* properties of the object on which the method is called are set to the same values as the corresponding properties of the passed-in object.
If the `properties` parameter is a JavaScript object, then properties in the passed-in object that correspond to a read-only property in the object on which the method is called are either ignored or cause an exception, depending on the `options` parameter.

#### Syntax

```js
object.set(properties[, options]);
```

#### Parameters

| Parameter	   | Type	|Description|
|:---------------|:--------|:----------|
|properties|object|Either an object *of the same Office type* on which the method is called, or a JavaScript object of property names and values that mirrors the structure of the properties of the object type on which the method is called.|
|options|object|Optional. Can only be passed when the first parameter is a JavaScript object. The object can contain the following property: `throwOnReadOnly?: boolean` (Default is `true`: throw an error if the passed in JavaScript object includes read-only properties.)|

#### Returns

void    

#### Examples

The following example sets several Excel format properties with a JavaScript object. The example assumes that there is data in range B2:E2.

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


## *OrNull objects

Many of the APIs returns exception when the condition of the API is not met. For example, if you attempt to get a worksheet based on the name that doesn't exist, the API returns `ItemNotFound` exception. If the scenario is to create a worksheet only if the worksheet doesn't exist, then the structure of the code can be complex as the business logic now needs to be handleded through exception handling functions. In order to make the code flow better, some of the Excel JavaScript APIs contain `OrNullObject` varient that returns a null object (not the JavaScript `null`). Common example is `getItemOrNullObject` on various collections such as `worksheets` collection. 

The null object is returned consists of `isNullObject` boolean property that can be checked to see if the object exists or not.

```js
	let dataSheet = context.workbook.worksheets.getItemOrNullObject("Data"); 
	if (dataSheet.isNullObject) { 
		// Create the sheet
		}
	)
	dataSheet.position = 1;
	//...

```

