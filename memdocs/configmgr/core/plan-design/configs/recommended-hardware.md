---
title: 推荐硬件
titleSuffix: Configuration Manager
description: 获取硬件建议，有助于在基本部署以上缩放 Configuration Manager 环境。
ms.date: 05/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5267f0af-34d3-47a0-9ab8-986c41276e6c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 36b90627f25c5cf19b867a78e141b69266478c58
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428787"
---
# <a name="recommended-hardware-for-configuration-manager"></a>用于 Configuration Manager 的推荐硬件

适用范围：Configuration Manager (Current Branch)

以下建议是一些指南，可以帮助缩放 Configuration Manager 环境，支持比非常基本的站点、站点系统和客户端部署更高级的部署。 这些指南并未打算涵盖所有可能的站点和层次结构配置。  

使用下列部分中的信息作为帮助你计划硬件的指南。 请确保硬件可以满足使用可用 Configuration Manager 功能的客户端和站点的处理负载。

有关详细信息，请参阅 [Configuration Manager 性能和缩放指南白皮书](https://gallery.technet.microsoft.com/Configuration-Manager-ba55428e)。

## <a name="site-systems"></a><a name="bkmk_ScaleSieSystems"></a>站点系统

本部分提供适用于 Configuration Manager 站点系统的推荐硬件配置。 使用这些建议以支持最大数量的客户端，并使用大部分或全部 Configuration Manager 功能。 如果你的环境支持的客户端数量小于最大限制且仅使用部分可用功能，则该环境需要的资源可能更少。 通常，下列关键因素限制整个系统的性能：

1. 磁盘 I/O 性能

2. 可用内存

3. CPU

为了获得最佳性能，请将 RAID 10 配置用于所有数据驱动器以及 1 Gbps 以太网。

### <a name="site-servers"></a><a name="bkmk_ScaleSiteServer"></a>站点服务器

|网站配置|CPU（核心数）|内存(GB)|SQL Server 的内存分配 (%)|  
|-------------------------------|---------------|---------------|----------------------------------------|  
|在同一服务器上具有数据库站点角色的独立主站点服务器<sup>[注释 1](#bkmk_note1)</sup>|16|96|80|  
|具有远程站点数据库的独立主站点服务器|8|16|-|  
|独立主站点的远程数据库服务器|16|72|90|  
|在同一服务器上具有数据库站点角色的管理中心站点服务器<sup>[注释 1](#bkmk_note1)</sup>|20|128|80|  
|具有远程站点数据库的管理中心站点服务器|8|16|-|  
|管理中心站点的远程数据库服务器|16|96|90|  
|数据库站点角色在同一服务器上的子主站点|16|96|80|  
|具有远程站点数据库的子主站点服务器|8|16|-|  
|子主站点的远程数据库服务器|16|72|90|  
|辅助站点服务器|8|16|-|  

#### <a name="note-1-collocated-sql"></a><a name="bkmk_note1"></a> 注释 1：已并置的 SQL

在同一台计算机上安装站点服务器和 SQL Server 时，部署对站点和客户端支持[调整大小和缩放数量](size-and-scale-numbers.md)的最大值。 此配置可以限制[高可用性选项](../../servers/deploy/configure/high-availability-options.md)，像使用 SQL Server 群集那样。 如果你的环境较大，由于在同一台计算机上支持两个角色具有较高的 I/O 要求，请考虑使用远程 SQL Server。

### <a name="remote-site-system-servers"></a><a name="bkmk_RemoteSiteSystem"></a>远程站点系统服务器

以下指南适用于具有单一站点系统角色的计算机。 在同一台计算机上安装多个站点系统角色时，请计划调整。

|站点系统角色|CPU（核心数）|内存 (GB)|硬盘空间 (GB)|  
|----------------------|---------------|---------------|--------------------|  
|管理点|4|8|50|  
|分发点|2|8|遵循 OS 的要求，并存储所部署的内容|  
|软件更新点<sup>[注释 2](#bkmk_note2)</sup>|8|16|遵循 OS 的要求，并存储所部署的更新|  
|所有其他站点系统角色|4|8|50|  

#### <a name="note-2-wsus-configurations"></a><a name="bkmk_note2"></a> 注释 2：WSUS 配置

托管软件更新点的计算机要求 IIS 应用程序池使用以下配置：  

- 将 **WsusPool 队列长度** 增加到 **2000**。  

- 将 WsusPool 专用内存限制增加 4 倍，或设置为 0（无限制） 。  

### <a name="disk-space-for-site-systems"></a><a name="bkmk_DiskSpace"></a>站点系统的磁盘空间

磁盘分配和配置会影响 Configuration Manager 的性能。 由于每个 Configuration Manager 环境都不同，因此，所实现的值可能会不同于下列指南的值。

为了获得最佳性能，请将每个对象都放在单独、专用的 RAID 卷上。 对于所有数据卷（Configuration Manager 及其数据库文件），请使用 RAID 10 以获得最佳性能。

|数据用途|最小磁盘空间|25,000 个客户端|50,000 个客户端|100,000 个客户端|150,000 个客户端|700,000 个客户端（管理中心站点）|  
|----------------|------------------------|--------------------|--------------------|---------------------|---------------------|-----------------------------------------------------|  
|Configuration Manager 应用程序和日志文件|25 GB|50 GB|100 GB|200 GB|300 GB|200 GB|  
|站点数据库 .mdf 文件|每 25,000 个客户端 75 GB|75 GB|150 GB|300 GB|500 GB|2 TB|  
|站点数据库 .ldf 文件|每 25,000 个客户端 25 GB|25 GB|50 GB|100 GB|150 GB|100 GB|  
|临时数据库文件（.mdf 和 .ldf）|按需而定|按需而定|按需而定|按需而定|按需而定|按需而定|  

对于 Windows 系统磁盘，请参阅调整已安装 OS 版本的大小的指南。

对于分发点上的内容，这取决于你的部署。 该指南不包括站点服务器或分发点上的内容库所需的磁盘空间。 有关详细信息，请参阅[内容库](../../../core/plan-design/hierarchy/the-content-library.md)。

在规划磁盘空间要求时，请考虑下列其他指南：

- 每个客户端都需要大约 5-10 MB 的数据库空间。 此数值取决于层次结构类型、配置和客户端数量。 对于较大的环境，此大小通常不够。 对于较小的站点，每个客户端的数据库使用量更大。<!-- SCCMDocs#1048 -->

- 对于主站点的临时数据库，规划的组合大小应为站点数据库 .mdf 文件大小的 25% 到 30%。 实际大小可能更小或更大。 大小具体取决于站点服务器的性能，以及短期和长期的传入数据量。

  > [!NOTE]
  > 站点有 50,000 个或更多客户端时，请计划使用 4 个或更多临时数据库 .mdf 文件。

- 管理中心站点的临时数据库大小通常比主站点的临时数据库大小要小得多。

- 如果将 SQL Server Express 用于辅助站点数据库，它会将数据库大小限制为 10 GB。

## <a name="clients"></a><a name="bkmk_ScaleClient"></a>客户端

本部分提供使用 Configuration Manager 客户端软件管理计算机的推荐硬件配置。

### <a name="client-for-windows-computers"></a>Windows 计算机的客户端

以下是使用 Configuration Manager 管理基于 Windows 的计算机的最低要求，包括嵌入的版本：

- **处理器和内存：** 请参阅 OS 的处理器和 RAM 要求。

- **磁盘空间：** 500 MB 可用磁盘空间，建议有 5 GB 用于 Configuration Manager 客户端缓存。 如果使用自定义设置安装 Configuration Manager 客户端，则需要的磁盘空间较少。

  - 使用 client.msi 属性“SMSCACHESIZE”设置小于默认值 5120 MB 的缓存大小。 最小大小为 1 MB。 以下示例将创建一个 2 MB 的缓存：`CCMSetup.exe SMSCACHESIZE=2`

    有关详细信息，请参阅[关于客户端安装属性](../../../core/clients/deploy/about-client-installation-properties.md)。

    > [!TIP]
    > 使用最小磁盘空间安装客户端适用于 Windows Embedded 设备，此设备的磁盘大小通常比标准 Windows 计算机的磁盘大小要小。

以下是 Configuration Manager 中可选功能的其他最低硬件要求：

- **OS 部署：** 至少 384 MB 的 RAM

- **软件中心：** 至少 500 MHz 的处理器

- **远程控制：** 为获得最佳体验，需要至少 Pentium 4 Hyper-Threaded 3 GHz（单核）或同等能力的 CPU，以及至少 1 GB 的 RAM。

### <a name="client-for-linux-and-unix"></a>适用于 Linux 和 UNIX 的客户端

以下是对使用 Configuration Manager 管理的 Linux 和 UNIX 服务器的最低要求。

|要求|详细信息|  
|-----------------|-------------|  
|处理器和内存|请参阅计算机 OS 的处理器和 RAM 要求。|  
|硬盘空间|500 MB 可用磁盘空间，建议有 5 GB 用于 Configuration Manager 客户端缓存。|  
|网络连接|Configuration Manager 客户端计算机必须具有到 Configuration Manager 站点系统的网络连接才能启用管理。|  

## <a name="configuration-manager-console"></a><a name="bkmk_ScaleConsole"></a> Configuration Manager 控制台

以下最低硬件要求适用于运行 Configuration Manager 控制台的每台计算机：

- Intel i3 或相当的 CPU  

- 2 GB RAM  

- 2 GB 磁盘空间  

|DPI 设置|最小分辨率|  
|-----------------|------------------------|  
|96/100%|1024 x 768|  
|120/125%|1280 x 960|  
|144/150%|1600 x 1200|  
|196/200%|2500 x 1600|  

## <a name="lab-deployments"></a><a name="bkmk_ScaleLab"></a>实验室部署

对 Configuration Manager 的实验室和测试部署使用下列建议的最低硬件配置。 这些建议适用于所有站点类型，并可用于最多 100 个客户端：  

|Role|CPU（核心数）|内存 (GB)|硬盘空间 (GB)|  
|----------|---------------|-------------------|-----------------------|  
|站点和数据库服务器|2 - 4|8 - 12|100|  
|站点系统服务器|1 - 4|2 - 4|50|  
|客户端|1 - 2|1 - 3|30|  
