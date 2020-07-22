---
title: 配置客户端状态
titleSuffix: Configuration Manager
description: 选择 Configuration Manager 中的客户端状态设置。
ms.date: 07/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a2275ba2-c83d-43e7-90ed-418963a707fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a352e53a672f7fb47416214884fe7adf0fb829cc
ms.sourcegitcommit: 488db8a6ab272f5d639525d70718145c63d0de8f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/14/2020
ms.locfileid: "86384904"
---
# <a name="how-to-configure-client-status-in-configuration-manager"></a>如何在 Configuration Manager 中配置客户端状态

适用范围：Configuration Manager (Current Branch)

先配置站点的客户端状态设置，才能监视 Configuration Manager 客户端和修正问题。 这些设置指定站点用于将客户端标记为不活动的参数。 还可以配置在客户端活动低于指定的阈值时向你发出警报的选项。

## <a name="configure-client-status"></a>配置客户端状态

1. 在 Configuration Manager 控制台中，转到“监视”工作区，然后选择“客户端状态”节点 。 在功能区的“主页”选项卡上，在“客户端状态”组中，选择“客户端状态设置”。  

1. 配置下列设置：

    > [!NOTE]
    > 如果客户端不满足其中任何设置，则站点会将其标记为不活动。

    - **以下几天的客户端策略请求：** 指定自客户端从站点请求策略以来的天数。 默认值为 `7` 天。

      将此值与客户端设置“客户端策略”组中的“客户端策略轮询间隔”设置进行比较。  其默认值为 60 分钟。 换言之，客户端应每小时轮询一次站点以获取策略。 如果客户端一周未请求策略，则站点将其标记为不活动。

    - **以下几天的检测信号发现：** 指定自客户端将检测信号发现记录发送到站点以来的天数。 默认值为 `7` 天。

      将此值与[检测信号发现方法](../../servers/deploy/configure/about-discovery-methods.md)的计划进行比较。 默认情况下，站点每周运行一次检测信号发现。

    - **以下几天的硬件清单：** 指定自客户端将硬件清单记录发送到站点以来的天数。 默认值为 `7` 天。

      将此值与客户端设置“硬件清单”组中的“硬件清单计划”设置进行比较。  其默认值为 7 天。

    - **以下几天的软件清单：** 指定自客户端将软件清单记录发送到站点以来的天数。 默认值为 `7` 天。

      将此值与客户端设置“软件清单”组中的“计划软件清单和文件收集”设置进行比较。  其默认值为 7 天。

    - **以下几天的状态消息：** 指定自客户端将任何状态消息发送到站点以来的天数。 默认值为 `7` 天。 客户端可以发送不同类型活动（如运行任务序列）的状态消息。 站点将在维护任务“删除过期的状态消息”中删除旧状态消息。

1. 指定以下值以确定站点要将客户端状态历史记录数据保持多久：

    - **保留以下几天的客户端状态历史记录：** 默认情况下，站点会将客户端状态信息保留 `31` 天。 此设置不会对客户端或站点行为产生任何影响。 这与客户端状态历史记录的维护任务类似。

## <a name="configure-the-schedule"></a>配置计划

1. 在 Configuration Manager 控制台中，转到“监视”工作区，然后选择“客户端状态”节点 。 在功能区的“主页”选项卡上，在“客户端状态”组中，选择“计划客户端状态更新”。  

1. 配置希望客户端状态更新的时间间隔。

    > [!NOTE]
    > 如果更改客户端状态更新的计划，则在按以前的计划进行下一次计划的客户端状态更新时，更改才会生效。

## <a name="configure-alerts"></a>配置警报

1. 在 Configuration Manager 控制台中，转到“资产和符合性”工作区，并选择“设备集合”节点。

1. 选择要为其配置警报的集合。 在功能区“主页”选项卡的“属性”组中，选择“属性”。

    > [!NOTE]
    > 无法为用户集合配置警报。

1. 切换到“警报”选项卡，然后选择“添加”。 

   > [!TIP]
   > 仅当你的安全角色具有警报的权限时，你才能查看“警报”选项卡。

    选择希望站点为客户端状态阈值生成的警报，然后选择“确定”。

1. 在“警报”选项卡的“条件”列表中，选择每个客户端状态警报，然后指定下列信息： 

    - **警报名称**：接受默认名称，或者输入新的警报名称。

    - **警报严重性**：选择 Configuration Manager 控制台显示的警报级别。

    - **引发警报**：指定警报的阈值百分比。

## <a name="automatic-remediation-exclusion"></a>自动修正排除

1. 在要禁止自动修正的客户端计算机上，打开注册表编辑器。

    > [!WARNING]
    > 如果不正确地使用注册表编辑器，可能会导致严重问题而需要重新安装 Windows。 Microsoft 不保证能够解决因注册表编辑器使用不当而导致的问题。 使用它的风险由你自己承担。

1. 导航到注册表项 HKEY_LOCAL_MACHINE\Software\Microsoft\CCM\CcmEval。

1. 更改 NotifyOnly 项的值：

    - `TRUE`：客户端不会自动修正其发现的任何问题。 但站点仍会在“监视”工作区中通知与此客户端相关的任何问题。

    - `FALSE`：此设置为默认设置。 客户端会在发现问题时自动修正问题，站点会在“监视”工作区中通知你。

安装客户端时，可以通过 NotifyOnly 安装属性将其从自动修正中排除。 有关详细信息，请参阅[关于客户端安装属性](about-client-installation-properties.md)。

## <a name="next-steps"></a>后续步骤

[监视客户端](../manage/monitor-clients.md)
