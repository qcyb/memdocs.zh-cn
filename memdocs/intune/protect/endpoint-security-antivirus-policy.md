---
title: 在 Microsoft Intune 中使用终结点安全性策略管理防病毒设置 |Microsoft Docs
description: 在 Microsoft Endpoint Manager 中为使用终结点安全性防病毒策略管理的设备配置和部署策略并使用报告。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/24/2020
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
ms.openlocfilehash: 2460a132711fb19d12f33bbada23756fc2344cca
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89194240"
---
# <a name="antivirus-policy-for-endpoint-security-in-intune"></a>Intune 中的关于终结点安全性的防病毒策略

Intune 终结点安全性防病毒策略可帮助安全管理员专注于管理托管设备的独立防病毒设置组。 若要使用防病毒策略，请将 Intune 与 Microsoft Defender 高级威胁防护 (Microsoft Defender ATP) 集成为移动威胁防御解决方案。

防病毒策略包含多个配置文件。 每个配置文件仅包含 Microsoft Defender ATP 防病毒相关设置，这些设置适用于 macOS、Windows 10 或 Windows 10 上 Windows 安全应用中的用户体验。

可在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)的终结点安全节点中的“管理”下查找防病毒策略。

防病毒策略所包含的设置与[设备配置](../configuration/device-profile-create.md)策略的*终结点保护*或*设备限制*配置文件中的设置相同，并与[设备合规性](../protect/device-compliance-get-started.md)策略中的设置相似。 但是，这些策略类型包含其他类别的与防病毒无关的设置。 其他设置可能会使配置防病毒的任务复杂化。 此外，适用于 macOS 的防病毒策略中的设置无法通过其他策略类型使用。 使用 macOS 防病毒配置文件后，就无需使用 `.plist` 文件配置设置。

## <a name="prerequisites-for-antivirus-policy"></a>防病毒策略的先决条件

常规：

- **macOS**
  - 任何支持的 macOS 版本
  - 为了使 Intune 能够管理设备上的防病毒设置，需要在该设备上安装 Microsoft Defender ATP。 请参阅 [适用于 macOS 的 Microsoft Defender ATP](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac)（在 Microsoft Defender ATP 文档中）

- **Windows 10 及更高版本**
  - 无需其他先决条件。

**对 Configuration Manager 客户端的支持**（*预览*）

*此方案处于预览状态，需要使用 Configuration Manager Current Branch version 版本 2006 或更高版本*。
<!--*This scenario is in preview and requires use of Configuration Manager Technical Preview version 2007 or later*.-->

- **为 Configuration Manager 设备设置租户附加** - 若要支持将防病毒策略部署到 Configuration Manager 托管的设备，请配置 *“租户附加”* 。 设置租户附加包含配置 Configuration Manager 设备集合，以支持 Intune 终结点安全策略。

  若要设置租户附加，请参阅[配置租户附加以支持 Endpoint Protection 策略](../protect/tenant-attach-intune.md)。

## <a name="antivirus-profiles"></a>防病毒配置文件

### <a name="devices-managed-by-intune"></a>由 Intune 管理的设备

对于使用 Intune 管理的设备，支持以下配置文件：

**macOS**：

- 平台：**macOS**

  - 配置文件：**防病毒** - 管理适用于 macOS 的[防病毒策略设置](../protect/antivirus-microsoft-defender-settings-macos.md)。

    使用[适用于 Mac 的 Microsoft Defender ATP](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) 时，可以配置防病毒设置并将其部署到托管的 macOS 设备，方式是通过 Intune 而不是使用 `.plist` 文件配置这些设置。

**Windows 10**：

