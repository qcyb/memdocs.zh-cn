---
title: 在 Microsoft Intune 中创建设备配置文件 - Azure | Microsoft Docs
description: 在 Microsoft Intune 中添加或配置设备配置文件。 选择平台类型，配置设置并添加作用域标记。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/11/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d98aceff-eb35-4e3e-8e40-5f300e7335cc
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 886f572212a1af3e38fd5ea10afa21ce24c23411
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2020
ms.locfileid: "85093299"
---
# <a name="create-a-device-profile-in-microsoft-intune"></a>在 Microsoft Intune 中创建设备配置文件

使用设备配置文件，可以添加和配置设置，然后将这些设置推送到组织中的设备。 有关更多详细信息（包括可以执行的操作），请参阅[对使用设备配置文件的设备应用功能和设置](device-profiles.md)。

本文：

- 列出创建配置文件的步骤。
- 演示如何添加作用域标记以“筛选”配置文件。
- 描述 Windows 10 设备上的适用性规则，并演示如何创建规则。
- 列出设备接收配置文件和任何配置文件更新时的签入刷新周期时间。

## <a name="create-the-profile"></a>创建配置文件

在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)创建配置文件。 在此管理中心中，选择“设备”。 有下列选项：

- **概述**：列出配置文件的状态，并提供有关分配给用户和设备的配置文件的其他详细信息。
- **监视**：检查配置文件的状态（成功或失败），并查看配置文件中的日志。
- 按平台：创建并查看按平台列出的策略和配置文件。 此视图还可能会显示特定于平台的功能。 例如，选择“Windows”。 你将看到特定于 Windows 的功能，如 Windows 10 更新通道和 PowerShell 脚本 。
- **策略**：创建设备配置文件，并上传自定义 [PowerShell 脚本](../apps/intune-management-extension.md)以在设备上运行，然后使用 [eSIM](esim-device-configuration.md) 向设备添加数据计划。

创建配置文件（“配置文件” > “创建配置文件” ）时，请选择平台：

- **Android 设备管理员**
- **Android Enterprise**
- **iOS/iPadOS**
- **macOS**
- **Windows 10 及更高版本**
- **Windows 8.1 及更高版本**
- **Windows Phone 8.1**

然后选择配置文件类型。 根据所选择的平台，可配置的设置有所不同。 以下文章介绍了不同配置文件类型的设置：

- [管理模板 (Windows)](administrative-templates-windows.md)
- [自定义](custom-settings-configure.md)
- [传递优化 (Windows)](delivery-optimization-windows.md)
- [派生凭据（Android Enterprise、iOS、iPadOS）](../protect/derived-credentials.md)
- [设备功能（macOS、iOS、iPadOS）](device-features-configure.md)
- [设备固件 (Windows)](device-firmware-configuration-interface-windows.md)
- [设备限制](device-restrictions-configure.md)
- [域加入 (Windows)](domain-join-configure.md)
- [版本升级和模式切换 (Windows)](edition-upgrade-configure-windows-10.md)
- [教育（iOS、iPadOS）](../fundamentals/education-settings-configure-ios.md)
- [Email](email-settings-configure.md)
- [Endpoint Protection（macOS、Windows）](../protect/endpoint-protection-configure.md)
- [扩展 (macOS)](kernel-extensions-overview-macos.md)
- [标识保护 (Windows)](../protect/identity-protection-configure.md)
- [展台](kiosk-settings.md)
- [Microsoft Defender ATP (Windows)](../protect/advanced-threat-protection.md)
- [移动扩展 (MX) 配置文件（Android 设备管理员）](android-zebra-mx-overview.md)
- [OEMConfig (Android Enterprise)](android-oem-configuration-overview.md)
- [PKCS 证书](../protect/certficates-pfx-configure.md)
- [PKCS 导入的证书](../protect/certificates-imported-pfx-configure.md)
- [首选项文件 (macOS)](preference-file-settings-macos.md)
- [SCEP 证书](../protect/certificates-scep-configure.md)
- [安全评估（教育）(Windows)](education-settings-configure.md)
- [共享的多用户设备 (Windows)](shared-user-device-settings.md)
- [电信费用（Android 设备管理员、iOS、iPadOS）](telecom-expenses-monitor.md)
- [受信任的证书](../protect/certificates-configure.md)
- [VPN](vpn-settings-configure.md)
- [Wi-Fi](wi-fi-settings-configure.md)
- [有线网络 (macOS)](wired-network-settings-macos.md)

例如，如果选择“iOS/iPadOS”作为平台，配置文件选项将类似于以下配置文件：

:::image type="content" source="./media/device-profile-create/create-device-profile.png" alt-text="在 Microsoft Intune 中创建 iOS/iPadOS 配置文件。":::

## <a name="scope-tags"></a>作用域标记

添加设置后，还可以向配置文件添加作用域标记。 “作用域标记”将配置文件筛选到特定 IT 组（例如 `US-NC IT Team` 或 `JohnGlenn_ITDepartment`）。 并且用于分布式 IT。

若要详细了解作用域标记以及可以执行的操作，请参阅[将 RBAC 和作用域标记用于分布式 IT](../fundamentals/scope-tags.md)。

## <a name="applicability-rules"></a>适用性规则

适用于：

- Windows 10 及更高版本

适用性规则允许管理员针对满足特定条件的组中的设备。 例如，你创建了一个适用于所有 Windows 10 设备组的设备限制配置文件。 接下来，只需将配置文件分配给运行 Windows 10 企业版的设备。

若要执行此任务，请创建适用性规则。 这些规则对于以下情况非常有用：

