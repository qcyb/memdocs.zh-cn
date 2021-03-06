---
title: 租户附加设备中 Microsoft Defender 防病毒的 Windows 10 防病毒策略设置| Microsoft Docs
description: 参阅适用于 Configuration Manager 托管的 Windows 10 设备的 Microsoft Defender 防病毒配置文件中的设置列表。 为 Configuration Manager 配置租户附加后，可以在 Microsoft Intune 中将这些设置配置为终结点安全性防病毒策略的一部分。
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
ms.openlocfilehash: 3bb1d4806271ab40c60f0ad419e4e708d36bbc97
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89194117"
---
# <a name="settings-for-microsoft-defender-antivirus-policy-for-tenant-attached-devices-in-microsoft-intune"></a>Microsoft Intune 中租户附加设备的 Microsoft Defender 防病毒策略的设置。

查看可通过 Intune 的 **Microsoft Defender 防病毒策略 (ConfigMgr)** 配置文件管理的 Microsoft Defender 防病毒设置。 配置 Intune [终结点安全防病毒策略](../protect/endpoint-security-antivirus-policy.md)时，配置文件可用，并在配置了[租户附加](../protect/tenant-attach-intune.md)方案时，策略部署到通过 Configuration Manager 管理的设备。

## <a name="cloud-protection"></a>云保护

