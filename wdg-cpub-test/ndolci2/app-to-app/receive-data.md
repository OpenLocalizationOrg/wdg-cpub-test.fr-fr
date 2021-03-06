---
description: This article explains how to receive content in your Universal Windows Platform (UWP) app shared from another app using Share contract. This Share contract allows your app to be presented as an option when the user invokes Share.
title: Receive data
ms.assetid: 0AFF9E0D-DFF4-4018-B393-A26B11AFDB41
---

# Receive data

\[ Updated for UWP apps on Windows 10. For Windows 8.x articles, see the [archive](http://go.microsoft.com/fwlink/p/?linkid=619132) \]


This article explains how to receive content in your Universal Windows Platform (UWP) app shared from another app using Share contract. This Share contract allows your app to be presented as an option when the user invokes Share.

## Declare your app as a share target

The system displays a list of possible target apps when a user invokes Share. In order to appear on the list, your app need to declare that it supports the Share contract. This lets the system know that your app is available to receive content.

1.  Open the manifest file. It should be called something like **package.appxmanifest**.
2.  Open the **Declarations** tab.
3.  Choose **Share Target** from the **Available Declarations** list and click **Add**.

## Choose file types and formats

Next, decide what file types and data formats you support. The Share APIs support several standard formats, such as Text, HTML, and Bitmap. You can also specify custom file types and data formats. If you do, remember that source apps have to know what those types and formats are, otherwise those apps can't use the formats to share data.

Only register for formats your app can handle. Only target apps that support the data being shared appear when the user invokes share.

To set file types:

1.  Open the manifest file. It should be called something like **package.appxmanifest**.
2.  In the **Supported File Types** section of the **Declarations** page, click **Add New**.
3.  Type the file name extension that you want to support. For example, .docx. You need to include the period. If you want to support all file types, check the **SupportsAnyFileType** box.

To set data formats:

1.  Open the manifest file.
2.  Open the **Data Formats** section of the **Declarations** page and click **Add New**.
3.  Type the name of the data format you support. For example, "Text".

## Handle share activation

When a user selects your app (usually by selecting it from a list of available target apps in the share UI), an [**Application.OnShareTargetActivated**][OnShareTargetActivated] event is raised. Your app needs to handle this event to process the data the user wants to share.

Note that if your app is running when it is activated as a Share target, the existing instance of your app is terminated and a new instance of your app is launched to handle the contract.

<!-- For some reason, the snippets in this file are all inline in the WDCML topic. Suggest moving to VS project with rest of snippets. -->
```cs
protected override async void OnShareTargetActivated(ShareTargetActivatedEventArgs args)
{
    // Code to handle activation goes here. 
} 
```

The data that the user wants to share is contained in a ShareOperation object. You can use this object to check the format of the data it contains.

```cs
ShareOperation shareOperation = args.ShareOperation;
if (shareOperation.Data.Contains(StandardDataFormats.Text))
{
    string text = await shareOperation.Data.GetTextAsync();

    // To output the text from this example, you need a TextBlock control
    // with a name of &quot;sharedContent&quot;.
    sharedContent.Text = &quot;Text: &quot; + text;
} 
```

## Report sharing status

In some cases, it can take time for your app to process the data it wants to share. Examples include users sharing collections of files or images. These items are larger than a simple text string, so they take longer to process.

```cs
shareOperation.ReportDataRetreived(); 
```

After calling [**ReportStarted**][ReportStarted], don't expect any more user interaction with your app. As a result, you shouldn't call it unless your app is at a point where it can be dismissed by the user.

With an extended share, it's possible that the user might dismiss the source app before your app has all the data from the DataPackage object. As a result, we recommend that you let the system know when your app has acquired the data it needs. This way, the system can suspend or terminate the source app as necessary.

```cs
shareOperation.ReportSubmittedBackgroundTask(); 
```

If something goes wrong, call [**ReportError**][ReportError] to send an error message to the system. The user will see the message when they check on the status of the share. At that point, your app is shut down and the share is ended. The user will need to start again to share the content to your app. Depending on your scenario, you may decide that a particular error isn't serious enough to end the share operation. In that case, you can choose to not call **ReportError** and to continue with the share.

```cs
shareOperation.ReportError(&quot;Could not reach the server! Try again later.&quot;); 
```

Finally, when your app has successfully processed the shared content, you should call [**ReportCompleted**][ReportCompleted] to let the system know.

```cs
shareOperation.ReportCompleted();
```

When you use these methods, you usually call them in the order just described, and you don't call them more than once. However, there are times when a target app can call [**ReportDataRetrieved**][ReportDataRetrieved] before [**ReportStarted**][ReportStarted]. For example, the app might retrieve the data as part of a task in the activation handler, but not call **ReportStarted** until the user clicks a Share button.

## Return a QuickLink if sharing was successful

When a user selects your app to receive content, we recommend that you create a [**QuickLink**][QuickLink]. A **QuickLink** is like a shortcut that makes it easier for users to share information with your app. For example, you could create a **QuickLink** that opens a new mail message pre-configured with a friend's email address.

A **QuickLink** must have a title, an icon, and an Id. The title (like "Email Mom") and icon appear when the user taps the Share charm. The Id is what your app uses to access any custom information, such as an email address or login credentials. When your app creates a **QuickLink**, the app returns the **QuickLink** to the system by calling [**ReportCompleted**][ReportCompleted].

A **QuickLink** does not actually store data. Instead, it contains an identifier that, when selected, is sent to your app. Your app is responsible for storing the Id of the **QuickLink** and the corresponding user data. When the user taps the **QuickLink**, you can get its Id through the [**ShareOperation.QuickLinkId**][QuickLInkId] property.

```cs
async void ReportCompleted(ShareOperation shareOperation, string quickLinkId, string quickLinkTitle)
{
    QuickLink quickLinkInfo = new QuickLink
    {
        Id = quickLinkId,
        Title = quickLinkTitle,

        // For quicklinks, the supported FileTypes and DataFormats are set 
        // independently from the manifest
        SupportedFileTypes = { &quot;*&quot; },
        SupportedDataFormats = { StandardDataFormats.Text, StandardDataFormats.Uri, 
                StandardDataFormats.Bitmap, StandardDataFormats.StorageItems }
    };

    StorageFile iconFile = await Windows.ApplicationModel.Package.Current.InstalledLocation.CreateFileAsync(
            &quot;assets\\user.png&quot;, CreationCollisionOption.OpenIfExists);
    quickLinkInfo.Thumbnail = RandomAccessStreamReference.CreateFromFile(iconFile);
    shareOperation.ReportCompleted(quickLinkInfo);
}
```

## Related topics
* [Share data](share-data.md)
 
<!-- LINKS -->
* [OnShareTargetActivated](https://msdn.microsoft.com/en-us/library/windows/apps/windows.ui.xaml.application.onsharetargetactivated.aspx)
* [ReportStarted](https://msdn.microsoft.com/en-us/library/windows/apps/windows.applicationmodel.datatransfer.sharetarget.shareoperation.reportstarted.aspx)
* [ReportError](https://msdn.microsoft.com/en-us/library/windows/apps/windows.applicationmodel.datatransfer.sharetarget.shareoperation.reporterror.aspx)
* [ReportCompleted](https://msdn.microsoft.com/en-us/library/windows/apps/windows.applicationmodel.datatransfer.sharetarget.shareoperation.reportecompleted.aspx)
* [ReportDataRetrieved](https://msdn.microsoft.com/en-us/library/windows/apps/windows.applicationmodel.datatransfer.sharetarget.shareoperation.reportdataretrieved.aspx)
* [ReportStarted](https://msdn.microsoft.com/en-us/library/windows/apps/windows.applicationmodel.datatransfer.sharetarget.shareoperation.reportstarted.aspx)
* [QuickLink](https://msdn.microsoft.com/en-us/library/windows/apps/windows.applicationmodel.datatransfer.sharetarget.quicklink.aspx)
* [QuickLInkId](https://msdn.microsoft.com/en-us/library/windows/apps/windows.applicationmodel.datatransfer.sharetarget.quicklink.id.aspx)




<!--HONumber=May16_HO4-->


