---
title: 大小和扩展
titleSuffix: Configuration Manager
description: 确定需要用来支持环境中设备的站点系统角色和站点的数量。
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c5a42100-2f60-4952-b495-918025ea6559
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0d8057d61ebaaa8a545d21b31331faec1c04884e
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126692"
---
# <a name="size-and-scale-numbers-for-configuration-manager"></a>用于 Configuration Manager 的大小和扩展数量

适用范围：Configuration Manager (Current Branch)

每个 Configuration Manager 部署都存在可支持的站点、站点系统角色和设备的最大数量。 这些数量因层次结构（使用的站点的类型和数量）和部署的站点系统角色而异。 本文中的信息可帮助确定用于支持需要管理的设备的站点系统角色和站点的数量。

有关详细信息，请参阅下列文章：

- [推荐硬件](recommended-hardware.md)
- [站点系统服务器支持的操作系统](supported-operating-systems-for-site-system-servers.md)  
- [客户端和设备支持的操作系统](supported-operating-systems-for-clients-and-devices.md)
- [站点和站点系统先决条件](site-and-site-system-prerequisites.md)

这些支持数量基于为 Configuration Manager 使用推荐的硬件。 还基于所有可用的 Configuration Manager 功能的默认设置。 如果不使用推荐的硬件或使用效力较强的自定义设置时，站点系统的性能可能会降低。 站点系统可能不满足规定的支持级别。 （效力较强的客户端设置示例：比默认每七天一次更频繁地运行硬件或软件清单。）

## <a name="site-types"></a><a name="bkmk_SiteSystemScale"></a>站点类型  

### <a name="central-administration-site"></a>管理中心站点  

- 一个管理中心站点最多可支持 25 个子主站点。  

### <a name="primary-site"></a>主站点  

- 每个主站点最多支持 250 个辅助站点。  

