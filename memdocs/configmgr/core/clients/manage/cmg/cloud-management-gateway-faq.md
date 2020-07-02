---
title: CMG 常见问题解答
titleSuffix: Configuration Manager
description: 使用本文解答有关云管理网关的常见问题
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 06/10/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 4c1a128d-22fb-49f1-8e0b-36513a8dc117
ms.openlocfilehash: bd846b0155a0baddad76d6027ffbd239d7dbf26f
ms.sourcegitcommit: 5f15a3abf33ce7bfd6855ffeef2ec3cd4cd48a7f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721884"
---
# <a name="frequently-asked-questions-about-the-cloud-management-gateway"></a>有关云管理网关的常见问题解答

适用范围：Configuration Manager (Current Branch)

本文解答了有关云管理网关的常见问题。 有关详细信息，请参阅[规划云管理网关](plan-cloud-management-gateway.md)。

## <a name="frequently-asked-questions"></a>常见问题解答

### <a name="what-certificates-do-i-need"></a>我需要什么证书？

有关更多详细信息，请参阅[云管理网关的证书](certificates-for-cloud-management-gateway.md)。

### <a name="do-i-need-azure-expressroute"></a>我需要 Azure ExpressRoute 吗？

不能。 通过 [Azure ExpressRoute](/azure/expressroute/expressroute-introduction) 可将本地网络扩展到 Microsoft 云中。 ExpressRoute 或其他此类虚拟网络连接对 Configuration Manager 云管理网关不是必需的。 云管理网关的设计允许基于 Internet 的客户端通过 Azure 服务与本地站点系统进行通信，而无需其他网络配置。 有关详细信息，请参阅[规划云管理网关](plan-cloud-management-gateway.md)

<!-- SCCMDocs#1659 -->

### <a name="do-i-need-to-maintain-the-azure-virtual-machines"></a>我需要维护 Azure 虚拟机吗？

不需要维护。 云管理网关的设计使用 Azure 平台即服务 (PaaS)。 通过使用你提供的订阅，Configuration Manager 可创建必要的虚拟机 (VM)、存储和网络。 Azure 可保护和更新虚拟机。 与基础结构即服务 (IaaS) 一样，这些 VM 不是本地环境的一部分。 云管理网关是将 Configuration Manager 环境扩展到云端的 PaaS。 有关详细信息，请参阅[保护 PaaS 部署](/azure/security/security-paas-deployments)。

### <a name="how-can-i-ensure-service-continuity-during-service-updates"></a>如何在服务更新期间确保服务连续性？

通过扩展 CMG 以包含两个或更多实例，可以自动从 Azure 的更新域中受益。 请参阅[如何更新云服务](/azure/cloud-services/cloud-services-update-azure-service)。

### <a name="im-already-using-ibcm-if-i-add-cmg-how-do-clients-behave"></a>我已经在使用 IBCM 了。 如果添加 CMG，客户端会有何种行为？

如果已经部署[基于 Internet 的客户端管理](../plan-internet-based-client-management.md) (IBCM)，还可以部署云管理网关。 客户端会收到这两个服务的策略。 当它们漫游到 Internet 上时，会随机选择并使用这些基于 Internet 的服务之一。

### <a name="do-the-user-accounts-have-to-be-in-the-same-azure-ad-tenant-as-the-tenant-associated-with-the-subscription-that-hosts-the-cmg-cloud-service"></a><a name="bkmk_tenant"></a> 用户帐户是否必须与托管 CMG 云服务的订阅关联的租户位于同一 Azure AD 租户中？
<!--SCCMDocs-pr issue #2873-->
否，可以将 CMG 部署到任何可以托管 Azure 云服务的订阅中。

阐明术语：

- 租户是用户帐户和应用注册的目录。 一个租户可以有多个订阅。
- 订阅将计费、资源和服务分开。 它与单个租户相关联。

此问题在以下方案中很常见：  

- 当拥有不同测试和生产 Active Directory 和 Azure AD 环境时，只需一个集中式 Azure 托管订阅。

