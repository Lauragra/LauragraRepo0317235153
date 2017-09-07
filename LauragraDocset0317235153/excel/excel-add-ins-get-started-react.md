# Build an Excel add-in using React

This article walks you through the process of building an Excel add-in by using React and the Excel JavaScipt API.

## Prerequisites

Get started by completing the following prerequisite tasks:

1. If you haven't done so previously, install [Create React App](https://github.com/facebookincubator/create-react-app) globally.
```bash
npm install -g create-react-app
```

2. If you haven't done so previously, install [Yeoman](https://github.com/yeoman/yo) and the [Yeoman generator for Office Add-ins](https://github.com/OfficeDev/generator-office) globally.
```bash
npm install -g yo generator-office
```

## Generate a new React app

Use Create React App to generate your React app by running the following command.

```bash
create-react-app my-addin
```

## Generate the manifest file and sideload the add-in

An add-in's manifest file defines its settings and capabilities.

1. Navigate to your app folder.
```bash
cd my-addin
```

2. Use the Yeoman generator to generate the manifest file for your add-in by running the following command and then answering the prompts as shown in the screenshot below.
```bash
yo office
```
![Yeoman generator](images/yo-office.png)
>**Note**: If you are prompted to overwrite **package.json**, answer **No** (do not overwrite).

3. Open the manifest file (i.e., the file in the root directory of your app with a name ending in "manifest.xml"). Replace all occurrences of `https://localhost:3000` with `http://localhost:3000` and save your changes.

4. Sideload the add-in within Excel by following the instructions for the platform you'll be using to run your add-in.
    - Windows: [Sideload Office Add-ins for testing on Windows](../testing/create-a-network-shared-folder-catalog-for-task-pane-and-content-add-ins.md)
    - Excel Online: [Sideload Office Add-ins in Office Online](../testing/sideload-office-add-ins-for-testing.md#sideload-an-office-add-in-on-office-online)
    - iPad and Mac: [Sideload Office Add-ins on iPad and Mac](../testing/sideload-an-office-add-in-on-ipad-and-mac.md)

## Update the app: Initialize

1. Open **public/index.html**, add the following `<script>` tag immediately before the `</head>` tag, and save your change.
```html
<script src="https://appsforoffice.microsoft.com/lib/beta/hosted/office.debug.js"></script>
```

2. Open **src/index.js**, replace `ReactDOM.render(<App />, document.getElementById('root'));` with the following code, and save your change. 

```typescript
const Office = window.Office;

Office.initialize = () => {
  ReactDOM.render(<App />, document.getElementById('root'));
};
```

## Update the app: Add "Color Me" functionality 

Open **src/App.js**, replace file contents with the following code, and save your changes. 

```javascript
import React, { Component } from 'react';

class App extends Component {
  constructor(props) {
    super(props);

    this.onColorMe = this.onColorMe.bind(this);
  }

  onColorMe() {
    window.Excel.run(async (context) => {
      const range = context.workbook.getSelectedRange();
      range.format.fill.color = 'green';
      await context.sync();
    });
  }

  render() {
    return (
      <button onClick={this.onColorMe}>Color Me</button>
    );
  }
}

export default App;
```

## Try it out

1. Start the dev server by running one of the following commands via the terminal.
    - Windows:  `set HTTPS=false&&npm start`
    - macOS: `HTTPS=false npm start`

1. Start the dev server by running one of the following commands via the terminal.
```bash
npm start
```
or
```bash
yarn start
```

2. In Excel, on the **Home** tab, choose the **Show Taskpane** button in the ribbon to open the add-in task pane. Choose the **Color Me** button in the task pane to change the background color of the selected range to green.

## Next steps

Congratulations, you've successfully created an Excel add-in using React! Next, check out [Core concepts](excel-add-ins-core-concepts.md?product=excel) to learn more about the fundamentals of building Excel add-ins.


