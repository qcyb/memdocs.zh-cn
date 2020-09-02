---
title: 在 Microsoft Intune 中向 macOS 设备添加首选项文件设置 - Azure | Microsoft Docs
titleSuffix: ''
description: 添加包含有关应用的密钥信息的 xml 或 plist 文件。 使用首选项文件设备配置文件更改属性列表文件中的密钥信息，并将其分配给 macOS 设备。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/05/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 478cce186d5f2943aeb5730acf90c3e875c8b687
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915307"
---
# <a name="add-a-property-list-file-to-macos-devices-using-microsoft-intune"></a>使用 Microsoft Intune 将属性列表文件添加到 macOS 设备

使用 Microsoft Intune，可以为 macOS 设备或 macOS 设备上的应用添加属性列表文件 (.plist)。

此功能适用于：

- macOS 10.7 及更高版本

属性列表文件包含有关 macOS 应用程序的信息。 有关详细信息，请参阅[关于信息属性列表文件](https://developer.apple.com/library/archive/documentation/General/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html)（Apple 网站）和[自定义有效负载设置](https://support.apple.com/guide/mdm/custom-mdm9abbdbe7/1/web/1)。

本文列出并介绍了可以添加到 macOS 设备的不同属性列表文件设置。 作为移动设备管理 (MDM) 解决方案的一部分，请使用这些设置添加应用程序包 ID (`com.company.application`) 及应用的 .plist 文件。

我们将这些设置添加到 Intune 中的设备配置配置文件中，然后分配或部署到 macOS 设备。

## <a name="what-you-need-to-know"></a>须知内容

- 这些设置未验证。 在将配置文件分配给设备之前，请务必测试你的更改。
- 如果不确定如何输入应用密钥，请在应用中更改设置。 然后，使用 [Xcode](https://developer.apple.com/xcode/) 查看应用的首选项文件，了解设置的配置方式。 Apple 建议在导入文件前使用 Xcode 删除不可管理的设置。
- 只有某些应用使用托管首选项，并且可能不允许管理所有设置。
- 请确保上传的属性列表文件的目标是设备通道设置，而非用户通道设置。 属性列表文件以整个设备为目标。

## <a name="create-the-profile"></a>创建配置文件

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“设备” > “配置文件” > “创建配置文件”。
3. 输入以下属性：

    - **平台**：选择“macOS”
    - **配置文件**：选择“首选项文件”。

4. 选择“创建”。
5. 在“基本信息”中，输入以下属性：

    - **名称**：输入策略的描述性名称。 为策略命名，以便稍后可以轻松地识别它们。 例如，策略名称最好是“macOS：配置登录屏幕”**添加在设备上配置 Microsoft Defender ATP 的首选项文件**。
    - **描述**：输入策略的说明。 此设置是可选的，但建议进行。

6. 选择“下一步”。

7. 在“配置设置”中，配置以下设置：

    - **首选项域名**：输入该程序包 ID，例如 `com.company.application`。 例如，输入 `com.Contoso.applicationName`、`com.Microsoft.Edge` 或 `com.microsoft.wdav`。

      属性列表文件通常用于 Web 浏览器 (Microsoft Edge)、[Microsoft Defender 高级威胁防护](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac)和自定义应用。 创建首选项域时，还会创建一个程序包 ID。

    - **属性列表文件**：选择与应用关联的属性列表文件。 请确保它是 `.plist` 或 `.xml` 文件。 例如上传 `YourApp-Manifest.plist` 或 `YourApp-Manifest.xml` 文件。

      显示属性列表文件中的密钥信息。 如果需要更改密钥信息，请在另一个编辑器中打开列表文件，然后在 Intune 中重新上传文件。

    请确保文件的格式正确。 文件应仅具有键值对，并且不应包装在 `<dict>``<plist>` 或 `<xml>` 标记中。 例如，属性列表文件应类似于以下文件：

    ```xml
    <key>SomeKey</key>
    <string>someString</string>
    <key>AnotherKey</key>
    <false/>
    ...
    ```

8. 选择“下一步”。
9. 在“作用域标记”（可选）中，分配一个标记以将配置文件筛选到特定 IT 组（如 `US-NC IT Team` 或 `JohnGlenn_ITDepartment`）。 有关范围标记的详细信息，请参阅[将 RBAC 和范围标记用于分布式 IT](../fundamentals/scope-tags.md)。

    选择“下一步”。

10. 在“分配”中，选择将接收配置文件的用户或组。 有关分配配置文件的详细信息，请参阅[分配用户和设备配置文件](device-profile-assign.md)。

    选择“下一步”。

11. 在“查看并创建”中查看设置。 选择“创建”时，将保存所做的更改并分配配置文件。 该策略也会显示在配置文件列表中。

## <a name="next-steps"></a>后续步骤

[分配配置文件](device-profile-assign.md)并[监视其状态](device-profile-monitor.md)。

有关 Microsoft Edge 首选项文件的详细信息，请参阅[配置 macOS 上的 Microsoft Edge 策略设置](/deployedge/configure-microsoft-edge-on-mac)。