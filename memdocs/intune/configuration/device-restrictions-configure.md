---
title: 在 Microsoft Intune 中使用策略限制设备功能 - Azure | Microsoft Docs
description: 在 Microsoft Intune 中添加设备配置文件以限制 Android 设备管理员、Android Enterprise、macOS、iOS、iPadOS、Windows Phone 和 Windows 10 设备上的功能。
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
ms.openlocfilehash: 470ca47aa92b30acacc8a251c6d7d1741513bdf1
ms.sourcegitcommit: 7687cf8fdecd225216f58b8113ad07a24e43d4a3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2020
ms.locfileid: "80359218"
---
# <a name="configure-device-restriction-settings-in-microsoft-intune"></a>在 Microsoft Intune 中配置设备限制设置

Intune 包含设备限制策略，有助于管理员控制 Android、iOS/iPadOS、macOS 和 Windows 设备。 这些限制允许控制各种设置和功能，以保护组织的资源。 例如，管理员可以：

- 允许或阻止设备照相机。
- 控制对 Google Play、应用商店、查看文档和游戏的访问。
- 阻止内置应用，或创建允许或禁止的应用列表。
- 允许或阻止将文件备份到云和存储帐户。
- 设置最小密码长度和阻止简单密码。

这些功能在 Intune 中可用，并可供管理员进行配置。 Intune 使用“配置文件”创建和自定义这些设置，从而满足组织需求。 在配置文件中添加这些功能后，就可以将配置文件推送或部署到组织中的设备上。

本文介绍了如何创建设备限制配置文件。 还可以查看所有适用于不同平台的可用设置。

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
        - **Windows 8.1 及更高版本**
        - **Windows Phone 8.1**

    - **配置文件**：选择“设备限制”  。

        若要为 Windows 10 协同版设备（如 Surface Hub）创建设备限制配置文件，请选择“设备限制(Windows 10 协同版)”  。

4. 选择“创建”。 
5. 在“基本信息”  中，输入以下属性：

    - **名称**：输入策略的描述性名称。 为策略命名，以便稍后可以轻松地识别它们。 例如，策略名称最好是“iOS/iPadOS：阻止设备上的照相机”：  。
    - **描述**：输入策略的说明。 此设置是可选的，但建议进行。

6. 选择“下一步”  。

7. 在“配置设置”  中，根据所选择的平台，可配置的设置有所不同。 选择平台，以了解详细设置：

    - [Android 设备管理员](device-restrictions-android.md)
    - [Android Enterprise](device-restrictions-android-for-work.md)
    - [iOS/iPadOS](device-restrictions-ios.md)
    - [macOS](device-restrictions-macos.md)
    - [Windows Phone 8.1](device-restrictions-windows-phone-8-1.md)
    - [Windows 8.1](device-restrictions-windows-8-1.md)
    - [Windows 10 及更高版本](device-restrictions-windows-10.md)
    - [Windows 10 协同版](device-restrictions-windows-10-teams.md)
    - [Windows Holographic for Business](device-restrictions-windows-holographic.md)

8. 选择“下一步”  。
9. 在“作用域标记”（可选）中，分配一个标记以将配置文件筛选到特定 IT 组（如 `US-NC IT Team` 或 `JohnGlenn_ITDepartment`）  。 有关范围标记的详细信息，请参阅[将 RBAC 和范围标记用于分布式 IT](../fundamentals/scope-tags.md)。

    选择“下一步”  。

10. 在“分配”中，选择将接收配置文件的用户或组  。 有关分配配置文件的详细信息，请参阅[分配用户和设备配置文件](device-profile-assign.md)。

    选择“下一步”  。

11. 在“查看并创建”中查看设置  。 选择“创建”时，将保存所做的更改并分配配置文件  。 该策略也会显示在配置文件列表中。

## <a name="next-steps"></a>后续步骤

创建配置文件后，即可进行分配。 下一步，[分配配置文件](device-profile-assign.md)并[监视其状态](device-profile-monitor.md)。

<!--  Removing image as part of design review; retaining source until we known the disposition.

## Example of device restriction settings

In this high-level example, you'll create a device restriction policy that blocks the use of the built-in camera app on Android devices.

![How to disable the camera on Android devices](./media/device-restrictions-configure/disable-android-camera.png)

-->
