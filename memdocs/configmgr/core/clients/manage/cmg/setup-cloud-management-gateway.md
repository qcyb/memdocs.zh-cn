---
title: 设置云管理网关
titleSuffix: Configuration Manager
description: 使用此分步过程来设置云管理网关 (CMG)。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/26/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: e0ec7d66-1502-4b31-85bb-94996b1bc66f
ms.openlocfilehash: 36d256e674a0fe973eca4bc692a244af034d5cc1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "82076758"
---
# <a name="set-up-cloud-management-gateway-for-configuration-manager"></a>为 Configuration Manager 设置云管理网关

适用范围：  Configuration Manager (Current Branch)

此过程包括设置云管理网关 (CMG) 所需执行的步骤。

> [!Note]  
> 默认情况下，Configuration Manager 不启用此项可选功能。 必须在使用前启用此功能。 有关详细信息，请参阅[启用更新中的可选功能](../../../servers/manage/install-in-console-updates.md#bkmk_options)。


## <a name="before-you-begin"></a>在开始之前

先阅读[规划云管理网关](plan-cloud-management-gateway.md)一文。 使用该文章确定你的 CMG 设计。

使用以下清单确保具有创建 CMG 所需的信息和先决条件：  

- 要使用的 Azure 环境。 例如，Azure 公有云或 Azure 美国政府云。  

- 需要一个或多个 CMG 证书，具体取决于你的设计。 有关详细信息，请参阅[云管理网关的证书](certificates-for-cloud-management-gateway.md)。  

- 对于 CMG 的 [Azure 资源管理器](plan-cloud-management-gateway.md#azure-resource-manager)部署，需要满足以下要求：  

    - 与 [Azure AD](../../../servers/deploy/configure/azure-services-wizard.md) 集成以实现**云管理**。 不需要 Azure AD 用户发现。  

    - 必须在 Azure 订阅中注册 Microsoft.ClassicCompute & Microsoft.Storage 资源提供程序   。 有关详细信息，请参阅 [Azure 资源管理器](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-supported-services)。

    - 订阅管理员需要进行登录。  

- 服务的全局唯一名称。 此名称来自 [CMG 服务器身份验证证书](certificates-for-cloud-management-gateway.md#bkmk_serverauth)。  

- 如果启用 CMG 作为云分发点，则所选的同一个全局唯一 CMG 服务名称还需要可用作全局唯一存储帐户名称。 此名称来自 [CMG 服务器身份验证证书](certificates-for-cloud-management-gateway.md#bkmk_serverauth)。

- 此 CMG 部署所在的 Azure 区域。  

- 实现扩展和冗余所需的 VM 实例数。  

- 如果仍需要在 Configuration Manager 1810 版本或更早版本中使用 Azure 经典服务部署，则需要满足以下要求：  

    > [!Important]  
    > 从版本 1810 开始，Configuration Manager 已弃用 Azure 的经典服务部署。 将 Azure 资源管理器部署用于云管理网关。 有关详细信息，请参阅 [CMG 规划](plan-cloud-management-gateway.md#azure-resource-manager)。  
    >
    > 从 Configuration Manager 版本 1902 起，Azure 资源管理器是云管理网关的新实例的唯一部署机制。<!-- 3605704 -->

    - Azure 订阅 ID  

    - Azure 管理证书  


## <a name="set-up-a-cmg"></a>设置 CMG

在顶层站点上执行此过程。 该站点要么是独立的主站点，要么是管理中心站点。

1. 在 Configuration Manager 控制台中，转到“管理”  工作区，展开“云服务”  ，然后选择“云管理网关”  。  

2. 选择功能区中的“创建云管理网关”  。  

3. 在向导的“常规”页上，选择“登录”  。 使用 Azure 订阅管理员帐户进行身份验证。 向导使用 Azure AD 集成先决条件过程中存储的 信息，自动填充其余字段。 如果拥有多个订阅，请选择要使用的所需订阅的**订阅 ID**。

    > [!Note]  
    > 从版本 1810 开始，Configuration Manager 已弃用 Azure 的经典服务部署。 在版本 1902 和更早版本中，选择 Azure 资源管理器部署作为 CMG 部署方法  。
    >
    > 如果需要使用经典服务部署，请在此页面上选择该选项。 首先输入 Azure 订阅 ID  。 然后选择“浏览”并选择 Azure 管理证书的 .PFX 文件  。

4. 为此 CMG 指定 **Azure 环境**。 下拉列表中的选项可能会因部署方法而异。  

5. 选择“下一步”  。 等待站点测试与 Azure 的连接。  

6. 在向导的“设置”页上，先选择“浏览”，然后选择 CMG 服务器身份验证证书的 .PFX 文件  。 来自此证书的名称将填充“服务 FQDN”  和“服务名称”  必填字段。  

   > [!NOTE]  
   > CMG 服务器身份验证证书支持通配符。 如果使用通配符证书，请将“服务 FQDN”  字段中的星号 (`*`) 替换为 CMG 所需的主机名。<!--491233-->  

7. 选择“区域”下拉列表，选择此 CMG 所在的 Azure 区域  。  

8. 选择“资源组”  选项。
   1. 如果选择“使用现有项”  ，则从下拉列表中选择现有的资源组。 所选的资源组必须已位于步骤 7 中所选的区域。 如果选择的现有资源组不在之前所选区域中，则 CMG 将预配失败。
   2. 如果选择“新建”  ，则输入新的资源组名称。

9. 在“VM 实例”  字段中，输入此服务的 VM 数量。 默认值为 1，但每个 CMG 最多可扩展到 16 个 VM。  

10. 选择“证书”以添加受信任的客户端根证书  。 添加信任链中的所有证书。  

    > [!Note]  
    > 从 1806 版开始，创建 CMG 时，不再需要在设置页上提供受信任的根证书。 使用 Azure Active Directory (Azure AD) 进行客户端身份验证时不需要此证书，但往往在向导中需要。 如果使用 PKI 客户端身份验证证书，则仍须向 CMG 添加受信任的根证书。<!--SCCMDocs-pr issue #2872-->  
    >
    > 在版本 1902 和更早版本中，只能添加两个受信任的根 CA 和四个中间（从属）CA。<!-- SCCMDocs-pr#4022 -->

11. 默认情况下，向导会启用“验证客户端证书吊销”  选项。 必须公开发布证书吊销列表 (CRL) 才能使此验证生效。 有关详细信息，请参阅[发布证书吊销列表](security-and-privacy-for-cloud-management-gateway.md#bkmk_crl)。  

12. 从版本 1906 开始，可以强制执行 TLS 1.2。  此设置仅适用于 Azure 云服务 VM。 它不适用于任何本地 Configuration Manager 站点服务器或客户端。 有关 TLS 1.2 的详细信息，请参阅[如何启用 TLS 1.2](../../../plan-design/security/enable-tls-1-2.md)。<!-- SCCMDocs-pr#4021 -->

13. 默认情况下，从版本 1806 开始，向导会启用以下选项：允许 CMG 充当云分发点，并提供 Azure 存储中的内容  。 CMG 现还可向客户提供内容。 此功能减少了所需的证书和 Azure VM 的成本。  

14. 选择“下一步”  。  

15. 若要通过 14 天阈值监视 CMG 通信，请选中相应复选框以打开阈值警报。 然后，指定阈值，以及引发不同警报级别所依据的百分比。 完成后选择“下一步”  。  

16. 检查设置，然后选择“下一步”  。 Configuration Manager 开始设置服务。 关闭向导后，需花 5 到 15 分钟在 Azure 中完整预配该服务。 检查新 CMG 的“状态”  列，确定服务是否已准备就绪。  

    > [!Note]  
    > 若要排查 CMG 部署问题，请使用 **CloudMgr.log** 和 **CMGSetup.log**。 有关详细信息，请参阅[日志文件](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway)。


## <a name="configure-primary-site-for-client-certificate-authentication"></a>为主站点配置客户端证书身份验证

如果在客户端向 CMG 验证身份时使用[客户端身份验证证书](certificates-for-cloud-management-gateway.md#bkmk_clientauth)，则按照以下过程来配置每个主站点。  

1. 在 Configuration Manager 控制台中，转到“管理”  工作区，展开“站点配置”  ，然后选择“站点”  。  

2. 选择要将基于 Internet 的客户端分配到的主站点，选择“属性”  。  

3. 切换到主站点属性表的“客户端计算机通信”  选项卡，选中“在可用时使用 PKI 客户端证书(客户端身份验证)”  。  

    > [!Note]
    > 从版本 1906 开始，此选项卡称为“通信安全”  。<!-- SCCMDocs#1645 -->  

4. 如果未发布 CRL，请取消选择“客户端检查站点系统的证书吊销列表(CRL)”选项  。  


## <a name="add-the-cmg-connection-point"></a>添加 CMG 连接点

CMG 连接点是与 CMG 通信的站点系统角色。 若要添加 CMG 连接点，请按照常规说明[安装站点系统角色](../../../servers/deploy/configure/install-site-system-roles.md)。 在“添加站点系统角色”向导的“系统角色选择”页上，选择“云管理网关连接点”  。 然后选择该服务器连接到的“云管理网关名称”  。 该向导会显示选定 CMG 所在的区域。

> [!Important]
> 在某些情况下，CMG 连接点必须具有[客户端身份验证证书](certificates-for-cloud-management-gateway.md#bkmk_clientauth)。

若要排查 CMG 服务运行状况问题，请使用 **CMGService.log** 和 **SMS_Cloud_ProxyConnector.log**。 有关详细信息，请参阅[日志文件](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway)。


## <a name="configure-client-facing-roles-for-cmg-traffic"></a>为 CMG 通信配置面向客户端的角色

配置管理点和软件更新点站点系统以接受 CMG 通信。 在主站点上，针对为基于 Internet 的客户端提供服务的所有管理点和软件更新点执行以下过程。  

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“站点配置”，然后选择“服务器和站点系统角色”节点    。 在功能区“主页”选项卡的“查看”组中，选择“具有角色的服务器”  。 然后从列表中选择“管理点”  。  

2. 选择要为 CMG 通信配置的站点系统服务器。 在细节窗格中选择“管理点”角色，然后选择功能区中的“属性”   。  

3. 在管理点属性表中的“客户端连接”下，选中“允许 Configuration Manager 云管理网关通信”  旁边的复选框。

    根据你的 CMG 设计和 Configuration Manager 版本，可能需要启用“HTTPS”  选项。 有关详细信息，请参阅[为管理点启用 HTTPS](certificates-for-cloud-management-gateway.md#bkmk_mphttps)。  

4. 选择“确认”以关闭管理点属性窗口  。  

为其他管理点（酌情而定）和所有软件更新点重复这些步骤。


## <a name="configure-boundary-groups"></a>配置边界组

<!--3640932-->
从版本 1902 开始，可以将 CMG 与边界组关联。 此配置允许客户端根据边界组关系默认或回退到 CMG 以进行客户端通信。

有关边界组的详细信息，请参阅[配置边界组](../../../servers/deploy/configure/boundary-groups.md)。

在[创建或边界组](../../../servers/deploy/configure/boundary-group-procedures.md)时，在“引用”  选项卡上，添加云管理网关。 此操作将 CMG 与此边界组关联。


## <a name="configure-clients-for-cmg"></a>为 CMG 配置客户端

一旦运行 CMG 和站点系统角色，客户端就会在发出下一个位置请求时自动获取 CMG 服务的位置。 除非[安装并分配 Windows 10 客户端（使用 Azure AD 进行身份验证）](../../deploy/deploy-clients-cmg-azure.md)，否则客户端必须位于 Intranet 上，才能接收 CMG 服务的位置。 位置请求的轮询周期为 24 小时。 如果不想等待按正常计划执行的位置请求，可以通过重新启动计算机上的 SMS 代理主机服务 (ccmexec.exe) 强制执行该请求。  

> [!Note]
> 默认情况下，所有客户端均接收 CMG 策略。 可使用客户端设置[“允许客户端使用云管理网关”](../../deploy/about-client-settings.md#enable-clients-to-use-a-cloud-management-gateway)控制此行为。

Configuration Manager 客户端会自动确定它是在 Intranet 上还是在 Internet 上。 如果客户端可以访问域控制器或本地管理点，它会将自己的连接类型设置为“当前 Intranet”  。 否则，它会切换为“当前 Internet”  ，并使用 CMG 服务的位置与站点通信。

>[!NOTE]
> 不管客户端是在 Intranet 上还是在 Internet 上，都可以强制它始终使用 CMG。 此配置可用于测试目的，或用于你希望强制始终使用 CMG 的客户端。 请在客户端上设置以下注册表项：
>
> `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Security, ClientAlwaysOnInternet = 1`
>
> 也可以在客户端安装期间使用 [CCMALWAYSINF](../../deploy/about-client-installation-properties.md#ccmalwaysinf) 属性指定此设置。
>
> 即使客户端漫游到边界组配置将以其他方式利用本地资源的位置，此设置也将始终适用。


若要验证客户端是否具有指定 CMG 的策略，请在客户端计算机上以管理员身份打开 Windows PowerShell 命令提示符，然后运行以下命令：`Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}`

此命令会显示客户端知道的所有基于 Internet 的管理点。 虽然 CMG 在技术上不是基于 Internet 的管理点，但对客户端而言却是如此。

> [!Note]  
> 若要排查 CMG 客户端通信问题，请使用 **CMGHttpHandler.log**、**CMGService.log** 和 **SMS_Cloud_ProxyConnector.log**。 有关详细信息，请参阅[日志文件](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway)。


## <a name="modify-a-cmg"></a>修改 CMG

创建 CMG 之后，可以修改它的某些设置。 在 Configuration Manager 控制台中选择该 CMG，然后选择“属性”  。 配置以下选项卡上的设置：  

#### <a name="general"></a>常规

- **Azure 管理证书**：更改 CMG 的 Azure 管理证书。 在证书过期之前更新证书时，此选项很有用。  

#### <a name="settings"></a>设置

- **证书文件**：更改 CMG 的服务器身份验证证书。 在证书过期之前更新证书时，此选项很有用。  

- **VM 实例**：更改该服务在 Azure 中使用的虚拟机数量。 此设置允许你基于利用率或成本考虑，以动态方式横向或纵向扩展该服务。  

- **证书**：添加或删除受信任的根或中间 CA 证书。 在添加新的 CA 或停用过期证书时，此选项很有用。  

- **验证客户端证书吊销**：如果最初在创建 CMG 时未启用此设置，可以在发布 CRL 后启用。 有关详细信息，请参阅[发布证书吊销列表](security-and-privacy-for-cloud-management-gateway.md#bkmk_crl)。  

- 允许 CMG 充当云分发点，并提供 Azure 存储中的内容  ：从版本 1806 开始，默认启用此新选项。 CMG 现还可向客户提供内容。 此功能减少了所需的证书和 Azure VM 的成本。<!--1358651-->  

#### <a name="alerts"></a>警报

可在创建 CMG 后随时重新配置警报。


### <a name="redeploy-the-service"></a>重新部署服务

较重大的更改（例如以下配置）需要重新部署服务：

- 经典部署方法改为 Azure 资源管理器部署方法
- 订阅
- 服务名称
- 专用于公有 PKI
- 区域

为基于 Internet 的客户端始终保留至少一个活动的 CMG，以便接收更新的策略。 基于 Internet 的客户端无法与已删除的 CMG 通信。 除非漫游回到 Intranet，否则客户端不知道有新的 CMG。 在创建第二个 CMG 实例以删除第一个 CMG 实例时，还要创建另一个 CMG 连接点。

默认情况下，客户端每 24 小时刷新一次策略，因此，在创建新的 CMG 后至少要等一天才能删除旧的 CMG。 如果客户端处于关闭状态或未连接到 Internet，你可能需要等待更长时间。

如果经典部署方法上已有 CMG，则必须部署新的 CMG 才能使用 Azure 资源管理器部署方法。<!--509753--> 共有两个选项：  

- 如果要重新使用相同的服务名称：  

    1. 首先删除经典 CMG，删除时应考虑为基于 Internet 的客户端始终保留至少一个活动的 CMG 的指导原则。  

    2. 使用资源管理器部署创建新的 CMG。 重新使用相同的服务器身份验证证书。  

    3. 将 CMG 连接点重新配置为使用新的 CMG 实例。  

- 如果要使用新的服务名称：  

    1. 使用资源管理器部署创建新的 CMG。 使用新的服务器身份验证证书。  

    2. 创建新的 CMG 连接点并与新的 CMG 链接。  

    3. 等待至少一天，以便基于 Internet 的客户端接收有关新 CMG 的策略。  

    4. 删除经典 CMG。  

> [!Tip]  
> 确定 CMG 的当前部署模型：<!--SCCMDocs issue #611-->  
>
> 1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“云管理网关”节点    。  
> 2. 选择 CMG 实例。  
> 3. 在窗口底部的“详细信息”窗格中，查找“部署模型”属性  。 对于资源管理器部署，该属性为“Azure 资源管理器”  。 具有 Azure 管理证书的旧版部署模型显示为 Azure Service Manager  。
>
> 还可将“部署模型”属性作为列添加到列表视图中  。  

### <a name="modifications-in-the-azure-portal"></a>在 Azure 门户中进行修改

只能从 Configuration Manager 控制台修改 CMG。 不支持直接在 Azure 中修改该服务或基础 VM。 任何更改都有可能在不预先通知的情况下丢失。 与所有 PaaS 一样，该服务可以随时重新生成 VM。 在进行后端硬件维护或向 VM OS 应用更新时，可能会发生这些重新生成操作。

### <a name="delete-the-service"></a>删除服务

如果需要删除 CMG，也从 Configuration Manager 控制台执行此操作。 手动删除 Azure 中的任何组件都会导致系统不一致。 此状态会留下孤立的信息，并且可能发生意外的行为。


## <a name="next-steps"></a>后续步骤

- [监视云管理网关的客户端](monitor-clients-cloud-management-gateway.md)
- [有关云管理网关的常见问题解答](cloud-management-gateway-faq.md)
