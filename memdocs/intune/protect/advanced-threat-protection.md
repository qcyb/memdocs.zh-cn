---
title: 在 Microsoft Intune 中使用 Microsoft Defender ATP - Azure | Microsoft Docs
description: 将 Microsoft Defender 高级威胁防护 (Microsoft Defender ATP) 与 Intune 一起使用（包括设置和配置、载入带 ATP 的 Intune 设备），然后将设备 ATP 风险评估与 Intune 设备合规性和条件访问策略结合使用来保护网络资源。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/23/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1420bf03fe236decba0345e299eb5d5893f96c93
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915103"
---
# <a name="enforce-compliance-for-microsoft-defender-atp-with-conditional-access-in-intune"></a>使用 Intune 中的条件访问强制执行 Microsoft Defender ATP 的符合性

可以将 Microsoft Defender 高级威胁防护 (Microsoft Defender ATP) 和 Microsoft Intune 集成为 Mobile Threat Defense 解决方案。 集成可让你免受安全漏洞的威胁，并帮助限制组织中的漏洞影响。

Microsoft Defender ATP 适用于运行 Windows 10 或更高版本的设备以及 Android 设备。

若要成功，你将配合使用以下配置：

- **在 Intune 和 Microsoft Defender ATP 之间创建一个服务到服务的连接**。 通过这个连接，Microsoft Defender ATP 可以从使用 Intune 管理的受支持设备收集有关计算机风险的数据。
- **使用设备配置配置文件将设备载入 Microsoft Defender ATP**。 载入设备将其配置为与 Microsoft Defender ATP 进行通信，并提供有助于评估其风险级别的数据。
- **使用设备合规性策略设置要允许的风险级别**。 由 Microsoft Defender ATP 报告风险等级。 将超出允许风险级别的设备识别为不合规。
- “使用条件访问策略”阻止用户从不合规的设备访问公司资源。

将 Intune 与 Microsoft Defender ATP 集成时，可以充分利用 Microsoft Defender ATP 威胁和漏洞管理 (TVM) 并[使用 Intune 修正由 TVM 标识的终结点漏洞](atp-manage-vulnerabilities.md)。

## <a name="example-of-using-microsoft-defender-atp-with-intune"></a>将 Microsoft Defender ATP 和 Intune 结合使用的示例

下面的示例有助于解释这些解决方案如何协同工作以帮助保组织。 在此示例中，Microsoft Defender ATP 和 Intune 已经集成在一起了。

有人向组织内的用户发送包含嵌入式恶意代码的 Word 附件。

- 在用户打开附件时，将启用内容。
- 提升的权限攻击随即启动，且来自远程计算机的攻击者对受害者的设备具有管理权限。
- 然后，攻击者会远程访问用户的其他设备。 此安全漏洞可能会影响整个组织。

Microsoft Defender ATP 可以帮助解决类似这种情况的安全事件。

- 在本例中，Microsoft Defender ATP 检测设备是否存在以下情形：执行了异常代码、遇到了进程权限提升、插入了恶意代码，以及发布了可疑的远程 Shell。
- 基于该设备的这些操作，Microsoft Defender ATP [将该设备分类为高风险](/windows/security/threat-protection/microsoft-defender-atp/alerts-queue#severity)，并在 Microsoft Defender 安全中心门户中包含可疑活动的详细报告。

可以将 Microsoft Defender 高级威胁防护 (Microsoft Defender ATP) 和 Microsoft Intune 集成为 Mobile Threat Defense 解决方案。 集成可让你免受安全漏洞的威胁，并帮助限制组织中的漏洞影响。

因为你有 Intune 设备合规性策略来对具有“中等”或“高”风险级别的设备分类为不合规，所以受危害的设备被分类为不合规 。 这种分类允许条件访问策略介入并阻止从该设备访问公司资源。

对于运行 Android 的设备，你可以使用 Intune 策略修改 Android 上 Microsoft Defender ATP 的配置。 有关详细信息，请参阅 [Microsoft Defender ATP Web 保护](../protect/advanced-threat-protection-manage-android.md)。

## <a name="prerequisites"></a>必备条件

若要将 Microsoft Defender ATP 与 Intune 结合使用，请确保已配置以下各项，并可供使用：

- 企业移动性 + 安全性 E3 和 Windows E5（或 Microsoft 365 企业版 E5）的许可租户
- Microsoft Intune 环境，包含同样加入了 Azure AD 的 [Intune 托管的](../enrollment/windows-enroll.md) Windows 10 或 Android 设备
- [Microsoft Defender ATP](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) 环境将授予你对 Microsoft Defender 安全中心（ATP 门户）的访问权限

> [!NOTE]
> iOS/iPadOS 和 Android Intune 应用保护策略不支持 Microsoft Defender ATP。

## <a name="next-steps"></a>后续步骤

- 若要将 Microsoft Defender ATP 连接到 Intune、载入设备并配置条件访问策略，请参阅[在 Intune 中配置 Microsoft Defender ATP](../protect/advanced-threat-protection-configure.md)。

有关详细信息，请参阅 Intune 文档：

- [使用带有 ATP 漏洞管理的安全任务来修复设备上的问题](atp-manage-vulnerabilities.md)
- [设备符合性策略入门](device-compliance-get-started.md)

有关详细信息，请参阅 Microsoft Defender ATP 文档：

- [Microsoft Defender ATP 条件访问](/windows/security/threat-protection/microsoft-defender-atp/conditional-access)
- [Microsoft Defender ATP 风险仪表板](/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard)