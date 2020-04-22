---
title: 站点服务器弃用的内容
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 站点服务器不再支持的产品和操作系统。
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d53ac075-438b-41da-ab85-42f33982da0c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2b6f9dfae2eaa4e7fac4cc9b059b608de3c1386a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702565"
---
# <a name="removed-and-deprecated-for-configuration-manager-site-servers"></a>Configuration Manager 站点服务器已删除和已弃用的内容

适用范围：  Configuration Manager (Current Branch)

本文介绍 Configuration Manager 站点服务器的支持中删除的，或者将在未来更新中删除（弃用）的产品和操作系统。 针对可能会影响使用 Configuration Manager 的将来更改提出早期通知。  

此信息以后可能会有所更改。 它可能不包括每个已弃用的功能、产品或操作系统。  

## <a name="server-os"></a>服务器 OS  

|操作系统|首次宣布弃用|删除的支持|
|-|-|-|
|Windows Server 2008 R2 SP1|2015 年 10 月| 版本 1702|
|带 SP2 的 Windows Server 2008|2015 年 10 月|版本 1511|

## <a name="sql-server"></a>SQL Server

|SQL Server 版本|首次宣布弃用|删除的支持|
|-|-|-|
|SQL Server 2008 R2|2015 年 10 月|版本 1702|
|SQL Server 2008|2015 年 10 月|版本 1511|

如果需要升级 SQL Server 版本，建议采用以下由易到难的方法：

1. [就地升级 SQL Server](../../../servers/manage/upgrade-on-premises-infrastructure.md#BKMK_SupConfigUpgradeDBSrv)（推荐）。  

2. 在一台新计算机上安装 SQL Server 的新版本。 然后使用 Configuration Manager 安装程序的[数据库移动选项](../../../servers/manage/modify-your-infrastructure.md#bkmk_dbconfig)指向新 SQL Server 上的站点服务器。  

3. 使用[备份和恢复](../../../servers/manage/backup-and-recovery.md)。  

## <a name="next-steps"></a>后续步骤

有关详细信息，请参阅下列文章：

- [已删除和已弃用的项](removed-and-deprecated.md)  

- [Microsoft 支持生命周期](https://support.microsoft.com/lifecycle)  

- [对 Configuration Manager Current Branch 版本的支持](../../../servers/manage/current-branch-versions-supported.md)  
