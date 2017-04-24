# Pivot Component in Office UI Fabric

In Add-in, Pivot control, “Tab pattern” are used for quick navigation to frequently accessed, distinct content categories. It allows for navigation between two or more content views and relies on text headers to articulate the different sections of content. Tabs are a visual variant of Pivot that use a combination of icons and text or just icons to articulate section content.
  
#### Example: Breadcrumb on a task pane

img
* example image to place the component in context.

## Best Practices

img
* Do - Use on content-heavy pages that require a significant amount of scrolling to access the various sections.
* Don't - Don’t use on pages which doesn’t scroll.

img
* Do - Be concise on the navigation labels, ideally one or two words rather than a phrase.
* Don't - Don’t use full sentences or complex punctuation (colons, semicolons, etc.).

img
* Do - When there are two levels of pivots, the top-level and sub-level headers should have enough visual differentiation so that users can clearly separate the two.
* Don't - Don’t nest pivots more than two levels (top-level/sub-level pattern).

img
* Do - Pivot headers should persist on-screen.
* Don't - Don’t use pivots to navigate to another page. Use link navigation instead.

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
        <td>img</td>
    </tr>
    <tr>
        <td><h4>Pivot with icons – Text and icons<h4></td>
        <td></td>
        <td>img</td>
    </tr>
    <tr>
        <td><h4>Links of Tab Style<h4></td>
        <td></td>
        <td>img</td>
    </tr>
    <tr>
        <td><h4>Pivot with Trigger onchange event<h4></td>
        <td></td>
        <td>img</td>
    </tr>
    <tr>
        <td><h4>Pivot with Rendering nested components within the Pivot<h4></td>
        <td></td>
        <td>img</td>
    </tr>
</table>

## Implementation

For details, see [Pivot](https://dev.office.com/fabric#/components/pivot) on the Office UI Fabric website.

## Additional Resources
* [UX Pattern Sample](https://office.visualstudio.com/DefaultCollection/OC/_git/GettingStarted-FabricReact)
* [GitHub Development Resources](https://github.com/OfficeDev/Office-Add-in-UX-Design-Patterns-Code)