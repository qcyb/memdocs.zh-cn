---
title: 站点管理的安全和隐私
titleSuffix: Configuration Manager
description: 优化 Configuration Manager 中的站点管理的安全和隐私
ms.date: 04/27/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1d58176e-abc0-4087-8583-ce70deb4dcf5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 923018e35fae1ec1f5e9c0869ef22d43b5de552b
ms.sourcegitcommit: 53bab52e42de28b87e53596646a3532e25eb9c14
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2020
ms.locfileid: "82182253"
---
# <a name="security-and-privacy-for-site-administration-in-configuration-manager"></a>Configuration Manager 中的站点管理的安全和隐私

适用范围：  Configuration Manager (Current Branch)

本文包含有关 Configuration Manager 站点和层次结构的安全和隐私信息。

## <a name="security-guidance-for-site-administration"></a><a name="BKMK_Security_Sites"></a> 站点管理的安全指南

使用以下指南，帮助保护 Configuration Manager 站点和层次结构的安全。  

### <a name="run-setup-from-a-trusted-source-and-secure-communication"></a>从受信任源中运行安装程序并保护通信安全

为帮助防止某人篡改源文件，请从受信任源中运行 Configuration Manager 安装程序。 如果将文件存储在网络上，请保护网络位置的安全。  

如果你确实要从网络位置中运行安装程序，那么，为了在通过网络传输文件时防止攻击者篡改文件，请在安装程序文件的源位置和站点服务器之间使用 IPsec 或 SMB 签名。  

如果使用安装程序下载程序来下载安装程序所需的文件，请确保保护存储这些文件的位置的安全。 同时在运行安装程序时保护此位置的信道的安全。  

### <a name="extend-the-active-directory-schema-and-publish-sites-to-the-domain"></a>扩展 Active Directory 架构并将站点发布到域  

架构扩展不是运行 Configuration Manager 所必需的，但它们确实可创建更安全的环境。 客户端和站点服务器可以从受信任源中检索信息。  

如果客户端位于不受信任域中，请在客户端的域中部署下列站点系统角色：  

- 管理点  

- 分发点  

> [!NOTE]  
> Configuration Manager 的受信任域需要 Kerberos 身份验证。 如果客户端所在的林与站点服务器的林没有双向林信任，则会将这些客户端视为不受信任的域。 外部信任不足以实现此目的。  

### <a name="use-ipsec-to-secure-communications"></a>使用 IPsec 保护通信安全

尽管 Configuration Manager 确实会保护站点服务器和运行 SQL Server 的计算机之间的通信安全，但不会保护站点系统角色和 SQL Server 之间的通信安全。 只能使用 HTTPS 配置某些站点系统进行站点内通信。  

如果不使用其他控制来保护这些服务器到服务器通道的安全，攻击者将能对站点系统发起各种欺骗和中间人攻击。 在无法使用 IPsec 时使用 SMB 签名。  

> [!Important]  
> 保护站点服务器和包源服务器之间的信道的安全。 此通信使用 SMB。 如果无法使用 IPsec 来保护此通信的安全，请使用 SMB 签名来确保在客户端下载并运行文件之前文件未被篡改。  

### <a name="dont-change-the-default-security-groups"></a>不要更改默认安全组

不要更改 Configuration Manager 为站点系统通信创建和管理的以下安全组：

- **SMS_SiteSystemToSiteServerConnection_MP_&lt;SiteCode\>**  

- **SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;SiteCode\>**  

- **SMS_SiteSystemToSiteServerConnection_Stat_&lt;SiteCode\>**  

Configuration Manager 自动创建和管理这些安全组。 此行为包括在删除站点系统角色时删除计算机帐户。  

为了确保服务连续性和最小特权，请不要手动编辑这些组。  

### <a name="manage-the-trusted-root-key-provisioning-process"></a>管理受信任的根密钥预配过程

如果客户端无法查询全局编录来查找 Configuration Manager 信息，则它们必须依赖于受信任的根密钥来验证有效的管理点。 受信任的根密钥存储在客户端注册表中。 它可以通过使用组策略或手动配置进行设置。  

