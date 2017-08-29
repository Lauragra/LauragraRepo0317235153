# Excel add-ins overview

An Excel add-in is an app that runs in Excel and can interact with content in the workbook where it runs. You can create an Excel add-in that extends the functionality of Excel by adding custom ribbon buttons or menu commands, inserting task panes, opening dialog boxes, or even embedding rich, web-based objects such as charts or interactive visualizations within a workbook. 

The [Office Add-ins platform](../overview/office-add-ins.md) provides the framework and APIs that enable you to create and run Excel add-ins. By using the Office Add-ins platform to create your Excel add-in, you'll get the following benefits:

* **Cross-platform support**: Excel add-ins run in Office for Windows, Mac, iOS, and Office Online.
* **Centralized deployment**: Admins can quickly and easily deploy Excel add-ins across an organization.
* **Single sign on (SSO)**: Easily integrate your Excel add-in with users' Office 365 accounts.
* **Use of standard web technology**: Create your Excel add-in using familiar web technologies such as HTML, CSS, and JavaScript, and use any library you like.
* **Distribution via the Office Store**: Share your Excel add-in with a broad audience by publishing it to the [Office Store](https://store.office.com/en-us/appshome.aspx).

> **Note**: Excel add-ins are different from COM and VSTO add-ins, which are earlier Office integration solutions that run only on Office for Windows. Unlike COM add-ins, Excel add-ins do not require you to install any code to the user's device or to the Excel client itself. 

## Anatomy of an Excel add-in 

An Excel add-in consists of two main components: an XML manifest file and a web app.

![Excel add-in components](../../images/ExcelAddinComponents.png)

### Manifest

The XML manifest file defines an Excel add-in's settings and capabilities such as: 

* The add-in's display name, description, ID, version, and default locale.
* How the add-in integrates with Excel, including any custom UI that the add-in creates (ribbon buttons, etc.).
* The permissions that the add-in requires, such as reading and writing to the document.
* The location of the add-in's web app.

For more information about the XML manifest file, see [Office Add-ins XML manifest](../overview/add-in-manifests.md).

### Web app 

An Excel add-in's web app can enable the add-in to interact with content in the workbook where it runs, can facilitate a user's interaction with online resources from within Excel, and in general, can do anything that a typical web app may do. For example, an add-in's app may do things such as:

* Create, read, update, and delete data in the workbook (worksheets, ranges, tables, charts, named items, and more).
* Facilitate a user's authentication with an online service by using the standard OAuth 2.0 flow.
* Issue API requests to Microsoft Graph and/or other APIs.

Your app can be hosted on any web server and can be built using any server-side technology that your hosting provider supports, such as ASP.NET, Node.js, PHP, Python, etc. Likewise, you can use any client-side framework for the web app, such as Angular, React, jQuery, etc., or even just use VanillaJS. 

## Capabilities of an Excel add-in

An Excel add-in can add custom ribbon buttons or menu commands, insert task panes, open dialog boxes, and even embed rich, web-based objects such as charts or interactive visualizations within a worksheet, as shown in the following screenshots. For more detailed information about each of these capabilities, see [Core concepts](excel-add-ins-core-concepts.md).

**Custom ribbon buttons**  
![Add-in commands](../../images/Excel_add-in_commands.png)

**Task pane**  
![Add-in dialog box](../../images/Excel_add-in_task_pane.png)

**Dialog box**  
![Add-in dialog box](../../images/Excel_add-in_dialog.png)

**Embedded web-based object**  
![Content add-in](../../images/Excel_add-in_content.png)

## JavaScript APIs for Excel

To interact with Office clients and documents, you use the Office.js JavaScript APIs. 


- introduce Office.js
- explain availability of / difference between Shared APIs (2013) and Excel APIs (2016)
- discuss host support?
- mention requirement sets (and link to more detailed topic)?
- link to...?

## Supported hosts

## Next steps

- link to (Excel) 'Get started' topics
- link to Core Concepts

## Additional resources

- Office Add-ins platform overview
- Excel JavaScript API reference
- Get started (Excel)
- Core concepts (Excel)

