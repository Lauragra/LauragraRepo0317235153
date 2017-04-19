# Use the autoopen feature to open a task pane with a document automatically

Add-ins with commands are launched from a UI control, such as a button on the Ribbon. Some scenarios, however, require a pane to be automatically opened with certain documents without explicit user interaction. The auto-open taskpane feature, part of AddInCommands 1.1 [add link to requirement set page to be created] allows you automatically open a pane in those scenarios.  

[Screenshot here showing a document and pane opened] 

## How is this different from “inserting” a taskpane?  

Add-ins without commands, such as when users run add-ins in Office 2013, are by default inserted into the document, making it stick to that document without any explicit user or developer intent to do so. As a result,  any other user that opens that document is promted to install the add-in and the pane opens.  The challenge with this model is that in many cases users don’t want the add-in to stick with the document, all they want is to use a particular add-in. For example, a student using a dictionary add-in doesn’t want his class-mates or teachers to open that same document and be prompted to install a dictionary add-in.   

In contrast, the auto-open pane feature is driven by the add-in developer as opposed to being a default behavior.  This means that developers explicitly opt-in, or provide affordances for users to opt-in,  to use the feature on specific add-ins and specific documents that require it.  


## Best Practices 

### Do 

* Use add-in commands along with auto-open if your scenario requires a specific pane within your add-in to stick with the document such as: 

o The document can’t function properly without the add-in, for example, a template that without the add-in can’t work.  

o The user is likely to always use the add-in for that document. For example, an add-in that keeps data in synch with an external source, where users will most of the time have the add-in open to keep the data fresh.  

[screenshot here showing stock connector as a good example] 

* Provide users control to turn on/off if a pane in your add-in should auto-open. For example a UI affordance in case users no longer want your add-in to auto-open a pane.  

* Use requirement set detection [add link] to determine if this feature is available and provide a fallback behavior if it isn’t  [likely need to elaborate on how to do this, which essentially to have the requirement set on overrides but still support the non-overrides section ] 

### Don’t 

* Abuse this feature as means to artificially increase usage of your add-in. If it doesn’t make sense for your add-in to automatically open with certain documents you should not use this feature; it 

will annoy users and your add-in might get rejected from the Office store if Microsoft detects an abuse.  

[Add screenshot of add-in, like Wikipedia, that doesn’t make sense to stick] 

* Use this feature as a generic “pinning” capability for panes. This feature doesn’t allow you to pin a specific pane in place, instead, it just lets you to designate ONE page to auto-open along with a document. If your add-in has multiple panes, you can only designate one to auto-open automatically.  

## Implementation 

There are 2 main elements required to use this feature: Tagging a document and spefifying the pane to be opened. 

### Tagging a document 

To trigger auto-open a document must be appropiately tagged. Documents that are not tagged will not trigger auto-open. You can tag a document in 2 main ways, choose the one that makes the most sense for your scenario: 

#### Client side 

Set the appropiate setting using Office.js. Use this method if you need to tag the document as part of your add-in interaction (E.g. as soon as the user creates a binding, or clicks on a UI affordance on your add-in to “pin” it)  

Office.context.document.settings.set("Office.AutoShowTaskpaneWithDocument", true); Office.context.document.settings.saveAsync(); 


#### Server Side 

You can use OpenXML to create/modify a document to add the appropriate tag 

[We need a  sample that shows how to do this…]  


### Specifying the pane to open 

You indicate which pane will be auto-opened on your manifest by specifying a well-known value for the TaskpaneId attibute. 

          <ExtensionPoint xsi:type="PrimaryCommandSurface">             <OfficeTab id="TabHome">               <Group id="Contoso.Group1"> …                 <Control xsi:type="Button" id="Contoso.TaskpaneButton">                …                   <Action xsi:type="ShowTaskpane">                     <TaskpaneId>Office.AutoShowTaskpaneWithDocument</TaskpaneId>                     <SourceLocation resid="Contoso.Taskpane.Url" />                   </Action>                 </Control> … 


Important: The pane that you designate will only automatically open if, by the time the user opens the document, your add-in is already installed on the users device.  If you require to also distribute the add-in with the document, so that users are prompted to install it, you also need to set the pane visibility property to 1, you can only do this server side via OpenXML [link to article/sample to be created]

## Samples and other resources 

Here are some examples that show you how to use this feature.  

[Add link to simple example, Humberto is building one] 

[Add links to related articles, samples] 
