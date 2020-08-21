---
title: 设置桌面分析
titleSuffix: Configuration Manager
description: 关于设置和载入桌面分析的操作指南。
ms.date: 02/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 7ff8d453-f24d-4230-a116-585190a663fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: facfb2be1972933524c7ad632537fc8306939c1c
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700746"
---
# <a name="how-to-set-up-desktop-analytics"></a>如何设置桌面分析

使用此过程登录桌面分析并在订阅中对其进行配置。 此过程是为组织设置桌面分析的一次性过程。  

> [!Important]  
> 有关 Configuration Manager 的桌面分析一般先决条件的信息，请参阅[先决条件](overview.md#prerequisites)。  

## <a name="initial-onboarding"></a>初始载入

1. 以具有“全局管理员”角色的用户身份  ，在 Microsoft 365 设备管理中打开[桌面分析门户](https://aka.ms/desktopanalytics)。 选择“启动”  。 或者，在 Configuration Manager 控制台中，转到“软件库”工作区，选择“桌面分析服务”节点，然后选择“计划部署”    。

2. 在“接受服务协议”  页上，查看服务协议，然后选择“接受”  。  

3. 在“确认订阅”  页上，查看所需的合格许可证的列表。 将“你拥有受支持的或更高版本的订阅吗?”旁的设置切换到“是”，然后选择“下一步”    。  

4. 在“授予用户访问权限”  页上：

    - **允许桌面分析代表你管理目录角色**：桌面分析自动向“工作区所有者”分配“桌面分析管理员”角色   。 如果这些组已是“全局管理员”  ，则不会发生任何更改。

        如果未选择此选项，桌面分析仍会将用户添加为安全组的成员。 “全局管理员”  需要为用户手动分配“桌面分析管理员”  角色。

        有关在 Azure Active Directory 中分配管理员角色权限以及分配给“桌面分析管理员”的权限的详细信息  ，请参阅 [Azure Active Directory 中的管理员角色权限](/azure/active-directory/users-groups-roles/directory-assign-admin-roles)。  

    - 桌面分析在 Azure Active Directory 中预先配置“工作区所有者”  安全组，以创建和管理工作区和部署计划。

        若要将用户添加到组，请在“输入用户名或电子邮件地址”  部分键入其名称或电子邮件地址。 完成后，选择“下一步”  。

5. 在“设置工作区”页面上  ：  

    > [!NOTE]  
    > 若要完成此步骤，用户需要“工作区所有者”权限以及对 Azure 订阅和资源组的其他访问权限  。 有关详细信息，请参阅[先决条件](overview.md#prerequisites)。  

    - 若要将现有工作区用于桌面分析，请选中它，然后继续下一步。  

        > [!TIP]  
        > 每个 Azure AD 租户只能有一个桌面分析工作区。 设备只能向一个工作区发送诊断数据。  

    - 若要创建桌面分析工作区，请选择“添加工作区”  。  

        1. 输入全局唯一“工作区名称”  。

        2. 选择下拉列表以“选择此工作区的 Azure 订阅名称”  ，然后选择此工作区的 Azure 订阅。  

        3. “新建资源组”或“使用现有”   。

        4. 从列表中选择“区域”  ，然后选择“添加”  。  

6. 选择新的或现有工作区，然后选择“设置为桌面分析工作区”  。  然后，在“确认并授予访问权限”对话框中选择“继续”   。  

7. 在新浏览器选项卡中，选取一个用于登录的帐户。 选择“代表组织同意”  ，然后选择“接受”  。  

    > [!Note]  
    > 此同意是为 MALogAnalyticsReader 应用程序分配工作区的 Log Analytics 阅读者角色。 桌面分析需要此应用程序角色。 有关详细信息，请参阅 [MALogAnalyticsReader 应用程序角色](troubleshooting.md#bkmk_MALogAnalyticsReader)。  

8. 返回到“设置工作区”页面，选择“下一步”   。  

9. 在“最后几步”  页上，选择“转到桌面分析”  。

Azure 门户显示桌面分析主页  。

## <a name="next-steps"></a>后续步骤

转到下一篇文章，了解如何将 Configuration Manager 与桌面分析连接。
> [!div class="nextstepaction"]  
> [连接 Configuration Manager](connect-configmgr.md)