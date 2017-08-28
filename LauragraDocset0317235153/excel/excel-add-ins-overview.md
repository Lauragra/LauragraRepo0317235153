# Excel add-ins overview

An Excel add-in is a web app that runs in Excel and can interact with objects in the workbook where it runs. Excel add-ins enable third parties to extend the functionality of Excel by adding custom ribbon buttons or menu commands, inserting task panes, opening dialog boxes, and even embedding rich, web-based objects such as charts or interactive visualizations within a workbook. 

The [Office Add-ins platform](../overview/office-add-ins.md) enables you to create an Excel add-in that delivers the following key benefits:

* Cross-platform support: Excel add-ins will run in Office for Windows, Mac, iOS, and Office Online.
* Centralized deployment and distribution: Admins can quickly and easily deploy Excel add-ins across an organization.
* Single sign on (SSO): Easily integrate your Excel add-in with users' Office 365 accounts.
* Standard web technology: Create your Excel add-in using familiar web technologies such as HTML, CSS, and JavaScript, and use any library you like.
* Office Store: Share your Excel add-in with a broad audience by publishing it to the [Office Store](https://store.office.com/en-us/appshome.aspx)

> **Note**: Excel add-ins are different from COM and VSTO add-ins, which are earlier Office integration solutions that run only on Office for Windows. Unlike COM add-ins, Excel add-ins do not require you to install any code to the user's device or to the Excel client itself. 

## Anatomy of an Excel add-in 

- An Office Add-in is a web app that you can host anywhere. It runs in an Office application. A manifest.xml file specifies where the web app is located and how it should appear.


## Capabilities of an Excel add-in

(intro) -- subsections showing each of these things? or just summary paragraph(s), with link(s) to more detailed topic(s) in Core Concepts
** also mention: like any web app, an Excel add-in can call REST APIs, which means it can use Microsoft Graph or any other REST API
** maybe change TOC "Extension points" to "Extend Excel functionality" instead -- more understandable, more applicable to all 5 things...
** maybe change TOC "Get started" to "Quickstart" within Excel section?

### Task panes

### Add-in commands

### Content 

### Dialogs

## JavaScript APIs for Excel

- introduce Office.js
- explain availability of / difference between Shared APIs (2013) and Excel APIs (2016)
- discuss host support?
- mention requirement sets (and link to more detailed topic)?
- link to...?

## Next steps

- link to (Excel) 'Get started' topics
- link to Core Concepts

## Additional resources

- Office Add-ins platform overview
- Excel JavaScript API reference
- Get started (Excel)
- Core concepts (Excel)

