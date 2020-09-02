---
title: 适用于Microsoft Edge 的 Intune 安全基线设置
titleSuffix: Microsoft Intune
description: Intune 支持用于管理 Microsoft Edge 浏览器的安全基线设置
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/17/2020
ms.topic: reference
ms.service: microsoft-intune
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
zone_pivot_groups: edge-baseline-versions
ms.reviewer: laarrizz
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8fd6943be69f66d4cd6fde2e9c08bec9323005a5
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914423"
---
<!-- Pivots in use: 
::: zone pivot="edge-october-2019"
::: zone-end

::: zone pivot="edge-april-2020"
::: zone-end

::: zone pivot="edge-october-2019,edge-april-2020"
::: zone-end
-->

# <a name="microsoft-edge-baseline-settings-for-intune"></a>适用于 Intune 的 Microsoft Edge 基线设置

请查看 Microsoft Intune 支持的 Microsoft Edge Web 浏览器基线设置。 Microsoft Edge 基线默认值表示针对 Microsoft Edge 浏览器的建议配置，可能与其他安全基线中的基线默认值不匹配。

::: zone pivot="edge-october-2019"

> [!NOTE]
> 2019 年 10 月的 Microsoft Edge 基线是公共预览版。

::: zone-end
::: zone pivot="edge-april-2020"

