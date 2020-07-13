---
title: 在 Microsoft Intune 中使用终结点安全性策略管理防火墙设置 | Microsoft Docs
description: 在 Microsoft Endpoint Manager 中为使用终结点安全性防护墙策略管理的设备配置和部署策略。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 5b33be56975713c801d2ad3fdea17e6303687274
ms.sourcegitcommit: 03d2331876ad61d0a6bb1efca3aa655b88f73119
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2020
ms.locfileid: "85946906"
---
# <a name="firewall-policy-for-endpoint-security-in-intune"></a>Intune 中关于终结点安全性的防火墙策略

使用 Intune 中的终结点安全性防火墙策略为运行 macOS 和 Windows 10 的设备配置设备内置防火墙。

虽然可以通过在设备配置中使用 Endpoint Protection 配置文件来配置相同的防火墙设置，但设备配置文件还包含其他类别的设置。 这些附加设置与防火墙无关，可能会使仅需要为环境配置防火墙设置的任务复杂化。

在 [Microsoft endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)的“终结点安全性”节点的“管理”下查找用于防火墙的终结点安全性策略。

查看[防火墙配置文件的设置](../protect/endpoint-security-Firewall-profile-settings.md)。

## <a name="prerequisites-for-firewall-profiles"></a>防火墙配置文件的先决条件

- Windows 10 或更高版本
- 任何支持的 macOS 版本

## <a name="firewall-profiles"></a>防火墙配置文件

**macOS 配置文件**：

- **macOS 防火墙** - 启用和配置 macOS 上内置防火墙的设置。

**Windows 10 配置文件**：

- **Microsoft Defender 防火墙** - 配置具有高级安全性的 Windows Defender 防火墙设置。 Windows Defender 防火墙为设备提供基于主机的双向网络通讯筛选，并阻止未授权的网络流量流向或流出本地设备。

- **Microsoft Defender 防火墙规则**（预览） - 定义详细的防火墙规则（包括特定端口、协议、应用程序和网络），允许或阻止网络流量。 此配置文件的每个实例最多支持 150 个自定义规则。

## <a name="firewall-rule-mergers-and-policy-conflicts"></a>防火墙规则合并和策略冲突

规划防火墙策略，将其应用于仅使用一个策略的设备。 使用单个策略实例和策略类型有助于避免两个独立的策略对同一设置应用不同的配置，从而产生冲突。 当使用不同值管理相同设置的两个策略实例或策略类型之间存在冲突时，该设置不会被发送到设备。

- Microsoft Defender 防火墙配置文件可能会发生这种形式的策略冲突，该配置文件可能与其他 Microsoft Defender 防火墙配置文件发生冲突，或者与由其他策略类型（如设备配置）提供的防火墙配置文件发生冲突。

  Microsoft Defender 防火墙配置文件不会与 Microsoft Defender 防火墙规则配置文件相冲突 。

使用 Microsoft Defender 防火墙规则配置文件时，可对同一设备应用多个规则配置文件。 但是，当具有不同配置的相同设置具有不同的规则时，两个规则都会被发送到设备，然后在该设备上产生冲突。

- 例如，如果一个规则阻止 Teams.exe 通过防火墙，另一个规则允许 Teams.exe，则两个规则都将发送到客户端 。 此结果与通过用于防火墙设置的其他策略产生的冲突不同。

当来自多个规则配置文件的规则彼此不冲突时，设备会合并所有这些配置文件的规则，在设备上创建一个复合的防火墙规则配置。 通过此操作，可以将每个配置文件支持的 150 多个规则部署到设备。

- 例如，你有两个 Microsoft Defender 防火墙规则配置文件。 第一个配置文件允许 Teams.exe 通过防火墙。 第二个配置文件允许 Outlook.exe 通过防火墙。 当设备同时收到两个配置文件时，该设备将配置为同时允许两个应用通过防火墙。

## <a name="next-steps"></a>后续步骤

[配置终结点安全策略](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
