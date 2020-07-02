---
title: Internet 访问要求
titleSuffix: Configuration Manager
description: 了解允许使用 Configuration Manager 功能的完整功能的 Internet 终结点。
ms.date: 06/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b34fe701-5d05-42be-b965-e3dccc9363ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fb965ec6547ff1c06586464780b6db224b943000
ms.sourcegitcommit: 9a8a9cc7dcb6ca333b87e89e6b325f40864e4ad8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2020
ms.locfileid: "84740755"
---
# <a name="internet-access-requirements"></a>Internet 访问要求

某些 Configuration Manager 功能依赖 Internet 连接来获取完整功能。 如果组织使用防火墙或代理设备限制与 Internet 的网络通信，请确保允许使用这些终结点。

<!-- SCCMDocs-pr #3403 -->

## <a name="service-connection-point"></a><a name="bkmk_scp"></a>服务连接点

这些配置适用于托管服务连接点的计算机以及该计算机与 Internet 之间的任何防火墙。 它们都必须允许通过 HTTPS 的传出端口“TCP 443”和 HTTP 的传出端口“TCP 80”与以下 Internet 位置传递通信 。

服务连接点支持使用 Web 代理（具有或不具有身份验证皆可）来使用这些位置。 有关详细信息，请参阅[代理服务器支持](proxy-server-support.md)。

有关服务连接点的详细信息，请参阅[关于服务连接点](../../servers/deploy/configure/about-the-service-connection-point.md)。

其他 Configuration Manager 功能可能需要来自服务连接点的其他终结点。 有关详细信息，请参阅本文中的其他部分。

