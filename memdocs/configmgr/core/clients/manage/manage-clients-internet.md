---
title: 管理 Internet 上的客户端
titleSuffix: Configuration Manager
description: 了解如何通过 Configuration Manager 中的云管理网关和基于 Internet 的客户端管理来管理客户端。
ms.date: 06/10/2020
ms.prod: configuration-manager
ms.topic: conceptual
ms.technology: configmgr-client
ms.assetid: c667d6af-80c4-485f-910c-896c0171fd00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2840b30bee20d2fa73531b07c095e028979f6274
ms.sourcegitcommit: 2f1963ae208568effeb3a82995ebded7b410b3d4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2020
ms.locfileid: "84715588"
---
# <a name="manage-clients-on-the-internet-with-configuration-manager"></a>使用 Configuration Manager 管理 Internet 上的客户端

适用范围：Configuration Manager (Current Branch)

通常，Configuration Manager 中的多数托管计算机和服务器与执行管理功能的站点系统服务器物理上位于同一内部网络中。 但是，当客户端连接到 Internet 时，你可以在内部网络外对其进行管理。 此功能不需要客户端通过 VPN 连接到站点系统服务器。

Configuration Manager 提供两种方法来管理连接了 Internet 的客户端：

- 云管理网关

- 基于 Internet 的客户端管理

> [!NOTE]
> 可以将两个服务的组合用于单个站点。 如果某个设备从该站点获取 IBCM 和 CMG 的策略，则该设备将在它们之间随机进行通信。 可用于控制通信的唯一机制是客户端身份验证。 例如，如果加入 Azure AD 的客户端不信任基于 Internet 的管理点的服务器身份验证证书，则只能使用 CMG。 如果加入域的客户端不信任 CMG 的服务器身份验证证书，则只能使用基于 Internet 的管理点。<!-- SCCMDocs#1541 -->

## <a name="cloud-management-gateway"></a>云管理网关

云管理网关可管理基于 Internet 的客户端。 它将 Microsoft Azure 云服务以及与该服务通信的本地站点系统角色结合使用。 基于 Internet 的客户端使用该云服务与本地 Configuration Manager 进行通信。

### <a name="cmg-advantages"></a>CMG 优点

- 无需额外的本地基础结构投资。  

- 不会向 Internet 公开本地基础结构。  

- 运行服务的云虚拟机由 Azure 完全管理且免维护。  

- 可轻松在 Configuration Manager 控制台中进行设置和配置。  

### <a name="cmg-disadvantages"></a>CMG 缺点  

- 云订阅费用。  

- 通过云服务发送的管理数据。  

有关详细信息，请参阅[规划云管理网关](cmg/plan-cloud-management-gateway.md)。  

## <a name="internet-based-client-management"></a>基于 Internet 的客户端管理

此方法依赖于面向 Internet 的站点系统服务器，为了进行管理，客户端会直接与这些服务器通信。 它要求配置客户端和站点系统服务器，实现基于 Internet 的客户端管理 (IBCM)。

### <a name="ibcm-advantages"></a>IBCM 优点

- 无云服务依赖关系。  

- 无与云订阅关联的费用。  

- 可完全控制提供服务的服务器和角色。  

### <a name="ibcm-disadvantages"></a>IBCM 缺点

- 需要额外的基础结构投资。  

- 额外基础结构的日常管理费用和运营费用。  

- 必须向 Internet 公开基础结构。  

有关详细信息，请参阅[规划基于 Internet 的客户端管理](plan-internet-based-client-management.md)。  
