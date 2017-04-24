# TextField Component in Office UI Fabric

The TextField component in add-in enables a user to type text. It's typically used to capture a single line of text but can be configured to capture multiple lines of text. The text displays on the screen in a simple, uniform format.
  
#### Example: Breadcrumb on a task pane

img
* example image to place the component in context.

## Best Practices

img
* Do - Use the TextField to accept data input on a form or page.
* Don't - Don’t use a TextField to render basic copy as part of a body element of a page.

img
* Do - Label the TextField with a helpful name.
* Don't - Don’t provide an unlabeled TextField and expect that users will know what to do with it.

img
* Do - Provide concise helper text that specifies what content is expected to be entered.
* Don't - Don’t be overly verbose with helper text.

img
* Do - When part of a form, provide clear designations for which fields are required vs. optional.
* Don't - Don’t place a TextField inline with body copy.

img
* Do - Provide all appropriate states for the control (static, hover, focus, engaged, unavailable, error).
* Don't - Don’t occlude the entry or allow entry when the active content is not visible.

<table>
    <tr>
        <th>Do</th>
        <th>Don't</th>
    </tr>
    <tr>
        <td>Make the width of your text-fields about a third wider than the longest anticipated input.</td>
        <td>Don’t use a text-field if the valid input options can be pre-defined. Consider using a dropdown instead.</td>
    </tr>
    <tr>
        <td>Limit the length of allowable input text.</td>
        <td>Don’t use a text-field for date or time entry. Consider using a datetime picker instead.</td>
    </tr>
    <tr>
        <td>When stacking many text-fields, try to group them together with group headings to make the amount of text-fields less overwhelming and scannable.</td>
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
        <td><h4>Default TextField<h4></td>
        <td>Disabled uncontrolled Dropdown with defaultSelectedKey</td>
        <td>img</td>
    </tr>
    <tr>
        <td><h4>Disabled TextField<h4></td>
        <td></td>
        <td>img</td>
    </tr>
    <tr>
        <td><h4>Required TextField<h4></td>
        <td></td>
        <td>img</td>
    </tr>
    <tr>
        <td><h4>TextField with a placeholder<h4></td>
        <td></td>
        <td>img</td>
    </tr>
    <tr>
        <td><h4>Multiline TextField<h4></td>
        <td></td>
        <td>img</td>
    </tr>
</table>

## Implementation

For details, see [TextField](https://dev.office.com/fabric#/components/textfield) on the Office UI Fabric website.

## Additional Resources
* [UX Pattern Sample](https://office.visualstudio.com/DefaultCollection/OC/_git/GettingStarted-FabricReact)
* [GitHub Development Resources](https://github.com/OfficeDev/Office-Add-in-UX-Design-Patterns-Code)