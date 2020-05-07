---
title: Endpoint Protection 恶意软件定义
titleSuffix: Configuration Manager
description: 了解如何配置 Configuration Manager 软件更新以将定义更新交付到客户端计算机。
ms.date: 04/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3b9c4027-a98b-406b-935c-ccabcfe713df
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c0b734fe2a63373e8fd1af9abe77cde7f52b6824
ms.sourcegitcommit: 2871a17e43b2625a5850a41a9aff447c8ca44820
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2020
ms.locfileid: "82126085"
---
# <a name="use-configuration-manager-to-deliver-definition-updates"></a>使用 Configuration Manager 来交付定义更新

适用范围：  Configuration Manager (Current Branch)

可配置 Configuration Manager 软件更新，以将定义更新自动交付到客户端计算机。 在开始创建自动部署规则之前，请务必配置 Configuration Manager 软件更新。 有关详细信息，请参阅[软件更新简介](../../sum/understand/software-updates-introduction.md)。

> [!NOTE]
> 此过程特定于 Endpoint Protection。 有关自动部署规则的更常规信息，详细信息，请参阅[自动部署软件更新](../../sum/deploy-use/automatically-deploy-software-updates.md)。

1. 在 Configuration Manager 控制台中，转到“软件库”工作区  。 展开“软件更新”，然后选择“自动部署规则”   。

1. 在功能区的“主页”选项卡上的“创建”组中，选择“创建自动部署规则”    。

1. 在“创建自动部署规则向导”  的“常规”  页上，指定下列信息：

    - **名称**：输入自动部署规则的唯一名称。

    - **集合**：选择你想要将定义更新部署到的设备集合。

        > [!NOTE]
        > 不能将定义更新部署到用户集合。

1. 选择“添加到现有软件更新组”  。

1. 选择“运行此规则后启用部署”  。

1. 在向导的“部署设置”页面上，对于“详细信息级别”，选择“仅错误消息”    。

    > [!NOTE]
    > 选择“仅错误消息”时，会减少定义部署发送的状态消息数  。 此配置有助于减少 Configuration Manager 服务器上的 CPU 处理量。

1. 在“软件更新”  页面上：

    1. 选择“更新分类”属性筛选器  。 在“搜索条件”列表中，选择“<要查找的项\>”   。

        在“搜索条件”窗口中，选择“定义更新”，然后选择“确定”    。

    1. 获取“产品”属性筛选器  。 在“搜索条件”列表中，选择“<要查找的项\>”   。

        在“搜索条件”窗口中，选择“System Center Endpoint Protection”（针对 Windows 8.1 及更低版本）或“Windows Defender”（针对 Windows 10 及更高版本），然后选择“确定”     。

    > [!NOTE]
    > 可根据需要筛选被取代的更新。 选择“已被取代”  属性筛选器。 在“搜索条件”列表中，选择“<要查找的项\>”   。 在“搜索条件”窗口中，选择“否”，然后选择“确定”    。

1. 在向导的“评估计划”页面上，选择“在任何软件更新点同步之后运行规则”   。

1. 在向导的“部署计划”  页上配置下列设置：

    - **时间基于**：如果客户端同时安装最新定义，请选择“UTC”  。 实际安装时间有所变化，但不超过两小时。

    - **软件可用时间**：指定此规则创建的部署可用的时间。 指定的时间必须至少为自动部署规则运行之后的一小时。 此配置可确保有足够时间将内容复制到分发点。 一些定义更新还可能包括反恶意软件引擎更新，这些更新可能要花更长时间才能到达分发点。

    - **安装截止时间**：选择“尽快”  。

        > [!NOTE]
        > 软件更新截止时间有所不同，但都在两小时内。 此行为可防止所有客户端同时请求某一个更新。

1. 在向导的“用户体验”页面上，对于“用户通知”，选择“在软件中心和所有通知中隐藏”    。 通过此配置，定义更新安装时无提示。

1. 在向导的“部署包”页面上，选择现有部署包或创建新的部署包  。

    > [!NOTE]
    > 考虑将定义更新放置在不包含其他软件更新的包中。 此策略可保持定义更新包的大小较小，从而使其可以更快复制到分发点。

1. 如果创建新的部署包，则在向导的“分发点”页面上，选择一个或多个分发点  。 站点会将此包的内容复制到这些分发点。

1. 在向导的“下载位置”页面中，选择“从 Internet 下载软件更新”   。

1. 在向导的“语言选择”页面中，选择要下载的更新的每个语言版本  。

1. 在“下载设置”页面上，选择必要的软件更新下载行为  。

1. 完成向导。

验证 Configuration Manager 控制台的“自动部署规则”节点是否显示新规则  。

> [!div class="nextstepaction"]
> [创建和部署反恶意软件策略](endpoint-antimalware-policies.md)
