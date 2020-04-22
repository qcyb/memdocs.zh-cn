---
title: 准备未知计算机部署
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 环境中将操作系统部署到不受 Configuration Manager 管理的计算机。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 9e447e34-0943-49ed-b6ba-3efebf3566c1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6e79e2ec1d42c7ed0e520b5e117fbac73817511a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708815"
---
# <a name="prepare-for-unknown-computer-deployments-in-configuration-manager"></a>在 Configuration Manager 中准备未知计算机部署

适用范围：  Configuration Manager (Current Branch)

使用本主题中的信息将操作系统部署到 Configuration Manager 环境中的未知计算机。 未知计算机是不受 Configuration Manager 管理的计算机。 这意味着 Configuration Manager 数据库中没有这些计算机的记录。 未知计算机包括下列各项：  

- 未安装 Configuration Manager 客户端的计算机  

- 未导入到 Configuration Manager 中的计算机  

- 未被 Configuration Manager 发现的计算机  

  你可以使用下列部署方法将操作系统部署到未知计算机中：  

- [使用 PXE 通过网络部署 Windows](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)  

- [使用可启动媒体部署操作系统](../deploy-use/create-bootable-media.md)  

- [使用预留媒体部署操作系统](../deploy-use/create-prestaged-media.md)  

## <a name="unknown-computer-deployment-workflow"></a>未知计算机部署工作流  
 下面是将操作系统部署到未知计算机的基本工作流：  

-   选择要在部署中使用的未知计算机对象。 可将操作系统部署到“所有未知计算机”集合中的其中一个未知计算机对象  ，也可将  “所有未知计算机”集合中的对象添加到另一个集合。 在“所有未知计算机”  集合中 Configuration Manager 提供了两个未知计算机对象。 一种对象表示 x86 计算机，另一种对象表示 x64 计算机。  

    > [!NOTE]  
    >  “x86 未知计算机”  对象表示仅支持 x86 的计算机。 “x64 未知计算机”  对象表示支持 x86 和 x64 的计算机。 换句话说，这些对象描述目标计算机的体系结构。 它们不描述你要在目标计算机上部署的操作系统。  

-   配置已启用 PXE 的分发点或创建媒体以支持未知计算机部署。  

-   部署用以安装操作系统的任务序列。  

## <a name="unknown-computer-installation-process"></a>未知计算机安装过程  
 第一次从 PXE 或媒体中启动计算机时，Configuration Manage 会进行检查以确定 Configuration Manage 数据库中是否存在该计算机的记录。 如果有记录，Configuration Manager 随后将进行检查以确定是否有部署到该记录的任何任务序列。 如果没有记录，Configuration Manager 将进行检查以确定是否有部署到未知计算机对象的任何任务序列。 在任何一种情况下，Configuration Manager 都会随后执行以下操作之一：  

- 如果有可用的任务序列，Configuration Manager 将提示用户运行该任务序列。  

- 如果有必需的任务序列，Configuration Manager 将自动运行该任务序列。  

- 如果没有为记录部署任务序列，Configuration Manager 将生成错误，指出目标计算机没有任何部署的任务序列。  

  在启动未知计算机时，Configuration Manager 会将该计算机识别为未预配的计算机，而不是未知计算机。 这意味着计算机现在可接收之前部署到未知计算机对象的任务序列。 部署的任务序列随后安装必须包括 Configuration Manager 客户端的操作系统映像。  

  安装 Configuration Manager 客户端之后，将创建计算机的记录，并且计算机会在相应的 Configuration Manager 集合中列出。 如果该计算机未能安装操作系统映像或 Configuration Manager 客户端，则将为该计算机的创建一条“未知”记录，并且该计算机将出现在“所有系统”  集合中。  

> [!NOTE]  
>  在操作系统映像安装过程中，任务序列可从此计算机中检索集合变量，而无法检索计算机变量。  

##  <a name="enabling-unknown-computer-support"></a><a name="BKMK_EnablingUnknown"></a> 启用未知计算机支持  
 在使用 PXE、可启动媒体和预留媒体部署操作系统时，使用以下内容可启用未知计算机支持。  

-   **PXE**  

     在针对 PXE 启用分发点的“PXE”  选项卡上，选中“启用未知计算机支持”  复选框。 有关详细信息，请参阅 [配置分发点以接受 PXE 请求](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)。  

-   **可启动媒体**  

     在创建任务序列媒体向导的“安全”  页上，选中“启用未知计算机支持”  复选框。 有关详细信息，请参阅[配置分发点以接受 PXE 请求](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)和[使用 PXE 与 Configuration Manager 一起通过网络部署 Windows](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)。  

-   **预留媒体**  

     在创建任务序列媒体向导的“安全”  页上，选中“启用未知计算机支持”  复选框。 有关详细信息，请参阅[使用 Configuration Manager 创建预留媒体](../deploy-use/create-prestaged-media.md)。  
