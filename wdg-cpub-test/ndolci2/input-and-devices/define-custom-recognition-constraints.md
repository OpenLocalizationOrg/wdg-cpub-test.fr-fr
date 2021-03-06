---
Description: Learn how to define and use custom constraints for speech recognition.
title: Define custom recognition constraints
ms.assetid: 26289DE5-6AC9-42C3-A160-E522AE62D2FC
label: Define custom recognition constraints
template: detail.hbs
---

# Define custom recognition constraints


\[ Updated for UWP apps on Windows 10. For Windows 8.x articles, see the [archive](http://go.microsoft.com/fwlink/p/?linkid=619132) \]

Learn how to define and use custom constraints for speech recognition.

**Important APIs**

-   [**SpeechRecognitionTopicConstraint**](https://msdn.microsoft.com/library/windows/apps/dn631446)
-   [**SpeechRecognitionListConstraint**](https://msdn.microsoft.com/library/windows/apps/dn631421)
-   [**SpeechRecognitionGrammarFileConstraint**](https://msdn.microsoft.com/library/windows/apps/dn631412)


Speech recognition requires at least one constraint to define a recognizable vocabulary. If no constraint is specified, the predefined dictation grammar of Universal Windows apps is used. See [Speech recognition](speech-recognition.md).


## <span id="Add_constraints"></span><span id="add_constraints"></span><span id="ADD_CONSTRAINTS"></span>Add constraints


Use the [**SpeechRecognizer.Constraints**](https://msdn.microsoft.com/library/windows/apps/dn653241) property to add constraints to a speech recognizer.

Here, we cover the three kinds of speech recognition constraints used from within an app. (For voice command constraints, see [Launch a foreground app with voice commands in Cortana](launch-a-foreground-app-with-voice-commands-in-cortana.md).)

-   [**SpeechRecognitionTopicConstraint**](https://msdn.microsoft.com/library/windows/apps/dn631446)—A constraint based on a predefined grammar (dictation or web search).
-   [**SpeechRecognitionListConstraint**](https://msdn.microsoft.com/library/windows/apps/dn631421)—A constraint based on a list of words or phrases.
-   [**SpeechRecognitionGrammarFileConstraint**](https://msdn.microsoft.com/library/windows/apps/dn631412)—A constraint defined in a Speech Recognition Grammar Specification (SRGS) file.

Each speech recognizer can have one constraint collection. Only these combinations of constraints are valid:

-   A single-topic constraint, or predefined grammar (dictation or web search). No other constraints are allowed.
-   A combination of list constraints and/or grammar-file constraints.

**Remember:  **Call the [**SpeechRecognizer.CompileConstraintsAsync**](https://msdn.microsoft.com/library/windows/apps/dn653240) method to compile the constraints before starting the recognition process.

## <span id="Specify_a_web-search_grammar__SpeechRecognitionTopicConstraint_"></span><span id="specify_a_web-search_grammar__speechrecognitiontopicconstraint_"></span><span id="SPECIFY_A_WEB-SEARCH_GRAMMAR__SPEECHRECOGNITIONTOPICCONSTRAINT_"></span>Specify a web-search grammar (SpeechRecognitionTopicConstraint)


Topic constraints (dictation or web-search grammar) must be added to the constraints collection of a speech recognizer.

Here, we add a web-search grammar to the constraints collection.

```CSharp
private async void WeatherSearch_Click(object sender, RoutedEventArgs e)
{
    // Create an instance of SpeechRecognizer.
    var speechRecognizer = new Windows.Media.SpeechRecognition.SpeechRecognizer();

    // Listen for audio input issues.
    speechRecognizer.RecognitionQualityDegrading += speechRecognizer_RecognitionQualityDegrading;

    // Add a web search grammar to the recognizer.
    var webSearchGrammar = new Windows.Media.SpeechRecognition.SpeechRecognitionTopicConstraint(Windows.Media.SpeechRecognition.SpeechRecognitionScenario.WebSearch, "webSearch");


    speechRecognizer.UIOptions.AudiblePrompt = "Say what you want to search for...";
    speechRecognizer.UIOptions.ExampleText = @"Ex. &#39;weather for London&#39;";
    speechRecognizer.Constraints.Add(webSearchGrammar);

    // Compile the constraint.
    await speechRecognizer.CompileConstraintsAsync();

    // Start recognition.
    Windows.Media.SpeechRecognition.SpeechRecognitionResult speechRecognitionResult = await speechRecognizer.RecognizeWithUIAsync();
    //await speechRecognizer.RecognizeWithUIAsync();

    // Do something with the recognition result.
    var messageDialog = new Windows.UI.Popups.MessageDialog(speechRecognitionResult.Text, "Text spoken");
    await messageDialog.ShowAsync();
}
```

## <span id="Specify_a_programmatic_list_constraint__SpeechRecognitionListConstraint_"></span><span id="specify_a_programmatic_list_constraint__speechrecognitionlistconstraint_"></span><span id="SPECIFY_A_PROGRAMMATIC_LIST_CONSTRAINT__SPEECHRECOGNITIONLISTCONSTRAINT_"></span>Specify a programmatic list constraint (SpeechRecognitionListConstraint)


List constraints must be added to the constraints collection of a speech recognizer.

Keep the following points in mind:

-   You can add multiple list constraints to a constraints collection.
-   You can use any collection that implements **IIterable&lt;String&gt;** for the string values.

Here, we programmatically specify an array of words as a list constraint and add it to the constraints collection of a speech recognizer.

```CSharp
private async void YesOrNo_Click(object sender, RoutedEventArgs e)
{
    // Create an instance of SpeechRecognizer.
    var speechRecognizer = new Windows.Media.SpeechRecognition.SpeechRecognizer();

    // You could create this array dynamically.
    string[] responses = { "Yes", "No" };


    // Add a list constraint to the recognizer.
    var listConstraint = new Windows.Media.SpeechRecognition.SpeechRecognitionListConstraint(responses, "yesOrNo");

    speechRecognizer.UIOptions.ExampleText = @"Ex. &#39;yes&#39;, &#39;no&#39;";
    speechRecognizer.Constraints.Add(listConstraint);

    // Compile the constraint.
    await speechRecognizer.CompileConstraintsAsync();

    // Start recognition.
    Windows.Media.SpeechRecognition.SpeechRecognitionResult speechRecognitionResult = await speechRecognizer.RecognizeWithUIAsync();

    // Do something with the recognition result.
    var messageDialog = new Windows.UI.Popups.MessageDialog(speechRecognitionResult.Text, "Text spoken");
    await messageDialog.ShowAsync();
}
```

## <span id="Specify_an_SRGS_grammar_constraint__SpeechRecognitionGrammarFileConstraint_"></span><span id="specify_an_srgs_grammar_constraint__speechrecognitiongrammarfileconstraint_"></span><span id="SPECIFY_AN_SRGS_GRAMMAR_CONSTRAINT__SPEECHRECOGNITIONGRAMMARFILECONSTRAINT_"></span>Specify an SRGS grammar constraint (SpeechRecognitionGrammarFileConstraint)


SRGS grammar files must be added to the constraints collection of a speech recognizer.

The SRGS Version 1.0 is the industry-standard markup language for creating XML-format grammars for speech recognition. Although Universal Windows apps provide alternatives to using SRGS for creating speech-recognition grammars, you might find that using SRGS to create grammars produces the best results, particularly for more involved speech recognition scenarios.

SRGS grammars provide a full set of features to help you architect complex voice interaction for your apps. For example, with SRGS grammars you can:

-   Specify the order in which words and phrases must be spoken to be recognized.
-   Combine words from multiple lists and phrases to be recognized.
-   Link to other grammars.
-   Assign a weight to an alternative word or phrase to increase or decrease the likelihood that it will be used to match speech input.
-   Include optional words or phrases.
-   Use special rules that help filter out unspecified or unanticipated input, such as random speech that doesn't match the grammar, or background noise.
-   Use semantics to define what speech recognition means to your app.
-   Specify pronunciations, either inline in a grammar or via a link to a lexicon.

For more info about SRGS elements and attributes, see the [SRGS Grammar XML Reference](http://go.microsoft.com/fwlink/p/?LinkID=269886) . To get started creating an SRGS grammar, see [How to Create a Basic XML Grammar](http://go.microsoft.com/fwlink/p/?LinkID=269887).

Keep the following points in mind:

-   You can add multiple grammar-file constraints to a constraints collection.
-   Use the .grxml file extension for XML-based grammar documents that conform to SRGS rules.

This example uses an SRGS grammar defined in a file named srgs.grxml (described later). In the file properties, the **Package Action** is set to **Content** with **Copy to Output Directory** set to **Copy always**:

```CSharp
private async void Colors_Click(object sender, RoutedEventArgs e)
{
    // Create an instance of SpeechRecognizer.
    var speechRecognizer = new Windows.Media.SpeechRecognition.SpeechRecognizer();

    // Add a grammar file constraint to the recognizer.
    var storageFile = await Windows.Storage.StorageFile.GetFileFromApplicationUriAsync(new Uri("ms-appx:///Colors.grxml"));
    var grammarFileConstraint = new Windows.Media.SpeechRecognition.SpeechRecognitionGrammarFileConstraint(storageFile, "colors");

    speechRecognizer.UIOptions.ExampleText = @"Ex. &#39;blue background&#39;, &#39;green text&#39;";
    speechRecognizer.Constraints.Add(grammarFileConstraint);

    // Compile the constraint.
    await speechRecognizer.CompileConstraintsAsync();

    // Start recognition.
    Windows.Media.SpeechRecognition.SpeechRecognitionResult speechRecognitionResult = await speechRecognizer.RecognizeWithUIAsync();

    // Do something with the recognition result.
    var messageDialog = new Windows.UI.Popups.MessageDialog(speechRecognitionResult.Text, "Text spoken");
    await messageDialog.ShowAsync();
}
```

This SRGS file (srgs.grxml) includes semantic interpretation tags. These tags provide a mechanism for returning grammar match data to your app. Grammars must conform to the World Wide Web Consortium (W3C) [Semantic Interpretation for Speech Recognition (SISR) 1.0](http://go.microsoft.com/fwlink/p/?LinkID=201765) specification.

Here, we listen for variants of "yes" and "no".

```CSharp
<grammar xml:lang="en-US" 
         root="yesOrNo"
         version="1.0" 
         tag-format="semantics/1.0"
         xmlns="http://www.w3.org/2001/06/grammar">

    <!-- The following rules recognize variants of yes and no. -->
      <rule id="yesOrNo">
         <one-of>
            <item>
              <one-of>
                 <item>yes</item>
                 <item>yeah</item>
                 <item>yep</item>
                 <item>yup</item>
                 <item>un huh</item>
                 <item>yay yus</item>
              </one-of>
              <tag>out="yes";</tag>
            </item>
            <item>
              <one-of>
                 <item>no</item>
                 <item>nope</item>
                 <item>nah</item>
                 <item>uh uh</item>
               </one-of>
               <tag>out="no";</tag>
            </item>
         </one-of>
      </rule>
</grammar>
```

## <span id="Manage_constraints"></span><span id="manage_constraints"></span><span id="MANAGE_CONSTRAINTS"></span>Manage constraints


After a constraint collection is loaded for recognition, your app can manage which constraints are enabled for recognition operations by setting the [**IsEnabled**](https://msdn.microsoft.com/library/windows/apps/dn631402) property of a constraint to **true** or **false**. The default setting is **true**.

It's usually more efficient to load constraints once, enabling and disabling them as needed, rather than to load, unload, and compile constraints for each recognition operation. Use the [**IsEnabled**](https://msdn.microsoft.com/library/windows/apps/dn631402) property, as required.

Restricting the number of constraints serves to limit the amount of data that the speech recognizer needs to search and match against the speech input. This can improve both the performance and the accuracy of speech recognition.

Decide which constraints are enabled based on the phrases that your app can expect in the context of the current recognition operation. For example, if the current app context is to display a color, you probably don't need to enable a constraint that recognizes the names of animals.

To prompt the user for what can be spoken, use the [**SpeechRecognizerUIOptions.AudiblePrompt**](https://msdn.microsoft.com/library/windows/apps/dn653235) and [**SpeechRecognizerUIOptions.ExampleText**](https://msdn.microsoft.com/library/windows/apps/dn653236) properties, which are set by means of the [**SpeechRecognizer.UIOptions**](https://msdn.microsoft.com/library/windows/apps/dn653254) property. Preparing users for what they can say during the recognition operation increases the likelihood that they will speak a phrase that can be matched to an active constraint.

## <span id="related_topics"></span>Related articles


* [Speech interactions](speech-interactions.md)

**Samples**
* [Speech recognition and speech synthesis sample](http://go.microsoft.com/fwlink/p/?LinkID=619897)
 

 






<!--HONumber=May16_HO4-->