- **启用云提供的保护**  
  CSP：[AllowCloudProtection](/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  默认情况下，Windows 10 桌面版设备上的 Defender 将有关发现的任何问题的信息发送给 Microsoft。 Microsoft 分析该信息，详细了解影响你和其他客户的问题，并提供改进的解决方案。

  - **未配置**（默认值）- 设置将还原为系统默认值。
  - **不允许。** 关闭 Microsoft Active Protection Service。
  - **允许。**  启用 Microsoft Active Protection Service。

- **云提供的保护级别**  
  CSP：[CloudBlockLevel](/windows/client-management/mdm/policy-csp-defender#defender-cloudblocklevel)

  配置 Defender 防病毒在阻止和扫描可疑文件方面的积极程度。
  - **未配置**（默认值）- 默认的 Defender 阻止级别。
  - **高** - 主动阻止未知文件，同时针对客户端性能进行优化（误报的可能性更大）。
  - **超高** - 主动阻止未知文件，并应用额外的保护措施（可能影响客户端的性能）。
  - **零容差** - 阻止所有未知的可执行文件。

- **Defender 云扩展超时(秒)**  
  CSP：[CloudExtendedTimeout](/windows/client-management/mdm/policy-csp-defender#defender-cloudextendedtimeout)

  Defender 防病毒会自动阻止可疑文件 10 秒钟，使其可以扫描云中的文件以确保安全性。 使用此设置，最多可以将此超时值增加 50 秒。

## <a name="microsoft-defender-antivirus-exclusions"></a>Microsoft Defender 防病毒排除项

对于此组中的每项设置，可以展开设置，选择“添加”，然后为排除项指定一个值。

- **要排除的 Defender 进程**  
  CSP：[ExcludedProcesses](/windows/client-management/mdm/policy-csp-defender#defender-excludedprocesses)

  指定在扫描期间要忽略的由进程打开的文件列表。 进程本身不会从扫描中排除。

- **要从扫描和实时保护中排除的文件扩展名**  
  CSP：[ExcludedExtensions](/windows/client-management/mdm/policy-csp-defender#defender-excludedextensions)

  指定在扫描期间要忽略的文件类型扩展名的列表。

- 要**排除的 Defender 文件和文件夹**  
  CSP：[ExcludedPaths](/windows/client-management/mdm/policy-csp-defender#defender-excludedpaths)

  指定在扫描期间要忽略的文件和目录路径列表。

## <a name="real-time-protection"></a>实时保护

- **启用实时保护**  
  CSP：[AllowRealtimeMonitoring](/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

  需要 Windows 10 桌面版设备上的 Defender 使用实时监视功能。
  - **未配置**（默认值）- 设置将还原为系统默认值
  - **不允许。** 关闭实时监视服务。
  - **允许。** 启用并运行实时监视服务。

- **启用访问保护**  
  CSP：[AllowOnAccessProtection](https://go.microsoft.com/fwlink/?linkid=2113935)

  配置病毒防护保持活动状态，而不是按需启用。

  - **未配置**（默认值）- 此策略不会更改设备上此设置的状态。 设备上的现有状态保持不变。
  - **不允许。** 关闭实时监视服务。
  - **允许。**

- **监视传入和传出文件**  
  CSP：[Defender/RealTimeScanDirection](https://go.microsoft.com/fwlink/?linkid=2113943)

  配置此设置以确定监视哪个 NTFS 文件和程序活动。
  - **监视所有文件（双向）。** (*默认*)
  - **监视传入的文件。**
  - **监视传出的文件。**

- **启用行为监视**  
  CSP：[AllowBehaviorMonitoring](https://go.microsoft.com/fwlink/?linkid=2114048)

  默认情况下，Windows 10 桌面版设备上的 Defender 使用行为监视功能。

  - **未配置**（默认值）- 设置将还原为系统默认值。
  - **不允许。** 关闭行为监视。
  - **允许。** 启用实时行为监视。

- **允许入侵防护系统**  
  - **未配置**（默认值）- 设置将还原为系统默认值。
  - **不允许。**
  - **允许。**

- **扫描所有已下载的文件和附件**  
  CSP：[EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=2113939)

  配置 Defender 以扫描所有已下载的文件和附件。

  - **未配置**（默认值）- 设置将还原为系统默认值。
  - **不允许。**
  - **允许。**

- **扫描在 Microsoft 浏览器中使用的脚本**  
  CSP：[AllowScriptScanning](https://go.microsoft.com/fwlink/?linkid=2114054)

  配置 Defender 以扫描脚本。

  - **未配置**（默认值）- 设置将还原为系统默认值。
  - **不允许。**
  - **允许。**

- **扫描网络文件**  
  CSP：[AllowScanningNetworkFiles](https://go.microsoft.com/fwlink/?linkid=2114049&)

  配置 Defender 以扫描网络文件。

  - **未配置**（默认值）- 设置将还原为系统默认值。
  - **不允许。** 关闭网络文件扫描。
  - **允许。** 扫描网络文件。

- **扫描电子邮件**  
  CSP：[AllowEmailScanning](https://go.microsoft.com/fwlink/?linkid=2114052)

  配置 Defender 以扫描传入电子邮件。

  - **未配置**（默认值）- 设置将还原为系统默认值。
  - **不允许。** 关闭电子邮件扫描。
  - **允许。** 启用电子邮件扫描。

## <a name="remediation"></a>补救

- **已隔离的恶意软件的保留天数(0-90)**  
  CSP：[DaysToRetainCleanedMalware](https://go.microsoft.com/fwlink/?linkid=2114055)

  指定在已隔离项被自动删除之前，系统存储已隔离项的天数（0-99）。 如果值为零，则会保持项的隔离状态，并且不会自动将其删除。

- **提交示例同意**  

  - **未配置**（默认）
  - **始终提示。**
  - **自动发送安全示例。**
  - **从不发送。**
  - **自动发送所有示例。**

- **对潜在有害应用执行的操作**  
  CSP：[PUAProtection](https://go.microsoft.com/fwlink/?linkid=2114051)

  指定潜在有害应用程序 (PUA) 的检测级别。 当正在下载或尝试在设备上安装潜在有害软件时，Defender 会向用户发出警报。

  - **未配置**（默认值）- 设置将还原为系统默认值（PUA 保护禁用）。
  - **关闭 PUA 保护。** Windows Defender 将不会对可能不需要的应用程序提供保护。
  - **启用 PUA 保护。** 已阻止检测到的项目。 这些项目将与其他威胁一起显示在历史记录中。
  - **审核模式。** Defender 检测可能不需要的应用程序，但不执行任何操作。 可以通过在事件查看器中搜索 Defender 创建的事件，查看有关 Defender 将对其执行操作的应用程序的信息。

- **清理计算机之前创建系统还原点**  
  - **是**（默认）
  - 否
  - **未配置**

- **针对检测到的威胁的操作**  
  CSP：[ThreatSeverityDefaultAction](https://go.microsoft.com/fwlink/?linkid=2113938)

  根据恶意软件的威胁级别指定 Defender 针对检测到的恶意软件采取的操作。
  
  Defender 会将它检测到的恶意软件归类为以下严重级别之一：
  - **低威胁**
  - **中等威胁**
  - **高威胁**
  - **严重威胁**

  对于每个级别，请指定要执行的操作。 每个严重性级别默认都为“未配置”。

  - **未配置**（默认）
  - **清理** - 服务将尝试恢复文件并尝试杀毒。
  - **隔离** - 将文件移到隔离区。
  - **删除** - 从设备删除文件。
  - **允许** - 允许文件并且不执行其他操作。
  - **用户定义** - 设备用户可以决定要执行的操作。
  - **阻止** - 阻止文件执行。

## <a name="scan"></a>扫描

- **扫描存档文件**  
  CSP：[AllowArchiveScanning](https://go.microsoft.com/fwlink/?linkid=2114047)

  配置 Defender 以扫描存档文件（如 ZIP 或 CAB 文件）。

  - **未配置** *（默认值）* - 设置将还原为客户端默认值（扫描存档文件），但用户可能禁用了此扫描。
了解更多
  - **不允许**对已存档的文件禁用扫描。
  - **允许。** 扫描存档文件。

- **对计划的扫描启用低 CPU 优先级**  
  CSP：[EnableLowCPUPriority](https://go.microsoft.com/fwlink/?linkid=2113944)

  配置计划扫描的 CPU 优先级。
  - **未配置**（默认值））- 设置将还原为系统默认值（不对 CPU 优先级进行任何更改）。
  - **已禁用**
  - **Enabled**

- **禁用追加完全扫描**  
  CSP：[DisableCatchupFullScan](https://go.microsoft.com/fwlink/?linkid=2114042)

  为计划的完全扫描配置弥补扫描。 Catch-Up 扫描是在错过定期计划扫描后而启动的扫描。 由于计算机在计划时间内关闭，通常会错过这些计划扫描。

  - **未配置**（默认值）- 设置将还原为客户端默认值（为完全扫描启用弥补扫描），但用户可能禁用了此项。
  - **已禁用**
  - **Enabled**

- **禁用弥补快速扫描**  
  CSP：[DisableCatchupQuickScan](https://go.microsoft.com/fwlink/?linkid=2113941)

  为计划的快速扫描配置弥补扫描。 Catch-Up 扫描是在错过定期计划扫描后而启动的扫描。 由于计算机在计划时间内关闭，通常会错过这些计划扫描。

  - **未配置**（默认值）- 设置将还原为客户端默认值（启用弥补快速扫描），但用户可能禁用了此项。
  - **已禁用**
  - **Enabled**

- **每个扫描的 CPU 使用率限制 (0-100%)**  
  CSP：[AvgCPULoadFactor](https://go.microsoft.com/fwlink/?linkid=2114046)

  指定 Defender 扫描的平均 CPU 负载系数（从 0 到 100 的百分比）。

- **启用在完全扫描期间扫描映射的网络驱动器**  
  CSP：[AllowFullScanOnMappedNetworkDrives](https://go.microsoft.com/fwlink/?linkid=2113945)

  配置 Defender 以扫描映射的网络驱动器。

  - **未配置**（默认值）- 设置将还原为系统默认值（禁止扫描映射的网络驱动器）。
  - **不允许。** 对映射网络驱动器禁用扫描。
  - **允许。** 扫描映射的网络驱动器

- **每日快速扫描运行时间**  
  CSP：[ScheduleQuickScanTime](https://go.microsoft.com/fwlink/?linkid=2114053)

  选择每天运行 Defender 快速扫描的时间。
  默认情况下**未配置**此选项。

- **扫描类型**  
  CSP：[ScanParameter](https://go.microsoft.com/fwlink/?linkid=2114045)

  选择 Defender 运行的扫描类型。

  - **未配置**（默认值）
  - **快速扫描**
  - **完全扫描**

- **一周中运行计划扫描的日期**  
  - **未配置**（默认值）

- **一天中运行计划扫描的时间**  
  - **未配置**（默认值）

- **在运行扫描之前检查签名更新**  
  - **未配置**（默认值）
  - **已禁用**
  - **Enabled**

- **随机化计划的扫描和安全智能更新开始时间**  
  -**未配置**（*默认值*） - **是**
  -**否**

- **在完全扫描期间扫描可移动驱动器**
  - **未配置**（默认值）
  - **不允许。** 对可移动驱动器禁用扫描。
  - **允许。** 扫描可移动驱动器。

## <a name="updates"></a>更新

- **输入检查安全智能更新的频率(0-24 小时)**  
  CSP：[SignatureUpdateInterval](https://go.microsoft.com/fwlink/?linkid=2113936)

  指定用于检查签名的时间间隔，从 0 到 24（以小时为单位）。 如果值为零，则不会检查新的签名。 如果值为 2，将每隔两小时检查一次，依此类推。

- **签名更新回退顺序(设备)**

- **签名更新文件共享源(设备)**

- **安全智能位置(设备)**  

## <a name="user-experience"></a>用户体验

- **阻止用户访问 Microsoft Defender 应用**  
  - **未配置**（默认值）
  - **不允许。** 阻止用户访问 UI。
  - **允许。** 允许用户访问 UI。

- **当用户需要运行完整扫描、更新安全智能或运行 Windows Defender 脱机版时在客户端计算机上显示通知消息**  
  - **未配置**（默认值）
  - **是**
  - **否**

- **禁用客户端用户界面**  
  - **未配置**（默认值）
  - **是**
  - **否**

- **允许用户查看完整历史记录结果**
  - **未配置**（默认值）
  - **是**
  - **否**