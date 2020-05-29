---
title: 共同管理的路径
titleSuffix: Configuration Manager
description: 了解设置共同管理的两种主要方法的先决条件。
ms.date: 06/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 5beb5564-2fdf-4f0a-8801-d0cec8214c43
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 27994107c32fac87a465240f07b68d57fddfc140
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/27/2020
ms.locfileid: "83983824"
---
# <a name="paths-to-co-management"></a>共同管理的路径

可以使用两种主要方法来设置共同管理。 请务必了解每种方法的先决条件。 这两种方法都需要结合使用 Azure Active Directory (Azure AD)、Configuration Manager、Microsoft Intune 和 Windows 10。 

1. [将现有 Configuration Manager 管理的设备自动注册到 Intune](#bkmk_path1)  
2. [使用新式配置启动 Configuration Manager 客户端](#bkmk_path2)  

![共同管理方法的关系图](media/co-management-paths.png)



## <a name="path-1-auto-enroll-existing-clients"></a><a name="bkmk_path1"></a>方法 1：自动注册现有客户端

采用此方法可将现有的 Configuration Manager 管理的设备快速注册到 Intune。 在 Configuration Manager 中管理这些设备的方式与启用共同管理之前没有差别。 现在，可以获得所有基于云的优势。 此方法对用户而言是透明的。

以下是需要设置的选项：
- 混合 Azure AD
    - 以下 [Azure AD 混合标识选项](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin)之一：  
       - 含[无缝单一登录 (SSO)](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso) 的[密码哈希同步](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin#password-hash-synchronization)
       - 含[无缝单一登录 (SSO)](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso) 的[直通身份验证](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-pta)
       - [联合 SSO（含 Active Directory 联合身份验证服务 (AD FS)）](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin#federation-that-uses-a-new-or-existing-farm-with-ad-fs-in-windows-server-2012-r2)
    - Azure AD Connect
    - Azure AD Premium 许可证
    - 配置混合 Azure AD 联接（选择一个选项）：
        - 针对托管域
        - 针对联盟域
- 混合 Azure AD 联接的客户端代理设置
- 配置设备自动注册到 Intune
- 在 Configuration Manager 中启用共同管理

有关此方法的教程，请参阅[教程：为现有 Configuration Manager 客户端启用共同管理](tutorial-co-manage-clients.md)。



## <a name="path-2-bootstrap-with-modern-provisioning"></a><a name="bkmk_path2"></a> 方法 2：使用新式预配启动

以下是需要设置的选项：

1. [设置增强型 HTTP](../core/plan-design/hierarchy/enhanced-http.md)  
2. [在 Azure 中创建云服务](../core/servers/deploy/configure/azure-services-wizard.md)  
3. [配置管理点和客户端以使用云管理网关](../core/clients/manage/cmg/setup-cloud-management-gateway.md)  
4. [使用 Intune 部署 Configuration Manager 客户端](how-to-prepare-Win10.md)  

> [!Note]  
> 此方法的教程即将推出。