- 平台：**Windows 10 配置文件**

  - 配置文件：**Microsoft Defender 防病毒** - 管理适用于 Windows 10 的[防病毒策略设置](../protect/antivirus-microsoft-defender-settings-windows.md)。

    Defender 防病毒是 Microsoft Defender 高级威胁防护 (Microsoft Defender ATP) 的下一代保护组件。 下一代防护结合了机器学习等技术和云基础结构，旨在为企业组织中的设备提供保护。

    Microsoft Defender 防病毒配置文件是设备配置策略的设备限制配置文件中防病毒设置的一个独立实例 。
  
    与设备限制配置文件中的防病毒设置不同，这些设置可用于共同托管的设备。 若要使用这些设置，需要将用于 Endpoint Protection 的[共同管理工作负载滑块](/configmgr/comanage/how-to-switch-workloads)设置为 Intune。

  - 配置文件：**Microsoft Defender 防病毒排除项** - 仅管理[防病毒排除项](../protect/antivirus-microsoft-defender-settings-windows.md#microsoft-defender-antivirus-exclusions)的策略设置。
  
    通过此策略，可以管理用于定义防病毒排除项的以下 Microsoft Defender 防病毒配置服务提供商 (CSP) 的设置：

    - Defender/ExcludedPaths
    - Defender/ExcludedExtensions
    - Defender/ExcludedProcesses

    这些用于防病毒排除项的 CSP 也由 *Microsoft Defender 防病毒*策略进行管理，其中包括与排除项相同的设置。 来自两个策略类型（*防病毒*和*防病毒排除项*）的设置受[策略合并](#policy-merge-for-settings)限制，并为适用的设备和用户创建排除项超集。

  - 配置文件：**Windows 安全体验** - 管理最终用户可在 Microsoft Defender 安全中心查看的 [Windows 安全应用设置](../protect/antivirus-security-experience-windows-settings.md)以及他们收到的通知。

    许多 Windows 安全功能会使用 Windows 安全应用来提供关于计算机运行和安全状况的通知。 安全应用通知包括防火墙、防病毒产品、Windows Defender SmartScreen 和其他内容。

### <a name="devices-managed-by-configuration-manager-in-preview"></a>Configuration Manager 托管的设备 *（处于预览状态）*

[!INCLUDE [Profiles for Configuration Manager tenant attached devices](includes/configmgr-antivirus-profiles.md)]

## <a name="policy-merge-for-settings"></a>设置的策略合并

某些防病毒策略设置支持*策略合并*。 如果将多个策略应用于相同的设备并配置相同的设置，则策略合并有助于避免冲突。 对于从所有适用策略中获取的每个用户或设备，Intune 会评估策略合并支持的设置。 然后，这些设置将合并到策略的单一超集。

例如，你创建三个单独的防病毒策略来定义不同的防病毒文件路径排除项。 最终，所有三个策略都将分配给同一个用户。 由于 Microsoft Defender 文件路径排除项 CSP 支持策略合并，因此 Intune 会评估并合并该用户的所有适用策略的文件排除项。 排除项将添加到超集，并向用户的设备传递单个排除项列表。

如果某个设置不支持策略合并，则可能会发生冲突。 冲突可能导致用户或设备无法收到设置的任何策略。 例如，策略合并不支持用于阻止安装匹配的设备 ID (*PreventInstallationOfMatchingDeviceIDs*) 的 CSP。 此 CSP 的配置不会合并，而是单独进行处理。

单独处理时，按如下方式解决策略冲突：

1. 应用最安全的策略。
2. 如果两个策略同样安全，则会应用最后修改的策略。
3. 如果最后修改的策略无法解决冲突，则不会向设备传递策略。

### <a name="settings-and-csps-that-support-policy-merge"></a>支持策略合并的设置和 CSP

以下设置支持策略合并：

[Microsoft Defender 防病毒策略](../protect/antivirus-microsoft-defender-settings-windows.md)

- **要排除的 Defender 进程** - CSP：[Defender/ExcludedProcesses](/windows/client-management/mdm/policy-csp-defender#defender-excludedprocesses)
- **要从扫描和实时保护中排除的文件扩展名** - CSP：[Defender/ExcludedExtensions](/windows/client-management/mdm/policy-csp-defender#defender-excludedextensions)
- **要排除的 Defender 文件和文件夹** - CSP：[Defender/ExcludedPaths](/windows/client-management/mdm/policy-csp-defender#defender-excludedpaths)

## <a name="antivirus-policy-reports"></a>防病毒策略报告

防病毒策略报告显示有关终结点安全性防病毒策略和设备状态的状态详细信息。 这些报告在 Microsoft Endpoint Manager 管理中心的终结点安全节点中提供。

若要查看报告，在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，转到终结点安全性并选择“防病毒”。 选择“防病毒”后会打开“摘要”页面。 其他报告和状态视图可在附加页面中查看。

### <a name="summary"></a>“摘要”

在“摘要”页面上，可[创建新策略](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)并查看之前创建的策略列表。 此列表包含关于策略包含的配置文件（策略类型）以及策略是否分配的高级别的详细信息。

![防病毒策略的“摘要”页](./media/endpoint-security-antivirus-policy/antivirus-summary.png)

从列表中选择某策略时，该策略实例的“概述”页面随即打开并显示详细信息。 在该视图中选择某个磁贴后，Intune 会显示配置文件的相应详细信息（如果有）。

![防病毒策略的“概述”页面](./media/endpoint-security-antivirus-policy/policy-overview.png)

### <a name="windows-10-unhealthy-endpoints"></a>Windows 10 不正常的终结点

在“Windows 10 不正常的终结点”页面上，可以查看有关 MDM 托管的 Windows 10 设备的防病毒状态的信息。 此信息从设备上运行的 Windows Defender 防病毒功能返回，反映威胁代理状态。

此视图中仅显示检测到问题的设备。 此视图不显示识别为“干净的”的设备的详细信息。

![防病毒策略的“不正常终结点”页](./media/endpoint-security-antivirus-policy/antivirus-unhealthy-endpoints.png)

## <a name="next-steps"></a>后续步骤

[配置终结点安全策略](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)