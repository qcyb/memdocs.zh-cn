---
title: Microsoft Intune 中的设备符合性策略 - Azure | Microsoft Docs
description: 开始使用符合性策略，包括 Microsoft Intune 的符合性策略设置和设备符合性策略。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/14/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0ae39f91c4daa67c40c42022f63137f0b23daf80
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88911057"
---
# <a name="use-compliance-policies-to-set-rules-for-devices-you-manage-with-intune"></a>通过符合性策略为使用 Intune 管理的设备设置规则

Intune 等移动设备管理 (MDM) 解决方案都要求用户和设备必须符合一些要求，从而帮助保护组织数据。 在 Intune 中，此功能称为“符合性策略”。

Intune 中的符合性策略：

- 定义用户和设备符合要求所必须满足的规则和设置。
- 包括适用于不合规设备的操作。 针对非符合性的操作可能会提醒用户注意不符合要求的情况，并保护不合规设备上的数据。
- 可与[条件访问结合使用](#integrate-with-conditional-access)，进而阻止不符合规则的用户和设备。

Intune 中的符合性策略由两部分组成：

- **符合性策略设置** - 租户范围的设置，类似于每台设备接收的内置符合性策略。 符合性策略设置会在 Intune 环境中设置符合性策略工作原理的基线，包括未收到任何设备符合性策略的设备是否符合要求。

- **设备符合性策略** - 平台特定的规则，可配置和部署到用户组或设备组。  这些规则定义了对设备的要求，例如最低操作系统或要求使用磁盘加密。 设备必须符合这些规则才能被视为合规。

与其他 Intune 策略一样，设备的符合性策略评估取决于设备向 Intune 签入的时间以及[策略和配置文件刷新周期](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned)。

## <a name="compliance-policy-settings"></a>合规性策略设置

符合性策略设置是租户范围的设置，用于确定 Intune 的符合性服务如何与设备交互。 这些设置不同于在设备符合性策略中配置的设置。

若要管理符合性策略设置，请登录 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，然后转到“终结点安全” > 设备符合性” > “符合性策略设置”  。

符合性策略设置包括以下设置：

- **将未分配到符合性策略的设备标记为**

  此设置确定 Intune 如何处理尚未分配有设备符合性策略的设备。 此设置具有两个值：
  - **符合**（默认）：此安全功能已关闭。 未收到设备符合性策略的设备被视为“符合”。
  - **不符合**：此安全功能已启用。 未收到设备符合性策略的设备被视为“不符合”。

  如果将条件访问与设备符合性策略结合使用，则建议你将此设置更改为“不符合”，确保仅确认为“符合”的设备可访问你的资源。

  如果最终用户因未分配有策略而不符合要求，[公司门户应用](../apps/company-portal-app.md)会显示“未分配符合性策略”。

- **增强型越狱检测**（仅适用于 iOS/iPadOS）

  此设置仅适用于以阻止越狱设备的设备符合性策略为目标的设备。  （请参阅 iOS/iPadOS 的[设备运行状况](compliance-policy-create-ios.md#device-health)设置。）

  此设置具有两个值：

  - **已禁用**（默认）：此安全功能已关闭。 此设置对接收阻止越狱设备的设备符合性策略的设备没有影响。
  - **启用**：此安全功能已启用。 接收设备符合性策略以阻止越狱设备的设备使用增强型越狱检测。

  在适用的 iOS/iPadOS 设备上启用时，设备：

  - 在操作系统级别启用定位服务。
  - 始终允许公司门户使用定位服务。
  - 使用定位服务在后台更频繁地触发越狱检测。 Intune 不会存储用户位置数据。

  增强型越狱检测在以下情况下运行评估：

  - 公司门户应用处于打开状态
  - 设备实际移动距离相当大，大约 500 米或更远。 Intune 不能保证每次明显的位置更改都能引发越狱检测检查，因为检查取决于设备当时的网络连接。

  在 iOS 13 及更高版本上，每次设备提示用户继续允许公司门户在后台使用其位置时，此功能都将要求用户选择“始终允许”。 如果用户不总是允许位置访问并配置了具有此设置的策略，则其设备将被标记为“不符合”。

- **符合性状态有效期(天)**

  指定设备必须成功报告其接收的所有符合性策略的时间段。 如果设备未能在有效期结束之前报告策略的符合性状态，则设备将被视为“不符合”。

  默认情况下，此时间段设置为 30 天。 你可将时间段配置为 1 到 120 天。

  可查看设备符合性和有效期设置等各种详细信息。 登录 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，然后转到“设备” > “监视” > “设置符合性”  。 此设置在“设置”列中的名称为“处于活动状态”。  要详细了解此视图及相关的符合性状态视图，请参阅[监视设备符合性](compliance-policy-monitor.md)。

## <a name="device-compliance-policies"></a>设备合规性策略

Intune 设备符合性策略：

- 定义用户和托管设备符合要求所必须满足的规则和设置。 规则示例包括要求设备运行最低操作系统版本、不越狱或取得 root 权限，以及不超过与 Intune 集成的威胁管理软件所指定的威胁级别。
- 支持适用于不满足符合性策略的设备的操作。 操作示例包括远程锁定，或者向设备用户发送电子邮件告知设备状态，便于他们进行修复。
- 部署给用户组中的用户或设备组中的设备。 将符合性策略部署给用户后，会检查该用户的所有设备是否符合要求。 在此方案中使用设备组有助于生成符合性报告。

如果使用条件访问，则条件访问策略可使用设备符合性结果来阻止不合规设备对资源的访问。

可在设备符合性策略中指定的可用设置取决于创建策略时选择的平台类型。 不同的设备平台支持不同的设置，每种平台类型都需要单独的策略。  

以下主题链接到专门介绍设备配置策略各个方面的文章。

- [**针对非符合性的操作**](actions-for-noncompliance.md) - 每个设备符合性策略都包含一个或多个针对非符合性的操作。 这些操作是应用于不符合策略中设置的条件的设备的规则。

  默认情况下，每个设备符合性策略都包含在设备不符合策略规则时将设备标记为“不符合”的操作。 然后，该策略将根据你为这些操作设置的计划，将已配置的针对非符合性的任何其他操作应用于设备。

  针对非符合性的操作有助于在用户设备不符合要求时提醒用户，或保护设备上可能存在的数据。 操作示例包括：

  - 向用户和组发送电子邮件警报，告知关于不合规设备的详细信息。 可将策略配置为在标记为“不符合”时立即发送电子邮件，然后定期发送，直到设备符合要求为止。
  - 将不符合状态达一段时间的设备远程锁定。
  - 在设备的不符合状态达一段时间后停用设备。 此操作将从 Intune 管理中删除该设备并从设备中删除所有公司数据。

- [配置网络位置](use-network-locations.md) - 受 Android 设备支持，你可配置网络位置，然后将这些位置用作设备符合性规则。 这种类型的规则可在设备超出或离开指定网络时将其标记为“不符合”。 必须先配置网络位置，然后才能指定位置规则。

- [创建策略](create-compliance-policy.md) - 你可通过本文信息查看先决条件、操作规则配置选项、指定针对非符合性的操作并将策略分配给组。 本文还包括有关策略刷新时间的信息。

  请查看不同设备平台的设备符合性设置：

  - [Android](compliance-policy-create-android.md)
  - [Android Enterprise](compliance-policy-create-android-for-work.md)
  - [iOS](compliance-policy-create-ios.md)
  - [macOS](compliance-policy-create-mac-os.md)
  - [Windows Holographic for Business](compliance-policy-create-windows.md#windows-holographic-for-business)
  - [Windows 8.1 及更高版本](compliance-policy-create-windows-8-1.md)
  - [Windows 10 及更高版本](compliance-policy-create-windows.md)

## <a name="monitor-compliance-status"></a>监视符合性状态

Intune 有一个设备符合性仪表板，你可用它来监视设备的符合性状态，并深入了解策略和设备以获取详细信息。 要详细了解此仪表板，请参阅[监视设备符合性](compliance-policy-monitor.md)。

## <a name="integrate-with-conditional-access"></a>与条件访问集成

使用条件访问时，可将条件访问策略配置为使用设备符合性策略的结果来确定哪些设备可访问组织资源。 此访问控制是对设备符合性策略中包含的针对非符合性的操作的补充，并与之分离。

在 Intune 中注册设备时，也会在 Azure AD 中进行注册。 设备的符合性状态报告给 Azure AD。 如果条件访问策略将访问控制设置为“要求设备被标记为符合”，则条件访问将使用该符合性状态来确定是授予还是阻止对电子邮件和其他组织资源的访问。

如果你将设备符合性状态与条件访问策略一起使用，请查看你的租户是如何配置“将未分配到符合性策略的设备标记为”的（可在[符合性策略设置](#compliance-policy-settings)下管理此项）。

要详细了解如何将条件访问与设备符合性策略一起使用，请参阅[基于设备的条件访问](conditional-access-intune-common-ways-use.md#device-based-conditional-access)

在 Azure AD 文档中详细了解条件访问：

- [什么是条件访问](/azure/active-directory/conditional-access/overview)
- [什么是设备标识](/azure/active-directory/device-management-introduction)

### <a name="reference-for-non-compliance-and-conditional-access-on-the-different-platforms"></a>不同平台上关于非符合情况和条件访问的参考

下表说明了将符合性策略与条件访问策略一起使用时如何管理非符合性设置：

- **已修正**：设备操作系统强制执行符合性。 例如，强制用户设置 PIN。

- **已隔离**：设备操作系统不会强制执行符合性。 例如，Android 和 Android Enterprise 设备不强制用户加密设备。 设备不符合时，系统将进行以下操作：
  - 如果对用户应用了条件访问策略，设备将被阻止。
  - 公司门户应用会就任何符合性问题通知用户。

---------------------------

|**策略设置**| **平台** |
| --- | ----|
| **PIN 或密码配置** | - **Android 4.0 及更高版本**：已隔离<br>- **Samsung Knox 标准版 4.0 及更高版本**：已隔离<br>- **Android Enterprise**：已隔离  <br>  <br>- **iOS 8.0 及更高版本**：已修正<br>- **macOS 10.11 及更高版本**：已修正  <br>  <br>- **Windows 8.1 及更高版本**：已修正|
| **设备加密** | - **Android 4.0 及更高版本**：已隔离<br>- **Samsung Knox 标准版 4.0 及更高版本**：已隔离<br>- **Android Enterprise**：已隔离<br><br>- **iOS 8.0 及更高版本**：已修正（通过设置 PIN）<br>- **macOS 10.11 及更高版本**：已修正（通过设置 PIN）<br><br>- **Windows 8.1 及更高版本**：“不适用”|
| **已越狱或取得 root 权限的设备** | - **Android 4.0 及更高版本**：已隔离（非设置）<br>- **Samsung Knox 标准版 4.0 及更高版本**：已隔离（非设置）<br>- **Android Enterprise**：已隔离（非设置）<br><br>- **iOS 8.0 及更高版本**：已隔离（非设置）<br>- **macOS 10.11 及更高版本**：“不适用”<br><br>- **Windows 8.1 及更高版本**：“不适用” |
| **电子邮件配置文件** | - **Android 4.0 及更高版本**：“不适用”<br>- **Samsung Knox 标准版 4.0 及更高版本**：“不适用”<br>- **Android Enterprise**：“不适用”<br><br>- **iOS 8.0 及更高版本**：已隔离<br>- **macOS 10.11 及更高版本**：已隔离<br><br>- **Windows 8.1 及更高版本**：“不适用” |
| **最低操作系统版本** | - **Android 4.0 及更高版本**：已隔离<br>- **Samsung Knox 标准版 4.0 及更高版本**：已隔离<br>- **Android Enterprise**：已隔离<br><br>- **iOS 8.0 及更高版本**：已隔离<br>- **macOS 10.11 及更高版本**：已隔离<br><br>- **Windows 8.1 及更高版本**：已隔离|
| **最高操作系统版本** | - **Android 4.0 及更高版本**：已隔离<br>- **Samsung Knox 标准版 4.0 及更高版本**：已隔离<br>- **Android Enterprise**：已隔离<br><br>- **iOS 8.0 及更高版本**：已隔离<br>- **macOS 10.11 及更高版本**：已隔离<br><br>- **Windows 8.1 及更高版本**：已隔离 |
| **Windows 运行状况证明** | - **Android 4.0 及更高版本**：“不适用”<br>- **Samsung Knox 标准版 4.0 及更高版本**：“不适用”<br>- **Android Enterprise**：“不适用”<br><br>- **iOS 8.0 及更高版本**：“不适用”<br>- **macOS 10.11 及更高版本**：“不适用”<br><br>- Windows 10：已隔离<br>- **Windows 8.1 及更高版本**：已隔离 |

---------------------------

## <a name="next-steps"></a>后续步骤

- [配置位置](../protect/use-network-locations.md)以用于 Android 设备
- [创建和部署策略](../protect/create-compliance-policy.md)并查看先决条件
- [监视设备合规性](../protect/compliance-policy-monitor.md)
- [Microsoft Intune 中设备策略和配置文件的常见疑问、问题和解决方案](../configuration/device-profile-troubleshoot.md)
- [策略实体参考](../developer/reports-ref-policy.md)中有 Intune 数据仓库策略实体的相关信息