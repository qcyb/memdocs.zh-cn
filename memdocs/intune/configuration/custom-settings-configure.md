---
title: 在 Microsoft Intune 中使用自定义设备设置 - Azure | Microsoft Docs
description: 添加或创建配置文件，以便通过 Microsoft Intune 使用适用于 Windows Phone、Windows 8.1、Windows 10 及更高版本、Android 设备管理员、Android Enterprise、macOS 和 iOS/iPadOS 设备的自定义设置。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/18/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6122f4624cc40152184c1c460afa6a7a39976063
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/21/2020
ms.locfileid: "80083990"
---
# <a name="create-a-profile-with-custom-settings-in-intune"></a>使用 Intune 中的自定义设置创建配置文件

Microsoft Intune 含有许多内置设置，用于控制设备上的不同功能。 还可以创建自定义配置文件，这些文件的创建方式类似于内置配置文件。 希望使用未内置于 Intune 中的设备设置和功能时，自定义配置文件非常有用。 这些配置文件包含用于控制组织中设备的功能和设置。 例如，你可以创建自定义配置文件，为每台 iOS/iPadOS 设备设置相同的功能。

每个平台的自定义设置配置都不相同。 例如，要控制 Android 和 Windows 设备上的功能，可输入开放移动联盟统一资源标识符 (OMA-URI) 值。 对于 Apple 设备，则可以导入使用 [Apple Configurator](https://itunes.apple.com/us/app/apple-configurator-2/id1037126344?mt=12) 或 [Apple 配置文件管理器](https://support.apple.com/profile-manager)创建的文件。

有关配置文件的详细信息，请参阅[什么是 Microsoft Intune 设备配置文件？](device-profiles.md)。

本文介绍如何为 Android 设备管理员、Android Enterprise、iOS/iPadOS、macOS 和 Windows 创建自定义配置文件。 还可以查看所有适用于不同平台的可用设置。

## <a name="create-the-profile"></a>创建配置文件

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“设备”   > “配置文件”   > “创建配置文件”  。
3. 输入以下属性：

    - **名称**：输入策略的描述性名称。 为策略命名，以便稍后可以轻松地识别它们。 例如，将策略名称命名为“Windows 10:  自定义启用 AllowVPNOverCellular 自定义 OMA-URI 的配置文件。
    - **描述**：输入配置文件的说明。 此设置是可选的，但建议进行。
    - **平台**：选择设备平台。 选项包括：

      - **Android 设备管理员**
      - **Android Enterprise**
      - **iOS/iPadOS**
      - **macOS**
      - **Windows 10 及更高版本**
      - **Windows 8.1 及更高版本**

    - **配置文件类型**：选择“自定义”  。

4. 针对每个平台的设置会有所不同。 若要查看特定平台的设置，请选择你的平台：

    - [Android 设备管理员](custom-settings-android.md)
    - [Android Enterprise](custom-settings-android-for-work.md)
    - [iOS/iPadOS](custom-settings-ios.md)
    - [macOS](custom-settings-macos.md)
    - [Windows 10](custom-settings-windows-10.md)
    - [Windows Holographic for Business](custom-settings-windows-holographic.md)
    - [Windows Phone 8.1](custom-settings-windows-phone-8-1.md)

5. 完成后，依次选择“创建配置文件”   > “创建”  。

此时，配置文件创建，并显示在配置文件列表中（“设备配置”   > “配置文件”  ）。

## <a name="next-steps"></a>后续步骤

创建配置文件后，即可进行分配。 下一步，[分配配置文件](device-profile-assign.md)并[监视其状态](device-profile-monitor.md)。
