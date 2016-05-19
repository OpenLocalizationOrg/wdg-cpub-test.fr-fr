---
Description: Provide deep links from the background app service in Cortana to launch the app to the foreground in a specific state or context.
title: Deep link from Cortana to a background app
ms.assetid: BE811A87-8821-476A-90E4-2E20D37E4043
label: Deep link to a background app
template: detail.hbs
---

# Deep link from Cortana to a background app


\[ Updated for UWP apps on Windows 10. For Windows 8.x articles, see the [archive](http://go.microsoft.com/fwlink/p/?linkid=619132) \]


**Important APIs**

-   [**Windows.ApplicationModel.VoiceCommands**](https://msdn.microsoft.com/library/windows/apps/dn706594)
-   [**Voice Command Definition (VCD) elements and attributes v1.2**](https://msdn.microsoft.com/library/windows/apps/dn706593)

Provide deep links from the background app service in **Cortana** to launch the app to the foreground in a specific state or context.

A deep link is displayed by default on the **Cortana** completion screen, but you can display deep links on various other screens. For more info, see [Interact with a background app in Cortana](interact-with-a-background-app-in-cortana.md).

**Prerequisites:  **

This topic builds on [Interact with a background app in Cortana](interact-with-a-background-app-in-cortana.md). We continue using a trip planning and management app named **Adventure Works** to demonstrate various **Cortana** features.

If you're new to developing Universal Windows Platform (UWP) apps, have a look through these topics to get familiar with the technologies discussed here.

-   [Create your first app](https://msdn.microsoft.com/library/windows/apps/bg124288)
-   Learn about events with [Events and routed events overview](https://msdn.microsoft.com/library/windows/apps/mt185584)

**User experience guidelines:  **

See [Cortana design guidelines](https://msdn.microsoft.com/library/windows/apps/dn974233) for info about how to integrate your app with **Cortana** and [Speech design guidelines](https://msdn.microsoft.com/library/windows/apps/dn596121) for helpful tips on designing a useful and engaging speech-enabled app.

## <span id="Overview"></span><span id="overview"></span><span id="OVERVIEW"></span>Overview


Users can access your app through **Cortana** by:

-   Launching it as a foreground app (see [Launch a foreground app with voice commands in Cortana](launch-a-foreground-app-with-voice-commands-in-cortana.md)).
-   Exposing specific functionality as a background app service (see [Launch a background app with voice commands in Cortana](launch-a-background-app-with-voice-commands-in-cortana.md)).
-   Deep linking to specific pages, content, and state or context.

We discuss the last item here.

Deep linking is useful when Cortana and your app service are a gateway to the full app (instead of requiring the user to launch your app through the Start menu), or for providing access to richer detail and functionality within your app that is not possible through Cortana. Deep linking is another way to increase usability and access to your app.

There are three ways to provide deep links:

-   A "Go to &lt;app&gt;" link on various **Cortana** screens.
-   A link embedded in a content tile on various **Cortana** screens.
-   The app service programmatically launches the foreground app.

Both **Cortana** and the background app service are terminated when the foreground app is launched.

## <span id="Go_to__app__deep_link"></span><span id="go_to__app__deep_link"></span><span id="GO_TO__APP__DEEP_LINK"></span>"Go to &lt;app&gt;" deep link


**Cortana** can expose a "Go to &lt;app&gt;" deep link below the content tile on various screens.

![cortana background app completion screen](images/cortana-completion-screen.png)

You can provide a launch argument for this link to open your app with similar context as the app service. If you don't provide a launch argument, the app is launched to the main screen.

Here, we add an [**AppLaunchArgument**](https://msdn.microsoft.com/library/windows/apps/dn974183) parameter with a value of "Las Vegas" to a [**VoiceCommandResponse**](https://msdn.microsoft.com/library/windows/apps/dn974182) object used in the [**ReportSuccessAsync**](https://msdn.microsoft.com/library/windows/apps/dn706580) call of the [**VoiceCommandServiceConnection**](https://msdn.microsoft.com/library/windows/apps/dn974204). object

```CSharp
var userMessage = new VoiceCommandUserMessage();
string keepingTripToDestination = string.Format(
  cortanaResourceMap.GetValue("KeepingTripToDestination", 
    cortanaContext).ValueAsString, destination);
userMessage.DisplayMessage = userMessage.SpokenMessage = 
  keepingTripToDestination;

response = VoiceCommandResponse.CreateResponse(userMessage);
response.AppLaunchArgument = “Las Vegas”;
await voiceServiceConnection.ReportSuccessAsync(response);
```

## <span id="Content_tile_deep_link"></span><span id="content_tile_deep_link"></span><span id="CONTENT_TILE_DEEP_LINK"></span>Content tile deep link


You can provide full content tile deep links on various **Cortana** screens.

![cortana background app hand-off screen ](images/cortana-backgroundapp-progress-result.png)

Like the "Go to &lt;app&gt;" links, you can provide a launch argument to open your app with similar context as the app service. If you don't provide a launch argument, the content tile is not linked to your app.

Here, we add two content tiles with different [**AppLaunchArgument**](https://msdn.microsoft.com/library/windows/apps/dn974183) parameter values to a [**VoiceCommandContentTile**](https://msdn.microsoft.com/library/windows/apps/dn974168) list used in the [**ReportSuccessAsync**](https://msdn.microsoft.com/library/windows/apps/dn706580) call of the [**VoiceCommandServiceConnection**](https://msdn.microsoft.com/library/windows/apps/dn974204) object.

```CSharp
var userMessage = new VoiceCommandUserMessage();
userMessage.DisplayMessage = "Here are your trips.";
userMessage.SpokenMessage = 
  "You have two trips to Vegas coming up.";

var destinationsContentTiles = new List<VoiceCommandContentTile>();

var destinationTile1 = new VoiceCommandContentTile();
destinationTile1.ContentTileType = 
  VoiceCommandContentTileType.TitleWith68x68IconAndText;
destinationTile1.AppLaunchArgument = “id_Vegas_001";
destinationTile1.Title = "Las Vegas Tech Conference";
destinationTile1.TextLine1 = "May 15th 2015";
destinationsContentTiles.Add(destinationTile1);

var destinationTile2 = new VoiceCommandContentTile();
destinationTile2.ContentTileType = 
  VoiceCommandContentTileType.TitleWith68x68IconAndText;
destinationTile2.AppLaunchArgument = “id_Vegas_002";
destinationTile2.Title = "Fun in Vegas";
destinationTile2.TextLine1 = "August 24th 2015";
destinationsContentTiles.Add(destinationTile2);

var response = 
  VoiceCommandResponse.CreateResponse(userMessage, destinationsContentTiles);

response.AppLaunchArgument = “destination=Las Vegas";
    
await voiceServiceConnection.ReportSuccessAsync(response);
```

## <span id="Programmatic_deep_link"></span><span id="programmatic_deep_link"></span><span id="PROGRAMMATIC_DEEP_LINK"></span>Programmatic deep link


You can also programmatically launch your app with a launch argument to open your app with similar context as the app service. If you don't provide a launch argument, the app is launched to the main screen.

Here, we add an [**AppLaunchArgument**](https://msdn.microsoft.com/library/windows/apps/dn974183) parameter with a value of "Las Vegas" to a [**VoiceCommandResponse**](https://msdn.microsoft.com/library/windows/apps/dn974182) object used in the [**RequestAppLaunchAsync**](https://msdn.microsoft.com/library/windows/apps/dn706581) call of the [**VoiceCommandServiceConnection**](https://msdn.microsoft.com/library/windows/apps/dn974204) object.

```CSharp
var userMessage = new VoiceCommandUserMessage();
userMessage.DisplayMessage = "Here are your trips.";
userMessage.SpokenMessage = 
  "You have one trip to Vegas coming up.";

response = VoiceCommandResponse.CreateResponse(userMessage);
response.AppLaunchArgument = “Las Vegas”;
await  VoiceCommandServiceConnection.RequestAppLaunchAsync(response);
```

## <span id="App_manifest"></span><span id="app_manifest"></span><span id="APP_MANIFEST"></span>App manifest


To enable deep linking to your app, you must declare the `windows.personalAssistantLaunch` extension in the Package.appxmanifest file of your app project.

Here, we declare the `windows.personalAssistantLaunch` extension for the **Adventure Works** app.

```XML
<Extensions>
  <uap:Extension Category="windows.appService" 
    EntryPoint="AdventureWorks.VoiceCommands.AdventureWorksVoiceCommandService">
    <uap:AppService Name="AdventureWorksVoiceCommandService"/>
  </uap:Extension>
  <uap:Extension Category="windows.personalAssistantLaunch"/> 
</Extensions>
```

## <span id="Protocol_contract"></span><span id="protocol_contract"></span><span id="PROTOCOL_CONTRACT"></span>Protocol contract


Your app is launched to the foreground through Uniform Resource Identifier (URI) activation using a [**Protocol**](https://msdn.microsoft.com/library/windows/apps/br224693) contract. Your app must override your app's [**OnActivated**](https://msdn.microsoft.com/library/windows/apps/br242330) event and check for an **ActivationKind** of **Protocol**. For more info, see [Handle URI activation](https://msdn.microsoft.com/library/windows/apps/mt228339).

Here, we decode the URI provided by the [**ProtocolActivatedEventArgs**](https://msdn.microsoft.com/library/windows/apps/br224742) to access the launch argument. For this example, the [**Uri**](https://msdn.microsoft.com/library/windows/apps/br224746) is set to "windows.personalassistantlaunch:?LaunchContext=Las Vegas".

```CSharp
if (args.Kind == ActivationKind.Protocol)
  {
    var commandArgs = args as ProtocolActivatedEventArgs;
    Windows.Foundation.WwwFormUrlDecoder decoder = 
      new Windows.Foundation.WwwFormUrlDecoder(commandArgs.Uri.Query);
    var destination = decoder.GetFirstValueByName("LaunchContext");

    navigationCommand = new ViewModel.TripVoiceCommand(
      "protocolLaunch",
      "text",
      "destination",
      destination);

    navigationToPageType = typeof(View.TripDetails);

    rootFrame.Navigate(navigationToPageType, navigationCommand);

    // Ensure the current window is active.
    Window.Current.Activate();
  }
```

## <span id="related_topics"></span>Related articles


**Developers**
* [Cortana interactions](cortana-interactions.md)
* [**VCD elements and attributes v1.2**](https://msdn.microsoft.com/library/windows/apps/dn706593)

**Designers**
* [Cortana design guidelines](https://msdn.microsoft.com/library/windows/apps/dn974233)
* [Speech design guidelines](https://msdn.microsoft.com/library/windows/apps/dn596121)

**Samples**
* [Cortana voice command sample](http://go.microsoft.com/fwlink/p/?LinkID=619899)
 

 






<!--HONumber=Mar16_HO2-->


