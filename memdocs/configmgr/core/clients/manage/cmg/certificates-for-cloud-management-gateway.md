---
title: CMG 证书
titleSuffix: Configuration Manager
description: 了解用于云管理网关的各种数字证书。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 06/10/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 71eaa409-b955-45d6-8309-26bf3b3b0911
ms.openlocfilehash: b5a9a4a7f23942ac06dc16a0b54b657c7fd617a9
ms.sourcegitcommit: 2f1963ae208568effeb3a82995ebded7b410b3d4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2020
ms.locfileid: "84715605"
---
# <a name="certificates-for-the-cloud-management-gateway"></a>云管理网关证书

适用范围：Configuration Manager (Current Branch)

根据通过云管理网关 (CMG) 管理 Internet 上的客户端所用的方案，可能需要以下一个或多个数字证书：  

- [CMG 服务器身份验证证书](#bkmk_serverauth)  
  - [针对客户端的 CMG 受信任的根证书](#bkmk_cmgroot)  
  - [由公共提供程序颁发的服务器身份验证证书](#bkmk_serverauthpublic)  
  - [企业 PKI 颁发的服务器身份验证证书](#bkmk_serverauthpki)  

- [客户端身份验证证书](#bkmk_clientauth)
  - [CMG 连接点](#bkmk_cmgcp)
  - [针对 CMG 的客户端受信任的根证书](#bkmk_clientroot)  

- [为 HTTPS 启用管理点](#bkmk_mphttps)  

- [Azure 管理证书](#bkmk_azuremgmt)  

有关不同方案的详细信息，请参阅[规划云管理网关](plan-cloud-management-gateway.md)。

## <a name="general-information"></a>常规信息

<!--SCCMDocs issue #779-->
云管理网关的证书支持以下配置：  

- 2048 位或 4096 位密钥长度

- 证书私钥的密钥存储提供程序。 有关详细信息，请参阅 [CNG 证书概述](../../../plan-design/network/cng-certificates-overview.md)。  

- 在使用以下策略配置 Windows 时：**系统加密：对加密、哈希和签名使用 FIPS 兼容算法**  

- TLS 1.2。 有关详细信息，请参阅[如何启用 TLS 1.2](../../../plan-design/security/enable-tls-1-2.md)。  

## <a name="cmg-server-authentication-certificate"></a><a name="bkmk_serverauth"></a>CMG 服务器身份验证证书

所有方案都需要此证书。

在 Configuration Manager 控制台中创建 CMG 时需要提供此证书。

CMG 创建基于 Internet 的客户端要连接到的 HTTPS 服务。 此服务器需要使用服务器身份验证证书构建安全频道。 请从公共提供程序获取此用途的证书，或通过公钥基础结构 (PKI) 颁发此证书。 有关详细信息，请参阅[针对客户端的 CMG 受信任的根证书](#bkmk_cmgroot)。

> [!NOTE]
> CMG 服务器身份验证证书支持通配符。 某些证书颁发机构颁发证书时将通配符用作主机名。 例如，`*.contoso.com`。 某些组织使用通配符证书简化其 PKI 并降低维护成本。<!--491233-->  
>
> 有关如何将 CMG 与通配符证书配合使用的详细信息，请参阅[设置 CMG](setup-cloud-management-gateway.md#set-up-a-cmg)。<!--SCCMDocs issue #565-->  

此证书需要使用全局唯一名称标识 Azure 中的服务。 请求证书前，请确认所需的 Azure 域名是否唯一。 例如，GraniteFalls.CloudApp.Net。

1. 登录到 [Azure 门户](https://portal.azure.com)。
1. 选择“所有资源”，然后选择“添加”。 
1. 搜索“云服务”。 选择“创建”。
1. 在“DNS 名称”字段中，键入所需的前缀，例如 GraniteFalls。 界面将反映域名是否可用，或是否已被其他服务使用。

    > [!Important]  
    > 不要在门户中创建服务，仅使用此流程检查名称可用性。

若还要为内容启用 CMG，请确认 CMG 服务名称也是唯一的 Azure 存储帐户名称。 若 CMG 云服务名称是唯一的，但存储帐户名称不是唯一的，Configuration Manager 将无法在 Azure 中预配此服务。 在 Azure 门户中重复上面的过程，并执行下面的更改：

- 搜索“存储帐户”
- 在“存储帐户名称”字段中测试你的名称

DNS 名称前缀（例如 GraniteFalls）的长度应为 3 到 24 个字符，并且只能使用字母数字字符。 不要使用特殊字符，如短划线 (`-`)。<!-- SCCMDocs#1080 -->

### <a name="cmg-trusted-root-certificate-to-clients"></a><a name="bkmk_cmgroot"></a>针对客户端的 CMG 受信任的根证书

客户端必须信任 CMG 服务器身份验证证书。 有两种方法可实现此信任：

- 使用公共和全局受信任的证书提供程序提供的证书。 例如（但不限于）DigiCert、Thawte 或 VeriSign。 Windows 客户端包括来自这些提供程序的受信任的根证书颁发机构 (CA)。 通过使用这些受信任提供程序中的一个提供程序发布的服务器身份验证证书，客户端会自动信任该证书。  

- 使用公钥基础结构 (PKI) 中的企业 CA 颁发的证书。 大多数企业 PKI 实现会向 Windows 客户端添加受信任的根 CA。 例如，在组策略中使用 Active Directory 证书服务。 如果从客户端不自动信任的 CA 颁发 CMG 服务器身份验证证书，请将 CA 受信任的根证书添加到基于 Internet 的客户端。  

  - 还可以使用 Configuration Manager 证书配置文件在客户端上预配证书。 有关详细信息，请参阅[证书配置文件简介](../../../../protect/deploy-use/introduction-to-certificate-profiles.md)。

  - 如果打算[从 Intune 安装 Configuration Manager 客户端](../../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client)，还可以使用 Intune 证书配置文件在客户端上预配证书。 有关详细信息，请参阅[配置证书配置文件](../../../../../intune/protect/certificates-configure.md)。

### <a name="server-authentication-certificate-issued-by-public-provider"></a><a name="bkmk_serverauthpublic"></a>由公共提供程序颁发的服务器身份验证证书

第三方证书提供商无法为 CloudApp.net 创建证书，因为该域为 Microsoft 所拥有。 你只能获取为你拥有的域颁发的证书。 从第三方提供商获取证书的主要原因是你的客户已经信任该提供商的根证书。

使用以下流程创建 DNS 别名：

1. 在组织的公共 DNS 中创建规范名称记录 (CNAME)。 该记录会将 CMG 的别名创建为一个友好名称，你可以在公共证书中使用。

    例如，Contoso 将其 CMG 命名为“GraniteFalls”。 在 Azure 中，此名称变为“GraniteFalls.CloudApp.Net”。 在 Contoso 的公共 DNS contoso.com 命名空间中，DNS 管理员为实际主机名 GraniteFalls.CloudApp.net 新建 GraniteFalls.Contoso.com 的 CNAME 记录 。  

2. 使用 CNAME 别名的公用名称 (CN) 向公共提供程序请求一个服务器身份验证证书。
例如，Contoso 对证书 CN 使用 **GraniteFalls.Contoso.com**。  

3. 使用此证书在 Configuration Manager 控制台中创建 CMG。 在创建云管理网关向导的“设置”页面：  

    - 当（从“证书文件”）添加此云服务的服务器证书时，向导将从证书 CN 中提取主机名用作服务名称。  

    - 然后将该主机名追加到 Azure 美国政府云的 cloudapp.net 或 usgovcloudapp.net，作为用于在 Azure 中创建服务的服务 FQDN 。  

    - 例如，当 Contoso 创建 CMG 时，Configuration Manager 会从证书 CN 中提取主机名 GraniteFalls。 Azure 将实际服务创建为 GraniteFalls.CloudApp.net。  

在 Configuration Manager 中创建 CMG 实例时，虽然该证书具有 GraniteFalls.Contoso.com，但 Configuration Manager 仅提取主机名，例如：GraniteFalls。 它将该主机名追加到创建云服务时 Azure 所需的 CloudApp.net。 域的 DNS 命名空间中的 CNAME 别名 Contoso.com 将这两个 FQDN 映射在一起。 Configuration Manager 为客户端提供了用于访问此 CMG 的策略，DNS 映射将其绑定在一起，以便它们可以安全地访问 Azure 中的服务。<!--SCCMDocs issue #565-->  

### <a name="server-authentication-certificate-issued-from-enterprise-pki"></a><a name="bkmk_serverauthpki"></a>企业 PKI 颁发的服务器身份验证证书

为 CMG 创建与云分发点相同的自定义 SSL 证书。 按照[为基于云的分发点部署服务证书](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clouddp2008_cm2012)中的说明，但以不同方式执行以下操作：

- 请求自定义 Web 服务器证书时，为证书公用名称提供 FQDN。 该名称可以是你拥有的公共域名，或者你也可以使用 cloudapp.net 域。 如果使用你自己的公共域，请参阅以上过程，以便在组织的公共 DNS 中创建 DNS 别名。  

- 将 cloudapp.net 公共域用于 CMG Web 服务器证书时：  

  - 在 Azure 公有云上，请使用以 cloudapp.net 结尾的名称  

  - 针对 Azure 美国政府云，请使用以 usgovcloudapp.net 结尾的名称  

## <a name="client-authentication-certificate"></a><a name="bkmk_clientauth"></a>客户端身份验证证书

客户端身份验证证书要求：

- 运行未加入 Azure Active Directory (Azure AD) 的 Windows 8.1 和 Windows 10 设备的基于 Internet 的客户端需要此证书。
- CMG 连接点可能需要此证书。 有关详细信息，请参阅 [CMG 连接点](#bkmk_cmgcp)。
- 加入 Azure AD 的 Windows 10 客户端不需要此证书。
- 如果你的站点为版本 2002 或更高版本，则设备可以使用由该站点颁发的令牌。 有关详细信息，请参阅[基于令牌的 CMG 身份验证](../../deploy/deploy-clients-cmg-token.md)。

客户端使用此证书向 CMG 进行身份验证。 已加入混合域或云域的 Windows 10 设备不需要此证书，因为它们使用 Azure AD 进行身份验证。

请在 Configuration Manager 的上下文外预配此证书。 例如，使用 Active Directory 证书服务和组策略颁发客户端身份验证证书。 有关详细信息，请参阅[为 Windows 计算机部署客户端证书](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012)。

> [!NOTE]
> Microsoft 建议将设备加入 Azure AD。 基于 Internet 的设备可以使用 Azure AD 向 Configuration Manager 进行身份验证。 无论设备是在 Internet 上还是连接到内部网络，它都同时支持设备和用户方案。 有关详细信息，请参阅[使用 Azure AD 标识安装和注册客户端](../../deploy/deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity)。
>
> 从版本 2002 开始，<!--5686290--> Configuration Manager 扩展了它对基于 Internet 的设备的支持，这些设备不经常连接到内部网络、无法加入 Azure AD 且无法安装 PKI 颁发的证书。 有关详细信息，请参阅[基于令牌的 CMG 身份验证](../../deploy/deploy-clients-cmg-token.md)。

### <a name="cmg-connection-point"></a><a name="bkmk_cmgcp"></a> CMG 连接点

若要安全转发客户端请求，CMG 连接点需要与管理点建立安全连接。 根据配置设备和管理点的方式，确定 CMG 连接点配置。

- 管理点是 HTTPS

  - 客户端具有客户端身份验证证书：CMG 连接点需要与 HTTPS 管理点上的服务器身份验证证书相对应的客户端身份验证证书。

  - 客户端使用 Azure AD 身份验证或 Configuration Manager 令牌：此证书不是必需的。

- 如果为增强型 HTTP 配置管理点：此证书不是必需的。

有关详细信息，请参阅[为管理点启用 HTTPS](#bkmk_mphttps)。

### <a name="client-trusted-root-certificate-to-cmg"></a><a name="bkmk_clientroot"></a>针对 CMG 的客户端受信任的根证书

*使用客户端身份验证证书时需要此证书。如果所有客户端使用 Azure AD 进行身份验证，则不需要此证书*。

在 Configuration Manager 控制台中创建 CMG 时需要提供此证书。

CMG 必须信任客户端身份验证证书。 要实现此信任，请提供受信任的根证书链。 请务必添加信任链中的所有证书。 例如，若客户端身份验证证书由中间 CA 颁发，请同时添加中间和根 CA 证书。

> [!NOTE]  
> 创建 CMG 时，不再需要在“设置”页面上提供受信任的根证书。 使用 Azure AD 进行客户端身份验证时不需要此证书，但往往在向导中需要。 如果使用 PKI 客户端身份验证证书，则仍须向 CMG 添加受信任的根证书。<!--SCCMDocs-pr issue #2872 SCCMDocs issue #1319-->
>
> 在版本 1902 和更早版本中，只能添加两个受信任的根 CA 和四个中间（从属）CA。

#### <a name="export-the-client-certificates-trusted-root"></a>导出客户端证书的受信任根

向计算机颁发客户端身份验证证书后，在该计算机上使用以下流程导出受信任的根。

1. 单击“开始”菜单。 键入“run”打开“运行”窗口。 打开 `mmc`。  

2. 在“文件”菜单中，选择“添加/删除管理单元...”。  

3. 在“添加/删除管理单元”对话框中，选择“证书”，然后选择“添加” 。  

    1. 在“证书管理单元”对话框中，选择“计算机帐户”，然后选择“下一步” 。  

    1. 在“选择计算机”对话框中，选择“本地计算机”，然后选择“完成” 。  

    1. 在“添加/删除管理单元”对话框中，选择“确定”。  

4. 依次展开“证书”、“个人”，然后选择“证书”  。  

5. 选择一个预期用途为“客户端身份验证”的证书。  

    1. 从“操作”菜单中，选择“打开”。  

    1. 转到“证书路径”选项卡。  

    1. 从证书链上选择下一个证书，然后选择“查看证书”。  

6. 在新“证书”对话框中，转到“详细信息”选项卡。选择“复制到文件...”。  

7. 使用默认证书格式（DER 编码二进制 X.509 (.CER)）完成证书导出向导。 记下导出证书的名称和位置。  

8. 导出原始客户端身份验证证书的证书路径中的所有证书。 记下哪些导出证书是中间 CA，哪些是受信任的根 CA。  

## <a name="enable-management-point-for-https"></a><a name="bkmk_mphttps"></a>为 HTTPS 启用管理点

请在 Configuration Manager 的上下文外预配此证书。 例如，使用 Active Directory 证书服务和组策略颁发 Web 服务器证书。 有关详细信息，请参阅 [PKI 证书要求](../../../plan-design/network/pki-certificate-requirements.md)和[为运行 IIS 的站点系统部署 Web 服务器证书](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012)。

使用站点选项“使用 Configuration Manager 为 HTTP 站点系统生成的证书”时，管理点可以是 HTTP。 有关详细信息，请参阅[增强型 HTTP](../../../plan-design/hierarchy/enhanced-http.md)。

> [!TIP]
> 如果未使用增强型 HTTP，并且你的环境具有多个管理点，则无需使用 HTTPS 针对 CMG 启用所有管理点。 将启用 CMG 的管理点配置为“仅 Internet”。 你的本地客户端就不会尝试使用它们。<!-- SCCMDocs#1676 -->

### <a name="enhanced-http-certificate-for-management-points"></a>管理点的增强型 HTTP 证书

如果你启用增强型 HTTP，站点服务器会生成名为“SMS 角色 SSL 证书”的自签名证书（由根 SMS 颁发证书颁发）。 管理点将此证书添加到绑定到端口 443 的 IIS 默认网站。

### <a name="management-point-client-connection-mode-summary"></a>管理点客户端连接模式摘要

这些表总结了管理点是否需要 HTTP 或 HTTPS，具体取决于客户端和站点版本的类型。

#### <a name="for-internet-based-clients-communicating-with-the-cloud-management-gateway"></a>对于与云管理网关通信的基于 Internet 的客户端

配置本地管理点以允许来自 CMG 的连接具有以下客户端连接模式：

| 客户端的类型   | 管理点 |
|------------------|------------------|
| 工作组        | E-HTTP<sup>[备注 1](#bkmk_note1)</sup>HTTPS |
| AD 域加入 | E-HTTP<sup>[备注 1](#bkmk_note1)</sup>HTTPS |
| Azure AD 加入  | E-HTTP、HTTPS |
| 混合加入    | E-HTTP、HTTPS |

<a name="bkmk_note1"></a>

> [!Note]  
> **备注 1**：此配置要求客户端具有[客户端身份验证证书](#bkmk_clientauth)，并且仅支持以设备为中心的方案。  

#### <a name="for-on-premises-clients-communicating-with-the-on-premises-management-point"></a>对于与本地管理点通信的本地客户端

使用以下客户端连接模式配置本地管理点：

| 客户端的类型   | 管理点 |
|------------------|------------------|
| 工作组        | HTTP、HTTPS |
| AD 域加入 | HTTP、HTTPS |
| Azure AD 加入  | HTTPS       |
| 混合加入    | HTTP、HTTPS |

> [!NOTE]  
> AD 域加入客户端支持与 HTTP 或 HTTPS 管理点通信的以设备和用户为中心的方案。  
>
> Azure AD 加入和混合加入客户端可以通过 HTTP 以设备为中心的方案进行通信，但需要使用 E-HTTP 或 HTTPS 来启用以用户为中心的方案。 否则它们的行为与工作组客户端相同。  

#### <a name="legend-of-terms"></a>图例中的术语

- *工作组*：设备未加入域或 Azure AD，但具有[客户端身份验证证书](#bkmk_clientauth)。
- *AD 域加入*：将设备加入本地 Active Directory 域。
- *Azure AD 加入*：也称为云域加入，将设备加入 Azure AD 租户。 有关详细信息，请参阅[加入 Azure AD 的设备](https://docs.microsoft.com/azure/active-directory/devices/concept-azure-ad-join)。
- *混合加入*：将设备加入本地 Active Directory，并向 Azure AD 注册。 有关详细信息，请参阅[已加入混合 Azure AD 的设备](https://docs.microsoft.com/azure/active-directory/devices/concept-azure-ad-join-hybrid)。
- *HTTP*：在管理点属性上，将客户端连接设置为“HTTP”。
- *HTTPS*：在管理点属性上，将客户端连接设置为“HTTPS”。
- *E-HTTP*：在站点属性的“通信安全”选项卡上，将站点系统设置设为“HTTPS 或 HTTP”，并启用选项“将 Configuration Manager 生成的证书用于 HTTP 站点系统”。 为 HTTP 配置管理点，HTTP 管理点可用于 HTTP 和 HTTPS 通信（令牌身份验证方案）。

    > [!Note]
    > 在版本 1902 及更早版本中，此选项卡称为“客户端计算机通信”。<!-- SCCMDocs#1645 -->

## <a name="azure-management-certificate"></a><a name="bkmk_azuremgmt"></a>Azure 管理证书

经典服务部署需要此证书。 Azure 资源管理器部署不需要此证书。

> [!Important]  
> 从版本 1810 开始，Configuration Manager 已弃用 Azure 的经典服务部署。 开始使用适用于云管理网关的 Azure 资源管理器部署。 有关详细信息，请参阅 [CMG 规划](plan-cloud-management-gateway.md#azure-resource-manager)。
>
> 从 Configuration Manager 版本 1902 起，Azure 资源管理器是云管理网关的新实例的唯一部署机制。 Configuration Manager 版本 1902 或更高版本不再需要此证书。<!-- 3605704 -->

在 Azure 门户中的 Configuration Manager 控制台中创建 CMG 时需要提供此证书。

要在 Azure 中创建 CMG，Configuration Manager 服务连接点需要首先对 Azure 订阅进行身份验证。 使用经典服务部署时，它将 Azure 管理证书用于此身份验证。 Azure 管理员会将此证书上传到你的订阅。 在 Configuration Manager 控制台中创建 CMG 时，请提供此证书。

有关如何上传管理证书的详细信息和说明，请参阅 Azure 文档中的以下文章：

- [云服务和管理证书](https://docs.microsoft.com/azure/cloud-services/cloud-services-certs-create#what-are-management-certificates)  

- [上传 Azure 服务管理证书](https://docs.microsoft.com/azure/azure-api-management-certs)  

> [!IMPORTANT]
> 请确保复制与管理证书关联的订阅 ID。 在 Configuration Manager 控制台中创建 CMG 时需使用此证书。

## <a name="next-steps"></a>后续步骤

- [设置云管理网关](setup-cloud-management-gateway.md)  

- [有关云管理网关的常见问题解答](cloud-management-gateway-faq.md)  

- [云管理网关的安全和隐私](security-and-privacy-for-cloud-management-gateway.md)  
