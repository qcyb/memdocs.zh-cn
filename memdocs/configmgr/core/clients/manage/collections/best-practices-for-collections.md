---
title: 集合最佳实践
titleSuffix: Configuration Manager
description: 获取有关在 Configuration Manager 中配置集合和集合计算的建议。
ms.date: 06/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 7a2abb79-9ae5-4a25-9e18-5dcf528de3bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b1bc72a3691e4a6f47c29a5a91ef11c92f0f7e7c
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88693278"
---
# <a name="best-practices-for-collections-in-configuration-manager"></a>Configuration Manager 中的集合最佳实践

适用范围：Configuration Manager (Current Branch)

某些集合管理指南可能相互矛盾。 例如，出于性能方面的考虑，应限制频繁更新的集合的数量。 但频繁更新集合非常方便，因为大多数 Configuration Manager 功能都依赖于集合。 设计和配置集合和集合评估时，请仔细考虑性能影响和业务要求。

使用以下 Configuration Manager 中的集合最佳实践。  

## <a name="configure-maintenance-window-for-updates"></a>配置更新的维护时段

可为设备集合配置维护时段，以限制 Configuration Manager 可在这些设备上安装软件的次数。 如果你将该维护时段配置得太小，则客户端可能无法安装关键的软件更新，这使客户端容易遇到更新可缓解的问题。

规划维护时段时要牢记的重要注意事项：

- 默认的软件更新最大运行时间为 60 分钟。
- Configuration Manager 评估是否可以安装更新时，它会为最大运行时间增加 5 分钟，以将重启计算在内。
- 维护时段的剩余持续时间必须长于软件更新最大运行时间加上 5 分钟之后的值。

## <a name="avoid-frequent-collection-evaluation"></a>避免频繁集合评估

完整的集合评估不仅评估目标集合，而且还评估更新发生时该集合所限制的所有集合。 此外，如果没有计划的集合的限制集合更新，则仍会对该集合进行评估。 因此，可能会比预期更频繁地对某些集合进行评估。

在繁忙的 Configuration Manager 环境中，可以通过缩减日程安排来改善集合评估性能，以避免重复的集合评估。 在深层树中，随着集合在树中的深度下降，可以降低集合评估频率，因为较高级别的集合评估还会触发较低级别的集合评估。

## <a name="understand-the-collection-evaluation-graph"></a>了解集合评估关系图

