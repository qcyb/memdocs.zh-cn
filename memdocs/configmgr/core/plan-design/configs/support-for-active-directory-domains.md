---
title: 对 Active Directory 域的支持
titleSuffix: Configuration Manager
description: 了解 Active Directory 域中 Configuration Manager 站点系统的要求。
ms.date: 10/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8c5a13f8-42d5-4898-b7b6-e594dae8b335
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ab317597633eb432c73d2999590c1859124ddcfd
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688575"
---
# <a name="support-for-active-directory-domains-in-configuration-manager"></a>对 Configuration Manager 中的 Active Directory 域的支持

适用范围：  Configuration Manager (Current Branch)

所有 Configuration Manager 站点系统必须均为受支持的 Active Directory 域的成员。 Configuration Manager 客户端计算机可以是域成员，也可以是工作组成员。  

## <a name="requirements-and-limitations"></a>要求和限制

- 域成员资格也适用于在外围网络中支持基于 Internet 的客户端管理的站点系统。 （这些网络也称为 DMZ、边缘网络和外围子网）。  

- 不支持为托管站点系统角色的计算机更改以下配置：  

  - 域成员资格，包括从域中删除站点系统，然后重新加入同一域。

  - 域名  

  - 计算机名称  

  在进行这些更改之前，请卸载站点系统角色。 要对站点服务器进行这些更改，请先卸载站点。 还可以考虑[在被动模式下创建站点服务器](../../servers/deploy/configure/site-server-high-availability.md)，以帮助在站点服务器上管理此更改。

- Configuration Manager 支持 Windows Server 2008 R2 或更高版本的域和林功能级别。<!-- SCCMDocs#1853 -->

## <a name="disjoint-namespace"></a><a name="bkmk_Disjoint"></a> 非连续命名空间

可以在具有非连续命名空间的域中安装 Configuration Manager 站点系统和客户端  。  

在非连续命名空间中，计算机的主 DNS 后缀与该计算机的 Active Directory DNS 域名不匹配。 如果域控制器的 NetBIOS 域名与 Active Directory DNS 域名不匹配，则会产生另一种非连续命名空间方案。  

### <a name="disjoint-scenarios"></a>非连续方案

以下部分标识了非连续命名空间受支持的方案。  

#### <a name="scenario-1"></a>方案 1

域控制器的主 DNS 后缀与 Active Directory DNS 域名不同。 是域成员的计算机可以是非连续的或连续的。

在此方案中，域控制器是非连续的。 作为域成员的计算机（例如站点服务器和计算机）可以具有匹配以下内容之一的主 DNS 后缀：

- 域控制器的主 DNS 后缀
- Active Directory DNS 域名

#### <a name="scenario-2"></a>方案 2

Active Directory 域中的成员计算机是非连续的，即使域控制器是连续的。

在此方案中，站点系统的主 DNS 后缀与 Active Directory DNS 域名不同。 域控制器的主 DNS 后缀与 Active Directory DNS 域名相同。 作为 Configuration Manager 客户端的成员计算机可以具有匹配以下内容之一的主 DNS 后缀：

- 非连续站点系统服务器的主 DNS 后缀
- Active Directory DNS 域名

### <a name="configure-disjoint-namespace"></a>配置非连续命名空间

若要允许计算机访问非连续域控制器，请更改域对象容器上的 msDS-AllowedDNSSuffixes Active Directory 属性  。 将两个 DNS 后缀都加入到属性中。  

若要确保 DNS 后缀搜索列表包含组织中的所有 DNS 命名空间，请在非连续域中配置每台计算机的搜索列表  。 在命名空间列表中包含以下后缀：

- 域控制器的主 DNS 后缀
- DNS 域名
- Configuration Manager 可能与之通信的其他服务器的任何其他命名空间

可以使用组策略来配置“域名系统 (DNS) 后缀搜索”列表  。  

> [!IMPORTANT]  
> 引用 Configuration Manager 中的计算机时，使用其主 DNS 后缀输入该计算机。 此后缀应与在 Active Directory 域中注册为 dnsHostName 属性的完全限定的域名相匹配和与该系统关联的服务主体名称相匹配  。  

## <a name="single-label-domains"></a><a name="bkmk_SLD"></a> 单标签域

在满足以下条件时，Configuration Manager 支持单标签域中的站点系统和客户端：  

- 使用具有有效顶级域的非连续 DNS 命名空间，配置 Active Directory 域服务中的单标签域。  

  例如  ：Contoso 的单一标签域配置为，在 contoso.com 的 DNS 中具有非连续命名空间。 当在 Configuration Manager 中为 Contoso 域中的计算机指定 DNS 后缀时，应指定 Contoso.com 而不是 Contoso。  

- 系统上下文中的站点服务器之间的分布式组件对象模型 (DCOM) 连接必须使用 Kerberos 身份验证成功完成。  
