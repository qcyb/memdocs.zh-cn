---
title: 基于 Internet 的客户端管理
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中创建管理基于 Internet 的客户端的计划。
ms.date: 04/29/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 83a7c934-3b11-435d-ba22-cbc274951e83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f7054c75643c6ffa37decba74f9fe85831728985
ms.sourcegitcommit: b7e5b053dfa260e7383a9744558d50245f2bccdc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/29/2020
ms.locfileid: "82587216"
---
# <a name="plan-for-internet-based-client-management-in-configuration-manager"></a>Configuration Manager 中基于 Internet 的客户端管理计划

适用范围：  Configuration Manager (Current Branch)

在 Configuration Manager 客户端未连接到你的 Internet 网络时，使用基于 Internet 的客户端管理 (IBCM) 来管理这些客户端。 使用 IBCM 的优点：

- 可完全控制提供服务的服务器和角色
- 不依赖云服务
- 无需虚拟专用网络 (VPN)
- 所有成本均与本地服务相关

由于在公共网络上管理客户端计算机对安全性的要求较高，因此 IBCM 要求使用 PKI 证书。 此配置可确保通过独立机构对连接进行了身份验证。 当 IBCM 客户端和站点服务器发送数据时，数据会被加密并受到保护。  

## <a name="client-communications"></a>客户端通信

主站点上的下列站点系统角色支持来自不受信任的位置的客户端连接：

> [!NOTE]
> 尽管 IBCM 主要侧重于基于 Internet 的方案，但相同的行为也适用于不受信任的 Active Directory 林中的客户端。 辅助站点不支持来自不受信任位置的客户端连接。

- 用于 Configuration Manager 策略模块 (NDES) 的证书注册点

- 分发点

- 基于云的分发点

- 注册代理点

- 回退状态点

- 管理点

- 软件更新点

> [!NOTE]
> 版本 1910 已终止对应用程序目录角色的支持。 有关详细信息，请参阅[删除应用程序目录](../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat)。 对于仍然受支持的 Configuration Manager 1906 或更低版本，应用程序目录网站点可接受来自基于 Internet 的客户端的连接。

### <a name="about-internet-facing-site-systems"></a>关于面向 Internet 的站点系统

客户端的林和站点系统服务器的林之间不需要信任。 但当包含面向 Internet 的站点系统的林信任包含用户帐户的林时，如果启用“客户端策略”客户端设置“启用来自 Internet 客户端的用户策略请求”，则此配置对 Internet 上的设备支持基于用户的策略   。

例如，以下配置说明了当 IBCM 支持 Internet 上设备的用户策略时：

- 基于 Internet 的管理点位于外围网络中。 该网络还有一个只读域控制器，用于对用户进行身份验证。 外围网络与内部网络之间的防火墙允许 Active Directory 数据包。

- 用户帐户位于基于 Intranet 的林中。 基于 Internet 的管理点位于基于外围的林中。 外围林信任内部林。 外围网络与内部网络之间的防火墙允许身份验证数据包。

- 用户帐户和基于 Internet 的管理点都位于基于 Intranet 的林中。 你使用 Web 代理服务器将管理点发布到 Internet。

### <a name="use-a-web-proxy-server"></a>使用 Web 代理服务器

在使用 Web 代理服务器将基于 Internet 的站点系统发布到 Internet 中时，可将这些系统放在 Intranet 中。 可仅为 Internet 客户端连接配置这些站点系统，也可为 Internet 和 Intranet 客户端连接进行配置。 使用 Web 代理服务器时，可针对到 SSL 的安全套接字层 (SSL) 桥接或 SSL 隧道来配置它。

#### <a name="ssl-bridging-to-ssl"></a>到 SSL 的 SSL 桥接

推荐使用“到 SSL 的 SSL 桥接”配置，它更加安全，因为它将 SSL 终止和身份验证结合使用。 它通过计算机身份验证对客户端计算机进行身份验证。 通过 Configuration Manager 注册的移动设备不支持 SSL 桥接。

