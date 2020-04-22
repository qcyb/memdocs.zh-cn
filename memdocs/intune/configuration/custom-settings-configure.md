---
title: 在 Microsoft Intune 中使用自定义设备设置 - Azure | Microsoft Docs
description: 添加或创建配置文件，以便通过 Microsoft Intune 使用适用于 Windows Phone、Windows 8.1、Windows 10 及更高版本、Android 设备管理员、Android Enterprise、macOS 和 iOS/iPadOS 设备的自定义设置。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/24/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: feb211b1de15aa0400e9ff71b428e2db02ef4b03
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "80551365"
---
# <a name="create-a-profile-with-custom-settings-in-intune"></a>使用 Intune 中的自定义设置创建配置文件

Microsoft Intune 含有许多内置设置，用于控制设备上的不同功能。 还可以创建自定义配置文件，这些文件的创建方式类似于内置配置文件。 希望使用未内置于 Intune 中的设备设置和功能时，自定义配置文件非常有用。 这些配置文件包含用于控制组织中设备的功能和设置。 例如，你可以创建自定义配置文件，为每台 iOS/iPadOS 设备设置相同的功能。

每个平台的自定义设置配置都不相同。 例如，要控制 Android 和 Windows 设备上的功能，可输入开放移动联盟统一资源标识符 (OMA-URI) 值。 对于 Apple 设备，则可以导入使用 [Apple Configurator](https://itunes.apple.com/us/app/apple-configurator-2/id1037126344?mt=12) 或 [Apple 配置文件管理器](https://support.apple.com/profile-manager)创建的文件。

有关配置文件的详细信息，请参阅[什么是 Microsoft Intune 设备配置文件？](device-profiles.md)。

本文介绍如何为 Android 设备管理员、Android Enterprise、iOS/iPadOS、macOS 和 Windows 创建自定义配置文件。 还可以查看所有适用于不同平台的可用设置。

> [!NOTE]
> Intune 用户界面 (UI) 正在更新为提供全屏体验，可能需要数周时间才能完成。 在租户收到此更新之前，创建或编辑本文所述的设置时的工作流将略有不同。

## <a name="create-the-profile"></a>创建配置文件

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“设备”   > “配置文件”   > “创建配置文件”  。
3. 输入以下属性：

    - **平台**：选择设备平台。 选项包括：  

        - **Android 设备管理员**
        - **Android Enterprise**
        - **iOS/iPadOS**
        - **macOS**
        - **Windows 10 及更高版本**
        - **Windows Phone 8.1**

    - **配置文件**：选择“自定义”  。

4. 选择“创建”。 
5. 在“基本信息”  中，输入以下属性：

    - **名称**：输入策略的描述性名称。 为策略命名，以便稍后可以轻松地识别它们。 例如，将策略名称命名为“Windows 10:  自定义启用 AllowVPNOverCellular 自定义 OMA-URI 的配置文件。
    - **描述**：输入策略的说明。 此设置是可选的，但建议进行。

6. 选择“下一步”  。

7. 在“配置设置”  中，根据所选择的平台，可配置的设置有所不同。 选择平台，以了解详细设置：

    - [Android 设备管理员](custom-settings-android.md)
    - [Android Enterprise](custom-settings-android-for-work.md)
    - [iOS/iPadOS](custom-settings-ios.md)
    - [macOS](custom-settings-macos.md)
    - [Windows 10](custom-settings-windows-10.md)
    - [Windows Holographic for Business](custom-settings-windows-holographic.md)
    - [Windows Phone 8.1](custom-settings-windows-phone-8-1.md)

8. 选择“下一步”  。
9. 在“作用域标记”（可选）中，分配一个标记以将配置文件筛选到特定 IT 组（如 `US-NC IT Team` 或 `JohnGlenn_ITDepartment`）  。 有关范围标记的详细信息，请参阅[将 RBAC 和范围标记用于分布式 IT](../fundamentals/scope-tags.md)。

    选择“下一步”  。

10. 在“分配”中，选择将接收配置文件的用户或组  。 有关分配配置文件的详细信息，请参阅[分配用户和设备配置文件](device-profile-assign.md)。

    选择“下一步”  。

11. 在“查看并创建”中查看设置  。 选择“创建”时，将保存所做的更改并分配配置文件  。 该策略也会显示在配置文件列表中。

## <a name="example"></a>示例

下面的示例中启用了 Connectivity/AllowVPNOverCellular 设置  。 此设置可允许 Windows 10 设备在处于移动电话网络中时打开 VPN 连接。

> [!div class="mx-imgBorder"]
> ![Intune 和 Endpoint Manager 中包含 VPN 设置的自定义策略的示例](./media/custom-settings-configure/custom-policy-example.png)

## <a name="next-steps"></a>后续步骤

此时，配置文件创建完成，但它可能尚未执行任何操作。 下一步，[分配配置文件](device-profile-assign.md)并[监视其状态](device-profile-monitor.md)。
