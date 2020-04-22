---
title: 远程控制的先决条件
titleSuffix: Configuration Manager
description: 获取远程控制 Configuration Manager 中的先决条件。
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c1b2057e-b74f-43fa-a293-763a8f866d3d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f19f8799dd90fc61c0bfeeee1dc60125ba491fef
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696415"
---
# <a name="prerequisites-for-remote-control-in-configuration-manager"></a>远程控制 Configuration Manager 中的先决条件

适用范围：  Configuration Manager (Current Branch)

Configuration Manager 中的远程控制具有外部依赖关系和产品中的依赖关系。  

## <a name="dependencies-external-to-configuration-manager"></a>Configuration Manager 的外部依赖关系  

|依赖关系|更多信息|  
|----------------|----------------------|  
|计算机视屏卡驱动程序|为获得最优的远程控制性能，请确保客户端计算机上已安装了最新的视屏驱动程序。|  

 运行 Windows Embedded、Windows Embedded for Point of Service (POS) 以及 Windows Fundamentals for Legacy PC 的设备不支持远程控制查看器，但它们却支持远程控制客户端。  

 Configuration Manager 远程控制不能用于远程管理运行 Systems Management Server 2003 或 Configuration Manager 2007 的客户端计算机。  

> [!NOTE]  
>  没有 Windows 服务是必需的因为远程控制的外部依赖关系。  

### <a name="supported-operating-systems-for-the-remote-control-viewer"></a>支持远程控制查看器的操作系统  
在 Configuration Manager 控制台支持的所有操作系统上，支持使用远程控制查看器。 有关详细信息，请参阅 [Configuration Manager 控制台支持的配置](../../../../core/plan-design/configs/supported-operating-systems-consoles.md)。   

## <a name="configuration-manager-dependencies"></a>Configuration Manager 依赖关系  

|依赖关系|更多信息|  
|----------------|----------------------|  
|必须为客户端启用远程控制|默认情况下，安装 Configuration Manager时，不启用远程控制。 有关如何启用和配置远程控制的信息，请参阅[配置远程控制](../../../../core/clients/manage/remote-control/configuring-remote-control.md)。|  
|Reporting Services 点|在远程控制的报表前，必须先安装 Reporting Services 点站点系统角色。 有关详细信息，请参阅[报表简介](../../../servers/manage/introduction-to-reporting.md)。|  
|管理远程控制的安全权限|访问集合资源和从 Configuration Manager 控制台发起远程控制会话需要：“集合”对象的“读取”、“读取资源”和“远程控制”权限     。<br /><br /> “远程工具操作人员”  安全角色包括这些在 Configuration Manager 中管理远程控制所需要的权限。<br /><br /> 有关详细信息，请参阅[为 Configuration Manager 配置基于角色的管理](../../../../core/servers/deploy/configure/configure-role-based-administration.md)。<br /><br /> 此外，还必须将获准的查看器添加到“远程工具”  客户端设置中的“获准的远程控制和远程协助查看器”  列表中，它们才有权使用远程控制。
