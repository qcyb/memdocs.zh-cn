---
title: 监视 Linux/UNIX 客户端
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中监视 Linux 和 UNIX 服务器上的客户端。
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d827cf91-b18f-4ee7-b538-24ba6f003ab9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d2ea3a0b630e1710aeaf74a4349f202806d45039
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696765"
---
# <a name="how-to-monitor-clients-for-linux-and-unix-servers-in-configuration-manager"></a>如何在 Configuration Manager 中监视 Linux 和 UNIX 服务器上的客户端

适用范围：  Configuration Manager (Current Branch)

> [!Important]  
> 从版本 1902 开始，Configuration Manager 不支持 Linux 或 UNIX 客户端。 
> 
> 请考虑使用 Microsoft Azure 管理来管理 Linux 服务器。 Azure 解决方案具有广泛的 Linux 支持（包括面向 Linux 的端到端补丁管理），在大多数情况下优于 Configuration Manager 的功能。

可以使用查看基于 Windows 的客户端的信息的相同方法在 Configuration Manager 控制台中查看来自于 Linux 和 UNIX 服务器的信息。  

 可以查看的信息包括:  

- 客户端的状态详细信息（在 Configuration Manager 控制台仪表板中）  

- 默认 Configuration Manager 报表中有关客户端的详细信息  

- 资源浏览器中的清单详细信息  

  以下各节描述了如何从资源浏览器和报表中获取这些详细信息。  

##  <a name="use-resource-explorer-to-view-inventory-for-linux-and-unix-servers"></a><a name="BKMK_UseResourceExpforLnU"></a> 使用资源浏览器查看适用于 Linux 和 UNIX 服务器的清单  

 在 Configuration Manager 客户端向 Configuration Manager 站点提交硬件清单后，可以使用资源浏览器查看此信息。 适用于 Linux 和 UNIX 的 Configuration Manager 客户端不会向资源浏览器添加新的清单类或视图。 Linux 和 UNIX 清单数据映射到现有的 WMI 类。 可以使用资源浏览器在基于 Windows 的分类中查看 Linux 和 UNIX 服务器的详细清单信息。  

 例如，可以收集在 Linux 和 UNIX 服务器上找到的所有以本机方式安装的程序的列表。 以本机方式安装的程序的示例包括 Linux 中的 **.rpms** 或 Solaris 中的 **.pkgs** 。 在 Linux 或 UNIX 客户端提交清单后，可以在 Configuration Manager 控制台内资源浏览器中查看所有以本机方式安装的 Linux 或 UNIX 程序列表。  

 有关如何使用资源浏览器的信息，请参阅[如何使用资源浏览器来查看硬件清单](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md)。  

##  <a name="how-to-use-reports-to-view-information-for-linux-and-unix-servers"></a><a name="BKMK_UseReportsforLnU"></a> 如何使用报表来查看 Linux 和 UNIX 服务器的信息  
 Configuration Manager 的报表包括来自 Linux 和 UNIX 服务器的信息以及来自基于 Windows 的计算机的信息。 无需其他配置就可将 Linux 和 UNIX 数据集成到报表中。  

 例如，如果运行名为“操作系统版本计数”的报表，该报表会显示不同操作系统的列表和运行每个操作系统的客户端数目。 报表基于运行于不同操作系统的不同 Configuration Manager 客户端所发送的硬件清单信息。  

 还可以创建特定于 Linux 和 UNIX 服务器数据的自定义报表。 硬件清单类“操作系统”  的“标题”  属性的是一个有用的属性，可用于在报表查询中标识特定的操作系统。  

 有关 Configuration Manager 中报表的信息，请参阅[报表简介](../../servers/manage/introduction-to-reporting.md)。  
