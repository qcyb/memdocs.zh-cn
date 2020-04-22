---
title: '硬件清单 '
titleSuffix: Configuration Manager
description: 获取 Configuration Manager 中硬件清单的简介。
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3969952e-9d05-49c9-82a2-e7e90ccef511
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7baf6bad80fbccb698278602c519f3a75b8a4b5f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695405"
---
# <a name="introduction-to-hardware-inventory-in-configuration-manager"></a>Configuration Manager 中硬件清单的简介

适用范围：  Configuration Manager (Current Branch)

使用 Configuration Manager 中的硬件清单可收集有关组织中的客户端设备硬件配置的信息。 必须选中客户端设置中的“在客户端上启用硬件清单”  设置，才能收集硬件清单。  

 在硬件清单启用且客户端运行硬件清单周期后，客户端便会将信息发送到客户端站点中的管理点。 随后，管理点将清单信息转发到 Configuration Manager 站点服务器，将清单信息存储在站点数据库中。 硬件清单会根据你在客户端设置中指定的计划在客户端上运行。  
## <a name="view-hardware-inventory"></a>查看硬件清单 

 可使用多种方法来查看 Configuration Manager 收集的硬件清单数据，这些方法包括：  

- [创建返回基于特定硬件配置的设备的查询](../../../../core/servers/manage/introduction-to-queries.md)。  

- [创建基于特定硬件配置的基于查询的集合](../../../../core/clients/manage/collections/introduction-to-collections.md)。 基于查询的集合成员身份会按计划自动更新。 可以使用集合执行多项任务（包括软件部署）。

- [运行显示有关组织中硬件配置的特定详细信息的报表](../../../servers/manage/introduction-to-reporting.md)。

- [使用资源浏览器](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md)查看从客户端设备收集的硬件清单详细信息。

当硬件清单在客户端设备上运行时，客户端返回的第一批清单数据始终是完整清单。 后续清单数据仅包含增量清单信息。 站点服务器按接收顺序来处理增量清单信息。 如果缺少客户端的增量信息，站点服务器会拒绝其他增量信息，并指示客户端运行完整清单周期。  

 Configuration Manager 为双引导计算机提供有限支持。 Configuration Manager 可以发现双引导计算机，但只从在清单周期运行时处于活动状态的操作系统返回清单信息。  

> [!NOTE]  
>  有关如何使用运行 Linux 和 UNIX 的客户端硬件清单的信息，请参阅 [Linux 和 UNIX 的硬件清单](../../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md)。  

## <a name="extending-configuration-manager-hardware-inventory"></a>扩展 Configuration Manager 硬件清单  
 除了 Configuration Manager 中的内置硬件清单之外，还可以使用下面的一种方法来扩展硬件清单，以收集更多信息：  

- 在 Configuration Manager 控制台中启用、禁用、添加和删除硬件清单的清单类。  
- 使用 NOIDMIF 文件收集 Configuration Manager 无法收集清单的客户端设备的相关信息。 例如，您可能想要收集设备资产编号的信息仅作为在设备上的标签存在。 NOIDMIF 清单是自动与收集从客户端设备相关联。  
- 使用 IDMIF 文件收集不与 Configuration Manager 客户端关联的资产（例如，投影仪、复印机和网络打印机）的相关信息。


## <a name="next-steps"></a>后续步骤
有关使用这些方法扩展 Configuration Manager 硬件清单的详细信息，请参阅[如何配置硬件清单](../../../../core/clients/manage/inventory/configure-hardware-inventory.md)。  
