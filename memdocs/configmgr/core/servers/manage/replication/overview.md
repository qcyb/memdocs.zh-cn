---
title: SQL 复制故障排除
titleSuffix: Configuration Manager
description: 使用这些图示来帮助了解 Configuration Manager 站点之间的 SQL 复制并进行故障排除
ms.date: 02/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 71d7430e-c5aa-485b-8dc0-c80fd8f29f17
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 202a3360b5e04d66ada0d3b47ddd4638c2197167
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703985"
---
# <a name="troubleshoot-sql-replication"></a>SQL 复制故障排除

在多站点层次结构中，Configuration Manager 使用 SQL 复制在站点之间传输数据。 有关详细信息，请参阅[数据库复制](../../../plan-design/hierarchy/database-replication.md)。

为了更好地了解和帮助排查 SQL 复制相关问题，请使用以下图示。

- [SQL 复制](sql-replication.md)
- [SQL 配置](sql-configuration.md)
- [SQL 性能](sql-performance.md)
- [SQL 复制重新初始化 (reinit)](sql-replication-reinit.md)
- [全局数据重新初始化](global-data-reinit.md)
- [站点数据重新初始化](site-data-reinit.md)
- [重新初始化丢失的消息](reinit-missing-message.md)

这些故障排除图示是相互关联的。 使用以下图示了解其关系：

![SQL 复制故障排除过程概述图](media/overview.png)

<!-- PNG used instead of SVG because of weird blankspace in the SVG. The SVG file exists in the same location. -->

有关详细信息，请参阅以下 Microsoft 支持部门的系列博客：

- [ConfigMgr DRS 同步内部机制](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-drs-synchronization-internals/ba-p/1154317)
- [ConfigMgr 2012 数据复制服务 (DRS) 揭秘](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-data-replication-service-drs-unleashed/ba-p/339916)
- [ConfigMgr 2012 DRS – 故障排除常见问题解答](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-drs-troubleshooting-faqs/ba-p/339934)
- [ConfigMgr 2012 DRS 初始化内部机制](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-drs-initialization-internals/ba-p/339948)
- [ConfigMgr 2012：DRS 和 SQL Service Broker 证书问题](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-drs-and-sql-service-broker-certificate-issues/ba-p/339910)
