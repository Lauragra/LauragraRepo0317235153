#Use Office UI Fabric React in Office Add-ins

If you are building an Office Add-in, we encourage you to use [Office UI Fabric](https://dev.office.com/fabric) to create your user experience. 

Office UI Fabric is a JavaScript front-end framework for building user experiences for Office and Office 365. Fabric provides visuals-focused components that you can extend, rework, and use in your Office Add-in. Because Fabric uses the Office Design Language, Fabric's UX components look like a natural extension of Office.

Fabric consists of several projects:

- **Fabric Core** - Contains the core elements of the design language such as icons, colors, type, and grid. Both Fabric React and Fabric JS use Fabric Core. 
- **Fabric React** - Implements Fabric's UX components using the React framework.
- **Fabric JS** - Implements UX components using JavaScript only.  

The following sections show you how to get started using Fabric Core and Fabric React.

##Use Fabric Core

To get started using Fabric Core in your add-in, perform the following steps:

###1. Add the Fabric CDN reference. 
 
To reference Fabric from the CDN, add the following HTML code to your page.

`<link rel="stylesheet" href="https://static2.sharepointonline.com/files/fabric/office-ui-fabric-js/1.4.0/css/fabric.min.css">`

###2. Use Fabric icons and fonts 

To use a Fabric icon, include the "i" element on your page, and then reference the appropriate classes. You can control the size of the icon by changing the font size. For example, the following code shows how to make an extra-large table icon that uses the themePrimary (#0078d7) color. 
   
`<i class="ms-Icon ms-font-xl ms-Icon--Table ms-fontColor-themePrimary"></i>`

To find more icons that are available in Office UI Fabric, use the search feature on the [Icons](https://dev.office.com/fabric#/styles/icons) page. When you find an icon to use in your add-in, be sure to prefix the icon name with `ms-Icon--`. 

For information about font sizes and colors that are available in Office UI Fabric, see [Typography](https://dev.office.com/fabric#/styles/typography) and [Colors](https://dev.office.com/fabric#/styles/colors).


##Use Fabric React components.

Fabric provides several React-based UX components, like buttons or checkboxes, that you can use in your add-in. To get started using Fabric React's components in your add-in, perform the following steps.

> Note: If you follow the steps in this section, there's no need to add the reference to Fabric Core, as outlined in the previous section.

### Step 1 - Create your project with the Yeoman generator for Office. 

To create an add-in that uses Fabric React, we recommend that you use the Yeoman generator for Office. The Yeoman generator for Office provides the project scaffolding and build management needed to develop an Office add-in. 

To create your project, perform the following steps from [Create an Office Add-in using any editor](https://dev.office.com/docs/add-ins/get-started/create-an-office-add-in-using-any-editor):

1. Install the pre-requisites.
2. Run `yo office` to create the project files for your add-in. 
3. When prompted to select an Office client application, choose **Word**. 
4. Ensure you are in the directory with the project files, and then run `npm start`. A browser window showing a spinner opens automatically.
5. Sideload your manifest to view the full UI of the add-in.    

>**Important**: Use **Windows PowerShell**, not the command prompt, to run the commands to create your project. 

### Step 2 - Add a Fabric React Button

Next, we want to add a button to our add-in. We create a new React component, called **ButtonPrimaryExample**, that consists of a Label and PrimaryButton from Fabric React. To create **ButtonPrimaryExample**, perform the following steps:

1. Open the project folder created by the Yeoman generator, and navigate to **src\components**.
2. Create **button.tsx**.
3. In **button.tsx**, enter the following code to create the **ButtonPrimaryExample** component. 

```
import * as React from 'react';
import { PrimaryButton, IButtonProps } from 'office-ui-fabric-react/lib/Button';
import { Label } from 'office-ui-fabric-react/lib/Label';

export class ButtonPrimaryExample extends React.Component<IButtonProps, {}> {
  public constructor() {
    super();
  }

   insertText = async () => {
        // In the click event, write text to the document. 

        await Word.run(async (context) => {
            var body = context.document.body;  
            body.insertParagraph('Hello Office UI Fabric React!', Word.InsertLocation.end);  
            await context.sync();
        });
    }

  public render() {
    let { disabled } = this.props;

    return (
      <div className='ms-BasicButtonsExample'>
        <Label>Click the button to insert text.</Label>
        <PrimaryButton
          data-automation-id='test'
          disabled={ disabled }
          text='Insert text...'
          onClick={ this.insertText }
        />
      </div>
    );
  }
}
```
The above code does the following:

- References the React library using `import * as React from 'react';`.
- Reference the Fabric components (PrimaryButton, IButtonProps, Label) that are used to create `ButtonPrimaryExample`. 
- Declare and make public the new `ButtonPrimaryExample` component using `export class ButtonPrimaryExample extends React.Component`. 
- Declare the `insertText` function to handle the onclick event. 
- Define the UI of the React component in the `render` function. Render defines the structure of the component. Within `render`, we wire up the onclick event using `this.insertText`.

### Step 3 - Add your React component to your add-in 

Add `ButtonPrimaryExample` to your add-in by opening **src\components\app.tsx** and performing the following steps: 

- Add the following import statement to reference `ButtonPrimaryExample` from **button.tsx** created in step 2 (no file extension is needed): 
`
import {ButtonPrimaryExample} from './button';
` 

- Replace the default `render()` function with the following code that uses `<ButtonPrimaryExample />`. Notice that the default text and button is replaced with the text and primary button defined in `ButtonPrimaryExample`.
```
render() {
        return (
            <div className='ms-welcome'>
                <Header logo='assets/logo-filled.png' title={this.props.title} message='Welcome' />
                <HeroList message='Discover what this add-in can do for you today!' items={this.state.listItems}>                    
                    <ButtonPrimaryExample />
                </HeroList>
            </div>
        );
    };
```

Save your changes. All open browser instances, including the add-in, updates automatically and shows the `ButtonPrimaryExample` React component.  
	
### Recommended components

The following is a list of the Fabric React UX components that we recommend for use in an add-in.  

> **Note:** We will add additional components over time. 

- [Breadcrumb](https://dev.office.com/docs/add-ins/design/add-in-design)
- [Button](https://dev.office.com/docs/add-ins/design/add-in-design) 
- [Checkbox](https://dev.office.com/docs/add-ins/design/add-in-design)
- [ChoiceGroup](https://dev.office.com/docs/add-ins/design/add-in-design)
- [Dropdown](https://dev.office.com/docs/add-ins/design/add-in-design)
- [Label](https://dev.office.com/docs/add-ins/design/add-in-design)
- [Pivot](https://dev.office.com/docs/add-ins/design/add-in-design)
- [TextField](https://dev.office.com/docs/add-ins/design/add-in-design)
- [Toggle](https://dev.office.com/docs/add-ins/design/add-in-design)

##Related resources

- [Getting started with Fabric React code sample](https://github.com/OfficeDev/)
- [UX design patterns (uses Fabric 2.6.1)](https://github.com/OfficeDev/Office-Add-in-UX-Design-Patterns-Code) 
- [Office Add-in Fabric UI sample (uses Fabric 1.0)](https://github.com/OfficeDev/Office-Add-in-Fabric-UI-Sample) 
- [Using Fabric 2.6.1 in an Office Add-in](https://dev.office.com/docs/add-ins/design/ui-elements/using-office-ui-fabric)
- [Yeoman generator for Office](https://github.com/OfficeDev/generator-office)
 

