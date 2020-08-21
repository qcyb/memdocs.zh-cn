---
title: 启用数据共享
titleSuffix: Configuration Manager
description: 使用桌面分析共享诊断数据的参考指南。
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: be680198-4cea-4378-a686-d52f382ba483
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 40ebeabaaf236377388660a2a1a328e308a708ab
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125931"
---
# <a name="enable-data-sharing-for-desktop-analytics"></a>启用桌面分析的数据共享

若要将设备注册到桌面分析，需要将诊断数据发送给 Microsoft。 如果你的环境使用代理服务器，请使用此信息来帮助配置代理。

## <a name="diagnostic-data-levels"></a>诊断数据级别

:::image type="content" source="media/diagnostic-data-levels.png" alt-text="桌面分析的诊断数据级别关系图":::

将 Configuration Manager 与桌面分析集成时，还可以使用它来管理设备上的诊断数据级别。 为获得最佳体验，请使用 Configuration Manager。

> [!IMPORTANT]
> 在大多数情况下，仅使用 Configuration Manager 来配置这些设置。 也不要在域组策略对象中应用这些设置。 有关详细信息，请参阅[冲突解决](enroll-devices.md#conflict-resolution)。

桌面分析的基本功能在“必需”[诊断数据级别](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#diagnostic-data-levels)可用。 如果没有在 Configuration Manager 中配置“可选(受限)”级别，则无法使用以下桌面分析功能：

- 应用使用情况
- [其他 App Insights](compat-assessment.md#additional-insights)
- [部署状态数据](deploy-prod.md#address-deployment-alerts)
- [运行状况监视数据](health-status-monitoring.md)

Microsoft 建议为桌面分析启用“可选(受限)”诊断数据级别，以最大化你的受益。

> [!TIP]
> Configuration Manager 中的“可选(受限)”设置与运行 Windows 10 版本 1709 及更高版本的设备上可用的“将增强的诊断数据限制为 Windows Analytics 要求的最小值”策略设置相同。
>
> 运行 Windows 10 版本 1703 及更低版本、Windows 8.1 或 Windows 7 的设备没有此策略设置。 如果你在 Configuration Manager 中配置“可选(受限)”设置，这些设备会回退到“必需”级别。
>
> 运行 Windows 10 版本 1709 的设备具有此策略设置。 不过，如果你在 Configuration Manager 中配置“可选(受限)”设置，这些设备也会回退到“必需”级别。
>
> 在 Configuration Manager 版本 2002 及更低版本中，这些设置的名称不同：<!-- 7363467 -->
>
> | 版本 2006 及更高版本 | 版本 2002 及更低版本 |
> |---------|---------|
> | 必需 | 基本版 |
> | 可选(受限) | 增强(受限) |
> | 空值 | 增强版 |
> | 可选 | 完全 |
>
> 如果你之前在“增强”级别配置过任何设备，那么当你升级到版本 2006 时，这些设备将恢复为“可选(受限)”。 然后，它们将向 Microsoft 发送更少的数据。 此更改应该不会影响桌面分析中显示的内容。

若要详细了解使用“可选(受限)”与 Microsoft 共享的诊断数据，请参阅 [Windows 10 增强的诊断数据事件和字段](https://docs.microsoft.com/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields)。

> [!IMPORTANT]
> Microsoft 坚定地承诺提供用于让你自己控制隐私的工具和资源。 因此，尽管桌面分析支持 Windows 8.1 设备，但 Microsoft 不会从欧洲国家/地区（EEA 和瑞士）的 Windows 8.1 设备中收集 Windows 诊断数据。

有关详细信息，请参阅[桌面分析隐私](privacy.md)。

以下文章也可让你更好地了解 Windows 诊断数据级别：

- [Windows 10 和 GDPR：面向 IT 决策者的信息](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance)  

- [配置组织中的 Windows 诊断数据](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

> [!NOTE]
> 配置为发送“可选(受限)”诊断数据的客户端将在初始完全扫描完成后向 Microsoft 云发送大约 2MB 的数据。 每日增量在 250-400 KB 之间变化。
>
> 每日增量扫描发生在上午3:00（设备本地时间）。 某些事件会在一天中的第一个可用时间发送。 这些时间不可配置。
>
> 有关详细信息，请参阅[配置组织中的 Windows 诊断数据](https://aka.ms/enterprisetelemetry)。  

## <a name="endpoints"></a>终结点

要启用数据共享，请将代理服务器配置为允许以下 Internet 终结点。

> [!IMPORTANT]
> 对于隐私和数据完整性，Windows 在与诊断数据终结点通信时检查 Microsoft SSL 证书（证书固定）。 无法进行 SSL 拦截和检查。 若要使用桌面分析，请从 SSL 检查中排除这些终结点。<!-- BUG 4647542 -->

从版本 2002 开始，如果 Configuration Manager 站点无法连接到云服务所需的终结点，则会引发严重状态消息 ID 11488。 当无法连接到服务时，SMS_SERVICE_CONNECTOR 组件状态将更改为严重。 在 Configuration Manager 控制台的[“组件状态”](../core/servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus)节点中查看详细状态。<!-- 5566763 -->

> [!NOTE]
> 有关 Microsoft IP 地址范围的详细信息，请参阅 [Microsoft 公共 IP 空间](https://www.microsoft.com/download/details.aspx?id=53602)。 这些地址会定期更新。 服务没有粒度，可以使用这些范围内的任何 IP 地址。

[!INCLUDE [Internet endpoints for Desktop Analytics](../core/plan-design/network/includes/internet-endpoints-desktop-analytics.md)]

## <a name="proxy-server-authentication"></a>代理服务器身份验证

如果你的组织使用代理服务器身份验证进行 Internet 访问，请确保它不会因为身份验证而阻止诊断数据。 如果你的代理不允许设备发送此数据，则它们不会显示在桌面分析中。

### <a name="bypass-recommended"></a>免验证（推荐）

将代理服务器配置为不要求对诊断数据终结点的流量进行代理身份验证。 此选项是最全面的解决方案。 适用于所有 Windows 10 版本。  

### <a name="user-proxy-authentication"></a>用户代理身份验证

将设备配置为使用登录用户的上下文进行代理身份验证。 此方法需要以下配置：

- 设备具有受支持的 Windows 版本的最新质量更新

- 在 Windows 设置的“网络和 Internet”组中的“代理设置”中配置用户级代理（WinINET 代理）。 还可以使用旧版”Internet 选项”控制面板。

- 确保用户拥有访问诊断数据终结点的代理权限。 此选项要求设备具有拥有代理权限的控制台用户，因此无法将此方法用于无外设设备。

> [!IMPORTANT]
> 用户代理身份验证方法与使用 Microsoft Defender 高级威胁防护不兼容。 出现此行为是因为，此身份验证依赖于设置为 `0` 的 DisableEnterpriseAuthProxy 注册表项，而 Microsoft Defender ATP 要求将其设置为 `1`。 有关详细信息，请参阅[在 Microsoft Defender ATP 中配置计算机代理和 Internet 连接设置](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/configure-proxy-internet-windows-defender-advanced-threat-protection)。

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
