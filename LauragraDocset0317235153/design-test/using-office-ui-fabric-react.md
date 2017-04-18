#Use Office UI Fabric in Office Add-ins

If you are building an Office Add-in, we encourage you to use [Office UI Fabric](https://dev.office.com/fabric) to create your user experience. 

Office UI Fabric is a JavaScript front-end framework for building user experiences for Office and Office 365. Fabric provides visuals-focused components that you can extend, rework, and use in your Office Add-in. Because Fabric uses the Office Design Language, Fabric's UX components look like a natural extension of Office.

Fabric consists of several projects:

- **Fabric Core** - Contains the core elements of the design language such as icons, colors, type, and grid. Both Fabric JS and Fabric React use Fabric Core. 
- **Fabric React (recommended)** - Implements the UX components using the React framework.
- **Fabric JS** - Implements UX components using JavaScript only. Use Fabric JS if you don't want to take a dependency on the React framework.  

The following sections walk you through the basics of using Fabric Core and Fabric React.



##Use Fabric Core.
Fabric core provides the main elements of the design language including fonts, types, icons and branded assets available
look at Fabric site to get what it provides. 
Include the guidance on using the icons and fonts. 

##2. Use Fabric icons and fonts
Using icons is simple. All you have to do is use an "i" element and reference the appropriate classes. You can control the size of the icon by changing the font size. For example, the following code shows how to make an extra-large table icon that uses the themePrimary (#0078d7) color. 
   
    <i class="ms-Icon ms-font-xl ms-Icon--Table ms-fontColor-themePrimary"></i>

To find more icons that are available in Office UI Fabric, use the search feature on the [Icons](https://dev.office.com/fabric#/styles/icons) page. When you find an icon to use in your add-in, be sure to prefix the icon name with `ms-Icon--`. 

For information about font sizes and colors that are available in Office UI Fabric, see [Typography](https://dev.office.com/fabric#/styles/typography) and [Colors](https://dev.office.com/fabric#/styles/colors).


##Use Fabric React components.
follow these steps

When you use the Fabric React components as described in this section, you don't need a separate refernce to Fabric Core. 

#Where do the recommended components go?

###1. Create your project with the Yeoman generator for Office. 

To create an add-in that uses Fabric React, we recommend that you use the Yeoman generator for Office. The Yeoman generator for Office provides the project scaffolding and build management needed to develop and Office add-in. For more information on getting started with the Yeoman generator, see [Create an Office Add-in using any editor](https://dev.office.com/docs/add-ins/get-started/create-an-office-add-in-using-any-editor) and [https://github.com/OfficeDev/generator-office](https://github.com/OfficeDev/generator-office).

>Important: Ensure you use **Windows PowerShell**, not the command prompt, to run the commands. 

After running `npm start`, a browser window opens that displays a spinner. To view the full UI of the add-in, ensure you sideload your manifest and then open the add-in. For more information, see [Sideload Office Add-ins for testing](https://dev.office.com/docs/add-ins/testing/create-a-network-shared-folder-catalog-for-task-pane-and-content-add-ins).

###4. Add a Fabric React Button
To add a button to your add-in, perform the following steps:



create button file
go to the Fabric site button page
copy and paste the code
add imports statement to index.html
add <button>
add some click code
View the change




##3. Use Fabric JS UX components

Fabric provides several UX components, like buttons or checkboxes, that you can use in your add-in. The following is a list of the Fabric JS UX components that we recommend for use in an add-in. To use one of the Fabric components in your add-in, follow the link to the Fabric documentation, and then follow the instructions in **Using this component**.

> **Note:** We will add additional components over time. 

- [Breadcrumb](https://dev.office.com/fabric-js/Components/Breadcrumb/Breadcrumb.html)
- [Button](https://dev.office.com/fabric-js/Components/Button/Button.html) (Consider using the small button variant in your add-in. Add 16px of padding to small buttons to ensure a 40px minimum touch target on touch devices.)
- [Checkbox](https://dev.office.com/fabric-js/Components/CheckBox/CheckBox.html)
- [ChoiceFieldGroup](https://dev.office.com/fabric-js/Components/ChoiceFieldGroup/ChoiceFieldGroup.html)
- [Date Picker](https://dev.office.com/fabric-js/Components/DatePicker/DatePicker.html) (For an example that shows how to implement the Date Picker in an add-in, see the [Excel Sales Tracker](https://github.com/OfficeDev/Excel-Add-in-JavaScript-SalesTracker) code sample.)
- [Dropdown](https://dev.office.com/fabric-js/Components/Dropdown/Dropdown.html)
- [Label](https://dev.office.com/fabric-js/Components/Label/Label.html)
- [Link](https://dev.office.com/fabric-js/Components/Link/Link.html)
- [List](https://dev.office.com/fabric-js/Components/List/List.html) (Consider changing the component's default styles in the CSS.)
- [MessageBanner](https://dev.office.com/fabric-js/Components/MessageBanner/MessageBanner.html)
- [MessageBar](https://dev.office.com/fabric-js/Components/MessageBar/MessageBar.html)
- [Overlay](https://dev.office.com/fabric-js/Components/Overlay/Overlay.html)
- [Panel](https://dev.office.com/fabric-js/Components/Panel/Panel.html)
- [Pivot](https://dev.office.com/fabric-js/Components/Pivot/Pivot.html)
- [ProgressIndicator](https://dev.office.com/fabric-js/Components/ProgressIndicator/ProgressIndicator.html)
- [Searchbox](https://dev.office.com/fabric-js/Components/SearchBox/SearchBox.html)
- [Spinner](https://dev.office.com/fabric-js/Components/Spinner/Spinner.html)
- [Table](https://dev.office.com/fabric-js/Components/Table/Table.html)
- [TextField](https://dev.office.com/fabric-js/Components/TextField/TextField.html)
- [Toggle](https://dev.office.com/fabric-js/Components/Toggle/Toggle.html)
  

##Next steps
If you're looking for an end-to-end code sample that shows you how to use Fabric JS, we've got you covered. See the following resource:

- [Excel Sales Tracker](https://github.com/OfficeDev/Excel-Add-in-JavaScript-SalesTracker) 

##Related resources
If you're looking for code samples or documentation on a previous release of Fabric, see the following:

- [UX design patterns (uses Fabric 2.6.1)](https://github.com/OfficeDev/Office-Add-in-UX-Design-Patterns-Code) 
- [Office Add-in Fabric UI sample (uses Fabric 1.0)](https://github.com/OfficeDev/Office-Add-in-Fabric-UI-Sample) 
- [Using Fabric 2.6.1 in an Office Add-in](https://dev.office.com/docs/add-ins/design/ui-elements/using-office-ui-fabric)
 

