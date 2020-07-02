---
title: 集合评估
titleSuffix: Configuration Manager
description: 了解集合评估过程、类型和触发器。 了解集合评估关系图和层次结构。
ms.date: 06/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d17e1188-d277-438f-9236-db9cd213b421
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: af90154b848ddcd7cbff21917ef122ab10585098
ms.sourcegitcommit: 1d8bf691780b94a945e94945115d4d1df4242808
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/10/2020
ms.locfileid: "84663857"
---
# <a name="collection-evaluation-in-configuration-manager"></a>Configuration Manager 中的集合评估

适用范围：Configuration Manager (Current Branch)

Configuration Manager 根据你定义的集合规则使用集合评估更新集合成员资格。 集合评估范围和计时因站点和集合配置以及评估类型而有所不同。 

请务必了解集合评估行为，以便可以做出适当的集合设计决策。 有关集合评估指南和建议，请参阅[集合的最佳实践](best-practices-for-collections.md)。

## <a name="evaluation-process"></a>评估过程

当集合计算器创建、更改和删除集合时，[colleval.log](https://docs.microsoft.com/mem/configmgr/core/plan-design/hierarchy/log-files#BKMK_ServerLogs) 会进行记录。

在高级别中，每个集合评估和更新均执行以下步骤：

![高级集合更新过程](media/high-level-collection-update-process.png)

1. 执行集合查询。
1. 添加属于直接成员的任何系统。
1. 评估所有包含集合。
   
   如果包含集合还具有查询规则，或者具有包含或排除集合，则也对它们进行评估。 如果包含集合本身是限制集合，则评估它们下面的所有集合。 完全评估树后，将结果返回到调用集合。
   
1. 在返回的结果和限制集合之间执行逻辑 `AND`。
1. 评估排除集合。
   
   如果排除集合还具有查询规则，或者具有包含或排除集合，则也对它们进行评估。 如果排除集合本身是限制集合，则评估它们下面的所有集合。 完全评估树后，将结果返回到调用集合。
   
1. 将评估直接成员和包含集合所得的结果与评估排除集合所得的结果进行比较。
1. 将更改写入数据库并执行更新。
1. 同时触发任何从属集合进行更新。 从属集合是当前集合限制的集合，或者是使用包含或排除规则引用当前集合的集合。

## <a name="collection-evaluation-types-and-triggers"></a>集合评估类型和触发器

此类线程根据评估类型处理集合评估：

- “主要”，用于计划集合更新
- “辅助”，用于手动更新具有从属集合的集合
- “单个”，用于手动更新没有从属集合的集合
- “快速”，用于增量集合更新

下表描述了集合评估触发器及其对应的评估类型。 

| 触发器 | 评估类型 | 说明 |
|---------|-----------------|-------------|
|手动|单个或辅助|“手动”是优先级最高的集合评估。 当管理员请求进行手动集合评估时，集合计算器会将下一个可用评估线程分配给该评估。|
|已计划|主|计划评估的过程与手动评估相同，不同之处在于评估是时间驱动的，而不是事件驱动的。|
|过渡|单个或辅助|所有集合直接或间接依赖于所有系统或所有用户和用户组 。 这两类集合每天凌晨 4:00 执行完整集合评估。 对其中任意一个集合的更改都会根据[完整集合关系图](#collection-evaluation-graph)触发从属集合的更新。
|增量|快速|如果增量集合成员资格的更新发生更改，则增量评估使用集合评估关系图来评估和更新从属集合。 Configuration Manager 监视和更新为增量更新配置的所有集合中的资源对象。<br /><br />如果集合查询基于以后要更新的信息（如硬件清单），则 Configuration Manager 仅在计划集合更新过程中添加资源或从集合中删除资源。|

## <a name="collection-evaluation-graph"></a>集合评估关系图

“集合评估关系图”映射与评估的目标集合相关的所有集合。 集合评估涉及目标集合和集合评估关系图中的任何相关集合。

集合评估开始后，从该周期中的最高级别开始，Configuration Manager 会生成一张关系图，其中包含由于目标集合更改而可能需要评估的所有集合。 然后，集合计算器按顺序遍历关系图，依次评估每个集合成员资格。 完全评估集合后，集合计算器将从集合评估关系图中删除不受此周期影响的低级集合。

如果要评估的一个或多个集合具有包含或排除规则，则集合计算器会将包含或排除的集合添加到关系图中，同时添加集合限制的所有集合。 如果在评估包含和排除集合的过程中发生了任何更改，则关系图将在该分支上继续，然后再返回到主分支。

Configuration Manager 生成两种类型的评估关系图，即“增量”或“完整” 。

### <a name="incremental-collection-evaluation"></a>增量集合评估

当表数据发生更改时，SQL 触发器将在 CollectionNotifications 表中插入一行。 下次触发集合评估计划时，将对现有集合查询与资源 ID 执行 `AND`，并触发已为增量集合启用的集合的更新。

每台计算机的增量集合评估执行一个查询。 增量集合评估的默认站点配置为每五分钟一次。

仅在为增量评估启用了引用的集合时，增量集合评估关系图才会映射这些集合。 如果增量评估仅限于未为增量评估启用的集合，则关系图将根据限制集合的现有成员资格评估集合。 

例如，下图显示了新发现的适用于所有集合的资源。 但是，集合评估仅更新“所有服务器”和“所有域控制器”集合 。 集合计算器不会评估其他集合，因为未为增量评估启用“所有成员服务器”集合。

![增量集合评估关系图示例](media/incremental-collection-evaluation-graph.png)

### <a name="full-collection-evaluation"></a>完整集合评估

手动或计划的集合评估生成所有从属集合的完整集合评估关系图。 该关系图包括引用正在更新的集合和后续集合的所有集合。 只要正在处理集合的更新，Configuration Manager 就会继续评估关系图。

下图显示了“所有服务器”集合的计划或手动集合更新请求如何生成包含所有适用集合的完整关系图。 新的 DNS 服务器和域控制器资源都在所有集合的成员资格查询范围内，因此，所有集合都进行了更新。

![完整集合评估关系图示例 1](media/full-collection-evaluation-graph-1.png)

完整评估并不总是评估所有集合。 如果当前引用的集合发生更新，则集合评估关系图只会继续评估从属集合。 如果增量更新的集合在计划的增量评估过程中更新，则未为增量更新启用的引用集合可能不会更新。 完整评估不会更新集合，而是结束集合评估关系图和该周期的任何引用集合评估。 

在下面的示例中，在现有服务器上安装 DNS 会使其成为“DNS 服务器”集合的成员，但由于其限制“所有成员服务器”集合没有任何更新，因此完整评估不会评估“DNS 服务器”集合  。 下一个增量评估周期将评估“DNS 服务器”集合，因为它是增量集合。

![完整集合评估关系图示例 2](media/full-collection-evaluation-graph-2.png)

## <a name="next-steps"></a>后续步骤
- [如何创建集合](create-collections.md)
- [集合的最佳实践](best-practices-for-collections.md)
- [集合评估查看器](https://docs.microsoft.com/mem/configmgr/core/support/ceviewer)
- 在 TechEd 澳大利亚举办的 [ConfigMgrDogs 故障排除 ConfigMgr 2012](https://channel9.msdn.com/Events/TechEd/Australia/2014/DCI411) 大会
