---
title: 监视软件更新
titleSuffix: Configuration Manager
description: Configuration Manager 控制台提供警报和状态以监视更新和符合性。
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/08/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 9afd7b0f-5c8e-48bc-9a65-1f7d74103688
ms.openlocfilehash: 278f859d58c4feda6fa13522b476ec2beb60f514
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709485"
---
# <a name="monitor-software-updates-in-configuration-manager"></a>在 Configuration Manager 中监视软件更新

适用范围：  Configuration Manager (Current Branch)

Configuration Manager 提供了许多方式来帮助你监视软件更新对象、过程和符合性信息。 使用以下部分可监视软件更新。

## <a name="software-updates-dashboard"></a>软件更新仪表板

（从版本 1610 中引入） 

从 Configuration Manager 版本 1610 开始，可以使用软件更新仪表板查看组织中设备的当前符合性状态，并快速分析数据以确定哪些设备处于风险中。 若要查看仪表板，请导航到“监视”   > “概述”   > “安全性”   > “软件更新仪表板”  。

## <a name="drill-through-required-updates"></a>钻取必需更新
<!--4224414-->
（从版本 1906 中引入） 

可深入查看符合性统计信息，了解哪些设备需要特定 Office 365 软件更新。 若要查看设备列表，需要具有查看更新和设备所属集合的权限。 向下钻取设备列表：

1. 转到“软件库” > “软件更新” > “所有软件更新”    。
1. 选择至少一台设备所需的任何更新。
1. 查看“摘要”选项卡，找到“统计信息”下的饼图   。
1. 选择饼图旁的“查看所需更新”超链接以深入查看设备列表  。
1. 此操作将转到“设备”下的临时节点，可以在其中查看需要更新的设备  。 还可对节点执行操作，例如从列表创建新集合。


##  <a name="alerts-for-software-updates"></a><a name="BKMK_SUAlerts"></a> 软件更新的警报  
 可以配置软件更新的警报，以便在软件更新部署的符合性级别低于已配置的百分比时通知管理用户。 可以在下列位置中配置软件更新部署的警报：  

-   ADR 设置：可以在“自动部署规则向导”中和 ADR 的属性中配置警报设置。  

-   部署设置：可以在“部署软件更新向导”中和部署属性中配置警报设置。  

配置警报设置后，如果出现指定的条件，则 Configuration Manager 会生成警报。 可以在下列位置中查看软件更新警报：  

1.  在“软件库”  工作区的“软件更新”  节点中查看最新警报。  

2.  在“监视”  工作区的“警报”  节点中管理已配置的警报。  

##  <a name="software-updates-synchronization-status"></a><a name="BKMK_SUSyncStatus"></a> 软件更新同步状态  
 启动同步过程之后，可以通过 Configuration Manager 控制台监视层次结构中的所有软件更新点的同步过程。 使用下列过程来监视软件更新同步过程。  

#### <a name="to-monitor-the-software-updates-synchronization-process"></a>监视软件更新同步过程  

- 在 Configuration Manager 控制台中，导航到“监视”   > “概述”   > “软件更新点同步状态”  。  

    Configuration Manager 层次结构中的软件更新点显示在结果窗格中。 从此视图中，你可以监视所有软件更新点的同步状态。 若要了解有关同步过程的更多详细信息，请查看每台站点服务器上的 <ConfigMgrInstallationPath  >\Logs 中的 wsyncmgr.log 文件。  

##  <a name="software-update-deployment-status"></a><a name="BKMK_SUDeployStatus"></a> 软件更新部署状态  
 在软件更新组中部署软件更新或部署单个软件更新之后，可以监视部署状态。 使用下列过程来监视软件更新组或软件更新的部署状态。  

#### <a name="to-monitor-deployment-status"></a>监视部署状态  

1.  在 Configuration Manager 控制台中，导航到“监视”   > “概述”   > “部署”  。  

2.  单击要监视其部署状态的软件更新组或软件更新。  

3.  在“主页”  选项卡上的“部署”  组中，单击“查看状态”  。  

##  <a name="software-updates-reports"></a><a name="BKMK_SUReports"></a> 软件更新报表  
 软件更新的状态消息提供了有关软件更新的符合性的信息，以及有关软件更新部署的评估和强制状态的信息。 可以运行软件更新报表以显示这些状态消息。 可以使用 30 多个预定义的软件更新报表。 它们分为几个类别，可用于报告有关软件更新和部署的特定信息。 除了使用预先配置的报表之外，还可以按照企业的需求创建自定义软件更新报表。 有关详细信息，请参阅[报表的操作和维护](../../core/servers/manage/operations-and-maintenance-for-reporting.md)。  

