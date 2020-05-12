---
title: 监视操作系统部署
titleSuffix: Configuration Manager
description: 为帮助你监视操作系统部署对象，Configuration Manager 控制台提供了警报、报表和各种状态指示器。
ms.date: 05/04/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 08085d94-295c-432f-b5e3-9736bce0193b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7afab9fbbb443b2f9fb4af15a3805c0b7df7a014
ms.sourcegitcommit: 14d7dd0a99ebd526c9274d5781c298c828323ebf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82802160"
---
# <a name="monitor-operating-system-deployments-in-configuration-manager"></a>在 Configuration Manager 中监视操作系统部署

适用范围：  Configuration Manager (Current Branch)

Configuration Manager 控制台提供了以下方式来帮助你监视操作系统部署对象。  


##  <a name="alerts-for-operating-system-deployments"></a><a name="BKMK_OSDAlerts"></a> 操作系统部署警报  
 你可以在任务序列部署设置中配置警报，以便在部署符合性水平低于配置百分比时通知管理用户。  

 配置警报设置后，如果出现指定的条件，则 Configuration Manager 会生成警报。 你可以在下列位置查看任务序列部署警报：  

1.  在“软件库”  工作区的“操作系统”  节点中查看最近警报。  

2.  在“监视”  工作区的“警报”  节点中管理已配置的警报。  

##  <a name="task-sequence-deployment-status"></a><a name="BKMK_TSDeployStatus"></a> 任务序列部署状态  
 部署任务序列后，你可以监视部署状态。 使用下列过程来监视任务序列的部署状态。  

#### <a name="to-monitor-deployment-status"></a>监视部署状态  

1.  在 Configuration Manager 控制台中，单击“监视”  。  

2.  在“监视”工作区中，单击“部署”  。  

3.  单击要监视其部署状态的任务序列。  

4.  在“主页”  选项卡上的“部署”  组中，单击“查看状态”  。  

> [!NOTE]  
> 启动升级时，将生成状态消息 52200。 这包含进行升级的用户。  

##  <a name="operating-system-deployment-reports"></a><a name="BKMK_TSReports"></a> 操作系统部署报表  
 提供多个预定义的操作系统部署报表。 它们分为几个类别，可用于报告有关状态迁移和任务序列部署的特定信息。 除了使用预先配置的报表之外，还可以按照企业的需求创建自定义软件更新报表。 有关详细信息，请参阅[报表的操作和维护](../../core/servers/manage/operations-and-maintenance-for-reporting.md)。  

##  <a name="monitor-content"></a><a name="BKMK_MonitorContent"></a> 监视内容  
 可以在 Configuration Manager 控制台中监视内容，以查看与关联的分发点相关的所有包类型的状态。 这可以包括包中的内容的内容验证状态、分配给特定分发点组的内容的状态、分配给分发点的内容的状态和每个分发点的可选功能（内容验证、PXE 和多播）的状态。  

###  <a name="content-status-monitoring"></a><a name="BKMK_ContentStatus"></a> 内容状态监视  
 “监视”  工作区中的“内容状态”  节点提供有关内容包的信息。 可以查看有关包的常规信息、包的分发状态和有关包的详细状态信息。 使用下列过程来查看内容状态。  

#### <a name="to-monitor-content-status"></a>监视内容状态  

1.  在 Configuration Manager 控制台中，单击“监视”  。  

2.  在“监视”工作区中，展开“分发状态”  ，然后单击“内容状态”  。 此时会显示包。  

3.  选择要查看其详细状态信息的包。  

4.  在“主页”  选项卡上，单击“查看状态”  。 此时会显示包的详细状态信息。  

###  <a name="distribution-point-group-status"></a><a name="BKMK_DPGroupStatus"></a> 分发点组状态  
 “监视”  工作区中的“分发点组状态”  节点提供有关分发点组的信息。 可以查看有关分发点组的常规信息（例如分发点组状态和符合性比率），以及分发点组的详细状态信息。 使用下列过程来查看分发点组状态。  

#### <a name="to-monitor-distribution-point-group-status"></a>监视分发点组状态  

1.  在 Configuration Manager 控制台中，单击“监视”  。  

2.  在“监视”工作区中，展开“分发状态”  ，然后单击“分发点组状态”  。 此时会显示分发点组。  

3.  选择要查看其详细状态信息的分发点组。  

4.  在“主页”  选项卡上，单击“查看状态”  。 此时会显示分发点组的详细状态信息。  

###  <a name="distribution-point-configuration-status"></a><a name="BKMK_DPConfigStatus"></a> 分发点配置状态  
 “监视”  工作区中的“分发点配置状态”  节点提供有关分发点的信息。 可以查看为分发点启用的属性，例如 PXE、多播和内容验证。 还可以查看分发点的详细状态信息。 使用下列过程来查看分发点配置状态。  

#### <a name="to-monitor-distribution-point-configuration-status"></a>监视分发点配置状态  

1.  在 Configuration Manager 控制台中，单击“监视”  。  

2.  在“监视”工作区中，展开“分发状态”  ，然后单击“分发点配置状态”  。 此时会显示分发点。  

3.  选择要查看其分发点状态信息的分发点。  

4.  在结果窗格中，单击“详细信息”  选项卡。此时会显示分发点的状态信息。  
