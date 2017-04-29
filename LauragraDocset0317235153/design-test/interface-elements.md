# Office UI elements

Developers use Office UI elements to extend the Office UI. The following Office UI elements look like a natural extension of Office, allow you to insert your custom web-based code, and works across platforms.

* __Add-in Commands__ which start actions in your add-in by either running JavaScript code, or launching an HTML container. There are two types of add-in commands available:
  * __Ribbon Buttons, Menus & Tabs__ which can be used to add custom buttons, menus (dropdowns) or tabs to the default ribbon in Office. Buttons and menus are used to trigger an action in Office. Tabs are used to group and organize buttons and menus. 
  * __Context Menus__ which extends the default context menu. Context menus are displayed when users right-click text or an Excel table cell in an Office document. 
* __HTML Containers__ are used to embed HTML-based UI code within Office clients. These web pages can then reference the Office JavaScript API to interact with content in the document. There are 3 types of HTML containers available:
  * __Task Panes__ which display custom UI in the right pane of the Office document. Use task panes when side-by-side usage interaction is necessary between your add-in and the Office document. 
  * __Content add-ins__ which display custom UI embedded within Office documents. Use content add-ins when your add-in is meant to be a part of the page, worksheet or slide. For example, you may want to show external content such as videos or data visualizations from other sources. 
  *  __Dialog__ which displays custom UI in a dialog on top of Office. Use a dialog when usage should be focused within the dialog, and does not require interaction with the Office document.

## Related Resources

- [Add-in commands for Excel, Word, and PowerPoint](add-in-commands.md)
- [Task panes in Office Add-ins](task-pane-add-ins.md)
- [Content add-ins](content-add-ins.md)
- [Dialog boxes in Office Add-ins](dialog-boxes.md)