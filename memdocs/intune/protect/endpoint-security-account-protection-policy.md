---
title: 使用 Microsoft Intune 中的终结点安全策略管理攻击帐户保护设置 | Microsoft Docs
description: 使用 Microsoft Endpoint Manager 中的终结点安全帐户保护策略设置为你管理的设备配置和部署策略。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
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
ms.openlocfilehash: 6fb5702b7c809c7810004a53d084f19fa94dea9e
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431847"
---
# <a name="account-protection-policy-for-endpoint-security-in-intune"></a>Intune 中的终结点安全帐户保护策略

使用用于帐户保护的 Intune 终结点安全策略来保护用户的身份和帐户。 帐户保护策略侧重于 Windows Hello 和 Credential Guard 的设置，这是 Windows 身份和访问管理的一部分。

- Windows Hello 企业版将电脑和移动设备上的密码替换成了强双重身份验证。
- Credential Guard 有助于保护你在设备中使用的凭据和密码。

若要了解详细信息，请参阅 Windows 标识和访问管理文档中的[标识和访问管理](https://docs.microsoft.com/windows/security/identity-protection/)。

在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)“终结点安全”节点的“管理”下，查找用于帐户保护的终结点安全策略。

查看[帐户保护配置文件设置](../protect/endpoint-security-asr-profile-settings.md)。

## <a name="prerequisites-for-account-protection-profiles"></a>帐户保护配置文件的先决条件

- Windows 10 或更高版本

## <a name="account-protection-profiles"></a>帐户保护配置文件

帐户保护配置文件目前以预览版提供。

**Windows 10 配置文件**：

- 帐户保护（预览版）– 适用于帐户保护策略的设置有助于保护用户凭据。

## <a name="next-steps"></a>后续步骤

[配置终结点安全策略](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
