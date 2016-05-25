---
Description: Learn how to store and retrieve local, roaming, and temporary app data.
title: Store and retrieve settings and other app data
ms.assetid: 41676A02-325A-455E-8565-C9EC0BC3A8FE
label: App settings and data
template: detail.hbs
---

# Store and retrieve settings and other app data

\[ Updated for UWP apps on Windows 10. For Windows 8.x articles, see the [archive](http://go.microsoft.com/fwlink/p/?linkid=619132) \]

*App data* is mutable data that is specific to a particular app. It includes runtime state, user preferences, and other settings. App data is different from *user data*, data that the user creates and manages when using an app. User data includes document or media files, email or communication transcripts, or database records holding content created by the user. User data may be useful or meaningful to more than one app. Often, this is data that the user wants to manipulate or transmit as an entity independent of the app itself, such as a document.

**Important note about app data:  **The lifetime of the app data is tied to the lifetime of the app. If the app is removed, all of the app data will be lost as a consequence. Don't use app data to store user data or anything that users might perceive as valuable and irreplaceable. We recommend that the user's libraries and Microsoft OneDrive be used to store this sort of information. App data is ideal for storing app-specific user preferences, settings, and favorites.

## Types of app data

There are two types of app data: settings and files.

-   **Settings**

    Use settings to store user preferences and application state info. The app data API enables you to easily create and retrieve settings (we'll show you some examples later in this article).

    Here are data types you can use for app settings:

    -   **UInt8**, **Int16**, **UInt16**, **Int32**, **UInt32**, **Int64**, **UInt64**, **Single**, **Double**
    -   **Boolean**
    -   **Char16**, **String**
    -   [**DateTime**](https://msdn.microsoft.com/library/windows/apps/br206576), [**TimeSpan**](https://msdn.microsoft.com/library/windows/apps/br225996)
    -   **GUID**, [**Point**](https://msdn.microsoft.com/library/windows/apps/br225870), [**Size**](https://msdn.microsoft.com/library/windows/apps/br225995), [**Rect**](https://msdn.microsoft.com/library/windows/apps/br225994)
    -   [**ApplicationDataCompositeValue**](https://msdn.microsoft.com/library/windows/apps/br241588): A set of related app settings that must be serialized and deserialized atomically. Use composite settings to easily handle atomic updates of interdependent settings. The system ensures the integrity of composite settings during concurrent access and roaming. Composite settings are optimized for small amounts of data, and performance can be poor if you use them for large data sets.
-   **Files**

    Use files to store binary data or to enable your own, customized serialized types.

## Storing app data in the app data stores

When an app is installed, the system gives it its own per-user data stores for settings and files. You don't need to know where or how this data exists, because the system is responsible for managing the physical storage, ensuring that the data is kept isolated from other apps and other users. The system also preserves the contents of these data stores when the user installs an update to your app and removes the contents of these data stores completely and cleanly when your app is uninstalled.

Within its app data store, each app has system-defined root directories: one for local files, one for roaming files, and one for temporary files. Your app can add new files and new containers to each of these root directories.

## Local app data

Local app data should be used for any information that needs to be preserved between app sessions and is not suitable for roaming app data. Data that is not applicable on other devices should be stored here as well. There is no general size restriction on local data stored. Use the local app data store for data that it does not make sense to roam and for large data sets.

### Retrieve the local app data store

Before you can read or write local app data, you must retrieve the local app data store. To retrieve the local app data store, use the [**ApplicationData.LocalSettings**](https://msdn.microsoft.com/library/windows/apps/br241622) property to get the app's local settings as an [**ApplicationDataContainer**](https://msdn.microsoft.com/library/windows/apps/br241599) object. Use the [**ApplicationData.LocalFolder**](https://msdn.microsoft.com/library/windows/apps/br241621) property to get the files in a [**StorageFolder**](https://msdn.microsoft.com/library/windows/apps/br227230) object. Use the [**ApplicationData.LocalCacheFolder**](https://msdn.microsoft.com/library/windows/apps/dn633825) property to get the folder in the local app data store where you can save files that are not included in backup and restore.

```cs
Windows.Storage.ApplicationDataContainer localSettings = 
    Windows.Storage.ApplicationData.Current.LocalSettings;
Windows.Storage.StorageFolder localFolder = 
    Windows.Storage.ApplicationData.Current.LocalFolder;
```

### Create and retrieve a simple local setting

To create or write a setting, use the [**ApplicationDataContainer.Values**](https://msdn.microsoft.com/library/windows/apps/br241615) property to access the settings in the `localSettings` container we got in the previous step. This example creates a setting named `exampleSetting`.

```cs
// Simple setting

localSettings.Values["exampleSetting"] = "Hello Windows";
```

To retrieve the setting, you use the same [**ApplicationDataContainer.Values**](https://msdn.microsoft.com/library/windows/apps/br241615) property that you used to create the setting. This example shows how to retrieve the setting we just created.

```cs
// Simple setting
Object value = localSettings.Values["exampleSetting"];
```

### Create and retrieve a local composite value

To create or write a composite value, create an [**ApplicationDataCompositeValue**](https://msdn.microsoft.com/library/windows/apps/br241588) object. This example creates a composite setting named `exampleCompositeSetting` and adds it to the `localSettings` container.

```cs
// Composite setting

Windows.Storage.ApplicationDataCompositeValue composite = 
    new Windows.Storage.ApplicationDataCompositeValue();
composite["intVal"] = 1;
composite["strVal"] = "string";

localSettings.Values["exampleCompositeSetting"] = composite;
```

This example shows how to retrieve the composite value we just created.

```cs
// Composite setting

Windows.Storage.ApplicationDataCompositeValue composite = 
   (Windows.Storage.ApplicationDataCompositeValue)localSettings.Values["exampleCompositeSetting"];

if (composite == null)
{
   // No data
}
else
{
   // Access data in composite["intVal"] and composite["strVal"]
}
```

### Create and read a local file

To create and update a file in the local app data store, use the file APIs, such as [**Windows.Storage.StorageFolder.CreateFileAsync**](https://msdn.microsoft.com/library/windows/apps/br227249) and [**Windows.Storage.FileIO.WriteTextAsync**](https://msdn.microsoft.com/library/windows/apps/hh701505). This example creates a file named `dataFile.txt` in the `localFolder` container and writes the current date and time to the file. The **ReplaceExisting** value from the [**CreationCollisionOption**](https://msdn.microsoft.com/library/windows/apps/br241631) enumeration indicates to replace the file if it already exists.

```cs
async void WriteTimestamp()
{
   Windows.Globalization.DateTimeFormatting.DateTimeFormatter formatter = 
       new Windows.Globalization.DatetimeFormatting.DateTimeFormatter("longtime");

   StorageFile sampleFile = await localFolder.CreateFileAsync("dataFile.txt", 
       CreateCollisionOption.ReplaceExisting);
   await FileIO.WriteTextAsync(sampleFile, formatter.Format(DateTime.Now));
}
```

To open and read a file in the local app data store, use the file APIs, such as [**Windows.Storage.StorageFolder.GetFileAsync**](https://msdn.microsoft.com/library/windows/apps/br227272), [**Windows.Storage.StorageFile.GetFileFromApplicationUriAsync**](https://msdn.microsoft.com/library/windows/apps/hh701741), and [**Windows.Storage.FileIO.ReadTextAsync**](https://msdn.microsoft.com/library/windows/apps/hh701482). This example opens the `dataFile.txt` file created in the previous step and reads the date from the file. For details on loading file resources from various locations, see [How to load file resources](https://msdn.microsoft.com/library/windows/apps/xaml/hh965322).

```cs
async void ReadTimestamp()
{
   try
   {
      StorageFile sampleFile = await localFolder.GetFileAsync("dataFile.txt");
      String timestamp = await FileIO.ReadTextAsync(sampleFile);
      // Data is contained in timestamp
   }
   catch (Exception)
   {
      // Timestamp not found
   }
}
```

## Roaming data

If you use roaming data in your app, your users can easily keep your app's app data in sync across multiple devices. If a user installs your app on multiple devices, the OS keeps the app data in sync, reducing the amount of setup work that the user needs to do for your app on their second device. Roaming also enables your users to continue a task, such as composing a list, right where they left off even on a different device. The OS replicates roaming data to the cloud when it is updated, and synchronizes the data to the other devices on which the app is installed.

The OS limits the size of the app data that each app may roam. See [**ApplicationData.RoamingStorageQuota**](https://msdn.microsoft.com/library/windows/apps/br241625). If the app hits this limit, none of the app's app data will be replicated to the cloud until the app's total roamed app data is less than the limit again. For this reason, it is a best practice to use roaming data only for user preferences, links, and small data files.

Roaming data for an app is available in the cloud as long as it is accessed by the user from some device within the required time interval. If the user does not run an app for longer than this time interval, its roaming data is removed from the cloud. If a user uninstalls an app, its roaming data isn't automatically removed from the cloud, it's preserved. If the user reinstalls the app within the time interval, the roaming data is synchronized from the cloud.

### Register to receive notification when roaming data changes

To use roaming app data, you need to register for roaming data changes and retrieve the roaming data containers so you can read and write settings.

1.  Register to receive notification when roaming data changes.

    The [**DataChanged**](https://msdn.microsoft.com/library/windows/apps/br241620) event notifies you when roaming data changes. This example sets `DataChangeHandler` as the handler for roaming data changes.

```cs
void InitHandlers()
    {
       Windows.Storage.ApplicationData.Current.DataChanged += 
          new TypedEventHandler<ApplicationData, object>(DataChangeHandler);
    }

    void DataChangeHandler(Windows.Storage.ApplicationData appData, object o)
    {
       // TODO: Refresh your data
    }
```

2.  Get the containers for the app's settings and files.

    Use the [**ApplicationData.RoamingSettings**](https://msdn.microsoft.com/library/windows/apps/br241624) property to get the settings and the [**ApplicationData.RoamingFolder**](https://msdn.microsoft.com/library/windows/apps/br241623) property to get the files.

```cs
Windows.Storage.ApplicationDataContainer roamingSettings = 
        Windows.Storage.ApplicationData.Current.RoamingSettings;
    Windows.Storage.StorageFolder roamingFolder = 
        Windows.Storage.ApplicationData.Current.RoamingFolder;
```

### Create and retrieve roaming settings

Use the [**ApplicationDataContainer.Values**](https://msdn.microsoft.com/library/windows/apps/br241615) property to access the settings in the `roamingSettings` container we got in the previous section. This example creates a simple setting named `exampleSetting` and a composite value named `composite`.

```cs
// Simple setting

roamingSettings.Values["exampleSetting"] = "Hello World";
// High Priority setting, for example, last page position in book reader app
roamingSettings.values["HighPriority"] = "65";

// Composite setting

Windows.Storage.ApplicationDataCompositeValue composite = 
    new Windows.Storage.ApplicationDataCompositeValue();
composite["intVal"] = 1;
composite["strVal"] = "string";

roamingSettings.Values["exampleCompositeSetting"] = composite;

```

This example retrieves the settings we just created.

```cs
// Simple setting

Object value = roamingSettings.Values["exampleSetting"];

// Composite setting

Windows.Storage.ApplicationDataCompositeValue composite = 
   (Windows.Storage.ApplicationDataCompositeValue)roamingSettings.Values["exampleCompositeSetting"];

if (composite == null)
{
   // No data
}
else
{
   // Access data in composite["intVal"] and composite["strVal"]
}
```

### Create and retrieve roaming files

To create and update a file in the roaming app data store, use the file APIs, such as [**Windows.Storage.StorageFolder.CreateFileAsync**](https://msdn.microsoft.com/library/windows/apps/br227249) and [**Windows.Storage.FileIO.WriteTextAsync**](https://msdn.microsoft.com/library/windows/apps/hh701505). This example creates a file named `dataFile.txt` in the `roamingFolder` container and writes the current date and time to the file. The **ReplaceExisting** value from the [**CreationCollisionOption**](https://msdn.microsoft.com/library/windows/apps/br241631) enumeration indicates to replace the file if it already exists.

```cs
async void WriteTimestamp()
{
   Windows.Globalization.DateTimeFormatting.DateTimeFormatter formatter = 
       new Windows.Globalization.DatetimeFormatting.DateTimeFormatter("longtime");

   StorageFile sampleFile = await roamingFolder.CreateFileAsync("dataFile.txt", 
       CreationCollisionOption.ReplaceExisting);
   await FileIO.WriteTextAsync(sampleFile, formatter.Format(DateTime.Now));
}
```

To open and read a file in the roaming app data store, use the file APIs, such as [**Windows.Storage.StorageFolder.GetFileAsync**](https://msdn.microsoft.com/library/windows/apps/br227272), [**Windows.Storage.StorageFile.GetFileFromApplicationUriAsync**](https://msdn.microsoft.com/library/windows/apps/hh701741), and [**Windows.Storage.FileIO.ReadTextAsync**](https://msdn.microsoft.com/library/windows/apps/hh701482). This example opens the `dataFile.txt` file created in the previous section and reads the date from the file. For details on loading file resources from various locations, see [How to load file resources](https://msdn.microsoft.com/library/windows/apps/xaml/hh965322).

```cs
async void ReadTimestamp()
{
   try
   {
      StorageFile sampleFile = await roamingFolder.GetFileAsync("dataFile.txt");
      String timestamp = await FileIO.ReadTextAsync(sampleFile);
      // Data is contained in timestamp
   }
   catch (Exception)
   {
      // Timestamp not found
   }
}
```

## Temporary app data

The temporary app data store works like a cache. Its files do not roam and could be removed at any time. The System Maintenance task can automatically delete data stored at this location at any time. The user can also clear files from the temporary data store using Disk Cleanup. Temporary app data can be used for storing temporary information during an app session. There is no guarantee that this data will persist beyond the end of the app session as the system might reclaim the used space if needed. The location is available via the [**temporaryFolder**](https://msdn.microsoft.com/library/windows/apps/br241629) property.

### Retrieve the temporary data container

Use the [**ApplicationData.TemporaryFolder**](https://msdn.microsoft.com/library/windows/apps/br241629) property to get the files. The next steps use the `temporaryFolder` variable from this step.

```cs
Windows.Storage.StorageFolder temporaryFolder = ApplicationData.Current.TemporaryFolder;
```

### Create and read temporary files

To create and update a file in the temporary app data store, use the file APIs, such as [**Windows.Storage.StorageFolder.CreateFileAsync**](https://msdn.microsoft.com/library/windows/apps/br227249) and [**Windows.Storage.FileIO.WriteTextAsync**](https://msdn.microsoft.com/library/windows/apps/hh701505). This example creates a file named `dataFile.txt` in the `temporaryFolder` container and writes the current date and time to the file. The **ReplaceExisting** value from the [**CreationCollisionOption**](https://msdn.microsoft.com/library/windows/apps/br241631) enumeration indicates to replace the file if it already exists.

```cs
async void WriteTimestamp()
{
   Windows.Globalization.DateTimeFormatting.DateTimeFormatter formatter = 
       new Windows.Globalization.DatetimeFormatting.DateTimeFormatter("longtime");

   StorageFile sampleFile = await temporaryFolder.CreateFileAsync("dataFile.txt", 
       CreateCollisionOption.ReplaceExisting);
   await FileIO.WriteTextAsync(sampleFile, formatter.Format(DateTime.Now));
}
```

To open and read a file in the temporary app data store, use the file APIs, such as [**Windows.Storage.StorageFolder.GetFileAsync**](https://msdn.microsoft.com/library/windows/apps/br227272), [**Windows.Storage.StorageFile.GetFileFromApplicationUriAsync**](https://msdn.microsoft.com/library/windows/apps/hh701741), and [**Windows.Storage.FileIO.ReadTextAsync**](https://msdn.microsoft.com/library/windows/apps/hh701482). This example opens the `dataFile.txt` file created in the previous step and reads the date from the file. For details on loading file resources from various locations, see [How to load file resources](https://msdn.microsoft.com/library/windows/apps/xaml/hh965322).

```cs
async void ReadTimestamp()
{
   try
   {
      StorageFile sampleFile = await temporaryFolder.GetFileAsync("dataFile.txt");
      String timestamp = await FileIO.ReadTextAsync(sampleFile);
      // Data is contained in timestamp
   }
   catch (Exception)
   {
      // Timestamp not found
   }
}
```

## Organize app data with containers


To help you organize your app data settings and files, you create containers (represented by [**ApplicationDataContainer**](https://msdn.microsoft.com/library/windows/apps/br241599) objects) instead of working directly with directories. You can add containers to the local, roaming, and temporary app data stores. Containers can be nested up to 32 levels deep.

To create a settings container, call the [**ApplicationDataContainer.CreateContainer**](https://msdn.microsoft.com/library/windows/apps/br241611) method. This example creates a local settings container named `exampleContainer` and adds a setting named `exampleSetting`. The **Always** value from the [**ApplicationDataCreateDisposition**](https://msdn.microsoft.com/library/windows/apps/br241616) enumeration indicates that the container is created if it doesn't already exist.

```cs
Windows.Storage.ApplicationDataContainer localSettings = 
    Windows.Storage.ApplicationData.Current.LocalSettings;
Windows.Storage.StorageFolder localFolder = 
    Windows.Storage.ApplicationData.Current.LocalFolder;

// Setting in a container
Windows.Storage.ApplicationDataContainer container = 
   localSettings.CreateContainer("exampleContainer", Windows.Storage.ApplicationDataCreateDisposition.Always);

if (localSettings.Containers.ContainsKey("exampleContainer"))
{
   localSettings.Containers["exampleContainer"].Values["exampleSetting"] = "Hello Windows";
}
```

## Delete app settings and containers


To delete a simple setting that your app no longer needs, use the [**ApplicationDataContainerSettings.Remove**](https://msdn.microsoft.com/library/windows/apps/br241608) method. This example deletesthe `exampleSetting` local setting that we created earlier.

```cs
Windows.Storage.ApplicationDataContainer localSettings = 
    Windows.Storage.ApplicationData.Current.LocalSettings;
Windows.Storage.StorageFolder localFolder = 
    Windows.Storage.ApplicationData.Current.LocalFolder;

// Delete simple setting

localSettings.Values.Remove("exampleSetting");
```

To delete a composite setting, use the [**ApplicationDataCompositeValue.Remove**](https://msdn.microsoft.com/library/windows/apps/br241597) method. This example deletes the local `exampleCompositeSetting` composite setting we created in an earlier example.

```cs
Windows.Storage.ApplicationDataContainer localSettings = 
    Windows.Storage.ApplicationData.Current.LocalSettings;
Windows.Storage.StorageFolder localFolder = 
    Windows.Storage.ApplicationData.Current.LocalFolder;

// Delete composite setting

localSettings.Values.Remove("exampleCompositeSetting");
```

To delete a container, call the [**ApplicationDataContainer.DeleteContainer**](https://msdn.microsoft.com/library/windows/apps/br241612) method. This example deletes the local `exampleContainer` settings container we created earlier.

```cs
Windows.Storage.ApplicationDataContainer localSettings = 
    Windows.Storage.ApplicationData.Current.LocalSettings;
Windows.Storage.StorageFolder localFolder = 
    Windows.Storage.ApplicationData.Current.LocalFolder;

// Delete container

localSettings.DeleteContainer("exampleContainer");
```

## Versioning your app data


You can optionally version the app data for your app. This would enable you to create a future version of your app that changes the format of its app data without causing compatibility problems with the previous version of your app. The app checks the version of the app data in the data store, and if the version is less than the version the app expects, the app should update the app data to the new format and update the version. For more info, see the[**Application.Version**](https://msdn.microsoft.com/library/windows/apps/br241630) property and the [**ApplicationData.SetVersionAsync**](https://msdn.microsoft.com/library/windows/apps/hh701429) method.

 

 






<!--HONumber=May16_HO4-->


