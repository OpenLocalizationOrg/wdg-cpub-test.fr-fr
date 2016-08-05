---
author: drewbatgit
ms.assetid: 3b75d881-bdcf-402b-a330-23cd29d68e53
description: This article lists the DeviceInformation properties related to audio devices
title: Audio device information properties
translationtype: Human Translation
ms.sourcegitcommit: 015108445108522621f90863a4d5a9637f8484dd
ms.openlocfilehash: b1bcb5b005e82303884c2e096356d5a0f542b1e1

---

# Audio device information properties

This article lists the device information properties related to audio devices. On Windows, each hardware device has associated [**DeviceInformation**](https://msdn.microsoft.com/library/windows/apps/BR225393) properties providing detailed information about a device that you can use when you need specific information about the device or when you are building a device selector. For general information about enumerating devices on Windows, see [**Enumerate devices**](../devices-sensors/enumerate-devices.md) and [**Device information properties**](../devices-sensors/device-information-properties.md).


|Name|Type|Description|
|------------------------------------------------------------|------------|------------------------------------------------------|
|**System.Devices.AudioDevice.SpeechProcessingSupported**|Boolean|Indicates whether the audio device supports speech processing.|
|**System.Devices.AudioDevice.RawProcessingSupported**|Boolean|Indicates whether the audio device supports raw processing.|
|**System.Devices.MicrophoneArray.Geometry**|unsigned char[]|Geometry data for a microphone array.|
## Related topics

* [**Enumerate devices**](../devices-sensors/enumerate-devices.md)
* [**Device information properties**](../devices-sensors/device-information-properties.md)
* [**Build a device selector**](../devices-sensors/build-a-device-selector.md)







<!--HONumber=Jul16_HO3-->


