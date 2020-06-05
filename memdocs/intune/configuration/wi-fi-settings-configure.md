---
title: 在 Microsoft Intune 中为设备创建 Wi-Fi 配置文件 - Azure | Microsoft Docs
description: 请参阅具体步骤以在 Microsoft Intune 中创建 Wi-Fi 设备配置文件。 创建适用于 Android 设备管理员、Android Enterprise、Android 展台、iOS、iPadOS、macOS、Windows 10 及更高版本以及 Windows Holographic for Business 的配置文件。 使用这些配置文件创建 WiFi 连接以使用证书、选择 EAP 类型、选择身份验证方法和启用代理等。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/19/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: maholdaa
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ca2a5ddd3d2b4c0aa93c7c955d0d688944ee8f95
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/27/2020
ms.locfileid: "83985497"
---
# <a name="add-and-use-wi-fi-settings-on-your-devices-in-microsoft-intune"></a>在 Microsoft Intune 中添加和使用设备上的 Wi-Fi 设置

Wi-Fi 是许多移动设备用来实现网络访问的无线网络。 Microsoft Intune 包括内置 Wi-Fi 设置，可部署到组织中的用户和组织。 此组设置称为“配置文件”，可以分配到不同的用户和组。 分配后，用户有权访问组织的 Wi-Fi 网络，而无需自行配置。

例如，安装名为“Contoso Wi-Fi”的新 Wi-Fi 网络。 然后你要将所有 iOS/iPadOS 设备设置为连接到此网络。 过程如下：

1. 创建 Wi-Fi 配置文件，其中包含用于连接到 Contoso Wi-Fi 无线网络的设置。
2. 将配置文件分配到包含所有 iOS/iPadOS 设备用户的组。
3. 在其设备上，用户在无线网络列表中找到新的 Contoso Wi-Fi 网络。 然后，他们可以使用所选的身份验证方法连接到该网络。

本文列出了创建 Wi-Fi 配置文件的步骤。 它还收录了介绍每个平台的不同设置的链接。

## <a name="supported-device-platforms"></a>受支持的设备平台

Wi-Fi 配置文件支持以下设备平台：

- Android 5 及更高版本
- Android Enterprise 和展台
- iOS 11.0 及更高版本
- iPadOS 13.0 及更高版本
- macOS X 10.12 及更高版本
- Windows 10 及更高版本、Windows 10 移动版和 Windows Holographic for Business

> [!NOTE]
> 对于运行 Windows 8.1 的设备，你可以导入之前从另一台设备导出的 Wi-Fi 配置。

## <a name="create-the-profile"></a>创建配置文件

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“设备” > “配置文件” > “创建配置文件”。
3. 输入以下属性：

    - **平台**：选择设备平台。 选项包括：

      - **Android 设备管理员**
      - **Android Enterprise**
      - **iOS/iPadOS**
      - **macOS**
      - **Windows 10 及更高版本**
      - **Windows 8.1 及更高版本**

    - **配置文件**：选择“Wi-Fi”。

      > [!TIP]
      >
      > - 对于作为专用设备（展台）运行的 Android Enterprise 设备，依次选择“仅设备所有者” > “Wi-Fi”。
      > - 对于 Windows 8.1 及更高版本，可以选择“Wi-Fi 导入” 。 此选项允许你以之前从其他设备导出的 XML 文件形式导入 Wi-Fi 设置。

4. 选择“创建”。
5. 在“基本信息”中，输入以下属性：

    - **名称**：输入配置文件的描述性名称。 为配置文件命名，以便稍后可以轻松地识别它们。 例如，配置文件名称最好是“整个公司的 WiFi 配置文件”。
    - **描述**：输入配置文件的说明。 此设置是可选的，但建议进行。

6. 选择“下一步”。
7. 在“配置设置”中，根据所选择的平台，可配置的设置有所不同。 选择平台，进行详细设置：

    - [Android 设备管理员](wi-fi-settings-android.md)
    - [Android Enterprise](wi-fi-settings-android-enterprise.md)（包括专用设备）
    - [iOS/iPadOS](wi-fi-settings-ios.md)
    - [macOS](wi-fi-settings-macos.md)
    - [Windows 10 及更高版本](wi-fi-settings-windows.md)
    - [Windows 8.1 及更高版本](wi-fi-settings-import-windows-8-1.md)，包括 Windows Holographic for Business

8. 选择“下一步”。
9. 在“作用域标记”（可选）中，分配一个标记以将配置文件筛选到特定 IT 组（如 `US-NC IT Team` 或 `JohnGlenn_ITDepartment`）。 有关范围标记的详细信息，请参阅[将 RBAC 和范围标记用于分布式 IT](../fundamentals/scope-tags.md)。

    选择“下一步”。

10. 在“分配”中，选择将接收配置文件的用户或组。 有关分配配置文件的详细信息，请参阅[分配用户和设备配置文件](device-profile-assign.md)。

    选择“下一步”。

11. 在“查看并创建”中查看设置。 选择“创建”时，将保存所做的更改并分配配置文件。 该策略也会显示在配置文件列表中。

> [!TIP]
> 如果对 Wi-Fi 配置文件使用基于证书的身份验证，请将 Wi-Fi 配置文件、证书配置文件和受信任的根配置文件部署到同一组，以确保每台设备都能识别证书颁发机构的合法性。  有关详细信息，请参阅[如何使用 Microsoft Intune 配置证书](../protect/certificates-configure.md)。


## <a name="next-steps"></a>后续步骤

配置文件已创建，但未执行任何操作。 下一步是[分配此配置文件](device-profile-assign.md)，并[监视配置文件状态](device-profile-monitor.md)。

[Intune 中的 Wi-Fi 配置文件有问题](troubleshoot-wi-fi-profiles.md)。
