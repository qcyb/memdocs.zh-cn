---
title: 证书配置文件简介
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 中的证书配置文件如何与 Active Directory 证书服务一起使用。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 41dcc259-f147-4420-bff2-b65bdf8cff77
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3598c95d1431915431d96b16c10c7c913741fe3d
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699987"
---
# <a name="introduction-to-certificate-profiles-in-configuration-manager"></a>Configuration Manager 中的证书配置文件简介

适用范围：  Configuration Manager (Current Branch)

证书配置文件适用于 Active Directory 证书服务和网络设备注册服务 (NDES) 角色。 创建并部署托管设备的身份验证证书，让用户可以轻松访问组织资源。 例如，可以创建和部署证书配置文件来为用户提供必要的证书，从而连接到 VPN 和无线连接。

证书配置文件可以自动为用户设备配置对组织资源（如 Wi-Fi 网络和 VPN 服务器）的访问权限。 用户可以访问这些资源，而无需手动安装证书或使用带外进程。 证书配置文件有助于保证公司资源的安全，因为可使用受公钥基础结构 (PKI) 支持的更安全的设置。 例如，可以要求对所有 Wi-fi 和 VPN 连接进行服务器身份验证，因为已在托管设备上部署了所需证书。

证书配置文件提供以下管理功能：  

- 运行不同 OS 类型和版本的设备从证书颁发机构 (CA) 注册和续订证书。 这些证书随后可用于 Wi-Fi 和 VPN 连接。  

- 部署受信任的根 CA 证书和中间 CA 证书。 这些证书在需要服务器身份验证时针对 VPN 和 Wi-Fi 连接在设备上配置一个信任链。  

- 监视并报告已安装的证书。  

**示例 1**：所有员工都需要连接到多个办公室位置的 Wi-Fi 热点。 若要启用简单的用户连接，请先部署连接 Wi-Fi 所需的证书。 然后部署引用该证书的 Wi-Fi 配置文件。  

**示例 2**：假设你的 PKI 已就位。 你希望采用更灵活安全的方法来部署证书。 用户需要从个人设备访问组织资源，但又不影响安全性。 使用特定设备平台支持的设置和协议配置证书配置文件。 随后设备可从面向 Internet 的注册服务器自动请求这些证书。 然后，配置 VPN 配置文件以使用这些证书，以便设备能够访问组织资源。  

## <a name="types"></a>类型

有 3 种类型的证书配置文件：  

- **受信任的 CA 证书**：部署受信任的根 CA 证书或中间 CA 证书。 在设备必须对服务器进行身份验证时，这些证书会形成信任链。  

- **简单证书注册协议 (SCEP)** ：使用 SCEP 协议为设备或用户请求证书。 该类型需要运行 Windows Server 2012 R2 或更高版本的服务器上的网络设备注册服务 (NDES) 角色。

    首先创建“受信任的 CA 证书”证书配置文件，然后才能创建“简单证书注册协议(SCEP)”证书配置文件   。

