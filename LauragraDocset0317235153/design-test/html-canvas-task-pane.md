# HTML Canvases – Task Pane
 
Task Panes are interface surfaces typically docked to the right side of the window within Word, PowerPoint, Excel, and Outlook. Task Panes allow users to utilize interface controls that run code to modify documents, emails or display data from a data source for example. Task Pane surfaces should be utilized when embedding functionality directly into the document is not needed or wanted.

### Layout

The recommended layout for a task pane includes the following elements:
* Add-in Name (required) – Include the name of your add-in. We recommend using short descriptive names and avoiding additions like “Add-in,” “For Word,” or “for Office 365.” The short name can prevent the title from being cut off.
* Navigation/Commanding element (optional) - Include some navigational or commanding element such as the CommandBar or Pivot at the top of your add-in with a maximum height of 44 pixels.
* Add-in content
* Branding element (optional) – Include a branding element such as the BrandBar at the bottom of your add-in with a maximum height of 44 pixels. Avoid using the BrandBar component within Outlook for both the desktop and online platforms.

Image displayed at 1366x768 resolution

![An example image displaying a typical layout for task panes.](path-needed)

### Specifications

> Note: When designing for Desktop use we recommend using a 1366x768 resolution. The following specifications for both Office 2016 Desktop and Office 365 Online have been measured using the 1366x768 resolution.

![Image displaying the various Task Pane sizes at 1366x768](path-needed)

Office 2016 Desktop Task Pane Sizes:
* Excel: 320x455 pixels
* Outlook: 348x535 pixels
* PowerPoint: 320x531 pixels
* Word: 320x531 pixels

Office 365 Online Task Pane Sizes:
* Excel: 350x378 pixels
* Outlook Web App: 320x570 pixels
* PowerPoint: 348x391 pixels
* Word: 329x445 pixels

### Personality Menu

> Note: Personality menus can obstruct navigational and commanding elements located near the top right of the add-in. Listed below are the current dimensions of the personality menu on Windows and Mac.

**Windows:** 12x32 pixels

![Image showing the personality meny on Windows Desktop](path-needed)

**Mac:** 26x26 pixels

![Image showing the personality meny on Mac Desktop](path-needed)

Add-in personality menus for Task Panes provide developers the following set of user tools: 
* Get Support – Opens a browser window to display help and support information for the add-in. 
* Select – Sets the focus on the Task Pane. 
* Reload – Reloads the Task Pane window.
* View Source – Allows the user to see the code source of the current page. 
* Show as Saved Image – Allows the user to preview the add-in as a saved image.
* Security Info – Provides security information to the user. 
