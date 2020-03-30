---
title: 开发过程中 - Microsoft Intune
titleSuffix: ''
description: 开发过程中的 Microsoft Intune 功能
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/21/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 18b42dffc2c34adea1f70c4587b5eb5384d0a778
ms.sourcegitcommit: 795e8a6aca41e1a0690b3d0d55ba3862f8a683e7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/24/2020
ms.locfileid: "80220126"
---
# <a name="in-development-for-microsoft-intune---march-2020"></a>Microsoft Intune 开发过程中的功能 - 2020 年 3 月

为了辅助就绪性和计划，此页面列出了正在开发但尚未发布的 Intune UI 更新和功能。 除本页上的信息外，另请注意： 

- 如果我们预计你需要在更改之前采取措施，我们将在 Office 消息中心发布补充性的文章。
- 当某个功能进入生产（无论是提供预览还是正式发布），其功能描述都将从本页移动到[新增功能](whats-new.md)。
- 此页和[新增功能页](whats-new.md)会定期更新。 返回查看其他更新。
- 有关策略性可交付内容和时间线，请参阅 [Microsoft 365 路线图](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS)。

> [!NOTE]
> 此页反映了我们目前希望在未来版本中提供的 Intune 功能。 日期和各项功能可能会更改。 本页未介绍我们正在开发的全部功能。

**RSS 源**：通过将以下 URL 复制并粘贴到源阅读器中，可以在页面更新时收到通知：`https://docs.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us`

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

### <a name="company-portal-for-ios-to-support-landscape-mode--6048329----"></a>适用于 iOS 的公司门户将支持横向模式<!--6048329  -->
用户将能够使用自己选择的的屏幕方向注册设备、查找应用并获得 IT 支持。 应用会自动检测并调整屏幕以适应纵向或横向模式，除非你将屏幕锁定为纵向模式。

### <a name="improved-sign-in-experience-in-company-portal-for-android---6103997----"></a>改进了适用于 Android 的公司门户中的登录体验<!-- 6103997  -->
我们即将更新适用于 Android 的公司门户应用中多个登录屏幕的布局，让用户体验更现代化、更简洁。

<!-- ***********************************************-->
## <a name="device-configuration"></a>设备配置

### <a name="wired-network-device-configuration-profiles-for-macos-devices---3508686----"></a>macOS 设备的有线网络设备配置文件<!-- 3508686  -->
可使用新的 macOS 设备配置文件来配置有线网络（“设备配置” > “配置文件” > “创建配置文件” > 选择“macOS”作为平台 > 选择“有线网络”作为配置文件类型      ）。 使用此功能创建 802.1x 配置文件来管理有线网络，并将这些有线网络部署到 macOS 设备。

适用于：
- macOS

### <a name="improved-user-interface-experience-when-creating-configuration-profiles-on-iosipados-and-macos-devices---5569008-5569039-5569057-5569110-5569116-5569131-5569139-5569153-5859984----"></a>改善了在 iOS/iPadOS 和 macOS 设备上创建配置文件时的用户界面体验<!-- 5569008-5569039-5569057-5569110-5569116-5569131-5569139-5569153-5859984  -->
为 iOS/iPadOS 或 macOS 设备创建配置文件时，将更新“终结点管理”管理中心中的体验。 此更改会影响以下设备配置文件（“设备” > “配置文件” > “创建配置文件” >  选择“iOS”或“macOS”作为平台      ）：

- 自定义：iOS/iPadOS、macOS
- 设备功能：iOS/iPadOS、macOS
- 设备限制：iOS/iPadOS、macOS
- 终结点保护：macOS
- 扩展：macOS
- 首选项文件：macOS

### <a name="improved-user-interface-experience-when-creating-oemconfig-configuration-profiles-on-android-enterprise-devices---5568645-----"></a>改善了在 Android 企业版设备上创建 OEMConfig 配置文件时的用户界面体验<!-- 5568645   -->
创建或编辑适用于 Android 企业版设备的 OEMConfig 配置文件时，将更新“终结点管理”管理中心中的体验。 更新的体验将提供已配置设置的摘要的概览。 此更改会影响 OEMConfig 设备配置文件（“设备” > “配置文件” > “创建配置文件” >  选择“Android 企业版”作为平台 > 选择“OEMConfig”作为配置文件类型      ）。

