---
title: SQL 配置
titleSuffix: Configuration Manager
description: 使用此图示开始对 Configuration Manager 的 SQL 配置进行故障排除
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 95ab8cbd-0807-4422-823a-f5f9314ba623
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b909d992dc16b6e786c62143347ed420d913dbc5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707615"
---
# <a name="sql-configuration"></a>SQL 配置

在多站点层次结构中，Configuration Manager 使用 SQL 复制在站点之间传输数据。 有关详细信息，请参阅[数据库复制](../../../plan-design/hierarchy/database-replication.md)。

使用以下图示开始对与 SQL Service Broker 相关的 SQL 配置进行故障排除：

![SQL 配置故障排除图示](media/sql-configuration.svg)

## <a name="queries"></a>查询

此图示包含以下查询和操作：

### <a name="check-if-sql-can-deliver-ssb-messages"></a>检查 SQL 能否传递 SSB 消息

```sql
SELECT transmission_status, *
FROM sys.transmission_queue
ORDER BY enqueue_time DESC
```

## <a name="remediation-actions"></a>修正操作

### <a name="remediate-the-issues-reported-from-transmission_status"></a>修正 transmission_status 报告的问题

常见问题：

- 防火墙配置
- 网络配置
- SSB 证书配置错误

### <a name="run-sql-profiler-to-trace-ssb-events"></a>运行 SQL 探查器以跟踪 SSB 事件

在 CAS 和主站点数据库上运行 SQL 探查器以跟踪与 SQL Service Broker 相关的事件：

- **审核 Broker 登录**
- **审核 Broker 会话**
- Broker  类别中的事件
