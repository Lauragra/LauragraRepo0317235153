# Error handling

Accounting for run time errors is critical given the asynchronous nature of the add-in and batching of API instructions. Throughout the documentation code snippets you will notice that `catch` statements accompany `run` method in order to catch any errors happening inside of the `run` batch. We recommend the same pattern be used anytime Excel JavaScript APIs are called. 

The Excel JavaScript APIs return an error object when an API fails to run successfully. The error object consists of error `code`, `message`, and in some cases `debugInfo` properties to help with debugging. 

Error code returns strings such as `InvalidReference` that are part of `OfficeExtension.ErrorCodes` or `Excel.ErrorCodes` list. The error codes are not localized. The error message returns summary of the error in the localized string. Note that the error message is not intended for end user consumption and developers should show the right error messaging to the end users based on the error code and relevant business logic. The `debugInfo` when present gives more information for developers to help understand the root cause of the error. 

```js
 try {  
 	await Excel.run(async (context) => 
	 	{ 
	 		// API calls 
	 		await context.sync(); 
	 	}); 
 	} catch (e) { 
 		 errorHandlerFunction(e);  
 	}
```

Note that the `console.log()` usage will result in error message to be shown on the server side. The users will not see any errors in the add-in taskpane or anywhere in the host application.
