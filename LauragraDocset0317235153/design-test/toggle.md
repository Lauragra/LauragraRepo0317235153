# Toggle Component in Office UI Fabric

In add-ins, Toggles represent a physical switch to turn things on or off. Use Toggles to present two mutually exclusive options (e.g. on/off), where choosing an option results in an immediate action.
  
#### Example: Toggle on a task pane

![An image showing the checkbox](../images/overview_toggle.png)

## Best Practices

|**Do**|**Don't**|
|:------------|:--------------|
|Use a Toggle for binary settings when changes become effective immediately after the user changes them.|Don’t use a Toggle if it requires users to perform an extra step for changes to take effect.|
|![Do ChoiceGroup example](../images/toggleDo.png)|![Don't ChoiceGroup example](../images/toggleDont.png)|

|**Do**|**Don't**|
|:------------|:--------------|
|Only replace the On and Off labels if there are more specific labels for the setting. If there are short (3-4 characters) labels that represent binary opposites that are more appropriate for a particular setting, use them.| |

## Variants

|**Variation**|**Description**|**Example**|
|:------------|:--------------|:----------|
|**Enabled and checked**|Needs description|![Needs image](../images/primary.pn)|
|**Enabled and unchecked**|Needs description|![Needs image](../images/default.pn)|
|**Disabled and checked**|Needs description|![Needs image](../images/default.pn)|
|**Disabled and unchecked**|Needs description|![Needs image](../images/default.pn)|

## Implementation

For details, see [Toggle](https://dev.office.com/fabric#/components/toggle) on the Office UI Fabric website.

## Additional Resources
* [UX Pattern Sample](https://office.visualstudio.com/DefaultCollection/OC/_git/GettingStarted-FabricReact)
* [GitHub Development Resources](https://github.com/OfficeDev/Office-Add-in-UX-Design-Patterns-Code)