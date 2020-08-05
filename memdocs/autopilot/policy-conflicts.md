---
title: Windows Autopilot 策略冲突
ms.reviewer: ''
manager: laurawi
description: 就 Windows Autopilot 部署过程中可能出现的已知问题进行通知。
keywords: mdm, 设置, windows, windows 10, oobe, 管理, 部署, autopilot, ztd, 零接触, 合作伙伴, msfb, intune
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: mtniehaus
ms.author: mniehaus
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: 432656fc46d9b2a6e9cad6c8c9b7e287afc34b7b
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87756146"
---
# <a name="windows-autopilot---policy-conflicts"></a>Windows Autopilot-策略冲突

**适用于**

- Windows 10

适用于 Windows 10 的策略设置有很多，它们都是本机 MDM 策略和组策略 (ADMX 的) 设置。 其中一些可能会导致某些 Windows Autopilot 方案中的问题，因为它们如何更改 Windows 10 的行为。 如果遇到这些问题，请删除相关策略以解决问题。

<table>
<th>策略<th>详细信息

<tr><td width="50%">设备限制/<a href="https://docs.microsoft.com/windows/client-management/mdm/devicelock-csp">密码策略</a></td>
<td>如果某些<a href="https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock">DeviceLock 策略</a>（如最小密码长度和密码复杂性）或任何类似的组策略设置 (包括任何禁用自动登录) 的设备，并且在设备注册状态页 (ESP) 期间重新启动设备，则全新体验 (OOBE) 或用户桌面自动登录可能会意外失败。  对于自动生成密码的展台方案，尤其如此。</td>

<tr><td width="50%">Windows 10 安全基线/<a href="https://docs.microsoft.com/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions">管理员提升提示行为</a>
<br>Windows 10 安全基线/<a href="https://docs.microsoft.com/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions">管理员批准模式</a></td>
<td>当使用设备注册状态页 (ESP) 修改用户帐户控制 (UAC) 设置时，可能会导致其他 UAC 提示，尤其是在应用这些策略后设备重新启动时，使其生效。  若要解决此问题，可以将策略定向到用户而不是设备，以便以后在此过程中应用。</td>

<tr><td width="50%">设备限制/云和存储/ <a href="https://docs.microsoft.com/mem/intune/configuration/device-restrictions-windows-10#cloud-and-storage">Microsoft 帐户登录助手</a></td>
<td>将此策略设置为 "已禁用" 将禁用 Microsoft 登录助手服务 (wlidsvc) 。  Windows Autopilot 需要此服务来获取 Windows Autopilot 配置文件。</td>

</table>

## <a name="related-topics"></a>相关主题

[Windows Autopilot 故障排除](troubleshooting.md)
