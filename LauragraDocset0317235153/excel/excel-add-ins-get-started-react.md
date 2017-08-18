# Create an Excel add-in using React

## Step 1. Generate the React project by **Create React App**

If you never install [Create React App](https://github.com/facebookincubator/create-react-app) before, first install it globally.

```bash
npm install -g create-react-app
```

Then generate your React app by

```bash
create-react-app my-addin
```

## Step 2. Generate the manifest file by **YO Office**.

If you never install [Yeoman](https://github.com/yeoman/yo) and [YO Office](https://github.com/OfficeDev/generator-office) before, first install them globally.

```bash
npm install -g yo generator-office
```

Go to your app folder.

```bash
cd my-addin
```

Generate the manifest file following the steps in the screenshot below.

```bash
yo office
```

![Yeoman generator](/images/yo-office.png)

You should be able to see your manifest file with the name ends with **manifest.xml**.

To run the add-in, you need side-load the add-in within the Excel application. Follow the way below to side-load the manifest file:

* Windows

  Follow [this tutorial](https://dev.office.com/docs/add-ins/testing/create-a-network-shared-folder-catalog-for-task-pane-and-content-add-ins).

* macOS

  Move the manifest file to the folder `/Users/{username}/Library/Containers/com.microsoft.Excel/Data/Documents/wef` \(if the folder does not exist, create one\)

* Excel Online

  Click **Upload My Add-in** button to upload the manifest file.

  ![Excel Online upload](/images/excel-online-upload.png)

## Step 3. Initialize

Open **public/index.html**, add

```html
<script src="https://appsforoffice.microsoft.com/lib/beta/hosted/office.debug.js"></script>
```

before `</head>` tag.

Open **src/index.js**, add `Office.initialize` out of `ReactDOM.render(<App />, document.getElementById('root'));` like below:

```typescript
Office.initialize = () => {
  ReactDOM.render(<App />, document.getElementById('root'));
};
```

## Step 4. Add "Color Me"

Open **src/App.js**. Replace by

```javascript
import React, { Component } from 'react';

const Excel = window.Excel;

class App extends Component {
  constructor(props) {
    super(props);

    this.onColorMe = this.onColorMe.bind(this);
  }

  onColorMe() {
    Excel.run(async (context) => {
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

## Step 5. Run

Run the dev server through the terminal.

* Windows

  ```bash
    set HTTPS=true&&npm start
  ```

* macOS

  ```bash
   HTTPS=true npm start
  ```

Open Excel and click your add-in to load.

Congratulations you just finish your first React add-in for Excel!

