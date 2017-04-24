# Toggle Component in Office UI Fabric

In add-in, Toggles represent a physical switch to turn things on or off. Use Toggles to present two mutually exclusive options (e.g. on/off), where choosing an option results in an immediate action.
  
#### Example: Breadcrumb on a task pane

img
* example image to place the component in context.

## Best Practices

img
* Do - Use a Toggle for binary settings when changes become effective immediately after the user changes them.
* Don't - Don’t use a Toggle if it requires user to perform an extra step for changes to be effective.

<table>
    <tr>
        <th>Do</th>
        <th>Don't</th>
    </tr>
    <tr>
        <td>Only replace the On and Off labels if there are more specific labels for the setting. If there are short (3-4 characters) labels that represent binary opposites that are more appropriate for a particular setting, use them.</td>
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
        <td><h4>Enabled and checked<h4></td>
        <td>Disabled uncontrolled Dropdown with defaultSelectedKey</td>
        <td>img</td>
    </tr>
    <tr>
        <td><h4>Enabled and unchecked<h4></td>
        <td></td>
        <td>img</td>
    </tr>
    <tr>
        <td><h4>Disabled and checked<h4></td>
        <td></td>
        <td>img</td>
    </tr>
    <tr>
        <td><h4>Disabled and unchecked<h4></td>
        <td></td>
        <td>img</td>
    </tr>
</table>

## Implementation

For details, see [Toggle](https://dev.office.com/fabric#/components/toggle) on the Office UI Fabric website.

## Additional Resources
* [UX Pattern Sample](https://office.visualstudio.com/DefaultCollection/OC/_git/GettingStarted-FabricReact)
* [GitHub Development Resources](https://github.com/OfficeDev/Office-Add-in-UX-Design-Patterns-Code)