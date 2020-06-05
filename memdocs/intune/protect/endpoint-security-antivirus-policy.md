---
title: 在 Microsoft Intune 中使用终结点安全性策略管理防病毒设置 |Microsoft Docs
description: 在 Microsoft Endpoint Manager 中为使用终结点安全性防病毒策略管理的设备配置和部署策略并使用报告。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 2f3a378cdb3b5e24371edb2fd6dc240962f80342
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431899"
---
# <a name="antivirus-policy-for-endpoint-security-in-intune"></a>Intune 中的关于终结点安全性的防病毒策略

Intune 终结点安全性防病毒策略可帮助安全管理员专注于管理托管设备的独立防病毒设置组。 若要使用防病毒策略，请将 Intune 和 Microsoft Defender 高级威胁防护 (Defender ATP) 集成为 Mobile Threat Defense 解决方案。

防病毒策略包含多个配置文件。 每个配置文件仅包含 Defender ATP 防病毒相关设置，这些设置适用于 macOS、Windows 10 或 Windows 10 上 Windows 安全应用中的用户体验。

可在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)的终结点安全节点中的“管理”下查找防病毒策略。

防病毒策略所包含的设置与[设备配置](../configuration/device-profile-create.md)策略的终结点保护或设备限制配置文件中的设置相同，并与[设备合规性](../protect/device-compliance-get-started.md)策略中的设置相似 。 但是，这些策略类型包含其他类别的与防病毒无关的设置。 其他设置可能会使配置防病毒的任务复杂化。 此外，适用于 macOS 的防病毒策略中的设置无法通过其他策略类型使用。 使用 macOS 防病毒配置文件后，就无需使用 `.plist` 文件配置设置。

## <a name="prerequisites-for-antivirus-policy"></a>防病毒策略的先决条件

- **macOS**
  - 任何支持的 macOS 版本
  - 为了使 Intune 能够管理设备上的防病毒设置，需要在该设备上安装 Defender ATP。 请参阅 [适用于 macOS 的 Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac)（在 Defender ATP 文档中）

- **Windows 10 及更高版本**
  - 为了使 Intune 能够管理设备上的防病毒设置，需要在该设备上安装 Defender ATP。 请参阅 Intune 文档中的[适用于 Windows 的 Microsoft Defender ATP](../protect/advanced-threat-protection.md)。
  - 运行 Windows 10 的所有设备上都安装了 Windows 安全应用，不需要满足额外的先决条件。

## <a name="antivirus-profiles"></a>防病毒配置文件

**macOS 配置文件**：

- **防病毒** - 管理适用于 macOS 的[防病毒策略设置](../protect/antivirus-microsoft-defender-settings-macos.md)。

  使用[适用于 Mac 的 Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) 时，可以配置防病毒设置并将其部署到托管的 macOS 设备，方式是通过 Intune 而不是使用 `.plist` 文件配置这些设置。

**Windows 10 配置文件**：

- **Microsoft Defender 防病毒** - 管理适用于 Windows 10 的[防病毒策略设置](../protect/antivirus-microsoft-defender-settings-windows.md)。

  Defender 防病毒是 Microsoft Defender 高级威胁防护 (Microsoft Defender ATP) 的下一代保护组件。 下一代防护结合了机器学习、大数据分析、深度威胁抵御研究和云基础结构，旨在为企业组织中的设备提供保护。

  Microsoft Defender 防病毒配置文件是设备配置策略的设备限制配置文件中防病毒设置的一个独立实例 。
  
  与设备限制配置文件中的防病毒设置不同，这些设置可用于共同托管的设备。 若要使用这些设置，需要将用于 Endpoint Protection 的[共同管理工作负载滑块](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads)设置为 Intune。

- **Windows 安全体验** - 管理最终用户可在 Microsoft Defender 安全中心查看的 [Windows 安全应用设置](../protect/antivirus-security-experience-windows-settings.md)以及他们收到的通知。 许多 Windows 安全功能会使用 Windows 安全应用来提供关于计算机运行和安全状况的通知。 安全应用通知包括防火墙、防病毒产品、Windows Defender SmartScreen 和其他内容。

## <a name="antivirus-policy-reports"></a>防病毒策略报告

防病毒策略报告显示有关终结点安全性防病毒策略和设备状态的状态详细信息。 这些报告在 Microsoft Endpoint Manager 管理中心的终结点安全节点中提供。

若要查看报告，在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，转到终结点安全性并选择“防病毒”。 选择“防病毒”后会打开“摘要”页面。 其他报告和状态视图可在附加页面中查看。

### <a name="summary"></a>“摘要”

在“摘要”页面上，可[创建新策略](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)并查看之前创建的策略列表。 此列表包含关于策略包含的配置文件（策略类型）以及策略是否分配的高级别的详细信息。

![防病毒策略的“概述”页面](./media/endpoint-security-antivirus-policy/antivirus-summary.png)

从列表中选择某策略时，该策略实例的“概述”页面随即打开并显示详细信息。 在该视图中选择某个磁贴时，Intune 会显示配置文件的相应详细信息（如果有）。

![防病毒策略的“概述”页面](./media/endpoint-security-antivirus-policy/policy-overview.png)

### <a name="windows-10-unhealthy-endpoints"></a>Windows 10 不正常的终结点

在“Windows 10 不正常的终结点”页面上，可以查看有关 MDM 托管的 Windows 10 设备的防病毒状态的信息。 此信息从设备上运行的 Windows Defender 防病毒功能返回，反映威胁代理状态。

此视图中仅显示检测到问题的设备。 此视图不显示识别为“干净的”的设备的详细信息。

![防病毒策略的“概述”页面](./media/endpoint-security-antivirus-policy/antivirus-unhealthy-endpoints.png)

## <a name="next-steps"></a>后续步骤

[配置终结点安全策略](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