> [!TIP]  
> 服务连接点在连接到 `go.microsoft.com` 或 `manage.microsoft.com` 时使用 Microsoft Intune 服务。 存在以下已知问题：如果未在服务连接点上安装 Baltimore CyberTrust 根证书、该证书已过期或损坏，则 Intune 连接器会遇到连接问题。 有关详细信息，请参阅 [KB 3187516：服务连接点不下载更新](https://support.microsoft.com/help/3187516)。  

从版本 2002 开始，如果 Configuration Manager 站点无法连接到云服务所需的终结点，则会引发严重状态消息 ID 11488。 当无法连接到服务时，SMS_SERVICE_CONNECTOR 组件状态将更改为严重。 在 Configuration Manager 控制台的[“组件状态”](../../servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus)节点中查看详细状态。<!-- 5566763 -->

### <a name="updates-and-servicing"></a><a name="bkmk_scp-updates"></a> 更新和服务

有关该功能的详细信息，请参阅 [Configuration Manager 的更新和服务](../../servers/manage/updates.md)。

> [!Tip]  
> 为[管理见解](../../servers/manage/management-insights.md)规则（即，将站点连接到 Microsoft 云来实现 Configuration Manager 更新）启用这些终结点。

- `*.akamaiedge.net`  

- `*.akamaitechnologies.com`  

- `*.manage.microsoft.com`  

- `go.microsoft.com`  

- `*.blob.core.windows.net`  

- `download.microsoft.com`  

- `download.windowsupdate.com`  

- `sccmconnected-a01.cloudapp.net`  

- `configmgrbits.azureedge.net`  

### <a name="windows-10-servicing"></a>Windows 10 维护服务

有关该功能的详细信息，请参阅[管理 Windows 即服务](../../../osd/deploy-use/manage-windows-as-a-service.md)。

- `download.microsoft.com`  

- `https://go.microsoft.com/fwlink/?LinkID=619849`  

- `dl.delivery.mp.microsoft.com`  

### <a name="azure-services"></a>Azure 服务

有关该功能的详细信息，请参阅[配置用于 Configuration Manager 的 Azure 服务](../../servers/deploy/configure/azure-services-wizard.md)。

- `management.azure.com`（Azure 公有云）
- `management.usgovcloudapi.net`（Azure 美国政府云）

## <a name="co-management"></a>共同管理

如果将 Windows 10 设备注册到 Microsoft Intune 以进行共同管理，请确保这些设备可以访问 Intune 所需的终结点。 有关详细信息，请参阅 [Microsoft Intune 的终结点](https://docs.microsoft.com/intune/intune-endpoints)。

## <a name="microsoft-store-for-business"></a>适用于企业的 Microsoft Store

如果将 Configuration Manager 与[适用于企业的 Microsoft Store](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md) 集成，请确保服务连接点和目标设备能够访问云服务。 有关详细信息，请参阅[适用于企业的 Microsoft Store 代理配置](https://docs.microsoft.com/microsoft-store/prerequisites-microsoft-store-for-business#proxy-configuration)。

## <a name="delivery-optimization"></a>传递优化

如果使用传递优化，则客户端需要与其云服务 `*.do.dsp.mp.microsoft.com` 进行通信

支持 Microsoft 连接缓存的分发点也需要这些终结点。

有关详细信息，请参阅下列文章：

- [传递优化常见问题解答](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions)
- [Configuration Manager 中内容管理的基本概念](../hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization)
- [Configuration Manager 中的 Microsoft Connected Cache](../hierarchy/microsoft-connected-cache.md)

## <a name="cloud-services"></a><a name="bkmk_cloud"></a> 云服务

<!-- SCCMDocs-pr #3402 -->

本部分介绍以下功能：

- 云管理网关 (CMG)
- 云分发点 (CDP)
- Azure Active Directory (Azure AD) 集成
- 基于 Azure AD 的发现

有关 CMG 的详细信息，请参阅 [CMG 规划](../../clients/manage/cmg/plan-cloud-management-gateway.md)。

以下部分按角色列出终结点。 某些终结点通过 `<name>`（这是 CMG 或 CDP 的云服务名称）引用服务。 例如，如果 CMG 为 `GraniteFalls.CloudApp.Net`，则实际存储终结点为 `GraniteFalls.blob.core.windows.net`。<!-- SCCMDocs#2288 -->

### <a name="service-connection-point"></a>服务连接点

对于 CMG/CDP 服务部署，服务连接点需要访问：

- 特定的 Azure 终结点因环境而异，具体取决于配置。 Configuration Manager 将这些终结点存储在站点数据库中。 查询 SQL Server 中的 AzureEnvironments 表以获取 Azure 终结点的列表。

- [Azure 服务](#azure-services)

- 对于 Azure AD 用户发现：

  - 1902 版及更高版本：Microsoft Graph 终结点 `https://graph.microsoft.com/`

  - 1810 版及更早版本：Azure AD Graph 终结点 `https://graph.windows.net/`  

### <a name="cmg-connection-point"></a>CMG 连接点

CMG 连接点需要访问以下服务终结点：

- 云服务名称（用于 CMG 或 CDP）：
  - `<name>.cloudapp.net`（Azure 公有云）
  - `<name>.usgovcloudapp.net`（Azure 美国政府云）

- 服务管理终结点：`https://management.core.windows.net/`  

- 存储终结点（用于启用内容的 CMG 或 CDP）：
  - `<name>.blob.core.windows.net`（Azure 公有云）
  - `<name>.blob.core.usgovcloudapi.net`（Azure 美国政府云）
<!--  and `<name>.table.core.windows.net` per DC, only used internally -->

CMG 连接点站点系统支持使用 Web 代理。 有关配置代理的此角色的详细信息，请参阅[代理服务器支持](proxy-server-support.md#configure-the-proxy-for-a-site-system-server)。 CMG 连接点仅需要连接到 CMG 服务终结点。 它不需要访问其他 Azure 终结点。

### <a name="configuration-manager-client"></a>Configuration Manager 客户端

- 云服务名称（用于 CMG 或 CDP）：
  - `<name>.cloudapp.net`（Azure 公有云）
  - `<name>.usgovcloudapp.net`（Azure 美国政府云）

- 存储终结点（用于启用内容的 CMG 或 CDP）：
  - `<name>.blob.core.windows.net`（Azure 公有云）
  - `<name>.blob.core.usgovcloudapi.net`（Azure 美国政府云）

- 对于 Azure AD 令牌检索，Azure AD 终结点：
  - `login.microsoftonline.com`（Azure 公有云）
  - `login.microsoftonline.us`（Azure 美国政府云）

### <a name="configuration-manager-console"></a>Configuration Manager 控制台

- 对于 Azure AD 令牌检索，Azure AD 终结点：

  - Azure 公有云
    - `login.microsoftonline.com`
    - `aadcdn.msauth.net`<!-- MEMDocs#351 -->
    - `aadcdn.msftauth.net`

  - Azure 美国政府云
    - `login.microsoftonline.us`

## <a name="software-updates"></a><a name="bkmk_sum"></a>软件更新

允许活动的软件更新点访问以下终结点，以便 WSUS 和自动更新可以与 Microsoft Update 云服务通信：  

- `http://windowsupdate.microsoft.com`  

- `http://*.windowsupdate.microsoft.com`  

- `https://*.windowsupdate.microsoft.com`  

- `http://*.update.microsoft.com`  

- `https://*.update.microsoft.com`  

- `http://*.windowsupdate.com`  

- `http://download.windowsupdate.com`  

- `http://download.microsoft.com`  

- `http://*.download.windowsupdate.com`  

- `http://test.stats.update.microsoft.com`  

- `http://ntservicepack.microsoft.com`  

有关软件更新的详细信息，请参阅[规划软件更新](../../../sum/plan-design/plan-for-software-updates.md)。

### <a name="intranet-firewall"></a>Intranet 防火墙

在以下情况下，你可能需要将终结点添加到两个站点系统之间的防火墙：

- 如果子站点具有软件更新点
- 如果站点上具有基于 Internet 的远程活动软件更新点

#### <a name="software-update-point-on-the-child-site"></a>子站点上的软件更新点

- `http://<FQDN for software update point on child site>`  

- `https://<FQDN for software update point on child site>`  

- `http://<FQDN for software update point on parent site>`  

- `https://<FQDN for software update point on parent site>`  

## <a name="manage-office-365"></a>管理 Office 365

> [!NOTE]
> 自 2020 年 4 月 21 日起，Office 365 专业增强版已重命名为 Microsoft 365 企业应用版。 有关详细信息，请参阅 [Office 365 专业增强版的名称变更](https://docs.microsoft.com/deployoffice/name-change)。 在控制台更新期间，你可能仍会看到 Configuration Manager 控制台和支持文档中引用的是旧名称。

如果使用 Configuration Manager 部署和更新 Microsoft 365 企业应用版，请允许以下终结点：

<!-- SCCMDocs#929 -->

- `officecdn.microsoft.com`，用于为企业客户端更新同步 Microsoft 365 企业应用版的软件更新点

- `config.office.com`，用于为企业部署创建 Microsoft 365 企业应用版的自定义配置

## <a name="configuration-manager-console"></a>Configuration Manager 控制台

具有 Configuration Manager 控制台的计算机需要访问以下 Internet 终结点获取特定功能：

### <a name="in-console-feedback"></a>控制台内反馈

- `http://petrol.office.microsoft.com`

有关此功能的详细信息，请参阅[产品反馈](../../understand/find-help.md#product-feedback)。

### <a name="community-workspace"></a>社区工作区

#### <a name="documentation-node"></a>文档节点

有关此控制台节点的详细信息，请参阅[使用 Configuration Manager 控制台](../../servers/manage/admin-console.md)。

- `https://aka.ms`

- `https://raw.githubusercontent.com`

#### <a name="community-hub"></a>社区中心

有关此功能的详细信息，请参阅[社区中心](../../servers/manage/community-hub.md)。

- `https://github.com`

- `https://communityhub.microsoft.com`

### <a name="monitoring-workspace-site-hierarchy-node"></a>“监视”工作区、“站点层次结构”节点

如果你使用“地理视图”，则允许访问以下终结点：

- `http://maps.bing.com`

## <a name="desktop-analytics"></a>桌面分析

有关桌面分析云服务所需终结点的详细信息，请参阅[启用数据共享](../../../desktop-analytics/enable-data-sharing.md#endpoints)。

## <a name="microsoft-public-ip-addresses"></a>Microsoft 公共 IP 地址

有关 Microsoft IP 地址范围的详细信息，请参阅 [Microsoft 公共 IP 空间](https://www.microsoft.com/download/details.aspx?id=53602)。 这些地址会定期更新。 服务没有粒度，可以使用这些范围内的任何 IP 地址。

## <a name="see-also"></a>另请参阅

- [Configuration Manager 中使用的端口](../hierarchy/ports.md)

- [Configuration Manager 中的代理服务器支持](proxy-server-support.md)
