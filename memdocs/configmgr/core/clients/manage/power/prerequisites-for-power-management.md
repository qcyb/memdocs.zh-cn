---
title: 电源管理的先决条件
titleSuffix: Configuration Manager
description: 获取 Configuration Manager 中电源管理的先决条件。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 9c062f13-3c1f-4621-9cae-de0e322aa03f
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: a816d333d96dba6cb1c38f6499ccac78e2db8a3c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696515"
---
# <a name="prerequisites-for-power-management-in-configuration-manager"></a>Configuration Manager 中电源管理的先决条件

适用范围：  Configuration Manager (Current Branch)

Configuration Manager 中的电源管理具有外部依赖关系和产品内依赖关系。  

## <a name="dependencies-external-to-configuration-manager"></a>Configuration Manager 的外部依赖关系  
 下表针对使用电源管理列出了 Configuration Manager 的外部依赖关系。  

|依赖关系|更多信息|  
|----------------|----------------------|  
|客户端计算机必须能够支持所需的电源状态|若要使用电源管理的所有功能，客户端计算机必须能够支持睡眠、休眠、从睡眠状态唤醒，以及从休眠状态唤醒操作。 可以使用“电源功能”  报表来确定计算机是否可以支持这些操作。 有关详细信息，请参阅[如何监视和规划电源管理](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md)主题中的[电源功能报表](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Capabilites)。|  

## <a name="configuration-manager-dependencies"></a>Configuration Manager 依赖关系  
 下表针对使用电源管理列出了 Configuration Manager 的内部依赖关系。  

|依赖关系|更多信息|  
|----------------|----------------------|  
|必须先启用电源管理才能创建和监视电源计划。|有关如何启用和配置电源管理的信息，请参阅[配置电源管理](../../../../core/clients/manage/power/configuring-power-management.md)。|  
|Reporting Services 点|在查看电源管理报表前，必须先配置一个 Reporting Services 点。 有关详细信息，请参阅[报表简介](../../../servers/manage/introduction-to-reporting.md)。|  
