---
Description: If your app does not provide good keyboard access, users who are blind or have mobility issues can have difficulty using your app or may not be able to use it at all.
title: Keyboard accessibility
ms.assetid: DDAE8C4B-7907-49FE-9645-F105F8DFAD8B
label: Keyboard accessibility
template: detail.hbs
---

Keyboard accessibility
=================================================================================

\[ Updated for UWP apps on Windows 10. For Windows 8.x articles, see the [archive](http://go.microsoft.com/fwlink/p/?linkid=619132) \]


If your app does not provide good keyboard access, users who are blind or have mobility issues can have difficulty using your app or may not be able to use it at all.

<span id="keyboard_navigation_among_UI_elements"></span><span id="keyboard_navigation_among_ui_elements"></span><span id="KEYBOARD_NAVIGATION_AMONG_UI_ELEMENTS"></span>Keyboard navigation among UI elements
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

To use the keyboard with a control, the control must have focus, and to receive focus (without using a pointer) the control must be accessible in a UI design via tab navigation. By default, the tab order of controls is the same as the order in which they are added to a design surface, listed in XAML, or programmatically added to a container.

In most cases, the default order based on how you defined controls in XAML is the best order, especially because that is the order in which the controls are read by screen readers. However, the default order does not necessarily correspond to the visual order. The actual display position might depend on the parent layout container and certain properties that you can set on the child elements to influence the layout. To be sure your app has a good tab order, test this behavior yourself. Especially if you have a grid metaphor or table metaphor for your layout, the order in which users might read versus the tab order could end up different. That's not always a problem in and of itself. But just make sure to test your app's functionality both as a touchable UI and as a keyboard-accessible UI and verify that your UI makes sense either way.

You can make the tab order match the visual order by adjusting the XAML. Or you can override the default tab order by setting the [**TabIndex**](https://msdn.microsoft.com/library/windows/apps/BR209461) property, as shown in the following example of a [**Grid**](https://msdn.microsoft.com/library/windows/apps/BR242704) layout that uses column-first tab navigation.

<span codelanguage="XAML"></span>
<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">XAML</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><pre><code>&lt;!--Custom tab order.--&gt; 
&lt;Grid&gt;
  &lt;Grid.RowDefinitions&gt;...&lt;/Grid.RowDefinitions&gt;
  &lt;Grid.ColumnDefinitions&gt;...&lt;/Grid.ColumnDefinitions&gt;

  &lt;TextBlock Grid.Column=&quot;1&quot; HorizontalAlignment=&quot;Center&quot;&gt;Groom&lt;/TextBlock&gt;
  &lt;TextBlock Grid.Column=&quot;2&quot; HorizontalAlignment=&quot;Center&quot;&gt;Bride&lt;/TextBlock&gt;

  &lt;TextBlock Grid.Row=&quot;1&quot;&gt;First name&lt;/TextBlock&gt;
  &lt;TextBox x:Name=&quot;GroomFirstName&quot; Grid.Row=&quot;1&quot; Grid.Column=&quot;1&quot; TabIndex=&quot;1&quot;/&gt;
  &lt;TextBox x:Name=&quot;BrideFirstName&quot; Grid.Row=&quot;1&quot; Grid.Column=&quot;2&quot; TabIndex=&quot;3&quot;/&gt;

  &lt;TextBlock Grid.Row=&quot;2&quot;&gt;Last name&lt;/TextBlock&gt;
  &lt;TextBox x:Name=&quot;GroomLastName&quot; Grid.Row=&quot;2&quot; Grid.Column=&quot;1&quot; TabIndex=&quot;2&quot;/&gt;
  &lt;TextBox x:Name=&quot;BrideLastName&quot; Grid.Row=&quot;2&quot; Grid.Column=&quot;2&quot; TabIndex=&quot;4&quot;/&gt;
&lt;/Grid&gt;</code></pre></td>
</tr>
</tbody>
</table>

You may want to exclude a control from the tab order. You typically do this only by making the control noninteractive, for example by setting its [**IsEnabled**](https://msdn.microsoft.com/library/windows/apps/BR209419) property to **false**. A disabled control is automatically excluded from the tab order. But occasionally you might want to exclude a control from the tab order even if it is not disabled. In this case, you can set the [**IsTabStop**](https://msdn.microsoft.com/library/windows/apps/BR209422) property to **false**.

Any elements that can have focus are usually in the tab order by default. The exception to this is that certain text-display types such as [**RichTextBlock**](https://msdn.microsoft.com/library/windows/apps/BR227565) can have focus so that they can be accessed by the clipboard for text selection; however, they're not in the tab order because it is not expected for static text elements to be in the tab order. They're not conventionally interactive (they can't be invoked, and don't require text input, but do support the [Text control pattern](https://msdn.microsoft.com/library/windows/desktop/Ee671194) that supports finding and adjusting selection points in text). Text should not have the connotation that setting focus to it will enable some action that's possible. Text elements will still be detected by assistive technologies, and read aloud in screen readers, but that relies on techniques other than finding those elements in the practical tab order.

Whether you adjust [**TabIndex**](https://msdn.microsoft.com/library/windows/apps/BR209461) values or use the default order, these rules apply:

-   UI elements with [**TabIndex**](https://msdn.microsoft.com/library/windows/apps/BR209461) equal to 0 are added to the tab order based on declaration order in XAML or child collections.
-   UI elements with [**TabIndex**](https://msdn.microsoft.com/library/windows/apps/BR209461) greater than 0 are added to the tab order based on the **TabIndex** value.
-   UI elements with [**TabIndex**](https://msdn.microsoft.com/library/windows/apps/BR209461) less than 0 are added to the tab order and appear before any zero value. This potentially differs from HTML's handling of its **tabindex** attribute (and negative **tabindex** was not supported in older HTML specifications).

<span id="keyboard_navigation_within_a_UI_element"></span><span id="keyboard_navigation_within_a_ui_element"></span><span id="KEYBOARD_NAVIGATION_WITHIN_A_UI_ELEMENT"></span>Keyboard navigation within a UI element
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

For composite elements, it is important to ensure proper inner navigation among the contained elements. A composite element can manage its current active child to reduce the overhead of having all child elements able to have focus. Such a composite element is included in the tab order, and it handles keyboard navigation events itself. Many of the composite controls already have some inner navigation logic built into the into control's event handling. For example, arrow-key traversal of items is enabled by default on the [**ListView**](https://msdn.microsoft.com/library/windows/apps/BR242878), [**GridView**](https://msdn.microsoft.com/library/windows/apps/BR242704view), [**ListBox**](https://msdn.microsoft.com/library/windows/apps/BR242868) and [**FlipView**](https://msdn.microsoft.com/library/windows/apps/BR242678) controls.

<span id="keyboard_activation"></span><span id="KEYBOARD_ACTIVATION"></span>Keyboard alternatives to pointer actions and events for specific control elements
-------------------------------------------------------------------------------------------------------------------------------------------------------------

Ensure that UI elements that can be clicked can also be invoked by using the keyboard. To use the keyboard with a UI element, the element must have focus. Only classes that derive from [**Control**](https://msdn.microsoft.com/library/windows/apps/BR209390) support focus and tab navigation.

For UI elements that can be invoked, implement keyboard event handlers for the Spacebar and Enter keys. This makes the basic keyboard accessibility support complete and enables users to accomplish basic app scenarios by using only the keyboard; that is, users can reach all interactive UI elements and activate the default functionality.

In cases where an element that you want to use in the UI cannot have focus, you could create your own custom control. You must set the [**IsTabStop**](https://msdn.microsoft.com/library/windows/apps/BR209422) property to **true** to enable focus and you must provide a visual indication of the focused state by creating a visual state that decorates the UI with a focus indicator. However, it is often easier to use control composition so that the support for tab stops, focus, and Microsoft UI Automation peers and patterns are handled by the control within which you choose to compose your content.

For example, instead of handling a pointer-pressed event on an [**Image**](https://msdn.microsoft.com/library/windows/apps/BR242752), you could wrap that element in a [**Button**](https://msdn.microsoft.com/library/windows/apps/BR209265) to get pointer, keyboard, and focus support.

<span codelanguage="XAML"></span>
<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">XAML</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><pre><code>&lt;!--Don&#39;t do this.--&gt;
&lt;Image Source=&quot;sample.jpg&quot; PointerPressed=&quot;Image_PointerPressed&quot;/&gt;

&lt;!--Do this instead.--&gt;
&lt;Button Click=&quot;Button_Click&quot;&gt;&lt;Image Source=&quot;sample.jpg&quot;/&gt;&lt;/Button&gt;</code></pre></td>
</tr>
</tbody>
</table>

<span id="keyboard_shortcuts"></span><span id="KEYBOARD_SHORTCUTS"></span>Keyboard shortcuts
--------------------------------------------------------------------------------------------

In addition to implementing keyboard navigation and activation for your app, it is a good practice to implement shortcuts for your app's functionality. Tab navigation provides a good, basic level of keyboard support, but with complex forms you may want to add support for shortcut keys as well. This can make your application more efficient to use, even for people who use both a keyboard and pointing devices.

A *shortcut* is a keyboard combination that enhances productivity by providing an efficient way for the user to access app functionality. There are two kinds of shortcut:

-   An *access key* is a shortcut to a piece of UI in your app. Access keys consist of the Alt key plus a letter key.
-   An *accelerator key* is a shortcut to an app command. Your app may or may not have UI that corresponds exactly to the command. Accelerator keys consist of the Ctrl key plus a letter key.

It is imperative that you provide an easy way for users who rely on screen readers and other assistive technology to discover your app's shortcut keys. Communicate shortcut keys by using tooltips, accessible names, accessible descriptions, or some other form of on-screen communication. At a minimum, shortcut keys should be well documented in your app's Help content.

You can document access keys through screen readers by setting the [**AutomationProperties.AccessKey**](https://msdn.microsoft.com/library/windows/apps/Hh759763) attached property to a string that describes the shortcut key. There is also an [**AutomationProperties.AcceleratorKey**](https://msdn.microsoft.com/library/windows/apps/Hh759762) attached property for documenting non-mnemonic shortcut keys, although screen readers generally treat both properties the same way. Try to document shortcut keys in multiple ways, using tooltips, automation properties, and written Help documentation.

The following example demonstrates how to document shortcut keys for media play, pause, and stop buttons.

<span codelanguage="XAML"></span>
<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">XAML</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><pre><code>&lt;Grid KeyDown=&quot;Grid_KeyDown&quot;&gt;

  &lt;Grid.RowDefinitions&gt;
    &lt;RowDefinition Height=&quot;Auto&quot; /&gt;
    &lt;RowDefinition Height=&quot;Auto&quot; /&gt;
  &lt;/Grid.RowDefinitions&gt;

  &lt;MediaElement x:Name=&quot;DemoMovie&quot; Source=&quot;xbox.wmv&quot; 
    Width=&quot;500&quot; Height=&quot;500&quot; Margin=&quot;20&quot; HorizontalAlignment=&quot;Center&quot; /&gt;

  &lt;StackPanel Grid.Row=&quot;1&quot; Margin=&quot;10&quot;
    Orientation=&quot;Horizontal&quot; HorizontalAlignment=&quot;Center&quot;&gt;

    &lt;Button x:Name=&quot;PlayButton&quot; Click=&quot;MediaButton_Click&quot;
      ToolTipService.ToolTip=&quot;Shortcut key: Ctrl+P&quot;
      AutomationProperties.AcceleratorKey=&quot;Control P&quot;&gt;
      &lt;TextBlock&gt;Play&lt;/TextBlock&gt;
    &lt;/Button&gt;

    &lt;Button x:Name=&quot;PauseButton&quot; Click=&quot;MediaButton_Click&quot;
      ToolTipService.ToolTip=&quot;Shortcut key: Ctrl+A&quot; 
      AutomationProperties.AcceleratorKey=&quot;Control A&quot;&gt;
      &lt;TextBlock&gt;Pause&lt;/TextBlock&gt;
    &lt;/Button&gt;

    &lt;Button x:Name=&quot;StopButton&quot; Click=&quot;MediaButton_Click&quot;
      ToolTipService.ToolTip=&quot;Shortcut key: Ctrl+S&quot; 
      AutomationProperties.AcceleratorKey=&quot;Control S&quot;&gt;
      &lt;TextBlock&gt;Stop&lt;/TextBlock&gt;
    &lt;/Button&gt;

  &lt;/StackPanel&gt;

&lt;/Grid&gt;</code></pre></td>
</tr>
</tbody>
</table>

**Important**  Setting [**AutomationProperties.AcceleratorKey**](https://msdn.microsoft.com/library/windows/apps/Hh759762) or [**AutomationProperties.AccessKey**](https://msdn.microsoft.com/library/windows/apps/Hh759763) doesn't enable keyboard functionality. It only reports to the UI Automation framework what keys should be used, so that such information can be passed on to users via assistive technologies. The implementation for key handling still needs to be done in code, not XAML. You will still need to attach handlers for [**KeyDown**](https://msdn.microsoft.com/library/windows/apps/BR208941) or [**KeyUp**](https://msdn.microsoft.com/library/windows/apps/BR208942) events on the relevant control in order to actually implement the keyboard shortcut behavior in your app. Also, the underline text decoration for an access key is not provided automatically. You must explicitly underline the text for the specific key in your mnemonic as inline [**Underline**](https://msdn.microsoft.com/library/windows/apps/BR209982) formatting if you wish to show underlined text in the UI.

 

For simplicity, the preceding example omits the use of resources for strings such as "Ctrl+A". However, you must also consider shortcut keys during localization. Localizing shortcut keys is relevant because the choice of key to use as the shortcut key typically depends on the visible text label for the element.

For more guidance about implementing shortcut keys, see [Shortcut keys](http://go.microsoft.com/fwlink/p/?linkid=221825) in the Windows User Experience Interaction Guidelines.

### <span id="Implementing_a_key_event_handler"></span><span id="implementing_a_key_event_handler"></span><span id="IMPLEMENTING_A_KEY_EVENT_HANDLER"></span>Implementing a key event handler

Input events such as the key events use an event concept called *routed events*. A routed event can bubble up through the child elements of a composited control, such that a common control parent can handle events for multiple child elements. This event model is convenient for defining shortcut key actions for a control that contains several composite parts that by design cannot have focus or be part of the tab order.

For example code that shows how to write a key event handler that includes checking for modifiers such as the Ctrl key, see [Keyboard interactions](https://msdn.microsoft.com/library/windows/apps/Mt185607).

<span id="Keyboard_navigation_for_custom_controls"></span><span id="keyboard_navigation_for_custom_controls"></span><span id="KEYBOARD_NAVIGATION_FOR_CUSTOM_CONTROLS"></span>Keyboard navigation for custom controls
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

We recommend the use of arrow keys as keyboard shortcuts for navigating among child elements, in cases where the child elements have a spacial relationship to each other. If tree-view nodes have separate sub-elements for handling expand-collapse and node activation, use the left and right arrow keys to provide keyboard expand-collapse functionality. If you have an oriented control that supports directional traversal within the control content, use the appropriate arrow keys.

Generally you implement custom key handling for custom controls by including an override of [**OnKeyDown**](https://msdn.microsoft.com/library/windows/apps/BR209390_onkeydown) and [**OnKeyUp**](https://msdn.microsoft.com/library/windows/apps/BR209390_onkeyup) methods as part of the class logic.

<span id="An_example_of_a_visual_state_for_a_focus_indicator"></span><span id="an_example_of_a_visual_state_for_a_focus_indicator"></span><span id="AN_EXAMPLE_OF_A_VISUAL_STATE_FOR_A_FOCUS_INDICATOR"></span>An example of a visual state for a focus indicator
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

We mentioned earlier that any custom control that enables the user to focus it should have a visual focus indicator. Usually that focus indicator is as simple as drawing a rectangle shape immediately around the control's normal bounding rectangle. The [**Rectangle**](https://msdn.microsoft.com/library/windows/apps/BR243371) for visual focus is a peer element to the rest of the control's composition in a control template, but is initially set with a [**Visibility**](https://msdn.microsoft.com/library/windows/apps/BR208992) value of **Collapsed** because the control isn't focused yet. Then, when the control does get focus, a visual state is invoked that specifically sets the **Visibility** of the focus visual to **Visible**. Once focus is moved elsewhere, another visual state is called, and the **Visibility** becomes **Collapsed**.

All of the default XAML controls will display an appropriate visual focus indicator when focused (if they can be focused). There are also potentially different looks depending on the user's selected theme (particularly if the user is using a high contrast mode.) If you're using the XAML controls in your UI and not replacing the control templates, you don't need to do anything extra to get visual focus indicators on controls that behave and display correctly. But if you're intending to retemplate a control, or if you're curious about how XAML controls provide their visual focus indicators, the remainder of this section explains how this is done in XAML and in the control logic.

Here's some example XAML that comes from the default XAML template for a [**Button**](https://msdn.microsoft.com/library/windows/apps/BR209265).

<span codelanguage="XAML"></span>
<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">XAML</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><pre><code>&lt;ControlTemplate TargetType=&quot;Button&quot;&gt;
... 
    &lt;Rectangle 
      x:Name=&quot;FocusVisualWhite&quot; 
      IsHitTestVisible=&quot;False&quot; 
      Stroke=&quot;{ThemeResource FocusVisualWhiteStrokeThemeBrush}&quot; 
      StrokeEndLineCap=&quot;Square&quot; 
      StrokeDashArray=&quot;1,1&quot; 
      Opacity=&quot;0&quot; 
      StrokeDashOffset=&quot;1.5&quot;/&gt;
    &lt;Rectangle 
      x:Name=&quot;FocusVisualBlack&quot; 
      IsHitTestVisible=&quot;False&quot; 
      Stroke=&quot;{ThemeResource FocusVisualBlackStrokeThemeBrush}&quot; 
      StrokeEndLineCap=&quot;Square&quot; 
      StrokeDashArray=&quot;1,1&quot; 
      Opacity=&quot;0&quot; 
      StrokeDashOffset=&quot;0.5&quot;/&gt;
...
&lt;/ControlTemplate&gt;</code></pre></td>
</tr>
</tbody>
</table>

So far this is just the composition. To control the focus indicator's visibility, you define visual states that toggle the [**Visibility**](https://msdn.microsoft.com/library/windows/apps/BR208992) property. This is done using the [**VisualStateManager.VisualStateGroups**](https://msdn.microsoft.com/library/windows/apps/Hh738505) attached property, as applied to the root element that defines the composition.

<span codelanguage="XAML"></span>
<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">XAML</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><pre><code>&lt;ControlTemplate TargetType=&quot;Button&quot;&gt;
  &lt;Grid&gt;
    &lt;VisualStateManager.VisualStateGroups&gt; 
       &lt;!--other visual state groups here--&gt;
       &lt;VisualStateGroup x:Name=&quot;FocusStates&quot;&gt; 
         &lt;VisualState x:Name=&quot;Focused&quot;&gt; 
           &lt;Storyboard&gt; 
             &lt;DoubleAnimation 
               Storyboard.TargetName=&quot;FocusVisualWhite&quot; 
               Storyboard.TargetProperty=&quot;Opacity&quot; 
               To=&quot;1&quot; Duration=&quot;0&quot;/&gt;
             &lt;DoubleAnimation 
               Storyboard.TargetName=&quot;FocusVisualBlack&quot; 
               Storyboard.TargetProperty=&quot;Opacity&quot; 
               To=&quot;1&quot; Duration=&quot;0&quot;/&gt;
         &lt;/VisualState&gt; 
         &lt;VisualState x:Name=&quot;Unfocused&quot; /&gt; 
         &lt;VisualState x:Name=&quot;PointerFocused&quot; /&gt; 
       &lt;/VisualStateGroup&gt;
     &lt;VisualStateManager.VisualStateGroups&gt;
&lt;!--composition is here--&gt;
   &lt;/Grid&gt;
&lt;/ControlTemplate&gt;</code></pre></td>
</tr>
</tbody>
</table>

Note how only one of the named states adjusts [**Visibility**](https://msdn.microsoft.com/library/windows/apps/BR208992) directly whereas the others are seemingly empty. The way that visual states work is that as soon as the control uses another state from the same [**VisualStateGroup**](https://msdn.microsoft.com/library/windows/apps/BR209014), any animations applied by the previous state are immediately canceled. Because the default **Visibility** from composition is **Collapsed**, this means the rectangle will not appear. The control logic controls this by listening for focus events like [**GotFocus**](https://msdn.microsoft.com/library/windows/apps/BR208927) and changing the states with [**GoToState**](https://msdn.microsoft.com/library/windows/apps/BR209025). Often this is already handled for you if you are using a default control or customizing based on a control that already has that behavior.

<span id="_Keyboard_accessibility_and_Windows_Phone"></span><span id="_keyboard_accessibility_and_windows_phone"></span><span id="_KEYBOARD_ACCESSIBILITY_AND_WINDOWS_PHONE"></span> Keyboard accessibility and Windows Phone
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

A Windows Phone device typically doesn't have a dedicated, hardware keyboard. However, a Soft Input Panel (SIP) can support several keyboard accessibility scenarios. Screen readers can read text input from the **Text** SIP, including announcing deletions. Users can discover where their fingers are because the screen reader can detect that the user is scanning keys, and it reads the scanned key name aloud. Also, some of the keyboard-oriented accessibility concepts can be mapped to related assistive technology behaviors that don't use a keyboard at all. For example, even though a SIP won't include a Tab key, Narrator supports a touch gesture that's the equivalent of pressing the Tab key, so having a useful tab order through the controls in a UI is still an important accessibility principle. Arrow keys as used for navigating the parts within complex controls are also supported through Narrator touch gestures. Once focus has reached a control that's not for text input, Narrator supports a gesture that invokes that control's action.

Keyboard shortcuts aren't typically relevant for Windows Phone apps, because a SIP won't include Control or Alt keys.

## Related topics

* [Accessibility](accessibility.md)
* [Keyboard interactions](https://msdn.microsoft.com/library/windows/apps/Mt185607)
* [Input: Touch keyboard sample](http://go.microsoft.com/fwlink/p/?linkid=246019)
* [Responding to the appearance of the on-screen keyboard sample](http://go.microsoft.com/fwlink/p/?linkid=231633)
* [XAML accessibility sample](http://go.microsoft.com/fwlink/p/?linkid=238570)
 

 





<!--HONumber=May16_HO4-->


