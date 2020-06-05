---
title: 使用 Microsoft Intune 中的终结点安全策略管理攻击面减少设置 | Microsoft Docs
description: 使用 Microsoft Intune 中的终结点安全攻击面减少策略设置，为你管理的设备配置和部署策略
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
ms.openlocfilehash: 20c8cc73e8037c0f394547b64d562cf75271240c
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431444"
---
# <a name="attack-surface-reduction-policy-for-endpoint-security-in-intune"></a>Intune 中终结点安全的攻击面减少策略

在 Windows 10 设备上使用 Defender 防病毒时，可以使用 Intune 终结点安全策略来减少攻击面，以管理设备的这些设置。

攻击面减少策略通过最小化组织易受网络威胁和攻击的地方，帮助减少攻击面。 有关详细信息，请参阅 Windows 威胁防护文档中的[攻击面减少概述]( https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/overview-attack-surface-reduction)。

在 [Microsoft endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)“终结点安全”节点的“管理”下，查找用于减少攻击面的终结点安全策略。 每个攻击面减少配置文件管理 Windows 10 设备特定区域的设置。

查看[攻击面减少配置文件的设置](../protect/endpoint-security-asr-profile-settings.md)。

## <a name="prerequisites-for-attack-surface-reduction-profiles"></a>攻击面减少配置文件的先决条件

- Windows 10 或更高版本
- Defender 防病毒必须是设备上的主要防病毒软件

## <a name="attack-surface-reduction-profiles"></a>攻击面减少配置文件

**Windows 10 配置文件**：

- **应用和浏览器隔离** - 作为 Defender ATP 的一部分，管理 Windows Defender 应用程序防护（以下简称应用程序防护）的设置。 应用程序防护有助于防止旧的和新出现的攻击，并可以将企业定义的站点隔离为不受信任的站点，同时定义受信任的站点、云资源和内部网络。

  要了解详细信息，请参阅 Microsoft Defender ATP 文档中的[应用程序防护](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/wd-app-guard-overview)。

- **Web 保护** - 你可以在 Microsoft Defender ATP 中管理用于 Web 保护的设置，这些设置可配置网络保护以保护计算机免受 Web 威胁。 通过与 Microsoft Edge 和常见的第三方浏览器（如 Chrome 和 Firefox）集成，Web 保护可以在没有 Web 代理的情况下阻止 Web 威胁，并可保护远程或本地计算机。 Web 保护会阻止对以下内容的访问：
  - 钓鱼网站
  - 恶意软件载体
  - 攻击网站
  - 不可信或低信誉网站
  - 已在自定义指标列表中阻止的网站。

  要了解详细信息，请参阅 Microsoft Defender ATP 文档中的 [Web 保护](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/web-protection-overview)。

- **应用程序控制** - 应用程序控制设置可以通过限制用户可运行的应用程序以及在系统内核中运行的代码来帮助缓解安全威胁。 管理可阻止未签名脚本和 MSI 的设置，并限制 Windows PowerShell 在受约束的语言模式下运行。

  要了解详细信息，请参阅 Microsoft Defender ATP 文档中的[应用程序控制](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control)。

- **攻击面减少规则** - 配置攻击表面减少规则的相关设置，专门针对恶意软件和恶意应用通常用来感染计算机的行为，包括：
  - 在 Office 应用或 Web 邮件中使用的试图下载或运行文件的可执行文件和脚本
  - 含义模糊或可疑的脚本
  - 应用通常不会在日常工作中启动的行为。减少攻击面意味着向攻击者提供更少的攻击方式。

  要了解更多信息，请参阅 Microsoft Defender ATP 文档中的[攻击面减少规则](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)。

- **设备控制** - 通过设备控制设置，可为设备配置分层方法，以保护可移动媒体。 Microsoft Defender ATP 提供了多种监视和控制功能，可帮助防止未经授权外围设备中的威胁危害你的设备。

  要了解更多信息，请参阅 Microsoft Defender ATP 文档中的[如何使用 Microsoft Defender ATP 控制 USB 设备和其他可移动媒体](https://docs.microsoft.com/windows/security/threat-protection/device-control/control-usb-devices-using-intune)。

- **Exploit Protection** - Exploit Protection 设置可以帮助抵御利用漏洞来感染设备并传播的恶意软件。 Exploit Protection 包括许多可应用于操作系统或单个应用的缓解措施。

  要了解详细信息，请参阅 Microsoft Defender ATP 文档中的[启用 Exploit Protection](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/enable-exploit-protection)。

## <a name="next-steps"></a>后续步骤

[配置终结点安全策略](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
