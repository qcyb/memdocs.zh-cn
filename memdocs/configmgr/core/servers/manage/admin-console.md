---
title: Configuration Manager 控制台
titleSuffix: Configuration Manager
description: 了解如何导航 Configuration Manager 控制台。
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 463ce307-59dd-4abd-87b8-42ca9db178d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: bcc1f8e93f4fb312b74fd7e5746928182b05710f
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126488"
---
# <a name="how-to-use-the-configuration-manager-console"></a>如何使用 Configuration Manager 控制台

适用范围：  Configuration Manager (Current Branch)

管理员使用 Configuration Manager 控制台管理 Configuration Manager 环境。 本文介绍导航控制台的基础知识。  

## <a name="open-the-console"></a><a name="bkmk_open"></a> 打开控制台

Configuration Manager 控制台始终安装在每个站点服务器上。 你还可以将其安装在其他计算机上。 有关详细信息，请参阅[安装 Configuration Manager 控制台](../deploy/install/install-consoles.md)。

在 Windows 10 计算机上打开控制台的最简单方法是按“开始”并键入 `Configuration Manager console` 。 你可能无需为 Windows 键入整个字符串就可找到最佳匹配。

如果浏览“开始”菜单，请在“Microsoft Endpoint Manager”组中查找“Configuration Manager 控制台”图标   。

![Microsoft Endpoint Manager“开始”菜单图标](media/microsoft-endpoint-manager-start-menu.png)

> [!NOTE]
> 版本 1910 中的“开始”菜单路径已更改。 在 1906 及更早版本中，文件夹名为“System Center”  。 将 Configuration Manager 更新到 1910 或更高版本时，请确保更新你维护的任何内部文档以包含此新位置。

## <a name="connect-to-a-site-server"></a>连接到站点服务器

控制台可连接到管理中心站点服务器或主站点服务器。 但是，无法将 Configuration Manager 控制台连接到辅助站点。 安装过程中，指定控制台连接的站点服务器的完全限定的域名 (FQDN)。

要连接到其他站点服务器，请按以下步骤操作：

