---
title: 创建 App-V 虚拟环境
titleSuffix: Configuration Manager
description: 使用 Microsoft Application Virtualization 创建虚拟环境，使应用可以相互共享数据。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: b6b86078-fcc4-46cf-87d6-4b52b914b712
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2280218d3d237f91f0db3150dbc2031bad3e1816
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689725"
---
# <a name="create-app-v-virtual-environments-in-configuration-manager"></a>在 Configuration Manager 中创建 App-V 虚拟环境

适用范围：  Configuration Manager (Current Branch)

在 Configuration Manager 中的 Microsoft Application Virtualization (App-V) 虚拟环境中，已部署的虚拟应用程序可在客户端 Windows 电脑上共享相同的文件系统和注册表。 与标准虚拟应用程序不同，这些应用程序可以相互共享数据。 在安装应用程序时，或者在客户端接下来评估已安装的应用程序时，会在客户端电脑上创建或修改虚拟环境。 可以对这些应用程序进行排序，以便在多个应用程序尝试修改一个文件系统或注册表值时，排在最前面的应用程序优先进行修改。  

> [!IMPORTANT]  
>  不要依靠 App-V 虚拟环境来提供安全保护（例如抵御恶意软件）。  

 使用下列过程在 Configuration Manager 中创建 App-V 虚拟环境。  

## <a name="create-an-app-v-virtual-environment"></a>创建 App-V 虚拟环境  

1.  在 Configuration Manager 控制台中，选择“软件库”   > “应用程序管理”   > “App-V 虚拟环境”  。  

3.  在“主页”  选项卡的“创建”  组中，选择“创建虚拟环境”  。  

4.  在“创建虚拟环境”  对话框中，输入下列信息：  

    -   **名称**。  输入虚拟环境的唯一名称（最多 128 个字符）。  

    -   **说明**。 （可选）输入虚拟环境的说明。  

5.  若要将新的部署类型添加到虚拟环境中，请选择“添加”  。 必须添加至少一种部署类型。  

6.  在“添加应用程序”  对话框中，指定**组名**（最多 128 个字符）。 用户可以使用此名称指代添加到虚拟环境的应用程序组。  

7.  选择“添加”  ，选择要添加到组中的 App-V 5 应用程序和部署类型，然后选择“确定”  。  

8.  在“添加应用程序”  对话框中，可以选择“升序”  或“降序”  ，以设置在多个应用程序尝试修改同一个虚拟环境中的文件系统或注册表设置时哪个应用程序将优先进行修改。  

9. 若要返回到“创建虚拟环境”  对话框，请选择“确定”  。  

10. 在完成添加组的操作后，选择“确定”  以创建虚拟环境。 新的虚拟环境显示在 Configuration Manager 控制台的“App-V 虚拟环境”  节点中。 可以使用“App-V 虚拟环境状态”报告来监视虚拟环境的状态。  

    > [!NOTE]  
    >  在安装应用程序时，或者在客户端接下来评估已安装的应用程序时，会在客户端电脑上添加或修改虚拟环境。  
