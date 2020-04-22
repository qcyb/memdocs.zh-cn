---
title: 管理查询
titleSuffix: Configuration Manager
description: 了解如何管理查询。 包括用于详细参考的表。
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e562e2a0-8df8-4952-952f-e8c38461c612
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 37050a3a96b732df3f56269592e049077008ab2b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694465"
---
# <a name="how-to-manage-queries-in-configuration-manager"></a>如何管理 Configuration Manager 中的查询

适用范围：  Configuration Manager (Current Branch)

本文介绍了如何在 Configuration Manager 中管理查询。  

 有关如何创建查询的信息，请参阅[如何创建查询](../../../core/servers/manage/create-queries.md)。  

## <a name="manage-queries"></a>管理查询
 在“监视”  工作区中，选择“查询”  ，接着选择要管理的查询，然后选择管理任务。  

 下表列出了管理任务的相关信息。  

|管理任务|详细信息| 
|---------------------|-------------|
|**运行**|运行所选查询并在 Configuration Manager 控制台中显示结果。|
|**安装客户端**|打开“安装客户端向导”  。使用此向导，可以在选定查询返回的计算机上安装 Configuration Manager 客户端。<br /><br /> 此选项不适用于返回移动设备、用户或用户组的查询。 <br /><br /> 有关如何使用客户端请求安装 Configuration Manager 客户端的详细信息，请参阅[将客户端部署到 Windows 计算机](../../clients/deploy/deploy-clients-to-windows-computers.md)。| 
|**导出**|打开“导出对象向导”  。 使用此向导，可以将查询导出到随后可在其他站点导入的托管对象格式 (MOF) 文件。
|**移动**|打开“移动选定项”  对话框。 在此对话框中，可以将选定查询移到之前在“查询”  节点下创建的文件夹中。|

## <a name="next-steps"></a>后续步骤 
 [创建查询](../../../core/servers/manage/create-queries.md)
