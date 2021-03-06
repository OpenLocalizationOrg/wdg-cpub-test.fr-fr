---
Description: Learn how to select an installed language to use for speech recognition.
title: Specify the speech recognizer language
ms.assetid: 4C463A1B-AF6A-46FD-A839-5D6724955B38
label: Specify the speech recognizer language
template: detail.hbs
---

# Specify the speech recognizer language


Learn how to select an installed language to use for speech recognition.

\[ Updated for UWP apps on Windows 10. For Windows 8.x articles, see the [archive](http://go.microsoft.com/fwlink/p/?linkid=619132) \]


**Important APIs**

-   [**SupportedTopicLanguages**](https://msdn.microsoft.com/library/windows/apps/dn653251)
-   [**SupportedGrammarLanguages**](https://msdn.microsoft.com/library/windows/apps/dn653250)
-   [**Language**](https://msdn.microsoft.com/library/windows/apps/br206804)


Here, we enumerate the languages installed on a system, identify which is the default language, and select a different language for recognition.

**Prerequisites:  **

This topic builds on [Speech recognition](speech-recognition.md).

You should have a basic understanding of speech recognition and recognition constraints.

If you're new to developing Universal Windows Platform (UWP) apps, have a look through these topics to get familiar with the technologies discussed here.

-   [Create your first app](https://msdn.microsoft.com/library/windows/apps/bg124288)
-   Learn about events with [Events and routed events overview](https://msdn.microsoft.com/library/windows/apps/mt185584)

**User experience guidelines:  **

For helpful tips about designing a useful and engaging speech-enabled app, see [Speech design guidelines](https://msdn.microsoft.com/library/windows/apps/dn596121) .

## <span id="Identify_the_default_language"></span><span id="identify_the_default_language"></span><span id="IDENTIFY_THE_DEFAULT_LANGUAGE"></span>Identify the default language


A speech recognizer uses the system speech language as its default recognition language. This language is set by the user on the device Settings &gt; System &gt; Speech &gt; Speech Language screen.

We identify the default language by checking the [**SystemSpeechLanguage**](https://msdn.microsoft.com/library/windows/apps/dn653252) static property.

```CSharp
var language = SpeechRecognizer.SystemSpeechLanguage; </code></pre></td>
</tr>
</tbody>
</table>
```

## <span id="Confirm_an_installed_language"></span><span id="confirm_an_installed_language"></span><span id="CONFIRM_AN_INSTALLED_LANGUAGE"></span>Confirm an installed language


Installed languages can vary between devices. You should verify the existence of a language if you depend on it for a particular constraint.

**Note**  A reboot is required after a new language pack is installed. An exception with error code SPERR\_NOT\_FOUND (0x8004503a) is raised if the specified language is not supported or has not finished installing.

 

Determine the supported languages on a device by checking one of two static properties of the [**SpeechRecognizer**](https://msdn.microsoft.com/library/windows/apps/dn653226) class:

-   [**SupportedTopicLanguages**](https://msdn.microsoft.com/library/windows/apps/dn653251)—The collection of [**Language**](https://msdn.microsoft.com/library/windows/apps/br206804) objects used with predefined dictation and web search grammars.

-   [**SupportedGrammarLanguages**](https://msdn.microsoft.com/library/windows/apps/dn653250)—The collection of [**Language**](https://msdn.microsoft.com/library/windows/apps/br206804) objects used with a list constraint or a Speech Recognition Grammar Specification (SRGS) file.

## <span id="Specify_a_language"></span><span id="specify_a_language"></span><span id="SPECIFY_A_LANGUAGE"></span>Specify a language


To specify a language, pass a [**Language**](https://msdn.microsoft.com/library/windows/apps/br206804) object in the [**SpeechRecognizer**](https://msdn.microsoft.com/library/windows/apps/dn653226) constructor.

Here, we specify "en-US" as the recognition language.

<span codelanguage="CSharp"></span>
```CSharp
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">C#</th>
</tr>
</thead>
<tbody>
<tr class="odd">
var language = new Windows.Globalization.Language(“en-US”); 
var recognizer = new SpeechRecognizer(language); 
```

## <span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>Remarks


A topic constraint can be configured by adding a [**SpeechRecognitionTopicConstraint**](https://msdn.microsoft.com/library/windows/apps/dn631446) to the [**Constraints**](https://msdn.microsoft.com/library/windows/apps/dn653241) collection of the [**SpeechRecognizer**](https://msdn.microsoft.com/library/windows/apps/dn653226) and then calling [**CompileConstraintsAsync**](https://msdn.microsoft.com/library/windows/apps/dn653240). A [**SpeechRecognitionResultStatus**](https://msdn.microsoft.com/library/windows/apps/dn631433) of **TopicLanguageNotSupported** is returned if the recognizer is not initialized with a supported topic language.

A list constraint is configured by adding a [**SpeechRecognitionListConstraint**](https://msdn.microsoft.com/library/windows/apps/dn631421) to the [**Constraints**](https://msdn.microsoft.com/library/windows/apps/dn653241) collection of the [**SpeechRecognizer**](https://msdn.microsoft.com/library/windows/apps/dn653226) and then calling [**CompileConstraintsAsync**](https://msdn.microsoft.com/library/windows/apps/dn653240). You cannot specify the language of a custom list directly. Instead, the list will be processed using the language of the recognizer.

An SRGS grammar is an open-standard XML format represented by the [**SpeechRecognitionGrammarFileConstraint**](https://msdn.microsoft.com/library/windows/apps/dn631412) class. Unlike custom lists, you can specify the language of the grammar in the SRGS markup. [**CompileConstraintsAsync**](https://msdn.microsoft.com/library/windows/apps/dn653240) fails with a [**SpeechRecognitionResultStatus**](https://msdn.microsoft.com/library/windows/apps/dn631433) of **TopicLanguageNotSupported** if the recognizer is not initialized to the same language as the SRGS markup.

## <span id="related_topics"></span>Related articles


**Developers**
* [Speech interactions](speech-interactions.md)
**Designers**
* [Speech design guidelines](https://msdn.microsoft.com/library/windows/apps/dn596121)
**Samples**
* [Speech recognition and speech synthesis sample](http://go.microsoft.com/fwlink/p/?LinkID=619897)
 

 






<!--HONumber=May16_HO4-->