借助代理上的 SSL 终止，它会在将数据包转发到内部网络之前，从 Internet 中检查这些数据包。 代理将对来自客户端的连接进行验证，将其终止，然后建立一个新的经身份验证的连接，连接到基于 Internet 的站点系统。 如果 Configuration Manager 客户端使用代理，则客户端会安全地在数据包有效负载中包含其标识 (GUID)。 管理点不会将代理视为客户端。 Configuration Manager 不支持 HTTP 到 HTTPS 的桥接，也不支持 HTTPS 到 HTTP 的桥接。

> [!NOTE]
> Configuration Manager 不支持设置第三方 SSL 桥接配置。 例如，Citrix Netscaler 或 F5 BIG-IP。 请与设备供应商协作，以将其配置为与 Configuration Manager 结合使用。

#### <a name="tunneling"></a>隧道

如果代理 Web 服务器无法支持 SSL 桥接的要求，则 Configuration Manager 也支持 SSL 隧道。 你还可使用 SSL 隧道来支持通过 Configuration Manager 注册的移动设备。 该方法安全性较低，因为代理会在不终止 SSL 的情况下将来自 Internet 的 SSL 数据包转发到站点系统。 代理不会检查数据包中是否包含恶意内容。 使用 SSL 隧道时，代理 Web 服务器不需要证书。

## <a name="plan-for-internet-based-clients"></a>基于 Internet 的客户端规划

确定是同时针对 Intranet 和 Internet 上的管理配置基于 Internet 的客户端，还是只针对基于 Internet 的客户端管理进行配置。 只能在客户端安装期间配置此管理选项。 稍后若要更改，需重新安装客户端。

> [!NOTE]
> 如果配置管理点来支持基于 Internet 的客户端，则连接到该管理点的客户端在接下来刷新其可用管理点的列表时，会变为支持 Internet。
>
> 你不必只允许 Internet 使用仅限 Internet 的客户端管理的配置。 你也可以在 Intranet 上使用它。

为仅限 Internet 的管理配置的客户端仅与为 Internet 的客户端连接配置的站点系统通信。 在以下情况中使用此配置：

- 针对你知道永不会连接到你的 Intranet 的计算机。 例如，位于远程位置的销售点计算机。
- 用于仅限与 HTTPS 进行客户端通信。 例如，为了支持防火墙和受限的安全策略。
- 在外围网络中按照基于 Internet 的站点系统，以及在你想要将这些服务器作为 Configuration Manager 客户端进行管理时。

> [!NOTE]
> 想要管理 Internet 上的工作组客户端时，请将其安装为仅限 Internet 的客户端。
>
> 将移动设备配置为使用基于 Internet 的管理点时，会将该设备自动配置为仅限 Internet 的客户端。

可为 Internet 和 Intranet 客户端管理配置其他客户端。 当它们检测到网络更改时，它们会在 IBCM 和 Intranet 客户端管理之间自动切换。 如果这些客户端可找到并连接到支持 Intranet 客户端连接的管理点，则会将这些客户端作为 Intranet 客户端进行管理。 Intranet 客户端具有 Configuration Manager 的完整功能。 如果客户端找不到或无法连接到支持 Intranet 客户端连接的管理点，它们会尝试连接到基于 Internet 的管理点。 如果此操作成功，则这些客户端会在其分配的站点中由基于 Internet 的站点系统进行管理。

自动切换的优势在于，客户端可在连接到 Intranet 时使用所有功能，在位于 Internet 上获得基本管理。 Internet 上开始的内容下载可在 Intranet 上无缝地继续，反之亦然。

## <a name="prerequisites"></a>必备条件

Configuration Manager 中的 IBCM 具有以下依赖关系：

- 客户端需要建立 Internet 连接。 Configuration Manager 使用设备的现有 Internet 连接。 移动设备必须直接连接到 Internet。 完整的客户端计算机可直接连接到 Internet，也可使用代理 Web 服务器进行连接。

