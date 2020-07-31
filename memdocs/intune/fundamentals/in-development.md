---
title: 开发过程中 - Microsoft Intune
titleSuffix: ''
description: 开发过程中的 Microsoft Intune 功能
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/24/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: b55c8cced4e559655018b36843e1599cc6e2d1bf
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "87262731"
---
# <a name="in-development-for-microsoft-intune"></a>Microsoft Intune 开发过程中的功能

为了辅助就绪性和计划，此页面列出了正在开发但尚未发布的 Intune UI 更新和功能。 除本页上的信息外，另请注意： 

- 如果我们预计你需要在更改之前采取措施，我们将在 Office 消息中心发布补充性的文章。
- 当某个功能进入生产（无论是提供预览还是正式发布），其功能描述都将从本页移动到[新增功能](whats-new.md)。
- 此页和[新增功能页](whats-new.md)会定期更新。 返回查看其他更新。
- 有关策略性可交付内容和时间线，请参阅 [Microsoft 365 路线图](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS)。

> [!NOTE]
> 此页反映了我们目前希望在即将到来的版本中提供的 Intune 功能。 日期和各项功能可能会更改。 本页未介绍我们正在开发的全部功能。

**RSS 源**：通过将以下 URL 复制并粘贴到源阅读器中，可以在页面更新时收到通知：`https://docs.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us`

本文的上次更新日期在上面的标题下方列出。

<!--
## What's coming to Intune in the Azure portal 
## What's coming to Intune apps
## Notices
-->

<!-- Common categories:  
## App management
## Device configuration
## Device enrollment
## Device management
## Intune apps
## Monitor and troubleshoot
## Role-based access control
## Security

-->
 
<!-- ***********************************************-->
## <a name="app-management"></a>应用管理