- 对 Azure 的使用在不同团队中已得到长足发展

使用资源管理器部署时，加入与订阅关联的 Azure AD 租户。 此连接允许 Configuration Manager 对 Azure 进行身份验证，以创建、部署和管理 CMG。  

若对通过 CMG 托管的用户和设备使用 Azure AD 身份验证，则载入该 Azure AD 租户。 有关云管理的 Azure 服务的详细信息，请参阅[配置 Azure 服务](../../../servers/deploy/configure/azure-services-wizard.md)。 载入每个 Azure AD 租户时，单个 CMG 可为多个租户提供 Azure AD 身份验证，无论托管位置在何处。

#### <a name="example-1-one-tenant-with-multiple-subscriptions"></a>示例 1：一个包含多个订阅的租户

用户标识、设备注册和应用注册都在同一个租户中。 你可以选择 CMG 使用的订阅。 可以将多个 CMG 服务从一个站点部署到单独的订阅中。 该站点与租户之间存在一对一的关系。 可以根据各种原因（如计费或逻辑分离）决定要使用的订阅。

#### <a name="example-2-multiple-tenants"></a>示例 2：多个租户

换句话说，你的环境具有多个 Azure AD。 如果需要支持两个租户中的用户和设备标识，则需要将站点附加到每个租户。 此过程需要每个租户的管理帐户才能在该租户中创建应用注册。 然后，一个站点可以在多个租户中托管 CMG 服务。 可以在任一租户的任何可用订阅中创建 CMG。 已联接或混合联接任一 Azure AD 的设备可以使用 CMG。

如果用户和设备标识在一个租户中，但 CMG 的订阅在另一个租户中，则需要将该站点连接到这两个租户。 从技术上讲，只具有 CMG 服务的第二个租户不需要客户端应用。 客户端应用仅为使用 CMG 服务的客户端提供用户和设备身份验证。<!-- SCCMDocs#1902 -->

### <a name="how-does-cmg-affect-my-clients-connected-via-vpn"></a>CMG 如何影响通过 VPN 连接的客户端？

通过 VPN 连接到环境的漫游客户端通常被检测到面向 Intranet。 它们尝试连接到本地基础结构，如管理点和分发点。 一些客户希望由云服务管理这些漫游客户端，即使在通过 VPN 连接的情况下。 从版本 1902 开始，可以将 CMG 与边界组关联。 此操作将强制这些客户端不使用本地站点系统。 有关详细信息，请参阅[配置边界组](setup-cloud-management-gateway.md#configure-boundary-groups)。

### <a name="if-i-enable-a-cmg-will-my-clients-only-connect-to-the-cmg-enabled-management-point-when-theyre-connected-to-the-intranet"></a>如果启用 CMG，那么客户端在连接到 Intranet 时是否仅连接到已启用 CMG 的管理点？

为了保护通过 CMG 发送的敏感流量，可配置 HTTPS 管理点或使用增强型 HTTP。

如果选择部署 CMG，并使用 PKI 证书在已启用 CMG 的管理点上进行 HTTPS 通信，请在管理点属性上选择“仅允许 Internet 客户端”。 此设置可确保内部客户端继续在你的环境中使用 HTTP 管理点。

如果使用增强型 HTTP，则无需配置此设置。 直接与已启用 CMG 的管理点通信时，客户端继续使用 HTTP。 有关详细信息，请参阅[增强型 HTTP](../../../plan-design/hierarchy/enhanced-http.md)。

## <a name="next-steps"></a>后续步骤

- [规划云管理网关](plan-cloud-management-gateway.md)
- [设置云管理网关](setup-cloud-management-gateway.md)
- [云管理网关的证书](certificates-for-cloud-management-gateway.md)
- [云管理网关的安全和隐私](security-and-privacy-for-cloud-management-gateway.md)
- [云管理网关的大小和扩展数量](../../../plan-design/configs/size-and-scale-numbers.md#bkmk_cmg)