- 支持 IBCM 的站点系统需要连接 Internet，且必须位于 Active Directory 域中。 基于 Internet 的站点系统不需要与站点服务器的 Active Directory 林建立信任关系。 但是，当基于 Internet 的管理点可通过使用 Windows 身份验证对用户进行身份验证时，它也支持用户策略。 如果 Windows 身份验证失败，则它仅支持设备策略。

    > [!NOTE]
    > 若要支持用户策略，还可在“客户端策略”组中启用以下客户端设置  ：
    >
    > - **在客户端上启用用户策略轮询**
    > - **启用来自 Internet 客户端的用户策略请求**  

- 公钥基础结构 (PKI)，用于部署和管理基于 Internet 的客户端和站点系统服务器所需的证书。 有关详细信息，请参阅 [PKI 证书要求](../../plan-design/network/pki-certificate-requirements.md)。

- 为支持 IBCM 的站点系统的 Internet 完全限定的域名 (FQDN) 注册公共 DNS 主机。

### <a name="client-communication-requirements"></a>客户端通信要求

干预防火墙或代理服务器必须允许基于 Internet 的站点系统的客户端通信：

- 支持 HTTP 1.1  

- 允许多部件 MIME 附件的 HTTP 内容类型（多部件/混合和应用程序/八进制数流）  

#### <a name="verbs"></a>谓词

允许对基于 Internet 的站点系统服务器角色使用以下谓词：

| 角色 | 谓词 |
|------|-------|
| 管理点 | - HEAD<br>- CCM_POST<br>- BITS_POST<br>- GET<br>- PROPFIND |
| 分发点 | - HEAD<br>- GET<br>- PROPFIND |
| 回退状态点 | POST |
| 应用程序目录网站点 | -POST<br>-GET |

#### <a name="http-headers"></a>HTTP 头

允许对基于 Internet 的站点系统服务器角色使用以下 HTTP 头：

| 角色 | HTTP 头 |
|------|--------------|
| 管理点 | - Range:<br>- CCMClientID:<br>- CCMClientIDSignature:<br>- CCMClientTimestamp:<br>- CCMClientTimestampsSignature: |
| 分发点 | 范围： |

关于使用 Internet 中客户端连接的软件更新点时的类似通信要求，请参阅 Windows Server Update Services (WSUS) 的文档。

## <a name="unsupported-features"></a>不支持的功能

并非所有客户端管理功能都适用于 Internet。 Configuration Manager 不支持 Internet 上的客户端的某些功能。 这些不受支持的功能通常依赖于 Active Directory 域服务，或者不适合于公用网络。

通过 IBCM 管理 Internet 上的客户端时，下列功能不受支持：

- 通过 Internet 进行的客户端部署，如客户端请求和基于软件更新的客户端部署。 使用手动客户端安装。

- 自动站点分配

- LAN 唤醒

- 操作系统部署。 但是，你可部署不部署操作系统的任务序列。

- 远程控制

- 针对用户的软件部署。 此功能依赖于已被弃用的应用程序目录。

- 客户端漫游。 漫游能够使客户端始终找到最近的分发点来下载内容。 客户端不确定地选择基于 Internet 的站点系统之一，而不考虑带宽或物理位置。

如果你将软件更新点配置为接受 Internet 连接，则基于 Internet 的客户端始终会对此软件更新点进行扫描，以确定需要的软件更新。 如果这些客户端在 Internet 上，则它们首先会尝试从 Microsoft 更新下载软件更新，而不是从基于 Internet 的分发点中下载。 如果此行为失败，它们随后会尝试从基于 Internet 的分发点下载所需的软件更新。

> [!TIP]
> Configuration Manager 客户端会自动确定它是在 Intranet 上还是在 Internet 上。 如果客户端可连接域控制器或本地管理点，它会将自己的连接类型设置为“当前 Intranet”  。 否则，它会切换到“当前 Internet”，并与分配到其站点的站点系统进行通信  。
