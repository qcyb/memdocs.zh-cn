---
title: 全局数据重新初始化
titleSuffix: Configuration Manager
description: 使用此图示开始对 Configuration Manager 层次结构中的全局数据进行 SQL 复制重新初始化故障排除
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d36622c0-776c-493b-971a-4a586fc394d4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9fed8a5b257591aa95fcd53b4e12a82249fce762
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694295"
---
# <a name="troubleshoot-global-data-reinit"></a>全局数据重新初始化故障排除

在多站点层次结构中，Configuration Manager 使用 SQL 复制在站点之间传输数据。 有关详细信息，请参阅[数据库复制](../../../plan-design/hierarchy/database-replication.md)。

使用以下图示开始对 Configuration Manager 层次结构中的全局数据进行 SQL 复制重新初始化 (reinit) 故障排除：

![对全局数据重新初始化进行故障排除的图示](media/global-data-reinit.svg)

## <a name="queries"></a>查询

此图示使用以下查询：

### <a name="check-if-site-replication-hasnt-finished-reinit"></a>检查站点复制是否尚未完成重新初始化

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N`Global'
```

### <a name="get-the-trackingguid--status-from-the-primary-site"></a>从主站点获取 TrackingGuid 和状态

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N`Global'
```

### <a name="get-the-trackingguid--status-from-the-cas"></a>从 CAS 获取 TrackingGuid 和状态

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
WHERE RequestTrackingGUID=@trackingGuid
```

### <a name="check-request-status-for-the-tracking-id"></a>检查跟踪 ID 的请求状态

```sql
SELECT Status FROM RCM_InitPackageRequest
WHERE RequestTrackingGUID=@trackGuid
```

## <a name="next-steps"></a>后续步骤

- [重新初始化丢失的消息](reinit-missing-message.md)
