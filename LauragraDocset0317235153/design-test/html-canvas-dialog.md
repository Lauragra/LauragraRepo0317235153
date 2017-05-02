# HTML Canvases – Dialog
 
Dialogs are surfaces that float above the active Office application window. Dialogs allow you to provide additional screen space for tasks such as sign-in pages that cannot be opened directly in a task pane, confirming an action taken by a user that could potentially destroy document data, and host videos that may be too small if confined to a task pane for example.

> Note: Because overlapping UI can annoy users, avoid opening a dialog from a task pane unless your scenario requires it.

### Layout

Dialog layouts vary depending on use. Dialogs include the following elements:
* Title (required) - Include a descriptive title that includes your add-in name along with the current task at hand. 
* Dialog content – Dialog content includes browser content, notifications with action buttons, and sign in experiences.  

Image displayed at 1366x768 resolution

![An example image displaying a typical layout for a dialog.](path-needed)

### Specifications

> Note: When designing for Desktop use we recommend using a 1366x768 resolution. The following specifications for both Office 2016 Desktop and Office 365 Online have been measured using the 1366x768 resolution.

![Image displaying a client dialog at 1366x768](path-needed)

![Image displaying a embedded dialog at 1366x768](path-needed)

Office 2016 Desktop & Office 365 Online Content Add-in Sizes:
* Embedded Dialog: need measurements 
* Client Dialog: 50% of the viewport width by 50% of the viewport height
