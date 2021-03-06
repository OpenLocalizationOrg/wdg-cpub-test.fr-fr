---
author: drewbatgit
ms.assetid: 05E418B4-5A62-42BD-BF66-A0762216D033
description: This topic shows you how to get a preview frame from the media capture preview stream.
title: Get a preview frame
translationtype: Human Translation
ms.sourcegitcommit: 015108445108522621f90863a4d5a9637f8484dd
ms.openlocfilehash: c512ec92272ab03cfd8e91602018f09ef8225652

---

# Get a preview frame

\[ Updated for UWP apps on Windows 10. For Windows 8.x articles, see the [archive](http://go.microsoft.com/fwlink/p/?linkid=619132) \]

This topic shows you how to get a preview frame from the media capture preview stream.

**Note**  
This article builds on concepts and code discussed in [Capture Photos and Video with MediaCapture](capture-photos-and-video-with-mediacapture.md), which describes the steps for implementing basic photo and video capture. It is recommended that you familiarize yourself with the basic media capture pattern in that article before moving on to more advanced capture scenarios. The code in this article assumes that your app already has an instance of MediaCapture that has been properly initialized and that you have a [**CaptureElement**](https://msdn.microsoft.com/library/windows/apps/br209278) with an active video preview stream.

In addition to the namespaces required for basic media capture, capturing a preview frame requires the following namespace.

[!code-cs[PreviewFrameUsing](./code/BasicMediaCaptureWin10/cs/MainPage.xaml.cs#SnippetPreviewFrameUsing)]

When you request a preview frame, you can specify the format in which you would like to receive the frame by creating a [**VideoFrame**](https://msdn.microsoft.com/library/windows/apps/dn930917) object with the format you desire. This example creates a video frame that is the same resolution as the preview stream by calling [**VideoDeviceController.GetMediaStreamProperties**](https://msdn.microsoft.com/library/windows/apps/br211995) and specifying [**MediaStreamType.VideoPreview**](https://msdn.microsoft.com/library/windows/apps/br226640) to request the properties for the preview stream. The width and height of the preview stream is used to create the new video frame.

[!code-cs[CreateFormatFrame](./code/BasicMediaCaptureWin10/cs/MainPage.xaml.cs#SnippetCreateFormatFrame)]

If your [**MediaCapture**](https://msdn.microsoft.com/library/windows/apps/br241124) object is initialized and you have an active preview stream, call [**GetPreviewFrameAsync**](https://msdn.microsoft.com/library/windows/apps/dn926711) to get a preview stream. Pass in the video frame created in the last step to specify the format of the returned frame.

[!code-cs[GetPreviewFrameAsync](./code/BasicMediaCaptureWin10/cs/MainPage.xaml.cs#SnippetGetPreviewFrameAsync)]

Get a [**SoftwareBitmap**](https://msdn.microsoft.com/library/windows/apps/dn887358) representation of the preview frame by accessing the [**SoftwareBitmap**](https://msdn.microsoft.com/library/windows/apps/dn930926) property of the [**VideoFrame**](https://msdn.microsoft.com/library/windows/apps/dn930917) object. For information on saving, loading, and modifying software bitmaps, see [Imaging](imaging.md).

[!code-cs[GetPreviewBitmap](./code/BasicMediaCaptureWin10/cs/MainPage.xaml.cs#SnippetGetPreviewBitmap)]

You can also get a [**IDirect3DSurface**](https://msdn.microsoft.com/library/windows/apps/dn965505) representation of the preview frame if you want to use the image with Direct3D APIs.

[!code-cs[GetPreviewSurface](./code/BasicMediaCaptureWin10/cs/MainPage.xaml.cs#SnippetGetPreviewSurface)]

**Important**  
Either the [**SoftwareBitmap**](https://msdn.microsoft.com/library/windows/apps/dn930926) property or the [**Direct3DSurface**](https://msdn.microsoft.com/library/windows/apps/dn930920) property of the returned **VideoFrame** may be null depending on how you call **GetPreviewFrameAsync** and also depending on the device on which your app is running.

-   If you call the overload of [**GetPreviewFrameAsync**](https://msdn.microsoft.com/library/windows/apps/dn926713) that accepts a **VideoFrame** argument, then the returned **VideoFrame** will have a non-null **SoftwareBitmap** and the **Direct3DSurface** property will be null.
-   If you call the overload of [**GetPreviewFrameAsync**](https://msdn.microsoft.com/library/windows/apps/dn926712) that has no arguments on a device that uses a Direct3D surface to represent the frame internally, the **Direct3DSurface** property will be non-null and the **SoftwareBitmap** property will be null.
-   If you call the overload of [**GetPreviewFrameAsync**](https://msdn.microsoft.com/library/windows/apps/dn926712) that has no arguments on a device that does not use a Direct3D surface to represent the frame internally, the **SoftwareBitmap** property will be non-null and the **Direct3DSurface** property will be null.

Your app should always check for a null value before trying to operate on the objects returned by the **SoftwareBitmap** or **Direct3DSurface** properties.

When you are done using the preview frame, be sure to call its [**Close**](https://msdn.microsoft.com/library/windows/apps/dn930918) method (projected to Dispose in C#) to free the resources used by the frame. Or, use the **using** pattern, which automatically disposes of the object.

[!code-cs[CleanUpPreviewFrame](./code/BasicMediaCaptureWin10/cs/MainPage.xaml.cs#SnippetCleanUpPreviewFrame)]

## Related topics

* [Capture photos and video with MediaCapture](capture-photos-and-video-with-mediacapture.md)
 

 







<!--HONumber=Jul16_HO3-->


