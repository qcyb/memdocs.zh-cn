---
title: 使用 Exchange 管理设备
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中通过 Exchange Server 连接器管理移动设备。
ms.date: 12/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: aba688d9-fd5b-4c42-8cb4-f7e1b161ef50
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 08d92d5c09331d675dc679a374e1bbf81633748e
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724801"
---
# <a name="device-management-with-exchange-and-configuration-manager"></a>具有 Exchange 和 Configuration Manager 的设备管理

适用范围：  Configuration Manager (Current Branch)

如果你有通过 ActiveSync 协议连接到 Exchange Server 的移动设备，则可以使用 Configuration Manager 中的 Exchange Server 连接器来管理这些设备。 连接器适用于本地 Exchange Server 或 Exchange Online。 使用 Configuration Manager 控制台来配置 Exchange 移动设备管理功能。 例如，远程设备擦除和针对多个 Exchange 服务器的设置控制。

![Exchange Server 连接器与 Configuration Manager 的逻辑关系图](media/configmgr-with-exchange.png)  

当你通过此连接器管理移动设备时，它不会安装 Configuration Manager 客户端或通过 MDM 注册设备。 与这些其他选项相比，Exchange Server 的管理功能受到限制。 例如，你无法安装软件或使用配置项目来配置这些设备。 有关详细信息，请参阅[选择 Configuration Manager 的设备管理解决方案](../../core/plan-design/choose-a-device-management-solution.md)。  

## <a name="policies"></a>策略

使用连接器时，Configuration Manager 会在移动设备上配置设置。 设备不使用默认的 Exchange ActiveSync 邮箱策略。 定义要在以下组中使用的设置：

- **常规**
- **密码**
- **电子邮件管理**
- **安全性**
- **应用程序**

例如，在 "**密码**" 组中，可以配置以下设置：

- 移动设备是否需要密码
- 最短密码长度
- 密码复杂性
- 是否允许密码恢复

配置该组中的至少一个设置时，Configuration Manager 将为移动设备管理该组中的所有设置。 如果未在组中配置任何设置，则 Exchange 将继续管理这些移动设备的设置。 仍会应用在 Exchange Server 上配置并分配给用户的任何 Exchange ActiveSync 邮箱策略。

## <a name="access-rules-and-remote-actions"></a>访问规则和远程操作

你还可以配置 Exchange Server 连接器来管理 Exchange 访问规则。 这些访问规则包括 "允许"、"阻止" 或 "隔离移动设备"。 你可以使用 Configuration Manager 控制台远程擦除移动设备，并且用户可以使用应用程序目录以远程方式擦除其移动设备。

当你管理用户的移动设备并且 Exchange Server 位于本地时，该移动设备将自动出现在应用程序目录中。 若要让移动设备在使用 Exchange Online 时显示在应用程序目录中，请手动配置用户设备相关性。 有关详细信息，请参阅将[用户和设备与用户设备相关性相链接](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)。

> [!TIP]  
> 将移动设备转移到另一个用户时，在新所有者在设备上配置其 Exchange 帐户之前，请从 Configuration Manager 控制台中删除该移动设备。

## <a name="prerequisites"></a>先决条件

> [!IMPORTANT]  
> 安装此连接器之前，请确认 Configuration Manager 支持你的 Exchange 版本。 有关详细信息，请参阅[支持的配置-Exchange Server 连接器](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_ExSrvConOS)。  

### <a name="permissions-to-configure-the-connector"></a>用于配置连接器的权限

在 Configuration Manager 中，需要以下安全权限才能配置 Exchange Server 连接器：

- 若要添加、修改和删除注册 Exchange Server 连接器：“站点” **** 对象的“修改” **** 权限。  

- 若要要配置移动设备设置：“站点” **** 对象的“ModifyConnectorPolicy” **** 权限。  

例如，**完全权限管理员**的内置角色包括这些必需的权限。  

### <a name="permissions-to-manage-mobile-devices"></a>管理移动设备的权限

需要以下安全权限才能管理移动设备：  

- 若要擦除移动设备：“集合” **** 对象的“删除资源” **** 权限。  

- 若要取消擦除命令：“集合” **** 对象的“修改资源” **** 权限。  

- 允许和阻止移动设备：“集合” **** 对象的 **修改资源** 权限。  

例如，**操作管理员**内置角色包括这些必需的权限。

有关详细信息，请参阅[配置基于角色的管理](../../core/servers/deploy/configure/configure-role-based-administration.md)。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [安装和配置 Exchange connector](install-configure-exchange-connector.md)
