---
author: drewbatgit
ms.assetid: 923D8156-81D3-4A1E-9D02-DB219F600FDB
description: This article describes how to create Universal Windows Platform (UWP) apps that play audio in the background.
title: Background Audio
translationtype: Human Translation
ms.sourcegitcommit: 015108445108522621f90863a4d5a9637f8484dd
ms.openlocfilehash: 9275a194017f08692adee6de1c4d1f6deb680613

---

# Background Audio

\[ Updated for UWP apps on Windows 10. For Windows 8.x articles, see the [archive](http://go.microsoft.com/fwlink/p/?linkid=619132) \]


This article describes how to create Universal Windows Platform (UWP) apps that play audio in the background. This means that even after the user has minimized your app, returned to the home screen, or has navigated away from your app in some other way, your app can continue to play audio. This article discusses the components of a background audio app and how they work together.

Scenarios for background audio playback include:

-   **Long-running playlists:** The user briefly brings up a foreground app to select and start a playlist, after which the user expects the playlist to continue playing in the background.

-   **Using task switcher:** The user briefly brings up a foreground app to start playing audio, then switches to another open app using the task switcher. The user expects the audio to continue playing in the background.

The background audio implementation described in this article will allow your app to run universally on all Windows devices including Mobile, Desktop, and Xbox.

**Note**  
The [Background audio UWP sample](http://go.microsoft.com/fwlink/?LinkId=619485) implements the code discussed in this overview. You can download the sample to see the code in context or to use as a starting point for your own app.

 

## Background audio architecture

An app performing background playback consists of two processes. The first process is the main app, which contains the app UI and client logic, running in the foreground. The second process is the background playback task, which implements [**IBackgroundTask**](https://msdn.microsoft.com/library/windows/apps/br224794) like all UWP app background tasks. The background task contains the audio playback logic and background services. The background task communicates with the system through the System Media Transport Controls.

The following diagram is an overview of how the system is designed.

![windows 10 background audio architecture](images/backround-audio-architecture-win10.png)
## MediaPlayer

The [**Windows.Media.Playback**](https://msdn.microsoft.com/library/windows/apps/dn640562) namespace contains APIs used to play audio in the background. There is a single instance of [**MediaPlayer**](https://msdn.microsoft.com/library/windows/apps/dn652535) per app through which playback occurs. Your background audio app calls methods and sets properties on the **MediaPlayer** class to set the current track, start playback, pause, fast forward, rewind, and so on. The media player object instance is always accessed through the [**BackgroundMediaPlayer.Current**](https://msdn.microsoft.com/library/windows/apps/dn652528) property.

## MediaPlayer Proxy and Stub

When **BackgroundMediaPlayer.Current** is accessed from your app's background process, the **MediaPlayer** instance is activated in the background task host and can be manipulated directly.

When **BackgroundMediaPlayer.Current** is accessed from the foreground application, the **MediaPlayer** instance that is returned is actually a proxy that communicates with a stub in the background process. This stub communicates with the actual **MediaPlayer** instance, which is also hosted in the background process.

Both the foreground and background process can access most of the properties of the **MediaPlayer** instance, with the exception of [**MediaPlayer.Source**](https://msdn.microsoft.com/library/windows/apps/dn987010) and [**MediaPlayer.SystemMediaTransportControls**](https://msdn.microsoft.com/library/windows/apps/dn926635) which can only be accessed from the background process. The foreground app and the background process can both receive notifications of media-specific events like [**MediaOpened**](https://msdn.microsoft.com/library/windows/apps/dn652609), [**MediaEnded**](https://msdn.microsoft.com/library/windows/apps/dn652603), and [**MediaFailed**](https://msdn.microsoft.com/library/windows/apps/dn652606).

## Playback Lists

A common scenario for background audio applications is to play multiple items in a row. This is most easily accomplished in your background process by using a [**MediaPlaybackList**](https://msdn.microsoft.com/library/windows/apps/dn930955) object, which can be set as a source on the **MediaPlayer** by assigning it to the [**MediaPlayer.Source**](https://msdn.microsoft.com/library/windows/apps/dn987010) property.

It is not possible to access a **MediaPlaybackList** from the foreground process that was set in the background process.

## System Media Transport Controls

A user may control audio playback without directly using your app's UI through means such as Bluetooth devices, SmartGlass, and the System Media Transport Controls. Your background task uses the [**SystemMediaTransportControls**](https://msdn.microsoft.com/library/windows/apps/dn278677) class to subscribe to these user-initiated system events.

To get a **SystemMediaTransportControls** instance from within the background process, use the [**MediaPlayer.SystemMediaTransportControls**](https://msdn.microsoft.com/library/windows/apps/dn926635) property. Foreground apps get an instance of the class by calling [**SystemMediaTransportControls.GetForCurrentView**](https://msdn.microsoft.com/library/windows/apps/dn278708), but the instance returned is a foreground-only instance that does not relate to the background task.

## Sending Messages Between Tasks

There are times when you will want to communicate between the two processes of a background audio app. For example, you might want the background task to notify the foreground task when a new track starts playing, and then send the new song title to the foreground task to display on the screen.

A simple communication mechanism raises events in both the foreground and background processes. The [**SendMessageToForeground**](https://msdn.microsoft.com/library/windows/apps/dn652533) and [**SendMessageToBackground**](https://msdn.microsoft.com/library/windows/apps/dn652532) methods each invoke events in the corresponding process. Messages can be received by subscribing to the [**MessageReceivedFromBackground**](https://msdn.microsoft.com/library/windows/apps/dn652530) and [**MessageReceivedFromForeground**](https://msdn.microsoft.com/library/windows/apps/dn652531) events.

Data can be passed as an argument to the send message methods that are then passed into the message received event handlers. Pass data using the [**ValueSet**](https://msdn.microsoft.com/library/windows/apps/dn636131) class. This class is a dictionary that contains a string as a key and other value types as values. You can pass simple value types such as integers, strings, and booleans.

**Note**  
Apps should only call [**SendMessageToForeground**](https://msdn.microsoft.com/library/windows/apps/dn652533) while the foreground app is running. Attempting to call this method while the foreground app is not running will throw an exception. An app is responsible for communicating the foreground app state to the background process. This can be done using app lifecycle events, state values kept  in local storage, and messages between processes. 

## Background Task Life Cycle

The lifetime of a background task is closely tied to your app's current playback status. For example, when the user pauses audio playback, the system may terminate or cancel your app depending on the circumstances. After a period of time without audio playback, the system may automatically shut down the background task.

The [**IBackgroundTask.Run**](https://msdn.microsoft.com/library/windows/apps/br224811) method is called the first time your app accesses either [**BackgroundMediaPlayer.Current**](https://msdn.microsoft.com/library/windows/apps/dn652528) from code running in the foreground app or when you register a handler for the [**MessageReceivedFromBackground**](https://msdn.microsoft.com/library/windows/apps/dn652530) event, whichever occurs first. It is recommended that you register for the message received handler before calling **BackgroundMediaPlayer.Current** for the first time so that the foreground app doesn't miss any messages sent from the background process.

To keep the background task alive, your app must request a [**BackgroundTaskDeferral**](https://msdn.microsoft.com/library/windows/apps/hh700499) from within the **Run** method and call [**BackgroundTaskDeferral.Complete**](https://msdn.microsoft.com/library/windows/apps/hh700504) when the task instance receives the [**Canceled**](https://msdn.microsoft.com/library/windows/apps/br224798) or [**Completed**](https://msdn.microsoft.com/library/windows/apps/br224788) events. Do not loop or wait in the **Run** method because this consumes resources and may cause your app's background task to be terminated by the system.

Your background task gets the **Completed** event when the **Run** method is completed and deferral is not requested. In some cases, when your app gets the **Canceled** event, it can be also followed by the **Completed** event. Your task may receive a **Canceled** event while **Run** is executing, so be sure to manage this potential concurrence.

Situations in which the background task can be cancelled include:

-   A new app with audio playback capabilities starts on systems that enforce the exclusivity sub-policy. See the [System policies for background audio task lifetime](#system-policies-for-background-audio-task-lifetime) section below.

-   A background task has been launched but music is not yet playing, and then the foreground app is suspended.

-   Other media interruptions, such as incoming phone calls or VoIP calls.

Situations in which the background task can be terminated without notice include:

-   A VoIP call comes in and there is not enough available memory on the system to keep the background task alive.

-   A resource policy is violated.

-   Task cancellation or completion does not end gracefully.

## System policies for background audio task lifetime

The following policies help determine how the system manages the lifetime of background audio tasks.

### Exclusivity

If enabled, this sub-policy limits the number of background audio tasks to be at most 1 at any given time. It is enabled on Mobile and other non-Desktop SKUs.

### Inactivity Timeout

Due to resource constraints, the system may terminate your background task after a period of inactivity.

A background task is considered “inactive” if both of the following conditions are met:

-   The foreground app is not visible (it is suspended or terminated).

-   The background media player is not in the playing state.

If both of these conditions are satisfied, the background media system policy will start a timer. If neither condition has changed when the timer expires, the background media system policy will terminate the background task.

### Shared Lifetime

If enabled, this sub-policy forces the background task to be dependent on the lifetime of the foreground task. If the foreground task is shut down, either by the user or the system, the background task will also shut down.

However, note that this does not mean that the foreground is dependent on the background. If the background task is shut down, this does not force the foreground task to shut down.

The following table lists the which policies are enforced on which device types.

| Sub-policy             | Desktop  | Mobile   | Other    |
|------------------------|----------|----------|----------|
| **Exclusivity**        | Disabled | Enabled  | Enabled  |
| **Inactivity Timeout** | Disabled | Enabled  | Disabled |
| **Shared Lifetime**    | Enabled  | Disabled | Disabled |

 

 

 







<!--HONumber=Jul16_HO3-->


