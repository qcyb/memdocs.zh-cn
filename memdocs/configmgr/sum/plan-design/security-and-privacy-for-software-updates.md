---
title: 软件更新的安全和隐私
titleSuffix: Configuration Manager
description: 请遵循以下软件更新安全的最佳做法，了解 Configuration Manager 如何处理隐私信息。
manager: dougeby
ms.date: 09/16/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 41d6d5d8-ba84-4efb-b105-4d1eed239824
author: mestew
ms.author: mstewart
ms.openlocfilehash: 0838f43abf7ff972ac3f6ca2cdf44dcafda323ca
ms.sourcegitcommit: 6176a7825d6c663faa318a6818b7764bc70f08fc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90718716"
---
# <a name="security-and-privacy-for-software-updates-in-configuration-manager"></a>Configuration Manager 中软件更新的安全和隐私

适用范围：  Configuration Manager (Current Branch)

此主题包含 Configuration Manager 中软件更新的安全和隐私信息。  

##  <a name="security-best-practices-for-software-updates"></a><a name="BKMK_Security_HardwareInventory"></a> 软件更新的最佳安全方案  
 在将软件更新部署到客户端时，请使用以下最佳安全方案：  

-   不要更改有关软件更新包的默认权限。  

     默认情况下，软件更新包设置为向管理员提供“完全控制”  访问权，以及向用户提供“读取”  访问权。 如果更改这些权限，则可能会使攻击者能够添加、移除或删除软件更新。  

-   控制对软件更新下载位置的访问。  

     与 SMS 提供程序、站点服务器和实际上将软件更新下载到下载位置的管理用户对应的计算机帐户需要此下载位置的“写入”  访问权。 限制对此下载位置的访问，以减少攻击者在下载位置中篡改软件更新源文件的风险。  

     此外，如果将 UNC 共享用于下载位置，则通过使用 IPsec 或 SMB 签名来保护网络通道，以防止软件更新源文件在通过网络传输时被篡改。  

-   使用 UTC 来估计部署时间。  

     如果使用本地时间而不是 UTC，则用户可能会通过更改其计算机上的时区来延迟软件更新的安装。  

-   在 WSUS 上启用 SSL，然后按照保护 Windows Server Update Services (WSUS) 的最佳方案进行。  

     找到并遵循用于 Configuration Manager 的 WSUS 版本的安全最佳做法。 

     有关启用 SSL 的详细信息，请参阅[将软件更新点配置为结合使用 TLS/SSL 与 PKI 证书教程](../get-started/software-update-point-ssl.md)。 

    > [!IMPORTANT]  
    >  如果配置软件更新点以便为 WSUS 服务器启用 SSL 通信，则必须在 WSUS 服务器上配置 SSL 的虚拟根。  

-   启用 CRL 检查。  

     默认情况下，Configuration Manager 不会检查证书吊销列表 (CRL)，以便在将软件更新部署到计算机之前验证软件更新上的签名。 如果在每次使用证书时都检查 CRL，则能更好地抵御因使用已吊销的证书而造成的安全威胁，但这样做会使连接出现延迟，并在执行 CRL 检查的计算机上引发额外的处理操作。  

     有关如何为软件更新启用 CRL 检查的详细信息，请参阅[如何对软件更新启用 CRL 检查](../get-started/manage-settings-for-software-updates.md#crl-checking-for-software-updates)。  

-   配置 WSUS 以使用自定义网站。  

     在软件更新点上安装 WSUS 时，可以选择使用现有的 IIS 默认网站或创建自定义的 WSUS 网站。 为 WSUS 创建自定义网站，以便 IIS 在专用的虚拟网站中承载 WSUS 服务，而不是共享由其他 Configuration Manager 站点系统或其他应用程序使用的同一个网站。  

     有关详细信息，请参阅 [Configure WSUS to use a custom web site](plan-for-software-updates.md#BKMK_CustomWebSite)。  

##  <a name="privacy-information-for-software-updates"></a><a name="BKMK_Privacy_HardwareInventory"></a>软件更新的隐私信息  
 软件更新会扫描客户端计算机，以确定所需的软件更新，然后将该信息发送回站点数据库。 在软件更新过程中， Configuration Manager 可能会在客户端和服务器之间传输信息，这些信息标识计算机和登录帐户。  

 Configuration Manager 会维护有关软件部署过程的状态信息。 状态信息在传输或存储期间并未加密。 状态信息存储在 Configuration Manager 数据库中，而且由数据库维护任务删除。 状态信息不会发送给 Microsoft。  

 使用 Configuration Manager 软件更新在客户端计算机上安装软件更新时，可能要遵守这些更新的软件许可证条款，它们不同于 Configuration Manager 的软件许可证条款。 在使用 Configuration Manager 安装软件更新之前，请务必查看并同意软件许可条款。  

 默认情况下，Configuration Manager 并不实施软件更新，而且在收集信息前，需要执行几个配置步骤。  

 在配置软件更新之前，请考虑隐私要求。  
