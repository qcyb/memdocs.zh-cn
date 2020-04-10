---
title: 适用于Microsoft Edge 的 Intune 安全基线设置
titleSuffix: Microsoft Intune
description: Intune 支持用于管理 Microsoft Edge 浏览器的安全基线设置
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/30/2019
ms.topic: reference
ms.service: microsoft-intune
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: shpate
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6108fc56b978c57bfc70b2bce9911f7901a01a3e
ms.sourcegitcommit: 0ad7cd842719887184510c6acd9cdfa290a3ca91
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/02/2020
ms.locfileid: "80551739"
---
# <a name="microsoft-edge-baseline-settings-for-intune"></a>适用于 Intune 的 Microsoft Edge 基线设置

请查看 Microsoft Intune 支持的 Microsoft Edge Web 浏览器基线设置。 Microsoft Edge 基线默认值表示针对 Microsoft Edge 浏览器的建议配置，可能与其他安全基线中的基线默认值不匹配。

> [!NOTE]
> Microsoft Edge 基线处于公共预览版状态。 

## <a name="microsoft-edge"></a>Microsoft Edge

- 阻止绕过适用于站点的 Microsoft Defender SmartScreen 提示   
  **默认值**：Enabled  
  Microsoft Edge CSP：[Browser/PreventSmartScreenPromptOverride](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)

  此策略设置使你可以决定用户是否可替代有关潜在恶意网站的 Microsoft Defender SmartScreen 警告。 
  - 如果启用此设置，则用户无法忽略 Microsoft Defender SmartScreen 警告，他们会被阻止继续访问站点。 
  - 如果禁用或未配置此设置，则用户可以忽略 Microsoft Defender SmartScreen 警告并继续访问站点。

- 已启用最低 SSL 版本   
  **默认值**：Enabled  

  设置 SSL 的最低支持版本。 如果将此策略设置为“未配置”  ，则 Microsoft Edge 会使用默认最低版本 TLS 1.0  。 设置为“已启用”  时，可以从以下值中选择最低版本：

  - TLS 1.0
  - TLS 1.1
  - TLS 1.2

  - 已启用最低 SSL 版本   
    **默认值**：TLS 1.2

- 阻止绕过有关下载的 Microsoft Defender SmartScreen 警报   
  **默认值**：Enabled  
  Microsoft Edge CSP：[Browser/PreventSmartScreenPromptOverrideForFiles](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)  

  此策略使你可以确定用户是否可以替代有关未验证下载的 Microsoft Defender SmartScreen 警告。
  - 如果启用此策略，则组织中的用户无法忽略 Microsoft Defender SmartScreen 警告，会被阻止完成未经验证的下载。
  - 如果禁用或未配置此策略，则用户可以忽略 Microsoft Defender SmartScreen 警告并完成未经验证的下载。

- 允许用户从 SSL 警报页继续   
  **默认值**：已禁用  
  Microsoft Edge CSP：[Browser/PreventCertErrorOverrides](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventcerterroroverrides)  

  当用户访问具有 SSL 错误的站点时，Microsoft Edge 将显示警告页。 如果将此策略设置为“已启用”  或“未配置”  ，则用户可以单击浏览这些警告页面。 当此策略设置为“已禁用”  时，用户会被阻止单击浏览任何警告页面。 

- 默认 Adobe Flash 设置   
  **默认值**：Enabled  
  Microsoft Edge CSP：[Browser/AllowFlash](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowflash) 和 [Browser/AllowFlashClickToRun](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowflashclicktorun)  

  确定未由“PluginsAllowedForUrls”或“PluginsBlockedForUrls”涵盖的网站是否可以自动运行 Adobe Flash 插件。 

  - 选择“BlockPlugins”可在所有站点上的阻止 dobe Flash
  - 选择“ClickToPlay”可让 Adobe Flash 运行，但要求用户单击占位符以启动它。
  
   在任何情况下，“PluginsAllowedForUrls”和“PluginsBlockedForUrls”策略都优先于“DefaultPluginsSetting”。 仅对于“PluginsAllowedForUrls”策略中显式列出的域，才允许进行自动播放。 
   如果要为所有站点启用自动播放，请考虑将 http://* 和 https://* 添加到此列表。 
   
   - 如果将此策略设置为“未配置”  ，则用户可以手动更改此设置。 * 2 = 阻止 Adobe Flash 插件 * 3 = 单击可播放；前面的“1” 选项设置 allow-all，但此功能现在仅由“PluginsAllowedForUrls”策略进行处理。 使用“1”的现有策略会在单击可播放模式下运行。  
 
  - 默认 Adobe Flash 设置   
    **默认值**：阻止 Adobe Flash 插件

