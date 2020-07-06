---
title: Microsoft Intune 中的新增功能 - Azure | Microsoft Docs
titleSuffix: ''
description: 了解 Intune Azure 门户新增功能
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/25/2020
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
ms.openlocfilehash: 89703c8aec11517417f9459391c431b9db75456c
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2020
ms.locfileid: "85502283"
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
### Scripts


<!-- ########################## -->

## <a name="week-of-june-22-2020"></a>2020 年 6 月 22 日当周

### <a name="app-management"></a>应用管理

#### <a name="newly-available-protected-apps-for-intune---7248952---"></a>新提供的适用于 Intune 的受保护应用<!-- 7248952 -->
现在提供了以下受保护的应用：
- BlueJeans 视频会议
- Cisco Jabber for Intune
- Tableau Mobile for Intune
- ZERO for Intune

有关受保护应用的详细信息，请参阅[受 Microsoft Intune 保护的应用](../apps/apps-supported-intune-apps.md)。

### <a name="monitor-and-troubleshoot"></a>监视和故障排除

#### <a name="use-endpoint-analytics-to-improve-user-productivity-and-reduce-it-support-costs---5653063---"></a>使用终结点分析来提高用户工作效率并降低 IT 支持成本<!-- 5653063 --> 
在接下来的一周内，此功能将会推出。终结点分析旨在通过提供用户体验见解来提高用户工作效率，并降低 IT 支持成本。 通过这些见解，IT 可以使用主动支持来优化最终用户体验，并通过评估配置更改对用户的影响来检测用户体验回归。 有关详细信息，请参阅[终结点分析（预览）](https://aka.ms/uea)。

#### <a name="proactively-remediate-end-user-device-issues-using-script-packages---5933328---"></a>使用脚本包主动修正最终用户设备问题<!-- 5933328 -->
你可以在最终用户设备上创建和运行脚本包，以主动查找和修复组织中的主要支持问题。 部署脚本包将有助于减少支持调用。 选择自行创建脚本包，也可部署我们编写并在我们的环境中使用的某个脚本包，以减少支持工单。 借助 Intune，可查看已部署脚本包的状态，并监视检测和修正结果。 在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，选择“报表” > “终结点分析” > “主动修正”  。 有关详细信息，请参阅[主动修正](https://aka.ms/uea_prs)。

### <a name="device-security"></a>设备安全性

#### <a name="use-microsoft-defender-atp-in-compliance-policies-for-android---4425686----"></a>在面向 Android 的合规性策略中使用 Microsoft Defender ATP<!-- 4425686  -->

现在你可以使用 Intune [将 Android 设备载入到 Microsoft Defender 高级威胁防护](../protect/advanced-threat-protection.md#onboard-android-devices)。 载入注册的设备后，面向 Android 的合规性策略可以使用来自 Microsoft Defender ATP 的威胁级别信号。 这些信号与先前可以用于 Windows 10 设备的信号相同。

#### <a name="configure-defender-atp-web-protection-for-android-devices---6185563-wnready---"></a>配置面向 Android 设备的 Defender ATP Web 保护<!-- 6185563 WNReady -->

当使用面向 Android 设备的 Microsoft Defender 高级威胁防护 (Microsoft Defender ATP) 时，可以[配置 Microsoft Defender ATP Web 保护](../protect/advanced-threat-protection.md#configure-web-protection-on-devices-that-run-android)以禁用钓鱼网站扫描功能，或阻止扫描使用 VPN。

根据 Android 设备注册 Intune 的方式，可用选项如下：

- Android 设备管理员 - 使用自定义 OMA-URI 设置禁用 Web 保护功能，或仅在扫描期间禁用 VPN。
- Android 企业工作配置文件 - 使用应用配置文件和配置设计器禁用所有 Web 保护功能。

## <a name="week-of-june-15-2020--2006-service-release"></a>2020 年 6 月 15 日当周（2006 服务版本）

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>应用管理  

#### <a name="telecommunications-data-transfer-protection-for-managed-apps---6884491----"></a>托管应用的电信数据传输保护<!-- 6884491  -->
当在受保护的应用中检测到超链接电话号码时，Intune 将检查是否应用了允许将该号码传输到拨号程序应用的保护策略。 你可以选择当从策略托管的应用启动电话号码时要如何处理此类型的内容传输。 在 Microsoft Endpoint Manager 中创建应用保护策略时，请从“将组织数据发送到其他应用”中选择一个托管的应用选项，然后从“将电信数据传输到”中选择一个选项 。 有关此数据保护设置的详细信息，请参阅 [Microsoft Intune 中的 Android 应用保护策略设置](../apps/app-protection-policy-settings-android.md)和 [iOS 应用保护策略设置](../apps/app-protection-policy-settings-ios.md)。 

#### <a name="unified-delivery-of-azure-ad-enterprise-and-office-online-applications-in-the-company-portal---7414033----"></a>在公司门户中统一交付 Azure AD 企业应用程序和 Office Online 应用程序<!-- 7414033  -->
在 Intune 的“自定义”窗格上，可以选择在公司门户中同时隐藏或显示 Azure AD 企业应用程序和 Office Online 应用程序    。 每位最终用户将从所选的 Microsoft 服务中看到其整个应用程序目录。 默认情况下，每个附加的应用源会设置为“隐藏”。 此功能将首先在公司门户网站中生效，并应兼容 Windows 公司门户中的支持。 在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，选择“租户管理” > “自定义”，查找此配置设置 。 如需了解相关信息，请参阅[如何自定义 Intune 公司门户应用、公司门户网站和 Intune 应用](../apps/company-portal-app.md)。

#### <a name="improvements-to-the-company-portal-for-macos-enrollment-experience---6444452----"></a>对公司门户中的 macOS 注册体验的改进<!-- 6444452  -->
用于 macOS 注册的公司门户提供的注册过程更简单，与用于 iOS 注册的公司门户高度一致。 设备用户将看到：  
- 流畅的用户界面。  
- 改进的注册清单。  
- 更清晰的设备注册说明。  
- 改进的疑难解答选项。  

有关公司门户的详细信息，请参阅[如何自定义 Intune 公司门户应用、公司门户网站和 Intune 应用](../apps/company-portal-app.md)。

#### <a name="improvements-to-devices-page-of-iosipados-and-macos-company-portals---6055001---"></a>对 iOS/iPadOS 和 macOS 公司门户“设备”页的改进<!-- 6055001 -->
我们已经对公司门户“设备”页面进行了更改，以改进 iOS/iPadOS 和 Mac 用户的应用体验。 除创建更现代的外观和使用体验之外，我们还将设备详细信息重新组织到了具有定义的节标头的单个列下，以便用户可以更轻松地查看其设备状态。 我们还为设备不合规的用户添加了更为清晰的消息传送和故障排除步骤。 有关公司门户的详细信息，请参阅[如何自定义 Intune 公司门户应用、公司门户网站和 Intune 应用](../apps/company-portal-app.md)。 若要手动同步设备，请参阅[手动同步 iOS 设备](../user-help/sync-your-device-manually-ios.md)。  

#### <a name="cloud-setting-for-iosipados-company-portal-app---7071303----"></a>适用于 iOS/iPadOS 公司门户应用的云设置<!-- 7071303  -->
iOS/iPadOS 公司门户新的“云”设置允许用户将其身份验证重定向到适合组织的相应云。 默认情况下，该设置配置为“自动”，这会将身份验证定向到用户设备自动检测到的云。 如果必须将组织的身份验证重定向到自动检测到的云以外的云（如公共或政府），则用户可以通过选择“设置”应用 >“公司门户” > “云”手动选择相应云  。 如果用户是从另一台设备登录，并且其设备未自动检测到相应云，则应只能从“自动”更改“云”设置 。 

#### <a name="duplicate-apple-vpp-tokens---7101606----"></a>复制 Apple VPP 令牌<!-- 7101606  -->
具有相同“令牌位置”的 Apple VPP 令牌现在标记“重复”，并且可以在删除重复令牌后再次同步 。 你仍然可以为标记为重复的令牌分配和撤销许可证。 但是，令牌标记为重复后，购买的新应用和书籍的许可证可能不会反映出来。 若要查找租户的 Apple VPP 令牌，请从 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，选择“租户管理” > “连接器和令牌” > “Apple VPP 令牌”  。 有关 VPP 令牌的详细信息，请参阅[如何使用 Microsoft Intune 管理通过 Apple Volume Purchase Program 购买的 iOS 和 macOS 应用](../apps/vpp-apps-ios.md)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>设备配置

#### <a name="add-multiple-root-certificates-for-eap-tls-authentication-in-wi-fi-profiles-on-macos-devices---2077871----"></a>在 macOS 设备的 Wi-Fi 配置文件中为 EAP-TLS 身份验证添加多个根证书<!-- 2077871  -->

在 macOS 设备上，可以创建 Wi-Fi 配置文件，并选择可扩展身份验证协议 (EAP) 身份验证类型（“设备” > “配置配置文件” > “创建配置文件” > “macOS”（作为平台）>“Wi-Fi”（作为配置文件）>“Wi-Fi 类型”设置为 Enterprise）     。

将“EAP Type”设置为“EAP-TLS”、“EAP-TTLS”或“PEAP”身份验证时，可以添加多个根证书   。 以前，只能添加一个根证书。

有关可以配置的设置的详细信息，请参阅[在 Microsoft Intune 中添加适用于 macOS 设备的 Wi-Fi 设置](../configuration/wi-fi-settings-macos.md)。

适用于：
- macOS

#### <a name="use-pkcs-certificates-with-wi-fi-profiles-on-windows-10-and-newer-devices---3246388-----"></a>在 Windows 10 及更高版本设备上的 Wi-Fi 配置文件中使用 PKCS 证书<!-- 3246388   -->
可以使用 SCEP 证书对 Windows Wi-Fi 配置文件进行身份验证（“设备配置” > “配置文件” > “创建配置文件” > “Windows 10 和更高版本”（作为平台）>“Wi-Fi”（作为配置文件类型）>“Enterprise” > “EAP 类型”      ）。 现在，你可以在 Windows Wi-Fi 配置文件中使用 PKCS 证书。 此功能允许用户使用租户中新的或现有的 PKCS 证书配置文件对 Wi-Fi 配置文件进行身份验证。 

有关可以配置的 Wi-Fi 设置的详细信息，请参阅[在 Intune 中添加适用于 Windows 10 及更高版本设备的 Wi-Fi 设置](../configuration/wi-fi-settings-windows.md)。

适用于：
- Windows 10 及更高版本

#### <a name="wired-network-device-configuration-profiles-for-macos-devices---3508686----"></a>macOS 设备的有线网络设备配置文件<!-- 3508686  -->
可使用新的 macOS 设备配置文件来配置有线网络（“设备”>“配置配置文件”>“创建配置文件” > “macOS”（作为平台）>“有线网络”（作为配置文件））   。 使用此功能创建 802.1x 配置文件来管理有线网络，并将这些有线网络部署到 macOS 设备。

有关此功能的详细信息，请参阅 [macOS 设备上的有线网络](../configuration/wired-networks-configure.md)。

适用于：
- macOS

#### <a name="use-microsoft-launcher-as-the-default-launcher-for-fully-managed-android-enterprise-devices---4927976-----"></a>使用微软桌面作为完全托管的 Android Enterprise 设备的默认启动程序<!-- 4927976   -->
在 Android Enterprise 设备所有者设备上，可以将微软桌面设置为完全托管的设备的默认启动程序（“设备” > “配置文件” > “创建配置文件” >  针对平台选择“Android Enterprise”>“设备所有者” >  针对配置文件选择“设备限制”>“设备体验”）。 若要配置所有其他微软桌面设置，请使用[应用配置策略](../apps/configure-microsoft-launcher.md)。 

此外，还有一些其他 UI 更新，包括将“专用设备”重命名为“设备体验”。

要查看可以限制的所有设置，请参阅[使用 Intune 允许或限制功能的 Android Enterprise 设备设置](../configuration/device-restrictions-android-for-work.md)。 

适用于：
- Android Enterprise 设备所有者完全托管的设备 (COBO)

#### <a name="use-autonomous-single-app-mode-settings-to-configure-the-ios-company-portal-app-to-be-a-sign-insign-out-app---7055619-----"></a>使用自治单应用模式设置将 iOS 公司门户应用配置为登录/注销应用<!-- 7055619   -->
在 iOS/iPadOS 设备上，可以将应用配置为在自治单应用模式 (ASAM) 下运行。 现在，公司门户应用支持 ASAM，并且可以配置为“登录/注销”应用。 在此模式下，用户必须登录到公司门户应用才能使用设备上的其他应用和“主屏幕”按钮。 当用户注销公司门户应用时，设备将返回到单应用模式，并在公司门户应用上锁定。

若要将公司门户配置为 ASAM，请转到“设备” > “配置配置文件” > “创建配置文件” > “iOS/iPadOS”（作为平台）>“设备限制”（作为配置文件）>“自治单应用模式”     。

有关详细信息，请参阅[自治单应用模式 (ASAM)](../configuration/device-restrictions-ios.md#autonomous-single-app-mode-asam) 和[单应用模式](https://support.apple.com/guide/mdm/single-app-mode-mdm80a981/1/web/1)（打开 Apple 的网站）。

适用于：
- iOS/iPadOS

#### <a name="configure-content-caching-on-macos-devices---7106872-----"></a>在 macOS 设备上配置内容缓存<!-- 7106872   -->
在 macOS 设备上，可以创建配置内容缓存的配置文件（“设备” > “配置文件” > “创建配置文件” >  针对平台选择“macOS” > 针对配置文件选择“设备功能”）。 使用这些设置可以删除缓存，允许共享缓存，设置磁盘上的缓存限制等。

有关内容缓存的详细信息，请参阅 [ContentCaching](https://developer.apple.com/documentation/devicemanagement/contentcaching)（打开 Apple 的网站）。

若要查看可配置的设置，请转到 [Intune 中的 macOS 设备功能设置](../configuration/macos-device-features-settings.md)。

适用于：
- macOS

#### <a name="add-new-schema-settings-and-search-for-existing-schema-settings-using-oemconfig-on-android-enterprise---6394386-----"></a>添加新架构设置，并使用 Android Enterprise 上的 OEMConfig 搜索现有架构设置<!-- 6394386   -->
在 Intune 中，可以使用 OEMConfig 来管理 Android Enterprise 设备上的设置（“设备” > “配置文件” > “创建配置文件” >  针对平台选择“Android Enterprise”> 针对配置文件选择“OEMConfig”）。 使用“配置设计器”时，将显示应用架构中的属性。 现在可在“配置设计器”中执行以下操作：

- 向应用架构添加新设置。
- 在应用架构中搜索新设置和现有设置。

若要详细了解 Intune 中的 OEMConfig 配置文件，请参阅[通过 Microsoft Intune 中的 OEMConfig 使用和管理 Android Enterprise 设备](../configuration/android-oem-configuration-overview.md)。

适用于：
- Android Enterprise

#### <a name="block-shared-ipad-temporary-sessions-on-shared-ipad-devices---6613794----"></a>阻止共享 iPad 设备上的共享 iPad 临时会话<!-- 6613794  -->
在 Intune 中，有一个新的“阻止共享 iPad 临时会话”设置，可阻止共享 iPad 设备上的临时会话（“设备” > “配置文件” > “创建配置文件”： >  针对平台选择“iOS/iPadOS”> 针对配置文件类型选择“设备限制”>“共享 iPad”）。 启用后，最终用户无法使用来宾帐户。 他们必须使用其管理的 Apple ID 和密码登录设备。 

有关详细信息，请参阅[便于允许或限制功能的 iOS 和 iPadOS 设备设置](../configuration/device-restrictions-ios.md)。

适用于：
- 运行 iOS/iPadOS 13.4 及更高版本的共享 iPad 设备

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>设备注册

#### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344----"></a>自带设备可以使用 VPN 进行部署<!--5015344  -->
使用新的 Autopilot 配置文件“跳过域连接检查”切换，可以部署混合 Azure AD 联接设备，而无需使用自己的第三方 Win32 VPN 客户端访问企业网络。 若要查看新的切换，请前往 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431) > “设备”  > “Windows” > “Windows 注册” > “部署配置文件” > “创建配置文件” > “全新体验 (OOBE)”     。

#### <a name="enrollment-status-page-profiles-can-be-set-to-device-groups--3952138---"></a>注册状态页配置文件可以设置为设备组<!--3952138 -->
以前，注册状态页 (ESP) 配置文件只能针对用户组。 现在，还可以将其设置为面向设备组。 有关详细信息，请参阅[设置注册状态页](../enrollment/windows-enrollment-status.md)。

#### <a name="automated-device-enrollment-sync-errors---6988214---"></a>自动设备注册同步错误<!-- 6988214 -->
将为 iOS/iPadOS 和 macOS 设备报告新错误，包括：
- 电话号码中的字符无效或该字段为空。 
- 配置文件的配置名称无效或为空。 
- 游标值无效/过期或找不到游标。
- 令牌被拒绝或已过期。 
- 部门字段为空或长度过长。 
- Apple 找不到配置文件，需要创建一个新配置文件。 
- 删除的 Apple Business Manager 设备的计数将添加到“概览”页，可以在其中看到设备状态。

#### <a name="shared-ipads-for-business--6367326-----"></a>适用于企业的共享 iPad<!--6367326   -->
可以使用 Intune 和 Apple Business Manager 轻松、安全地设置共用的 iPad，使多个员工可以共享设备。 Apple 的[共享 iPad](https://developer.apple.com/education/shared-ipad/) 可以为多个用户提供个性化的体验，同时保留用户数据。 借助托管 Apple ID，用户在登录组织中的任何共享 iPad 后即可访问他们的应用、数据和设置。 共享 iPad 使用联合标识。

为了了解此功能，请转到[Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431) > “设备” > “iOS” > “iOS 注册” > “注册计划令牌”> 选择令牌** >“配置文件” > “创建配置文件” > “iOS”      。 在“管理设置”页上，选择“不使用用户关联注册”，你会看到“共享 iPad”选项  。

需要：iPadOS 13.4 及更高版本。 此版本添加了对使用共享 iPad 的临时会话的支持，因此用户不使用托管 Apple ID 也可访问设备。 注销后，设备会清除所有用户数据，以便立即准备投入使用，因此无需擦除设备。 

#### <a name="updated-user-interface-for-apples-automated-device-enrollment--7430322---"></a>Apple 的自动设备注册的更新用户界面<!--7430322 -->
用户界面已经更新，已将 Apple 的设备注册计划替换为反映 Apple 术语的自动设备注册。


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>设备管理

#### <a name="device-remote-lock-pin-available-for-macos--7281557-----"></a>可用于 macOS 的设备远程锁定固定<!--7281557   -->
macOS 设备远程锁定固定的可用时间已从 7 天增至 30 天。

#### <a name="change-primary-user-on-co-managed-devices--7319183----"></a>更改共同管理的设备上的主要用户<!--7319183  -->
你可以为共同管理的 Windows 设备更改设备的主要用户。 有关如何查找和更改主要用户的详细信息，请参阅[查找 Intune 设备的主要用户](../remote-actions/find-primary-user.md)。 此功能将在接下来的几周内逐步推出。

#### <a name="setting-the-intune-primary-user-also-sets-the-azure-ad-owner-property--7319227---"></a>设置 Intune 主要用户还会设置 Azure AD 所有者属性<!--7319227 -->
此新功能在设置 Intune 主要用户的同时，还将自动设置新注册的已加入混合 Azure AD 的设备上的所有者属性。 有关主要用户的详细信息，请参阅[查找 Intune 设备的主要用户](../remote-actions/find-primary-user.md)。

这是对注册过程的更改，并且仅适用于新注册的设备。 对于现有混合 Azure AD 联接设备，必须手动更新 Azure AD 所有者属性。 为此，可以使用[更改主要用户功能](../remote-actions/find-primary-user.md#change-a-devices-primary-user)或[脚本](https://github.com/microsoftgraph/powershell-intune-samples/tree/master/ManagedDevices)。

当 Windows 10 设备建立混合 Azure Active Directory 联接时，该设备的第一个用户将成为 Endpoint Manager 中的主要用户。  当前，未在相应的 Azure AD 设备对象上设置该用户。 在将 Azure AD 门户中的“所有者”属性与 Microsoft Endpoint Manager 管理中心中的“主要用户”属性进行比较时，这会导致不一致。 Azure AD 所有者属性用于保护对 BitLocker 恢复密钥的访问。 该属性未在混合 Azure AD 联接设备上填充。 此限制可防止从 Azure AD 设置 BitLocker 恢复的自助服务。 这一即将推出的功能可解决此限制。


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>设备安全性

#### <a name="hide-the-recovery-key-from-users-during-filevault-2-encryption-for-macos-devices---5459801----"></a>在对 macOS 设备进行 FileVault 2 加密期间向用户隐藏恢复密钥<!-- 5459801  -->
我们已向 [macOS Endpoint Protection](../protect/endpoint-protection-macos.md#filevault) 模板中的 FileVault 类别添加以下新设置：隐藏恢复密钥。 此设置将在 FileVault 2 加密过程中向最终用户隐藏个人密钥。 

若要查看加密 macOS 设备的个人恢复密钥，设备用户可以转到以下任意位置，然后单击 macOS 设备的“获取恢复密钥”： 

- IOS/iPadOS 公司门户应用
- Intune 应用
- 公司门户网站
- Android 公司门户应用

#### <a name="support-for-smime-signing-and-encryption-certificates-with-outlook-on-android-fully-managed--5896415-----"></a>支持 Android 完全托管上的 Outlook 的 S/MIME 签名和加密证书<!--5896415   -->
现在，可以在运行 Android Enterprise 完全托管的设备上对 Outlook 使用证书进行 S/MIME 签名和加密。

此内容是对上个月为其他 Android 版本添加的支持的补充（支持 Android 上的 Outlook 的 S/MIME 签名和加密证书）。 可以使用 SCEP 和 PKCS 导入的证书配置文件来预配这些证书。

有关此支持的详细信息，请参阅 Exchange 文档中的[适用于 iOS 和 Android 的敏感度标签和保护](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/sensitive-labeling-and-protection-outlook-for-ios-android)。

#### <a name="add-a-link-to-your-company-portal-support-website-to-emails-for-noncompliance---7225498------"></a>将指向公司门户支持网站的链接添加到设备不合规的用户的电子邮件中<!-- 7225498    -->
当[配置通知消息模板](../protect/actions-for-noncompliance.md#create-a-notification-message-template)用于发送有关不合规的电子邮件通知时，可使用新的设置“公司门户网站链接”来自动包含指向公司门户网站的链接。 将此选项设置为“启用”时，具有不合规设备的用户如果收到基于此模板的电子邮件，可以使用链接打开网站，以了解有关其设备不合规的原因的详细信息。 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="licensing"></a>许可

#### <a name="admins-no-longer-require-an-intune-license-to-access-microsoft-endpoint-manager-admin-console--1335430---"></a>管理员不再需要 Intune 许可证即可访问 Microsoft Endpoint Manager 管理控制台<!--1335430 -->
现在，你可以设置一个租户范围的切换，从而删除管理员访问 MEM 管理控制台和查询图形 API 的 Intune 许可要求。 删除许可证要求后，就不能再将其恢复。 



<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="scripts"></a>脚本 

#### <a name="availability-of-shell-scripts-on-macos-devices---7134839----"></a>macOS 设备上 Shell 脚本的可用性<!-- 7134839  -->
适用于 macOS 设备的 Shell 脚本现在可用于政府云和中国客户。 有关 shell 脚本的详细信息，请参阅[在 Intune 中的 macOS 设备上使用 Shell 脚本](../apps/macos-shell-scripts.md)。



<!-- ########################## -->
## <a name="week-of-june-8-2020"></a>2020 年 6 月 8 日当周   

### <a name="app-management"></a>应用管理  

#### <a name="updates-to-informational-screen-in-company-portal-for-iosipados---7032452---"></a>适用于 iOS/iPadOS 公司门户中信息屏幕的更新 <!--7032452 -->
适用于 iOS/iPadOS 公司门户中的信息屏幕已经更新，以更好地说明管理员可以在设备上看到和执行的操作。 这些说明仅涉及公司拥有的设备。 只更新了文本，没有对管理员可以在用户设备上看到或执行的操作进行实际修改。 若要查看更新后的屏幕，请转到 [Intune 最终用户应用的 UI 更新](./whats-new-app-ui.md)。

#### <a name="updated-android-app-conditional-launch-end-user-experience---5736084---"></a>更新的 Android 应用条件启动最终用户体验<!-- 5736084 -->
2006 年发布的 Android 公司门户网站在 2005 年版本更新的基础上进行了一些修改。 2005 年，我们推出了一项更新，在该更新中，应用保护策略发出警告、阻止或擦除的 Android 设备的最终用户可以看到一条完整的页面消息，描述发出警告、阻止或擦除的原因以及解决问题的步骤。 2006 年，首次分配应用保护策略的 Android 应用用户将通过引导流来解决导致其应用访问被阻止的问题。 

<!-- ########################## -->
## <a name="week-of-may-25-2020"></a>2020 年 5 月 25 日当周

### <a name="app-management"></a>应用管理

#### <a name="windows-32-bit-x86-apps-on-arm64-devices---5477661---"></a>ARM64 设备上的 Windows 32 位 (x86) 应用<!-- 5477661 -->
根据部署可用于 ARM64 设备的 Windows 32 位 (x86) 应用现将在公司门户中显示。 有关 Windows 32 位应用的详细信息，请参阅 [Win32 应用管理](../apps/apps-win32-app-management.md)。

#### <a name="windows-company-portal-app-icon---7114635---"></a>Windows 公司门户应用图标<!-- 7114635 -->
Windows 公司门户应用的图标已更新。 有关公司门户的更多详细信息，请参阅[如何自定义 Intune 公司门户应用、公司门户网站和 Intune 应用](../apps/company-portal-app.md)。


<!-- ########################## -->
## <a name="week-of-may-18-2020"></a>2020 年 5 月 18 日当周

### <a name="app-management"></a>应用管理  

#### <a name="update-to-icons-in-company-portal-app-for-iosipados-and-macos--6057697---"></a>更新公司门户中 iOS/iPadOS 和 macOS 应用的图标<!--6057697 -->
更新了公司门户中的图标，创建向 Microsoft Fluent Design System 看齐、双屏幕设备支持的时尚外观。 若要查看更新后的图标，请转到 [Intune 最终用户应用的 UI 更新](./whats-new-app-ui.md)。 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>设备安全性

#### <a name="use-endpoint-detection-and-response-policy-to-onboard-devices-to-defender-atp---7130165----"></a>使用终结点检测和响应策略将设备加入 Defender ATP<!-- 7130165  -->

使用终结点安全[策略来实现终结点检测和响应](../protect/endpoint-security-edr-policy.md) (EDR)，以便载入和配置用于 Microsoft Defender 高级威胁防护 (Defender ATP) 部署的设备。 EDR 支持由 Intune (MDM) 管理的 Windows 设备的策略，以及由 Configuration Manager 管理的 Windows 设备的独立策略。 

若要将策略用于 Configuration Manager 设备，必须[设置 Configuration Manager 以支持 EDR 策略](../protect/endpoint-security-edr-policy.md#set-up-configuration-manager-to-support-edr-policy)。 设置包括：

- 为 Configuration Manager 配置“租户附加”。
- 安装 Configuration Manager 的控制台内部更新，以启用对 EDR 策略的支持。 此更新仅适用于已启用租户附加的层次结构。
- 将你的设备集合从层次结构同步到 Microsoft Endpoint Manager 管理中心。


<!-- ########################## -->
## <a name="week-of-may-11-2020-2005-service-release"></a>2020 年 5 月 11 日当周（2005 服务版本）

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>应用管理

#### <a name="customize-self-service-device-actions-in-the-company-portal--4393379---"></a>自定义公司门户中的自助设备操作<!--4393379 -->
可自定义在公司门户应用和网站中向最终用户显示的可用自助服务设备操作。 为了帮助防止发生意外的设备操作，可以通过选择“租户管理” > “自定义”，为公司门户应用配置这些设置 。 提供了以下选项：
- 隐藏公司 Windows 设备上的“删除”按钮。
- 隐藏公司 Windows 设备上的“重置”按钮。
- 隐藏公司 iOS 设备上的“重置”按钮。
- 隐藏公司 iOS 设备上的“删除”按钮。
有关详细信息，请参阅[公司门户中的用户自助设备操作](../apps/company-portal-app.md#user-self-service-device-actions-from-the-company-portal)。

#### <a name="auto-update-vpp-available-apps---3640511----"></a>自动更新 VPP 可用应用<!-- 3640511  -->
如果为 VPP 令牌启用了“自动应用更新”功能，则发布为批量购买计划 (VPP) 可用应用的应用会自动更新。 以前，VPP 可用应用不会自动更新。 如果发布了新版本，最终用户不得不转到公司门户重新安装该应用。 必需的应用将继续支持自动更新。




#### <a name="android-company-portal-user-experience---5736084----"></a>Android 公司门户用户体验<!-- 5736084  -->
在 2005 版本的 Android 公司门户中，收到应用保护策略发出的警告、阻止或擦除命令的 Android 设备的最终用户将看到新的用户体验。 最终用户将看到一条完整的页面消息，其中描述了警告、阻止或擦除的原因，以及解决此问题的步骤，并且不再看到当前的对话框体验。 有关详细信息，请参阅[适用于 Android 设备的应用保护体验](../apps/app-protection-policy.md#app-protection-experience-for-android-devices)和 [Microsoft Intune 中的 Android 应用保护策略设置](../apps/app-protection-policy-settings-android.md)。

#### <a name="support-for-multiple-accounts-in-company-portal-for-macos---5779449----"></a>支持在公司门户中设置适用于 macOS 的多个帐户<!-- 5779449  -->
macOS 设备上的公司门户现在会缓存用户帐户，使登录更容易。 用户不再需要在每次启动应用程序时登录到公司门户。 此外，如果缓存了多个用户帐户，则公司门户将显示帐户选取器，使用户无需输入其用户名。 

#### <a name="newly-available-protected-apps---7060934-----"></a>新提供的受保护应用<!-- 7060934   -->
现在提供了以下受保护的应用：
- Board Papers
- 适用于 Intune 的 Breezy
- Hearsay Relate for Intune
- 适用于 Intune 的 ISEC7 Mobile Exchange Delegate
- 适用于 Intune 的 Lexmark
- Meetio Enterprise
- Microsoft Whiteboard
- Now® Mobile - Intune
- Qlik Sense Mobile 
- ServiceNow® Agent - Intune
- ServiceNow® Onboarding - Intune
- 适用于 Intune 的 Smartcrypt
- 适用于 Intune 的 Tact
- Zero - 律师电子邮件

有关受保护应用的详细信息，请参阅[受 Microsoft Intune 保护的应用](../apps/apps-supported-intune-apps.md)。

#### <a name="search-the-intune-docs-from-the-company-portal---1736480-----"></a>从公司门户搜索 Intune 文档<!-- 1736480   -->
现在可以从 macOS 应用的公司门户直接搜索 Intune 文档。 在菜单栏中，选择“帮助” > “搜索”，然后输入搜索的关键字以快速找到问题的答案 。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>设备配置

#### <a name="improvements-to-oemconfig-support-for-zebra-technologies-devices---4184154---"></a>对 Zebra Technologies 设备的 OEMConfig 支持的改进<!-- 4184154 -->
Intune 完全支持 Zebra OEMConfig 提供的所有功能。 通过 Android Enterprise 和 OEMConfig 管理 Zebra Technologies 设备的客户可以将多个 OEMConfig 配置文件部署到一台设备。 客户还可以查看有关其 Zebra OEMConfig 配置文件状态的丰富报告。

有关详细信息，请参阅[在 Microsoft Intune 中将多个 OEMConfig 配置文件部署到 Zebra 设备](../configuration/oemconfig-zebra-android-devices.md)。

其他 OEM 的 OEMConfig 行为没有变化。

适用于：
- Android Enterprise
- 支持 OEMConfig 的 Zebra Technologies 设备。 有关支持的特定详细信息，请联系 Zebra。

#### <a name="configure-system-extensions-on-macos-devices---6255624---"></a>在 macOS 设备上配置系统扩展<!-- 6255624 -->
在 macOS 设备上，你可以创建一个内核扩展配置文件，在内核级别配置设置（“设备” > “配置文件” >  平台的“macOS”> 配置文件的“内核扩展”）   。 Apple 最终会弃用内核扩展，并在将来的版本中将它们替换为系统扩展。

系统扩展在用户空间中运行，并且无法访问内核。 目的是为了提高安全性并提供更多的最终用户控制，同时在内核级别限制攻击。 内核扩展和系统扩展都允许用户安装可扩展操作系统的本机功能的应用扩展。

在 Intune 中，你可以同时配置内核扩展和系统扩展（“设备” > “配置文件” >  平台的“macOS”> 配置文件的“内核扩展”）   。 内核扩展适用于 10.13.2 和更高版本。 系统扩展适用于 10.15 和更高版本。 从 macOS 10.15 到 macOS 10.15.4，内核扩展和系统扩展可并行运行。 

要了解 macOS 设备上的这些扩展，请参阅[添加 macOS 扩展](../configuration/kernel-extensions-overview-macos.md)。

适用于：
- macOS 10.15 及更高版本

#### <a name="configure-app-and-process-privacy-preferences-on-macos-devices---2934232-----"></a>在 macOS 设备上配置应用和进程隐私首选项<!-- 2934232   --> 
随着 macOS Catalina 10.15 的发布，Apple 添加了新的安全和隐私增强功能。 默认情况下，应用程序和进程只有取得用户许可才能访问特定数据。 如果用户不提供许可，则应用程序和进程可能无法正常工作。 Intune 即将添加对以下设置的支持：对于运行 macOS 10.14 及更高版本的设备，允许 IT 管理员代表最终用户授予或不授予数据访问许可。 这些设置将确保应用程序和进程继续正常工作，并减少提示的数量。 

有关可管理的设置的详细信息，请参阅 [macOS 隐私首选项](../configuration/device-restrictions-macos.md#privacy-preferences)。

适用于：
- macOS 10.14 及更高版本

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>设备注册

#### <a name="enrollment-restrictions-support-scope-tags--4209550----"></a>注册限制支持作用域标记<!--4209550  -->
现在可以向注册限制分配作用域标记。 为此，请转到 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431) > “设备” > “注册限制” > “创建限制”  。 创建任一一种限制，然后将看到“作用域标记”页。 有关详细信息，请参阅[创建注册限制](../enrollment/enrollment-restrictions-set.md)。

#### <a name="autopilot-support-for-hololens-2-devices--6305220----"></a>Hololens 2 设备的 Autopilot 支持<!--6305220  -->
Windows Autopilot 现在支持 Hololens 2 设备。 有关使用适用于 Hololens 的 Autopilot 的详细信息，请参阅[适用于 HoloLens 2 的 Windows Autopilot](https://docs.microsoft.com/hololens/hololens2-autopilot)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>设备管理

#### <a name="use-sync-remote-action-in-bulk-for-ios--6440956--idmiss--"></a>对 iOS 批量使用同步远程操作<!--6440956  idmiss-->
现在可以一次在多达 100 个 iOS 设备上使用同步远程操作。 若要查看此功能，请转到 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431) > “设备” > “所有设备” > “批量设备操作”  。 

#### <a name="automated-device-sync-interval-down-to-12-hours--3077535----"></a>自动设备同步间隔缩短到 12 小时<!--3077535  -->
对于 Apple 的自动设备注册，Intune 和 Apple Business Manager 之间的自动设备同步间隔已从 24 小时缩短到 12 小时。 有关同步的详细信息，请参阅[同步托管设备](../enrollment/device-enrollment-program-enroll-ios.md#sync-managed-devices)。


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>设备安全性

#### <a name="derived-credentials-support-for-disa-purebred-on-android-devices---6939073-------"></a>派生凭据支持在 Android 设备上使用 DISA Purebred<!-- 6939073     -->
现在可以在 Android Enterprise 完全托管设备上使用 DISA Purebred 作为[派生凭据](../protect/derived-credentials.md)提供程序。 支持检索 DISA Purebred 的派生凭据。 可以使用派生凭据进行应用身份验证、Wi-Fi、VPN 或 S/MIME 签名，并/或通过支持该凭据的应用进行加密。 

#### <a name="send-push-notifications-as-an-action-for-noncompliance----1733150-----"></a>针对非符合性操作发送推送通知 <!-- 1733150   -->
现在可以配置[非符合性操作](../protect/actions-for-noncompliance.md#available-actions-for-noncompliance)，当用户设备无法满足符合性策略条件时，该操作会向用户发送推送通知。 新操作向最终用户发送推送通知，支持 Android 和 iOS 设备。

当用户在其设备上选择推送通知时，将打开公司门户或 Intune 应用，显示有关其不符合原因的详细信息。

#### <a name="endpoint-security-content-and-new-features---5720009-5892558-7130145-5653324-7140602----"></a>终结点安全内容和新功能<!-- 5720009 5892558, 7130145, 5653324, 7140602  -->

Intune [终结点安全](../protect/endpoint-security.md)的相关文档现已可供使用。 在 Microsoft Endpoint Manager 管理中心的终结点安全节点中可以：

- 创建重点安全策略并将其部署到托管设备
- 配置与 Microsoft Defender 高级威胁防护的集成，并管理安全任务以帮助消除由 ATP 团队识别到的设备风险
- 配置安全基线
- 管理设备符合性和条件性访问策略
- 在为 Configuration Manager 配置了“客户端附加”时，查看 Intune 和 Configuration Manager 中所有设备的符合性状态。

除了内容的可用性之外，本月终结点安全还新增了以下内容：

- [终结点安全策略](../protect/endpoint-security-policy.md)已结束预览状态，现已可在生产环境中使用（正式推出），但有两个例外情况 ：

  - 在新的“公共预览版”中，可以使用适用于 Windows 10 防火墙策略的 [Microsoft Defender 防火墙规则配置文件](../protect/endpoint-security-firewall-policy.md#firewall-profiles)。 在此配置文件的每个实例中，可以配置多达 150 个防火墙规则来补充你的 Microsoft Defender 防火墙配置文件。 
  - 帐户保护安全策略仍处于预览阶段。 

- 现在可以[创建终结点安全策略的副本](../protect/endpoint-security-policy.md#duplicate-a-policy)。 副本将保留原始策略的设置配置，但会有一个新名称。 然后，在编辑新策略实例以添加组之前，新策略实例不包含对组的任何分配。 可以复制以下策略：
  - 防病毒
  - 磁盘加密
  - 防火墙
  - 终结点检测和响应
  - 攻击面减少
  - 帐户保护

- 现在可以[**创建安全基线的副本**](../protect/security-baselines.md#duplicate-a-security-baseline)。 副本将保留原始基线的设置配置，但会有一个新的名称。 在编辑新基线实例以添加组之前，新基线实例不包含对组的任何分配。

- 现已推出新的终结点安全防病毒策略报告功能：[Windows 10 不正常终结点](../protect/endpoint-security-antivirus-policy.md#windows-10-unhealthy-endpoints)。 此报告功能是在查看终结点安全防病毒策略时可以选择的新页面。 此报告显示 MDM 管理的 Windows 10 设备的防病毒状态。  

#### <a name="support-for-smime-signing-and-encryption-certificates-with-outlook-on-android---7207474----"></a>支持 Android 上的 Outlook 的 S/MIME 签名和加密证书<!-- 7207474  -->
现在可以对 Android 的 Outlook 使用证书进行 S/MIME 签名和加密。 通过此支持，可以使用 SCEP、PKCS 和 PKCS 导入的证书配置文件来预配这些证书。 支持的 Android 平台如下：

- Android Enterprise 工作配置文件
- Android 设备管理员

即将推出对 Android Enterprise 完全托管设备的支持。

有关此支持的详细信息，请参阅 Exchange 文档中的[适用于 iOS 和 Android 的敏感度标签和保护](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/sensitive-labeling-and-protection-outlook-for-ios-android)。


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>监视和故障排除

#### <a name="device-reports-ui-update---6269408---"></a>设备报告 UI 更新<!-- 6269408 -->
报告概述窗格现在提供“摘要”和“报告”选项卡 。在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，选择“报告”，然后选择“报告”选项卡以查看可用的报告类型 。 有关相关信息，请参阅 [Intune 报告](../fundamentals/reports.md)。


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="scripting"></a>脚本编写

#### <a name="macos-script-support---6376978----"></a>macOS 脚本支持<!-- 6376978  -->
macOS 的脚本支持现已正式发布。 此外，我们已添加对用户分配的脚本和已注册 Apple 自动设备注册（原名“设备注册计划”）的 macOS 设备的支持。 有关详细信息，请参阅[在 Intune 中的 macOS 设备上使用 Shell 脚本](../apps/macos-shell-scripts.md)。


<!-- ########################## -->
## <a name="week-of-may-4-2020"></a>2020 年 5 月 4 日当周  

### <a name="company-portal-for-android-guides-users-to-get-apps-after-work-profile-enrollment----6103999---"></a>适用于 Android 的公司门户可指导用户在注册了工作配置文件后获取应用 <!-- 6103999 -->
我们改进了公司门户中的应用内指南，可便于用户更轻松地查找和安装应用。 注册工作配置文件管理后，用户将看到一条说明如何在徽章版 Google Play 中查找建议的应用的消息。 [使用 Android 配置文件注册设备](../user-help/enroll-device-android-work-profile.md)中的最后一步已更新为显示这条新消息。 用户还将在左侧的公司门户抽屉中看到新的“获取应用”链接。 为了给这些新体验和改进体验腾出地方，“应用”选项卡已被删除。 若要查看更新后的屏幕，请转到 [Intune 最终用户应用的 UI 更新](./whats-new-app-ui.md)。 

<!-- ########################## -->
## <a name="week-of-april-20-2020"></a>2020 年 4 月 20 日当周

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>设备管理

#### <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions---6317104-cm3555758----"></a>Microsoft Endpoint Manager 租户附加：设备同步和设备操作<!-- 6317104, CM3555758  -->
Microsoft 终结点管理器将 Configuration Manager 和 Intune 组合为单个控制台。 从 Configuration Manager 版本 2002 开始，可在管理中心将 Configuration Manager 设备上传到云服务并对它们执行操作。 有关详细信息，请参阅 [Microsoft Endpoint Manager 租户附加：设备同步和设备操作](../../configmgr/tenant-attach/device-sync-actions.md)。 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>应用管理

#### <a name="microsoft-office-365-proplus-rename---6368143---"></a>Microsoft Office 365 专业增强版重命名<!-- 6368143 -->
Microsoft Office 365 专业增强版将重命名为 Microsoft 365 企业应用版。 要了解详细信息，请参阅 [Office 365 专业增强版的名称变更](https://docs.microsoft.com/deployoffice/name-change)。 在我们的文档中，我们通常将它称为 Microsoft 365 应用版。 在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，可选择“应用” > “Windows” > “添加”来查找应用套件  。 要了解如何添加应用，请参阅[向 Microsoft Intune 添加应用](../apps/apps-add.md)。

<!-- ########################## -->
## <a name="week-of-april-13-2020-2004-service-release"></a>2020 年 4 月 13 日当周（2004 服务版本）

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>应用管理

#### <a name="manage-smime-settings-for-outlook-on-android-enterprise-devices---6517085-----"></a>在 Android Enterprise 设备上管理 Outlook 的 S/MIME 设置<!-- 6517085   -->
可以使用应用配置策略在运行 Android Enterprise 的设备上管理 Outlook 的 S/MIME 设置。 还可以选择是否允许设备用户在 Outlook 设置中启用或禁用 S/MIME。 若要使用适用于 Android 的应用配置策略，请在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)内，依次转到“应用” > “应用配置策略” > “添加” > “受管理设备”。 若要详细了解如何配置 Outlook 设置，请参阅 [Microsoft Outlook 配置设置](../apps/app-configuration-policies-outlook.md)。

#### <a name="pre-release-testing-for-managed-google-play-apps---2681933----"></a>托管的 Google Play 应用的预发布测试<!-- 2681933  -->
如果组织使用 [Google Play 的应用预发布测试的封闭式测试轨道](https://support.google.com/googleplay/android-developer/answer/3131213)，可以使用 Intune 管理这些轨道。 你可以有选择性地将发布到 Google Play 预生产轨道的应用分配给试点组，从而执行测试。 在 Intune 中，可以查看是否向应用发布了预生产内部版本测试轨道，并能将此轨道分配给 AAD 用户或设备组。 此功能适用于我们当前支持的所有 Android Enterprise 方案（工作配置文件、完全托管和专用）。 在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)内，可以依次选择“应用” > “Android” > “添加”，从而添加托管的 Google Play 应用。 有关详细信息，请参阅[处理托管的 Google Play 封闭式测试轨道](../apps/apps-add-android-for-work.md#working-with-managed-google-play-closed-testing-tracks)。

#### <a name="microsoft-teams-is-now-included-in-the-office-365-suite-for-macos---5903936----"></a>Microsoft Teams 现已包含在适用于 macOS 的 Office 365 套件中<!-- 5903936  -->
除了现有的 Microsoft Office 应用（Word、Excel、PowerPoint、Outlook 和 OneNote）外，在 Microsoft Endpoint Manager 中分配有 Microsoft Office for macOS 的用户现在还会获得 Microsoft Teams。 Intune 将识别已安装其他 Office for macOS 应用的现有 Mac 设备，并在下次设备使用 Intune 签入时尝试安装 Microsoft Teams。 在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，可以通过选择“应用” > “macOS” > “添加”来查找适用于 macOS 的 Office 365 套件   。 有关详细信息，请参阅[使用 Microsoft Intune 将 Office 365 分配给 macOS 设备](../apps/apps-add-office365-macos.md)。

#### <a name="update-to-android-app-configuration-policies---6113334----"></a>更新到 Android 应用配置策略<!-- 6113334  -->
Android 应用配置策略已更新为，允许管理员在创建应用配置文件前选择设备注册类型。 此功能将添加到基于注册类型（工作配置文件或设备所有者）的证书配置文件帐户中。  此更新包括以下内容：

1. 如果新建了配置文件，并为设备注册类型选择了“工作配置文件”和“设备所有者配置文件”，则无法关联证书配置文件与应用配置策略。
2. 如果已创建新的配置文件，并且选择了仅“工作配置文件”，那么可以使用在设备配置下创建的工作配置文件证书策略。
3. 如果已创建新的配置文件，并且选择了仅“设备所有者”，那么可以使用在设备配置下创建的设备所有者证书策略。 

> [!IMPORTANT]
> 在此功能发布前（2004 年 - 2020 年 4 月版本）创建的且没有与任何证书配置文件关联的现有策略，将默认为设备注册类型选择“工作配置文件”和“设备所有者配置文件”。 另外，在此功能发布前创建的且与证书配置文件关联的现有策略，将默认为设备注册类型只选择“工作配置文件”。

此外，我们还将添加 Gmail 和 Nine 电子邮件配置文件，它们将同时适用于“工作配置文件”和“设备所有者配置文件”注册类型，包括对这两种电子邮件配置类型使用证书配置文件。  在“工作配置文件”的“设备配置”下创建的任何 Gmail 或 9 个策略将继续应用于设备，没有必要将它们移动到应用配置策略。

在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)内，可以依次选择“应用” > “应用配置策略”，从而查找应用配置策略。 若要详细了解应用配置策略，请参阅 [Microsoft Intune 的应用配置策略](../apps/app-configuration-policies-overview.md)。

#### <a name="push-notification-when-device-ownership-type-is-changed---5575875---"></a>更改设备所有权类型时的推送通知<!-- 5575875 -->
可以配置推送通知，以在 Android 和 iOS 公司门户用户的设备所有权类型因隐私保护原因从“个人”更改为“企业”时发送给他们。 此推送通知默认设为“关”。 在 Microsoft Endpoint Manager 中，可以通过依次选择“租户管理” > “自定义”来找到此设置。 若要了解有关设备所有权如何影响最终用户的详细信息，请参阅[更改设备所有权](../enrollment/corporate-identifiers-add.md#change-device-ownership)。

#### <a name="group-targeting-support-for-customization-pane---4722837----"></a>“自定义”窗格的组目标支持<!-- 4722837  -->
可以将“自定义”窗格中的设置定目标到用户组。 若要在 Intune 中查找这些设置，请导航到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，选择“租户管理” > “自定义”。 有关自定义的详细信息，请参阅[如何自定义 Intune 公司门户应用、公司门户网站和 Intune 应用](../apps/company-portal-app.md)。


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>设备配置

#### <a name="multiple-evaluate-each-connection-attempt-on-demand-vpn-rules-supported-on-ios-ipados-and-macos---6424615----"></a>iOS、iPadOS 和 macOS 上支持多个“评估每次连接尝试”按需 VPN 规则<!-- 6424615  -->
Intune 用户体验允许将同一个 VPN 配置文件中的多个按需 VPN 规则用于“评估每次连接尝试”操作（“设备” > “配置文件” > “创建配置文件” > “iOS/iPadOS”或“macOS”（作为平台）>“VPN”（作为配置文件）>“自动 VPN” > “按需”）。

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
- 在 SSO 配置文件（“设备” > “配置文件” > “创建配置文件” > “iOS/iPadOS”(针对平台) >“设备功能”(针对配置文件) >“单一登录”），将 Kerberos 主体名称设置为 SSO 配置文件中的安全帐户管理器 (SAM) 帐户名称     。 
- 在 SSO 应用扩展配置文件（“设备” > “配置文件” > “创建配置文件” > “iOS/iPadOS”(针对平台) >“设备功能”(针对配置文件) >“单一登录应用扩展”）中，使用新的 SSO 应用扩展类型，以较少的单击次数配置 iOS/iPadOS Microsoft Azure AD 扩展     ）。 可以为共享设备模式下的设备启用 Azure AD 扩展，并向扩展发送特定于扩展的数据。

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
在“所有设备”页上，“管理者”列的条目已更改：
- 现在显示“Intune”，而不是“MDM”
- 现在显示“共同管理”，而不是“MDM/ConfigMgr 代理”

导出值不变。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>设备管理

#### <a name="trusted-platform-manager-tpm-version-information-now-on-device-hardware-page--6224914-idmiss---"></a>“设备硬件”页上现在提供受信任的平台管理器 (TPM) 版本信息<!--6224914 idmiss -->
现在，可以在“设备硬件”页上查看 TPM 版本号（[Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)  > “设备”> 选择设备 >“硬件”> 在“系统机箱”下查找）。

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
为 Android 或 Android Enterprise 设备创建配置文件时，将更新 Endpoint Management 管理中心中的体验。 此更改会影响以下设备配置文件（“设备” > “配置文件” > “创建配置文件” >   选择“Android 设备管理员”或“Android Enterprise”平台）：

- 设备限制：Android 设备管理员
- 设备限制：Android Enterprise 设备所有者
- 设备限制：Android Enterprise 工作配置文件

有关可配置设备限制的详细信息，请参阅 [Android 设备管理员](../configuration/device-restrictions-android.md)和 [Android Enterprise ](../configuration/device-restrictions-android-for-work.md)。

### <a name="improved-user-interface-experience-when-creating-configuration-profiles-on-iosipados-and-macos-devices---5569002-5568997---"></a>改善了在 iOS/iPadOS 和 macOS 设备上创建配置文件时的用户界面体验<!-- 5569002 5568997 -->
为 iOS 或 macOS 设备创建配置文件时，将更新 Endpoint Management 管理中心中的体验。 此更改会影响以下设备配置文件（“设备” > “配置文件” > “创建配置文件” >  选择“iOS/iPadOS”或“macOS”作为平台    ）：

- 自定义：iOS/iPadOS、macOS
- 设备功能：iOS/iPadOS、macOS
- 设备限制：iOS/iPadOS、macOS
- 终结点保护：macOS
- 扩展：macOS
- 首选项文件：macOS

### <a name="hide-from-user-configuration-setting-in-device-features-on-macos-devices---6524869---"></a>macOS 设备上设备功能中的“不在用户配置中显示”设置<!-- 6524869 -->

在 macOS 设备上创建设备功能配置文件时，有一个新的“不在用户配置中显示”设置（“设备” > “配置文件” > “创建配置文件” > “适用于平台的 macOS”>“适用于配置文件的设备功能”>“登录项”）      。

此功能在 macOS 设备上的“用户和组”登录项应用列表中设置应用的隐藏复选标记。 现有配置文件将列表中的此设置显示为未配置。 若要配置此设置，管理员可以更新现有配置文件。

当设置为“隐藏”时，将选中应用的隐藏复选框，并且用户无法更改它。 用户登录到其设备后，它还会向用户隐藏应用。

> [!div class="mx-imgBorder"]
> ![用户在 Microsoft Intune 和 Endpoint Manager 中登录设备后，在 macOS 设备上隐藏应用](./media/whats-new/macos-hide-checkmark-users-groups-login-items-apps-list.png)

有关可以配置的设置的详细信息，请参阅 [macOS 设备功能设置](../configuration/macos-device-features-settings.md)。

此功能适用于：

- macOS

<!-- ########################## -->
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

- 将该窗格重命名为“自定义”。
- 改进设置的组织和设计。
- 改进设置文本和工具提示。

若要在 Intune 中查找这些设置，请导航到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，选择“租户管理” > “自定义”。 有关现有自定义的信息，请参阅[如何配置 Microsoft Intune 公司门户应用](../apps/company-portal-app.md)。

#### <a name="users-personal-encrypted-recovery-key---6273943----"></a>用户的个人加密恢复密钥<!-- 6273943  -->
这提供了新的 Intune 功能，使用户能够通过 Android 公司门户应用程序或 Android Intune 应用程序检索其个人加密 FileVault 恢复密钥。 公司门户应用程序和 Intune 应用程序中都会提供一个链接，该链接将打开 Chrome 浏览器并转到 Web 公司门户，用户可以在其中查看访问其 Mac 设备所需的 FileVault 恢复密钥。 有关加密的详细信息，请参阅 [使用 Intune 设备加密](../protect/encrypt-devices.md)。

#### <a name="optimized-dedicated-device-enrollment----6114580----"></a>优化专用设备注册 <!-- 6114580  -->
我们正在优化 Android Enterprise 专用设备的注册，并使与 Wi-Fi 关联的 SCEP 证书更轻松地应用于 2019 年 11 月 22 日之前注册的专用设备。 对于新注册，Intune 应用将继续安装，但最终用户将不再需要在注册期间执行“启用 Intune 代理”步骤。 将在后台自动进行安装，并且可以部署和设置与 Wi-Fi 关联的 SCEP 证书，而无需最终用户交互。  

随着 Intune 服务后端部署的展开，这些更改将于三月分阶段推出。 在三月份结束时，所有租户都将具有这一新行为。 相关信息请参阅[支持 Android Enterprise 专用设备中的 SCEP 证书](https://techcommunity.microsoft.com/t5/intune-customer-success/support-for-scep-certificates-in-android-enterprise-dedicated/ba-p/928147)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>设备配置

#### <a name="new-user-experience-when-creating-administrative-templates-on-windows-devices--5096036---"></a>在 Windows 设备上创建管理模板时的新用户体验<!--5096036 -->
根据客户反馈，以及我们迁移到新的 Azure 全屏体验，我们使用文件夹视图重新构建了“管理模板”配置文件体验。 我们尚未对任何设置或现有配置文件进行更改。 因此，现有配置文件将保持不变，并将在新视图中可用。 仍可以通过选择“所有设置”并使用搜索来导航所有设置选项。 树视图根据“计算机”和“用户”配置进行拆分。 你将会在其相关文件夹中找到 Windows、Office 和 Edge 设置。  

适用于：
- Windows 10 及更高版本

#### <a name="vpn-profiles-with-ikev2-vpn-connections-can-use-always-on-with-iosipados-devices---1947932-----"></a>具有 IKEv2 VPN 连接的 VPN 配置文件可将“始终可用”用于 iOS/iPadOS 设备<!-- 1947932   -->
在 iOS/iPadOS 设备上，可创建使用 IKEv2 连接的 VPN 配置文件（“设备” > “配置文件” > 创建配置文件 > “iOS/iPadOS”(针对平台) >选择“VPN”(针对配置文件类型)）。 现在，可为 IKEv2 配置“始终可用”。 配置后，IKEv2 VPN 配置文件会自动连接并保持连接（或快速重新连接）到 VPN。 即使切换网络或重启设备，它仍会保持连接。

在 iOS/iPadOS 上，始终可用 VPN 仅限于 IKEv2 配置文件。

要查看可配置的 IKEv2 设置，请转到[在 iOS 设备上的 Microsoft Intune 中添加 VPN 设置](../configuration/vpn-settings-ios.md#ikev2-settings)。

适用于：
- iOS/iPadOS

#### <a name="delete-bundles-and-bundle-arrays-in-oemconfig-device-configuration-profiles-on-android-enterprise-devices---5550355-----"></a>在 Android Enterprise 设备上删除 OEMConfig 设备配置文件中的捆绑包和捆绑包系列<!-- 5550355   -->
在 Android Enterprise 设备上，创建和更新 OEMConfig 配置文件（“设备” > “配置文件” > “创建配置文件” > “Android Enterprise”(针对平台) >“OEMConfig”(针对配置文件类型)）。 用户现在可以使用 Intune 中的“配置设计器”删除捆绑包和捆绑包系列。

若要详细了解 OEMConfig 配置文件，请参阅[通过 Microsoft Intune 中的 OEMConfig 使用和管理 Android Enterprise 设备](../configuration/android-oem-configuration-overview.md)。

适用于：
- Android Enterprise

#### <a name="configure-the-iosipados-microsoft-azure-ad-sso-app-extension---5672534-----"></a>配置 iOS/iPadOS Microsoft Azure AD SSO 应用扩展<!-- 5672534   -->
Microsoft Azure AD 团队创建了重定向单一登录 (SSO) 应用扩展，让 iOS/iPadOS 13.0 以上的用户能够通过一次登录获取对 Microsoft 应用和网站的访问权限。 此前通过 Microsoft Authenticator 应用进行中转身份验证的所有应用都将继续获取具有新 SSO 扩展的 SSO。 在 Azure AD SSO 应用扩展版本中，可以配置包含重定向 SSO 应用扩展类型的 SSO 扩展（“设备” > “配置文件” > “创建配置文件” > “iOS/iPadOS”(针对平台) >“设备功能”(针对配置文件类型) >“单一登录应用扩展”）。

适用于：
- iOS 13.0 及更高版本
- iPadOS 13.0 及更高版本

有关 iOS SSO 应用扩展的详细信息，请参阅[单一登录应用扩展](../configuration/device-features-configure.md#single-sign-on-app-extension)。

#### <a name="enterprise-app-trust-settings-modification-setting-is-removed-from-iosipados-device-restriction-profiles---6225131-----"></a>已从 iOS/iPadOS 设备限制配置文件中删除了“修改企业应用信任设置”设置<!-- 6225131   -->
在 iOS/iPadOS 设备上，创建设备限制配置文件（“设备” > “配置文件” > “创建配置文件” > “iOS/iPadOS”> 选择“设备限制”作为配置文件类型）。 Apple 删除了“修改企业应用信任设置”设置，因此 Intune 中也删除了它。 如果当前在配置文件中使用此设置，则不会产生任何影响，并将从现有配置文件中将其删除。 还将从 Intune 的任何报表中删除此设置。

适用于：
- iOS/iPadOS

要查看可以限制的设置，请转到[允许或限制功能的 iOS 和 iPadOS 设备设置](../configuration/device-restrictions-ios.md)。

#### <a name="troubleshooting-pending-mam-policy-notification-changed-to-informational-icon--6348954---"></a>故障排除：挂起 MAM 策略通知更改为信息图标<!--6348954 -->
“疑难解答”边栏选项卡上的挂起 MAM 策略的通知图标已更改为信息图标。

####  <a name="ui-update-when-configuring-compliance-policy---3961639------"></a>配置合规性策略时的 UI 更新<!-- 3961639    -->

我们更新了在 Microsoft 终结点管理器中[创建合规性策略](../protect/create-compliance-policy.md#create-the-policy)时的 UI（“设备” > “合规性策略” > “策略” > “创建策略”）。 我们提供了新的用户体验，它包含与以前使用过的相同的设置和详细信息。 新体验遵循类似向导的过程来创建合规性策略，并包含用于为策略添加“分配”的页面，以及用于在创建策略前检查配置的“审查 + 创建”页面。

#### <a name="retire-noncompliant-devices---1827291---------"></a>停用不合规的设备<!-- 1827291       -->
我们为可添加到任何策略中的不合规设备添加了新的操作，以便[停用不合规的设备](../protect/actions-for-noncompliance.md#add-actions-for-noncompliance)。  “停用不符合要求的设备”这一新操作会导致从设备中删除所有公司数据，并且还会将设备从 Intune 管理中删除。  当达到配置的值（以天为单位），此操作将运行，此时设备将变为可停用状态。 最小值为 30 天。  需要明确的 IT 管理员批准，才能使用“停用不合规的设备”部分（管理员可在其中停用所有符合条件的设备）停用设备。

#### <a name="support-for-wpa-and-wpa2-in-ios-enterprise-wi-fi-profiles--6215273-----"></a>iOS 企业 Wi-Fi 配置文件中对 WPA 和 WPA2 的支持<!--6215273   -->
[适用于 iOS 的企业 Wi-Fi 配置文件](../configuration/wi-fi-settings-ios.md#enterprise-profiles)现支持安全类型字段。 对于安全类型，你可以选择“WPA 企业”或“WPA/WPA2 企业”，然后为“EAP 类型”指定选择。  （“设备” > “配置文件” > “创建配置文件”，并选择“iOS/iPadOS”作为“平台”，然后选择“Wi-Fi”作为“配置文件”）。 

新的企业选项类似于为适用于 iOS 的基本 Wi-Fi 配置文件提供的选项。

#### <a name="new-user-experience-for-certificate-email-vpn-and-wi-fi-vpn-profiles---5615208-----"></a>证书、电子邮件、VPN 和 Wi-Fi、VPN 配置文件的新用户体验<!-- 5615208   -->
我们更新了在“终结点管理”管理中心创建和修改以下配置文件类型的[用户体验](../configuration/device-profile-create.md)（“设备” > “配置文件” > “创建配置文件”）。 新体验显示与以前相同的设置，但使用类似向导的体验，减少了需要进行的水平滚动。 新体验推出后，无需修改现有配置。

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
可以配置 Android 和 iOS 设备上的公司门户中的设备注册可以在有提示、无提示的情况下进行，还是不允许用户注册。 若要在 Intune 中查找这些设置，请转到 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，然后依次选择“租户管理” > “自定义” > “编辑” > “设备注册”。  

支持设备注册设置要求最终用户具有以下公司门户版本：
-    iOS 上的公司门户：版本 4.4 或更高版本
-    Android 上的公司门户：版本 5.0.4715.0 或更高版本

有关现有公司门户自定义的详细信息，请参阅[如何配置 Microsoft Intune 公司门户应用](../apps/company-portal-app.md)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>设备管理

#### <a name="new-android-report-on-android-devices-overview-page---5435435-----"></a>“Android 设备概述”页面上新增 Android 报告<!-- 5435435   -->
我们已向“Android 设备概述”页面中的 Microsoft 终结点管理器管理控制台添加报告，显示每个设备管理解决方案中已注册的 Android 设备数。 此图表（像 Azure 控制台中已经存在的相同图表一样）显示工作配置文件、完全托管、专用和设备管理员注册的设备计数。 若要查看报告，请选择“设备” > “Android” > “概述”。

#### <a name="guide-users-from-android-device-administrator-management-to-work-profile-management--5857738-----"></a>指导用户从 Android 设备管理员管理转到工作配置文件管理<!--5857738   -->
我们将发布 Android 设备管理员平台的新合规性性设置。 通过此设置，你可以将通过设备管理员管理的设备设为不合规。

在这些不合规的设备上，用户将在“更新设备设置”页上看到“转到新设备管理设置”消息。  如果用户点击“解决”按钮，则会被引导完成以下操作：

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
可以使用 Intune 数据仓库提供额外的设备清单属性。 现在可以通过[设备](../developer/reports-ref-devices.md#devices) beta 收集公开以下属性：
- `ethernetMacAddress` - 此设备的唯一网络标识符。
- `model` - 设备型号。
- `office365Version` - 设备上安装的 Office 365 版本。
- `windowsOsEdition` - 操作系统版本。

现在可以通过 [devicePropertyHistory](../developer/reports-ref-devices.md#devicepropertyhistories) beta 收集公开以下属性：
- `physicalMemoryInBytes` - 物理内存（以字节为单位）。
- `totalStorageSpaceInBytes` - 总存储容量（以字节为单位）。

有关详细信息，请参阅 [Microsoft Intune 数据仓库 API](../developer/reports-nav-intune-data-warehouse.md)。

#### <a name="help-and-support-workflow-update-to-support-additional-services---5654170-----"></a>帮助和支持工作流更新以支持其他服务<!-- 5654170   -->
我们已在 Microsoft 终结点管理器管理中心更新了“帮助和支持”页，现在可以从中[选择你使用的管理类型](../fundamentals/get-support.md#options-to-access-help-and-support)。 此次更改后，你可以从以下管理类型中进行选择：

- Configuration Manager（包括桌面分析）
- Intune
- 共同管理

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="security"></a>安全

#### <a name="use-a-preview-of-security-administrator-focused-policies-as-part-of-endpoint-security--6131401----"></a>使用以安全管理员为中心的策略预览作为终结点安全性的一部分<!--6131401  -->
作为公共预览版，我们已在 Microsoft“终结点管理”管理中心的“终结点安全性”节点下添加了几个新策略组。 作为安全管理员，你可以使用这些新策略来关注设备安全性的特定方面，以管理不同的相关设置组，而无需承担较大的设备配置策略主体的开销。

除了新的适用于 Microsoft Defender 防病毒的防病毒策略（见下文）外，这些新预览策略和配置文件中每项新设置都是当下你可能通过[设备配置文件](../configuration/device-profile-create.md)配置的相同设置。

以下是所有以预览形式提供的新策略类型及其可用的配置文件类型：

- **防病毒(预览)** ：
  - macOS：
    - **防病毒** - 管理 macOS 的[防病毒策略设置](../protect/antivirus-microsoft-defender-settings-macos.md)以管理[适用于 Mac 的 Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac)。

  - Windows 10 及更高版本：
    - **Microsoft Defender 防病毒** - 管理云保护、防病毒排除项、修正、扫描选项等的[防病毒策略设置](../protect/antivirus-microsoft-defender-settings-windows.md)。

      Microsoft Defender 防病毒的防病毒配置文件是一个例外，它引入了作为设备限制配置文件的一部分提供的新设置实例。 新防病毒设置如下：

        - 与在设备限制中找到的设置相同，但支持在配置为设备限制时不可用的第三个配置选项。
        - 当 Endpoint Protection 的[共同管理工作负载滑块](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads)设置为 Intune 时，适用于通过 Configuration Manager 共同管理的设备。

     计划使用新的“防病毒” > “Microsoft Defender 防病毒”配置文件，而不是通过设备限制配置文件进行配置。

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

你可以配置传递优化代理，使其基于分配在后台或前台模式下下载 Win32 应用内容。 对于现有的 Win32 应用，将继续在后台模式下下载内容。 在 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，选择“应用” > “所有应用” > 选择 Win32 应用 > “属性” 。 选择“分配”旁边的“编辑” 。  若要编辑分配，请在“必需”部分的“模式”下选择“包括”  。  你将在“应用设置”部分中找到新设置。 有关传递优化的详细信息，请参阅 [Win32 应用管理 - 传递优化](../apps/apps-win32-app-management.md#delivery-optimization)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>设备管理

#### <a name="change-primary-user-for-windows-devices---3794742-----"></a>更改 Windows 设备的主要用户<!-- 3794742   -->
你可以更改 Windows 混合设备和 Azure AD 联接设备的主要用户。 为此，请转到“Intune” > “设备” > “所有设备”> 选择设备 >“属性” > “主要用户”。 有关详细信息，请参阅[更改设备的主要用户](../remote-actions/find-primary-user.md#change-a-devices-primary-user)。

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
你现在可以为以下远程操作发出批量命令：重启、重命名、Autopilot 重置、擦除和删除。 若要查看新的批量操作，请转到 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431) > “设备” > “所有设备” > “批量操作”  。

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
- 注册期间获得更好的 Microsoft AutoUpdate 体验，这可确保用户拥有最新版本的公司门户。
- 注册期间增强的符合性检查步骤。
- 支持复制的事件 ID，使用户可更快地将错误从其设备发送到公司支持团队。

有关注册和适用于 Mac 的公司门户应用的详细信息，请参阅[使用公司门户应用注册 macOS 设备](../user-help/enroll-your-device-in-intune-macos-cp.md)。

#### <a name="app-protection-policies-for-better-mobile-now-supports-ios-and-ipados---6224512----"></a>Better Mobile 的应用保护策略现在支持 iOS 和 iPadOS<!-- 6224512  -->

2019 年 10 月，Intune 应用保护策略增加了使用 Microsoft 威胁防护合作伙伴提供的数据的功能。 借助此更新，你现在可以使用应用保护策略阻止或使用 iOS 和 iPadOS 上的 Better Mobile 基于设备的运行状况选择性地擦除用户的公司数据。  有关详细信息，请参阅[使用 Intune 创建移动威胁防御应用保护策略](../protect/mtd-app-protection-policy.md)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>设备管理

#### <a name="exports-from-the-all-devices-list--now-in-zipped-csv-format--6343117--"></a>现在从所有设备列表以 CSV 压缩格式导出<!--6343117-->
现在从“设备” > “所有设备”页面以 CSV 压缩格式导出 。


<!-- ########################## -->
## <a name="week-of-february-17-2020-2002-service-release"></a>2020 年 2 月 17 日当周（2002 服务版本）

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>应用管理

#### <a name="microsoft-defender-advanced-threat-protection-atp-app-for-macos---5424618---"></a>适用于 macOS 的 Microsoft Defender 高级威胁防护 (ATP) 应用<!-- 5424618 -->
Intune 将提供一种简单的方法，将适用于 macOS 的 Microsoft Defender 高级威胁防护 (ATP) 应用部署到托管 Mac 设备。 有关详细信息，请参阅[使用 Microsoft Intune 向 macOS 设备添加 Microsoft Defender ](../apps/apps-advanced-threat-protection-macos.md)和[适用于 Mac 的 Microsoft Defender 高级威胁防护](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac)。  

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>设备配置

#### <a name="enable-network-access-control-nac-with-cisco-anyconnect-vpn-on-ios-devices---4860111----"></a>在 iOS 设备上使用 Cisco AnyConnect VPN 启用网络访问控制 (NAC)<!-- 4860111  -->
在 iOS 设备上，你可以创建一个 VPN 配置文件，并使用不同的连接类型，包括 Cisco AnyConnect（“设备配置” > “配置文件” > “创建配置文件” > 选择“iOS”作为平台，“VPN”作为配置文件类型，再选择“Cisco AnyConnect”作为连接类型）     。

你可以使用 Cisco AnyConnect 启用网络访问控制 (NAC)。 使用此功能需要：

1. 根据[Cisco 标识服务引擎管理员指南](https://www.cisco.com/c/en/us/td/docs/security/ise/2-1/admin_guide/b_ise_admin_guide_21/b_ise_admin_guide_20_chapter_01000.html)，使用“将 Microsoft Intune 配置为 MDM Server”中的步骤在 Azure 中配置 Cisco 标识服务引擎 (ISE)。
2. 在 Intune 设备配置配置文件中，选择“启用网络访问控制(NAC)”设置。

若要查看所有可用 VPN 设置，请转至[在 iOS 设备上配置 VPN](../configuration/vpn-settings-ios.md)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>设备注册

#### <a name="serial-number-on-the-apple-mdm-push-certificate-page--5947765----"></a>Apple MDM Push 证书页上的序列号<!--5947765  -->
Apple MDM Push 证书页当前显示序列号。 如果对创建该证书的 Apple ID 的访问权限丢失，则需要该序列号以重新获得对 Apple MDM Push 证书的访问权限。 若要查看序列号，请转到“设备” > “iOS” > “iOS 注册” > “Apple MDM Push 证书”。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>设备管理

#### <a name="new-update-schedule-options-for-pushing-os-updates-to-enrolled-iosipados-devices--5879689----"></a>用于将 OS 更新推送到已注册 iOS/iPadOS 设备的新更新计划选项<!--5879689  -->
在为 iOS/iPadOS 设备计划操作系统更新时，可从以下选项中进行选择。 这些选项适用于使用 Apple Business Manager 或 Apple School Manager 注册类型的设备。
- 下次签入时更新
- 在计划时间内更新
- 在计划时间外更新

对于后两个选项，可创建多个时间窗口。

若要查看新选项，请转到 MEM >“设备” > “iOS” > “更新 iOS/iPadOS 的策略” > “创建配置文件”。

#### <a name="choose-which-iosipados-updates-to-push-to-enrolled-devices--5879689----"></a>选择要推送到已注册设备的 iOS/iPadOS 更新<!--5879689  -->
可选择特定的 iOS/iPadOS 更新（最新的更新除外），将更新推送到已使用 Apple Business Manager 或 Apple School Manager 注册的设备。 此类设备必须设置设备配置策略，将软件更新可见性延迟数天。 若要查看此功能，请转到 MEM >“设备” > “iOS” > “更新 iOS/iPadOS 的策略” > “创建配置文件”。



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
我们合并了路径，以便在 Microsoft 终结点管理器管理中心查找[安全基线](../protect/security-baselines.md)，方法是从多个 UI 位置删除“安全基线”。 若要查找安全基线，现在请使用以下路径：“终结点安全” > “安全基线” 。

#### <a name="expanded-support-for-imported-pkcs-certificates---6044197----"></a>对导入的 PKCS 证书的扩展支持<!-- 6044197  -->
我们已扩展了对使用[导入的 PKCS 证书](../protect/certificates-imported-pfx-configure.md#supported-platforms)的支持以支持“Android 企业完全托管的设备”。 通常，导入 PFX 证书的操作适用于 S/MIME 加密方案，在这些方案中，用户的加密证书在其所有设备上都是必需的，以便能够进行电子邮件解密。

以下平台支持导入 PFX 证书：

- Android - 设备管理员
- Android Enterprise - 完全托管
- Android Enterprise - 工作配置文件
- iOS
- Mac
- Windows 10

#### <a name="view-the-endpoint-security-configuration-for-devices---6206460----"></a>查看设备的终结点安全配置<!-- 6206460  -->
我们更新了 Microsoft 终结点管理器管理中心的选项名称，以便查看[适用于特定设备的终结点安全配置](../protect/security-baselines-monitor.md#view-endpoint-security-configurations-per-device)。 此选项将重命名为“终结点安全配置”，因为它显示了适用的安全基线以及在安全基线之外创建的其他策略。 此选项以前称为“安全基线”。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>基于角色的访问控制

#### <a name="intune-roles-user-interface-changes-coming--5801612-----"></a>即将更改“Intune 角色”用户界面<!--5801612   -->
[Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)的用户界面  > “租户管理” > “角色”已改进为更易用的直观设计 。 此体验提供的设置和详细信息与你现在使用的相同，但是新体验采用类似于向导的过程。

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
从公司门户中的 Android 工作配置文件注册流中删除了“下一步是什么?”屏幕，简化用户体验。 请转到[使用 Android 工作配置文件注册](../user-help/enroll-device-android-work-profile.md)，查看更新后的 Android 工作配置文件注册流。  

#### <a name="company-portal-app-improved-performance---6178652---"></a>公司门户应用提高了性能<!-- 6178652 -->
公司门户应用已更新，以支持使用 ARM64 处理器的设备（例如 Surface Pro X）的更高性能。以前，公司门户以仿真 ARM32 模式运行。 现在，在版本 10.4.7080.0 及更高版本中，公司门户应用已针对 ARM64 进行了本地编译。 有关公司门户应用的详细信息，请参阅[如何配置 Microsoft Intune 公司门户应用](../apps/company-portal-app.md)。

## <a name="whats-new-archive"></a>新增功能存档
若要了解前几个月的新增功能，请参阅[新增功能存档](whats-new-archive.md)。

## <a name="notices"></a>通知

[!INCLUDE [Intune notices](../includes/intune-notices.md)]


