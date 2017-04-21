# Checkbox Component in Office UI Fabric

A Checkbox is a UI element that allows users to select or deselect actions items in add-in. It is used to switch between two mutually exclusive options through a single click and to indicate a subordinate setting or preference when paired with another control.

The control has two selection states: unselected and selected.
  
#### Example: Breadcrumb on a task pane

img 
* example image to place the component in context.

## Best Practices

img 
* Do - Allow users to choose any combination of options when several Checkboxes are grouped together.
* Don't - Don't put two groups of Checkboxes next to each other. Separate the two groups with labels.

img 
* Do - Use Checkbox to facilitate choosing within the collection, while preserving the ability to check or uncheck sub choices.
* Don't - Don’t use a Checkbox when the user can choose only one option from the group, use radio buttons instead.

img 
* Do - Use Checkbox to indicate a status
* Don't - Don’t use Checkbox to show/indicate an action

<table>
    <tr>
        <th>Do</th>
        <th>Don't</th>
    </tr>
    <tr>
        <td>Use a single Checkbox for a subordinate setting, such as with a “remember me?” login scenario with a terms of service agreement.</td>
        <td>Don’t use checkbox as an on/off, instead use a toggle switch</td>
    </tr>
    <tr>
        <td>Use multiple Checkboxes for multi-select scenarios in which a user chooses one or more items from a group of choices that are not mutually exclusive.</td>
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
        <td><h4>Uncontrolled checkbox<h4></td>
        <td>It is typically placed in a horizontal form, under the masthead or navigation of a primary content area</td>
        <td>img</td>
    </tr>
    <tr>
        <td><h4>Uncontrolled checkbox with default checked true<h4></td>
        <td>It is typically placed in a horizontal form, under the masthead or navigation of a primary content area</td>
        <td>img</td>
    </tr>
    <tr>
        <td><h4>Disabled uncontrolled checkbox with default checked true<h4></td>
        <td>It is typically placed in a horizontal form, under the masthead or navigation of a primary content area</td>
        <td>img</td>
    </tr>
    <tr>
        <td><h4>Controlled checkbox<h4></td>
        <td>It is typically placed in a horizontal form, under the masthead or navigation of a primary content area</td>
        <td>img</td>
    </tr>
</table>

## Implementation

For details, see [Checkbox](https://dev.office.com/fabric#/components/checkbox) on the Office UI Fabric website.

## Additional Resources
* [UX Pattern Sample](https://office.visualstudio.com/DefaultCollection/OC/_git/GettingStarted-FabricReact)
* [GitHub Development Resources](https://github.com/OfficeDev/Office-Add-in-UX-Design-Patterns-Code)