此功能适用于：
- Android Enterprise 

### <a name="device-configuration-profile-settings-and-values-will-be-updated-for-windows-platforms---4091122---"></a>将为 Windows 平台更新设备配置文件设置和值<!-- 4091122 -->
为 Windows 平台创建设备配置文件时（“设备”   > “配置文件”   > “创建配置文件”  > 任意“Windows”  平台选项），某些设置及其值与 CSP 不同，可能会令人不解。 将更新这些设置名称及其值，为清晰地反应其功能。

适用于：

- Windows 10 及更高版本的设备配置文件
- Windows Holographic for Business 设备配置文件
- Windows 8.1 设备配置文件
- Windows Phone 8.1 设备配置文件

### <a name="improved-user-interface-experience-when-creating-device-restrictions-profiles-on-android-and-android-enterprise-devices---5841361---"></a>改进了在 Android 和 Android Enterprise 设备上创建设备限制配置文件时的用户界面体验<!-- 5841361 -->
将改进在“终结点管理”管理中心为 Android 或 Android Enterprise 设备创建配置文件时的体验。 此更改会影响以下设备配置文件（“设备”   >   “配置文件” >   “创建配置文件” >    选择“Android 设备管理员”或“Android Enterprise”平台）：

- 设备限制：Android 设备管理员
- 设备限制：Android Enterprise 设备所有者
- 设备限制：Android Enterprise 工作配置文件

有关可配置设备限制的详细信息，请参阅 [Android 设备管理员](../configuration/device-restrictions-android.md)和 [Android Enterprise ](../configuration/device-restrictions-android-for-work.md)。

### <a name="configure-the-microsoft-defender-atp-app-for-macos-----5520115----"></a>配置适用于 macOS 的 Microsoft Defender ATP 应用  <!-- 5520115  -->
很快就可以在 Endpoint Protection 设备配置文件中为运行 macOS 的设备配置 Microsoft Defender ATP 应用的[设置](../protect/endpoint-protection-macos.md)了（转到“设备”   >   “配置文件” >       “创建配置文件”，选择“macOS”作为“平台”，然后选择“Endpoint Protection”作为“配置文件类型”）。 macOS 设备配置将提供 8 项设置。 

macOS 10.13 (High Sierra) 及更高版本支持 Defender ATP，必须在应用这些设置之后才能将 [Microsoft Defender ATP](../apps/apps-advanced-threat-protection-macos.md) 应用部署到设备。  应在部署应用之前将这些设置下发到设备。 不支持 macOS 的 Beta 版本。

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>macOS Endpoint Protection 设备配置策略中新增 FileVault 设置<!-- 5459801   -->
我们将向 [macOS Endpoint Protection](../protect/endpoint-protection-macos.md) 模板中的 FileVault 类别添加新设置：隐藏恢复密钥。 （转到“设备”   >   “配置文件” >       “创建配置文件”，选择“macOS”作为“平台”，然后选择“Endpoint Protection”作为“配置文件类型”）。 此设置将在 FileVault 2 加密过程中向最终用户隐藏个人密钥。 设备用户可随时从 iOS 公司门户应用或公司门户网站查看其加密 macOS 设备的个人恢复密钥。 若要查看个人恢复密钥，用户可以转到设备详细信息，然后单击“获取恢复密钥”  。

此设置在以前创建的策略中不可用。 需要重新创建 FileVault 策略以配置此设置，才能利用它。 

