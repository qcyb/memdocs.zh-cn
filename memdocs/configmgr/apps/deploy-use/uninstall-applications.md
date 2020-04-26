---
title: 卸载应用程序
titleSuffix: Configuration Manager
description: 使用 Configuration Manager 卸载应用程序
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 0ea3edaa-27c6-4391-9896-cd97d9c5d06d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1d9b5152c094ecc1470f748c57f2831cfdd66474
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075840"
---
# <a name="uninstall-applications-with-configuration-manager"></a>使用 Configuration Manager 卸载应用程序

适用范围：  Configuration Manager (Current Branch)


执行以下操作可以卸载以前部署的应用程序。

-   在“创建部署类型向导”的“内容”  页上，指定用于卸载部署类型内容的命令行。  

-   使用“卸载”  这项部署操作来部署应用程序。  

> [!IMPORTANT]  
> 某些应用程序类型不支持卸载。  

 此列表提供有关应用程序卸载工作原理的详细信息：  

-   在卸载某个 Configuration Manager (Configuration Manager) 应用程序时，不会自动卸载依赖它的任何应用程序。  

-   如果将使用“卸载”操作的应用程序部署给某用户，则会为计算机的所有用户安装该应用程序。如果此用户的帐户没有卸载该应用程序的权限，则卸载可能会失败  。  

-   如果从应用程序部署到的集合中删除用户或设备，则不会自动从设备中删除应用程序。  

-   部署目的为“卸载”  的部署不会检查要求规则。 如果在运行部署的计算机上安装应用程序，则将会卸载它。  

> [!IMPORTANT]  
> 若要使用“卸载”操作部署应用程序，首先要删除此应用程序中现有的所有应用程序部署、模拟部署和任务序列部署。 

 有关如何创建部署类型的详细信息，请参阅[创建应用程序](../../apps/deploy-use/create-applications.md)。  

 有关如何部署应用程序的详细信息，请参阅[部署应用程序](../../apps/deploy-use/deploy-applications.md)。  

## <a name="uninstall-an-application"></a>卸载应用程序  

1.  使用下列方法之一，通过卸载命令行来配置应用程序部署类型：  

    -   在“创建部署类型向导”的“常规”  页上，选择“从安装文件中自动识别有关此部署类型的信息”  选项。 如果安装文件中提供了此信息，则卸载命令行会自动添加到部署类型属性中。  

    -   在“创建部署类型向导”的“内容”  页的“卸载程序”  字段中指定用于卸载应用程序的命令行。  

        > [!NOTE]  
        >  只有在“创建部署类型向导”的“常规”  页上选择了“手动指定部署类型信息”  选项后，才会显示“内容”  页面。  

    -   在“<部署类型名称> 属性”对话框的“程序”选项卡上，在“卸载程序”字段中指定用于卸载应用程序的命令行    。  

2.  部署应用程序，然后在“部署软件向导”的“部署设置”  页面中，选择“卸载”  部署操作。  

    > [!NOTE]  
    >  在选择部署操作“卸载”  时，部署目的会自动配置为“必需”  。  
