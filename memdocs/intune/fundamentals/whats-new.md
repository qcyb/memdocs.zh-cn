---
title: Microsoft Intune 中的新增功能 - Azure | Microsoft Docs
titleSuffix: ''
description: 了解 Intune Azure 门户新增功能
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/04/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 791ed23f-bd13-4ef0-a3dd-cd2d7332c5cc
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5b3c8287d9b5ca2d46094d04ee2179128bead4a8
ms.sourcegitcommit: 0dafd513a59afe592b5cfe2a80b6288020dc5bf0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2020
ms.locfileid: "82991744"
---
# <a name="whats-new-in-microsoft-intune"></a>Microsoft Intune 新增功能

在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)了解 Microsoft Intune 每周新增功能。 还可以找到[重要通知](#notices)、[过去版本](whats-new-archive.md)，以及有关[如何发布 Intune 服务更新](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728)的信息。 

> [!Note]
> 每个[每月更新](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728)可能需要长达三天才能推出，顺序如下：
>
> - 第 1 天：亚太地区 (APAC)
> - 第 2 天：欧洲、中东和非洲 (EMEA)
> - 第 3 天：北美
> - 第 4 天之后：Intune for Government
>
> 某些功能可能会在数周内推出，第一周内可能不能供所有客户使用。
>
> 有关版本中即将推出的功能的列表，请查看[开发过程中页面](in-development.md)。

**RSS 源**：通过将以下 URL 复制并粘贴到源阅读器中，可以在页面更新时收到通知：`https://docs.microsoft.com/api/search/rss?search=%22What%27s+new+in+microsoft+intune%3F+-+Azure%22&locale=en-us`

<!-- Common categories:  
### App management
### Device configuration
### Device enrollment
### Device management
### Device security
### Intune apps
### Monitor and troubleshoot

<!-- ########################## -->
## <a name="week-of-may-4-2020"></a>2020 年 5 月 4 日当周  

<!-- vvvvvvvvvvvvvvvvvvvvvv -->  

### <a name="company-portal-for-android-guides-users-to-get-apps-after-work-profile-enrollment----6103999---"></a>适用于 Android 的公司门户可指导用户在注册了工作配置文件后获取应用 <!-- 6103999 -->
我们改进了公司门户中的应用内指南，可便于用户更轻松地查找和安装应用。 注册工作配置文件管理后，用户将看到一条说明如何在徽章版 Google Play 中查找建议的应用的消息。 [使用 Android 配置文件注册设备](../user-help/enroll-device-android-work-profile.md)中的最后一步已更新为显示这条新消息。 用户还将在左侧的公司门户抽屉中看到新的“获取应用”  链接。 为了给这些新体验和改进体验腾出地方，“应用”  选项卡已被删除。 若要查看更新后的屏幕，请转到 [Intune 最终用户应用的 UI 更新](./whats-new-app-ui.md)。 

<!-- ########################## -->
## <a name="week-of-april-20-2020"></a>2020 年 4 月 20 日当周

<!-- vvvvvvvvvvvvvvvvvvvvvv -->

### <a name="device-management"></a>设备管理

#### <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions---6317104-cm3555758-idready---"></a>Microsoft Endpoint Manager 租户附加：设备同步和设备操作<!-- 6317104, CM3555758 idready -->
Microsoft 终结点管理器将 Configuration Manager 和 Intune 组合为单个控制台。 从 Configuration Manager 版本 2002 开始，可在管理中心将 Configuration Manager 设备上传到云服务并对它们执行操作。 有关详细信息，请参阅 [Microsoft Endpoint Manager 租户附加：设备同步和设备操作](../../configmgr/tenant-attach/device-sync-actions.md)。 

### <a name="app-management"></a>应用管理

#### <a name="microsoft-office-365-proplus-rename---6368143---"></a>Microsoft Office 365 专业增强版重命名<!-- 6368143 -->
Microsoft Office 365 专业增强版将重命名为 Microsoft 365 企业应用版  。 要了解详细信息，请参阅 [Office 365 专业增强版的名称变更](https://docs.microsoft.com/deployoffice/name-change)。 在我们的文档中，我们通常将它称为 Microsoft 365 应用版。 在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，可选择“应用” > “Windows” > “添加”来查找应用套件    。 要了解如何添加应用，请参阅[向 Microsoft Intune 添加应用](../apps/apps-add.md)。

<!-- ########################## -->
## <a name="week-of-april-13-2020-2004-service-release"></a>2020 年 4 月 13 日当周（2004 服务版本）

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>应用管理

#### <a name="manage-smime-settings-for-outlook-on-android-enterprise-devices---6517085-----"></a>在 Android Enterprise 设备上管理 Outlook 的 S/MIME 设置<!-- 6517085   -->
可以使用应用配置策略在运行 Android Enterprise 的设备上管理 Outlook 的 S/MIME 设置。 还可以选择是否允许设备用户在 Outlook 设置中启用或禁用 S/MIME。 若要使用适用于 Android 的应用配置策略，请在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)内，依次转到“应用”   > “应用配置策略”   > “添加”   > “受管理设备”  。 若要详细了解如何配置 Outlook 设置，请参阅 [Microsoft Outlook 配置设置](../apps/app-configuration-policies-outlook.md)。

#### <a name="pre-release-testing-for-managed-google-play-apps---2681933----"></a>托管的 Google Play 应用的预发布测试<!-- 2681933  -->
如果组织使用 [Google Play 的应用预发布测试的封闭式测试轨道](https://support.google.com/googleplay/android-developer/answer/3131213)，可以使用 Intune 管理这些轨道。 你可以有选择性地将发布到 Google Play 预生产轨道的应用分配给试点组，从而执行测试。 在 Intune 中，可以查看是否向应用发布了预生产内部版本测试轨道，并能将此轨道分配给 AAD 用户或设备组。 此功能适用于我们当前支持的所有 Android Enterprise 方案（工作配置文件、完全托管和专用）。 在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)内，可以依次选择“应用”   > “Android”   > “添加”  ，从而添加托管的 Google Play 应用。 有关详细信息，请参阅[处理托管的 Google Play 封闭式测试轨道](../apps/apps-add-android-for-work.md#working-with-managed-google-play-closed-testing-tracks)。

#### <a name="microsoft-teams-is-now-included-in-the-office-365-suite-for-macos---5903936----"></a>Microsoft Teams 现已包含在适用于 macOS 的 Office 365 套件中<!-- 5903936  -->
除了现有的 Microsoft Office 应用（Word、Excel、PowerPoint、Outlook 和 OneNote）外，在 Microsoft Endpoint Manager 中分配有 Microsoft Office for macOS 的用户现在还会获得 Microsoft Teams。 Intune 将识别已安装其他 Office for macOS 应用的现有 Mac 设备，并在下次设备使用 Intune 签入时尝试安装 Microsoft Teams。 在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，可以通过选择“应用” > “macOS” > “添加”来查找适用于 macOS 的 Office 365 套件     。 有关详细信息，请参阅[使用 Microsoft Intune 将 Office 365 分配给 macOS 设备](../apps/apps-add-office365-macos.md)。

#### <a name="update-to-android-app-configuration-policies---6113334----"></a>更新到 Android 应用配置策略<!-- 6113334  -->
Android 应用配置策略已更新为，允许管理员在创建应用配置文件前选择设备注册类型。 此功能将添加到基于注册类型（工作配置文件或设备所有者）的证书配置文件帐户中。  此更新包括以下内容：

1. 如果新建了配置文件，并为设备注册类型选择了“工作配置文件”和“设备所有者配置文件”，则无法关联证书配置文件与应用配置策略。
2. 如果已创建新的配置文件，并且选择了仅“工作配置文件”，那么可以使用在设备配置下创建的工作配置文件证书策略。
3. 如果已创建新的配置文件，并且选择了仅“设备所有者”，那么可以使用在设备配置下创建的设备所有者证书策略。 

> [!IMPORTANT]
> 在此功能发布前（2004 年 - 2020 年 4 月版本）创建的且没有与任何证书配置文件关联的现有策略，将默认为设备注册类型选择“工作配置文件”和“设备所有者配置文件”。 另外，在此功能发布前创建的且与证书配置文件关联的现有策略，将默认为设备注册类型只选择“工作配置文件”。

此外，我们还将添加 Gmail 和 Nine 电子邮件配置文件，它们将同时适用于“工作配置文件”和“设备所有者配置文件”注册类型，包括对这两种电子邮件配置类型使用证书配置文件。  在“工作配置文件”的“设备配置”下创建的任何 Gmail 或 9 个策略将继续应用于设备，没有必要将它们移动到应用配置策略。

在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)内，可以依次选择“应用”   > “应用配置策略”  ，从而查找应用配置策略。 若要详细了解应用配置策略，请参阅 [Microsoft Intune 的应用配置策略](../apps/app-configuration-policies-overview.md)。

#### <a name="push-notification-when-device-ownership-type-is-changed---5575875---"></a>更改设备所有权类型时的推送通知<!-- 5575875 -->
可以配置推送通知，以在 Android 和 iOS 公司门户用户的设备所有权类型因隐私保护原因从“个人”更改为“企业”时发送给他们。 此推送通知默认设为“关”。 在 Microsoft Endpoint Manager 中，可以通过依次选择“租户管理”   > “自定义”  来找到此设置。 若要了解有关设备所有权如何影响最终用户的详细信息，请参阅[更改设备所有权](../enrollment/corporate-identifiers-add.md#change-device-ownership)。

#### <a name="group-targeting-support-for-customization-pane---4722837----"></a>“自定义”窗格的组目标支持<!-- 4722837  -->
可以将“自定义”  窗格中的设置定目标到用户组。 若要在 Intune 中查找这些设置，请导航到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，选择“租户管理”   > “自定义”  。 有关自定义的详细信息，请参阅[如何自定义 Intune 公司门户应用、公司门户网站和 Intune 应用](../apps/company-portal-app.md)。


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>设备配置

#### <a name="multiple-evaluate-each-connection-attempt-on-demand-vpn-rules-supported-on-ios-ipados-and-macos---6424615----"></a>iOS、iPadOS 和 macOS 上支持多个“评估每次连接尝试”按需 VPN 规则<!-- 6424615  -->
Intune 用户体验允许将同一个 VPN 配置文件中的多个按需 VPN 规则用于“评估每次连接尝试”  操作（“设备”   > “配置文件”   > “创建配置文件”   > “iOS/iPadOS”  或“macOS”（作为平台）  >“VPN”（作为配置文件）  >“自动 VPN”   > “按需”  ）。

过去，只接受列表中的第一条规则。 此行为已修复，Intune 现在评估列表中的所有规则。 每个规则都按照在按需规则列表中的顺序进行评估。

> [!NOTE]
> 如果已有使用这些按需 VPN 规则的 VPN 配置文件，则此修复在你下次更改 VPN 配置文件时应用。 例如，进行次要更改，如更改连接名称，然后保存配置文件。
>
> 若要使用 SCEP 证书进行身份验证，这项更改会导致此 VPN 配置文件的证书重新颁发。

适用于：
- iOS/iPadOS
- macOS

若要详细了解 VPN 配置文件，请参阅[创建 VPN 配置文件](../configuration/vpn-settings-configure.md)。

#### <a name="additional-options-in-sso-and-sso-app-extension-profiles-on-iosipados-devices---6504155-----"></a>iOS/iPadOS 设备上 SSO 和 SSO 应用扩展配置文件中的其他选项<!-- 6504155   -->

在 iOS/iPadOS 设备上，可以：
- 在 SSO 配置文件（“设备” > “配置文件” > “创建配置文件” > “iOS/iPadOS”(针对平台) >“设备功能”(针对配置文件) >“单一登录”），将 Kerberos 主体名称设置为 SSO 配置文件中的安全帐户管理器 (SAM) 帐户名称       。 
- 在 SSO 应用扩展配置文件（“设备” > “配置文件” > “创建配置文件” > “iOS/iPadOS”(针对平台) >“设备功能”(针对配置文件) >“单一登录应用扩展”）中，使用新的 SSO 应用扩展类型，以较少的单击次数配置 iOS/iPadOS Microsoft Azure AD 扩展       ）。 可以为共享设备模式下的设备启用 Azure AD 扩展，并向扩展发送特定于扩展的数据。

适用于：
- iOS/iPadOS 13.0+

有关在 iOS/iPadOS 设备上使用单一登录的详细信息，请参阅[单一登录应用扩展概述](../configuration/device-features-configure.md#single-sign-on-app-extension)和[单一登录设置列表](../configuration/ios-device-features-settings.md#single-sign-on-app-extension)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>设备注册

#### <a name="delete-apple-automated-device-enrollment-token-when-default-profile-is-present--6393220---"></a>在有默认配置文件时删除 Apple 自动设备注册令牌<!--6393220 -->
以前，无法删除默认配置文件；也就是说，无法删除与之关联的自动设备注册令牌。 现在，可以在以下情况下删除此令牌：
- 未向令牌分配任何设备
- 有默认配置文件。为此，请依次删除默认配置文件和关联的令牌。
有关详细信息，请参阅[从 Intune 中删除 ADE 令牌](../enrollment/device-enrollment-program-enroll-ios.md#delete-an-ade-token-from-intune)。

#### <a name="scaled-up-support-for-apple-automated-device-enrollment-and-apple-configurator-2-devices-profiles-and-tokens--3542402---"></a>Apple 自动设备注册和 Apple Configurator 2 的设备、配置文件和令牌纵向扩展支持<!--3542402 -->
为了帮助分散的 IT 部门和组织，Intune 现在最多支持每令牌 1,000 个注册配置文件，每 Intune 帐户 2,000 个自动设备注册（旧称为“DEP”）令牌，以及每令牌 75,000 台设备。 对于每注册配置文件的设备数没有特定限制，只要低于每令牌的最大设备数。

Intune 现在最多支持 1,000 个 Apple Configurator 2 配置文件。

有关详细信息，请参阅[支持的卷](../enrollment/device-enrollment-program-enroll-ios.md#supported-volume)。

#### <a name="all-devices-page-column-entry-changes--6967616---"></a>“所有设备”页列条目更改<!--6967616 -->
在“所有设备”  页上，“管理者”  列的条目已更改：
- 现在显示“Intune”  ，而不是“MDM” 
- 现在显示“共同管理”  ，而不是“MDM/ConfigMgr 代理” 

导出值不变。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>设备管理

#### <a name="trusted-platform-manager-tpm-version-information-now-on-device-hardware-page--6224914-idmiss---"></a>“设备硬件”页上现在提供受信任的平台管理器 (TPM) 版本信息<!--6224914 idmiss -->
现在，可以在“设备硬件”页上查看 TPM 版本号（[Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)  > “设备”  > 选择设备 >“硬件”  > 在“系统机箱”  下查找）。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>监视和故障排除

#### <a name="collect-logs-to-better-troubleshoot-scripts-assigned-to-macos-devices---6359853----"></a>收集日志以更好地对分配给 macOS 设备的脚本进行故障排除<!-- 6359853  -->
现在可以收集日志，以更好地对分配给 macOS 设备的脚本进行故障排除。 可以收集最多 60MB（压缩）日志或 25 个文件（无论哪个在先）。 有关详细信息，请参阅[使用日志收集对 macOS Shell 脚本策略进行排除故障](../apps/macos-shell-scripts.md#troubleshoot-macos-shell-script-policies-using-log-collection)。
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="security"></a>安全

#### <a name="derived-credentials-to-provision-android-enterprise-fully-managed-devices-with-certificates--4839592------"></a>使用派生凭据通过证书预配 Android Enterprise 完全托管设备<!--4839592    -->
Intune 现在支持使用[派生凭据](../protect/derived-credentials.md)作为 Android 设备的身份验证方法。 派生凭据是国家标准与技术研究所 (NIST) 800-157 标准的实现，用于将证书部署到设备。 我们对 Android 的支持扩展了对运行 iOS/iPadOS 的设备的支持。

派生凭据依赖于使用个人身份验证 (PIV) 或通用访问卡 (CAC) 卡（如智能卡）。 若要为移动设备获取派生凭据，用户从 Microsoft Intune 应用入手，遵循你使用的提供程序所特有的注册工作流。 所有提供商都要求使用计算机上的智能卡向派生凭据提供商进行身份验证。 然后，该提供商向从用户智能卡派生的设备颁发证书。

可以使用派生凭据作为 VPN 和 Wi-Fi 设备配置文件的身份验证方法。 还可以对支持它们的应用使用它们来进行应用身份验证、S/MIME 签名和加密。

Intune 现在支持对 Android 使用以下派生凭据提供程序：
- Entrust Datacard
- Intercede

第三个提供程序 DISA Purebred 将在今后发布的版本中可用于 Android。

#### <a name="microsoft-edge-security-baseline-is-now-generally-available--6586139---"></a>Microsoft Edge 安全基线现已正式发布<!--6586139 -->

这一新基线将在接下来的几周内向租户推出。  我们预计所有租户将在五月上旬获得此新基线。

新版 [Microsoft Edge 安全基线](../protect/security-baselines.md#available-security-baselines)现已正式发布 (GA)。 之前的 Edge 基线是预览版。  新版基线在 2020 年 4 月版本（Edge 版本 80 及更高版本）中发布。 

随着这一新版基线的发布，将无法再根据旧版基线创建配置文件，但可以继续使用根据这些版本创建的配置文件。 还可以选择[将现有配置文件更新为使用最新版基线](../protect/security-baselines.md#change-the-baseline-version-for-a-profile)。 

<!-- ########################## -->
## <a name="week-of-april-6-2020"></a>2020 年 4 月 6 日当周

#### <a name="new-shell-script-settings-for-macos-devices---6884363---"></a>新增了适用于 macOS 设备的 Shell 脚本设置<!-- 6884363 -->
现在，在配置适用于 macOS 设备的 Shell 脚本时，可以配置以下新设置： 
- 在设备上隐藏脚本通知
- 脚本运行频率
- 脚本失败后重试的最大次数

有关详细信息，请参阅[在 Intune 中的 macOS 设备上使用 Shell 脚本](../apps/macos-shell-scripts.md)。

<!-- ########################## -->
## <a name="week-of-march-30-2020"></a>2020 年 3 月 30 日当周

### <a name="new-url-for-the-microsoft-endpoint-manager-admin-center---3704810---"></a>Microsoft Endpoint Manager 管理中心的新 URL<!-- 3704810 -->
为了与去年在 Ignite 发布的 Microsoft Endpoint Manager 公告保持一致，我们已将 Microsoft Endpoint Manager 管理中心（以前为 Microsoft 365 设备管理）的 URL 更改为 [https://endpoint.microsoft.com](https://endpoint.microsoft.com)。 旧的管理中心 URL ([https://devicemanagement.microsoft.com](https://devicemanagement.microsoft.com)) 将仍然有效，但我们建议你开始使用新 URL 访问 Microsoft Endpoint Manager 管理中心。

有关详细信息，请参阅[使用 Microsoft Endpoint Manager 管理中心简化 IT 任务](what-is-device-management.md#simplify-it-tasks-using-the-device-management-admin-center)。  


### <a name="app-management"></a>应用管理  

#### <a name="company-portal-for-ios-supports-landscape-mode--6048329----"></a>面向 iOS 的公司门户支持横向模式<!--6048329  -->   
现在，用户可以使用自己选择的屏幕方向来注册设备、查找应用和获得 IT 支持。 应用会自动检测并调整屏幕以适应纵向或横向模式，除非你将屏幕锁定为纵向模式。  

#### <a name="script-support-for-macos-devices-public-preview---4280361----"></a>对 macOS 设备的脚本支持（公共预览版）<!-- 4280361  -->
你将能够向 macOS 设备添加和部署脚本。 此支持扩展了你配置 macOS 设备的能力，让你不再限于使用 macOS 设备上的本机 MDM 功能进行配置。 有关详细信息，请参阅[在 Intune 中的 macOS 设备上使用 Shell 脚本](../apps/macos-shell-scripts.md)。

<!-- ########################## -->
## <a name="week-of-march-24-2020"></a>2020 年 3 月 24 日当周

### <a name="improved-user-interface-experience-when-creating-device-restrictions-profiles-on-android-and-android-enterprise-devices---5841361---"></a>改进了在 Android 和 Android Enterprise 设备上创建设备限制配置文件时的用户界面体验<!-- 5841361 -->
为 Android 或 Android Enterprise 设备创建配置文件时，将更新 Endpoint Management 管理中心中的体验。 此更改会影响以下设备配置文件（“设备”   >   “配置文件” >   “创建配置文件” >    选择“Android 设备管理员”或“Android Enterprise”平台）：

- 设备限制：Android 设备管理员
- 设备限制：Android Enterprise 设备所有者
- 设备限制：Android Enterprise 工作配置文件

有关可配置设备限制的详细信息，请参阅 [Android 设备管理员](../configuration/device-restrictions-android.md)和 [Android Enterprise ](../configuration/device-restrictions-android-for-work.md)。

### <a name="improved-user-interface-experience-when-creating-configuration-profiles-on-iosipados-and-macos-devices---5569002-5568997---"></a>改善了在 iOS/iPadOS 和 macOS 设备上创建配置文件时的用户界面体验<!-- 5569002 5568997 -->
为 iOS 或 macOS 设备创建配置文件时，将更新 Endpoint Management 管理中心中的体验。 此更改会影响以下设备配置文件（“设备” > “配置文件” > “创建配置文件” >  选择“iOS/iPadOS”或“macOS”作为平台      ）：

- 自定义：iOS/iPadOS、macOS
- 设备功能：iOS/iPadOS、macOS
- 设备限制：iOS/iPadOS、macOS
- 终结点保护：macOS
- 扩展：macOS
- 首选项文件：macOS

### <a name="hide-from-user-configuration-setting-in-device-features-on-macos-devices---6524869---"></a>macOS 设备上设备功能中的“不在用户配置中显示”设置<!-- 6524869 -->

在 macOS 设备上创建设备功能配置文件时，有一个新的“不在用户配置中显示”设置（“设备” > “配置文件” > “创建配置文件” > “适用于平台的 macOS”>“适用于配置文件的设备功能”>“登录项”）        。

此功能在 macOS 设备上的“用户和组”登录项应用列表中设置应用的隐藏复选标记  。 现有配置文件将列表中的此设置显示为未配置。 若要配置此设置，管理员可以更新现有配置文件。

当设置为“隐藏”时，将选中应用的隐藏复选框，并且用户无法更改它  。 用户登录到其设备后，它还会向用户隐藏应用。

> [!div class="mx-imgBorder"]
> ![用户在 Microsoft Intune 和 Endpoint Manager 中登录设备后，在 macOS 设备上隐藏应用](./media/whats-new/macos-hide-checkmark-users-groups-login-items-apps-list.png)

有关可以配置的设置的详细信息，请参阅 [macOS 设备功能设置](../configuration/macos-device-features-settings.md)。

此功能适用于：

- macOS

## <a name="week-of-march-16-2020-2003-service-release"></a>2020 年 3 月 16 日当周（2003 服务版本）

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>应用管理

#### <a name="macos-and-ios-company-portal-updates---5779439-5780234----"></a>macOS 和 iOS 公司门户更新<!-- 5779439, 5780234  -->
已更新 macOS 和 iOS 公司门户的“配置文件”窗格，使其包含注销按钮。 此外，还对 macOS 公司门户中“配置文件”窗格进行了 UI 改进。 有关公司门户的详细信息，请参阅[如何配置 Microsoft Intune 公司门户应用](../apps/company-portal-app.md)。

#### <a name="retarget-web-clips-to-microsoft-edge-on-ios-devices---5455276-----"></a>在 iOS 设备上将 Web 剪辑重定向到 Microsoft Edge<!-- 5455276   -->
在需要在受保护的浏览器中打开的 iOS 设备上，新部署的 Web 剪辑（固定的 Web 应用）将在 Microsoft Edge（而不是在 Intune Managed Browser 中）打开。 必须重定向现有 Web 剪辑，以确保它们在 Microsoft Edge 而不是 Managed Browser 中打开。 有关详细信息，请参阅[结合使用 Microsoft Edge 和 Microsoft Intune 管理 Web 访问](../apps/manage-microsoft-edge.md)和[向 Microsoft Intune 添加 Web 应用](../apps/web-app.md)。

#### <a name="use-the-intune-diagnostic-tool-with-microsoft-edge-for-android---4735244----"></a>在适用于 Android 的 Microsoft Edge 中使用 Intune 诊断工具<!-- 4735244  -->
适用于 Android 的 Microsoft Edge 现已与 Intune 诊断工具集成。 与适用于 iOS 的 Microsoft Edge 上的体验类似，在设备上的 Microsoft Edge 的 URL 栏（地址框）中输入“about:intunehelp”将启动 Intune 诊断工具。 此工具将提供详细日志。 可以指导用户收集这些日志并将其发送给 IT 部门，或查看特定应用的 MAM 日志。

#### <a name="updates-to-intune-branding-and-customization---5236032----"></a>Intune 品牌和自定义更新<!-- 5236032  -->
我们更新了名为“品牌和自定义”的 Intune 窗格，改进内容包括：

- 将该窗格重命名为“自定义”  。
- 改进设置的组织和设计。
- 改进设置文本和工具提示。

若要在 Intune 中查找这些设置，请导航到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，选择“租户管理”   > “自定义”  。 有关现有自定义的信息，请参阅[如何配置 Microsoft Intune 公司门户应用](../apps/company-portal-app.md)。

#### <a name="users-personal-encrypted-recovery-key---6273943----"></a>用户的个人加密恢复密钥<!-- 6273943  -->
这提供了新的 Intune 功能，使用户能够通过 Android 公司门户应用程序或 Android Intune 应用程序检索其个人加密 FileVault  恢复密钥。 公司门户应用程序和 Intune 应用程序中都会提供一个链接，该链接将打开 Chrome 浏览器并转到 Web 公司门户，用户可以在其中查看访问其 Mac 设备所需的 FileVault  恢复密钥。 有关加密的详细信息，请参阅 [使用 Intune 设备加密](../protect/encrypt-devices.md)。

#### <a name="optimized-dedicated-device-enrollment----6114580----"></a>优化专用设备注册 <!-- 6114580  -->
我们正在优化 Android Enterprise 专用设备的注册，并使与 Wi-Fi 关联的 SCEP 证书更轻松地应用于 2019 年 11 月 22 日之前注册的专用设备。 对于新注册，Intune 应用将继续安装，但最终用户将不再需要在注册期间执行“启用 Intune 代理”  步骤。 将在后台自动进行安装，并且可以部署和设置与 Wi-Fi 关联的 SCEP 证书，而无需最终用户交互。  

随着 Intune 服务后端部署的展开，这些更改将于三月分阶段推出。 在三月份结束时，所有租户都将具有这一新行为。 相关信息请参阅[支持 Android Enterprise 专用设备中的 SCEP 证书](https://techcommunity.microsoft.com/t5/intune-customer-success/support-for-scep-certificates-in-android-enterprise-dedicated/ba-p/928147)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>设备配置

#### <a name="new-user-experience-when-creating-administrative-templates-on-windows-devices--5096036---"></a>在 Windows 设备上创建管理模板时的新用户体验<!--5096036 -->
根据客户反馈，以及我们迁移到新的 Azure 全屏体验，我们使用文件夹视图重新构建了“管理模板”配置文件体验。 我们尚未对任何设置或现有配置文件进行更改。 因此，现有配置文件将保持不变，并将在新视图中可用。 仍可以通过选择“所有设置”  并使用搜索来导航所有设置选项。 树视图根据“计算机”和“用户”配置进行拆分。 你将会在其相关文件夹中找到 Windows、Office 和 Edge 设置。  

适用于：
- Windows 10 及更高版本

#### <a name="vpn-profiles-with-ikev2-vpn-connections-can-use-always-on-with-iosipados-devices---1947932-----"></a>具有 IKEv2 VPN 连接的 VPN 配置文件可将“始终可用”用于 iOS/iPadOS 设备<!-- 1947932   -->
在 iOS/iPadOS 设备上，可创建使用 IKEv2 连接的 VPN 配置文件（“设备”   > “配置文件”   > 创建配置文件   > “iOS/iPadOS”  (针对平台) >选择“VPN”  (针对配置文件类型)）。 现在，可为 IKEv2 配置“始终可用”。 配置后，IKEv2 VPN 配置文件会自动连接并保持连接（或快速重新连接）到 VPN。 即使切换网络或重启设备，它仍会保持连接。

在 iOS/iPadOS 上，始终可用 VPN 仅限于 IKEv2 配置文件。

要查看可配置的 IKEv2 设置，请转到[在 iOS 设备上的 Microsoft Intune 中添加 VPN 设置](../configuration/vpn-settings-ios.md#ikev2-settings)。

适用于：
- iOS/iPadOS

#### <a name="delete-bundles-and-bundle-arrays-in-oemconfig-device-configuration-profiles-on-android-enterprise-devices---5550355-----"></a>在 Android Enterprise 设备上删除 OEMConfig 设备配置文件中的捆绑包和捆绑包系列<!-- 5550355   -->
在 Android Enterprise 设备上，创建和更新 OEMConfig 配置文件（“设备”   > “配置文件”   > “创建配置文件”   > “Android Enterprise”  (针对平台) >“OEMConfig”  (针对配置文件类型)）。 用户现在可以使用 Intune 中的“配置设计器”  删除捆绑包和捆绑包系列。

若要详细了解 OEMConfig 配置文件，请参阅[通过 Microsoft Intune 中的 OEMConfig 使用和管理 Android Enterprise 设备](../configuration/android-oem-configuration-overview.md)。

适用于：
- Android Enterprise

#### <a name="configure-the-iosipados-microsoft-azure-ad-sso-app-extension---5672534-----"></a>配置 iOS/iPadOS Microsoft Azure AD SSO 应用扩展<!-- 5672534   -->
Microsoft Azure AD 团队创建了重定向单一登录 (SSO) 应用扩展，让 iOS/iPadOS 13.0 以上的用户能够通过一次登录获取对 Microsoft 应用和网站的访问权限。 此前通过 Microsoft Authenticator 应用进行中转身份验证的所有应用都将继续获取具有新 SSO 扩展的 SSO。 在 Azure AD SSO 应用扩展版本中，可以配置包含重定向 SSO 应用扩展类型的 SSO 扩展（“设备”   > “配置文件”   > “创建配置文件”   > “iOS/iPadOS”  (针对平台) >“设备功能”  (针对配置文件类型) >“单一登录应用扩展”  ）。

适用于：
- iOS 13.0 及更高版本
- iPadOS 13.0 及更高版本

有关 iOS SSO 应用扩展的详细信息，请参阅[单一登录应用扩展](../configuration/device-features-configure.md#single-sign-on-app-extension)。

#### <a name="enterprise-app-trust-settings-modification-setting-is-removed-from-iosipados-device-restriction-profiles---6225131-----"></a>已从 iOS/iPadOS 设备限制配置文件中删除了“修改企业应用信任设置”设置<!-- 6225131   -->
在 iOS/iPadOS 设备上，创建设备限制配置文件（“设备”   > “配置文件”   > “创建配置文件”   > “iOS/iPadOS”  > 选择“设备限制”作为配置文件类型  ）。 Apple 删除了“修改企业应用信任设置”  设置，因此 Intune 中也删除了它。 如果当前在配置文件中使用此设置，则不会产生任何影响，并将从现有配置文件中将其删除。 还将从 Intune 的任何报表中删除此设置。

适用于：
- iOS/iPadOS

要查看可以限制的设置，请转到[允许或限制功能的 iOS 和 iPadOS 设备设置](../configuration/device-restrictions-ios.md)。

#### <a name="troubleshooting-pending-mam-policy-notification-changed-to-informational-icon--6348954---"></a>故障排除：挂起 MAM 策略通知更改为信息图标<!--6348954 -->
“疑难解答”边栏选项卡上的挂起 MAM 策略的通知图标已更改为信息图标。

####  <a name="ui-update-when-configuring-compliance-policy---3961639------"></a>配置合规性策略时的 UI 更新<!-- 3961639    -->

我们更新了在 Microsoft 终结点管理器中[创建合规性策略](../protect/create-compliance-policy.md#create-the-policy)时的 UI（“设备”   > “合规性策略”   > “策略”   > “创建策略”  ）。 我们提供了新的用户体验，它包含与以前使用过的相同的设置和详细信息。 新体验遵循类似向导的过程来创建合规性策略，并包含用于为策略添加“分配”  的页面，以及用于在创建策略前检查配置的“审查 + 创建”  页面。

#### <a name="retire-noncompliant-devices---1827291---------"></a>停用不合规的设备<!-- 1827291       -->
我们为可添加到任何策略中的不合规设备添加了新的操作，以便[停用不合规的设备](../protect/actions-for-noncompliance.md#add-actions-for-noncompliance)。  “停用不符合要求的设备”  这一新操作会导致从设备中删除所有公司数据，并且还会将设备从 Intune 管理中删除。  当达到配置的值（以天为单位），此操作将运行，此时设备将变为可停用状态。 最小值为 30 天。  需要明确的 IT 管理员批准，才能使用“停用不合规的设备”  部分（管理员可在其中停用所有符合条件的设备）停用设备。

#### <a name="support-for-wpa-and-wpa2-in-ios-enterprise-wi-fi-profiles--6215273-----"></a>iOS 企业 Wi-Fi 配置文件中对 WPA 和 WPA2 的支持<!--6215273   -->
[适用于 iOS 的企业 Wi-Fi 配置文件](../configuration/wi-fi-settings-ios.md#enterprise-profiles)现支持安全类型  字段。 对于安全类型  ，你可以选择“WPA 企业”  或“WPA/WPA2 企业”  ，然后为“EAP 类型”  指定选择。  （“设备”   > “配置文件”   > “创建配置文件”  ，并选择“iOS/iPadOS”  作为“平台”  ，然后选择“Wi-Fi”  作为“配置文件”  ）。 

新的企业选项类似于为适用于 iOS 的基本 Wi-Fi 配置文件提供的选项。

#### <a name="new-user-experience-for-certificate-email-vpn-and-wi-fi-vpn-profiles---5615208-----"></a>证书、电子邮件、VPN 和 Wi-Fi、VPN 配置文件的新用户体验<!-- 5615208   -->
我们更新了在“终结点管理”管理中心创建和修改以下配置文件类型的[用户体验](../configuration/device-profile-create.md)（“设备”   > “配置文件”   > “创建配置文件”  ）。 新体验显示与以前相同的设置，但使用类似向导的体验，减少了需要进行的水平滚动。 新体验推出后，无需修改现有配置。

- 派生凭据
- 电子邮件
- PKCS 证书
- PKCS 导入的证书
- SCEP 证书
- 受信任的证书
- VPN
- Wi-Fi

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>设备注册

#### <a name="configure-if-enrollment-is-available-in-company-portal-for-android-and-ios---4260128----"></a>配置可否在适用于 Android 和 iOS 的公司门户中注册<!-- 4260128  -->
可以配置 Android 和 iOS 设备上的公司门户中的设备注册可以在有提示、无提示的情况下进行，还是不允许用户注册。 若要在 Intune 中查找这些设置，请转到 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，然后依次选择“租户管理”   > “自定义”   > “编辑”   > “设备注册”  。  

支持设备注册设置要求最终用户具有以下公司门户版本：
-    iOS 上的公司门户：版本 4.4 或更高版本
-    Android 上的公司门户：版本 5.0.4715.0 或更高版本

有关现有公司门户自定义的详细信息，请参阅[如何配置 Microsoft Intune 公司门户应用](../apps/company-portal-app.md)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>设备管理

#### <a name="new-android-report-on-android-devices-overview-page---5435435-----"></a>“Android 设备概述”页面上新增 Android 报告<!-- 5435435   -->
我们已向“Android 设备概述”页面中的 Microsoft 终结点管理器管理控制台添加报告，显示每个设备管理解决方案中已注册的 Android 设备数。 此图表（像 Azure 控制台中已经存在的相同图表一样）显示工作配置文件、完全托管、专用和设备管理员注册的设备计数。 若要查看报告，请选择“设备”   >   “Android” >   “概述”。

#### <a name="guide-users-from-android-device-administrator-management-to-work-profile-management--5857738---wnstaged--"></a>指导用户从 Android 设备管理员管理转到工作配置文件管理<!--5857738   wnstaged-->
我们将发布 Android 设备管理员平台的新合规性性设置。 通过此设置，你可以将通过设备管理员管理的设备设为不合规。

在这些不合规的设备上，用户将在“更新设备设置”页上看到“转到新设备管理设置”消息。   如果用户点击“解决”  按钮，则会被引导完成以下操作：

1. 从设备管理员管理取消注册
2. 在工作配置文件管理中注册
3. 解决合规性问题 
 
Google 将在新的 Android 版本中减少设备管理员支持，以便通过 Android Enterprise 实现更现代化、更丰富、更安全的设备管理。  Intune 将只能在 2020 年第二季度之前为运行 Android 10 及更高版本的设备管理员管理的 Android 设备提供完全支持。 在此之后，无法再对运行 Android 10 或更高版本的设备管理员管理的设备进行全面管理（Samsung 设备除外）。 特别是，受影响的设备将不会收到新的密码要求。

有关此设置的详细信息，请参阅[将 Android 设备从设备管理员移动到工作配置文件管理](../enrollment/android-move-device-admin-work-profile.md)。 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>监视和故障排除

#### <a name="the-data-warehouse-now-provides-the-mac-address---6123680----"></a>数据仓库现提供 MAC 地址<!-- 6123680  -->
Intune 数据仓库将 MAC 地址作为 `device` 实体中的新属性 (`EthernetMacAddress`) 提供，以允许管理员在用户和主机 MAC 地址之间建立关联。 此属性可帮助访问特定用户，并对网络上发生的事件进行故障排除。 管理员还可以在 [Power BI 报表](../developer/reports-proc-get-a-link-powerbi.md)中使用此属性来生成更丰富的报表。 有关详细信息，请参阅 Intune 数据仓库[设备](../developer/intune-data-warehouse-collections.md#devices)实体。

#### <a name="additional-data-warehouse-device-inventory-properties---6125732----"></a>额外的数据仓库设备清单属性<!-- 6125732  -->
可以使用 Intune 数据仓库提供额外的设备清单属性。 现在可以通过[设备](../developer/intune-data-warehouse-collections.md#devices)收集公开以下属性：
- “Model”- 设备型号。
- “Office365Version”- 设备上安装的 Office 365 版本。
- “PhysicalMemoryInBytes”- 物理内存（以字节为单位）。
- `TotalStorageSpaceInBytes` - 总存储容量（以字节为单位）。

有关详细信息，请参阅 [Microsoft Intune 数据仓库 API](../developer/reports-nav-intune-data-warehouse.md) 和 Intune 数据仓库[设备](../developer/intune-data-warehouse-collections.md#devices)实体。

#### <a name="help-and-support-workflow-update-to-support-additional-services---5654170-----"></a>帮助和支持工作流更新以支持其他服务<!-- 5654170   -->
我们已在 Microsoft 终结点管理器管理中心更新了“帮助和支持”页，现在可以从中[选择你使用的管理类型](../fundamentals/get-support.md#options-to-access-help-and-support)。 此次更改后，你可以从以下管理类型中进行选择：

- Configuration Manager（包括桌面分析）
- Intune
- 共同管理

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="security"></a>安全

#### <a name="use-a-preview-of-security-administrator-focused-policies-as-part-of-endpoint-security--6131401----"></a>使用以安全管理员为中心的策略预览作为终结点安全性的一部分<!--6131401  -->
作为公共预览版，我们已在 Microsoft“终结点管理”管理中心的“终结点安全性”节点下添加了几个新策略组。 作为安全管理员，你可以使用这些新策略来关注设备安全性的特定方面，以管理不同的相关设置组，而无需承担较大的设备配置策略主体的开销。

除了新的适用于 Microsoft Defender 防病毒的防病毒策略  （见下文）外，这些新预览策略和配置文件中每项新设置都是当下你可能通过[设备配置文件](../configuration/device-profile-create.md)配置的相同设置。

以下是所有以预览形式提供的新策略类型及其可用的配置文件类型：

- **防病毒(预览)** ：
  - macOS：
    - **防病毒** - 管理 macOS 的[防病毒策略设置](../protect/antivirus-microsoft-defender-settings-macos.md)以管理[适用于 Mac 的 Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac)。

  - Windows 10 及更高版本：
    - **Microsoft Defender 防病毒** - 管理云保护、防病毒排除项、修正、扫描选项等的[防病毒策略设置](../protect/antivirus-microsoft-defender-settings-windows.md)。

      Microsoft Defender 防病毒  的防病毒配置文件是一个例外，它引入了作为设备限制配置文件的一部分提供的新设置实例。 新防病毒设置如下：

        - 与在设备限制中找到的设置相同，但支持在配置为设备限制时不可用的第三个配置选项。
        - 当 Endpoint Protection 的[共同管理工作负载滑块](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads)设置为 Intune 时，适用于通过 Configuration Manager 共同管理的设备。

     计划使用新的“防病毒”   > “Microsoft Defender 防病毒”  配置文件，而不是通过设备限制配置文件进行配置。

  - **Windows 安全体验** - 管理最终用户可在 Microsoft Defender 安全中心查看的 Windows 安全设置以及他们收到的通知。 这些设置与设备配置的 Endpoint Protection 配置文件中提供的设置相同。

- **磁盘加密(预览)** ：
  - macOS：
    - **FileVault**
  - Windows 10 及更高版本：
    - **BitLocker**
- **防火墙(预览)** ：
  - macOS：
    - **macOS 防火墙**
  - Windows 10 及更高版本：
    - **Microsoft Defender 防火墙**
- **终结点检测和响应(预览)** ：
  - Windows 10 及更高版本：-**Windows 10 Intune**
- **攻击面减少(预览)** ：
  - Windows 10 及更高版本：
    - **应用和浏览器隔离**
    - **Web 保护**
    - **应用程序控制**
    - **攻击面减少规则**
    - **设备控制**
    - **Exploit protection**
- **帐户保护(预览)** ：
  - Windows 10 及更高版本：
    - **帐户保护**

<!-- ########################## -->
## <a name="week-of-march-9-2020"></a>2020 年 3 月 9 日当周

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>应用管理

#### <a name="configure-delivery-optimization-agent-when-downloading-win32-app-content---5410945---"></a>下载 Win32 应用内容时配置传递优化代理<!-- 5410945 -->

你可以配置传递优化代理，使其基于分配在后台或前台模式下下载 Win32 应用内容。 对于现有的 Win32 应用，将继续在后台模式下下载内容。 在 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，选择“应用” > “所有应用” > 选择 Win32 应用 > “属性”     。 选择“分配”旁边的“编辑”   。  若要编辑分配，请在“必需”部分的“模式”下选择“包括”    。  你将在“应用设置”部分中找到新设置  。 有关传递优化的详细信息，请参阅 [Win32 应用管理 - 传递优化](../apps/apps-win32-app-management.md#delivery-optimization)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>设备管理

#### <a name="change-primary-user-for-windows-devices---3794742-----"></a>更改 Windows 设备的主要用户<!-- 3794742   -->
你可以更改 Windows 混合设备和 Azure AD 联接设备的主要用户。 为此，请转到“Intune”   > “设备”   > “所有设备”  > 选择设备 >“属性”   > “主要用户”  。 有关详细信息，请参阅[更改设备的主要用户](../remote-actions/find-primary-user.md#change-a-devices-primary-user)。

还为此任务创建了一个新 RBAC 权限（托管设备/设置主要用户）。 该权限已添加到内置角色，包括帮助台操作员、学校管理员和终结点安全管理器。

此功能在预览状态下在全球向客户推出。 你应在接下来的几周内看到该功能。


<!-- ########################## -->
## <a name="week-of-march-2-2020"></a>2020 年 3 月 2 日当周

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>设备管理

#### <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions---6317104-cm3555758--"></a>Microsoft Endpoint Manager 租户附加：设备同步和设备操作<!-- 6317104, CM3555758-->
Microsoft 终结点管理器将 Configuration Manager 和 Intune 组合为单个控制台。 从 Configuration Manager 技术预览版 2002.2 开始，可以在管理中心将 Configuration Manager 设备上传到云服务并对它们执行操作。 有关详细信息，请参阅 [Configuration Manager 技术预览版 2002.2 中的功能](https://docs.microsoft.com/configmgr/core/get-started/2020/technical-preview-2002-2#bkmk_attach)。

安装此更新之前，请查看 [Configuration Manager 技术预览文章](https://docs.microsoft.com/configmgr/core/get-started/technical-preview)。 此文章将帮助你熟悉使用 Technical Preview 的常规要求和限制，如何在版本之间进行更新以及如何提供相关的反馈。

#### <a name="bulk-remote-actions--4576882--"></a>批量远程操作<!--4576882-->
你现在可以为以下远程操作发出批量命令：重启、重命名、Autopilot 重置、擦除和删除。 若要查看新的批量操作，请转到 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431) > “设备” > “所有设备” > “批量操作”    。

#### <a name="all-devices-list-improved-search-sort-and-filter--6179023--"></a>“所有设备”列改进了搜索、排序和筛选<!--6179023-->
已改进“所有设备”列以获得更好的性能、搜索、排序和筛选功能。 有关详细信息，请参阅[此支持提示](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-changes-in-all-devices-list-and-reporting-in-intune/ba-p/1220946)。  

### <a name="app-management"></a>应用管理  
####  <a name="improved-sign-in-experience-in-company-portal-for-android"></a>改进了适用于 Android 的公司门户中的登录体验    
我们即将更新适用于 Android 的公司门户应用中多个登录屏幕的布局，让用户体验更现代化、更简洁。 若要查看改进，请参阅[应用 UI 中的新增功能](https://docs.microsoft.com/mem/intune/fundamentals/whats-new-app-ui)。

<!-- ########################## -->
## <a name="week-of-february-24-2020"></a>2020 年 2 月 24 日当周

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>应用管理

#### <a name="macos-company-portal-user-experience-improvements---5568987---"></a>macOS 公司门户用户体验改进<!-- 5568987 -->
我们正在改进 macOS 设备注册体验和适用于 Mac 的公司门户应用。 你将看到以下改进：
- 注册期间获得更好的 Microsoft AutoUpdate  体验，这可确保用户拥有最新版本的公司门户。
- 注册期间增强的符合性检查步骤。
- 支持复制的事件 ID，使用户可更快地将错误从其设备发送到公司支持团队。

有关注册和适用于 Mac 的公司门户应用的详细信息，请参阅[使用公司门户应用注册 macOS 设备](../user-help/enroll-your-device-in-intune-macos-cp.md)。

#### <a name="app-protection-policies-for-better-mobile-now-supports-ios-and-ipados---6224512----"></a>Better Mobile 的应用保护策略现在支持 iOS 和 iPadOS<!-- 6224512  -->

2019 年 10 月，Intune 应用保护策略增加了使用 Microsoft 威胁防护合作伙伴提供的数据的功能。 借助此更新，你现在可以使用应用保护策略阻止或使用 iOS 和 iPadOS 上的 Better Mobile 基于设备的运行状况选择性地擦除用户的公司数据。  有关详细信息，请参阅[使用 Intune 创建移动威胁防御应用保护策略](../protect/mtd-app-protection-policy.md)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>设备管理

#### <a name="exports-from-the-all-devices-list--now-in-zipped-csv-format--6343117--"></a>现在从所有设备列表以 CSV 压缩格式导出<!--6343117-->
现在从“设备” > “所有设备”页面以 CSV 压缩格式导出   。


<!-- ########################## -->
## <a name="week-of-february-17-2020-2002-service-release"></a>2020 年 2 月 17 日当周（2002 服务版本）

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>应用管理

#### <a name="microsoft-defender-advanced-threat-protection-atp-app-for-macos---5424618---"></a>适用于 macOS 的 Microsoft Defender 高级威胁防护 (ATP) 应用<!-- 5424618 -->
Intune 将提供一种简单的方法，将适用于 macOS 的 Microsoft Defender 高级威胁防护 (ATP) 应用部署到托管 Mac 设备。 有关详细信息，请参阅[使用 Microsoft Intune 向 macOS 设备添加 Microsoft Defender ](../apps/apps-advanced-threat-protection-macos.md)和[适用于 Mac 的 Microsoft Defender 高级威胁防护](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac)。  

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>设备配置

#### <a name="enable-network-access-control-nac-with-cisco-anyconnect-vpn-on-ios-devices---4860111----"></a>在 iOS 设备上使用 Cisco AnyConnect VPN 启用网络访问控制 (NAC)<!-- 4860111  -->
在 iOS 设备上，你可以创建一个 VPN 配置文件，并使用不同的连接类型，包括 Cisco AnyConnect（“设备配置” > “配置文件” > “创建配置文件” > 选择“iOS”作为平台，“VPN”作为配置文件类型，再选择“Cisco AnyConnect”作为连接类型）       。

你可以使用 Cisco AnyConnect 启用网络访问控制 (NAC)。 使用此功能需要：

1. 根据[Cisco 标识服务引擎管理员指南](https://www.cisco.com/c/en/us/td/docs/security/ise/2-1/admin_guide/b_ise_admin_guide_21/b_ise_admin_guide_20_chapter_01000.html)，使用“将 Microsoft Intune 配置为 MDM Server”中的步骤在 Azure 中配置 Cisco 标识服务引擎 (ISE)  。
2. 在 Intune 设备配置配置文件中，选择“启用网络访问控制(NAC)”设置  。

若要查看所有可用 VPN 设置，请转至[在 iOS 设备上配置 VPN](../configuration/vpn-settings-ios.md)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>设备注册

#### <a name="serial-number-on-the-apple-mdm-push-certificate-page--5947765----"></a>Apple MDM Push 证书页上的序列号<!--5947765  -->
Apple MDM Push 证书页当前显示序列号。 如果对创建该证书的 Apple ID 的访问权限丢失，则需要该序列号以重新获得对 Apple MDM Push 证书的访问权限。 若要查看序列号，请转到“设备”   > “iOS”   > “iOS 注册”   > “Apple MDM Push 证书”  。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>设备管理

#### <a name="new-update-schedule-options-for-pushing-os-updates-to-enrolled-iosipados-devices--5879689----"></a>用于将 OS 更新推送到已注册 iOS/iPadOS 设备的新更新计划选项<!--5879689  -->
在为 iOS/iPadOS 设备计划操作系统更新时，可从以下选项中进行选择。 这些选项适用于使用 Apple Business Manager 或 Apple School Manager 注册类型的设备。
- 下次签入时更新
- 在计划时间内更新
- 在计划时间外更新

对于后两个选项，可创建多个时间窗口。

若要查看新选项，请转到 MEM >“设备”   > “iOS”   > “更新 iOS/iPadOS 的策略”   > “创建配置文件”  。

#### <a name="choose-which-iosipados-updates-to-push-to-enrolled-devices--5879689----"></a>选择要推送到已注册设备的 iOS/iPadOS 更新<!--5879689  -->
可选择特定的 iOS/iPadOS 更新（最新的更新除外），将更新推送到已使用 Apple Business Manager 或 Apple School Manager 注册的设备。 此类设备必须设置设备配置策略，将软件更新可见性延迟数天。 若要查看此功能，请转到 MEM >“设备”   > “iOS”   > “更新 iOS/iPadOS 的策略”   > “创建配置文件”  。



<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>设备安全性

#### <a name="improved-intune-reporting-experience---3791418-----"></a>改进了 Intune 报表体验<!-- 3791418   -->
Intune 现在提供了改进的报表体验，包括新的报表类型、更好的报表组织、更集中的视图、改进的报表功能以及更一致和更及时的数据。 报告体验将从公共预览版迁移到 GA 版（正式版）。 此外，GA 版本还将提供本地化支持、bug 修复、设计改进，并在 [Microsoft终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)的磁贴上聚合设备符合性数据。

新的报表类型侧重于以下信息：

- **操作** - 提供具有负面运行状况的全新记录。 
- **组织** - 提供总体状态的更广泛汇总。
- **历史** - 提供一段时间内的模式和趋势。
- **专业** - 允许使用原始数据创建自己的自定义报表。

第一组新报表侧重于设备符合性。 有关详细信息，请参阅[博客 - Microsoft Intune 报表框架](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/New-Reporting-Framework-Coming-to-Intune/ba-p/1009553)和 [Intune 报表](reports.md)。

#### <a name="consolidated-the-location-of-security-baselines-in-the-ui---6177074-----"></a>合并了 UI 中安全基线的位置<!-- 6177074   -->
我们合并了路径，以便在 Microsoft 终结点管理器管理中心查找[安全基线](../protect/security-baselines.md)，方法是从多个 UI 位置删除“安全基线”  。 若要查找安全基线，现在请使用以下路径：“终结点安全” > “安全基线”   。

#### <a name="expanded-support-for-imported-pkcs-certificates---6044197----"></a>对导入的 PKCS 证书的扩展支持<!-- 6044197  -->
我们已扩展了对使用[导入的 PKCS 证书](../protect/certificates-imported-pfx-configure.md#supported-platforms)的支持以支持“Android 企业完全托管的设备”  。 通常，导入 PFX 证书的操作适用于 S/MIME 加密方案，在这些方案中，用户的加密证书在其所有设备上都是必需的，以便能够进行电子邮件解密。

以下平台支持导入 PFX 证书：

- Android - 设备管理员
- Android Enterprise - 完全托管
- Android Enterprise - 工作配置文件
- iOS
- Mac
- Windows 10

#### <a name="view-the-endpoint-security-configuration-for-devices---6206460----"></a>查看设备的终结点安全配置<!-- 6206460  -->
我们更新了 Microsoft 终结点管理器管理中心的选项名称，以便查看[适用于特定设备的终结点安全配置](../protect/security-baselines-monitor.md#view-endpoint-security-configurations-per-device)。 此选项将重命名为“终结点安全配置”，因为它显示了适用的安全基线以及在安全基线之外创建的其他策略  。 此选项以前称为“安全基线”  。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>基于角色的访问控制

#### <a name="intune-roles-user-interface-changes-coming--5801612-----"></a>即将更改“Intune 角色”用户界面<!--5801612   -->
[Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)的用户界面  > “租户管理” > “角色”已改进为更易用的直观设计   。 此体验提供的设置和详细信息与你现在使用的相同，但是新体验采用类似于向导的过程。

<!-- ########################## -->
## <a name="week-of-february-17-2020"></a>2020 年 2 月 17 日当周

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>应用管理

#### <a name="microsofts-new-office-app---5859926---"></a>Microsoft 的新 Office 应用<!-- 5859926 -->
Microsoft 的新 Office 应用现已正式发布，可供下载和使用。 Office 应用是一种合并体验，用户可在其中跨 Word、Excel 和 PowerPoint 在单个应用中工作。 可以通过应用保护策略以应用为目标，确保要访问的数据受到保护。

有关详细信息，请参阅[如何使用 Office Mobile 预览版应用启用 Intune 应用保护策略](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-how-to-enable-intune-app-protection-policies-with/ba-p/1045493)。

<!-- ########################## -->

## <a name="week-of-february-10-2020"></a>2020 年 2 月 10 日当周

### <a name="windows-7-ends-extended-support--3042987---"></a>Windows 7 终止扩展支持<!--3042987 -->
Windows 7 已于 2020 年 1 月 14 日终止扩展支持。 Intune 已弃用对同时运行 Windows 7 的设备的支持。 帮助保护 PC 的技术协助和自动更新将不再可用。 应升级到 Windows 10。 有关详细信息，请参阅[变更计划博客文章](https://aka.ms/Windows7_Intune)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>应用管理

#### <a name="microsoft-edge-version-77-and-later-on-windows-10-devices---5843584---"></a>Windows 10 设备上的 Microsoft Edge 77 及更高版本<!-- 5843584 -->
Intune 现在支持卸载 Windows 10 设备上的 Microsoft Edge 版本 77 及更高版本。 有关详细信息，请参阅[将适用于 Windows 10 的 Microsoft Edge 添加到 Microsoft Intune](../apps/apps-windows-edge.md)。

#### <a name="screen-removed-from-company-portal-android-work-profile-enrollment--6103987---"></a>从公司门户的 Android 工作配置文件注册中删除了屏幕<!--6103987 -->
从公司门户中的 Android 工作配置文件注册流中删除了“下一步是什么?”  屏幕，简化用户体验。 请转到[使用 Android 工作配置文件注册](../user-help/enroll-device-android-work-profile.md)，查看更新后的 Android 工作配置文件注册流。  

#### <a name="company-portal-app-improved-performance---6178652---"></a>公司门户应用提高了性能<!-- 6178652 -->
公司门户应用已更新，以支持使用 ARM64 处理器的设备（例如 Surface Pro X）的更高性能。以前，公司门户以仿真 ARM32 模式运行。 现在，在版本 10.4.7080.0 及更高版本中，公司门户应用已针对 ARM64 进行了本地编译。 有关公司门户应用的详细信息，请参阅[如何配置 Microsoft Intune 公司门户应用](../apps/company-portal-app.md)。

<!-- ########################## -->
## <a name="week-of-january-27-2020"></a>2020 年 1 月 27 日当周

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>应用管理

#### <a name="intune-support-for-additional-microsoft-edge-version-77-deployment-channel-for-macos---5983950----"></a>对适用于 macOS 的其他 Microsoft Edge 版本 77 部署通道的 Intune 支持<!-- 5983950  -->
Microsoft Intune 现在支持适用于 macOS 的 Microsoft Edge 应用的其他稳定  部署通道。 “稳定”  通道是用于在企业环境中广泛部署 Microsoft Edge 的建议通道。 它每六周更新一次，每个版本中都会加入“Beta”通道的改进  。 除了“稳定”通道  和“Beta”  通道之外，Intune 还支持“开发”  通道。 公共预览版为适用于 macOS 的 Microsoft Edge 版本 77 及更高版本提供“稳定”通道和“开发”通道。 默认情况下启用浏览器的自动更新。 有关详细信息，请参阅[使用 Microsoft Intune 添加适用于 macOS 设备的 Microsoft Edge](../apps/apps-edge-macos.md)。

#### <a name="retirement-of-intune-managed-browser--5728447---"></a>停用 Intune Managed Browser<!--5728447 -->
Intune Managed Browser 将停用。 使用 Microsoft Edge 获取受保护的 Intune 浏览器体验。 

<!-- ########################## -->
## <a name="week-of-january-20-2020-2001-service-release"></a>2020 年 1 月 20 日当周（2001 服务版本）

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>应用管理

#### <a name="user-experience-change-when-adding-apps-to-intune---4705829-----"></a>向 Intune 添加应用时的用户体验更改<!-- 4705829   -->
向 Intune 添加应用时，你将获得全新的用户体验。 此体验提供的设置和详细信息与你之前使用的相同，但是，在向 Intune 添加应用时，新体验采用类似于向导的过程。 这种新体验还会在添加应用之前提供“审阅”页。 在 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，选择“应用”   > “所有应用”   > “添加”  。 有关详细信息，请参阅[将应用添加到 Microsoft Intune](../apps/apps-add.md)。

#### <a name="require-win32-apps-to-restart----5622282-----"></a>需要重启 Win32 应用 <!-- 5622282   -->
可以要求必须在成功安装 Win32 应用后重启。 此外，还可以选择必须重启之前的时间（宽限期）。

#### <a name="user-experience-change-when-configuring-apps-in-intune---4207990-----"></a>在 Intune 中配置应用时的用户体验变化<!-- 4207990   -->
在 Intune 中创建应用配置策略时，你将获得全新的用户体验。 此体验提供的设置和详细信息与你之前使用的相同，但是，在向 Intune 添加策略时，新体验采用类似于向导的过程。 在 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，选择“应用”   > “应用配置策略”   > “添加”  。 有关详细信息，请参阅 [Microsoft Intune 的应用配置策略](../apps/app-configuration-policies-overview.md)。 

#### <a name="intune-support-for-additional-microsoft-edge-for-windows-10-deployment-channel---5861774---"></a>对适用于 Windows 10 的其他 Microsoft Edge 部署通道的 Intune 支持<!-- 5861774 -->
Microsoft Intune 现在支持适用于 Windows 10 的 Microsoft Edge（版本 77 或更高版本）应用的其他稳定  部署通道。 “稳定”  通道是用于在企业环境中广泛部署适用于 Windows 10 的 Microsoft Edge 的建议通道。 此通道每六周更新一次，每个版本中都会加入“Beta”通道的改进  。 除了“稳定”通道  和“Beta”  通道之外，Intune 还支持“开发”  通道。 有关详细信息，请参阅[适用于 Windows 10 的 Microsoft Edge - 配置应用设置](../apps/apps-windows-edge.md#configure-app-settings)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>设备配置

#### <a name="improved-user-interface-experience-when-configuring-exchange-activesync-on-premises-connector-ui---5695492-----"></a>改进了配置 Exchange ActiveSync 本地连接器 UI 时的用户界面体验<!-- 5695492   -->
我们更新了[配置 Exchange ActiveSync 本地连接器](../protect/exchange-connector-install.md)的体验。 更新的体验使用单个窗格来配置、编辑和汇总本地连接器的详细信息。

#### <a name="add-automatic-proxy-settings-to-wi-fi-profiles-for-android-enterprise-work-profiles---4490822-----"></a>向 Android Enterprise 工作配置文件的 Wi-Fi 配置文件添加自动代理设置<!-- 4490822   -->
在 Android Enterprise 工作配置文件设备上，可以创建 Wi-Fi 配置文件。 选择 Wi-Fi“企业”类型时，还可以输入 Wi-Fi 网络上使用的可扩展身份验证协议 (EAP) 类型。

现在，选择“企业”类型时，还可以输入自动代理设置，包括代理服务器 URL，如 `proxy.contoso.com`。

若要查看可配置的现有 Wi-Fi 设置，请参阅[在 Microsoft Intune 中为运行 Android Enterprise 和 Android 展台的设备添加 Wi-Fi 设置](../configuration/wi-fi-settings-android-enterprise.md#work-profile-only)。

适用于：
- Android Enterprise 工作配置文件

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>设备注册

#### <a name="block-android-enrollments-by-device-manufacturer--5197392----"></a>阻止设备制造商进行 Android 注册<!--5197392  -->
可以阻止设备按设备制造商进行注册。 此功能适用于 Android 设备管理员和 Android Enterprise 工作配置文件设备。 若要查看注册限制，请转到 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)“设备” > “注册限制” > “设备限制”   。

#### <a name="improvements-to-the-iosipados-create-enrollment-type-profile-ui---6055005---"></a>对 iOS/iPadOS 创建注册类型配置文件 UI 的改进<!-- 6055005 -->
对于 iOS/iPadOS 用户注册，已简化“创建注册类型配置文件设置”页，   改进“注册类型”  选项进程，同时保持功能不变。 若要查看新 UI，请转到 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431) > “设备” > “iOS” > “iOS 注册” > “注册类型” > “创建配置文件” > “设置”页       。 有关详细信息，请参阅[在 Intune 中创建用户注册配置文件](../enrollment/ios-user-enrollment.md#create-a-user-enrollment-profile-in-intune)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>设备管理

#### <a name="new-information-in-device-details---4471759-5604099----"></a>设备详细信息中的新信息<!-- 4471759 5604099  -->
以下信息现在位于设备的“概述”  页上：
- 内存容量（设备上的物理内存量）
- 存储容量（设备上的物理存储量） 
- CPU 体系结构

#### <a name="ios-bypass-activation-lock-remote-action-renamed-to-disable-activation-lock---5904591----"></a>iOS“绕过激活锁”远程操作已重命名为“禁用激活锁” <!--5904591  -->
远程操作“绕过激活锁”  已重命名为“禁用激活锁”  。 有关详细信息，请参阅[通过 Intune 禁用 iOS 激活锁](../remote-actions/device-activation-lock-disable.md)。

#### <a name="windows-10-feature-update-deployment-support-for-autopilot-devices---5948137-----"></a>对 Autopilot 设备的 Windows 10 功能更新部署支持<!-- 5948137   -->
Intune 现在支持使用 [Windows 10 功能更新部署](../protect/windows-update-for-business-configure.md#windows-10-feature-updates)来定位 Autopilot 注册的设备。

在 Autopilot 开箱即用体验 (OOBE) 期间，不能应用 Windows 10 功能更新策略，这些策略仅在设备完成预配（通常为一天）后第一次进行 Windows 更新扫描时应用。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>监视和故障排除

#### <a name="windows-autopilot-deployment-reports-preview----3856172-----"></a>Windows Autopilot 部署报表（预览） <!-- 3856172   -->
新报告说明了通过 Windows Autopilot 部署的每个设备的详细信息。 有关详细信息，请参阅 [Autopilot 部署报告](../enrollment/enrollment-autopilot.md#autopilot-deployments-report)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>基于角色的访问控制

#### <a name="new-intune-built-in-role-endpoint-security-manager--4253397-----"></a>新的 Intune 内置角色终结点安全管理器<!--4253397   -->
提供新的 Intune 内置角色：终结点安全管理器。 这个新角色使管理员能够在 Intune 中完全访问终结点管理器节点，并具有对其他区域的只读访问权限。 该角色是 Azure AD 中“安全管理员”角色的扩展。 如果目前只有全局管理员角色，则无需进行任何更改。 如果你使用角色，并且想要终结点安全管理器提供的粒度，则在该角色可用时分配该角色。 有关内置角色的详细信息，请参阅[基于角色的访问控制](role-based-access-control.md)。

<!-- ########################## -->
## <a name="week-of-january-6-2020"></a>2020 年 1 月 6 日当周

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>应用管理

#### <a name="smime-support-for-microsoft-outlook-for-ios---2669398---"></a>对 Microsoft Outlook for iOS 提供 S/MIME 支持<!-- 2669398 -->
Intune 支持提供 S/MIME 签名和加密证书，适用于 iOS 设备上的 Outlook for iOS。 有关详细信息，请参阅[适用于 iOS 和 Android 的敏感度标签和保护](https://aka.ms/omsmime)。

#### <a name="cache-win32-app-content-using-microsoft-connected-cache-server---6030314---"></a>使用 Microsoft Connected Cache 服务器缓存 Win32 应用内容<!-- 6030314 -->
可以在 Configuration Manager 分发点上安装 Microsoft Connected Cache 服务器，用于缓存 Intune Win32 应用内容。 有关详细信息，请参阅 [Configuration Manager 中的 Microsoft Connected Cache - 对 Intune Win32 应用的支持](https://docs.microsoft.com/configmgr/core/plan-design/hierarchy/microsoft-connected-cache#bkmk_intune)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>基于角色的访问控制

#### <a name="windows-10-administrative-templates-admx-profiles-now-support-scope-tags---5137390---"></a>Windows 10 管理模板 (ADMX) 配置文件现支持范围标记 <!--5137390 -->
现在可以将范围标记分配给管理模板配置文件 (ADMX)。 为此，请前往“Intune”   > “设备”   > “配置文件”  >“在列表中选择管理模板配置文件”>“属性”   > “范围标记”  。 有关范围标记的详细信息，请参阅[向其他对象分配范围标记](../fundamentals/scope-tags.md#assign-scope-tags-to-other-objects)。

<!-- ########################## -->
## <a name="week-of-december-30-2019"></a>2019 年 12 月 30 日当周

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>应用管理

#### <a name="retrieve-personal-recovery-key-from-mem-encrypted-macos-devices---4851745---"></a>从 MEM 加密的 macOS 设备检索个人恢复密钥<!-- 4851745 -->
借助 iOS 公司门户应用，最终用户可以检索其个人恢复密钥（FileVault 密钥）。 拥有个人恢复密钥的设备必须已注册 Intune，并且通过 Intune 使用 FileVault 加密。 借助 iOS 公司门户应用，最终用户单击“获取恢复密钥”，即可以在加密的 macOS 设备中检索个人恢复密钥。  此外，还可以通过选择“设备” > “已加密和已注册的 macOS 设备” > “获取恢复密钥”，来从 Intune 检索恢复密钥。    有关 FileVault 的详细信息，请参阅[用于 macOS 的 FileVault 加密](../protect/encrypt-devices.md#filevault-encryption-for-macos)。

#### <a name="ios-and-ipados-user-licensed-vpp-apps---5619268---"></a>iOS 和 iPadOS 用户许可的 VPP 应用<!-- 5619268 -->
对于用户注册的 iOS 和 iPadOS 设备，将不再向最终用户显示部署为可用的新创建的设备许可的 VPP 应用程序。 不过，最终用户会继续看到公司门户中的所有用户许可的 VPP 应用。 有关 VPP 应用的详细信息，请参阅[如何使用 Microsoft Intune 管理通过 Apple Volume Purchase Program 购买的 iOS and macOS 应用](../apps/vpp-apps-ios.md)。

<!-- ########################## -->
## <a name="week-of-december-23-2019"></a>2019 年 12 月 23 日当周

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>应用管理

#### <a name="notice---windows-10-1703-rs2-will-be-moving-out-of-support----5026679---"></a>通知 - 不再支持 Windows 10 1703 (RS2) <!-- 5026679 -->
自 2018 年 10 月 9 日起，家庭版、专业版和专业工作站版的 Microsoft 平台支持不再包含 Windows 10 1703 (RS2)。 在 2019 年 10 月 8 日，Windows 10 企业版和教育版平台支持不再包含 Windows 10 1703 (RS2)。 自 2019 年 12 月 26 日起，我们会将 Windows 公司门户应用程序最低版本更新到 Windows 10 1709 (RS3)。 运行 1709 之前版本的计算机将不再从 Microsoft Store 收到此应用程序的更新版。 之前我们已通过消息中心将此变更告知使用 Windows 10 早期版本的客户。 有关详细信息，请参阅 [Windows 生命周期简报](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)。

<!-- ########################## -->

## <a name="week-of-december-16-2019"></a>2019 年 12 月 16 日当周

### <a name="device-configuration"></a>设备配置

#### <a name="updates-to-administrative-templates-for-windows-10-devices----5941568---"></a>Windows 10 设备管理模板更新 <!-- 5941568 -->

可以使用 Microsoft Intune 中的 ADMX 模板控制和管理用于 Microsoft Edge、Office 和 Windows 的设置。 Intune 中的管理模板做出以下策略设置更新：

- 添加了对 Microsoft Edge 版本 78 和 79 的支持。
- 包括[管理模板文件 (ADMX/ADML) 和适用于 Office 365 专业增强版、Office 2019 和 Office 2016 的 Office 自定义工具](https://www.microsoft.com/download/details.aspx?id=49030)中的 ADMX（2019 年 11 月 11 日）文件。

有关 Intune 中的 ADMX 模板的详细信息，请参阅[使用 Windows 10 模板在 Microsoft Intune 中配置组策略设置](../configuration/administrative-templates-windows.md)。

适用于：

- Windows 10 及更高版本

## <a name="week-of-december-9-2019-1912-service-release"></a>2019 年 12 月 9 日当周（1912 服务版本）

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>应用管理

#### <a name="migrating-to-microsoft-edge-for-managed-browsing-scenarios---5173762---"></a>迁移到适用于托管浏览方案的 Microsoft Edge<!-- 5173762 -->
由于即将停用 Intune Managed Browser，我们对应用保护策略进行了更改，以简化将用户转移到 Edge 所需的步骤。 我们将应用保护策略设置的选项“限制使用其他应用传输 Web 内容”更新为以下之一  ：

- 任何应用
- Intune 托管浏览器
- Microsoft Edge
- 非托管浏览器 

选择“Microsoft Edge”时，最终用户将看到条件访问消息，该消息通知他们托管浏览方案需要 Microsoft Edge  。 如果尚未下载，系统将提示他们下载 Microsoft Edge 并使用其 AAD 帐户登录 Microsoft Edge。  这等同于将目标设置为应用配置设置 `com.microsoft.intune.useEdge` 设为 True 的启用了 MAM 的应用  。 使用“策略托管浏览器”设置的现有应用保护策略现已选中“Intune Managed Browser”，你将看不到任何行为更改   。 这意味着，如果你将 useEdge 应用配置设置设为 True，则用户将看到一条要求使用 Microsoft Edge 的消息   。 我们鼓励所有使用托管浏览方案的客户通过“限制使用其他应用传输 Web 内容”来更新其应用保护策略，以确保用户无论从哪个应用启动链接，都可以看到过渡到 Microsoft Edge 的合适指南  。 

#### <a name="configure-app-notification-content-for-organization-accounts---2576686----"></a>配置组织帐户的应用通知内容<!-- 2576686  -->
借助 Android 和 iOS 设备上的 Intune 应用保护策略 (APP)，可以控制组织帐户的应用通知内容。 可以选择选项（“允许”、“阻止组织数据”或“阻止”）来指定为所选应用显示组织帐户通知的方式。 此功能需要应用程序的支持，可能不适用于所有启用了 APP 的应用程序。 Outlook for iOS 版本 4.15.0（或更高版本）和 Outlook for Android 4.83.0（或更高版本）将支持此设置。 可从控制台获取此设置，但此功能将从 2019 年 12 月 16 日之后开始生效。 有关 APP 的详细信息，请参阅[什么是应用保护策略？](../apps/app-protection-policy.md)。

#### <a name="microsoft-app-icons-update--4677605----"></a>Microsoft 应用图标更新<!--4677605  -->
应用保护策略和应用配置策略的应用目标窗格中用于 Microsoft 应用的图标已更新。

#### <a name="require-use-of-approved-keyboards-on-android--4761794----"></a>要求在 Android 上使用经过批准的键盘<!--4761794  -->
在应用保护策略中，可以指定设置[“批准的键盘”  ](../apps/app-protection-policy-settings-android.md#data-protection)，以管理可以将哪些 Android 键盘用于托管的 Android 应用。 当用户打开此托管应用并且尚未将批准的键盘用于该应用时，将提示他们切换到设备上已安装的一个经过批准的键盘。 必要时，会为用户提供从 Google Play Store 下载批准的键盘的链接，以便他们可以进行安装和设置。 如果用户的活动键盘不是经过批准的键盘，则用户只能够编辑托管应用中的文本字段。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>设备配置

#### <a name="updated-single-sign-on-experience-for-apps-and-websites-on-your-ios-ipados-and-macos-devices---4999578----"></a>更新了 iOS、iPadOS 和 macOS 设备上的应用和网站的单一登录体验<!-- 4999578  -->
Intune 添加了更多适用于 iOS、iPadOS 和 macOS 设备的单一登录 (SSO) 设置。 现在可以配置组织或标志提供者编写的重定向 SSO 应用扩展。 使用这些设置来为使用新式身份验证方法（如 OAuth 和 SAML2）的应用和网站配置无缝单一登录体验。 

这些新设置扩展了 SSO 应用扩展和 Apple 内置 Kerberos 扩展的旧设置（“设备”   > “设备配置”   > “配置文件”   > “创建配置文件”   >  为平台类型选择“iOS/iPadOS”或“macOS”> 为配置文件类型选择“设备功能”）。    

转到 [iOS 上的 SSO](../configuration/ios-device-features-settings.md#single-sign-on-app-extension) 和 [macOS 上的 SSO](../configuration/macos-device-features-settings.md#single-sign-on-app-extension)，可查看可配置的 SSO 应用扩展设置的完整范围。

适用于：

- iOS/iPadOS
- macOS

#### <a name="we-have-updated-two-device-restriction-settings-for-ios-and-ipados-devices-to-correct-their-behavior---5701352------"></a>我们更新了针对 iOS 和 iPadOS 设备的两个设备限制设置，以更正这些设备的行为<!-- 5701352    -->
对于 iOS 设备，你可以创建设备限制配置文件来“允许无线 PKI 更新”和“阻止 USB 受限模式”   （“设备”   > “设备配置”   > “配置文件”   > “创建配置文件”   >  为平台选择“iOS/iPadOS”> 为配置文件类型选择“设备限制”）。   在此版本之前，以下设置的 UI 设置和说明均不正确，现已更正。 自此版本开始，这些设置的行为如下所示：

**阻止无线 PKI 更新**：**阻止**：若设备未连接计算机，将阻止用户收到软件更新。 **未配置**（默认设置）：设备无需连接计算机，即可收到软件更新。
- 之前，你可以将此设置配置如下：**允许**：你的用户无需将设备连接到计算机，即可收到软件更新。
**在设备锁定时允许使用 USB 附件**：**允许**：允许 USB 附件与锁定超过一个小时的设备交换数据。 **未配置**（默认设置）：未更新设备的 USB 受限模式，若设备锁定时间超过一个小时，将阻止 USB 附件从设备传输数据。
- 之前，你可以将此设置配置如下：**阻止**：可禁用受监管设备上的 USB 受限模式。

有关可以配置的设置的详细信息，请参阅[使用 Intune 允许或限制功能的 iOS 和 iPadOS 设备设置](../configuration/device-restrictions-ios.md)。

此功能适用于：

- iOS/iPadOS

#### <a name="wired-network-device-configuration-profiles-for-macos-devices---3508686----"></a>macOS 设备的有线网络设备配置文件<!-- 3508686  -->
   > [!NOTE]
   > 此功能推迟到稍后发布。

#### <a name="block-users-from-configuring-certificate-credentials-in-the-managed-keystore-on-android-enterprise-device-owner-devices---3311998---"></a>阻止用户在 Android Enterprise 设备所有者设备的托管密钥存储中配置证书凭据<!-- 3311998 -->
在 Android Enterprise 设备所有者上，你可以配置一个新设置，来阻止用户在托管密钥存储中配置证书凭据（“设备配置”   > “配置文件”   > “创建配置文件”   > “Android Enterprise”（针对平台）>“仅设备所有者”>“设备限制”（针对配置文件类型）>“用户和帐户”）。   

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>设备管理

#### <a name="protected-wipe-action-now-available--51150000---"></a>受保护的擦除操作现已可用<!--51150000 -->
现在可以选择使用擦除设备操作对设备执行受保护的擦除。 除了受保护的擦除无法通过关闭设备规避，它与标准擦除相同。 受保护的擦除将继续尝试重置设备，直到成功为止。 在一些配置中，此操作可能会使设备无法重启。 有关详细信息，请参阅[停用或擦除设备](../remote-actions/devices-wipe.md)。

#### <a name="device-ethernet-mac-address-added-to-devices-overview-page--5562275---"></a>将设备以太网 MAC 地址添加到了设备的“概述”页<!--5562275 -->
现在可以从设备详细信息页看到设备的以太网 MAC 地址（“设备”   > “所有设备”  > 选择一个设备 > “概述”。 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>设备安全性

#### <a name="improved-experience-on-a-shared-device-when-device-based-conditional-access-policies-are-enabled---1734096----"></a>改进了启用基于设备的条件访问策略时共享设备中的体验<!-- 1734096  -->
通过在执行策略时选中针对用户的最新符合性评估，改进了具有多个用户（针对基于设备的条件访问策略）的共享设备中的体验。 有关详细信息，请参阅下列概述文章：
- [Azure 条件访问概述](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)
- [Intune 设备符合性概述](../protect/device-compliance-get-started.md)

#### <a name="use-pkcs-certificate-profiles-to-provision-devices-with-certificates---2317124-2317130-2317139-2340517-2340528-2340529----"></a>使用 PKCS 证书配置文件为设备预配证书<!-- 2317124, 2317130, 2317139, 2340517, 2340528, 2340529  -->
现在，当运行 Android for Work、iOS/iPadOS 和 Windows 的设备与 PKCS 证书配置文件关联时，可以使用配置文件向其颁发证书，例如用于 Wi-Fi 和 VPN 的配置文件  。 之前，这三个平台仅支持基于用户的证书，基于设备的支持仅限于 macOS。

> [!NOTE]
> Wi-Fi 配置文件不支持 PKCS 证书配置文件。 而是在使用 [EAP 类型](../configuration/wi-fi-settings-windows.md#enterprise-profile)时使用 SCEP 证书配置文件。

若要使用基于设备的证书，在为支持的平台[创建 PKCS 证书配置文件](../protect/certficates-pfx-configure.md#create-a-pkcs-certificate-profile)时选择“设置”。  现在将显示“证书类型”设置，它支持“设备”或“用户”选项。 


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>监视和故障排除

#### <a name="centralized-audit-logs--5603185-5697164---"></a>集中式化审核日志<!--5603185, 5697164 -->
现在全新的集中式审核日志体验可将各种类别的审核日志收集到一个页面。 可以通过筛选日志来获得你所寻找的数据。 若要查看审核日志，可转到“租户管理”   > “审核日志”。  

#### <a name="scope-tag-information-included-in-audit-log-activity-details--5763534---"></a>将范围标记信息包含在审核日志活动详细信息中<!--5763534 -->
现在审核日志活动详细信息包含范围标记信息（针对支持范围标记的 Intune 对象）。 有关审核日志的详细信息，请参阅[使用审核日志跟踪和监视事件](monitor-audit-logs.md)。

<!-- ########################## -->
## <a name="week-of-december-2-2019"></a>2019 年 12 月 2 日当周

#### <a name="new-microsoft-endpoint-configuration-manager-co-management-licensing--5027281--"></a>新的 Microsoft Endpoint Configuration Manager 共同管理许可<!--5027281-->
拥有软件保障的 Configuration Manager 客户在不购买额外的 Intune 共同管理许可证的情况下可获得适用于 Windows 10 电脑的 Intune 共同管理。 客户不再需要为其最终用户分配单独的 Intune/EMS 许可证以共同管理 Windows 10。
- 由 Configuration Manager 管理并注册加入共同管理的设备拥有与 Intune 独立 MDM 托管的电脑几乎相同的权限。 但在重置后，不能使用 Autopilot 重新预配它们。
- 通过使用其他方式注册到 Intune 的 Windows 10 设备需要完整的 Intune 许可证。
- 其他平台上的设备仍需要完整的 Intune 许可证。

有关详细信息，请参阅[许可条款](https://www.microsoft.com/en-us/Licensing/product-licensing/products)。

<!-- ########################## -->
## <a name="week-of-november-18-2019-1911-service-release"></a>2019 年 11 月 18 日当周（1911 服务版本）

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>应用管理

#### <a name="ui-update-when-selectively-wiping-app-data---4102028---"></a>针对何时选择性擦除应用数据更新了 UI<!-- 4102028 -->
更新了 Intune 中用于选择性擦除应用数据的 UI。 UI 更改包括：
- 简化了体验，可使用压缩在一个窗格中的向导式格式。
- 对创建流进行了更新，使其包含分配。
- 在创建新策略前查看属性时，或在编辑属性时，将显示包含已设置的所有内容的摘要页。 此外，编辑属性时，摘要将仅显示正在编辑的属性类别的项目列表。

有关详细信息，请参阅[如何仅擦除 Intune 托管应用中的企业数据](../apps/apps-selective-wipe.md)。

#### <a name="ios-and-ipados-third-party-keyboard-support---4922950---"></a>iOS 和 iPadOS 第三方键盘支持<!-- 4922950 -->
2019 年 3 月，我们宣布不再支持 iOS 应用保护策略设置“第三方键盘”。 此功能将返回到支持 iOS 和 iPadOS 的 Intune。 若要启用此设置，请访问新的或现有的 iOS/iPadOS 应用保护策略的“数据保护”  选项卡，并在“数据传输”  下查找“第三方键盘”  设置。

此策略设置的行为与以前的实现略有不同。 在使用 SDK 版本 12.0.16 及更高版本的多标识应用中，如果应用保护策略的目标是将此设置配置为“阻止”  ，则最终用户将无法在其组织和个人帐户中选择第三方键盘。 使用 SDK 版本 12.0.12 及更早版本的应用将继续显示以下博客文章标题中所述的行为：[已知问题：个人帐户的 iOS 中不阻止第三方键盘](https://aka.ms/3rdparty_iOS_Intune)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>设备配置

#### <a name="target-macos-user-groups-to-require-jamf-management---4061739----"></a>需要 Jamf 管理的目标 macOS 用户组<!-- 4061739  --> 
可以面向特定的用户组，这些用户将获得[由 Jamf 管理的 macOS 设备](../protect/conditional-access-integrate-jamf.md)。 此目标定向使你可以将 Jamf 符合性集成应用于 macOS 设备的子集，而其他设备由 Intune 管理。 如果已在使用 Jamf 集成，则默认情况下，所有用户都将作为集成目标。

#### <a name="new-exchange-activesync-settings-when-creating-an-email-device-configuration-profile-on-ios-devices---4892824-----"></a>在 iOS 设备上创建电子邮件设备配置文件时的新 Exchange ActiveSync 设置<!-- 4892824   --> 
在 iOS/iPadOS 设备上，可以在设备配置文件中创建电子邮件连接（“设备配置”   > “配置文件”   > “创建配置文件”   > “iOS/iPadOS”  (针对平台) >“电子邮件”  (针对配置文件类型)）。 

提供了新的 Exchange ActiveSync 设置，包括：
- **要同步的 Exchange 数据**：为日历、联系人、提醒、备注和电子邮件选择要同步（或阻止同步）的 Exchange 服务。
- **允许用户更改同步设置**：允许（或阻止）用户在其设备上更改这些服务的同步设置。  

有关这些设置的详细信息，请参阅 [Intune 中适用于 iOS 设备的电子邮件配置文件设置](../configuration/email-settings-ios.md)。 

适用于：

- iOS 13.0 及更高版本
- iPadOS 13.0 及更高版本

#### <a name="prevent-users-from-adding-personal-google-accounts-to-android-enterprise-fully-managed-and-dedicated-devices---5353228-----"></a>阻止用户将个人 Google 帐户添加到 Android Enterprise 完全托管的专用设备<!-- 5353228   -->
在 Android Enterprise 完全托管的专用设备上，提供了一个新设置以阻止用户创建个人 Google 帐户（“设备配置”   > “配置文件”   > “创建配置文件”   > “Android Enterprise”  (针对平台) >“仅设备所有者”>“设备限制”  (针对配置文件类型) >“用户和帐户设置”   > “个人 Google 帐户”  ）。

要查看可以配置的设置，请转到[便于使用 Intune 允许或限制功能的 Android Enterprise 设备设置](../configuration/device-restrictions-android-for-work.md)。

适用于：

- Android Enterprise 完全托管设备
- Android Enterprise 专用设备

#### <a name="server-side-logging-for-siri-commands-setting-is-removed-in-iosipados-device-restrictions-profile----5468501-----"></a>iOS/iPadOS 设备限制配置文件中删除了“Siri 命令的服务器端日志记录”设置 <!-- 5468501   -->
在 iOS 和 iPadOS 设备上，从 Microsoft 终结点管理器管理控制台中删除了“Siri 命令的服务器端日志记录”  设置（“设备配置”   > “配置文件”   > “创建配置文件”   > “iOS/iPadOS”  (针对平台) >“设备限制”  (针对配置文件类型) >“内置应用”  ）。 

此设置对设备不起作用。 若要从现有配置文件中删除此设置，请打开该配置文件，进行更改，然后保存该配置文件。 配置文件已更新，并从设备中删除了该设置。

若要查看可以配置的设置，请参阅[使用 Intune 允许或限制功能的 iOS 和 iPadOS 设备设置](../configuration/device-restrictions-ios.md)。

适用于：

- iOS/iPadOS

#### <a name="windows-10-feature-updates-public-preview---2384877---"></a>Windows 10 功能更新（公开预览版）<!-- 2384877 -->
你现在可以将 [Windows 10 功能更新](../protect/windows-update-for-business-configure.md#windows-10-feature-updates)部署到 Windows 10 设备。 Windows 10 功能更新是一个新的软件更新策略，该策略用于设置你想要在设备中安装和保留的 Windows 10 版本。 可以将此新策略类型和现有的 Windows 10 更新通道一起使用。

接收 Windows 10 功能更新策略的设备将安装指定版本的 Windows，然后一直保留该版本，直到策略被编辑或删除。 运行更高版本 Windows 的设备仍保持其当前版本。 保持在特定 Windows 版本的设备仍可以在 Windows 10 更新通道中安装该版本的质量和安全更新。

此新类型的策略在本周开始向租户推出。 如果你的租户尚未能使用此策略，敬请期待，很快就可以使用。

#### <a name="add-and-change-key-information-in-plist-files-for-macos-applications---4736278---"></a>为 macOS 应用程序添加和更改 plist 文件中的关键信息<!-- 4736278 -->
在 macOS 设备上，你现在可以创建设备配置文件，该配置文件将上传与应用或设备关联的属性列表文件 (.plist)（“设备”   > “配置文件”   > “创建配置文件”   > “macOS”  (针对平台) >“首选项文件”  (针对配置文件类型)）。

只有某些应用支持托管首选项，并且这些应用可能不允许管理所有设置。 请确保上传的属性列表文件可配置设备通道设置，而不是用户通道设置。

有关此功能的详细信息，请参阅[使用 Microsoft Intune 向 macOS 设备添加属性列表文件](../configuration/preference-file-settings-macos.md)。

适用于：

- 运行 10.7 及更高版本的 macOS 设备

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>设备管理

#### <a name="edit-device-name-value-for-autopilot-devices---2640074---"></a>编辑 Autopilot 设备的设备名称值<!-- 2640074 -->
可以编辑 Azure AD 联接的 Autopilot 设备的设备名称值。  有关详细信息，请参阅[编辑 Autopilot 设备属性](../enrollment/enrollment-autopilot.md#edit-autopilot-device-attributes)。

#### <a name="edit-group-tag-value-for-autopilot-devices---4816775-----"></a>编辑 Autopilot 设备的组标记值<!-- 4816775   -->
可以编辑 Autopilot 设备的组标记值。 有关详细信息，请参阅[编辑 Autopilot 设备属性](../enrollment/enrollment-autopilot.md#edit-autopilot-device-attributes)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>监视和故障排除

#### <a name="updated-support-experience---5012398---"></a>更新的支持体验<!-- 5012398 -->

从现在开始，针对[获取 Intune 的帮助和支持](get-support.md)将向租户推出已更新且简化的控制台内体验。 如果你尚未能感受此新体验，敬请期待，很快就会推出。

我们改进了针对常见问题的控制台内搜索和反馈，以及用于联系支持人员的工作流。 打开支持问题时，你将看到需要回拨或电子邮件答复的实时估计，并且顶级和统一支持客户可以轻松地为其问题指定严重性，以帮助更快地获得支持。

#### <a name="improved-intune-reporting-experience-public-preview----3791418---"></a>改进了 Intune 报表体验（公共预览版） <!-- 3791418 -->
Intune 现在提供了改进的报表体验，包括新的报表类型、更好的报表组织、更集中的视图、改进的报表功能以及更一致和更及时的数据。 新的报表类型侧重于以下内容：

- **操作** - 提供具有负面运行状况的全新记录。 
- **组织** - 提供总体状态的更广泛汇总。
- **历史** - 提供一段时间内的模式和趋势。
- **专业** - 允许使用原始数据创建自己的自定义报表。

第一组新报表侧重于设备符合性。 有关详细信息，请参阅[博客 - Microsoft Intune 报表框架](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/New-Reporting-Framework-Coming-to-Intune/ba-p/1009553)和 [Intune 报表](reports.md)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>基于角色的访问控制

#### <a name="duplicate-custom-or-built-in-roles----1081938-----"></a>复制自定义或内置角色 <!-- 1081938   -->
现在可以复制内置和自定义角色。 有关详细信息，请参阅[复制角色](../fundamentals/create-custom-role.md#copy-a-role)。

#### <a name="new-permissions-for-school-administrator-role----5621805----"></a>学校管理员角色的新权限 <!-- 5621805  -->  
已将两个新权限（“分配配置文件”  和“同步设备”  ）添加到了学校管理员角色 >“权限”   > “注册计划”  。 同步配置文件权限允许组管理员同步 Windows Autopilot 设备。 分配配置文件权限允许他们删除用户启动的 Apple 注册配置文件。 它还提供了相关权限以允许他们管理 Autopilot 设备分配和 Autopilot 部署配置文件分配。 有关所有学校管理员/组管理员权限的列表，请参阅[分配组管理员](https://docs.microsoft.com/intune-education/group-admin-delegate)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="security"></a>安全

#### <a name="bitlocker-key-rotation---2564951----"></a>BitLocker 密钥轮换<!-- 2564951  -->
对于运行 Windows 1909 或更高版本的托管设备，你可以使用 Intune 设备操作远程[轮换 BitLocker 恢复密钥](../protect/encrypt-devices.md#rotate-bitlocker-recovery-keys)。 若要获取相关资格以轮换恢复密钥，设备必须配置为支持恢复密钥轮换。  

#### <a name="updates-to-dedicated-device-enrollment-to-support-scep-device-certificate-deployment----5198878----"></a>更新了专用设备注册以支持 SCEP 设备证书部署 <!-- 5198878  -->
Intune 现在支持 SCEP 设备证书部署到 Android Enterprise 专用设备，以实现对 Wi-Fi 配置文件的基于证书的访问。 若要使部署正常工作，设备上必须存在 Microsoft Intune 应用。 因此，我们更新了 Android Enterprise 专用设备的注册体验。 新注册仍将以相同的方式（QR、NFC、零接触或设备标识符）启动，但现在需要用户安装 Intune 应用。 现有设备将开始以滚动的方式自动安装应用。

#### <a name="intune-audit-logs-for-business-to-business-collaboration--5670211---"></a>面向企业到企业协作的 Intune 审核日志<!--5670211 -->
企业到企业 (B2B) 协作可以安全地将公司的应用程序和服务与来自任何其他组织的来宾用户共享，同时保持对自己公司数据的控制。 Intune 现在支持 B2B 来宾用户的审核日志。 例如，当来宾用户进行更改时，Intune 将能够通过审核日志捕获此数据。 有关详细信息，请参阅[什么是 Azure Active Directory B2B 中的来宾用户访问权限？](https://docs.microsoft.com/azure/active-directory/b2b/what-is-b2b)

<!-- ########################## -->
## <a name="week-of-november-11-2019"></a>2019 年 11 月 11 日当周  

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>应用管理  

#### <a name="improved-macos-enrollment-experience-in-company-portal----5074349----"></a>在公司门户中改进了 macOS 注册体验 <!-- 5074349  -->  
用于 macOS 注册的公司门户提供的注册过程更简单，与用于 iOS 注册的公司门户高度一致。 设备用户现在可以看到：  

- 流畅的用户界面。  
- 改进的注册清单。  
- 更清晰的设备注册说明。  
- 改进的疑难解答选项。  

#### <a name="web-apps-launched-from-the-windows-company-portal-app---5030972---"></a>从 Windows 公司门户应用启动的 Web 应用<!-- 5030972 -->
最终用户现在可以直接从 Windows 公司门户应用启动 Web 应用。 最终用户可以选择 Web 应用，然后选择选项“在浏览器中打开”  。 已发布的 Web URL 直接在 Web 浏览器中打开。 此功能将在下周推出。 有关 Web 应用的详细信息，请参阅[向 Microsoft Intune 添加 Web 应用](../apps/web-app.md)。  

#### <a name="new-assignment-type-column-in-company-portal-for-windows-10----5459950----"></a>适用于 Windows 10 的公司门户中的”新建分配类型”列 <!-- 5459950  -->
“公司门户”>“安装的应用” > “分配类型”列已重命名为“你的组织需要”    。  在该列下，用户将看到“是”或“否”值，以指示应用是其组织必需的还是可选的   。 之所以做出这些更改是因为设备用户对可用应用的概念感到困惑。 用户可以参阅[在设备上安装和共享应用](../user-help/install-apps-cpapp-windows.md)以获取从公司门户安装应用的详细信息。 有关为用户配置公司门户应用的详细信息，请参阅[如何配置 Microsoft Intune 公司门户应用](../apps/company-portal-app.md)。  

<!-- ########################## -->
## <a name="week-of-november-4-2019"></a>2019 年 11 月 4 日当周

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>设备安全性

#### <a name="security-baselines-are-supported-on-microsoft-azure-government---4062552---"></a>Microsoft Azure 政府支持安全基线<!-- 4062552 -->

Microsoft Azure 政府  上托管的 Intune 实例现在可以使用[安全基线](../protect/security-baselines.md)来帮助保护用户和设备的安全。

## <a name="whats-new-archive"></a>新增功能存档
若要了解前几个月的新增功能，请参阅[新增功能存档](whats-new-archive.md)。

## <a name="notices"></a>通知

[!INCLUDE [Intune notices](../includes/intune-notices.md)]