请注意集合评估关系图的工作原理，以便可以设计适当的集合结构。 不要依赖于完整的集合评估来始终更新所有集合。 如果增量更新的集合按计划进行更新，则未为增量更新启用的引用集合可能不会更新。 由于更新可能在增量评估过程中发生，因此，完整的评估可能不会更新集合，而是结束该周期的集合评估关系图。 在这种情况下，不会进行任何引用集合评估。 有关详细信息，请参阅[集合评估关系图](collection-evaluation.md#collection-evaluation-graph)。

## <a name="limit-incremental-updates"></a><a name="bkmk_incremental"></a> 限制增量更新

为多个集合启用增量更新可能导致评估延迟。 最好将增量更新的集合的数量限制为 200。 确切的数目取决于：

- 集合总数
- 在层次结构中添加和更改新资源的频率
- 层次结构中的客户端数目
- 层次结构中的集合成员身份规则的复杂性

如果增量评估周期所用时间超过配置的更新频率，则 Configuration Manager 会不断处理集合评估，这可能会影响系统性能。 减少增量更新的集合的数量，或增加增量评估周期的时间间隔。

考虑到增量集合的潜在影响，必须制定一个用于创建集合并分配更新计划的策略或过程。 策略注意事项的示例可能如下：

- 仅对用于安全作用域、客户端设置和维护时段的集合使用增量更新。 这些集合更新会影响客户端行为和资源的访问权限。
- 对于没有许可审批的应用程序，请将应用程序播发到现有集合，并使用全局条件来限制可用性。
- 概述计划了完整集合更新的其他集合的适当时间段。

## <a name="avoid-evaluation-of-large-trees-from-the-cas"></a>避免从 CAS 评估大型树

在 Configuration Manager 环境中，管理中心站点 (CAS) 不会对集合成员身份进行评估。 主站点是评估集合的唯一站点。 辅助站点充当代理，只使用从其主站点复制的数据。

为了请求集合更新，CAS 会将请求发送到每个主站点。 主站点评估集合，并将结果发送回 CAS。 仅当所有集合评估指令复制到所有站点，所有站点评估所有集合，并且所有数据返回到 CAS 并进行合并之后，才会显示集合评估结果。

下图演示了 CAS 请求手动集合更新时的流：

![从 CAS 进行手动集合更新](media/manual-collection-update-from-cas.png)

从具有多个主站点的 CAS 进行的集合更新可能很耗时。 如果集合未及时评估，则会重复该请求。

集合评估线程开始并加载评估关系图后，评估将继续，直到集合评估关系图为空。 然后，线程会终止，并可用于下一次评估。 但是，如果在线程评估集合时另一个集合评估周期排队，则该线程会立即重启以尝试评估“错过”的周期。

每个评估方法都在其自己的线程中运行。 在线程中，Configuration Manager 可能会多次尝试绘制同一集合的关系图。 Configuration Manager 随后会删除第二个和后续请求。

若要防止出现这些情况，请避免对大型树进行手动集合评估，尤其是在从具有多个站点的 CAS 进行评估时。

## <a name="consider-collection-depth-and-cross-referencing"></a>考虑集合深度和交叉引用

若要在业务要求和性能之间取得平衡，必须了解所创建的集合结构及其在其他集合上的依赖关系。 如果创建的集合的规则引用了一个或多个集合，且这些集合也引用了其他集合，则将评估所有这些集合以创建集合的成员身份。

Configuration Manager 中的包含和排除集合规则使引用集合比编写自定义 WQL 查询更容易。 但是，如果使用包含和排除集合导致高性能受损，则可以改用 WQL 查询方法：

包含：

`Select * from SMSRSystem where SMSRSystem.ResourceId in (select ResourceID from SMS_CM_RES_COLL_[collection id])`

排除：

`Select * from SMSRSystem where SMSRSystem.ResourceId not in (select ResourceID from SMS_CM_RES_COLL_[collection id])`

## <a name="use-ceviewer-to-monitor-collection-evaluation"></a>使用 CEViewer 监视集合评估

可以使用[集合评估查看器 (CEViewer)](../../../support/ceviewer.md) 来监视正在评估的集合的数量，以及更新每个集合所需的时间。 CEViewer 位于站点服务器上的 CD.Latest 文件夹中。

若要使用 SQL 手动执行类似的检查，可以使用以下查询：

```sql
SELECT [t2].[CollectionName], [t2].[SiteID], [t2].[value] AS [Seconds], [t2].[LastIncrementalRefreshTime], [t2].[IncrementalMemberChanges] AS [IncChanges], [t2].[LastMemberChangeTime] AS [MemberChangeTime]
FROM (
    SELECT [t0].[CollectionName], [t0].[SiteID], DATEDIFF(Millisecond, [t1].[IncrementalEvaluationStartTime], [t1].[LastIncrementalRefreshTime]) * 0.001 AS [value], [t1].[LastIncrementalRefreshTime], [t1].[IncrementalMemberChanges], [t1].[LastMemberChangeTime], [t1].[IncrementalEvaluationStartTime], v1.[RefreshType]
    FROM [dbo].[Collections_G] AS [t0]
    INNER JOIN [dbo].[Collections_L] AS [t1] ON [t0].[CollectionID] = [t1].[CollectionID]
    inner join v_Collection v1 on [t0].[siteid] = v1.CollectionID
    ) AS [t2]
WHERE ([t2].[IncrementalEvaluationStartTime] IS NOT NULL) AND ([t2].[LastIncrementalRefreshTime] IS NOT NULL) and (refreshtype='4' or refreshtype='6')
ORDER BY [t2].[value] DESC
```