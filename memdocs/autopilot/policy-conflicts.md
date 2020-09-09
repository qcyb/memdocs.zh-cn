---
title: Windows Autopilot 策略冲突
ms.reviewer: ''
manager: laurawi
description: 向自己通知在 Windows Autopilot 部署过程中可能出现的策略冲突。
keywords: mdm, 设置, windows, windows 10, oobe, 管理, 部署, autopilot, ztd, 零接触, 合作伙伴, msfb, intune
ms.technology: windows
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
ms.openlocfilehash: 1f839f128dc869f7c9a4619237de0c33a21d66e1
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/09/2020
ms.locfileid: "89606578"
---
# <a name="windows-autopilot---policy-conflicts"></a>Windows Autopilot-策略冲突

**适用于**

- Windows 10

有大量适用于 Windows 10 的策略设置，其中包括：
- 本机 MDM 策略
- 组策略 (支持 ADMX 的) 设置

某些策略设置可能会导致一些 Windows Autopilot 方案中的问题。 由于策略如何更改 Windows 10 行为，因此可能会出现这些问题。 如果发现其中的任何问题，请删除相关策略以解决此问题。

<table>
<th>策略<th>详细信息

<tr><td width="50%">设备限制/ <a href="https://docs.microsoft.com/windows/client-management/mdm/devicelock-csp">密码策略</a></td>
<td>当设备在设备注册状态页 (ESP) 期间重新启动时， (OOBE) 或用户桌面自动登录可能会失败。 当某些 <a href="https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock">DeviceLock 策略</a> 应用到设备时，可能会发生此失败。 此类策略可能包括：<ul><li>最小密码长度和密码复杂性</li><li>任何类似的组策略设置 (包括禁用自动登录的任何设置) </li></ul>
对于自动生成密码的展台方案，此可能的失败尤其如此。</td>

<tr><td width="50%">Windows 10 安全基线/ <a href="/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions">管理员提升提示行为</a>
<br>Windows 10 安全基线/ <a href="https://docs.microsoft.com/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions">管理员批准模式</a></td>
<td>使用设备注册状态页 (ESP) 修改用户帐户控制 (UAC) 设置时，可能会出现更多提示。 如果设备在应用策略后重新启动，则更有可能出现提示增加的情况。 若要解决此问题，可以将策略定向到用户而不是设备，以便以后在此过程中应用。</td>

<tr><td width="50%">设备限制/云和存储/ <a href="https://docs.microsoft.com/mem/intune/configuration/device-restrictions-windows-10#cloud-and-storage">Microsoft 帐户登录助手</a></td>
<td>将此策略设置为 "已禁用" 将禁用 Microsoft 登录助手服务 (wlidsvc) 。 Windows Autopilot 需要此服务来获取 Windows Autopilot 配置文件。</td>

</table>

## <a name="related-topics"></a>相关主题

[Windows Autopilot 故障排除](troubleshooting.md)
