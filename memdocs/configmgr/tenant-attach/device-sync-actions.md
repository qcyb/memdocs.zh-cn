---
title: Microsoft Endpoint Manager 租户附加
titleSuffix: Configuration Manager
description: 将 Configuration Manager 设备上传到云服务，并从管理中心执行操作。
ms.date: 08/11/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 7a597d9e-a878-48d0-a7ce-56a1dbfd0e5c
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 4bdfbabf27906eb8a79ec8ba24f51c3e176dc028
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700399"
---
# <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions"></a><a name="bkmk_attach"></a> Microsoft 终结点管理器租户附加：设备同步和设备操作
<!--3555758 live 3/4/2020-->
适用范围：  Configuration Manager (Current Branch)

Microsoft Endpoint Manager 是用于管理所有设备的集成解决方案。 Microsoft 将 Configuration Manager 和 Intune 组合为单个控制台，称为“Microsoft Endpoint Manager 管理中心”。

从 Configuration Manager 版本2002开始，你可以将 Configuration Manager 设备上传到云服务，并从管理中心的 " **设备** " 边栏选项卡中执行操作。

## <a name="prerequisites"></a>先决条件

- 在应用此更改时作为 *全局管理员* 登录的帐户。 有关详细信息，请参阅 [Azure Active Directory (Azure AD) 管理员角色](/azure/role-based-access-control/rbac-and-directory-admin-roles#azure-ad-administrator-roles)。
   - 载入在 Azure AD 租户中创建第三方应用和第一方服务主体。
- Azure 公有云环境。
- 触发设备操作的用户帐户具有以下先决条件：
   - 已发现 [Azure Active Directory 用户发现](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc) 和 [Active Directory 用户发现](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)。
      - 这意味着用户帐户需要是 Azure AD 中的已同步用户对象。
   - Microsoft 终结点管理器管理中心中的 "**远程任务**" 下的 "**启动 Configuration Manager 操作**" 权限。
- 如果管理中心站点有 [远程提供程序](../core/plan-design/hierarchy/plan-for-the-sms-provider.md)，请按照 CMPivot 一文中的 ca 的说明进行 [远程访问](../core/servers/manage/cmpivot-changes.md#cas-has-a-remote-provider) 。 <!--7796824-->

## <a name="internet-endpoints"></a>Internet 终结点

[!INCLUDE [Internet endpoints for tenant attach](../core/plan-design/network/includes/internet-endpoints-tenant-attach.md)]

## <a name="enable-device-upload-when-co-management-is-already-enabled"></a><a name="bkmk_edit"></a> 启用共同管理时启用设备上传

如果当前已启用共同管理，则将使用共同管理属性来启用设备上传。 如果尚未启用共同管理，请 [使用 " **配置共同管理** " 向导](#bkmk_config) 来改为启用设备上传。

如果已启用共同管理，请使用以下说明编辑共同管理属性以启用设备上传：

1. 在 Configuration Manager 管理控制台中，转到“管理” > “概述” > “云服务” > “共同管理”   。
1. 在功能区中，选择共同管理生产策略的 " **属性** "。
1. 在“配置上传”选项卡中，选择“上传到 Microsoft Endpoint Manager 管理中心” 。 选择“应用”。
   - 设备上传的默认设置是“我所有由 Microsoft Endpoint Configuration Manager 管理的设备”。 如果需要，可以将上传限制为单个设备集合。
1. 如果你还想要深入了解[终结点分析](../../analytics/overview.md)中的最终用户体验，请选中 "为已**上传到 Microsoft 终结点管理器的设备启用终结点分析**" 选项。

   [![将设备上传到 Microsoft 终结点管理器管理中心](../../analytics/media/6051638-configure-upload-configmgr.png)](../../analytics/media/6051638-configure-upload-configmgr.png#lightbox)
1. 出现提示时，请使用全局管理员帐户登录。
1. 选择 **"是"** 以接受 **创建 AAD 应用程序** 通知。 此操作可预配一个服务主体，并创建 Azure AD 应用程序注册以促进同步。
1. 完成更改后，请选择 **"确定"** 退出共同管理的属性。


## <a name="enable-device-upload-when-co-management-isnt-enabled"></a><a name="bkmk_config"></a> 在未启用共同管理的情况启用设备上传

如果尚未启用共同管理，请使用 " **配置共同管理** " 向导来启用设备上传。 你可以上传设备，而无需为共同管理启用自动注册或将工作负荷切换到 Intune。 "**客户端**" 列中包含 **"是"** 的 Configuration Manager 管理的所有设备都将上传。 如果需要，可以将上传限制为单个设备集合。 如果已在你的环境中启用共同管理，则 [编辑共同管理属性](#bkmk_edit) 以启用设备上传。

如果未启用共同管理，请使用下面的说明来启用设备上传：

1. 在 Configuration Manager 管理控制台中，转到“管理” > “概述” > “云服务” > “共同管理”   。
1. 在功能区中，选择 " **配置共同管理** " 以打开向导。
1. 在“租户加入”页面上，为环境选择“AzurePublicCloud” 。 不支持 azure 政府云和 Azure 中国世纪互联。
1. 选择“登录”。 使用全局管理员帐户登录。
1. 请确保在 "**租户加入**" 页上选择了 "**上传到 Microsoft 终结点管理器管理中心**" 选项。
   - 如果你不想立即启用共同管理，请确保 " **为共同管理启用自动客户端注册** " 选项未选中。 如果确实要启用共同管理，请选择选项。
   - 如果启用共同管理和设备上传，则会在向导中提供附加页面以完成。 有关详细信息，请参阅[启用共同管理](../comanage/how-to-enable.md)。

   [![共同管理配置向导](./media/3555758-comanagement-wizard.png)](./media/3555758-comanagement-wizard.png#lightbox)
1. 选择 " **下一步** "，然后单击 **"是"** 以接受 **创建 AAD 应用程序** 通知。 此操作可预配一个服务主体，并创建 Azure AD 应用程序注册以促进同步。
     - 或者，你可以在从2006版) 开始的租户附加载入 (中导入以前创建的 Azure AD 应用程序。 有关详细信息，请参阅 [导入先前创建的 Azure AD 应用程序](#bkmk_aad_app) 部分。
1. 在 " **配置上传** " 页上，为 **Microsoft 终结点管理的所有设备**选择建议的设备上传设置 Configuration Manager。 如果需要，可以将上传限制为单个设备集合。
1. 如果你还想要深入了解[终结点分析](../../analytics/overview.md)中的最终用户体验，请选中 "为已**上传到 Microsoft 终结点管理器的设备启用终结点分析**" 选项
1. 选择 " **摘要** " 以查看你的选择，然后选择 " **下一步**"。
1. 向导完成后，选择 " **关闭**"。  

## <a name="perform-device-actions"></a>执行设备操作

1. 在浏览器中，导航到 `endpoint.microsoft.com`
1. 选择 " **设备** "，然后选择 " **所有设备** " 查看已上传的设备。 你将在 "已上传设备" 的 "**管理者**" 列中看到**ConfigMgr** 。
   [![Microsoft 终结点管理器管理中心中的所有设备](./media/3555758-all-devices.png)](./media/3555758-all-devices.png#lightbox)
1. 选择要加载其 " **概述** " 页的设备。
1. 选择以下任一操作：
   - **同步计算机策略**
   - **同步用户策略**
   - **应用评估周期**

   [![Microsoft 终结点管理器管理中心中的设备概述](./media/3555758-device-overview-actions.png)](./media/3555758-device-overview-actions.png#lightbox)

## <a name="import-a-previously-created-azure-ad-application-optional"></a><a name="bkmk_aad_app"></a> 导入以前创建的 Azure AD 应用程序 (可选) 
<!--6479246-->
* 2006版中引入的 () *

在 [新的载入](#bkmk_config)过程中，管理员可以在载入到租户时指定先前创建的应用程序。 不要在多个层次结构中共享或重复使用 Azure AD 应用程序。 如果有多个层次结构，请为每个层次结构创建单独的 Azure AD 应用程序。

从“共同管理配置向导”的“正在加入租户”页面中，选择“(可选)导入单独的 Web 应用，将 Configuration Manager 客户端数据同步到 Microsoft Endpoint Manager 管理中心”。   此选项将提示你指定 Azure AD 应用的以下信息：

- Azure AD 租户名称
- Azure AD 租户 ID
- 应用程序名称
- 客户端 ID
- 密钥
- 密钥到期日期
- 应用 ID URI

### <a name="azure-ad-application-permissions-and-configuration"></a>Azure AD 应用程序权限和配置

在载入到租户时使用以前创建的应用程序需要以下权限：

- Configuration Manager 微服务权限：
   - CmCollectionData。读取
   - CmCollectionData

- Microsoft Graph 权限：
   - Directory. Read. 所有 [应用程序权限](/graph/permissions-reference#application-permissions)
   - Directory. Read. 所有 [委派的目录权限](/graph/permissions-reference#directory-permissions)

- 确保为 Azure AD 应用程序选择 "为 **租户授予管理员许可** "。 有关详细信息，请参阅 [在应用注册中授予管理员许可](/azure/active-directory/manage-apps/grant-admin-consent)。

- 导入的应用程序需要配置如下：
   - 仅为 **此组织目录中的帐户**注册。 有关详细信息，请参阅 [更改可访问应用程序的人员](/azure/active-directory/develop/quickstart-modify-supported-accounts#to-change-who-can-access-your-application)。
   -  具有有效的应用程序 ID URI 和密钥



## <a name="next-steps"></a>后续步骤

- [将 Configuration Manager 设备注册到终结点分析](../../analytics/enroll-configmgr.md#bkmk_cm_enroll)
- 有关租户附加日志文件的信息，请参阅 [租户附加故障排除](troubleshoot.md)。