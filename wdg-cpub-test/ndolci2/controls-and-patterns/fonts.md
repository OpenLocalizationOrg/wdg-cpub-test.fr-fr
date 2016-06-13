---
Description: Follow these guidelines when selecting fonts and specifying font sizes and colors.
title: Fonts
ms.assetid: 1B8B90AD-CDC4-4997-ACDE-871C1E94A929
label: Fonts
template: detail.hbs
---

# Guidelines for fonts


\[ Updated for UWP apps on Windows 10. For Windows 8.x articles, see the [archive](http://go.microsoft.com/fwlink/p/?linkid=619132) \]


**Important APIs**

-   [**FontFamily (XAML)**](https://msdn.microsoft.com/library/windows/apps/br209655)
-   [**font-family (HTML)**](https://msdn.microsoft.com/library/windows/apps/hh996845)
-   [**font-size (HTML)**](https://msdn.microsoft.com/library/windows/apps/hh996846)

The proper use of font sizes, weights, colors, tracking, and spacing can help give your Universal Windows Platform (UWP) app a clean, uncluttered look that makes it easier to use. Follow these guidelines when selecting fonts and specifying font sizes and colors.

If you're looking for a list of Segoe UI Symbol icons, see [**Guidelines for Segoe UI Symbol icons**](segoe-ui-symbol-font.md).

## <span id="The_Windows_10_type_ramp"></span><span id="the_windows_10_type_ramp"></span><span id="THE_WINDOWS_10_TYPE_RAMP"></span>The Windows 10 type ramp


The type ramp establishes a crucial design relationship from headlines to body text and ensures a clear and understandable hierarchy between the different levels. Users immediately understand where to find information and how to parse the page.

Here's the type ramp that we recommend for UWP apps:

| Text style | Typeface | Weight    | Size (epx) | Line spacing (epx) | Word spacing | Tracking (1/1000 em) | XAML style key          |
|------------|----------|-----------|------------|--------------------|--------------|----------------------|-------------------------|
| Header     | Segoe UI | Light     | 46         | 56                 | 100%         | 0                    | HeaderTextBlockStyle    |
| Subheader  | Segoe UI | Light     | 34         | 40                 | 100%         | 0                    | SubheaderTextBlockStyle |
| Title      | Segoe UI | Semilight | 24         | 28                 | 100%         | 0                    | TitleTextBlockStyle     |
| Subtitle   | Segoe UI | Regular   | 20         | 24                 | 100%         | 0                    | SubtitleTextBlockStyle  |
| Base       | Segoe UI | Semibold  | 15         | 20                 | 100%         | 0                    | BaseTextBlockStyle      |
| Body       | Segoe UI | Regular   | 15         | 20                 | 100%         | 0                    | BodyTextBlockStyle      |
| Caption    | Segoe UI | Regular   | 12         | 14                 | 100%         | 0                    | CaptionTextBlockStyle   |

 

## <span id="Recommended_fonts"></span><span id="recommended_fonts"></span><span id="RECOMMENDED_FONTS"></span>Recommended fonts


You don't have to use the Segoe UI font for everything. You might use other fonts for certain scenarios, such as reading, or when display text in non-English languages.

Here's the list of fonts that are guaranteed to be available in all Windows 10 editions that support UWP apps.

**Note**  If you use a font that's not in this list, your app may trigger an automatic download of the font data from a Microsoft service. This can have performance and other impacts that may be a concern, particularly for mobile devices. In particular, note that this might consume some of a user's mobile data plan or result in mobile data usage costs. UWP apps that will available on mobile devices should never use fonts for UI content other than fonts in this list.

 

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Font-family</th>
<th align="left">Styles</th>
<th align="left">Comment</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Arial</td>
<td align="left">Regular, Italic, Bold, Bold Italic, Black</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">Calibri</td>
<td align="left">Regular, Italic, Bold, Bold Italic, Light, Light Italic</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">Cambria</td>
<td align="left">Regular</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">Cambria Math</td>
<td align="left">Regular</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">Comic Sans MS</td>
<td align="left">Regular, Italic, Bold, Bold Italic</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">Courier New</td>
<td align="left">Regular, Italic, Bold, Bold Italic</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">Ebrima</td>
<td align="left">Regular, Bold</td>
<td align="left">User-interface font for African scripts (Ethiopic, N'Ko, Osmanya, Tifinagh, Vai)</td>
</tr>
<tr class="even">
<td align="left">Gadugi</td>
<td align="left">Regular</td>
<td align="left">User-interface font for North American scripts (Canadian Syllabics, Cherokee)</td>
</tr>
<tr class="odd">
<td align="left">Georgia</td>
<td align="left">Regular, Italic, Bold, Bold Italic</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">Javanese Text Regular Fallback font for Javanese script</td>
<td align="left">Regular</td>
<td align="left">Fallback font for Javanese script</td>
</tr>
<tr class="odd">
<td align="left">Leelawadee UI</td>
<td align="left">Regular, Semilight, Bold</td>
<td align="left">User-interface font for Southeast Asian scripts (Buginese, Lao, Khmer, Thai)</td>
</tr>
<tr class="even">
<td align="left">Lucida Console</td>
<td align="left">Regular</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">Malgun Gothic</td>
<td align="left">Regular</td>
<td align="left">User-interface font for Korean</td>
</tr>
<tr class="even">
<td align="left">Microsoft Himalaya</td>
<td align="left">Regular</td>
<td align="left">Fallback font for Tibetan script</td>
</tr>
<tr class="odd">
<td align="left">Microsoft JhengHei</td>
<td align="left">Regular</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">Microsoft JhengHei UI</td>
<td align="left">Regular</td>
<td align="left">User-interface font for Traditional Chinese</td>
</tr>
<tr class="odd">
<td align="left">Microsoft New Tai Lue</td>
<td align="left">Regular</td>
<td align="left">Fallback font for New Tai Lue script</td>
</tr>
<tr class="even">
<td align="left">Microsoft PhagsPa</td>
<td align="left">Regular</td>
<td align="left">Fallback font for Phags-pa script</td>
</tr>
<tr class="odd">
<td align="left">Microsoft Tai Le</td>
<td align="left">Regular</td>
<td align="left">Fallback font for Tai Le script</td>
</tr>
<tr class="even">
<td align="left">Microsoft YaHei</td>
<td align="left">Regular</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">Microsoft YaHei UI</td>
<td align="left">Regular</td>
<td align="left">User-interface font for Simplified Chinese</td>
</tr>
<tr class="even">
<td align="left">Microsoft Yi Baiti</td>
<td align="left">Regular</td>
<td align="left">Fallback font for Yi script</td>
</tr>
<tr class="odd">
<td align="left">Mongolian Baiti</td>
<td align="left">Regular</td>
<td align="left">Fallback font for Mongolian script</td>
</tr>
<tr class="even">
<td align="left">MV Boli</td>
<td align="left">Regular</td>
<td align="left">Fallback font for Thaana script</td>
</tr>
<tr class="odd">
<td align="left">Myanmar Text</td>
<td align="left">Regular</td>
<td align="left">Fallback font for Myanmar script</td>
</tr>
<tr class="even">
<td align="left">Nirmala UI</td>
<td align="left">Regular, Semilight, Bold</td>
<td align="left">User-interface font for South Asian scripts (Bangla, Devanagari, Gujarati, Gurmukhi, Kannada, Malayalam, Odia, Ol Chiki, Sinhala, Sora Sompeng, Tamil, Telugu)</td>
</tr>
<tr class="odd">
<td align="left">Segoe MDL2 Assets</td>
<td align="left">Regular</td>
<td align="left">User-interface font for app icons</td>
</tr>
<tr class="even">
<td align="left">Segoe Print</td>
<td align="left">Regular</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">Segoe UI</td>
<td align="left">Regular, Italic, Bold, Bold Italic, Light, Semilight, Semibold, Black</td>
<td align="left">User-interface font for European and Middle East scripts (Arabic, Armenian, Cyrillic, Georgian, Greek, Hebrew, Latin), and also Lisu script</td>
</tr>
<tr class="even">
<td align="left">Segoe UI Emoji</td>
<td align="left">Regular</td>
<td align="left">The version that ships on Windows Phone includes a white outline around each emoji to ensure that it will show up on any color background. It is metrically compatible with the version that ships on Windows.</td>
</tr>
<tr class="odd">
<td align="left">Segoe UI Historic</td>
<td align="left">Regular</td>
<td align="left">Fallback font for historic scripts</td>
</tr>
<tr class="even">
<td align="left">Segoe UI Symbol</td>
<td align="left">Regular</td>
<td align="left">Fallback font for symbols</td>
</tr>
<tr class="odd">
<td align="left">SimSun</td>
<td align="left">Regular</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">Times New Roman</td>
<td align="left">Regular, Italic, Bold, Bold Italic</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">Trebuchet MS</td>
<td align="left">Regular, Italic, Bold, Bold Italic</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">Verdana</td>
<td align="left">Regular, Italic, Bold, Bold Italic</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">Webdings</td>
<td align="left">Regular</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">Wingdings</td>
<td align="left">Regular</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">Yu Gothic</td>
<td align="left">Medium</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">Yu Gothic UI</td>
<td align="left">Regular</td>
<td align="left">User-interface font for Japanese</td>
</tr>
</tbody>
</table>

 

## <span id="related_topics"></span>Related topics


**For designers**
* [Label (or text block)](labels.md)
* [Segoe UI Symbol icons](segoe-ui-symbol-font.md)
**For developers (XAML)**
* [XAML theme resources](https://msdn.microsoft.com/library/windows/apps/mt187274)
* [Laying out an app page](https://msdn.microsoft.com/library/windows/apps/hh872191)
* [Segoe UI Symbol icons](segoe-ui-symbol-font.md)
* [**TextBlock.FontFamily property**](https://msdn.microsoft.com/library/windows/apps/br209655)

**Samples**
* [XAML text display sample](http://go.microsoft.com/fwlink/p/?linkid=238578)
* [CSS stying: branding your app sample](http://go.microsoft.com/fwlink/p/?linkid=231641)
* [Language font mapping sample](http://go.microsoft.com/fwlink/p/?linkid=231603)
 

 






<!--HONumber=Jun16_HO1-->


