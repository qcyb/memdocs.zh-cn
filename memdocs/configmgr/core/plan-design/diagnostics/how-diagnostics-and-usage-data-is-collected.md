---
title: 诊断数据集合
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 如何收集关于其自身的诊断和使用情况数据。
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: becfa825-b19f-448c-ab82-bb929255e4ae
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ca40891c840e954f2828833c179f01bcbc6e7448
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688465"
---
# <a name="how-configuration-manager-collects-diagnostics-and-usage-data"></a>Configuration Manager 如何收集诊断和使用情况数据

适用范围：  Configuration Manager (Current Branch)

若要为 Configuration Manager 收集诊断和使用情况数据，每个主站点每周都会运行 SQL Server 查询。 在多站点层次结构中，数据会复制到管理中心站点。  

在层次结构的顶层站点上，服务连接点在检查更新时提交此信息。 服务连接点的模式决定数据的传输方式：

- **联机**：服务连接点每周自动向云服务发送诊断和使用情况数据。

- **脱机**：使用[服务连接工具](../../servers/manage/use-the-service-connection-tool.md)手动传输诊断和使用情况数据。

有关详细信息，请参阅[关于服务连接点](../../servers/deploy/configure/about-the-service-connection-point.md)。

> [!div class="nextstepaction"]
> [如何查看诊断和使用情况数据](view-diagnostics-and-usage-data.md)
