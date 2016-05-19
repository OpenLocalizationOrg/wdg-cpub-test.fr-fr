---
Description: The App properties page of the app submission process lets you define your app's category and indicate hardware preferences or other declarations.
title: Enter app properties
ms.assetid: CDE4AF96-95A0-4635-9D07-A27B810CAE26
---

# Enter app properties

The **App properties** page of the [app submission process](app-submissions.md) lets you define your app's category and indicate hardware preferences or other declarations. Here, we'll walk through the options on this page and what you should consider when entering this information.

**Note**  Age ratings are now a separate page of the submission process. For more info, see [Age ratings](age-ratings.md).


## Category and subcategory

In this section, you indicate the category (and subcategory, if applicable) which the Store should use to categorize your app. Specifying a category is required in order to submit your app.

For more info, see [Category and subcategory table](category-and-subcategory-table.md).

## Hardware preferences


In this section, you have the option to indicate if certain hardware features are required to run and interact with your app properly.

If so, the Windows Store will try to detect whether a customer's device supports the selected hardware feature. If we detect that it doesn’t, a warning will be presented that informs the customer that they are trying to download an app that has declared a preference for that hardware. Customers on Windows 10 devices will also see the selected feature(s) listed in the **Hardware requirements** section of your app’s Store listing.

This won't prevent people from downloading your app on devices that don't have the appropriate hardware, but they won't be able to rate or review your app on those devices.

**Important**  Except for **Touch screen**, these warnings are only displayed to customers on Windows 10 devices which don't have the selected feature(s).


In addition to making a selection here, we recommend adding runtime checks for the specified hardware into your app, since the Store may not always be able to detect that a customer's device is missing the selected feature and they'll still be able to download your app even if a warning is displayed.

**Tip**  If you want to prevent your UWP app from being downloaded on a device which doesn't meet minimum requirements for memory or DirectX level, you can designate the minimum requirements in a StoreManifest XML file. For more info, see [StoreManifest schema (Windows 10)](https://msdn.microsoft.com/library/windows/apps/mt617335).


## App declarations


You can check boxes in this section to indicate if any of the declarations apply to your app. This may affect the way your app is displayed, whether it is offered to certain customers, or how customers can use it.

For more info, see [App declarations](app-declarations.md).


<!--HONumber=Mar16_HO2-->


