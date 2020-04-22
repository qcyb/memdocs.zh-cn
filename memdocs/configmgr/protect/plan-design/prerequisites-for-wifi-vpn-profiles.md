---
title: Wi-Fi 和 VPN 配置文件先决条件
titleSuffix: Configuration Manager
description: 了解在 Configuration Manager 中管理 Wi-Fi 配置文件和 VPN 配置文件的先决条件
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: d2dacb2d-ab3b-42a2-8dc8-94da31f993c2
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9e7a557bab6b41be6e6335e3aa2744e8627d285b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706065"
---
# <a name="prerequisites-for-wi-fi-and-vpn-profiles-in-configuration-manager"></a>Configuration Manager 中 Wi-Fi 和 VPN 配置文件的先决条件

适用范围：  Configuration Manager (Current Branch)

Configuration Manager 中的 Wi-Fi 和 VPN 配置文件仅在产品内有依赖关系。

你需要下列安全权限才能管理公司资源访问设置，例如证书配置文件、Wi-Fi 配置文件和 VPN 配置文件：  

- 查看和管理 Wi-Fi 和配置文件的警报和报表：针对“警报”对象的“创建”、“删除”、“修改”、“修改报表”、“读取”和“运行报表”        。  

- 创建和管理证书配置文件：针对“证书配置文件”对象的“创作策略”、“修改报表”、“读取”和“运行报表”      。  

- 管理 Wi-Fi、证书和 VPN 配置文件部署：针对“集合”对象的“部署配置策略”、“修改客户端状态警报”、“读取”和“读取资源”      。  

- 管理所有配置策略：针对“配置策略”对象的“创建”、“删除”、“修改”、“读取”和“设置安全作用域”       。  

- 运行与 Wi-Fi 和 VPN 配置文件相关的查询：针对“查询”对象的“读取”权限   。  

- 在 Configuration Manager 控制台中查看 Wi-Fi 和 VPN 配置文件信息：针对“站点”  对象的“读取”  权限。  

- 查看 Wi-Fi 和 VPN 配置文件的状态消息：针对“状态消息”对象的“读取”权限   。  

- 创建和修改受信任的 CA 证书配置文件：针对“受信任的 CA 证书配置文件”对象的“创作策略”、“修改报表”、“读取”和“运行报表”      。  

- 创建和管理 VPN 配置文件：针对“VPN 配置文件”对象的“创作策略”、“修改报表”、“读取”和“运行报表”      。  

- 创建和管理 Wi-Fi 配置文件：针对“Wi-Fi 配置文件”对象的“创作策略”、“修改报表”、“读取”和“运行报表”      。  

在 Configuration Manager 中管理 Wi-Fi 配置文件需要“公司资源访问管理员”内置安全角色提供的这些权限  。 有关详细信息，请参阅[配置安全性](../../core/plan-design/security/configure-security.md)。
