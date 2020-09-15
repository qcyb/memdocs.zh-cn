---
title: 为服务器组提供服务
titleSuffix: Configuration Manager
description: 服务器组已替换为业务流程组
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/01/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 304a83ea-0f72-437d-9688-2e6e0c7526dd
ms.openlocfilehash: a5475d2a33ebcf7fb2e1500a8dc6573180b9a70c
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/09/2020
ms.locfileid: "89608406"
---
# <a name="service-a-server-group"></a>为服务器组提供服务

适用范围：  Configuration Manager (Current Branch)

>[!IMPORTANT]
> - 从 Configuration Manager 版本 2002 开始，服务器组已替换为业务流程组。 有关详细信息，请参阅[业务流程组](orchestration-groups.md)。
> - 预发行功能是指 Current Branch 中的功能，用于在生产环境中的早期测试。 这些功能完全受支持，但仍在开发过程中，所以在从预发行类别中划出之前，可能会有所变更。 必须启用此功能，使其可供使用。 有关详细信息，请参阅[使用更新中的预发行功能](../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease)。

从 Configuration Manager 版本 1606 开始，可以为集合配置服务器组设置，以定义集合中安装软件更新的计算机的数量、百分比和顺序。 还可以配置预先部署和后期部署 PowerShell 脚本以运行自定义操作。

将软件更新部署到配置了服务器组设置的集合时，Configuration Manager 将确定集合中有多少台计算机可以在任意给定时间安装软件更新，并提供相同数量的部署锁定。 只有获得部署锁定的计算机会启动软件更新安装。 当部署锁定可用时，计算机将获取该部署锁定、安装软件更新，然后在软件更新安装成功完成时解除部署锁定。 然后，该部署锁定便可用于其他计算机。 如果计算机无法解除部署锁定，则可以手动解除集合的所有服务器组部署锁定。

>[!IMPORTANT]
>集合中的所有计算机必须分配到同一站点。

#### <a name="to-create-a-collection-for-a-server-group"></a>创建服务器组的集合  
在设备集合的属性中配置服务器组。 若要为服务器组提供服务，集合中的所有成员必须分配到同一站点。 使用以下步骤创建集合并配置服务器组设置：
1.  [创建一个设备集合](../../core/clients/manage/collections/create-collections.md)，使其包含服务器组中的计算机。  

2.  在“资产和符合性”  工作区中，单击“设备集合”  ，右键单击包含服务器组中的计算机的集合，然后单击“属性”  。  

3.  在“常规”  选项卡上，选择“所有设备均为相同服务器组的一部分”  ，然后单击“设置”  。  

4.  在“服务器组设置”  页上指定下列设置之一：  

    -   **允许同时更新一定比例的计算机**：指定一次只更新一定百分比的客户端。 例如，如果集合中有 10 个客户端，并且配置该集合为可同时更新 30% 的客户端，则在任何给定时间只有 3 个客户端可安装软件更新。  

    -   **允许同时更新多台计算机**：指定一次只更新一定数量的客户端。  

    -   **指定维护日程安排**：指定集合中的客户端将按配置的顺序一次更新一个。 列表中位于某客户端前面的客户端完成安装其软件更新后，该客户端才能安装软件更新。  

5.  指定是否使用部署前（节点排出）脚本或部署后（节点恢复）脚本。  

    > [!WARNING]
    > Microsoft 不对自定义脚本进行签名。 维护这些脚本的完整性是你的责任。

    > [!TIP]  
    > 以下是可用于测试当前时间写入文本文件的部署前和部署后脚本的示例：  
    >   
    >  **前期部署**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\Windows\Temp\start.txt`  
    >   
    >  **后期部署**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\Windows\Temp\end.txt`  

## <a name="deploy-software-updates-to-the-server-group-and-monitor-status"></a>将软件更新部署到服务器组并监视状态  
使用典型的部署过程将软件更新部署到服务器组集合。 部署软件更新后，可以在 Configuration Manager 控制台中监视软件更新部署。
1.  将[软件更新部署](manually-deploy-software-updates.md)到服务器组集合。   

2.  [监视软件更新部署](monitor-software-updates.md)。 除了软件更新部署的标准监视视图之外，客户端在等待安装软件更新时，还将显示**等待锁定**状态。 有关详细信息，可查看 UpdatesDeployment.log 文件。


## <a name="clear-the-deployment-locks-for-computers-in-a-server-group"></a>清除服务器组中计算机的部署锁定  
如果计算机未能解除部署锁定，则可以手动解除集合的所有服务器组部署锁定。 仅当部署无法继续更新集合中的计算机并且仍然有不符合的计算机时，才会清除锁定。  
1.  在“资产和符合性”  工作区中，单击“设备集合”  ，然后单击要清除部署锁定的集合。  

2.  在“主页”  选项卡的“部署”  组中，单击“清除服务器组部署锁定”  。 当客户端未能安装软件更新并阻止其他客户端安装其软件更新时，可以手动清除部署锁定。  
