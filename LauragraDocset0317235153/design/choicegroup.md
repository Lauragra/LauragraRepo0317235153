# ChoiceGroup Component in Office UI Fabric

A Checkbox is a UI element that allows users to select or deselect actions items in add-in. It is used to switch between two mutually exclusive options through a single click and to indicate a subordinate setting or preference when paired with another control.

The control has two selection states: unselected and selected.
  
#### Example: Breadcrumb on a task pane

img 
* example image to place the component in context.

## Best Practices

img
* Do - Use when there are 2-7 options. Make sure there’s enough screen space. Otherwise, use a Checkbox or Dropdown list.
* Don't - Don’t use ChoiceGroup if there are more than 7 options. Use a Dropdown instead.

img
* Do - Use only one ChoiceGroup within a cluster of ChoiceGroup that may be selected at a time.
* Don't - Don’t use two ChoiceGroup for a single binary choice.

img
* Do - List the options in a logical order, such as most likely to be selected to least, simplest operation to most complex, or least risk to most. Alphabetical ordering is not recommended because it is language dependent and therefore not localizable.
* Don't - Don't use the options are numbers that have fixed steps. Instead, use a slide component.

img
* Do - Align radio buttons vertically instead of horizontally, if possible.
* Don't - Don’t align buttons horizontally. Horizontal alignment is harder to read and localize.

<table>
    <tr>
        <th>Do</th>
        <th>Don't</th>
    </tr>
    <tr>
        <td>If none of the options is a valid choice, add another option to reflect this choice, such as "None" or "Does not apply".</td>
        <td>Nest with other ChoiceGroup or CheckBoxes. If possible, keep all the options at the same level.</td>
    </tr>
    <tr>
        <td>Limit the ChoiceGroup label to a single line.</td>
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
        <td><h4>ChoiceGroups<h4></td>
        <td>Pairing a set of content with radio button with a single line label</td>
        <td>img</td>
    </tr>
    <tr>
        <td><h4>ChoiceGroups using Images<h4></td>
        <td>Pairing a set of images with radio button with a single line label</td>
        <td>img</td>
    </tr>
    <tr>
        <td><h4>ChoiceGroups using Icons<h4></td>
        <td>Pairing a set of icons with radio button with a single line label</td>
        <td>img</td>
    </tr>
</table>

## Implementation

For details, see [ChoiceGroup](https://dev.office.com/fabric#/components/choicegroup) on the Office UI Fabric website.

## Additional Resources
* [UX Pattern Sample](https://office.visualstudio.com/DefaultCollection/OC/_git/GettingStarted-FabricReact)
* [GitHub Development Resources](https://github.com/OfficeDev/Office-Add-in-UX-Design-Patterns-Code)