---
title: Configuration Manager 控制台通知
titleSuffix: Configuration Manager
description: 了解来自 Configuration Manager 控制台的通知。
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a0d709fa-c4f8-46e1-b432-582cc293be35
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 12ec788fdf19ec72e954f5a9f229a5a3f95a4610
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129498"
---
# <a name="configuration-manager-console-notifications"></a>Configuration Manager 控制台通知

适用范围：  Configuration Manager (Current Branch)

<!--3556016, fka 1318035-->
自 Configuration Manager 版本 1902 起，Configuration Manager 控制台通知你发生的特定事件。 可以为 Configuration Manager 站点配置一些事件通知。

- 不可配置的事件通知：
   - Configuration Manager 本身有可用的更新
   - 环境中发生生命周期和维护事件
- 可配置的事件通知：
   - [非关键站点运行状况更改](#bkmk_noncrit)
   - [来自 Microsoft 的消息](#bkmk_msft)（自版本 2006 起）

此通知位于功能区下方控制台窗口顶部的栏。 Configuration Manager 更新可用时，它将替换以前的体验。 这些控制台内通知仍显示关键信息，但不会干扰你在控制台中的工作。 不能消除重要通知。 控制台在标题栏的新通知区域中显示所有通知。

![控制台中的通知栏和标志](./media/1318035-notify-eval-version-expired.png)

## <a name="configure-a-site-to-show-non-critical-notifications"></a><a name="bkmk_noncrit"></a> 配置站点以显示非关键通知

可以从各个站点的属性中配置站点，以显示非重要通知。

1. 在“管理”工作区中，展开“站点配置”，然后选择“站点”节点    。
1. 选择想要为其配置非重要通知的站点。
1. 在功能区中，选择“属性”  。
1. 在“警报”选项卡上，选择“为非重要站点运行状况更改启用控制台通知”选项   。
   - 如果启用此设置，则所有控制台用户都会看到重要、警告和信息通知。 默认情况下将启用此设置。  
   - 如果禁用此设置，控制台用户只能看到重要通知。  

大多数控制台的通知都是按会话操作的。 控制台在用户启动查询时会对其进行评估。 要查看通知中的更改，请重启控制台。 如果用户关闭非重要通知，则在控制台重启时它会再次通知（如果仍然适用）。

以下通知每五分钟重新评估一次：

- 站点处于维护模式  
- 站点处于恢复模式  
- 站点处于升级模式  

通知遵循基于角色的管理的权限。 例如，如果用户没有权限查看 Configuration Manager 更新，则用户看不到这些通知。

某些通知具有相关操作。 例如，如果控制台版本与站点版本不匹配，请选择“安装新控制台版本”  。 此操作将启动控制台安装程序。

自版本 2006 起，如果你将 Azure 服务配置为云附加你的站点，则会看到包含[续订密钥](../deploy/configure/azure-services-wizard.md#bkmk_renew)操作的通知。<!--6386392--> 站点每小时评估一次以下警报的状态：

- 一个或多个 Azure AD 应用密钥即将过期时
- 一个或多个 Azure AD 应用密钥已过期时

以下通知最适用于技术预览分支：  

- 评估版本将在 30 天内到期（警告）：评估版本在 30 天内即将到期  
- 评估版已过期（重要）：已超过评估版本的到期日期  
- 控制台版本不匹配（重要）：控制台版本与站点版本不匹配  
- 有可用的站点更新（警告）：有一个新的更新包可用  

有关详细信息和疑难解答帮助，请参阅控制台计算机上的 SmsAdminUI.log 文件  。 默认情况下，此日志文件位于以下路径：`C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\AdminUILog\SmsAdminUI.log`。

## <a name="configure-a-site-to-receive-messages-from-microsoft"></a><a name="bkmk_msft"></a> 配置站点以接收来自 Microsoft 的消息
 <!--3953121-->

自版本 2006 起，可以选择在 Configuration Manager 控制台中接收来自 Microsoft 的通知。 这些通知可帮助你及时了解新功能或功能更新、对 Configuration Manager 和附加服务所做的更改，以及需要修正操作的问题。

### <a name="configure-notification-settings-for-microsoft-messages"></a>为通知设置配置 Microsoft 消息

1. 导航到“管理”   > “站点配置”   > “站点”  。
1. 右键单击站点并选择“属性”  。
1. 在“警报”  选项卡中，通过选择“从 Microsoft 接收消息”  来启用通知。 如果不希望接收以下任何通知，可以取消选择这些通知：  
   - 阻止/修复  ：会对你的组织造成影响的已知问题（可能需要你进行处理）。
   - 计划更改  ：针对 Configuration Manager 的更改（可能需要你采取措施）。
   - 随时获取最新信息  ：在推出新功能或功能更新时通知你。

     [ ![站点属性中“来自 Microsoft 的通知”选项](./media/3953121-microsoft-notifications.png)](./media/3953121-microsoft-notifications.png#lightbox)



## <a name="next-steps"></a>后续步骤

- [使用控制台](admin-console.md)
- [控制台提示](admin-console-tips.md)
- [辅助功能](../../understand/accessibility-features.md)