1. 选择[功能区](#ribbon)顶部的箭头，然后选择“连接到新站点”  。  

    ![将控制台连接到新站点](media/connect-to-a-new-site.png)  

2. 键入站点服务器的 FQDN。 如果之前已连接到站点服务器，可从下拉列表中选择服务器。  

    ![站点连接窗口，输入站点服务器的 FQDN](media/site-server-fqdn.png)  

3. 选择“**连接**”。  

从版本 1810 开始，可以为管理员指定访问 Configuration Manager 站点的最低身份验证级别。 此功能强制管理员以要求的级别登录到 Windows。 有关详细信息，请参阅[规划 SMS 提供程序](../../plan-design/hierarchy/plan-for-the-sms-provider.md#bkmk_auth)。 <!--1357013-->  

## <a name="navigation"></a>导航

控制台的某些区域可能未显示，具体取决于所分配的安全角色。 有关角色的详细信息，请参阅[基于角色的管理基础](../../understand/fundamentals-of-role-based-administration.md)。

### <a name="workspaces"></a>工作区

Configuration Manager 控制台中有四个工作区  ：  

- **资产和符合性**  

- **软件库**  

- **监视**  

- **管理**  

![带上下文菜单的 Configuration Manager 工作区](media/configuration-manager-workspaces.png)  

选择向下箭头并选择“导航窗格选项”，可对工作区按钮重新进行排序  。 选中某个项“上移”或“上移”   。 单击“重置”还原默认按钮顺序  。  

![用于对工作区重新排序的“导航窗格选项”窗口](media/navigation-pane-options.png)  

选择“显示更少按钮”可最小化工作区按钮  。 列表中的最后一个工作区首先最小化。 选择已最小化的按钮并选择“显示更多按钮”即可将按钮恢复为原始大小  。

![Configuration Manager 控制台中最小化的工作区](media/workspace-buttons.png)  

### <a name="nodes"></a>节点

工作区是一系列节点  。 其中一个节点是“软件库”工作区中的“软件更新组”节点   。

在节点中可选择箭头以最小化导航窗格。  

![示例节点和突出显示的最小化箭头](media/software-update-groups-node.png)  

当导航窗格处于最小化时，使用“导航栏”在控制台中移动  。  

![最小化的 Configuration Manager 导航窗格](media/minimized-navigation-pane.png)  

在控制台中，节点有时会被整理到文件夹中。 选择文件夹时，通常会显示导航索引或仪表板   。  

![Configuration Manager 软件更新导航索引](media/software-updates-navigation-index.png)  

### <a name="ribbon"></a>功能区

功能区位于 Configuration Manager 控制台顶部。 功能区可以有多个选项卡，且可使用右侧的箭头将其最小化。 功能区上的按钮数量因节点而异。 上下文菜单中也提供了功能区中的大多数按钮。  

![示例功能区，突出显示多个选项卡和最小化箭头](media/ribbon.png)

### <a name="details-pane"></a>细节窗格

若要获取有关项的其他信息，可查看细节窗格。 细节窗格中可以有一个或多个选项卡。 选项卡的数量因节点而异。  

![Configuration Manager 示例细节窗格](media/details-pane.png)

### <a name="columns"></a>列

可添加、删除、重新排列并调整列的大小。 通过这些操作，可让系统显示你喜欢的数据。 可用列的数量因节点而异。 要在视图中添加或删除列，请右键单击现有列标题，然后选择其中一项。 将列标题拖动到想要的位置即可对其重新排序。  

![Configuration Manager 添加列](media/add-columns.png)  

在列上下文菜单的底部，可以按列进行排序或分组。 另外，也可通过选择列标题对列进行排序。  

![Configuration Manager 按列分组](media/column-group-by.png)  

## <a name="reclaim-lock-for-editing-objects"></a><a name="bkmk_sedo"></a> 回收锁定以编辑对象

<!--4786915-->

如果 Configuration Manager 控制台停止响应，你可能会被锁定而无法做出进一步更改，直到 30 分钟后锁定到期。 此锁定是 Configuration Manager SEDO（分布式对象的序列化编辑）系统的一部分。 有关详细信息，请参阅 [Configuration Manager SEDO](../../../develop/core/understand/sedo.md)。

从[当前分支版本 1906](../../plan-design/changes/whats-new-in-version-1906.md#reclaim-sedo-lock-for-task-sequences) 开始，可以清除对任务序列的锁定。 从版本 1910 开始，可以清除对 Configuration Manager 控制台中任何对象的锁定。

此操作仅适用于被锁定的用户帐户，并且仅可在站点授予锁定的同一设备上执行。 尝试访问已锁定的对象时，现在可以放弃更改，并继续编辑对象  。 锁定过期时这些更改将丢失。

## <a name="view-recently-connected-consoles"></a><a name="bkmk_viewconnected"></a>查看最近连接的控制台

<!--3699367-->
从版本 1902 开始，可以查看 Configuration Manager 控制台的最新连接。 视图包括活动连接和最近连接。 始终可在列表中看到当前控制台连接，并且只能看见来自 Configuration Manager 控制台的连接。 而看不到 PowerShell 或其他基于 SDK 的到 SMS 提供程序的连接。 该站点将从列表中删除 30 天以前的实例。

### <a name="prerequisites-to-view-connected-consoles"></a><a name="bkmk_connections-prereq"></a> 查看已连接控制台的先决条件

- 帐户需要 SMS_Site 对象的读取权限  

- 配置管理服务 REST API。 有关详细信息，请参阅[什么是管理服务？](../../../develop/adminservice/overview.md)

### <a name="view-connected-consoles"></a>查看已连接控制台

1. 在 Configuration Manager 控制台中，转到“管理”  工作区。  

2. 展开“安全”并选择“控制台连接”节点   。  

3. 查看具有以下属性的最近连接：  

    - 用户名
    - 计算机名
    - 已连接的站点代码
    - 控制台版本
    - 上次连接时间：用户上一次打开控制台的时间 
    - 自版本 1910 开始，“上次控制台检测信号”列已替换“上次连接时间”列   。 <!--4923997-->
       - 在前台打开的一个控制台每 10 分钟发送一次检测信号。

![查看 Configuration Manager 控制台连接](media/console-connections.png)

## <a name="start-microsoft-teams-chat-from-console-connections"></a><a name="bkmk_message"></a> 从控制台连接启动 Microsoft Teams 聊天
<!--4923997-->
（从版本 1910 中引入） 

从版本 1910 开始，你可以使用 Microsoft Teams 从“控制台连接”节点向其他 Configuration Manager 管理员发送消息  。 当你选择向管理员“启动 Microsoft Teams 聊天”时，将启动 Microsoft Teams 并打开与用户的聊天  。

### <a name="prerequisites"></a>必备条件

- 对于启动与管理员的聊天，需要使用 [Azure AD 或 AD 用户发现](../deploy/configure/about-discovery-methods.md#bkmk_aboutUser)来发现要聊天的帐户。
- 在运行控制台的设备上安装了 Microsoft Teams。
注意
- 所有[查看已连接控制台的先决条件](#bkmk_connections-prereq)

### <a name="start-microsoft-teams-chat"></a>启动 Microsoft Teams 聊天

1. 转到“管理”   > “安全”   > “控制台连接”  。
1. 右键单击用户的控制台连接，并选择“启动 Microsoft Teams 聊天”  。
    - 如果找不到所选管理员的用户主体名称，则“启动 Microsoft Teams 聊天”  显示为灰色。
    - 如果在运行控制台的设备上没有安装 Microsoft Teams，则会出现一条错误消息，包括一个下载链接。
    - 如果在运行控制台的设备上安装了 Microsoft Teams，它将打开与用户的聊天。

### <a name="known-issues"></a>已知问题

如果下列注册表项不存在，则不会显示通知 Microsoft Teams 未安装的错误消息：

Computer\HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall

若要解决此问题，请手动创建注册表项。

## <a name="in-console-documentation-dashboard"></a><a name="bkmk_doc-dashboard"></a> 控制台中的文档仪表板

<!--3556019 FKA 1357546-->
从 Configuration Manager 版本 1902 起，新“社区”工作区包含“文档”节点。   此节点包含有关 Configuration Manager 文档和支持文章的最新信息。 它包括以下部分：  

### <a name="product-documentation-library"></a>产品文档库

-  推荐：重要文章的手动特选列表。
-  趋势：上个月的最热门文章。
-  最近更新：上个月修订的文章。

### <a name="support-articles"></a>支持文章

-  疑难解答文章：用来帮助排查 Configuration Manager 组件和功能问题的演练指南。
-  新的和更新的支持文章：过去两个月新的或更新的支持文章。

### <a name="troubleshooting-connection-errors"></a>排查连接错误
Documentation  节点没有显式代理配置。 它使用“Internet 选项”  控制面板小程序中的任意操作系统定义的代理。 若要在连接错误后重试，请刷新 Documentation  节点。


## <a name="command-line-options"></a>命令行选项

Configuration Manager 控制台提供下列命令行选项：

|选项|说明|  
|------------|-----------------|  
|`/sms:debugview=1`|DebugView 包含在用于指定视图的所有 ResultView 中。 DebugView 显示原始属性（名称和值）。|  
|`/sms:NamespaceView=1`|在控制台中显示命名空间视图。|  
|`/sms:ResetSettings`|控制台忽略用户保留的连接和视图状态。 窗口大小未重置。|  
|`/sms:IgnoreExtensions`|禁用任何 Configuration Manager 扩展。|  
|`/sms:NoRestore`|控制台忽略之前保留的节点导航。|  


## <a name="next-steps"></a>后续步骤

- [控制台通知](admin-console-notifications.md)
- [控制台提示](admin-console-tips.md)
- [辅助功能](../../understand/accessibility-features.md)
- [任务序列编辑器](../../../osd/understand/task-sequence-editor.md#bkmk_conditions)
