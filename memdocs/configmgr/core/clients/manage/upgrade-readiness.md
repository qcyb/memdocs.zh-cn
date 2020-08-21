---
title: Upgrade Readiness
titleSuffix: Configuration Manager
description: 将升级就绪情况与 Configuration Manager 集成来访问 Windows 10 升级兼容性数据和目标设备以进行升级或修正。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 01/31/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 68407ab8-c205-44ed-9deb-ff5714451624
ms.openlocfilehash: 6d9bd7aabb36895160ba8aa740c28155105e196a
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88693397"
---
# <a name="integrate-upgrade-readiness-with-configuration-manager"></a>将升级就绪情况与 Configuration Manager 集成

适用范围：  Configuration Manager (Current Branch)

> [!Important]  
> Windows Analytics 服务自 2020 年 1 月 31 日起停用。 有关详细信息，请参阅 [KB 4521815：Windows Analytics 将于 2020 年 1 月 31 日停用](https://support.microsoft.com/help/4521815/windows-analytics-retirement)。
>
> Windows Analytics 演变为桌面分析。 有关详细信息，请参阅[什么是桌面分析](../../../desktop-analytics/overview.md)。

如果 Configuration Manager 站点连接到升级就绪情况，则需要将其删除并重新配置客户端。

## <a name="remove-upgrade-readiness-connection"></a><a name="bkmk_remove"></a> 删除升级就绪情况连接

1. 以具有“完全权限管理员”  角色的用户身份打开 Configuration Manager 控制台。

1. 转到“管理”工作区，展开“云服务”，然后选择“Azure 服务”节点    。

1. 删除 Windows Analytics 服务。

## <a name="reconfigure-clients"></a>重新配置客户端

### <a name="unenroll-devices"></a>取消注册设备

首先，在 Windows Analytics 组中查看站点的默认设置或任何自定义客户端设备设置  。 例如，禁用以下设置：使用 Configuration Manager 管理 Windows 遥测设置  。

> [!IMPORTANT]
> 如果计划使用桌面分析，它会在客户端上配置 Windows 诊断数据设置。 使用 Azure 服务连接向导配置用于桌面分析的这些设置。 有关详细信息，请参阅[如何将 Configuration Manager 与桌面分析连接](../../../desktop-analytics/connect-configmgr.md)。

在已注册的设备上，从以下 Windows 注册表项中删除 CommercialID 值：

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

### <a name="windows-diagnostic-data-configuration"></a>Windows 诊断数据配置

如果不希望设备继续发送诊断数据：

- Windows 10：将诊断数据级别设置为“安全” 
- Windows 7 SP1 或 8.1：禁用“商业数据选择加入”项 

使用以下方法之一设置这些值：

- 组策略（在“计算机配置” > “管理模板” > “Windows 组件” > “数据集合和预览版本”中）     。
- 移动设备管理 (MDM)，例如 [Microsoft Intune](/intune/device-restrictions-windows-10#reporting-and-telemetry)

有关详细信息，请参阅[配置组织中的 Windows 诊断数据](/windows/privacy/configure-windows-diagnostic-data-in-your-organization)。

> [!NOTE]  
> 应用这些更改后，设备会立即停止发送诊断数据。 Microsoft 可能需要 24-48 小时才能停止为您的工作区处理见解。 Microsoft 会在 30 天内或更短时间内从其云服务中删除此数据。

<!--
Upgrade Readiness is a part of [Windows Analytics](/windows/deployment/upgrade/manage-windows-upgrades-with-upgrade-readiness). It allows you to assess and analyze the readiness of devices in your environment for an upgrade to Windows 10. Integrate Upgrade Readiness with Configuration Manager to access client upgrade compatibility data in the Configuration Manager console. Then use this data to create collections, and target devices for upgrade or remediation.



## Configure clients

Upgrade Readiness relies on Windows Analytics data. In order for Upgrade Readiness to receive sufficient data, configure the following prerequisites:

- Configure all clients with a *commercial ID key*  

- Configure Windows 10 clients for Windows Analytics to report at least basic level data  

- For clients running Windows 7 or 8.1:  

    - Install the updates as described in [Get started with Upgrade Readiness](/windows/deployment/upgrade/upgrade-readiness-get-started)  

    - Enable Windows Analytics client settings  

Configure these settings using Configuration Manager client settings. For more information, see [Use Windows Analytics](monitor-windows-analytics.md).

> [!NOTE]  
> Deploying the correct prerequisite updates and configuring client settings should be sufficient in most environments. If you encounter issues with Upgrade Readiness not receiving data from devices in your environment, then some of these issues may be addressed by using the [Upgrade Readiness deployment script](/windows/deployment/upgrade/upgrade-readiness-deployment-script). 



## Connect Configuration Manager to Upgrade Readiness

Use the [Azure services wizard](../../servers/deploy/configure/azure-services-wizard.md) to simplify the process of configuring Azure services you use with Configuration Manager. To connect Configuration Manager with Upgrade Readiness, create an Azure Active Directory (Azure AD) app registration of type *Web app / API* in the [Azure portal](https://portal.azure.com). For more information about how to create an app registration, see [Register your application with your Azure AD tenant](/azure/active-directory/active-directory-app-registration). 

In the Azure portal, give following permissions to your newly registered web app:
- *Reader* permissions to the resource group that contains the Log Analytics workspace with your Upgrade Readiness data
- *Contributor* permissions to the Log Analytics workspace that hosts your Upgrade Readiness data

The Azure services wizard uses this app registration to allow Configuration Manager to communicate securely with Azure AD and connect your infrastructure to your Upgrade Readiness data.

> [!IMPORTANT]  
> Grant permissions to the app itself, not to an Azure AD user identity. It's the registered app that accesses the data on behalf of your Configuration Manager infrastructure. To grant the permissions, search for the name of the app registration in the **Add users** area when assigning the permission. 
> 
> This process is the same as when providing Configuration Manager with permissions to Log Analytics. These steps must be completed before the app registration is imported into Configuration Manager with the *Azure services wizard*.
> 
> For more information, see [Connect Configuration Manager to Log Analytics](/azure/log-analytics/log-analytics-sccm).


### Use the Azure Wizard to create the connection

Follow the instructions in [Configure Azure services](../../servers/deploy/configure/azure-services-wizard.md) to create a connection to Upgrade Readiness by importing the web app registration you created above. 

If the web app import was successful and the correct permissions are assigned in the Azure portal, the *Configuration* page pre-populates the following values:   
-  Azure subscriptions  
-  Azure resource group  
-  Windows Analytics workspace  

More than one resource group or workspace is available in the following circumstances: 
- If the registered Azure AD web app has *Contributor* permissions on more than one resource group   
- If the selected resource group has more than one Log Analytics workspace  



## View and use Upgrade Readiness information in Configuration Manager

After you've integrated Upgrade Readiness with Configuration Manager, you can view the analysis of your clients' upgrade readiness.

1. In the Configuration Manager console, go to the **Monitoring** workspace, and select the **Upgrade Readiness** node.  

2. Review the data. For example:  
    - The upgrade readiness state  
    - The percent of Windows devices that are reporting data  

3. Filter the dashboard to view data for devices in specific collections.  

4. View the devices in a particular readiness state, and then create a dynamic collection for those devices. Then use that collection to upgrade those devices, or take action to remediate devices that are in a blocked state.  

> [!Note]  
> The site synchronizes data with Upgrade Readiness once a week. To manually trigger synchronization:
> 1. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Azure Services** node.  
> 2. Select the Upgrade Readiness connection from the list.  
> 3. In the ribbon, select the option to synchronize.  



## Next steps

- [Upgrade Windows to the latest version](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md)  
- [Create a task sequence to upgrade an OS](../../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md)  
- [Create phased deployments](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)