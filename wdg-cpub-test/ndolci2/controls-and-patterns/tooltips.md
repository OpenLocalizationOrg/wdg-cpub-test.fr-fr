---
Description: Use a tooltip to reveal more info about a control before asking the user to perform an action.
title: Tooltips
ms.assetid: A21BB12B-301E-40C9-B84B-C055FD43D307
label: Tooltips
template: detail.hbs

---

# Tooltips

\[ Updated for UWP apps on Windows 10. For Windows 8.x articles, see the [archive](http://go.microsoft.com/fwlink/p/?linkid=619132) \]

A tooltip is a short description that is linked to another control or object. Tooltips help users understand unfamiliar objects that aren't described directly in the UI. They display automatically when the user presses and holds or hovers the mouse pointer over a control. The tooltip disappears when the user moves the finger, the mouse pointer, or a pen pointer.

![A tooltip](images/controls/tool-tip.png)

**Important APIs**

-   [**ToolTip class**](https://msdn.microsoft.com/library/windows/apps/br227608)
-   [**ToolTipService class**](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.tooltipservice)

## Is this the right control?

Use a tooltip to reveal more info about a control before asking the user to perform an action. You can also use a tooltip to show the item under the finger during touchdown, so that users know where they are touching. (You should try to find other ways to disambiguate first, such as use a larger control, more spacing, or styling the control's active/hover state.)

When should you use a tooltip? To decide, consider these questions:

-   **Is the info displayed based on pointer hover?**

    If not, use another control. Display tips only as the result of user interaction—never display them on their own.

-   **Does a control have a text label?**

    If not, use a tooltip to provide the label. It is a good programming practice to label most controls and for these you don't need tooltips. Toolbar controls and command buttons with graphic labels need tooltips.

-   **Does an object benefit from a more detailed description or further info?**

    If so, use a tooltip. But the text must be supplemental—that is, not essential to the primary tasks. If it is essential, put it directly in the UI so that users don't have to discover or hunt for it.

-   **Is the supplemental info an error, warning, or status?**

    If so, use another UI element, such as a flyout.

-   **Do users need to interact with the tip?**

    If so, use another control. Users can't interact with tips because moving the mouse makes them disappear.

-   **Do users need to print the supplemental info?**

    If so, use another control.

-   **Will users find the tips annoying or distracting?**

    If so, consider using another solution—including doing nothing at all. If you do use tips where they might be distracting, allow users to turn them off.

One example of a good way to use tooltips is to show a preview of the linked website when users touch a hyperlink.

## Example

A tooltip in the Bing Maps app.

![A tooltip in the Bing Maps app](images/control-examples/tool-tip-maps.png)

## Recommendations

-   Use tooltips sparingly (or not at all). Tooltips are an interruption. A tooltip can be as distracting as a pop-up, so don't use them unless they add significant value.
-   Keep the tooltip text concise. Tooltips are perfect for short sentences and sentence fragments. Large blocks of text are difficult to read and overwhelming.
-   Create helpful, supplemental tooltip text. Tooltip text must be informative. Don't make it obvious or just repeat what is already on the screen. Because tooltip text isn't always visible, it should be supplemental info that users don't have to read. Communicate important info using self-explanatory control labels or in-place supplemental text.
-   Use images when appropriate. Sometimes it's better to use an image in a tooltip. For example, when the user touches a hyperlink, you can use a tooltip to show a preview of the linked page.
-   Don't use a tooltip to display text already visible in the UI. For example, don't put a tooltip on a button that shows the same text of the button unless touching the button blocks its text.
-   Don't put interactive controls inside the tooltip.
-   Don't put images that look like they are interactive inside the tooltip.

Tooltips should be used sparingly, and only when they are adding distinct value for the user who is trying to complete a task. One rule of thumb is that if the information is available elsewhere in the same experience, you do not need a tooltip. A valuable tooltip will clarify an unclear action.


## Related articles

* [**ToolTip class**](https://msdn.microsoft.com/library/windows/apps/br227608)


<!--HONumber=May16_HO4-->


