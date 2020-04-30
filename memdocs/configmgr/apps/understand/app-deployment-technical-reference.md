---
title: 应用程序部署排除故障技术参考
titleSuffix: Configuration Manager
description: Configuration Manager 中应用程序部署排除故障技术参考。
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: a4eb09c8-e570-4369-9adb-ded9c8ad3400
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5b3513131b73ac2b63cf18f31b1e39e15ee97420
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688865"
---
# <a name="technical-reference-for-application-deployment-in-configuration-manager"></a>在配置管理器中的应用程序部署的技术参考

适用范围：  Configuration Manager (Current Branch)

在本文中，你将了解应用程序部署的工作原理。

## <a name="before-you-begin"></a>准备工作

如果要对应用程序部署进行故障排除，则在检查客户端日志时，有几个项很有用。 这些项包括：

- 应用程序 CI ID
- 应用程序唯一 ID
- 部署类型唯一 ID
- 应用程序部署唯一 ID（也称为分配唯一 ID）
- 应用程序部署目的
- 内容唯一 ID
- 集合 ID 和名称
- 集合类型

要简化故障排除，可针对 Configuration Manager 数据库运行如下所示的 SQL 查询，以获取上面列出的信息。

```sql
SELECT APP.CI_ID [App CI ID], APP.CI_UniqueID [App Unique ID], APP.DisplayName [App Name],
DT.CI_UniqueID [DT Unique ID], DT.ContentId [DT Content ID],
CIA.Assignment_UniqueID [Assignment ID], CIA.CollectionID, CIA.CollectionName,
CASE CIA.OfferTypeID WHEN 0 THEN 'Required' WHEN 2 THEN 'Available' WHEN 3 THEN 'Simulate' ELSE 'Unknown' END AS [Deployment Purpose],
CASE C.CollectionType WHEN 1 THEN 'User Collection' WHEN 2 THEN 'Device Collection' ELSE 'Unknown' END AS [Collection Type],
DT.Technology, DT.DisplayName [DT Name]
FROM fn_ListApplicationCIs(1033) APP
JOIN fn_ListDeploymentTypeCIs(1033) DT ON DT.AppModelName = APP.ModelName AND DT.IsLatest = 1
LEFT JOIN v_CIAssignmentToCI CIACI ON CIACI.CI_ID = APP.CI_ID
LEFT JOIN v_CIAssignment CIA ON CIACI.AssignmentID = CIA.AssignmentID
LEFT JOIN v_Collection C ON C.CollectionID = CIA.CollectionID
WHERE APP.IsLatest = 1 AND APP.DisplayName = 'Application Name' -- Replace Application Name
```

> [!IMPORTANT]
> 执行此查询时，必须使用“应用程序属性”的“常规信息”选项卡中列出的应用程序名称，而不是使用“应用程序属性”的“软件中心”选项卡中列出的本地化应用程序名称  。

## <a name="next-steps"></a>后续步骤

- [应用程序部署策略](deployment-policy-technical-reference.md)
