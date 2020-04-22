---
title: 报告的先决条件
titleSuffix: Configuration Manager
description: 了解影响在 Configuration Manager 中使用报表的各种依赖关系。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9cc508a5-5023-4833-b776-ae9a6971138f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e08833a5ef560a0f958fe68b4ade0d4717dffc73
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703515"
---
# <a name="prerequisites-for-reporting-in-configuration-manager"></a>Configuration Manager 中报表的先决条件

适用范围：  Configuration Manager (Current Branch)

Configuration Manager 中的报表具有以下依赖关系：

- SQL Server Reporting Services
- Reporting Services 点
- Power BI 报表服务器（可选，从版本 2002 开始）

## <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

必须先安装和配置 SQL Server Reporting Services，然后才能在 Configuration Manager 中使用报表。

有关规划和部署 Reporting Services 的详细信息，请参阅[安装 SQL Server Reporting Services](https://docs.microsoft.com/sql/reporting-services/install-windows/install-reporting-services)。

在 64 位 SQL Server 安装的默认实例或命名实例上安装 Reporting Services 数据库。 将 SQL Server 实例与站点系统服务器并置，或在远程计算机上对其进行配置。

Configuration Manager 为报表提供的 SQL Server 版本支持与其为站点数据库提供的 SQL Server 版本支持相同。 有关详细信息，请参阅[支持的 SQL Server 版本](../../plan-design/configs/support-for-sql-server-versions.md#bkmk_SQLVersions)。

## <a name="reporting-services-point"></a>Reporting Services 点

必须先配置 Reporting Services 点站点系统角色，然后才能在 Configuration Manager 中使用报表。

有关详细信息，请参阅[站点和站点系统先决条件](../../plan-design/configs/site-and-site-system-prerequisites.md#bkmk_2012RSpoint)。

## <a name="power-bi-report-server"></a>Power BI 报表服务器

从版本 2002 开始，可以将报表与 Power BI 报表服务器集成。 有关详细信息（包括先决条件），请参阅[与 Power BI 报表服务器集成](powerbi-report-server.md)。

## <a name="next-steps"></a>后续步骤

[配置报表](configuring-reporting.md)
