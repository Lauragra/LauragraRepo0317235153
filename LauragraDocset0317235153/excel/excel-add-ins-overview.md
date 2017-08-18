# Excel Development

    > Content coming soon.

## (Info from Hongbo's 'Introduction' article: Microsoft Graph and Office.js)

> This doc  mainly focuses on Excel part of Office.js. To learn Excel part of Microsoft Graph, please go to [here](https://developer.microsoft.com/en-us/graph/docs/api-reference/v1.0/resources/excel).

In Office development, there are two technologies you will often hear - Microsoft Graph and Office.js.

**What is the difference between Microsoft Graph and Office.js?**

* Microsoft Graph lets you interact with Excel, Outlook, OneDrive, OneNote, Planner, SharePoint, etc. through REST API.

* Office.js lets you interact with Excel without network connection. It helps you build Office Add-ins.

**Which one should I use?**

* If you have an app which needs to interact with Office like Excel through REST APIT, then Microsoft Graph is your choice.

* If you want to build an add-in for Office like Excel to extend its functions, Office.js is your choice. However, you can also use Microsoft Graph in your add-in if neccessary.

## What is Office Add-in

An Office add-in can add features and functions to Excel, Word, PowerPoint, Outlook, OneNote, etc. The add-ins in [Office Store](https://store.office.com/en-us/appshome.aspx) can give you some ideas what an add-in can be done.

## Why Office.js

There are many ways to build an add-in such as VBA, VSTO, and so on. Why do we provide a new way Office.js?

* Cross platform. If you build an add-in using Office.js. It will not only support Windows, Mac, but also iOS, Online version Office.
* Single sign in. It integrate easily with users' Office 365 account.
* Centralized deployment and distribution. It helps the admin in the organization easily deploy and apply it to all employees in the corganization.
* Now we have an [Office store](https://store.office.com/en-us/appshome.aspx). You can submit your add-in in the store. It helps users find the add-in they want.
* An add-in built by Office.js is using the web technology. It is just a web app. Use any library you want! 

> For VSTO, VBA development, please check [here](https://msdn.microsoft.com/en-us/library/fp179694.aspx).



