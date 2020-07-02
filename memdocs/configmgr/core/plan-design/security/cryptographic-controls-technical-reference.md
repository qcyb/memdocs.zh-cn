---
title: 加密控制技术参考
titleSuffix: Configuration Manager
description: 了解在 Configuration Manager 中签名和加密如何帮助防范来自数据读取的攻击。
ms.date: 12/08/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fe50aad3cb35ab5908f604560f4dcd22800919a5
ms.sourcegitcommit: 22e1095a41213372c52d85c58b18cbabaf2300ac
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2020
ms.locfileid: "85353439"
---
# <a name="cryptographic-controls-technical-reference"></a>加密控制技术参考

适用范围：Configuration Manager (Current Branch)

Configuration Manager 使用签名和加密帮助保护 Configuration Manager 层次结构中的设备的管理。 借助签名，如果数据在传输过程中发生更改，则会放弃它。 加密可帮助阻止攻击者使用网络协议分析器读取数据。  

 Configuration Manager 用于签名的主要哈希算法是 SHA-256。 当两个 Configuration Manager 站点相互通信时，它们使用 SHA-256 对其通信签名。 Configuration Manager 中实现的主要加密算法是 3DES。 这用于在 Configuration Manager 数据库中存储数据和客户端 HTTP 通信。 通过 HTTPS 使用客户端通信时，可以将私钥基础结构 (PKI) 配置为将 RSA 证书与 [PKI 证书要求](../network/pki-certificate-requirements.md)中记录的最大哈希算法和密钥长度一起使用。  

 对于基于 Windows 的操作系统的大多数加密操作来说，Configuration Manager 使用 Windows CryptoAPI 库 rsaenh.dll 中的 SHA-2、3DES 和 AES 以及 RSA 算法。  

