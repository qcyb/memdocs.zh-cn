---
title: 迁移计划
titleSuffix: Configuration Manager
description: 将数据迁移到 Configuration Manager Current Branch 目标层次结构之前，了解有关站点和层次结构的信息。
ms.date: 01/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b2bf493e-1e10-496f-a139-2646522703ed
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b514e2bb0843801cfa6f0f307af8a5013fc3f9e6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702825"
---
# <a name="plan-for-migration-to-configuration-manager-current-branch"></a>规划如何迁移到 Configuration Manager Current Branch

适用范围：  Configuration Manager (Current Branch)

在将数据迁移到 Configuration Manager Current Branch 目标层次结构之前，请务必熟知 Configuration Manager 中的站点和层次结构。 有关站点和层次结构的详细信息，请参阅 [Configuration Manager 的基础知识](../../core/understand/fundamentals.md)。  

安装将成为目标层次结构的 Configuration Manager Current Branch 层次结构，然后才能从支持的源层次结构中迁移数据。  

安装目标层次结构之后，设置要在目标层次结构中使用的管理特性和功能，然后再开始迁移数据。  

此外，可能还必须规划源层次结构与目标层次结构之间的重叠。 例如，可能需要设置源层次结构以将相同网络位置或边界用作目标层次结构，随后将新客户端安装到目标层次结构并使用自动站点分配。 在这种情况下，因为新安装的 Configuration Manager 客户端可以从任一层次结构中选择要加入的站点，所以，该客户端可能会错误地分配到源层次结构。 为此，应计划将目标层次结构中的每个新客户端分配到该层次结构中的特定站点，而不是使用自动站点分配。  

有关站点分配的详细信息，请参阅 [Configuration Manager 不同版本之间的互操作性](../../core/plan-design/hierarchy/interoperability-between-different-versions.md)中的[客户端站点分配注意事项](../../core/plan-design/hierarchy/interoperability-between-different-versions.md#BKMK_SupConfigSiteAssignment)。  

使用下列文章来帮助你规划如何将支持的源层次结构迁移到 Configuration Manager 目标层次结构：

-   [迁移的先决条件](../../core/migration/prerequisites-for-migration.md)  

-   [针对迁移规划的管理员清单](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [确定是否将数据迁移到 Configuration Manager Current Branch](../../core/migration/determine-whether-to-migrate-data.md)  

-   [规划源层次结构策略](../../core/migration/planning-a-source-hierarchy-strategy.md)  

-   [针对迁移规划的管理员清单](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [规划客户端迁移策略](../../core/migration/planning-a-client-migration-strategy.md)  

-   [规划内容部署迁移策略](../../core/migration/planning-a-content-deployment-migration-strategy.md)  

-   [规划将 Configuration Manager 对象迁移到 Configuration Manager Current Branch](../../core/migration/planning-for-the-migration-of-objects.md)  

-   [规划迁移活动监视](../../core/migration/planning-to-monitor-migration-activity.md)  

-   [规划完成迁移](../../core/migration/planning-to-complete-migration.md)  
