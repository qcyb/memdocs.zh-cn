---
title: 增强型 HTTP
titleSuffix: Configuration Manager
description: 使用新式身份验证来保护客户端通信，而无需 PKI 证书。
ms.date: 08/07/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4deac022-e397-4f1f-bc0a-cea6c6c6368d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5d28e0ccef767770092d03898489104ae6f8c674
ms.sourcegitcommit: 693932432270ab3df1df9f5e6783c7f5c6f31252
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87997908"
---
# <a name="enhanced-http"></a>增强型 HTTP

适用范围：Configuration Manager (Current Branch)

<!--1356889,1358460-->

> [!Tip]  
> 此功能在版本 1806 中作为[预发行功能](../../servers/manage/pre-release-features.md)首次引入。 从版本 1810 开始，此功能不再属于预发行功能。  

Microsoft 建议对于所有 Configuration Manager 通信路径使用 HTTPS 通信，但由于管理 PKI 证书的开销，对一些客户来说可能是一个挑战。

Configuration Manager 版本 1806 包括对客户端与站点系统之间的通信方式的改进。 这些改进有两个主要目标：  

- 可保护敏感客户端通信，而无需提供 PKI 服务器身份验证证书。  

- 客户端可安全地从分发点访问内容，而无需网络访问帐户、客户端 PKI 证书和 Windows 身份验证。  

所有其他客户端通信均通过 HTTP 进行。 增强型 HTTP 并不等同于为客户端通信或站点系统启用 HTTPS。<!-- SCCMDocs issue #1212 -->

> [!Note]  
> 对于具有以下要求的客户，PKI 证书仍然是有效选项：  
>
> - 所有客户端通信均通过 HTTPS 进行  
> - 对签名基础架构的高级控制
>
> 另外，如果你已在使用 PKI，那么即使启用了增强型 HTTP，也将使用绑定在 IIS 中的 PKI 证书。



## <a name="scenarios"></a><a name="bkmk_scenario"></a> 方案

以下方案受益于这些改进：  

### <a name="scenario-1-client-to-management-point"></a><a name="bkmk_scenario1"></a> 方案 1：客户端到管理点

<!--1356889-->
如果为站点启用了增强型 HTTP，则[已加入 Azure Active Directory (Azure AD) 的设备](/azure/active-directory/devices/concept-azure-ad-join)和具有 [Configuration Manager 颁发的令牌](../../clients/deploy/deploy-clients-cmg-token.md)的设备可以与为 HTTP 配置的管理点通信。 启用增强型 HTTP 后，站点服务器会为管理点生成证书，使其能够通过安全通道进行通信。

> [!Note]  
> 此方案不需要使用启用了 HTTPS 的管理点，但作为一种使用增强型 HTTP 的替代方法，也受到了支持。 有关使用启用了 HTTPS 的管理点的详细信息，请参阅[为 HTTPS 启用管理点](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps)。  

### <a name="scenario-2-client-to-distribution-point"></a><a name="bkmk_scenario2"></a> 方案 2：客户端到分发点

<!--1358228-->
工作组或已加入 Azure AD 的客户端可通过安全通道从为 HTTP 配置的分发点进行身份验证及下载内容。 这些类型的设备还可从为 HTTPS 配置的分发点进行身份验证和下载内容，而无需在客户端上使用 PKI 证书。 将客户端身份验证证书添加到工作组或已加入 Azure AD 的客户端，这颇具挑战性。

