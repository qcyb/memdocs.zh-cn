---
title: 安全基础知识
titleSuffix: Configuration Manager
description: 了解有关 Configuration Manager 中的安全性层的信息。
ms.date: 10/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 035b7f73-8b78-4ed1-835e-a31f9a5c4a02
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6c702916f73d1fbc842966161a6958a61d24044a
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126063"
---
# <a name="fundamentals-of-security-for-configuration-manager"></a>Configuration Manager 安全性的基础知识

适用范围：  Configuration Manager (Current Branch)

本文总结了任何 Configuration Manager 环境的以下基本安全组件：
- [安全层](#bkmk_layers)
- [基于角色的管理](#bkmk_rba)
- [保护客户端终结点](#bkmk_endpoints)
- [Configuration Manager 帐户和组](#bkmk_accounts)
- [隐私](#bkmk_privacy)

## <a name="security-layers"></a><a name="bkmk_layers"></a> 安全层

Configuration Manager 的安全性包括以下层： 
- [Windows OS 和网络安全](#bkmk_layer-windows)
- [网络基础结构：防火墙、入侵检测、公钥基础结构 (PKI)](#bkmk_layer-network)
- [Configuration Manager 安全控件](#bkmk_layer-cm)
- [SMS 提供程序](#bkmk_layer-provider)
- [站点数据库权限](#bkmk_layer-db)

#### <a name="windows-os-and-network-security"></a><a name="bkmk_layer-windows"></a> Windows OS 和网络安全
第一层是 Windows 为 OS 和网络提供的安全功能。 该层包括以下组件：  

-   用于在 Configuration Manager 组件之间传输文件的文件共享  

-   帮助保护文件和注册表项的访问控制列表 (ACL)  

-   帮助保护通信的 Internet 协议安全性 (IPsec)  

-   用于设置安全策略的组策略  

-   用于分布式应用程序的分布式组件对象模型 (DCOM) 权限，例如 Configuration Manager 控制台  

-   用于存储安全主体的 Active Directory 域服务  

-   Windows 帐户安全，包括 Configuration Manager 在安装期间创建的一些组  

#### <a name="network-infrastructure"></a><a name="bkmk_layer-network"></a> 网络基础结构

附加的安全组件（如防火墙和入侵检测）帮助为整个环境提供防御。 由行业标准的公钥基础结构 (PKI) 实现所颁发的证书帮助提供身份验证、签名和加密。  

#### <a name="configuration-manager-security-controls"></a><a name="bkmk_layer-cm"></a> Configuration Manager 安全控件

除了 Windows Server 和网络基础结构提供的安全性之外，Configuration Manager 还以多种方式控制对其控制台和资源的访问。 默认情况下，只有本地管理员才有权访问 Configuration Manager 控制台需在安装它的计算机上使用的文件和注册表项。  

#### <a name="sms-provider"></a><a name="bkmk_layer-provider"></a> SMS 提供程序

下一个安全层建立在通过 Windows Management Instrumentation (WMI)（具体指 SMS 提供程序）进行的访问的基础上。 SMS 提供程序是一种 Configuration Manager 组件，它授予用户访问权限以查询站点数据库中的信息。 默认情况下，只有本地 SMS 管理员组的成员才能访问该提供程序。 此组最初仅包含安装了 Configuration Manager 的用户。 若要向其他帐户授予对通用信息模型 (CIM) 存储库和 SMS 提供程序的权限，请将这些帐户添加到 SMS 管理员组中。  

从版本 1810 开始，可以为管理员指定访问 Configuration Manager 站点的最低身份验证级别。 此功能强制管理员以要求的级别登录到 Windows。 <!--1357013-->  

有关详细信息，请参阅[规划 SMS 提供程序](../plan-design/hierarchy/plan-for-the-sms-provider.md)。

#### <a name="site-database-permissions"></a><a name="bkmk_layer-db"></a> 站点数据库权限

最后一个安全层基于与站点数据库中的对象有关的权限。 默认情况下，本地系统帐户和用于安装 Configuration Manager 的用户帐户可以管理站点数据库中的所有对象。 在 Configuration Manager 控制台中使用基于角色的管理向其他管理用户授予权限和限制其权限。  



## <a name="role-based-administration"></a><a name="bkmk_rba"></a>基于角色的管理  

 Configuration Manager 使用基于角色的管理来帮助保护对象（如集合、部署和站点）。 此管理模式为所有站点和站点设置集中定义及管理层次结构范围的安全访问设置。 

 管理员将“安全角色”分配给管理用户和组权限  。 权限连接到不同的 Configuration Manager 对象类型，用于创建或更改客户端设置等。 

 管理用户负责管理的特定于“安全作用域”组的对象实例，如安装 Microsoft 365 Apps 的应用程序。 

 安全角色、安全作用域和集合的组合定义管理用户可以查看和管理的对象。 Configuration Manager 为典型的管理任务安装某些默认安全角色。 创建自己的安全角色来满足特定业务需求。  

 有关详细信息，请参阅[配置基于角色的管理](../servers/deploy/configure/configure-role-based-administration.md)。  



## <a name="securing-client-endpoints"></a><a name="bkmk_endpoints"></a> 保护客户端终结点  

 Configuration Manager 通过使用自签名/PKI 证书或 Azure Active Directory (Azure AD) 令牌来保护客户端与站点系统角色的通信。 某些方案需要使用 PKI 证书。 例如，[基于 Internet 的客户端管理](../clients/manage/plan-internet-based-client-management.md)以及[移动设备客户端](../../mdm/plan-design/plan-on-premises-mdm.md)。  

 可以为 HTTPS 或 HTTP 客户端通信配置客户端连接的站点系统角色。 客户端计算机始终使用可用的最安全方法进行通信。 只有在具有允许 HTTP 通信的站点系统角色时，客户端计算机才会回退使用不太安全的通信方法。  

 有关详细信息，请参阅[安全规划](../plan-design/security/plan-for-security.md)。



## <a name="configuration-manager-accounts-and-groups"></a><a name="bkmk_accounts"></a> Configuration Manager 帐户和组  

 Configuration Manager 使用本地系统帐户来执行大部分站点操作。 某些管理任务可能需要创建和维护其他帐户。 在安装过程中，Configuration Manager 会创建几个默认的组和 SQL Server 角色。 可能要手动将计算机或用户帐户添加到默认的组和 SQL Server 角色中。  

 有关详细信息，请参阅 [Configuration Manager 中使用的帐户](../plan-design/hierarchy/accounts.md)。  



## <a name="privacy"></a><a name="bkmk_privacy"></a> 隐私  

 实施 Configuration Manager 前，请考虑隐私要求。 尽管企业管理产品因其可有效地管理大量客户端而提供了许多优点，但此软件可能会影响组织中用户的隐私。 Configuration Manager 包括很多用于收集数据和监视设备的工具。 一些工具可能在组织中存在隐私方面的隐患。  

 例如，在安装 Configuration Manager 客户端时，默认情况下会启用许多管理设置。 此配置会导致客户端软件向 Configuration Manager 站点发送信息。 该站点将客户端信息存储在站点数据库中。 不会将客户端信息直接发送给 Microsoft。 有关详细信息，请参阅[诊断和使用情况数据](../plan-design/diagnostics/diagnostics-and-usage-data.md)。



## <a name="see-also"></a>另请参阅

- [规划安全性](../plan-design/security/plan-for-security.md)  

- [Configuration Manager 客户端的安全和隐私](../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [配置安全性](../plan-design/security/configure-security.md)   

- [终结点之间的通信](../plan-design/hierarchy/communications-between-endpoints.md)  

- [加密控制技术参考](../plan-design/security/cryptographic-controls-technical-reference.md)  
