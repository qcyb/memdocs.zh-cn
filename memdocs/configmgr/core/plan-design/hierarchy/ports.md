---
title: 用于连接的端口
titleSuffix: Configuration Manager
description: 了解有关 Configuration Manager 用于连接的必需的和可自定义网络端口。
ms.date: 04/29/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c6777fb0-0754-4abf-8a1b-7639d23e9391
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2495c0d7b5b19b5d6f7741d3b28b6a9a0e213fc3
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700140"
---
# <a name="ports-used-in-configuration-manager"></a>Configuration Manager 中使用的端口

适用范围：  Configuration Manager (Current Branch)

本文列出了 Configuration Manager 使用的网络端口。 某些连接使用不可配置的端口，而某些连接支持指定的自定义端口。 如果使用任何端口筛选技术，请验证所需端口是否可用。 这些端口筛选技术包括防火墙、路由器、代理服务器或 IPsec。

> [!NOTE]  
> 如果通过 SSL 桥接支持基于 Internet 的客户端，则除了满足端口要求，可能还必须允许某些 HTTP 谓词和标头遍历防火墙。

## <a name="ports-you-can-configure"></a><a name="BKMK_ConfigurablePorts"></a> 你可以配置的端口：

Configuration Manager 可用于为以下通信类型配置端口：  

- 应用程序目录网站点到应用程序目录 Web 服务点  

- 注册代理点到注册点  

- 运行 IIS 的客户端到站点系统  

- 客户端到 Internet（作为代理服务器设置）  

- 软件更新点到 Internet（作为代理服务器设置）  

- 软件更新点到 WSUS 服务器  

- 站点服务器到站点数据库服务器  

- 站点服务器到 WSUS 数据库服务器

- Reporting Services 点  

  > [!NOTE]  
  > 在 SQL Server Reporting Services 中，配置用于 Reporting Services 点站点系统角色的端口。 之后，Configuration Manager 会在与 Reporting Services 点通信时使用这些端口。 请务必查看为 IPsec 策略或为配置防火墙定义 IP 筛选器信息的端口。  

默认情况下，客户端到站点系统通信所用的 HTTP 端口是端口 80，默认的 HTTPS 端口是 443。 在安装期间或在 Configuration Manager 站点的“站点属性”中，可更改通过 HTTP 或 HTTPS 进行客户端到站点系统通信的端口。  

在 SQL Server Reporting Services 中，配置用于 Reporting Services 点站点系统角色的端口。 之后，Configuration Manager 会在与 Reporting Services 点通信时使用这些端口。 请务必查看为 IPsec 策略或为配置防火墙定义 IP 筛选器信息时所用的端口。  

## <a name="non-configurable-ports"></a><a name="BKMK_NonConfigurablePorts"></a> 不可配置的端口  

Configuration Manager 不允许为以下通信类型配置端口：  

- 站点到站点  

- 站点服务器到站点系统  

- Configuration Manager 控制台到 SMS 提供程序  

- Configuration Manager 控制台到 Internet  

- 与云服务的连接，例如 Microsoft Intune 和云分发点  

## <a name="ports-used-by-configuration-manager-clients-and-site-systems"></a><a name="BKMK_CommunicationPorts"></a> Configuration Manager 客户端和站点系统使用的端口  

下列章节详述了 Configuration Manager 中用于通信的端口。 章节标题中的箭头显示通信的方向：  

- --> 表明一台计算机开始通信，另一台计算机始终响应  

- &lt;--> 表明任一计算机均可开始通信  

### <a name="asset-intelligence-synchronization-point----microsoft"></a><a name="BKMK_PortsAI"></a> 资产智能同步点 --> Microsoft  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

### <a name="asset-intelligence-synchronization-point----sql-server"></a><a name="BKMK_PortsAI-to-SQL"></a> 资产智能同步点 --> SQL Server  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 <sup>[备注 2](#bkmk_note2) 可用的备用端口</sup>|  

### <a name="application-catalog-web-service-point----sql-server"></a><a name="BKMK_PortsAppCatalogService-SQL"></a>应用程序目录 Web 服务点 --> SQL Server  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 <sup>[备注 2](#bkmk_note2) 可用的备用端口</sup>|  