### <a name="update-to-device-icons-in-company-portal-and-intune-apps-on-android---6057023----"></a>更新 Android 上公司门户和 Intune 应用中的设备图标<!-- 6057023  -->
我们正在更新 Android 设备上公司门户和 Intune 应用中的设备图标，以创建更加新式的外观，并与 Microsoft Fluent Design System 保持一致。 如需相关信息，请参阅[为 iOS/iPadOS 和 macOS 更新公司门户应用中的图标](../fundamentals/whats-new-app-ui.md#update-to-icons-in-company-portal-app-for-iosipados-and-macos-)。 

### <a name="ios-company-portal-will-support-apples-automated-device-enrollment-without-user-affinity---7282707----"></a>iOS 公司门户将支持 Apple 的自动设备注册，而无需用户关联<!-- 7282707  --> 
将支持在设备上使用 Apple 的自动设备注册来注册 iOS 公司门户，而无需分配的用户。 最终用户可以登录 iOS 公司门户，以在无需设备关联即可注册的 iOS/iPadOS 设备上将自己确立为主要用户。 若要详细了解自动设备注册，请参阅[使用 Apple 的自动设备注册自动注册 iOS/iPadOS 设备](../enrollment/device-enrollment-program-enroll-ios.md)。

### <a name="the-company-portal-adds-configuration-manager-application-support---4297660---"></a>公司门户现已开始支持 Configuration Manager 应用程序<!-- 4297660 -->
公司门户现在支持 Configuration Manager 应用程序。 借助此功能，最终用户可以在公司门户中同时看到 Configuration Manager 和 Intune 为共同受管理客户部署的应用程序。 此支持有助于管理员整合不同的最终用户门户体验。 有关详细信息，请参阅[在共同受管理设备上使用公司门户应用](https://docs.microsoft.com/mem/configmgr/core/get-started/2020/technical-preview-2006#bkmk_portal)。

<!-- ***********************************************-->
## <a name="device-configuration"></a>设备配置

### <a name="set-device-compliance-state-from-third-party-mdm-partners---6361689-----"></a>从第三方 MDM 合作伙伴设置设备合规状态<!-- 6361689   -->
拥有第三方 MDM 解决方案的 Microsoft 365 客户将能够通过与 Microsoft Intune 设备合规性服务的集成，为 iOS 和 Android 上的 Microsoft 365 应用强制实施条件访问策略。 第三方 MDM 供应商将利用 Intune 设备合规性服务向 Intune 发送设备合规性数据。 然后，Intune 将评估以确定设备是否受信任，并在 Azure AD 中设置条件访问属性。  客户将需要从 Microsoft Endpoint Manager 管理中心或 Azure AD 门户设置 Azure AD 条件访问策略。

### <a name="create-pkcs-certificate-profiles-for-android-enterprise-fully-managed-devices-cobo---4839686---"></a>为 Android Enterprise 完全托管设备创建 PKCS 证书配置文件 (COBO)<!-- 4839686 -->
你可以创建 PKCS 证书配置文件，以便将证书部署到 Android Enterprise 设备所有者和工作配置文件设备（“设备” > “配置文件” > “创建配置文件” > “Android Enterprise”>“仅限设备所有者”，或“Android Enterprise”>“仅限工作配置文件”[针对平台]>“PKCS”[针对配置文件]）。

不久，你将能够为 Android Enterprise 完全托管设备创建 PKCS 证书配置文件。 Intune PFX 证书连接器是必需的。 如果不使用 SCEP 并且只使用 PKCS，则可以在安装新的 PFX 连接器后删除 NDES 连接器。 新的 PFX 连接器导入 PFX 文件，并将 PKCS 证书部署到所有平台。

有关 PKCS 证书的详细信息，请参阅[配置 PKCS 证书并用于 Intune](../protect/certficates-pfx-configure.md)。

适用于：
- Android Enterprise 完全托管 (COBO)

### <a name="use-netmotion-as-a-vpn-connection-type-for-iosipados-and-macos-devices---1333631---"></a>将 NetMotion 用作 iOS/iPadOS 和 macOS 设备的 VPN 连接类型<!-- 1333631 -->
创建 VPN 配置文件时，NetMotion 将作为 VPN 连接类型（“设备” > “设备配置” > “创建配置文件” > “iOS/iPadOS”或“macOS”[针对平台] >“VPN”[针对配置文件] >“NetMotion”[针对连接类型]）。

有关 Intune 中 VPN 配置文件的详细信息，请参阅[创建 VPN 配置文件以连接到 VPN 服务器](../configuration/vpn-settings-configure.md)。

适用于：
- iOS/iPadOS
- macOS

### <a name="more-protected-extensible-authentication-protocol-peap-options-for-windows-10-wi-fi-profiles---3805024---"></a>适用于 Windows 10 Wi-Fi 配置文件的更受保护的可扩展身份验证协议 (PEAP) 选项<!-- 3805024 -->
在 Windows 10 设备上，可以使用可扩展身份验证协议 (EAP) 创建 Wi-Fi 配置文件来验证 Wi-Fi 连接（“设备” > “配置文件” > “创建配置文件” > “Windows 10 及更高版本”[针对平台] >“Wi-Fi”[针对配置文件] >“Enterprise”）。 选择“受保护的 EAP (PEAP)”时，可以使用新的设置：

- 在 PEAP 阶段 1 中执行服务器验证：在 PEAP 协商阶段 1 中，设备将验证证书，并验证服务器。
  - 在 PEAP 阶段 1 中禁止提示用户验证服务器：在 PEAP 协商阶段 1，未显示询问为受信任的证书颁发机构授权新 PEAP 服务器的用户提示。
- 需要加密绑定：阻止在 PEAP 协商期间连接到不使用加密绑定的 PEAP 服务器。

若要查看当前可配置的设置，请转到[添加适用于 Windows 10 及更高版本设备的 Wi-Fi 设置](../configuration/wi-fi-settings-windows.md)。

适用于： 
- Windows 10 及更高版本

### <a name="configure-the-macos-microsoft-enterprise-sso-plug-in---5627576---"></a>配置 macOS Microsoft 企业 SSO 插件<!-- 5627576 -->
Microsoft Azure AD 团队创建了重定向单一登录 (SSO) 应用扩展，让 macOS 10.15 以上的用户能够获取对支持 Apple SSO 功能的 Microsoft 应用、组织应用和网站的访问权限，并使用 Azure AD 通过一次登录进行身份验证。 在 Microsoft 企业 SSO 插件版本中，可以配置包含新的 Microsoft Azure AD 应用扩展类型的 SSO 扩展（“设备” > “配置文件” > “创建配置文件” > “macOS”[针对平台] >“设备功能”[针对配置文件] >“单一登录应用扩展”）>“SSO 应用扩展类型”>“Microsoft Azure AD”）。

若要实现具有 Microsoft Azure AD SSO 应用扩展类型的 SSO，用户需要在其 macOS 设备上安装公司门户应用并登录。 

有关 macOS SSO 应用扩展的详细信息，请参阅[单一登录应用扩展](../configuration/device-features-configure.md#single-sign-on-app-extension)。

适用于：
- macOS 10.15 及更高版本

### <a name="use-sso-app-extensions-on-more-iosipados-apps-with-the-microsoft-enterprise-sso-plug-in---7369991---"></a>在具有 Microsoft 企业 SSO 插件的更多 iOS/iPadOS 应用上使用 SSO 应用扩展<!-- 7369991 -->
[适用于 Apple 设备的 Microsoft 企业 SSO 插件](https://docs.microsoft.com/azure/active-directory/develop/apple-sso-plugin)可用于支持 SSO 应用扩展的所有应用。 在 Intune 中，此功能表示该插件适用于不使用适用于 Apple 设备的 Microsoft 身份验证库 (MSAL) 的移动 iOS/iPadOS 应用。 这些应用无需使用 MSAL，但需要使用 Azure AD 终结点进行身份验证。

若要将 iOS/iPadOS 应用配置为使用 SSO 和插件，在 iOS/iPadOS 配置文件中添加应用捆绑包标识符（“设备” > “配置文件” > “创建配置文件” > “iOS/iPadOS”[针对平台] >“设备功能”[针对配置文件] >“单一登录应用扩展” > “Microsoft Azure AD”[针对 SSO 应用扩展类型] >“应用捆绑包 ID”）。

若要查看可配置的当前 SSO 应用扩展设置，请参阅[单一登录应用扩展](../configuration/ios-device-features-settings.md#single-sign-on-app-extension)。

适用于：
- iOS/iPadOS

### <a name="improvement-to-update-device-settings-page-in-company-portal-app-for-android-to-show-descriptions---7414768---"></a>改进适用于 Android 的公司门户应用中的“更新设备设置”页面以显示说明<!-- 7414768 -->
在 Android 设备上的公司门户应用中，“更新设备设置”页面列出了用户需要更新以符合要求的设置。 我们已改进了用户体验，以便默认展开列出的设置，以显示说明和“解决”按钮（如果适用）。 以前，它们默认为折叠。 这一新的默认行为会减少单击次数，因此用户可以更快地解决问题。

<!-- ***********************************************-->
<!-- ## Device enrollment-->




<!-- ***********************************************-->
## <a name="device-management"></a>设备管理

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>对 BYOD 设备的 PowerShell 脚本支持<!-- 1862833  -->
PowerShell 脚本将支持 Intune 中已注册到 Azure AD 的设备。 有关 PowerShell 的详细信息，请参阅[在 Intune 中的 Windows 10 设备上使用 PowerShell 脚本](../apps/intune-management-extension.md)。 此功能不支持运行 Windows 10 家庭版的设备。

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics 将包括设备详细信息日志<!--6014987  -->
Intune 设备详细信息日志将在“报告” > “Log Analytics”中提供 。 可以关联设备详细信息以生成自定义查询和 Azure 工作簿。

### <a name="tenant-attach-device-timeline-in-the-admin-center--7220536-cm7141381---"></a>租户附加：管理中心内的设备时间线<!--7220536, CM7141381 -->
如果 Configuration Manager 通过租户附加将设备同步到 Microsoft Endpoint Manager，那么你将能够看到一个事件时间线。 此时间线显示设备上过去的活动，有助于排查问题。 有关详细信息，请参阅 [Configuration Manager 技术预览版 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_timeline)。  

### <a name="tenant-attach-install-an-application-from-the-admin-center---7220536-cm6024389---"></a>租户附加：从管理中心安装应用程序<!-- 7220536, CM6024389 -->
你将可以通过 Microsoft Endpoint Management 管理中心为租户附加的设备实时启动应用程序安装。 有关详细信息，请参阅 [Configuration Manager 技术预览版 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_apps)。

### <a name="tenant-attach-cmpivot-from-the-admin-center--7220536-cm6024392---"></a>租户附加：管理中心的 CMPivot<!--7220536, CM6024392 -->
你将能够将 [CMPivot](../../configmgr/tenant-attach/cmpivot-overview-attached.md) 的功能带入 Microsoft Endpoint Manager 管理中心。 允许其他人员（如支持人员）针对单个 ConfigMgr 托管设备从云启动实时查询，并将结果返回到管理中心。 它带来了 CMPivot 的所有传统优势，使 IT 管理员和其他指定的角色能够快速评估其环境中设备的状态并采取措施。 有关详细信息，请参阅 [Configuration Manager 技术预览版 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_cmpivot)。 

### <a name="tenant-attach-run-scripts-from-the-admin-center--7220536-cm6234688---"></a>租户附加：从管理中心运行脚本<!--7220536, CM6234688 -->
你将能够将 Configuration Manager 本地[运行脚本](../../configmgr/apps/deploy-use/create-deploy-scripts.md)这一强大功能引入到 Microsoft Endpoint Manager 管理中心。 允许其他角色（如支持人员）针对单个 Configuration Manager 托管设备从云中运行 PowerShell 脚本。 它提供了 PowerShell 脚本的所有传统优势，这些优势已由 Configuration Manager 管理员定义并批准进入这个新环境。 有关详细信息，请参阅 [Configuration Manager 技术预览版 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_scripts)。 

### <a name="new-merge-logic-for-windows-10-devices--179048--"></a>适用于 Windows 10 设备的新合并逻辑<!--179048-->
现在，如果客户对设备重置映像，然后重新注册该设备，则该设备的多条记录将显示在 Microsoft Endpoint Manager 管理控制台中。 新的合并逻辑正在开发中，用于合并 Windows 10 设备上的此类重复记录。

### <a name="deploy-software-updates-to-macos-devices----3194876---"></a>将软件更新部署到 macOS 设备 <!-- 3194876 -->
你将能够把软件更新部署到 macOS 设备组。 此功能包括关键更新、固件更新、配置文件更新和其他更新。 你将能够在下一次设备签入时发送更新，或选择每周计划在你设置的时间范围内外部署更新。 当你想要在非标准工作时间更新设备时，或者当支持人员已满员时，这会很有帮助。 你还将获得所有已部署更新的 macOS 设备的详细报告。 可以按设备向下钻取报告，以查看特定更新的状态。

### <a name="associated-licenses-revoked-before-deletion-of-apple-vpp-token--6195322---"></a>删除 Apple VPP 令牌之前撤销的关联许可证<!--6195322 -->
在将来的更新中，当你在 Microsoft Endpoint Manager 中删除 Apple VPP 令牌时，与该令牌关联的所有 Intune 分配的许可证将在删除之前自动撤销。

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>监视和故障排除

### <a name="power-bi-compliance-report-template-v20---636958----"></a>Power BI 合规性报告模板 V2.0<!-- 636958  -->
管理员能够将 Power BI 合规性报表模板的版本从 V1.0 更新到 V2.0。 V2.0 将包括改进后的设计，以及对作为模板一部分出现的计算和数据的更改。 如需了解相关信息，请参阅[使用 Power BI 连接到数据仓库](../developer/reports-proc-get-a-link-powerbi.md)。

<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
## <a name="security"></a>安全

### <a name="app-protection-policy-support-for-symantec-endpoint-security-and-check-point-sandblast----4452423-4731168---"></a>针对 Symantec Endpoint Security 和 Check Point Sandblast 的应用保护策略支持<!--  4452423, 4731168 -->

2019 年 10 月，Intune 应用保护策略新增了使用来自某些 Microsoft 威胁防御合作伙伴（MTD 合作伙伴）的数据的功能。 我们将开始支持以下合作伙伴，以使用应用保护策略来阻止或根据设备运行状况选择性地擦除用户的企业数据：

- Android、iOS 和 iPadOS 上的 Check Point Sandblast
- Android、iOS 和 iPadOS 上的 Symantec Endpoint Security

若要了解如何将应用保护策略与 MTD 合作伙伴配合使用，请参阅[使用 Intune 创建移动威胁防御应用保护策略](../protect/mtd-app-protection-policy.md)。

### <a name="microsoft-defender-atp-creates-endpoint-manager-security-task-with-vulnerability-details---5568193----"></a>Microsoft Defender ATP 创建具有漏洞详细信息的 Endpoint Manager 安全任务<!-- 5568193  -->
Microsoft Defender ATP 中的威胁和漏洞管理 (TVM) 发现设备上配置错误的安全设置。 管理员使用此信息更新易受攻击的设备。

不久，Microsoft Defender ATP 可能会引发具有漏洞详细信息的 Endpoint Manager 安全任务（“Endpoint Manager” > “终结点安全性” > “安全任务”），并显示受影响的设备。 IT 管理员可以接受安全任务，并部署所需的配置。 

有关安全任务的详细信息，请参阅[使用 Intune 修正由 Microsoft Defender ATP 标识的漏洞](../protect/atp-manage-vulnerabilities.md)。

### <a name="changes-for-endpoint-security-antivirus-policy-exclusions--5583940-6018119----"></a>终结点安全性防病毒策略排除项的更改<!--5583940, 6018119  -->
我们引入了两项更改，用于管理配置为终结点安全性防病毒策略一部分的 Microsoft Defender 防病毒排除项列表。 （“终结点安全性” > “防病毒” > “创建策略” > “Windows 10 及更高版本”[针对平台]）。 这两项更改有助于防止策略之间发生冲突，并且存在冲突的现有策略将不再与排除项列表冲突：

- 首先，我们要为 Windows 10 及更高版本添加新的配置文件类型：Microsoft Defender 防病毒排除项。  这一新的配置文件类型仅包括指定 Defender 进程列表的设置、文件扩展名以及不希望 Microsoft Defender 扫描的文件夹。    这可以通过将排除项列表与其他策略配置分离来帮助简化排除项列表的管理。
- 第二项更改是，根据应用于特定用户或设备的单个策略，在不同配置文件中定义的排除项列表将合并为每个设备或用户的单个排除项列表。 例如，如果针对具有三个不同策略的用户，则这三个策略中的排除项列表将合并为 Microsoft Defender 防病毒排除项的单一超集，然后将其应用于用户。 此合并包括正在添加的新配置文件类型的排除项列表，以及在 Microsoft Defender 防病毒配置文件中配置的任何现有策略的排除项列表。



<!-- ***********************************************-->
## <a name="notices"></a>通知

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>另请参阅

有关最近开发的详细信息，请参阅 [Microsoft Intune 中的新增功能](whats-new.md)。
