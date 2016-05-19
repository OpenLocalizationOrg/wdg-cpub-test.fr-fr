---
Description: Follow these best practices when globalizing your apps for a wider audience and when localizing your apps for a specific market.
Search.Refinement.TopicID: 180
title: Guidelines for globalization and localization
ms.assetid: 0342DC3F-DDD1-4DD4-872E-A4EC340CAE79
label: Do's and don'ts
template: detail.hbs
---

# Globalization and localization do's and don'ts

\[ Updated for UWP apps on Windows 10. For Windows 8.x articles, see the [archive](http://go.microsoft.com/fwlink/p/?linkid=619132) \]


**Important APIs**

-   [**Globalization**](https://msdn.microsoft.com/library/windows/apps/br206813)
-   [**Globalization.NumberFormatting**](https://msdn.microsoft.com/library/windows/apps/br226136)
-   [**Globalization.DateTimeFormatting**](https://msdn.microsoft.com/library/windows/apps/br206859)
-   [**Resources**](https://msdn.microsoft.com/library/windows/apps/br206022)
-   [**Resources.Core**](https://msdn.microsoft.com/library/windows/apps/br225039)

Follow these best practices when globalizing your apps for a wider audience and when localizing your apps for a specific market.

## Globalization

Prepare your app to easily adapt to different markets by choosing globally appropriate terms and images for your UI, using [**Globalization**](https://msdn.microsoft.com/library/windows/apps/br206813) APIs to format app data, and avoiding assumptions based on location or language.

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Recommendation</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Use the correct formats for numbers, dates, times, addresses, and phone numbers.</td>
<td align="left">The formatting used for numbers, dates, times, and other forms of data varies between cultures, regions, languages, and markets. If you're displaying numbers, dates, times, or other data, use [**Globalization**](https://msdn.microsoft.com/library/windows/apps/br206813) APIs to get the format appropriate for a particular audience.</td>
</tr>
<tr class="even">
<td align="left">Support international paper sizes.</td>
<td align="left">The most common paper sizes differ between countries, so if you include features that depend on paper size, like printing, be sure to support and test common international sizes.</td>
</tr>
<tr class="odd">
<td align="left">Support international units of measurement and currencies.</td>
<td align="left">Different units and scales are used in different countries, although the most popular are the metric system and the imperial system. If you deal with measurements, like length, temperature, or area, get the correct system measurement by using the [**CurrenciesInUse**](https://msdn.microsoft.com/library/windows/apps/br206793) property.</td>
</tr>
<tr class="even">
<td align="left">Display text and fonts correctly.</td>
<td align="left">The ideal font, font size, and direction of text varies between different markets.
For more info, see [**Adjust layout and fonts, and support RTL**](adjust-layout-and-fonts-and-support-rtl.md).</td>
</tr>
<tr class="odd">
<td align="left">Use Unicode for character encoding.</td>
<td align="left">By default, recent versions of Microsoft Visual Studio use Unicode character encoding for all documents. If you're using a different editor, be sure to save source files in the appropriate Unicode character encodings. All Windows Runtime APIs return UTF-16 encoded strings.</td>
</tr>
<tr class="even">
<td align="left">Record the language of input.</td>
<td align="left">When your app asks users for text input, record the language of input. This ensures that when the input is displayed later it's presented to the user with the appropriate formatting. Use the [**CurrentInputMethodLanguage**](https://msdn.microsoft.com/library/windows/apps/hh700658) property to get the current input language.</td>
</tr>
<tr class="odd">
<td align="left">Don't use language to assume a user's location, and don't use location to assume a user's language.</td>
<td align="left">In Windows, the user's language and location are separate concepts. A user can speak a particular regional variant of a language, like en-gb for English as spoken in Great Britain, but the user can be in an entirely different country or region. Consider whether your apps require knowledge about the user's language, like for UI text, or location, like for licensing issues.
For more info, see [**Manage language and region**](manage-language-and-region.md).</td>
</tr>
<tr class="even">
<td align="left">Don't use colloquialisms and metaphors.</td>
<td align="left">Language that's specific to a demographic group, such as culture and age, can be hard to understand or translate, because only people in that demographic group use that language. Similarly, metaphors might make sense to one person but mean nothing to someone else. For example, a "bluebird" means something specific to those who are part of skiing culture, but those who aren’t part of that culture don’t understand the reference. If you plan to localize your app and you use an informal voice or tone, be sure that you adequately explain to localizers the meaning and voice to be translated.</td>
</tr>
<tr class="odd">
<td align="left">Don't use technical jargon, abbreviations, or acronyms.</td>
<td align="left">Technical language is less likely to be understood by non-technical audiences or people from other cultures or regions, and it's difficult to translate. People don't use these kinds of words in everyday conversations. Technical language often appears in error messages to identify hardware and software issues. At times, this might be be necessary, but you should rewrite strings to be non-technical.</td>
</tr>
<tr class="even">
<td align="left">Don't use images that might be offensive.</td>
<td align="left">Images that might be appropriate in your own culture may be offensive or misinterpreted in other cultures. Avoid use of religious symbols, animals, or color combinations that are associated with national flags or political movements.</td>
</tr>
<tr class="odd">
<td align="left">Avoid political offense in maps or when referring to regions.</td>
<td align="left">Maps may include controversial regional or national boundaries, and they're a frequent source of political offense. Be careful that any UI used for selecting a nation refers to it as a "country/region". Putting a disputed territory in a list labeled "Countries", like in an address form, could get you in trouble.</td>
</tr>
<tr class="even">
<td align="left">Don't use string comparison by itself to compare language tags.</td>
<td align="left">BCP-47 language tags are complex. There are a number of issues when comparing language tags, including issues with matching script information, legacy tags, and multiple regional variants. The resource management system in Windows takes care of matching for you. You can specify a set of resources in any languages, and the system chooses the appropriate one for the user and the app.
For more on resource management, see [**Defining app resources**](https://msdn.microsoft.com/library/windows/apps/xaml/hh965321).</td>
</tr>
<tr class="odd">
<td align="left">Don't assume that sorting is always alphabetic.</td>
<td align="left">For languages that don't use Latin script, sorting is based on things like pronunciation, number of pen strokes, and other factors. Even languages that use Latin script don't always use alphabetic sorting. For example, in some cultures, a phone book might not be sorted alphabetically. The system can handle sorting for you, but if you create your own sorting algorithm, be sure to take into account the sorting methods used in your target markets.</td>
</tr>
</tbody>
</table>

 

## Localization

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Recommendation</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Separate resources such as UI strings and images from code.</td>
<td align="left">Design your apps so that resources, like strings and images, are separated from your code. This enables them to be independently maintained, localized, and customized for different scaling factors, accessibility options, and a number of other user and machine contexts.
Separate string resources from your app's code to create a single language-independent codebase. Always separate strings from app code and markup, and place them into a resource file, like a ResW or ResJSON file.
Use the resource infrastructure in Windows to handle the selection of the most appropriate resources to match the user's runtime environment.</td>
</tr>
<tr class="even">
<td align="left">Isolate other localizable resource files.</td>
<td align="left">Take other files that require localization, like images that contain text to be translated or that need to be changed due to cultural sensitivity, and place them in folders tagged with language names.</td>
</tr>
<tr class="odd">
<td align="left">Set your default language, and mark all of your resources, even the ones in your default language.</td>
<td align="left">Always set the default language for your apps appropriately in the app manifest (package.appxmanifest). The default language determines the language that's used when the user doesn't speak any of the supported languages of the app. Mark default language resources, for example en-us/Logo.png, with their language, so the system can tell which language the resource is in and how it's used in particular situations.</td>
</tr>
<tr class="even">
<td align="left">Determine the resources of your app that require localization.</td>
<td align="left">What needs to change if your app is to be localized for other markets? Text strings require translation into other languages. Images may need to be adapted for other cultures. Consider how localization affects other resources that your app uses, like audio or video.</td>
</tr>
<tr class="odd">
<td align="left">Use resource identifiers in the code and markup to refer to resources.</td>
<td align="left">Instead of having string literals or specific file names for images in your markup, use references to the resources. Be sure to use unique identifiers for each resource. For more info, see [**How to name resources using qualifiers**](https://msdn.microsoft.com/en-us/library/windows/apps/xaml/Hh965324).
Listen for events that fire when the system changes and it begins to use a different set of qualifiers. Reprocess the document so that the correct resources can be loaded.</td>
</tr>
<tr class="even">
<td align="left">Enable text size to increase.</td>
<td align="left">Allocate text buffers dynamically, since text size may expand when translated. If you must use static buffers, make them extra-large (perhaps doubling the length of the English string) to accommodate potential expansion when strings are translated. There also may be limited space available for a user interface. To accommodate localized languages, ensure that your string length is approximately 40% longer than what you would need for the English language. For really short strings, such as single words, you may needs as much as 300% more space. In addition, enabling multiline support and text-wrapping in a control will leave more space to display each string.</td>
</tr>
<tr class="odd">
<td align="left">Support mirroring.</td>
<td align="left">Text alignment and reading order can be left-to-right, as in English, or right-to-left (RTL), as in Arabic or Hebrew. If you are localizing your product into languages that use a different reading order than your own, be sure that the layout of your UI elements supports mirroring. Even items such as back buttons, UI transition effects, and images may need to be mirrored.
For more info, see [**Adjust layout and fonts, and support RTL**](adjust-layout-and-fonts-and-support-rtl.md).</td>
</tr>
<tr class="even">
<td align="left">Comment strings.</td>
<td align="left">Ensure that strings are properly commented, and only the strings that need to be translated are provided to localizers. Over-localization is a common source of problems.</td>
</tr>
<tr class="odd">
<td align="left">Use short strings.</td>
<td align="left">Shorter strings are easier to translate and enable translation recycling. Translation recycling saves money because the same string isn't sent to the localizer twice.
Strings longer than 8192 characters may not be supported by some localization tools, so keep string length to 4000 or less.</td>
</tr>
<tr class="even">
<td align="left">Provide strings that contain an entire sentence.</td>
<td align="left">Provide strings that contain an entire sentence, instead of breaking the sentence into individual words, because the translation of words may depend on their position in a sentence. Also, don't assume that a phrase with multiple parameters will keep those parameters in the same order for every language.</td>
</tr>
<tr class="odd">
<td align="left">Optimize image and audio files for localization.</td>
<td align="left">Reduce localization costs by avoiding use of text in images or speech in audio files. If you're localizing to a language with a different reading direction than your own, using symmetrical images and effects make it easier to support mirroring.</td>
</tr>
<tr class="even">
<td align="left">Don't re-use strings in different contexts.</td>
<td align="left">Don't re-use strings in different contexts, because even simple words like "on" and "off" may be translated differently, depending on the context.</td>
</tr>
</tbody>
</table>

 

## Related articles

**Samples**
* [Application resources and localization sample](http://go.microsoft.com/fwlink/p/?linkid=254478)
* [Globalization preferences sample](http://go.microsoft.com/fwlink/p/?linkid=231608)
 

 





<!--HONumber=Mar16_HO2-->


