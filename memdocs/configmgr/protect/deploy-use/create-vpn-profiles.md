---
title: 如何创建 VPN 配置文件
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中创建 VPN 配置文件。
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f338e4db-73b5-45ff-92f4-1b89a8ded989
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 17811d0bb0b72ebee6879d5dab90e165b439081b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694245"
---
# <a name="how-to-create-vpn-profiles-in-configuration-manager"></a>如何在 Configuration Manager 中创建 VPN 配置文件

适用范围：  Configuration Manager (Current Branch)

Configuration Manager 支持多个 VPN 连接类型。 如需详细了解不同设备平台可用的连接类型，请参阅 [VPN 配置文件](vpn-profiles.md)。

对于第三方 VPN 连接，请在部署 VPN 配置文件之前分发 VPN 应用。 如果不部署应用，则将在用户尝试连接到 VPN 时提示他们部署应用。 有关详细信息，请参阅[部署应用程序](../../apps/deploy-use/deploy-applications.md)。

## <a name="create-a-vpn-profile"></a>创建 VPN 配置文件

1. 在 Configuration Manager 控制台中，转到“资产和符合性”工作区中，依次展开“符合性设置”和“公司资源访问”，然后选择“VPN 配置文件”节点     。

1. 在功能区的“主页”选项卡上的“创建”组中，选择“创建 VPN 包”    。

1. 在“创建 VPN 配置文件向导”的“常规”页上，指定下列信息  ：

    - **名称**：输入唯一的名称以便在控制台中标识 VPN 配置文件。

        > [!NOTE]
        > 请勿在 VPN 配置文件名称中使用以下字符：`\/:*?<>|; `。 Windows VPN 配置文件不支持这些特殊字符。

    - **描述**：（可选）输入描述以提供有关 VPN 配置文件的详细信息。

    - **VPN 配置文件类型**：选择适当的平台。

        如果选择 Windows 8.1 平台，则还可以从文件中导入   。 此操作可从 XML 文件中导入 VPN 配置文件信息。 如果选择此选项，该向导的其余部分将简化为以下页面：“支持的平台”和“导入 VPN 配置文件”   。

1. 在“支持的平台”页上，选择此 VPN 配置文件支持的 OS 版本  。

1. 在“连接”页上，指定下列信息  ：

    - **连接类型**：选择 VPN 连接类型。 有关受支持类型的详细信息，请参阅 [VPN 配置文件](vpn-profiles.md)。

    - **服务器列表**：添加用于 VPN 连接的新服务器。 根据连接类型，可以添加一个或多个 VPN 服务器，并指定默认服务器。

    - **连接到公司网络时不使用 VPN**：将客户端配置为当其在你的内部网络上时不使用 VPN。 如有必要，请指定特定于连接的 DNS 名称。

