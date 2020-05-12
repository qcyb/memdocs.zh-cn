---
title: 代理服务器支持
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 站点系统服务器如何使用代理服务器。
ms.date: 05/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9123a87a-0b6f-43c7-b5c2-fac5d09686b1
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 89a2f76f394d3bdf8fd6785429ae0ae60302537a
ms.sourcegitcommit: 14d7dd0a99ebd526c9274d5781c298c828323ebf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82802083"
---
# <a name="proxy-server-support-in-configuration-manager"></a>Configuration Manager 中的代理服务器支持

适用范围：  Configuration Manager (Current Branch)

某些 Configuration Manager 站点系统服务器需要连接到 Internet。 如果环境需要 Internet 流量才能使用代理服务器，请配置这些站点系统角色以使用代理。  

- 托管站点系统服务器的计算机支持单个代理服务器配置。 该计算机上的所有站点系统角色都共享上述相同的代理配置。 如果需要为不同的角色或角色实例使用单独的代理服务器，请将这些角色放在不同的站点系统服务器上。  

- 在为已有代理服务器配置的站点系统服务器配置新的代理服务器设置时，将覆盖原始配置。  

- 默认情况下，使用托管站点系统角色的计算机的“系统”帐户连接到代理  。  

- 如果计算机帐户无法进行身份验证，则站点系统服务器可存储用户凭据来连接到代理服务器。 这些凭据就是站点系统代理服务器帐户  。  

## <a name="site-system-roles-that-use-a-proxy"></a>使用代理的站点系统角色

以下站点系统角色可连接到 Internet，且在必要时可使用代理服务器：  

### <a name="asset-intelligence-synchronization-point"></a>资产智能同步点

此站点系统角色连接到 Microsoft，并在托管资产智能同步点的计算机上使用代理服务器配置。  

### <a name="cloud-distribution-point"></a>云分发点

云分发点角色在 Microsoft Azure 中运行。 请不要将此站点系统角色配置为使用代理。 在管理云分发点的主站点服务器上设置代理配置。  

对于此配置，主站点服务器：  

- 必须能够连接到 Microsoft Azure 才能设置、监视并将内容分发到云分发点。  

- 默认情况下，使用计算机的“系统”帐户来建立连接  。 必要时，还可使用站点系统代理服务器帐户。  

- 使用 Windows Web 浏览器 API。  

### <a name="cloud-management-gateway-connection-point"></a>云管理网关连接点

云管理网关 (CMG) 连接点是与 Azure 中的 CMG 服务进行通信的本地角色。 有关详细信息，请参阅 [CMG 规划](../../clients/manage/cmg/plan-cloud-management-gateway.md)。

### <a name="distribution-point"></a>分发点

<!-- 5856396 -->

从版本 2002 开始，如果为 Microsoft 联网缓存启用了 Configuration Manager 分发点，则它可以通过未经身份验证的代理服务器进行通信以便实现 Internet 访问。 有关详细信息，请参阅 [Microsoft Connected Cache](../hierarchy/microsoft-connected-cache.md)。

### <a name="exchange-server-connector"></a>Exchange Server 连接器

此站点系统角色连接到 Exchange Server。 它在托管 Exchange Server 连接器的计算机上使用代理服务器配置。  

### <a name="service-connection-point"></a>服务连接点

此站点系统角色连接到 Configuration Manager 云服务以下载 Configuration Manager 的版本更新。 它使用在托管服务连接点的计算机上配置的代理服务器。  

### <a name="software-update-point"></a>软件更新点

此站点系统角色在连接到 Microsoft 更新来下载修补程序和同步相关更新信息时使用代理。 与其他所有站点系统角色一样，请先配置站点系统代理设置。 然后，配置软件更新点特定的下述选项：  

- **同步软件更新时使用代理服务器**  

- **使用自动部署规则下载内容时使用代理服务器**  

    > [!NOTE]
    > 虽然此设置可用，但辅助站点上的软件更新点不使用此设置。  

这些设置位于软件更新点属性的“代理和帐户设置”选项卡上  。  

> [!NOTE]
> 默认情况下，运行自动部署规则时，在创建了自动部署规则的站点的站点服务器上，“系统”帐户用于连接 Internet 并下载软件更新  。 或者，配置并使用站点系统代理服务器帐户。 
>
> 如果此帐户无法访问 Internet，则无法下载软件更新。 以下条目记录到 ruleengine.log 中  :  
> `Failed to download the update from internet. Error = 12007.`  

## <a name="other-features-that-use-the-proxy-for-a-site-system-server"></a><a name="bkmk_other"></a> 使用站点系统服务器的代理的其他功能

（从版本 2002 中引入） 

从 Configuration Manager 版本 2002 开始，以下功能使用承载[服务连接点](#service-connection-point)角色的站点系统的代理： <!--5913817-->

- [Azure Active Directory (Azure AD) 用户发现](../../servers/deploy/configure/about-discovery-methods.md#azureaddisc)
- [Azure AD 用户组发现](../../servers/deploy/configure/about-discovery-methods.md#bkmk_azuregroupdisco)
- [将集合成员身份结果同步到 Azure Active Directory 组](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync)

## <a name="configure-the-proxy-for-a-site-system-server"></a>配置站点系统服务器的代理  

1. 在 Configuration Manager 控制台中，转到“管理”  工作区。 展开“站点配置”，然后选择“服务器和站点系统角色”节点   。  

2. 选择要编辑的站点系统服务器。 在细节窗格中，右键单击“站点系统”角色，然后选择“属性”   。  

3. 在“站点系统属性”中，切换到“代理”选项卡  。配置以下代理设置：  

    - **同步 Internet 中的信息时使用代理服务器**：选择此选项可使站点系统服务器使用代理服务器。  

    - **代理服务器名称**：指定环境中代理服务器的主机名或 FQDN。  

    - **端口**：指定与代理服务器进行通信的网络端口。 默认使用端口 80  。  

    - **使用凭据连接至代理服务器**：许多代理服务器都要求用户进行身份验证。 站点系统服务器默认使用其计算机帐户来连接到代理服务器。 如有必要，请启用此选项，单击“设置”，然后选择“现有帐户”或指定“新帐户”    。 这些凭据就是站点系统代理服务器帐户  。  有关详细信息，请参阅 [Configuration Manager 中使用的帐户](../hierarchy/accounts.md)。  

4. 选择“确定”  以保存新的代理服务器配置。  

## <a name="next-steps"></a>后续步骤

如果你的组织使用防火墙或代理设备限制与 Internet 的网络通信，则需要允许访问 Internet 终结点。 有关详细信息，请参阅 [Internet 访问要求](internet-endpoints.md)。
