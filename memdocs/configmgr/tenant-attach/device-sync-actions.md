---
title: Microsoft Endpoint Manager 租户附加
titleSuffix: Configuration Manager
description: 将 Configuration Manager 设备上传到云服务，并从管理中心执行操作。
ms.date: 04/10/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 7a597d9e-a878-48d0-a7ce-56a1dbfd0e5c
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: be1c938cfcf332edb37e24e4094567f88f363560
ms.sourcegitcommit: c333fc6627f5577cde9d2fa8f59e642202a7027b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/16/2020
ms.locfileid: "84795612"
---
# <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions"></a><a name="bkmk_attach"></a>Microsoft 终结点管理器租户附加：设备同步和设备操作
<!--3555758 live 3/4/2020-->
适用范围：Configuration Manager (Current Branch)

Microsoft Endpoint Manager 是用于管理所有设备的集成解决方案。 Microsoft 将 Configuration Manager 和 Intune 组合为单个控制台，称为“Microsoft Endpoint Manager 管理中心”。

从 Configuration Manager 版本2002开始，你可以将 Configuration Manager 设备上传到云服务，并从管理中心的 "**设备**" 边栏选项卡中执行操作。

## <a name="prerequisites"></a>先决条件

- 在应用此更改时作为*全局管理员*登录的帐户。 有关详细信息，请参阅[Azure Active Directory （Azure AD）管理员角色](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles#azure-ad-administrator-roles)。
   - 载入在 Azure AD 租户中创建第三方应用和第一方服务主体。
- Azure 公有云环境。
- 触发设备操作的用户帐户具有以下先决条件：
   - 已发现[Azure Active Directory 用户发现](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc)和[Active Directory 用户发现](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)。
      - 这意味着用户帐户需要是 Azure AD 中的已同步用户对象。
   - Microsoft 终结点管理器管理中心中的 "**远程任务**" 下的 "**启动 Configuration Manager 操作**" 权限。


## <a name="internet-endpoints"></a>Internet 终结点

- `https://aka.ms/configmgrgateway`
- `https://*.manage.microsoft.com` <!--7424742-->

## <a name="enable-device-upload"></a>启用设备上传

- 如果当前已启用共同管理，请[编辑共同管理属性](#bkmk_edit)以启用设备上传。
- 如果尚未启用共同管理，请[使用 "**配置共同管理**" 向导](#bkmk_config)来启用设备上传。
   - 你可以上传设备，而无需为共同管理启用自动注册或将工作负荷切换到 Intune。
- "**客户端**" 列中包含 **"是"** 的 Configuration Manager 管理的所有设备都将上传。 如果需要，可以将上传限制为单个设备集合。

### <a name="edit-co-management-properties-to-enable-device-upload"></a><a name="bkmk_edit"></a>编辑共同管理属性以启用设备上传

如果当前已启用共同管理，请编辑共同管理属性，以使用以下说明启用设备上传：

1. 在 Configuration Manager 管理控制台中，转到“管理” > “概述” > “云服务” > “共同管理”   。
1. 右键单击共同管理设置，然后选择“属性”。
1. 在“配置上传”选项卡中，选择“上传到 Microsoft Endpoint Manager 管理中心” 。 单击“应用” 。
   - 设备上传的默认设置是“我所有由 Microsoft Endpoint Configuration Manager 管理的设备”。 如果需要，可以将上传限制为单个设备集合。

   [![共同管理配置向导](./media/3555758-configure-upload.png)](./media/3555758-configure-upload.png#lightbox)
1. 出现提示时，请使用全局管理员帐户登录。
1. 单击“是”接受“创建 AAD 应用程序”通知 。 此操作可预配一个服务主体，并创建 Azure AD 应用程序注册以促进同步。
1. 完成更改后，单击“确定”退出共同管理属性。


### <a name="use-the-configure-co-management-wizard-to-enable-device-upload"></a><a name="bkmk_config"></a>使用 "配置共同管理" 向导来启用设备上传
如果尚未启用共同管理，请使用 "**配置共同管理**" 向导来启用设备上传。 你可以上传设备，而无需为共同管理启用自动注册或将工作负荷切换到 Intune。 使用以下说明启用设备上传：

1. 在 Configuration Manager 管理控制台中，转到“管理” > “概述” > “云服务” > “共同管理”   。
1. 在功能区中，单击“配置共同管理”打开向导。
1. 在“租户加入”页面上，为环境选择“AzurePublicCloud” 。 不支持 Azure 政府云。
1. 单击“登录”。 使用全局管理员帐户登录。
1. 请确保在 "**租户加入**" 页上选择了 "**上传到 Microsoft 终结点管理器管理中心**" 选项。
   - 如果你不想立即启用共同管理，请确保 "**为共同管理启用自动客户端注册**" 选项未选中。 如果确实要启用共同管理，请选择选项。
   - 如果启用共同管理和设备上传，则会在向导中提供附加页面以完成。 有关详细信息，请参阅[启用共同管理](../comanage/how-to-enable.md)。

   [![共同管理配置向导](./media/3555758-comanagement-wizard.png)](./media/3555758-comanagement-wizard.png#lightbox)
1. 单击“下一步”，然后单击“是”接受“创建 AAD 应用程序”通知  。 此操作可预配一个服务主体，并创建 Azure AD 应用程序注册以促进同步。
1. 在 "**配置上传**" 页上，为**Microsoft 终结点管理的所有设备**选择建议的设备上传设置 Configuration Manager。 如果需要，可以将上传限制为单个设备集合。
1. 单击“摘要”查看所选内容，然后单击“下一步” 。
1. 完成向导后，单击“关闭”。  


## <a name="review-your-upload"></a><a name="bkmk_review"></a>查看上传

1. 从**CMGatewaySyncUploadWorker.log** &lt; ConfigMgr 安装目录中打开 CMGatewaySyncUploadWorker> \logs
1. 下一次同步时间由类似于的日志条目记录 `Next run time will be at approximately: 02/28/2020 16:35:31` 。
1. 对于设备上传，查找类似于的日志条目 `Batching N records` 。 **N**是上传到云的设备数。 
1. 每隔15分钟就会发生更改。 上传更改后，可能需要额外5到10分钟的时间，客户端更改才会显示在**Microsoft 终结点管理器管理中心**。

## <a name="perform-device-actions"></a>执行设备操作

1. 在浏览器中，导航到`endpoint.microsoft.com`
1. 选择 "**设备**"，然后选择 "**所有设备**" 查看已上传的设备。 你将在 "已上传设备" 的 "**管理者**" 列中看到**ConfigMgr** 。
   [![Microsoft 终结点管理器管理中心中的所有设备](./media/3555758-all-devices.png)](./media/3555758-all-devices.png#lightbox)
1. 单击设备以加载其 "**概述**" 页。
1. 单击下列任一操作：
   - **同步计算机策略**
   - **同步用户策略**
   - **应用评估周期**

   [![Microsoft 终结点管理器管理中心中的设备概述](./media/3555758-device-overview-actions.png)](./media/3555758-device-overview-actions.png#lightbox)

## <a name="known-issues"></a>已知问题

### <a name="specific-devices-dont-synchronize"></a>特定设备不同步

<!--7099564-->
Configuration Manager 客户端的特定设备可能不会上载到服务中。

**受影响的设备：** 如果设备是为分发点功能及其客户端代理使用相同 PKI 证书的分发点，则该设备不会包含在租户附加设备同步中。

**行为：** 当在进行 "在使用时" 阶段执行租户附加时，将首次执行完全同步。 后续同步周期是增量同步。 对受影响设备的任何更新都将导致从同步中删除设备。

## <a name="log-files"></a>日志文件
使用位于服务连接点上的以下日志：

- **CMGatewaySyncUploadWorker**
- **CMGatewayNotificationWorker**

## <a name="next-steps"></a>后续步骤

有关租户附加日志文件的详细信息，请参阅[租户附加故障排除](technical-reference.md)。
