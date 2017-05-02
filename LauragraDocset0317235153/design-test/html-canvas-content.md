# HTML Canvases – Content Add-in
 
Content add-ins are surfaces that can be embedded directly into Word, Excel, or PowerPoint documents. Content add-ins allow users to utilize interface controls that run code to modify documents or display data from a data source for example. Content add-ins should be utilized when embedding functionality directly into the document is needed and/or wanted.  


### Layout

The recommended layout for a content add-in includes the following elements:
* Navigation/Commanding element (optional) - Include some navigational or commanding element such as the CommandBar or Pivot at the top of your add-in with a maximum height of 44 pixels.
* Add-in content
* Branding element (optional) – Include a branding element such as the BrandBar at the bottom of your add-in with a maximum height of 44 pixels.

Image displayed at 1366x768 resolution

![An example image displaying a typical layout for content add-ins.](path-needed)

### Specifications

> Note: When designing for Desktop use we recommend using a 1366x768 resolution. The following specifications for both Office 2016 Desktop and Office 365 Online have been measured using the 1366x768 resolution.

![Image displaying the various content add-in sizes at 1366x768](path-needed)

Office 2016 Desktop & Office 365 Online Content Add-in Sizes:
* Excel: User specified
* PowerPoint: User specified
* Word: User specified

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