> [!IMPORTANT]  
>  有关针对 SSL 漏洞所建议的更改的信息，请参阅[有关 SSL 漏洞](#about-ssl-vulnerabilities)。  

##  <a name="cryptographic-controls-for-configuration-manager-operations"></a>Configuration Manager 操作的加密控制  
 Configuration Manager 中的信息可以进行签名和加密，无论你是否将 PKI 证书用于 Configuration Manager。  

### <a name="policy-signing-and-encryption"></a>策略签名和加密  
 客户端策略分配由自签名站点服务器签名证书进行签名，以帮助阻止泄露的管理点发送已遭篡改的策略的安全风险。 这在使用基于 Internet 的客户端管理时十分重要，因为此环境需要暴露在 Internet 通信中的管理点。  

 策略包含敏感数据时，系统使用 3DES 加密策略。 包含敏感数据的策略仅发送到授权客户端。 系统不对没有敏感数据的策略进行加密。  

 当策略存储在客户端上时，将使用数据保护应用程序编程接口 (DPAPI) 对其进行加密。  

### <a name="policy-hashing"></a>策略哈希处理  
 当 Configuration Manager 客户端请求策略时，它们首先获取一个策略分配，以便它们知道哪些策略适用于它们，然后仅请求那些策略的正文。 每个策略分配均包含相应策略正文的已计算哈希。 客户端检索合适的策略正文，然后计算该正文上的哈希。 如果下载的策略正文上的哈希与策略分配中的哈希不匹配，则客户端会丢弃该策略正文。  

 策略的哈希算法是 SHA-1 和 SHA-256。  

### <a name="content-hashing"></a>内容哈希处理  

站点服务器上的分发管理器服务会对所有包的内容文件进行哈希处理。 策略提供程序包含软件分发策略中的哈希。 当 Configuration Manager 客户端下载内容时，客户端会在本地重新生成哈希，并将其与策略中提供的哈希进行比较。 如果哈希匹配，则未修改内容，并且客户端将安装内容。 如果修改了内容的一个字节，则哈希将不匹配，因此将不安装软件。 此检查有助于确保安装正确的软件，因为会使用策略对实际内容进行交叉检查。  

内容的默认哈希算法为 SHA-256。

并非所有设备都可以支持内容哈希处理。 例外包括：  

- 流式传输 APP-V 内容时的 Windows 客户端。  

- Windows Phone 客户端，不过这些客户端会验证受信任的来源签署的应用程序签名。  

- Windows RT 客户端，不过这些客户端会验证受信任的来源签署的应用程序签名，并且也使用包完整名称 (PFN) 验证。  

- 在不支持 SHA-256 的 Linux 和 UNIX 版本上运行的客户端。 有关详细信息，请参阅[规划将客户端部署到 Linux 和 UNIX 计算机](../../clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md)。  

### <a name="inventory-signing-and-encryption"></a>清单签名和加密  
 客户端发送给管理点的清单始终由设备签名，无论它们是通过 HTTP 还是 HTTPS 与管理点通信，均不例外。 如果它们使用 HTTP，则可以选择加密此数据，这是最佳安全方案。  

### <a name="state-migration-encryption"></a>状态迁移加密  
 存储在操作系统部署的状态迁移点上的数据始终由用户状态迁移工具 (USMT) 使用 3DES 进行加密。  

### <a name="encryption-for-multicast-packages-to-deploy-operating-systems"></a>用于部署操作系统的多播包加密  
 对于每个操作系统部署包，你可以在使用多播向计算机传输包时启用加密。 加密使用高级加密标准 (AES)。 如果启用加密，则不需要其他证书配置。 启用多播的分发点将自动生成对称密钥来加密包。 每个包都有不同的加密密钥。 系统使用标准 Windows API 将密钥存储在启用多播的分发点上。 当客户端连接到多播会话时，会通过通道进行密钥交换，通道使用 PKI 颁发的客户端身份验证证书（如果客户端使用 HTTPS）或自签名证书（如果客户端使用 HTTP）进行加密。 客户端仅在多播会话期间将密钥存储在内存中。  

### <a name="encryption-for-media-to-deploy-operating-systems"></a>用于部署操作系统的媒体加密  
 使用媒体部署操作系统以及指定密码来保护媒体时，系统使用高级加密标准 (AES) 以及 128 位密钥大小对环境变量进行加密。 系统不加密媒体上的其他数据，包括应用程序的包和内容。  

### <a name="encryption-for-content-that-is-hosted-on-cloud-based-distribution-points"></a>基于云的分发点上承载的内容的加密  
 从 System Center 2012 Configuration Manager SP1 开始，在使用基于云的分发点时，使用高级加密标准 (AES) 以及 256 位密钥大小对上载到这些分发点的内容进行加密。 每当对内容进行更新时，都会重新加密内容。 当客户端下载内容时，会通过 HTTPS 连接来加密和保护内容。  

### <a name="signing-in-software-updates"></a>在软件更新中签名  
 所有软件更新都必须由受信任的发布者进行签名以防止篡改。 在客户端计算机上，Windows 更新代理 (WUA) 会扫描目录中的更新，但如果它在本地计算机上受信任的发布者存储上无法找到数字证书，则将不安装更新。 如果使用自签名的证书（如 WSUS 发布者自签名的证书）来发布更新目录，则该证书也必须位于本地计算机上受信任的根证书颁发机构的证书存储中，以验证证书的有效性。 WUA 还检查是否在本地计算机上启用了“允许来自 Intranet Microsoft 更新服务位置中的签名内容组策略”  设置。 必须为 WUA 启用此策略设置，以扫描使用 Updates Publisher 创建和发布的更新。  

 如果在 System Center Updates Publisher 中发布软件更新，则在将软件更新发布到更新服务器时，数字证书会对软件更新签名。 你可以指定 PKI 证书或将 Updates Publisher 配置为生成自签名证书，以对软件更新进行签名。  

### <a name="signed-configuration-data-for-compliance-settings"></a>符合性设置的签名配置数据  
 导入配置数据时，Configuration Manager 会验证文件的数字签名。 如果未对文件进行签名，或者数字签名验证检查失败，则会通知并提示你是否继续导入。 只有在你肯定信任发布者以及文件的完整性时，才继续导入配置数据。  

### <a name="encryption-and-hashing-for-client-notification"></a>客户端通知的加密和哈希处理  
 如果使用客户端通知，则所有通信都使用服务器和客户端操作系统可以协商的 TLS 和最高加密。 例如，运行 Windows 7 的客户端计算机和运行 Windows Server 2008 R2 的管理点可以支持 128 位 AES 加密，而与相同管理点相比，运行 Vista 的客户端计算机将进行协商，以将标准降至 3DES 加密。 系统将进行相同的协商，以对客户端通知过程中传输的包进行哈希处理，从而使用 SHA-1 或 SHA-2。  

##  <a name="certificates-used-by-configuration-manager"></a>Configuration Manager 使用的证书  
 有关 Configuration Manager 可以使用的公钥基础结构 (PKI) 证书、任何特殊要求或限制以及证书的使用方式的列表，请参阅 [PKI 证书要求](../network/pki-certificate-requirements.md)。 此列表包含支持的哈希算法和密钥长度。 大多数证书支持 SHA-256 和 2048 位密钥长度。  

> [!NOTE]  
>  Configuration Manager 使用的所有证书都必须在使用者名称或使用者可选名称中仅包含单字节字符。  

 以下情况需要 PKI 证书：  

- 在 Internet 上管理 Configuration Manager 客户端时。  

- 在移动设备上管理 Configuration Manager 客户端时。  

- 管理 Mac 计算机时。  

- 使用基于云的分发点时。  

  对于需要证书进行身份验证、签名或加密的大多数其他 Configuration Manager 通信，如果 PKI 证书可用，则 Configuration Manager 会自动使用这些证书。 如果这些证书不可用，则 Configuration Manager 会生成自签名证书。  

  Configuration Manager 在使用 Exchange Server 连接器管理移动设备时不使用 PKI 证书。  

### <a name="mobile-device-management-and-pki-certificates"></a>移动设备管理和 PKI 证书  
 如果移动运营商尚未锁定移动设备，则可以使用 Configuration Manager 或 Microsoft Intune 请求和安装客户端证书。 此证书在移动设备上的客户端与 Configuration Manager 站点系统或 Microsoft Intune 服务之间提供相互身份验证。 如果锁定了移动设备，则无法使用 Configuration Manager 或 Intune 部署证书。  

 如果启用移动设备硬件清单，则 Configuration Manager 或 Intune 还会清点移动设备上安装的证书。   

### <a name="operating-system-deployment-and-pki-certificates"></a>操作系统部署和 PKI 证书  
 当你使用 Configuration Manager 来部署操作系统，并且管理点需要 HTTPS 客户端连接时，客户端计算机还必须具有证书才能与管理点通信，即使在该计算机处于过渡阶段（例如从任务序列媒体或支持 PXE 的分发点中启动）中时也是如此。 为了支持此方案，你必须创建一个 PKI 客户端身份验证证书，并使用私钥将其导出，然后将该证书导入到站点服务器属性并同时添加管理点的受信任根 CA 证书。  

 如果创建可启动媒体，则在创建可启动媒体时导入客户端身份验证证书。 在可启动媒体上配置一个密码，以帮助保护私钥和任务序列中配置的其他敏感数据。 通过可启动媒体启动的每台计算机将根据需要为客户端功能（例如请求客户端策略）向管理点提供相同的证书。  

 如果使用 PXE 启动，则会将客户端身份验证证书导入到支持 PXE 的分发点，并且它为通过支持 PXE 的该分发点启动的每个客户端使用相同的证书。 作为最佳安全方案，请要求将其计算机连接到 PXE 服务的用户提供密码，以帮助保护私钥和任务序列中的其他敏感数据。  

 如果其中任何一个客户端身份验证证书已泄露，请在“管理”  工作区的“安全”  节点内的“证书”  节点中阻止证书。 要管理这些证书，你必须具有“管理操作系统部署证书”  权限。  

 部署了操作系统并安装了 Configuration Manager 之后，客户端将需要自己的 PKI 客户端身份验证证书来进行 HTTPS 客户端通信。  

### <a name="isv-proxy-solutions-and-pki-certificates"></a>ISV 代理解决方案和 PKI 证书  
 独立软件供应商 (ISV) 可创建扩展 Configuration Manager 的应用程序。 例如，ISV 可创建扩展来支持非 Windows 客户端平台，例如 Macintosh 或 UNIX 计算机。 但是，如果站点系统需要 HTTPS 客户端连接，则这些客户端还必须使用 PKI 证书以与站点进行通信。 Configuration Manager 包括将证书分配给启用 ISV 代理客户端与管理点之间的通信的 ISV 代理的功能。 如果使用需要 ISV 代理证书的扩展，请查阅该产品的文档。 有关如何创建 ISV 代理证书的详细信息，请查看 Configuration Manager 软件开发人员工具包 (SDK)。  

 如果 ISV 证书已泄露，请在“管理”  工作区的“安全”  节点内的“证书”  节点中阻止该证书。  

### <a name="asset-intelligence-and-certificates"></a>资产智能和证书  
 Configuration Manager 随同资产智能同步点用来连接到 Microsoft 的 X.509 证书一起安装。 Configuration Manager 使用此证书从 Microsoft 证书服务请求客户端身份验证证书。 客户端身份验证证书安装在资产智能同步点站点系统服务器上，并用于向 Microsoft 验证服务器。 Configuration Manager 使用客户端身份验证证书来下载资产智能目录和上载软件标题。  

 此证书的密钥长度为 1024 位。  

### <a name="cloud-based-distribution-points-and-certificates"></a>基于云的分发点和证书  
 从 System Center 2012 Configuration Manager SP1 开始，基于云的分发点需要你上载到 Microsoft Azure 的管理证书（自签名或 PKI）。 此管理证书需要服务器身份验证功能，并且要求证书密钥长度为 2048 位。 此外，你必须为每个基于云的分发点配置服务证书，该证书不能是自签名证书，但也具有服务器身份验证功能，并且最小证书密钥长度为 2048 位。  

> [!NOTE]  
>  自签名管理证书仅用于测试目的，不要在生产网络上使用。  

 客户端不需要客户端 PKI 证书来使用基于云的分发点；它们使用自签名证书或客户端 PKI 证书来向管理进行验证。 然后，管理点将 Configuration Manager 访问令牌颁发给客户端，客户端会将该令牌提供给基于云的分发点。 令牌的有效期为 8 小时。  

### <a name="the-microsoft-intune-connector-and-certificates"></a>Microsoft Intune 连接器和证书  
 当 Microsoft Intune 注册移动设备时，你可以通过创建 Microsoft Intune 连接器来在 Configuration Manager 中管理这些移动设备。 连接器使用具有客户端身份验证功能的 PKI 证书向 Microsoft Intune 验证 Configuration Manager，并通过使用 SSL 在它们之间传输所有信息。 证书密钥大小为 2048 位，并且使用 SHA-1 哈希算法。  

 安装连接器时，会在站点服务器上为旁加载密钥创建和存储签名证书，在证书注册点上创建和存储加密证书，以对简单证书注册协议 (SCEP) 质询进行加密。 这些证书也具有 2048 位的密钥大小，并且使用 SHA-1 哈希算法。  

 当 Intune 注册移动设备时，它将在移动设备上安装 PKI 证书。 此证书具有客户端身份验证功能，使用 2048 位的密钥大小，并使用 SHA-1 哈希算法。  

 Microsoft Intune 会自动请求、生成和安装这些 PKI 证书。  

### <a name="crl-checking-for-pki-certificates"></a>针对 PKI 证书的 CRL 检查  
 PKI 证书吊销列表 (CRL) 会增加管理和处理开销，但它更安全。 但是，如果启用了 CRL 检查但无法访问 CRL，则 PKI 连接将失败。 有关详细信息，请参阅 [Configuration Manager 的安全性和隐私](security-and-privacy.md)。  

 IIS 中默认情况下启用了证书吊销列表 (CRL) 检查，因此，如果你要将 CRL 与 PKI 部署结合使用，在运行 IIS 的大多数 Configuration Manager 站点系统上无需进行任何其他配置。 例外情况是软件更新，它需要一个手动步骤来启用 CRL 检查以验证软件更新文件上的签名。  

 对于客户端计算机，当它们使用 HTTPS 客户端连接时，CRL 检查默认情况下已启用。 在 Configuration Manager SP1 或更高版本中，你无法为 Mac 计算机上的客户端禁用 CRL 检查。  

 对于 Configuration Manager 中的下列连接，CRL 检查不受支持：  

-   服务器到服务器连接。  

-   Configuration Manager 注册的移动设备。  

-   Microsoft Intune 注册的移动设备。  

##  <a name="cryptographic-controls-for-server-communication"></a>服务器通信的加密控制  
 Configuration Manager 为服务器通信使用下列加密控制。  

### <a name="server-communication-within-a-site"></a>站点内的服务器通信  
 每个站点系统服务器使用证书将数据传输到同一 Configuration Manager 站点中的其他站点系统。 某些站点系统角色也使用证书进行身份验证。 例如，你将注册代理点安装在一个服务器上，并将注册点安装在另一个服务器上，则它们可通过使用此身份证书相互进行验证。 当 Configuration Manager 为此通信使用证书时，如果有具有服务器身份验证功能的 PKI 证书可用，则 Configuration Manager 将自动使用该证书；否则 Configuration Manager 将生成自签名证书。 此自签名证书具有服务器身份验证功能、使用 SHA-256，并且具有 2048 位的密钥长度。 Configuration Manager 将该证书复制到可能需要信任该站点系统的其他站点系统服务器上的“受信任人”存储。 然后，站点系统可通过使用这些证书和 PeerTrust 来相互信任。  

 除了每个站点系统服务器的此证书外，Configuration Manager 还会为大多数站点系统角色生成自签名证书。 如果同一站点中有站点系统角色的多个实例，它们将共享相同的证书。 例如，你可能在同一站点中有多个管理点或多个注册点。 此自签名证书也使用 SHA-256，并且密钥长度为 2048 位。 该证书也将复制到可能需要信任它的站点系统服务器上的“受信任人”存储。 下列站点系统角色会生成此证书：  

- 应用程序目录 Web 服务点  

- 应用程序目录网站点  

- 资产智能同步点  

- 证书注册点  

- Endpoint Protection 点  

- 注册点  

- 回退状态点  

- 管理点  

- 启用多播的分发点  

- Reporting Services 点  

- 软件更新点  

- 状态迁移点  

- Microsoft Intune 连接器  

这些证书由 Configuration Manager 自动管理并会在必要时自动生成。  

Configuration Manager 还使用客户端身份验证证书将状态消息从分发点发送到管理点。 如果仅针对 HTTPS 客户端连接配置了管理点，则必须使用 PKI 证书。 如果管理点接受 HTTP 连接，则你可以使用 PKI 证书，或选择选项以使用具有客户端身份验证功能、使用 SHA-256 并且密钥长度为 2048 位的自签名证书。  

### <a name="server-communication-between-sites"></a>站点间的服务器通信  
 Configuration Manager 通过使用数据库复制和基于文件的复制在站点之间传输数据。 有关详细信息，请参阅[终结点之间的通信](../hierarchy/communications-between-endpoints.md)。  

 Configuration Manager 自动配置站点之间的数据库复制，并使用具有服务器身份验证功能的 PKI 证书（如果这些证书可用）；否则，Configuration Manager 将为服务器身份验证创建自签名证书。 在这两种情况下，站点之间的身份验证都是通过“受信任人”存储（使用 PeerTrust）中的证书建立的。 此证书存储用于确保只有 Configuration Manager 层次结构使用的 SQL Server 计算机才参与站点间复制。 尽管主站点和管理中心站点可将配置更改复制到层次结构中的所有站点，但辅助站点只能将配置更改复制到其父站点。  

 站点服务器通过使用自动进行的安全密钥交换来建立站点间通信。 发送站点服务器生成哈希，并使用其私钥对该哈希进行签名。 接收站点服务器通过使用公钥来检查签名，并将哈希与本地生成的值进行比较。 如果它们匹配，则接收站点接受复制的数据。 如果值不匹配，则 Configuration Manager 拒绝复制数据。  

 Configuration Manager 中的数据库复制使用 SQL Server Service Broker 通过下列机制在站点之间传输数据：  

- SQL Server 到 SQL Server 的连接：此机制使用 Windows 凭据进行服务器身份验证，并使用具有 1024 位的自签名证书通过高级加密标准 (AES) 对数据进行签名和加密。 如果具有服务器身份验证功能的 PKI 证书可用，则将使用这些证书。 证书必须位于“计算机”证书存储的“个人”存储中。  

- SQL Service Broker：此机制使用具有 2048 位的自签名证书进行身份验证，以及通过使用高级加密标准 (AES) 对数据进行签名和加密。 证书必须位于 SQL Server master 数据库中。  

  基于文件的复制使用服务器消息块 (SMB) 协议，并使用 SHA-256 对未加密但不包含任何敏感数据的此数据进行签名。 如果要对此数据进行加密，你可以使用 IPsec，并且必须独立于 Configuration Manager 实现这一点。  

##  <a name="cryptographic-controls-for-clients-that-use-https-communication-to-site-systems"></a>使用站点系统 HTTPS 通信的客户端的加密控制  
 当站点系统角色接受客户端通信时，你可以将它们配置为接受 HTTPS 和 HTTP 连接，或仅接受 HTTPS 连接。 接受来自 Internet 的连接的站点系统角色仅接受通过 HTTPS 进行的客户端连接。  

 通过 HTTPS 进行的客户端连接通过与公钥基础结构 (PKI) 集成来帮助保护客户端到服务器通信，从而可提供较高级别的安全性。 但是，如果在未透彻理解 PKI 规划、部署和操作的情况下配置 HTTPS 客户端连接，将仍可能会使你易于受到攻击。 例如，你不保护根 CA 的安全，攻击者可能会危害整个 PKI 基础结构的信任。 如果未能使用受控和受保护的过程来部署和管理 PKI 证书，则可能会产生无法接收关键软件更新或包的不受管理的客户端。  

> [!IMPORTANT]  
>  用于客户端通信的 PKI 证书仅保护客户端和某些站点系统之间的通信。 它们不保护站点服务器和站点系统之间或站点服务器之间的信道。  

### <a name="communication-that-is-unencrypted-when-clients-use-https-communication"></a>客户端使用 HTTPS 通信时未加密的通信  
 当客户端使用 HTTPS 与站点系统通信时，通常会通过 SSL 对通信进行加密。 但是，在下列情况中，客户端会在不使用加密的情况下与站点系统通信：  

- 客户端无法在 Intranet 上建立 HTTPS 连接并回退为使用 HTTP（如果站点系统允许此配置）  

- 与下列站点系统角色的通信：  

  -   客户端将状态消息发送到回退状态点  

  -   客户端将 PXE 请求发送到支持 PXE 的分发点  

  -   客户端将通知数据发送到管理点  

  Reporting Services 点配置为独立于客户端通信模式使用 HTTP 或 HTTPS。  

##  <a name="cryptographic-controls-for-clients-chat-use-http-communication-to-site-systems"></a>使用站点系统 HTTP 通信的客户端的加密控制  
 当客户端使用与站点系统角色的 HTTP 通信时，它们可使用 PKI 证书进行客户端身份验证，或使用 Configuration Manager 生成的自签名证书。 当 Configuration Manager 生成自签名证书时，这些证书具有用于签名和加密的自定义对象标识符，并且用于唯一标识客户端。 对于除 Windows Server 2003 之外的所有受支持的操作系统，这些自签名证书使用 SHA-256，并且其密钥长度为 2048 位。 对于 Windows Server 2003，则使用 SHA1，且其密钥长度为 1024 位。  

### <a name="operating-system-deployment-and-self-signed-certificates"></a>操作系统部署和自签名证书  
 当你使用 Configuration Manager 来部署包含自签名证书的操作系统时，客户端计算机还必须具有证书才能与管理点通信，即使在该计算机处于过渡阶段（例如从任务序列媒体或支持 PXE 的分发点中启动）中时也是如此。 为了针对 HTTP 客户端连接支持此方案，Configuration Manager 会生成自签名证书，这些证书具有用于签名和加密的自定义对象标识符，并且用于唯一标识客户端。 对于除 Windows Server 2003 之外的所有受支持的操作系统，这些自签名证书使用 SHA-256，并且其密钥长度为 2048 位。 对于 Windows Server 2003，则使用 SHA1，且其密钥长度为 1024 位。 如果这些自签名证书已泄露，为了防止攻击者使用这些证书来模拟受信任的客户端，请在“管理”  工作区的“安全”  节点内的“证书”  节点中阻止证书。  

### <a name="client-and-server-authentication"></a>客户端和服务器身份验证  
 在客户端通过 HTTP 连接时，它们使用 Active Directory 域服务或 Configuration Manager 受信任的根密钥对管理点进行身份验证。 客户端不会对其他站点系统角色（例如状态迁移点或软件更新点）进行身份验证。  

 在管理点使用自签名客户端证书第一次对客户端进行身份验证时，此机制提供最低的安全性，因为任何计算机都能生成自签名证书。 在这种情况下，必须利用批准手段来强化客户端标识过程。 只应批准受信任的计算机 - 由 Configuration Manager 自动批准或由管理用户手动批准。 有关详细信息，请参阅[终结点之间的通信](../hierarchy/communications-between-endpoints.md)中的“审批”部分。  

## <a name="about-ssl-vulnerabilities"></a>有关 SSL 漏洞
若要提高 Configuration Manager 客户端和服务器的安全性，请执行以下操作：

- 启用 TLS 1.2

  若要启用 TLS 1.2 for Configuration Manager，请参阅：[如何启用 TLS 1.2 for Configuration Manager](enable-tls-1-2.md)。
- 禁用 SSL 3.0、TLS 1.0 和 TLS 1.1 
- 重新排序与 TLS 相关的密码套件 

有关详细信息，请参阅[如何限制使用特定的加密算法和 Schannel.dll 中的协议](https://support.microsoft.com/help/245030/)以及 [Prioritizing Schannel Cipher Suites](https://docs.microsoft.com/windows/win32/secauthn/prioritizing-schannel-cipher-suites)（以优先顺序排列 Schannel 密码套件）。 这些操作不会影响 Configuration Manager 的功能。

