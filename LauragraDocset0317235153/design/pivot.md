# Pivot Component in Office UI Fabric

In Add-in, Pivot control, “Tab pattern” are used for quick navigation to frequently accessed, distinct content categories. It allows for navigation between two or more content views and relies on text headers to articulate the different sections of content. Tabs are a visual variant of Pivot that use a combination of icons and text or just icons to articulate section content.
  
#### Example: Breadcrumb on a task pane

![Sample image displaying a primary and secondary button with the context of an Task Pane in an Office app.](../images/exampleButton@450.pn)

## Best Practices

![Sample image displaying a primary and secondary button with the context of an Task Pane in an Office app.](../images/buttonUsage-01.pn)

![Sample image displaying a primary and secondary button with the context of an Task Pane in an Office app.](../images/buttonUsage-01.pn)

![Sample image displaying a primary and secondary button with the context of an Task Pane in an Office app.](../images/buttonUsage-01.pn)

![Sample image displaying a primary and secondary button with the context of an Task Pane in an Office app.](../images/buttonUsage-01.pn)

<table>
    <tr>
        <th>Do</th>
        <th>Don't</th>
    </tr>
    <tr>
        <td>Pivots are stationary when all pivot headers fit within the allowed space.</td>
        <td>Don’t use the Pivot to link to a new page.</td>
    </tr>
    <tr>
        <td>Use Pivots carousel when all pivot headers don't fit within the allowed space.</td>
        <td>Don’t use the Pivot to link to hidden content.</td>
    </tr>
    <tr>
        <td>Pivot headers can contain icons, text or both.</td>
        <td>Don't use the left align option for the icon version as this will result in poor alignments.</td>
    </tr>
    <tr>
        <td>Recommend 3-5 pivot controls. Keep it small.</td>
        <td>Don’t use pivots to scroll the browser to specific content. Use in-page navigation instead.</td>
    </tr>
    <tr>
        <td>Place Pivot control toward the top of page, and not mixed in with page content.</td>
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
        <td><h4>Default Pivot – Text only<h4></td>
        <td>Disabled uncontrolled Dropdown with defaultSelectedKey</td>
        <td><img src="../images/primary.pn" alt="Primary Button Image" ></td>
    </tr>
    <tr>
        <td><h4>Pivot with icons – Text and icons<h4></td>
        <td></td>
        <td><img src="../images/primary.pn" alt="Primary Button Image" ></td>
    </tr>
    <tr>
        <td><h4>Links of Tab Style<h4></td>
        <td></td>
        <td><img src="../images/primary.pn" alt="Primary Button Image" ></td>
    </tr>
    <tr>
        <td><h4>Pivot with Trigger onchange event<h4></td>
        <td></td>
        <td><img src="../images/primary.pn" alt="Primary Button Image" ></td>
    </tr>
    <tr>
        <td><h4>Pivot with Rendering nested components within the Pivot<h4></td>
        <td></td>
        <td><img src="../images/primary.pn" alt="Primary Button Image" ></td>
    </tr>
</table>

## Implementation

For details, see [Pivot](https://dev.office.com/fabric#/components/pivot) on the Office UI Fabric website.

## Additional Resources
* [UX Pattern Sample](https://office.visualstudio.com/DefaultCollection/OC/_git/GettingStarted-FabricReact)
* [GitHub Development Resources](https://github.com/OfficeDev/Office-Add-in-UX-Design-Patterns-Code)