---
title: 开发过程中 - Microsoft Intune
titleSuffix: ''
description: 开发过程中的 Microsoft Intune 功能
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/28/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: feb277f30401f31ddb400f5e3f6cd7709fa31c0b
ms.sourcegitcommit: 75d6ea42a0f473dc5020ae7fcb667c9bdde7bd97
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/01/2020
ms.locfileid: "89286231"
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


<!-- ***********************************************-->
## <a name="device-configuration"></a>设备配置

### <a name="create-pkcs-certificate-profiles-for-android-enterprise-fully-managed-devices-cobo---4839686---"></a>为 Android Enterprise 完全托管设备创建 PKCS 证书配置文件 (COBO)<!-- 4839686 -->
你可以创建 PKCS 证书配置文件，以便将证书部署到 Android Enterprise 设备所有者和工作配置文件设备（“设备” > “配置文件” > “创建配置文件” > “Android Enterprise”>“仅限设备所有者”，或“Android Enterprise”>“仅限工作配置文件”[针对平台]>“PKCS”[针对配置文件]）。

不久，你将能够为 Android Enterprise 完全托管设备创建 PKCS 证书配置文件。 Intune PFX 证书连接器是必需的。 如果不使用 SCEP 并且只使用 PKCS，则可以在安装新的 PFX 连接器后删除 NDES 连接器。 新的 PFX 连接器导入 PFX 文件，并将 PKCS 证书部署到所有平台。

有关 PKCS 证书的详细信息，请参阅[配置 PKCS 证书并用于 Intune](../protect/certficates-pfx-configure.md)。

适用于：
- Android Enterprise 完全托管 (COBO)

### <a name="support-for-certificates-with-a-key-size-of-4096-on-ios-and-macos-devices---7659175-----"></a>在 iOS 和 macOS 设备上支持密钥大小为 4096 的证书<!-- 7659175   -->
Intune 即将支持在 SCEP 证书配置文件中使用 4096 位的密钥大小。 （“设备” > “配置文件” > “创建配置文件” > 选择平台 > 配置文件 = “SCEP 证书”）

以下平台将支持 4096 位密钥： 
- iOS 14 及更高版本
- macOS 11 及更高版本    

### <a name="new-setting-for-password-complexity-for-android-10-and-later---7992114----"></a>面向 Android 10 及更高版本的新设置“密码复杂性”<!-- 7992114  -->
为了支持 Android 10 及更高版本的新选项，我们将向“设备合规性”策略和“设备限制”策略添加名为“密码复杂性”的新设置。 （“设备” > “配置文件” > “创建配置文件” > “设备限制”和“设备” > “合规性策略” > “创建策略”）使用此设置可以管理密码强度的度量值，其中包括密码类型、长度和质量。 

系统将支持以下复杂性级别：
- **无** - 没有密码
- **低** - 密码满足以下条件之一：
  - 模式
  - 具有重复 (4444) 或有序（1234、4321、2468）序列的 PIN
- **中** - 密码满足以下条件之一：
  - 不带重复 (4444) 或有序（1234、4321、2468）序列的 PIN，长度至少为 4
  - 字母，长度至少为 4
  - 字母数字，长度至少为 4
- **高** - 密码满足以下条件之一：
  - 不带重复 (4444) 或有序（1234、4321、2468）序列的 PIN，长度至少为 8
  - 字母，长度至少为 6
  - 字母数字，长度至少为 6

密码复杂性不适用于运行 Android 10 及更高版本的 Samsung Knox 设备。 在这些设备上，“密码长度”和/或“密码类型”设置会替代“密码复杂性”。

### <a name="cope-preview-update-new-settings-to-create-requirements-for-the-work-profile-password-for-android-enterprise-corporate-owned-devices-with-a-work-profile--7088355---"></a>COPE 预览更新：用于为 Android Enterprise 公司拥有的工作配置文件设备创建工作配置文件密码要求的新设置<!--7088355 -->
将来的设置将使管理员能够为 Android Enterprise 公司拥有的工作配置文件设备设置工作配置文件密码要求。  （“设备” > “配置文件” > “创建配置文件” > “Android Enterprise”[针对平台] >“公司拥有的完全托管式专用工作配置文件” > “设备限制”[针对配置文件] >“工作配置文件密码”）：

- 所需的密码类型
- 最短密码长度
- 密码还剩多少天到期
- 必须有多少个密码后用户才能重用密码
- 登录失败多少次后擦除设备


