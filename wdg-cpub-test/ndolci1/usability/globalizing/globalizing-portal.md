---
Description: Globalization is the process of designing and developing your app to act appropriately for different global markets without any changes or customization.
Search.SourceType: Video
title: Globalization and localization
ms.assetid: c0791eec-5bb8-4a13-8977-61d7d98e35ce
label: Intro
template: detail.hbs
---

# Globalization and localization

\[ Updated for UWP apps on Windows 10. For Windows 8.x articles, see the [archive](http://go.microsoft.com/fwlink/p/?linkid=619132) \]

Windows is used worldwide, by audiences that vary in culture, region, and language. A user may speak any language, or even multiple languages. A user may be located anywhere in the world, and may speak any language in any location. You can increase the potential market for your app by designing it to be readily adaptable using *globalization* and *localization*.

**Globalization** is the process of designing and developing your app to act appropriately for different global markets without any changes or customization.

For example, you can:

-   Design the layout of your app to accommodate the different text lengths and font sizes of other languages in labels and text strings.
-   Retrieve text and culture-dependent images from resources that can be adapted to different local markets, instead of hard-coding them into your app's code or markup.
-   Use globalization APIs to display data that are formatted differently in different regions, such as numeric values, dates, times, and currencies.

**Localization** is the process of adapting your app to meet the language, cultural, and political requirements of a specific local market.

For example:

-   Translate the text and labels of the app for the new market, and create separate resources for its language.
-   Modify any culture-dependent images as necessary, and place in separate resources.

Watch this video for a brief introduction on how to prepare your app for the world: [Introduction to globalization and localization](https://channel9.msdn.com/Blogs/One-Dev-Minute/Introduction-to-globalization-and-localization).

## Articles

| Article                                                                              | Description                                                                                                                                                                                      |
|--------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [Do's and don'ts](guidelines-and-checklist-for-globalizing-your-app.md)             | Follow these best practices when globalizing your apps for a wider audience and when localizing your apps for a specific market.                                                                 |
| [Use global-ready formats](use-global-ready-formats.md)                                 | Develop a global-ready app by appropriately formatting dates, times, numbers, and currencies.                                                                                                    |
| [Manage language and region](manage-language-and-region.md)                             | Control how Windows selects UI resources and formats the UI elements of the app, by using the various language and region settings provided by Windows.                                          |
| [Use patterns to format dates and times](use-patterns-to-format-dates-and-times.md)     | Use the [Windows.Globalization.DateTimeFormatting](https://msdn.microsoft.com/library/windows/apps/br206859) API with custom patterns to display dates and times in exactly the format you wish. |
| [Adjust layout and fonts, and support RTL](adjust-layout-and-fonts-and-support-rtl.md) | Develop your app to support the layouts and fonts of multiple languages, including RTL (right-to-left) flow direction.                                                                           |
| [Prepare your app for localization](prepare-your-app-for-localization.md)               | Prepare your app for localization to other markets, languages, or regions.                                                                                                                       |
| [Put UI strings into resources](put-ui-strings-into-resources.md)                       | Put string resources for your UI into resource files. You can then reference those strings from your code or markup.                                                                             |

 
See also the documentation originally created for Windows 8.x, which still applies to Universal Windows Platform (UWP) apps and Windows 10.

-   [Globalizing your app](https://msdn.microsoft.com/library/windows/apps/xaml/hh965328)
-   [Language matching](https://msdn.microsoft.com/library/windows/apps/xaml/jj673578.aspx)
-   [NumeralSystem values](https://msdn.microsoft.com/library/windows/apps/xaml/jj236471.aspx)
-   [International fonts](https://msdn.microsoft.com/library/windows/apps/xaml/dn263115.aspx)
-   [App resources and localization](https://msdn.microsoft.com/library/windows/apps/xaml/hh710212.aspx)

 

 





<!--HONumber=May16_HO4-->


