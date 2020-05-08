---
title: 诊断和使用情况数据
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 收集的关于其自身的诊断和使用情况数据。
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 88ac4e55-d47b-4c94-b9c3-704c6a48b845
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ffa50d2cfb3095eb136128c09b74e9ee6a4eb501
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904396"
---
# <a name="diagnostics-and-usage-data-for-configuration-manager"></a>Configuration Manager 的诊断和使用情况数据

适用范围：  Configuration Manager (Current Branch)

Configuration Manager 收集有关自身的诊断和使用情况数据，Microsoft 使用这些数据改进将来版本的安装体验、质量和安全性。  

每个 Configuration Manager 层次结构都启用诊断和使用情况数据。 它包含在每个主站点和管理中心站点 (CAS) 每周运行一次的 SQL Server 查询。 层次结构使用 CAS 时，子主站点会将其数据复制到相应的 CAS。 在层次结构的顶层站点上，[服务连接点](../../servers/deploy/configure/about-the-service-connection-point.md)在检查更新时提交此信息。 如果服务连接点处于脱机模式下，则通过使用[服务连接工具](../../servers/manage/use-the-service-connection-tool.md)传输信息。

> [!NOTE]  
> Configuration Manager 仅从站点 SQL Server 数据库收集数据，而不会直接从客户端或站点服务器收集数据。  

有关详细信息，请参阅 [Microsoft 隐私声明](https://privacy.microsoft.com/privacystatement)。  

> [!div class="nextstepaction"]
> [Microsoft 如何使用诊断和使用情况数据](how-diagnostics-and-usage-data-is-used.md)