- 每个主站点的辅助站点数基于持续连接和可靠的广域网 (WAN) 连接。 对于具有少于 500 个客户端的位置，请考虑使用分发点而不是辅助站点。  

  有关主站点可支持的客户端数和设备数的信息，请参阅[站点和层次结构的客户端数量](#bkmk_clientnumbers)。  

### <a name="secondary-site"></a>辅助站点  

- 辅助站点不支持子站点。  

## <a name="site-system-roles"></a><a name="bkmk_roles"></a> Site system roles

### <a name="application-catalog-web-service-point"></a>应用程序目录 Web 服务点  

> [!Important]
> 从 Current Branch 版本 1806 开始，不支持应用程序目录的 Silverlight 用户体验。 自版本 1906 起，更新后的客户端自动使用管理点进行用户可用的应用程序部署。 仍然无法安装新的应用程序目录角色。 版本 1910 已终止对应用程序目录角色的支持。  
>
> 有关详细信息，请参阅下列文章：
>
> - [配置软件中心](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [已删除和已弃用的功能](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

- 你可以在主站点安装“应用程序目录”Web 服务点的多个实例。  

### <a name="application-catalog-website-point"></a>应用程序目录网站点  

> [!Important]
> 从 Current Branch 版本 1806 开始，不支持应用程序目录的 Silverlight 用户体验。 自版本 1906 起，更新后的客户端自动使用管理点进行用户可用的应用程序部署。 仍然无法安装新的应用程序目录角色。 版本 1910 已终止对应用程序目录角色的支持。  
>
> 有关详细信息，请参阅下列文章：
>
> - [配置软件中心](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [已删除和已弃用的功能](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

- 你可以在主站点安装“应用程序目录”网站点的多个实例。  

### <a name="cloud-management-gateway"></a><a name="bkmk_cmg"></a> 云管理网关

- 可以在主站点或管理中心站点安装多个云管理网关 (CMG) 的实例。  

    > [!Tip]  
    > 在层次结构中的管理中心站点创建 CMG。  

  - 在 Azure 云服务中，一个 CMG 支持 1 到 16 个虚拟机 (VM) 实例。  

  - 每个 CMG VM 实例支持 6,000 个并行客户端连接。 客户端数量超过受支持的数量导致 CMG 处于高负载状态时，它仍可处理请求，但可能会有延迟。  

有关详细信息，请参阅 CMG [性能和规模](../../clients/manage/cmg/plan-cloud-management-gateway.md#performance-and-scale)

### <a name="cloud-management-gateway-connection-point"></a>云管理网关连接点

- 可以在主站点安装 CMG 连接点的多个实例。  

- 一个 CMG 连接点可以支持最多带有 4 个 VM 实例的 CMG。 如果 CMG 的 VM 实例多于 4 个，请添加第二个 CMG 连接点以保持负载平衡。 带有 16 个 VM 实例的 CMG 应与 4 个 CMG 连接点连接。

有关详细信息，请参阅 CMG [性能和规模](../../clients/manage/cmg/plan-cloud-management-gateway.md#performance-and-scale)

> [!NOTE]
> 考虑 CMG 连接点的硬件要求时，请参阅[远程站点系统服务器的推荐硬件](recommended-hardware.md#bkmk_RemoteSiteSystem)。<!-- SCCMDocs#2276 -->

### <a name="distribution-point"></a>分发点  

- 每个站点的分发点：  

  - 每个主站点和辅助站点最多支持 250 个分发点。  

  - 每个主站点和辅助站点最多支持 2000 个被配置为请求分发点的其他分发点。 **例如**，当其中的 2000 个分发点被配置为请求分发点时，一个单一主站点可支持 2250 个分发点。  

  - 每个分发点最多支持来自 4,000 台客户端的连接。  

  - 请求分发点从源分发点访问内容时，它的作用类似于客户端。  

- 每个主站点最多支持合并总计 5,000 个分发点。 此总数包括主站点中的所有分发点和隶属于主站点的子辅助站点的所有分发点。  

- 每个分发点最多支持合并总计 10,000 个包和应用程序。  

> [!WARNING]  
> 一个分发点可以支持的客户端的实际数量取决于网络速度和服务器的硬件配置。  
>
> 一个源分发点可以支持的请求分发点的数量同样取决于网络速度和源分发点的硬件配置。 但这一数量还受已部署的内容量的影响。 这是因为请求分发点和客户端不同，各客户端通常在部署期间的不同时间访问内容，而所有请求分发点是同时请求内容的。 请求分发点可以请求所有可用内容，不仅是适用于它们的内容。 如果在源分发点上放置高处理负载，则可能在将内容分发至目标分发点的过程中出现意外的延迟。  

### <a name="fallback-status-point"></a>回退状态点  

- 每个回退状态点最多可支持 100,000 个客户端。  

### <a name="management-point"></a>管理点  

- 每个主站点最多支持 15 个管理点。  

    > [!TIP]  
    > 请勿在主站点服务器或站点数据库服务器通过慢速链接的服务器上安装管理点。  

- 每个辅助站点支持一个单一管理点，该管理点必须安装在辅助站点服务器上。  

有关管理点可支持的客户端数和设备数的信息，请参阅[管理点](#bkmk_mp)部分。  

> [!NOTE]
> 如果你启用管理点以支持[云管理网关](../../clients/manage/cmg/plan-cloud-management-gateway.md)，则它将按惯例为基于 Internet 的客户端请求提供服务。 管理点的调整大小指南并不会更改它是在本地还是基于 Internet 的客户端提供服务。

### <a name="software-update-point"></a>软件更新点  

使用以下建议作为基线。 此基线可帮助你确定适合于你的组织的软件更新容量计划相关信息。 实际容量要求可能与本文中所列的建议有所不同，具体取决于以下条件：

- 特定的网络环境
- 用于托管软件更新点站点系统的硬件
- 受管客户端的数量
- 服务器上安装的其他站点系统角色  

> [!NOTE]
> 如果你启用软件更新点以支持[云管理网关](../../clients/manage/cmg/plan-cloud-management-gateway.md)，则它将按惯例为基于 Internet 的客户端请求提供服务。 软件更新点的调整大小指南并不会更改它是在本地还是基于 Internet 的客户端提供服务。

#### <a name="capacity-planning-for-the-software-update-point"></a><a name="BKMK_SUMCapacity"></a> 软件更新点的容量规划  

支持的客户端数量取决于在软件更新点上运行的 Windows Server Update Services (WSUS) 的版本。 还取决于软件更新点站点系统角色是否与另一站点系统角色共存：  

- 当 WSUS 在软件更新点服务器上运行，并且软件更新点与另一站点系统角色共存时，软件更新点可支持多达 25,000 个客户端。  

- 当远程服务器满足 WSUS 要求、WSUS 与 Configuration Manager 配合使用，并且你配置了下述设置时，软件更新点可支持多达 150,000 个客户端：

  IIS 应用程序池：

  - 将 WsusPool 队列长度增加到 2000
  - 将 WsusPool 专用内存限制增加 4 倍，或设置为 0（无限制）。 例如，如果默认限制是 1,843,200 KB，则将其增加到 7,372,800。 有关详细信息，请参阅 [Configuration Manager 支持团队博客文章](https://www.phoenixtekk.com/configmgr-2012-support-tip-wsus-sync-fails-with-http-503-errors/)。  

    要详细了解软件更新点的硬件要求，请参阅[推荐的站点系统硬件](recommended-hardware.md#bkmk_ScaleSieSystems)。  

#### <a name="capacity-planning-for-software-updates-objects"></a><a name="bkmk_sum-capacity-obj"></a>软件更新对象的容量规划  

使用下列容量信息来规划软件更新对象：  

- **将部署中的软件更新数量限制为 1000** - 为每个软件更新部署将软件更新数限制为 1000。 创建自动部署规则 (ADR) 时，指定限制软件更新数量的条件。 如果指定的条件返回超过 1000 个软件更新时，ADR 失效。 在 Configuration Manager 控制台中的“自动部署规则”节点上查看 ADR 的状态。 手动部署软件更新时，选择进行部署的更新不能超过 1000 个。  

  配置基线中的软件更新数量也限制为 1000。 有关详细信息，请参阅[创建配置基线](../../../compliance/deploy-use/create-configuration-baselines.md)。

- **将自动部署规则的安全作用域数量限制为 580** -<!--ado 4962928-->
将自动部署规则 (ADR) 的安全作用域数量限制为小于 580。 创建 ADR 时，会自动添加有权访问该 ADR 的安全作用域。 如果设置的安全作用域超过 580，ADR 将无法运行，并会在 ruleengine.log 中记录一条错误。

### <a name="sms-provider"></a>SMS 提供程序

<!-- SCCMDocs#1958 -->

每个 SMS 提供程序的实例支持从多个请求进行同时连接。 对这些连接仅有的限制是 Windows 可用的服务器连接数量，以及服务器上满足连接请求的可用资源。

有关详细信息，请参阅[规划 SMS 提供程序](../hierarchy/plan-for-the-sms-provider.md)。

管理服务是每个 SMS 提供程序实例上的 REST API。 它最多支持 5,000 个请求/秒和 200 个请求/客户端 IP 地址。

## <a name="client-numbers-for-sites-and-hierarchies"></a><a name="bkmk_clientnumbers"></a>站点和层次结构的客户端数量

使用以下信息来确定站点中或层次结构中可以支持多少客户端和哪些客户端类型。  

### <a name="hierarchy-with-a-central-administration-site"></a><a name="bkmk_cas"></a>具有管理中心站点的层次结构

管理中心站点最多可支持包括对下列三组列出的设备数量总数：  

- 700,000 个 Windows 桌面。 另请参阅对[嵌入式设备](#embedded)的支持。

- 运行 Mac 和 Windows CE 7.0 的 25,000 台设备  

- 使用本地移动设备管理 (MDM) 管理的 100,000 台设备

例如，在层次结构中可以支持 700,000 台台式机、最多 25,000 台 Mac 和 Windows CE 7.0 设备以及最多 100,000 台由本地 MDM 管理的设备。 此层次结构总共支持 825,000 台设备。

> [!IMPORTANT]  
> 在管理中心站点使用标准版 SQL Server 的层次结构中，层次结构最多可支持 50,000 台台式机和设备。 要支持 50,000 个以上的桌面和设备，必须使用 SQL Server 的企业版。 此要求仅适用于管理中心站点。 不适用于独立主站点或子主站点。 主站点所使用的 SQL Server 版本不会限制它能支持的客户端数量。

在独立主站点上使用的 SQL Server 版本不限制该站点容量，以便其支持最大的规定客户端数量。  

### <a name="child-primary-site"></a><a name="bkmk_chipri"></a>子主站点

包含管理中心站点的层次结构中的每个子主站点支持以下数量的客户端：  

- 总共 150,000 台客户端和设备，不局限于特定组或类型，只要不超过层次结构所支持的数量。 另请参阅对[嵌入式设备](#embedded)的支持。

例如，主站点支持 25,000 台 Mac 和 Windows CE 7.0 设备。 这个数量是针对层次结构的限制。 此主站点还可支持额外 125,000 台台式计算机。 子主站点支持的设备总数上限为 150,000。

### <a name="stand-alone-primary-site"></a><a name="bkmk_pri"></a>独立主站点

独立主站点支持下列数量的设备：  

- 总数不超过 175,000 的客户端和设备  

  - 150,000 台台式机（运行 Windows、Linux 和 UNIX 的计算机）。 另请参阅对[嵌入式设备](#embedded)的支持。

  - 运行 Mac 和 Windows CE 7.0 的 25,000 台设备

  - 使用本地 MDM 管理的 50,000 台设备  

例如，支持 150,000 台台式机和 10,000 台 Mac 的独立主站点仅支持由本地 MDM 管理的另外 15,000 台移动设备。

### <a name="primary-sites-and-windows-embedded-devices"></a><a name="embedded"></a>主站点和 Windows Embedded 设备

主站点支持启用了基于文件的写入筛选器 (FBWF) 的 Windows Embedded 设备。 如果嵌入式设备没有启用写入筛选器，则主站点支持大量嵌入式设备，数量最多可以达到该站点允许的设备数。 嵌入式设备启用了 FBWF 或统一写入筛选器 (UWF) 时，主站点最多可支持 10,000 个 Windows 嵌入式设备。 这些设备必须针对[规划 Windows Embedded 设备的客户端部署](../../clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md)中重要说明中列出的异常进行配置。 主站点仅支持 3,000 台启用了 EWF 且不是为异常配置的 Windows Embedded 设备。

### <a name="secondary-sites"></a><a name="bkmk_sec"></a>辅助站点

辅助站点支持以下数量的设备：  

- 15,000 台台式机（运行 Windows、Linux 和 UNIX 的计算机）  

### <a name="management-points"></a><a name="bkmk_mp"></a>管理点

每个管理点可以支持以下数目的设备：  

- 总数不超过 25,000 的客户端和设备  

  - 25,000 台台式机（运行 Windows、Linux 和 UNIX 的计算机）  

  - 下列之一（不能两种都包含）：  

    - 使用本地 MDM 管理的 10,000 台设备  

    - 10,000 台运行 Mac 和 Windows CE 7.0 客户端的设备
