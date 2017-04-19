# Office Add-in design language
The Office design language is a clean and simple visual system that insures consistency across experiences. It contains a set of visual elements that define Office interfaces: a common typeface, a standard color palette, a set of typographic sizes and weights, icon guidelines, shared icon assets, animation definitions and common components.

Office UI Fabric is the official front-end framework for building with the Office design language. Use of Fabric is optional but it is the fastest way to insure your add-ins feel like a natural extension. Leverage it to design and build add-ins that complement Office.

Many Office Add-ins are associated with a preexisting brand. A strong brand and its visual or component language need not be discarded. Look for opportunities to retain your own visual language while integrating with Office. Consider ways to swap out Office colors, typography, icons or other stylistic elements with elements of your own brand. Consider ways to follow common add-in layouts or UX design patterns while inserting controls and components familiar to your customers.

Inserting a heavily branded HTML-based UI inside of Office can create dissonance for our customers. Find a balance that fits seamlessly in Office but also clearly aligns with your service or parent brand. When an add-in does not fit with Office it's often because stylistic elements conflict. Typography is to large and off grid. Colors are contrasting or particularly loud. Animations are superfluous and behave dramatically different than Office. The appearance and behavior of controls or components veer too far from Office standards.

##Typography
Segoe is the standard typeface for Office. Use it in your add-in to align with Office task panes, dialogs and content objects. Office UI Fabric gives you access to Segoe. It provides a full type ramp of Segoe with many variations - across font weight and size - in convenient CSS classes. Not all Office UI Fabric sizes and weights will look great in an Office Add-in. To fit harmoniously or avoid conflicts consider using a subset of the Fabric type ramp. Here's a list of Fabric's base classes recommended for use in Office Add-ins.

|Sample |Class |Size |Weight |Recommended Usage |
|------ |----- |---- |------ |----------------- |
| img |.ms-font-xxl |28 px | Segoe Light |<ul><li>This class is larger than all other typographic elements in Office. Use it sparingly to avoid unseating visual hierarchy.</li><li>Avoid use on long strings in constrained spaces.</li><li>Provide ample whitespace around text using this class.</li><li>Commonly used for first run messages, hero elements or other calls to action.</li></ul> |
