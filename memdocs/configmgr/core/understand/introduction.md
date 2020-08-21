---
title: 什么是 Configuration Manager？
titleSuffix: Configuration Manager
description: 了解 Microsoft Endpoint Configuration Manager 的基本信息。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3343eccf-bf09-41cd-9e68-03e893c7f904
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 99e02c190e02a5e017fe2c3f41682ad1624b6051
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699341"
---
# <a name="what-is-configuration-manager"></a>什么是 Configuration Manager？

适用范围：  Configuration Manager (Current Branch)

从版本 1910 开始，Configuration Manager 现在是 Microsoft Endpoint Manager 的一部分。

![Microsoft Endpoint Configuration Manager](media/4960084-endpoint-manager-logo.png)

Microsoft Endpoint Manager 是用于管理所有设备的集成解决方案。 无需复杂迁移，只通过简化授权 Microsoft 就可以将 Configuration Manager 和 Intune 组合在一起。 继续利用现有的 Configuration Manager 投资，同时按照自己的进度获取 Microsoft 云的优势。

以下 Microsoft 管理解决方案现已成为 Microsoft Endpoint Manager  品牌的一部分：

- [Configuration Manager](/configmgr)
- [Intune](/intune)
- [桌面分析](../../desktop-analytics/overview.md)
- [Autopilot](/intune/enrollment/enrollment-autopilot)
- [设备管理管理员控制台](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/microsoft-intune-rolls-out-an-improved-streamlined-endpoint/ba-p/937760)中的其他功能

有关详细信息，请参阅 [Microsoft Endpoint Configuration Manager 常见问题解答](microsoft-endpoint-manager-faq.md)。

## <a name="introduction"></a>简介

使用 Configuration Manager 帮助你执行以下系统管理活动：

- 减少手动任务并让你专注处理高价值项目，从而提高 IT 工作效率和效率。  
- 最大程度实现硬件和软件投资。  
- 在适当时间提供正确的软件，从而提高用户的工作效率。  

Configuration Manager 可实现以下各项以帮助你提供更有效的 IT 服务：

- 应用程序、软件更新和操作系统的安全和可扩展部署。
- 托管设备上的实时操作。
- 面向本地部署和基于 Internet 的设备云计算分析和管理。
- 符合性设置管理。  
- 服务器、台式机和笔记本电脑的全面管理。

Configuration Manager 扩展与许多 Microsoft 技术和解决方案协同工作。 例如，Configuration Manager 可与以下各项集成：  

- Microsoft Intune，共同管理各种移动设备平台
- Microsoft Azure，托管云服务以扩展管理服务
- Windows Server 更新服务 (WSUS)，管理软件更新
- 证书服务
- Exchange Server 和 Exchange Online
- 组策略
- DNS
- Windows 自动部署工具包 (Windows ADK) 和用户状态迁移工具 (USMT)
- Windows 部署服务 (WDS)
- 远程桌面和远程协助

Configuration Manager 也可使用：  

- Active Directory 域服务和 Azure Active Directory，以获取安全性、服务定位和配置，以及发现想要管理的用户和设备。  
- Microsoft SQL Server 作为分布式变更管理数据库，并与 SQL Server Reporting Services (SSRS) 集成以生成报表来监视和跟踪管理活动。  
- 站点系统角色，可扩展管理功能并使用 Internet Information Services (IIS) 的 Web 服务。
- 传递优化、Windows 低额外延迟后台传输 (LEDBAT)、后台智能传输服务 (BITS)、BranchCache 和其他对等缓存技术，以帮助管理网络和设备之间的内容。

要在生产环境中成功使用 Configuration Manager，请彻底规划和测试管理功能。 Configuration Manager 是一款功能强大的管理应用程序，可能会影响组织中的每台计算机。 如果在部署和管理 Configuration Manager 时经过了仔细规划并考虑了业务要求，Configuration Manager 可降低管理开销和总拥有成本。  

## <a name="user-interfaces"></a>用户界面

### <a name="the-configuration-manager-console"></a><a name="BKMK_Console"></a> Configuration Manager 控制台

安装 Configuration Manager 后，使用 Configuration Manager 控制台来配置站点和客户端，以及运行和监视管理任务。 此控制台是主要管理位置，可管理多个站点。  

可在其他计算机上安装 Configuration Manager 控制台，并且通过使用基于 Configuration Manager 角色的管理，限制访问并限制管理用户可以在控制台中看到的内容。  

有关详细信息，请参阅[使用 Configuration Manager 控制台](../servers/manage/admin-console.md)。

### <a name="software-center"></a><a name="BKMK_ApplicationCatalog"></a>软件中心

“软件中心”是在 Windows 设备上安装 Configuration Manager 客户端时安装的应用程序  。 用户可使用软件中心请求并安装部署的软件。 使用软件中心，用户可以执行下列操作：  

- 浏览并安装应用程序、软件更新和新操作系统版本
- 查看其软件请求历史记录
- 查看设备是否符合组织的策略

还可以在软件中心中显示自定义选项卡，以满足其他业务需求。

有关详细信息，请参阅[软件中心用户指南](software-center.md)。

## <a name="next-steps"></a>后续步骤

在安装 Configuration Manager 之前，请熟悉基本概念和术语：

- 如果你熟悉 System Center 2012 Configuration Manager，请参阅[自 System Center 2012 Configuration Manager 以来的更改内容](../plan-design/changes/what-has-changed-from-configuration-manager-2012.md)。

- 有关 Configuration Manager 的高级技术概述，请参阅 [Configuration Manager 的基础知识](fundamentals.md)。

熟悉了基本概念后，使用此文档库帮助成功部署和使用 Configuration Manager。 从以下文章开始：

- [Configuration Manager 的特性和功能](../plan-design/changes/features-and-capabilities.md)  
- [选择设备管理解决方案](../plan-design/choose-a-device-management-solution.md)  
- [通过构建自己的实验室环境来评估 Configuration Manager](../get-started/set-up-your-lab.md)
- [查找使用 Configuration Manager 的帮助](find-help.md)