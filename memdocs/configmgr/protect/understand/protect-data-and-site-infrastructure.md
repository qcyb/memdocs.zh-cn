---
title: 保护数据和站点基础结构
titleSuffix: Configuration Manager
description: 了解如何通过 Configuration Manager 保护组织资源免遭泄露或恶意攻击。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 2117f786-d521-4790-9e8d-ec096c63c9d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 381f9d190b1d73bbbab6142fd9587e881d0870ce
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708595"
---
# <a name="protect-data-and-site-infrastructure"></a>保护数据和站点基础结构

适用范围：  Configuration Manager (Current Branch)

你希望用户安全地访问贵组织的资源。 保护基础结构和数据免遭泄露或恶意攻击。 使用 Configuration Manager 启用访问权限，并帮助保护贵组织的资源。  

- 借助 [Endpoint Protection](../deploy-use/endpoint-protection.md)，可以管理客户端计算机的以下 Microsoft Defender 策略：

  - Microsoft Defender 反恶意软件
  - Microsoft Defender 防火墙
  - Microsoft Defender 高级威胁防护
  - Microsoft Defender 攻击防护
  - Microsoft Defender 应用程序防护
  - Microsoft Defender 应用程序控制

  > [!TIP]
  > 若要使用 Microsoft 终结点管理器云服务管理共同管理的 Windows 10 设备上的 Endpoint Protection，请将 [Endpoint Protection 工作负载](../../comanage/workloads.md#endpoint-protection) 切换为 Intune  。 有关详细信息，请参阅 [Microsoft Intune 的 Endpoint Protection](https://docs.microsoft.com/intune/endpoint-protection-windows-10)。

- 使用 BitLocker 驱动器加密 (BDE) 保护本地 Windows 客户端上存储的数据。 Configuration Manager 提供了可代替 Microsoft BitLocker Administration and Monitoring (MBAM) 的完整 BitLocker 生命周期管理。 有关详细信息，请参阅[规划 BitLocker 管理](../plan-design/bitlocker-management.md)。

- 在使用 Windows Hello 企业版的 Windows 10 设备上启用替代的登录方法，而不是使用旧密码。 有关详细信息，请参阅 [Windows Hello 企业版设置](../deploy-use/windows-hello-for-business-settings.md)。

- 通过使用 VPN 配置文件来启用 VPN 连接，最大限度地减少你的用户连接到资源所需执行的操作。 有关详细信息，请参阅 [VPN 配置文件](../deploy-use/vpn-profiles.md)。  

- Wi-Fi 配置文件提供了一组工具和资源，有助于你为组织中的设备管理无线网络设置。 通过部署这些设置，你可以最大程度地减少最终用户连接到无线网络所需执行的工作。 有关详细信息，请参阅 [Wi-Fi 配置文件](../deploy-use/create-wifi-profiles.md)。  

- 为设备预配用户连接到资源所需的证书。 有关详细信息，请参阅[证书配置文件](../deploy-use/introduction-to-certificate-profiles.md)。  
