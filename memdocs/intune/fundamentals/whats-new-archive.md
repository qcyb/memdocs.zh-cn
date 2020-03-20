---
title: Microsoft Intune 中前几个月的新增功能 - Azure | Microsoft Docs
titleSuffix: ''
description: 查看 Intune 新增功能页中早期的公告
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 1/28/2020
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 9ba01d60-4a03-4e3e-9aba-8be905c0054c
ROBOTS: NOINDEX,NOFOLLOW
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 17fa979f9563eb0735a68d2cc0ed82d800f8816f
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79354732"
---
# <a name="whats-new-in-the-microsoft-intune---previous-months"></a>Microsoft Intune 中前几个月的新增功能

[!INCLUDE [azure_portal](../includes/azure_portal.md)]


<!-- ########################## -->
## <a name="october-2019"></a>2019 年 10 月

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>应用管理

#### <a name="improved-checklist-design-in-company-portal-app-for-android---5550857---"></a>在适用于 Android 的公司门户应用中改进了清单设计<!-- 5550857 -->  
使用轻型设计和新图标更新了适用于 Android 的公司门户应用中的安装清单。 所做的更改与对适用于 iOS 的公司门户应用所做的最新更新一致。 有关更改的并行比较，请参阅[应用 UI 中的新增功能](whats-new-app-ui.md)。 若要查看更新的注册步骤，请参阅[使用 Android 工作配置文件注册](../user-help/enroll-device-android-work-profile.md)和[注册 Android 设备](../user-help/enroll-device-android-company-portal.md)。  

#### <a name="win32-apps-on-windows-10-s-mode-devices---3747604---"></a>Windows 10 S 模式设备上的 Win32 应用<!-- 3747604 --> 
可以在 Windows 10 S 模式托管设备上安装和运行 Win32 应用。 为此，可以使用 Windows Defender 应用程序控制 (WDAC) PowerShell 工具为 S 模式创建一个或多个补充策略。 使用设备保护签名服务对补充策略进行签名，然后通过 Intune 上传和分发策略。 在 Intune 中，可以通过选择“客户端应用”   > “Windows 10 S 补充策略”  来查找此功能。 有关详细信息，请参阅[在 S 模式设备上启用 Win32 应用](../apps/apps-win32-s-mode.md)。

#### <a name="set-win32-app-availability-based-on-a-date-and-time---3510685---"></a>基于日期和时间设置 Win32 应用可用性<!-- 3510685 -->
管理员可以为所需的 Win32 应用配置开始时间和截止时间。 在开始时间，Intune 管理扩展将启动应用内容下载并缓存它。 应用将在截止时间安装。 对于可用应用，开始时间将指示应用在公司门户中的可见时间。 有关详细信息，请参阅 [Intune Win32 应用管理](../apps/apps-win32-app-management.md#set-win32-app-availability-and-notifications)。

#### <a name="require-device-restart-based-on-grace-period-after-win32-app-install---3136567---"></a>需要在安装 Win32 应用后基于宽限期重新启动设备<!-- 3136567 -->
可以要求必须在成功安装 Win32 应用后重新启动设备。 有关详细信息，请参阅 [Win32 应用管理](../apps/apps-win32-app-management.md)。

#### <a name="dark-mode-for-ios-company-portal---4911422---"></a>适用于 iOS 公司门户的深色模式<!-- 4911422 -->
深色模式适用于 iOS 公司门户。 用户可以下载公司应用、管理其设备，并根据设备设置在所选的配色方案中获取 IT 支持。 iOS 公司门户将自动与最终用户的设备设置匹配，自动应用深色或浅色模式。 有关详细信息，请参阅[适用于 iOS 的 Microsoft Intune 公司门户上的深色模式简介](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Introducing-dark-mode-on-Microsoft-Intune-Company-Portal-for-iOS/ba-p/918453)。 有关 iOS 公司门户的详细信息，请参阅[如何配置 Microsoft Intune 公司门户应用](../apps/company-portal-app.md)。

#### <a name="android-company-portal-enforced-minimum-app-version---2378776---"></a>Android 公司门户强制执行最低应用版本<!-- 2378776 -->
通过使用应用保护策略的最小公司门户版本设置，可以指定在最终用户设备上强制执行的公司门户的特定最低定义版本  。 使用此条件启动设置，可以在不满足值时将“阻止访问”、“擦除数据”和“警告”作为可能的操作    。 此值的可能格式遵循 [主版本].[次版本]、[主版本].[次版本].[内部版本] 或 [主版本].[次版本].[内部版本].[修订版本]    。

如果已配置最小公司门户版本设置，则将影响获取公司门户版本 5.0.4560.0 的任何最终用户以及公司门户的任何未来版本  。 此设置对使用版本低于与此功能一起发布的公司门户版本的用户没有任何影响。 在设备上使用应用自动更新的最终用户可能看不到此功能的任何对话框，因为他们可能使用最新的公司门户版本。 此设置仅适用于已注册和未注册设备具有应用保护的 Android。 有关详细信息，请参阅 [Android 应用保护策略设置 - 条件启动](../apps/app-protection-policy-settings-android.md#conditional-launch)。

#### <a name="add-mobile-threat-defense-apps-to-unenrolled-devices---3005337---"></a>将移动威胁防御应用添加到未注册的设备<!-- 3005337 -->
可以创建可阻止的 Intune 应用保护策略，或者根据设备的运行状况选择性擦除用户的公司数据。 设备的运行状况使用所选的移动威胁防御 (MTD) 解决方案来确定。 此功能目前作为设备符合性设置存在于在 Intune 中注册的设备。 利用这项新功能，我们扩展了移动威胁防御供应商的威胁检测，使其在未注册的设备上正常工作。 在 Android 上，此功能需要在设备上使用最新的公司门户。 在 iOS 上，当应用集成最新的 Intune SDK (v 12.0.15+) 时，此功能将可供使用。 当第一个应用采用最新的 Intune SDK 时，我们将更新“新增功能”主题。 剩余的应用将陆续可用。 有关详细信息，请参阅[使用 Intune 创建移动威胁防御应用保护策略](../protect/mtd-app-protection-policy.md)。

#### <a name="available-google-play-app-reporting-for-android-work-profiles---3041956-----"></a>用于 Android 工作配置文件的可用 Google Play 应用报告<!-- 3041956   -->
对于 Android Enterprise 工作配置文件、专用和完全托管设备上的可用应用安装，可以查看应用安装状态以及托管 Google Play 应用的安装版本。 有关详细信息，请查看[如何监视应用保护策略](../apps/app-protection-policies-monitor.md)、[使用 Intune 管理 Android 工作配置文件设备](../enrollment/android-enterprise-overview.md)和[托管的 Google Play 应用类型](../apps/apps-add-android-for-work.md#managed-google-play-app-types)。

#### <a name="microsoft-edge-version-77-and-later-for-windows-10-and-macos-public-preview---3872025-4678761----"></a>适用于 Windows 10 和 MacOS 的 Microsoft Edge 77 及更高版本（公共预览版）<!-- 3872025, 4678761  -->
Microsoft Edge 版本 77 及更高版本将可以部署到运行 Windows 10 和 MacOS 的电脑上。

公共预览版为 Windows 10 提供了“开发”和“Beta”通道，为 macOS 提供了“Beta”通道    。 部署仅使用英语 (EN)，但最终用户可以在“设置” > “语言”下更改浏览器中的显示语言   。 Microsoft Edge 是一款安装在系统上下文和类似体系结构中的 Win32 应用（在 x86 OS 上安装为 x86 应用，在 x64 OS 上安装为 x64 应用）。 另外，默认“启用”浏览器自动更新，且无法卸载 Microsoft Edge  。 有关详细信息，请参阅[将 Microsoft Edge for Windows 10 添加到 Microsoft Intune](../apps/apps-windows-edge.md) 和 [Microsoft Edge 文档](https://go.microsoft.com/fwlink/?linkid=2103823)。

#### <a name="update-to-app-protection-ui-and-ios-app-provisioning-ui---4102027-4102029-----"></a>更新至应用保护 UI 和 iOS 应用预配 UI<!-- 4102027, 4102029   -->
Intune 中用于创建和编辑应用保护策略和 iOS 应用预配配置文件的 UI 已更新。 UI 更改包括：
- 简化了体验，现可使用压缩在一个边栏选项卡中的向导式格式。
- 对创建流进行了更新，使其包含分配。
- 在创建新策略前查看属性时，或在编辑属性时，将显示包含已设置的所有内容的摘要页。 此外，编辑属性时，摘要将仅显示正在编辑的属性类别的项目列表。

有关详细信息，请参阅[如何创建和分配应用保护策略](../apps/app-protection-policies.md)和[使用 iOS 应用预配配置文件](../apps/app-provisioning-profile-ios.md)。

#### <a name="intune-guided-scenarios---4850318-4831296-3610611----"></a>Intune 引导式方案<!-- 4850318, 4831296, 3610611  -->
Intune 现在提供引导式方案，可帮助你完成 Intune 中的特定任务或一组任务。 引导式方案是围绕一个端到端用例而定制的一系列步骤（工作流）。 常见方案基于管理员、用户或设备在组织中扮演的角色定义。 这些工作流通常需要精心设计的配置文件、设置、应用程序和安全控件的集合，以提供最佳的用户体验和安全性。 新引导式方案包括：
- [部署 Microsoft Edge for Mobile](guided-scenarios-edge.md)
- [保护 Microsoft Office 移动应用的安全](guided-scenarios-office-mobile.md)
- [云托管的新式桌面](guided-scenarios-cloud-managed-pc.md)

有关详细信息，请参阅 [Intune 引导式方案概述](guided-scenarios-overview.md)。

#### <a name="additional-app-configuration-variable-available---4969237-----"></a>其他应用程序配置变量可用<!-- 4969237   -->
创建应用配置策略时，可以将 `AAD Device ID` 配置变量作为配置设置的一部分。 在 Intune 中，选择“客户端应用”   > “应用配置策略”   > “添加”  。 输入配置策略详细信息并选择“配置设置”以查看“配置设置”边栏选项卡   。 有关详细信息，请参阅[托管 Android Enterprise 设备的应用配置策略 - 使用配置设计器](../apps/app-configuration-policies-use-android.md#use-the-configuration-designer)。

#### <a name="create-groups-of-management-objects-called-policy-sets---3762880----"></a>创建称为策略集的管理对象组<!-- 3762880  -->
策略集允许创建对现有管理实体的一系列引用，这些实体需要作为单个概念单元进行标识、定位和监视。 策略集不会替换现有的概念或对象。 你可以继续在 Intune 中分配各个对象，也可以将各个对象作为策略集的一部分进行引用。 因此，对各对象的任何更改都将反映在策略集中。  在 Intune 中，选择“策略集” > “创建”来创建新的策略集   。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>设备配置
”
#### <a name="new-device-firmware-configuration-interface-profile-for-windows-10-and-later-devices-public-preview---2266073----"></a>适用于 Windows 10 及更高版本设备的新设备固件配置接口配置文件（公开预览版）<!-- 2266073  -->
在 Windows 10 及更高版本中，可以创建设备配置文件来控制设置和功能（适用于平台的“设备配置” > “配置文件” > “创建配置文件” > “Windows 10 及更高版本”）     。 在此更新中，有一个新的设备固件配置接口配置文件类型，该类型允许 Intune 管理 UEFI (BIOS) 设置。

有关此功能的详细信息，请参阅[在 Microsoft Intune 中使用 Windows 设备上的 DFCI 配置文件](../configuration/device-firmware-configuration-interface-windows.md)。

适用于：

- 支持固件上的 Windows 10 RS5 (1809) 及更高版本

#### <a name="ui-update-for-creating-and-editing-windows-10-update-rings---4099089-----------"></a>创建和编辑 Windows 10 更新通道的 UI 更新<!-- 4099089         -->
我们为 Intune 更新了[创建和编辑 Windows 10 更新通道](../protect/windows-update-for-business-configure.md#create-and-assign-update-rings)的 UI 体验。 对 UI 的更改包括：  
- 将向导式格式压缩到单个控制台边栏选项卡中，它与配置更新通道时看到的扩展边栏选项卡无关。   
- 修改后的工作流包括“分配”，分配在完成通道的初始配置之前进行。
- 在保存和部署新更新通道之前，可以使用摘要页面来查看已进行的所有配置。 编辑更新通道时，摘要仅显示在你编辑的属性类别内设置的项目列表。

#### <a name="ui-update-for-creating-and-editing-ios-software-update-policy---4099090---------"></a>创建和编辑 iOS 软件更新策略的 UI 更新<!-- 4099090       --> 
我们为 Intune 更新了[创建](../protect/software-updates-ios.md#configure-the-policy)和[编辑](../protect/software-updates-ios.md#edit-a-policy) iOS 软件更新策略的 UI 体验。  对 UI 的更改包括：  
- 将向导式格式压缩到单个控制台边栏选项卡中，它与配置更新策略时看到的扩展边栏选项卡无关。   
- 修改后的工作流包括“分配”，分配在完成策略的初始配置之前进行。
- 在保存和部署新策略之前，可以使用摘要页面来查看已进行的所有配置。 编辑策略时，摘要仅显示在你编辑的属性类别内设置的项目列表。

#### <a name="engaged-restart-settings-are-removed-from-windows-update-rings----4464404--------"></a>预定重启设置已从 Windows 更新通道中删除<!--  4464404      -->
如前所述，Intune 的 Windows 10 更新通道现在[支持设置截止时间](../protect/windows-update-settings.md)，而不再支持预定重启  。 在 Intune 中配置或管理更新通道时，预定重启的设置将不再可用  。  

此更改与最新的 [Windows 服务更改](https://docs.microsoft.com//windows/whats-new/whats-new-windows-10-version-1903#servicing)一致。在运行 Windows 10 1903 或更高版本的设备上，截止时间将取代“预定重启”的配置   。

#### <a name="prevent-installation-of-apps-from-unknown-sources-on-android-enterprise-work-profile-devices---4760025-----"></a>防止在 Android Enterprise 工作配置文件设备上安装来自未知源的应用<!-- 4760025   -->
在 Android Enterprise 工作配置文件设备上，用户永远无法安装来自未知来源的应用。 此次更新添加了一个新设置 -“防止应用在个人配置文件中安装来自未知来源的应用”  。 默认情况下，此设置可以防止用户将来自未知来源的应用程序旁加载到设备上的个人配置文件中。

要查看可以配置的设置，请转到[允许或限制使用 Intune 的功能的 Android Enterprise 设备设置](../configuration/device-restrictions-android-for-work.md)。

适用于：

- Android Enterprise 工作配置文件

#### <a name="create-a-global-http-proxy-on-android-enterprise-device-owner-devices---4816339-----"></a>在 Android Enterprise 设备所有者设备上创建一个全局 HTTP 代理<!-- 4816339   -->
在 Android Enterprise 设备上，你可以配置全局 HTTP 代理，以满足组织的 Web 浏览标准（“设备配置” > “配置文件” > “创建配置文件” > 针对平台选择“Android Enterprise”> 设备所有者 > 针对配置文件类型选择“设备限制”>“连接”）       。 配置完成后，所有 HTTP 流量都将使用此代理。

要配置此功能并查看所配置的所有设置，请转到[允许或限制使用 Intune 的功能的 Android Enterprise 设备设置](../configuration/device-restrictions-android-for-work.md)。

适用于：

- Android Enterprise 设备所有者

#### <a name="connect-automatically-setting-is-removed-in-wi-fi-profiles-on-android-device-administrator-and-android-enterprise---5021055-----"></a>在 Android 设备管理员和 Android Enterprise 的 Wi-Fi 配置文件中删除了“自动连接”设置<!-- 5021055   -->
在 Android 设备管理员和 Android Enterprise 设备上，你可以创建 Wi-Fi 配置文件以配置其他设置（“设备配置” > “配置文件” > “创建配置文件” > “Android 设备管理员”或针对平台选择“Android Enterprise”> 针对配置文件类型选择“Wi-Fi”）       。 在此更新中，删除了“自动连接”设置，因为它[不受 Android 支持](https://developer.android.com/reference/android/net/wifi/WifiManager.html#enableNetwork%28int%2c%20boolean%29)  。 

如果在 Wi-Fi 配置文件中使用此设置，则可能会注意到“自动连接”不起作用  。 无需执行任何操作，但请注意，此设置已在 Intune 用户界面中删除。

若要查看当前设置，请转到 [Android Wi-Fi 设置](../configuration/wi-fi-settings-android.md)或 [Android Enterprise Wi-Fi 设置](../configuration/wi-fi-settings-android-enterprise.md)。

适用于：

- Android 设备管理员 
- Android Enterprise


#### <a name="new-device-configuration-settings-for-supervised-ios-and-ipados-devices---5199328-----"></a>受监督的 iOS 和 iPadOS 设备的新设备配置设置<!-- 5199328   -->
在 iOS 和 iPadOS 设备上，你可以创建配置文件以限制设备上的功能和设置（依次选择“设备配置” > “配置文件” > “创建配置文件” > 针对平台选择“iOS/iPadOS”> 针对配置文件类型选择“设备限制”）      。 在此更新中，可以控制以下新设置： 
- 在“文件”应用中访问网络驱动器  
- 在“文件”应用中访问 USB 驱动器 
- Wi-Fi 始终打开 

若要查看这些设置，请转到[允许或限制使用 Intune 的功能的 iOS 设备设置](../configuration/device-restrictions-ios.md)。

适用于：

- iOS 13.0 及更高版本
- iPadOS 13.0 及更高版本

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>设备注册

#### <a name="toggle-to-only-show-enrollment-status-page-on-devices-provisioned-by-out-of-box-experience-oobe--3959566--"></a>切换为在由全新体验 (OOBE) 预配的设备上仅显示注册状态页<!--3959566-->
现在，你可以选择在由 Autopilot OOBE 预配的设备上仅显示注册状态页。

若要查看新的切换，请选择“Intune”   > “设备注册”   > “Windows 注册”   > “注册状态页”   > “创建配置文件”   > “设置”   >   “在由全新体验 (OOBE) 预配的设备上仅显示页”。

#### <a name="specify-which-android-device-operating-system-versions-enroll-with-work-profile-or-device-administrator-enrollment---4350697-----"></a>指定使用工作配置文件或设备管理员注册注册哪些 Android 设备操作系统版本<!-- 4350697   -->
使用 Intune 设备类型限制，你可以使用设备的 OS 版本来指定哪些用户设备将使用 Android Enterprise 工作配置文件注册或 Android 设备管理员注册。  有关详细信息，请参阅[创建注册限制](../enrollment/enrollment-restrictions-set.md)。



<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>设备管理

#### <a name="intune-supports-ios-11-and-later---4665324----"></a>Intune 支持 iOS 11 及更高版本<!-- 4665324  -->
Intune 注册和公司门户现在支持 iOS 版本 11 及更高版本。 不支持早期版本。

#### <a name="new-restrictions-for-renaming-windows-devices---3478938----"></a>重命名 Windows 设备的新限制<!-- 3478938  -->
重命名 Windows 设备时，必须遵循新规则：
- 小于或等于 15 个字符（必须小于或等于 63 个字节，不包括尾随 NULL）
- 非 Null 或空字符串
- 允许的 ASCII：字母（a-z、A-Z），数字 (0-9) 和连字符
- 允许的 Unicode：0x80 及以后的字符，必须是有效的 UTF8，必须是可映射到 IDN（即 RtlIdnToNameprepUnicode 成功；请参阅 RFC 3492）
- 名称不得只包含数字
- 名称中不能包含空格
- 不允许的字符：{ | } ~ [ \ ] ^ ' : ; < = > ? & @ ! " # $ % ` ( ) + / , . _ *)

 有关详细信息，请参阅[在 Intune 中重命名设备](../remote-actions/device-rename.md)。

### <a name="new-android-report-on-devices-overview-page---4924364---"></a>“设备概述”页面上新增 Android 报告<!-- 4924364 -->
“设备概述”页面的新报告显示每个设备管理解决方案中注册了多少 Android 设备。 此图表显示工作配置文件、完全托管、专用和设备管理员注册的设备计数。 若要查看报告，请选择“Intune” > “设备” > “概述”    。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>设备安全性

#### <a name="microsoft-edge-baseline-preview----3787164----"></a>Microsoft Edge 基线（预览版）<!--  3787164  -->
已添加用于 [Microsoft Edge 设置](../protect/security-baseline-settings-edge.md)的安全基线（预览版）。 

#### <a name="pkcs-certificates-for-macos---1333650---------"></a>适用于 macOS 的 PKCS 证书<!-- 1333650       -->
现在可以[在 macOS 上使用 PKCS 证书](../protect/certficates-pfx-configure.md#create-a-pkcs-certificate-profile)。 可以选择 PKCS 证书作为 macOS 的配置文件类型，并部署具有[自定义主题和主题可选名称字段](../protect/certficates-pfx-configure.md#subject-name-format)的用户和设备证书。  

MacOS 的 PKCS 证书还支持新设置“允许所有应用访问”  。 使用此设置，可以启用对证书私钥的所有关联应用访问。  有关此设置的更多信息，请参阅 https://developer.apple.com/business/documentation/Configuration-Profile-Reference.pdf 处的 Apple 文档。

####   <a name="derived-credentials-to-provision-ios-mobile-devices-with-certificates----1736036-1736037-1772050-2777333-----------"></a>派生凭据以向 iOS 移动设备提供证书<!--  1736036, 1736037, 1772050, 2777333         -->  
Intune 支持使用[派生凭据](../protect/derived-credentials.md)作为身份验证方法，并支持 iOS 设备的 S/MIME 签名和加密。 派生凭据是美国国家标准与技术研究院 (NIST) 800-157 标准的实现，用于将证书部署到设备  。  

派生凭据依赖于使用个人身份验证 (PIV) 或通用访问卡 (CAC) 卡（如智能卡）。 若要获取移动设备的派生凭据，用户需从公司门户应用中开始，并遵循你所使用的提供商特有的注册工作流。  所有提供商都要求使用计算机上的智能卡向派生凭据提供商进行身份验证。 然后，该提供商向从用户智能卡派生的设备颁发证书。  

Intune 支持以下派生凭据提供商：
- DISA Purebred
- Entrust Datacard
- Intercede

使用派生凭据作为 VPN、Wi-Fi 和电子邮件的设备配置文件的身份验证方法。 还可以将它们用于应用身份验证、S/MIME 签名和加密。  

有关该标准的详细信息，请参阅 www.nccoe.nist.gov 上的[派生 PIV 凭据](https://www.nccoe.nist.gov/projects/building-blocks/piv-credentials)。

#### <a name="use-graph-api-to-specify-a-on-premises-user-principal-name-as-a-variable-for-scep-certificates----5437939----------"></a>使用图形 API 将本地用户主体名称指定为 SCEP 证书的变量<!--  5437939        -->  
使用 [Intune 图形 API](https://docs.microsoft.com/graph/api/resources/intune-graph-overview?view=graph-rest-1.0) 时，可以将 onPremisesUserPrincipalName 指定为 SCEP 证书的使用者可选名称 (SAN) 的变量。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->”
### <a name="microsoft-365-device-management"></a>Microsoft 365 设备管理

#### <a name="improved-administration-experience-in-microsoft-365-device-management---5551239---"></a>改进了 Microsoft 365 设备管理中的管理体验<!-- 5551239 -->
已刷新并简化的管理体验现已在 [https://devicemanagement.microsoft.com](https://devicemanagement.microsoft.com) 上的 Microsoft 365 设备管理专家工作区中公开发布，其中包括：

- **更新的导航**：你会发现简化的第一级导航（可对功能进行逻辑分组）。
- **新平台筛选器**：可以在“设备和应用”页上选择单一平台，该平台仅显示所选平台的策略和应用。
- **新主页**：在新主页上快速查看服务运行状况、租户状态、新闻等。
有关这些改进的详细信息，请参阅 Microsoft 技术社区网站上的[企业移动性 + 安全性博客文章](https://go.microsoft.com/fwlink/?linkid=2109094)。

#### <a name="introducing-endpoint-security-node-in-microsoft-365-device-management---5630102---"></a>Microsoft 365 设备管理中的终结点安全节点简介<!-- 5630102 -->

终结点安全节点现已在 https://devicemanagement.microsoft.com 上的 Microsoft 365 设备管理专家工作区中公开发布，可将这些功能组合在一起以保护终结点，例如  ：

- 安全基线：预配置的设置组，这些设置可帮助你应用 Microsoft 推荐的已知设置组和默认值。
- 安全任务：利用 Microsoft Defender ATP 威胁和漏洞管理 (TVM)，并使用 Intune 修正终结点漏洞。
- Microsoft Defender ATP：集成了 Microsoft Defender 高级威胁防护 (ATP) 来帮助阻止安全漏洞。""

这些设置仍能够从其他适用的节点（如设备）访问，并且，无论在何处访问和启用这些功能，当前配置的状态都是相同的。

有关这些改进的详细信息，请参阅 Microsoft 技术社区网站上的 [Intune 客户成功博客文章](https://aka.ms/Endpoint_security_node)。

<!-- ########################## -->
## <a name="september-2019"></a>2019 年 9 月

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>应用管理

#### <a name="managed-google-play-private-lob-apps---1464182----"></a>托管 Google Play 专用 LOB 应用<!-- 1464182  -->”
现在，借助 Intune，IT 管理员可以通过在 Intune 控制台中嵌入的 iframe 将专用 Android LOB 应用发布到托管 Google Play。  以前，IT 管理员需要将 LOB 应用直接发布到 Google Play 发布控制台，这需要执行几个步骤，并且很耗时。 这项新功能可让你轻松地使用一组最少的步骤发布 LOB 应用，而无需离开 Intune 控制台。  管理员不再需要使用 Google 手动注册为开发人员，并且不再需要向 Google 支付 25 美元注册费。  使用托管 Google Play 的任何 Android 企业管理方案都可以利用此功能（工作配置文件、专用、完全托管和非注册设备）。 在 Intune 中，选择“客户端应用”   > “应用”   > “添加”  。 从“应用类型”  列表中，选择“托管的 Google Play”  。 有关托管的 Google Play 应用的详细信息，请参阅[使用 Intune 将托管的 Google Play 应用添加到 Android Enterprise 设备](../apps/apps-add-android-for-work.md)。

#### <a name="windows-company-portal-experience---1473353-3598357---"></a>Windows 公司门户体验<!-- 1473353, 3598357 -->
Windows 公司门户正在更新。 你将能够在 Windows 公司门户中的“应用”页上使用多个筛选器。 “设备详细信息”页也正在使用改进的用户体验进行更新。 我们正在将这些更新推出给所有客户，希望在下周结束前完成。

#### <a name="macos-support-for-web-apps---3174427---"></a>Web 应用的 macOS 支持<!-- 3174427 -->
可以使用 macOS 公司门户将 Web 应用（此类应用可将快捷方式添加到网页 URL）安装到 Dock。 最终用户可以从 macOS 公司门户中的 Web 应用的应用详细信息页访问安装  操作。 有关 Web 链接  应用类型的详细信息，请参阅[将应用添加 Microsoft Intune](../apps/apps-add.md)和[将 Web 应用添加到 Microsoft Intune](../apps/web-app.md)。

#### <a name="macos-support-for-vpp-apps---3173501----"></a>VPP 应用的 macOS 支持<!-- 3173501  -->
当 Apple VPP 令牌在 Intune 中同步时，使用 Apple Business Manager 购买的 macOS 应用将显示在控制台中。 可以使用 Intune 控制台为组分配、撤消和重新分配设备和基于用户的许可证。 Microsoft Intune 可通过以下方式帮助用户管理为贵公司购买的 VPP 应用：

- 从应用商店中报告许可证信息。
- 跟踪已使用的许可证数量。
- 帮助防止安装的应用副本数超过所拥有的数目。

有关 Intune 和 VPP 的系详细信息，请参阅[使用 Microsoft Intune 管理批量购买的应用和书籍](../apps/vpp-apps.md)。

#### <a name="managed-google-play-iframe-support---2871756----"></a>托管 Google Play iframe 支持<!-- 2871756  -->
Intune 现在支持通过托管的 Google Play iframe 直接在 Intune 控制台中添加和管理 Web 链接。  这使 IT 管理员可以提交 URL 和图标图形，然后将这些链接部署到设备，就像常规 Android 应用一样。 使用托管 Google Play 的任何 Android 企业管理方案都可以利用此功能（工作配置文件、专用、完全托管和非注册设备）。 在 Intune 中，选择“客户端应用”   > “应用”   > “添加”  。 从“应用类型”  列表中，选择“托管的 Google Play”  。 有关托管的 Google Play 应用的详细信息，请参阅[使用 Intune 将托管的 Google Play 应用添加到 Android Enterprise 设备](../apps/apps-add-android-for-work.md)。

#### <a name="silently-install-android-lob-apps-on-zebra-devices---4252734----"></a>在 Zebra 设备上以无提示方式安装 Android LOB 应用<!-- 4252734  -->
当在 [Zebra 设备](../configuration/android-zebra-mx-overview.md)上安装 Android 业务线 (LOB) 应用时，不会提示你下载并安装 LOB 应用，而是能够以无提示方式安装应用。 在 Intune 中，选择“客户端应用” > “应用” > “添加”    。 在“选择应用类型”窗格中，选择“业务线应用”   。 有关详细信息，请参阅[将 Android 业务线应用添加到 Microsoft Intune](../apps/lob-apps-android.md)。

目前，下载 LOB 应用后，会在用户的设备上显示下载成功  通知。 只能通过在通知底纹中点击“全部清除”  来消除通知。 此通知问题将在即将发布的版本中得到解决，安装将完全无提示且无可视指示器。

#### <a name="read-and-write-graph-api-operations-for-intune-apps---5031704----"></a>针对 Intune 应用的读取和写入 Graph API 操作<!-- 5031704  -->
应用程序可以使用应用标识（而无需使用用户凭据）来调用 Intune Graph API 读写操作。 若要详细了解如何访问用于 Intune 的 Microsoft Graph API，请参阅[在 Microsoft Graph 中使用 Intune](https://docs.microsoft.com/graph/api/resources/intune-graph-overview?view=graph-rest-1.0)。

#### <a name="protected-data-sharing-and-encryption-for-intune-app-sdk-for-ios---3586942----"></a>适用于 iOS 的 Intune App SDK 受保护的数据共享和加密<!-- 3586942  -->
应用保护策略启用加密时，适用于 iOS 的 Intune App SDK 将使用 256 位加密密钥。 所有应用都需要 SDK 8.1.1 版本才能进行受保护的数据共享。

#### <a name="updates-to-microsoft-intune-app---4997846---"></a>对 Microsoft Intune 应用的更新<!-- 4997846 -->
适用于 Android 的 Microsoft Intune 应用已更新，具有以下改进：
- 更新并改进了布局，包含最重要操作的底部导航。
- 添加了一个显示用户个人资料的附加页面。
- 在应用中为用户添加了对可操作通知（例如需要更新其设备设置）的显示。
- 添加了对自定义推送通知的显示，将应用与适用于 iOS 和 Android 的公司门户应用中最近新增的支持保持一致。 有关详细信息，请参阅[使用 Intune 发送自定义通知](../remote-actions/custom-notifications.md)。
""
#### <a name="for-ios-devices-customize-the-enrollment-process-privacy-screen-of-the-company-portal---4394993---"></a>对于 iOS 设备，自定义公司门户的“注册过程隐私”屏幕<!-- 4394993 -->
使用 Markdown，可以自定义最终用户在 iOS 注册期间看到的公司门户的隐私屏幕。 具体来说，将能够自定义组织无法在设备上查看或执行的操作列表。 有关详细信息，请参阅[如何配置 Intune 公司门户应用](../apps/company-portal-app.md#privacy-statement-customization)。



<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>设备配置

#### <a name="support-for-ikev2-vpn-profiles-for-ios---1943438-----"></a>支持适用于 iOS 的 IKEv2 VPN 配置文件<!-- 1943438   -->
在此更新中，可以使用 IKEv2 协议为 iOS 本机 VPN 客户端创建 VPN 配置文件。 IKEv2 是以下位置中的新连接类型：“设备配置”   > “配置文件”   > “创建配置文件”   > 针对平台选择“iOS”  > 针对配置文件类型选择“VPN”  >“连接类型”  。

这些 VPN 配置文件配置本机 VPN 客户端，因此不会安装 VPN 客户端应用，也不会将其推送到托管设备。 此功能要求设备在 Intune （MDM 注册）中注册。

要查看当前可配置的 VPN 设置，请转到[在 iOS 设备上配置 VPN 设置](../configuration/vpn-settings-ios.md)。

适用于：

- iOS

#### <a name="device-features-device-restrictions-and-extension-profiles-for-ios-and-macos-settings-are-shown-by-enrollment-type---4886161-----"></a>适用于 iOS 和 macOS 设置的设备功能、设备限制和扩展配置文件按注册类型显示<!-- 4886161   -->

在 Intune 中，为 iOS 和 macOS 设备创建配置文件（依次选择“设备配置”   > “配置文件”   > “创建配置文件”   >  针对平台选择“iOS”或“macOS”   > 针对配置文件类型选择“设备功能”、“设备限制”或“扩展”    ）。 

在此更新中，Intune 门户中的可用设置按它们适用的注册类型分类：

- iOS
  - 用户注册""
  - 设备注册
  - 自动设备注册（监督）
  - 所有注册类型

- macOS
  - 用户已批准
  - 设备注册
  - 自动设备注册
  - 所有注册类型

适用于：

- iOS

#### <a name="new-voice-control-settings-for-supervised-ios-devices-running-in-kiosk-mode---4892835-----"></a>在展台模式下运行的受监督 iOS 设备的新语音控制设置<!-- 4892835   -->
在 Intune 中，你可以创建策略以将受监督的 iOS 设备作为展台或专用设备运行（“设备配置”   >  **“配置文件”**  > “创建配置文件”   > 针对平台选择“iOS”>  针对配置文件类型选择“设备限制”>“展台”   ）。

在此更新中，可以控制以下新设置：
- **语音控件**：在展台模式下启用设备上的语音控件。
- **修改语音控件**：允许用户在展台模式下更改设备上的语音控件设置。

若要查看当前设置，请转到 [iOS 展台设置](../configuration/device-restrictions-ios.md#kiosk)。

适用于：

- iOS 13.0 及更高版本

#### <a name="use-single-sign-on-for-apps-and-websites-on-your-ios-and-macos-devices---4893175-----"></a>在 iOS 和 macOS 设备上对应用和网站使用单一登录<!-- 4893175   -->
在此更新中，有一些用于 iOS 和 macOS 设备的新单一登录设置（依次选择“设备配置”   > “配置文件”   > “创建配置文件”   >  针对平台选择“iOS”或“macOS”   > 针对配置文件类型选择“设备功能”  ）。

使用这些设置来配置单一登录体验，特别是对于使用 Kerberos 身份验证的应用和网站。 你可以在通用凭据单一登录应用扩展和 Apple 的内置 Kerberos 扩展之间进行选择。

若要查看可配置的当前设备功能，请转到 [iOS 设备功能](../configuration/ios-device-features-settings.md)和 [macOS 设备功能](../configuration/macos-device-features-settings.md)。

适用于：

- iOS 13. 及更高版本
- macOS 10.15 及更高版本

#### <a name="associate-domains-to-apps-on-macos-1015-devices---4898079-----"></a>将域关联到 macOS 10.15 + 设备上的应用<!-- 4898079   -->
在 macOS 设备上，可以配置不同的功能，并使用策略将这些功能推送到设备（依次选择“设备配置”   > “配置文件”   > 创建配置文件   > 针对平台选择“macOS”  > 针对配置文件选择“设备功能”  ）。 在此更新中，你可以将域关联到应用。 此功能可帮助与应用相关的网站共享凭据，并可与 Apple 的单一登录扩展、通用链接和密码自动填充配合使用。 

若要查看可配置的当前功能，请转到 [Intune 中的 macOS 设备功能设置](../configuration/macos-device-features-settings.md)。

适用于：

- macOS 10.15 及更高版本

#### <a name="use-itunes-and-aps-in-the-itunes-app-store-url-when-showing-or-hiding-apps-on-ios-supervised-devices---4928474-----"></a>显示或隐藏 iOS 受监督设备上的应用时，请使用 iTunes 应用商店 URL 中的“iTunes”和“应用”<!-- 4928474   --> 
在 Intune 中，你可以创建策略以显示或隐藏受监督 iOS 设备上的应用（依次选择“设备配置”   > “配置文件”   > “创建配置文件”   > 针对平台选择“iOS”>  针对配置文件类型选择“设备限制”>  “显示或隐藏应用”  ）。 

可以输入 iTunes 应用商店 URL，例如 `https://itunes.apple.com/us/app/work-folders/id950878067?mt=8`。 在此更新中，`apps` 和`itunes` 均可用于 URL，例如：
- `https://itunes.apple.com/us/app/work-folders/id950878067?mt=8`
- `https://apps.apple.com/us/app/work-folders/id950878067?mt=8`

有关这些设置的详细信息，请参阅[显示或隐藏应用](../configuration/device-restrictions-ios.md#show-or-hide-apps)。

适用于：
- iOS

#### <a name="windows-10-compliance-policy-password-type-values-are-clearer-and-match-csp---5138985---"></a>Windows 10 合规性策略密码类型值更加清晰且匹配 CSP<!-- 5138985 -->
在 Windows 10 设备上，你可以创建需要特定密码功能的合规性策略（依次选择“设备合规性”   > “策略”   > “创建策略”   > 针对平台选择“Windows 10 及更高版本”>  “系统安全”  ）。 在此更新中：
- “密码类型”  值更加清晰，并更新以匹配 [DeviceLock/AlphanumericDevicePasswordRequired CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-alphanumericdevicepasswordrequired)。
- “密码过期(天)”  设置将更新为允许 1-730 天内的值。 

有关 Windows 10 合规性设置的详细信息，请参阅 [Windows 10 及更高版本设置以将设备标记为合规或不合规](../protect/compliance-policy-create-windows.md)。 

适用于：
- Windows 10 及更高版本

 #### <a name="updated-ui-for-configuring-microsoft-exchange-on-premises-access---4092920---"></a>更新了用于配置 Microsoft Exchange 本地访问的 UI<!-- 4092920 -->  
我们更新了控制台，你可在其中[配置 Microsoft Exchange 本地访问权限](../protect/conditional-access-exchange-create.md)。 现在，可以在控制台上用于*启用 Exchange 本地访问控制*的同一个窗格中提供 Exchange 本地访问权限的所有配置。  

#### <a name="allow-or-restrict-adding-app-widgets-to-the-home-screen-on-android-enterprise-work-profile-devices---1109650----"></a>允许或限制将应用小组件添加到 Android Enterprise 工作配置文件设备上的主屏幕<!-- 1109650  --> 
在 Android Enterprise 设备上，你可以配置工作配置文件中的功能（依次选择“设备配置”   > “配置文件”   > 创建配置文件”   > 针对平台选择“Android Enterprise”>  “仅限工作配置文件”>  针对配置文件类型选择“设备限制”）。 在此更新中，可以允许用户将工作配置文件应用公开的小组件添加到设备主屏幕。

要查看可以配置的设置，请转到[便于使用 Intune 允许或限制功能的 Android Enterprise 设备设置](../configuration/device-restrictions-android-for-work.md)。

适用于：
- Android Enterprise 工作配置文件

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>设备注册

#### <a name="new-tenants-will-default-away-from-android-device-administrator-management---4869790-----"></a>新租户将默认离开 Android 设备管理员管理<!-- 4869790   -->
Android Enterprise 已取代 Android 的设备管理员功能。 因此，建议改为使用 Android Enterprise 进行新注册。 在将来的更新中，新租户需要在 Android 注册中完成以下先决条件步骤，才能使用设备管理员管理：转到“Intune”   > “设备注册”   > “Android 注册”   > “个人和企业所有的具有设备管理权限的设备”   > “使用设备管理员管理设备”  。

现有租户的环境不会有任何变化。

有关 Intune 中 Android 设备管理员的详细信息，请参阅 [Android 设备管理员注册](https://docs.microsoft.com/intune/android-enroll-device-administrator)。

#### <a name="list-of-dep-devices-associated-with-a-profile---5012045----"></a>与配置文件关联的 DEP 设备的列表<!-- 5012045  -->
你现在可以查看与配置文件关联的 Apple 自动设备注册计划 (DEP) 设备的页面列表。 你可以从列表中的任何页面搜索列表。 要查看列表，请转到“Intune”   > “设备注册”   > “Apple 注册”   > “注册计划令牌”  > 选择令牌 >“配置文件”  > 选择配置文件 >“分配的设备”  （在“监视器”下  ）。

#### <a name="ios-user-enrollment-in-preview---4817900---"></a>预览版中的 iOS 用户注册<!-- 4817900 -->
Apple 的 iOS 13.1 版本包括用户注册，它是一种新的 iOS 设备轻型管理形式。 它可用于代替个人所有的设备的设备注册或自动设备注册（以前称为设备注册计划）。 Intune 预览版支持此功能集，方法是让你：

- 将用户注册面向用户组。
- 让最终用户在注册其设备时，可以在较轻的用户注册或更强的设备注册之间进行选择。

从 2019 年 9 月 24 日开始，随着 iOS 13.1 的发布，我们正在将这些更新推出给所有客户，希望在下周结束前完成。

适用于：

- iOS 13.1 及更高版本

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>设备管理

#### <a name="more-android-fully-managed-support---3464667-4631425-4631440-5227935-4062195-----"></a>更多 Android 完全托管支持<!-- 3464667, 4631425, 4631440, 5227935, 4062195   -->
我们为 Android 完全托管设备添加了以下支持：

- 完全托管 Android 的 SCEP 证书可用于作为设备所有者管理的设备上的证书身份验证。 工作配置文件设备上已支持 SCEP 证书。  有了针对设备所有者的 SCEP 证书，你将能够： <!-- 5227935 -->
    - 在 Android Enterprise 的 DO 部分下创建 SCEP 配置文件
    - 将 SCEP 证书链接到 DO Wi-Fi 配置文件以进行身份验证
    - 将 SCEP 证书链接到 DO VPN 配置文件以进行身份验证
    - 将 SCEP 证书链接到 DO 电子邮件配置文件以进行身份验证（通过 AppConfig）
- Android Enterprise 设备支持系统应用。 在 Intune 中，通过选择“客户端应用”   > “应用”   > “添加”  来添加 Android Enterprise 系统应用。 在“应用类型”  列表中，选择“Android Enterprise 系统应用”  。 有关详细信息，请参阅[将 Android Enterprise 系统应用添加到 Microsoft Intune](../apps/apps-ae-system.md)。 <!-- 4062195 -->
- 在“设备合规性”   > “Android Enterprise”   > “设备所有者”  中，你可以创建用于设置 Google SafetyNet 证明级别的合规性策略。   <!-- 4631425 -->
- 在 Android Enterprise 完全托管设备上，支持移动威胁防御提供程序。 在“设备合规性”   > “Android Enterprise”   > “设备所有者”  中，可以选择可接受的威胁级别。 <!-- 4631440 --> [使用 Intune 将设备标记为符合或不符合的 Android Enterprise 设置](../protect/compliance-policy-create-android-for-work.md#device-owner)会列出当前设置。
- 在 Android Enterprise 完全托管的设备上，现在可以通过应用配置策略配置 Microsoft Launcher 应用，以便在完全托管的设备上实现标准化的最终用户体验。 Microsoft Launcher 应用可用于个性化 Android 设备。 将该应用与 Microsoft 帐户或工作/学校帐户结合使用，可以访问个性化源中的日历、文档和最近活动。 <!-- 5334044 -->

有了此更新，我们很高兴地宣布 Intune 对 Android Enterprise 完全托管的支持现已正式发布。

适用于：

- Android Enterprise 完全托管设备

#### <a name="send-custom-notifications-to-a-single-device---4928910---"></a>向单个设备发送自定义通知<!-- 4928910 -->
现在，你可以选择单个设备，然后使用远程设备操作[仅向该设备发送自定义通知](../remote-actions/custom-notifications.md#send-a-custom-notification-to-a-single-device)。

#### <a name="wipe-and-passcode-reset-actions-arent-available-for-ios-devices-that-are-enrolled-by-using-user-enrollment---4950491---"></a>擦除和密码重置操作不适用于通过使用“用户注册”注册的 iOS 设备<!-- 4950491 -->
用户注册是一种新的 Apple 设备注册类型。 使用“用户注册”注册设备时，“擦除”和“密码重置”远程操作对此类设备不可用。

#### <a name="intune-support-for-ios-13-and-macos-catalina-devices---4665317---"></a>Intune 对 iOS 13 和 macOS Catalina 设备的支持<!-- 4665317 -->
Intune 现在支持管理 iOS 13 和 macOS Catalina 设备。
有关详细信息，请参阅 [Microsoft Intune 对 iOS 13 和 iPadOS 的支持博客文章](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Support-for-iOS-13-and-iPadOS/ba-p/861998)。

#### <a name="intune-support-for-ipados-and-ios-131-devices--5439574--"></a>Intune 支持 iPadOS 和 iOS 13.1 设备<!--5439574-->
Intune 现在支持管理 iPadOS 和 iOS 13.1 设备。 有关详细信息，请参阅[此博客文章](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Support-for-iOS-13-1-and-iPadOS/ba-p/873094)。


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>设备安全性

#### <a name="bitlocker-support-for-client-driven-recovery-password-rotation----3444125---"></a>对客户端驱动的恢复密码轮转的 BitLocker 支持<!--  3444125 -->
使用 Intune 终结点保护设置，可为运行 Windows 版本 1909 或更高版本的设备上的 BitLocker 配置[客户端驱动的恢复密码轮转](../protect/endpoint-protection-windows-10.md#windows-encryption)。

在 OS 驱动器恢复（通过使用 bootmgr 或 WinRE）和固定数据驱动器上的恢复密码解锁后，此设置启动客户端驱动的恢复密码刷新。 此设置将刷新使用的特定恢复密码，而卷上的其他未使用的密码仍保持不变。 有关详细信息，请参阅 BitLocker CSP 文档 [ConfigureRecoveryPasswordRotation](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp)。

#### <a name="tamper-protection-for-windows-defender-antivirus---4705448----------"></a>Windows Defender 防病毒的篡改防护<!-- 4705448        -->
使用 Intune 管理 Windows Defender 防病毒的篡改防护  。 当将设备配置文件用于 Windows 10 终结点保护时，你将在 Microsoft Defender 安全中心组中找到[篡改防护设置](../protect/endpoint-protection-windows-10.md#microsoft-defender-security-center)。 你可以将“篡改防护”设置为“启用”  以开启篡改防护限制，设置为“禁用”  以关闭限制，或者设置为“未配置”  以保持设备的当前配置。  

有关篡改防护的详细信息，请参阅 Windows 文档中的[篡改防护防止安全设置更改](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-antivirus/prevent-changes-to-security-settings-with-tamper-protection)。

#### <a name="advanced-settings-for-windows-defender-firewall-are-now-generally-available----5317392---------"></a>Windows Defender 防火墙高级设置现在已正式发布<!--  5317392       -->  
[用于终结点保护的 Windows Defender 自定义防火墙规则](../protect/endpoint-protection-configure.md#add-custom-firewall-rules-for-windows-10-devices)（配置为设备配置文件的一部分）已脱离公共预览版，并已正式发布 (GA)。  可以使用这些规则指定应用程序、网络地址和端口的入站和出站行为。 这些规则已在 7 月作为公共预览版发布。 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>监视和故障排除

#### <a name="intune-user-interface-update--tenant-status-dashboard---5273210----"></a>Intune 用户界面更新 - 租户状态仪表板<!-- 5273210  -->
租户状态仪表板的用户界面已更新为与 Azure 用户界面样式保持一致。 有关详细信息，请参阅[租户状态](tenant-status.md)。

### <a name="role-based-access-control"></a>基于角色的访问控制

#### <a name="scope-tags-now-support-terms-of-use-policies---2358863----"></a>作用域标记现在支持“使用条款”策略<!-- 2358863  -->
现在，你可以将[作用域标记](scope-tags.md)分配给“使用条款”策略。 为此，请转到“Intune”   > “设备注册”   > “条款和条件”  > 在列表中选择一项 >“属性”   > “作用域标记”  > 选择作用域标记。

<!-- ########################## -->
## <a name="august-2019"></a>2019 年 8 月

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>应用管理

#### <a name="control-ios-app-uninstall-behavior-at-device-unenrollment---3504144-----"></a>控制设备取消注册时的 iOS 应用卸载行为<!-- 3504144   -->
管理员可以管理当设备在用户或设备组级别取消注册时，应用是被删除还是保留在设备上。 

#### <a name="categorize-microsoft-store-for-business-apps---3926922---"></a>为适用于企业的 Microsoft Store 应用分类<!-- 3926922 -->
可以对适用于企业的 Microsoft Store 应用进行分类。 为此，请依次选择“Intune”   > “客户端应用”   > “应用”  ，选择适用于企业的 Microsoft Store 应用，再依次选择“应用信息”   > “类别”  。 在下拉菜单上，分配类别。

#### <a name="customized-notifications-for-microsoft-intune-app-users---4843354----"></a>面向 Microsoft Intune 应用用户的自定义通知<!-- 4843354  -->
适用于 Android 的 Microsoft Intune 应用现在支持显示自定义推送通知，这与适用于 iOS 和 Android 的公司门户应用中最近新增的支持保持一致。 有关详细信息，请参阅[使用 Intune 发送自定义通知](../remote-actions/custom-notifications.md)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>设备配置

### <a name="configure-microsoft-edge-settings-using-administrative-templates-for-windows-10-and-newer---5228061---"></a>使用适用于 Windows 10 和更高版本的管理模板配置 Microsoft Edge 设置<!-- 5228061 -->
在使用 Windows 10 和更高版本的设备上，可以创建管理模板以在 Intune 中配置组策略设置。 在此更新中，可以配置适用于 Microsoft Edge 版本 77 和更高版本的设置。

要详细了解管理模板，请参阅[使用 Windows 10 模板在 Intune 中配置组策略设置](../configuration/administrative-templates-windows.md)。

适用于：

- Windows 10 和更高版本 (Windows RS4+)

#### <a name="new-features-for-android-enterprise-dedicated-devices-in-multi-app-mode---3755304-3041943-3041946-----"></a>新增了适用于多应用模式下 Android Enterprise 专用设备的功能<!-- 3755304 3041943 3041946   -->

在 Intune 中，可以在 Android Enterprise 专用设备上通过展台样式体验来控制功能和设置（依次选择“设备配置”   > “配置文件”   > “创建配置文件”   > “Android Enterprise”  （作为平台）>“仅限设备所有者，设备限制”  （作为配置文件类型））。

在此更新中，新增了以下功能：

- “专用设备”   > “多应用”  ：虚拟主页按钮  可以通过在设备上向上轻扫来显示，也可以悬浮在屏幕上，这样用户就可以移动它。
- “专用设备”   > “多应用”  ：“闪光灯访问”  允许用户使用闪光灯。 
- “专用设备”   > “多应用”  ：“媒体音量控制”  允许用户使用滑块控制设备的媒体音量。 
- “专用设备”   > “多应用”  ：允许用户启用屏幕保护程序  ，上传自定义图像，并控制屏幕保护程序的显示时间。

要查看当前设置，请转到[便于使用 Intune 允许或限制功能的 Android Enterprise 设备设置](../configuration/device-restrictions-android-for-work.md#dedicated-device-settings)。

适用于：

- Android Enterprise 专用设备

#### <a name="new-app-and-configuration-profiles-for-android-enterprise-fully-managed-devices---3574215-3574238-3574235-3574232-----"></a>新增了适用于 Android Enterprise 完全托管设备的应用配置文件<!-- 3574215 3574238 3574235 3574232   -->
使用配置文件，可以配置设置，从而将 VPN、电子邮件和 Wi-Fi 设置应用于 Android Enterprise 设备所有者（完全托管）设备。 在此更新中，可以：

- 使用[应用配置策略](../apps/app-configuration-policies-use-android.md)来部署 Outlook、Gmail 和 Nine Work 电子邮件设置。
- 使用设备配置文件来部署[受信任的根证书设置](../protect/certificates-configure.md)。
- 使用设备配置文件来部署 [VPN](../configuration/vpn-settings-android-enterprise.md) 和 [Wi-Fi](../configuration/wi-fi-settings-android-enterprise.md) 设置。

> [!IMPORTANT]
> 利用此功能，用户可以使用 VPN、Wi-Fi 和电子邮件配置文件的用户名和密码进行身份验证。 目前，无法使用基于证书的身份验证。

适用于：  
- Android Enterprise 设备所有者（完全托管）

#### <a name="control-the-apps-files-documents-and-folders-that-open-when-users-sign-in-to-macos-devices--3914202-----"></a>控制在用户登录 macOS 设备后打开哪些应用、文件、文档和文件夹<!--3914202   -->
可以在 macOS 设备上启用和配置功能（依次选择“设备配置”   > “配置文件”   > “创建配置文件”   > “macOS”  （作为平台）>“设备功能”  （作为配置文件类型））。 

在此更新中，新增了“登录项”设置，用于控制在用户登录注册的设备后打开哪些应用、文件、文档和文件夹。 

若要查看当前设置，请转到 [Intune 中的 macOS 设备功能设置](../configuration/macos-device-features-settings.md)。

适用于：  
- macOS

#### <a name="deadlines-replace-engaged-restart-settings-for-windows-update-rings---4464404----------"></a>Windows 更新通道的“预定重启”设置替换为“截止时间”<!-- 4464404        -->
为了与最近的 [Windows 服务变更](https://docs.microsoft.com/windows/whats-new/whats-new-windows-10-version-1903#servicing)保持一致，Intune 的 Windows 10 更新通道现在[支持“截止时间”设置](../protect/windows-update-settings.md)。 “截止时间”  确定设备何时安装功能和安全更新程序。  在运行 Windows 10 1903 或更高版本的设备上，“截止时间”  取代“预定重启”  配置。  未来在旧版 Windows 10 上，“截止时间”  也会取代“预定重启”  。  

如果你未配置“截止时间”，设备会继续使用“预定重启”设置，但在将来的更新中 Intune 将会不支持“预定重启”设置   。  

请计划对所有 Windows 10 设备使用“截止时间”  。 在“截止时间”  设置就位后，可以将 Intune 配置“预定重启”更改为“未配置”  。 设置为“未配置”后，Intune 会停止管理设备上的这些设置，但不会从设备中删除上次配置的这些设置。 因此，上次配置的“预定重启”  设置会继续处于活动状态并用于设备，直到这些设置被除 Intune 以外的其他方法修改。 稍后，当设备 Windows 版本发生更改时，或当 Intune 对“截止时间”  的支持扩展到设备 Windows 版本时，设备就会开始使用已就位的新设置。

#### <a name="support-for-multiple-microsoft-intune-certificate-connectors-----4704642--------"></a>支持多个 Microsoft Intune 证书连接器<!--   4704642      -->
Intune 现在支持安装和使用多个 [Microsoft Intune 证书连接器来执行 PKCS 操作](../protect/certficates-pfx-configure.md)。 此变更支持连接器的负载均衡和高可用性。 每个连接器实例都可以处理来自 Intune 的证书请求。  如果一个连接器不可用，其他连接器将继续处理请求。

无需升级到最新版连接器软件，即可使用多个连接器。  

#### <a name="new-settings-and-changes-to-existing-settings-to-restrict-features-on-ios-and-macos-devices---4867699-4867709-----"></a>限制 iOS 和 macOS 设备上功能的新设置和现有设置变更<!-- 4867699 4867709   -->
可以在运行 iOS 和 macOS 的设备上创建限制设置的配置文件（依次选择“设备配置”   > “配置文件”   > “创建配置文件”   > “iOS”  或“macOS”  （作为平台）>“设备限制”  ）。 此更新包括以下功能：

- 依次转到“macOS”   > “设备限制”   > “云和存储”  ，使用新设置“移交”  来阻止用户在一台 macOS 设备上启动工作，并继续在另一台 macOS 或 iOS 设备上工作。

  要查看最新设置，请转到[使用 Intune 允许或限制功能的 macOS 设备设置](../configuration/device-restrictions-macos.md)。

- 依次转到“iOS”   > “设备限制”  ，有下面的一些变更：

  - “内置应用”   > “查找我的 iPhone (仅限受监督)”  ：“查找我的应用”功能中新增阻止此功能的设置。 
  - “内置应用”   > “查找我的好友(仅限受监督)”  ：“查找我的应用”功能中新增阻止此功能的设置。 
  - “无线”   > “修改 Wi-Fi 状态(仅限受监督)”  ：新增阻止用户在设备上打开或关闭 Wi-Fi 的设置。
  - “键盘和字典”   > “QuickPath (仅限受监督)”  ：新增阻止 QuickPath 功能的设置。
  - “云和存储”  ：“活动延续”  重命名为“移交”  。

  要查看最新设置，请转到[使用 Intune 允许或限制功能的 iOS 设备设置](../configuration/device-restrictions-ios.md)。

适用于：  
- macOS 10.15 及更高版本
- iOS 13 及更高版本

#### <a name="some-unsupervised-ios-device-restrictions-will-become-supervised-only-with-the-ios-130-release---4867809-----"></a>随着 iOS 13.0 版本推出，一些适用于不受监督的 iOS 设备的限制将适用于仅限受监督的设备<!-- 4867809   -->
在此更新中，随着 iOS 13.0 版本推出，一些设置适用于仅限受监督的设备。 如果这些设置是在 iOS 13.0 版本推出前配置并分配到不受监督的设备，它们仍适用于不受监督的设备。 在设备升级到 iOS 13.0 后，它们仍适用。 这些限制不适用于已备份和还原的不受监督的设备。

这些设置包括：

- App Store、文档查看和游戏
  - App Store
  - iTunes 限制级音乐、播客或新闻内容
  - 添加 Game Center 好友
  - 多玩家游戏
- 内置应用
  - 照相机
    - FaceTime
  - Safari
    - 自动填充
- 云和存储
  - 备份到 iCloud
  - 阻止 iCloud 文档同步
  - 阻止 iCloud 密钥链同步

要查看最新设置，请转到[使用 Intune 允许或限制功能的 iOS 设备设置](../configuration/device-restrictions-ios.md)。

适用于：  
- iOS 13.0 及更高版本

#### <a name="improved-device-status-for-macos-filevault-encryption---4944983-----------"></a>针对 macOS FileVault 加密改进了设备状态<!-- 4944983         -->
我们针对 macOS 设备上的 FileVault 加密更新了[多个设备状态消息](../protect/encryption-monitor.md#device-encryption-status)。

#### <a name="some-windows-defender-antivirus-scan-settings-in-the-reporting-show-a-failed-status---5119229---"></a>报告中的一些 Windows Defender 防病毒扫描设置显示“失败”状态<!-- 5119229 -->
在 Intune 中，可以创建使用 Windows Defender 防病毒来扫描 Windows 10 设备的策略（依次选择“设备配置”   > “配置文件”   > “创建配置文件”   > “Windows 10 及更高版本”  （作为平台）> “设备限制”  （作为配置文件类型）>“Windows Defender 防病毒”  ）。 “执行每日快速扫描的时间”  和“要执行的系统扫描类型”  报告显示“失败”状态（实际为“成功”状态）。 

在此更新中，这种行为得到了修复。 因此，“执行每日快速扫描的时间”  和“要执行的系统扫描类型”  设置在扫描成功完成后显示“成功”状态，并在无法应用设置时显示“失败”状态。

若要详细了解 Windows Defender 防病毒设置，请参阅[使用 Intune 允许或限制功能的 Windows 10（及更高版本）设备设置](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus)。

### <a name="zebra-technologies-is-a-supported-oem-for-oemconfig-on-android-enterprise-devices---4843713---"></a>Zebra Technologies 是 Android Enterprise 设备上受支持的 OEMConfig OEM<!-- 4843713 -->
在 Intune 中，可以创建设备配置文件，并使用 OEMConfig 将设置应用于 Android Enterprise 设备（依次选择“设备配置”   > “配置文件”   > “创建配置文件”   > “Android Enterprise”  （作为平台）>“OEMConfig”  （作为配置文件类型））。

在此更新中，Zebra Technologies 是受支持的 OEMConfig 原始设备制造商 (OEM)。 若要详细了解 OEMConfig，请参阅[通过 OEMConfig 使用和管理 Android Enterprise 设备](../configuration/android-oem-configuration-overview.md)。

适用于：  
- Android Enterprise


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>设备注册

#### <a name="default-scope-tags---3702875----"></a>默认作用域标记<!-- 3702875  -->
新增了内置默认作用域标记。 所有支持作用域标记的未标记 Intune 对象都会自动分配到默认作用域标记。 默认  作用域标记被添加到所有现有角色分配中，以与目前的管理员体验保持一致。 如果不想让管理员看到有默认作用域标记的 Intune 对象，请从角色分配中删除默认作用域标记。 此功能类似于 Configuration Manager 中的安全作用域功能。 有关详细信息，请参阅[将 RBAC 和作用域标记用于分布式 IT](scope-tags.md)。

#### <a name="android-enrollment-device-administrator-support---4869749-----"></a>Android 注册设备管理员支持<!-- 4869749   -->
Android 设备管理员注册选项已添加到“Android 注册”页（依次转到“Intune”   > “设备注册”   > “Android 注册”  ）。 默认情况下，所有租户仍将启用 Android 设备管理员。  有关详细信息，请参阅 [Android 设备管理员注册](../enrollment/android-enroll-device-administrator.md)。

#### <a name="skip-more-screens-in-setup-assistant---4877451----"></a>跳过设置助理中的更多屏幕 <!--4877451  -->
可以将设备注册计划配置文件设置为，跳过以下设置助理屏幕：
- 适用于 iOS
    - 外观
    - Express 语言
    - 首选语言
    - 设备间迁移
- 对于 macOS
    - 屏幕时间
    - Touch ID 设置

若要详细了解设置助理的自定义项，请参阅[创建适用于 iOS 的 Apple 注册配置文件](../enrollment/device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile)和[创建适用于 macOS 的 Apple 注册配置文件](../enrollment/device-enrollment-program-enroll-macos.md#create-an-apple-enrollment-profile)。

#### <a name="add-a-user-column-to-the-autopilot-device-csv-upload-process---3823054---"></a>将用户列添加到 Autopilot 设备 CSV 上传过程<!-- 3823054 -->
现在可以将用户列添加到 Autopilot 设备 CSV 上传内容中。 这样一来，就能在导入 CSV 时批量分配用户。 有关详细信息，请参阅[在 Intune 中使用 Windows AutoPilot 注册 Windows 设备](../enrollment/enrollment-autopilot.md)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>设备管理

#### <a name="configure-automatic-device-clean-up-time-limit-down-to-30-days--4231059----"></a>将自动设备清理时间限制配置缩短到 30 天<!--4231059  -->
可以将自动设备清理时间限制设置为，上次登录后 30 天（而不是之前的 90 天限制）。 为此，请依次转到“Intune”   > “设备”   > “设置”   > “设备清理规则”  。

#### <a name="build-number-included-on-android-device-hardware-page---4461910-----"></a>Android 设备“硬件”页上包含生成号<!-- 4461910   -->
每个 Android 设备的“硬件”页上都新增了包括设备操作系统生成号的条目。 有关详细信息，请参阅[使用 Intune 查看设备详细信息](../remote-actions/device-inventory.md)。

<!-- ########################## -->
## <a name="july-2019"></a>2019 年 7 月

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>应用管理

#### <a name="customized-notifications-for-users-and-groups---16766574------------"></a>发送给用户和组的自定义通知<!-- 16766574          -->
从公司门户应用向使用 Intune 管理的 iOS 和 Android 设备上的用户发送自定义推送通知。 这些移动推送通知是高度可自定义的免费文本，可以用于任何目的。 可以将它们的目标设定成组织中的不同用户组。 有关详细信息，请参阅[自定义通知](../remote-actions/custom-notifications.md)。

#### <a name="googles-device-policy-controller-app---3041950----"></a>Google 的 Device Policy Controller 应用<!-- 3041950  -->
托管主屏幕应用现在可以访问 Google 的 Android 设备策略应用。 托管主屏幕应用是一种自定义启动器，用于使用多应用展台模式在 Intune 中注册为 Android Enterprise (AE) 专用设备的设备。 你可以访问 Android 设备策略应用，或引导用户访问 Android 设备策略应用，以获取支持和进行调试。 此启动功能在设备注册并锁定到托管主屏幕时可用。 无需其他安装项，即可使用此功能。

#### <a name="outlook-protection-settings-for-ios-and-android-devices---3212619---"></a>适用于 iOS 和 Android 设备的 Outlook 保护设置<!-- 3212619 -->
现在可以使用简单的 Intune 管理控件，配置用于 Outlook for iOS 和 Outlook for Android 的常规应用配置设置和数据保护配置设置，而无需注册设备。 常规应用配置设置等同于，管理员在管理已注册设备上的 Outlook for iOS 和 Outlook for Android 时可以启用的设置。 若要详细了解 Outlook 设置，请参阅[部署 Outlook for iOS 和 Outlook for Android 应用配置设置](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune)。


#### <a name="managed-home-screen-and-managed-settings-icons---4918107---"></a>Managed Home Screen 应用图标和“托管设置”图标<!-- 4918107 -->
Managed Home Screen 应用图标和“托管设置”  图标已更新。 Managed Home Screen 应用仅用于，在 Intune 中注册为 Android Enterprise (AE) 的专用设备，且在多应用展台模式下运行的设备。 若要详细了解 Managed Home Screen 应用，请参阅[配置用于 Android Enterprise 的 Microsoft Managed Home Screen 应用](../apps/app-configuration-managed-home-screen-app.md)。

#### <a name="android-device-policy-on-android-enterprise-dedicated-devices---4918136---"></a>Android Enterprise 专用设备上的 Android Device Policy<!-- 4918136 -->
可以从 Managed Home Screen 应用的调试屏幕访问 Android Device Policy 应用。 Managed Home Screen 应用仅用于，在 Intune 中注册为 Android Enterprise (AE) 的专用设备，且在多应用展台模式下运行的设备。 有关详细信息，请参阅[配置用于 Android Enterprise 的 Microsoft Managed Home Screen 应用](../apps/app-configuration-managed-home-screen-app.md)。

#### <a name="ios-company-portal-updates---3902931---"></a>更新了 iOS 公司门户<!-- 3902931 -->
iOS 应用管理提示中的公司名称将替换当前的“i.manage.microsoft.com”文本。 例如，当尝试从公司门户安装 iOS 应用或允许管理应用时，用户将看到公司名称，而不是“i.manage.microsoft.com”。 这将在未来几天内向所有客户推出。

#### <a name="aad-and-app-on-android-enterprise-devices---3574267---"></a>Android Enterprise 设备上的 AAD 和 APP<!-- 3574267 -->
上手使用完全托管 Android Enterprise 设备时，用户现在会在初始设置新设备或恢复出厂设置的设备期间，向 Azure Active Directory (AAD) 注册。 之前，对于完全托管设备，在设置完成后，用户必须手动启动 Microsoft Intune 应用，才能启动 AAD 注册过程。 现在，当用户在初始设置后登陆设备主页时，设备就已注册。

除了更新了 AAD 之外，现在还支持在完全托管 Android Enterprise 设备上运行 Intune 应用保护策略 (APP)。 此功能将在我们推出后可用。有关详细信息，请参阅[使用 Intune 将托管 Google Play 应用添加到 Android Enterprise 设备](../apps/apps-add-android-for-work.md)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>设备配置

#### <a name="use-applicability-rules-when-creating-windows-10-device-configuration-profiles----2549910-eeready------"></a>在创建 Windows 10 设备配置配置文件时使用“适用性规则” <!-- 2549910 eeready    -->

可以创建 Windows 10 设备配置文件，具体方法为依次单击“设备配置”   > “配置文件”   > “创建配置文件”   > “Windows 10”  （作为平台）>“适用性规则”  。 在此次更新中，可以创建适用性规则  ，让配置文件仅应用于特定版本。 例如，创建一个启用某些 BitLocker 设置的配置文件。 添加配置文件后，请使用适用性规则，使配置文件仅适用于运行 Windows 10 企业版的设备。

若要添加适用性规则，请参阅[适用性规则](../configuration/device-profile-create.md#applicability-rules)。

适用于：Windows 10 及更高版本

#### <a name="use-tokens-to-add-device-specific-information-in-custom-profiles-for-ios-and-macos-devices---3330008----"></a>使用标记在 iOS 和 macOS 设备的自定义配置文件中添加设备专用信息<!-- 3330008  -->
可以使用 iOS 和 macOS 设备上的自定义配置文件，配置没有内置到 Intune 中的设置和功能，具体方法为依次单击“设备配置”   > “配置文件”   > “创建配置文件”   > “iOS”  或“macOS”  （作为平台）>“自定义”  （作为配置文件类型）。 在此次更新中，你可以向 `.mobileconfig` 文件添加标记，用于添加设备专用信息。 例如，可以将 `Serial Number: {{serialnumber}}` 添加到配置文件，用于显示设备序列号。

若要创建自定义配置文件，请参阅 [iOS 自定义设置](../configuration/custom-settings-ios.md)或 [macOS 自定义设置](../configuration/custom-settings-macos.md)。

适用于：
- iOS
- macOS

#### <a name="new-configuration-designer-when-creating-an-oemconfig-profile-for-android-enterprise---3712769-----"></a>在创建 Android Enterprise 的 OEMConfig 配置文件时使用新配置设计器<!-- 3712769   -->
在 Intune 中，可以创建使用 OEMConfig 应用的设备配置文件，具体方法为依次单击“设备配置”>“配置文件”>“创建配置文件”>“Android Enterprise”（作为平台）>“OEMConfig”（作为配置文件类型）。 当你这样做时，系统会打开 JSON 编辑器，其中包含模板和值以供你更改。 

在此次更新中，我们新增了配置设计器，它的用户体验更佳，显示应用中嵌入的详细信息，包括标题、说明等。 JSON 编辑器仍可用，并显示你在配置设计器中所做的任何更改。

若要查看当前设置，请转到[通过 OEMConfig 使用和管理 Android Enterprise 设备](../configuration/android-oem-configuration-overview.md)。

适用于：Android Enterprise

#### <a name="updated-ui-for-configuring-windows-hello---4089576--------------"></a>更新了用于配置 Windows Hello 的 UI<!-- 4089576            -->
我们更新了用于[将 Intune 配置为使用 Windows Hello 企业版](../protect/windows-hello.md)的控制台。 所有配置设置现在都位于用于启用支持 Windows Hello 的控制台的同一个窗格中。

#### <a name="intune-powershell-sdk---4924113---"></a>Intune PowerShell SDK<!-- 4924113 --> 
通过 Microsoft Graph 支持 Intune API 的 Intune PowerShell SDK 已更新到版本 6.1907.1.0。 SDK 现在支持以下功能：
- 用于 Azure 自动化。
- 支持仅限应用的身份验证读取操作。 
- 支持将易记的缩短名称用作别名。
- 符合 PowerShell 命名约定。 具体而言，`Connect-MSGraph` cmdlet 上的 `PSCredential` 参数已重命名为 `Credential`。
- 支持在使用 `Invoke-MSGraphRequest` cmdlet 时手动指定 `Content-Type` 标头的值。

有关详细信息，请参阅[用于 Microsoft Intune Graph API 的 PowerShell SDK](https://www.powershellgallery.com/packages/Microsoft.Graph.Intune)。

#### <a name="manage-filevault-for-macos----3858502--4557986--1210104----"></a>管理用于 macOS 的 FileVault<!--  3858502 + 4557986 + 1210104  -->
可以使用 Intune [管理用于 macOS 设备的 FileVault 密钥加密](../protect/encrypt-devices.md)。 若要加密设备，请使用终结点保护设备配置文件。

我们对 FileVault 的支持包括，加密未加密设备、托管设备个人恢复密钥、自动或手动轮换个人加密密钥，以及检索企业设备密钥。 最终用户还可以使用公司门户网站来获取加密设备的个人恢复密钥。

我们还扩展了加密报告，增加了 BitLocker 的 [FileVault 相关信息](../protect/encryption-monitor.md)，这样你就可以在一个地方集中查看所有设备加密详细信息了。

### <a name="new-office-windows-and-onedrive-settings-in-windows-10-administrative-templates----3510695---"></a>Windows 10 管理模板中新增 Office、Windows 和 OneDrive 设置 <!-- 3510695 -->

可以在 Intune 中创建模拟本地组策略管理的管理模板，具体方法为依次单击“设备管理”   > “配置文件”   > “创建配置文件”   > “Windows 10 及更高版本”  （作为平台）>“管理模板”  （作为配置文件类型）。

在此次更新中，我们新增了更多可添加到模板中的 Office、Windows 和 OneDrive 设置。 现在，利用这些新设置，可以配置超过 2500 项完全基于云的设置。

若要详细了解此功能，请参阅[使用 Windows 10 模板在 Intune 中配置组策略设置](../configuration/administrative-templates-windows.md)。

适用于：Windows 10 及更高版本

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>设备注册

#### <a name="updates-for-enrollment-restrictions---2871968---"></a>更新了注册限制<!-- 2871968 -->
新租户的注册限制已更新为，默认允许 Android Enterprise 工作配置文件。 现有租户不会有任何变化。 若要使用 Android Enterprise 工作配置文件，仍需[将 Intune 帐户连接到托管的 Google Play 帐户](../enrollment/connect-intune-android-enterprise.md)。

#### <a name="ui-updates-for-apple-enrollment-and-enrollment-restrictions--4089575-4089579----"></a>更新了用于 Apple 注册和注册限制的 UI<!--4089575, 4089579  -->
以下两个过程都使用向导样式的用户界面：
- Apple 设备注册。 有关详细信息，请参阅[通过 Apple 设备注册计划自动注册 iOS 设备](../enrollment/device-enrollment-program-enroll-ios.md)。
- 注册限制创建。 有关详细信息，请参阅[创建注册限制](../enrollment/enrollment-restrictions-set.md)。

#### <a name="handling-pre-configuration-of-corporate-device-identifiers-for-android-q-devices---4711509-----"></a>处理如何预配置 Android Q 设备的企业设备标识符<!-- 4711509   -->
在 Android Q (v10) 中，Google 将撤消旧版托管（设备管理员）Android 设备上的 MDM 代理收集设备标识符信息的功能。  Intune 有一项功能，可便于 IT 管理员[预配置设备序列号或 IMEI 列表](../enrollment/corporate-identifiers-add.md#identify-corporate-owned-devices-with-imei-or-serial-number)，以便自动将这些设备标记为企业所有。 此功能不适用于由设备管理员托管的 Android Q 设备。  无论设备的序列号或 IMEI 是否已上传，设备在 Intune 注册过程中始终被视为个人设备。  注册后，可以手动将所有权切换给企业。  这只影响了新注册的设备，而现有已注册设备则不受影响。  使用工作配置文件托管的 Android 设备不受此更改的影响，并将继续按目前的方式运行。  另外，注册为设备管理员的 Android Q 设备无法再将 Intune 控制台中的序列号或 IMEI 作为设备属性进行报告。

#### <a name="icons-have-changed-for-android-enterprise-enrollments-work-profile-dedicated-devices-and-fully-managed-devices---4977730---"></a>更改了用于 Android Enterprise 注册（工作配置文件、专用设备和完全托管设备）的图标<!-- 4977730 -->
Android Enterprise 注册配置文件的图标已更改。 若要查看新图标，请先依次转到“Intune”   > “注册”   > “Android 注册”  ，再在“注册配置文件”下查看  。

#### <a name="windows-diagnostic-data-collection-change---4113859---"></a>更改了 Windows 诊断数据收集<!-- 4113859 -->
对于运行 Windows 10 版本 1903 及更高版本的设备，用于诊断数据收集的默认值已更改。 自 Windows 10 1903 起，默认启用了诊断数据收集。 Windows 诊断数据是来自 Windows 设备的至关重要技术数据，包含设备相关信息以及 Windows 和相关软件的性能。 有关详细信息，请参阅[配置组织中的 Windows 诊断数据](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)。 Autopilot 设备也选择启用“全”遥测，除非在 Autopilot 配置文件中使用 [System/AllowTelemetry](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-system#system-allowtelemetry) 进行了其他设置。

#### <a name="windows-autopilot-reset-removes-the-devices-primary-user---4156123---"></a>Windows Autopilot 重置导致设备的主要用户遭删除<!-- 4156123 -->
如果设备使用 Autopilot 重置，设备的主要用户将会遭删除。 在重置后登录的下一个用户将被设置为主要用户。 此功能将在未来几天内向所有客户推出。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>设备管理

#### <a name="improve-device-location---3855417----"></a>改进了设备位置<!-- 3855417  -->
可以使用“定位设备”  操作来放大到设备的确切坐标。 若要详细了解如何定位丢失的 iOS 设备，请参阅[查找丢失的 iOS 设备](../remote-actions/device-locate.md)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>设备安全性

#### <a name="advanced-settings-for-windows-defender-firewall--public-preview----1311949-------"></a>Windows Defender 防火墙（公共预览版）的高级设置<!--  1311949     -->  
使用 Intune 管理[作为设备配置文件一部分的自定义防火墙规则](../protect/endpoint-protection-configure.md#add-custom-firewall-rules-for-windows-10-devices)，以在 Windows 10 设备上实现终结点保护。 规则可以指定应用程序、网络地址和端口的入站和出站行为。 

#### <a name="updated-ui-for-managing-security-baselines---4091125-------"></a>更新了用于管理安全基线的 UI<!-- 4091125     -->
我们在 Intune 控制台中更新了安全基线的[创建和编辑体验](../protect/security-baselines.md#create-the-profile)。 具体更改包括：

简化了向导样式格式，已压缩为一个边栏选项卡 。 这项新设计杜绝了边栏选项卡扩张，IT 专业人员不再需要向下钻取多个单独的窗格。  
现在可以在创建和编辑基线的过程中创建分配，而不必稍后返回来分配基线。 我们添加了设置摘要，你可以在新建基线和编辑现有基线前查看。 编辑时，摘要只显示正在编辑的一个属性类别中设置的项列表。

<!-- ########################## -->
## <a name="june-2019"></a>2019 年 6 月

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>应用管理

#### <a name="configure-which-browser-is-allowed-to-link-to-organization-data---3145939---"></a>配置允许哪种浏览器链接到组织数据<!-- 3145939 -->
现在，借助 Android 和 iOS 设备上的 Intune 应用保护策略 (APP)，可以将 组织网页链接
转移到特定浏览器，而不仅仅是 Intune Managed Browser 和 Microsoft Edge。  有关 APP 的详细信息，请参阅[什么是应用保护策略？](../apps/app-protection-policy.md)。

#### <a name="all-apps-page-identifies-onlineoffline-microsoft-store-for-business-apps--4089647---"></a>“所有应用”页标识适用于企业的 Microsoft Store 联机/脱机应用<!--4089647 -->
“所有应用”  页现在包含标签，用于将适用于企业的 Microsoft Store (MSFB) 应用识别为联机或脱机应用。 每个 MSFB 应用现在都包含“Online”  或“Offline”  后缀。 应用详细信息页还包含“许可证类型”  和“支持设备上下文安装”  （仅限脱机许可应用）信息。

#### <a name="company-portal-app-on-windows-shared-devices--4393553---"></a>Windows 共享设备上的公司门户应用<!--4393553 -->
用户现在可以在 Windows 共享设备上访问公司门户应用。 最终用户会在设备磁贴上看到“共享”  标签。 这适用于 Windows 公司门户应用版本 10.3.45609.0 及更高版本。

#### <a name="view-all-installed-apps-from-new-company-portal-web-page---4224326---"></a>从新版公司门户网页查看所有已安装应用<!-- 4224326 -->
公司门户网站的新增“已安装应用”  页面将列出用户设备上安装的所有（要求安装和允许安装的）托管应用。 除了分配类型，用户还可以看到应用的发布者、发布日期和当前安装状态。 如果你并未要求或允许用户安装任何应用，则用户将看到一条消息，说明尚未安装任何公司应用。 若要在 Web 上查看新页面，请转到[公司门户网站](https://portal.manage.microsoft.com)，并单击“已安装应用”  。  

#### <a name="new-view-lets-app-users-see-all-managed-apps-installed-on-device---2352913---"></a>新增视图，可让应用用户查看设备上安装的所有托管应用<!-- 2352913 -->  
现在，适用于 Windows 的公司门户应用将列出用户设备上安装的所有（要求安装和允许安装的）托管应用。 用户还可以看到已尝试和待处理的应用安装及其当前状态。 如果你并未要求或允许用户安装应用，则用户将看到一条消息，说明尚未安装任何公司应用。 若要查看新视图，请转到公司门户的导航窗格，并选择“应用”   > “已安装应用”  。

#### <a name="new-features-in-microsoft-intune-app"></a>Microsoft Intune 应用中的新功能
我们已向适用于 Android 的 Microsoft Intune 应用（预览版）添加新功能。 完全托管的 Android 设备上的用户现在可以：  

* 查看和管理通过 Intune 公司门户或 Microsoft Intune 应用注册的设备。
* 联系他们的组织以获取支持。
* 向 Microsoft 发送反馈。
* 如果组织已制定相关条款和条件，请进行查阅。

#### <a name="new-sample-apps-showing-intune-sdk-integration-available-on-github---2653471---"></a>可在 GitHub 上获取展示 Intune SDK 集成的新示例应用<!-- 2653471 -->
msintuneappsdk GitHub 帐户新增了适用于 iOS (Swift)、Android、Xamarin.iOS、Xamarin Forms 和 Xamarin.Android 的新示例应用。 这些应用旨在补充现有文档并演示如何将 Intune APP SDK 集成到自己的移动应用中。 如果你是需要其他 Intune SDK 指南的应用开发人员，请参阅以下链接示例：
- [Chatr](https://github.com/msintuneappsdk/Chatr-Sample-Intune-iOS-App) - 使用 Azure Active Directory 身份验证库 (ADAL) 进行中转身份验证的原生 iOS (Swift) 即时消息应用
。
- [Taskr](https://github.com/msintuneappsdk/Taskr-Sample-Intune-Android-App) - 使用 ADAL 进行中转身份验证的原生 Android 待办事项列表应用
。
- [Taskr](https://github.com/msintuneappsdk/Taskr-Sample-Intune-Xamarin-Android-Apps) - 使用 ADAL 进行代理身份验证的 Xamarin.Android 待办事项列表应用，此存储库还具有 Xamarin.Forms 应用。
- [Xamarin.iOS 示例应用](https://github.com/msintuneappsdk/sample-intune-xamarin-ios) - 基本 Xamarin.iOS 示例应用。


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>设备配置

#### <a name="configure-settings-for-kernel-extensions-on-macos-devices---2043024---"></a>在 macOS 设备上配置内核扩展的设置<!-- 2043024 -->
在 macOS 设备上，可以创建设备配置文件（依次选择“设备配置” > “配置文件” > “创建配置文件”> 针对平台选择“macOS”）     。 在此次更新中，我们新增了一组设置，可便于你在设备上配置和使用内核扩展。 你可以添加特定扩展，也可以允许来自特定合作伙伴或开发人员的所有扩展。

若要详细了解此功能，请参阅[内核扩展概述](../configuration/kernel-extensions-overview-macos.md)和[内核扩展设置](../configuration/kernel-extensions-settings-macos.md)。

适用于：macOS 10.13.2 及更高版本

#### <a name="apps-from-the-store-only-setting-for-windows-10-devices-includes-more-configuration-options---2697002---"></a>Windows 10 设备的“仅来自 Store 的应用”的设置包括更多配置选项<!-- 2697002 -->
为 Windows 设备创建设备限制配置文件时，可以使用“仅来自 Store 的应用”设置  ，使用户仅从 Windows 应用商店安装应用（“设备配置”   > “配置文件”   > “创建配置文件”   > 平台为“Windows 10 和更高版本”  >配置文件类型为“设备限制”  ）。 在此次更新中，我们扩展了这项设置，以支持更多选项。

若要查看新设置，请转到[允许或限制功能的 Windows 10（及更高版本）设备设置](../configuration/device-restrictions-windows-10.md#app-store)。

适用于：Windows 10 及更高版本

#### <a name="deploy-multiple-zebra-mobility-extensions-device-profiles-to-a-device-same-user-group-or-same-devices-group---4089955---"></a>将多个 Zebra 移动扩展设备配置文件部署到一台设备、同一用户组或同一设备组<!-- 4089955 -->
在 Intune 中，可以使用设备配置文件中的 Zebra 移动性扩展 (MX)，为没有内置到 Intune 中的 Zebra 设备自定义设置。 目前，可以将一个配置文件部署到一台设备。 在此次更新中，你可以将多个配置文件部署到：
- 同一用户组
- 同一设备组
- 一台设备

[通过 Microsoft Intune 中的 Zebra 移动扩展来使用和管理 Zebra 设备](../configuration/android-zebra-mx-overview.md)显示了如何在 Intune 中使用 MX。

适用于：Android

#### <a name="some-kiosk-settings-on-ios-devices-are-set-using-block-replacing-allow---4404075----"></a>iOS 设备上的一些展台设置是使用“阻止”（替代“允许”）设置的<!-- 4404075  -->
在 iOS 设备上创建设备限制配置文件时（“设备配置”   > “配置文件”   > “创建配置文件”   > 平台为“iOS”  >配置文件类型为“设备限制”  >“展台”  ），可以设置“自动锁定”  、“响铃切换”  、“屏幕旋转”  、“屏幕睡眠按钮”  和“音量按钮”  。

在此次更新中，值是“阻止”  （阻止此功能）或“未配置”  （允许此功能）。 若要查看设置，请转到[允许或限制功能的 iOS 设备设置](../configuration/device-restrictions-ios.md#kiosk)。

适用于：iOS

#### <a name="use-face-id-for-password-authentication-on-ios-devices---4490704---"></a>在 iOS 设备上使用人脸 ID 进行密码身份验证<!-- 4490704 -->
创建用于 iOS 设备的设备限制配置文件时，可将指纹用作密码。 在此次更新中，指纹密码设置还允许面部识别，具体方法为依次单击“设备配置”   > “配置文件”   > “创建配置文件”   > “iOS”  （作为平台）>“设备限制”  （作为配置文件类型）>“密码”  。 因此，更改了以下设置：

- “指纹解锁”现在更改为“Touch ID 和 Face ID 解锁”   。
- 指纹修改（仅限监管模式）现在更改为“Touch ID 和 Face ID 修改（仅限监管模式）”   。

Face ID 可在 iOS 11.0 和更高版本中使用。 若要查看设置，请转到[使用 Intune 允许或限制功能的 iOS 设备设置](../configuration/device-restrictions-ios.md#password)。

适用于：iOS

#### <a name="restricting-gaming-and-app-store-features-on-ios-devices-is-now-dependent-on-ratings-region---4593948---"></a>限制 iOS 设备上的游戏和应用商店功能现在取决于分级区域<!-- 4593948 -->
在 iOS 设备上，可以允许或限制与游戏、应用商店和查看文档相关的功能（“设备配置”   > “配置文件”   > “创建配置文件”   >  平台为“iOS”  > 配置文件类型为“设备限制”  >“应用商店、文档查看、游戏”  ）。 此外还可以选择分级区域，例如美国。

在此次更新中，“应用”  功能更改为“分级区域”  的子级，且依赖“分级区域”  。 若要查看设置，请转到[使用 Intune 允许或限制功能的 iOS 设备设置](../configuration/device-restrictions-ios.md#app-store-doc-viewing-gaming)。

适用于：iOS

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>设备注册

#### <a name="windows-autopilot-support-for-hybrid-azure-ad-join---4809146--"></a>Windows Autopilot 支持混合 Azure AD 联接<!-- 4809146-->
除了现有的 Azure AD 联接支持之外，现有设备的 Windows Autopilot 现在还支持混合 Azure AD 联接。 适用于运行 Windows 10 版本 1809 及更高版本的设备。 有关详细信息，请参阅[现有设备的 Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/existing-devices)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>设备管理

#### <a name="see-the-security-patch-level-for-android-devices---4461911---"></a>查看 Android 设备的安全修补程序级别<!-- 4461911 -->
现在可以查看 Android 设备的安全修补程序级别。 为此，请先依次选择“Intune”   > “设备”   > “所有设备”  ，再选择设备和“硬件”  。
此时，“操作系统”  部分列出了修补程序级别。

#### <a name="assign-scope-tags-to-all-managed-devices-in-a-security-group---3173810---"></a>将范围标记分配给安全组中的所有托管设备<!-- 3173810 -->
现在可以将范围标记分配给安全组，安全组中的所有设备也会与这些范围标记关联。 这些组中的所有设备也将分配有范围标记。 使用此功能设置的范围标记将覆盖使用当前设备范围标记流设置的范围标记。 有关详细信息，请参阅[将 RBAC 和范围标记用于分布式 IT](scope-tags.md)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>设备安全性

#### <a name="use-keyword-search-with-security-baselines------"></a>对安全基线使用关键字搜索<!--  -->
创建或编辑[安全基线配置文件](../protect/security-baselines.md#create-the-profile)时，可以在新“搜索”  栏中指定关键字，以从可用设置组中筛选出与搜索条件匹配的设置组。

#### <a name="the-security-baselines-feature-is-now-generally-available---3785395---"></a>安全基线功能现已推出正式版<!-- 3785395 -->
安全基线  功能已不再处于预览阶段，现已推出正式版 (GA)。  也就是说，此功能可供在生产中使用。 不过，各个基线模板可能仍处于预览阶段，并按自己的计划接受评估并推出正式版。

#### <a name="the-mdm-security-baseline-template-is-now-generally-available---3794072-4217151--3534649---"></a>MDM 安全基线模板现已推出正式版<!-- 3794072, 4217151,  3534649 -->
MDM 安全基线模板已不再处于预览阶段，现已推出正式版 (GA)。 此 GA 模板的标识为“2019 年 5 月 MDM 安全基线”  。  这是新模板，而不是从预览版升级的模板。  由于它是新模板，你需要先审阅[它包含的设置](../protect/security-baseline-settings-mdm.md)，再新建将此模板部署到设备的配置文件。 其他安全基线模板可能仍处于预览阶段。 有关可用基线的列表，请参阅[可用安全基线](../protect/security-baselines.md#available-security-baselines)。  

“2019 年 5 月 MDM 安全基线”  除了是新模板之外，还包含我们最近在开发文章中公布的两项设置：  
- 越过锁定：语音激活屏幕锁定的应用  
- DeviceGuard：在下次重启设备时使用基于虚拟化的安全性 (VBS)。  

“2019 年 5 月 MDM 安全基线”  还新增了几项新设置，删除了其他一些设置，并修订了一项设置的默认值。 有关从预览版到 GA 的更改的详细列表，请参阅“新模板中发生了什么变化”  。

#### <a name="security-baseline-versioning---3194322---"></a>安全基线版本控制<!-- 3194322 -->
用于 Intune 的安全基线支持版本控制。 借助此支持，在每个安全基线的新版本发布时，可以将现有安全基线配置文件更新为使用更高版本的基线，而无需从头开始重新创建和部署新基线。 此外，在 Intune 控制台中，还可以查看每个基线的相关信息，如使用基线的各个配置文件的数量、配置文件使用的不同基线版本的数量，以及特定安全基线的最新版本的发布时间。  有关详细信息，请参阅**安全基线**。

#### <a name="the-use-security-keys-for-sign-in-setting-has-moved---4501151---"></a>“使用安全密钥登录”设置已移动<!-- 4501151 -->
用于标识保护的设备配置设置“使用安全密钥登录”  不再是“配置 Windows Hello 企业版”  的子设置。 它现在是始终可用的顶级设置，即使你没有启用 Windows Hello 企业版，也不例外。 有关详细信息，请参阅[标识保护](../protect/identity-protection-windows-settings.md)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>基于角色的访问控制

#### <a name="new-permissions-for-assigned-group-admins---4504437-----"></a>新增了已分配的组管理员的权限<!-- 4504437   -->
Intune 的内置学校管理员角色现在对托管应用拥有创建、读取、更新和删除 (CRUD) 权限。 也就是说，在此次更新中，如果你在 Intune for Education 中被分配为组管理员，现在可以创建、查看、更新和删除 iOS MDM Push Certificate、iOS MDM 服务器令牌和 iOS VPP 令牌，此外还拥有[所有现有权限](https://docs.microsoft.com/intune-education/group-admin-delegate#group-admin-permissions)。 若要执行其中任何一项操作，请依次转到“租户设置”   > “iOS 设备管理”  。  

#### <a name="applications-can-use-the-graph-api-to-call-read-operations-without-user-credentials---4655885---"></a>应用可以使用 Graph API 来调用读取操作，而无需使用用户凭据<!-- 4655885 -->
应用可以通过应用标识来调用 Intune Graph API 读取操作，而无需使用用户凭据。 若要详细了解如何访问用于 Intune 的 Microsoft Graph API，请参阅[在 Microsoft Graph 中使用 Intune](https://docs.microsoft.com/graph/api/resources/intune-graph-overview?view=graph-rest-1.0)。

#### <a name="apply-scope-tags-to-microsoft-store-for-business-apps---4392555---"></a>将范围标记应用于适用于企业的 Microsoft Store 应用<!-- 4392555 -->
现在可以将范围标记应用于适用于企业的 Microsoft Store 应用。 若要详细了解范围标记，请参阅[将基于角色的访问控制 (RBAC) 和范围标记用于分布式 IT](scope-tags.md)。

<!-- ########################## -->
## <a name="may-2019"></a>2019 年 5 月

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>应用管理

#### <a name="reporting-for-potentially-harmful-apps-on-android-devices---4223162---"></a>报告 Android 设备上可能有害的应用<!-- 4223162 -->
Intune 现在提供有关 Android 设备上可能有害的应用的其他报告信息。 

#### <a name="windows-company-portal-app---3316993---"></a>Windows 公司门户应用<!-- 3316993 -->
Windows 公司门户应用将具有一个标记为“设备”的新页面  。 “设备”页面将显示最终用户已注册的所有设备  。 在用户使用 10.3.4291.0 或更高版本时，公司门户中将显示此更改。 要了解如何配置公司门户，请参阅[如何配置 Microsoft Intune 公司门户应用](../apps/company-portal-app.md)。

#### <a name="intune-policies-update-authentication-method-and-company-portal-app-installation---1927359----"></a>Intune 策略更新身份验证方法和公司门户应用安装<!-- 1927359  -->
在已经由“设置助理”注册的设备上（通过 Apple 公司设备注册方法之一），Intune 将不再支持由最终用户从应用商店手动安装的公司门户。 仅当在注册过程中使用 Apple 设置助理进行身份验证时，此更改才适用。 此更改也只会影响通过以下方式注册的 iOS 设备：  
* Apple 配置器
* Apple Business Manager
* Apple School Manager
* Apple 设备注册计划 (DEP)

如果用户从应用商店安装公司门户应用，然后尝试通过该应用注册这些设备，则他们将收到错误。 这些设备应仅在注册过程中通过 Intune 自动推送时，才会使用公司门户。 将更新 Azure 门户中的 Intune 注册配置文件，以便你可以指定设备的身份验证方式以及是否收到公司门户应用。 如果希望 DEP 设备用户具有公司门户，则需要在注册配置文件中指定你的首选项。 

此外，iOS 公司门户中的  “标识设备”屏幕将被删除。 因此，想要启用条件访问或部署公司应用的管理员必须更新 DEP 注册配置文件。 仅当使用设置助理对 DEP 注册进行身份验证时，此要求才适用。 在这种情况下，必须将公司门户推送到设备上。 为此，请选择“Intune” > “设备注册” > “Apple 注册” > “注册计划令牌”，依次选择令牌和“配置文件”，选择配置文件，再选择“属性”，然后将“安装公司门户”设置为“是”         。

若要在已注册的 DEP 设备上安装公司门户，需要转到“Intune”>“客户端应用”，并将其作为具有应用配置策略的托管应用进行推送。 

#### <a name="configure-how-end-users-update-a-line-of-business-lob-app-using-an-app-protection-policy---3568384---"></a>配置最终用户使用应用保护策略更新业务线 (LOB) 应用的方式<!-- 3568384 -->
用户现在可以配置最终用户可获取业务线 (LOB) 应用的更新版本的位置。 最终用户将在“最低应用版本”  条件启动对话框中看到此功能，系统将提示最终用户更新到 LOB 应用的最低版本。 必须提供这些更新详细信息作为 LOB 应用保护策略（APP）的一部分。 此功能在 iOS 和 Android 中可用。 在 iOS 上，此功能要求应用与 Intune SDK for iOS v. 10.0.7 或更高版本集成（或使用包装工具包装）。 在 Android 上，此功能需要使用最新的公司门户。 若要配置最终用户更新 LOB 应用的方式，则需要向应用发送托管应用配置策略并在其中包含键 `com.microsoft.intune.myappstore`。 发送的值将定义最终用户从哪个应用商店中下载应用。 如果应用是通过公司门户部署的，则值必须为 `CompanyPortal`。 对于任何其他应用商店，必须输入完整的 URL。

#### <a name="intune-management-extension-powershell-scripts---3734186----"></a>Intune 管理扩展 PowerShell 脚本<!-- 3734186  -->
用户可以在设备上配置使用用户的管理员权限运行的 PowerShell 脚本。 有关详细信息，请参阅[在 Intune 中的 Windows 10 设备上使用 PowerShell 脚本](../apps/intune-management-extension.md)和 [Win32 应用管理](../apps/app-management.md)。

#### <a name="android-enterprise-app-management---4459905---"></a>Android Enterprise 应用管理<!-- 4459905 -->
Intune 将自动向 Intune 管理控制台添加四个常见的与 Android Enterprise 相关的应用，以便 IT 管理员可以轻松配置和使用 Android Enterprise 管理。 这四个 Android Enterprise 应用如下所示：

- **[Microsoft Intune](https://play.google.com/store/apps/details?id=com.microsoft.intune)** - 用于 Android Enterprise 完全托管方案。
- **[Microsoft Authenticator](https://play.google.com/store/apps/details?id=com.azure.authenticator)** - 帮助你使用双因素身份验证登录帐户。
- **[Intune 公司门户](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal)** - 用于应用保护策略 (APP) 和 Android Enterprise 工作配置文件方案。
- [托管的主屏幕](https://play.google.com/store/apps/details?id=com.microsoft.launcher.enterprise) - 用于 Android Enterprise 专用/展台方案。

在过去，IT 管理员需要在设置过程中从[托管的 Google Play 商店](https://play.google.com/store/apps)手动查找并批准这些应用。 此更改消除了这些以前的手动步骤，客户可以更轻松快速地使用 Android Enterprise 管理。

当管理员首次将 Intune 租户连接到托管的 Google Play 时，他们将看到已自动添加到其 Intune 应用列表的这四个应用。 有关详细信息，请参阅[如何将 Intune 帐户连接到托管的 Google Play 帐户](../enrollment/connect-intune-android-enterprise.md)。 对于已连接其租户或已使用 Android Enterprise 的租户，管理员无需执行任何操作。 这四个应用将在 2019 年 5 月服务推出结束后的 7 天内自动显示。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>设备配置

#### <a name="updated-pfx-certificate-connector-for-microsoft-intune---1533038---"></a>更新了 Microsoft Intune 的 PFX 证书连接器<!-- 1533038 -->
我们已发布[用于 Microsoft Intune 的 PFX 证书连接器](../protect/certficates-pfx-configure.md#whats-new-for-connectors)的更新，该更新解决了以下问题：因现有 PFX 证书持续重新处理而导致连接器停止处理新请求。

#### <a name="intune-security-tasks-for-defender-atp-in-public-preview---3208597---"></a>适用于 Defender ATP 的 Intune 安全任务（公共预览版）<!-- 3208597 -->
在公共预览版中，可以使用 Intune 管理 [Microsoft Defender 高级威胁防护 (ATP) 的安全任务](../protect/atp-manage-vulnerabilities.md)。 这与 ATP 集成，并增加了基于风险的方法来发现终结点漏洞和配置错误，并对其设置优先级和进行修正，同时缩短了从发现到缓解的时间。

#### <a name="check-for-a-tpm-chipset-in-a-windows-10-device-compliance-policy---3617671-----"></a>了解 Windows 10 设备合规性策略中的 TPM 芯片组<!-- 3617671   -->
许多 Windows 10 及更高版本设备都具有受信任的平台模块 (TPM) 芯片组。 此更新包含一个新符合性设置，它将检查设备上的 TPM 芯片版本。

[Windows 10 及更高版本的符合性策略设置](../protect/compliance-policy-create-windows.md#device-security)介绍了此设置。

适用于：Windows 10 及更高版本

#### <a name="prevent-end-users-from-modifying-their-personal-hotspot-and-disable-siri-server-logging-on-ios-devices---4097904-----"></a>防止最终用户修改其个人热点，并禁止 Siri 服务器登录 iOS 设备<!-- 4097904   -->  
为 iOS 设备创建设备限制配置文件（在“设备配置”   > “配置文件”   > “创建配置文件”   >  针对平台选择“iOS”  > 针对配置文件类型选择“设备限制”  ）。 此更新包括可配置的新设置：

- **内置应用**：Siri 命令的服务器端日志记录
- **无线**：个人热点的用户修改（仅限监管模式）

若要查看这些设置，请转到[适用于 iOS 的内置应用设置](../configuration/device-restrictions-ios.md#built-in-apps)和[适用于 iOS 的无线设置](../configuration/device-restrictions-ios.md#wireless)。

适用于：iOS 12.2 及更新版本

#### <a name="new-classroom-app-device-restriction-settings-for-macos-devices---4097905-----"></a>macOS 设备的新 Classroom 应用设备限制设置<!-- 4097905   --> 
可以为 macOS 设备创建设备配置文件（依次选择“设备配置”   > “配置文件”   > “创建配置文件”   >  针对平台选择“macOS”  > 针对配置文件类型选择“设备限制”  ）。 在此次更新中，我们新增了 Classroom 应用设置
、用于阻止屏幕截图的选项，以及用于禁用 iCloud 照片库的选项。

要查看最新设置，请转到[使用 Intune 允许或限制功能的 macOS 设备设置](../configuration/device-restrictions-macos.md)。

适用范围：macOS

#### <a name="the-ios-password-to-access-app-store-setting-is-renamed---4557891----"></a>已重命名用于访问应用商店设置的 iOS 密码<!-- 4557891  -->
“用于访问应用商店的密码”  设置已重命名为“要求所有购买都输入 iTunes Store 密码”  （“设备配置”   > “配置文件”   > “创建配置文件”   > “iOS”  (针对平台) > 配置文件类型的“设备限制”  >“App Store、文档查看和游戏”  ）。

若要查看可用设置，请转到 [App Store、文档查看和游戏 iOS 设置](../configuration/device-restrictions-ios.md#app-store-doc-viewing-gaming)。

适用于：iOS

#### <a name="microsoft-defender-advanced-threat-protection--baseline--preview----3754134---"></a>Microsoft Defender 高级威胁防护基线（预览版）<!--  3754134 -->
已添加用于 [Microsoft Defender 高级威胁防护](../protect/security-baseline-settings-defender-atp.md)设置的安全基线（预览版）。 当环境满足使用 [Microsoft Defender 高级威胁防护](../protect/advanced-threat-protection.md#prerequisites)的先决条件时，此基线才可用。

#### <a name="outlook-signature-and-biometric-settings-for--ios-and-android-devices---4050557---"></a>适用于 iOS 和 Android 设备的 Outlook 签名和生物识别设置<!-- 4050557 -->
现在可以指定是否在 iOS 和 Android 设备上的 Outlook 中启用了默认签名。 此外，还可以选择允许用户更改 iOS 上的 Outlook 中的生物识别设置。

#### <a name="network-access-control-nac-support-for-f5-access-for-ios-devices---4500808---"></a>面向 iOS 设备针对 F5 Access 的网络访问控制 (NAC) 支持<!-- 4500808 -->
F5 发布了针对 BIG-IP 13 的更新，在 Intune 中实现了针对 iOS 上的 F5 Access 的 NAC 功能支持。 使用此功能需要：

- 将 BIG-IP 更新为 13.1.1.5 版。 不支持 BIG-IP 14。
- 将 BIG-IP 与 Intune 相集成以配置 NAC。 [概述：使用终结点管理系统配置 APM 以进行设备状态检查](https://techdocs.f5.com/kb/en-us/products/big-ip_apm/manuals/product/apm-client-configuration-7-1-6/6.html)中列出了相关步骤。
- 在 Intune 中的 VPN 配置文件中选择“启用网络访问控制(NAC)”设置  。

若要查看可用设置，请转至[在 iOS 设备上配置 VPN](../configuration/vpn-settings-ios.md)。

适用于：iOS

#### <a name="updated-pfx-certificate-connector-for-microsoft-intune---doc-vso-1521237----"></a>更新了 Microsoft Intune 的 PFX 证书连接器<!-- doc-vso 1521237  -->  
我们发布了针对 [Microsoft Intune 的 PFX 证书连接器](../protect/certficates-pfx-configure.md#whats-new-for-connectors)的更新，将轮询间隔从 5 分钟降到了 30 秒。


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>设备注册

#### <a name="autopilot-device-orderid-attribute-name-changed-to-group-tag----4659453---"></a>Autopilot 设备的 OrderID 属性名称已更改为“组标记” <!-- 4659453 -->

为更直观地显示，Autopilot 设备上的 OrderID 属性名称已更改“组标记”   。 在使用 CSV 上传 Autopilot 设备信息时，必须使用“组标记”而不是 OrderID 作为列标题。  

#### <a name="windows-enrollment-status-page-esp-is-now-generally-available---3605348---"></a>Windows 注册状态页 (ESP) 现已正式发布<!-- 3605348 -->
注册状态页现在没有预览版。 有关详细信息，请参阅[设置注册状态页](../enrollment/windows-enrollment-status.md)。

#### <a name="intune-user-interface-update---autopilot-enrollment-profile-creation---4593669---"></a>Intune 用户界面更新 - 创建 Autopilot 注册配置文件<!-- 4593669 -->
用于创建 Autopilot 注册配置文件的用户界面已更新为与 Azure 用户界面样式保持一致。 有关详细信息，请参阅[创建 Autopilot 注册配置文件](../enrollment/enrollment-autopilot.md#create-an-autopilot-deployment-profile)。 接下来，其他 Intune 方案将更新为此新 UI 样式。

#### <a name="enable-autopilot-reset-for-all-windows-devices---4225665---"></a>为所有 Windows 设备启用 Autopilot 重置<!-- 4225665 -->
Autopilot 重置现在适用于所有 Windows 设备，甚至包括那些未配置为使用注册状态页的设备。 如果在初始设备注册过程中未为设备配置注册状态页，则设备将在登录后直接转到桌面。 在 Intune 中可能需要多达 8 小时来进行同步并显示符合。 有关详细信息，请参阅[使用远程 Windows Autopilot 重置功能重置设备](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot-reset-remote)。

#### <a name="exact-imei-format-not-required-when-searching-all-devices--30407680---"></a>搜索所有设备时不需要确切的 IMEI 格式<!--30407680 -->
搜索“所有设备”  时，无需在 IMEI 号码中包含空格。

#### <a name="deleting-a-device-in-the-apple-portal-will-be-reflected-in-the-intune-portal--2489996---"></a>从 Apple 门户删除设备时，Intune 门户将反映此操作<!--2489996 -->
如果从 Apple 的设备注册计划或 Apple Business Manager 门户删除设备，下次同步时将自动从 Intune 删除该设备。

### <a name="the-enrollment-status-page-now-tracks-win32-apps---2714451---"></a>注册状态页现在跟踪 Win32 应用<!-- 2714451 -->
这仅适用于运行 Windows 10 版本 1903 及更高版本的设备。 有关详细信息，请参阅[设置注册状态页](../enrollment/windows-enrollment-status.md)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>设备管理

#### <a name="reset-and-wipe-devices-in-bulk-by-using-the-graph-api---3295288---"></a>使用 Graph API 批量重置和擦除设备<!-- 3295288 -->
用户现在可以使用 Graph API 批量重置和擦除多达 100 台设备。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>监视和故障排除

#### <a name="the-encryption-report-is-out-of-public-preview---4587546--------"></a>加密报表没有公共预览版<!-- 4587546      -->
[BitLocker 和设备加密的报表](../protect/encryption-monitor.md)现已正式发布，并且不再是公共预览版的一部分。


<!-- ########################## -->
## <a name="april-2019"></a>2019 年 4 月

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>应用管理
#### <a name="user-experience-update-for-the-company-portal-app-for-ios---2536024---"></a>iOS 版公司门户应用的用户体验更新<!-- 2536024 -->
适用于 iOS 设备的公司门户应用的主页已经过重新设计。 经此更改后，主页将更好地遵循 iOS UI 模式，更易于查找应用和电子书。

#### <a name="changes-to-company-portal-enrollment-for-ios-12-device-users--3448635---"></a>对 iOS 12 设备用户的公司门户注册的更改<!--3448635 -->
适用于 iOS 的公司门户的注册屏幕和步骤已更新，以与 Apple iOS 12.2 中发布的 MDM 注册更改保持一致。 更新的工作流提示用户执行以下操作：  

* 允许 Safari 在返回公司门户应用之前打开公司门户网站并下载管理配置文件。  
* 打开“设置”应用以在其设备上安装管理配置文件。
* 返回公司门户应用以完成注册。  

要了解更新的注册步骤和屏幕，请参阅[在 Intune 中注册 iOS 设备](https://docs.microsoft.com/user-help/enroll-your-device-in-intune-ios)。

#### <a name="openssl-encryption-for-android-app-protection-policies---3747362---"></a>Android 应用保护策略的 OpenSSL 加密<!-- 3747362 -->
Android 设备上的 Intune 应用保护策略 (APP) 现在使用符合 FIPS 140-2 标准的 OpenSSL 加密库。 有关详细信息，请参阅 [Microsoft Intune 中的 Android 应用保护策略设置](../apps/app-protection-policy-settings-android.md)的[加密](../apps/app-protection-policy-settings-android.md#encryption)部分。

#### <a name="enable-win32-app-dependencies---2617348----"></a>启用 Win32 应用依赖项<!-- 2617348  -->
管理员可以要求在安装 Win32 应用之前，将其他应用作为依赖项进行安装。 具体来说，设备必须先安装相关应用，再安装 Win32 应用。 在 Intune 中，选择“客户端应用” > “应用” > “添加”，以显示“添加应用”边栏选项卡     。 选择“Windows 应用(Win32)”作为“应用类型”   。 添加应用后，可以选择“依赖项”，添加在安装 Win32 应用之前必须安装的相关应用  。 有关详细信息，请参阅 [Intune 独立版 - Win32 应用管理](./../apps/app-management.md)。 

#### <a name="app-version-installation-information-for-microsoft-store-for-business-apps---3537391-----"></a>适用于企业的 Microsoft Store 应用的应用版本安装信息<!-- 3537391   -->
应用安装报告包括适用于企业的 Microsoft Store 应用的应用版本信息。 在 Intune 中，选择“客户端应用” > “应用”   。 选择“适用于企业的 Microsoft Store 应用”，然后在“监视”部分下选择“设备安装状态”    。

#### <a name="additions-to-win32-apps-requirement-rules---3676883-----"></a>Win32 应用要求规则的新增内容<!-- 3676883   -->
可以基于 PowerShell 脚本、注册表值和文件系统信息创建要求规则。 在 Intune 中，选择“客户端应用” > “应用” > “添加”    。 然后，在“添加应用”边栏选项卡中选择“Windows 应用(Win32)”作为“应用类型”    。  选择“要求” > “添加”，以配置其他要求规则   。 然后，选择“文件类型”、“注册表”或“脚本”作为“要求类型”     。 有关详细信息，请参阅 [Win32 应用管理](./../apps/app-management.md)。

#### <a name="configure-your-win32-apps-to-be-installed-on-intune-enrolled-azure-ad-joined-devices---3695227----"></a>配置在已注册到 Intune 并且已加入 Azure AD 的设备上安装Win32 应用<!-- 3695227  -->
可以分配在已注册到 Intune 并且已加入 Azure AD 的设备上安装 Win32 应用。 有关 Intune 中 Win32 应用的详细信息，请参阅 [Win32 应用管理](./../apps/app-management.md)。

#### <a name="device-overview-shows-primary-user--3794259----"></a>设备概述显示主要用户<!--3794259  -->
“设备概述”页将显示主要用户，也称为用户设备相关性用户 (UDA)。 要查看设备的主要用户，请选择“Intune” > “设备” > “所有设备”> 选择一个设备    。 主要用户将显示在靠近“概述”页顶部的位置  。

#### <a name="additional-managed-google-play-app-reporting-for-android-enterprise-work-profile-devices---4105925----"></a>Android Enterprise 工作配置文件设备的其他托管 Google Play 应用报告<!-- 4105925  -->
对于部署到 Android Enterprise 工作配置文件设备的托管 Google Play 应用，可以查看设备上安装的应用的特定版本号。 这仅适用于所需的应用。  

#### <a name="ios-third-party-keyboards---4111843-----"></a>iOS 第三方键盘<!-- 4111843   -->
由于 iOS 平台更改，不再支持适用于针对 iOS 的“第三方键盘”设置的 Intune 应用保护策略 (APP) 的支持  。 你将无法在 Intune 管理控制台中配置此设置，并且此设置将不会在 Intune App SDK 中的客户端上强制执行。


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>设备配置

#### <a name="updated-certificate-connectors---icm-113304612---"></a>更新了证书连接器<!-- ICM 113304612 -->
我们已经发布了针对 [Microsoft Intune 的 Intune 证书连接器和 PFX 证书连接器](../protect/certficates-pfx-configure.md#whats-new-for-connectors)的更新。 新版本修复了几个已知问题。

#### <a name="set-login-settings-and-control-restart-options-on-macos-devices---1210083----"></a>在 macOS 设备上设置登录设置和控制重启选项<!-- 1210083  -->
在 macOS 设备上，可以创建设备配置文件（依次选择“设备配置” > “配置文件” > “创建配置文件” > 针对平台选择“macOS”> 针对配置文件类型选择“设备功能”）      。 此更新包括新的登录窗口设置，例如显示自定义横幅、选择用户登录方式、显示或隐藏电源设置等。

要查看这些设置，请转到 [macOS 设备功能设置](../configuration/macos-device-features-settings.md)。

#### <a name="configure-wifi-on-android-enterprise-device-owner-dedicated-devices-running-in-multi-app-kiosk-mode--3041940----"></a>在以多应用展台模式运行的 Android Enterprise 和设备所有者专用设备上配置 WiFi<!--3041940  -->
可以在以多应用展台模式运行的 Android Enterprise 和设备所有者专用设备上启用设置。 在此更新中，可让用户配置和连接到 WiFi 网络（依次选择“Intune” > “设备配置” > “配置文件” > “创建配置文件” >  针对平台选择“Android Enterprise”> 针对配置文件类型选择“仅限设备所有者”>“设备限制”>“专用设备” > “展台模式”         ：“多应用” > “WiFi 配置”)   。

要查看可以配置的所有设置，请转到[用于允许或限制功能的 Android Enterprise 设备设置](../configuration/device-restrictions-android-for-work.md)。

适用于：以多应用展台模式运行的 Android Enterprise 专用设备

#### <a name="configure-bluetooth-and-pairing-on-android-enterprise-device-owner-dedicated-devices-running-in-multi-app-kiosk-mode---3041941----"></a>在以多应用展台模式运行的 Android Enterprise 和设备所有者专用设备上配置蓝牙和配对<!-- 3041941  -->
可以在以多应用展台模式运行的 Android Enterprise 和设备所有者专用设备上启用设置。 在此更新中，你可以允许最终用户启用蓝牙并通过蓝牙进行设备配对（依次选择“Intune” > “设备配置” > “配置文件” > “创建配置文件” >  针对平台选择“Android Enterprise”> 针对配置文件类型选择“仅限设备所有者”>“设备限制”>“专用设备” > “展台模式”         ：“多应用” > “蓝牙配置”)   。

要查看可以配置的所有设置，请转到[用于允许或限制功能的 Android Enterprise 设备设置](../configuration/device-restrictions-android-for-work.md)。

适用于：以多应用展台模式运行的 Android Enterprise 专用设备

#### <a name="create-and-use-oemconfig-device-configuration-profiles-in-intune---3305883----"></a>在 Intune 中创建和使用 OEMConfig 设备配置文件<!-- 3305883  -->
在此更新中，Intune 支持使用 OEMConfig 配置 Android Enterprise 设备。 具体来说，可以使用 OEMConfig 创建设备配置文件并将设置应用于 Android Enterprise 设备（依次选择“设备配置” > “配置文件” > “创建配置文件” >  针对平台选择“Android Enterprise”）     。

对 OEM 的支持目前基于每个 OEM。 如果 OEMConfig 应用列表中未包含所需 OEMConfig 应用，请联系 `IntuneOEMConfig@microsoft.com`。

要了解有关此功能的详细信息，请转到[在 Microsoft Intune 中通过 OEMConfig 使用和管理 Android Enterprise 设备](../configuration/android-oem-configuration-overview.md)。

适用于：Android Enterprise

#### <a name="windows-update-notifications---3316758-3316782----"></a>Windows 更新通知<!-- 3316758, 3316782  -->
我们已将两个“用户体验设置”添加到了你可以在 Intune 控制台中管理的 Windows 更新通道配置中  。 现在可以执行以下操作：
- 阻止或允许用户[扫描 Windows 更新](../protect/windows-update-settings.md)。
- 管理向用户显示的 [Windows 更新通知级别](../protect/windows-update-settings.md)。

#### <a name="new-device-restriction-settings-for-android-enterprise-device-owner---3574254----"></a>针对 Android Enterprise 和设备所有者的新设备限制设置<!-- 3574254  -->
在 Android Enterprise 设备上，可以创建设备限制配置文件，以允许或限制功能和设置密码规则等（依次选择“设备配置” > “配置文件” > “创建配置文件”> 针对平台选择“Android Enterprise”> 针对配置文件类型选择“仅限设备所有者”>“设备限制”      ）。 

此更新包括新密码设置，允许完全托管设备对 Google Play 商店中应用的完全访问权限，等等。 要查看设置的当前列表，请转到[用于允许或限制功能的 Android Enterprise 设备设置](../configuration/device-restrictions-android-for-work.md)。 

适用于：Android Enterprise 完全托管设备

#### <a name="check-for-a-tpm-chipset-in-a-windows-10-device-compliance-policy---3617671---"></a>了解 Windows 10 设备合规性策略中的 TPM 芯片组<!-- 3617671 -->

此功能已推迟，并计划稍后发布。

#### <a name="updated-ui-changes-for-microsoft-edge-browser-on-windows-10-and-later-devices---3775833-----"></a>更新了 Windows 10 及更高版本设备上 Microsoft Edge 浏览器的 UI 更改<!-- 3775833   -->
创建设备配置文件时，可以允许或限制 Windows 10 及更高版本设备上的 Microsoft Edge 功能（依次选择“设备配置” > “配置文件” > “创建配置文件”> 针对平台选择“Windows 10 和更高版本”> 针对配置文件类型选择“设备限制”>“Microsoft Edge 浏览器”     >     ）。 在此更新中，Microsoft Edge 设置的描述更具体，更易于理解。

要查看这些功能，请转到 [Microsoft Edge 浏览器设备限制设置](../configuration/device-restrictions-windows-10.md#microsoft-edge-browser)。

适用于：Windows 10 及更高版本

#### <a name="expanded-support-for-android-enterprise-fully-managed-devices--preview-----3903241-3903244-3903246-----"></a>扩展了对 Android Enterprise 完全托管设备（预览版）的支持<!--   3903241, 3903244, 3903246   -->
我们继续在公开预览版中扩展了对 Android Enterprise 完全托管设备的支持（于 2019 年 1 月首次发布，包括以下内容：

- 在完全托管设备和专用设备上，可以创建[合规性策略](../protect/compliance-policy-create-android-for-work.md)以包括密码规则和操作系统要求（依次选择“设备合规性” > “策略” > “创建策略”> 针对平台选择“Android Enterprise”> 针对配置文件类型选择“设备所有者”     >    ）。

  在专用设备上，设备可能显示为“不合规”  。 在专用设备上无法进行条件访问。 请务必完成任何任务或操作，以确保专用设备符合分配的策略。

- [条件访问](../protect/conditional-access.md) - 适用于 Android 的条件访问策略也适用于 Android Enterprise 完全托管设备。 用户现在可以使用 Microsoft Intune 应用在 Azure Active Directory 中注册其完全托管设备  。 然后，查看并解决任何合规性问题，以访问组织资源。

- 新最终用户应用（Microsoft Intune 应用）- 有一种用于 Android 完全托管设备的新最终用户应用，名为 Microsoft Intune  。 此新应用是轻量型且新式的
，可提供与公司门户应用类似的功能，但适用于完全托管设备。 有关详细信息，请参阅 [Google Play 上的 Microsoft Intune 应用](https://play.google.com/store/apps/details?id=com.microsoft.intune)。

若要设置完全托管的 Android 设备，请转到“设备注册”   > “Android 注册”   >   “公司拥有的完全托管的用户设备”。 完全托管的 Android 设备的支持仍为预览版，某些 Intune 功能可能无法完全正常运行。  

要详细了解此预览版，请参阅我们的博客 [Microsoft Intune - Preview 2 for Android Enterprise Fully Managed devices](https://aka.ms/preview2_AE_fullymanaged)（适用于 Android Enterprise 完全托管设备的 Microsoft Intune - 预览版 2）。

#### <a name="use-compliance-manager-to-create-assessments-for-microsoft-intune---4404750---"></a>使用合规性管理器为 Microsoft Intune 创建评估<!-- 4404750 -->

[合规性管理器](https://servicetrust.microsoft.com/ComplianceManager)（打开另一个 Microsoft 站点）是 Microsoft 服务信任门户中基于工作流的风险评估工具。 它使你能够跟踪、分配和验证组织中与 Microsoft 服务相关的法规遵从性活动。 可以使用 Office 365、Azure、Dynamics、专业服务和 Intune 创建自己的合规性评估。 Intune 提供两种评估：FFIEC 和 GDPR。

合规性管理器可将控件分类（由 Microsoft 管理的控件和由组织管理的控件），从而帮助你节省精力。 你可以完成评估，然后导出并打印评估。

[联邦金融机构检查委员会 (FFIEC)](https://www.microsoft.com/trustcenter/compliance/FFIEC)（打开另一个 Microsoft 站点）合规性是 FFIEC 发布的一套网上银行标准。 对于使用 Intune 的金融机构来说，这是最必不可少的评估。 它诠释了 Intune 如何帮助遵循与公有云工作负载相关的 FFIEC 网络安全指南。 Intune 的 FFIEC 评估是合规性管理器中的第二种 FFIEC 评估。

以下示例介绍 FFIEC 控件的明细。 Microsoft 负责 64 个控件。 你负责其余 12 个控件。

![请参阅 FFIEC 的 Intune 评估示例，其中包括客户操作和 Microsoft 操作](./media/whats-new/intune-ffiec-assessment-status.png)

[一般数据保护条例 (GDPR)](https://www.microsoft.com/trustcenter/privacy/gdpr/gdpr-overview)（打开另一个 Microsoft 站点）是欧盟 (EU) 法律，用于帮助保护个人及其数据的权利。 GDPR 是帮助遵守隐私法规的必不可少的评估。 

以下示例介绍 GDPR 控件的明细。 Microsoft 负责 49 个控件。 你负责其余 66 个控件。

![请参阅 GDPR 的 Intune 评估示例，其中包括客户操作和 Microsoft 操作](./media/whats-new/intune-assessment-status.png)


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>设备注册

#### <a name="configure-profile-to-skip-some-screens-during-setup-assistant---2276470----"></a>将配置文件配置为在“设置助手”期间跳过某些屏幕<!-- 2276470  -->
创建 macOS 注册配置文件时，可将其配置为在用户使用设置助手期间跳过以下任一屏幕：
- 外观
- 显示基调
- iCloudStorage：如果你新建或编辑配置文件，选定跳过屏幕需要与 Apple MDM 服务器同步。  用户可以发起手动同步设备，这样在选取配置文件变更时就不会有任何延迟。
有关详细信息，请参阅[通过设备注册计划或 Apple School Manager 自动注册 macOS 设备](../enrollment/device-enrollment-program-enroll-macos.md)。

#### <a name="bulk-device-naming-when-enrolling-corporate-ios-devices--3566569----"></a>注册企业 iOS 设备时批量命名设备<!--3566569  -->
使用 Apple 的任一企业注册方法 (DEP/ABM/ASM) 时，可以设置设备名格式，以自动命名传入的 iOS 设备。 可以在模板中指定包含设备类型和序列号的格式。 为此，请选择“Intune” > “设备注册” > “Apple 注册” > “注册程序令牌” > “选择令牌” >“创建配置文件” > “设备命名格式”        。 可以编辑现有配置文件，但只有新同步的设备才会应用该名称。

#### <a name="updated-default-timeout-message-on-enrollment-status-page---3959331---"></a>更新了“注册状态”页上的默认超时消息<!-- 3959331 -->
我们更新了在“注册状态”页 (ESP) 超过 ESP 配置文件中指定的超时值时用户看到的默认超时消息。 新的默认消息是用户看到的内容，可帮助他们了解 ESP 部署的下一步操作。  

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>设备管理

#### <a name="retire-noncompliant-devices---1827291-----"></a>停用不合规的设备<!-- 1827291   -->
此功能已推迟，并计划在将来版本中发布。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>监视和故障排除

#### <a name="intune-data-warehouse-v10-changes-reflecting-back-to-beta---4403765---"></a>Intune 数据仓库 V1.0 更改在 beta 版本中体现<!-- 4403765 -->
V1.0 在 1808 版本首次引入后，它在某些重要方面与 beta 版 API 有所不同。 在 1903 版本中，这些更改将在 beta 版 API 中体现。 如果有使用 beta 版 API 的重要报表，我们强烈建议将这些报表切换到 V1.0 以避免中断性变更。 有关详细信息，请参阅 [Intune 数据仓库 API 的更改日志](../developer/reports-changelog.md#1903-part-2)。

#### <a name="monitor-security-baseline-status-public-preview----3082047---"></a>监控安全基线状态（公共预览版） <!-- 3082047 --> 
我们向安全基线的监控添加了[每个类别的视图](../protect/security-baselines-monitor.md#per-category-view)（安全基线仍为预览版）。 （安全基线仍为预览版）。 每个类别的视图显示基线中的每个类别以及属于该类别的每个状态组的设备百分比。 现可查看与各个类别不匹配、配置错误或不适用的设备数量。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>基于角色的访问控制

#### <a name="scope-tags-for-apple-vpp-tokens--2371886----"></a>Apple VPP 令牌的范围标记<!--2371886  -->
现可将范围标记添加到 Apple VPP 令牌。 只有分配有相同范围标记的用户才能访问带有该标记的 Apple VPP 令牌。 使用该令牌购买的 VPP 应用和电子书会继承其范围标记。 有关范围标记的详细信息，请参阅[使用 RBAC 和范围标记](scope-tags.md)。

<!-- ########################## -->
## <a name="march-2019"></a>2019 年 3 月

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>应用管理
#### <a name="deploy-microsoft-visio-and-microsoft-project---3725386----"></a>部署 Microsoft Visio 和 Microsoft Project<!-- 3725386  -->
现可使用 Microsoft Intune，将 Microsoft Visio Pro for Office 365 和 Microsoft Project Online 桌面客户端作为独立应用部署到 Windows 10 设备（如果拥有这些应用的许可证）。 在 Intune 中，选择“客户端应用” > “应用” > “添加”，以显示“添加应用”边栏选项卡     。 在“添加应用”边栏选项卡上，选择“Windows 10”作为“应用类型”    。 然后，选择“配置应用套件”，以选择要安装的应用  。 有关适用于 Windows 10 设备的 Office 365 应用的详细信息，请参阅[使用 Microsoft Intune 将 Office 365 应用分配给 Windows 10 设备](../apps/apps-add-office365.md)。

#### <a name="microsoft-visio-pro-for-office-365-product-name-change---3593653----"></a>Microsoft Visio Pro for Office 365 产品名称更改<!-- 3593653  -->
Microsoft Visio Pro for Office 365 现在称为 Microsoft Visio Online 计划 2   。  有关 Microsoft Visio 的详细信息，请参阅 [Visio Online 计划 2](https://products.office.com/visio/visio-online-plan-2)。 有关适用于 Windows 10 设备的 Office 365 应用的详细信息，请参阅[使用 Microsoft Intune 将 Office 365 应用分配给 Windows 10 设备](../apps/apps-add-office365.md)。

#### <a name="intune-app-protection-policy-app-character-limit-setting---3291302----"></a>Intune 应用保护策略 (APP) 字符限制设置<!-- 3291302  -->
Intune 管理员可以指定 Intune APP“限制使用其他应用剪切、复制和粘贴”策略设置的例外情况  。  管理员可以指定可能会从托管应用中剪切或复制的字符数。 此设置允许将指定数量的字符共享到任何应用，而不受“限制使用其他应用剪切、复制和粘贴”设置的限制。 请注意，适用于 Android 的 Intune 公司门户应用版本需要 5.0.4364.0 或更高版本。 有关详细信息，请参阅 [iOS 数据保护](../apps/app-protection-policy-settings-ios.md#data-protection)、[Android 数据保护](../apps/app-protection-policy-settings-android.md#data-protection)和[查看客户端应用保护日志](../apps/app-protection-policy-settings-log.md#app-protection-policy-settings)。

#### <a name="office-deployment-tool-odt-xml-for-office-proplus-deployment---3192477-----"></a>用于进行 Office ProPlus 部署的 Office 部署工具 (ODT) XML<!-- 3192477   -->
在 Intune 管理控制台中创建 Office Pro Plus 实例时，将能够提供 Office 部署工具 (ODT) XML。 如果现有的 Intune UI 选项无法满足需求，这将允许进行更多自定义。 有关详细信息，请参阅[使用 Microsoft Intune 将 Office 365 应用分配到 Windows 10 设备](../apps/apps-add-office365.md)以及 [Office 部署工具的配置选项](https://docs.microsoft.com/DeployOffice/configuration-options-for-the-office-2016-deployment-tool)。

#### <a name="app-icons-will-now-be-displayed-with-an-automatically-generated-background---1429026----"></a>现在将显示自动生成背景的应用图标<!-- 1429026  -->
在 Windows 公司门户应用中，现在将显示应用图标，其中的背景根据图标主色（如果可检测到）自动生成。 如果适用，此背景将替换以前应用磁贴上显示的灰色边框。 用户将在 10.3.3451.0 之后的公司门户版本中看到此更改。

#### <a name="install-available-apps-using-the-company-portal-app-after-windows-bulk-enrollment---2751523-----"></a>在 Windows 批量注册后，使用公司门户应用安装可用的应用<!-- 2751523   -->
使用 [Windows 批量注册](../enrollment/windows-bulk-enroll.md)（预配包）注册到 Intune 的 Windows 设备将能够使用公司门户应用安装可用的应用。 有关公司门户应用的详细信息，请参阅[手动添加 Windows 10 公司门户](../apps/store-apps-company-portal-app.md)和[如何配置 Microsoft Intune 公司门户应用](../apps/company-portal-app.md)。

#### <a name="the-microsoft-teams-app-can-be-selected-as-part-of-the-office-app-suite---3828932----"></a>可以选择 Microsoft Teams 应用作为 Office 应用套件的一部分<!-- 3828932  -->
在安装 Office Pro Plus 应用套件的过程中，可以包含或排除 Microsoft Teams 应用。 此功能适用于 Office Pro Plus 内部版本号 16.0.11328.20116+。 用户必须先注销，然后登录设备，才能完成安装。 在 Intune 中，选择“客户端应用” > “应用” > “添加”    。 选择一种“Office 365 套件”应用类型，然后选择“配置应用套件”   。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>设备配置

#### <a name="automatically-start-an-app-when-running-multiple-apps-in-kiosk-mode-on-windows-10-and-later-devices---2351390---"></a>在 Windows 10 及更高版本的设备上以展台模式运行多个应用时自动启动应用<!-- 2351390 -->

在 Windows 10 及更高版本的设备上，能够以展台模式运行设备，并运行许多应用。 在此更新中，可以进行自动启动设置（依次选择“设备配置” > “配置文件” > “创建配置文件” >  针对平台选择“Windows 10 和更高版本”> 针对配置文件类型选择“展台”>“多应用展台”）        。 使用此设置可在用户登录设备时自动启动应用。

要查看所有展台设置的列表和说明，请参阅 [Intune 中作为展台运行的 Windows 10 和更高版本设备的设置](../configuration/kiosk-settings-windows.md)。

适用于：Windows 10 及更高版本

#### <a name="operational-logs-also-show-details-on-non-compliant-devices---4063755----"></a>操作日志还显示有关不合规设备的详细信息<!-- 4063755  -->
将 Intune 日志路由到 Azure 监视器功能时，还可以路由操作日志。 在此更新中，操作日志还提供有关不合规设备的信息。

有关此功能的详细信息，请参阅[在 Intune 中将日志数据发送到存储、事件中心或日志分析](review-logs-using-azure-monitor.md)。

#### <a name="route-logs-to-azure-monitor-in-more-intune-workloads---3804627---"></a>在更多 Intune 工作负载中，将日志路由到 Azure Monitor<!-- 3804627 -->
在 Intune 中，可以将审核和操作日志路由到 Azure Monitor 中的事件中心、存储和日志分析（依次选择“Intune” > “监视” > “诊断设置”）    。 在此更新中，可以路由更多 Intune 工作负载中的这些日志，包括合规性、配置、客户端应用等。

要了解有关将日志路由到 Azure Monitor 的详细信息，请参阅[将日志数据发送到存储、事件中心或日志分析](review-logs-using-azure-monitor.md)。

#### <a name="create-and-use-mobility-extensions-on-android-zebra-devices-in-intune---3305880-----"></a>使用 Android Zebra 设备在 Intune 中创建和使用移动扩展<!-- 3305880   -->
在此更新中，Intune 支持配置 Android Zebra 设备。 具体来说，可以创建设备配置文件，并使用 StageNow 生成的移动扩展 (MX) 配置文件将设置应用于 Android Zebra 设备（依次选择“设备配置” > “配置文件” > “创建配置文件” >  针对平台选择“Android”> 针对配置文件类型选择“MX 配置文件(仅限 Zebra)”）      。

有关此功能的详细信息，请参阅[通过 Intune 中的移动扩展使用和管理 Zebra 设备](../configuration/android-zebra-mx-overview.md)。

适用于：Android

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>设备管理
#### <a name="encryption-report-for-windows-10-devices-in-public-preview---2351538---"></a>Windows 10 设备的加密报表（公共预览版）<!-- 2351538 -->
使用新的[加密报表（预览版）](../protect/encryption-monitor.md)查看关于 Windows 10 设备加密状态的详细信息。 可用的详细信息包括设备 TPM 版本、加密准备和状态、错误报告等。  

#### <a name="access-bitlocker-recovery-keys-from-the-intune-portal-in-public-preview---2351547-----"></a>从 Intune 门户访问 BitLocker 恢复密钥（公共预览版）<!-- 2351547   -->
现在可以使用 Intune 从 Azure Active Directory 查看有关 BitLocker 密钥 ID 和 BitLocker 恢复密钥的[详细信息](../protect/encryption-monitor.md)。

#### <a name="microsoft-edge-support-for-intune-scenarios-on-ios-and-android-devices---3411007---"></a>Microsoft Edge 支持 iOS 和 Android 设备上的 Intune 方案<!-- 3411007 -->
Microsoft Edge 支持与 Intune Managed Browser 相同的所有管理方案，并新增了对最终用户体验的改进。 Intune 策略启用的 Microsoft Edge 企业功能包括双重标识、应用保护策略集成、Azure 应用程序代理集成、托管收藏夹和主页快捷方式。 有关详细信息，请参阅 [Microsoft Edge 支持](../apps/app-configuration-managed-browser.md#microsoft-edge-support)。

#### <a name="exchange-onlineintune-connector-deprecate-support-for-eas-only-devices--3105122----"></a>Exchange Online/Intune 连接器不再支持只有 EAS 的设备<!--3105122  -->
Intune 控制台不再支持查看和管理使用 Intune 连接器连接到 Exchange Online 的只有 EAS 的设备。 但你有以下选项：
- 在移动设备管理 (MDM) 中注册设备
- 使用 Intune 应用保护策略管理设备
- 使用 [Exchange Online 中的客户端和移动设备](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/clients-and-mobile-in-exchange-online)中所述的 Exchange 控件

#### <a name="search-the-all-devices-page-for-an-exact-device-by-using-name--4254930---"></a>使用[名称]在“所有设备”页中精确搜索设备<!--4254930 -->
现在可以精确搜索的设备名。 转到“Intune” > “设备” > “所有设备”> 在搜索框中，使用 {} 将设备名括起来，以精确搜索匹配项    。 例如，{Device12345}  。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>监视和故障排除

#### <a name="support-for-additional-connectors-on-the-tenant-status-page---3617202----"></a>支持“租户状态”页上的其他连接器<!-- 3617202  -->
[“租户状态”页](tenant-status.md)现可显示其他连接器的状态信息，包括 Windows Defender 高级威胁防护 (ATP) 和其他 Mobile Threat Defense 连接器  。

#### <a name="support-for-the-power-bi-compliance-app-from-the-data-warehouse-blade-in-microsoft-intune---4260871---"></a>Microsoft Intune 中的“数据仓库”边栏选项卡中对 Power BI 合规性应用的支持<!-- 4260871 -->
以前，“Intune 数据仓库”边栏选项卡中的“下载 Power BI 文件”链接会下载 Intune 数据仓库报表（.pbix 文件）   。 此报表已替换为 Power BI 合规性应用。 Power BI 合规性应用无需特殊加载或设置。 它将直接在 Power BI 在线门户中打开，并根据凭据专门向 Intune 租户显示数据。 在 Intune 中，选择“Intune”边栏选项卡右侧的“设置 Intune 数据仓库”链接  。 然后，单击“获取 Power BI 应用”  。 有关详细信息，请参阅[使用 Power BI 连接到数据仓库](../developer/reports-proc-get-a-link-powerbi.md)。


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>基于角色的访问控制

#### <a name="granting-intune-read-only-access-to-some-azure-active-directory-roles---3637917----"></a>向某些 Azure Active Directory 角色授予 Intune 只读访问权限<!-- 3637917  -->
已向以下 Azure AD 角色授予 Intune 只读访问权限。 通过 Azure AD 角色授予的权限取代了通过 Intune 基于角色的访问控制 (RBAC) 授予的权限。

对 Intune 审核数据的只读访问权限：

- 合规性管理员
- 符合性数据管理员

对所有 Intune 数据的只读访问权限：

- 安全管理员
- 安全操作员
- 安全读取者

有关详细信息，请参阅[基于角色的访问控制](role-based-access-control.md)。

#### <a name="scope-tags-for-ios-app-provisioning-profiles--2934430-----"></a>iOS 应用预配配置文件的范围标记<!--2934430   -->
可以向 iOS 应用预配配置文件添加范围标记，以便只有具有特定角色（该角色也分配有该作用域标记）的人员才能够访问 iOS 应用预配配置文件。 有关详细信息，请参阅[使用 RBAC 和范围标记](scope-tags.md)。

#### <a name="scope-tags-for-app-configuration-policies--2371891-----"></a>应用配置策略的范围标记<!--2371891   -->
可以向应用配置策略添加范围标记，以便只有具有特定角色（该角色也分配有该作用域标记）的人员才能够访问应用配置策略。 应用配置策略仅针对或关联到分配有相同范围标记的应用。 有关详细信息，请参阅[使用 RBAC 和范围标记](scope-tags.md)。

#### <a name="microsoft-edge-support-for-intune-scenarios-on-ios-and-android-devices---3411007---"></a>Microsoft Edge 支持 iOS 和 Android 设备上的 Intune 方案<!-- 3411007 -->
Microsoft Edge 将增加对最终用户体验的改进，支持与 Intune 托管浏览器相同的所有管理方案。 Intune 策略启用的 Microsoft Edge 企业功能包括双重标识、应用保护策略集成、Azure 应用程序代理集成、托管收藏夹和主页快捷方式。 有关详细信息，请参阅 [Microsoft Edge 支持](../apps/app-configuration-managed-browser.md#microsoft-edge-support)。




<!-- ########################## -->
## <a name="february-2019"></a>2019 年 2 月

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>应用管理
#### <a name="intune-macos-company-portal-dark-mode---3300524----"></a>Intune macOS 公司门户深色模式<!-- 3300524  -->
Intune macOS 公司门户现在支持 macOS 的深色模式。 在 macOS 10.14+ 设备上启用深色模式时，公司门户将调整其外观以反映该模式的颜色。

#### <a name="intune-will-leverage-google-play-protect-apis-on-android-devices---2577355-----"></a>Intune 将在 Android 设备上使用 Google Play Protect API<!-- 2577355   -->
某些 IT 管理员面临着 BYOD 情况，最终用户可能会使他们的手机获取 root 权限或越狱。 此行为虽然有时并非恶意，但会导致绕过许多 Intune 策略，这些策略是为了保护组织在最终用户设备上的数据而设置的。 因此，Intune 为已注册和未注册的设备提供 root 权限和越狱检测。 在此版本中，Intune 现在将利用 Google Play Protect API 添加到我们对未注册设备的现有 root 权限检测检查。 虽然 Google 不会共享发生的所有 root 权限检测检查，但我们预期这些 API 能够检测出因设备自定义而导致设备获取 root 权限的用户，以及能够在旧设备上获得较新 OS 更新的用户。 然后，可以阻止这些用户访问公司数据，或者可以从其启用策略的应用中删除其公司帐户。 为了获得额外价值，IT 管理员现在将在 Intune 应用保护边栏选项卡中进行多次报告更新 -“已标记的用户”报告将显示通过 Google Play Protect 的 SafetyNet API 扫描检测到的用户，“潜在有害应用”报告将显示通过 Google 的 Verify Apps API 扫描检测到的应用。 此功能在 Android 中可用。

#### <a name="win32-app-information-available-in-troubleshooting-blade---2617342-----"></a>“故障排除”边栏选项卡显示 Win32 应用信息<!-- 2617342   -->
现在可以从 Intune 应用“排除故障”边栏选项卡收集 Win32 应用安装的失败日志文件  。 有关应用安装排除故障的详细信息，请参阅[排查应用安装问题](./../apps/troubleshoot-app-install.md)和[排查 Win32 应用问题](./../apps/troubleshoot-app-install.md#win32-app-installation-troubleshooting)。

#### <a name="app-status-details-for-ios-apps---3761235-----"></a>iOS 应用的应用状态详细信息<!-- 3761235   -->
将出现与以下内容相关的新应用安装错误消息：
- 在共享 iPad 上安装 VPP 应用失败
- 禁用 App Store 失败
- 未能找到应用的 VPP 许可证
- 无法使用 MDM 提供程序安装系统应用
- 设备处于丢失模式或展台模式时无法安装应用
- 用户未登录 App Store 时无法安装应用

在 Intune 中，选择“客户端应用” > “应用”>“应用名称”>“设备安装状态”    。 “状态详细信息”列中将提供新的错误消息  。

#### <a name="new-app-categories-screen-in-the-company-portal-app-for-windows-10---3834780----"></a>适用于 Windows 10 的公司门户应用中的全新应用类别屏幕<!-- 3834780  -->
添加了名为“应用类别”的新屏幕，以改善适用于 Windows 10 的公司门户中的应用浏览和选择体验  。 用户现在可以看到他们的应用按照“特别推荐”、“教育”和“工作效率”等类别进行排序    。 此更改将出现在公司门户 10.3.3451.0 版及更高版本中。 要查看新屏幕，请参阅[应用 UI 中的新增功能](whats-new-app-ui.md)。 有关公司门户中应用的详细信息，请参阅[在设备上安装和共享应用](https://docs.microsoft.com/user-help/install-apps-cpapp-windows)。  

#### <a name="power-bi-compliance-app---1455231-doc-work-item---"></a>Power BI 合规性应用<!-- 1455231 doc-work-item -->
使用 [Intune 合规性（数据仓库）](https://aka.ms/intune/datawarehouseapi/getpowerbiapp)应用访问 Power BI Online 中的 Intune 数据仓库。 使用此 Power BI 应用，可立即访问和共享预创建的报表，无需任何设置，也无需离开 Web 浏览器。 有关详细信息，请参阅[更改日志 - Power BI 合规性应用](../developer/reports-changelog.md#power-bi-compliance-app)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>设备配置

#### <a name="powershell-scripts-can-run-in-a-64-bit-host-on-64-bit-devices---1862675-----"></a>PowerShell 脚本可以在 64 位设备上的 64 位主机上运行<!-- 1862675   -->
将 PowerShell 脚本添加到设备配置概要文件时，该脚本始终以 32 位执行，即使在 64 位操作系统上也是如此。 通过此更新，管理员可以在 64 位设备上的 64 位 PowerShell 主机中运行该脚本（“设备配置” > “PowerShell 脚本” > “添加” > “配置” > “在 64 位 PowerShell 主机中运行脚本”）      。

有关使用 PowerShell 的更多详细信息，请参阅 [Intune 中的 PowerShell 脚本](../apps/intune-management-extension.md)。

适用于：Windows 10 及更高版本

#### <a name="macos-users-are-prompted-to-update-their-password---1873216---"></a>系统会提示 macOS 用户更新密码<!-- 1873216 -->
Intune 会在 macOS 设备上强制实施 ChangeAtNextAuth 设置  。 此设置会影响具有合规性密码策略或设备限制密码配置文件的最终用户和设备。 系统会提示一次最终用户更新其密码。 每当用户首次运行需要身份验证的任务（例如，登录设备）时，就会出现此提示。 在执行需要管理权限的任何操作（例如，请求密钥链访问权限）时，系统也会提示用户更新密码。

管理员更改任何新的或现有的密码策略时，系统会再次提示最终用户更新密码。

适用于：  
macOS

#### <a name="assign-scep-certificates-to-a-userless-macos-device---2340521------"></a>将 SCEP 证书分配给无用户的 macOS 设备<!-- 2340521    -->
可以使用设备属性将简单证书注册协议 (SCEP) 证书分配给 macOS 设备（包括没有用户关联的设备），并将证书配置文件与 Wi-Fi 或 VPN 配置文件相关联。 此操作扩展了现有的支持，可向[运行 Windows、iOS 和 Android 的具有和没有用户关联的设备分配 SCEP 证书](../protect/certificates-profile-scep.md)。  此更新添加了一个选项，可在配置 macOS 的 SCEP 证书配置文件时，选择设备的证书类型  。

适用于：
- macOS

#### <a name="intune-conditional-access-ui-update---2432313-----"></a>Intune 条件访问 UI 更新<!-- 2432313   -->
我们已对 Intune 控制台中条件访问的 UI 进行了改进。 其中包括:
- 使用 Azure Active Directory 中的边栏选项卡替换了 Intune“条件访问”边栏选项卡  。 这将确保可在 Intune 控制台中访问[条件访问](../protect/conditional-access.md)的所有设置和配置，这仍是 Azure AD 技术。 
- 我们已将“本地访问”边栏选项卡重命名为“Exchange 访问”，并将 Exchange 服务连接器设置重定位到此重命名的边栏选项卡    。  此更改合并了[配置和监视与 Exchange Online 和 Exchange 本地相关的详细信息](../protect/exchange-connector-install.md)的位置。  

#### <a name="kiosk-browser-and-microsoft-edge-browser-apps-can-run-on-windows-10-devices-in-kiosk-mode---2935135-----"></a>展台浏览器和 Microsoft Edge 浏览器应用能够在 Windows 10 设备上以展台模式运行<!-- 2935135   -->
可以在展台模式下使用 Windows 10 设备运行一个应用或多个应用。 此更新包括在展台模式下使用浏览器应用的若干更改，包括：

- 添加 Microsoft Edge 浏览器或 Kiosk Browser 以在展台设备上作为应用程序运行（“设备配置” > “配置文件” > “新配置文件” > “Windows 10 及更高版本”（针对平台）>“展台”（针对配置文件类型））      。
- 可以允许或限制新的功能和设置（依次选择“设备配置” > “配置文件” > “新配置文件” >  针对平台选择“Windows 10 和更高版本”> 针对配置文件类型选择“设备限制”），包括      ：

- Microsoft Edge 浏览器：
  - 使用 Microsoft Edge 展台模式
  - 空闲时间后刷新浏览器

- 收藏夹和搜索：
  - 允许更改搜索引擎

有关这些设置的列表，请参阅：

- [将 Windows 10 及更高版本设备设置为以展台形式运行
](../configuration/kiosk-settings-windows.md)
- [Microsoft Edge 浏览器的设备限制](../configuration/device-restrictions-windows-10.md#microsoft-edge-browser)
- [收藏夹和搜索设备限制](../configuration/device-restrictions-windows-10.md#favorites-and-search)

适用于：Windows 10 及更高版本

#### <a name="new-device-restriction-settings-for-ios-and-macos-devices---3448774-----"></a>适用于 iOS 和 macOS 设备的新设备限制设置<!-- 3448774   -->
你可以在运行 iOS 和 macOS 的设备上限制某些设置和功能（“设备配置” > “配置文件” > “新配置文件” > “iOS”或“macOS”（针对平台）>“设备限制”（针对配置文件类型））       。 此更新添加了可以控制的更多功能和设置，包括在 iOS 设备上设置屏幕时间、更改 eSIM 设置更改和蜂窝计划等。 此外，还包括在 macOS 设备上延迟用户见到软件更新的时间和阻止内容缓存。

要查看可以限制的功能和设置，请参阅：

- [iOS 设备限制设置](../configuration/device-restrictions-ios.md)
- [macOS 设备限制设置](../configuration/device-restrictions-macos.md)

适用于：

- iOS
- macOS

#### <a name="kiosk-devices-are-now-called-dedicated-devices-on-android-enterprise-devices---3598402-----"></a>在 Android Enterprise 设备上，“展台”设备现在称为“专用设备”<!-- 3598402   -->
为了与 Android 术语保持一致，“展台”将更改为适用于 Android Enterprise 设备的“专用设备”（依次选择“设备配置” > “配置文件” > “创建配置文件”> 针对平台选择“Android Enterprise”>“仅限设备所有者” > “设备限制” > “专用设备”）         。

要查看可用设置，请转到[允许或限制功能的设备设置](../configuration/device-restrictions-android-for-work.md#dedicated-device-settings)。

适用于：  
Android Enterprise

#### <a name="safari-and-delaying-user-software-update-visibility-ios-settings-are-moving-in-the-intune-ui---3640850-3803313-----"></a>Safari 和“延迟用户软件更新可见性”iOS 设置将移至 Intune UI<!-- 3640850, 3803313   -->
对于 iOS 设备，可以设置 Safari 设置并配置软件更新。 在此更新中，这些设置将移至 Intune UI 的不同部分：

- Safari 设置已从“Safari”（“设备配置” > “配置文件” > “新配置文件” > “iOS”（针对平台）>“设备限制”（针对配置文件类型））移动到[内置应用](../configuration/device-restrictions-ios.md#built-in-apps)        。
- 受监督的 iOS 设备的“延迟用户软件更新可见性”设置（“软件更新” > “iOS 的更新策略”）将移至“设备限制” > [常规](../configuration/device-restrictions-ios.md#general)      。  有关对现有策略的影响的详细信息，请参阅 [iOS 软件更新](../protect/software-updates-ios.md#configure-the-policy)。

有关设置列表，请参阅：

- [iOS 设备限制](../configuration/device-restrictions-ios.md) 
- [iOS 软件更新](../protect/software-updates-ios.md)

此功能适用于：

- iOS

#### <a name="enabling-restrictions-in-the-device-settings-is-renamed-to-screen-time-on-ios-devices---3699164-----"></a>在 iOS 设备上将设备设置中的启用限制重命名为屏幕时间<!-- 3699164   -->
可以在受监管的 iOS 设备上配置“设备设置中的启用限制”（“设备配置” > “配置文件” > “新配置文件” > “iOS”（针对平台）>“设备限制”（针对配置文件类型）>“常规”）        。 在此更新中，此设置将重命名为“屏幕时间(仅监管模式)”  。

操作是相同的。 具体而言：

- iOS 11.4.1 及更早版本：“阻止”阻止最终用户在设备设置中设置自己的限制  。 
- iOS 12.0 及更高版本：“阻止”阻止最终用户在设备设置中设置自己的“屏幕时间”，包括内容和隐私限制   。 升级到 iOS 12.0 的设备将不再在设备设置中看到限制选项卡。 这些设置位于“屏幕时间”  。 

有关设置列表，请参阅 [iOS 设备限制](../configuration/device-restrictions-ios.md#general)。

适用于：
- iOS


#### <a name="intune-powershell-module---951068----"></a>Intune PowerShell 模块<!-- 951068  -->
现在，[Microsoft PowerShell 库](https://www.powershellgallery.com/packages/Microsoft.Graph.Intune/6.1902.1.10)中提供了 Intune PowerShell 模块，该模块可通过 Microsoft Graph 提供对 Intune API 的支持。

- [有关如何使用此模块的详细信息](https://github.com/Microsoft/Intune-PowerShell-SDK/blob/master/README.md)
- [使用此模块的方案示例](https://github.com/Microsoft/Intune-PowerShell-SDK/blob/master/Samples/README.md)

#### <a name="improved-support-for-delivery-optimization--3183757----"></a>改进了对传递优化的支持<!--3183757  -->
我们扩展了 Intune 中对配置传递优化的支持。 现在可以配置[传递优化设置](../configuration/delivery-optimization-settings.md)的扩展列表，并直接从 Intune 控制台将其定向到设备。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>设备管理

#### <a name="rename-an-enrolled-windows-device---1911112----"></a>重命名已注册的 Windows 设备<!-- 1911112  -->
现在可以重命名已注册的 Windows 10 设备（RS4 或更高版本）。 若要执行此操作，请选择“Intune” > “设备” > “所有设备”> 选择设备 >“重命名设备”     。 此功能当前不支持重命名混合 Azure AD Windows 设备。

#### <a name="auto-assign-scope-tags-to-resources-created-by-an-admin-with-that-scope---3173823----"></a>将范围标记自动分配给具有该范围的管理员创建的资源<!-- 3173823  -->
管理员创建资源时，分配给管理员的任何范围标记都将自动分配给这些新资源。

### <a name="monitor-and-troubleshoot"></a>监视和故障排除

#### <a name="failed-enrollment-report-moves-to-the-device-enrollment-blade---3560202----"></a>“失败注册”报表将移至“设备注册”边栏选项卡<!-- 3560202  -->
“失败注册”报表已迁移到“设备注册”边栏选项卡的“监视”部分    。 已添加两个新列（“注册方法”和“OS 版本”）。

#### <a name="company-portal-abandonment-report-renamed-to-incomplete-user-enrollments--3815076-eemiss---"></a>“公司门户放弃报表”已重命名为“部分用户注册”<!--3815076 eemiss -->
“公司门户放弃报表”已重命名为“部分用户注册”   。






<!-- ########################## -->
## <a name="january-2019"></a>2019 年 1 月

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>应用管理

#### <a name="intune-app-pin---2298397---"></a>Intune 应用 PIN<!-- 2298397 -->
作为 IT 管理员，你现在可以配置在最终用户必须更改其 Intune 应用 PIN 之前可以等待的天数。 新设置是在该等待天数之后重置的 PIN，同时，通过选择“Intune”“客户端应用” > “应用保护策略” > “创建策略” > “设置” > “访问要求” > ，便会在 Azure 门户中提供新设置        。 可用于 [iOS](../apps/app-protection-policy-settings-ios.md) 和 [Android](../apps/app-protection-policy-settings-android.md) 设备，此功能支持正整数。

#### <a name="intune-device-reporting-fields---2748738---"></a>Intune 设备报告字段<!-- 2748738 -->
Intune 提供其他设备报告字段，包括 Android 注册 ID、Android 制造商、模型和安全修补程序版本以及 iOS 型号。 在 Intune 中，通过选择“客户端应用” > “应用保护状态”并选择“应用保护报告: iOS、Android”来获取这些字段    。 此外，这些参数将帮助你配置设备制造商“允许”  列表 (Android)、设备型号的“允许”  列表（Android 和 iOS）和最低 Android 安全修补程序版本设置。

#### <a name="toast-notifications-for-win32-apps---3136566-----"></a>Win32 应用的 Toast 通知<!-- 3136566   -->
可以取消显示每个应用分配的最终用户 Toast 通知。 在 Intune 中，依次选择“客户端应用”   > “应用”  > 应用 >“分配”   > “包括组”  。

#### <a name="intune-app-protection-policies-ui-update---3251427----"></a>Intune 应用保护策略用户界面更新<!-- 3251427  -->
我们已更改 Intune 应用保护的设置和按钮的标签，以使用户更容易理解每个选项。 一些更改包括：  
- 控件从“是” / “否”控件更改为主要“阻止” / “允许”和“禁用” / “启用”控件       。 标签也会更新。  
- 将对设置重新设置格式，以在控件中并排显示设置及其标签，从而提供更好的浏览。

默认设置和设置数目将保持不变，但此更改可使用户更轻松地了解、浏览以及利用设置，以应用所选的应用保护策略。 有关信息，请参阅 [iOS 设置](../apps/app-protection-policy-settings-ios.md)和 [Android 设置](../apps/app-protection-policy-settings-android.md)。

#### <a name="additional-settings-for-outlook---3301182----"></a>Outlook 的其他设置<!-- 3301182  -->
现在可以使用 Intune 为 iOS 和 Android 配置 Outlook 以下其他设置：

- 仅允许在 iOS 和 Android 的 Outlook 中使用工作或学校帐户
- 部署适用于 Office 365 和混合新式身份验证本地帐户的新式身份验证
- 选择基本身份验证时，请使用 `SAMAccountName` 作为电子邮件配置文件中的用户名字段
- 允许保存联系人
- 配置外部收件人邮件提示
- 配置“重点收件箱” 
- 需要进行生物识别来访问适用于 iOS 的 Outlook
- 阻止外部图像

> [!NOTE]
> 如果使用 Intune 应用保护策略来管理公司标识的访问权限，则应考虑不启用“需要生物识别”  。 有关详细信息，请参阅 [iOS 访问设置](../apps/app-protection-policy-settings-ios.md#access-requirements)和 [Android 访问设置](../apps/app-protection-policy-settings-android.md#access-requirements)的“必须有公司凭据才能访问”  。

有关详细信息，请参阅 [Microsoft Outlook 配置设置](../apps/app-configuration-policies-outlook.md)。

#### <a name="delete-android-enterprise-apps---1352553---"></a>删除 Android Enterprise 应用<!-- 1352553 -->
可以从 Microsoft Intune 中删除托管 Google Play 应用。 若要删除托管 Google Play 应用，请在 Azure 门户中打开“Microsoft Intune”，并依次选择“客户端应用”   > “应用”  。 在应用列表中，选择托管 Google Play 应用右侧的省略号 (...)，再从随即显示的列表中选择“删除”  。 从应用列表删除托管的 Google Play 应用时，托管的 Google Play 应用会自动变为未批准状态。

#### <a name="managed-google-play-app-type---1352580---"></a>“托管 Google Play”应用类型<!-- 1352580 -->
“托管的 Google Play”应用类型让你可以专门将[托管的 Google Play 应用](https://play.google.com/work/search?q=microsoft&c=apps)添加到 Intune  。 作为 Intune 管理员，现在可以在 Intune 中浏览、搜索、批准、同步和分配已批准的托管 Google Play 应用。  不再需要单独转到托管 Google Play 控制台，也不再需要重新进行身份验证。  在 Intune 中，选择“客户端应用” > “应用” > “添加”    。 在“应用类型”列表中，将应用类型选择为“托管的 Google Play”   。

#### <a name="default-android-pin-keyboard---3802457---"></a>默认为 Android PIN 键盘<!-- 3802457 -->
对于在 Android 设备上使用“数字”PIN 类型设置 Intune 应用保护策略 (APP) PIN 的最终用户来说，他们将看到默认的 Android 键盘，而不是之前设计的固定 Android 键盘 UI。 在 Android 和 iOS 上使用默认键盘时，此更改对于“数字”和/或“密码”这两种 PIN 类型是一致的。 有关 Android 上最终用户访问设置的详细信息，如应用 PIN，请参阅 [Android 访问要求](../apps/app-protection-policy-settings-android.md#access-requirements)。


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>设备配置

#### <a name="administrative-templates-are-in-public-preview-and-moved-to-their-own-configuration-profile----3322847---"></a>管理模板为公共预览版，并移动到其自己的配置文件 <!-- 3322847 -->

Intune 中的管理模板（“设备配置”   >   “管理模板”）当前为公共预览版。 借助此更新：

- 管理模板包括大约 300 个可在 Intune 中托管的设置。 以前，这些设置仅存在于组策略编辑器中。
- 管理模板现已推出公共预览版。
- 管理模板从“设备配置” > “管理模板”移动到“设备配置” > “配置文件” > “创建配置文件”> 在“平台”中，选择“Windows 10 及更高版本” > 在“配置文件类型”中，选择“管理模板”。         
- 已启用报告

有关此功能的更多信息，请转到[用于配置组策略设置的 Windows 10 模板](../configuration/administrative-templates-windows.md)。

适用于：Windows 10 及更高版本

#### <a name="use-smime-to-encrypt-and-sign-multiple-devices-for-a-user---1333642---"></a>使用 S/MIME 对用户的多个设备进行加密和签名<!-- 1333642 -->
此更新包括使用新导入的证书配置文件进行 S/MIME 电子邮件加密（“设备配置” > “配置文件” > “创建配置文件”>“选择平台”>“PKCS 导入的证书”配置文件类型）     。 在 Intune 中，可以 PFX 格式导入证书。 然后 Intune 可以将这些相同的证书传递给单个用户注册的多个设备。 还包括：
- 原生 iOS 电子邮件配置文件支持使用 PFX 格式导入的证书启用 S/MIME 加密。
- Windows Phone 10 设备上的原生电子邮件应用自动使用 S/MIME 证书。
- 可以跨多个平台传递私有证书。 但并非所有电子邮件应用都支持 S/MIME。
- 在其他平台上，可能需要手动配置电子邮件应用以启用 S/MIME。  
- 支持 S/MIME 加密的电子邮件应用可能以 MDM 不支持的方式（例如从发布者的证书存储读取）处理对 S/MIME 电子邮件加密的证书检索。
有关此功能的详细信息，请参阅[对电子邮件进行签名和加密的 S/MIME 概述](../protect/certificates-s-mime-encryption-sign.md)。
在以下设备上受支持：Windows、Windows Phone 10、macOS、iOS、Android

#### <a name="new-options-to-automatically-connect-and-persist-rules-when-using-dns-settings-on-windows-10-and-later-devices---1333665-2999078---"></a>在 Windows 10 及更高版本设备上使用 DNS 设置时自动连接并保留规则的新选项<!-- 1333665, 2999078 -->
在 Windows 10 及更高版本设备上，可以创建包含 DNS 服务器列表的 VPN 配置文件来解析域，如 contoso.com。 这一升级包括名称解析的新设置（“设备配置” > “配置文件” > “创建配置文件”> 选择“Windows 10 及更高版本”作为平台 > 选择“VPN”作为配置文件类型 >“DNS 设置” >“添加”）        ： 
- **自动连接**：如果为“已启用”  ，则当设备与所输入的域（如 contoso.com）通信时，会自动连接到 VPN。
- **永久性**：默认情况下，只要使用此 VPN 配置文件连接设备，所有名称解析策略表 (NRPT) 规则就会处于活动状态。 当 NRPT 规则的此设置为  “已启用”时，该规则将在设备上保持活动状态，即使 VPN 断开连接也是如此。 该规则会保持活动状态，直到删除 VPN 配置文件或手动删除该规则，删除操作可以使用 PowerShell 完成。
[Windows 10 VPN 设置](../configuration/vpn-settings-windows-10.md)介绍了设置。

#### <a name="use-trusted-network-detection-for-vpn-profiles-on-windows-10-devices---1500165---"></a>在 Windows 10 设备上使用 VPN 配置文件的受信任网络检测<!-- 1500165 -->
使用受信任的网络检测时，可以在用户已使用受信任的网络时阻止 VPN 配置文件自动创建 VPN 连接。 通过此更新，可以添加 DNS 后缀，以便在运行 Windows 10 及更高版本的设备上启用受信任的网络检测（“设备配置” > “配置文件” > “创建配置文件” > “Windows 10 及更高版本”作为平台 >“VPN”作为配置文件类型）      。
[Windows 10 VPN 设置](../configuration/vpn-settings-windows-10.md)列出了当前的 VPN 设置。

#### <a name="manage-windows-holographic-for-business-devices-used-by-multiple-users---1907917-1063203---"></a>管理多个用户使用的 Windows Holographic for Business 设备<!-- 1907917, 1063203 -->
目前，你可以在使用自定义 OMA-URI 设置的 Windows 10 和 Windows Holographic for Business 设备上配置共享电脑设置。 通过此更新，会添加新的配置文件以配置共享设备设置（“设备配置” > “配置文件” > “创建配置文件” > “Windows 10 及更高版本” > “共享多用户设备”）      。
若要了解关于此功能的更多信息，请转到[用于托管共享设备的 Intune 设置](../configuration/shared-user-device-settings.md)。
适用于：Windows 10 及更高版本、Windows Holographic for Business

#### <a name="new-windows-10-update-settings--2626030--2512994----"></a>新的 Windows 10 更新设置<!--2626030  2512994  -->
对于 [Windows 10 更新通道](../protect/windows-update-for-business-configure.md)，可以配置：
- **自动更新行为** - 使用新选项“重置为默认值”，在运行“2018 年 10 月更新”的 Windows 10 计算机上还原初始的自动更新设置  
- **阻止用户暂停 Windows 更新** - 配置新的软件更新设置，使你能够阻止或允许用户通过其计算机的“设置”暂停更新安装  。

#### <a name="ios-email-profiles-can-use-smime-signing-and-encryption---2662949---"></a>iOS 电子邮件配置文件可以使用 S/MIME 签名和加密<!-- 2662949 -->
你可以创建包含不同设置的电子邮件配置文件。 此更新包括可用于在 iOS 设备上对电子邮件通信进行签名和加密的 S/MIME 设置（“设备配置” > “配置文件” > “创建配置文件”> 选择“iOS”作为平台 >“电子邮件”作为配置文件类型）      。
[iOS 电子邮件配置设置](../configuration/email-settings-ios.md)列出了设置。

#### <a name="some-bitlocker-settings-support-windows-10-pro-edition---2727036---"></a>某些 BitLocker 设置支持 Windows 10 专业版<!-- 2727036 -->
你可以创建在 Windows 10 设备上设置 Endpoint Protection 设置的配置文件，包括 BitLocker。 此更新会为某些 BitLocker 设置添加对 Windows 10 专业版的支持。
若要查看这些保护设置，请转到[适用于 Windows 10 的 Endpoint protection 设置](../protect/endpoint-protection-windows-10.md#windows-encryption)。

#### <a name="shared-device-configuration-is-renamed-to-lock-screen-message-for-ios-devices-in-the-azure-portal---2809362---"></a>Azure 门户中的共享设备配置将重命名为适用于 iOS 设备的“锁屏消息”<!-- 2809362 -->
创建适用于 iOS 设备的配置文件时，你可以添加“共享设备配置”设置以在锁屏上显示特定文本  。 此更新包括以下更改： 
- Azure 门户中的“共享设备配置”  设置将重命名为“锁定屏幕消息(仅限受监督的设备)”（“设备配置”   > “配置文件”   > “创建配置文件”  > 选择“iOS”  作为平台 > 选择“设备功能”  作为配置文件类型 >“锁定屏幕消息”  ）。
- 添加锁屏消息时，可以插入序列号、设备名称或另一个特定于设备的值作为“资产标记信息”和“锁屏脚注”中的变量   。 例如，可以使用大括号输入 `Device name: {{devicename}}` 或 `Serial number is {{serialnumber}}`。 [iOS 令牌](../apps/app-configuration-policies-use-ios.md#tokens-used-in-the-property-list)列出了可用的令牌。
[用于在锁屏上显示消息的设置](../configuration/ios-device-features-settings.md#lock-screen-message)列出了设置。

#### <a name="new-app-store-doc-viewing-gaming-device-restriction-settings-added-to-ios-devices---2827760--"></a>添加到 iOS 设备的新 App Store、文档查看和游戏设备限制设置<!-- 2827760-->
在“设备配置” > “配置文件” > “创建配置文件” > 平台选择“iOS”> 配置文件类型选择“设备限制”>“App Store、文档查看和游戏”中，添加了以下设置       ：允许托管应用将联系人写入非托管联系人帐户。允许非托管应用从托管联系人帐户中读取联系人。要查看这些设置，请转到 [iOS 设备限制](../configuration/device-restrictions-ios.md#app-store-doc-viewing-gaming)。

#### <a name="new-notification-hints-and-keyguard-settings-to-android-enterprise-device-owner-devices---3201839-3201843---"></a>Android Enterprise 设备所有者设备的新通知、提示和锁屏设置<!-- 3201839 3201843 -->
以设备所有者身份运行时，此更新包括 Android Enterprise 设备上的多项新功能。 若要使用这些功能，请转到“设备配置”   > “配置文件”   > “创建配置文件”  > 在“平台”  中，选择“Android Enterprise”  > 在“配置文件类型”  中，选择“仅设备所有者”   > “设备限制”  。

新的功能包括：

- 禁止显示系统通知，包括传入呼叫、系统警报、系统错误等。
- 建议跳过首次打开的应用的启动教程和提示。
- 禁用高级锁屏设置，例如照相机、通知、指纹解锁等。

若要查看这些设置，请转到 [Android Enterprise 设备限制设置](../configuration/device-restrictions-android-for-work.md)。

#### <a name="android-enterprise-device-owner-devices-can-use-always-on-vpn-connections---3202194---"></a>Android Enterprise 设备所有者设备可以使用 Always On VPN 连接<!-- 3202194 -->
在此更新中，可以在 Android Enterprise 设备所有者设备上使用 Always-on VPN 连接。 Always-on VPN 连接一直保持连接状态
，或在用户解锁设备、设备重启或无线网络更改时立即重新连接。 还可以将连接置于“锁定”模式，该模式会阻止所有网络流量，直到 VPN 连接处于活动状态。
可以在“设备配置” > “配置文件” > “创建配置文件” >  适用于平台的“Android 企业版”>“仅设备所有者”的“设备限制”>“连接”设置中启用 Always-on VPN       。 若要查看这些设置，请转到 [Android Enterprise 设备限制设置](../configuration/device-restrictions-android-for-work.md)。

#### <a name="new-setting-to-end-processes-in-task-manager-on-windows-10-devices---3285177---"></a>Windows 10 设备上的任务管理器中的结束进程的新设置<!-- 3285177 --> 
此更新包括使用 Windows 10 设备上的任务管理器来结束进程的新设置。 使用设备配置文件（“设备配置”   > “配置文件”   > “创建配置文件”  > 在  “平台”中，选择“Windows 10”  > 在  “配置文件类型”中，选择“设备限制”   >   “常规”设置），选择允许或阻止此设置。
若要查看这些设置，请转到 [Windows 10 设备限制设置](../configuration/device-restrictions-windows-10.md)。
适用于：Windows 10 及更高版本

#### <a name="use-microsoft-recommended-settings-with-security-baselines-public-preview---2055484-----"></a>结合使用 Microsoft 建议设置与安全基线（公共预览版）<!-- 2055484   -->

Intune 可与其他专注于安全性的服务集成，包括 Windows Defender ATP 和 Office 365 ATP。 客户要求能在各项 Microsoft 365 服务中采用通用策略和一组统一的端到端安全工作流。 我们的目标是实现策略一致，构建连接安全操作和常见管理员任务的解决方案。 在 Intune 中，我们旨在通过发布一组 Microsoft 推荐的“安全基线”（“Intune” > “安全基线”）来实现这一目标   。  管理员可以直接通过这些基线创建安全策略，再将它们部署到用户。 还可以自定义最佳做法建议，以满足组织需求。 Intune 可确保设备始终符合这些基线，并通知不符合的用户管理员或设备。

此功能存在于公共预览版，因此现在创建的任何配置文件都不会转移到通用 (GA) 的安全基线模板。 不应计划在生产环境中使用这些预览模板。

若要详细了解安全基线，请参阅[在 Intune 中创建 Windows 10 安全基线](../protect/security-baselines-monitor.md)。

此功能适用于：Windows 10 及更高版本

#### <a name="non-administrators-can-enable-bitlocker-on-windows-10-devices-joined-to-azure-ad---2147379-----"></a>非管理员可以在已加入 Azure AD 的 Windows 10 设备上启用 BitLocker<!-- 2147379   -->
在 Windows 10 设备上启用 BitLocker 设置时（“设备配置”   > “配置文件”   > “创建配置文件”   >   “Windows 10 及更高版本”作为平台 >  “Endpoint protection”作为配置文件类型 >“Windows 加密”  ），将添加 BitLocker 设置。

此更新包括新的 BitLocker 设置，以允许标准用户（非管理员）启用加密。

若要查看设置，请转到[适用于 Windows 10 的 Endpoint Protection 设置](../protect/endpoint-protection-windows-10.md#windows-encryption)。

#### <a name="check-for-configuration-manager-compliance---2192052--eepublished----"></a>检查 Configuration Manager 合规性<!-- 2192052  eepublished  -->
此更新包括新的 Configuration Manager 符合性设置（“设备符合性” > “策略” > “创建策略” > “Windows 10 及更高版本” > “Configuration Manager 符合性”）      。 Configuration Manager 向 Intune 符合性发送信号。 使用此设置，可以要求所有 Configuration Manager 信号都返回“符合”。

例如，要求所有软件更新都安装在设备上。 在 Configuration Manager 中，此要求具有“已安装”状态。 如果设备上的任意计划处于未知状态，此设备在 Intune 中不符合要求。

[Configuration Manager 符合性](../protect/compliance-policy-create-windows.md#configuration-manager-compliance)介绍了此设置。

适用于：Windows 10 及更高版本

#### <a name="customize-wallpaper-on-supervised-ios-devices-using-a-device-configuration-profile---2809324-----"></a>使用设备配置配置文件在受监管的 iOS 设备上自定义壁纸<!-- 2809324   -->
为 iOS 设备创建设备配置文件时，可以自定义一些功能（“设置配置”   > “配置文件”   > “创建配置文件”   > “iOS”  （作为平台）>“设备功能”  （作为配置文件类型））。 此更新包括新的墙纸  设置，可便于管理员在主屏幕或锁定屏幕上使用 .png、.jpg 或 .jpeg 格式图像。 这些壁纸设置仅适用于受监督的设备。 

有关这些设置的列表，请参阅 [iOS 设备功能设置](../configuration/ios-device-features-settings.md)。

#### <a name="windows-10-kiosk-is-generally-available---3594661----"></a>Windows 10 展台已全面推出<!-- 3594661  -->
在此更新中，Windows 10 及更高版本设备上的展台功能已全面推出（正式版）。 若要查看可以添加和配置的所有设置，请参阅[适用于 Windows 10（及更高版本）的展台设置](../configuration/kiosk-settings.md)。

#### <a name="contact-sharing-via-bluetooth-is-removed-in-device-restrictions--device-owner-for-android-enterprise---3598396-----"></a>在“设备限制”>“Android Enterprise 的设备所有者”中删除“通过蓝牙共享联系人”<!-- 3598396   -->
在创建 Android Enterprise 设备的设备限制配置文件时，会有一个“通过蓝牙共享联系人”设置  。 在此更新中，“通过蓝牙共享联系人”  设置遭删除（“设备配置”   > “配置文件”   > “创建配置文件”   > “Android Enterprise”  （作为平台）>“设备限制”  >“设备所有者”（作为配置文件类型）>“常规”  ）。

Android Enterprise 设备所有者管理不支持“通过蓝牙共享联系人”设置  。 因此，在删除此设置时，即使在环境中启用并配置了此设置，此更改也不会影响任何设备或租户。

要查看设置的当前列表，请转到[用于允许或限制功能的 Android Enterprise 设备设置](../configuration/device-restrictions-android-for-work.md)。

适用于：Android Enterprise 设备所有者


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>设备注册

#### <a name="more-detailed-enrollment-restriction-failure-messaging---3111564---"></a>更详细的注册限制失败消息<!-- 3111564 -->
不满足注册限制时，会收到更详细的错误消息。 若要查看这些消息，请转到“Intune”   > “故障排除”  > 并检查“注册故障”表。 有关详细信息，请参阅[注册失败列表](help-desk-operators.md#enrollment-failure-reference)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>设备管理
#### <a name="preview-of-support-for-android-corporate-owned-fully-managed-devices---1574342----"></a>对 Android 公司拥有的完全托管设备的支持（预览版）<!-- 1574342  -->
Intune 现支持完全托管的 Android 设备，这是公司拥有的“设备所有者”方案，其中设备由 IT 管理员严格管理并与各个用户关联。 这样，管理员便可以管理整个设备、强制扩展不可用于工作配置文件的策略控制的范围并限制用户仅从托管的 Google Play 安装应用。 有关详细信息，请参阅[设置 Android 完全托管的设备的 Intune 注册](../enrollment/android-fully-managed-enroll.md)和[注册专用设备或完全托管的设备](../enrollment/android-dedicated-devices-fully-managed-enroll.md)。  请注意，此功能处于预览状态。 Android 完全托管的用户设备目前无法使用部分 Intune 功能，例如证书、符合性以及条件访问。

#### <a name="selective-wipe-support-for-wip-without-enrollment-devices---1434452---"></a>对未注册的 WIP 设备的选择性擦除支持<!-- 1434452 -->
未注册的 Windows 信息保护 (WIP-WE) 允许客户保护其在 Windows 10 设备上的公司数据，而不需要完整的 MDM 注册。 使用 WIP-WE 策略保护文档后，Intune 管理员可以选择性擦除受保护的数据。 通过选择用户和设备，并发送擦除请求，所有通过 WIP-WE 策略保护的数据都将不可用。 从 Azure 门户中的 Intune，选择“移动应用” > “应用选择性擦除”   。


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>监视和故障排除

#### <a name="tenant-status-dashboard---1124854---"></a>租户状态仪表板<!-- 1124854 -->
新[租户状态页](tenant-status.md)会提供一个位置，可以在其中查看租户状态和相关详情。  该仪表板分为 4 个区域：
- **租户详细信息** - 显示租户姓名和位置、MDM 机构、租户中的注册设备总数以及许可证计数等信息。 此部分还为租户列出当前服务版本。
- **连接器状态** - 显示有关已配置的可用连接器的信息，还可以列出尚未启用的连接器。  
   根据每个连接器的当前状态，将其标记为“正常”、“警告”或“不正常”。 选择要了解的连接器，并查看其详细信息或为其配置其他信息。
- **Intune 服务运行状况** - 显示租户活动事件或服务中断情况的详细信息。 该部分信息直接检索自 Office 消息中心。
- **Intune 新闻** - 显示租户的活动信息。 消息包括在租户收到最新 Intune 功能时的通知等。  该部分信息直接检索自 Office 消息中心。

#### <a name="new-help-and-support-experience-in-company-portal-for-windows-10---1488939--"></a>适用于 Windows 10 的公司门户的新“帮助和支持”体验<!-- 1488939-->
新的公司门户“帮助和支持”页有助于用户针对应用和访问问题进行故障排除和请求帮助。 在新页面中，用户可以通过电子邮件发送错误和诊断日志的详细信息，并查找其组织的支持人员详细信息。 用户还可以查找常见问题解答部分，其中带有相关 Intune 文档的链接。

#### <a name="new-help-and-support-experience-for-intune---3307080---"></a>Intune 的新的“帮助和支持”体验<!-- #3307080 -->
我们将在未来几天向所有租户推出新的“帮助和支持”体验。 可以在 Intune 上进行此新体验，并且可以在使用 [Azure 门户](https://portal.azure.com/)中的“Intune”边栏选项卡时对其进行访问。
通过新体验，可以用自己的语言描述问题，并获得故障排除见解和基于 Web 的修复内容。 这些解决方案通过基于规则的机器学习算法提供并依赖于用户查询。
除特定于问题的指南之外，还会使用新的案例创建工作流，通过电子邮件或电话来打开支持案例。 此新体验取代了一组静态预选选项的先前的“帮助和支持”体验，这些选项基于打开“帮助和支持”时所在控制台的区域。
有关详细信息，请参阅[如何获取对 Microsoft Intune 的支持](get-support.md)。

#### <a name="new-operational-logs-and-ability-to-send-logs-to-azure-monitor-services---3762211----"></a>新推出运行日志，以及向 Azure Monitor 服务发送日志的功能<!-- 3762211  -->
Intune 有内置审核日志，可以在事件变更时跟踪事件。 此更新包含新日志功能，包括： 
- 运行日志（预览版）显示已注册用户和设备的详细信息，其中包括成功和失败尝试次数。
- 可将审核日志和运行日志发送到 Azure Monitor，包括存储帐户、事件中心和 Log Analytics。 借助这些服务，可以存储数据、使用分析工具（如 Splunk 和 QRadar），并能获取日志数据的可视化效果。

[使用 Intune 将日志数据发送到存储、事件中心或 Log Analytics](review-logs-using-azure-monitor.md) 详细介绍了此功能。

#### <a name="skip-more-setup-assistant-screens-on-an-ios-dep-device---2687509----"></a>在 iOS DEP 设备上跳过更多设置助理屏幕<!-- 2687509  -->
除了当前可以跳过的屏幕之外，还可以将 iOS DEP 设备设置为在用户注册设备时跳过设置助理中的以下屏幕：显示色调、隐私、Android 迁移、主页按钮、iMessage 和 FaceTime、载入、监视迁移、外观、屏幕时间、软件更新、SIM 安装程序。
若要选择要跳过的屏幕，请转到“设备注册”   > “Apple 注册”   > “注册计划令牌”  > 选择令牌 >“配置文件”  > 选择配置文件 >“属性”   > “设置助理的自定义项”  > 对于要跳过的任何屏幕选择“隐藏”  >“确定”  。
如果你新建或编辑配置文件，选定跳过屏幕需要与 Apple MDM 服务器同步。 用户可以发起手动同步设备，这样在选取配置文件变更时就不会有任何延迟。

#### <a name="android-enterprise-app-we-app-deployment---1171203---"></a>Android Enterprise APP-WE 应用部署<!-- 1171203 -->
对于没有注册 (APP-WE) 部署方案的未注册应用保护策略中的 Android 设备，现在可以使用托管的 Google Play 将应用商店应用和 LOB 应用部署到用户。 具体而言，可以向最终用户提供应用目录以及不再需要最终用户通过允许从未知源进行安装来放宽其设备的安全状况的安装体验。 此外，此部署方案将改进最终用户体验。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>基于角色的访问控制

#### <a name="scope-tags-for-apps---1081941---"></a>应用的作用域标记<!-- 1081941 -->
可创建作用域标记来限制对角色和应用的访问。 可向应用添加作用域标记，以便只有具有特定角色（该角色也分配有该作用域标记）的人员才可以访问该应用。 目前，无法向从托管 Google Play 添加到 Intune 的应用或使用 Apple Volume Purchase Program (VPP) 购买的应用分配作用域标记（但计划在将来提供此支持）。 有关详细信息，请参阅[使用作用域标记筛选策略](scope-tags.md)。




<!-- ########################## -->
## <a name="december-2018"></a>2018 年 12 月

### <a name="app-management"></a>应用管理

#### <a name="updates-for-application-transport-security---748318---"></a>针对应用传输安全进行更新<!-- 748318 -->

Microsoft Intune 支持传输层安全性 (TLS) 1.2+，以提供一流的加密，确保 Intune 在默认情况下更为安全，并与 Microsoft Office 365 等其他 Microsoft 服务一致。 为了满足此要求，iOS 和 macOS 公司门户将强制执行 Apple 更新的应用程序传输层安全性 (ATS) 要求，这些要求也需要 TLS 1.2+。 ATS 用于对所有通过 HTTPS 的应用通信强制实施更严格的安全措施。 此更改会影响使用 iOS 和 macOS 公司门户应用的 Intune 客户。 有关详细信息，请参阅 [Intune 支持博客](https://aka.ms/compportalats)。

#### <a name="the-intune-app-sdk-will-support-256-bit-encryption-keys---1832174---"></a>Intune App SDK 将支持 256 位加密密钥<!-- 1832174 -->
由应用保护策略启用加密时，适用于 Android 的 Intune App SDK 现在将使用 256 位加密密钥。 SDK 将继续提供 128 位密钥支持以与使用旧版 SDK 的内容和应用兼容。

#### <a name="microsoft-auto-update-version-450-required-for-macos-devices---3503442---"></a>macOS 设备所需的 Microsoft Auto Update 版本 4.5.0<!-- 3503442 -->
若要继续接收公司门户和其他 Office 应用程序的更新，由 Intune 管理的 macOS 设备必须升级到 Microsoft Auto Update 4.5.0。 用户可能已经拥有此版本的 Office 应用程序。

### <a name="device-management"></a>设备管理

#### <a name="intune-requires-macos-1012-or-later---2827778---"></a>Intune 需要 macOS 10.12 或更高版本<!-- 2827778 -->
Intune 现在需要 macOS 版本 10.12 或更高版本。 使用以前的 macOS 版本的设备无法使用公司门户注册到 Intune。 若要获得支持协助和新功能，用户必须将设备升级到 macOS 10.12 或更高版本，并将公司门户升级到最新版本。

<!-- ########################## -->
## <a name="november-2018"></a>2018 年 11 月

### <a name="app-management"></a>应用管理

#### <a name="uninstalling-apps-on-corporate-owned-supervised-ios-devices---1281677---"></a>卸载公司拥有的受监督 iOS 设备上的应用<!-- 1281677 -->
你可以删除公司拥有的受监督 iOS 设备上的应用。 可以通过以“卸载”分配类型的用户或设备组为目标来删除任何应用  。 对于个人或无监督的 iOS 设备，你将继续只能删除使用 Intune 安装的应用。

#### <a name="downloading-intune-win32-app-content---2617320---"></a>下载 Intune Win32 应用内容<!-- 2617320 -->
Windows 10 RS3 及更高版本的客户端将在 Windows 10 客户端上使用传递优化组件下载 Intune Win32 应用内容。 传递优化提供了在默认情况下处于打开状态的对等功能。 目前，可以通过组策略配置传递优化。 有关详细信息，请参阅[适用于 Windows 10 的传递优化](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization)。

#### <a name="end-user-device-and-app-content-menu---2771453---"></a>最终用户设备的应用内容菜单<!-- 2771453 -->
最终用户现在可以使用设备上的上下文菜单和应用来触发常见操作，例如，重命名设备或检查合规性。

#### <a name="set-custom-background-in-managed-home-screen-app----3041945---"></a>在托管的主屏幕应用中设置自定义背景 <!-- 3041945 -->
我们将添加一种设置，使你可自定义 Android Enterprise、多应用和展台模式设备上托管的主屏幕应用的背景外观。  要配置“自定义 URL 背景”，请转到的 Azure 门户中的 Intune >“设备配置”  。 选择当前设备配置文件或创建新配置文件以编辑其展台设置。
若要查看展台设置，请参阅 [Android Enterprise 设备限制](../configuration/device-restrictions-android-for-work.md)。

#### <a name="app-protection-policy-assignment-save-and-apply---3104570---"></a>应用保护策略分配将保存并应用<!-- 3104570 -->
现在可以更好地控制[应用保护策略分配](../apps/app-protection-policies.md)。 选择“分配”  以设置或编辑策略的分配时，必须先  保存你的配置才能使更改生效。 使用“放弃”  以清除你所做的所有更改，而不保存对包括或排除列表进行的任何更改。  通过要求“保存”或“放弃”，仅向你预期的用户分配应用保护策略。

#### <a name="new-microsoft-edge-browser-settings-for-windows-10-and-later---3174639---"></a>适用于 Windows 10 及更高版本的新 Microsoft Edge 浏览器设置<!-- 3174639 -->
此更新包括用于帮助控制和管理设备上的 Microsoft Edge 浏览器的新设置。 有关这些设置的列表，请参阅[适用于 Windows 10（及更高版本）的设备限制](../configuration/device-restrictions-windows-10.md#microsoft-edge-browser)。

#### <a name="new-apps-support-with-app-protection-policies---3330037---"></a>具有应用保护策略的新应用支持<!-- 3330037 -->
现在可以管理以下具有 [Intune 应用保护策略](../apps/app-protection-policies.md)的应用：
- Stream (iOS)
- To DO（Android、iOS）
- PowerApps（Android、iOS）
- Flow（Android、iOS）

使用应用保护策略来保护这些应用（如其他 Intune 策略托管应用）的公司数据和控制数据传输。 注意：如果 Flow 在控制台中尚不可见，则在创建或编辑应用保护策略时添加 Flow。 若要执行此操作，请使用“+ 更多应用”  选项，然后在输入字段中指定 Flow 的“应用 ID”  。 对于 Android，请使用“com.microsoft.flow”  ，对于 iOS，请使用“com.microsoft.procsimo”  。


### <a name="device-configuration"></a>设备配置

#### <a name="support-for-ios-12-oauth-in-ios-email-profiles--2155106---"></a>支持 iOS 电子邮件配置文件中的 iOS 12 OAuth<!--2155106 -->
Intune 的 iOS 电子邮件配置文件支持 iOS 12 Open Authorization (OAuth)。 要查看此功能，请创建新配置文件（“设备配置” > “配置文件” > “创建配置文件” >  iOS 平台 >“电子邮件”配置文件类型），或更新现有的 iOS 电子邮件配置文件      。 如果在已部署到用户的配置文件中启用 OAuth，则会提示用户重新进行身份验证，然后再次下载其电子邮件。

[iOS 电子邮件配置文件](../configuration/email-settings-ios.md)提供了有关在电子邮件配置文件中使用 OAuth 的详细信息。

#### <a name="network-access-control-nac-support-for-citrix-sso-for-ios---3259404---"></a>对 Citrix SSO for iOS 的网络访问控制 (NAC) 支持<!-- 3259404 -->
Citrix 已向 Citrix Gateway 发布更新以允许对 Intune 中的 Citrix SSO for iOS 使用网络访问控制 (NAC)。 可以选择在 Intune 中将设备 ID 包括在 VPN 配置文件中，然后将此配置文件推送到 iOS 设备。 你需要将最新更新安装到 Citrix Gateway 才能使用此功能。

[在 iOS 设备上配置 VPN 设置](../configuration/vpn-settings-ios.md#base-vpn-settings)提供了有关使用 NAC 的详细信息，包括一些附加要求。 

#### <a name="ios-and-macos-version-numbers-and-build-numbers-are-shown---1892471---"></a>将显示 iOS 和 macOS 的版本号和生成号<!-- 1892471 -->
在“设备符合性” > “设备符合性”中，iOS 和 macOS 操作系统版本都会显示，并且可在符合性策略中使用   。 此更新包括可为这两个平台配置的生成号。
Apple 每次发布安全更新时，会保留版本号，更新生成号。 通过在符合性策略中使用生成号，可轻松地检查是否已安装漏洞更新。
若要使用此功能，请参阅 [iOS](../protect/compliance-policy-create-ios.md#device-health) 和 [macOS](../protect/compliance-policy-create-mac-os.md#device-properties) 符合性策略。

#### <a name="update-rings-are-being-replaced-with-delivery-optimization-settings-for-windows-10-and-later---2753807---"></a>更新通道被替换为适用于 Windows 10 及更高版本的传递优化设置<!-- 2753807 -->
传递优化是适用于 Windows 10 及更高版本的新配置文件。 此功能可简化将软件更新传递到组织中的设备的过程。 此更新还可帮助你使用配置文件传递新更新通道和现有更新通道中的设置。
若要配置传递优化配置文件，请参阅 [Windows 10（及更高版本）传递优化设置](../configuration/delivery-optimization-windows.md)。

#### <a name="new-device-restriction-settings-added-to-ios-and-macos-devices---2827760---"></a>将新设备限制设置添加到 iOS 和 macOS 设备<!-- 2827760 -->
此更新包括随 iOS 12 发布的 iOS 和 macOS 设备的新设置：

**iOS 设置**： 
- 常规：阻止应用删除（仅监管模式）
- 常规：阻止 USB 受限模式（仅监管模式）
- 常规：强制执行自动日期和时间（仅监管模式）
- 密码:阻止密码自动填充（仅监管模式）
- 密码:阻止密码临近感应请求（仅监管模式）
- 密码:阻止密码共享（仅监管模式）

**macOS 设置**： 
- 密码:阻止密码自动填充
- 密码:阻止密码临近感应请求
- 密码:阻止密码共享

要了解有关这些设置的详细信息，请参阅 [iOS](../configuration/device-restrictions-ios.md) 和 [macOS](../configuration/device-restrictions-macos.md) 设备限制设置。

### <a name="device-enrollment"></a>设备注册

#### <a name="autopilot-support-for-hybrid-azure-active-directory-joined-devices-preview---1048100--"></a>已加入混合 Azure Active Directory 的设备的 Autopilot 支持（预览）<!-- 1048100-->
现在可以使用 Autopilot 对已加入混合 Azure Active Directory 的设备进行设置。 设备必须加入组织网络中，才能使用混合 Autopilot 功能。 有关详细信息，请参阅[使用 Intune 和 Windows Autopilot 部署已加入混合 Azure AD 的设备](../enrollment/windows-autopilot-hybrid.md)。
此功能将在未来几天内在整个用户群中推出。 因此，在推送到你的帐户之前，你可能无法执行这些步骤。

#### <a name="select-apps-tracked-on-the-enrollment-status-page---2531007---"></a>选择注册状态页上跟踪的应用<!-- 2531007 -->
可以选择在“注册状态”页面上跟踪的应用。 在安装这些应用之前，用户无法使用该设备。 有关详细信息，请参阅[设置注册状态页](../enrollment/windows-enrollment-status.md)。

#### <a name="search-for-autopilot-device-by-serial-number--2595788---"></a>按序列号搜索 Autopilot 设备<!--2595788 -->
现在可以按序列号搜索 Autopilot 设备。 若要执行此操作，请选择“设备注册”   > “Windows 注册”   > “设备”  > 在“按序列号搜索”框中键入序列号  > 按 Enter。

#### <a name="track-installation-of-office-proplus--2620217---"></a>跟踪 Office 专业增强版的安装过程<!--2620217 -->
用户可以使用[注册状态页面](../enrollment/windows-enrollment-status.md)来跟踪 [Office 专业增强版](../apps/apps-add-office365.md)的安装进度。 有关详细信息，请参阅[设置注册状态页](../enrollment/windows-enrollment-status.md)。

#### <a name="alerts-for-expiring-vpp-token-or-company-portal-license-running-low---2237572---"></a>针对即将过期的 VPP 令牌或公司门户许可证不足的警报<!-- 2237572 -->
如果在 DEP 注册期间使用批量采购计划 (VPP) 预先设置公司门户，则在 VPP 令牌即将过期以及公司门户的许可证不足的情况下，Intune 将发出警报。

#### <a name="macos-device-enrollment-program-support-for-apple-school-manager-accounts--3006133---"></a>macOS 设备注册计划支持 Apple School Manager 帐户<!--3006133 -->
Intune 现在支持对 Apple School Manager 帐户使用 macOS 设备上的设备注册计划。  有关详细信息，请参阅[通过 Apple School Manager 或设备注册计划自动注册 macOS 设备](../enrollment/device-enrollment-program-enroll-macos.md)。

#### <a name="new-intune-device-subscription-sku--3312071--"></a>新的 Intune 设备订阅 SKU<!--3312071-->
为了帮助降低企业中管理设备的成本，现在已提供基于设备的新订阅 SKU。 此 Intune 设备 SKU 按月按设备获取许可。 价格因许可计划而异。 可直接通过 Microsoft 365 管理中心，以及通过[企业协议](https://www.microsoft.com/licensing/licensing-programs/enterprise?activetab=enterprise-tab:primaryr2) (EA)、[Microsoft 产品和服务协议](https://www.microsoft.com/licensing/mpsa/default) (MPSA)、[Microsoft 开放式协议](https://partner.microsoft.com/licensing/licensing-agreements)和[云解决方案提供商](https://www.microsoftpartnercommunity.com/t5/Partnership-101/What-is-the-Cloud-Solution-Provider-CSP-program/td-p/2453) (CSP) 获得许可。

### <a name="device-management"></a>设备管理

#### <a name="temporarily-pause-kiosk-mode-on-android-devices-to-make-changes---3041935---"></a>暂时暂停 Android 设备上的展台模式以进行更改<!-- 3041935 -->
在多应用展台模式下使用 Android 设备时，IT 管理员可能需要对设备进行更改。 此更新包括新的多应用展台设置，允许 IT 管理员使用 PIN 临时暂停展台模式，并有权访问整个设备。
若要查看展台设置，请参阅 [Android Enterprise 设备限制](../configuration/device-restrictions-android-for-work.md)。

#### <a name="enable-virtual-home-button-on-android-enterprise-kiosk-devices----3042021---"></a>启用 Android Enterprise 展台设备上的虚拟主页按钮 <!-- 3042021 -->
新的设置将允许用户点击其设备上的软键按钮，以在其多应用展台设备上托管的主屏幕应用和其他已分配的应用之间进行切换。 此设置在用户的展台应用未对“后退”按钮及时做出响应的情况下特别有用。 可为公司拥有的一次性 Android 设备配置此设置。 要启用或禁用“虚拟主页”按钮，请转至 Azure 门户中的 Intune >“设备配置”  。 选择当前设备配置文件或创建新配置文件以编辑其展台设置。
若要查看展台设置，请参阅 [Android Enterprise 设备限制](../configuration/device-restrictions-android-for-work.md)。




<!-- ########################## -->
## <a name="october-2018"></a>2018 年 10 月

### <a name="app-management"></a>应用管理

#### <a name="access-to-key-profile-properties-using-the-company-portal-app---772203---"></a>使用公司门户应用访问键配置文件属性<!-- 772203 -->
最终用户现在可以从公司门户应用访问关键帐户属性和操作，如密码重置。 

#### <a name="3rd-party-keyboards-can-be-blocked-by-app-settings-on-ios---1248481---"></a>可通过 iOS 上的 APP 设置阻止第三方键盘<!-- 1248481 -->
在 iOS 设备上，Intune 管理员可以阻止使用第三方键盘在受策略保护的应用中访问组织数据。 当应用程序保护策略 (APP) 设置为阻止第三方键盘时，设备用户将在首次使用第三方键盘与公司数据交互时收到一条消息。 将阻止本地键盘以外的所有选项，设备用户不会看到它们。 设备用户只会看到一次对话消息。 

#### <a name="user-account-access-of-intune-apps-on-managed-android-and-ios-devices---1248496---"></a>托管的 Android 和 iOS 设备上的 Intune 应用的用户帐户访问权限<!-- 1248496 -->
作为 Microsoft Intune 管理员，可控制将哪些用户帐户添加到托管设备上的 Microsoft Office 应用程序。 可以将访问权限限制为仅允许的组织用户帐户，并阻止已注册设备上的个人帐户。 

#### <a name="outlook-ios-and-android-app-configuration-policy--1828527---"></a>Outlook for iOS 和 Outlook for Android 应用配置策略<!--1828527 -->
现在可以为通过 ActiveSync 协议进行基本身份验证的本地用户创建适用于 iOS 和 Android 的 Outlook for iOS 和 Outlook for Android 应用配置策略。 将为 Outlook for iOS 和 Outlook for Android 启用和添加其他配置设置。

#### <a name="office-365-pro-plus-language-packs---1833450---"></a>Office 365 Pro Plus 语言包<!-- 1833450 -->
作为 Intune 管理员，你将能够为通过 Intune 管理的 Office 365 Pro Plus 应用部署其他语言。 可用语言列表包括语言包的“类型”（核心、部分和校对）  。 在 Azure 门户中，选择“Microsoft Intune” > “客户端应用” > “应用” > “添加”     。 在“添加应用”边栏选项卡的“应用类型”列表中，选择“Office 365 套件”下的“Windows 10”     。 在“应用套件设置”边栏选项卡中选择“语言”   。

#### <a name="windows-line-of-business-lob-apps-file-extensions---1884873---"></a>Windows 业务线 (LOB) 应用文件扩展名<!-- 1884873 -->
Windows LOB 应用的文件扩展名现在包括 .msi、.appx、.appxbundle、.msix 和 .msixbundle      。 可以在 Microsoft Intune 中添加应用，方法是通过选择“客户端应用” > “应用” > “添加”    。 将显示“添加应用”窗格，可选择“应用类型”   。 对于 Windows LOB 应用，选择“业务线”应用作为应用类型，选择“应用包文件”，然后输入带有扩展名的安装文件   。

#### <a name="windows-10-app-deployment-using-intune---2309001---"></a>使用 Intune 部署 Windows 10 应用<!-- 2309001 -->
在业务线 (LOB) 应用和适用于企业的 Microsoft Store 应用的现有支持上进行构建时，管理员可以使用 Intune 将其组织的大部分现有应用程序部署到 Windows 10 设备上的最终用户。 管理员可以使用各种格式（例如 MSI、Setup.exe 或 MSP）为 Windows 10 用户添加、安装和卸载应用程序。 Intune 将在下载和安装、使用 Windows 10 操作中心通知最终用户状态或重新启动需求之前评估要求规则。 此功能将有效地清除对将此工作负荷转移到 Intune 和云感兴趣的组织所存在的阻碍。 此功能目前处于公共预览状态，我们预计在未来的几个月内为此功能添加重要的新功能。 

#### <a name="app-protection-policy-app-settings-for-web-data---2662995---"></a>适用于 Web 数据的应用保护策略 (APP) 设置<!-- 2662995 -->
将更新 Android 和 iOS 设备上适用于 Web 内容的应用策略设置，以更好地处理 http 和 https Web 链接，以及通过 iOS 通用链接和 Android 应用链接进行的数据传输。 

#### <a name="end-user-device-and-app-content-menu---2771453---"></a>最终用户设备的应用内容菜单<!-- 2771453 -->
最终用户现在可以在设备和应用上使用上下文菜单触发常见操作，例如重命名设备或检查符合性。 

#### <a name="windows-company-portal-keyboard-shortcuts---2771518---"></a>Windows 公司门户键盘快捷方式<!-- 2771518 -->
最终用户现在可以使用键盘快捷方式（快捷键）在 Windows 公司门户中触发应用和设备操作。

#### <a name="require-non-biometric-pin-after-a-specified-timeout---1506985---"></a>在指定的超时后需要非生物识别 PIN<!-- 1506985 -->
在管理员指定的超时时长后要求输入非生物识别 PIN，Intune 会限制使用生物识别来访问公司数据，从而为启用了移动应用管理 (MAM) 的应用提升安全性。 这些设置会影响依靠 Touch ID (iOS)、Face ID (iOS)、Android Biometric 或其他未来生物识别身份验证方法访问启用了 APP/MAM 的应用程序的用户。 这些设置会使 Intune 管理员能够更精细地控制用户访问，让带有多个指纹或其他生物识别访问方法的设备只能向正确的用户显示公司数据。 在 Azure 门户中，打开“Microsoft Intune”  。 选择“客户端应用” > “应用保护策略” > “添加策略” > “设置”     。 找到特定设置的“访问”部分  。 有关访问设置的信息，请参阅 [iOS 设置](../apps/app-protection-policy-settings-ios.md#access-requirements)和 [Android 设置](../apps/app-protection-policy-settings-android.md#access-requirements)。

#### <a name="intune-app-data-transfer-settings-on-ios-mdm-enrolled-devices---2244713---"></a>iOS MDM 注册设备上的 Intune 应用数据传输设置<!-- 2244713 -->
可以将 iOS MDM 注册设备上的 Intune 应用数据传输设置控制与指定注册用户的身份（也称为用户主体名称 (UPN)）分开。 不使用 IntuneMAMUPN 的管理员不会观察到行为更改。 当此功能可用时，使用 IntuneMAMUPN 控制已注册设备上的数据传输行为的管理员应检查新设置，并根据需要更新其应用设置。

#### <a name="windows-10-win32-apps---2617325---"></a>Windows 10 Win32 应用<!-- 2617325 -->
可以将 Win32 应用配置为在单个用户的用户上下文中安装，而不是为该设备的所有用户安装应用。

#### <a name="windows-win32-apps-and-powershell-scripts---2617330---"></a>Windows Win32 应用和 PowerShell 脚本<!-- 2617330 -->
最终用户无需登录设备即可安装 Win32 应用或执行 PowerShell 脚本。 

#### <a name="troubleshooting-client-app-installation---1363711---"></a>客户端应用安装疑难解答<!-- 1363711 -->
可以通过查看“故障排除”边栏选项卡中标有“应用安装”的列来解决客户端应用的安装问题   。 要查看“故障排除”边栏选项卡，请在 Intune 门户中，选择“故障排除”下的“帮助和支持”    。

### <a name="device-configuration"></a>设备配置

#### <a name="create-dns-suffixes-in-vpn-configuration-profiles-on-devices-running-windows-10---1333668---"></a>在运行 Windows 10 的设备上的 VPN 配置文件中创建 DNS 后缀<!-- 1333668 -->
在创建 VPN 设备配置的配置文件（“设备配置”   > “配置文件”   > “创建配置文件”   > “Windows 10 及更高版本”  平台>“VPN”  配置文件类型）时，需要输入一些 DNS 设置。 通过此更新，还可以在 Intune 中输入多个 DNS 后缀  。 使用 DNS 后缀时，可以使用其短名称而不是完全限定的域名 (FQDN) 搜索网络资源。 此更新还允许在 Intune 中更改 DNS 后缀的顺序。
[Windows 10 VPN 设置](../configuration/vpn-settings-windows-10.md#dns-settings)列出了当前的 DNS 设置。
适用于：Windows 10 设备

#### <a name="support-for-always-on-vpn-for-android-enterprise-work-profiles---1333705---"></a>支持 Android 企业工作配置文件的始终可用 VPN<!-- 1333705 -->
在此更新中，可以在具有托管工作配置文件的 Android 企业设备上使用始终可用的 VPN 连接。 Always-on VPN 连接一直保持连接状态
，或在用户解锁设备、设备重启或无线网络更改时立即重新连接。 还可以将连接置于“锁定”模式，该模式会阻止所有网络流量，直到 VPN 连接处于活动状态。
可以在“设备配置” > “配置文件” > “创建配置文件” >  适用于平台的“Android 企业版”>“设备限制” > “连接”设置中启用始终可用的 VPN       。

#### <a name="issue-scep-certificates-to-user-less-devices---1744554---"></a>向无用户设备颁发 SCEP 证书<!-- 1744554 -->
目前证书的颁发对象是用户。 通过此更新，SCEP 证书可以颁发给设备，包括无用户设备，例如网亭（“设备配置” > “配置文件” > “创建配置文件” >  适用于平台的“Windows 10 及更高版本”> 配置文件的“SCEP 证书”）      。 其他更新包括：
- SCEP 配置文件中的“使用者”  属性现在是自定义文本框，可以包含新的变量。 
- SCEP 配置文件中的“使用者可选名称(SAN)”  属性现在是表格式，可以包含新的变量。 在表中，管理员可以添加属性并在自定义文本框中填写值。 SAN 将支持以下属性： 
  - DNS
  - 电子邮件地址
  - UPN

  可以在自定义值文本框中使用静态文本添加这些新变量。 例如，可以将 DNS 属性添加为 `DNS = {{AzureADDeviceId}}.domain.com`。

  > [!NOTE]
  > 在 SAN 的静态文本中无法使用大括号 ({ })、分号 (;) 和竖杠符号 (|)。 `Subject` 或 `Subject alternative name` 只接受大括号仅包含一个新设备证书变量的情况。 

新的设备证书变量：  

```
"{{AAD_Device_ID}}",
"{{Device_Serial}}",
"{{Device_IMEI}}",
"{{SerialNumber}}",
"{{IMEINumber}}",
"{{AzureADDeviceId}}",
"{{WiFiMacAddress}}",
"{{IMEI}}",
"{{DeviceName}}",
"{{FullyQualifiedDomainName}}",
"{{MEID}}",
```

> [!NOTE]
> - `{{FullyQualifiedDomainName}}` 仅适用于 Windows 和已加入域的设备。 
> - 在使用者或 SAN 中为设备证书指定设备属性（如 IMEI、序列号和完全限定的域名）时，请注意这些属性可能被有权访问设备的人员模仿。 

[创建 SCEP 证书配置文件](../protect/certificates-profile-scep.md#create-a-scep-certificate-profile)列出了创建 SCEP 配置的配置文件时的当前变量。 

适用于：Windows 10 及更高版本和 iOS，支持用于 Wi-fi

#### <a name="remotely-lock-uncompliant-devices---2064495---"></a>远程锁定不兼容的设备<!-- 2064495 -->
如果设备不兼容，可以根据符合性策略创建一个可以远程锁定设备的操作。 在 Intune >“设备符合性”中，创建新的策略或选择现有策略 >“属性”   。 选择“针对非符合性的操作”   > “添加”  ，然后选择远程锁定设备。
在以下设备上受支持： 
- Android
- iOS
- macOS
- Windows 10 移动版 
- Windows Phone 8.1 及更高版本 

#### <a name="windows-10-and-later-kiosk-profile-improvements-in-the-azure-portal---2748224---"></a>Azure 门户中的 Windows 10 和更高版本的展台配置文件改进<!-- 2748224 -->
此更新包括对 Windows 10 网亭设备配置文件的以下改进（“设备配置” > “配置文件” > “创建配置文件” >  适用于平台的“Windows 10 及更高版本”> 配置文件类型的“网亭预览”）      ： 
- 目前，用户可以在同一设备上创建多个网亭配置文件。 利用此更新，Intune 将支持每台设备只有一个网亭配置文件。 如果你仍需要在单台设备上创建多个网亭配置文件，可以使用自定义 URI。
- 在“多应用网亭”配置文件中，可以在应用程序网格中对“开始菜单布局”选择应用程序磁贴大小和顺序   。 如果需要更多自定义设置，可以继续上传 XML 文件。
- 网亭浏览器设置移入“网亭”  设置。 目前，“网亭 Web 浏览器”  设置在 Azure 门户中具有其自己的类别。
适用于：Windows 10 及更高版本

#### <a name="pin-prompt-when-you-change-fingerprints-or-face-id-on-an-ios-device----2637704----"></a>当你在 iOS 设备上更改指纹或 Face ID 时，系统将提示你输入 PIN <!-- 2637704  -->
当用户在其 iOS 设备上进行生物识别更改后，系统将提示用户输入 PIN。 这包括对已注册的指纹或 Face ID 的更改。 出现提示的时间取决于如何配置“以下时间(以分钟为单位)之后重新检查访问要求”  超时。  未设置 PIN 时，会提示用户设置一个 PIN。 
 
此功能仅适用于 iOS，并且需要集成了 Intune APP SDK for iOS 版本 9.0.1 或更高版本的应用程序参与。 必须集成 SDK，以便可以在目标应用程序上强制执行行为。 此集成陆续进行，取决于特定应用程序团队。 参与的一些应用包括 WXP、Outlook、Managed Browser 和 Yammer。

#### <a name="network-access-control-support-on-ios-vpn-clients---1333693---"></a>iOS VPN 客户端上的网络访问控制支持<!-- 1333693 -->
通过此更新，可以在为 Cisco AnyConnect、F5 Access 和 Citrix SSO for iOS 创建 VPN 配置文件时启用网络访问控制 (NAC)。 此设置允许将设备的 NAC ID 包含在 VPN 配置文件中。 目前，没有任何支持此新 NAC ID 的 VPN 客户端或 NAC 合作伙伴解决方案，但我们将通过[支持博客文章](ttps://aka.ms/iOS12_and_vpn)发送通知。

要使用 NAC，需要：
1. 选择加入以允许 Intune 在 VPN 配置文件中包含设备 ID
2. 使用直接来自 NAC 提供程序的指导更新 NAC 提供程序软件/固件

有关 iOS VPN 配置文件中此设置的信息，请参阅[在 Microsoft Intune 的 iOS 设备上添加 VPN 设置](../configuration/vpn-settings-ios.md)。 有关网络访问控制的详细信息，请参阅[网络访问控制 (NAC) 与 Intune 集成](../protect/network-access-control-integrate.md)。 

适用于：iOS

#### <a name="remove-an-email-profile-from-a-device-even-when-theres-only-one-email-profile---1818139---"></a>即使只有一个电子邮件配置文件，也可从设备中删除该电子邮件配置文件<!-- 1818139 -->
以前，如果只有唯一一个电子邮件配置文件，则无法从设备删除该电子邮件配置文件  。 有了此更新，该行为发生了变化。 现在，即使设备上只有唯一一个电子邮件配置文件，也可删除该电子邮件配置文件。 有关详细信息，请参阅[使用 Intune 向设备添加电子邮件设置](../configuration/email-settings-configure.md)。

#### <a name="powershell-scripts-and-aad---2309469---"></a>PowerShell 脚本和 AAD<!-- 2309469 -->
Intune 中的 PowerShell 脚本可应用于 AAD 设备安全组。

#### <a name="new-required-password-type-default-setting-for-android-android-enterprise---2649963---"></a>适用于 Android、Android 企业版的新的“所需密码类型”默认设置<!-- 2649963 -->
创建新的符合性策略时（“Intune” > “设备符合性” > “策略” > “创建策略” > > Android 或 Android Enterprise 平台 >“系统安全性”），所需密码类型的默认值会更改：       

更改自：设备默认设置：最少数字

适用于：Android、Android Enterprise

要查看这些设置，请转到 [Android](../protect/compliance-policy-create-android.md) 和 [Android Enterprise](../protect/compliance-policy-create-android-for-work.md)。

#### <a name="use-a-pre-shared-key-in-a-windows-10-wi-fi-profile---2662938---"></a>在 Windows 10 Wi-Fi 配置文件中使用预共享密钥<!-- 2662938 -->
通过本次更新，用户能够使用预共享密钥 (PSK) 和 WPA/WPA2 个人安全协议对 Windows 10 的 Wi-Fi 配置的配置文件进行身份验证。 还可以在 Windows 10 的 2018 年 10 月更新中为设备指定按流量计费的网络的成本配置。

目前，必须导入 Wi-Fi 配置文件，或创建自定义配置文件才能使用预共享密钥。 [Windows 10 的 Wi-Fi 设置](../configuration/wi-fi-settings-windows.md)列出了当前设置。 

#### <a name="remove-pkcs-and-scep-certificates-from-your-devices---3218390---"></a>从设备中删除 PKCS 和 SCEP 证书<!-- 3218390 -->
在某些情况下，即使从组中删除策略，删除配置或合规性部署，或是由管理员更新现有 SCEP 或 PKCS 配置文件，PKCS 和 SCEP 证书仍会存留在设备上。 此更新改变了这种情况。 在某些情况下，PKCS 和 SCEP 证书会从设备中删除，而在其他一些情况下，这些证书会存留在设备上。 请参阅[在 Microsoft Intune 中删除 SCEP 和 PKCS 证书](../protect/remove-certificates.md)了解这些情况。

#### <a name="use-gatekeeper-on-macos-devices-for-compliance---2504381---"></a>在 macOS 设备上使用网关守卫实现合规性<!-- 2504381 -->
此更新包括 macOS 网关守卫，用于评估设备的符合性。 要设置网关守卫属性，请[为 macOS 设备添加设备符合性策略](../protect/compliance-policy-create-mac-os.md)。


### <a name="device-enrollment"></a>设备注册

#### <a name="apply-autopilot-profile-to-enrolled-win-10-devices-not-already-registered-for-autopilot---1558983---"></a>将 Autopilot 配置文件应用到尚未注册 Autopilot 的已注册 Win 10 设备<!-- 1558983 -->
可以将 Autopilot 配置文件应用到尚未注册 Autopilot 的已注册 Win 10 设备。 在 Autopilot 配置文件中，选择“将所有目标设备转换为 Autopilot”  选项，以使用 Autopilot 部署服务自动注册非 Autopilot 设备。 等待 48 小时来处理注册。 取消注册设备并重置后，Autopilot 将对其进行配置。

#### <a name="create-and-assign-multiple-enrollment-status--page-profiles-to-azure-ad-groups---2526564---"></a>创建多个注册状态页配置文件并将其分配给 Azure AD 组<!-- 2526564 -->
现在可以[创建](../enrollment/windows-enrollment-status.md)多个注册状态页面配置文件并将其分配给 Azure AD 组。

#### <a name="migration-from-device-enrollment-program-to-apple-business-manager-in-intune--2748613--"></a>在 Intune 中从设备注册计划迁移到 Apple Business Manager<!--2748613-->
Apple Business Manager (ABM) 在 Intune 中工作，可以将你的帐户从设备注册计划 (DEP) 升级到 ABM。 Intune 中的过程是相同的。 若要将你的 Apple 帐户从 DEP 升级到 ABM，请转到 [https://support.apple.com/HT208817]( https://support.apple.com/HT208817)。

#### <a name="alert-and-enrollment-status-tabs-on-the-device-enrollment-overview-page--2748656--"></a>“设备注册概述”页上的“警报”和“注册状态”选项卡<!--2748656-->
警报和注册失败现在显示在“设备注册概述”页的单独选项卡上。

#### <a name="enrollment-abandonment-report---1382924---"></a>注册放弃报告<!-- 1382924 -->
我们在“设备注册” > “监视”下发布了新报表，其中提供了有关已放弃注册的详细信息   。 有关详细信息，请参阅[公司门户放弃报表](../enrollment/enrollment-report-company-portal-abandon.md)。

#### <a name="new-azure-active-directory-terms-of-use-feature---2870393---"></a>新的 Azure Active Directory 使用条款功能<!-- 2870393 -->
Azure Active Directory 具备可供使用的使用条款功能，而不必再使用现有的 Intune 条款和条件。 Azure AD 使用条款功能在显示哪些条款以及何时显示这些条款方面更加灵活，并能更好地支持本地化，更好地控制条款的呈现方式以及改进报告。 Azure AD 使用条款功能需要 Azure Active Directory Premium P1，后者也是企业移动性 + 安全性 E3 套件的一部分。 要了解详情，请参阅[管理公司的用户访问条款和条件](../enrollment/terms-and-conditions-create.md)一文。

#### <a name="android-device-owner-mode-support--3188762--"></a>Android 设备所有者模式支持<!--3188762-->
对于 Samsung Knox 移动注册，Intune 现在支持将设备注册到 Android 设备所有者管理模式。 使用 WiFi 或移动电话网络的用户在第一次打开他们的设备时，只需几次点击即可进行注册。 有关详细信息，请参阅[使用 Samsung 的 Knox 移动注册自动注册 Android 设备](../enrollment/android-samsung-knox-mobile-enroll.md)。

### <a name="device-management"></a>设备管理
#### <a name="new-settings-for-software-updates-----1907869---"></a>软件更新的新设置  <!-- 1907869 -->  
- 现在可以将某些通知配置为向最终用户发出完成最新软件更新安装后需要重新启动的警报。   
- 现在可以配置在非工作时间重新启动的重新启动警告提示，这支持 BYOD 方案。

#### <a name="group-windows-autopilot-enrolled-devices-by-correlator-id---2075110---"></a>按交换码 ID 对已注册 Windows Autopilot 的设备进行分组<!-- 2075110 -->
通过 Configuration Manager [使用 Autopilot 为现有设备注册](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430)时，Intune 现已支持按交换码 ID 对 Windows 设备进行分组。 交换码 ID 是 Autopilot 配置文件的参数。 Intune 会自动将 [Azure AD 设备属性 enrollmentProfileName](https://docs.microsoft.com/azure/active-directory/users-groups-roles/groups-dynamic-membership#rules-for-devices) 设置为“OfflineAutopilotprofile - <correlator ID>”。 如此，即可通过离线 Autopilot 注册的 enrollmentprofileName 属性，根据交换码 ID 创建任意 Azure AD 动态组。 有关详细信息，请参阅[面向现有设备的 Windows Autopilot](../enrollment/enrollment-autopilot.md#windows-autopilot-for-existing-devices)。

#### <a name="intune-app-protection-policies---2984657---"></a>Intune 应用保护策略<!-- 2984657 -->
可使用 Intune 应用保护策略为受 Intune 保护的应用（如 Microsoft Outlook 和 Microsoft Word）配置各种数据保护设置。 我们为 [iOS](../apps/app-protection-policy-settings-ios.md) 和 [Android](../apps/app-protection-policy-settings-android.md) 更改了这些设置的外观，以便更轻松地查找单个设置。 策略设置分为三类：
- **数据重定位** - 此组包含数据丢失防护 (DLP) 控件，如剪切、复制、粘贴和另存为限制。 这些设置决定了用户与应用中的数据的交互方式。
- **访问要求** - 该组包含每个应用的 PIN 选项，用于确定最终用户在工作环境中访问应用的方式。  
- **条件启动** - 该组包含最低操作系统设置、已越狱和取得 Root 权限的设备检测以及脱机宽限期等设置。  
  
设置的功能不会更改，但在处理策略创作流程时会更容易找到它们。

#### <a name="restricts-apps-and-block-access-to-company-resources-on-android-devices---2451462----"></a>限制应用，并阻止对 Android 设备上公司资源的访问<!-- 2451462  -->  
在“设备符合性” > “策略” > “创建策略” > “Android” > “系统安全”中，“设备安全”部分下有一个名为“受限制的应用”的新设置        。 如果设备上安装了某些应用，“受限制的应用”设置将使用符合性策略来阻止对公司资源的访问  。 除非从设备中删除受限制的应用，否则设备会一直被视为不符合要求。
适用于： 
- Android

### <a name="intune-apps"></a>Intune 应用

#### <a name="intune-will-support-a-maximum-package-size-of-8-gb-for-lob-apps---1727158---"></a>对于 LOB 应用，Intune 将支持最大为 8 GB 的包大小<!-- 1727158 -->
Intune 将业务线 (LOB) 应用的最大包大小增加到 8 GB。 有关详细信息，请参阅[将应用添加到 Microsoft Intune](../apps/apps-add.md)。

#### <a name="add-custom-brand-image-for-company-portal-app---1916266---"></a>为公司门户应用添加自定义品牌图像<!-- 1916266 -->
Microsoft Intune 管理员可以上传自定义品牌图像，该图像将在 iOS 公司门户应用的用户配置文件页面上作为背景图像显示。 有关配置公司门户应用的详细信息，请参阅[如何配置 Microsoft Intune 公司门户应用](../apps/company-portal-app.md)。

#### <a name="intune-will-maintain-the-office-localized-language-when-updating-office-on-end-users-machines---2971030---"></a>在最终用户计算机上更新 Office 时，Intune 将维护维持 Office 本地化语言<!-- 2971030 -->
Intune 在最终用户计算机上安装 Office 时，最终用户将自动获得与以前安装的 .MSI Office 相同的语言包。 有关详细信息，请参阅[使用 Microsoft Intune 将 Office 365 应用分配到 Windows 10 设备](../apps/apps-add-office365.md)。

### <a name="monitor-and-troubleshoot"></a>监视和故障排除

#### <a name="new-intune-support-experience-in-the-microsoft-365-device-management-portal---3076965---"></a>Microsoft 365 设备管理门户中的新 Intune 支持体验<!-- 3076965 -->
我们正在 [Microsoft 365 设备管理门户]( https://devicemanagement.microsoft.com)中推出适用于 Intune 的新的“帮助和支持”体验。 通过新体验，可以用自己的语言描述问题，并获得故障排除见解和基于 Web 的修复内容。 这些解决方案通过基于规则的机器学习算法提供并依赖于用户查询。  

除特定于问题的指南之外，还可以使用新的案例创建工作流通过电子邮件或电话打开支持案例。  

对于参与部署的客户，此新体验取代了一组静态预选选项的当前“帮助和支持”体验，这些选项基于打开“帮助和支持”时所在控制台的区域。  

 我们正在向部分租户（不是所有租户）推出此新的“帮助和支持”体验，你可在“设备管理”门户中进行找到。此新体验的参与者是在可用的 Intune 租户中随机选择的。在我们扩大推出时，将添加新租户。  

有关详细信息，请参阅“如何获取对 Microsoft Intune 的支持”中的[“帮助和支持”体验](get-support.md#help-and-support-experience)。  

#### <a name="powershell-module-for-intune--preview-available---951068---"></a>适用于 Intune 的 PowerShell 模块 - 提供预览版<!-- 951068 -->
现在，[GitHub](https://aka.ms/intunepowershell) 上提供了新 PowerShell 模块的预览版，该模块可通过 Microsoft Graph 提供对 Intune API 的支持。 有关如何使用此模块的详细信息，请参阅该处的自述文件。

<!-- ########################## -->
## <a name="september-2018"></a>2018 年 9 月

### <a name="app-management"></a>应用管理

#### <a name="remove-duplication-of-app-protection-status-tiles---3083391---"></a>删除应用保护状态磁贴的副本<!-- 3083391 -->
“iOS 用户状态”和“Android 用户状态”磁贴都会出现在“客户端应用 - 概述”页，以及“客户端应用 - 应用保护状态”页     。 已从“客户端应用 - 概述”页删除状态磁贴，以避免重复  。 

### <a name="device-configuration"></a>设备配置

#### <a name="support-for-more-third-party-certification-authorities-ca---3093107---"></a>为更多第三方证书颁发机构 (CA) 提供支持<!-- 3093107 -->
通过简单证书注册协议 (SCEP)，现在可以使用 Windows、iOS、Android 和 macOS 在移动设备上发布新证书和续订证书。

### <a name="device-enrollment"></a>设备注册

#### <a name="intune-moves-to-support-ios-10-and-later---2454656---"></a>Intune 转为支持 iOS 10 及更高版本<!-- 2454656 -->  
Intune 注册、公司门户和托管浏览器现在仅支持运行 iOS 10 及更高版本的 iOS 设备。 若要查看组织中受影响的设备或用户，请转到 Azure 门户中的 Intune >“设备” > “所有设备”   。 按 OS 进行筛选，然后单击“列”以显示 OS 版本详细信息  。 请让这些用户将其设备升级到受支持的 OS 版本。  

如果拥有下面列出的任何设备，或者想要注册下面列出的任何设备，请注意，它们仅支持 iOS 9 及更早版本。  若要继续访问 Intune 公司门户，必须将这些设备升级到支持 iOS 10 或更高版本的设备：  

* iPhone 4S 
* iPod Touch  
* iPad 2 
* iPad（第 3 代） 
* iPad Mini（第 1 代）  

### <a name="device-management"></a>设备管理

#### <a name="microsoft-365-device-management-administration-center---3078424---"></a>Microsoft 365 设备管理管理中心<!-- 3078424 -->
Microsoft 365 的承诺之一是简化管理，多年来我们整合了后端 Microsoft 365 服务，以提供端到端方案（如 Intune 和 Azure AD 条件访问）。 新 [Microsoft 365 管理中心](https://devicemanagement.microsoft.com)整合、简化并集成了管理员体验。 借助设备管理的专家工作区，可轻松访问组织所需的所有设备和应用管理信息和任务。 我们希望这能成为企业最终用户计算团队的主要云工作区。


<!-- ########################## -->
## <a name="august-2018"></a>2018 年 8 月

### <a name="app-management"></a>应用管理

#### <a name="packet-tunnel-support-for-ios-per-app-vpn-profiles-for-custom-and-pulse-secure-connection-types---1520957---"></a>针对自定义和 Pulse Secure 连接类型的 iOS 每应用 VPN 配置文件的数据包隧道支持<!-- 1520957 -->
如果使用 iOS 每应用 VPN 配置文件，可选择使用应用层隧道（应用-代理）或数据包级别隧道（数据包-隧道）。 这些选项适用于以下连接类型：
- 自定义 VPN
- Pulse Secure - 如果不确定使用哪个值，请查阅 VPN 提供商的文档。

#### <a name="delay-when-ios-software-updates-are-shown-on-the-device---1949583---"></a>延迟 iOS 软件更新在设备上的显示时间<!-- 1949583 -->
在 Intune >“软件更新”   > “适用于 iOS 的更新策略”  中，可配置不希望设备安装任何更新的日期和时间段。 在未来的某个更新中，可延迟软件更新在设备上的显示时间（1-90 天）。 
[在 Microsoft Intune 中配置 iOS 更新策略](../protect/software-updates-ios.md)列出了当前设置。

#### <a name="office-365-proplus-version---2213968---"></a>Office 365 专业增强版<!-- 2213968 -->
如果使用 Intune 将 Office 365 专业增强版应用分配到 Windows 10 设备，则可选择 Office 的版本。 在 Azure 门户中，选择“Microsoft Intune” > “应用” > “添加应用”    。 然后，从“类型”  下拉列表中选择“Office 365 专业增强版套件(Windows 10)”  。 选择“应用套件设置”  以显示关联的边栏选项卡。 将“更新通道”  设置为一个值，如“每月”  。 （可选）选择“是”  ，从最终用户设备中删除其他版本的 Office (msi)。 选择“特定”  ，在最终用户设备上为所选通道安装特定的 Office 版本。 此时，可选择要使用的“特定版本”  的 Office。 可用版本会随时间发生变化。 因此，在创建新部署时，可用版本可能为更新的版本，而不再提供某些较旧版本。 当前部署会继续部署旧版本，但版本列表会持续按通道更新。 有关详细信息，请参阅 [Office 365 专业增强版的更新频道概述](https://docs.microsoft.com/DeployOffice/overview-of-update-channels-for-office-365-proplus)。

#### <a name="support-for-register-dns-setting-for-windows-10-vpn---2282852---"></a>支持面向 Windows 10 VPN 的注册 DNS 设置<!-- 2282852 -->
通过此次更新，可将 Windows 10 VPN 配置文件配置为使用内部 DNS 动态注册分配给 VPN 接口的 IP 地址，而无需使用自定义配置文件。
有关当前可用的 VPN 配置文件设置的信息，请参阅 [Windows 10 VPN 设置](../configuration/vpn-settings-windows-10.md)。

#### <a name="the-macos-company-portal-installer-now-includes-the-version-number-in-the-installer-file-name--2652728--"></a>macOS 公司门户安装程序的安装程序文件名中现在包含版本号<!--2652728-->

#### <a name="ios-automatic-app-updates---2729759---"></a>iOS 自动应用更新<!-- 2729759 -->
自动应用更新适用于设备和用于 iOS 11.0 及更高版本的用户许可应用。

### <a name="device-configuration"></a>设备配置

#### <a name="windows-hello-will-target-users-and-devices---1106609---"></a>Windows Hello 面向用户和设备<!-- 1106609 -->
创建 [Windows hello 企业版](../protect/windows-hello.md)策略后，该策略会应用到组织中的所有用户（租户范围）。 进行此更新后，还可使用设备配置策略（“设备配置”   > “配置文件”   > “创建配置文件”   > “标识保护”   > “Windows Hello 企业版”  ），将此策略应用于特定用户或特定设备。
在 Intune Azure 门户中，Windows Hello 配置和设置现在同时存在于“设备注册”和“设备配置”中   。 **设备注册**面向整个组织（租户范围内），并支持 Windows AutoPilot (OOBE)。 **设备配置**面向使用某种策略的设备和用户，该策略会在签入期间应用。
此功能适用于：  
- Windows 10 及更高版本
- Windows Holographic for Business

#### <a name="zscaler-is-an-available-connection-for-vpn-profiles-on-ios---1769858---"></a>Zscaler 是适用于 iOS 上 VPN 配置文件的可用连接<!-- 1769858 -->
创建 iOS VPN 设备配置文件时（“设备配置”   > “配置文件”   > “创建配置文件”   > “iOS”  “平台”>“VPN  配置文件类型”），有几种连接类型，包括 Cisco、Citrix 等。 此次更新将 Zscaler 添加为一个连接类型。 
[运行 iOS 的设备的 VPN 设置](../configuration/vpn-settings-ios.md)列出了可用的连接类型。

#### <a name="fips-mode-for-enterprise-wi-fi-profiles-for-windows-10---1879077---"></a>适用于 Windows 10 企业 Wi-Fi 配置文件的 FIPS 模式<!-- 1879077 -->
现在可在 Intune Azure 门户中启用适用于 Windows 10 企业 Wi-Fi 配置文件的美国联邦信息处理标准 (FIPS) 模式。 如果在 Wi-Fi 配置文件中启用 FIPS 模式，请确保 Wi-Fi 基础结构上已启用该模式。
有关如何创建 Wi-Fi 配置文件，请参阅 [Intune 中适用于 Windows 10 及更高版本设备的 Wi-Fi 设置](../configuration/wi-fi-settings-windows.md)。

#### <a name="control-s-mode-on-windows-10-and-later-devices---public-preview---1958649---"></a>在 Windows 10 和更高版本设备上的控制 S 模式 - 公共预览版<!-- 1958649 -->
利用该功能更新，可创建一个设备配置文件，用于将 Windows 10 设备从 S 模式下切换出来，或用于防止用户将设备从 S 模式下切换出来。 此功能的位置：Intune >“设备配置” > “配置文件” >  “Windows 10 及更高版本” > “版本升级和模式切换”     。
[S 模式下的 Windows 10 简介](https://www.microsoft.com/windows/s-mode)提供了有关 S 模式的详细信息。
适用于：最新的 [Windows 预览体验](https://docs.microsoft.com/windows-insider/at-work-pro/)版本（预览版）。

#### <a name="windows-defender-atp-configuration-package-automatically-added-to-configuration-profile---2144658---"></a>Windows Defender ATP 配置包自动添加到配置文件<!-- 2144658 -->
在 Intune 中使用[高级威胁防护和加入](../protect/advanced-threat-protection.md#onboard-devices-by-using-a-configuration-profile)设备时，需要提前下载配置包并将其添加到配置文件。 通过此次更新，Intune 可自动从 Windows Defender 安全中心获取该包，并将其添加到配置文件。
适用于 Windows 10 和更高版本。

#### <a name="require-users-to-connect-during-device-setup--2311457--"></a>要求用户在设备设置过程中进行连接<!--2311457-->
现在可以设置设备配置文件，要求设备在 Windows 10 设置过程中连接到网络，然后才能继续完成“网络”页面的操作。 虽然此功能处于预览状态，但 Windows 预览体验内部版本 1809 或更高版本需要使用此设置。
适用于：最新的 [Windows 预览体验](https://docs.microsoft.com/windows-insider/at-work-pro/)版本（预览版）。

#### <a name="restricts-apps-and-block-access-to-company-resources-on-ios-and-android-enterprise-devices---2451462---"></a>限制应用，并阻止对 iOS 和 Android Enterprise 设备上公司资源的访问<!-- 2451462 -->
在“设备符合性” > “策略” > “创建策略” > “iOS” > “系统安全”中，有一个新的“受限制的应用程序”设置       。 如果设备上安装了某些应用，此新设置会使用符合性策略来阻止对公司资源的访问。 除非从设备中删除受限制的应用，否则设备会一直被视为不符合要求。
适用于：iOS

#### <a name="modern-vpn-support-updates-for-ios---2459928-1819876-and-2650856---"></a>适用于 iOS 的新式 VPN 支持更新<!-- 2459928, 1819876, and 2650856 -->
此次更新添加了对以下 iOS VPN 客户端的支持：
- F5 Access（版本 3.0.1 及更高版本）
- Citrix SSO
- 此次更新还包含 Palo Alto Networks GlobalProtect 版本 5.0 及更高版本：
- iOS 的现有“F5 访问”连接类型已重命名为“旧版 F5 访问”   。
- iOS 的现有“Palo Alto Networks GlobalProtect”连接类型已重命名为“旧版 Palo Alto Networks GlobalProtect”   。
使用这些连接类型的现有配置文件将继续使用其各自的旧版 VPN 客户端。 如果要将 Cisco 旧式 AnyConnect、旧版 F5 访问、Citrix VPN 或 Palo Alto Networks GlobalProtect 4.1 及更早版本与 iOS 配合使用，则应改为使用新应用。 尽快执行此操作以确保可在更新到 iOS 12 的 iOS 设备上实现 VPN 访问。
有关 iOS 12 和 VPN 配置文件的详细信息，请参阅 [Microsoft Intune 支持团队博客](https://go.microsoft.com/fwlink/?linkid=2013806)。

#### <a name="export-azure-classic-portal-compliance-policies-to-recreate-these-policies-in-the-intune-azure-portal---2469637---"></a>导出 Azure 经典门户的符合性策略，以在 Intune Azure 门户中重新创建这些策略<!-- 2469637 -->
将弃用 Azure 经典门户中创建的符合性策略。 可查看和删除任何现有符合性策略，但无法更新它们。 如果需要将任何符合性策略迁移到最新的 Intune Azure 门户，可将策略导出为逗号分隔的文件（.csv 文件）  。 然后使用文件中的详细信息在 Intune Azure 门户中重新创建这些策略。

> [!IMPORTANT]
> Azure 经典门户停用后，将无法访问或查看符合性策略。 因此，在 Azure 经典门户停用之前，务必导出策略并在 Azure 门户中重新创建这些策略。

#### <a name="better-mobile---new-mobile-threat-defense-partner---22662717---"></a>Better Mobile - 新移动威胁防御合作伙伴<!-- 22662717 -->
可根据 Better Mobile 进行的风险评估，使用条件访问控制移动设备对公司资源的访问，Better Mobile 是与 Microsoft Intune 集成的移动威胁防御解决方案。

### <a name="device-enrollment"></a>设备注册

#### <a name="lock-the-company-portal-in-single-app-mode-until-user-sign-in--1067692---"></a>将公司门户锁定在单应用模式下，直至用户登录<!--1067692 --> 
如果在 DEP 注册过程中通过公司门户而非“设置助理”来对用户进行身份验证，那么现在可选择在单应用模式下运行公司门户。 此选项会在“设置助手”操作完成后立即锁定设备，这样用户须登录才能访问设备。 此过程可确保设备完成载入，且不会进入无任何用户绑定的孤立状态。

#### <a name="assign-a-user-and-friendly-name-to-an-autopilot-device--1346521---"></a>为 Autopilot 设备分配一个用户和友好名称<!--1346521 -->
现在可[将用户分配到单独的 Autopilot 设备](../enrollment/enrollment-autopilot.md)。 在使用 Autopilot 为用户设置设备时，管理员还可提供友好名称来问候用户。
适用于：最新的 [Windows 预览体验](https://docs.microsoft.com/windows-insider/at-work-pro/)版本（预览版）。

#### <a name="use-vpp-device-licenses-to-pre-provision-the-company-portal-during-dep-enrollment---1608345---"></a>在 DEP 注册期间，使用 VPP 设备许可证预设置公司门户<!-- 1608345 -->
现可在设备注册计划 (DEP) 注册期间，使用批量采购计划 (VPP) 设备许可证预先设置公司门户。 若要完成此操作，在[创建或编辑注册配置文件](../enrollment/device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile)时，指定要用于安装公司门户的 VPP 令牌。 请确保令牌没有过期，并且具有足够的公司门户应用许可证。 如果令牌过期或许可证用完，Intune 将改为推送 App Store 公司门户（这将提示输入 Apple ID）。

#### <a name="confirmation-required-to-delete-vpp-token-that-is-being-used-for-company-portal-pre-provisioning---2237634---"></a>需要确认才能删除正用于公司门户预设置的 VPP 令牌<!-- 2237634 -->
如果在 DEP 注册期间正在使用批量购买计划 (VPP) 预先设置公司门户，则现在需要确认是否删除此令牌。

#### <a name="block-windows-personal-device-enrollments---1849498---"></a>阻止 Windows 个人设备注册<!-- 1849498 -->
可通过 Intune 中的[移动设备管理](../enrollment/windows-enroll.md)[阻止 Windows 个人设备](../enrollment/enrollment-restrictions-set.md)进行注册。 无法使用此功能阻止注册了 [Intune PC 代理](manage-windows-pcs-with-microsoft-intune.md)的设备。 这一功能将在随后几周内推出，因此你可能无法立即在用户界面中看到此功能。

#### <a name="specify-machine-name-patterns-in-an-autopilot-profile--1849855--"></a>在 Autopilot 配置文件中指定计算机名称模式<!--1849855-->
可[指定一个计算机名称模板](../enrollment/enrollment-autopilot.md#create-an-autopilot-deployment-profile)，用于在 Autopilot 注册过程中生成和设置[计算机名](https://docs.microsoft.com/windows/client-management/mdm/accounts-csp)。 适用于：最新的 [Windows 预览体验](https://docs.microsoft.com/windows-insider/at-work-pro/)版本（预览版）。

#### <a name="for-windows-autopilot-profiles-hide-the-change-account-options-on-the-company-sign-in-page-and-domain-error-page--1901669---"></a>对于 Windows Autopilot 配置文件，隐藏公司登录页面和域错误页面上的“更改帐户”选项<!--1901669 -->
提供[新的 Windows Autopilot 配置文件选项](../enrollment/enrollment-autopilot.md#create-an-autopilot-deployment-profile)，允许管理员隐藏公司登录页和域错误页上的更改帐户选项。 要隐藏这些选项，需在 Azure Active Directory 中配置公司品牌。 适用于：最新的 [Windows 预览体验](https://docs.microsoft.com/windows-insider/at-work-pro/)版本（预览版）。

### <a name="macos-support-for-apple-device-enrollment-program---747651---"></a>Apple 设备注册计划支持注册 macOS 设备<!-- 747651 -->
Intune 现支持将 macOS 设备注册到 Apple 设备注册计划 (DEP) 中。 有关详细信息，请参阅[通过 Apple 设备注册计划自动注册 macOS 设备](../enrollment/device-enrollment-program-enroll-macos.md)。

### <a name="device-management"></a>设备管理

#### <a name="delete-jamf-devices---2653306--"></a>删除 Jamf 设备<!-- 2653306-->
通过转到“设备”>“选择 Jamf 设备”>“删除”，可以删除 JAMF 托管的设备   。

#### <a name="change-terminology-to-retire-and-wipe---2175759---"></a>将术语更改为“停用”和“擦除”<!-- 2175759 -->
为了与 Graph API 保持一致，Intune 用户界面和文档已更改以下术语：
- “删除公司数据”更改为“停用” 
- “恢复出厂设置”  将更改为“擦除” 

#### <a name="confirmation-dialog-if-admin-tries-to-delete-mdm-push-certificate---297909500--"></a>管理员尝试删除 MDM 推送证书时出现的确认对话框<!-- 297909500-->
如果有人尝试删除 Apple MDM 推送证书，确认对话框会显示相关的 iOS 和 macOS 设备数。 删除证书后，需要重新注册这些设备。

#### <a name="additional-security-settings-for-windows-installer---2282430---"></a>Windows Installer 的其他安全设置<!-- 2282430 -->
可允许用户控制应用安装。 如果启用，则允许因安全冲突而停止的安装继续进行。 当 Windows Installer 在系统上安装任何程序时，可指示它使用提升的权限。 此外，还可以对 Windows 信息保护 (WIP) 项目编制索引，并将有关这些项目的元数据存储在未加密的位置。 禁用策略后，不会索引受 WIP 保护的项，也不会在 Cortana 或文件资源管理器的结果中显示这些项。 默认情况下禁用这些选项的功能。 

#### <a name="new-user-experience-update-for-the-company-portal-website--2000968---"></a>公司门户网站的新用户体验更新<!--2000968 -->
我们已根据客户反馈向公司门户网站添加新功能。 可从设备上体验到现有功能和可用性的重大改进。 该网站的各个区域（如设备详细信息、反馈与支持以及设备概述）都采用了全新的现代化快速响应设计。 你还会看到：

- 简化了跨所有设备平台的工作流
- 改进了设备标识和注册流
- 更多有用的错误消息
- 更友好的语言，减少了专业技术性术语
- 能够共享指向应用的直接链接
- 改善了大型应用目录的性能
- 为所有用户增加了辅助功能  

已更新 [Intune 公司门户网站文档](https://docs.microsoft.com/user-help/using-the-intune-company-portal-website)以体现这些更改。 若要查看应用增强功能的示例，请参阅[Intune 最终用户应用的 UI 更新](whats-new-app-ui.md)。  

### <a name="monitor-and-troubleshoot"></a>监视和故障排除

#### <a name="enhanced-jailbreak-detection-in-compliance-reporting---2198738---"></a>相容性报告中的强化型越狱检测<!-- 2198738 -->
现在，强化型越狱检测设置状态将显示在管理员控制台中的所有符合性报告中。

### <a name="role-based-access-control"></a>基于角色的访问控制

#### <a name="scope-tags-for-policies--1081974---"></a>策略的作用域标记<!--1081974 -->
可[创建作用域标记](scope-tags.md)来限制对 Intune 资源的访问。 将作用域标记添加到某个角色分配，然后将作用域标记添加到某个配置文件。 角色将仅有权访问符合后列条件的资源：其资源配置文件的作用域标记与角色标记匹配或无作用域标记。





<!-- ########################## -->
## <a name="july-2018"></a>2018 年 7 月

### <a name="app-management"></a>应用管理

#### <a name="line-of-business-lob-app-support-for-macos---1895847---"></a>对 macOS 的业务线 (LOB) 应用支持<!-- 1895847 -->
Microsoft Intune 允许将 macOS LOB 应用部署为“必需”或“注册时可用”   。 最终用户可通过适用于 macOS 公司门户或[公司门户网站](https://portal.manage.microsoft.com)获得部署为“可用”的应用  。

#### <a name="ios-built-in-app-support-for-kiosk-mode---2051098---"></a>iOS 内置应用支持展台模式<!-- 2051098 -->
除了应用商店应用和托管应用，现在可以选择在 iOS 设备上以展台模式运行的内置应用（例如 Safari）。

#### <a name="edit-your-office-365-pro-plus-app-deployments---2150145---"></a>编辑 Office 365 Pro Plus 应用部署<!-- 2150145 -->
作为 Microsoft Intune 管理员，现在可以对 Office 365 专业增强版应用部署进行更多编辑。 此外，不再需要删除部署以更改任何套件属性。 在 Azure 门户中，选择“Microsoft Intune” > “客户端应用” > “应用”    。 从应用列表中选择你的 Office 365 Pro Plus 套件。  

#### <a name="updated-intune-app-sdk-for-android-is-now-available---2744271--"></a>现推出了更新的 Intune App SDK for Android<!-- 2744271-->
现在提供 Intune App SDK for Android 的更新版本，以支持 Android P 版本。 如果你是应用开发人员并使用 Intune SDK for Android，则必须安装 Intune app SDK 的更新版本，以确保 Android 应用中的 Intune 功能在 Android P 设备上运行正常。 此版本的 Intune App SDK 提供了一个内置插件来执行 SDK 更新。 你无需重写集成的任何现有代码。 有关详细信息，请参阅 [Intune SDK for Android](https://github.com/msintuneappsdk/ms-intune-app-sdk-android)。 如果你使用的是 Intune 的旧标记样式，我们建议你使用公文包图标。 有关品牌打造的详细信息，请参阅[此 GitHub 存储库](https://github.com/msintuneappsdk/intune-app-partner-badge)。

#### <a name="more-opportunities-to-sync-in-the-company-portal-app-for-windows"></a>更多在适用于 Windows 的公司门户应用中同步的机会  
适用于 Windows 的公司门户应用现在允许直接从 Windows 任务栏和“开始”菜单启动同步。 如果唯一任务是同步设备并访问公司资源，那么此功能特别有用。 要访问新功能，请右键单击固定到任务栏或“开始”菜单的公司门户图标。 在菜单选项（也称为跳转列表）中，选择“同步此设备”  。 公司门户将打开“设置”页面并启动同步  。若要了解新功能，请参阅 [UI 中的新增功能](whats-new-app-ui.md)。

#### <a name="new-browsing-experiences-in-the-company-portal-app-for-windows"></a>适用于 Windows 的公司门户应用中的全新浏览体验  
现在，在适用于 Windows 的公司门户应用中浏览或搜索应用时，用户能在现有的“磁贴”视图和新添加的“详细信息”视图之间切换   。 新视图列出应用程序详细信息，如名称、发布服务器、发布日期和安装状态。  

通过“应用”页的“已安装”视图，可查看有关已完成和进行中的应用安装的详细信息   。 若要查看新视图的外观，请参阅 [UI 中的新增功能](whats-new-app-ui.md)。  

#### <a name="improved-company-portal-app-experience-for-device-enrollment-managers"></a>针对设备注册管理员，改进了公司门户应用体验  
现在，当设备注册管理员 (DEM) 登录到适用于 Windows 的公司门户应用时，该应用将仅列出 DEM 当前正在运行的设备。 以前应用尝试显示所有 DEM 注册设备，会出现较长的超时，此改进则将减少超时时间。  

#### <a name="block-app-access-based-on-unapproved-device-vendors-and-models----1425689----"></a>基于未批准的设备供应商和型号阻止应用的访问 <!-- 1425689 ! -->
Intune IT 管理员可通过 Intune 应用保护策略强制实施指定的 Android 制造商和/或 iOS 型号列表。 IT 管理员可以提供适用于 Android 策略的供应商列表和适用于 iOS 策略的设备型号列表，列表以分号分隔。 Intune App 保护策略仅适用于 Android 和 iOS。 可针对此指定列表执行两个单独的操作：
- 阻止应用访问未指定的设备。
- 或者，选择性地擦除未指定的设备上的企业数据。 

如果未满足策略要求，则用户将无法访问目标应用程序。 根据设置，用户可能会被阻止或选择性地删除应用中的用户企业数据。 在 iOS 设备上，需使用一些应用程序（例如 WXP、Outlook、Managed Browser 和 Yammer）与 Intune APP SDK 进行集成，才能在目标应用程序中强制实施此功能。 此集成陆续进行，取决于特定应用程序团队。 在 Android 上，此功能需要使用最新的公司门户。 

在最终用户设备上，Intune 客户端将根据 Intune 边栏选项卡中针对应用程序保护策略所指定的字符串的简单匹配来执行操作。 这完全取决于设备报告的值。 为此，建议 IT 管理员确保预期行为的准确性。 这可以通过根据面向较小规模用户组的各种设备制造商和型号对此设置进行测试来实现。 在 Microsoft Intune 中，选择“客户端应用” > “应用保护策略”，可查看和添加应用保护策略   。 有关应用保护策略的详细信息，请参阅[什么是应用保护策略](../apps/app-protection-policy.md)和[在 Intune 中使用应用保护策略访问操作选择性地擦除数据](../apps/app-protection-policies-access-actions.md)。

#### <a name="access-to-macos-company-portal-pre-release-build---1734766---"></a>访问 macOS 公司门户预发布版本<!-- 1734766 -->
借助 Microsoft 自动更新，可通过加入预览体验计划注册抢先收到内部版本。 注册后，即可在公司门户更新版向最终用户推出前使用它。 有关详细信息，请参阅 [Microsoft Intune 博客](https://blogs.technet.microsoft.com/intunesupport/2018/07/13/use-microsoft-autoupdate-for-early-access-to-the-macos-company-portal-app/)。

### <a name="device-configuration"></a>设备配置

#### <a name="create-device-compliance-policy-using-firewall-settings-on-macos-devices---1497640---"></a>在 macOS 设备上使用防火墙设置创建设备合规性策略<!-- 1497640 -->
创建新的 macOS 符合性策略（“设备符合性” > “策略” > “创建策略” > “平台: macOS” > “系统安全性”）时，有一些新的可用“防火墙”设置       ： 

- **防火墙**：配置环境对传入连接的处理方式。
- **传入连接**：阻止  所有传入连接，DHCP、Bonjour 和 IPSec 等基本 Internet 服务需要的连接除外。 此设置还会阻止所有共享服务。
- **隐藏模式**：  启用隐藏模式以防止设备响应探测请求。 设备会继续回应已授权应用的传入请求。

适用于：macOS 10.12 及更高版本

#### <a name="new-wi-fi-device-configuration-profile-for-windows-10-and-later---1879077---"></a>Windows 10 及更高版本的新 Wi-Fi 设备配置文件<!-- 1879077 -->
目前，可以使用 XML 文件导入和导出 Wi-Fi 配置文件。 通过此次更新，能够直接在 Intune 中创建 Wi-Fi 设备配置文件，与在某些其他平台上的操作一样。

若要创建配置文件，打开“设备配置” > “配置文件” > “创建配置文件” > “Windows 10 及更高版本” > “Wi-Fi”      。 

适用于 Windows 10 和更高版本。

#### <a name="kiosk---obsolete-is-grayed-out-and-cant-be-changed---2149998---"></a>展台 - 已过时显示为灰色，无法更改<!-- 2149998 -->
展台（预览）功能（“设备配置” > “配置文件” > “创建配置文件” > “Windows 10 及更高版本” > “设备限制”）已过时，并替换为[适用于 Windows 10 和更高版本的展台设置](../configuration/kiosk-settings.md)      。 更新后，“展台 - 已过时”功能显示为灰色，并且无法更改或更新用户界面  。 

若要启用展台模式，请参阅 [Windows 10 及更高版本的 Kiosk 设置](../configuration/kiosk-settings.md)。

应用于 Windows 10 及更高版本、Windows Holographic for Business

#### <a name="apis-to-use-3rd-party-certification-authorities---2184013---"></a>使用第三方证书颁发机构的 API<!-- 2184013 -->
此更新中有一个 Java API，能实现第三方证书颁发机构与 Intune 和 SCEP 的集成。 然后用户可以将 SCEP 证书添加到配置文件，并使用 MDM 将其应用于设备。

目前 Intune 支持[使用 Active Directory 证书服务的 SCEP 请求](../protect/certificates-scep-configure.md)。

#### <a name="toggle-to-show-or-not-show-the-end-session-button-on-a-kiosk-browser---2455253---"></a>切换以显示或不显示展台浏览器上的“结束会话”按钮<!-- 2455253 -->
现可配置展台浏览器是否显示“结束会话”按钮。 可以在“设备配置” > “Kiosk（预览）” > “Kiosk Web 浏览器”中看到控件    。 若关闭，用户单击按钮时，应用会提示是否结束会话。 确定结束时，浏览器清除所有浏览数据并导航回到默认 URL。

#### <a name="create-an-esim-cellular-configuration-profile---2564077---"></a>创建 eSIM 卡移动电话配置文件<!-- 2564077 -->
在“设备配置”中，可创建 eSIM 手机网络配置文件  。 可以导入包含移动运营商提供的移动电话激活码的文件。 然后，可以将这些配置文件部署到支持 eSIM LTE 的 Windows 10 设备，例如 Surface Pro LTE 和其他支持 eSIM 卡的设备。

检查[设备是否支持 eSIM 卡配置文件](https://support.microsoft.com/help/4020763/windows-10-use-esim-for-cellular-data)。

适用于 Windows 10 和更高版本。

#### <a name="select-device-categories-by-using-the-access-work-or-school-settings---1058963-eenotready---"></a>使用“访问工作单位或学校”设置选择设备类别<!-- 1058963 eenotready --> 
如果已启用[设备组映射](../enrollment/device-group-mapping.md)，Windows 10 用户现将在通过“设置”   > “帐户”   > “访问工作或学校帐户”  中的“连接”  按钮注册后，看到选择设备类别的提示。 

#### <a name="use-samaccountname-as-the-account-username-for-email-profiles---1500307---"></a>使用 sAMAccountName 作为电子邮件配置文件的帐户用户名<!-- 1500307 -->
可使用本地“sAMAccountName”作为 Android、iOS 和 Windows 10 的电子邮件配置文件的帐户用户名  。 还可从 Azure Active Directory (Azure AD) 中的 `domain` 或 `ntdomain` 属性获取域。 或者，输入自定义静态域。

若要使用此功能，必须将本地 Active Directory 环境中的 `sAMAccountName` 属性同步到 Azure AD。

适用于 [Android](../configuration/email-settings-android.md)、[iOS](../configuration/email-settings-ios.md)、[Windows 10 及更高版本](../configuration/email-settings-windows-10.md)

#### <a name="see-device-configuration-profiles-in-conflict---1556983---"></a>查看冲突的设备配置文件<!-- 1556983 -->
“设备配置”中将显示现有配置文件列表  。 此更新中添加了新列，用于提供有冲突的配置文件的详细信息。 可选中冲突的行以查看存在冲突的设置和配置文件。 

可在[管理配置文件](../configuration/device-profile-monitor.md#view-conflicts)中查看详细信息。

#### <a name="new-status-for-devices-in-device-compliance---2308882---"></a>设备合规性中的设备新状态<!-- 2308882 -->
在“设备符合性” > “策略”>“选择策略”>“概述”中，添加以下新状态    ：
- 成功
- 错误
- 冲突
- 挂起
- 不适用 还显示了图像，展示其他平台的设备计数。 例如，如果正在查看 iOS 配置文件，则新磁贴会显示同时分配给到配置文件的非 iOS 设备数。 请参阅[设备符合性策略](../protect/compliance-policy-monitor.md#view-status-of-device-policies)。

#### <a name="device-compliance-supports-3rd-party-anti-virus-solutions---2325484---"></a>设备合规性支持第三方防病毒解决方案<!-- 2325484 -->
创建设备符合性策略（“设备符合性”   > “策略”   > “创建策略”   > “平台: Windows 10 及更高版本”   > “设置”   > “系统安全”  ）时，有以下新的 **[设备安全](../protect/compliance-policy-create-windows.md)** 选项： 
- **防病毒**：当设置为“必需”时，可以使用在 Windows 安全中心注册的防病毒解决方案（如 Symantec 和 Windows Defender）来检查符合性  。 
- **反间谍软件**：当设置为“必需”时，可以使用在 Windows 安全中心注册的反间谍软件解决方案（如 Symantec 和 Windows Defender）来检查符合性  。 

适用于：Windows 10 及更高版本 

### <a name="device-enrollment"></a>设备注册

#### <a name="automatically-mark-android-devices-enrolled-by-using-samsung-knox-mobile-enrollment-as-corporate---2404851---"></a>自动标记使用 Samsung Knox 移动注册为“公司”注册的 Android 设备。<!-- 2404851 -->
默认情况下，使用 Samsung Knox 移动注册的 Android 设备现在标记为“设备所有权”下的“公司”   。 使用 Knox 移动注册之前，不需要使用 IMEI 或序列号手动识别公司设备。

#### <a name="devices-without-profiles-column-in-the-list-of-enrollment-program-tokens---1853904---"></a>注册计划令牌列表中没有配置文件列的设备<!-- 1853904 -->
注册计划令牌列表中存在一个新列，显示未分配配置文件的设备数量。 这有助于管理员在将配置文件分发给用户之前，先为这些设备分配配置文件。 若要查看新列，请转到“设备注册” > “Apple 注册” > “注册计划令牌”    。

### <a name="device-management"></a>设备管理

#### <a name="bulk-delete-devices-on-devices-blade---1793693---"></a>在设备边栏选项卡上批量删除设备<!-- 1793693 -->
现在可在“设备”边栏选项卡上一次删除多个设备。 选择“设备” > “所有设备”>“选择要删除的设备”>“删除”    。 对于无法删除的设备，会出现警告。

#### <a name="google-name-changes-for-android-for-work-and-play-for-work--842873---"></a>Android for Work 和 Play for Work 的 Google 名称更改<!--842873 -->
Intune 已更新“Android for Work”术语，以反映 Google 品牌的更改。 不再使用术语“Android for Work”和“Play for Work”。 根据上下文使用不同的术语：
- “Android 企业”指整个现代 Android 管理堆栈。
- “工作配置文件”或“配置文件所有者”指使用工作配置文件管理的 BYOD 设备。
- “托管的 Google Play”指 Google 应用商店。

#### <a name="rules-for-removing-devices---1609459---"></a>删除设备的规则<!-- 1609459 -->
提供新规则，用于自动删除未在设置天数内进行签入的设备。 要查看新规则，请转到“Intune”窗格，依次选择“设备”和“设备清理规则”    。

#### <a name="corporate-owned-single-use-support-for-android-devices---1630973---"></a>支持公司拥有的单一用途 Android 设备<!-- 1630973 -->

Intune 现支持受到高度管控的锁定展台式 Android 设备。 这使管理员可以将设备的使用进一步锁定到单个应用或一小组应用，并阻止用户在设备上启用其他应用或执行其他操作。 若要设置 Android 展台，请转到 Intune >“设备注册” > “Android 注册” > “展台和任务设备注册”    。 有关详细信息，请参阅[设置 Android 企业展台设备的注册](../enrollment/android-kiosk-enroll.md)。

#### <a name="per-row-review-of-duplicate-corporate-device-identifiers-uploaded---2203794--"></a>逐行查看上传的重复公司设备标识符<!-- 2203794-->
上传企业 ID 时，Intune 现提供重复项列表，你可以选择替换或保留现有信息。 选择“设备注册” > “公司设备标识符” > “添加标识符”后，如果有重复项，将显示报告    。 

#### <a name="manually-add-corporate-device-identifiers---2203803---"></a>手动添加公司设备标识符<!-- 2203803 -->
现在可以手动添加公司设备 ID。 选择“设备注册” > “公司设备标识符” > “添加”    。 


<!-- ########################## -->
## <a name="june-2018"></a>2018 年 6 月

### <a name="app-management"></a>应用管理

#### <a name="microsoft-edge-mobile-support-for-intune-app-protection-policies---1817882---"></a>针对 Intune 应用保护策略的 Microsoft Edge 移动设备支持<!-- 1817882 -->
移动设备的 Microsoft Edge 浏览器现在支持在 Intune 中定义的应用保护策略。

#### <a name="retrieve-the-associated-app-user-model-id-aumid-for-microsoft-store-for-business-apps-in-kiosk-mode---1560077----"></a>在展台模式下检索适用于企业的 Microsoft Store 应用的关联应用用户模型 ID (AUMID)<!-- 1560077 ! -->
Intune 现在可以检索适用于企业的 Microsoft Store (WSfB) 应用的应用用户模型 ID，以改进展台配置文件的配置。

有关适用于企业的 Microsoft Store 应用的详细信息，请参阅[管理来自适用于企业的 Microsoft Store 应用](../apps/windows-store-for-business.md)。

#### <a name="new-company-portal-branding-page---1916370---"></a>新的公司门户品牌页<!-- 1916370 -->
公司门户品牌页拥有新的布局、消息和工具提示。


### <a name="device-configuration"></a>设备配置

#### <a name="pradeo---new-mobile-threat-defense-partner---1169249---"></a>Pradeo - 新移动威胁防御合作伙伴<!-- 1169249 -->
可根据 Pradeo 给出的风险评估，使用条件访问控制移动设备对公司资源的访问，Pradeo 是与 Microsoft Intune 集成的移动威胁防御解决方案。

#### <a name="use-fips-mode-with-the-ndes-certificate-connector---1333688---"></a>将 FIPS 模式用于 NDES 证书连接器<!-- 1333688 -->
在已启用美国联邦信息处理标准 (FIPS) 模式的计算机上安装 NDES 证书连接器时，颁发和吊销证书不能按预期工作。 在此更新中，NDES 证书连接器中包含 FIPS 支持。 

此更新还包括：

- NDES 证书连接器需要 .NET 4.5 Framework，Windows Server 2016 和 Windows Server 2012 R2 中自动包含此内容。 以前，.NET 3.5 Framework 是最低要求版本。
- NDES 证书连接器中包含 TLS 1.2 支持。 因此，如果已安装 NDES 证书连接器的服务器支持 TLS 1.2，则使用 TLS 1.2。 如果服务器不支持 TLS 1.2，则使用 TLS 1.1。 目前，TLS 1.1 用于设备和服务器之间的身份验证。

有关详细信息，请参阅[配置和使用 SCEP 证书](../protect/certificates-scep-configure.md)和[配置和使用 PKCS 证书](../protect/certficates-pfx-configure.md)。

#### <a name="support-for-palo-alto-networks-globalprotect-vpn-profiles---1333680----"></a>支持 Palo Alto Networks GlobalProtect VPN 配置文件<!-- 1333680 ! -->
通过此更新，可选择 Palo Alto Networks GlobalProtect 作为 Intune 中 VPN 配置文件的 VPN 连接类型（“设备配置” > “配置文件” > “创建配置文件” > “配置文件类型” > “VPN”）      。 在此版本中，支持以下平台： 

- iOS
- Windows 10

#### <a name="additions-to-local-device-security-options-settings---1403702---"></a>新增本地设备安全选项设置<!-- 1403702 -->
现在可以配置适用于 Windows 10 设备的其他本地设备安全选项设置。 其他设置在 Microsoft 网络客户端、Microsoft 网络服务器、网络访问和安全性和交互式登录的区域内可用。 创建 Windows 10 设备配置策略时，可以在终结点保护类别中查找这些设置。

#### <a name="enable-kiosk-mode-on-windows-10-devices---1560072----"></a>在 Windows 10 设备上启用展台模式<!-- 1560072 ! -->
在 Windows 10 设备上，可以创建配置文件并启用展台模式（“设备配置”   > “配置文件”   > “创建配置文件”   > “Windows 10”   > “设备限制”   > “展台”  ）。 在此更新中，“展台(预览版)”  设置被重命名为“展台(旧版)”  。 不再推荐使用“展台(旧版)”  ，但该版本在 7 月更新之前仍能正常使用。 “展台(旧版)”  被替换为新的“展台”  配置文件类型（“创建配置文件”   > “Windows 10”   > “展台(预览版)”  ），该类型将包含配置 Windows 10 RS4 和更高版本上的展台的设置。

适用于 Windows 10 和更高版本。

#### <a name="device-profile-graphical-user-chart-is-back---2160133---"></a>设备配置文件图形用户图表已恢复<!-- 2160133 -->
为了改进设备配置文件图形图表上显示的计数（“设备配置”   > “配置文件”  > 选择现有配置文件 >“概述”  ），图形用户图表曾被暂时删除。

在此更新中，图形用户图表得到恢复，并显示在 Azure 门户中。

### <a name="device-enrollment"></a>设备注册

#### <a name="support-for-windows-autopilot-enrollment-without-user-authentication---1165118---"></a>支持无需用户身份验证的 Windows Autopilot 注册<!-- 1165118 -->
Intune 现在支持无需用户身份验证的 Windows Autopilot 注册。 这是 Windows Autopilot 部署配置文件中的新选项，“Autopilot 部署模式”设置为“自部署”。  设备必须运行 Windows 10 Insider Preview 内部版本 17672 或更高版本并且具有 TPM 2.0 芯片，才能成功完成此类型的注册。 由于不需要用户身份验证，因此应仅将此选项分配给你具有物理控制权限的设备。

#### <a name="new-languageregion-setting-when-configuring-oobe-for-autopilot---1821766---"></a>配置 Autopilot 的 OOBE 时的新语言/区域设置<!-- 1821766 -->
在 Out of Box Experience 期间，会提供新的配置设置，以设置 Autopilot 配置文件的语言和区域。 要查看新设置，请选择“设备注册” > “Windows 注册” > “部署配置文件” > “创建配置文件” > “部署模式” = “自部署” > “默认配置”        。

#### <a name="new-setting-for-configuring-device-keyboard---1821768---"></a>配置设备键盘的新设置<!-- 1821768 -->
在 Out of Box Experience 期间，将提供新的设置，以配置 Autopilot 配置文件的键盘。 要查看新设置，请选择“设备注册” > “Windows 注册” > “部署配置文件” > “创建配置文件” > “部署模式” = “自部署” > “默认配置”        。

#### <a name="autopilot-profiles-moving-to-group-targeting---1877935---"></a>将 AutoPilot 配置文件移动到组目标<!-- 1877935 -->
AutoPilot 部署配置文件可以分配给包含 AutoPilot 设备的 Azure AD 组。

### <a name="device-management"></a>设备管理

#### <a name="set-compliance-by-device-location---851881----"></a>按设备位置设置合规性<!-- 851881 ! -->
在某些情况下，你可能想要将访问企业资源的权限限制到某个特定位置（该位置由网络连接定义）。 现在可以基于设备的 IP 地址来创建符合性策略（“设备符合性” > “位置”）   。 如果设备移动到 IP 范围以外，则该设备将无法访问企业资源。

适用于：Android 设备 6.0 及更高版本，并安装了最新的公司门户应用

#### <a name="prevent-consumer-apps-and-experiences-on-windows-10-enterprise-rs4-autopilot-devices---1621980---"></a>在 Windows 10 企业版 RS4 AutoPilot 设备上阻止使用者应用和体验<!-- 1621980 -->
你将能够阻止在 Windows 10 企业版 RS4 AutoPilot 设备上安装使用者应用和体验。 要查看此功能，请转到“Intune” > “设备配置” > “配置文件” > “创建配置文件” > “平台” = “Windows 10 或更高版本” > “配置文件类型” = “设备限制” > “配置” > “Windows 聚焦” > “使用者功能”            。 

#### <a name="uninstall-the-latest-from-windows-10-software-updates---1732948---"></a>从 Windows 10 软件更新中卸载最新版本<!-- 1732948 -->
如果发现 Windows 10 计算机上存在重大问题，则可以选择卸载（回滚）最新的功能更新或最新的质量更新。 卸载某功能或质量更新仅适用于设备所在的服务通道。 卸载将触发恢复 Windows 10 计算机上的先前更新的策略。 特别是对于功能更新，可以限制卸载最新版本的时间（2-60 天）。 要设置软件更新卸载选项，请从 Azure 门户中的“Microsoft Intune ”边栏选项卡中选择“软件更新”   。 然后，从“软件更新”边栏选项卡中选择“Windows 10 更新通道”   。 然后，可以从“概述”部分选择“卸载”选项   。

#### <a name="search-all-devices-for-imei-and-serial-number---1793685---"></a>搜索所有设备以获取 IMEI 和序列号<!-- 1793685 -->
现在可以在“所有设备”边栏选项卡上搜索 IMEI 和序列号（电子邮件、UPN、设备名称和管理名称仍然可用）。 在 Intune 中，选择“设备” > “所有设备”> 在搜索框中输入你的搜索   。

#### <a name="management-name-field-will-be-editable---1875989---"></a>管理名称字段将可编辑<!-- 1875989 -->
现在可以在设备的“属性”边栏选项卡上编辑管理名称字段  。 若要编辑此字段，请选择“设备”   > “所有设备”  > 选择设备 >“属性”  。 可以使用管理名称字段来唯一标识设备。

#### <a name="new-all-devices-filter-device-category---1878520---"></a>新的“所有设备”筛选器：设备类别<!-- 1878520 -->
现在可以按设备类别筛选“所有设备”列表  。 为此，请选择“设备” > “所有设备” > “筛选器” > “设备类别”     。

#### <a name="use-teamviewer-to-screen-share-ios-and-macos-devices---1985547---"></a>使用 TeamViewer 共享 iOS 和 MacOS 设备的屏幕<!-- 1985547 -->
管理员现在可以连接到 [TeamViewer](../remote-actions/teamviewer-support.md)，并启动与 iOS 和 macOS 设备之间的屏幕共享会话。 iPhone、iPad 和 macOS 用户可以与任何其他桌面或移动设备实时共享其屏幕。 

#### <a name="multiple-exchange-connector-support---2070451---"></a>多个 Exchange 连接器支持<!-- 2070451 -->
你不再受到每租户一个 Microsoft Intune Exchange Connector 的限制。 Intune 现在支持多个 Exchange Connector，你可以设置多个本地 Exchange 组织的 Intune 条件访问。

凭借 Intune 本地 Exchange 连接器，可以根据设备是否已在 Intune 中注册且是否符合 Intune 设备符合性策略来管理设备对本地 Exchange 邮箱的访问。 若要设置连接器，请从 Azure 门户下载 Intune 本地 Exchange 连接器，并将它安装在 Exchange 组织中的服务器上。 在 Microsoft Intune 仪表板上，选择“本地访问”，然后在“设置”下选择“Exchange ActiveSync 连接器”    。 下载 Exchange 本地连接器，并将它安装在 Exchange 组织中的服务器上。 由于你已经不再受到每租户一个 Exchange 连接器的限制，因此，如果拥有其他的 Exchange 组织，则可以按照此相同的过程为其他每个 Exchange 组织下载并安装连接器。

#### <a name="new-device-hardware-detail-ccid---2156657---"></a>新的设备硬件详细信息：CCID<!-- 2156657 -->
现在每台设备均包含芯片卡接口设备 (CCID) 信息。 要查看该信息，请选择“设备” > “所有设备”> 选择一台设备 >“硬件”> 在“网络详情”下查看     >

#### <a name="assign-all-users-and-all-devices-as-scope-groups---2196803---"></a>将所有用户和所有设备分配为范围组<!-- 2196803 -->
现在可以分配所有用户、所有设备，以及范围组中的所有用户和所有设备。 要执行此操作，请选择“Intune 角色” > “所有角色” > “策略和配置文件管理器” > “分配”> 选择一项分配 >“范围(组)”      。

#### <a name="udid-information-now-included-for-ios-and-macos-devices---2219806---"></a>现包括在 iOS 和 macOS 设备中的 UDID 信息<!-- 2219806 -->
要查看适用于 iOS 和 macOS 设备的唯一设备标识符 (UDID)，请转到“设备” > “所有设备”> 选择一台设备 >“硬件”    。 UDID 仅适用于公司设备（如“设备” > “所有设备”> 选择一台设备 >“属性” > “设备所有权”下的设置）     。

### <a name="intune-apps"></a>Intune 应用

#### <a name="improved-troubleshooting-for-app-installation---928990---"></a>改进了对应用安装的故障排除<!-- 928990 -->
在 Microsoft Intune MDM 托管的设备上，有时应用安装可能会失败。 当这些应用安装失败时，可能难以了解失败原因或解决此问题。 我们将发布我们的应用疑难解答功能的公共预览版。 你将在每个设备下注意到名为“托管应用”  的新节点。 该节点列出了通过 Intune MDM 提供的应用。 在该节点内，将看到应用安装状态的列表。 如果选择单个应用，将看到该特定应用的疑难解答视图。 在疑难解答视图中，将看到应用的端到端生命周期，例如，应用创建、修改、设为目标和提供给设备的时间。 此外，如果应用安装失败，将向你显示错误代码以及有有助于了解错误原因的消息。 

#### <a name="intune-app-protection-policies-and-microsoft-edge---1818968---"></a>Intune 应用保护策略和 Microsoft Edge<!-- 1818968 -->
面向移动设备（iOS 和 Android）的 Microsoft Edge 浏览器现支持 Microsoft Intune 应用保护策略。 在 Microsoft Edge 应用程序中使用其企业 Azure AD 帐户登录的 iOS 和 Android 设备用户将受 Intune 保护。 在 iOS 设备上，“需要使用托管浏览器获取 Web 内容”的策略允许用户在托管的 Microsoft Edge 中打开链接  。

<!-- ########################## -->
## <a name="may-2018"></a>2018 年 5 月

### <a name="app-management"></a>应用管理

#### <a name="configuring-your-app-protection-policies---2144597-part-2---"></a>配置应用保护策略<!-- 2144597 Part 2 -->

在 Azure 门户中，现在只需转到 Intune，而不是转到 Intune 应用保护服务边栏选项卡。 Intune 中现在只有一个应用保护策略位置。 请注意，所有应用保护策略都位于 Intune 中“移动应用”边栏选项卡上的“应用保护策略”下   。 此集成将有助于简化云管理。 请记住，Intune 中已具备所有应用保护策略，并且你可以修改先前配置的任何策略。 Intune 应用策略保护 (APP) 和条件访问 (CA) 策略现在位于“Microsoft Intune”边栏选项卡中“管理”部分的“条件访问”下，或“Azure Active Directory”边栏选项卡中“安全性”部分的“条件访问”下      。 有关修改条件访问策略的详细信息，请参阅 [Azure Active Directory 中的条件访问](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)。 有关其他信息，请参阅[应用保护策略是什么？](../apps/app-protection-policy.md)

### <a name="device-configuration"></a>设备配置

#### <a name="require-installation-of-policies-apps-certificate-and-network-profiles---1553555---"></a>需要安装策略、应用、证书和网络配置文件<!-- 1553555 -->
除非 Intune 在 AutoPilot 设备预配期间安装策略、应用、证书和网络配置文件，否则管理员可阻止最终用户访问 Windows 10 RS4 桌面。 有关详细信息，请参阅[设置注册状态页](../enrollment/windows-enrollment-status.md)。

### <a name="device-enrollment"></a>设备注册

#### <a name="samsung-knox-mobile-enrollment-support--1112863--"></a>Samsung Knox 移动注册支持<!--1112863-->
将 Intune 与 Samsung Knox 移动注册 (KME) 结合使用时，可以注册大量公司拥有的 Android 设备。 使用 WiFi 或移动电话网络的用户在第一次打开他们的设备时，只需几次点击即可进行注册。 在使用 Knox 部署应用时，可使用蓝牙或 NFC 注册设备。 有关详细信息，请参阅[使用 Samsung 的 Knox 移动注册自动注册 Android 设备](../enrollment/android-samsung-knox-mobile-enroll.md)。

### <a name="monitor-and-troubleshoot"></a>监视和故障排除 

#### <a name="requesting-help-in-the-company-portal-for-windows-10---1874137---"></a>在适用于 Windows 10 的公司门户中请求帮助<!-- 1874137 -->
当用户启动获取问题的帮助的工作流时，Windows 10 公司门户现在将直接向 Microsoft 发送应用日志。 这样一来，可以更为轻松地排除和解决向 Microsoft 提出的问题。

<!-- ########################## -->
## <a name="april-2018"></a>2018 年 4 月

### <a name="app-management"></a>应用管理

#### <a name="passcode-support-for-mam-pin-on-android---1438086---"></a>Android 上对 MAM PIN 的密码支持<!-- 1438086 -->

Intune 管理员能够设置应用程序启动要求以强制使用密码而不是数字 MAM PIN。 如果进行此配置，在访问启用 MAM 的应用程序前，用户需要在出现提示时设置并使用密码。 密码是至少包含一个特殊字符或大写/小写字母的数字 PIN。 Intune 对密码的支持与支持现有数字 PIN 类似，可通过管理员控制台设置最短长度并且允许重复字符和序列。 此功能需要最新版 Android 公司门户。 此功能已可应用于 iOS。

#### <a name="line-of-business-lob-app-support-for-macos---1473977---"></a>对 macOS 的业务线 (LOB) 应用支持<!-- 1473977 -->
Microsoft Intune 将提供从 Azure 门户安装 macOS LOB 应用的功能。 使用 GitHub 中提供的工具对 macOS LOB 应用进行预处理后，可以将该应用添加到 Intune。 在 Azure 门户的“Intune”边栏选项卡中，选择“客户端应用”   。 在“客户端应用”边栏选项卡上，选择“应用” > “添加”    。 在“添加应用”边栏选项卡，选择“业务线应用”   。 

#### <a name="built-in-all-users-and-all-devices-group-for-android-enterprise-work-profile-app-assignment---1813073---"></a>面向 Android Enterprise 工作配置文件应用分配的内置“所有用户”和“所有设备”组<!-- 1813073 -->
可以利用面向 Android Enterprise 工作配置文件应用分配的内置“所有用户”和“所有设备”组   。 有关详细信息，请参阅[在 Microsoft Intune 中包括和排除应用分配](../apps/apps-inc-exl-assignments.md)。

#### <a name="intune-will-reinstall-required-apps-that-are-uninstalled-by-users---1947010---"></a>Intune 将重新安装用户卸载的所需应用<!-- 1947010 -->
如果最终用户卸载所需应用，Intune 将在 24 小时内自动重新安装该应用，而不是等待 7 天的重新评估周期。

#### <a name="update-where-to-configure-your-app-protection-policies---2144597---"></a>更新配置应用保护策略的位置<!-- 2144597 -->

在 Microsoft Intune 服务的 Azure 门户中，我们将从“Intune 应用保护服务”  边栏选项卡暂时重定向到“移动应用”  边栏选项卡。 请注意，Intune 中“应用配置”下的“移动应用”  边栏选项卡已包括所有应用保护策略。 直接转到 Intune 即可，无需转到“Intune 应用保护”。 在 2018 年 4 月，我们将停止重定向并将完全删除“Intune 应用保护服务”  边栏选项卡，以便在 Intune 中只存在应用保护策略的一个位置。 

**这会对我产生哪些影响？**
此更改将同时影响 Intune 独立版客户和混合版（带 Configuration Manager 的 Intune）客户。 此集成将有助于简化云管理。

**我需要如何准备应对此项变化？**
请将 Intune  标记为收藏（而不是“Intune 应用保护服务”  边栏选项卡），并确保熟悉 Intune 的“移动应用”  边栏选项卡中的应用保护策略工作流。 我们将重定向一小段时间，然后删除“应用保护”  边栏选项卡。 请记住，Intune 中已具备所有应用保护策略，并且你可以修改任何条件访问策略。 有关修改条件访问策略的详细信息，请参阅 [Azure Active Directory 中的条件访问](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)。 有关其他信息，请参阅[应用保护策略是什么？](../apps/app-protection-policy.md) 

### <a name="device-configuration"></a>设备配置

#### <a name="device-profile-chart-and-status-list-show-all-devices-in-a-group---1449153---"></a>设备配置文件图表和状态列表将显示组中的所有设备<!-- 1449153 -->
配置设备配置文件（“设备配置” > “配置文件”）时，选择设备配置文件，如 iOS   。 将此配置文件分配到包括 iOS 设备和非 iOS 设备的组。 图形图表显示应用到 iOS 和非 iOS 设备的配置文件计数（“设备配置” > “配置文件”> 选择一个现有配置文件 >“概述”）     。 选择“概述”选项卡中的图形图表时，“设备状态”将列出组中的所有设备，而不仅仅是 iOS 设备   。 

此次更新后，图形图表（“设备配置”   > “配置文件”  >选择一个现有配置文件>“概述”  ）将仅显示特定设备配置文件的计数。 例如，如果配置设备配置文件应用于 iOS 设备，则图表仅列出 iOS 设备的计数。 选中图形图表并打开“设备状态”后，将仅列出 iOS 设备  。

当此更新正在进行时，用户图形图表将暂时删除。 

#### <a name="always-on-vpn-for-windows-10--1333666---"></a>适用于 Windows 10 的 Always On VPN<!--1333666 -->

目前，通过使用自定义虚拟专用网络 (VPN) 配置文件（使用 OMA-URI 创建），可在 Windows 10 设备上使用 [Always On](https://docs.microsoft.com/windows/security/identity-protection/vpn/vpn-auto-trigger-profile#always-on)。

此次更新后，管理员可以在 Azure 门户中的 Intune 中直接面向 Windows 10 VPN 配置文件启用 Always On。 Always On VPN 配置文件将在以下情况下自动连接：

- 用户登录其设备
- 设备上的网络发生更改
- 设备屏幕在关闭后重新打开

#### <a name="new-printer-settings-for-education-profiles---1308900---"></a>教育配置文件的新打印机设置<!-- 1308900 -->

对于教育配置文件，新的设置在“打印机”  类别下可用：“打印机”、“默认打印机”、“添加新的打印机”    。

#### <a name="show-caller-id-in-personal-profile---android-enterprise-work-profile--1098984---"></a>在个人资料中显示呼叫方 ID - Android Enterprise 工作配置文件<!--1098984 -->
在设备上使用个人资料时，最终用户可能不会看到工作联系人的呼叫方 ID 详细信息。 

进行此更新后，  “Android Enterprise” >   “设备限制” > “工作配置文件设置”  中将出现新设置：
- 在个人资料中显示工作联系人呼叫方 ID

启用（不配置）后，工作联系人的呼叫方详细信息将显示在个人资料中。 阻止后，工作联系人的呼叫方号码不会显示在个人资料中。 

适用于：Android OS v6.0 和更高版本的 Android 工作配置文件设备

#### <a name="new-windows-defender-credential-guard-settings-added-to-endpoint-protection-settings--1102252-----from-1802-and-1804--"></a>添加到 Endpoint Protection 设置的新 Windows Defender Credential Guard 设置<!--1102252 --><!--from 1802 and 1804-->

此次更新后，[Windows Defender Credential Guard](https://docs.microsoft.com/windows/access-protection/credential-guard/credential-guard)（“设备配置”   > “配置文件”   > “Endpoint Protection”  ）将包括以下设置： 

- **Windows Defender Credential Guard**：以基于虚拟化的安全性启用 Credential Guard。 启用此功能可帮助在下次同时启用“使用安全启动的平台安全级别”  和“基于虚拟化的安全性”  而重新启动时保护凭据。 选项包括：
  - **禁用**：如果之前已使用“无锁启用”  选项启用 Credential Guard，则会远程关闭 Credential Guard。

  - **使用 UEFI 锁启用**：可确保 Credential Guard 不能使用注册表项或使用组策略禁用。 若要使用此设置来禁用 Credential Guard，必须将组策略设置为“禁用”。 然后，与实际存在的用户一起，从每台计算机中删除安全功能。 这些步骤清除保留在 UEFI 中的配置。 只要 UEFI 配置仍然存在，Credential Guard 就会保持启用状态。

  - **无锁启用**：允许使用组策略远程禁用 Credential Guard。 使用此设置的设备必须至少在 Windows 10（版本 1511）上运行。

配置 Credential Guard 时，会自动启用以下相关技术： 

- **启用基于虚拟化的安全 (VBS)** ：在下次重新启动时打开基于虚拟化的安全 (VBS)。 基于虚拟化的安全性使用 Windows 虚拟机监控程序提供对安全服务的支持，并要求“安全启动”。
- **安全启动和直接内存访问 (DMA)** ：通过“安全启动”和直接内存访问启用 VBS。 DMA 保护需要硬件支持，并且仅在正确配置的设备上启用。 

#### <a name="use-a-custom-subject-name-on-scep-certificate---2064190---"></a>对 SCEP 证书使用自定义使用者名称<!-- 2064190 -->
可以使用“OnPremisesSamAccountName”  作为 SCEP 证书配置文件中自定义使用者的公用名称。 例如，你可以使用 `CN={OnPremisesSamAccountName})`。

#### <a name="block-camera-and-screen-captures-on-android-enterprise-work-profiles---1098977---"></a>在 Android Enterprise 工作配置文件上阻止照相机和屏幕捕获<!-- 1098977 -->
配置 Android 设备的设备限制时，可以阻止两个新属性： 
- 照相机：阻止访问设备上的所有照相机
- 屏幕捕获：阻止屏幕捕获，还会阻止在不具有安全视频输出的显示设备上显示内容

适用于 Android Enterprise 工作配置文件。

#### <a name="use-cisco-anyconnect-client-for-ios---1333708---"></a>对 iOS 使用 Cisco AnyConnect 客户端<!-- 1333708 -->

创建适用于 iOS 的新 VPN 配置文件时，现在有以下两个选项：Cisco AnyConnect 和 Cisco 旧式 AnyConnect   。 Cisco AnyConnect 配置文件支持 4.0.7x 和更新版本。 现有 iOS Cisco AnyConnect VPN 配置文件将被标记为“Cisco Legacy AnyConnect”  ，并将继续适用于 Cisco AnyConnect 4.0.5x 和较旧版本，如现在一样。

> [!NOTE]
> 此更改仅适用于 iOS。 将继续只提供一个适用于 Android、Android Enterprise 工作配置文件和 macOS 平台的 Cisco AnyConnect 选项。


### <a name="device-enrollment"></a>设备注册

#### <a name="new-enrollment-steps-for-users-on-devices-with-macos-high-sierra-10132--1734567---"></a>用户在使用 macOS High Sierra 10.13.2+ 的设备上的新注册步骤<!--1734567 -->
macOS High Sierra 10.13.2 引入了“用户批准的”MDM 注册的概念。 批准的注册将允许 Intune 管理某些安全敏感设置。 有关详细信息，请参阅此处的 Apple 支持文档： https://support.apple.com/HT208019 。

如果最终用户未打开“系统首选项”并手动批准，使用 macOS 公司门户注册的设备将被视为“未经用户批准”。 为此，macOS 公司门户现直接在注册过程末尾指示使用 macOS 10.13.2 及以上版本的用户手动批准注册。 Intune 管理员控制台将就注册设备的用户批准情况进行报告。

#### <a name="jamf-enrolled-macos-devices-can-now-register-with-intune---2370684---"></a>Jamf 注册的 macOS 设备现在可以使用 Intune 注册<!-- 2370684 -->
macOS 公司门户版本 1.3 和 1.4 未成功向 Intune 注册 Jamf 设备。 macOS 门户版本 1.4.2 可修复此问题。

#### <a name="updated-help-experience-in-company-portal-app-for-android---1631531---"></a>更新了适用于 Android 的公司门户应用的帮助体验<!-- 1631531 -->
我们更新了 Android 适用的公司门户应用中的帮助体验，使其符合 Android 平台的最佳做法。 现在如果在使用应用时遇到问题，用户可以点击“菜单” > “帮助”，然后进行以下操作   ：
- 将诊断日志上传到 Microsoft。
- 向公司支持人员发送内含问题描述和事件 ID 的电子邮件。  

如需查看更新后的帮助体验，请转到[使用电子邮件发送日志](../user-help/send-logs-to-your-it-admin-by-email-android.md)和[向 Microsoft 发送错误](../user-help/send-logs-to-microsoft-android.md)。


#### <a name="new-enrollment-failure-trend-chart-and-failure-reasons-table---1471783---"></a>新的注册失败趋势图表和失败原因表<!-- 1471783 -->
“注册概述”页中会显示注册失败趋势和前五个失败原因。 单击图表或表可查看详细信息，以查找故障排除建议和修正建议。


### <a name="device-management"></a>设备管理

#### <a name="advanced-threat-protection-atp-and-intune-are-fully-integrated---1629303---"></a>高级威胁防护 (ATP) 和 Intune 完全集成<!-- 1629303 -->

[高级威胁防护 (ATP)](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/dashboard-windows-defender-advanced-threat-protection) 显示 Windows 10 设备的风险级别。 在 Windows Defender 安全中心（ATP 门户）中，可以创建到 Microsoft Intune 的连接。 创建后，将使用 Intune 符合性策略确定可接受的威胁级别。 如果超出威胁级别，则 Azure Active Directory (AD) 条件访问策略可以阻止访问组织内的不同应用。

此功能使 ATP 能够扫描文件、检测威胁并报告 Windows 10 设备上的任何风险。

请参阅[在 Intune 中启用具有条件访问的 ATP](../protect/advanced-threat-protection.md)。

#### <a name="support-for-user-less-devices---1637553---"></a>对无用户设备的支持<!-- 1637553 -->
Intune 支持在无用户设备（如 Microsoft Surface Hub）上评估符合性的功能。 符合性策略可以面向特定设备。 这样可以确定不具有关联用户的设备的符合性（和不符合性）。

#### <a name="delete-autopilot-devices---1713650---"></a>删除 Autopilot 设备<!-- 1713650 -->
Intune 管理员可以[删除 AutoPilot 设备](../enrollment/enrollment-autopilot.md#delete-autopilot-devices)。

#### <a name="improved-device-deletion-experience--1832333---"></a>设备删除体验改进<!--1832333 -->
[删除 Intune 中的设备](../remote-actions/devices-wipe.md#delete-devices-from-the-intune-portal)前，将不再需要删除公司数据或将设备恢复出厂设置。

要感受新体验，请登录 Intune，选择“设备” > “所有设备”> 设备的名称 >“删除”    。

如果仍希望确认擦除/停用，可使用标准设备生命周期流程，即在“删除”前执行“删除公司数据”和“恢复出厂设置”    。 

#### <a name="play-sounds-on-ios-when-in-lost-mode---1947769---"></a>“丢失”模式下在 iOS 上播放声音<!-- 1947769 -->
当受监督的 iOS 设备处于移动设备管理 (MDM)[丢失模式](../remote-actions/device-lost-mode.md)时，可以[播放声音](../remote-actions/device-locate.md#activate-lost-mode-sound-alert-on-an-ios-device)（“设备”   > “所有设备”  >选择一个 iOS 设备 >“概述”   > “更多”  ）。 声音将持续播放，直到将该设备移除“丢失”模式或用户在该设备上禁用声音。 适用于 iOS 9.3 和更高版本的设备。

#### <a name="block-or-allow-web-results-in-searches-made-on-an-intune-device--1972804--"></a>阻止或允许在 Intune 设备上所执行的搜索中出现 Web 结果<!--1972804-->

管理员现在可以阻止在设备上所执行的搜索中出现 Web 结果。

#### <a name="improved-error-messaging-for-apple-mdm-push-certificate-upload-failure---2172331---"></a>针对 Apple MDM Push Certificate 上传失败的错误消息改进<!-- 2172331 -->

错误消息说明，续订现有 MDM 证书时必须使用相同 Apple ID。

#### <a name="test-the-company-portal-for-macos-on-virtual-machines---2216679---"></a>在虚拟机上测试适用于 macOS 的公司门户<!-- 2216679 -->

我们已发布可帮助 IT 管理员在 Parallels Desktop 和 VMware Fusion 虚拟机上测试适用于 macOS 的公司门户应用的指南。 有关详细信息，请参阅[注册用于测试的虚拟 macOS 计算机](../enrollment/macos-enroll.md#enroll-virtual-macos-machines-for-testing)。

### <a name="intune-apps"></a>Intune 应用

#### <a name="user-experience-update-for-the-company-portal-app-for-ios--1412866---"></a>iOS 版公司门户应用的用户体验更新<!--1412866 -->
我们已向 iOS 版公司门户应用发布用户体验主要更新。 此更新具有经过完全重新设计的视觉效果，包括现代化的外观。 我们保留了应用的功能，但提高了其可用性和可访问性。  

你还会看到：
- 对 iPhone X 的支持。
- 应用启动速度和响应加载速度更快，可节省用户时间。
- 可为用户提供最新状态信息的附加进度条。
- 改进了用户上传日志的方式，因此可在出现问题时更轻松地报告该问题。  

要查看更新的外观，请转到[应用 UI 中的新增功能](whats-new-app-ui.md)。

#### <a name="protect-on-premises-exchange-data-using-intune-app-and-ca---1056954---"></a>使用 Intune APP 和 CA 保护本地 Exchange 数据<!-- 1056954 -->
现在可以使用 Intune 应用策略保护 (APP) 和条件访问 (CA) 保护通过 Outlook Mobile 对本地 Exchange 数据的访问权限。 若要在 Azure 门户中添加或修改应用保护策略，请选择“Microsoft Intune” > “客户端应用” > “应用保护策略”    。 使用此功能之前，请确保满足[适用于 iOS 和 Android 的 Outlook 要求](https://technet.microsoft.com/library/mt846639(v=exchg.160).aspx)。


### <a name="user-interface"></a>用户界面

#### <a name="improved-device-tiles-in-the-windows-10-company-portal--2213364---"></a>改进了 Windows 10 公司门户中的设备磁贴<!--2213364 -->

更新后的磁贴更易于视力较差的用户使用，还可使屏幕阅读工具提供更好的性能。

#### <a name="send-diagnostic-reports-in-company-portal-app-for-macos---2216677---"></a>在适用于 macOS 的公司门户应用中发送诊断报告<!-- 2216677 -->
适用于 macOS 设备的公司门户应用已进行更新，改进了用户报告 Intune 相关错误的方式。 员工可从公司门户应用中：

- 将诊断报告直接上传给 Microsoft 开发人员团队。
- 通过电子邮件将事件 ID 发送给公司的 IT 支持团队。

有关详细信息，请参阅[发送 macOS 错误](../user-help/send-errors-macos.md)。

#### <a name="intune-adapts-to-fluent-design-system-in-the-company-portal-app-for-windows-10---1195010---"></a>Intune 适用于面向 Windows 10 的公司门户中的 Fluent Design System<!-- 1195010 -->
适用于 Windows 10 的 Intune 公司门户应用经已更新 [Fluent Design System 的导航窗格视图](https://docs.microsoft.com/windows/uwp/design/basics/navigation-basics)。 在这款应用旁边，你会注意到一个静态、垂直的所有顶级页面列表。 单击任意链接，可以快速查看页面并在其之间进行切换。 这是你将看到的众多更新中的第一个更新，是我们持续不断努力成果的一部分，以便在 Intune 中创造更具适应性、更能感同身受且更为熟悉的体验。 要查看更新的外观，请转到[应用 UI 中的新增功能](whats-new-app-ui.md)。

<!-- ########################## -->
## <a name="march-2018"></a>2018 年 3 月

### <a name="app-management"></a>应用管理

#### <a name="alerts-for-expiring-ios-line-of-business-lob-apps-for-microsoft-intune---748789---"></a>Microsoft Intune 适用的 iOS 业务线 (LOB) 应用即将过期的警报<!-- 748789 -->

在 Azure 门户中，Intune 将发出警报，通知某些 iOS 业务线应用即将过期。 上传新版本的 iOS 业务线应用后，Intune 会从应用列表删除过期通知。 此过期通知只适用于新上传的 iOS 业务线应用。 系统将在 iOS LOB 应用预配配置文件到期前 30 天显示警告。 过期后，警报会变为已过期。

#### <a name="customize-your-company-portal-themes-with-hex-codes--1049561---"></a>使用十六进制代码自定义公司门户主题<!--1049561 -->

可以使用十六进制代码自定义公司门户应用中的主题颜色。 输入十六进制代码时，Intune 会确定文本颜色，用于提供文本颜色和背景颜色之间的最大对比度。 可以在“客户端应用” > “公司门户”中预览文本颜色和公司徽标之间的颜色对比   。

### <a name="including-and-excluding-app-assignment-based-on-groups-for-android-enterprise---1813081---"></a>根据 Android Enterprise 组包括和排除应用分配<!-- 1813081 -->

Android Enterprise（以前称为 Android for Work）支持包含和排除组，但不支持预创建的“所有用户”和“所有设备”内置组   。 有关详细信息，请参阅[在 Microsoft Intune 中包括和排除应用分配](../apps/apps-inc-exl-assignments.md)。


### <a name="device-management"></a>设备管理

### <a name="export-all-devices-into-csv-files-in-ie-microsoft-edge-or-chrome---2258071---"></a>在 IE、Microsoft Edge 或 Chrome 中将所有设备导出到 CSV 文件中<!-- 2258071 -->
在“设备” > “所有设备”中，可以将设备“导出”为 CSV 格式的列表    。 设备数量 >10,000 台的 Internet Explorer (IE) 用户可以将其设备成功地导出到多个文件中。 每个文件中的设备数量最多为 10,000 台。

设备数量 >30,000 台的 Microsoft Edge 和 Chrome 用户可以将其设备成功地导出到多个文件中。 每个文件中的设备数量最多为 30,000 台。

[管理设备](../remote-actions/device-management.md)中对你管理的设备的用途进行了更详细的介绍。

#### <a name="new-security-enhancements-in-the-intune-service----1637539---"></a>Intune 服务中新的安全性增强功能 <!-- 1637539 -->   

我们在 Azure 中引入了 Intune 的切换键。Intune 独立客户可以使用它将未分配任何策略的设备视为“符合”（安全功能关闭时），或将这些设备视为“不符合”（安全功能开启时）   。 这样可以确保只在对设备符合性进行评估后才能访问资源。

不同的用户受此功能的影响不同，具体取决于其是否已分配有符合性策略。

- 如果是新帐户或现有帐户，且没有已分配符合性策略的任何设备，切换键将自动设置为“符合”  。 该功能在控制台中的默认设置为“关闭”。 对最终用户没有任何影响。
- 如果是现有帐户，且具有已分配符合性策略的设备，切换键将自动设置为“不符合”  。 三月版更新推出后，此功能的默认设置为“启用”。

如果通过条件访问 (CA) 使用符合性策略，且该功能已启用，CA 现在会阻止所有未分配至少 1 个符合性策略的设备。 除非向所有设备分配至少 1 个符合性策略，否则与这些设备关联的最终用户（以前允许访问电子邮件）会失去访问权限。   

请注意，尽管 Intune 服务三月更新版推出后，默认的切换状态会立即显示在 UI 中，但此切换状态不会立即强制执行。 我们将帐户设置为具有有效的切换键之前，你对切换键所作的任何更改都不会影响设备的符合性。 对帐户的设置完成时，我们将通过消息中心告知。 此操作可能会在 Intune 服务更新至三月版后几天内完成。

其他信息：[https://aka.ms/compliance_policies](https://aka.ms/compliance_policies) 

#### <a name="enhanced-jailbreak-detection---846515---"></a>增强型越狱检测<!-- 846515 -->

增强的越狱检测是一种新的符合性设置，能改善 Intune 评估已越狱设备的方式。 此设置会导致设备更频繁地与 Intune 进行确认，这会使用设备的位置服务并影响电池使用情况。

#### <a name="reset-passwords-for-android-o-devices---1238299---"></a>重置 Android O 设备的密码<!-- 1238299 -->
可以使用 Work 配置文件重置已注册的 Android 8.0 设备的密码。 将“重置密码”请求发送到 Android 8.0 设备时，它将针对当前用户设置新的设备解锁密码或托管的配置文件质询。 系统会发送该密码或质询并立即生效。

#### <a name="targeting-compliance-policies-to-devices-in-device-groups--1307012---"></a>将合规性策略目标定到设备组中的设备<!--1307012 -->

可以将用户组中的用户设为应用符合性策略的目标用户。 进行此更新后，可以将设备组中的设备设为应用符合性策略的目标设备。 目标设备组中的设备不会收到任何符合性操作。

#### <a name="new-management-name-column---1333586---"></a>新的管理名称列<!-- 1333586 -->
 设备边栏选项卡上提供一个名为“管理名称”的新列  。 这是基于以下公式按每设备分配的自动生成、不可编辑的名称：
- 所有设备的默认名称：<username><em><devicetype></em><enrollmenttimestamp>
- 对于批量添加的设备：<PackageId/ProfileId><em><DeviceType></em><EnrollmentTime>

在设备边栏选项卡中，这是可选列。 默认情况下此列不可用，只能通过列选择器使用。 设备名称不受此新列的影响。

#### <a name="ios-devices-are-prompted-for-a-pin-every-15-minutes--1550837---"></a>系统每 15 分钟提示一次 iOS 设备设置 PIN<!--1550837 -->
符合性或配置策略应用到 iOS 设备后，系统会每 15 分钟提示用户一次，要求设置 PIN。 设置 PIN 之前，系统会持续提示用户。

#### <a name="schedule-your-automatic-updates--1805514---"></a>安排自动更新<!--1805514 -->
Intune 使你能够使用 [Windows 更新通道设置](../protect/windows-update-for-business-configure.md)控制自动更新的安装。 进行此更新后，可以安排定期更新，包括每周更新、每日更新，甚至具体到某个时间更新。

#### <a name="use-fully-distinguished-name-as-subject-for-scep-certificate--2221763---"></a>将完全可分辨名称用作 SCEP 证书的使用者<!--2221763 -->
创建 SCEP 证书配置文件时，输入使用者名称。 进行此更新后，即可将完全可分辨名称用作使用者。 对于“使用者名称”，选择“自定义”，然后输入 `CN={{OnPrem_Distinguished_Name}}`   。 要使用 `{{OnPrem_Distinguished_Name}}` 变量，请务必使用 [Azure Active Directory (AD) 连接](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)将 `onpremisesdistingishedname` 用户属性同步到 Azure AD。

### <a name="device-configuration"></a>设备配置

#### <a name="enable-bluetooth-contact-sharing---android-for-work--1098983---"></a>启用蓝牙联系人共享 - Android for Work<!--1098983 -->
Android 默认禁止通过蓝牙设备同步工作配置文件中的联系人。 因此，工作配置文件联系人不会显示在蓝牙设备的主叫方 ID 中。

进行此更新后，“Android for Work” > “设备限制” > “Work 配置文件设置”中将出现新设置    ：
- 通过蓝牙共享联系人

Intune 管理员可以配置这些设置，启用共享。 将设备与显示免提的主叫方 ID 的车载蓝牙设备配对时，这非常有用。 启用时，显示工作配置文件联系人。 未启用时，不会显示工作配置文件联系人。

#### <a name="configure-gatekeeper-to-control-macos-app-download-source---1690459---"></a>配置网关守卫以控制 macOS 应用下载源<!-- 1690459 -->

可以配置网关守卫，通过控制可以下载应用的位置保护设备免受应用侵害。 你可以配置以下下载源：Mac 应用商店、Mac 应用商店和确定的开发人员或任何来源    。 还可以配置用户是否可以通过按住 Control 并单击以替代这些网关守卫控件来安装应用。

可以在“设备配置” -> “创建配置文件” -> “macOS” -> “终结点保护”下找到这些设置     。

#### <a name="configure-the-mac-application-firewall---1690461---"></a>配置 Mac 应用程序防火墙<!-- 1690461 -->

可以配置 Mac 应用程序防火墙。 可以使用此操作以基于每个应用程序来控制连接，而不是基于每个端口来进行控制。 这样一来，可以更轻松地获得防火墙保护的优势，还有助于防止不良应用控制为合法应用打开的网络端口。

可以在“设备配置” -> “创建配置文件” -> “macOS” -> “终结点保护”下找到此功能     。

启用防火墙设置后，即可使用两种策略来配置防火墙：

- 阻止所有传入连接

   可以阻止目标设备的所有传入连接。 如果选择进行此操作，系统会阻止所有应用的传入连接。

- 允许或阻止特定应用

   可以允许或阻止特定应用接收传入连接。 还可以启用隐藏模式，阻止对探测请求做出响应。

#### <a name="detailed-error-codes-and-messages---1376342---"></a>详细的错误代码和消息<!-- 1376342 -->

在“设备配置”中，可以查看更详细的错误代码和错误消息。 这一改进的报告显示了相关设置、这些设置的状态以及详细的故障排查信息。

##### <a name="more-information"></a>更多信息

- 阻止所有传入连接

   这将阻止所有共享服务（例如文件共享和屏幕共享）接收传入连接。 仍然允许接收传入连接的系统服务包括：
  - configd - 实现 DHCP 和其他网络配置服务
  - mDNSResponder - 实现 Bonjour
  - racoon - 实现 IPSec

    若要使用共享服务，请确保将“传入连接”设置为“未配置”（不“阻止”）    。

- 隐藏模式

   启用此选项可防止计算机对探测请求做出响应。 计算机仍然会响应授权应用的传入请求。 意外的请求将被忽略，如 ICMP (ping)。

#### <a name="disable-checks-on-device-restart--1805490---"></a>禁用设备重启检查<!--1805490 -->
Intune 使你可以控制[对软件更新的管理](../protect/windows-update-for-business-configure.md)。 进行此更新后，提供“重新启动检查”属性，并默认启用。 要跳过重启设备时出现的典型检查（如活动用户、电池水平等），请选择“跳过”。

#### <a name="new-windows-10-insider-preview-channels-available-for-deployment-rings---1746293---"></a>提供用于部署圈的新 Windows 10 Insider Preview 通道<!-- 1746293 -->
现在创建 Windows 10 部署圈时，可以选择是否选择以下 Windows 10 Insider Preview 服务通道：
- Windows 预览体验内部版本 - 快
- Windows 预览体验内部版本 - 慢
- 发布 Windows 预览体验内部版本 

有关这些通道的详细信息，请参阅[管理 Insider Preview 内部版本](https://insider.windows.com/en-us/for-business-getting-started/#explore)。
有关在 Intune 中创建部署通道的详细信息，请参阅[在 Intune 中管理软件更新](../protect/windows-update-for-business-configure.md)。

### <a name="new-windows-defender-exploit-guard-settings---1631893---"></a>新 Windows Defender 攻击防护设置<!-- 1631893 -->

现可提供六个新的“攻击面减少”设置和扩展的“受控文件夹访问权限: 文件夹保护”功能。 可以在以下位置找到这些设置：Device configuration\Profiles\
Create profile\Endpoint protection\Windows Defender Exploit Guard 中找到。

#### <a name="attack-surface-reduction"></a>攻击面减少

|设置名  |设置选项  |说明  |
|---------|---------|---------|
|高级勒索软件防护|启用、审核、未配置|使用激进的勒索软件防护。|
|标记从 Windows 本地安全机构子系统窃取的凭据|启用、审核、未配置|标记从 Windows 本地安全机构子系统 (lsass.exe) 窃取的凭据。|
|来自 PSExec 和 WMI 命令的进程创建|阻止、审核、未配置|阻止来自 PSExec 和 WMI 命令的进程创建。|
|从 USB 运行的不受信任和未签名的进程|阻止、审核、未配置|阻止从 USB 运行不受信任和未签名的进程。|
|不符合普及程度、年龄或信任列表条件的可执行文件|阻止、审核、未配置|阻止运行可执行文件，除非它们符合传播、年龄或受信任列表条件。|

#### <a name="controlled-folder-access"></a>受控文件夹访问权限

|              设置名               |                                                              设置选项                                                              | 说明 |
|-----------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|-------------|
| 文件夹保护（已实现） | 未配置、启用、仅审核（已实现）<br><br> <strong>新建</strong><br>阻止磁盘修改、审核磁盘修改 |             |

阻止不友好应用对文件和文件夹进行未经授权的更改。<br><br>**启用**：阻止不受信任的应用修改或删除受保护文件夹中的文件，以及阻止写入到磁盘扇区。<br><br>
**仅阻止磁盘修改**：<br>阻止不受信任的应用写入到磁盘扇区。 不受信任的应用仍可以修改或删除受保护文件夹中的文件。|

### <a name="intune-apps"></a>Intune 应用

### <a name="azure-active-directory-web-sites-can-require-the-intune-managed-browser-app-and-support-single-sign-on-for-the-managed-browser-public-preview---710595---"></a>Azure Active Directory 网站可能需要 Intune Managed Browser 应用，并且支持 Managed Browser（公共预览版）的单一登录<!-- 710595 -->

利用 Azure Active Directory (Azure AD)，现可在移动设备上将网站访问限制为仅可访问 Intune Managed Browser 应用。 在 Managed Browser 中，网站数据可保持安全并且独立于最终用户的个人数据。 此外，Managed Browser 支持受 Azure AD 保护的站点的单一登录功能。 通过登录 Managed Browser，或在设备上搭配使用 Managed Browser 和 Intune 管理的其他应用，用户无需输入凭据，Managed Browser 即可访问受 Azure AD 保护的公司站点。 此功能适用于 Outlook Web Access (OWA) 和 SharePoint Online 等站点，以及通过 Azure 应用代理访问的其他公司站点（如 Intranet 资源）。 有关详细信息，请参阅 [Azure Active Directory 条件访问中的访问控制](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-controls)。

#### <a name="company-portal-app-for-android-visual-updates--976944---"></a>适用于 Android 的公司门户应用的可视化更新<!--976944 -->

我们已更新适用于 Android 的公司门户应用以遵循 Android 的 [Material Design](https://material.io/)（材料设计）准则。 可以在[应用 UI 中的新增功能](whats-new-app-ui.md)一文中查看新图标的图像。

#### <a name="company-portal-enrollment-improved---1874230-eeready--"></a>改进的公司门户注册<!-- 1874230 eeready-->
在 Windows 10 内部版本 1703 和更高版本上使用公司门户注册设备的用户能够在不退出应用的情况下完成注册的第一步。
#### <a name="hololens-and-surface-hub-now-appear-in-device-lists--1725868---"></a>HoloLens 和 Surface Hub 现在会出现在设备列表中<!--1725868 -->
我们向适用于 Android 的公司门户应用添加了对显示已注册 Intune 的 HoloLens 和 Surface Hub 设备的支持。

#### <a name="custom-book-categories-for-volume-purchase-program-vpp-ebooks---1488911---"></a>批量采购计划 (VPP) 电子书的自定义书籍类别<!-- 1488911 -->
能够创建自定义电子书类别，然后将 VPP 电子书分配到自定义电子书类别。 最终用户即可以看到新建的电子书类别以及分配给该类别的书籍。 有关系详细信息，请参阅[使用 Microsoft Intune 管理批量购买的应用和书籍](../apps/vpp-apps.md)。  

#### <a name="support-changes-for-company-portal-app-for-windows-send-feedback-option---2070166---"></a>支持对 Windows 公司门户应用中的“发送反馈”选项进行更改<!-- 2070166 -->
从 2018 年 4 月 30 日起，Windows 公司门户应用中的“发送反馈”  选项将仅适用于运行 Windwos 10 周年更新 (1607) 和更高版本的设备。 当在以下版本中使用 Windows 公司门户应用时，将不再支持“发送反馈”选项：  
- Windows 10（1507 版本）  
- Windows 10（1511 版本）  
- Windows Phone 8.1

如果你的设备在 Windows 10 RS1 或更高版本上运行，请从应用商店下载最新版本的 Windows 公司门户应用。 如果你运行的是不受支持的版本，请继续使用以下渠道发送反馈：
- Windows 10 上的反馈中心应用
- 电子邮件 WinCPfeedback@microsoft.com  

#### <a name="new-windows-defender-application-guard-settings---1631890---"></a>新 Windows Defender 应用程序防护设置<!-- 1631890 -->

- **启用图形加速**：管理员可以为 Windows Defender 应用程序防护启用虚拟图形处理器。 此设置使 CPU 可以将图形呈现卸载到 vGPU。 这可以提升使用图形密集型网站或在容器中观看视频时的性能。

- **SaveFilestoHost**：管理员可以使文件从在容器中运行的 Microsoft Edge 传递到主机文件系统。 打开此选项后，用户可以从容器中的 Microsoft Edge 将文件下载到主机文件系统。

#### <a name="mam-protection-policies-targeted-based-on-management-state---1665993---"></a>根据管理状态设置 MAM 保护策略的适用对象<!-- 1665993 -->
你可以根据设备的管理状态设置 MAM 策略的适用对象：
- **Android 设备** - 可以让非托管设备、Intune 托管设备和 Intune 托管的 Android Enterprise 配置文件（以前称为 Android for Work）使用该策略。
- **iOS 设备** - 可以让非托管设备（仅限 MAM）或 Intune 托管设备使用该策略。

    > [!NOTE]
    > - 2018 年 4 月推出了此功能对 iOS 的支持。

有关详细信息，请参阅[根据设备管理状态设置应用保护策略的适用对象](../apps/app-protection-policies.md)。

#### <a name="improvements-to-the-language-in-the-company-portal-app-for-windows---1683758---"></a>改进了 Windows 适用的公司门户应用中的语言<!-- 1683758 -->
我们对 Windows 10 适用的公司门户中的语言进行了改进，使其更加用户友好，并且更适合你的公司。 如需查看新增功能的示例图片，请参阅[应用 UI 中的新增功能](whats-new-app-ui.md)。

#### <a name="new-additions-to-our-docs-about-user-privacy---1440709---"></a>新增了一些有关用户隐私的文档<!-- 1440709 -->
我们一直在努力增强用户对其数据和隐私的控制权，作为此工作的一部分，我们更新了一些文档，在其中介绍了如何通过公司门户应用查看和删除存储在本地的数据。 了解这些更新的方式如下：

- **Android**：[如何从 Intune 删除 Android 设备](../user-help/unenroll-your-device-from-intune-android.md)
- **Android（如果用户拒绝了使用条款）** ：[拒绝“使用条款”后删除对设备的管理](../user-help/unenroll-your-device-from-intune-if-you-declined-terms-of-use-android.md)
- **iOS**：[从 Intune 删除 iOS 设备](../user-help/unenroll-your-device-from-intune-ios.md)
- **Windows**：[从 Intune 删除 Windows 设备](../user-help/unenroll-your-device-from-intune-windows.md)

<!-- ########################## -->
## <a name="february-2018"></a>2018 年 2 月

### <a name="device-enrollment"></a>设备注册

#### <a name="intune-support-for-multiple-apple-dep--apple-school-manager-accounts---747685---"></a>Intune 支持多个 Apple DEP/Apple School Manager 帐户<!-- 747685 -->

Intune 现支持最多通过 100 个不同的 [Apple 设备注册计划 (DEP)](../enrollment/device-enrollment-program-enroll-ios.md) 或 [Apple School Manager](../enrollment/apple-school-manager-set-up-ios.md) 帐户注册设备。 可以单独管理注册配置文件和设备的每个已上传令牌。 可以根据已上传的 DEP/ School Manager 令牌自动分配不同的注册配置文件。 如果上传了多个 School Manager 令牌，一次只能与 Microsoft 学校数据同步共享一个令牌。

迁移后，通过 Graph 管理 Apple DEP 或 ASM 的 beta 版本 Graph API 和已发布脚本将不再有效。 新的 beta 版本 Graph API 正在进行开发，将在迁移后发布。

#### <a name="see-enrollment-restrictions-per-user---1634444-eeready-wnready---"></a>请参阅每个用户的注册限制<!-- 1634444 eeready wnready -->
在“故障排除”边栏选项卡上，现可通过选择“分配”列表中的“注册限制”，查看对每个用户有效的[注册限制](../enrollment/enrollment-restrictions-set.md)    。

#### <a name="new-option-for-user-authentication-for-apple-bulk-enrollment---747625-eeready---"></a>新增了 Apple 批量注册所需的用户身份验证选项<!-- 747625 eeready -->

> [!NOTE]
> 新租户可立即查看此功能。 对于现有租户，此功能将于四月推出。 此次推出完成之前，你可能无权访问这些新功能。

对于以下注册方法，Intune 现支持使用“公司门户”应用验证设备：

- Apple 设备注册计划
- Apple School Manager
- Apple Configurator 注册

使用“公司门户”选项时，可以强制执行 Azure Active Directory 多重身份验证，而不会屏蔽这些注册方法。

使用“公司门户”选项时，Intune 会跳过 iOS 设置助理中用于用户关联注册的用户身份验证。 也就是说，设备最初注册为无用户设备，因此不会接收用户组的配置或策略。 只会接收设备组的配置和策略。 不过，Intune 会在设备上自动安装“公司门户”应用。 首个启动并登录“公司门户”应用的用户将与 Intune 中的设备相关联。 此时，用户将会接收用户组的配置和策略。 只有重新注册，才能更改用户关联。

#### <a name="intune-support-for-multiple-apple-dep--apple-school-manager-accounts---747685-eeready---"></a>Intune 支持多个 Apple DEP/Apple School Manager 帐户<!-- 747685 eeready -->

Intune 现支持最多通过 100 个不同的 Apple 设备注册计划 (DEP) 或 Apple School Manager 帐户注册设备。 可以单独管理注册配置文件和设备的每个已上传令牌。 可以根据已上传的 DEP/ School Manager 令牌自动分配不同的注册配置文件。 如果上传了多个 School Manager 令牌，一次只能与 Microsoft 学校数据同步共享一个令牌。

迁移后，通过 Graph 管理 Apple DEP 或 ASM 的 beta 版本 Graph API 和已发布脚本将不再有效。 新的 beta 版本 Graph API 正在进行开发，将在迁移后发布。

### <a name="remote-printing-over-a-secure-network---1709994----"></a>通过安全网络远程打印<!-- 1709994  -->
使用 PrinterOn 的无线移动打印解决方案，用户将可以随时随地通过安全网络进行远程打印。 PrinterOn 将集成适用于 iOS 和 Android 的 Intune APP SDK。 将可以通过管理控制台中的 Intune“应用保护策略”  边栏选项卡，将应用保护策略定目标到此应用。 最终用户将能够通过 Play 商店或 iTunes 下载“PrinterOn for Microsoft”应用，以便在 Intune 生态系统内使用。

### <a name="macos-company-portal-support-for-enrollments-that-use-the-device-enrollment-manager---1352411---"></a>对使用设备注册管理器的注册的 macOS 公司门户支持<!-- 1352411 -->

用户现在能够在注册 macOS 公司门户时使用设备注册管理员。

### <a name="device-management"></a>设备管理

#### <a name="windows-defender-health-status-and-threat-status-reports--854704---"></a>Windows Defender 运行状况状态和威胁状态报告<!--854704 -->

了解 Windows Defender 的运行状况和状态是管理 Windows 电脑的关键。  通过此更新，Intune 向 Windows Defender 代理的状态和健康状况添加新的报告和操作。 通过使用[设备符合性工作负载](../protect/compliance-policy-monitor.md)中的状态汇总报告，可以看到需要以下任一项的设备：
- 签名更新
- 重启
- 手动干预
- 完全扫描
- 需要干预的其他代理状态

每个状态类别的深入报告列出需要注意的各个电脑，或者报告为“清理”的电脑  。

#### <a name="new-privacy-settings-for-device-restrictions--1308926---"></a>设备限制的新隐私设置<!--1308926 -->
现在将为设备提供[两个新的隐私设置](../configuration/device-restrictions-windows-10.md#privacy)：
- **发布用户活动**：将此设置为“阻止”可阻止任务切换程序中最近使用资源的共享体验和发现  。
- **仅限本地活动**：将此设置为“阻止”可仅基于本地活动阻止任务切换程序中最近使用资源的共享体验和发现  。

#### <a name="new-settings-for-the-microsoft-edge-browser--1469166---"></a>Microsoft Edge 浏览器的新设置<!--1469166 -->
现在将为具有 Microsoft Edge 浏览器的设备提供[两个新设置](../configuration/device-restrictions-windows-10.md#microsoft-edge-browser)：“到收藏夹文件的路径”和“对收藏夹的更改”   。

### <a name="app-management"></a>应用管理

#### <a name="protocol-exceptions-for-applications--1035509---"></a>应用程序的协议异常<!--1035509 -->

现在可以为 Intune 移动应用程序管理 (MAM) 数据传输策略创建例外情况以打开特定的非托管应用程序。 此类应用程序必须受到 IT 的信任。 除创建的例外情况外，当数据传输策略设置为“仅限托管应用”时，数据传输仍仅限于由 Intune 托管的应用程序  。 可以使用协议 (iOS) 或包 (Android) 创建限制。

例如，可以将 Webex 包作为异常添加到 MAM 数据传输策略。 这样使托管 Outlook 电子邮件消息中的 Webex 链接可以直接在 Webex 应用程序中打开。 其他非托管的应用程序中将继续限制数据传输。 有关详细信息，请参阅[应用的数据传输策略例外情况](../apps/app-protection-policies-exception.md)。

#### <a name="windows-information-protection-wip-encrypted-data-in-windows-search-results---1469193---"></a>Windows 搜索结果中的 Windows 信息保护 (WIP) 加密数据<!-- 1469193 -->
借助 Windows 信息保护 (WIP) 策略中的设置，现在可以控制是否在 Windows 搜索结果中包含 WIP 加密数据。 通过在 Windows 信息保护策略的“高级设置”中选择“允许 Windows Search 索引器搜索加密项”设置此应用保护策略选项   。 应用保护策略必须设置为 Windows 10 平台，应用策略“注册状态”必须设置为“已注册”    。 有关详细信息，请参阅[允许 Windows Search 索引器搜索加密项](../apps/windows-information-protection-policy-create.md#allow-windows-search-indexer-to-search-encrypted-items)。

#### <a name="configuring-a-self-updating-mobile-msi-app---1740840---"></a>配置自我更新的移动 MSI 应用<!-- 1740840 -->
可以配置已知的自我更新移动 MSI 应用以忽略版本检查过程。 此功能有助于避免出现争用条件。 例如，在应用是由应用开发者自动更新并且也由 Intune 更新时，可能会出现此类争用条件。 两者都可能在 Windows 客户端上尝试强制执行一个应用版本，这可能会产生冲突。 对于这些自动更新的 MSI 应用，可以在“应用信息”边栏选项卡中配置“忽略应用版本”设置   。 当此设置切换为“是”时，Microsoft Intune 将会忽略在 Windows 客户端上安装的应用版本  。

#### <a name="related-sets-of-app-licenses-supported-in-intune---1864117---"></a>Intune 中支持的应用许可证的相关集<!-- 1864117 -->
Azure 门户中的 Intune 现在支持应用许可证的相关集，以作为 UI 中的单个应用项。 此外，任何从适用于企业的 Microsoft Store 同步的脱机许可的应用都将合并到单个应用条目中，并且各个包中的任何部署详细信息都将迁移到单个条目中。 若要在 Azure 门户中查看相关的应用许可证集，请从“客户端应用”边栏选项卡中选择“应用许可证”   。

### <a name="device-configuration"></a>设备配置
#### <a name="windows-information-protection-wip-file-extensions-for-automatic-encryption---1463582---"></a>自动加密的 Windows 信息保护 (WIP) 文件扩展名<!-- 1463582 -->
Windows 信息保护 (WIP) 策略中的设置现在允许按照 WIP 策略中的定义，在从公司边界内的服务器消息块 (SMB) 共享进行复制时，指定自动加密哪些文件扩展名。

#### <a name="configure-resource-account-settings-for-surface-hubs"></a>为 Surface Hub 配置资源帐户设置

现在可以为 Surface Hub 远程配置资源帐户设置。

资源帐户由 Surface Hub 用于对 Skype/Exchange 进行身份验证，以便它可以加入会议。
需要创建一个唯一的资源帐户，以使 Surface Hub 可以作为会议室出现在会议中。
例如“会议室 B41/6233”等资源帐户  。

> [!NOTE]
> - 如果将字段留空，则将替代之前在设备上配置的特性。
>
> - 资源帐户属性可以在 Surface Hub 上动态变化。 例如，在启用密码轮转的情况下。 所以，Azure 控制台中的值可能需要一些时间才能反映设备上的实际情况。
>
>   若要了解 Surface Hub 上当前配置的内容，可以将资源帐户信息包括在硬件清单中（已有 7 天的间隔时间）或者作为只读属性包括。 若要在远程操作发生后增强准确性，可以在运行操作以更新 Surface Hub 上的帐户/参数后立即获取参数的状态。

##### <a name="attack-surface-reduction"></a>攻击面减少

|设置名  |设置选项  |说明  |
|---------|---------|---------|
|从电子邮件中执行受密码保护的可执行内容|阻止、审核、未配置|防止运行通过电子邮件下载的受密码保护的可执行文件。|
|高级勒索软件防护|启用、审核、未配置|使用激进的勒索软件防护。|
|标记从 Windows 本地安全机构子系统窃取的凭据|启用、审核、未配置|标记从 Windows 本地安全机构子系统 (lsass.exe) 窃取的凭据。|
|来自 PSExec 和 WMI 命令的进程创建|阻止、审核、未配置|阻止来自 PSExec 和 WMI 命令的进程创建。|
|从 USB 运行的不受信任和未签名的进程|阻止、审核、未配置|阻止从 USB 运行不受信任和未签名的进程。|
|不符合普及程度、年龄或信任列表条件的可执行文件|阻止、审核、未配置|阻止运行可执行文件，除非它们符合传播、年龄或受信任列表条件。|

##### <a name="controlled-folder-access"></a>受控文件夹访问权限

|              设置名               |                                                              设置选项                                                              | 说明 |
|-----------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|-------------|
| 文件夹保护（已实现） | 未配置、启用、仅审核（已实现）<br><br> <strong>新建</strong><br>阻止磁盘修改、审核磁盘修改 |             |

阻止不友好应用对文件和文件夹进行未经授权的更改。<br><br>**启用**：阻止不受信任的应用修改或删除受保护文件夹中的文件，以及阻止写入到磁盘扇区。<br><br>
**仅阻止磁盘修改**：<br>阻止不受信任的应用写入到磁盘扇区。 不受信任的应用仍可以修改或删除受保护文件夹中的文件。|

#### <a name="additions-to-system-security-settings-for-windows-10-and-later-compliance-policies--1704133--"></a>新增适用于 Windows 10 及更高版本合规性策略的系统安全设置<!--1704133-->

现在提供对 Windows 10 符合性设置的添加，包括需要防火墙和 Windows Defender 防病毒。

### <a name="intune-apps"></a>Intune 应用

#### <a name="support-for-offline-apps-from-the-microsoft-store-for-business--1222672--"></a>支持适用于企业的 Microsoft Store 中的脱机应用<!--1222672-->
从适用于企业的 Microsoft Store 购买的脱机应用现在已同步到 Azure 门户。 可以将这些应用部署到设备组或用户组。 这些脱机应用由 Intune 安装，而不是由应用商店安装。

#### <a name="prevent-end-users-from-manually-adding-or-removing-accounts-in-the-work-profile---1728700---"></a>防止最终用户手动添加或删除工作配置文件中的帐户<!-- 1728700 -->

将 Gmail 应用部署到 Android for Work 配置文件中后，现在可防止最终用户通过使用 Android for Work 设备限制配置文件中的“添加和删除帐户”设置手动添加或删除工作配置文件中的帐户  。

<!-- ########################## -->
## <a name="january-2018"></a>2018 年 1 月

### <a name="device-enrollment"></a>设备注册

#### <a name="alerts-for-expired-tokens-and-tokens-that-will-soon-expire---1639263---"></a>已到期令牌和即将到期令牌的警报<!-- 1639263 -->
概述页现在显示已到期令牌和即将到期令牌的警报。 单击一个令牌的警报后，将转到令牌的详细信息页。  如果单击多个令牌的警报，将转到所有令牌及其状态的列表。 管理员应在到期日期之前续订令牌。

### <a name="device-management"></a>设备管理

#### <a name="remote-erase-command-support-for-macos-devices---1438084---"></a>macOS 设备的远程“清除”命令支持<!-- 1438084 -->

管理员可以对 macOS 设备远程发出清除命令。

> [!IMPORTANT]
> 由于清除命令无法撤消，因此应谨慎使用。

清除命令不仅会从设备中删除所有数据（包括操作系统）， 还会从 Intune 管理范围中删除设备。 不过，并不会向用户发出警告，而是在命令发出后立即执行清除操作。

必须配置 6 位恢复 PIN。 此 PIN 可用于解锁已清除的设备，此时将开始重新安装操作系统。 开始清除后，PIN 便会显示在 Intune 中设备概述边栏选项卡上的状态栏中。 只要清除正在进行中，PIN 就会一直显示。 清除完成后，设备便会从 Intune 管理范围中完全消失。 请务必记录恢复 PIN。这样一来，无论是谁恢复设备，都可以使用它。

#### <a name="revoke-licenses-for-an-ios-volume-purchasing-program-token---820870---"></a>撤销 iOS 批量采购计划令牌的许可证<!-- 820870 -->
可以撤销给定 VPP 令牌的所有 iOS 批量采购计划 (VPP) 应用的许可证。

### <a name="app-management"></a>应用管理

#### <a name="revoking-ios-volume-purchase-program-apps----820863---"></a>撤销 iOS 批量采购计划应用 <!-- 820863 -->
对于具有一个或多个 iOS 批量采购计划 (VPP) 应用的给定设备，可以撤销相关的基于设备的应用许可证。 撤销应用许可证将不会从设备中卸载相关的 VPP 应用。 若要卸载 VPP 应用，必须将分配操作更改为“卸载”  。 有关详细信息，请参阅[如何使用 Microsoft Intune 管理通过批量采购计划购买的 iOS 应用](../apps/vpp-apps-ios.md)。

#### <a name="assign-office-365-mobile-apps-to-ios-and-android-devices-using-built-in-app-type---1332318---"></a>使用内置应用类型将 Office 365 移动应用分配到 iOS 和 Android 设备<!-- 1332318 -->
借助内置应用类型，可更轻松地创建 Office 365 应用并将其分配到管理的 iOS 和 Android 设备  。 这些应用包括 Word、Excel、PowerPoint 和 OneDrive 等 Office 365 应用。 可将特定应用分配到应用类型并编辑应用信息配置。

#### <a name="including-and-excluding-app-assignment-based-on-groups---1406920---"></a>根据组添加和排除应用分配<!-- 1406920 -->

在应用分配期间以及在选择分配类型后，可以选择要包括和排除的组。

### <a name="device-configuration"></a>设备配置

#### <a name="you-can-assign-an-application-configuration-policy-to-groups-by-including-and-excluding-assignments----1480316---"></a>可通过包括和排除分配来向组分配应用程序配置策略 <!-- 1480316 -->

可通过结合使用包括分配和排除分配来向一组用户和设备分配应用程序配置策略。 可通过自定义选择组或虚拟组的方式来选择分配。 虚拟组包括“所有用户”、“所有设备”或“所有用户 + 所有设备”    。

#### <a name="support-for-windows-10-edition-upgrade-policy-----903672archived-1119689---"></a>支持 Windows 10 版本升级策略  <!-- 903672(archived), 1119689 -->  
可以创建 Windows 10 版本升级策略，将 Windows 10 设备升级到 Windows 10 教育版、Windows 10 教育版 N、Windows 10 专业版、Windows 10 专业版 N、Windows 10 专业教育版和 Windows 10 专业教育版 N。有关 Windows 10 版本升级的详细信息，请参阅[如何配置 Windows 10 版本升级](../configuration/edition-upgrade-configure-windows-10.md)。

#### <a name="conditional-access-policies-for-intune-is-only-available-from-the-azure-portal----1737088-1634311---"></a>适用于 Intune 的条件访问策略只能通过 Azure 门户访问 <!-- 1737088 1634311 -->

从此版本开始，必须配置和管理 [Azure 门户](https://portal.azure.com)中的条件访问策略（“Azure Active Directory”   > “条件访问”  ）。 为方便起见，也可以通过 Azure 门户中的“Intune”   >   “条件访问”，从 Intune 访问此边栏选项卡。

#### <a name="updates-to-compliance-emails--1637547---"></a>更新了合规性电子邮件<!--1637547 -->

发送电子邮件以报告不符合设备时，会包括不符合设备的详细信息。

### <a name="intune-apps"></a>Intune 应用

#### <a name="new-functionality-for-the-resolve-action-for-android-devices--1583480--"></a>Android 设备的“解决”操作的新功能<!--1583480-->

适用于 Android 的公司门户应用正在展开更新设备设置的“解决”  操作，从而解决[设备加密问题](../user-help/encrypt-your-device-android.md)。

#### <a name="remote-lock-available-in-company-portal-app-for-windows-10--676506--"></a>适用于 Windows 10 的公司门户应用中提供远程锁定<!--676506-->
最终用户现在可以从适用于 Windows 10 的公司门户应用远程锁定他们的设备。 此功能将不会为他们当前使用的本地设备显示。

#### <a name="easier-resolution-of-compliance-issues-for-the-company-portal-app-for-windows-10--676546--"></a>可以更轻松地解决适用于 Windows 10 的“公司门户”应用的合规性问题<!--676546-->
使用 Windows 设备的最终用户将能够点击“公司门户”应用中的不符合原因。 在可能的情况下，这会将用户直接带到设置应用中的正确位置来解决此问题。

<!-- ########################## -->
## <a name="december-2017"></a>2017 年 12 月

### <a name="device-configuration"></a>设备配置

#### <a name="new-automatic-redeployment-setting---1469168---"></a>新的自动重新部署设置<!-- 1469168 -->
使用“自动重新部署”设置，具有管理权限的用户可在设备锁定屏幕上使用 CTRL+Win+R 删除所有用户数据和设置   。 设备会自动进行重新配置并重新注册到管理。 此设置可在“Windows 10”>“设备限制”>“常规”>“自动重新部署”中找到。 有关详细信息，请参阅[适用于 Windows 10 的 Intune 设备限制设置](../configuration/device-restrictions-windows-10.md#general)。

#### <a name="support-for-additional-source-editions-in-the-windows-10-edition-upgrade-policy----903672--1119689---"></a>支持在 Windows 10 版本升级策略中指定其他源版本 <!-- 903672,  1119689 -->
现在可以使用 Windows 10 版本升级策略从其他 Windows 10 版本（Windows 10 专业版、Windows 10 专业教育版、Windows 10 云端版等）升级。 在此版本发布前，支持的版本升级路径更加受限。 有关详细信息，请参阅[如何配置 Windows 10 版本升级](../configuration/edition-upgrade-configure-windows-10.md)。

#### <a name="new-windows-defender-security-center-wdsc-device-configuration-profile-settings---1335507---"></a>新的 Windows Defender 安全中心 (WDSC) 设备配置文件设置<!-- 1335507 -->

Intune 在名为  “Windows Defender 安全中心”的端点保护下添加了一个新的设备配置文件设置部分。 IT 管理员可以配置最终用户能访问 Windows Defender 安全中心应用的支柱类型。 如果 IT 管理员在 Windows Defender 安全中心应用中隐藏支柱，则与隐藏支柱相关的所有通知都不会显示在用户设备上。

以下是管理员可以在 Windows Defender 安全中心设备配置文件设置中隐藏的支柱：
- 病毒和威胁防护
- 设备性能和运行状况
- 防火墙和网络保护
- 应用和浏览器控制
- 产品系列选项

IT 管理员还可以自定义用户接收的通知。 例如，你可以配置用户是接收由 WDSC 中的可见支柱生成的所有通知还是仅接收关键通知。 非关键通知包括 Windows Defender 防病毒活动的周期性摘要以及扫描完成时的通知。 所有其他通知被视为是关键通知。 另外，还可以自定义通知内容，例如，可以提供 IT 联系信息以嵌入用户设备上显示的通知。

#### <a name="multiple-connector-support-for-scep-and-pfx-certificate-handling---1361755---"></a>SCEP 和 PFX 证书处理的多个连接器支持<!-- 1361755 -->

使用本地 NDES 连接器向设备提供证书的客户现在可以在一个租户中配置多个连接器。

这项新功能支持以下方案：

-  高可用性

每个 NDES 连接器从 Intune 中拉取证书请求。  如果一个 NDES 连接器脱机，另一个连接器可以继续处理请求。

#### <a name="customer-subject-name-can-use-aad_device_id-variable----1468599---"></a>客户的使用者名称可以使用 AAD_DEVICE_ID 变量 <!-- 1468599 -->

在 Intune 中创建 SCEP 证书配置文件时，现在可以使用 AAD_DEVICE_ID 变量生成自定义使用者名称。   如果使用此 SCEP 配置文件请求获取证书，这个变量会被替换为发出证书请求的设备的 AAD 设备 ID。


### <a name="device-management"></a>设备管理

#### <a name="manage-jamf-enrolled-macos-devices-with-intunes-device-compliance-engine---1592747---"></a>使用 Intune 的设备合规性引擎管理 Jamf 注册的 macOS 设备<!-- 1592747 -->
现在可以使用 Jamf 将 macOS 设备状态信息发送到 Intune。然后，Intune 会评估它与 Intune 控制台中定义的策略的符合性。 基于设备符合性状态以及其他条件（如位置、用户风险等），条件访问将强制实现 macOS 设备访问云和与 Azure AD 连接的本地应用程序（包括 Office 365）的符合性。 详细了解如何[设置 Jamf 集成](../protect/conditional-access-integrate-jamf.md)和[强制 Jamf 托管设备遵守策略](../protect/conditional-access-assign-jamf.md)。

#### <a name="new-ios-device-action-----1424701---"></a>新的 iOS 设备操作  <!-- 1424701 -->

现在可以关闭 iOS 10.3 监管的设备。 此操作会立即关闭设备，而不会向最终用户发出警告。   当你在“设备”工作负载中选择设备时，可以在设备属性中找到“关闭（仅监督）”操作。

#### <a name="disallow-datetime-changes-to-samsung-knox-devices---1468103---"></a>禁止对 Samsung Knox 设备更改日期/时间<!-- 1468103 -->

我们新增了一项功能，以便用户能够禁止对 Samsung Knox 设备更改日期和时间。 此功能位于“设备配置文件”   > “设备限制(Android)”   > “常规”  中。

#### <a name="surface-hub-resource-account-supported---1566442----"></a>支持的 Surface Hub 资源帐户<!-- 1566442  -->

我们新增了一项设备操作，以便管理员能够定义和更新与 Surface Hub 关联的资源帐户。

资源帐户由 Surface Hub 用于通过 Skype/Exchange 进行身份验证，以便它可以加入会议。 可以创建一个唯一的资源帐户，以使 Surface Hub 作为会议室出现在会议中。 例如，资源帐户可能会显示为“会议室 B41/6233”  。 通常需要针对会议室位置以及何时需要更改其他资源帐户参数来配置 Surface Hub 的资源帐户（称为设备帐户）。

如果管理员需要更新设备上的资源帐户，他们必须提供与该设备关联的当前 Active Directory/Azure Active Directory 凭据。 如果为设备启用了密码轮换，则管理员必须转到 Azure Active Directory 以查找密码。

> [!NOTE]
> 所有字段都会向下发送到一个包中，覆盖之前配置的所有字段。 空字段也会覆盖现有字段。

以下是管理员可以配置的设置：

-  资源帐户
  - **Active Directory 用户**

    域名\用户名或用户主体名称 (UPN)：user@domainname.com

  - **密码**

-  可选的资源帐户参数（必须使用指定的资源帐户设置）

  - **密码轮转周期**

    出于安全原因，确保帐户密码每周由 Surface Hub 自动更新。 在启用此功能之后，要配置任何参数，Azure Active Directory 中的帐户必须先进行密码重置。

  - **SIP (会话初始协议)地址**

    仅在自动发现失败时使用。

  - **Email**

    设备/资源帐户的电子邮件地址。

  - **Exchange Server**

    仅在自动发现失败时需要。

  - **日历同步**

    指定是否启用日历同步和其他 Exchange Server 服务。 例如：会议同步。

#### <a name="install-office-apps-on-macos-devices---1494311---"></a>在 macOS 设备上安装 Office 应用<!-- 1494311 -->
现在可以在 macOS 设备上安装 Office 应用。 这个新的应用类型将允许你安装 Word、Excel、PowerPoint、Outlook 和 OneNote。 这些应用还随附 Microsoft AutoUpdate (MAU)，有助于保护和不断更新应用。

### <a name="app-management"></a>应用管理

#### <a name="delete-an-ios--volume-purchasing-program-token---820879---"></a>删除 iOS 批量采购计划令牌<!-- 820879 -->
可以使用控制台删除 iOS Volume Purchase Program (VPP) 令牌。 当你有重复的 VPP 令牌实例时，可能需要执行此操作。

### <a name="intune-apps"></a>Intune 应用


### <a name="role-based-access-control"></a>基于角色的访问控制

#### <a name="a-new-entity-collection-named-current-user-is-limited-to-currently-active-user-data---1667026---"></a>名为“当前用户”的新实体集合仅限于当前活动的用户数据<!-- 1667026 -->

User  实体集合包含企业中分配有许可证的所有 Azure Active Directory (Azure AD) 用户。 例如，在上个月期间，可能将某个用户添加到 Intune 然后又将其删除。 尽管在提交报告时该用户已不存在，但在数据中仍然会显示该用户及其状态。 可以创建一个报告，该报告将显示用户的历史记录在你的数据中存在的持续时间。

相比之下，新的“当前用户”  实体集合只包含尚未被删除的用户。 “当前用户”  实体集合仅包含当前活动的用户。 有关“当前用户”  实体集合的信息，请参阅[引用当前用户实体](../developer/reports-ref-data-model.md)。

### <a name="updated-graph-apis---1736360---"></a>更新了 Graph API<!-- 1736360 -->

在此版本中，我们更新了一些适用于 Intune 且处于 beta 阶段的 Graph API。 有关详细信息，请查看每月的 [Graph API 更改日志](https://developer.microsoft.com/graph/docs/concepts/changelog)。

### <a name="monitor-and-troubleshoot"></a>监视和故障排除

#### <a name="intune-supports-windows-information-protection-wip-denied-apps---1479103---"></a>Intune 支持 Windows 信息保护 (WIP) 拒绝的应用<!-- 1479103 -->
可在 Intune 中指定已拒绝的应用。 如果某个应用被拒，它会被阻止访问公司信息，允许的应用列表则与此相反。 有关详细信息，请参阅 [Recommended deny list for Windows Information Protection](https://docs.microsoft.com/windows/client-management/mdm/applocker-csp?f=255&MSPPError=-2147217396#recommended-deny-list-for-windows-information-protection)（Windows 信息保护的推荐拒绝列表）。

<!-- ########################## -->
## <a name="november-2017"></a>2017 年 11 月

### <a name="troubleshoot-enrollment-issues----746324---"></a>排查注册问题 <!-- 746324 -->

“疑难解答”工作区现在显示用户注册问题  。 问题的相关详细信息和建议的修正步骤可帮助管理员和支持人员排查问题。 某些注册问题可能无法捕获，还有某些错误可能没有修正建议。

### <a name="group-assigned-enrollment-restrictions---747598---"></a>组分配注册限制<!-- 747598 -->

作为 Intune 管理员，现在可[为用户组创建自定义设备类型和设备限制注册限制](../enrollment/enrollment-restrictions-set.md)。

使用 Intune Azure 门户，每种限制类型最多可创建 25 个实例，然后这些实例可分配给用户组。 组分配限制会替代默认限制。

所有限制类型实例均保存在严格有序的列表中。 此顺序定义冲突解决的优先级值。 受多个限制实例影响的用户仅受优先级值最高的实例限制。 通过将给定实例拖至列表中其他位置，可更改其优先级。

将 Android for Work 设置从 Android For Work 注册菜单迁移到注册限制菜单时，会随之发布此功能。 由于这种迁移可能需要几天时间，帐户可能会在 11 月版本的其他部分中升级，然后才能看到已为注册限制启用组分配。

### <a name="support-for-multiple-network-device-enrollment-service-ndes-connectors---1528104---"></a>支持多个网络设备注册服务 (NDES) 连接器<!-- 1528104 -->

NDES 允许无域凭据运行的移动设备基于简单证书注册协议 (SCEP) 获取证书。
利用此更新可支持多个 NDES 连接器。

### <a name="manage-android-for-work-devices-independently-from-android-devices---1490731-eeready--"></a>独立于 Android 设备管理 Android for Work 设备<!-- 1490731 EEready-->

Intune 支持独立于 Android 平台管理 Android for Work 设备的注册。 这些设置位于“设备注册” > “注册限制” > “设备类型限制”下    。 （这些设置之前位于“设备注册” > “Android for Work 注册” > “Android for Work 注册设置”下    。）

默认情况下，Android for Work 设备的设置与 Android 设备的设置相同。 但是，更改 Android for Work 设置后则不再相同。

如果阻止个人 Android for Work 注册，那么仅公司 Android 设备可注册为 Android for Work。

使用新设置时，请考虑下列几点：

#### <a name="if-you-have-never-previously-onboarded-android-for-work-enrollment"></a>如果之前从未载入 Android for Work 注册

默认设备类型限制将阻止新的 Android for Work 平台。 载入该功能后，可允许设备注册 Android for Work。 为此，请更改默认值或新建一个设备类型限制，取代默认设备类型限制。

#### <a name="if-you-have-onboarded-android-for-work-enrollment"></a>如果已载入 Android for Work 注册

如果之前已载入，那么情况取决于所选设置：

| 设置 | 默认设备类型限制中的 Android for Work 状态 | 注意 |
| --- | --- | --- |
| **将所有设备作为 Android 管理** | 已阻止 | 所有 Android 设备均不注册 Android for Work。 |
| 将受支持设备作为 Android for Work 管理  | 然后用户才能访问 | 所有支持 Android for Work 的 Android 设备均须注册 Android for Work。 |
| **仅为这些组中的用户将受支持设备作为 Android for Work 管理** | 已阻止 | 创建单独的设备类型限制策略替代默认值。 此策略将之前选择的组定义为允许 Android for Work 注册。 允许所选组中的用户继续注册 Android for Work 设备。 所有其他用户则不能注册 Android for Work。 |

所有情况下都将保留预期规则。 对你来说，无需任何操作即可维护环境中的 Android for Work 全局或按组允许。

### <a name="google-play-protect-support-on-android---908720---"></a>Android 上的 Google Play Protect 支持<!-- 908720 -->

随着 Android Oreo 的发布，Google 引入了一系列名为 Google Play Protect 的安全功能，以便用户和组织可以运行安全的应用和 Android 映像。 Intune 现支持 Google Play Protect 功能，包括 SafetyNet 远程认证。 管理员可以设置符合性策略要求，要求配置和正常运行 Google Play Protect。
“SafetyNet 设备认证”  设置要求设备连接到 Google 服务，以验证设备是否正常运行且未遭到入侵。 管理员还可以对 Android for Work 设置配置文件设置，以要求 Google Play 服务对已安装的应用进行验证。 如果设备不符合 Google Play Protect 要求，条件访问可能会阻止用户访问公司资源。

- 了解[如何创建用于启用 Google Play 保护的设备符合性策略](../protect/compliance-policy-create-android.md)。

### <a name="text-protocol-allowed-from-managed-apps---1414050----"></a>允许受管理应用发送文本协议<!-- 1414050  -->

由 Intune App SDK 管理的应用可发送短信。


### <a name="app-install-report-updated-to-include-install-pending-status---1249446---"></a>已更新应用安装报表以包括安装挂起状态<!-- 1249446 -->  

通过“客户端应用”工作负荷中的“应用”列表，可获取每个应用的“应用安装状态”报表，该报表现在包括用户和设备的“安装挂起”计数     。

### <a name="ios-11-app-inventory-api-for-mobile-threat-detection---1391759---"></a>移动威胁检测的 iOS 11 应用清单 API<!-- 1391759 -->

Intune 从个人和公司所有的设备收集应用清单信息，这些信息可供移动威胁检测 (MTD) 提供程序提取，例如 Lookout for Work。 可通过 iOS 11+ 设备的用户收集应用清单。

**应用清单**  
清单（来自公司所有的 iOS 11+ 和个人所有的设备）将发送给 MTD 服务提供程序。 应用清单中的数据包括：

- 应用 ID
- 应用版本
- 应用内部版本号
- 应用名称
- 应用程序包大小
- 应用动态大小
- 应用是否经过验证
- 应用是否受管理

### <a name="migrate-hybrid-mdm-users-and-devices-to-intune-standalone---1463747-wnready---"></a>将混合 MDM 用户及其设备迁移至 Intune 独立版<!-- 1463747 wnready -->
现有新的流程和工具可用于将混合 MDM 的用户及其设备迁移至 Azure 门户中的 Intune，这可让你执行以下任务：
- 将 Configuration Manager 控制台中的策略和配置文件复制到 Azure 门户中的 Intune
- 将一部分用户移至 Azure 门户中的 Intune，同时将剩余用户保留在混合 MDM 中
- 将设备迁移至 Azure 门户中的 Intune，而无需重新注册这些设备

### <a name="on-premises-exchange-connector-high-availability-support----676614---"></a>本地 Exchange 连接器高可用性支持 <!-- 676614 -->
使用指定的 客户端访问服务器 (CAS) 建立与 Exchange 的连接后，Exchange 连接器现在可以发现其他 CAS。 如果主 CAS 不可用，在主 CAS 的故障修复前，连接器会先故障转移到其他可用的 CAS。 有关详细信息，请参阅[本地 Exchange 连接器高可用性支持](../protect/exchange-connector-install.md#on-premises-intune-exchange-connector-high-availability-support)。

### <a name="remotely-restart-ios-device-supervised-only---1424595---"></a>远程重启 iOS 设备（仅限被监督的设备）<!-- 1424595 -->

可使用设备操作触发受监督的 iOS 10.3+ 设备重启。 要详细了解如何使用设备重启操作，请参阅[使用 Intune 远程重启设备](../remote-actions/device-restart.md)。

> [!Note]
> 此命令需要受监督的设备和“设备锁定”访问权限  。 设备会立即重启。 密码锁定的 iOS 设备重启后不会重新加入 Wi-Fi 网络；重启后，它们可能无法与服务器进行通信。

### <a name="single-sign-on-support-for-ios---1333645---"></a>iOS 的单一登录支持<!-- 1333645 -->  

可对 iOS 用户使用 SSO。 编码为在单一登录有效负载中查找用户凭据的 iOS 应用可使用此有效负载配置更新。 还可使用 UPN 和 Intune 设备 ID 配置主体名称和领域。 有关详细信息，请参阅[配置 Intune for iOS 设备 SSO](../configuration/ios-device-features-settings.md#single-sign-on)。

### <a name="add-find-my-iphone-for-personal-devices--1427287--"></a>为个人设备添加“查找我的 iPhone”<!--1427287-->
现可查看 iOS 设备是否已开启“激活锁”。 经典门户中的 Intune 之前并不提供此功能。

### <a name="remotely-lock-managed-macos-device-with-intune---1437691---"></a>使用 Intune 远程锁定受管理的 macOS 设备<!-- 1437691 -->

可锁定丢失的 macOS 设备并设置 6 位数的恢复 PIN。 锁定时，“设备概述”边栏选项卡会显示 PIN，直到发送另一个设备操作  。

有关详细信息，请参阅[使用 Intune 远程锁定受管理设备](../remote-actions/device-remote-lock.md)。

### <a name="new-scep-profile-details-supported---1559808---"></a>支持新的 SCEP 配置文件详细信息<!-- 1559808 -->

在 Windows、iOS、macOS 和 Android 平台上创建 SCEP 配置文件时，管理员现可设置其他设置。  管理员可设置 IMEI、序列号或公用名，包括采用使用者名称格式的电子邮件。

<!-- #### Update to what device details your company may see -1616825
The Company Portal app for Android can now use geofencing to protect access to company resources. It uses network details such as IP address, default gateway address, and Domain Name System (DNS) to determine whether to allow access to protected company resources. -->

### <a name="retain-data-during-a-factory-reset---1588489---"></a>在恢复出厂设置过程中保留数据 <!--1588489 -->
将 Windows 10 版本 1709 及更高版本重置为出厂设置时，可使用新功能。 管理员可指定在恢复出厂设置过程中，是否将设备注册和其他配置数据保留在设备上。

恢复出厂设置过程中保留以下数据：
- 与设备关联的用户帐户
- 计算机状态（域加入，已加入 Azure Active Directory）
- MDM 注册
- OEM 安装的应用（存储和 Win32 应用）
- 用户配置文件
- 用户配置文件以外的用户数据
- 用户自动登录

不保留以下数据：
- 用户文件
- 用户安装的应用（存储和 Win32 应用）
- 非默认设备设置


### <a name="window-10-update-ring-assignments-are-displayed---1621837---"></a>显示 Windows 10 更新通道分配<!-- 1621837 -->
进行故障排除时，对于正在查看的用户，可看到任何 Windows 10 更新通道分配  。  

### <a name="windows-defender-advanced-threat-protection-reporting-frequency-settings----1455974----"></a>Windows Defender 高级威胁防护报告频率设置 <!-- 1455974  -->
Windows Defender 高级威胁防护 (WDATP) 服务允许管理员对受管理设备的报告频率进行管理。 借助新的“提高遥测报告频率”选项，WDATP 可提高收集数据和评估风险的频率  。 报告的默认值可优化速度和性能。 提高报告频率十分适合高风险设备。 在“设备配置”的“Windows Defender ATP”配置文件中可找到此设置   。

### <a name="audit-updates---1412961---"></a>审核更新<!-- 1412961 -->  
Intune 审核提供与 Intune 相关的更改操作记录。  捕获所有创建、更新、删除和远程任务操作，并保留一年。  通过 Azure 门户，可查看每个工作负荷中过去 30 天的审核数据，还可对这些数据进行筛选。  利用相应的图形 API，可检索过去一年存储的审核数据。

“审核”位于“监视”组下  。 每个工作负荷都有一个“审核日志”菜单项  。

### <a name="company-portal-app-for-macos-is-available--1541700--"></a>现已提供适用于 macOS 的公司门户应用<!--1541700-->
macOS 上的 Intune 公司门户具有更新的体验，该体验已进行了优化，对于用户已注册的所有设备它均可以清楚地显示用户所需的所有信息和符合性通知。 而且，Intune 公司门户部署到设备后，Microsoft AutoUpdate for macOS 将为其提供更新。 可以从 macOS 设备登录到 Intune 公司门户网站来下载适用于 macOS 的新 Intune 公司门户。

### <a name="microsoft-planner-is-now-part-of-the-mobile-app-management-mam-list-of-approved-apps----1248473---"></a>Microsoft Planner 现已加入已批准应用的移动应用管理 (MAM) 列表 <!-- 1248473 -->
适用于 iOS 和 Android 的 Microsoft Planner 应用现在属于移动应用管理 (MAM) 的已批准应用。 可以通过 Azure 门户中的“Intune 应用保护”边栏选项卡为所有租户配置应用。
- 了解有关[已批准应用的 MAM 列表](https://www.microsoft.com/cloud-platform/microsoft-intune-apps)的详细信息。

### <a name="per-app-vpn-requirement-update-frequency-on-ios-devices-----1547061---"></a>iOS 设备上的每应用 VPN 要求更新频率  <!-- 1547061 -->  
管理员现在可以删除 iOS 设备上应用程序的每个应用程序 VPN 要求；受影响的设备将在下一次 Intune 签入后更新，通常在 15 分钟内发生。  

### <a name="support-for-system-center-operations-manager-management-pack-for-exchange-connector---885457---"></a>支持适用于 Exchange 连接器的 System Center Operations Manager 管理包<!-- 885457 -->
现已提供适用于 Exchange 连接器的 System Center Operations Manager 管理包帮助你分析 Exchange 连接器日志。 在你需要进行故障排除时，此功能可提供多种监视该服务的方式。

### <a name="co-management-for-windows-10-devices----1243445---"></a>适用于 Windows 10 设备的共同管理 <!-- 1243445 -->
共同管理是一种解决方案，可在传统管理与现代管理之间架起一座桥梁，为你提供利用分阶段的方法实现转换的途径。 共同管理本质上是一种解决方案，其中 Configuration Manager 和 Microsoft Intune 同时管理 Windows 10 设备，并且这些设备可联接到 Active Directory (AD) 和 Azure Active Directory (Azure AD)。  此配置提供以适合组织的步调（如果无法即刻完成所有迁移）逐步实现现代化的方式。  

### <a name="restrict-windows-enrollment-by-os-version---245498---"></a>通过 OS 版本限制 Windows 注册<!-- 245498 -->
作为 Intune 管理员，现在可为设备注册指定 Windows 10 的最低和最高版本。 可以在“平台配置”边栏选项卡中设置这些限制  。

Intune 将继续支持 Windows 8.1 电脑和手机注册。 但只有对 Windows 10 才可设置最高和最低版本限制。 若要允许注册 8.1 设备，请将最低限制留空。

### <a name="alerts-for-windows-autopilot-unassigned-devices----1631236---"></a>Windows Autopilot 未分配设备警报 <!-- 1631236 -->
在“Microsoft Intune” > “设备注册” > “概述”页中，为 Windows AutoPilot 未分配设备提供了一个新警报    。 此警报显示有多少来自 AutoPilot 计划的设备尚未分配 AutoPilot 部署配置文件。 使用警报中的信息可创建配置文件，并将其分配到未分配的设备。 单击警报时，会看到 Windows AutoPilot 设备的完整列表，以及与之相关的详细信息。 有关详细信息，请参阅[使用 Windows AutoPilot Deployment 计划注册 Windows 设备](../enrollment/enrollment-autopilot.md)。


### <a name="refresh-button-for-devices-list------1333581---"></a>设备列表的刷新按钮   <!-- 1333581 -->
由于设备列表不会自动刷新，可使用新的“刷新”按钮来更新列表中显示的设备。

### <a name="support-for-symantec-cloud-certification-authority-ca----1333638---"></a>对 Symantec 云证书颁发机构 (CA) 的支持 <!-- 1333638 -->    
Intune 现在支持 Symantec 云 CA，允许 Intune 证书连接器从 Symantec 云 CA 向 Intune 受管理设备颁发 PKCS 证书。 如果现已将 Intune 证书连接器和 Microsoft 证书颁发机构 (CA) 配合使用，则可以利用现有 Intune 证书连接器设置添加 Symantec CA 支持。

### <a name="new-items-added-to-device-inventory----1404455---"></a>添加到设备清单的新项  <!--1404455 -->
以下新项目现在适用于[由已注册设备获取的清单](../remote-actions/device-inventory.md)：

- Wi-Fi MAC 地址
- 总存储空间
- 总可用空间
- MEID
- 订阅者运营商

### <a name="set-access-for-apps-by-minimum-android-security-patch-on-the-device---1278463---"></a>通过在设备上定义最低 Android 安全修补程序版本设置对应用的访问权限<!-- 1278463 -->   
管理员可定义最低 Android 安全修补程序版本，必须在设备上安装该修补程序才能访问托管帐户下的托管应用程序。

> [!Note]  
> 此功能仅适用于在安装了 Android 6.0 及更高版本的设备上限制由 Google 发布的安全修补程序。

### <a name="app-conditional-launch-support---1193313---"></a>应用条件启动支持<!-- 1193313 -->
IT 管理员现可通过 Azure 管理门户设置要求，通过移动应用管理 (MAM) 强制要求在应用程序启动时输入密码，而不是输入数字 PIN。 如果进行此配置，在访问启用 MAM 的应用程序前，用户需要在出现提示时设置并使用密码。 密码是至少包含一个特殊字符或大写/小写字母的数字 PIN。 此版本的 Intune 仅在 iOS 上支持此功能  。 Intune 对密码的支持与支持数字 PIN 类似，设置了最短长度并且允许重复字符和序列。 该功能需要一些应用程序（例如 WXP、Outlook、Managed Browser、Yammer）的参与，将 Intune APP SDK 与代码集成，以便此功能准备就绪并在目标应用程序中强制实施密码设置。

### <a name="app-version-number-for-line-of-business-in-device-install-status-report---1233999---"></a>设备安装状态报表中业务线的应用版本号<!-- 1233999 -->
在此版本中，设备安装状态报告显示适用于 iOS 和 Android 的业务线应用的应用版本号。 可使用此信息对应用进行故障排除，或者查找正在运行过时应用版本的设备。

### <a name="admins-can-now-configure-the-firewall-settings-on-a-device-using-a-device-configuration-profile---951708---"></a>管理员现在可以使用设备配置文件在设备上配置防火墙设置<!-- 951708 -->   
管理员可以启用防火墙，还可以为域、专用网络和公用网络配置多种协议。  可在“Endpoint Protection”配置文件中找到这些防火墙设置。

### <a name="windows-defender-application-guard-helps-protect-devices-from-untrusted-websites-as-defined-by-your-organization---958257---"></a>Windows Defender 应用程序防护根据组织的定义，帮助阻止设备访问不受信任的网站<!-- 958257 -->   
利用 Windows 信息保护工作流或设备配置下的新“网络边界”配置文件，管理员可将站点定义为“受信任站点”或“公司站点”。 如果使用 Microsoft Edge 访问未在 64 位 Windows 10 设备的受信任网络边界中列出的站点，这些站点将转为在 Hyper-V 虚拟计算机内的浏览器中打开。

可在设备配置文件“Endpoint Protection”中找到应用程序防护。 管理员可在其中配置虚拟化浏览器与主机，以及非受信任站点与受信任站点之间的交互，同时存储虚拟化浏览器中生成的数据。 要在设备上使用应用程序防护，首先必须配置网络边界。 仅可为每个设备定义一个网络边界，这一点非常重要。  

### <a name="windows-defender-application-control-on-windows-10-enterprise-provides-mode-to-trust-only-authorized-apps---1031096---"></a>Windows 10 企业版上的 Windows Defender 应用程序控制提供仅信任经授权应用的模式<!-- 1031096 -->    
由于每天都有成千上万个新恶意文件生成，因此使用基于签名的防病毒检测来抵御恶意软件可能无法再针对新型攻击提供足够的防御。 通过在 Windows 10 企业版上使用 Windows Defender 应用程序控制，可以更改设备配置，从信任防病毒软件或其他安全解决方案未阻止的所有应用的模式，更改为操作系统仅信任经企业授权的应用的模式。 可在 Windows Defender 应用程序控制中将信任分配给应用。

利用 Intune，可以在“仅审核”模式或强制执行模式下配置应用程序控制策略。 在“仅审核”模式下运行的应用不会受到阻止。 “仅审核”模式在本地客户端日志中记录所有事件。 还可以配置是仅允许运行 Windows 组件和 Microsoft Store 应用，还是允许运行 Intelligent Security Graph 定义的信誉良好的其他应用。

### <a name="window-defender-exploit-guard-is-a-new-set-of-intrusion-prevention-capabilities-for-windows-10---1063615---"></a>Windows Defender 攻击防护是面向 Windows 10 的一组新入侵防护功能<!-- 1063615 -->   
Windows Defender 攻击防护内含自定义规则，可降低应用程序受到攻击的可能性、预防宏和脚本威胁、自动阻止网络连接到可信度较低的 IP 地址，以及保护数据免受勒索软件和未知威胁的攻击。 Windows Defender 攻击防护包含以下组成部分：

- “攻击面减少”提供用于预防宏、脚本和电子邮件威胁的规则  。
- “控制文件夹访问”可自动阻止访问受保护文件夹中的内容  。
- “网络筛选器”可阻止从任何应用到低可信度 IP/域的出站连接 
- “攻击防护”提供内存、控制流和策略限制，可用于保护应用程序免受攻击  。

### <a name="manage-powershell-scripts-in-intune-for-windows-10-devices---790537---"></a>在 Intune 中管理 PowerShell 脚本以供 Windows 10 设备使用<!-- 790537 -->

Intune 管理扩展允许你在 Intune 中上传 PowerShell 脚本以在 Windows 10 设备上运行。 扩展对 Windows 10 移动设备管理 (MDM) 功能进行了补充，使你可更轻松地采用新式管理。 有关详细信息，请参阅[在 Intune 中管理 PowerShell 脚本以供 Windows 10 设备使用](../apps/intune-management-extension.md)。

### <a name="new-device-restriction-settings-for-windows-10--------1308850---"></a>适用于 Windows 10 的 Intune 新设备限制设置     <!-- 1308850 -->
- 消息传送（仅限移动设备）- 禁用测试或 MMS 消息
- 密码 - 此设置用于启用 FIPS，并且支持使用 Windows Hello 设备辅助设备进行身份验证 
- 显示 - 此设置用于打开或关闭旧版应用的 GDI 缩放

### <a name="windows-10-kiosk-mode-device-restrictions---1308872---"></a>Windows 10 设备的展台模式限制<!-- 1308872 -->   
可将 Windows 10 设备的用户限制为使用展台模式，从而限制这些用户仅使用一组预定义的应用。  为此，需创建 Windows 10 设备限制配置文件并设置展台设置。

展台模式支持两种模式：“单应用”模式（仅允许用户运行一个应用）或“多应用”模式（允许访问多个应用）   。  可定义用户帐户和设备名，确定受支持的应用。  用户登录时，仅可访问定义的应用。  有关详细信息，请参阅 [AssignedAccess CSP](https://docs.microsoft.com/windows/client-management/mdm/assignedaccess-csp)。 

展台模式要求：

- MDM 机构必须是 Intune。
- 必须已在目标设备上安装应用。
- 设备必须[正确预配](https://docs.microsoft.com/windows/configuration/set-up-a-kiosk-for-windows-10-for-desktop-editions)。

### <a name="new-device-configuration-profile-for-creating-network-boundaries---1311967---"></a>用于创建网络边界的新设备配置文件<!-- 1311967 -->   
名为“网络边界”的新设备配置文件与其他设备配置文件可以位于同一位置  。 使用此配置文件定义要视为公司资源和受信任资源的在线资源。 必须先为设备定义网络边界，然后才能在设备上使用 Windows Defender 应用程序防护和 Windows 信息保护等功能  。 仅可为每个设备定义一个网络边界，这一点非常重要。

可以定义可信任的企业云资源、IP 地址范围和内部代理服务器。 定义后，Windows Defender 应用程序防护和 Windows 信息保护等功能即可使用网络边界。

### <a name="two-additional-settings-for-windows-defender-antivirus---1338409---"></a>Windows Defender 防病毒软件的两个其他设置<!-- 1338409 -->  
**文件阻止级别**

| | |
|---|---|
| 未配置 | “未配置”使用 Windows Defender 防病毒软件的默认阻止级别，并提供强大的检测功能而不会增加检测出合法文件的风险  。 |
| 高 | “高”级别执行级别较高的检测  。
| 高 +  | “高 +”级别执行“高”级别检测，同时采取额外的保护措施，但可能会影响客户端性能  。
| 零容差  | “零容差”可阻止所有未知的可执行文件  。 |

级别设置为“高”可能导致检测出一些合法文件，但出现此情况的可能性不大  。
建议将文件阻止级别设置为默认级别，即“未配置”  。

**云扫描文件的超时延长**  

| | |
|--|--|
| 秒数 (0 - 50) | 指定等待云返回结果时，Windows Defender 防病毒软件应阻止文件的最长时间。 默认值为 10 秒：此处指定的任意额外时间（最多 50 秒）都将与这 10 秒相加。 大多数情况下，扫描所需的时间远少于最大值。 延长时间可使云对可疑文件进行全面调查。 建议启用此设置，并至少指定 20 秒的延长时间。 |

### <a name="citrix-vpn-added-for-windows-10-devices---1512457---"></a>添加了适用于 Windows 10 设备的 Citrix VPN<!-- 1512457 -->  
可为 Windows 10 设备配置 Citrix VPN。 为 Windows 10 或更高版本配置 VPN 时，可在“基础 VPN”边栏选项卡中的“选择连接类型”列表中选择“Citrix VPN”   。

> [!Note]
> 适用于 iOS 和 Android 的 Citrix 配置已存在。

### <a name="wi-fi-connections-support-pre-shared-keys-on-ios---1550823---"></a>iOS 上的 Wi-Fi 连接支持预共享密钥<!-- 1550823 -->
客户可配置 Wi-Fi 配置文件，以便在 iOS 设备上为“WPA/WPA2 个人”连接使用预共享密钥 (PSK)。 当设备在 Intune 中注册时，这些配置文件将被推送至用户的设备。

当配置文件推送到设备时，下一步采取何种操作取决于配置文件的配置。  如果设置为自动连接，则它将在下一次需要网络时执行自动连接。  如果手动连接配置文件，则用户必须手动激活连接。  

### <a name="access-to-managed-app-logs-for-ios---1469920---"></a>访问 iOS 的托管应用日志<!-- 1469920 -->
安装了 Managed Browser 的最终用户现在可查看所有 Microsoft 已发布应用的管理状态，并可针对托管 iOS 应用的疑难问题发送日志。

若要了解如何在运行于 iOS 设备上的 Managed Browser 中启用疑难解答模式，请参阅[如何在 iOS 上使用 Managed Browser 访问托管应用日志](../apps/app-configuration-managed-browser.md#how-to-access-to-managed-app-logs-using-the-managed-browser-on-ios)。

### <a name="improvements-to-device-setup-workflow-in-the-company-portal-for-ios-in-version-290---1417174---"></a>在适用于 iOS 的公司门户（版本 2.9.0）中对设备设置工作流的改进<!-- 1417174 -->

改进了适用于 iOS 的公司门户应用中的设备设置工作流。 语言更贴近用户，并尽可能地将屏幕合并。 通过在整个设置文本中使用公司名称使语言特定于你的公司。 可以在 [应用 UI 的新增功能](whats-new-app-ui.md)页上看到此更新的工作流。

### <a name="user-entity-contains-latest-user-data-in-data-warehouse-data-model---1544273---"></a>用户实体包含数据仓库数据模型中的最新用户数据<!-- 1544273 -->
Intune 数据库仓库数据模型的第一个版本只包含 Intune 的最近历史数据。 报表制作者无法捕获用户的当前状态。 在此更新中，用户实体将包含最新用户数据  。

<!-- ########################## -->
## <a name="october-2017"></a>2017 年 10 月

### <a name="ios-and-android-line-of-business-app-version-number-is-visible---1380712---"></a>iOS 和 Android 业务线应用版本号是可见的<!-- 1380712 -->

现在，Intune 中的应用会显示 iOS 和 Android 业务线应用的版本号。 版本号会在 Azure 门户、应用列表和应用概述边栏选项卡中显示。 最终用户可在公司门户应用和 Web 门户中查看应用的版本号。

__完整版本号__ 完整版本号标识应用的特定版本。 该号码显示为“版本号(内部版本号)”   。 例如：2.2(2.2.17560800)

完整版本号包含两个部分：

- **版本**  
  版本号是应用的发行版号（可人工读取）。 最终用户使用版本号确定应用的不同发行版。

- **内部版本号**  
  内部版本号是一个内部号码，可在应用检测中使用，并可用于以编程方式管理应用。 内部版本号是指应用的迭代，应用可引用代码中的更改。

要详细了解版本号以及如何开发业务线应用，请参阅 [Microsoft Intune App SDK 入门](../developer/app-sdk-get-started.md#line-of-business-app-version-numbers)。

### <a name="device-and-app-management-integration---677972---"></a>设备和应用管理集成<!-- 677972 -->
由于 Intune 移动设备管理 (MDM) 和移动应用管理 (MAM) 均可通过 Azure 门户访问，因此 Intune 已开始集成有关应用程序和设备管理的 IT 管理员体验。 这些更改旨在简化设备和应用的管理体验。

有关 MDM 和 MAM 更改的详细信息，请参阅 [Intune 支持团队博客](https://blogs.technet.microsoft.com/intunesupport/2017/09/19/support-tip-setting-up-communication-between-mam-managed-and-mdm-managed-apps/)中的发布内容。

### <a name="new-enrollment-alerts-for-apple-devices---1471790---"></a>Apple 设备的新注册警报<!-- 1471790 -->
注册的概述页将介绍一些有关 Apple 设备管理的警报，这些警报适用于 IT 管理员。 如果存在下列情况，“概述”页上就会显示警报：Apple MDM 推送消息称证书将过期或已过期；设备注册计划令牌将过期或已过期；设备注册计划中存在未分配的设备。

### <a name="support-token-replacement-for-app-configuration-without-device-enrollment---1080364---"></a>支持使用令牌替换应用配置（无需设备注册）<!-- 1080364 -->

对于未注册设备上的应用，可在应用配置期间使用令牌获取动态值。 有关详细信息，请参阅[为受管理应用添加应用配置策略（无需设备注册）](../apps/app-configuration-policies-managed-app.md)。

### <a name="updates-to-the-company-portal-app-for-windows-10--1299474--"></a>更新适用于 Windows 10 的公司门户应用<!--1299474-->
适用于 Windows 10 的公司门户应用的“设置”页面已更新，以使设置和预期的用户操作在所有设置中更加一致。 其更新也旨在匹配其他 Windows 应用的布局。 你可以在[应用 UI 中的新增功能](whats-new-app-ui.md)页找到更新之前/之后的图像。

### <a name="inform-end-users-what-device-information-can-be-seen-for-windows-10-devices--1337920--"></a>告知最终用户可以查看 Windows 10 设备的哪些设备信息<!--1337920-->
在适用于 Windows 10 的公司门户应用上，我们还在“设备详细信息”屏幕中添加了“所有权类型”  。 这样，用户可以直接从此页在 Intune 最终用户文档中找到隐私的相关详情。用户还可以在“关于”  屏幕上找到此类信息。

### <a name="feedback-prompts-for-the-company-portal-app-for-android--1165249--"></a>适用于 Android 的公司门户应用的反馈提示<!--1165249-->
适用于 Android 的公司门户应用现在请求最终用户反馈。 此反馈将直接发送给 Microsoft，并且最终用户将有机会在公开的 Google Play 商店中评价该应用。 反馈不是必填项，可轻松消除此提示，以便用户可以继续使用此应用。

<!-- #### Update to what device details an organization can see 1616825
The Company Portal app for Android can now use geofencing to protect access to company resources. It uses network details such as IP address, default gateway address, and Domain Name System (DNS) to determine whether to allow access to protected company resources.-->

### <a name="helping-your-users-help-themselves-with-the-company-portal-app-for-android---1573324-1573150-1558616-1564878---"></a>使用适用于 Android 的公司门户应用帮助用户自助<!-- 1573324, 1573150, 1558616, 1564878 -->

适用于 Android 的公司门户应用为最终用户添加了说明，帮助他们了解并自行解决（如果可能）新用例。
- 如果最终用户已达到他们可添加的最大设备数，他们将被引导至 [Azure Active Directory 门户](https://account.activedirectory.windowsazure.com/r/#/profile)以移除设备。
- 为最终用户提供要遵守的步骤以帮助他们[修复 Samsung Knox 设备上的激活错误](https://go.microsoft.com/fwlink/?linkid=859718)或者[关闭节能模式](https://go.microsoft.com/fwlink/?linkid=2077422&clcid=0x409)。 如果这些解决方案都不能解决他们的问题，我们将提供如何[将日志提交到 Microsoft](../user-help/send-logs-to-microsoft-android.md) 的说明。

### <a name="new-resolve-action-available-for-android-devices---1583480---"></a>适用于 Android 设备的新“解决”操作<!-- 1583480 -->

适用于 Android 的公司门户应用“更新设备设置”页面上引入了“解析”操作  。 选择此选项可使最终用户直接进入导致其设备为不符合设备的设置。 Android 版公司门户应用当前为以下设置提供此操作：[设备密码](../user-help/set-your-pin-or-password-android.md)、[USB 调试](../user-help/you-need-to-turn-off-usb-debugging-android.md)和[未知源](../user-help/you-need-to-turn-off-unknown-sources-android.md)。

### <a name="device-setup-progress-indicator-in-android-company-portal---1565657---"></a>适用于 Android 的公司门户中的设备设置进度指示器<!-- 1565657 -->
适用于 Android 的公司门户应用在用户注册设备时显示设备安装进度指示器。 指示器显示新状态，从“安装设备...”开始，然后“注册设备...”，接下来“完成注册设备...”，最后“完成安装设备...”。

### <a name="certificate-based-authentication-support-on-the-company-portal-for-ios--1029830--"></a>iOS 版公司门户上基于证书的身份验证支持<!--1029830-->
我们在适用于 IOS 的公司门户应用中添加了对基于证书的身份验证 (CBA) 的支持。 具有 CBA 的用户输入其用户名，然后点击“使用证书登录”链接。 CBA 已支持用于 Android 和 Windows 的公司门户应用。 你可以在[登录到公司门户应用](../user-help/sign-in-to-the-company-portal.md)页上了解详细信息。

### <a name="apps-that-are-available-with-or-without-enrollment-can-now-be-installed-without-being-prompted-for-enrollment---1334712---"></a>现在可以在没有注册提示的情况下，安装可注册或不可注册的应用。<!-- 1334712 -->

在 Android 公司门户应用中，现可在没有注册提示的情况下，安装通过/不通过注册而获取的公司应用。

### <a name="windows-autopilot-deployment-program-support-in-microsoft-intune----747617----"></a>Microsoft Intune 中的 Windows AutoPilot Deployment 计划支持 <!-- 747617  -->
现在可将 Microsoft Intune 与 Windows AutoPilot Deployment 计划配合使用，授权用户在不劳烦 IT 的情况下设置其企业设备。 可以自定义全新体验 (OOBE)，引导用户将设备加入 Azure AD 并在 Intune 中注册。 在配合使用 Microsoft Intune 与 Windows AutoPilot 时，完全无需部署、维护和管理操作系统映像。 有关详细信息，请参阅 [Enroll Windows devices using Windows AutoPilot Deployment Program](../enrollment/enrollment-autopilot.md)（使用 Windows AutoPilot Deployment 计划注册 Windows 设备）。

### <a name="quickstart-for-device-enrollment----1425655---"></a>设备注册快速入门 <!-- 1425655 --> 
快速入门当前在“设备注册”中可用，此外还提供了用于管理平台和配置注册过程的参考表格  。 对每个项目的简短说明和包含分步说明的文档链接提供了有用的文章，可帮助简化入门过程。

### <a name="device-categorization---1427491---"></a>设备分类<!-- 1427491 -->
“设备”>“概述”边栏选项卡中的已注册设备平台图可以按平台（包括 Android、iOS、macOS、Windows 和 Windows Mobile）整理设备  。  运行其他操作系统的设备将被分到“其他”组。  这包括由 Blackberry 和 NOKIA 等厂家生产的设备。  

要了解租户中的哪些设备会受到影响，请选择“管理”>“所有设备”，然后使用“筛选器”限制“操作系统”字段    。

### <a name="zimperium---new-mobile-threat-defense-partner-----954681---"></a>Zimperium - 新移动威胁防御合作伙伴  <!-- 954681 -->  
可根据 Zimperium 进行的风险评估，使用条件访问控制移动设备对公司资源的访问，Zimperium 是与 Microsoft Intune 集成的移动威胁防御解决方案。

#### <a name="how-integration-with-intune-works"></a>与 Intune 集成的工作原理
基于从运行 Zimperium 的设备收集的遥测评估风险。 可以基于通过 Intune 设备符合性策略启动的 Zimperium 风险评估配置 EMS 条件访问策略，从而根据检测到的威胁允许或阻止不符合要求的设备访问公司资源。

### <a name="new-settings-for-windows-10-device-restriction-profile-----978575-1308849---"></a>Windows 10 设备限制配置文件的新设置 <!--- 978575, 1308849, -->  
我们将向 Windows Defender SmartScreen 类别中的 Windows 10 设备限制配置文件中添加新设置。

有关 Windows 10 设备限制配置文件的详细信息，请参阅 [Windows 10 和更高版本的设备限制设置](../configuration/device-restrictions-windows-10.md)。

### <a name="remote-support-for-windows-and-windows-mobile-devices-----1070473---"></a>Windows 和 Windows Mobile 设备的远程支持  <!-- 1070473 -->  
Intune 现在可以使用 [TeamViewer](https://www.teamviewer.com) 软件（单独购买），为运行 Windows 和 Windows Mobile 设备的用户提供远程协助。

### <a name="scan-devices-with-windows-defender---1280988--1280990-----"></a>使用 Windows Defender 扫描设备<!-- 1280988  1280990   -->
现可在托管的 Windows 10 设备上，使用 Windows Defender 防病毒运行“快速扫描”、“完全扫描”和“更新签名”    。 在设备的“概览”边栏选项卡上，选择要在设备上运行的操作。 在命令发送到设备之前，系统会提示用户确认操作。 

**快速扫描**：快速扫描可扫描恶意软件注册启动的位置，如注册表项和已知的 Windows 启动文件夹。 快速扫描平均需要五分钟才能完成。 “始终开启实时保护”  设置可在用户打开、关闭文件、转到文件夹时扫描文件。与此设置配合使用，快速扫描可有助于保护系统或内核免遭潜在恶意软件威胁。 扫描完成时，用户可以在设备上查看扫描结果。 

**完全扫描**：完全扫描非常适合受恶意软件威胁的设备，以确定是否需要更彻底地清理任何停用组件，并且十分适用于运行按需扫描。 完全扫描可能需要一小时才能完成。 扫描完成时，用户可以在设备上查看扫描结果。 

**更新签名**：更新签名命令可更新 Windows Defender 防病毒恶意软件定义和签名。 这有助于确保 Windows Defender 防病毒可以有效地检测恶意软件。 此功能仅适用于挂起设备 Internet 连接的 Windows 10 设备。 

### <a name="the-enabledisable-button-is-removed-from-the-intune-certificate-authority-page-of-the-intune-azure-portal----1400455---"></a>已将“启用/禁用”按钮从 Intune Azure 门户的 Intune 证书颁发机构页中删除 <!-- 1400455 -->
 我们正在删除在 Intune 上设置证书连接器这一额外步骤。 当前，需要下载证书连接器，然后在 Intune 控制台中启用它。 但如果在 Intune 控制台中禁用它，该连接器仍将持续颁发证书。

#### <a name="how-does-this-affect-me"></a>这对我有何影响？
从 10 月开始，Azure 门户的证书颁发机构页中将不再显示“启用/禁用”按钮。 连接器功能保持不变。 证书仍将部署到在 Intune 中注册的设备。 可以继续下载并安装证书连接器。 若要停止颁发证书，当前需卸载证书连接器，而不是禁用它。

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>我需要如何准备应对此项变化？
如果目前已禁用证书连接器，则应该卸载它。

### <a name="new-settings-for-windows-10-team-device-restriction-profile------1308838---"></a>Windows 10 协同版设备限制配置文件的新设置  <!--- 1308838 -->
在此版本中，我们向 Windows 10 协同版设备限制配置文件添加了许多新设置，以帮助用户控制 Surface Hub 设备。

有关此配置文件的详细信息，请参阅 [Windows 10 协同版设备限制设置](../configuration/device-restrictions-windows-10-teams.md)。

### <a name="prevent-users-of-android-devices-from-changing-their-device-date-and-time----1333292---"></a>禁止 Android 设备用户更改其设备日期和时间 <!-- 1333292 -->
将可以使用 [Android 自定义设备策略](../configuration/custom-settings-android.md)，禁止 Android 设备用户更改设备日期和时间。

为此，请将 URI ./Vendor/MSFT/PolicyManager/My/System/AllowDateTimeChange 设置为 TRUE  ，配置 Android 自定义策略，再将策略分配给相应组。

### <a name="bitlocker-device-configuration---1397398---"></a>BitLocker 设备配置<!-- 1397398 -->
在“Windows 加密”>“基本设置”中，现可以使用新的“针对其他磁盘加密的警告”设置，从而禁止对用户设备上可能使用的其他磁盘加密显示[警告提示](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp#allowwarningforotherdiskencryption)   。  警告提示要求先征得最终用户同意，然后才能在设备上设置 BitLocker，并且会在最终用户确认之前禁止设置 BitLocker。  这一新设置可以禁用最终用户警告。


### <a name="volume-purchase-program-for-business-apps-will-now-sync-to-your-intune-tenant---800882---"></a>适用于企业的 Volume Purchase Program 应用现在将同步到你的 Intune 租户<!-- 800882 -->  
第三方开发人员可以私下将应用分发给适用于 iTunes Connect 中指定的业务成员的经授权 Volume Purchase Program。 这些面向业务成员的 VPP 可以登录 Volume Purchase Program App Store 并购买应用。

此版本中，最终用户购买的适用于业务应用的 VPP 将开始同步到其 Intune 租户中。

### <a name="select-apple-countryregion-store-to-sync-vpp-apps----1332311---"></a>选择 Apple 国家/地区应用商店以同步 VPP 应用 <!-- 1332311 -->  
将可以在上传 VPP 令牌时，配置 Volume Purchase Program (VPP) 国家/地区应用商店。 Intune 将同步指定 VPP 国家/地区应用商店中所有区域设置对应的 VPP 应用。

> [!NOTE]  
> 目前，Intune 只会同步 VPP 国家/地区应用商店中，区域设置与创建 Intune 租户所用的 Intune 区域设置一致的 VPP 应用。


### <a name="block-copy-and-paste-between-work-and-personal-profiles-in-android-for-work---1098994---"></a>在 Android for Work 中，禁止在工作配置文件与个人配置文件之间进行复制粘贴<!-- 1098994 -->
在此版本中，将可以配置 Android for Work 工作配置文件，以禁止在工作应用与个人应用之间进行复制粘贴。 可以转到 Android for Work  平台的“设备限制”  配置文件，在“工作配置文件设置”  中找到这一新设置。

### <a name="create-ios-apps-limited-to-specific-regional-apple-app-stores---1281692---"></a>创建特定区域 Apple App Store 专属的 iOS 应用<!-- 1281692 -->
将可以在创建 Apple App Store 管理的应用期间，指定国家/地区区域设置。

> [!Note]  
> 目前，只能创建美国国家/地区应用商店中具备的 Apple App Store 托管应用。

### <a name="update-ios-vpp-user-and-device-licensed-apps----1305564---"></a>更新 iOS VPP 用户和设备许可的应用 <!-- 1305564 -->  
将可以把 iOS VPP 令牌配置为，更新针对此令牌通过 Intune 服务购买的所有应用。 Intune 将在应用商店内检测 VPP 应用更新，并在设备进行检测时自动将这些更新推送到设备中。

有关设置 VPP 令牌和启用自动更新的步骤，请参阅 [如何使用 Microsoft Intune 管理通过批量采购计划购买的 iOS 应用] (/intune/vpp-apps-ios)。


### <a name="user-device-association-entity-collection-added-to-intune-data-warehouse-data-model---1187917---"></a>添加到 Intune 数据仓库数据模型的用户设备关联实体集合<!-- 1187917 -->
现在可使用用户设备关联信息（该信息将用户和设备实体集合相关联）生成报表和数据可视化效果。 可通过从“数据仓库 Intune”页检索到的 Power BI 文件 (PBIX)、通过 OData 终结点或通过开发自定义客户端，访问数据模型。

### <a name="review-policy-compliance-for-windows-10-update-rings---1067886---"></a>检查 Windows 10 更新通道的策略合规性<!-- 1067886 -->
将可以在“软件更新”>“每个更新通道的部署状态”中检查 Windows 10 更新通道的策略报告。 策略报告包括已配置的更新通道的部署状态。 

### <a name="new-report-that-lists-ios-devices-with-older-ios-versions-----1352223---"></a>列出使用较旧 iOS 版本的 iOS 设备的新报表  <!-- 1352223 -->
可在“软件更新”工作区中获取“过期 iOS 设备”报告   。 在报表中，可以查看已应用 iOS 更新策略且具有可用更新的受监督 iOS 设备的列表。 可以查看每个设备的状态，了解该设备未自动更新的原因。 

### <a name="view-app-protection-policy-assignments-for-troubleshooting----1475003---"></a>查看应用保护策略分配以进行故障排除<!--  1475003 -->
在即将发布的这一版本中，“应用保护策略”  选项将添加到“疑难解答”边栏选项卡上的“分配”  下拉列表中。 现在可以选择应用保护策略，查看分配给选定用户的应用保护策略。



### <a name="improvements-to-device-setup-workflow-in-company-portal--1490692--"></a>对公司门户中的设备设置工作流的改进<!--1490692-->
我们改进了适用于 Android 的公司门户应用中的设备安装工作流。 语言更贴近你公司的用语习惯，在可能的情况下我们还对屏幕进行了合并。 在[应用 UI 中的新增功能](whats-new-app-ui.md#week-of-october-2-2017)页上可以看到这些内容。

### <a name="improved-guidance-around-the-request-for-access-to-contacts-on-android-devices--1484985--"></a>改进了与请求访问 Android 设备上的联系人相关的指南<!--1484985-->

适用于 Android 的公司门户应用通常需要最终用户接受“联系人”权限。 如果最终用户拒绝授予此访问权限，现在他们将看到应用内通知，提醒他们授予此权限以实现条件访问。 

### <a name="secure-startup-remediation-for-android--1490712--"></a>面向 Android 的安全启动修正<!--1490712-->

使用 Android 设备的最终用户将能够点击公司门户应用中的不符合性原因。 在可能的情况下，这会将用户直接带到设置应用中的正确位置来解决此问题。 

### <a name="additional-push-notifications-for-end-users-on-the-company-portal-app-for-android-oreo--1475932--"></a>向最终用户额外发送有关适用于 Android Oreo 的公司门户应用的推送通知<!--1475932-->

最终用户可以看到其他通知，其中指明了 Android Oreo 公司门户应用何时执行后台任务，如从 Intune 服务检索策略。 这进一步提高了透明度，可方便最终用户了解公司门户应用何时在其设备上执行管理任务。 这是 Android Oreo 公司门户应用的全部[公司门户 UI 优化](https://blogs.technet.microsoft.com/intunesupport/2017/08/21/android-8-0-o-behaviour-changes-and-microsoft-intune)中的一部分。 

Android Oreo 中启用的新 UI 元素有进一步的优化。  最终用户将看到附加通知，指示他们公司门户何时执行从 Intune 服务中检索策略等后台任务。  最终用户可以更加清楚地了解公司门户何时在设备上执行管理任务。

### <a name="new-behaviors-for-the-company-portal-app-for-android-with-work-profiles---1485783---"></a>适用于 Android 的公司门户应用与工作配置文件配合使用时的新行为<!-- 1485783 -->

当你使用工作配置文件注册 Android for Work 设备时，它是工作配置文件中在设备上执行管理任务的公司门户应用。 

除非你在个人配置文件中使用启用了 MAM 的应用，否则适用于 Android 的公司门户应用将不再提供任何服务。 若要改进工作配置文件体验，Intune 将在工作配置文件成功注册后自动隐藏个人的公司门户应用。

通过浏览 [Play Store 中的公司门户](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal)并点击“启用”  ，可以随时在个人配置文件中启用适用于 Android 的公司门户应用。

### <a name="company-portal-for-windows-81-and-windows-phone-81-moving-to-sustaining-mode--1428681--"></a>适用于 Windows 8.1 和 Windows Phone 8.1 的公司门户将移至维护模式<!--1428681-->

从 2017 年 10 月开始，适用于 Windows 8.1 和 Windows Phone 8.1 的公司门户应用将移至维护模式。 这意味着应用和现有方案（如注册和符合性）将继续支持这些平台。 这些应用将继续通过现有版本通道下载，如 Microsoft 应用商店。 

一旦进入持续性模式，这些应用仅可收到重要安全更新程序。 将不会对这些应用发布任何其他更新或功能。 对于新功能，我们建议将设备更新到 Windows 10 或 Windows 10 移动版。 


### <a name="block-unsupported-samsung-knox-device-enrollment----1490695---"></a>阻止不受支持的 Samsung Knox 设备注册 <!-- 1490695 -->

公司门户应用仅尝试注册受支持的 Samsung Knox 设备。 为了避免出现阻止 MDM 注册的 Knox 激活错误，仅在 [Samsung 发布的设备列表](https://www.samsungknox.com/knox-supported-devices/knox-workspace)中有相应设备时，才尝试执行设备注册。 Samsung 设备的一些型号支持 Knox，而另一些型号则不支持 Knox。 在采购和部署之前，需与设备经销商验证 Knox 的兼容性。 有关已验证设备的完整列表，可以参阅 [Android 和 Samsung Knox Standard 策略设置](supported-devices-browsers.md#intune-supported-web-browsers)。

### <a name="end-of-support-for-android-43-and-lower---1171126-1326920---"></a>不再支持 Android 4.3 及更低版本<!-- 1171126, 1326920 -->
Android 托管的应用和公司门户应用需要使用 Android 4.4 和更高版本访问公司资源。 截至 12 月，所有注册的设备都将在 12 月内被强制停用，进而将无法再访问公司资源。 如果使用应用保护策略而不使用 MDM，应用将不会收到更新，并且随着时间推移其体验质量将会降低。

### <a name="inform-end-users-what-device-information-can-be-seen-on-enrolled-devices--1165314--"></a>告知最终用户可在已注册设备上查看哪些设备信息<!--1165314-->
在所有公司门户应用上，我们在“设备详细信息”屏幕中添加了“所有权类型”  。 这样，用户可以直接从[公司可以看到哪些信息？](../user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune.md)一文中找到隐私的相关详情。 这将在不久的将来在所有公司门户应用中推出。 我们在 [9 月](#september-2017)宣布了对 iOS 推出。

<!-- ########################## -->
## <a name="september-2017"></a>2017 年 9 月

### <a name="intune-supports-ios-11--1428975--"></a>Intune 支持 iOS 11<!--1428975-->
Intune 支持 iOS 11。 此信息之前已在 [Intune 支持博客](https://blogs.technet.microsoft.com/intunesupport/2017/09/12/support-tip-intune-support-for-ios-11/)中发布。

### <a name="end-of-support-for-ios-80---1164477---"></a>iOS 8.0 不再受支持<!-- 1164477 -->
托管应用和 iOS 公司门户应用将要求必须使用 iOS 9.0 及更高版本，才能访问公司资源。 今年 9 月之前不更新的设备将不再能够访问公司门户应用或这些应用。 

### <a name="refresh-action-added-to-the-company-portal-app-for-windows-10--1132468--"></a>添加到适用于 Windows 10 的公司门户应用的刷新操作<!--1132468-->
使用 Windows 10 版公司门户应用，用户可以通过下拉刷新或在桌面上按 F5 来刷新应用中的数据。

### <a name="inform-end-users-what-device-information-can-be-seen-for-ios--739894--"></a>通知最终用户可查看哪些 iOS 设备信息<!--739894-->

我们已在适用于 iOS 的公司门户应用的“设备详细信息”屏幕上添加“所有权类型”  。 这样，用户可以直接从此页在 Intune 最终用户文档中找到隐私的相关详情。用户还可以在“关于”屏幕上找到此类信息。

### <a name="allow-end-users-to-access-the-company-portal-app-for-android-without-enrollment---1169910---"></a>允许最终用户无需进行注册便可访问适用于 Android 的公司门户应用<!---1169910--->

最终用户很快将无需注册其设备就能访问 Android 公司门户应用。 使用应用保护策略的组织中的最终用户在打开公司门户应用时将不再收到指示其注册设备的提示。 最终用户也将能够从公司门户安装应用而无需注册其设备。 


### <a name="easier-to-understand-phrasing-for-the-company-portal-app-for-android---1396349---"></a>适用于 Android 的公司门户应用的表述更易于理解<!---1396349--->  

Android 公司门户应用的注册流程进行了简化，新增了文本，更易于最终用户进行注册。 若有自定义注册文档，不妨进行更新，以反映新屏幕。 有关示例图像，可以访问 [Intune 最终用户应用的 UI 更新](whats-new-app-ui.md#week-of-september-11-2017)页。

### <a name="windows-10-company-portal-app-added-to-windows-information-protection-allow-policy---677129---"></a>添加到 Windows 信息保护允许策略的 Windows 10 公司门户应用<!-- 677129 -->

Windows 10 公司门户应用已更新为支持 Windows 信息保护 (WIP)。 可以将应用添加到 WIP 允许策略。 此更改生效后，无需再将应用添加到“豁免”  列表。


<!-- ########################## -->
## <a name="august-2017"></a>2017 年 8 月

### <a name="improvements-to-device-overview---1404453---"></a>设备概述改进<!-- 1404453 -->  
设备概述改进现在显示已注册设备，但不包含由 Exchange ActiveSync 管理的设备。 Exchange ActiveSync 设备没有与已注册设备相同的管理选项。 要在 Azure 门户的 Intune 中查看已注册设备数和各平台的已注册设备数，请转到“设备”   > “概述”  。

### <a name="improvements-to-device-inventory-collected-by-intune"></a>Intune 所收集设备清单的改进
<!-- 961134, 1104426, 1281327, 1333543 -->
此版本中，我们对由你管理的设备收集的清单信息做出了以下改进：
 
- 对于 Android 设备，现在可向设备清单添加一列，显示每个设备的最新修补程序级别。 将“安全修补程序级别”  列添加到设备列表可查看此项。
- 筛选设备视图时，现在可按设备注册日期筛选设备。 例如，可仅显示于指定日期后注册的设备。
- 我们已对“上次签入日期”  项所用的筛选器做出了一些改进。
- 在设备列表中，现在可显示公司拥有设备的电话号码。
此外，还可使用筛选器窗格按电话号码搜索设备。

有关设备清单的详细信息，请参阅[如何查看 Intune 设备清单](../remote-actions/device-inventory.md)。

### <a name="conditional-access-support-for-macos-devices"></a>对 macOS 设备的条件访问支持 
<!-- 720172 -->
现在可设置一个条件访问策略，要求 Mac 设备注册 Intune 且符合其设备符合性策略。 例如，用户可以下载适用于 macOS 的 Intune 公司门户应用并向 Intune 注册其 Mac 设备。 Intune 会评估 Mac 设备是否符合 PIN、加密、OS 版本和系统完整性等要求。

- 深入了解[对 macOS 设备的条件访问支持](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)。

### <a name="company-portal-app-for-macos-is-in-public-preview---1484796---"></a>适用于 macOS 的公司门户应用当前为公共预览版<!---1484796--->
适用于 macOS 的公司门户应用目前作为企业移动性 + 安全性中条件访问公共预览版的一部分提供。 此版本支持 macOS 10.11 及更高版本。 在 [https://aka.ms/macOScompanyportal](https://aka.ms/macOScompanyportal) 处获取它。 


### <a name="new-device-restriction-settings-for-windows-10"></a>适用于 Windows 10 的 Intune 新设备限制设置    
<!--1063965, 1308850  -->
在此版本中，我们为 [Windows 10 设备限制配置文件](/intune/device-restrictions-windows-10)添加了新设置，类别如下：

- Windows Defender SmartScreen
- App Store

### <a name="updates-to-the-windows-10-endpoint-protection-device-profile-for-bitlocker-settings"></a>更新至 Windows 10 终结点保护设备配置文件以应用 BitLocker 设置
<!--1459533 -->    
此版本中，我们已对 BitLocker 设置在 Windows 10 终结点保护设备配置文件中的作用方式做出如下改进：
 
- 在“BitLocker OS 驱动器设置”  下，对于“包含非兼容 TPM 芯片的 BitLocker”  设置，选择“阻止”  后，以前这会导致实际上允许 BitLocker 的问题。 我们已修复此问题，在选中“阻止”后会阻止 BitLocker。
- 在“BitLocker OS 驱动器设置”  下，对于“基于证书的数据恢复代理”  设置，现在可显式阻止基于证书的数据恢复代理。 但是，默认情况下允许此代理。
- 在“BitLocker 固定数据驱动器设置”  下，对于“数据恢复代理”  设置，现在可显式阻止数据恢复代理。
有关详细信息，请参阅[适用于 Windows 10 及更高版本的 Endpoint Protection 设置](../protect/endpoint-protection-windows-10.md)。


### <a name="new-signed-in-experience-for-android-company-portal-users-and-app-protection-policy-users---621669---"></a>Android 公司门户用户和应用保护策略用户的新登录体验<!-- 621669 -->
最终用户现在可以使用 Android 公司门户应用浏览应用、管理设备和查看 IT 联系人信息，而无需注册其 Android 设备。 此外，如果最终用户已使用受 Intune 应用保护策略保护的应用并启动了 Android 公司门户，则最终用户将不会再收到注册设备的提示。

### <a name="new-setting-in-the-android-company-portal-app-to-toggle-battery-optimization--1405990--"></a>Android 公司门户应用中用于切换电池优化的新设置<!--1405990-->
适用于 Android 的公司门户应用的“设置”页添加了新设置，该设置可使用户轻松关闭公司门户和 Microsoft Authenticator 应用的电池优化  。 设置中显示的应用名称将有所区别，具体取决于使用哪一应用管理工作帐户。 我们建议用户关闭电池优化，以提高用于同步电子邮件和数据的工作应用的性能。 

### <a name="multi-identity-support-for-onenote-for-ios--------1234281---"></a>对适用于 iOS 的 OneNote 的多身份支持     <!-- 1234281 -->
最终用户现在可对适用于 iOS 的 Microsoft OneNote 使用不同的帐户（工作帐户和个人帐户）。 应用保护策略可应用于工作笔记本中的公司数据，而不会影响个人笔记本。 例如，可通过应用策略允许用户查找工作笔记本中的信息，但阻止用户将工作笔记本中的公司数据复制粘贴到个人笔记本。
 
- 详细了解支持 Intune 的[应用保护和多身份](https://www.microsoft.com/cloud-platform/microsoft-intune-apps)的应用。

### <a name="new-settings-to-allow-and-block-apps-on-samsung-knox-standard-devices"></a>允许和阻止在 Samsung Knox Standard 设备上运行应用的新设置
<!-- 1305423 822899-->  
在此版本中，将添加新的[设备限制设置](../configuration/device-restrictions-android.md)，以便用户能够指定以下应用列表：
 
- 允许用户安装的应用
- 已阻止用户运行的应用
- 设备上对用户隐藏的应用
 
可以通过 URL、包名称或从管理的应用列表中指定应用。

### <a name="new-azure-ad-app-based-conditional-access-policy-ui-link-from-intune"></a>Intune 中新 Azure AD 基于应用的条件访问策略用户界面链接
<!-- 1016201 -->
IT 管理员现可通过 Azure AD 工作负荷中的新条件访问策略 UI 设置基于应用的条件策略。 位于 Azure 门户中 Intune 应用保护部分的基于应用的条件访问策略只是暂时保持现状，未来将逐步强制实施。 此外，还有指向 Intune 工作负荷中新条件访问策略 UI 的便捷链接。

- 深入了解 [Azure AD 中基于应用的条件访问](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-technical-reference)。

<!-- ########################## -->
## <a name="july-2017"></a>2017 年 7 月

### <a name="restrict-android-and-ios-device-enrollment-restriction-by-os-version-----1333256--1245463----"></a>按 OS 版本限制 Android 和 iOS 设备注册 <!--- 1333256,  1245463 --->
Intune 现在支持按操作系统版本号限制 iOS 和 Android 注册。 在  “设备类型限制”下，IT 管理员现可设置平台配置，限制最低和最高操作系统值之间的注册。 Android 操作系统版本必须指定为 Major.Minor.Build.Rev，其中 Minor、Build 和 Rev 是可选的。 iOS 版本必须指定为 Major.Minor.Build，其中 Minor 和 Build 是可选的。 详细了解[设备注册限制](../enrollment/enrollment-restrictions-set.md)。

>[!NOTE]
>请勿通过 Apple 注册计划或 Apple Configurator 限制注册。

### <a name="restrict-android-ios-and-macos-device-personally-owned-device-enrollment-----1333272--1333275-1245709----"></a>限制 Android、iOS 和 macOS 设备的个人私有设备注册 <!--- 1333272,  1333275, 1245709 --->
Intune 可通过将企业设备 IMEI 号码列入允许列表来限制个人设备注册。 Intune 现已使用设备序列号将此功能扩展到 iOS、Android 和 macOS。 通过将序列号上传到 Intune，可将设备预声明为企业所有的设备。 使用注册限制，可以阻止私人拥有的设备 (BYOD)，仅允许企业所有的设备进行注册。 详细了解[设备注册限制](../enrollment/enrollment-restrictions-set.md)。

若要导入序列号，请转至“设备注册”   > “公司设备标识符”  ，单击“添加”  ，然后上传一个 CSV 文件（无标头，含两列，分别是序列号和详细信息，如 IMEI 号）。 若要限制私人拥有的设备，请转到“设备注册” > “注册限制”   。 在“设备类型限制”下，选择“默认”，然后选择“平台配置”。    可以针对 iOS、Android 和 macOS“允许”或“阻止”私人拥有的设备。  


### <a name="new-device-action-to-force-devices-to-sync-with-intune---711369---"></a>用于强制设备与 Intune 同步的新设备操作<!-- 711369 -->
在此版本中，我们添加了一个新的设备操作，可强制所选设备立即通过 Intune 签入。 当设备签入时，该设备会立即收到已分配给自己的任何挂起的操作或策略。  此操作可帮助立即验证和对已分配的策略进行故障排除，而无需等待下一个安排的签入。
有关详细信息，请参阅[同步设备](../remote-actions/device-sync.md)

### <a name="force-supervised-ios-devices-to-automatically-install-the-latest-available-software-update---777100---"></a>强制受监视的 iOS 设备自动安装可用的最新软件更新<!-- 777100 -->
软件更新工作区推出了一项新策略，可在该工作区中强制受监视的 iOS 设备自动安装可用的最新软件更新。 有关详细信息，请参阅[配置 iOS 更新策略](/intune/software-updates-ios)

### <a name="check-point-sandblast-mobile---new-mobile-threat-defense-partner----954651-1172027---"></a>Check Point SandBlast Mobile - 新移动威胁防御伙伴 <!-- 954651, 1172027 -->
可根据 Checkpoint SandBlast Mobile 给出的风险评估，使用条件访问控制移动设备对公司资源的访问，Check Point SandBlast Mobile 是与 Microsoft Intune 集成的移动威胁防御解决方案。

#### <a name="how-integration-with-intune-works"></a>与 Intune 的集成是如何发挥作用的？
基于从运行 Check Point SandBlast Mobile 的设备收集的遥测评估风险。 可基于通过 Intune 设备符合性策略启用的 Check Point SandBlast Mobile 风险评估配置 EMS 条件访问策略。 根据检测到的威胁，可允许或阻止不符合设备访问企业资源。


### <a name="deploy-an-app-as-available-in-the-microsoft-store-for-business---748101---"></a>将应用部署为在适用于企业的 Microsoft Store 中可用应用<!-- 748101 -->
通过此版本，管理员现可将适用于企业的 Microsoft 应用商店分配为可用。 设置为可用时，最终用户可安装来自公司门户应用或网站的应用，而无需重定向到 Microsoft 应用商店。

### <a name="ui-updates-to-the-company-portal-website--1313244-part-1--"></a>公司门户网站的用户界面更新<!--1313244 part 1-->
我们对[公司门户网站](https://portal.manage.microsoft.com)的用户界面进行了几项更新，目的是增强最终用户体验。

- __对应用磁贴的改进__：应用图标现在显示时将具有基于图标主导颜色（如果可检测到）自动生成的背景色。 适用时，此背景会替代以前应用磁贴上显示的灰色边框。

    在即将发布的版本中，公司门户网站会尽可能显示大图标。 建议 IT 管理员使用像素大小不低于 120 x120 的高分辨率图标发布应用。 

- __导航更改__：导航栏项已移至左上角的汉堡菜单。 已删除“类别”页面。 用户现在可在浏览时按类别筛选内容。

- __对精选应用的更新__：我们在网站中添加了一个专用页面，用户可在其中浏览精选的应用，还可以对主页的“精选”部分做出一些用户界面调整。

### <a name="ibooks-support-for-the-company-portal-website--1231841--"></a>针对公司门户网站的 iBooks 支持<!--1231841-->
我们已向公司门户网站添加了一个专用页面，允许用户浏览和下载 iBooks。 


### <a name="additional-help-desk-troubleshooting-details-----applies-to-1263399-1326964-1341642----"></a>有关支持人员故障排除的其他详细信息<!---  Applies to 1263399, 1326964, 1341642 --->
Intune 更新了故障排除的显示内容，并添加了提供给管理人员和支持人员的信息。 现在用户可以看到一个“分配”表，表中按组成员身份汇总了针对用户的所有分配  。 此列表包括：
- 移动应用
- 相容性策略
- 配置文件

此外，“设备”表格现包括“Azure AD 联接类型”和“Azure AD 符合性”列    。 有关详细信息，请参阅[帮助用户解决问题](help-desk-operators.md)。



### <a name="intune-data-warehouse-public-preview"></a>Intune 数据仓库（公共预览版）
Intune 数据仓库每天对数据进行采样，提供租户的历史视图。 可使用 Power BI 文件 (PBIX) 访问数据，该文件是一个 OData 链接，可与许多分析工具兼容或与 REST API 交互。 有关详细信息，请参阅[使用 Intune 数据仓库](../developer/reports-nav-create-intune-reports.md)。


### <a name="light-and-dark-modes-available-for-the-company-portal-app-for-windows-10---676547---"></a>适用于 Windows 10 的公司门户应用的浅色和深色模式<!---676547--->
最终用户将能够为 Windows 10 公司门户应用自定义颜色模式。 用户能够在公司门户应用的“设置”部分进行更改。 更改将在用户重启应用后显示。 对于 Windows 10 版本 1607 及更高版本，应用模式将默认为系统设置。 对于 Windows 10 版本 1511 及更早版本，应用模式将默认为浅色模式。

### <a name="enable-end-users-to-tag-their-device-group-in-the-company-portal-app-for-windows-10---807046--"></a>让最终用户能够在适用于 Windows 10 的公司门户应用中标记其设备组<!---807046-->
最终用户现在能够选择其设备所属的组，方法是直接从 Windows 10 公司门户应用中标记该组。

<!-- ########################## -->
## <a name="june-2017"></a>2017 年 6 月

### <a name="new-role-based-administration-access-for-intune-admins-----1099990---"></a>面向 Intune 管理员的全新基于角色的管理访问权限  <!-- 1099990 -->  
将添加新的条件访问管理员角色，以查看、创建、修改和删除 Azure AD 条件访问策略。 以前，只有全局管理员和安全管理员具有此权限。 可以为 Intune 管理员授予此角色权限，以便他们有权访问条件访问策略。


### <a name="tag-corporate-owned-devices-with-serial-number---1215070---"></a>用序列号标记公司拥有的设备<!-- 1215070 -->  
Intune 现支持上传 iOS、macOS 和 Android 序列号作为公司设备的标识符。 此时，你将不能使用序列号来阻止个人设备进行注册，因为在注册过程中未验证序列号。 在不久的将来将推出按序列号阻止个人设备。


### <a name="new-remote-actions-for-ios-devices---854689---"></a>适用于 iOS 设备的新远程操作<!-- 854689 -->
在此版本中，我们增加了两个适用于托管 Apple 课堂应用的共享 iPad 设备的新远程设备操作：

- [注销当前用户](../remote-actions/device-logout-user.md) - 注销所选 iOS 设备上的当前用户。
- [删除用户](../remote-actions/device-remove-user.md) - 从 iOS 设备上的本地缓存中删除所选用户。


### <a name="support-for-shared-ipads-with-the-ios-classroom-app---1044681---"></a>支持与 iOS Classroom 应用共享 iPad<!-- 1044681 -->
在此版本中，我们扩展了对管理 iOS Classroom 应用的支持，以便为使用托管 Apple ID 登录共享 iPad 的学生提供支持。


### <a name="changes-to-intune-built-in-apps---1332306---"></a>Intune 内置应用的更改<!-- 1332306 -->
之前，Intune 包含了一些可供快速分配的内置应用。 根据你的反馈，我们已将此列表删除，你将不再看到内置应用。
但是，如果你已分配任何内置应用，则在应用列表中仍会看到这些应用。 你可以根据需要继续分配这些应用。
在后续版本中，我们计划提供一种方法，以便用户可以更轻松地在 Azure 门户中选择并分配内置应用。

### <a name="easier-installation-of-office-365-apps----1121362----"></a>更简易的 Office 365 应用安装<!--- 1121362 --->
通过使用新的 Office 365 专业增强版  应用类型，可轻松将 Office 365 专业增强版 2016 应用分配到所管理的运行 Windows 10 最新版本的设备。 此外，如果拥有 Microsoft Project 和 Microsoft Visio 的许可证，还可以安装这两个应用。 所需的应用将被捆绑在一起，并且显示为 Intune 控制台的应用列表中的一个应用。
有关详细信息，请参阅[如何为 Windows 10 添加 Office 365 应用](../apps/apps-add-office365.md)。


### <a name="support-for-offline-apps-from-the-microsoft-store-for-business----777044----"></a>支持适用于企业的 Microsoft Store 中的脱机应用<!--- 777044 --->
从适用于企业的 Microsoft 应用商店购买的离线应用现在将同步到 Azure 门户。 然后，便可以将这些应用部署到设备组或用户组。 脱机应用由 Intune 安装，而不是由应用商店安装。

### <a name="microsoft-teams-is-now-part-of-the-app-based-ca-list-of-approved-apps-----1257019---"></a>Microsoft Teams 现加入已批准应用的基于应用的 CA 列表  <!-- 1257019 -->
对于适用于 Exchange 和 SharePoint Online 的基于应用的条件访问策略，适用于 iOS 和 Android 的 Microsoft Teams 应用现属于已批准应用。 将能够利用基于应用的条件访问通过 Azure 门户中的“Intune 应用保护”边栏选项卡为所有租户配置应用。

### <a name="managed-browser-and-app-proxy-integration---1287310---"></a>Managed Browser 和应用代理集成<!-- 1287310 -->
Intune Managed Browser 现在可与 Azure AD 应用程序代理服务集成，以使用户甚至可在远程工作的时候访问内部网站。 浏览器用户只需像平时一样简单输入网站 URL，Managed Browser 便会通过应用代理 Web 网关路由请求。 有关详细信息，请参阅[使用 Managed Browser 策略管理 Internet 访问](../apps/app-configuration-managed-browser.md)。

### <a name="new-app-configuration-settings-for-the-intune-managed-browser---682951---"></a>Intune Managed Browser 的新应用配置设置<!-- 682951 -->
在此版本中，我们为适用于 iOS 和 Android 的 Intune Managed Browser 应用添加了进一步配置。 现在你能够使用应用配置策略为浏览器配置默认主页和书签。
有关详细信息，请参阅[使用 Managed Browser 策略管理 Internet 访问](../apps/app-configuration-managed-browser.md)

### <a name="bitlocker-settings-for-windows-10----951707---"></a>适用于 Windows 10 的 BitLocker 设置 <!-- 951707 -->
你现在可以使用新的 Intune 设备配置文件为 Windows 10 设备配置 BitLocker 设置。 例如，可以要求加密设备，还可以配置在打开 BitLocker 时应用的进一步设置。
有关详细信息，请参阅[适用于 Windows 10 及更高版本的 Endpoint Protection 设置](../protect/endpoint-protection-windows-10.md)。

### <a name="new-settings-for-windows-10-device-restriction-profile----978527--978550-978569-1050031-1058611-----"></a>Windows 10 设备限制配置文件的新设置<!--- 978527,  978550, 978569, 1050031, 1058611,  --->
在此版本中，我们为 Windows 10 设备限制配置文件添加了新设置，按照以下类别：

- Windows Defender
- 手机网络和连接性
- 锁定屏幕体验
- 隐私
- 搜索
- Windows 聚焦
- Microsoft Edge 浏览器

有关 Windows 10 设置的详细信息，请参阅 [Windows 10 及更高版本的设备限制设置](../configuration/device-restrictions-windows-10.md)。


### <a name="company-portal-app-for-android-now-has-a-new-end-user-experience-for-app-protection-policies--1305217--"></a>适用于 Android 的公司门户应用现推出了全新的应用保护政策最终用户体验<!--1305217-->
根据客户反馈，已修改适用于 Android 的公司门户应用，以便显示“访问公司内容”  按钮。 其目的在于，使最终用户在仅需要访问支持应用保护策略（Intune 移动应用程序管理的一项功能）的应用时，无需完成不必要的注册过程。 可以在[应用 UI 的新增功能](whats-new-app-ui.md)页中查看这些更改。

### <a name="new-menu-action-to-easily-remove-company-portal--1164569--"></a>新增可轻松删除公司门户的菜单操作<!--1164569-->
根据用户反馈，适用于 Android 的公司门户应用新添加了一个菜单操作，可启动对设备中公司门户的删除。 此操作可从 Intune 管理中删除设备，这样用户就可以从设备中删除应用。 你可以在[应用 UI 中的新增功能](whats-new-app-ui.md)页和 [Android 最终用户文档](../user-help/unenroll-your-device-from-intune-android.md)中查看这些更改。

### <a name="improvements-to-app-syncing-with-windows-10-creators-update--676505--"></a>与 Windows 10 创意者更新的应用同步改进<!--676505-->
面向 Windows 10 的公司门户应用，现在将针对具有 Windows 10 创意者更新（版本 1703）的设备自动启动应用安装请求同步。 这将减少“正在挂起同步”状态下的应用安装停止问题。 此外，用户也能够从应用中手动启动同步。 可以在[应用 UI 的新增功能](whats-new-app-ui.md)页中查看这些更改。

### <a name="new-guided-experience-for-windows-10-company-portal---1058938---"></a>Windows 10 公司门户的全新引导式体验<!---1058938--->
适用于 Windows 10 的公司门户应用将为尚未被标识或注册的设备提供引导式的 Intune 演练体验。 新体验提供了循序渐进的说明，引导用户完成 AAD 注册（条件性访问功能所需）和 MDM 注册（设备管理功能所需）。 引导式体验可从公司门户主页获取。 如果用户没有完成注册，仍可以继续使用应用，但可用功能受到限制。

此更新仅在运行 Windows 10 周年更新（内部版本 1607）或更高版本的设备上可见。 可以在[应用 UI 的新增功能](whats-new-app-ui.md)页中查看这些更改。


### <a name="microsoft-intune-and-conditional-access-admin-consoles-are-generally-available"></a>Microsoft Intune 和条件性访问管理控制台正式发布
我们要宣布的是，新的 Azure 门户中 Intune 管理控制台和条件访问管理控制台正式发布。 通过 Azure 门户中 Intune，现在可以在一个位置上统一管理所有 Intune MAM 和 MDM 功能，并利用 Azure AD 分组和定位功能。 Azure 中的条件访问可以跨 Azure AD 和 Intune 在一个统一的控制台中集成丰富的功能。 而且，从管理体验上来看，移动到 Azure 平台还可让你用上现代浏览器。

现在，Intune 在 Azure 门户 (portal.azure.com) 中显示，但不随附“预览”  标签。

此时，现有客户无需进行任何操作，除非你已在消息中心收到过系列消息之一，请求你采取操作，以便我们迁移组。 你可能还收到过一则消息中心通知，通知你由于我方的 bug，迁移将花费更长时间。 我们正在继续努力工作，以迁移任何受影响的客户。

### <a name="improvements-to-the-app-tiles-in-the-company-portal-app-for-ios"></a>对适用于 iOS 的公司门户应用中应用磁贴的改进
我们更新了主页上的应用磁贴设计，现在可以反映你为公司门户设置的品牌颜色。 有关详细信息，请参阅[应用 UI 中的新增功能](whats-new-app-ui.md)。

### <a name="account-picker-now-available-for-the-company-portal-app-for-ios"></a>适用于 iOS 的公司门户应用现在可使用帐户选取器
当 iOS 设备用户登录公司门户时，如果他们使用其工作或学校帐户登录其他 Microsoft 应用，则会看到新的帐户选取器。 有关详细信息，请参阅[应用 UI 中的新增功能](whats-new-app-ui.md)。

<!-- ########################## -->
## <a name="may-2017"></a>2017 年 5 月

### <a name="change-your-mdm-authority-without-unenrolling-managed-devices--1103950--"></a>无需取消注册受管理设备即可更改 MDM 颁发机构<!--1103950-->
你现在可以更改 MDM 颁发机构，而无需联系 Microsoft 支持部门，并且无需取消注册并重新注册现有的受管理设备。 在“Configuration Manager”控制台中，可以通过“设置”将 MDM 颁发机构从“Configuration Manager (混合)”更改为“Microsoft Intune (独立)”，反之亦然。


### <a name="improved-notification-for-samsung-knox-startup-pins--1087143--"></a>改进了 Samsung Knox 启动 PIN 通知<!--1087143-->
如果最终用户需要在 Samsung Knox 设备上设置启动 PIN 以符合加密要求，点击所看到的通知后将会转到“设置”应用中的确切位置。  以前，该通知会将最终用户转到密码更改屏幕。

### <a name="device-enrollment"></a>设备注册

#### <a name="apple-school-manager-asm-support-with-shared-ipad---748864-770395--"></a>共享 iPad 的 Apple School Manager (ASM) 支持<!-- 748864, 770395-->

Intune 现在支持使用 Apple School Manager (ASM) 来替换 Apple 设备注册计划，从而提供 iOS 设备开箱注册体验。 需要执行 ASM 载入才能将 Classroom 应用用于共享 iPad，并且需要执行此操作才会允许通过 Microsoft 学校数据同步 (SDS) 将数据从 ASM 同步到 Azure Active Directory。 有关详细信息，请参阅[通过 Apple School Manager 进行 iOS 设备注册](../enrollment/apple-school-manager-set-up-ios.md)。

> [!NOTE]
> 配置与课堂应用配合使用的共享 iPad 将需要在 Azure 中进行 iOS 教育版配置，这一功能尚未提供。  此功能将很快添加。

### <a name="device-management"></a>设备管理

#### <a name="provide-remote-assistance-to-android-devices-using-teamviewer---675418---"></a>使用 TeamViewer 为 Android 设备提供远程协助<!-- 675418 -->

Intune 现在可使用 [TeamViewer](https://www.teamviewer.com) 软件（另行购买）为运行 Android 设备的用户提供远程协助。 有关详细信息，请参阅[向 Intune 托管的 Android 设备提供远程协助](../remote-actions/teamviewer-support.md)。

### <a name="app-management"></a>应用管理

#### <a name="new-app-protection-policies-conditions-for-mam---679864---"></a>MAM 的新应用保护策略条件<!-- 679864 -->

你现在可以为没有注册用户的 MAM 设置强制执行以下策略的要求：

- 最低应用程序版本
- 最低操作系统版本
- 目标应用程序的最低 Intune APP SDK 版本（仅 iOS）

Android 和 iOS 上均提供此功能。 Intune 支持对 OS 平台版本、应用程序版本和 Intune APP SDK 的最低版本强制要求。 在 iOS 上，已集成 SDK 的应用程序还可在 SDK 级别设置最低版本强制要求。 如果上述三种不同级别中均未满足应用保护策略中的最低要求，用户将无法访问目标应用程序。 此时，用户可以删除其帐户（对于多重身份标识的应用程序）、关闭应用程序，或更新其 OS 或应用程序版本。

你还可以通过配置其他设置来提供建议进行 OS 或应用程序升级的非阻止型通知。 可以关闭此通知，并且应用程序可供正常使用。

有关详细信息，请参阅 [iOS 应用保护策略设置](../apps/app-protection-policy-settings-ios.md)和 [Android 应用保护策略设置](../apps/app-protection-policy-settings-android.md)。

#### <a name="configure-app-configurations-for-android-for-work---621621---"></a>配置适用于 Android for Work 的应用配置<!-- 621621 -->
应用商店中的部分 Android 应用支持托管的配置选项，可让 IT 管理员控制应用在工作配置文件中的运行方式。 使用 Intune，现在可以查看应用支持的配置，并在 Azure 门户中使用配置设计器或 JSON 编辑器对它们进行配置。 有关详细信息，请参阅[使用针对 Android for Work 的应用配置](../apps/app-configuration-policies-use-android.md)。

#### <a name="new-app-configuration-capability-for-mam-without-enrollment---677969---"></a>针对没有注册的 MAM 的新应用注册功能<!-- 677969 -->
你现在可以通过没有注册通道的 MAM 创建应用配置策略。 此功能相当于移动设备管理 (MDM) 应用配置中提供的应用配置策略。 有关使用没有注册的 MAM 的应用配置示例，请参阅[使用 Microsoft Intune 的 Managed Browser 策略管理 Internet 访问](../apps/app-configuration-managed-browser.md)。

#### <a name="configure-allowed-and-blocked-url-lists-for-the-managed-browser---682960---"></a>为 Managed Browser 配置允许和阻止的 URL 列表<!-- 682960 -->
你现在可以使用 Azure 门户中的应用配置设置为 Intune Managed Browser 配置允许和阻止的域和 URL 列表。 无论是在受管还是不受管的设备上使用它，都可以配置这些设置。 有关详细信息，请参阅[使用 Microsoft Intune 的 Managed Browser 策略管理 Internet 访问](../apps/app-configuration-managed-browser.md)。

#### <a name="app-protection-policy-helpdesk-view---1069473---"></a>应用保护策略支持人员视图<!-- 1069473 -->
IT 支持人员用户现在可以在“疑难解答”边栏选项卡中查看用户许可证状态和已分配给用户的应用保护策略应用的状态。 有关详细信息，请参阅[疑难解答](./help-desk-operators.md)。

### <a name="device-configuration"></a>设备配置

#### <a name="control-website-visits-on-ios-devices---723832---"></a>控制 iOS 设备上的网站访问<!-- 723832 -->
你现在可以使用以下两种方法之一控制 iOS 设备的用户可以访问的网站：

- 使用 Apple 内置的 Web 内容筛选器添加允许和阻止的 URL。

- 只允许 Safari 浏览器访问指定的网站。 将在 Safari 中为你指定的每个站点创建书签。

有关详细信息，请参阅[适用于 iOS 设备的 Web 内容筛选器设置](../configuration/ios-device-features-settings.md#web-content-filter)。

#### <a name="preconfigure-device-permissions-for-android-for-work-apps---621614---"></a>预配置 Android for Work 应用的设备权限<!-- 621614 -->
对于已部署到 Android for Work 设备工作配置文件的应用，你现在可以针对各个应用配置权限状态。  默认情况下，要求位置或设备摄像头访问权限等设备权限的 Android 应用将提示用户接受或拒绝权限。  例如，如果应用要使用设备的麦克风，则将提示最终用户授予该应用使用麦克风的权限。 通过此功能，可让你代表最终用户定义权限。  你可以将权限配置为 a) 无需通知用户即自动拒绝；b) 无需通知用户即自动批准，或 c) 提示用户接受或拒绝。 有关详细信息，请参阅 [Microsoft Intune 中的 Android for Work 设备限制设置](../configuration/device-restrictions-android-for-work.md)。

#### <a name="define-app-specific-pin-for-android-for-work-devices---728976-1102534---"></a>为 Android for Work 设备定义特定于应用的 PIN<!-- 728976, 1102534 -->
具有作为 Android for Work 设备管理的工作配置文件的 Android 7.0 及更高版本的设备，可让管理员定义仅适用于工作配置文件中应用于各应用的密码策略。  选项包括：

- 定义仅设备范围的密码策略 - 这是用户解锁整个设备时必须使用的密码。
- 仅定义工作配置文件密码策略 - 只要打开工作配置文件中的任何应用，系统均会提示用户输入密码。
- 同时定义设备和工作配置文件策略 - IT 管理员可以选择同时以不同的长度定义设备密码策略和工作配置文件密码策略（例如，使用四位数的 PIN 来解锁设备，使用六位数的 PIN 来打开任意工作应用）。

有关详细信息，请参阅 [Microsoft Intune 中的 Android for Work 设备限制设置](../configuration/device-restrictions-android-for-work.md)。

> [!NOTE]
> 此选项仅适用于 Android 7.0 及更高版本。  默认情况下，最终用户可以使用两个单独定义的 PIN，或者他们可以选择将两个已定义的 PIN 合并为二者中较强大的一个 PIN。

#### <a name="new-settings-for-windows-10-devices---978585---"></a>适用于 Windows 10 设备的新设置<!-- 978585 -->
我们已添加新的 [Windows 设备限制设置](../configuration/device-restrictions-windows-10.md)，可控制无线显示、设备发现、任务切换和 SIM 卡错误消息等功能。

#### <a name="updates-to-certificate-configuration---918991-and-823198---"></a>证书配置更新<!-- 918991 and 823198 -->
创建 SCEP 证书配置文件时，对于“使用者名称格式”，可以使用适用于 iOS、 Android 和 Windows 设备的“自定义”选项。 在本次更新之前，“自定义”字段仅适用于 iOS 设备。 有关详细信息，请参阅[创建 SCEP 证书配置文件](../protect/certificates-profile-scep.md)。

创建 PKCS 证书配置文件时，对于“使用者可选名称”  ，可以选择“自定义 Azure AD 属性”  。 当选择“自定义 Azure AD 属性”  时，将出现“部门”  选项。 有关详细信息，请参阅[创建 PKCS 证书配置文件](../protect/certficates-pfx-configure.md#create-a-pkcs-certificate-profile)。

#### <a name="configure-multiple-apps-that-can-run-when-an-android-device-is-in-kiosk-mode---662059---"></a>配置多个当 Android 设备处于展台模式时可以运行的应用<!-- 662059 -->
当 Android 设备处于展台模式时，你之前仅能配置一个允许运行的应用。 现在，你可以使用应用 ID、应用商店 URL，或通过选择一个已经管理的 Android 应用配置多个应用。 有关详细信息，请参阅[展台模式设置](../configuration/device-restrictions-android.md#kiosk)。

<!-- ########################## -->
## <a name="april-2017"></a>2017 年 4 月

### <a name="support-for-managing-the-apple-classroom-app"></a>支持管理 Apple Classroom 应用
现在可以在 iPad 设备上管理 iOS Classroom 应用。 使用正确的班级和学生数据设置教师 iPad 上的 Classroom 应用，然后配置已注册到某个班级的学生 iPad，方便使用此应用进行控制。
有关详细信息，请参阅[配置 iOS 教育设置](education-settings-configure-ios.md)。

### <a name="support-for-managed-configuration-options-for-android-apps---621621---"></a>支持 Android 应用的托管配置选项<!-- 621621 -->
Play Store 中支持托管配置选项的 Android 应用现在可以由 Intune 进行配置。  使用此功能，IT 人员可以查看应用支持的配置值列表，并能通过引导式优质 UI 配置这些值。

### <a name="new-android-policy-for-complex-pins---722069---"></a>复杂 PIN 的新 Android 策略<!-- 722069 -->
现在可以在运行 Android 5.0 及更高版本的设备的 Android 设备配置文件中设置数字复杂度的必需[密码](../configuration/device-restrictions-android.md#password)类型。  使用此设置可防止设备用户创建包含重复或连续数字（如 1111 或 1234）的 PIN。

### <a name="additional-support-for-android-for-work-devices"></a>对 Android for Work 设备的其他支持
- **管理密码及工作配置文件设置**<!-- 612808 -->

  通过新的 Android for Work 设备限制策略，现在可让你在管理的 Android for Work 设备上管理密码和工作配置文件设置。

- **允许在工作和个人配置文件之间共享数据**<!-- 1045102 -->

此 Android for Work 设备限制配置文件现在具有新的选项来帮助你配置工作和个人配置文件之间共享的数据。

- **限制工作配置文件和个人配置文件之间的复制和粘贴**<!-- 1046094 -->

  借助适用于 Android for Work 设备的新的自定义设备配置文件，现在可以限制是否允许在工作和个人应用之间进行复制和粘贴操作。

有关详细信息，请参阅 [Android for Work 的设备限制](../configuration/device-restrictions-android-for-work.md)。

### <a name="assign-lob-apps-to-ios-and-android-devices---1057568---"></a>将 LOB 应用分配到 iOS 和 Android 设备<!-- 1057568 -->
现在可以为用户或设备分配适用于 [iOS](../apps/lob-apps-ios.md)（.ipa 文件）和 [Android](../apps/lob-apps-android.md)（.apk 文件）的业务线 (LOB) 应用。


### <a name="new-device-policies-for-ios---723774-723815-723826-723830---"></a>适用于 iOS 的新设备策略<!-- 723774, 723815, 723826, 723830 -->
- **主屏幕上的应用** - 控制用户在[其 iOS 设备的主屏幕](../configuration/ios-device-features-settings.md#home-screen-layout)上看到的应用。 此策略将更改主屏幕的布局，但不会部署任何应用。

- **与 AirPrint 设备的连接** - 控制 iOS 设备的最终用户可以连接到的 [AirPrint 设备](../configuration/ios-device-features-settings.md#airprint)（网络打印机）。

- **与 AirPlay 设备的连接** - 控制 iOS 设备的最终用户可以连接到的 [AirPlay 设备](../configuration/ios-device-features-settings.md)（如 Apple TV）。

- **自定义锁屏界面消息** - 配置用户将在其 iOS 设备的锁屏界面上看到的自定义消息（替换默认的锁屏界面消息）。 有关详细信息，请参阅[激活 iOS 设备上的丢失模式](../remote-actions/device-lost-mode.md)

### <a name="restrict-push-notifications-for-ios-apps---723767---"></a>限制 iOS 应用的推送通知<!-- 723767 -->
在 Intune 设备限制配置文件中，现在可以为 iOS 设备配置以下[通知设置](../configuration/ios-device-features-settings.md#app-notifications)：

- 为指定应用完全启用或禁用通知。
- 在通知中心中打开或关闭指定应用的通知。
- 指定警报类型：“无”  、“横幅”  或“提醒”  。
- 指定是否允许此应用的徽章。
- 指定是否允许通知声音。

### <a name="configure-ios-apps-to-run-in-single-app-mode-autonomously---737837---"></a>配置 iOS 应用以单一应用模式自主运行<!-- 737837 -->
可以使用 Intune 设备配置文件配置 iOS 设备，以[自主单一应用模式](../configuration/device-restrictions-ios.md#autonomous-single-app-mode)运行指定应用。 配置此模式并运行应用时，将锁定设备，因此该设备只能运行该应用。 举个例子，当你配置一个允许用户在设备上进行测试的应用时就是如此。 应用的操作完成或删除此策略时，设备将恢复正常状态。

### <a name="configure-trusted-domains-for-email-and-web-browsing-on-ios-devices---723765---"></a>为 iOS 设备上的电子邮件和 Web 浏览配置受信任的域<!-- 723765 -->
现在可以从 iOS 设备限制配置文件配置以下[域设置](../configuration/device-restrictions-ios.md#domains)：

- **未标记的电子邮件域** - 用户发送或接收的电子邮件如果不匹配在此处指定的域，将标记为不受信任。

- **托管的 Web 域** - 从此处指定的 URL 下载的文档将被视为托管(仅限 Safari)。  

- **Safari 密码自动填充域** - 用户只能在 Safari 中保存与你在此处指定的模式相匹配的 URL 的密码。 若要使用此设置，设备必须处于监督模式，不配置为用于多个用户。 （iOS 9.3 及更高版本）


### <a name="vpp-apps-available-in-ios-company-portal---748782---"></a>iOS 公司门户中可用的 VPP 应用<!-- 748782 -->
现在可以将 iOS 批量购买的 (VPP) 应用作为**可用**安装分配给最终用户。 最终用户必须拥有 Apple Store 帐户，才能安装此类应用。

### <a name="synchronize-ebooks-from-apple-vpp-store---800878---"></a>同步 Apple VPP 应用商店的电子书<!-- 800878 -->
现在可以将 Intune 与从 Apple 批量采购计划应用商店购买的书[同步](../apps/vpp-apps-ios.md)，并将其分配给用户。

### <a name="multi-user-management-for-samsung-knox-standard-devices---971988---"></a>Samsung Knox Standard 设备的多用户管理<!-- 971988 -->
现在，运行 Samsung Knox Standard 的设备支持使用 Intune 进行[多用户管理](../enrollment/android-enroll.md)。 这意味着最终用户可以使用其 Azure Active Directory 凭据登录和注销设备，并且无论是否正在使用，都会集中管理设备。  最终用户登录时，可以访问应用，还可以获得已应用于应用的任何策略。 用户注销时，会清除所有应用数据。

### <a name="additional-windows-device-restriction-settings---818566---"></a>其他 Windows 设备限制设置<!-- 818566 -->
我们添加了对其他 [Windows 设备限制设置](../configuration/device-restrictions-windows-10.md)的支持，如其他 Microsoft Edge 浏览器支持、设备锁屏界面自定义、开始菜单自定义、Windows 聚焦搜索集壁纸和代理设置。

### <a name="multi-user-support-for-windows-10-creators-update---822547---"></a>Windows 10 创意者更新的多用户支持<!-- 822547 -->
我们为运行 Windows 10 创意者更新的设备和加入 Azure Active Directory 域的设备添加了对[多用户管理](../enrollment/windows-enroll.md)的支持。 这意味着不同的标准用户使用其 Azure AD 凭据登录设备时，他们将收到分配给其用户名的所有应用和策略。 用户当前无法将公司门户用于自助服务方案，如安装应用。

### <a name="fresh-start-for-windows-10-pcs---1004830---"></a>Windows 10 电脑的全新启动<!-- 1004830 -->
现在提供 Windows 10 电脑的全新 [Fresh Start 设备操作](../remote-actions/device-fresh-start.md)。  发出此操作后，将会删除 PC 上安装的任何应用，并且 PC 会自动更新到最新版本的 Windows。 这可用于删除新电脑通常附带的预先安装的 OEM 应用。 发出此设备操作时可以配置是否保留用户数据。

### <a name="additional-windows-10-upgrade-paths---903672---"></a>Windows 10 其他升级途径<!-- 903672 -->
现可创建[版本升级策略](../configuration/edition-upgrade-configure-windows-10.md)，将设备升级到以下的其他 Windows 10 版本：

- Windows 10 专业版
- Windows 10 专业版 N
- Windows 10 专业教育版
- Windows 10 专业教育版 N

### <a name="bulk-enroll-windows-10-devices---747607---"></a>批量注册 Windows 10 设备<!-- 747607 -->
现在可以使用 Windows 配置设计器 (WCD) 将运行 Windows 10 创意者更新的大量设备加入到 Azure Active Directory 和 Intune。 若要启用 Azure AD 租户的[批量 MDM 注册](../enrollment/windows-bulk-enroll.md)，请使用 Windows 配置设计器创建将设备加入你的 Azure AD 租户的预配程序包，并将程序包应用到你想要批量注册和管理的公司所有的设备。 将程序包应用到设备后，设备将加入 Azure AD 并在 Intune 中注册，以供 Azure AD 用户登录。  Azure AD 用户是这些设备上的标准用户并接收分配的策略和必需的应用。 目前不支持自助服务和公司门户方案。

### <a name="new-mam-settings-for-pin-and-managed-storage-locations---581122-736644---"></a>PIN 和托管存储位置的新 MAM 设置<!-- 581122, 736644 -->
现在这两个新的应用设置可用于帮助你处理移动应用程序管理 (MAM) 方案：

- **托管设备 PIN 时，禁用应用 PIN** - 检测已注册设备上是否有设备 PIN；如果有，将绕过应用保护策略触发的应用 PIN。 此设置允许减少用户在注册设备上打开已启用 MAM 的应用程序时所看到的 PIN 提示次数。 此功能适用于 Android 和 iOS。

- **选择可将公司数据保存到其中的存储服务** - 允许你指定可将公司数据保存到哪些存储位置。 用户可以保存到所选存储位置服务，这意味着将阻止所有未列出的其他存储位置服务。

  支持的存储位置服务列表：

  - OneDrive
  - Business SharePoint Online
  - 本地存储

### <a name="help-desk-troubleshooting-portal---907448---"></a>技术支持疑难解答门户<!-- 907448 -->
新的[疑难解答门户](help-desk-operators.md)允许技术支持人员和 Intune 管理员查看用户及其设备，并执行任务以解决 Intune 技术问题。

<!-- ########################## -->
## <a name="march-2017"></a>2017 年 3 月

### <a name="support-for-ios-lost-mode--431695--"></a>对 iOS 丢失模式的支持<!--431695-->
对于 iOS 9.3 和更高版本设备，Intune 增加了对**丢失模式**的支持。 现在可以锁定设备以防止所有使用并显示设备锁定屏幕的消息和联系人电话号码。

最终用户将无法解锁设备，直到管理员禁用丢失模式。 启用丢失模式后，可以使用“查找设备”  操作在 Intune 控制台中的地图上显示该设备的地理位置。

此设备必须是处于监督模式下通过 EDP 注册的公司所有的 iOS 设备。

有关详细信息，请参阅[什么是 Microsoft Intune 设备管理](../remote-actions/device-management.md)？

### <a name="improvements-to-device-actions-report--677150--"></a>设备操作报告的改进<!--677150-->
改进了设备操作报告，进而改善了性能。 此外，现可按状态筛选报告。 例如，可筛选报告以仅显示“已完成”的设备操作。

### <a name="custom-app-categories--748805--"></a>自定义应用类别<!--748805-->
现可以为添加到 Intune 的应用创建、编辑和分配类别。 目前，只能以英文指定类别。
请参阅[如何将应用添加到 Intune](../apps/apps-add.md)。

### <a name="assign-lob-apps-to-users-with-unenrolled-devices--748823--"></a>将 LOB 应用分配给未注册设备的用户<!--748823-->
现在，无论用户的设备是否已注册 Intune，都可以设置应用商店到用户业务线应用程序。 如果用户设备未注册 Intune，他们必须转到公司门户网站（而非公司门户应用）安装它。

### <a name="new-compliance-reports--846671--"></a>新相容性报告<!--846671-->
现可通过符合性报告了解设备在公司中的符合性状态，以便快速解决用户遇到的与符合性相关的问题。 可查看以下相关信息

- 设备的总体符合性状态
- 单个设置的符合性状态
- 单个策略的符合性状态

还可使用这些报告深入了解各个设备，查看影响该设备的特定设置和策略。

<!--- You can now create an edition upgrade policy to upgrade devices to the following additional Windows 10 editions:

- Windows 10 Professional
- Windows 10 Professional N
- Windows 10 Professional Education
- Windows 10 Professional Education N --->

### <a name="direct-access-to-apple-enrollment-scenarios--951869--"></a>直接访问 Apple 注册方案<!--951869-->
对于在 2017 年 1 月之后创建的 Intune 帐户，Intune 支持在 Azure 门户中使用注册设备工作负荷直接访问 Apple 注册方案。 以前，只能通过 Azure 门户中的链接访问 Apple 注册预览版。 2017 年 1 月之前创建的 Intune 帐户需要进行一次性迁移，然后才能使用 Azure 中的这些功能。 虽然迁移时间表尚未宣布，但会尽快发布详细信息。 强烈建议创建一个试用帐户，在现有帐户无法访问预览版时测试新体验。


<!-- ########################## -->
## <a name="february-2017"></a>2017 年 2 月

### <a name="ability-to-restrict-mobile-device-enrollment--747600-795782--"></a>限制移动设备注册的功能<!--747600, 795782-->
Intune 新增了注册限制，可控制允许注册的移动设备平台。 Intune 将移动设备平台分为 iOS、macOS，Android、Windows 和 Windows Mobile。

- 限制移动设备注册不会限制电脑客户端注册。  
- 阻止个人自有设备的注册有一个附加选项，该选项仅适用于 iOS 和 Android。

Intune 将所有新设备都标记为个人所有，除非 IT 管理员将设备标记为公司所有，如[本文](../enrollment/device-enrollment.md)所述。

### <a name="view-all-actions-on-managed-devices--677150--"></a>查看受管理设备上的所有操作<!--677150-->
新添加的__设备操作__报表显示了在设备上执行远程操作（如出厂重置）的操作者，还额外显示了该操作的状态。 请参阅 [What is device management?](../remote-actions/device-management.md)（什么是设备管理？）。

### <a name="non-managed-devices-can-access-assigned-apps--664691--"></a>非受管理设备可访问已分配的应用<!--664691-->
公司门户网站上的设计更改之一是，iOS 和 Android 用户能够在其非托管设备上安装分配到的“可用且无需注册”设备。 用户可使用其 Intune 凭据登录到公司门户网站，并查看分配到的应用列表。 “可用且无需注册”应用的应用包可通过公司门户网站进行下载。 需要注册才能安装的应用不受此更改影响，如果用户想安装这类应用，则会提示用户注册其设备。

### <a name="custom-app-categories--748805--"></a>自定义应用类别<!--748805-->
现可以为添加到 Intune 的应用创建、编辑和分配类别。 目前，只能以英文指定类别。
请参阅[如何将应用添加到 Intune](../apps/apps-add.md)。

### <a name="display-device-categories--814654--"></a>显示设备类别<!--814654-->
现在可以将设备类别作为设备列表中的一列进行查看。 并且还可以在设备属性边栏选项卡的属性部分编辑该类别。 请参阅[如何将应用添加到 Intune](../apps/apps-add.md)。

### <a name="configure-windows-update-for-business-settings--776716--"></a>配置适用于企业的 Windows 更新设置<!--776716-->

Windows 即服务是为 Windows 10 提供更新的新方式。 从 Windows 10 开始，任何新的功能更新和质量更新都将包含所有此前更新的内容。 这意味着，只要安装了最新更新，你的 Windows 10 设备将完全保持最新状态。 与以前版本的 Windows 不同的是，现在必须安装完整的更新，而不是部分更新。

借助 Windows Update for Business 可以简化更新管理体验，不需要批准设备组的单个更新。 通过配置更新推出策略仍可以管理环境中的风险，并且 Windows 更新将确保在适当的时间安装更新。 Microsoft Intune 提供在设备上配置更新设置的功能，使你能够延迟更新安装。 Intune 不会存储更新，仅存储更新策略分配。 设备直接访问 Windows 更新以进行更新。使用 Intune 来配置和管理 **Windows 10 更新通道**。 更新通道包含一组设置，可配置何时以及如何安装 Windows 10 更新。 有关详细信息，请参阅[配置 Windows Update for Business 设置](../protect/windows-update-for-business-configure.md)。