### <a name="application-catalog-website-point----application-catalog-web-service-point"></a><a name="BKMK_PortsAppCatalogWebSitePoint_AppCatalogWebServicePoint"></a> 应用程序目录网站点 --> 应用程序目录 Web 服务点  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[备注 2](#bkmk_note2) 可用的备用端口</sup>|  
|HTTPS|--|443 <sup>[备注 2](#bkmk_note2) 可用的备用端口</sup>|  

### <a name="client----application-catalog-website-point"></a><a name="BKMK_PortsClient-AppCatalogWebsitePoint"></a> 客户端 --> 应用程序目录网站点  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[备注 2](#bkmk_note2) 可用的备用端口</sup>|  
|HTTPS|--|443 <sup>[备注 2](#bkmk_note2) 可用的备用端口</sup>|  

### <a name="client----client"></a><a name="BKMK_PortsClient-ClientWakeUp"></a> 客户端 --> 客户端  

唤醒代理还使用从一个客户端发送到另一个客户端的 ICMP 回显请求消息。 客户端使用此通信确认网络上的另一台客户端是否处于唤醒状态。 ICMP 有时称为 ping 命令。 ICMP 没有 UDP 或 TCP 协议号，因此未在下表中列出。 但是，这些客户端计算机或者子网中的介入性网络设备上的任何基于主机的防火墙都必须允许 ICMP 流量，以便成功进行唤醒代理通信。  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|LAN 唤醒|9 <sup>[备注 2](#bkmk_note2) 可用的备用端口</sup>|--|  
|唤醒代理|25536 <sup>[备注 2](#bkmk_note2) 可用的备用端口</sup>|--|  
|Windows PE 对等缓存广播|8004|--|  
|Windows PE 对等缓存下载|--|8003|  

有关详细信息，请参阅 [Windows PE 对等缓存](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md#BKMK_PeerCacheRequirements)。

### <a name="client----configuration-manager-network-device-enrollment-service-ndes-policy-module"></a><a name="BKMK_PortsClient-PolicyModule"></a> 客户端--> Configuration Manager 网络设备注册服务 (NDES) 策略模块

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP||80|  
|HTTPS|--|443|  

### <a name="client----cloud-distribution-point"></a><a name="BKMK_PortsClient-CloudDP"></a> 客户端 --> 云分发点  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

有关详细信息，请参阅[端口和数据流](use-a-cloud-based-distribution-point.md#bkmk_dataflow)。

### <a name="client----cloud-management-gateway-cmg"></a><a name="bkmk_client-cmg"></a> 客户端 --> 云管理网关 (CMG)  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

有关详细信息，请参阅 [CMG 端口和数据流](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow)。

### <a name="client----distribution-point-both-standard-and-pull"></a><a name="BKMK_PortsClient-DP"></a> 客户端 --> 分发点（标准和拉取）  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[备注 2](#bkmk_note2) 可用的备用端口</sup>|  
|HTTPS|--|443 <sup>[备注 2](#bkmk_note2) 可用的备用端口</sup>|
|快速更新|--|8005 <sup>[备注 2](#bkmk_note2) 可用的备用端口</sup>|<!-- SCCMDocs#2091 -->

> [!NOTE]
> 使用客户端设置来配置快速更新的备用端口。 有关详细信息，请参阅[客户端用于接收增量内容请求的端口](../../clients/deploy/about-client-settings.md#port-that-clients-use-to-receive-requests-for-delta-content)。

### <a name="client----distribution-point-configured-for-multicast-both-standard-and-pull"></a><a name="BKMK_PortsClient-DP2"></a> 客户端 --> 配置进行多播的分发点（标准和拉取）  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|服务器消息块 (SMB)|--|445|  
|多播协议|63000-64000|--|  

### <a name="client----distribution-point-configured-for-pxe-both-standard-and-pull"></a><a name="BKMK_PortsClient-DP3"></a> 客户端 --> 为 PXE 配置的分发点（标准和拉取）  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|DHCP|67 和 68|--|  
|TFTP|69 <sup>[备注 4](#bkmk_note4)</sup> |--|  
|启动信息协商层 (BINL)|4011|--|  

> [!Important]  
> 若启用基于主机的防火墙，请确保规则允许服务器在这些端口上进行发送和接收。 为 PXE 启用分发点时，Configuration Manager 可在 Windows 防火墙上启用入站（接收）规则。 它不会配置出站（发送）规则。<!--SCCMDocs issue #744-->  

### <a name="client----fallback-status-point"></a><a name="BKMK_PortsClient-FSP"></a> 客户端 --> 回退状态点  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[备注 2](#bkmk_note2) 可用的备用端口</sup>|  

### <a name="client----global-catalog-domain-controller"></a><a name="BKMK_PortsClient-GCDC"></a> 客户端 --> 全局编录域控制器

如果 Configuration Manager 客户端是工作组计算机或者配置为仅限 Internet 通信，则该客户端不会联系全局目录服务器。  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|全局编录 LDAP|--|3268|  

### <a name="client----management-point"></a><a name="BKMK_PortsClient-MP"></a> 客户端 --> 管理点  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|客户端通知（在回退到 HTTP 或 HTTPS 之前的默认通信）|--|10123 <sup>[备注 2](#bkmk_note2) 可用的备用端口</sup>|  
|HTTP|--|80 <sup>[备注 2](#bkmk_note2) 可用的备用端口</sup>|  
|HTTPS|--|443 <sup>[备注 2](#bkmk_note2) 可用的备用端口</sup>|  

### <a name="client----software-update-point"></a><a name="BKMK_PortsClient-SUP"></a> 客户端 --> 软件更新点  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 或 8530 <sup>[备注 3](#bkmk_note3)</sup>|  
|HTTPS|--|443 或 8531 <sup>[备注 3](#bkmk_note3)</sup>|  

### <a name="client----state-migration-point"></a><a name="BKMK_PortsClient-SMP"></a> 客户端 --> 状态迁移点  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[备注 2](#bkmk_note2) 可用的备用端口</sup>|  
|HTTPS|--|443 <sup>[备注 2](#bkmk_note2) 可用的备用端口</sup>|  
|服务器消息块 (SMB)|--|445|  

### <a name="cmg-connection-point----cmg-cloud-service"></a><a name="bkmk_cmgcp-cmg"></a> CMG 连接点 --> CMG 云服务  

Configuration Manager 使用这些连接来构建 CMG 通道。 有关详细信息，请参阅 [CMG 端口和数据流](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow)。

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|TCP-TLS（首选）|--|10140-10155|  
|HTTPS（具有一个 VM 的回退）|--|443|  
|HTTPS（具有两个或以上的 VM 的回退）|--|10124-10139|  

### <a name="cmg-connection-point----management-point"></a><a name="bkmk_cmgcp-mp"></a> CMG 连接点 --> 管理点  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|

有关详细信息，请参阅 [CMG 端口和数据流](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow)。

### <a name="cmg-connection-point----software-update-point"></a><a name="bkmk_cmgcp-sup"></a> CMG 连接点 --> 软件更新点  

特定端口取决于软件更新点配置。

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|
|HTTP|--|80|  

有关详细信息，请参阅 [CMG 端口和数据流](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow)。

### <a name="configuration-manager-console----client"></a><a name="BKMK_PortsConsole-Client"></a> Configuration Manager 控制台 --> 客户端  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|远程控制（控制）|--|2701|  
|远程辅助（RDP 和 RTC）|--|3389|  

### <a name="configuration-manager-console----internet"></a><a name="BKMK_PortsConsole-Internet"></a>Configuration Manager 控制台 --> Internet  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80|  
|HTTPS|--|443|

Configuration Manager 控制台使用 Internet 访问获取以下操作：

- 从 Microsoft 更新下载部署软件包的软件更新。
- 功能区中的反馈项。
- 控制台内的文档链接。
<!--506823-->

### <a name="configuration-manager-console----reporting-services-point"></a><a name="BKMK_PortsConsole-RSP"></a> Configuration Manager 控制台 --> Reporting Services 点  

|说明|UDP|TCP|
|-----------------|---------|---------|
|HTTP|--|80 <sup>[备注 2](#bkmk_note2) 可用的备用端口</sup>|  
|HTTPS|--|443 <sup>[备注 2](#bkmk_note2) 可用的备用端口</sup>|  

### <a name="configuration-manager-console----site-server"></a><a name="BKMK_PortsConsole-Site"></a> Configuration Manager 控制台 --> 站点服务器  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|RPC（最初连接到 WMI，以找到提供程序系统）|--|135|  

### <a name="configuration-manager-console----sms-provider"></a><a name="BKMK_PortsConsole-Provider"></a> Configuration Manager 控制台 --> SMS 提供程序  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|RPC 终结点映射程序|135|135|  
|RPC|--|DYNAMIC <sup>[备注 6](#bkmk_note6)</sup>|  

### <a name="configuration-manager-network-device-enrollment-service-ndes-policy-module----certificate-registration-point"></a><a name="BKMK_PortsCertificateRegistationPoint_PolicyModule"></a> Configuration Manager 网络设备注册服务 (NDES) 策略模块 --> 证书注册点  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443 <sup>[备注 2](#bkmk_note2) 可用的备用端口</sup>|  

### <a name="data-warehouse-service-point----sql-server"></a><a name="BKMK_PortsDWSPSQL"></a> 数据仓库服务点 --> SQL Server  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 <sup>[备注 2](#bkmk_note2) 可用的备用端口</sup>|  

### <a name="distribution-point-both-standard-and-pull----management-point"></a><a name="BKMK_PortsDist_MP"></a> 分发点（标准和拉取）--> 管理点

在以下情况中，分发点向管理点通信：  

- 报告预留内容的状态  

- 报告使用情况摘要数据  

- 报告内容验证  

- 报告包下载的状态（仅拉取分发点）

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[备注 2](#bkmk_note2) 可用的备用端口</sup>|  
|HTTPS|--|443 <sup>[备注 2](#bkmk_note2) 可用的备用端口</sup>|  

### <a name="endpoint-protection-point----internet"></a><a name="BKMK_PortsEndpointProtection_Internet"></a>Endpoint Protection 点 --> Internet  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80|  

### <a name="endpoint-protection-point----sql-server"></a><a name="BKMK_PortsEP-to-SQL"></a> Endpoint Protection 点 --> SQL Server  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 <sup>[备注 2](#bkmk_note2) 可用的备用端口</sup>|  

### <a name="enrollment-proxy-point----enrollment-point"></a><a name="BKMK_PortsEnrollmentProxyEnrollmentPoint"></a> 注册代理点 --> 注册点  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443 <sup>[备注 2](#bkmk_note2) 可用的备用端口</sup>|  

### <a name="enrollment-point----sql-server"></a><a name="BKMK_PortsEnrollmentEnrollmentSQL"></a> 注册点 --> SQL Server  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 <sup>[备注 2](#bkmk_note2) 可用的备用端口</sup>|  

### <a name="exchange-server-connector----exchange-online"></a><a name="BKMK_PortsExchangeConnectorHosted"></a> Exchange Server 连接器 --> Exchange Online  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|通过 HTTPS 进行的 Windows 远程管理|--|5986|  

### <a name="exchange-server-connector----on-premises-exchange-server"></a><a name="BKMK_PortsExchangeConnectorOnPrem"></a> Exchange Server 连接器 --> 本地 Exchange Server  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|通过 HTTP 进行的 Windows 远程管理|--|5985|  

### <a name="mac-computer----enrollment-proxy-point"></a><a name="BKMK_PortsMacEnrollmentProxyPoint"></a> Mac 计算机 --> 注册代理点  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

### <a name="management-point----domain-controller"></a><a name="BKMK_PortsMP-DC"></a> 管理点 --> 域控制器  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|轻型目录访问协议 (LDAP)|389|389|  
|安全 LDAP（LDAPS，用于签名和绑定）|636|636|  
|全局编录 LDAP|--|3268|  
|RPC 终结点映射程序|--|135|  
|RPC|--|DYNAMIC <sup>[备注 6](#bkmk_note6)</sup>|  

### <a name="management-point-lt---site-server"></a><a name="BKMK_PortsMP-Site"></a> 管理点 &lt;--> 站点服务器

<sup>[备注 5](#bkmk_note5)</sup>

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|RPC 终结点映射程序|--|135|  
|RPC|--|DYNAMIC <sup>[备注 6](#bkmk_note6)</sup>|  
|服务器消息块 (SMB)|--|445|  

### <a name="management-point----sql-server"></a><a name="BKMK_PortsMP-SQL"></a> 管理点 --> SQL Server  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 <sup>[备注 2](#bkmk_note2) 可用的备用端口</sup>|  

### <a name="mobile-device----enrollment-proxy-point"></a><a name="BKMK_PortsMobileDeviceClient-EnrollmentProxyPoint"></a> 移动设备 --> 注册代理点  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

###  <a name="reporting-services-point----sql-server"></a><a name="BKMK_PortsRSP-SQL"></a> Reporting Services 点 --> SQL Server  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 <sup>[备注 2](#bkmk_note2) 可用的备用端口</sup>|  

### <a name="service-connection-point----azure-cmg"></a><a name="bkmk_scp-cmg"></a> 服务连接点 --> Azure (CMG)  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|用于 CMG 服务部署的 HTTPS|--|443|

有关详细信息，请参阅 [CMG 端口和数据流](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow)。

### <a name="site-server-lt---application-catalog-web-service-point"></a><a name="BKMK_PortsAppCatalogWebServicePoint_SiteServer"></a> 站点服务器 &lt;--> 应用程序目录 Web 服务点  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|服务器消息块 (SMB)|--|445|  
|RPC 终结点映射程序|135|135|  
|RPC|--|DYNAMIC <sup>[备注 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---application-catalog-website-point"></a><a name="BKMK_PortsAppCatalogWebSitePoint_SiteServer"></a> 站点服务器 &lt;--> 应用程序目录网站点  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|服务器消息块 (SMB)|--|445|  
|RPC 终结点映射程序|135|135|  
|RPC|--|DYNAMIC <sup>[备注 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---asset-intelligence-synchronization-point"></a><a name="BKMK_PortsSite-AISP"></a> 站点服务器 &lt;--> 资产智能同步点  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|服务器消息块 (SMB)|--|445|  
|RPC 终结点映射程序|135|135|  
|RPC|--|DYNAMIC <sup>[备注 6](#bkmk_note6)</sup>|  

### <a name="site-server----client"></a><a name="BKMK_PortsSite-Client"></a> 站点服务器 --> 客户端  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|LAN 唤醒|9 <sup>[备注 2](#bkmk_note2) 可用的备用端口</sup>|--|  

### <a name="site-server----cloud-distribution-point"></a><a name="BKMK_PortsSiteServer-CloudDP"></a> 站点服务器 --> 云分发点  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

有关详细信息，请参阅[端口和数据流](use-a-cloud-based-distribution-point.md#bkmk_dataflow)。

### <a name="site-server----distribution-point-both-standard-and-pull"></a><a name="BKMK_PortsSite-DP"></a> 站点服务器 --> 分发点（标准和拉取）

<sup>[备注 5](#bkmk_note5)</sup>  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|服务器消息块 (SMB)|--|445|  
|RPC 终结点映射程序|135|135|  
|RPC|--|DYNAMIC <sup>[备注 6](#bkmk_note6)</sup>|  

### <a name="site-server----domain-controller"></a><a name="BKMK_PortsSite-DC"></a> 站点服务器 --> 域控制器  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|轻型目录访问协议 (LDAP)|389|389|
|安全 LDAP（LDAPS，用于签名和绑定）|636|636|
|全局编录 LDAP|--|3268|  
|RPC 终结点映射程序|--|135|  
|RPC|--|DYNAMIC <sup>[备注 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---certificate-registration-point"></a><a name="BKMK_PortsCertificateRegistrationPoint_SiteServer"></a> 站点服务器 &lt;--> 证书注册点  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|服务器消息块 (SMB)|--|445|  
|RPC 终结点映射程序|135|135|  
|RPC|--|DYNAMIC <sup>[备注 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---cmg-connection-point"></a><a name="BKMK_CMGCP_SiteServer"></a> 站点服务器 &lt;--> CMG 连接点

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|服务器消息块 (SMB)|--|445|  
|RPC 终结点映射程序|135|135|  
|RPC|--|DYNAMIC <sup>[备注 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---endpoint-protection-point"></a><a name="BKMK_PortsEndpointProtection_SiteServer"></a>站点服务器 &lt;--> Endpoint Protection 点  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|服务器消息块 (SMB)|--|445|  
|RPC 终结点映射程序|135|135|  
|RPC|--|DYNAMIC <sup>[备注 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---enrollment-point"></a><a name="BKMK_EnrollmentPoint_SiteServer"></a> 站点服务器 &lt; --> 注册点  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|服务器消息块 (SMB)|--|445|  
|RPC 终结点映射程序|135|135|  
|RPC|--|DYNAMIC <sup>[备注 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---enrollment-proxy-point"></a><a name="BKMK_EnrollmentProxyPoint_SiteServer"></a> 站点服务器 &lt;--> 注册代理点  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|服务器消息块 (SMB)|--|445|  
|RPC 终结点映射程序|135|135|  
|RPC|--|DYNAMIC <sup>[备注 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---fallback-status-point"></a><a name="BKMK_PortsSite-FSP"></a> 站点服务器 &lt;--> 回退状态点

<sup>[备注 5](#bkmk_note5)</sup>  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|服务器消息块 (SMB)|--|445|  
|RPC 终结点映射程序|135|135|  
|RPC|--|DYNAMIC <sup>[备注 6](#bkmk_note6)</sup>|  

### <a name="site-server----internet"></a><a name="BKMK_PortSite-Internet"></a> 站点服务器 --> Internet  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[备注 1](#bkmk_note1)</sup>|  

### <a name="site-server-lt---issuing-certification-authority-ca"></a><a name="BKMK_PortsIssuingCA_SiteServer"></a> 站点服务器 &lt;--> 证书颁发机构 (CA)

当你使用证书注册点部署证书配置文件时，将使用此通信。 层次结构中并非每个站点服务器均使用该通信。 而仅用于层次结构顶部的站点服务器。  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|RPC 终结点映射程序|135|135|  
|RPC (DCOM)|--|DYNAMIC <sup>[备注 6](#bkmk_note6)</sup>|  

### <a name="site-server----server-hosting-remote-content-library-share"></a><a name="BKMK_PortsSite-RCL"></a> 站点服务器 --> 托管远程内容库共享的服务器

可将内容库移动到另一个存储位置，以释放管理中心站点或主站点服务器上的硬盘空间。 有关详细信息，请参阅[配置用于站点服务器的远程内容库](the-content-library.md#bkmk_remote)。

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|服务器消息块 (SMB)|--|445|  

### <a name="site-server-lt---service-connection-point"></a><a name="BKMK_SCP_SiteServer"></a> 站点服务器 &lt;--> 服务连接点

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|服务器消息块 (SMB)|--|445|  
|RPC 终结点映射程序|135|135|  
|RPC|--|DYNAMIC <sup>[备注 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---reporting-services-point"></a><a name="BKMK_PortsSite-RSP"></a> 站点服务器 &lt;--> Reporting Services 点

<sup>[备注 5](#bkmk_note5)</sup>  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|服务器消息块 (SMB)|--|445|  
|RPC 终结点映射程序|135|135|  
|RPC|--|DYNAMIC <sup>[备注 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---site-server"></a><a name="BKMK_PortsSite-Site"></a> 站点服务器 &lt;--> 站点服务器  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|服务器消息块 (SMB)|--|445|  

### <a name="site-server----sql-server"></a><a name="BKMK_PortsSite-SQL"></a> 站点服务器 --> SQL Server  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 <sup>[备注 2](#bkmk_note2) 可用的备用端口</sup>|  

安装使用远程 SQL Server 托管站点数据库的站点期间，请在站点服务器和 SQL Server 之间打开以下端口：  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|服务器消息块 (SMB)|--|445|  
|RPC 终结点映射程序|135|135|  
|RPC|--|DYNAMIC <sup>[备注 6](#bkmk_note6)</sup>|  

### <a name="site-server----sql-server-for-wsus"></a><a name="BKMK_PortsSite-SQL-WSUS"></a> 站点服务器 --> SQL Server for WSUS  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 <sup>[备注 3](#bkmk_note3) 可用的备用端口</sup>|  

### <a name="site-server----sms-provider"></a><a name="BKMK_PortsSite-Provider"></a> 站点服务器 --> SMS 提供程序  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|服务器消息块 (SMB)|--|445|  
|RPC 终结点映射程序|135|135|  
|RPC|--|DYNAMIC <sup>[备注 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---software-update-point"></a><a name="BKMK_PortsSite-SUP"></a> 站点服务器 &lt;--> 软件更新点

<sup>[备注 5](#bkmk_note5)</sup>  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|服务器消息块 (SMB)|--|445|  
|HTTP|--|80 或 8530 <sup>[备注 3](#bkmk_note3)</sup>|  
|HTTPS|--|443 或 8531 <sup>[备注 3](#bkmk_note3)</sup>|  

### <a name="site-server-lt---state-migration-point"></a><a name="BKMK_PortsSite-SMP"></a> 站点服务器 &lt;--> 状态迁移点

<sup>[备注 5](#bkmk_note5)</sup>  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|服务器消息块 (SMB)|--|445|  
|RPC 终结点映射程序|135|135|  

### <a name="sms-provider----sql-server"></a><a name="BKMK_PortsProvider-SQL"></a> SMS 提供程序 --> SQL Server  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 <sup>[备注 2](#bkmk_note2) 可用的备用端口</sup>|  

### <a name="software-update-point----internet"></a><a name="BKMK_PortsSUP-Internet"></a> 软件更新点 --> Internet  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[备注 1](#bkmk_note1)</sup>|  

### <a name="software-update-point----upstream-wsus-server"></a><a name="BKMK_PortsSUP-WSUS"></a> 软件更新点 --> 上游 WSUS 服务器  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 或 8530 <sup>[备注 3](#bkmk_note3)</sup>|  
|HTTPS|--|443 或 8531 <sup>[备注 3](#bkmk_note3)</sup>|  

### <a name="sql-server----sql-server"></a><a name="BKMK_PortsSQL-SQL"></a> SQL Server --&gt; SQL Server

需要一个站点中的 SQL Server 直接与其父或子站点的 SQL Server 通信，才可进行站点间的数据库复制。  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|SQL Server 服务|--|1433 <sup>[备注 2](#bkmk_note2) 可用的备用端口</sup>|  
|SQL Server Service Broker|--|4022 <sup>[备注 2](#bkmk_note2) 可用的备用端口</sup>|  

> [!TIP]  
> Configuration Manager 不需要使用端口 UDP 1434 的 SQL Server Browser。  

### <a name="state-migration-point----sql-server"></a><a name="BKMK_PortsStateMigrationPoint-to-SQL"></a> 状态迁移点 --> SQL Server  

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 <sup>[备注 2](#bkmk_note2) 可用的备用端口</sup>|  

### <a name="notes-for-ports-used-by-configuration-manager-clients-and-site-systems"></a><a name="BKMY_PortNotes"></a> 有关 Configuration Manager 客户端和站点系统使用的端口的备注  

#### <a name="note-1-proxy-server-port"></a><a name="bkmk_note1"></a> 注释 1：代理服务器端口

无法配置此端口，但它可通过配置的代理服务器路由。  

#### <a name="note-2-alternate-port-available"></a><a name="bkmk_note2"></a> 注释 2：可用的备用端口

可在 Configuration Manager 中为此值定义备用端口。 如果定义了自定义端口，请在 IPsec 策略的 IP 筛选器信息中使用该自定义端口，或者使用该端口来配置防火墙。  

#### <a name="note-3-windows-server-update-services-wsus"></a><a name="bkmk_note3"></a> 注释 3：Windows Server Update Services (WSUS)

可安装 WSUS 以使用端口 80/443 或端口 8530/8531 进行客户端通信。 在 Windows Server 2012 或 Windows Server 2016 中运行 WSUS 时，WSUS 被默认配置为针对 HTTP 使用端口 8530，针对 HTTPS 使用端口 8531。  

安装后，您可以更改端口。 不必在整个站点层次结构中使用相同的端口号。  

- 如果 HTTP 端口为 80，则 HTTPS 端口必须为 443。  

- 如果 HTTP 端口为其他端口，则 HTTPS 端口号必须大于等于 1，例如 8530 和 8531。

    > [!NOTE]  
    >  在配置使用 HTTPS 的软件更新点时，还必须打开 HTTP 端口。 未加密的数据（如特定更新的 EULA）使用 HTTP 端口。

- 当为 WSUS 清理启用以下选项时，站点服务器将与托管 SUSDB 的 SQL Server 建立连接：
  - 将非聚集索引添加到 WSUS 数据库以提高 WSUS 清理性能
  - 从 WSUS 数据库中删除过时的更新
  
  如果使用 SQL Server 配置管理器将默认 SQL Server 端口更改为备用端口，请确保该站点服务器可以使用定义的端口进行连接。 Configuration Manager 不支持动态端口。 默认情况下，SQL Server 命名实例使用动态端口连接到数据库引擎。 使用命名实例时，请手动配置静态端口。

#### <a name="note-4-trivial-ftp-tftp-daemon"></a><a name="bkmk_note4"></a> 注释 4：日常文件传输协议 (TFTP) 守护程序

日常文件传输协议 (TFTP) 守护程序系统服务不需要用户名或密码，并且它是 Windows 部署服务 (WDS) 不可或缺的一部分。 普通文件传输协议后台程序服务支持下列 RFC 定义的 TFTP 协议：  

- RFC 1350：TFTP  

- RFC 2347：选项扩展  

- RFC 2348：块大小选项  

- RFC 2349：超时间隔和传输大小选项  

TFTP 为支持无盘启动环境而设计。 TFTP 后台程序侦听 UDP 端口 69，但从动态分配的高端口响应。 如果启用此端口，TFTP 服务可接收传入的 TFTP 请求，但所选服务器无法响应这些请求。 除非将 TFTP 服务器配置为从端口 69 响应，否则所选服务器无法响应入站 TFTP 请求。  

Windows PE 中已启用 PXE 的分发点和客户端选择动态分配的高端口进行 TFTP 传输。 这些端口由 Microsoft 定义（49152 - 65535）。 有关详细信息，请参阅 [Windows 的服务概述和网络端口要求](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows)

但是，在实际的 PXE 启动期间，设备上的网络卡可选择其在 TFTP 传输过程中使用的动态分配的高端口。 设备上的网络卡未绑定到 Microsoft 定义的动态分配的高端口。 它只绑定到 RFC 1350 中定义的端口。 此端口可以是 0 到 65535 中的任意值。 要详细了解网络卡所使用的动态分配的高端口，请与设备硬件制造商联系。

#### <a name="note-5-communication-between-the-site-server-and-site-systems"></a><a name="bkmk_note5"></a> 注释 5：站点服务器和站点系统之间的通信

默认情况下，站点服务器和站点系统之间的通信是双向的。 站点服务器开始通信以配置站点系统，然后大部分站点系统连接回站点服务器以发送状态信息。 Reporting Services 点和分发点不会发送状态信息。 如果在安装站点系统后选择站点系统属性页上的“要求站点服务器启动到此站点系统的连接”，则该系统不会开始与站点服务器通信  。 转而，站点服务器会开始通信。 它使用站点系统安装帐户对站点系统服务器进行身份验证。  

#### <a name="note-6-dynamic-ports"></a><a name="bkmk_note6"></a> 注释 6：动态端口

动态端口使用由 OS 版本定义的一系列端口号。 这些端口也称为临时端口。 有关默认端口范围的详细信息，请参阅 [Service overview and network port requirements for Windows（Windows 的服务概述和网络端口要求）](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows)。  

## <a name="additional-lists-of-ports"></a><a name="BKMK_AdditionalPorts"></a> 其他端口列表  

下列部分提供了有关 Configuration Manager 使用的端口的其他信息。

### <a name="client-to-server-shares"></a><a name="BKMK_ClientShares"></a> 客户端到服务器共享

客户端在连接到 UNC 共享时使用服务器消息块 (SMB)。 例如：

- 指定了 CCMSetup.exe **/source:** 命令行属性的手动客户端安装  

- 从 UNC 路径下载定义文件的 Endpoint Protection 客户端

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|服务器消息块 (SMB)|--|445|  

### <a name="connections-to-microsoft-sql-server"></a><a name="BKMK_SQLPorts"></a> 与 Microsoft SQL Server 的连接

对于与 SQL Server 数据库引擎的通信和站点间复制，可以使用默认的 SQL Server 端口，也可以指定自定义端口：  

- 站点间通信使用：  

  - SQL Server Service Broker，默认为端口 TCP 4022。  

  - SQL Server 服务，默认为端口 TCP 1433。  

- SQL Server 数据库引擎与各种 Configuration Manager 站点系统角色之间的“站点内通信”默认使用端口 TCP 1433。  

- Configuration Manager 使用相同的端口和协议与承载站点数据库的每个 SQL 可用性组副本进行通信，就像该副本是独立的 SQL Server 实例。

使用 Azure 时，如果站点数据库位于内部或外部负载平衡器后面，请配置以下组件：

- 每个副本上的防火墙例外
- 负载均衡算法

配置下列端口：

- SQL over TCP：TCP 1433
- SQL Server Service Broker：TCP 4022
- 服务器消息块 (SMB)：TCP 445
- RPC 端点映射程序：TCP 135

> [!WARNING]  
> Configuration Manager 不支持动态端口。 默认情况下，SQL Server 命名实例使用动态端口连接到数据库引擎。 使用命名实例时，请手动配置静态端口以进行站点内通信。  

下列站点系统角色直接与 SQL Server 数据库进行通信：  

- 应用程序目录 Web 服务点  

- 证书注册点角色  

- 注册点角色  

- 管理点  

- 站点服务器  

- Reporting Services 点  

- SMS 提供程序  

- SQL Server --> SQL Server  

SQL Server 托管多个站点中的数据库时，每个数据库必须使用独立的 SQL Server 实例。 使用一组唯一的端口配置每个实例。  

若在 SQL Server 上启用基于主机的防火墙，请将其配置为允许正确的端口。 另请在与 SQL Server 通信的计算机之间配置网络防火墙。  

有关如何将 SQL Server 配置为使用特定端口的示例，请参阅[将服务器配置为侦听特定的 TCP 端口](/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port)。  

### <a name="discovery-and-publishing"></a><a name="bkmk_discovery"> </a>发现和发布

Configuration Manager 使用下列端口发现和发布站点信息：

- 轻型目录访问协议 (LDAP)：389
- 安全 LDAP（LDAPS，用于签名和绑定）：636
- 全局编录 LDAP：3268
- RPC 端点映射程序：135
- RPC：动态分配的高 TCP 端口
- TCP：1024：5000
- TCP：49152：65535

### <a name="external-connections-made-by-configuration-manager"></a><a name="BKMK_External"></a> Configuration Manager 建立的外部连接

本地 Configuration Manager 客户端或站点系统可以建立下列外部连接：  

- [资产智能同步点 --&gt; Microsoft](#BKMK_PortsAI)  

- [Endpoint Protection 点 --&gt; Internet](#BKMK_PortsEndpointProtection_Internet)  

- [客户端 --&gt; 全局编录域控制器](#BKMK_PortsClient-GCDC)  

- [Configuration Manager 控制台 --&gt; Internet](#BKMK_PortsConsole-Internet)  

- [管理点 --&gt; 域控制器](#BKMK_PortsMP-DC)  

- [站点服务器 --&gt; 域控制器](#BKMK_PortsSite-DC)  

- [站点服务器 &lt; --&gt; 证书颁发机构 (CA)](#BKMK_PortsIssuingCA_SiteServer)  

- [软件更新点 --&gt; Internet](#BKMK_PortsSUP-Internet)  

- [软件更新点 --&gt; 上游 WSUS 服务器](#BKMK_PortsSUP-WSUS)  

- [服务连接点 --> Azure](#bkmk_scp-cmg)  

- [ CMG 连接点 --> CMG 云服务](#bkmk_cmgcp-cmg)  

### <a name="installation-requirements-for-site-systems-that-support-internet-based-clients"></a><a name="BKMK_IBCMports"></a> 支持基于 Internet 的客户端的站点系统的安装要求

> [!Note]  
> 本节仅适用于基于 Internet 的客户端管理 (IBCM)。 本节不适用于云管理网关。 有关详细信息，请参阅[在 Internet 上管理客户端](../../clients/manage/manage-clients-internet.md)。  

基于 Internet 的管理点和分发点（它们支持基于 Internet 的客户端）、软件更新点以及回退状态点均使用下列端口进行安装和修复：  

- 站点服务器 --> 站点系统：RPC 终结点映射程序使用 UDP 和 TCP 端口 135。  

- 站点服务器 --> 站点系统：RPC 动态 TCP 端口  

- 站点服务器 &lt; --> 站点系统：服务器消息块 (SMB) 使用 TCP 端口 445

分发点上的应用程序和包安装需要下列 RPC 端口：  

- 站点服务器 --> 分发点：RPC 端点映射程序使用 UDP 和 TCP 端口 135

- 站点服务器 --> 分发点：RPC 动态 TCP 端口  

使用 IPsec 帮助确保站点服务器和站点系统之间的通信安全。 如果必须限制针对 RPC 使用的动态端口，可使用 Microsoft RPC 配置工具 (rpccfg.exe)。 使用该工具为这些 RPC 数据包配置一组有限的端口。 有关详细信息，请参阅 [如何配置 RPC 以使用特定端口以及如何使用 IPsec 来帮助保护这些端口](https://support.microsoft.com/help/908472/how-to-configure-rpc-to-use-certain-ports-and-how-to-help-secure-those)。  

> [!IMPORTANT]
> 在安装这些站点系统之前，请确保站点系统服务器上正在运行远程注册表服务；如果站点系统位于不同的 Active Directory 林中且不具有信任关系，则另请确保指定了站点系统安装帐户。 例如，在运行站点系统的服务器上使用远程注册表服务，如分发点（拉取和标准）、远程 SQL Server 和应用程序目录。

### <a name="ports-used-by-configuration-manager-client-installation"></a><a name="BKMK_PortsClientInstall"></a> Configuration Manager 客户端安装使用的端口

Configuration Manager 在客户端安装期间使用的端口取决于部署方法。

- 有关每种客户端部署方法的端口列表，请参阅 [Configuration Manager 客户端部署期间使用的端口](../../clients/deploy/windows-firewall-and-port-settings-for-clients.md#ports-used-during-configuration-manager-client-deployment)  

- 有关如何为客户端安装和安装后通信配置客户端上的 Windows 防火墙的信息，请参阅[客户端的 Windows 防火墙和端口设置](../../clients/deploy/windows-firewall-and-port-settings-for-clients.md)  

### <a name="ports-used-by-migration"></a><a name="BKMK_MigrationPorts"></a> 迁移使用的端口

运行迁移的站点服务器使用多个端口连接到源层次结构中的适用站点。 有关详细信息，请参阅[迁移所需的配置](../../migration/prerequisites-for-migration.md#BKMK_Required_Configurations)。  

### <a name="ports-used-by-windows-server"></a><a name="BKMK_ServerPorts"></a> Windows Server 使用的端口

下表列出了 Windows Server 使用的一些关键端口。

|说明|UDP|TCP|  
|-----------------|---------|---------|  
|DNS|53|53|  
|DHCP|67 和 68|--|  
|NetBIOS 名称解析|137|--|  
|NetBIOS 数据报服务|138|--|  
|NetBIOS 会话服务|--|139|  
|Kerberos 身份验证|--|88|

有关详细信息，请参阅下列文章：

- [Windows Server 系统的服务概述和网络端口要求](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows)

- [如何为域和信任关系配置防火墙](https://support.microsoft.com/help/179442/how-to-configure-a-firewall-for-domains-and-trusts)