### <a name="recommended-software-updates-reports"></a>推荐的软件更新报表
以下是一些有助于识别潜在问题的报表： 

#### <a name="compliance-9---overall-health-and-compliance-starting-in-version-1806"></a>符合性 9 - 总体运行状况和符合性（自版本 1806 起）
报告包括以下几个部分：

- **运行正常的客户端与客户端总数**：此条形图比较了在指定时间段内与站点通信的“运行正常”客户端的数量和指定集合中的客户端总数。
- **符合性概述**：此饼图显示了指定集合中活动客户端上的特定软件更新组的总体符合性状态。
- **前 5 个不符合（按文章 ID）** ：此条形图显示了特定组中在指定集合中的活动客户端上不符合的前五个软件更新。
- 报告底部是具有更多详细信息的表，其中列出了指定组中的软件更新。

#### <a name="management-2---updates-required-but-not-deployed"></a>管理 2 - 需要更新但未部署

此报表显示已检测到为客户端必需但未部署到特定集合的特定更新分类中供应商特定的软件更新。 

#### <a name="troubleshooting-2---deployment-errors"></a>疑难解答 2 - 部署错误

此报表返回站点上的部署错误以及遇到各个错误的计算机的计数。 


##  <a name="monitor-content"></a><a name="BKMK_MonitorContent"></a> 监视内容  
 可以在 Configuration Manager 控制台中监视内容，以查看与关联的分发点相关的所有包类型的状态。 这可以包括包中的内容的内容验证状态、分配给特定分发点组的内容的状态、分配给分发点的内容的状态和每个分发点的可选功能（内容验证、PXE 和多播）的状态。  

###  <a name="content-status-monitoring"></a><a name="BKMK_ContentStatus"></a> 内容状态监视  
 “监视”  工作区中的“内容状态”  节点提供有关内容包的信息。 可以查看有关包的常规信息、包的分发状态和有关包的详细状态信息。 使用下列过程来查看内容状态。  

#### <a name="to-monitor-content-status"></a>监视内容状态  

1.  在 Configuration Manager 控制台中，导航到“监视”   > “概述”   > “分发状态”   > “内容状态”  。 此时会显示包。  

2.  选择要查看其详细状态信息的包。  

3.  在“主页”  选项卡上，单击“查看状态”  。 此时会显示包的详细状态信息。  

###  <a name="distribution-point-group-status"></a><a name="BKMK_DPGroupStatus"></a> 分发点组状态  
 “监视”  工作区中的“分发点组状态”  节点提供有关分发点组的信息。 可以查看有关分发点组的常规信息（例如分发点组状态和符合性比率），以及分发点组的详细状态信息。 使用下列过程来查看分发点组状态。  

#### <a name="to-monitor-distribution-point-group-status"></a>监视分发点组状态  

1.  在 Configuration Manager 控制台中，导航到“监视”   > “概述”   > “分发状态”   > “分发点组状态”  。 此时会显示分发点组。  

2.  选择要查看其详细状态信息的分发点组。  

3.  在“主页”  选项卡上，单击“查看状态”  。 此时会显示分发点组的详细状态信息。  

###  <a name="distribution-point-configuration-status"></a><a name="BKMK_DPConfigStatus"></a> 分发点配置状态  
 “监视”  工作区中的“分发点配置状态”  节点提供有关分发点的信息。 可以查看为分发点启用的属性，例如 PXE、多播和内容验证。 还可以查看分发点的详细状态信息。 使用下列过程来查看分发点配置状态。  

#### <a name="to-monitor-distribution-point-configuration-status"></a>监视分发点配置状态  

1.  在 Configuration Manager 控制台中，导航到“监视”   > “概述”   > “分发状态”   > “分发点配置状态”  。 此时会显示分发点。  

2.  选择要查看其分发点状态信息的分发点。  

3.  在结果窗格中，单击“详细信息”  选项卡。此时会显示分发点的状态信息。  

## <a name="next-steps"></a>后续步骤

- [软件更新日志文件](../../core/plan-design/hierarchy/log-files.md#BKMK_SU_NAPLog)

- [软件更新管理白皮书](https://www.microsoft.com/download/confirmation.aspx?id=44578)