### <a name="configure-delivery-optimization-agent-when-downloading-win32-app-content---5410945----"></a>下载 Win32 应用内容时配置传递优化代理<!-- 5410945  -->
你将能够配置传递优化代理以，使其基于分配在后台或前台模式下下载 Win32 应用内容。 对于现有的 Win32 应用，将继续在后台模式下下载内容。 在 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，选择“应用” > “所有应用” > 选择 Win32 应用 > “属性”     。 选择“分配”旁边的“编辑”   。  若要编辑分配，请在“必需”部分的“模式”下选择“包括”    。  你将在“应用设置”部分中找到新设置（如果可用）  。 有关传递优化的详细信息，请参阅 [Win32 应用管理 - 传递优化](../apps/apps-win32-app-management.md#delivery-optimization)。

<!-- ***********************************************-->
<!--## Device enrollment-->

<!-- ***********************************************-->
## <a name="device-management"></a>设备管理

### <a name="change-primary-user-for-windows-devices----3794742---"></a>更改 Windows 设备的主要用户 <!-- 3794742 -->
你能够更改 Windows 混合设备和 Azure AD 联接设备的主要用户。 为此，请转到“Intune”   > “设备”   > “所有设备”  > 选择设备 >“属性”   > “主要用户”  。

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>对 BYOD 设备的 PowerShell 脚本支持<!-- 1862833  -->
PowerShell 脚本将支持 Intune 中已注册到 Azure AD 的设备。 有关 PowerShell 的详细信息，请参阅[在 Intune 中的 Windows 10 设备上使用 PowerShell 脚本](../apps/intune-management-extension.md)。 此功能不支持运行 Windows 10 家庭版的设备。

### <a name="new-information-in-device-details---5604099---"></a>设备详细信息中的新信息<!-- 5604099 -->
以下信息将显示在设备的“概述”  页上：

- 存储容量（设备上的物理存储量）
- 内存容量（设备上的物理内存量）

### <a name="script-support-for-macos-devices---4280361----"></a>对 macOS 设备的脚本支持<!-- 4280361  -->
你将能够向 macOS 设备添加和部署脚本。 此支持扩展了你配置 macOS 设备的能力，让你不再限于使用 macOS 设备上的本机 MDM 功能进行配置。

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
<!--
## Monitor and troubleshoot
-->

<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
## <a name="security"></a>安全

### <a name="derived-credentials-support-on-android-fully-managed-devices--4839592--"></a>Android 完全托管设备上的派生凭据支持<!--4839592-->
你将能够在 Android 企业版完全托管设备上使用派生凭据。 将添加有关为 Entrust Datacard、Intercede 和 DISA Purebred 检索派生凭据的支持。 你将能够使用派生凭据进行应用身份验证、Wi-Fi、VPN 或 S/MIME 签名，并/或通过支持该凭据的应用进行加密。

### <a name="privacy-preferences-settings-for-macos-devices---2934232---"></a>macOS 设备的隐私首选项设置<!-- 2934232 --> 
随着 macOS Catalina 10.15 的发布，Apple 添加了新的安全和隐私增强功能。 默认情况下，应用程序和进程只有取得用户许可才能访问特定数据。 如果用户不提供许可，则应用程序和进程可能无法正常工作。 Intune 即将添加对以下设置的支持：对于运行 macOS 10.14 及更高版本的设备，允许 IT 管理员代表最终用户授予或不授予数据访问许可。 这些设置将确保应用程序和进行继续正常工作，并减少向最终用户显示的提示。

### <a name="updated-ui-text-and-labels-for-windows-10-endpoint-protection-profile-settings---5983747---"></a>更新了 Windows 10 Endpoint Protection 配置文件设置的 UI 文本和标签<!-- 5983747 -->
我们将更新以 Windows 10 设备配置文件的形式配置的各项设置的文本，让你能更轻松地了解设置的用途和效果。

我们将更新的设置包括以下 Windows 10 设备配置文件：

- [设备限制](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus) > Microsoft Defender 防病毒  
- [Endpoint Protection](../protect/endpoint-protection-windows-10.md) > Microsoft Defender 防病毒

不会更改 Intune 支持的设置。 这只是对“Microsoft 终结点管理”管理中心 UI 文本的更新。

<!-- ***********************************************-->
## <a name="notices"></a>通知

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>另请参阅

有关最近开发的详细信息，请参阅 [Microsoft Intune 中的新增功能](whats-new.md)。
