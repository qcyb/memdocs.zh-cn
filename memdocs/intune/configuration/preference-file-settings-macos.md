---
title: 在 Microsoft Intune 中向 macOS 设备添加首选项文件设置 - Azure | Microsoft Docs
titleSuffix: ''
description: 添加包含有关应用的密钥信息的 xml 或 plist 文件。 使用首选项文件设备配置文件更改属性列表文件中的密钥信息，并将其分配给 macOS 设备。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/09/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d226888c3d710a7b80357ebb92130b34ab2fef94
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79360751"
---
# <a name="add-a-property-list-file-to-macos-devices-using-microsoft-intune"></a>使用 Microsoft Intune 将属性列表文件添加到 macOS 设备

使用 Microsoft Intune，可以为 macOS 设备或 macOS 设备上的应用添加属性列表文件 (.plist)。

此功能适用于：

- 运行 10.7 及更高版本的 macOS 设备

属性列表文件通常包含有关 macOS 应用程序的信息。 有关详细信息，请参阅[关于信息属性列表文件](https://developer.apple.com/library/archive/documentation/General/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html)（Apple 网站）和[自定义有效负载设置](https://support.apple.com/guide/mdm/custom-mdm9abbdbe7/1/web/1)。

本文列出并介绍了可以添加到 macOS 设备的不同属性列表文件设置。 作为移动设备管理 (MDM) 解决方案的一部分，请使用这些设置添加应用程序包 ID (`com.company.application`) 及其 .plist 文件。

我们将这些设置添加到 Intune 中的设备配置配置文件中，然后分配或部署到 macOS 设备。

## <a name="before-you-begin"></a>在开始之前

[创建配置文件](device-profile-create.md)。

## <a name="what-you-need-to-know"></a>须知内容

- 这些设置未验证。 在将配置文件分配给设备之前，请务必测试你的更改。
- 如果不确定如何输入应用密钥，请在应用中更改设置。 然后，使用 [Xcode](https://developer.apple.com/xcode/) 查看应用的首选项文件，了解设置的配置方式。 Apple 建议在导入文件前使用 Xcode 删除不可管理的设置。
- 只有某些应用使用托管首选项，并且可能不允许管理所有设置。
- 请确保上传的属性列表文件的目标是设备通道设置，而非用户通道设置。 属性列表文件以整个设备为目标。

## <a name="preference-file"></a>首选项文件

- **首选项域名**：属性列表文件通常用于 Web 浏览器 (Microsoft Edge)、[Microsoft Defender 高级威胁防护](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac)和自定义应用。 创建首选项域时，还会创建一个程序包 ID。 输入该程序包 ID，例如 `com.company.application`。 例如，输入 `com.Contoso.applicationName`、`com.Microsoft.Edge` 或 `com.microsoft.wdav`。
- **属性列表文件**：选择与应用关联的属性列表文件。 请确保它是 `.plist` 或 `.xml` 文件。 例如上传 `YourApp-Manifest.plist` 或 `YourApp-Manifest.xml` 文件。
- **文件内容**：显示属性列表文件中的密钥信息。 如果需要更改密钥信息，请在另一个编辑器中打开列表文件，然后在 Intune 中重新上传文件。

请确保文件的格式正确。 文件应仅具有键值对，并且不应包装在 `<dict>``<plist>` 或 `<xml>` 标记中。 例如，属性列表文件应类似于以下文件：

```xml
<key>SomeKey</key>
<string>someString</string>
<key>AnotherKey</key>
<false/>
...
```

选择“确定”   > “创建”  以保存所做的更改。 此时，配置文件创建完成，并出现在配置文件列表中。

## <a name="next-steps"></a>后续步骤

配置文件已创建，但它尚未起到任何作用。 下一步，[分配配置文件](device-profile-assign.md)并[监视其状态](device-profile-monitor.md)。

有关 Microsoft Edge 首选项文件的详细信息，请参阅[配置 macOS 上的 Microsoft Edge 策略设置](https://docs.microsoft.com/deployedge/configure-microsoft-edge-on-mac)。