此行为包括 OS 部署方案，其中任务序列从启动媒体、PXE 或软件中心运行。 有关详细信息，请参阅[网络访问帐户](accounts.md#network-access-account)。<!--1358278-->

### <a name="scenario-3-azure-ad-device-identity"></a><a name="bkmk_scenario3"></a> 方案 3：Azure AD 设备标识

<!--1358460-->
没有 Azure AD 用户登录的已加入 Azure AD 的设备或[混合 Azure AD 设备](/azure/active-directory/devices/concept-azure-ad-join-hybrid)可安全地与其分配的站点进行通信。 现在，对于以设备为中心的方案，基于云的设备标识足以通过 CMG 和管理点进行身份验证。 （以用户为中心的方案仍然需要用户令牌。）  


## <a name="features"></a>功能

以下 Configuration Manager 功能支持或要求增强型 HTTP：

- [云管理网关](../../clients/manage/cmg/plan-cloud-management-gateway.md)
- [没有网络访问帐户的 OS 部署](../../../osd/plan-design/planning-considerations-for-automating-tasks.md#enhanced-http)
- [为基于 Internet 的新 Windows 10 设备启用共同管理](../../../comanage/tutorial-co-manage-new-devices.md)
- [通过电子邮件批准应用程序](../../../apps/deploy-use/app-approval.md#bkmk_email-approve)
- [管理服务](../../../develop/adminservice/overview.md)
- [查看最近连接的控制台](../../servers/manage/admin-console.md#bkmk_viewconnected)

> [!Note]  
> 软件更新点和相关方案始终支持与客户端以及云管理网关的安全 HTTP 通信。 它使用的管理点机制与基于证书或令牌的身份验证不同。<!-- SCCMDocs issue #1148 -->


## <a name="prerequisites"></a>必备条件  

- 针对 HTTP 客户端连接配置的管理点。 在管理点角色属性的“常规”选项卡上设置此选项。  

- 针对 HTTP 客户端连接配置的分发点。 在管理点角色属性的“通信”选项卡上设置此选项。 请勿启用选项“允许客户端进行匿名连接”。  

- 将站点载入 Azure AD 以便进行云管理。  

- 仅适用于[方案 3](#bkmk_scenario3)：运行 Windows 10 版本 1803 或更高版本且已加入 Azure AD 的客户端。 客户端需要此配置来进行 Azure AD 设备身份验证。<!-- SCCMDocs issue 1126 -->


## <a name="configure-the-site"></a>配置站点

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“站点配置”，然后选择“站点”节点  。 选择一个站点，然后选择功能区中的“属性”。  

2. 切换到“客户端计算机通信”选项卡。

    > [!Note]
    > 从版本 1906 开始，此选项卡称为“通信安全”。<!-- SCCMDocs#1645 -->  

    选择“HTTPS 或 HTTP”的选项。 然后启用“将 Configuration Manager 生成的证书用于 HTTP 站点系统”选项。

> [!Tip]
> 请等待 30 分钟以便管理点从站点接收并配置新证书。

<!--3798957-->
从版本 1902 开始，还可以启用管理中心站点的增强型 HTTP。 使用此相同流程，并打开管理中心站点的属性。 此操作仅为管理中心站点上的 SMS 提供程序角色启用增强型 HTTP。 它不是适用于层次结构中所有站点的全局设置。

可以在 Configuration Manager 控制台中查看这些证书。 转到“管理”工作区，展开“安全”，然后选择“证书”节点。 查找“SMS 发证”根证书，以及由 SMS 发证根颁发的站点服务器角色证书。

有关客户端如何使用此配置与管理点和分发点进行通信的详细信息，请参阅[从客户端到站点系统和服务的通信](communications-between-endpoints.md#Planning_Client_to_Site_System)。

## <a name="validate-the-certificate"></a>验证证书

如果你启用增强型 HTTP，站点服务器会生成名为“SMS 角色 SSL 证书”的自签名证书。 此证书由根“SMS 颁发”证书颁发。 管理点将此证书添加到与端口 443 绑定的 IIS 默认网站。

若要查看配置的状态，请查阅 mpcontrol.log。

## <a name="see-also"></a>另请参阅

- [规划安全性](../security/plan-for-security.md)  

- [Configuration Manager 客户端的安全和隐私](../../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [配置安全性](../security/configure-security.md)  

- [终结点之间的通信](communications-between-endpoints.md)  