要了解此版本基线相对于以前版本的变化情况，请使用[比较基线](../protect/security-baselines.md#compare-baseline-versions)操作，该操作在查看此基线的“版本”窗格时可用。

::: zone-end
::: zone pivot="edge-october-2019,edge-april-2020"

## <a name="microsoft-edge"></a>Microsoft Edge

::: zone-end
::: zone pivot="edge-april-2020"

- 支持的身份验证方案  
  指定支持的 HTTP 身份验证方案。 可以使用下面这些值来配置策略：“基本”、“摘要式”、“NTLM”和“协商”。 用逗号分隔多个值。 如果未配置此策略，则使用所有这四个方案。

  - 已启用（默认）- 使用你选择的方案。
  - **禁用**
  - 未配置 - 使用所有四个方案。
  
  如果设置为“已启用”，可以配置以下设置，即选择要使用哪个身份验证：

  - 支持的身份验证方案  
    选择从以下选项：
    - 基本
    - 摘要式
    - NTLM（默认选中）
    - 协商（默认选中）

- 默认 Adobe Flash 设置  
  CSP：[Browser/AllowFlash](/windows/client-management/mdm/policy-csp-browser#browser-allowflash) 和 [Browser/AllowFlashClickToRun](/windows/client-management/mdm/policy-csp-browser#browser-allowflashclicktorun)

  允许配置以下设置，即配置运行 Adobe Flash 插件的行为。  

  - 已启用（默认）
  - **禁用**
  - 未配置

  如果设置为“已启用”，可以配置以下设置。

  - 默认 Adobe Flash 设置

    - 阻止 Adobe Flash 插件（默认）- 在所有站点上阻止 Adobe Flash
    - 单击可播放 - Adobe Flash 运行，但用户必须选择选项才能启动它。

- 控制不可安装哪些扩展  
  允许使用列表来指定用户无法在 Microsoft Edge 中安装的特定扩展。 如果使用列表，列表上以前安装的任何设置都会被禁用，且用户无法启用它们。 如果从已阻止扩展列表中删除某个项目，则会在之前安装该扩展的任何位置处自动重新启用该扩展。

  - 已启用（默认）- 允许使用列表来阻止扩展。
  - **禁用**
  - 未配置 - 用户可以在 Microsoft Edge 中安装任何扩展。
  
  如果设置为“已启用”，可以配置以下设置，即定义要阻止的扩展列表。

  - 应阻止用户安装的扩展 ID (或用 * 表示全部)

    选择“添加”并指定其他扩展。 **\*** 默认处于选中状态。

- 允许用户级本机消息传递主机(不使用管理员权限安装)  
  启用本机消息传递主机的用户级别安装。

  - **Enabled**
  - 已禁用（默认）- Microsoft Edge 只使用在系统级安装的本机消息传递主机。
  - 未配置 - Microsoft Edge 默认允许使用用户级本机消息传递主机。

- 允许将密码保存到密码管理器  
  Microsoft Edge CSP：[Browser/AllowPasswordManager](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)  

  使 Microsoft Edge 可以保存用户密码。

  - 已启用 - 用户可以在 Microsoft Edge 中保存密码。 下次访问该站点时，Microsoft Edge 会自动输入该密码。 用户无法在 Microsoft Edge 中更改或替代此策略。
  - 已禁用（默认）- 用户无法保存新密码，但可以继续使用以前保存的密码。 用户无法在 Microsoft Edge 中更改或替代此策略。
  - 未配置 - 用户可以保存密码，并禁用此功能。

- 阻止绕过适用于站点的 Microsoft Defender SmartScreen 提示  
  CSP：[Browser/PreventSmartScreenPromptOverride](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)

  决定用户能否替代有关潜在恶意网站的 Microsoft Defender SmartScreen 警告。

  - 已启用（默认）- 用户无法忽略 Microsoft Defender SmartScreen 警告，他们会被阻止继续访问站点。
  - 已禁用 - 用户可以忽略 Microsoft Defender SmartScreen 警告，并继续访问站点。
  - 未配置 - 用户可以忽略 Microsoft Defender SmartScreen 警告，并继续访问站点

- 阻止绕过有关下载的 Microsoft Defender SmartScreen 警报  
  CSP：[Browser/PreventSmartScreenPromptOverrideForFiles](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)  

  决定用户能否替代有关未验证下载的 Microsoft Defender SmartScreen 警告。

  - 已启用（默认）- 用户无法忽略 Microsoft Defender SmartScreen 警告，会被阻止完成未验证下载。
  - 已禁用 - 用户可以忽略 Microsoft Defender SmartScreen 警告，并完成未验证下载。
  - 未配置 - 用户可以忽略 Microsoft Defender SmartScreen 警告，并完成未验证下载。

- 对每个站点启用站点隔离  
  配置站点隔离，以防用户选择退出隔离所有站点的默认行为。
  
  - 已启用（默认）- 用户无法选择退出默认行为（即每个站点都在自己的进程中运行）。
  - 已禁用 - 用户可以选择退出站点隔离。 站点隔离未禁用。
  - 未配置 - 用户可以选择退出站点隔离。 站点隔离未禁用。

  Microsoft Edge 还支持 [IsolateOrigins](/deployedge/microsoft-edge-policies#isolateorigins) 策略，可用于隔离更细化的其他源。  Intune 不支持配置 IsolateOrigins 策略。
  
- 配置 Microsoft Defender SmartScreen  
  CSP：[Browser/AllowSmartScreen](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)  
  
  Microsoft Defender SmartScreen 提供警告消息，有助于保护用户免受潜在钓鱼式欺诈和恶意软件威胁。 默认情况下，Microsoft Defender SmartScreen 处于开启状态。
  
  - 已启用（默认）- Microsoft Defender SmartScreen 已启用，且用户无法禁用它。
  - 已禁用 - Microsoft Defender SmartScreen 已禁用，且用户无法启用它。
  - 未配置 - 用户可以选择是否使用 Microsoft Defender SmartScreen。

  此策略仅适用于加入 Microsoft Active Director 域的 Windows 实例，或已注册进行设备管理的 Windows 10 专业版或企业实例。

- **将 Microsoft Defender SmartScreen 配置为阻止可能不需要的应用**  
    配置阻止可能不需要的应用的 Microsoft Defender SmartScreen 行为。 Microsoft Defender SmartScreen 可以提供警告消息，有助于保护用户免受广告程序、CoinMiner、捆绑程序以及网站托管的其他低信誉应用威胁。 Microsoft Defender SmartScreen 中的“阻止可能不需要的应用”默认处于禁用状态。

  - 已启用（默认）- 阻止可能不需要的应用。
  - 已禁用 - 不阻止可能不需要的应用。
  - 未配置 - 用户可以选择是否使用 Microsoft Defender SmartScreen 中的“阻止可能不需要的应用”。

  此策略仅适用于加入 Microsoft Active Director 域的 Windows 实例，或已注册进行设备管理的 Windows 10 专业版或企业实例。

- 允许用户从 SSL 警报页继续  
   CSP：[Browser/PreventCertErrorOverrides](/windows/client-management/mdm/policy-csp-browser#browser-preventcerterroroverrides)  

  当用户访问具有 SSL 错误的站点时，Microsoft Edge 将显示警告页。
  - 已启用 - 用户可以单击后转到警告页。
  - 已禁用（默认）- 用户被阻止单击后转到任何警告页。
  - 未配置 - 用户可以单击后转到这些警告页。

- 已启用最低 SSL 版本  
  启用选项，以设置支持的 SSL 最低版本。

  - 已启用（默认）- 允许配置下一个设置，即指定要使用的 TLS 最低版本。
  - **禁用**
  - 未配置 - Microsoft Edge 使用默认最低版本，即 TLS 1.0。

  如果设置为“已启用”，可以使用以下设置来配置 TLS。

  - 已启用最低 SSL 版本 - 设置要使用的 TLS 最低版本。 Microsoft Edge 不会使用任何低于指定版本的 SSL/TLS 版本。
    - TLS 1.0
    - TLS 1.1
    - TLS 1.2（默认）

::: zone-end

::: zone pivot="edge-october-2019"

- 阻止绕过适用于站点的 Microsoft Defender SmartScreen 提示  
  **默认值**：Enabled  
  Microsoft Edge CSP：[Browser/PreventSmartScreenPromptOverride](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)

  此策略设置使你可以决定用户是否可替代有关潜在恶意网站的 Microsoft Defender SmartScreen 警告。 
  - 如果启用此设置，则用户无法忽略 Microsoft Defender SmartScreen 警告，他们会被阻止继续访问站点。 
  - 如果禁用或未配置此设置，则用户可以忽略 Microsoft Defender SmartScreen 警告并继续访问站点。

- 已启用最低 SSL 版本  
  **默认值**：Enabled  

  设置 SSL 的最低支持版本。 如果将此策略设置为“未配置”，则 Microsoft Edge 会使用默认最低版本 TLS 1.0。 设置为“已启用”时，可以从以下值中选择最低版本：

  - TLS 1.0
  - TLS 1.1
  - TLS 1.2

  - 已启用最低 SSL 版本  
    **默认值**：TLS 1.2

- 阻止绕过有关下载的 Microsoft Defender SmartScreen 警报  
  **默认值**：Enabled  
  Microsoft Edge CSP：[Browser/PreventSmartScreenPromptOverrideForFiles](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)  

  此策略使你可以确定用户是否可以替代有关未验证下载的 Microsoft Defender SmartScreen 警告。
  - 如果启用此策略，则组织中的用户无法忽略 Microsoft Defender SmartScreen 警告，会被阻止完成未经验证的下载。
  - 如果禁用或未配置此策略，则用户可以忽略 Microsoft Defender SmartScreen 警告并完成未经验证的下载。

- 允许用户从 SSL 警报页继续  
  **默认值**：已禁用  
  Microsoft Edge CSP：[Browser/PreventCertErrorOverrides](/windows/client-management/mdm/policy-csp-browser#browser-preventcerterroroverrides)  

  当用户访问具有 SSL 错误的站点时，Microsoft Edge 将显示警告页。 如果将此策略设置为“已启用”或“未配置”，则用户可以单击浏览这些警告页面。 当此策略设置为“已禁用”时，用户会被阻止单击浏览任何警告页面。 

- 默认 Adobe Flash 设置  
  **默认值**：Enabled  
  Microsoft Edge CSP：[Browser/AllowFlash](/windows/client-management/mdm/policy-csp-browser#browser-allowflash) 和 [Browser/AllowFlashClickToRun](/windows/client-management/mdm/policy-csp-browser#browser-allowflashclicktorun)  

  确定未由“PluginsAllowedForUrls”或“PluginsBlockedForUrls”涵盖的网站是否可以自动运行 Adobe Flash 插件。 

  - 选择“BlockPlugins”可在所有站点上的阻止 dobe Flash
  - 选择“ClickToPlay”可让 Adobe Flash 运行，但要求用户单击占位符以启动它。
  
  在任何情况下，“PluginsAllowedForUrls”和“PluginsBlockedForUrls”策略都优先于“DefaultPluginsSetting”。 仅对于“PluginsAllowedForUrls”策略中显式列出的域，才允许进行自动播放。 
   如果要为所有站点启用自动播放，请考虑将 http://* 和 https://* 添加到此列表。

  - 如果将此策略设置为“未配置”，则用户可以手动更改此设置。 * 2 = 阻止 Adobe Flash 插件 * 3 = 单击可播放；前面的“1” 选项设置 allow-all，但此功能现在仅由“PluginsAllowedForUrls”策略进行处理。 使用“1”的现有策略会在单击可播放模式下运行。  

  - 默认 Adobe Flash 设置  
    **默认值**：阻止 Adobe Flash 插件

- 对每个站点启用站点隔离  
  **默认值**：Enabled  

  “SitePerProcess”策略可以用于防止用户选择不使用隔离所有站点的默认行为。 你还可以使用 IsolateOrigins 策略隔离更细化的其他来源。

  - 将此策略设置为“已弃用”，用户无法选择退出默认行为（其中每个站点都在自己的进程中运行）。 
  - 如果使用“已禁用”或“未配置”，则用户可以选择退出站点隔离 。 （例如，在 edge://flags 中使用“Disable site isolation”。）禁用策略或不配置策略不会关闭站点隔离。

- 支持的身份验证方案  
  **默认值**：Enabled  

  指定支持的 HTTP 身份验证方案。 可以使用以下值配置策略：“基本”、“摘要”、“ntlm”和“协商”。 用逗号分隔多个值。 如果未配置此策略，则使用所有这四个方案。

  - 支持的身份验证方案  
    选择从以下选项：
    - 基本
    - 摘要
    - NTLM（已默认选择）
    - 协商（已默认选择）

- 允许将密码保存到密码管理器  
  **默认值**：已禁用  
  Microsoft Edge CSP：[Browser/AllowPasswordManager](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)  

  使 Microsoft Edge 可以保存用户密码。
  - 如果启用此策略，则用户可以在 Microsoft Edge 中保存其密码。 下次访问该站点时，Microsoft Edge 会自动输入该密码。
  - 如果禁用此策略，则用户无法保存新密码，但仍可使用以前保存的密码。
  
  将此策略设置为“已启用”或“已禁用”时，用户无法在 Microsoft Edge 中更改或替代此策略。
  
  如果将此项设置为“未配置”，则用户可以保存密码，以及关闭此功能。

- 控制不可安装哪些扩展  
  **默认值**：Enabled  

  列出用户无法在 Microsoft Edge 中安装的特定扩展。 部署此策略时，会禁用此列表上以前安装的任何扩展，用户将无法启用它们。 如果从已阻止扩展列表中删除某个项目，则会在之前安装该扩展的任何位置处自动重新启用该扩展。
  
  使用 **\*** 可阻止在允许列表中未显式列出的所有扩展。 如果将此策略设置为“未配置”，则用户可以在 Microsoft Edge 中安装任何扩展。
  
  示例值：extension_id1 extension_id2。  
  <br>
  - 应阻止用户安装的扩展 ID (或用 * 表示全部)  
    选择“添加”并指定其他扩展。 **\*** 默认处于选中状态。

- 配置 Microsoft Defender SmartScreen  
  **默认值**：Enabled  
  Microsoft Edge CSP：[Browser/AllowSmartScreen](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

  此策略设置使你可以配置是否启用 Microsoft Defender SmartScreen。 Microsoft Defender SmartScreen 提供警告消息，可帮助用户防范潜在网络钓鱼诈骗和恶意软件。
  
  - 默认情况下，Microsoft Defender SmartScreen 处于开启状态。 如果启用此设置，则会打开 Microsoft Defender SmartScreen，用户无法将其关闭。
  - 如果禁用此设置，则会关闭 Microsoft Defender SmartScreen，用户无法将其打开。
  - 设置为“未配置”，用户可以选择是否要使用 Microsoft Defender SmartScreen。
  
  此策略仅适用于加入 Microsoft Active Director 域的 Windows 实例，或已注册进行设备管理的 Windows 10 专业版或企业实例。

- 允许用户级本机消息传递主机(不使用管理员权限安装)  
  **默认值**：已禁用

  启用本机消息传递主机的用户级别安装。 
  - 如果禁用此策略，则 Microsoft Edge 仅使用在系统级别上安装的本机消息传递主机。 默认情况下，如果未配置此策略，则 Microsoft Edge 允许使用用户级别本机消息传递主机。

::: zone-end

## <a name="next-steps"></a>后续步骤

- [了解安全基线](security-baselines.md)
- [避免冲突](security-baselines.md#avoid-conflicts)
- [在 Intune 中对策略和配置文件进行故障排除](../configuration/troubleshoot-policies-in-microsoft-intune.md)