如果客户端在首次联系管理点时没有受信任的根密钥的副本，它将信任与之通信的第一个管理点。 为了降低攻击者将客户端错误定向到未授权管理点的风险，你可以使用受信任的根密钥来预先设置客户端。 有关详细信息，请参阅[规划受信任的根密钥](../security/plan-for-security.md#BKMK_PlanningForRTK)。  

### <a name="use-non-default-port-numbers"></a>使用非默认端口号

使用非默认端口号可以提供额外的安全性。 这样会使攻击者更难于探索准备攻击的环境。 如果决定使用非默认端口，请在安装 Configuration Manager 之前规划这些端口。 在层次结构中的所有站点上一致地使用它们。 例如，可在客户端请求端口和 LAN 唤醒中使用非默认端口号。  

### <a name="use-role-separation-on-site-systems"></a>在站点系统上使用角色分隔

尽管你可以在单一计算机上安装所有站点系统角色，但这种做法在生产网络上很少用。 原因是它会创建单一故障点。  

### <a name="reduce-the-attack-profile"></a>减小攻击面

通过将每个站点系统角色隔离在不同服务器上，可降低利用单个站点系统中的漏洞攻击不同站点系统的几率。 许多角色都需要在站点系统上安装 Internet Information Services (IIS)，而这会增大攻击面。 如果必须合并角色以减少硬件支出，请将 IIS 角色仅与需要 IIS 的其他角色合并。  

> [!IMPORTANT]  
> 回退状态点角色是一个例外。 由于此站点系统角色接受未经身份验证的客户端数据，因此不要将回退状态点角色分配给任何其他 Configuration Manager 站点系统角色。  

### <a name="configure-static-ip-addresses-for-site-systems"></a>为站点系统配置静态 IP 地址

静态 IP 地址可以更轻松地抵御名称解析攻击。  

静态 IP 地址也可简化 IPsec 的配置。 保护 Configuration Manager 中站点系统间通信安全的最佳安全做法是使用 IPsec。  

### <a name="dont-install-other-applications-on-site-system-servers"></a>不要在站点系统服务器上安装其他应用程序

如果在站点系统服务器上安装其他应用程序，将会增大 Configuration Manager 的攻击面。 还会增加出现不兼容性问题的风险。  

### <a name="require-signing-and-enable-encryption-as-a-site-option"></a>要求签名并启用加密作为站点选项

为站点启用签名和加密选项。 确保所有客户端均可支持 SHA-256 哈希算法，然后启用“需要 SHA-256”  选项。  

### <a name="restrict-and-monitor-administrative-users"></a>限制和监视管理用户

仅向你信任的用户授予 Configuration Manager 的管理访问权限。 然后通过使用内置安全角色或通过自定义安全角色来向他们授予最低权限。 如果管理用户可创建、修改并部署软件和配置，则他们可能会潜在地控制 Configuration Manager 层次结构中的设备。  

定期审核管理用户分配及其授权级别以验证所需的更改。  

有关详细信息，请参阅[配置基于角色的管理](../../servers/deploy/configure/configure-role-based-administration.md)。  

### <a name="secure-configuration-manager-backups"></a>保护 Configuration Manager 备份的安全

备份 Configuration Manager 时，此信息包括攻击者可用于假冒的证书和其他敏感数据。  

在通过网络传输此数据时使用 SMB 签名或 IPsec，并保护备份位置的安全。  

### <a name="secure-locations-for-exported-objects"></a>保护导出对象位置的安全

每当将对象从 Configuration Manager 控制台导入或导出到网络位置时，请保护该位置和网络通道的安全。

限制可访问网络文件夹的人员。  

若要防止攻击者篡改导出的数据，请在网络位置和站点服务器之间使用 SMB 签名或 IPsec。 同时保护运行 Configuration Manager 控制台和站点服务器的计算机之间的通信的安全。 使用 IPsec 对网络上的数据进行加密以防止信息泄漏。  

### <a name="manually-remove-certificates-from-failed-servers"></a>从故障服务器中手动删除证书

如果站点系统未正确卸载或者停止正常工作且无法还原，请从其他 Configuration Manager 服务器中手动删除此服务器的 Configuration Manager 证书。

若要删除最初使用站点系统和站点系统角色建立的对等信任，则手动删除适用于其他站点系统服务器上“受信任人”  证书存储中的故障服务器的 Configuration Manager 证书。 如果重用服务器而不对其进行重新格式化，则此操作非常重要。  

有关详细信息，请参阅[服务器通信的加密控制](../security/cryptographic-controls-technical-reference.md#cryptographic-controls-for-server-communication)。  

### <a name="dont-configure-internet-based-site-systems-to-bridge-the-perimeter-network"></a>不要配置基于 Internet 的站点系统来桥接外围网络

不要将站点系统服务器配置为多宿主，防止它们连接到外围网络和 Intranet。 尽管这种配置允许基于 Internet 的站点系统接受来自 Internet 和 Intranet 的客户端连接，但它会消除外围网络和 Intranet 之间的安全边界。  

### <a name="configure-the-site-server-to-initiate-connections-to-perimeter-networks"></a>配置站点服务器以启动到外围网络的连接

如果站点系统位于不受信任网络（例如外围网络）上，请配置站点服务器以启动到站点系统的连接。

默认情况下，站点系统会启动到站点服务器的连接，以传输数据。 当启动从不受信任的网络到受信任的网络的连接时，此配置可能有安全风险。 当站点系统接受来自 Internet 的连接或位于不受信任的林中时，请将站点系统选项配置为“要求站点服务器启动到此站点系统的连接”  。 安装站点系统和任何角色之后，所有连接都由站点服务器从受信任的网络启动。  

### <a name="use-ssl-bridging-and-termination-with-authentication"></a>使用 SSL 桥接和终止操作并进行身份验证

如果为基于 Internet 的客户端管理使用 Web 代理服务器，请通过使用终止操作并进行身份验证来使用到 SSL 的 SSL 桥接。

如果在代理 Web 服务器上配置 SSL 终止，则在将来自 Internet 的数据包转发到内部网络之前，会对该数据进行检测。 代理 Web 服务器将对来自客户端的连接进行验证，将其终止，然后建立一个新的经身份验证的连接，连接到基于 Internet 的站点系统。  

Configuration Manager 客户端计算机使用代理 Web 服务器连接到基于 Internet 的站点系统时，客户端标识 (GUID) 将安全地包含在数据包负载中。 管理点就不会将代理 Web 服务器视为客户端。

如果代理 Web 服务器无法支持 SSL 桥接的要求，则也支持 SSL 隧道。 此选项的安全级别较低。 在不终止的情况下将来自 Internet 的 SSL 数据包转发到站点系统。 这样无法检测它们是否包含恶意内容。  

> [!WARNING]  
> 通过 Configuration Manager 注册的移动设备无法使用 SSL 桥接。 它们必须仅使用 SSL 隧道。  

### <a name="configurations-to-use-if-you-configure-the-site-to-wake-up-computers-to-install-software"></a>将站点配置为唤醒计算机以安装软件时所要使用的配置

- 如果使用传统的唤醒数据包，请使用单播，而不是子网导向型广播。  

- 如果必须使用子网导向型广播，请配置路由器，仅允许来自站点服务器且位于非默认端口号上的 IP 导向型广播。  

若要深入了解不同的 LAN 唤醒技术，请参阅[规划如何唤醒客户端](../../clients/deploy/plan/plan-wake-up-clients.md)。

### <a name="if-you-use-email-notification-configure-authenticated-access-to-the-smtp-mail-server"></a>如果使用电子邮件通知，请配置对 SMTP 邮件服务器的身份验证访问权限

尽可能使用支持身份验证访问权限的邮件服务器。 使用站点服务器的计算机帐户进行身份验证。 如果必须指定用于身份验证的用户帐户，请使用具有最低权限的帐户。 

### <a name="enforce-ldap-channel-binding-and-ldap-signing"></a>强制执行 LDAP 通道绑定和 LDAP 签名

可配置服务器，使其拒绝不要求进行签名的简单身份验证和安全层 (SASL) LDAP 绑定，或者拒绝在明文连接上执行的 LDAP 简单绑定，从而提高 Active Directory 域控制器的安全性。 自版本 1910 起，Configuration Manager 支持强制执行 LDAP 通道绑定和 LDAP 签名。 有关详细信息，请参阅 [2020 年针对 Windows 的 LDAP 通道绑定和 LDAP 签名要求](https://support.microsoft.com/help/4520412/2020-ldap-channel-binding-and-ldap-signing-requirements-for-windows)。 <!--6244453-->


## <a name="security-guidance-for-the-site-server"></a><a name="BKMK_Security_SiteServer"></a> 站点服务器的安全指南

使用以下指南，帮助保护 Configuration Manager 站点服务器的安全。  

### <a name="install-configuration-manager-on-a-member-server-instead-of-a-domain-controller"></a>在成员服务器而不是域控制器上安装 Configuration Manager

Configuration Manager 站点服务器和站点系统不需要安装在域控制器上。 域控制器没有除域服务器之外的本地安全帐户管理 (SAM) 数据库。 在成员服务器上安装 Configuration Manager 时，可在本地 SAM 数据库而不是域数据库中维护 Configuration Manager 帐户。  

这种做法还减小了域控制器的攻击面。  

### <a name="install-secondary-sites-without-copying-the-files-over-the-network"></a>安装辅助站点，而不通过网络复制文件

运行安装程序以及创建辅助站点时，请不要选择用于将文件从父站点复制到辅助站点的选项。 也不要使用网络源位置。 通过网络复制文件时，熟练的攻击者可能会劫持辅助站点安装包，并在安装文件之前篡改文件。 确定攻击时间并不容易。 通过在传输文件时使用 IPsec 或 SMB，可以减轻此攻击。  

在辅助站点服务器上，请将源文件从媒体文件夹复制到本地文件夹，而不是通过网络复制文件。 然后，运行安装程序创建辅助站点时，请在“安装源文件”  页选择“使用辅助站点计算机上以下位置中的源文件(最安全)”  ，并指定此文件夹。  

有关详细信息，请参阅[安装辅助站点](../../servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_secondary)。

### <a name="site-role-installation-inherits-permissions-from-drive-root"></a>站点角色安装从驱动器根目录继承权限

<!-- SCCMDocs#1380 -->
确保在将第一个站点系统角色安装到任何服务器之前正确配置系统驱动器权限。 例如，`C:\SMS_CCM` 从 `C:\` 继承权限。 如果未正确保护驱动器根目录的安全，则低权限用户可能能够访问或修改 Configuration Manager 文件夹中的内容。


## <a name="security-guidance-for-sql-server"></a><a name="BKMK_Security_SQLServer"></a> SQL Server 的安全指南

Configuration Manager 使用 SQL Server 作为后端数据库。 如果数据库遭到泄露，攻击者可以绕过 Configuration Manager。 如果他们直接访问 SQL Server，则可以通过 Configuration Manager 启动攻击。 请将对 SQL Server 的攻击视为高风险并进行相应缓解。  

使用以下安全指南，帮助保护 Configuration Manager SQL Server 的安全。  

### <a name="dont-use-the-configuration-manager-site-database-server-to-run-other-sql-server-applications"></a>不要使用 Configuration Manager 站点数据库服务器来运行其他 SQL Server 应用程序

提高对 Configuration Manager 站点数据库服务器的访问权限时，此操作会增加 Configuration Manager 数据的风险。 如果 Configuration Manager 站点数据库遭到泄露，还会危及同一 SQL Server 计算机上的其他应用程序。  

### <a name="configure-sql-server-to-use-windows-authentication"></a>将 SQL Server 配置为使用 Windows 身份验证

虽然 Configuration Manager 使用 Windows 帐户和 Windows 身份验证来访问站点数据库，但仍然可以将 SQL Server 配置为使用 SQL Server 混合模式。 SQL Server 混合模式允许其他 SQL 登录访问数据库。 此配置不是必需的，会增大受攻击面。  

### <a name="update-sql-server-express-at-secondary-sites"></a>更新辅助站点上的 SQL Server Express

安装主站点时，Configuration Manager 从 Microsoft 下载中心下载 SQL Server Express。 然后将文件复制到主站点服务器。 安装辅助站点并选择安装 SQL Server Express 的选项时，Configuration Manager 会安装以前下载的版本。 不会检查是否有新版本可用。 为确保辅助站点具有最新版本，请执行以下任务之一：  

- 安装辅助站点之后，请在辅助站点服务器上运行 Windows 更新。  

- 安装辅助站点之前，请在辅助站点服务器上手动安装 SQL Server Express。 确保安装最新版本和任何软件更新。 然后安装辅助站点，并选择选项以使用现有 SQL Server 实例。  

定期运行所有已安装的 SQL Server 版本的 Windows 更新。 这种做法可确保它们具有最新的软件更新。  

### <a name="follow-general-guidance-for-sql-server"></a>遵循 SQL Server 的通用指南

确定并遵循 SQL Server 版本的通用指南。 但是，请考虑 Configuration Manager 的以下要求：  

- 站点服务器的计算机帐户必须是运行 SQL Server 的计算机上“管理员”组的成员。 如果遵循 SQL Server 的“显式预配管理员主体”建议，则在站点服务器上运行安装程序时所用的帐户必须隶属于 SQL 用户组。  

- 如果使用域用户帐户安装 SQL Server，请确保针对发布到 Active Directory 域服务的服务主体名称 (SPN) 配置站点服务器计算机帐户。 如果没有 SPN，Kerberos 身份验证和 Configuration Manager 安装程序都将失败。  


## <a name="security-guidance-for-site-systems-that-run-iis"></a><a name="BKMK_Security_IIS"></a> 运行 IIS 的站点系统的安全指南

Configuration Manager 中的一些站点系统角色需要 IIS。 通过保护 IIS 安全的过程，Configuration Manager 可正确运行并减小安全攻击的风险。 若可行，请将需要 IIS 的服务器的数量降至最低。 例如，请仅运行支持客户端群所需数目的管理点，并针对基于 Internet 的客户端管理考虑高可用性和网络隔离。  

使用以下指南，帮助保护运行 IIS 的站点系统的安全。  

### <a name="disable-iis-functions-that-you-dont-require"></a>禁用不必要的 IIS 功能

仅针对你安装的站点系统角色安装最少的 IIS 功能。 有关详细信息，请参阅[站点和站点系统先决条件](../configs/site-and-site-system-prerequisites.md)。  

### <a name="configure-the-site-system-roles-to-require-https"></a>配置需要 HTTPS 的站点系统角色

当客户端使用 HTTP 而不是使用 HTTPS 连接到站点系统时，它们使用 Windows 身份验证。 此行为可能会回退到使用 NTLM 身份验证而不是 Kerberos 身份验证。 当使用 NTLM 身份验证时，客户端可能会连接到恶意服务器。  

本指南的例外情况可能是分发点。 配置用于 HTTPS 的分发点时，包访问帐户不起作用。 包访问帐户为内容提供授权，以便你可以限制能够访问内容的用户。 有关详细信息，请参阅[内容管理的最佳安全做法](security-and-privacy-for-content-management.md#BKMK_Security_ContentManagement)。  

### <a name="configure-a-certificate-trust-list-ctl-in-iis-for-site-system-roles"></a>在 IIS 中为站点系统角色配置证书信任列表 (CTL)

站点系统角色：  

- 配置用于 HTTPS 的分发点  

- 配置用于 HTTPS 且启用以支持移动设备的管理点

CTL 是受信任的根证书颁发机构 (CA) 的定义列表。 将 CTL 与组策略和公钥基础结构 (PKI) 部署一起使用时， CTL 允许你补充在网络上配置的受信任的现有根 CA。 例如，使用 Microsoft Windows 自动安装或通过 Windows 企业根 CA 添加的 CA。 在 IIS 中配置 CTL 时，它会定义受信任的根 CA 的子集。  

该子集可让你更好地控制安全性。 CTL 将接受的客户端证书限制为仅从 CTL 中的 CA 列表颁发的证书。 例如，Windows 附带了许多已知的第三方 CA 证书，如 VeriSign 和 Thawte。

默认情况下，运行 IIS 的计算机信任链接到这些已知 CA 的证书。 如果没有为所列出的站点系统角色配置 IIS 和 CTL，则站点会接受具有从这些 CA 中颁发的证书的任何设备作为有效的客户端。 如果为 IIS 配置的 CTL 不包含这些 CA，而证书链接到这些 CA，则站点会拒绝客户端连接。 为使列出的站点系统角色接受 Configuration Manager 客户端，必须与指定 Configuration Manager 客户端使用的 CA 的 CTL 一起配置 IIS。  

> [!NOTE]  
> 只要列出的站点系统角色要求在 IIS 中配置 CTL。 在客户端计算机连接到 HTTPS 管理点时，Configuration Manager 用于管理点的证书颁发者列表为这些计算机提供了相同的功能。  

有关如何在 IIS 中配置受信任的 CA 列表的详细信息，请参阅 IIS 文档。  

### <a name="dont-put-the-site-server-on-a-computer-with-iis"></a>不要将站点服务器放在带有 IIS 的计算机上

角色分离有助于减小攻击配置文件以及提高可恢复性。 站点服务器的计算机帐户通常具有所有站点系统角色的管理权限。 如果使用客户端请求安装，则可能还具有 Configuration Manager 客户端的这些权限。  

### <a name="use-dedicated-iis-servers-for-configuration-manager"></a>对 Configuration Manager 使用专用 IIS 服务器

虽然可以在 Configuration Manager 也使用的 IIS 服务器上托管多个基于 Web 的应用程序，但此做法可能会大大增加攻击面。 配置不良的应用程序可能允许攻击者获取 Configuration Manager 站点系统的控制权。 此漏洞可能允许攻击者获取层次结构的控制权。  

如果必须在 Configuration Manager 站点系统上运行其他基于 Web 的应用程序，请为 Configuration Manager 站点系统创建自定义的网站。  

### <a name="use-a-custom-website"></a>使用自定义网站

对于运行 IIS 的站点系统，将 Configuration Manager 配置为使用自定义网站，而不使用默认网站。 如果必须在站点系统上运行其他 Web 应用程序，请使用自定义网站。 此设置是站点范围设置，而不是特定站点系统的设置。  

### <a name="when-you-use-custom-websites-remove-the-default-virtual-directories"></a>使用自定义网站时，删除默认虚拟目录

从使用默认网站更改为使用自定义网站时，Configuration Manager 不会删除旧虚拟目录。 删除 Configuration Manager 最初在默认网站下创建的虚拟目录。  

例如，删除分发点的以下虚拟目录：  

- SMS_DP_SMSPKG$  

- SMS_DP_SMSSIG$  

- NOCERT_SMS_DP_SMSPKG$  

- NOCERT_SMS_DP_SMSSIG$  

### <a name="follow-iis-server-security-guidance"></a>遵循 IIS 服务器安全指南

确定并遵循 IIS 服务器版本的通用指南。 考虑 Configuration Manager 对特定站点系统角色的任何要求。 有关详细信息，请参阅[站点和站点系统先决条件](../configs/site-and-site-system-prerequisites.md)。  


## <a name="security-guidance-for-the-management-point"></a><a name="BKMK_Security_ManagementPoint"></a> 管理点的安全指南

管理点是设备与 Configuration Manager 之间的主要接口。 请将对管理点以及运行它的服务器的攻击视为高风险并进行相应缓解。 应用所有适当的安全指南并监视异常活动。  

使用以下指南，帮助保护 Configuration Manager 中管理点的安全。  

### <a name="assign-the-client-on-a-management-point-to-the-same-site"></a>将管理点上的客户端分配给同一站点

请避免出现以下情况：将管理点上的 Configuration Manager 客户端分配给该管理点站点之外的其他站点。  

如果从早期版本迁移到 Configuration Manager 当前分支，需尽快将管理点上的客户端迁移到新站点。  


## <a name="security-guidance-for-the-fallback-status-point"></a><a name="BKMK_Security_FSP"></a> 回退状态点的安全指南

如果在 Configuration Manager 中安装回退状态点，请使用以下安全指南：

若要深入了解安装回退状态点时的安全注意事项，请参阅[确定是否需要回退状态点](../../clients/deploy/plan/determine-the-site-system-roles-for-clients.md#fallback-status-point)。  

### <a name="dont-run-any-other-roles-on-the-same-site-system"></a>不要在同一站点系统上运行任何其他角色

回退状态点设计为接受来自任何计算机的未经身份验证的通信。 如果使用其他角色或域控制器运行此站点系统角色，则会大大增加该服务器的风险。  

### <a name="install-the-fallback-status-point-before-you-install-clients-with-pki-certificates"></a>在安装具有 PKI 证书的客户端之前安装回退状态点

如果 Configuration Manager 站点系统不接受 HTTP 客户端通信，则由于与 PKI 相关的证书问题的缘故，你可能不知道客户端不受管理。 如果将客户端分配给回退状态点，则该状态点将报告这些证书问题。  

出于安全原因，无法在安装客户端后向其分配回退状态点。 只能在客户端安装期间分配此角色。  

### <a name="avoid-using-the-fallback-status-point-in-the-perimeter-network"></a>避免在外围网络中使用回退状态点

回退状态点设计为可以接受来自任何客户端的数据。 虽然外围网络中的回退状态点可以帮助你解决基于 Internet 的客户端的问题，但必须在下列两者之间取得平衡：解决问题的好处，以及在可公开访问的网络中接受未经身份验证的数据的站点系统所面临的风险。  

如果在外围网络或任何不受信任的网络中安装回退状态点，请配置站点服务器以启动数据传输。 不要使用允许回退状态点的默认设置启动到站点服务器的连接。  


## <a name="security-issues-for-site-administration"></a><a name="BKMK_SecurityIssues_Clients"></a>站点管理的安全问题

查看以下有关 Configuration Manager 的安全问题：  

- Configuration Manager 不会防范使用 Configuration Manager 来攻击网络的获授权的管理用户。 未经授权的管理用户是一个高安全风险因素。 他们可能会启动许多攻击，其中包括以下策略：  

    - 使用软件部署，在组织中的每台 Configuration Manager 客户端计算机上自动安装和运行恶意软件。  

    - 在无客户端权限的情况下远程控制 Configuration Manager 客户端。  

    - 配置快速轮询间隔和极端数量的库存。 此操会对客户端和服务器创建拒绝服务攻击。  

    - 使用层次结构中的一个站点将数据写入到另一个站点的 Active Directory 数据中。  

    站点层次结构是安全边界。 站点仅被视为管理边界。  

    审核管理用户的所有活动，并定期查看审核日志。 录用前，要求所有 Configuration Manager 管理用户接受背景调查。 要求定期复查（列为录用条件）。  

- 如果注册点遭到泄露，攻击者可能会获得身份验证证书。 他们可能会窃取注册了移动设备的用户的凭据。  

    注册点与 CA 通信。 它可创建、修改和删除 Active Directory 对象。 切勿在外围网络中安装注册点。 始终监视异常活动。  

- 如果你允许基于 Internet 的客户端管理的用户策略，则会增大攻击面。  

    除了使用 PKI 证书进行客户端到服务器的连接之外，这些配置还需要 Windows 身份验证。 而这可能会回退到使用 NTLM 身份验证而不是 Kerberos。 NTLM 身份验证容易受到假冒和重播攻击。 为了成功对 Internet 上的用户进行身份验证，必须允许从基于 Internet 的站点系统到域控制器的连接。  

- 站点系统服务器上需要 Admin$  共享。  

    Configuration Manager 站点服务器使用 Admin$ 共享来连接到站点系统，以及在其上执行服务操作。 不要禁用或删除此共享。  

- Configuration Manager 使用名称解析服务连接到其他计算机。 这些服务难以抵御以下安全攻击：
    - 欺骗
    - 篡改
    - 否认
    - 信息泄露
    - 拒绝服务
    - 特权提升

    确定并遵循用于名称解析的 DNS 版本的任何安全指南。  

## <a name="privacy-information-for-discovery"></a><a name="BKMK_Privacy_Cliients"></a> 有关发现的隐私信息

发现会创建网络资源的记录，并将它们存储在 Configuration Manager 数据库中。 发现数据记录包含各种计算机信息，例如 IP 地址、OS 版本和计算机名称。 也可以配置 Active Directory 发现方法，以返回你的组织存储在 Active Directory 域服务中的任何信息。  

Configuration Manager 在默认情况下启用的唯一发现方法是检测信号发现。 此方法仅发现已安装 Configuration Manager 客户端软件的计算机。  

不会将发现信息直接发送给 Microsoft。 而是存储在 Configuration Manager 数据库中。 Configuration Manager 将信息保留在数据库中，直到它删除数据。 站点维护任务“删除过期的发现数据”  每 90 天执行一次此过程。  
