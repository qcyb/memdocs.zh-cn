---
title: 监视迁移
titleSuffix: Configuration Manager
description: 了解如何使用 Configuration Manager 控制台来监视迁移作业的进度和成功情况。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: fc731d3f-edd7-4049-b17b-653d6693a564
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f9d1766a374c7abd8b13f503c3c7a64e35a5ac2c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693395"
---
# <a name="planning-to-monitor-migration-activity-in-configuration-manager"></a>规划在 Configuration Manager 中监视迁移活动

适用范围：  Configuration Manager (Current Branch)

使用 Configuration Manager，可以在连接到目标层次结构的 Configuration Manager 控制台中监视迁移。 在 Configuration Manager 控制台的“管理”  工作区中，可以使用“迁移”  节点监视迁移工作的进度和成功情况。 你可以查看每个迁移作业的摘要信息，该信息确定已迁移的对象、尚未迁移的那些对象，以及从迁移作业中排除的对象的数量。 你还将看到有关任何迁移问题的详细信息。  

## <a name="view-migration-progress"></a>查看迁移进度  
 若要查看迁移作业的进度，请使用下列任何操作：  

-   在 Configuration Manager 控制台的“管理”  工作区中，展开“迁移作业”  节点，选择一个迁移作业，然后选择“作业中的对象”  选项卡。  

-   使用 Configuration Manager 日志文件来查看迁移进度或发现任何问题。 迁移管理器是 Configuration Manager 过程，用于跟踪迁移操作并将这些操作记录在站点服务器上 **\&lt;InstallationPath\>\\LOGS** 文件夹中的 migmctrl.log 文件中。  

    > [!NOTE]  
    >  如果迁移作业失败，请尽快在 migmctrl.log 文件中查看详细信息。 迁移日志条目会一直添加到该文件中并覆盖旧详细信息。 如果条目被覆盖，你可能无法确定你可能遇到的任何迁移对象问题是否与迁移问题相关。 不管在配置迁移时 Configuration Manager 控制台连接到哪个站点，迁移活动都记录在层次结构的顶层站点上。  

-   使用 Configuration Manager 报表。 Configuration Manager 提供了若干内置迁移报表，可以选择对它们进行编辑以满足你的需求。 有关 Configuration Manager 报表的详细信息，请参阅[报表简介](../servers/manage/introduction-to-reporting.md)。  
