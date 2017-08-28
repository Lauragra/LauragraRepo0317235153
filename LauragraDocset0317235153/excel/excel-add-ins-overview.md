# Excel add-ins overview

> **Note**: This article is a work-in-progress.  

An Excel add-in runs in Excel and can interact with data in the workbook where it is running.

- define Excel add-in

- state value prop of Excel add-in
    - cross platform
    - centralized deployment and distribution
    - SSO (integrate easily with users' Office 365 accounts)
    - just an app -- build with any web technology you want -- use any library you want.
    - Hongbo's list:
        * Cross platform. If you build an add-in using Office.js. It will not only support Windows, Mac, but also iOS, Online version Office.
        * Single sign in. It integrate easily with users' Office 365 account.
        * Centralized deployment and distribution. It helps the admin in the organization easily deploy and apply it to all employees in the corganization.
        * Now we have an [Office store](https://store.office.com/en-us/appshome.aspx). You can submit your add-in in the store. It helps users find the add-in they want.
        * An add-in built by Office.js is using the web technology. It is just a web app. Use any library you want! 

- explain how Excel web add-ins differ from VBA, VSTO, COM (link to those docs)
    > For VSTO, VBA development, please check [here](https://msdn.microsoft.com/en-us/library/fp179694.aspx).

    > how are add-ins different than VBA, COM, VSTO: https://dev.office.com/docs/add-ins/overview/office-add-ins#how-are-office-add-ins-different-than-com-and-vsto-add-ins

good overview info: https://dev.office.com/docs/add-ins/overview/office-add-ins

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

