---
title: 监视器连接运行状况
titleSuffix: Configuration Manager
description: 有关如何在 Configuration Manager 中监视桌面分析的连接运行状况和设备状态的详细信息。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 1f4e26f7-42f2-40c8-80cf-efd405349c6c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 37555c6b60b0d2c18096c2778e9a077baeb9143f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695595"
---
# <a name="monitor-connection-health"></a>监视器连接运行状况

使用 Configuration Manager 中的“连接运行状况”  仪表板，按设备运行状况向下钻取类别。 在 Configuration Manager 控制台中，转到“软件库”工作区，展开“桌面分析服务”节点，然后选择“连接运行状况”仪表板    。  

[![Configuration Manager 连接运行状况仪表板的屏幕截图](media/connection-health-dashboard.png)](media/connection-health-dashboard.png#lightbox)

首次设置桌面分析时，这些图表可能不会显示完整的数据。 活动设备需要 2-3 天才能将诊断数据发送到桌面分析服务进行处理，然后与 Configuration Manager 站点同步。<!-- 4098037 -->

## <a name="connection-details"></a>连接详细信息

此磁贴显示下列有关从 Configuration Manager 到桌面分析的连接的基本信息：

- **租户名称**：“Azure 服务”  节点中的桌面分析连接的名称

- **目标集合**：将 Configuration Manager 连接到桌面分析时指定的相同目标集合  。 此集合包括 Configuration Manager 使用你的商业 ID 和诊断数据设置配置的所有设备。 它是 Configuration Manager 连接到桌面分析服务的完整设备集。

- **目标设备**：目标集合中的所有设备，以下类型的设备除外：

  - 已停用
  - 已过时
  - 非活动
  - 非托管
  - 运行 Windows 10 长期服务渠道 (LTSC) 版本的设备
  - 运行 Windows Server 的设备

    有关这些设备状态的详细信息，请参阅[关于客户端状态](../core/clients/manage/monitor-clients.md#bkmk_about)。

    > [!Note]  
    > Configuration Manager 将目标集合中的所有设备（已停用和已过时的客户端除外）上载到桌面分析。

- **符合 DA 条件的设备**：目标设备（不符合桌面分析条件的设备除外）的数量。 例如，目标集合中运行 Windows Server 或 Windows 10 长期服务渠道 (LTSC) 版本的设备。

## <a name="last-sync-details"></a>上次同步详细信息

此磁贴显示 Configuration Manager 与桌面分析云服务同步的时间以及它同步的设备数量。

- **同步的设备**：Configuration Manager 发送到桌面分析的合格设备数。 服务将这些设备包括在当前可见的快照中。

- **上次服务同步**：与桌面分析门户中“上次更新”  时间相同。

- **下次服务同步**：预计在桌面分析中获得下一个每日快照的时间。

> [!Note]  
> 第一次将设备注册到桌面分析时，可能需要几天时间才能完成数据上载和处理。 在此期间，“上次同步详细信息”  磁贴可能会显示为空白。
> 此外，当你请求按需快照时，此磁贴中的任何值都不会自动更新。 有关详细信息，请参阅[数据延迟](troubleshooting.md#data-latency)。

如果认为某些设备未显示在桌面分析中，请确保桌面分析支持这些设备。 有关详细信息，请参阅[先决条件](overview.md#prerequisites)。

## <a name="connection-health"></a>连接运行状况

“连接运行状况”  图表显示处于以下运行状况状态下的设备数：  

- [正确注册](#properly-enrolled)：设备显示在桌面分析中并具有完整清单
- [无法注册](#unable-to-enroll)：出现阻止设备注册的阻塞性问题
- [配置警报](#configuration-alert)：设备不显示在桌面分析中，或显示时具有不完整的清单。 Configuration Manager 还识别到设备注册问题。
- [正在等待注册](#awaiting-enrollment)：Configuration Manager 配置了设备，但它尚未显示在桌面分析中
- [状态挂起](#status-pending)：Configuration Manager 仍在配置此设备，或者设备上没有足够的数据来确定其状态
- [缺少数据](#missing-data)：Configuration Manager 配置了设备，但桌面分析只包含部分数据

<!-- 
- [Configuration issues](#configuration-issues)  
- [Client not installed](#client-not-installed)  
- [Waiting for enrollment](#waiting-for-enrollment)  
- [Missing prerequisites](#missing-prerequisites)  
 -->

此图表中的设备总数应该与“连接详细信息”磁贴中“符合 DA 条件的设备”  值相同。

在图表中选择切片，以向下钻取到具有该状态的设备列表。 有关详细信息，请参阅[设备列表](#device-list)。

在图例中选择要在图表中删除或添加的类别名称。 此操作有助于放大图表，以便查看较小段的相对大小。

### <a name="properly-enrolled"></a>正确注册

设备具有以下属性：

- Configuration Manager 客户端版本 1902 或更高版本  
- 没有配置错误  
- 桌面分析在过去 28 天内接收到此设备的完整诊断数据  
- 桌面分析提供设备配置和已安装应用的完整清单  

### <a name="unable-to-enroll"></a>无法注册

Configuration Manager 检测到一个或多个阻止设备注册的阻塞性问题。 有关详细信息，请参阅 [Configuration Manager 中的桌面分析设备属性](#bkmk_config-issues)列表。  

例如，Configuration Manager 客户端版本低于 1902 (5.0.8790)。 将客户端更新到最新版本。 考虑为 Configuration Manager 站点启用自动客户端升级。 有关详细信息，请参阅[升级客户端](../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade)。  

从版本 2002 开始，可以在两个领域更轻松地确定客户端代理配置问题：

- **终结点连接性检查**：如果客户端无法访问所需的终结点，你会在仪表板中看到配置警报。 向下钻取到无法注册的客户端，查看由于代理配置问题而导致客户端无法连接到的终结点。 有关详细信息，请参阅[终结点连接性检查](#endpoint-connectivity-checks)。<!-- 4963230 -->

- **连接性状态**：如果客户端使用代理服务器访问桌面分析，Configuration Manager 会显示来自客户端的代理身份验证问题。 向下钻取以查看由于代理身份验证问题而无法注册的客户端。 有关详细信息，请参阅[连接性状态](#connectivity-status)。<!-- 4963383 -->

### <a name="configuration-alert"></a>配置警报

设备不显示在桌面分析中，或显示时具有不完整的清单。 Configuration Manager 还识别到设备注册问题。 有关详细信息，请参阅 [Configuration Manager 中的桌面分析设备属性](#bkmk_config-issues)列表。

例如，设备没有与服务连接。 有关详细信息，请参阅 [Windows 诊断终结点连接](#windows-diagnostic-endpoint-connectivity)。

### <a name="awaiting-enrollment"></a>正在等待注册

桌面分析没有此设备的诊断数据。 此问题可能是因为最近将设备添加到目标集合，但它尚未发送数据。 也可能表示设备未与服务正常通信，最新的诊断数据是 28 天前的数据。

确保设备可以与服务通信。 有关详细信息，请参阅[终结点](enable-data-sharing.md#endpoints)。  

### <a name="status-pending"></a>状态挂起

Configuration Manager 仍在配置此设备，或者设备上没有足够的数据来确定其状态。

### <a name="missing-data"></a>缺少数据

Configuration Manager 已成功配置设备，但桌面分析无法创建兼容性评估。 它没有设备配置（统计）或已安装的应用（清单）的完整数据集。

当设备重试时，通常会自动修复此问题。 如果问题仍然存在，请确保设备可以与服务通信。 有关详细信息，请参阅[终结点](enable-data-sharing.md#endpoints)。  

## <a name="device-list"></a>设备列表

若要按状态查看特定的设备列表，请从“连接运行状况”  仪表板开始。 选择“连接运行状况”磁贴  的一个段，向下钻取到处于此状态的设备的列表。 默认情况下，此自定义设备视图显示以下桌面分析列：

- 商业 ID 配置
- 最低兼容性更新
- Windows 诊断数据选择加入
- Windows 商业数据选择加入
- Windows 诊断终结点连接
- 连接性状态（从版本 2002 开始）
- 终结点连接性检查（从版本 2002 开始）

这些列对应于设备用来与桌面分析通信的关键[先决条件](overview.md#prerequisites)。

[![无法注册的设备列表的屏幕截图](media/device-list-unable-to-enroll.png)](media/device-list-unable-to-enroll.png#lightbox)

选择一个设备，可在详细信息窗格中查看可用属性的完整列表。 你还可以将任何这些属性作为列添加到设备列表中。

## <a name="device-properties"></a><a name="bkmk_config-issues"></a> 设备属性

以下桌面分析设备属性可作为 Configuration Manager 设备列表中的列：

- [终结点连接性检查](#endpoint-connectivity-checks)（从版本 2002 开始）
- [连接性状态](#connectivity-status)（从版本 2002 开始）
- [配置](#appraiser-configuration)  
- [最低兼容性更新](#minimum-compatibility-update)  
- [版本](#appraiser-version)  
- [评估程序的上次成功完全运行](#last-successful-full-run-of-appraiser)  
- [评估程序数据收集](#appraiser-data-collection)  
- [统计的上次成功完全运行](#last-successful-full-run-of-census)  
- [统计数据收集](#census-data-collection)  
- [Windows 诊断终结点连接](#windows-diagnostic-endpoint-connectivity)  
- [检查最终用户诊断数据](#check-end-user-diagnostic-data)  
- [检查用户代理](#check-user-proxy)  
- [商业 ID 配置](#commercial-id-configuration)  
- [Windows 商业数据选择加入](#windows-commercial-data-opt-in)  
- [检查诊断数据中的设备名称](#check-device-name-in-diagnostic-data)  
- [DiagTrack 服务配置](#diagtrack-service-configuration)  
- [DiagTrack 版本](#diagtrack-version)  
- [SQM ID 检索](#sqm-id-retrieval)  
- [唯一设备标识符检索](#unique-device-identifier-retrieval)  
- [Windows 诊断数据选择加入](#windows-diagnostic-data-opt-in)  

“连接运行状况”仪表板的“最常见的注册阻止程序和配置警报”  磁贴显示最常被设备报告为问题的属性。

### <a name="endpoint-connectivity-checks"></a>终结点连接性检查

从版本 2002 开始，<!-- 4963230 --> 为了检测代理身份验证问题，客户端对所需的终结点执行连接性检查。 如果客户端无法到达所需的终结点，则此属性显示由于代理配置问题而无法连接到的终结点的编号列表。 将此列表与已发布的[所需终结点](enable-data-sharing.md#endpoints)列表进行比较。

### <a name="connectivity-status"></a>连接性状态

从版本 2002 开始，<!-- 4963383 --> 如果客户端使用代理服务器访问桌面分析，则此属性显示代理身份验证问题。 它包括以下与代理身份验证有关的详细信息：

- 状态代码
- 返回代码

你会在日志文件中看到类似于以下内容的错误：

`Error 407: Can't connect to Microsoft %s. Check your network/proxy settings`

其中 `%s` 是所需终结点的 URL。

你可能还会看到在设备出现注册问题之前不需要注意的非确定性错误消息。 例如：

`This status is not related to proxy configuration, consider to investigate only if you are experiencing device enrollment or configuration alert issues.`

有关配置代理服务器以与桌面分析结合使用的详细信息，请参阅[代理服务器身份验证](enable-data-sharing.md#proxy-server-authentication)。

### <a name="appraiser-configuration"></a>评估程序配置

<!--20,21-->
评估程序是与[兼容性更新](enroll-devices.md#update-devices)对应的 Windows 组件。 它会评估设备上的应用和驱动程序是否与最新版本的 Windows 兼容。

如果此检查成功，则已在设备上正确配置评估程序组件。

否则，可能会显示以下错误之一：

- 无法配置设备应用兼容性数据收集 (SetRequestAllAppraiserVersions)。 检查日志中是否有异常详细信息  

- 无法配置设备应用兼容性数据收集 (SetRequestAllAppraiserVersions)。 检查日志中是否有异常详细信息  

- 无法将 RequestAllAppraiserVersions 写入注册表项 `HKLM:\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\AppCompatFlags\Appraiser`。 检查权限  

检查此注册表项的权限。 确保本地系统帐户可以访问此项，以便 Configuration Manager 客户端进行设置。  

有关详细信息，请查看客户端上的 M365AHandler.log。  

### <a name="minimum-compatibility-update"></a>最低兼容性更新

<!--18,19,32-->
兼容性更新 (appraiser.dll) 未安装在设备上或已过期。 它低于桌面分析的最低版本要求 10.0.17763。

安装最新的兼容性更新。 有关详细信息，请参阅[兼容性更新](enroll-devices.md#update-devices)。

### <a name="appraiser-version"></a>评估程序版本

此属性显示设备上的评估程序组件的当前版本。 它显示 `%windir%\System32\appraiser.dll` 上的文件版本（不带小数点）。 例如，文件版本 10.0.17763 显示为 10017763。

### <a name="last-successful-full-run-of-appraiser"></a>评估程序的上次成功完全运行

此属性显示设备上一次成功运行评估程序的日期和时间。

### <a name="appraiser-data-collection"></a>评估程序数据收集

<!--Appraiser run status-->
<!--22,33-->
此属性显示 Windows 运行评估程序组件的最新结果。

如果不成功，它可能会显示以下错误之一：

- 无法收集应用兼容性数据 (RunAppraiser)。 查看日志以获取详细信息  

- 应用兼容性数据收集 (CompatTelRunner.exe) 以错误代码结束  

有关详细信息，请查看客户端上的 M365AHandler.log。

检查以下文件：`%windir%\System32\CompatTelRunner.exe`。 如果文件不存在，请重新安装所需的[兼容性更新](enroll-devices.md#update-devices)。 确保没有其他系统组件（如组策略或反恶意软件服务）正在删除此文件。

如果客户端上的 M365AHandler.log 文件包含以下错误之一：

``` Log
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x800703F1
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80070005
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80080005
```

若要帮助修正这些错误，请在受影响的客户端上从提升的 Windows PowerShell 控制台运行以下命令：

```PowerShell
# stop associated services
Stop-Service -Name diagtrack #Connected User Experiences and Telemetry
Stop-Service -Name pcasvc #Program Compatibility Assistant Service
Stop-Service -Name dps #Diagnostic Policy Service

# regenerate diagnostic data cache
Remove-Item -Path $Env:WinDir\appcompat\programs\amcache.hve
Remove-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags" -Name AmiHivePermissionsCorrect -Force

# set ASL logging level to output log files in %windir%\temp
New-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags" -Name LogFlags -Value 4 -PropertyType DWord -Force

# restart services
Start-Service -Name diagtrack
Start-Service -Name pcasvc
Start-Service -Name dps
```

### <a name="last-successful-full-run-of-census"></a>统计的上次成功完全运行

此属性显示设备上一次成功运行统计的日期和时间。

### <a name="census-data-collection"></a>统计数据收集

<!-- Census run status -->
<!--51,52-->
统计是对设备进行清点的 Windows 组件。 此清单数据用于了解设备及其配置。

此属性显示 Windows 运行统计组件的最新结果。

如果不成功，它可能会显示以下错误之一：

- 无法收集有关设备及其配置的数据 (RunCensus)。 检查日志中是否有异常详细信息  

- 找不到设备和配置数据收集工具 (devicecensus.exe)  

有关详细信息，请查看客户端上的 M365AHandler.log。

检查以下文件：`%windir%\System32\DeviceCensus.exe`。 如果文件不存在，请重新安装所需的[兼容性更新](enroll-devices.md#update-devices)。 确保没有其他系统组件（如组策略或反恶意软件服务）正在删除此文件。

### <a name="windows-diagnostic-endpoint-connectivity"></a>Windows 诊断终结点连接

<!--12,15-->
如果此检查成功，则设备可以连接到“已连接的用户体验和遥测”终结点 (Vortex)。

否则，可能会显示以下错误之一：  

- 无法连接到“已连接的用户体验和遥测”终结点 (Vortex)。 检查网络/代理设置  

- 无法检查与“已连接的用户体验和遥测”终结点的连接(CheckVortexConnectivity)。 检查日志中是否有异常详细信息  

设备基于 OS 版本验证是否已通过 GET 请求连接到以下终结点：

| OS 版本 | 终结点 |
|------------|----------|
| - Windows 10，版本 1809 或更高版本<br/>- Windows 10，版本 1803，带有 2018-09 或更高版本的累积更新 | `https://v10c.events.data.microsoft.com/health/keepalive` |
| Windows 10，版本 1803，不带  2018-09 或更高版本的累积更新 | `https://v10.events.data.microsoft.com/health/keepalive` |
| Windows 10，版本 1709 或更高版本 | `https://v10.vortex-win.data.microsoft.com/health/keepalive` |
| Windows 7 或 Windows 8.1 | `https://vortex-win.data.microsoft.com/health/keepalive` |

确保设备可以与服务通信。 此检查将验证某些（但不是全部）所需的终结点。 有关详细信息，请参阅[终结点](enable-data-sharing.md#endpoints)。  

有关详细信息，请查看客户端上的 M365AHandler.log。  

### <a name="check-end-user-diagnostic-data"></a>检查最终用户诊断数据

<!--1004-->
如果此检查不成功，则用户在设备上选择了较低版本的 Windows 诊断数据。 它也可能由冲突的组策略对象引起。 有关详细信息，请参阅 [Windows 设置](enroll-devices.md#windows-settings)。

根据你的业务需求，可以通过组策略禁用用户选择。 使用此设置**配置遥测选择加入设置用户界面**。 有关详细信息，请参阅[配置组织中的 Windows 诊断数据](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management)。

### <a name="check-user-proxy"></a>检查用户代理

<!--30,35-->
默认情况下，为 Windows 7 启用了 DisableEnterpriseAuthProxy 设置。 对于 Windows 8.1 计算机，Configuration Manager 将 DisableEnterpriseAuthProxy 设置为 0（未禁用）。

此属性可能会显示以下错误：

- 身份验证代理已启用。 在 `HKLM\Software\Policies\Microsoft\Windows\DataCollection` 中将 DisableEnterpriseAuthProxy 设置为 0

- 无法检查身份验证代理状态。 检查日志中是否有异常详细信息

有关详细信息，请查看客户端上的 M365AHandler.log。  

检查此注册表项的权限。 确保本地系统帐户可以访问此项，以便 Configuration Manager 客户端进行设置。 它也可能由冲突的组策略对象引起。 有关详细信息，请参阅 [Windows 设置](enroll-devices.md#windows-settings)。  

### <a name="commercial-id-configuration"></a>商业 ID 配置

<!--9, 11, 53-->
Microsoft 使用唯一商业 ID 将设备中的信息映射到桌面分析工作区。 将 Configuration Manager 与桌面分析集成时，它会自动查询该 ID 的服务。 Configuration Manager 应自动将此 ID 应用于桌面分析设置所针对的客户端。

如果此检查成功，则已使用商业 ID 正确配置了设备。

否则，可能会显示以下错误之一：

- 无法将 CommercialId 写入注册表项 `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`。 检查权限  

- 无法更新注册表项 `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection` 中的 CommercialId。 检查日志中是否有异常详细信息  

- 在 `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection` 提供正确的 CommercialId 值  

有关详细信息，请查看客户端上的 M365AHandler.log。  

检查此注册表项的权限。 确保本地系统帐户可以访问此项，以便 Configuration Manager 客户端进行设置。 它也可能由冲突的组策略对象引起。 有关详细信息，请参阅 [Windows 设置](enroll-devices.md#windows-settings)。  

设备有不同的 ID。 此注册表项由组策略使用。 其优先级高于 Configuration Manager 提供的 ID。  

<a name="bkmk_ViewCommercialID"></a> 若要在桌面分析门户中查看商业 ID，请使用以下过程：

1. 转到桌面分析门户，在“全局设置”组中选择“连接服务”  。  

2. 在“连接服务”  窗格中，默认情况下“注册设备”  窗格处于选中状态。 在“注册设备”窗格中，“信息”部分显示你的商业 ID 项。  

[![桌面分析门户中商业 ID 的屏幕截图](media/commercial-id.png)](media/commercial-id.png#lightbox)

> [!Important]  
> 只有在无法使用当前 ID 项时，才获取新 ID 项  。 如果重新生成商业 ID，请 [使用新 ID 重新注册设备](enroll-devices.md#device-enrollment)。此过程可能会导致在过渡期间丢失诊断数据。  

### <a name="windows-commercial-data-opt-in"></a>Windows 商业数据选择加入

<!--64-->
此属性特定于运行 Windows 7 或 Windows 8.1 的设备。 它运行的测试与 [Windows 诊断数据选择加入](#windows-diagnostic-data-opt-in)类似（CommercialDataOptIn 值除外）。

### <a name="check-device-name-in-diagnostic-data"></a>检查诊断数据中的设备名称

<!--56,58-->
如果此检查成功，则设备已正确配置为共享设备名称。

否则，可能会显示以下错误之一：

- 无法检查作为 Windows 诊断数据的一部分发送给 Microsoft 的设备名称。 检查日志中是否有异常详细信息  

- 无法将 AllowDeviceNameInTelemetry 写入注册表项 `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`。 检查权限  

有关详细信息，请查看客户端上的 M365AHandler.log。  

检查此注册表项的权限。 确保本地系统帐户可以访问此项，以便 Configuration Manager 客户端进行设置。 它也可能由冲突的组策略对象引起。 有关详细信息，请参阅 [Windows 设置](enroll-devices.md#windows-settings)。  

确保其他策略机制（如组策略）未禁用此设置。

### <a name="diagtrack-service-configuration"></a>DiagTrack 服务配置

<!--44,45,50-->
如果此检查成功，则已在设备上正确配置 DiagTrack 组件。 桌面分析所需的最低版本为 10010586 (10.0.10586)。

否则，可能会显示以下错误之一：

- “已连接的用户体验和遥测”(diagtrack.dll) 组件已过时。 检查要求  

- 找不到“已连接的用户体验和遥测”(diagtrack.dll) 组件。 检查要求  

- 启用并启动“已连接的用户体验和遥测”服务以将数据发送给 Microsoft  

<!--
 - An updated Connected User Experience and Telemetry (diagtrack.dll) component is available. Check requirements - this is for the newer version that improves performance
 -->

<!--include something about diagtrack perf update https://go.microsoft.com/fwlink/?linkid=2011593-->

安装最新更新。 有关详细信息，请参阅[设备更新](enroll-devices.md#update-devices)。

确保设备上的“已连接的用户体验和遥测”服务正在运行  。

### <a name="diagtrack-version"></a>DiagTrack 版本

此属性显示设备上“已连接的用户体验和遥测”组件的当前版本。 它显示 `%windir%\System32\diagtrack.dll` 上的文件版本（不带小数点）。 例如，文件版本 10.0.10586 显示为 10010586。

### <a name="sqm-id-retrieval"></a>SQM ID 检索

<!--38-->
此属性主要用于 Windows 7 设备。 更高的操作系统版本可能会将其用作设备的回退标识符。

如果不成功，可能显示以下错误：

- 无法检索旧设备遥测标识符 (SQM ID)

有关详细信息，请查看客户端上的 M365AHandler.log。  

确保环境中没有重复的 ID。 例如，如果使用未通用化的 OS 映像部署设备。

### <a name="unique-device-identifier-retrieval"></a>唯一设备标识符检索

<!--54-->
桌面分析将 Microsoft 帐户服务用于更可靠的设备标识。

确保未禁用“Microsoft 帐户登录助手”  服务。 启动类型应为“手动（触发器启动）”  。

若要禁用最终用户 Microsoft 帐户访问权限，请使用策略设置，而不是阻止此终结点。 有关详细信息，请参阅[企业中的 Microsoft 帐户](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication)。

### <a name="windows-diagnostic-data-opt-in"></a>Windows 诊断数据选择加入

<!--8,40,55,62-->
此属性检查 Windows 是否已正确配置为允许诊断数据。 它将检查以下注册表项中的 AllowTelemetry 值：

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

检查对这些注册表项的权限。 确保本地系统帐户可以访问这些项，以便 Configuration Manager 客户端进行设置。 它也可能由冲突的组策略对象引起。 有关详细信息，请参阅 [Windows 设置](enroll-devices.md#windows-settings)。  

有关详细信息，请查看客户端上的 M365AHandler.log。  

## <a name="see-also"></a>另请参阅

[桌面分析疑难解答](troubleshooting.md)
