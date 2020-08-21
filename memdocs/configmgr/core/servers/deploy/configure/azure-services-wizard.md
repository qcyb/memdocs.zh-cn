---
title: 配置 Azure 服务
titleSuffix: Configuration Manager
description: 通过云管理、适用于企业的 Microsoft Store 以及 Log Analytics 等 Azure 服务连接 Configuration Manager 环境。
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
ms.assetid: a26a653e-17aa-43eb-ab36-0e36c7d29f49
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ebdd07874f09ff6d97747826d6056df177e2c735
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128471"
---
# <a name="configure-azure-services-for-use-with-configuration-manager"></a>配置用于 Configuration Manager 的 Azure 服务

适用范围：Configuration Manager (Current Branch)

使用“Azure 服务向导”简化用于 Configuration Manager 的 Azure 云服务的配置过程。 此向导通过使用 Azure Active Directory (Azure AD) Web 应用注册提供通用的配置体验。 这些应用提供订阅和配置详细信息，以及与 Azure AD 之间的身份验证通信。 每次使用 Azure 设置新的 Configuration Manager 组件或服务时，应用都会输入此相同的信息。

## <a name="available-services"></a>可用服务

使用此向导配置下列 Azure 服务：  

- **云管理**：此服务使用 Azure AD 支持站点和客户端进行身份验证。 此身份验证支持其他方案，例如：  

  - [安装并分配 Configuration Manager Windows 10 客户端（使用 Azure AD 进行身份验证）](../../../clients/deploy/deploy-clients-cmg-azure.md)  

  - [配置 Azure AD 用户发现](configure-discovery-methods.md#azureaadisc)  

  - [配置 Azure AD 用户组发现](configure-discovery-methods.md#bkmk_azuregroupdisco)

  - 支持某些[云管理网关方案](../../../clients/manage/cmg/plan-cloud-management-gateway.md#scenarios)  

  - [应用审批电子邮件通知](../../../../apps/deploy-use/app-approval.md#bkmk_email-approve)

- **Log Analytics 连接器**：[连接到 Azure 日志分析](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm)。 将集合数据同步到 Log Analytics。  

    > [!Note]  
    > 本文引用 Log Analytics 连接器（以前称为“OMS 连接器”）。 没有任何功能区别。 有关详细信息，请参阅 [Azure 管理 - 监视](https://docs.microsoft.com/azure/azure-monitor/terminology#log-analytics)。  

- **适用于企业的 Microsoft Store**：连接到[适用于企业的 Microsoft Store](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)。 为组织获取可使用 Configuration Manager 部署的 Microsoft Store 应用。  

### <a name="service-details"></a>服务详细信息

下表列出每个服务的详细信息。  

- **租户**：可以配置的服务实例数量。 每个实例必须为不同的 Azure AD 租户。  

- **云**：所有服务都支持全局 Azure 云，但是并非所有服务都支持私有云，例如 Azure 美国政府云。  

- **Web 应用**：指定服务是否使用“Web 应用/API”类型的 Azure AD 应用（在 Configuration Manager 中也被称为服务器应用）。  

- **本机应用**：指定服务是否使用“本机”类型的 Azure AD 应用（在 Configuration Manager 中也被称为客户端应用）。  

- **操作**：指定是否可以在 Configuration Manager Azure 服务向导中导入或创建这些应用。  

|服务  |租户  |云  |Web 应用  |本机应用  |操作  |
|---------|---------|---------|---------|---------|---------|
|云管理及<br>Azure AD 发现 | 多个 | 公共、私有 | ![支持](media/green_check.png) | ![支持](media/green_check.png) | 导入、创建 |
|Log Analytics 连接器 | 一个 | 公共、私有 | ![支持](media/green_check.png) | ![不支持](media/Red_X.png) | 导入 |
|适用于企业和教育的<br>Microsoft Store | 一个 | 公共 | ![支持](media/green_check.png) | ![不支持](media/Red_X.png) | 导入、创建 |

### <a name="about-azure-ad-apps"></a>关于 Azure AD 应用

不同的 Azure 服务需要在 Azue 门户进行不同的配置。 此外，针对 Azure 资源，每个服务的应用可能需要单独的权限。  

单个应用可用于多个服务。 在 Configuration Manager 和 Azure AD 中只需管理一个对象。 当应用的安全密钥到期时，只需刷新一个密钥。

在向导中创建其他 Azure 服务时，Configuration Manager 会重复使用服务之间通用的信息。 此行为让你无需多次输入同样的信息。

有关每个服务所需的应用权限及配置的详细信息，请查看相关 Configuration Manager 文章中的[可用服务](#available-services)部分。

有关 Azure 应用的详细信息，请从以下文章开始阅读：

- [Azure 应用服务中的身份验证和授权](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview)
- [Web 应用概述](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview)
- [在 Azure AD 中注册应用程序的基本知识](/azure/active-directory/develop/authentication-scenarios)  
- [用 Azure Active Directory 租户注册应用程序](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration)

## <a name="before-you-begin"></a>在开始之前

决定好要连接到的服务后，请参考[服务详细信息](#service-details)中的表。 此表为你提供完成 Azure 服务向导所需的信息。 请提前与你的 Azure AD 管理员进行讨论。 决定执行以下哪项操作：

- 在 Azure 门户中提前手动创建应用。 然后将应用详细信息导入 Configuration Manager。  

- 使用 Configuration Manager 直接在 Azure AD 中创建应用。 若要从 Azure AD 收集必要数据，请查看本文其他部分中的信息。  

部分服务需要 Azure AD 应用具备特定的权限。 查看每个服务的信息以确定任何所需权限。 例如，在导入某个 Web 应用之前，Azure 管理员必须先在 [Azure 门户](https://portal.azure.com)中创建该应用。

在 Log Analytics 连接器时，在包含相关工作区的资源组上授予新注册的 Web 应用“参与者”权限。 此权限允许 Configuration Manager 访问该工作区。 分配权限时，在 Azure 门户的“添加用户”区域中搜索应用注册的名称。 此过程与[向 Configuration Manager 提供 Log Analytics 权限](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#grant-configuration-manager-with-permissions-to-log-analytics)相同。 Azure 管理员必须在将应用导入 Configuration Manager 之前分配这些权限。

## <a name="start-the-azure-services-wizard"></a>开始使用 Azure 服务向导

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“Azure 服务”节点  。  

2. 在功能区的“主页”选项卡上的“Azure 服务”组中，选择“配置 Azure 服务”  。  

3. 在 Azure 服务向导的“Azure 服务”页上进行以下操作：  

    1. 指定 Configuration Manager 中的对象名称。  

    2. 指定可选说明以帮助标识服务。  

    3. 选择想要通过 Configuration Manager 连接到的 Azure 服务。  

4. 选择“下一步”继续转至 Azure 服务向导的 [Azure 应用属性](#azure-app-properties)页。  

## <a name="azure-app-properties"></a>Azure 应用属性

先从 Azure 服务向导的“应用”页上的列表中选择“Azure 环境” 。 根据[服务详细信息](#service-details)中的表，判定该服务当前可用的环境。

应用页的其余部分根据特定服务而定。 根据[服务详细信息](#service-details)中的表，判定服务使用哪种应用以及可以进行什么操作。

- 如果应用同时支持导入和创建操作，请选择“浏览”。 此操作会打开[服务器应用对话框](#server-app-dialog)或[客户端应用对话框](#client-app-dialog)。  

- 如果应用只支持导入操作，请选择“导入”。 此操作会打开[导入应用对话框（服务器）](#import-apps-dialog-server)或[导入应用对话框（客户端）](#import-apps-dialog-client)。

在此页面指定好应用后，选择“下一步”以继续转至 Azure 服务向导的[配置或发现](#configuration-or-discovery)页。

### <a name="web-app"></a>Web 应用

此应用为“Web 应用/API”类型的 Azure AD 应用（在 Configuration Manager 中也被称为服务器应用）。

#### <a name="server-app-dialog"></a>服务器应用对话框

在 Azure 服务向导的应用页上的“Web 应用”选择“浏览”时，会打开服务器应用对话框 。 对话框会显示一个列表，显示任何现有 Web 应用的以下属性：

- 租户友好名称
- 应用友好名称
- 服务类型

你可以从服务器应用对话框进行三种操作：

- 如要重复使用现有 Web 应用，请从列表中选择它。
- 选择“导入”以打开[“导入应用”对话框](#import-apps-dialog-server)。
- 选择“创建”以打开[“创建服务器应用程序”对话框](#create-server-application-dialog)。

选择、导入或创建 Web 应用后，选择“确定”以关闭“服务器应用”对话框。 此操作会返回至 Azure 服务向导的[应用页](#azure-app-properties)。

#### <a name="import-apps-dialog-server"></a>导入应用对话框（服务器）

从 Azue 服务向导的服务器应用对话框或应用页选择“导入”时，会打开“导入应用”对话框。 此页可以输入 Azure 门户中已创建的 Azure AD Web 应用的相关信息。 它会将 Web 应用的元数据导入至 Configuration Manager。 指定下列信息：

- **Azure AD 租户名称**：Azure AD 租户的名称。
- **Azure AD 租户 ID**：Azure AD 租户的 GUID。
- **应用程序名称**：应用的易记名称，应用注册中的显示名称。
- **客户端 ID**：应用注册的“应用程序(客户端) ID”值。 格式为标准 GUID。
- **密钥**：在 Azure AD 中注册应用时，必须复制该密钥。
- **密钥到期日期**：从日历选择一个未来的日期。
- **应用 ID URI**：此值在 Azure AD 租户中必须是唯一的。 它在 Configuration Manager 客户端用于请求访问服务的访问令牌中。 值是 Azure AD 门户中应用注册条目的“应用程序 ID URI”。 格式类似于 `https://ConfigMgrService`。

输入信息后，选择“验证”。 然后选择“确定”，关闭“导入应用”对话框。 此操作会返回 Azure 服务向导的[应用页](#azure-app-properties)或[服务器应用对话框](#server-app-dialog)。

> [!TIP]
> 在 Azure AD 中注册应用时，可能需要手动指定以下重定向 URI：`ms-appx-web://Microsoft.AAD.BrokerPlugin/<ClientID>`。 指定应用的客户端 ID GUID，例如：`ms-appx-web://Microsoft.AAD.BrokerPlugin/a26a653e-17aa-43eb-ab36-0e36c7d29f49`。<!-- SCCMDocs#1135 -->

#### <a name="create-server-application-dialog"></a>创建服务器应用程序对话框

在服务器应用对话框中选择“创建”时，会打开“创建服务器应用程序”对话框。 此页会自动在 Azure AD 中创建 Web 应用。 指定下列信息：

- **应用程序名称**：应用的友好名称。
- **主页 URL**：Configuration Manager 不使用此值，但是 Azure AD 需要它。 默认情况下，此值为 `https://ConfigMgrService`。  
- **应用 ID URI**：此值在 Azure AD 租户中必须是唯一的。 它在 Configuration Manager 客户端用于请求访问服务的访问令牌中。 默认情况下，此值为 `https://ConfigMgrService`。  
- **密钥有效期**：从下拉列表中选择“1 年”或“2 年” 。 默认值为一年。

选择“登录”以进行 Azure 管理用户的身份验证。 Configuration Manager 不保存这些凭据。 此角色不需要 Configuration Manager 中的权限，其帐户也不需要与运行 Azure 服务向导的帐户相同。 成功完成 Azure 身份验证后，该页面会显示 Azure AD 租户名称以供参考。

选择“确定”以在 Azure AD 中创建 Web 应用，并关闭“创建服务器应用程序”对话框。 此操作会返回至[服务器应用对话框](#server-app-dialog)。

> [!NOTE]
> 如果定义了 Azure AD 条件访问策略并应用于所有云应用 - 必须从此策略中排除创建的服务器应用程序。 有关如何排除特定应用的详细信息，请参阅 [Azure AD 条件访问文档](https://docs.microsoft.com/azure/active-directory/conditional-access/)。

### <a name="native-client-app"></a>本机客户端应用

此应用为“本机”类型的 Azure AD 应用（在 Configuration Manager 中中也被称为服客户端应用）。

#### <a name="client-app-dialog"></a>客户端应用对话框

在 Azure 服务向导的“应用”页上的“本机客户端应用”选择“浏览”时，会打开“客户端应用”对话框 。 对话框会显示一个列表，显示任何现有本机应用的以下属性：

- 租户友好名称
- 应用友好名称
- 服务类型

你可以从客户端应用对话框进行三种操作：

- 如要重复使用现有本机应用，请从列表中选择它。 
- 选择“导入”以打开[“导入应用”对话框](#import-apps-dialog-client)。
- 选择“创建”以打开[“创建客户端应用程序”对话框](#create-client-application-dialog)。

选择、导入或创建本机应用后，选择“确定”以关闭“客户端应用”对话框。 此操作会返回至 Azure 服务向导的[应用页](#azure-app-properties)。

#### <a name="import-apps-dialog-client"></a>导入应用对话框（客户端）

在“客户端应用”对话框中选择“导入”时，会打开“导入应用”对话框。 此页可以输入 Azure 门户中已创建的 Azure AD 本机应用的相关信息。 它会将本机应用的元数据导入至 Configuration Manager。 指定下列信息：

- **应用程序名称**：应用的友好名称。
- **客户端 ID**：应用注册的“应用程序(客户端) ID”值。 格式为标准 GUID。

输入信息后，选择“验证”。 然后选择“确定”，关闭“导入应用”对话框。 此操作会返回至[客户端应用对话框](#client-app-dialog)。

#### <a name="create-client-application-dialog"></a>创建客户端应用程序对话框

在“客户端应用”对话框中选择“创建”时，会打开“创建客户端应用程序”对话框。 此页会自动在 Azure AD 中创建本机应用。 指定下列信息：

- **应用程序名称**：应用的友好名称。
- **回复 URL**：Configuration Manager 不使用此值，但是 Azure AD 需要它。 默认情况下，此值为 `https://ConfigMgrService`。

选择“登录”以进行 Azure 管理用户的身份验证。 Configuration Manager 不保存这些凭据。 此角色不需要 Configuration Manager 中的权限，其帐户也不需要与运行 Azure 服务向导的帐户相同。 成功完成 Azure 身份验证后，该页面会显示 Azure AD 租户名称以供参考。

选择“确定”以在 Azure AD 中创建本机应用，并关闭“创建客户端应用程序”对话框。 此操作会返回至[客户端应用对话框](#client-app-dialog)。

## <a name="configuration-or-discovery"></a>配置或发现

在“应用”页指定 Web 应用和本机应用后，Azure 服务向导根据要连接的服务转到“配置”或“发现”页 。 此页的详细信息因不同的服务而异。 有关详细信息，请参阅以下文章之一：  

- “云管理”服务，“发现”页：[配置 Azure AD 用户发现](configure-discovery-methods.md#azureaadisc)  

- “Log Analytics 连接器”服务，“配置”页：[配置到 Log Analytics 的连接](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm)  

- “适用于企业的 Microsoft Store”服务，“配置”页：[配置适用于企业的 Microsoft Store 同步](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md#bkmk_config)  

最后，通过“摘要”页、“进度”页和“完成”页完成 Azure 服务向导。 已在 Configuration Manager 中完成一项 Azure 服务的配置。 重复执行此过程以配置其他 Azure 服务。

## <a name="renew-secret-key"></a><a name="bkmk_renew"></a> 续订密钥

需要在 Azure AD 应用密钥的有效期结束之前续订密钥。 如果你让密钥过期，那么 Configuration Manager 就无法使用 Azure AD 进行身份验证，进而导致已连接的 Azure 服务停止运行。

自版本 2006 起，Configuration Manager 控制台对以下情况显示通知：<!--6386392-->

- 一个或多个 Azure AD 应用密钥即将过期时
- 一个或多个 Azure AD 应用密钥已过期时

若要缓解这两种情况，请续订密钥。

若要详细了解如何与这些通知进行交互，请参阅 [Configuration Manager 控制台通知](../../manage/admin-console-notifications.md)。

### <a name="renew-key-for-created-app"></a>续订已创建应用的密钥

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“Azure Active Directory 租户”节点。

1. 在“详细信息”窗格中，选择应用的 Azure AD 租户。

1. 在功能区中，选择“续订密钥”。 输入应用所有者或 Azure AD 管理员的凭据。

### <a name="renew-key-for-imported-app"></a>续订已导入应用的密钥

如果已在 Configuration Manager 中导入 Azure 应用，则使用 Azure 门户进行续订。 请注意新的密钥和到期日期。 在“续订密钥”向导上添加此信息。  

> [!NOTE]
> 保存密钥，然后关闭 Azure 应用程序属性“密钥”页。 关闭该页后，此信息将被删除。

## <a name="view-the-configuration-of-an-azure-service"></a>查看 Azure 服务的配置

查看已配置进行使用的 Azure 服务的属性。 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“Azure 服务”  。 选择想要查看或编辑的服务，然后选择“属性”。

如果选择服务并选择功能区中的“删除”，则会删除 Configuration Manager 中的连接。 这不会从 Azure AD 删除该应用。 请 Azure 管理员删除不再需要的应用。 或运行 Azure 服务向导来导入应用。<!--483440-->

## <a name="cloud-management-data-flow"></a>云管理数据流

下图是一个概念性数据流，展示 Configuration Manager、Azure AD 与连接的云服务之间的交互。 此特定示例使用云管理服务，包括 Windows 10 客户端、服务器应用和客户端应用。 其他服务的流与之类似。

![Configuration Manager 与 Azure AD 和云管理的数据流关系图](media/aad-auth.png)

1. Configuration Manager 管理员在 Azure AD 中导入或创建客户端应用和服务器应用。  

2. Configuration Manager Azure AD 用户发现方法运行。 站点使用 Azure AD 服务器应用令牌以向 Microsoft Graph 查询用户对象。  

3. 站点存储关于用户对象的数据。 有关详细信息，请参阅 [Azure AD 用户发现](about-discovery-methods.md#azureaddisc)。  

4. Configuration Manager 客户端请求 Azure AD 用户令牌。 客户端使用 Azure AD 客户端应用的应用程序 ID 发出声明，且将服务器应用作为受众。 有关详细信息，请参阅 [Azure AD 安全令牌中的声明](/azure/active-directory/develop/authentication-scenarios#security-tokens)。  

5. 客户端通过向云管理网关和本地启用了 HTTPS 的管理点提供 Azure AD 令牌向站点进行身份验证。  

有关更多详细信息，请参阅 [Azure AD 身份验证工作流](../../../clients/manage/azure-ccmsetup.md)。
