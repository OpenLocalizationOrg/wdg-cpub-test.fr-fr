---
Description: Describes the steps needed to ensure your Universal Windows Platform (UWP) app is usable when a high-contrast theme is active.
title: High-contrast themes
ms.assetid: FD7CA6F6-A8F1-47D8-AA6C-3F2EC3168C45
label: High-contrast themes
template: detail.hbs
---

# High-contrast themes

\[ Updated for UWP apps on Windows 10. For Windows 8.x articles, see the [archive](http://go.microsoft.com/fwlink/p/?linkid=619132) \]


Describes the steps needed to ensure your Universal Windows Platform (UWP) app is usable when a high-contrast theme is active.

A UWP app supports high-contrast themes by default. If a user has chosen that they want the system to use a high-contrast theme from system settings or accessibility tools, the framework automatically uses colors and style settings that produce a high-contrast layout and rendering for controls and components in the UI.

This default support is based on using the default themes and templates. These themes and templates make references to system colors as resource definitions, and the resource sources change automatically when the system is using a high-contrast mode. However, if you use custom templates, themes, and styles for your control, be careful that you do not disable the built-in support for high contrast. If you use one of the XAML designers for Microsoft Visual Studio for styling, the designer generates a separate, high-contrast theme alongside the primary theme whenever you define a template that is significantly different from the default template. The separate theme dictionaries go into the [**ThemeDictionaries**](https://msdn.microsoft.com/library/windows/apps/BR208807) collection, a dedicated property of a [**ResourceDictionary**](https://msdn.microsoft.com/library/windows/apps/BR208794) element.

For more info on themes and control templates, see [Quickstart: Control templates](https://msdn.microsoft.com/library/windows/apps/xaml/Hh465374). It's often very informative to look at the XAML resource dictionaries and themes for specific controls and see how the themes are constructed and how they reference resources that are similar but different for each possible high-contrast setting.

## Detecting when a high-contrast theme is enabled

A UWP app can use members of the [**AccessibilitySettings**](https://msdn.microsoft.com/library/windows/apps/BR242237) class to detect the current settings for high-contrast themes. The [**HighContrast**](https://msdn.microsoft.com/library/windows/apps/BR242237_highcontrast) property determines whether a high-contrast theme is currently selected. If **HighContrast** is set to **true**, then the next step is to check the value of the [**HighContrastScheme**](https://msdn.microsoft.com/library/windows/apps/BR242237_highcontrastscheme) property to get the name of the high-contrast theme that is used. "High Contrast White" and "High Contrast Black" are typically values for **HighContrastScheme** that your code should respond to. XAML-defined [**ResourceDictionary**](https://msdn.microsoft.com/library/windows/apps/BR208794) keys can't have spaces, so the keys for these themes in a resource dictionary are typically "HighContrastWhite" and "HighContrastBlack" respectively. You should also have fallback logic for a default high-contrast theme in case the value is some other string. [XAML high contrast sample](http://go.microsoft.com/fwlink/p/?linkid=254993) shows the logic for this.

**Note**  Make sure you call the [**AccessibilitySettings**](https://msdn.microsoft.com/library/windows/apps/BR242237) constructor from a scope where the app is initialized and is already displaying content.

 

Apps can switch to using high-contrast resource values while the app is running. This works so long as the resources are requested using the [{ThemeResource} markup extension](https://msdn.microsoft.com/library/windows/apps/Mt185591) in the style or template XAML. The default themes (generic.xaml) all use this {ThemeResource} markup extension technique, so you'll get this behavior if you're using default control themes. Custom controls or custom control styling can do this if you've used this {ThemeResource} markup extension resource technique in your custom templates and styles also.

## Related topics

* [Accessibility](accessibility.md)
* [UI contrast and settings sample](http://go.microsoft.com/fwlink/p/?linkid=231539)
* [XAML accessibility sample](http://go.microsoft.com/fwlink/p/?linkid=238570)
* [XAML high contrast sample](http://go.microsoft.com/fwlink/p/?linkid=254993)
* [**AccessibilitySettings**](https://msdn.microsoft.com/library/windows/apps/BR242237)
 

 





<!--HONumber=Jun16_HO1-->