### <a name="new-settings-using-per-app-vpn-or-on-demand-vpn-on-iosipados-and-macos-devices---7758772-7758837-7758886----"></a>在 iOS/iPadOS 和 macOS 设备上使用每应用 VPN 或按需 VPN 的新设置<!-- 7758772 7758837 7758886  -->
- **防止用户禁用自动 VPN** ：创建自动“每应用 VPN”或“按需 VPN”连接时，可以强制用户保持自动 VPN 的“已启用且正在运行”状态。
- **关联域**：创建自动“每应用 VPN”连接时，可以在 VPN 配置文件中指定自动启动 VPN 连接的关联域。 
- **排除的域**：创建自动“每应用 VPN”连接时，可以创建一个域列表，当连接每应用 VPN 时，这些域可以绕过 VPN 连接。

可以在“设备” > “配置文件” > “创建配置文件” > “iOS/iPadOS”或“macOS”[针对平台] >“VPN”[针对配置文件] >“自动 VPN”中配置自动 VPN 配置文件。

有关关联域的详细信息，请参阅[关联域](../configuration/device-features-configure.md#associated-domains)。

若要查看可配置的设置，请参阅[为 iOS/iPadOS 设备设置每应用虚拟专用网络 (VPN)](../configuration/vpn-setting-configure-per-app.md#create-a-per-app-vpn-profile)。

适用于：
- iOS/iPadOS 14 及更高版本
- macOS Big Sur (macOS 11)

### <a name="cope-preview-update-new-settings-to-configure-the-personal-profile-for-android-enterprise-corporate-owned-devices-with-a-work-profile---7086356----"></a>COPE 预览更新：用于为 Android Enterprise 公司拥有的工作配置文件设备配置个人配置文件的新设置<!-- 7086356  -->
对于 Android Enterprise 公司拥有的工作配置文件设备，可以配置一些仅适用于个人配置文件的新设置（“设备” > “配置文件” > “创建配置文件” > “Android Enterprise”[针对平台] >“公司拥有的完全托管式专用工作配置文件” > “设备限制”[针对配置文件] >“个人配置文件”）：

- **照相机**：使用此设置可在个人使用期间禁止访问照相机。
- **屏幕捕获**：使用此设置可在个人使用期间禁止屏幕捕获。
- **允许用户在个人配置文件中安装来自未知来源的应用**：使用此设置可以允许用户在个人配置文件中安装来自未知来源的应用。 

若要查看可以配置的当前设置，请转到[用于允许或限制功能的 Android Enterprise 设备设置](../configuration/device-restrictions-android-for-work.md)。

### <a name="block-app-clips-on-iosipados-and-defer-non-os-software-updates-on-macos-devices---7518422----"></a>在 iOS/iPadOS 上阻止应用剪辑，在 macOS 设备上延迟非 OS 软件更新<!-- 7518422  -->
在 iOS/iPadOS 和 macOS 设备上创建设备限制配置文件时，会有一些新设置：

**iOS/iPadOS 14.0+ 阻止应用剪辑**
- 适用于 iOS/iPadOS 14.0 及更高版本。
- 必须使用设备注册或自动设备注册（受监督的设备）来注册设备。
- “阻止应用剪辑”设置可阻止托管设备上的应用剪辑（“设备” > “配置文件” > “创建配置文件” > “iOS/iPadOS”[针对平台] >“设备限制”[针对配置文件] >“常规”）。 被阻止时，用户无法添加任何应用剪辑，并且系统会从设备中删除所有现有的应用剪辑。  

**macOS 11+ 延迟软件更新**
- 适用于 macOS 11 及更高版本。 在受监督的 macOS 设备上，设备必须具有用户批准的设备注册，或通过自动设备注册进行注册。
- “延迟软件更新”设置会延迟用户对非 OS 软件更新的可见性（“设备” > “配置文件” > “创建配置文件” > “macOS”[针对平台] >“设备限制”[针对配置文件] >“常规”）。 如果延迟这些更新，则只有在延迟期过后，用户才能看到新发布的更新；延迟期使用“延迟软件更新的可见性”设置进行配置。 延迟非操作系统软件更新不会影响计划的更新。
- 现有“延迟软件更新”设置将与此新设置结合使用。 使用新设置可以延迟 OS 软件更新和非 OS 软件更新。 可以继续使用“延迟软件更新的可见性”设置来设置天数，该天数将同时应用于这两个软件更新延迟设置。
- 不会更改、影响或删除现有策略的行为。 现有策略将自动迁移到具有相同配置的新设置。

### <a name="disable-mac-address-randomization-on-wi-fi-networks-on-iosipados-devices---7758689----"></a>对 iOS/iPadOS 设备上的 Wi-Fi 网络禁用 MAC 地址随机化<!-- 7758689  -->
从 iOS/iPadOS 14 开始，默认情况下，设备在连接到网络时会提供一个随机 MAC 地址，而不是物理 MAC 地址。 建议将此行为用于隐私保护，因为它可以增加通过 MAC 地址跟踪设备的难度。 此功能还会中断依赖静态 MAC 地址的功能，包括网络访问控制 (NAC)。 

可以在 Wi-Fi 配置文件中按网络禁用 MAC 地址随机化（“设备” > “配置文件” > “创建配置文件” > “iOS/iPadOS”[针对平台] >“Wi-Fi”[针对配置文件] >“基本”或“企业”[针对 Wi-Fi 类型]）。

若要查看当前可配置的设置，请转到[添加适用于 iOS 和 iPadOS 设备的 Wi-Fi 设置](../configuration/wi-fi-settings-ios.md)。

适用于：
- iOS/iPadOS 14 及更高版本

### <a name="set-maximum-transmission-unit-for-ikev2-vpn-connections-on-iosipados-devices---7758937----"></a>在 iOS/iPadOS 设备上设置 IKEv2 VPN 连接的最大传输单位<!-- 7758937  -->
从 iOS/iPadOS 14 及更高版本的设备开始，可以在使用 IKEv2 VPN 连接时配置自定义最大传输单位 (MTU)（“设备” > “配置文件” > “创建配置文件” > “iOS/iPadOS”[针对平台] >“VPN”[针对配置文件] ->“IKEv2”[针对连接类型]）。

有关可配置的设置的详细信息，请参阅 [IKEv2 设置](../configuration/vpn-settings-ios.md#ikev2-settings)。

适用于：
- iOS/iPadOS 14 及更高版本

### <a name="per-account-vpn-connection-for-email-profiles-on-iosipados-devices---7759116----"></a>iOS/iPadOS 设备上的电子邮件配置文件的每帐户 VPN 连接<!-- 7759116  -->
从 iOS/iPadOS 14 开始，可以根据用户所使用的帐户，通过 VPN 来路由本机 Mail 应用的电子邮件流量。 现在，可以指定要用于此基于帐户的 VPN 连接的每应用 VPN 配置文件。  当用户在 Mail 应用中使用其组织帐户时，每应用 VPN 连接将自动打开。

若要查看当前可配置的设置，请转到[添加适用 iOS 和 iPadOS 设备的电子邮件设置](../configuration/email-settings-ios.md)。

适用于：
- iOS/iPadOS 14 及更高版本

### <a name="use-netmotion-as-a-vpn-connection-type-for-android-enterprise-work-profile-devices---7764263---"></a>将 NetMotion 用作 Android Enterprise 工作配置文件设备的 VPN 连接类型<!-- 7764263 -->
创建 VPN 配置文件时，NetMotion 可用作 VPN 连接类型（“设备” > “设备配置” > “创建配置文件” > “Android Enterprise 工作配置文件”[针对平台] >“VPN”[针对配置文件] >“NetMotion”[针对连接类型]）。

有关 Intune 中 VPN 配置文件的详细信息，请参阅[创建 VPN 配置文件以连接到 VPN 服务器](../configuration/vpn-settings-configure.md)。

适用于：
- Android Enterprise 工作配置文件

### <a name="changes-for-password-settings-in-device-restriction-profiles-for-android-device-administrator---7662279----"></a>Android 设备管理员的设备限制配置文件中的密码设置更改<!-- 7662279  --> 
我们将为 Android 设备管理员的设备限制和合规性策略的密码设置引入一些更改。 （“设备” > “配置文件” > “创建配置文件” > “设备限制”和“设备” > “合规性策略” > “创建策略”）这些更改可帮助 Intune 适应 Android 10 及更高版本中的更改，以确保密码设置继续按预期方式应用于设备。
 
具体更改包括：
- 删除“密码”的顶级选项。  
- 设置将根据其应用到的设备重新组织为多个部分。
- 除非将“密码类型”配置为适用密码长度的值，否则将禁用“最短密码长度”。
- 对标签和示例文本的其他更新。

这些更改将应用于设置的 UI，而不会影响现有配置文件。 

<!-- ***********************************************-->
## <a name="device-enrollment"></a>设备注册

### <a name="ending-support-for-ios-11--7327321---"></a>结束对 iOS 11 的支持<!--7327321 -->
iOS 14 发布后，Intune 注册和公司门户应用将支持 iOS 12 及更高版本。 旧版本不再受支持，但会继续接收策略。

### <a name="ending-support-for-macos-1012--7327326---"></a>结束对 macOS 10.12 的支持<!--7327326 -->
macOS 11 发布后，Intune 注册和公司门户将支持 macOS 10.13 及更高版本。 旧版本不再受支持。


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

### <a name="deploy-software-updates-to-macos-devices----3194876---"></a>将软件更新部署到 macOS 设备 <!-- 3194876 -->
你将能够把软件更新部署到 macOS 设备组。 此功能包括关键更新、固件更新、配置文件更新和其他更新。 你将能够在下一次设备签入时发送更新，或选择每周计划在你设置的时间范围内外部署更新。 当你想要在非标准工作时间更新设备时，或者当支持人员已满员时，这会很有帮助。 你还将获得所有已部署更新的 macOS 设备的详细报告。 可以按设备向下钻取报告，以查看特定更新的状态。

### <a name="cope-preview-update-reset-work-profile-password-for-android-enterprise-corporate-owned-devices-with-a-work-profile---7217228---"></a>COPE 预览更新：为 Android Enterprise 公司拥有的工作配置文件设备重置工作配置文件密码 <!--7217228 -->
将来的管理员操作将使管理员能够在 Android Enterprise 公司拥有的工作配置文件设备上重置工作配置文件密码。

### <a name="rename-a-co-managed-device-that-is-azure-active-directory-joined--7728043---"></a>重命名已加入 Azure Active Directory 的共同管理设备<!--7728043 -->
你将能够重命名已加入 Azure AD 的共同管理设备。 为此，请转到 MEM >“设备” > “所有设备”> 选择设备 >“...” > “重命名设备”。

### <a name="support-for-powerprecision-and-powerprecision-batteries-for-zebra-devices--3724987---"></a>支持 Zebra 设备的 PowerPrecision 和 PowerPrecision+ 电池<!--3724987 -->
在设备的硬件详细信息页面上，你将能够看到有关使用 PowerPrecision 和 PowerPrecision+ 电池的 Zebra 设备的以下信息：
- 由 Zebra 决定的运行状况等级（仅限 PowerPrecision+ 电池）
- 已消耗的完整充电周期数
- 上次在设备中找到的电池的上次签入日期
- 上次在设备中找到的电池组的序列号

<!-- ***********************************************-->
## <a name="intune-apps"></a>Intune 应用

### <a name="unified-delivery-of-azure-ad-enterprise-and-office-online-applications-in-the-windows-company-portal---1817861----"></a>在 Windows 公司门户中统一交付 Azure AD 企业应用程序和 Office Online 应用程序<!-- 1817861  -->
在 2006 版中，我们推出了[在公司门户中统一交付 Azure AD 企业应用程序和 Office Online 应用程序](../fundamentals/whats-new.md#unified-delivery-of-azure-ad-enterprise-and-office-online-applications-in-the-company-portal)。 Windows 公司门户将支持此功能。 在 Intune 的“自定义”窗格上，你将能够选择在 Windows 公司门户中同时隐藏或显示 Azure AD 企业应用程序和 Office Online 应用程序    。 每位最终用户将从所选的 Microsoft 服务中看到其整个应用程序目录。 默认情况下，每个附加的应用源会设置为“隐藏”。 在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，你将选择“租户管理” > “自定义”来查找此配置设置 。 如需了解相关信息，请参阅[如何自定义 Intune 公司门户应用、公司门户网站和 Intune 应用](../apps/company-portal-app.md)。
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>监视和故障排除

### <a name="power-bi-compliance-report-template-v20---636958----"></a>Power BI 合规性报告模板 V2.0<!-- 636958  -->
管理员能够将 Power BI 合规性报表模板的版本从 V1.0 更新到 V2.0。 V2.0 将包括改进后的设计，以及对作为模板一部分出现的计算和数据的更改。 如需了解相关信息，请参阅[使用 Power BI 连接到数据仓库](../developer/reports-proc-get-a-link-powerbi.md)。


### <a name="new-and-improved-microsoft-defender-antivirus-reporting-for-windows-10-and-newer---6018169----"></a>适用于 Windows 10 及更高版本的新的和改进的 Microsoft Defender 防病毒报告功能<!-- 6018169  -->
我们将在 Windows 10 上的“终结点安全性” > “防病毒”下添加四个新的 Microsoft Defender 防病毒报告。
- 两个操作报告：“检测到恶意软件的设备”和“代理状态”。
- 两个组织报告：“检测到恶意软件”和“代理状态”。

例如，操作报告“代理状态”将一目了然地显示设备名称、用户名、用户电子邮件和 UPN，以及是否启用了实时保护和网络保护。 当这些报告可供使用时，我们将分享更多详细信息。

有关 Intune 中的终结点安全性的详细信息，请参阅[在 Microsoft Intune 中管理终结点安全性](../protect/endpoint-security.md)。

### <a name="analyze-your-on-premises-gpos-using-group-policy-analytics-preview--7200950---"></a>使用组策略分析（预览版）分析本地 GPO<!--7200950 -->
在“设备” > “组策略分析(预览版)”中，可以导入 Endpoint Manager 管理中心的组策略对象 (GPO)。 导入时，Intune 会自动分析 GPO，并显示在 Intune 中具有等效设置的策略。 它还会显示已弃用或不再受支持的 GPO。

适用于：
- Windows 10 及更高版本

#### <a name="new-windows-10-feature-update-report---6473121-----"></a>新的 Windows 10 功能更新报告<!-- 6473121   -->
“功能更新失败”报告将为“Windows 10 功能更新”策略所面向的、已尝试更新的设备提供失败详细信息。 在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，你将选择“设备” > “监视” > “功能更新失败”来查看此报告。

#### <a name="new-windows-10-feature-update-report---6473128----"></a>新的 Windows 10 功能更新报告<!-- 6473128  -->
“Windows 功能更新”报告将为“Windows 10 功能更新”策略面向的设备提供总体合规性视图。 在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，你将选择“报告” > “Windows 更新(预览版)” > “功能更新失败”来查看此报告的摘要。 若要查看特定策略的报告，请选择“报告”选项卡，然后打开“Windows 功能更新报告”。 

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

### <a name="improved-certificate-deployment-for-android-enterprise----6296499----"></a>改进了 Android Enterprise 的证书部署 <!-- 6296499  -->
运行 Android Enterprise 公司拥有的完全托管式专用工作配置文件的设备很快就能够在 Outlook 中使用 S/MIME 证书，而无需设备用户授予访问权限。 通过在设备配置中使用 PKCS 导入的证书配置文件，可部署 S/MIME 证书。 （“设备” > “配置文件” > “创建配置文件” > “Android Enterprise” > “公司拥有的完全托管式专用工作配置文件”类别中的“PKCS 导入的证书”）。

### <a name="tri-state-options-for-settings-are-coming-to-endpoint-security-firewall-policy---6586159-----"></a>即将在终结点安全性防火墙策略中添加设置的三态选项<!-- 6586159   -->
我们将在终结点安全性防火墙策略中添加设置的三态配置，其中，平台（Windows 或 macOS）可以支持附加选项（“终结点安全性” > “防火墙”）。

例如，如果某个设置当前提供“未配置”和“是”，则在平台支持的情况下，我们将添加选项“否”。

### <a name="new-security-baseline-for-office---3150261----"></a>新的 Office 安全基线<!-- 3150261  -->
我们将添加新的安全基线（“终结点安全性” > “安全基线”）来管理 Microsoft Office O365 的设置。 基线中的设置将包括 Office 应用的配置，例如加载项管理、MIME 处理等。

### <a name="improved-status-details-in-security-baseline-reports---7221051------"></a>改进了安全基线报告中的状态详细信息<!-- 7221051    -->
我们将改进你在查看已部署安全基线的结果时看到的状态详细信息。 （“终结点安全性” > “安全基线” >  选择安全基线类型，例如“Windows 10 安全基线” > “配置文件” > 选择该配置文件的实例以查看状态 > 选择配置文件报告，例如“设备状态”）

这些改进将修订我们用于状态的通用标签和定义，以更好地适应状态的意图。 例如：
- “与基线匹配”将更新为“与默认设置匹配”，后者更好地描述了识别设备配置何时匹配默认（未修改的）基线配置的意图。
- “错误配置”将细分为更具体的详细信息，例如“错误”、“冲突”和“挂起”。 新状态将使控制台的其他区域保持一致。

### <a name="expanded-rbac-permissions-for-the-endpoint-security-role--7312374--idstaged---"></a>扩展了终结点安全性角色的 RBAC 权限<!--7312374  idstaged -->
Intune 的“终结点安全性管理员”角色对远程任务的基于角色的访问控制 (RBAC) 权限将得到扩展。此角色可授予对 Microsoft Endpoint Manager 管理中心的访问权限，并且可供管理安全性和合规性功能（包括安全基线、设备合规性、条件访问和 Microsoft Defender 高级威胁防护）的人员使用。

若要查看 Intune RBAC 角色的权限，请转到（“租户管理员” > “Intune 角色” > 选择角色 > “权限”）。

针对远程任务的扩展权限包括：

- 立即重启
- 远程锁定
- 轮换 BitLocker 密钥（预览版）
- 轮换 FileVault 密钥
- 同步设备
- Microsoft Defender
- 启动配置管理器操作

### <a name="updates-for-security-baselines---7102146-7103916----"></a>安全基线更新<!-- 7102146, 7103916  -->
我们即将发布对以下安全基线（“终结点安全性” > “安全基线”）的更新：
- **MDM 安全基线**（Windows 10 安全性）
- **Microsoft Defender ATP 基线**

更新的基线版本引入了对最新设置的支持，以帮助维护各个产品团队推荐的最佳做法配置。

### <a name="use-endpoint-security-configuration-details-to-identify-the-source-of-policy-conflicts-for-devices---7567503--idstaged----"></a>使用终结点安全性配置详细信息来识别设备的策略冲突根源<!-- 7567503  idstaged  -->
为了帮助解决冲突，你很快就能深入到安全基线配置文件，以查看所选设备的终结点安全性配置。 在该处，你可以选择显示“冲突”或“错误”的设置，并继续深入，以查看包含属于冲突的配置文件和策略的详细信息列表。 如果你随后选择的策略是冲突根源，则 Intune 会打开策略“概述”窗格，你可以在其中查看或修改策略配置。 （“设备” > 选择设备 > “终结点安全性配置” > 选择配置文件或基线 > 从应用于设备的设置列表中选择一个设置）。

深入到安全基线时，可以将以下策略类型标识为冲突根源：
- 设备配置策略
- 终结点安全性策略

### <a name="new-details-in-the-endpoint-security-configuration-for-a-device---7745029-----"></a>设备终结点安全性配置中的新详细信息<!-- 7745029   -->
我们将为设备添加新的详细信息，这些信息可作为设备终结点安全性配置的一部分进行查看。 （“终结点安全性” > “安全基线” > 所选基线 > “配置文件” > 所选配置文件 > “设备状态” > “终结点安全性配置”）。 新的详细信息：

- **UPN**（用户主体名称）：UPN 用于标识哪个终结点安全性配置文件分配给设备上的给定用户。 这有助于区分设备上的多个用户和分配给设备的配置文件或基线的多个条目。 
- **最差状态**：此详细信息用于标识设备的最差状态条件。 如果此状态为“成功”，则表示设备没有策略冲突或错误。

### <a name="android-11-deprecates-deployment-of-trusted-root-certificates-to-device-administrator-enrolled-devices--7662775----"></a>Android 11 不支持将受信任的根证书部署到设备管理员注册的设备<!--7662775  -->
在 Android 11 中，再也无法将受信任的根证书部署到以 Android 设备管理员身份注册的设备。 由于 Intune 与 Knox 平台的集成，此更改不会影响 Samsung Knox 设备。 对于非 Samsung 设备，用户必须在设备上手动安装受信任的根证书。 

在设备上手动安装受信任的根证书之后，便可使用 SCEP 将证书预配给设备。 在这种情况下，仍需创建受信任证书策略并将其部署到设备，同时将该策略链接到 SCEP 证书配置文件。

- 如果设备上有受信任的根证书，则 SCEP 证书配置文件将安装成功。 
- 如果找不到受信任的证书，则 SCEP 证书配置文件将失败。

<!-- ***********************************************-->
## <a name="notices"></a>通知

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>另请参阅

有关最近开发的详细信息，请参阅 [Microsoft Intune 中的新增功能](whats-new.md)。