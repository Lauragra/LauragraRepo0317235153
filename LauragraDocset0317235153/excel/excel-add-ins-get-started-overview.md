# Get started with Excel add-ins

    > Content coming soon.

## (Info from Hongbo's 'Quick Start' article)

An add-in built by Office.js has two parts: the **web app** and the **manifest file**. The manifest file tells Office where should find the app.

Let's see a simple app which changes the color of the range in Excel.

```typescript
Excel.run(context => {
  const range = context.workbook.getSelectedRange();
  range.format.fill.color = 'blue';

  return context.sync();
});
```

`Excel.run()` executes a batch script that performs actions on the Excel object model. The batch commands include definitions of local JavaScript proxy objects and `sync()` methods that synchronize the state between local and Excel objects and promise resolution.

The `run()` method takes in RequestContext and returns a promise \(typically, just the result of context.sync\(\)\).

> The advantage of batching requests in `Excel.run()` is that when the promise is resolved, any tracked range objects that were allocated during the execution will be automatically released. It is possible to run the batch operation outside of the `Excel.run()`. However, in such a scenario, any range object references needs to be manually tracked and managed.

The `sync()` method, available on the request context, synchronizes the state between JavaScript proxy objects and real objects in Excel by executing instructions queued on the context and retrieving properties of loaded Office objects for use in your code. This method returns a promise, which is resolved when synchronization is complete.