- 你使用 Windows 10 教育版 (EDU)。 在毕罗思大学，你希望针对 RS3 和 RS4 之间的所有 Windows 10 EDU 设备。
- 你希望针对 Contoso 人力资源的所有用户，但只需要 Windows 10 专业版或企业版设备。

若要实现这些方案，你需要：

- 创建包括毕罗思大学的所有设备的设备组。 在配置文件中，添加一个在操作系统最低版本为 `16299`、最大版本为 `17134` 时应用的适用性规则。 将此配置文件分配给毕罗思大学设备组。

  分配该配置文件后，该配置文件将应用于输入的最低和最高版本之间的设备。 对于不在输入的最低和最高版本之间的设备，其状态显示为“不适用”。

- 创建一个用户组，该用户组包括 Contoso 的人力资源 (HR) 中的所有用户。 在配置文件中，添加一个适用性规则，使其适用于运行 Windows 10 专业版或企业版的设备。 将此配置文件分配给 HR 用户组。

  分配该配置文件后，该配置文件将应用于运行 Windows 10 专业版或企业版的设备。 对于未运行这些版本的设备，其状态显示为“不适用”。

- 如果有两个配置文件具有完全相同的设置，则会应用没有适用性规则的配置文件。 

  例如，ProfileA 针对 Windows 10 设备组，它启用 BitLocker，并且没有适用性规则。 ProfileB 针对相同的 Windows 10 设备组，它启用 BitLocker，并且具有仅将配置文件应用于 Windows 10 企业版的适用性规则。

  如果同时分配了两个配置文件，则会应用 ProfileA，因为它没有适用性规则。 

将配置文件分配给组时，适用性规则充当筛选器，仅针对满足条件的设备。

### <a name="add-a-rule"></a>添加规则

1. 选择“适用性规则”。 你可以选择“规则”和“属性” ：

    :::image type="content" source="./media/device-profile-create/applicability-rules.png" alt-text="在 Microsoft Intune 中向 Windows 10 设备配置文件添加适用性规则。":::

2. 在“规则”中，选择是否要包括或排除用户或组。 选项包括：

    - **在以下情况下分配配置文件**：包括满足你输入的条件的用户或组。
    - **在以下情况下不分配配置文件**：排除满足你输入的条件的用户或组。

3. 在“属性”中，选择筛选器。 选项包括： 

    - **OS 版本**：在列表中，选中要在规则中包括（或排除）的 Windows 10 版本。
    - **OS 版本**：输入要在规则中包括（或排除）的最小和最大 Windows 10 版本号 。 两个值都是必需的。

      例如，对于最低版本，可以输入 `10.0.16299.0`（RS3 或 1709），对于最高版本，可以输入 `10.0.17134.0`（RS4 或 1803）。 或者，可以更精细地输入 `10.0.16299.001` 表示最低版本，`10.0.17134.319` 表示最高版本。

4. 选择“添加”，保存所做更改。

## <a name="refresh-cycle-times"></a>刷新周期时间

Intune 使用不同的刷新周期来检查配置文件的更新。 如果设备是最近注册的，则会增加运行签入的频率。 [策略和配置文件刷新周期](device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned)列出了估计的刷新时间。

用户可以随时打开公司门户应用，并同步设备以立即检查配置文件更新。

## <a name="recommendations"></a>建议

创建配置文件时，请考虑下列建议：

- 命名策略，以便了解其定义和用途。 所有[符合性策略](../protect/create-compliance-policy.md)和[配置文件](../configuration/device-profile-create.md)都有一个可选的“说明”属性。 在“说明”中，具体明确并包含信息，使其他人知道策略的用途。

  某些配置文件示例包括：

  **配置文件名称**：管理模板 - 适用于所有 Windows 10 用户的 OneDrive 配置文件  
  **配置文件说明**：OneDrive 管理模板配置文件，其中包括适用于所有 Windows 10 用户的最小和基本设置。 由 user@contoso.com 创建，可防止用户将组织数据共享到个人 OneDrive 帐户。

  **配置文件名称**：适用于所有 iOS/iPadOS 用户的 VPN 配置文件  
  **配置文件说明**：VPN 配置文件，其中包括适用于要连接到 Contoso VPN 的所有 iOS/iPadOS 用户的最小和基本设置。 由 user@contoso.com 创建，以便用户自动向 VPN 进行身份验证，而不是提示用户输入其用户名和密码。

- 按照任务创建配置文件，例如配置 Microsoft Edge 设置、启用 Microsoft Defender 防病毒设置、阻止 iOS/iPadOS 越狱设备等。

- 创建适用于特定组（如市场营销、销售、IT 管理员）的配置文件，或按位置或学校系统创建配置文件。

- 将用户策略与设备策略分开。

  例如，[Intune 中的管理模板](administrative-templates-windows.md)具有数千个 ADMX 设置。 这些模板将显示是否将设置应用于用户或设备。 创建管理模板时，将用户设置分配给用户组，并将设备设置分配给设备组。

  下图显示了可应用于用户和/或应用于设备的设置示例：

  :::image type="content" source="./media/device-profile-create/setting-applies-to-user-and-device.png" alt-text="适用于用户和设备的 Intune 管理模板。":::

- 每次创建限制性策略时，请将此更改传达给用户。 例如，如果要将密码要求从四 (4) 个字符更改为六 (6) 个字符，请在分配策略之前告知用户。

## <a name="next-steps"></a>后续步骤

[分配配置文件](device-profile-assign.md)并[监视其状态](device-profile-monitor.md)。
