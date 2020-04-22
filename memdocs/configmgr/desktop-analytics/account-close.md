---
title: 如何关闭帐户
titleSuffix: Configuration Manager
description: 如何从 Azure 帐户中删除桌面分析
ms.date: 10/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 6e7d2850-b0af-497e-bbc1-bfc2a7420a7a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e1d031588100f3930bf5bf25970f544b91017d77
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706605"
---
# <a name="how-to-close-your-account"></a>如何关闭帐户

如果你在环境中设置了桌面分析，但之后决定要删除它，请使用此过程来关闭帐户。

## <a name="prerequisites"></a>必备条件

只有“全局管理员”  才能在 Azure 门户中关闭或重新激活帐户。

## <a name="process-to-offboard"></a>退出过程

1. 以具有“全局管理员”  角色的用户身份在 Microsoft 365 设备管理中打开[“桌面分析门户”](https://aka.ms/desktopanalytics)。

1. 在“全局设置”  菜单中，选择“连接服务”  。 在“注册设备”部分，选择“退出”的选项  。

1. 如果决定继续，则帐户将关闭。

> [!Important]
> 只能在 90 天后，或者在不重新激活的情况下，继续本文剩余部分所述的操作。
>
> 如果你想不用等待 90 天就完全关闭帐户，请先[重置](account-reset.md)你的帐户。

## <a name="reactivate"></a>重新激活

在接下来的 90 天，你的组织中访问桌面分析门户的任何管理员都将看到你选择退出的通知。

全局管理员可以在 90 天内重新激活帐户。 若要为你的组织还原桌面分析，请选择“重新访问”选项  。

## <a name="delete-the-solution"></a>删除解决方案

> [!Warning]
> 只能在 90 天后，或者在不重新激活的情况下，继续本文剩余部分所述的操作。 如果删除并断开这些其他组件，请不要尝试重新激活。

1. 以具有“全局管理员”  角色的用户身份登录 [Azure 门户](https://portal.azure.com)。

1. 在“所有资源”中搜索桌面分析工作区的名称  。 此名称是在注册服务时创建的。

1. 删除类型为“解决方案”的 `Microsoft365Analytics(YourWorkspaceName)` 。

桌面分析数据会基于工作区的数据保留策略而过期。 你可以继续使用同一工作区中的任何其他解决方案。

> [!Important]  
> 如果将 Log Analytics 工作区与其他解决方案一起使用，请不要删除工作区。

## <a name="remove-user-and-app-access"></a>删除用户和应用访问权限

1. 以具有“全局管理员”  角色的用户身份登录 [Azure 门户](https://portal.azure.com)。 转到 Azure Active Directory  。

1. 在“角色和管理员”  中，搜索“桌面分析管理员”  角色。 删除其成员。

1. 在“组”  中，删除以下组的成员：

    - **M365 Analytics 客户端管理员（Log Analytics 所有者）**
    - **M365 Analytics 客户端管理员（Log Analytics 参与者）**

1. 在“企业应用程序”  中，删除或撤销以下应用的访问权限：

    - `MaLogAnalyticsReader`

    - ConfigMgr 应用。 若要查找此应用的名称，请转到 Configuration Manager 控制台。 在“管理”工作区中，展开“云服务”，然后选择“Azure 服务”节点    。 打开“桌面分析”  服务的属性，切换到“应用程序”  选项卡。“Web 应用”  是此 Azure 应用。

        > [!Important]  
        > 在 Azure AD 中对此应用进行更改之前，确保不会将其重新与 Configuration Manager 中的其他服务一起使用。

## <a name="disconnect-configuration-manager"></a>断开 Configuration Manager 的连接

1. 以具有“完全权限管理员”  角色的用户身份打开 Configuration Manager 控制台。

1. 转到“管理”工作区，展开“云服务”，然后选择“Azure 服务”节点    。

1. 删除桌面分析服务。

### <a name="delete-collections-for-the-pilot-and-production-deployments"></a>删除试点和生产部署的集合

1. 在 Configuration Manager 控制台中，在“资产和符合性”工作区中选择“设备集合”   。

1. 删除不再使用的所有集合。 默认情况下，集合位于“部署计划”  文件夹下。  

## <a name="reconfigure-clients"></a>重新配置客户端

### <a name="unenroll-devices"></a>取消注册设备

在已注册的设备上，从以下 Windows 注册表项中删除 CommercialID 值：

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

### <a name="windows-diagnostic-data-configuration"></a>Windows 诊断数据配置

如果不希望设备继续发送诊断数据：

- Windows 10：将诊断数据级别设置为“安全” 
- Windows 7 SP1 或 8.1：禁用“商业数据选择加入”项 

使用以下方法之一设置这些值：

- 组策略（在“计算机配置” > “管理模板” > “Windows 组件” > “数据集合和预览版本”中）     。
- 移动设备管理 (MDM)，例如 [Microsoft Intune](https://docs.microsoft.com/intune/device-restrictions-windows-10#reporting-and-telemetry)

有关详细信息，请参阅[配置组织中的 Windows 诊断数据](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)。

> [!NOTE]  
> 应用这些更改后，设备会立即停止发送诊断数据。 Microsoft 可能需要 24-48 小时才能停止为您的工作区处理见解。 Microsoft 会在 30 天内或更短时间内从其云服务中删除此数据。
