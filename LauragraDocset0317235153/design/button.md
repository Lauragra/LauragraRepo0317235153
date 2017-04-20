# Buttons Component in Office UI Fabric

Buttons are best used to enable a user to commit a change or complete steps in a task. The text of a button should communicate the intent of the interaction. Therefore, as a guiding pattern for add-ins, buttons are placed at the bottom of the UI container of a task pane, dialogs, or content pane.

For example, use buttons at the end of a form to submit it; to close the end of a dialog, or move to the next settings screen to commit changes.
  
#### Example: Buttons on a task pane

![Sample image displaying a primary and secondary button with the context of an Task Pane in an Office app.](../images/exampleButton@450.png)

## Best Practices

![Sample image displaying a primary and secondary button with the context of an Task Pane in an Office app.](../images/buttonUsage-01.png)

![Sample image displaying a primary and secondary button with the context of an Task Pane in an Office app.](../images/buttonUsage-02.pnG)

<table>
    <tr>
        <th>Do</th>
        <th>Don't</th>
    </tr>
    <tr>
        <td>Use only a single line of text in the label of the button.</td>
        <td>Don’t put too much text in a button – try keep text to a minimum.</td>
    </tr>
    <tr>
        <td>Button should be placed below a related content area the button.</td>
        <td>Don’t place a button at the top of a table or inline.</td>
    </tr>
    <tr>
        <td>Make sure the label conveys a clear purpose of the button to the user.</td>
        <td>Don’t use a button to navigate to another place with exception of “Back” and “Next” buttons, use a link instead.</td>
    </tr>
    <tr>
        <td>Expose only one or two buttons to the user at a time. For example, “Accept” and “Cancel”.</td>
        <td></td>
    </tr>
    <tr>
        <td>“Submit”, “OK”, and “Apply” buttons should always be styled as primary buttons. When “Reset” or “Cancel” buttons appear alongside one of the above, they should be styled as secondary buttons.</td>
        <td></td>
    </tr>
    <tr>
        <td>Task buttons should be used to cause actions to complete a task or cause a transitional task.</td>
        <td></td>
    </tr>
</table>

## Variants

<table>
    <tr>
        <th>Variation</th>
        <th>Description</th>
        <th>Example</th>
    </tr>
    <tr>
        <td><h4>Primary Button<h4></td>
        <td>Inherits theme color at rest state. Use this as the main call to action.</td>
        <td><img src="../images/primary.png" alt="Primary Button Image" ></td>
    </tr>
    <tr>
        <td><h4>Default button<h4></td>
        <td>Default button should always perform safe operations and should never delete.</td>
        <td><img src="../images/default.png" alt="Default Button Image" ></td>
    </tr>
    <tr>
        <td><h4>Compound Button<h4></td>
        <td>Used to cause actions that complete a task or cause a transitional task.</td>
        <td><img src="../images/compound.png" alt="Compound Button Image" ></td>
    </tr>
</table>

## Implementation

For details, see [Button](https://dev.office.com/fabric#/components/button) on the Office UI Fabric website.

## Additional Resources
* [UX Pattern Sample](https://office.visualstudio.com/DefaultCollection/OC/_git/GettingStarted-FabricReact)
* [GitHub Development Resources](https://github.com/OfficeDev/Office-Add-in-UX-Design-Patterns-Code)