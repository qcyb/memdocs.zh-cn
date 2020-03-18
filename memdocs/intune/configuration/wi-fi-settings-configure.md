---
title: 在 Microsoft Intune 中为设备创建 Wi-Fi 配置文件 - Azure | Microsoft Docs
description: 请参阅具体步骤以在 Microsoft Intune 中创建 Wi-Fi 设备配置文件。 创建适用于 Android、Android Enterprise、Android 展台、iOS、iPadOS、macOS、Windows 10 及更高版本以及 Windows Holographic for Business 的配置文件。 使用这些配置文件创建 WiFi 连接以使用证书、选择 EAP 类型、选择身份验证方法和启用代理等。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/18/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5297f87dd3aad6b88281b491ccb7c1f0878ffc1e
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79343123"
---
# <a name="add-and-use-wi-fi-settings-on-your-devices-in-microsoft-intune"></a>在 Microsoft Intune 中添加和使用设备上的 Wi-Fi 设置

Wi-Fi 是许多移动设备用来实现网络访问的无线网络。 Microsoft Intune 包括内置 Wi-Fi 设置，可部署到组织中的用户和组织。 此组设置称为“配置文件”，可以分配到不同的用户和组。 分配后，用户有权访问组织的 Wi-Fi 网络，而无需自行配置。

例如，安装名为“Contoso Wi-Fi”的新 Wi-Fi 网络。 然后你要将所有 iOS/iPadOS 设备设置为连接到此网络。 过程如下：

1. 创建 Wi-Fi 配置文件，其中包含用于连接到 Contoso Wi-Fi 无线网络的设置。
2. 将配置文件分配到包含所有 iOS/iPadOS 设备用户的组。
3. 用户在其设备上的无线网络列表中找到新的 Contoso Wi-Fi 网络。 然后，他们可以使用所选的身份验证方法连接到该网络。

本文列出了创建 Wi-Fi 配置文件的步骤。 它还收录了介绍每个平台的不同设置的链接。

## <a name="supported-device-platforms"></a>受支持的设备平台

Wi-Fi 配置文件支持以下设备平台：

- Android 4 及更高版本
- Android Enterprise 和展台
- iOS 8.0 及更高版本
- iPadOS 13.0 及更高版本
- macOS X 10.11 及更高版本
- Windows 10 及更高版本、Windows 10 移动版和 Windows Holographic for Business

> [!NOTE]
> 对于运行 Windows 8.1 的设备，你可以导入之前从另一台设备导出的 Wi-Fi 配置。

## <a name="create-a-device-profile"></a>创建设备配置文件

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“设备”   > “配置文件”   > “创建配置文件”  。
3. 输入以下属性：

    - **名称**：输入配置文件的描述性名称。 为配置文件命名，以便稍后可以轻松地识别它们。 例如，配置文件名称最好是“整个公司的 WiFi 配置文件”  。
    - **描述**：输入配置文件的说明。 此设置是可选的，但建议进行。
    - **平台**：选择设备平台。 选项包括：

      - **Android**
      - **Android Enterprise**
      - **iOS/iPadOS**
      - **macOS**
      - **Windows 8.1 及更高版本**
      - **Windows 10 及更高版本**

    - **配置文件类型**：选择“Wi-Fi”  。

      > [!TIP]
      >
      > - 对于作为专用设备（展台）运行的 Android Enterprise  设备，依次选择“仅设备所有者”   > “Wi-Fi”  。
      > - 对于 Windows 8.1 及更高版本  ，可以选择“Wi-Fi 导入”  。 此选项允许你以之前从其他设备导出的 XML 文件形式导入 Wi-Fi 设置。

4. 某些 Wi-Fi 设置针对每个平台会有所不同。 若要查看特定平台的设置，请选择你的平台：

    - [Android](wi-fi-settings-android.md)
    - [Android Enterprise](wi-fi-settings-android-enterprise.md)（包括专用设备）
    - [iOS/iPadOS](wi-fi-settings-ios.md)
    - [macOS](wi-fi-settings-macos.md)
    - [Windows 10 及更高版本](wi-fi-settings-windows.md)
    - [Windows 8.1 及更高版本](wi-fi-settings-import-windows-8-1.md)，包括 Windows Holographic for Business

5. 完成后，依次选择“创建配置文件”   > “创建”  。

此时，配置文件创建，并显示在配置文件列表中（“设备配置”   > “配置文件”  ）。

## <a name="next-steps"></a>后续步骤

配置文件已创建，但未执行任何操作。 下一步是[分配此配置文件](device-profile-assign.md)，并[监视配置文件状态](device-profile-monitor.md)。

[Intune 中的 Wi-Fi 配置文件有问题](troubleshoot-wi-fi-profiles.md)。
