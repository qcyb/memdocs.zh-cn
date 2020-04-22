---
title: 集合先决条件
titleSuffix: Configuration Manager
description: 获得在 Configuration Manager 中使用集合的先决条件。
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a53e4cf1-518a-4210-9c16-022c4261d2fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 313c3183cd6401390d743575ba513026a3e3f607
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695535"
---
# <a name="prerequisites-for-collections-in-configuration-manager"></a>Configuration Manager 中的集合的先决条件

适用范围：  Configuration Manager (Current Branch)

Configuration Manager 中的集合仅包含产品内部的依赖关系。  

## <a name="configuration-manager-dependencies"></a>Configuration Manager 依赖关系  

|依赖关系|更多信息|  
|----------------|----------------------|  
|Reporting Services 点|在运行集合的报表前，必须先安装 Reporting Services 点站点系统角色。 有关详细信息，请参阅[报表简介](../../../servers/manage/introduction-to-reporting.md)。|  
|必须授予特定的安全权限来管理集合|必须具有以下安全权限才能管理符合性设置：<br /><br /> - 创建和管理集合需要：“集合”对象的“创建”、“删除”、“修改”、“修改文件夹”、“移动对象”、“读取”和“读取资源”权限         。<br /><br /> - 管理集合设置需要：“集合”对象的“修改集合设置”权限   。<br /><br /> 所有集合文件夹（包括根文件夹）都需要“修改文件夹”  权限。|  
