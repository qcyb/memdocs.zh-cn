---
title: 在 Microsoft Intune 中向 macOS 设备添加自定义设置 - Azure | Microsoft Docs
titleSuffix: ''
description: 从 Apple Configurator 或 Apple 配置文件管理器工具导出 macOS 设置，然后将这些设置导入 Microsoft Intune。 这些设置可以创建、使用和控制 macOS 设备上的自定义设置和功能。 之后，可以将此自定义配置文件分配或分发到组织中的 macOS 设备，以创建基线或标准。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/04/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: kakyker
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: e92315377a839a537dfc4c2da00d282d2cddf58f
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429089"
---
# <a name="use-custom-settings-for-macos-devices-in-microsoft-intune"></a>在 Microsoft Intune 中使用适用于 macOS 设备的自定义设置

借助 Microsoft Intune，可以使用“自定义配置文件”添加或创建适用于 macOS 设备的自定义设置。 自定义配置文件是 Intune 中的一项功能。 这项功能用于添加未内置到 Intune 的设备设置和功能。

使用 macOS 设备时，可以通过两种方法将自定义设置引入 Intune：

- [Apple Configurator](https://itunes.apple.com/app/apple-configurator-2/id1037126344?mt=12)
- [Apple 配置文件管理器](https://support.apple.com/profile-manager)

这些工具可用于将设置导出到配置文件。 在 Intune 中，导入此文件，然后将该配置文件分配给 macOS 用户和设备。 分配后，将分配设置。 它们还为组织中的 macOS 创建基准或标准。

本文提供了有关使用 Apple Configurator 和 Apple 配置文件管理器的一些指导，并介绍了可配置的属性。

## <a name="before-you-begin"></a>在开始之前

[创建 macOS 自定义配置文件](custom-settings-configure.md)。

## <a name="what-you-need-to-know"></a>须知内容

- 使用 Apple 配置器创建配置文件时，请确保导出的设置与设备上的 macOS 版本兼容。 有关如何解决不兼容设置的信息，请在 [Apple 开发人员](https://developer.apple.com/)网站上搜索“配置文件参考”和“移动设备管理协议参考” 。

- 使用 Apple 配置文件管理器时，请务必：

  - 在配置文件管理器中启用[移动设备管理](https://help.apple.com/serverapp/mac/5.7/#/apd05B9B761-D390-4A75-9251-E9AD29A61D0C)。
  - 在配置文件管理器中添加 [macOS 设备](https://help.apple.com/profilemanager/mac/5.7/#/pm9onzap1984)。
  - 在配置文件管理器中添加设备后，转到“在库之下” > “设备”>“选择设备”>“设置”  。 输入设备的常规、安全性、隐私、目录和证书设置。

    下载并保存此文件。 需在 Intune 配置文件中输入此文件。 

  - 请确保从 Apple 配置文件管理器导出的设置与设备上的 macOS 版本兼容。 有关如何解决不兼容设置的信息，请在 [Apple 开发人员](https://developer.apple.com/)网站上搜索“配置文件参考”和“移动设备管理协议参考” 。

## <a name="custom-configuration-profile-settings"></a>自定义配置文件设置

- **配置文件名称**：输入策略的名称。 此名称将在设备上和 Intune 状态中显示。
- **配置的配置文件**：浏览到使用 Apple Configurator 或 Apple 配置文件管理器创建的 `.xml` 或 `.mobileconfig` 文件。 文件最大为 1000000 字节（不到 1 MB）。 将显示导入的文件。 添加文件后，也可以删除文件。

  还可以将设备令牌添加到 `.mobileconfig` 文件中。 设备令牌用于添加特定于设备的信息。 例如，若要显示序列号，请输入 `{{serialnumber}}`。 在设备上，显示的文本类似于每个设备的唯一 `123456789ABC`。 输入变量时，请务必使用大括号 `{{ }}`。 [应用配置令牌](../apps/app-configuration-policies-use-ios.md#tokens-used-in-the-property-list)包含可用变量的列表。 还可以使用 `deviceid` 或任何其他特定于设备的值。

  > [!NOTE]
  > 变量不在 UI 中进行验证，且区分大小写。 因此，可能会看到使用不正确输入保存的配置文件。 例如，如果输入 `{{DeviceID}}` 而不是 `{{deviceid}}`，则显示文本字符串而不是设备的唯一 ID。 请确保输入正确的信息。

## <a name="next-steps"></a>后续步骤

[分配配置文件](device-profile-assign.md)并[监视其状态](device-profile-monitor.md)。

[在 iOS/iPadOS 设备上创建自定义配置文件](custom-settings-ios.md)。
