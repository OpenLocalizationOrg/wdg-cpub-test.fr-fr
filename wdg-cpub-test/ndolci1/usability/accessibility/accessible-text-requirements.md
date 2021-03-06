---
Description: This topic describes best practices for accessibility of text in an app, by assuring that colors and backgrounds satisfy the necessary contrast ratio.
title: Accessible text requirements
ms.assetid: BA689C76-FE68-4B5B-9E8D-1E7697F737E6
label: Text requirements
template: detail.hbs
---

# Accessible text requirements

\[ Updated for UWP apps on Windows 10. For Windows 8.x articles, see the [archive](http://go.microsoft.com/fwlink/p/?linkid=619132) \]


This topic describes best practices for accessibility of text in an app, by assuring that colors and backgrounds satisfy the necessary contrast ratio. This topic also discusses the Microsoft UI Automation roles that text elements in a Universal Windows Platform (UWP) app can have, and best practices for text in graphics.

## Contrast ratios

Although users always have the option to switch to a high-contrast mode, your app design for text should regard that option as a last resort. A much better practice is to make sure that your app text meets certain established guidelines for the level of contrast between text and its background. Evaluation of the level of contrast is based on deterministic techniques that do not consider color hue. For example, if you have red text on a green background, that text might not be readable to someone with a color blindness impairment. Checking and correcting the contrast ratio can prevent these types of accessibility issues.

The recommendations for text contrast documented here are based on a web accessibility standard, [G18: Ensuring that a contrast ratio of at least 4.5:1 exists between text (and images of text) and background behind the text](http://go.microsoft.com/fwlink/p/?linkid=221823). This guidance exists in the *W3C Techniques for WCAG 2.0* specification.

To be considered accessible, visible text must have a minimum luminosity contrast ratio of 4.5:1 against the background. Exceptions include logos and incidental text, such as text that is part of an inactive UI component.

Text that is decorative and conveys no information is excluded. For example, if random words are used to create a background, and the words can be rearranged or substituted without changing meaning, the words are considered to be decorative and do not need to meet this criterion.

Use color contrast tools to verify that the visible text contrast ratio is acceptable. See [Techniques for WCAG 2.0 G18 (Resources section)](http://www.w3.org/TR/WCAG20-TECHS/G18.html#G18-resources) for tools that can test contrast ratios.

**Note**  Some of the tools listed by Techniques for WCAG 2.0 G18 can't be used interactively with a UWP app. You may need to enter foreground and background color values manually in the tool, or make screen captures of app UI and then run the contrast ratio tool over the screen capture image.

 

## Text element roles

A UWP app can use these default elements (commonly called *text elements* or *textedit controls*):

-   [**TextBlock**](https://msdn.microsoft.com/library/windows/apps/BR209652): role is [**Text**](https://msdn.microsoft.com/library/windows/apps/BR209182)
-   [**TextBox**](https://msdn.microsoft.com/library/windows/apps/BR209683): role is [**Edit**](https://msdn.microsoft.com/library/windows/apps/BR209182)
-   [**RichTextBlock**](https://msdn.microsoft.com/library/windows/apps/BR227565) (and overflow class [**RichTextBlockOverflow**](https://msdn.microsoft.com/library/windows/apps/BR227565overflow)): role is [**Text**](https://msdn.microsoft.com/library/windows/apps/BR209182)
-   [**RichEditBox**](https://msdn.microsoft.com/library/windows/apps/BR227548): role is [**Edit**](https://msdn.microsoft.com/library/windows/apps/BR209182)

When a control reports that is has a role of [**Edit**](https://msdn.microsoft.com/library/windows/apps/BR209182), assistive technologies assume that there are ways for users to change the values. So if you put static text in a [**TextBox**](https://msdn.microsoft.com/library/windows/apps/BR209683), you are misreporting the role and thus misreporting the structure of your app to the accessibility user.

In the text models for XAML, there are two elements that are primarily used for static text, [**TextBlock**](https://msdn.microsoft.com/library/windows/apps/BR209652) and [**RichTextBlock**](https://msdn.microsoft.com/library/windows/apps/BR227565). Neither of these are a [**Control**](https://msdn.microsoft.com/library/windows/apps/BR209390) subclass, and as such neither of them are keyboard-focusable or can appear in the tab order. But that does not mean that assistive technologies can't or won't read them. Screen readers are typically designed to support multiple modes of reading the content in an app, including a dedicated reading mode or navigation patterns that go beyond focus and the tab order, like a "virtual cursor". So don't put your static text into focusable containers just so that tab order gets the user there. Assistive technology users expect that anything in the tab order is interactive, and if they encounter static text there, that is more confusing than helpful. You should test this out yourself with Narrator to get a sense of the user experience with your app when using a screen reader to examine your app's static text.

## Text in graphics

Whenever possible, avoid including text in a graphic. For example, any text that you include in the image source file that is displayed in the app as an [**Image**](https://msdn.microsoft.com/library/windows/apps/BR242752) element is not automatically accessible or readable by assistive technologies. If you must use text in graphics, make sure that the [**AutomationProperties.Name**](https://msdn.microsoft.com/library/windows/apps/Hh759770) value that you provide as the equivalent of "alt text" includes that text or a summary of the text's meaning. Similar considerations apply if you are creating text characters from vectors as part of a [**Path**](https://msdn.microsoft.com/library/windows/apps/BR243355), or by using [**Glyphs**](https://msdn.microsoft.com/library/windows/apps/BR209921).

## Text font size

Many readers have difficulty reading text in an app when that text is using a text font size that's simply too small for them to read. You can prevent this issue by making the text in your app's UI reasonably large in the first place. There are also assistive technologies that are part of Windows, and these enable users to change the view sizes of apps, or the display in general.

-   Some users change dots per inch (dpi) values of their primary display as an accessibility option. That option is available from **Make things on the screen larger** in **Ease of Access**, which redirects to a **Control Panel** UI for **Appearance and Personalization** / **Display**. Exactly which sizing options are available can vary because this depends on the capabilities of the display device.
-   The Magnifier tool can enlarge a selected area of the UI. However, it's difficult to use the Magnifier tool for reading text.

## Text scale factor

Various text elements and controls have an [**IsTextScaleFactorEnabled**](https://msdn.microsoft.com/library/windows/apps/BR209652_istextscalefactorenabled) property. This property has the value **true** by default. When its value is **true**, the setting called **Text scaling** on the phone (**Settings &gt; Ease of access**), causes the text size of text in that element to be scaled up. The scaling will affect text that has a small **FontSize** to a greater degree than it will affect text that has a large **FontSize**. But you can disable that automatic enlargement by setting an element's **IsTextScaleFactorEnabled** property to **false**. Try this markup, adjust the **Text size** setting on the phone, and see what happens to the **TextBlock**s:

```xaml
<TextBlock Text=&quot;In this case, IsTextScaleFactorEnabled has been left set to its default value of true.&quot; 
    Style=&quot;{StaticResource BodyTextBlockStyle}&quot;/>

<TextBlock Text=&quot;In this case, IsTextScaleFactorEnabled has been set to false.&quot; 
    Style=&quot;{StaticResource BodyTextBlockStyle}&quot; IsTextScaleFactorEnabled=&quot;False&quot;/>
```

Please don't disable automatic enlargement routinely, though, because scaling UI text universally across all apps is an important accessibility experience for users and they will expect it to work in your app too.

You can also use the [**TextScaleFactorChanged**](https://msdn.microsoft.com/library/windows/apps/Dn633867) event and the [**TextScaleFactor**](https://msdn.microsoft.com/library/windows/apps/Dn633866) property to find out about changes to the **Text size** setting on the phone. Here’s how:

```csharp
{
    ...
    var uiSettings = new Windows.UI.ViewManagement.UISettings();
    uiSettings.TextScaleFactorChanged += UISettings_TextScaleFactorChanged;
    ...
}

private async void UISettings_TextScaleFactorChanged(Windows.UI.ViewManagement.UISettings sender, object args)
{
    var messageDialog = new Windows.UI.Popups.MessageDialog(string.Format(&quot;It&#39;s now {0}&quot;, sender.TextScaleFactor), &quot;The text scale factor has changed&quot;);
    await messageDialog.ShowAsync();
}
```

The value of **TextScaleFactor** is a double in the range \[1,2\]. The smallest text is scaled up by this amount. You might be able to use the value to, say, scale graphics to match the text. But remember that not all text is scaled by the same factor. Generally speaking, the larger text is to begin with, the less it’s affected by scaling.

These types have an **IsTextScaleFactorEnabled** property:

-   [**ContentPresenter**](https://msdn.microsoft.com/library/windows/apps/BR209378)
-   [**Control**](https://msdn.microsoft.com/library/windows/apps/BR209390) and derived classes
-   [**FontIcon**](https://msdn.microsoft.com/library/windows/apps/Dn279514)
-   [**RichTextBlock**](https://msdn.microsoft.com/library/windows/apps/BR227565)
-   [**TextBlock**](https://msdn.microsoft.com/library/windows/apps/BR209652)
-   [**TextElement**](https://msdn.microsoft.com/library/windows/apps/BR209967) and derived classes

## Related topics

* [Accessibility](accessibility.md)
* [Basic accessibility information](basic-accessibility-information.md)
* [XAML text display sample](http://go.microsoft.com/fwlink/p/?linkid=238579)
* [XAML text editing sample](http://go.microsoft.com/fwlink/p/?linkid=251417)
* [XAML accessibility sample](http://go.microsoft.com/fwlink/p/?linkid=238570)
 

 





<!--HONumber=May16_HO4-->