- **个人信息交换 (.pfx)** ：为设备或用户请求一个 .pfx（又称 PKCS #12）证书。<!--1321368--> 创建 PFX 证书配置文件的方法有两种：

  - 从现有证书[导入凭据](../../mdm/deploy-use/import-pfx-certificate-profiles.md)
  - [定义证书](../../mdm/deploy-use/create-pfx-certificate-profiles.md)颁发机构来处理请求

  > [!Note]  
  > 默认情况下，Configuration Manager 不启用此项可选功能。 必须在使用前启用此功能。 有关详细信息，请参阅[启用更新中的可选功能](../../core/servers/manage/install-in-console-updates.md#bkmk_options)。<!--505213-->  

  可以将 Microsoft 或 Entrust 用作“个人信息交换 (.pfx)”证书的证书颁发机构  。

## <a name="requirements"></a>要求

若要部署使用 SCEP 的证书配置文件，请在站点系统服务器上安装证书注册点。 此外还要在运行 Windows Server 2012 R2 或更高版本的服务器上，为 NDES 安装策略模块（Configuration Manager 策略模块）。 此服务器需要 Active Directory 证书服务角色。 它还需要可供需要证书的设备访问的有效 NDES。 如果设备需要从 Internet 注册证书，那么 NDES 服务器必须可以从 Internet 访问。 例如，若要安全地启用从 Internet 到 NDES 服务器的流量，可以使用 [Azure 应用程序代理](/azure/active-directory/manage-apps/application-proxy)。

PFX 证书还需要一个证书注册点。 此外，请指定证书的证书颁发机构 (CA) 和相关访问凭据。 可以将 Microsoft 或 Entrust 指定为证书颁发机构。  

有关 NDES 如何支持策略模块以便 Configuration Manager 可以部署证书的详细信息，请参阅[结合使用策略模块和网络设备注册服务](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn473016\(v=ws.11\))。

Configuration Manager 支持将证书部署到不同设备类型和操作系统上的不同证书存储，具体取决于要求。 支持下列设备和操作系统：  

- Windows 10

- Windows 10 移动版

- Windows 8.1  

- Windows Phone 8.1  

> [!NOTE]  
> 使用 Configuration Manager 本地 MDM 来管理 Windows Phone 8.1 和 Windows 10 移动版。 有关详细信息，请参阅[本地 MDM](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)。

Configuration Manager 的典型方案是，安装受信任的根 CA 证书，用于对 Wi-Fi 和 VPN 服务器进行身份验证。 典型连接使用以下协议：

- 身份验证协议：EAP-TLS、EAP-TTLS 和 PEAP
- VPN 隧道协议：IKEv2、L2TP/IPsec 和 Cisco IPsec

必须在设备上安装企业根 CA 证书，然后设备才能使用 SCEP 证书配置文件请求证书。  

可以在 SCEP 证书配置文件中指定设置，以便针对不同的环境或连接要求请求自定义证书。 “创建证书配置文件向导”有两个注册参数页面  。 首先，“SCEP 注册”包括有关注册请求以及在何处安装证书的设置  。 其次，“证书属性”  本身描述了请求的证书。  

## <a name="deploy"></a>部署

如果你部署 SCEP 证书配置文件，由 Configuration Manager 客户端处理策略。 然后，它从管理点请求获取 SCEP 质询密码。 设备创建公钥/私钥对，并生成证书签名请求 (CSR)。 它将此请求发送到 NDES 服务器。 NDES 服务器通过 NDES 策略模块将此请求转发给证书注册点站点系统。 证书注册点验证此请求，检查 SCEP 质询密码，并验证此请求是否没有被篡改。 然后，它批准或拒绝此请求。 如果获得批准，NDES 服务器将签名请求发送到连接的证书颁发机构 (CA) 进行签名。 CA 对此请求进行签名，然后将证书返回给发出请求的设备。

将证书配置文件部署到用户或设备集合。 可以为每个证书指定目标存储。 适用性规则确定设备能否安装证书。

将证书配置文件部署到用户集合时，[用户设备相关性](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)会确定在用户的哪台设备上安装证书。 如果你将包含用户证书的证书配置文件部署到设备集合，用户的所有主要设备都会默认安装证书。 可在“创建证书配置文件向导”的“SCEP 注册”页上更改此行为，以将证书安装在用户的任何设备上   。 如果设备位于工作组中，那么 Configuration Manager 就不会部署用户证书。  

## <a name="monitor"></a>监视

可通过查看符合性结果或报表来监视证书配置文件部署。 有关详细信息，请参阅[如何监视证书配置文件](monitor-certificate-profiles.md)。

## <a name="automatic-revocation"></a>自动吊销

Configuration Manager 在以下情况下会自动撤销使用证书配置文件部署的用户和计算机证书：  

- 设备已停用 Configuration Manager 管理。  

- 设备在 Configuration Manager 层次结构中受阻止。  

为了吊销证书，站点服务器会将吊销命令发送至证书颁发机构。 吊销原因是“停止操作”  。

> [!NOTE]
> 层次结构中首要网站的计算机帐户必须有权在 CA 中颁发和管理证书  ，才能正确吊销证书。
>
> 为了提高安全性，还可以在 CA 中限制 CA 管理员。 然后，只向此帐户授予对特定证书模板的权限，此模板用于站点上的 SCEP 配置文件。

## <a name="next-steps"></a>后续步骤

- [创建证书配置文件](create-certificate-profiles.md)

- [配置证书基础结构](certificate-infrastructure.md)