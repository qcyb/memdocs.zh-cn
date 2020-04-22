---
title: VPN 配置文件
titleSuffix: Configuration Manager
description: 了解如何使用 Configuration Manager 中的 VPN 配置文件将 VPN 设置部署到组织中的用户。
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: c0f094f1-852e-4606-91db-97846d8f0772
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9463d857599e676da6267313df575c8881436f93
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706245"
---
# <a name="vpn-profiles-in-configuration-manager"></a>Configuration Manager 中的 VPN 配置文件

适用范围：  Configuration Manager (Current Branch)

<!--1283610-->
使用 Configuration Manager 中的 VPN 配置文件将 VPN 设置部署到组织中的用户。 通过部署这些设置，你可以最大限度减少最终用户连接到公司网络资源需要进行的工作。  

例如，你希望用连接到内部网络上的文件共享所需的设置来配置所有 Windows 10 设备。 用连接到内部网络所需的设置创建 VPN 配置文件。 然后将此配置文件部署至拥有运行 Windows 10 的设备的所有用户。 用户能在可用网络的列表中看到 VPN 连接，并可以轻松连接。

创建 VPN 配置文件时，可以纳入各种安全设置。 这些设置包括服务器验证和客户端身份验证（使用 Configuration Manager 证书配置文件预配）的证书。 有关详细信息，请参阅[证书配置文件](introduction-to-certificate-profiles.md)。

> [!Note]
> 默认情况下，Configuration Manager 不启用此项可选功能。 必须在使用前启用此功能。 有关详细信息，请参阅[启用更新中的可选功能](../../core/servers/manage/install-in-console-updates.md#bkmk_options)。<!--505213-->  

## <a name="supported-platforms"></a>受支持的平台

下表介绍了可为各种设备平台配置的 VPN 配置文件。

|连接类型|Windows 8.1|Windows RT|Windows RT 8.1|Windows 10|
|---------------|-----------|----------|--------------|----------|
|**Pulse Secure**|是|否|是|是|
|**F5 Edge Client**|是|否|是|是|
|**Dell SonicWALL Mobile Connect**|是|否|是|是|
|**Check Point Mobile VPN**|是|否|是|是|
|**Microsoft SSL (SSTP)**|是|是|是|否|
|**Microsoft Automatic**|是|是|是|否|
|**IKEv2**|是|是|是|否|
|**PPTP**|是|是|是|否|
|**L2TP**|是|是|是|否|

## <a name="next-step"></a>下一步

> [!div class="nextstepaction"]
> [如何创建 VPN 配置文件](create-vpn-profiles.md)

## <a name="see-also"></a>另请参阅

- [VPN 配置文件的先决条件](../plan-design/prerequisites-for-wifi-vpn-profiles.md)

- [VPN 配置文件的安全和隐私](../plan-design/security-and-privacy-for-wifi-vpn-profiles.md)
