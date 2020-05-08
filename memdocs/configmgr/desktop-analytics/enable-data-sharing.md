---
title: 启用数据共享
titleSuffix: Configuration Manager
description: 使用桌面分析共享诊断数据的参考指南。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: be680198-4cea-4378-a686-d52f382ba483
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f8dd7c4c561ca22c679ee8ae03764ebb20b87664
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906088"
---
# <a name="enable-data-sharing-for-desktop-analytics"></a>启用桌面分析的数据共享

若要将设备注册到桌面分析，需要将诊断数据发送给 Microsoft。 如果你的环境使用代理服务器，请使用此信息来帮助配置代理。

## <a name="diagnostic-data-levels"></a>诊断数据级别

![桌面分析的诊断数据级别关系图](media/diagnostic-data-levels.png)

将 Configuration Manager 与桌面分析集成时，还可以使用它来管理设备上的诊断数据级别。 为获得最佳体验，请使用 Configuration Manager。

> [!Important]  
> 在大多数情况下，仅使用 Configuration Manager 来配置这些设置。 也不要在域组策略对象中应用这些设置。 有关详细信息，请参阅[冲突解决](enroll-devices.md#conflict-resolution)。

桌面分析的基础功能以基本的[诊断数据级别](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#diagnostic-data-levels)进行工作  。 如果未在 Configuration Manager 中配置“增强(受限)”级别，则不会获得桌面分析的以下功能  ：

- 应用使用情况
- [其他 App Insights](compat-assessment.md#additional-insights)
- 部署状态数据
- 运行状况监视数据

Microsoft 建议使用桌面分析来启用“增强(受限)”诊断数据级别以从中获得最大好处  。

> [!Tip]
> Configuration Manager 中的“增强(受限)”设置与运行 Windows 10 版本 1709 及更高版本的设备上可用的“将增强的诊断数据限制为 Windows Analytics 要求的最小值”策略设置相同   。
>
> 运行 Windows 10 版本 1703 及更低版本、Windows 8.1 或 Windows 7 的设备没有此策略设置。 在 Configuration Manager 中配置“增强(受限)”设置时，这些设备会返回到“基本”级别   。
>
> 运行 Windows 10 版本 1709 的设备具有此策略设置。 但是，当在 Configuration Manager 中配置“增强(受限)”设置时，这些设备也会返回到“基本”级别   。

有关使用“增强(受限)”与 Microsoft 共享的诊断数据的详细信息，请参阅 [Windows 10 增强的诊断数据事件与字段](https://docs.microsoft.com/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields)  。

> [!Important]
> Microsoft 坚定地承诺提供用于让你自己控制隐私的工具和资源。 因此，尽管桌面分析支持 Windows 8.1 设备，但 Microsoft 不会从欧洲国家/地区（EEA 和瑞士）的 Windows 8.1 设备中收集 Windows 诊断数据。

有关详细信息，请参阅[桌面分析隐私](privacy.md)。

以下文章也可让你更好地了解 Windows 诊断数据级别：

- [Windows 10 和 GDPR：面向 IT 决策者的信息](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance)  

- [配置组织中的 Windows 诊断数据](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

> [!Note]  
> 在初始完全扫描时，配置为限制增强诊断数据的客户端将向 Microsoft 云发送大约 2 MB 的数据。 每日增量在 250-400 KB 之间变化。
>
> 每日增量扫描发生在上午3:00（设备本地时间）。 某些事件会在一天中的第一个可用时间发送。 这些时间不可配置。
>
> 有关详细信息，请参阅[配置组织中的 Windows 诊断数据](https://aka.ms/enterprisetelemetry)。  

## <a name="endpoints"></a>终结点

要启用数据共享，请将代理服务器配置为允许以下 Internet 终结点。

> [!Important]  
> 对于隐私和数据完整性，Windows 在与诊断数据终结点通信时检查 Microsoft SSL 证书（证书固定）。 无法进行 SSL 拦截和检查。 若要使用桌面分析，请从 SSL 检查中排除这些终结点。<!-- BUG 4647542 -->

从版本 2002 开始，如果 Configuration Manager 站点无法连接到云服务所需的终结点，则会引发严重状态消息 ID 11488。 当无法连接到服务时，SMS_SERVICE_CONNECTOR 组件状态将更改为严重。 在 Configuration Manager 控制台的[“组件状态”](../core/servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus)节点中查看详细状态。<!-- 5566763 -->

> [!NOTE]
> 有关 Microsoft IP 地址范围的详细信息，请参阅 [Microsoft 公共 IP 空间](https://www.microsoft.com/download/details.aspx?id=53602)。 这些地址会定期更新。 服务没有粒度，可以使用这些范围内的任何 IP 地址。

### <a name="server-connectivity-endpoints"></a>服务器连接终结点

服务连接点需要与以下终结点进行通信：

| 终结点  | 函数  |
|-----------|-----------|
| `https://aka.ms` | 用于查找服务 |
| `https://graph.windows.net` | 用于在将层次结构附加到桌面分析时自动检索 CommercialId 等设置（在 Configuration Manager 服务器角色上）。 有关详细信息，请参阅[配置站点系统服务器的代理](../core/plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server)。 |
| `https://*.manage.microsoft.com` | 用于使用桌面分析同步设备集合成员身份、部署计划和设备就绪状态（仅限在 Configuration Manager 服务器角色上）。 有关详细信息，请参阅[配置站点系统服务器的代理](../core/plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server)。 |

### <a name="user-experience-and-diagnostic-component-endpoints"></a>用户体验和诊断组件终结点

客户端设备需要与以下终结点进行通信：

| 终结点  | 函数  |
|-----------|-----------|
| `https://v10c.events.data.microsoft.com` | 已连接的用户体验和诊断组件终结点。 由运行安装了 2018-09 累积更新或更高版本的 Windows 10 版本 1809 或更高版本或版本 1803 的设备使用。 |
| `https://v10.events.data.microsoft.com` | 已连接的用户体验和诊断组件终结点。 由运行未安装 2018-09 累积更新的 Windows 10 版本 1803 的设备使用  。 |
| `https://v10.vortex-win.data.microsoft.com` | 已连接的用户体验和诊断组件终结点。 由运行 Windows 10 版本 1709 或更高版本的设备使用。 |
| `https://vortex-win.data.microsoft.com` | 已连接的用户体验和诊断组件终结点。 由运行 Windows 7 和 Windows 8.1 的设备使用 |

### <a name="client-connectivity-endpoints"></a>客户端连接终结点

客户端设备需要与以下终结点进行通信：

| 索引 | 终结点  | 函数  |
|-------|-----------|-----------|
| 1 | `https://settings-win.data.microsoft.com` | 启用兼容性更新以将数据发送到 Microsoft。 |
| 2 | `http://adl.windows.com` | 允许兼容性更新以从 Microsoft 接收最新的兼容性数据。 |
| 3 | `https://watson.telemetry.microsoft.com` | [Windows 错误报告 (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting)。 需要在 Windows 10 版本 1803 或更低版本中监视部署运行状况。 |
| 4 | `https://umwatsonc.events.data.microsoft.com` | [Windows 错误报告 (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting)。 Windows 10 版本 1809 或更高版本中的设备运行状况报告所必需的。 |
| 5 | `https://ceuswatcab01.blob.core.windows.net` | [Windows 错误报告 (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting)。 需要在 Windows 10 版本 1809 或更高版本中监视部署运行状况。 |
| 6 | `https://ceuswatcab02.blob.core.windows.net` | [Windows 错误报告 (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting)。 需要在 Windows 10 版本 1809 或更高版本中监视部署运行状况。 |
| 7 | `https://eaus2watcab01.blob.core.windows.net` | [Windows 错误报告 (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting)。 需要在 Windows 10 版本 1809 或更高版本中监视部署运行状况。 |
| 8 | `https://eaus2watcab02.blob.core.windows.net` | [Windows 错误报告 (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting)。 需要在 Windows 10 版本 1809 或更高版本中监视部署运行状况。 |
| 9 | `https://weus2watcab01.blob.core.windows.net` | [Windows 错误报告 (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting)。 需要在 Windows 10 版本 1809 或更高版本中监视部署运行状况。 |
| 10 | `https://weus2watcab02.blob.core.windows.net` | [Windows 错误报告 (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting)。 需要在 Windows 10 版本 1809 或更高版本中监视部署运行状况。 |
| 11 | `https://kmwatsonc.events.data.microsoft.com` | [联机崩溃分析 (OCA)](https://docs.microsoft.com/windows/win32/dxtecharts/crash-dump-analysis)。 Windows 10 版本 1809 或更高版本中的设备运行状况报告所必需的。 |
| 12 | `https://oca.telemetry.microsoft.com`  | [联机崩溃分析 (OCA)](https://docs.microsoft.com/windows/win32/dxtecharts/crash-dump-analysis)。 需要在 Windows 10 版本 1803 或更低版本中监视部署运行状况。 |
| 13 | `https://login.live.com` | 需要为桌面分析提供更可靠的设备标识。 <br> <br>若要禁用最终用户 Microsoft 帐户访问权限，请使用策略设置，而不是阻止此终结点。 有关详细信息，请参阅[企业中的 Microsoft 帐户](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication)。 |
| 14 | `https://v20.events.data.microsoft.com` | 已连接的用户体验和诊断组件终结点。 |

## <a name="proxy-server-authentication"></a>代理服务器身份验证

如果你的组织使用代理服务器身份验证进行 Internet 访问，请确保它不会因为身份验证而阻止诊断数据。 如果你的代理不允许设备发送此数据，则它们不会显示在桌面分析中。

### <a name="bypass-recommended"></a>免验证（推荐）

将代理服务器配置为不要求对诊断数据终结点的流量进行代理身份验证。 此选项是最全面的解决方案。 适用于所有 Windows 10 版本。  

### <a name="user-proxy-authentication"></a>用户代理身份验证

将设备配置为使用登录用户的上下文进行代理身份验证。 此方法需要以下配置：

- 设备具有受支持的 Windows 版本的最新质量更新

- 在 Windows 设置的“网络和 Internet”组中的“代理设置”中配置用户级代理（WinINET 代理）  。 还可以使用旧版”Internet 选项”控制面板。

- 确保用户拥有访问诊断数据终结点的代理权限。 此选项要求设备具有拥有代理权限的控制台用户，因此无法将此方法用于无外设设备。

> [!IMPORTANT]
> 用户代理身份验证方法与使用 Microsoft Defender 高级威胁防护不兼容。 出现此行为是因为，此身份验证依赖于设置为 `0` 的 DisableEnterpriseAuthProxy 注册表项，而 Microsoft Defender ATP 要求将其设置为 `1` 。 有关详细信息，请参阅[在 Microsoft Defender ATP 中配置计算机代理和 Internet 连接设置](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/configure-proxy-internet-windows-defender-advanced-threat-protection)。

### <a name="device-proxy-authentication"></a>设备代理身份验证

此方法支持以下方案：

- 无外设的设备，其中无用户进行登录或该设备的用户无法访问 Internet

- 不使用 Windows 集成身份验证的经验证的代理

- 如果你同时还使用了 Microsoft Defender 高级威胁防护

此方法是最复杂的方法，因为它需要以下配置：

- 确保设备可以通过 WinHTTP 在本地系统上下文中访问代理服务器。 使用下列选项之一来配置此行为：

  - 命令行 `netsh winhttp set proxy`

  - Web 代理自动发现 (WPAD) 协议

  - 透明代理

  - 使用以下组策略设置配置设备范围内的 WinINET 代理：**按每台计算机（而不是每个用户）配置代理设置** (ProxySettingsPerUser = `1`)

  - 路由的连接，或使用网络地址转换 (NAT) 的连接

- 配置代理服务器以允许 Active Directory 中的计算机帐户访问诊断数据终结点。 此配置要求代理服务器支持 Windows 集成身份验证。  