1. 在向导的“身份验证方法”页上，选择连接类型支持的方法  。 此页上的设置和可用选项因所选连接类型而异。 有关详细信息，请参阅[身份验证方法引用](#bkmk_auth)。

1. 在“代理设置”页上，如果 VPN 使用的是代理服务器，请选择适合环境的选项之一  。 然后提供代理的配置信息。

1. “应用程序”页仅适用于 Windows 10 配置文件  。 添加自动连接到此 VPN 的桌面应用和通用应用。 应用的类型决定应用标识符：

    - 对于桌面应用，请提供应用的文件路径  。

    - 对于通用的应用，请提供包系列名称 (PFN)  。 若要了解如何查找应用的 PFN，请参阅[查找每个应用 VPN 的包系列名称](find-a-pfn-for-per-app-vpn.md)。

    你还可以配置一个选项，以便仅列出的应用可以使用此 VPN  。

    > [!IMPORTANT]
    > 保护为配置每应用 VPN 而编译的关联应用的所有列表。 如果未经授权的用户更改你的列表，且你将此表导入每应用 VPN 应用列表中，则可能向不应拥有访问权限的应用授予 VPN 访问权限。

1. “边界”页仅适用于 Windows 10 配置文件，用于配置 VPN 边界  。 可以添加以下选项：

    - **网络流量规则**：设置针对 VPN 连接要启用的协议、本地端口、远程端口和地址范围。  

        > [!Note]
        > 如果未创建网络流量规则，则会启用所有协议、端口和地址范围。 创建流量规则后，VPN 连接只会使用此规则或其他规则中指定的协议、端口和地址范围。

    - **DNS 名称和服务器**：设备建立连接后，VPN 连接使用的 DNS 服务器。

    - **路由**：使用 VPN 连接的网络路由。 创建超过 60 个路由可能会导致策略失败。

1. 完成向导。

新的 VPN 配置文件将显示在“资产和符合性”  工作区的“VPN 配置文件”  节点中。

## <a name="authentication-method-reference"></a><a name="bkmk_auth"></a> 身份验证方法参考

可用的 VPN 身份验证方法视连接类型而定：

### <a name="certificates"></a>证书

如果客户端证书对 RADIUS 服务器（如网络策略服务器）进行身份验证，请将证书中的使用者可选名称设置为用户主体名称。

支持的连接类型：

- 脉冲安全
- F5 Edge Client
- Dell SonicWALL Mobile Connect
- Check Point Mobile VPN

### <a name="username-and-password"></a>用户名和密码

支持的连接类型：

- 脉冲安全
- F5 Edge Client
- Dell SonicWALL Mobile Connect
- Check Point Mobile VPN

### <a name="microsoft-eap-ttls"></a>Microsoft EAP-TTLS

支持的连接类型：

- Microsoft SSL (SSTP)
- Microsoft Automatic
- PPTP
- IKEv2
- L2TP

### <a name="microsoft-protected-eap-peap"></a>Microsoft 受保护的 EAP (PEAP)

支持的连接类型：

- Microsoft SSL (SSTP)
- Microsoft Automatic
- IKEv2
- PPTP
- L2TP

### <a name="microsoft-secured-password-eap-mschap-v2"></a>Microsoft 受保护的密码 (EAP-MSCHAP v2)

支持的连接类型：

- Microsoft SSL (SSTP)
- Microsoft Automatic
- IKEv2
- PPTP
- L2TP

### <a name="smart-card-or-other-certificate"></a>智能卡或其他证书

支持的连接类型：

- Microsoft SSL (SSTP)
- Microsoft Automatic
- IKEv2
- PPTP
- L2TP

### <a name="mschap-v2"></a>MSCHAP v2

支持的连接类型：

- Microsoft SSL (SSTP)
- Microsoft Automatic
- IKEv2
- PPTP
- L2TP

### <a name="use-machine-certificates"></a>使用计算机证书

支持的连接类型：

- IKEv2

### <a name="additional-authentication-options"></a>附加身份验证选项

当 Windows 客户端版本支持时，“配置”身份验证方法的选项可用  。 此选项将打开 Windows 属性窗口以配置身份验证方法。

可能需要指定更多信息，具体视选择的选项而定，例如：

- **每次登录时记住用户凭据**：记住用户凭据，这样用户就不必在每次连接时都输入凭据。  

- **选择用于客户端身份验证的客户端证书**：选择之前创建的客户端 SCEP 证书配置文件，对 VPN 连接进行身份验证。 有关详细信息，请参阅[创建 PFX 证书配置文件](create-certificate-profiles.md)。

## <a name="next-steps"></a>后续步骤

- 对于第三方 VPN 连接，请在部署 VPN 配置文件之前分发 VPN 应用。 如果不部署应用，则将在用户尝试连接到 VPN 时提示他们部署应用。 有关详细信息，请参阅[部署应用程序](../../apps/deploy-use/deploy-applications.md)。

- 部署 VPN 配置文件。 有关详细信息，请参阅[如何部署配置文件](deploy-wifi-vpn-email-cert-profiles.md)。