- 对每个站点启用站点隔离   
  **默认值**：Enabled  

  “SitePerProcess”策略可以用于防止用户选择不使用隔离所有站点的默认行为。 你还可以使用 IsolateOrigins 策略隔离更细化的其他来源。

  - 将此策略设置为“已弃用”  ，用户无法选择退出默认行为（其中每个站点都在自己的进程中运行）。 
  - 如果使用“已禁用”或“未配置”，则用户可以选择退出站点隔离   。 （例如，在 edge://flags 中使用“Disable site isolation”。）禁用策略或不配置策略不会关闭站点隔离。

- 支持的身份验证方案   
  **默认值**：Enabled  

  指定支持的 HTTP 身份验证方案。 可以使用以下值配置策略：“基本”、“摘要”、“ntlm”和“协商”。 用逗号分隔多个值。 如果未配置此策略，则使用所有这四个方案。
 
  - 支持的身份验证方案   
    选择从以下选项： 
    - 基本
    - 摘要
    - NTLM  （已默认选择）
    - 协商（已默认选择） 

- 允许将密码保存到密码管理器   
  **默认值**：已禁用  
  Microsoft Edge CSP：[Browser/AllowPasswordManager](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)  

  使 Microsoft Edge 可以保存用户密码。 
  - 如果启用此策略，则用户可以在 Microsoft Edge 中保存其密码。 下次访问该站点时，Microsoft Edge 会自动输入该密码。 
  - 如果禁用此策略，则用户无法保存新密码，但仍可使用以前保存的密码。 
  
  将此策略设置为“已启用”  或“已禁用”  时，用户无法在 Microsoft Edge 中更改或替代此策略。 
  
  如果将此项设置为“未配置”  ，则用户可以保存密码，以及关闭此功能。

- 控制不可安装哪些扩展   
  **默认值**：Enabled  

  列出用户无法在 Microsoft Edge 中安装的特定扩展。 部署此策略时，会禁用此列表上以前安装的任何扩展，用户将无法启用它们。 如果从已阻止扩展列表中删除某个项目，则会在之前安装该扩展的任何位置处自动重新启用该扩展。
  
  使用 **\*** 可阻止在允许列表中未显式列出的所有扩展。 如果将此策略设置为“未配置”  ，则用户可以在 Microsoft Edge 中安装任何扩展。 
  
  示例值：extension_id1 extension_id2。  
  <br>
  - 应阻止用户安装的扩展 ID (或用 * 表示全部)   
    选择“添加”  并指定其他扩展。 **\*** 默认处于选中状态。

- 配置 Microsoft Defender SmartScreen   
  **默认值**：Enabled  
  Microsoft Edge CSP：[Browser/AllowSmartScreen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)  
  
  此策略设置使你可以配置是否启用 Microsoft Defender SmartScreen。 Microsoft Defender SmartScreen 提供警告消息，可帮助用户防范潜在网络钓鱼诈骗和恶意软件。 
  
  - 默认情况下，Microsoft Defender SmartScreen 处于开启状态。 如果启用此设置，则会打开 Microsoft Defender SmartScreen，用户无法将其关闭。
  - 如果禁用此设置，则会关闭 Microsoft Defender SmartScreen，用户无法将其打开。 
  - 设置为“未配置”  ，用户可以选择是否要使用 Microsoft Defender SmartScreen。 
  
  此策略仅适用于加入 Microsoft Active Director 域的 Windows 实例，或已注册进行设备管理的 Windows 10 专业版或企业实例。

- 允许用户级本机消息传递主机(不使用管理员权限安装)   
  **默认值**：已禁用  

  启用本机消息传递主机的用户级别安装。 
  - 如果禁用此策略，则 Microsoft Edge 仅使用在系统级别上安装的本机消息传递主机。 默认情况下，如果未配置此策略，则 Microsoft Edge 允许使用用户级别本机消息传递主机。

## <a name="next-steps"></a>后续步骤

- [了解安全基线](security-baselines.md)
- [避免冲突](security-baselines.md#avoid-conflicts)
- [在 Intune 中对策略和配置文件进行故障排除](../configuration/troubleshoot-policies-in-microsoft-intune.md)
