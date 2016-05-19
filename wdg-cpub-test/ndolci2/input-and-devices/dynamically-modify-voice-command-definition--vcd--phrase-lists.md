---
Description: Learn how to access and update the list of supported phrases (PhraseList elements) in a Voice Command Definition (VCD) file using the speech recognition result at run time.
title: Dynamically modify VCD phrase lists
ms.assetid: 98024EAC-EC0E-44AA-AEC5-A611BA7C5884
label: Modify VCD phrase lists
template: detail.hbs
---

# Dynamically modify VCD phrase lists


\[ Updated for UWP apps on Windows 10. For Windows 8.x articles, see the [archive](http://go.microsoft.com/fwlink/p/?linkid=619132) \]


**Important APIs**

-   [**Windows.ApplicationModel.VoiceCommands**](https://msdn.microsoft.com/library/windows/apps/dn706594)
-   [**VCD elements and attributes v1.2**](https://msdn.microsoft.com/library/windows/apps/dn706593)

Learn how to access and update the list of supported phrases (**PhraseList** elements) in a Voice Command Definition (VCD) file using the speech recognition result at run time.

Dynamically modifying a phrase list at run time can be useful if the voice command is specific to a task involving some kind of user-defined favorites or transient app data.

For example, let's say you have a travel app where users can enter destinations, and you want users to be able to start the app by saying the app name followed by "Show trip to &lt;destination&gt;". You don't need to create a separate **ListenFor** element for each possible destination. Instead, you can dynamically populate **PhraseList** at run time with the destinations created by the user. In the **ListenFor** element itself, you could specify something like: `<ListenFor> Show trip to {destination}  </ListenFor>`, where "destination" is the value of the **Label** attribute for the **PhraseList**.

For more info about **PhraseList** and other VCD elements, see the [**VCD elements and attributes v1.2**](https://msdn.microsoft.com/library/windows/apps/dn706593) reference.

**Prerequisites:  **

This topic builds on [Launch a foreground app with voice commands in Cortana](launch-a-foreground-app-with-voice-commands-in-cortana.md). We continue here to demonstrate features with a trip planning and management app named **Adventure Works**.

If you're new to developing Universal Windows Platform (UWP) apps, have a look through these topics to get familiar with the technologies discussed here.

-   [Create your first app](https://msdn.microsoft.com/library/windows/apps/bg124288)
-   Learn about events with [Events and routed events overview](https://msdn.microsoft.com/library/windows/apps/mt185584)

**User experience guidelines:  **

See [Cortana design guidelines](https://msdn.microsoft.com/library/windows/apps/dn974233) for info about how to integrate your app with **Cortana** and [Speech design guidelines](https://msdn.microsoft.com/library/windows/apps/dn596121) for helpful tips on designing a useful and engaging speech-enabled app.

## <span id="Identify_the_command"></span><span id="identify_the_command"></span><span id="IDENTIFY_THE_COMMAND"></span>Identify the command


To update a **PhraseList** element in the VCD file, get the **CommandSet** element that contains the phrase list. Use the **Name** attribute of that **CommandSet** element (**Name** must be unique in the VCD file) as a key to access the [**VoiceCommandManager.InstalledCommandSets**](https://msdn.microsoft.com/library/windows/apps/dn653257) property and get the [**VoiceCommandSet**](https://msdn.microsoft.com/library/windows/apps/dn653258) reference.

## <span id="Replace_the_phrase_list"></span><span id="replace_the_phrase_list"></span><span id="REPLACE_THE_PHRASE_LIST"></span>Replace the phrase list


After you've identified the command set, get a reference to the phrase list that you want to modify and call the [**SetPhraseListAsync**](https://msdn.microsoft.com/library/windows/apps/dn653261) method; use the **Label** attribute of the **PhraseList** element and an array of strings as the new content of the phrase list.

**Note**  If you modify a phrase list, the entire phrase list is replaced. If you want to insert new items into a phrase list, you must specify both the existing items and the new items in the call to [**SetPhraseListAsync**](https://msdn.microsoft.com/library/windows/apps/dn653261).

 

Here, the VCD file defines a **Command**"showTripToDestination" with a **PhraseList** that defines three options for selecting a destination in our **Adventure Works** travel app. As the user saves and deletes destinations in the app, the app updates the options in the **PhraseList**.

```XML
<?xml version="1.0" encoding="utf-8"?>
<VoiceCommands xmlns="http://schemas.microsoft.com/voicecommands/1.1">
  <CommandSet xml:lang="en-us" Name="AdventureWorksCommandSet_en-us">
    <CommandPrefix> Adventure Works, </CommandPrefix>
    <Example> Show trip to London </Example>

    <Command Name="showTripToDestination">
      <Example> show trip to London  </Example>
      <ListenFor> show trip to {destination} </ListenFor>
      <Feedback> Showing trip to {destination} </Feedback>
      <Navigate/>
    </Command>

    <PhraseList Label="destination">
      <Item> London </Item>
      <Item> Dallas </Item>
      <Item> New York </Item>
    </PhraseList>

  </CommandSet>

<!-- Other CommandSets for other languages -->

</VoiceCommands>
```

Here's how to update the **PhraseList** shown in the previous example with an additional destination to Phoenix.

```CSharp
Windows.ApplicationModel.VoiceCommands.VoiceCommnadDefinition.VoiceCommandSet commandSetEnUs;

if (Windows.ApplicationModel.VoiceCommands.VoiceCommandDefinitionManager.
      InstalledCommandSets.TryGetValue(
        "AdventureWorksCommandSet_en-us", out commandSetEnUs))
{
  await commandSetEnUs.SetPhraseListAsync(
    "destination", new string[] {“London”, “Dallas”, “New York”, “Phoenix”});
}
```

## <span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>Remarks


Using a **PhraseList** to constrain the recognition is appropriate for a relatively small set or words. When the set of words is too large (hundreds of words, for example), or shouldn’t be constrained at all, use the **PhraseTopic** element and a **Subject** element to refine the relevance of speech-recognition results to improve scalability.

In our example, we have a **PhraseTopic** with a **Scenario** of "Search", further refined by a **Subject** of "City\\State".

```XML
<?xml version="1.0" encoding="utf-8"?>
<VoiceCommands xmlns="http://schemas.microsoft.com/voicecommands/1.1">
  <CommandSet xml:lang="en-us" Name="AdventureWorksCommandSet_en-us">
    <CommandPrefix> Adventure Works, </CommandPrefix>
    <Example> Show trip to London </Example>

    <Command Name="showTripToDestination">
      <Example> show trip to London  </Example>
      <ListenFor> show trip to {destination} </ListenFor>
      <Feedback> Showing trip to {destination} </Feedback>
      <Navigate/>
    </Command>

    <PhraseList Label="destination">
      <Item> London </Item>
      <Item> Dallas </Item>
      <Item> New York </Item>
    </PhraseList>

    <PhraseTopic Label="destination" Scenario="Search">
      <Subject>City/State</Subject>
    </PhraseTopic>

  </CommandSet>
```

## <span id="related_topics"></span>Related articles


**Developers**
* [Cortana interactions](cortana-interactions.md)
* [Launch a foreground app with voice commands in Cortana](launch-a-foreground-app-with-voice-commands-in-cortana.md)
* [Launch a background app with voice commands in Cortana](launch-a-background-app-with-voice-commands-in-cortana.md)
* [**VCD elements and attributes v1.2**](https://msdn.microsoft.com/library/windows/apps/dn706593)
**Designers**
* [Cortana design guidelines](https://msdn.microsoft.com/library/windows/apps/dn974233)
* [Speech design guidelines](https://msdn.microsoft.com/library/windows/apps/dn596121)
**Samples**
* [Cortana voice command sample](http://go.microsoft.com/fwlink/p/?LinkID=619899)
 

 






<!--HONumber=Mar16_HO2-->


