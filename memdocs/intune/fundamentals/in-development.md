---
title: 开发过程中 - Microsoft Intune
titleSuffix: ''
description: 开发过程中的 Microsoft Intune 功能
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/30/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2a807a90cdca18d79e7b92b4efeb56d341da2596
ms.sourcegitcommit: 6a6a713fc1090e03893d80f4259dc7300fb1d5ff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/31/2020
ms.locfileid: "80438723"
---
# <a name="in-development-for-microsoft-intune---april-2020"></a>在 Microsoft Intune 的开发中 - 2020 年 4 月

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

### <a name="update-to-android-app-configuration-policies---6113334----"></a>更新到 Android 应用配置策略<!-- 6113334  -->
将更新 Android 应用配置策略，以允许管理员在创建应用配置文件之前选择设备注册类型。 此功能将添加到基于注册类型（工作配置文件或设备所有者）的证书配置文件帐户中。  发布时，将发生以下情况：

- 在此功能发布之前创建的、没有任何与此策略关联的证书配置文件的现有策略将默认为适用于设备注册类型的工作配置文件和设备所有者配置文件。
- 在此功能发布之前创建的、具有与证书配置文件关联的现有策略将默认为仅“工作配置文件”。
- 如果已创建新的配置文件，并且为设备注册类型选择了“工作配置文件”和“设备所有者配置文件”，则无法将证书配置文件与应用配置策略关联。
- 如果已创建新的配置文件，并且选择了仅“工作配置文件”，那么可以使用在设备配置下创建的工作配置文件证书策略。
- 如果已创建新的配置文件，并且选择了仅“设备所有者”，那么可以使用在设备配置下创建的设备所有者证书策略。

现有策略不会修正或颁发新证书。

此外，我们还将添加 Gmail 和 9 个电子邮件配置文件，它们将同时适用于“工作配置文件”和“设备所有者”注册类型，包括对这两种电子邮件配置类型使用证书配置文件。  在“工作配置文件”的“设备配置”下创建的任何 Gmail 或 9 个策略将继续应用于设备，没有必要将它们移动到应用配置策略。

在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，可以通过选择“应用” > “应用配置策略”来查找应用配置策略   。 若要详细了解应用配置策略，请参阅 [Microsoft Intune 的应用配置策略](../apps/app-configuration-policies-overview.md)。

### <a name="microsoft-teams-is-now-included-in-the-office-365-suite-for-macos---5903936----"></a>Microsoft Teams 现已包含在适用于 macOS 的 Office 365 套件中<!-- 5903936  -->
除了现有 Microsoft Office 应用（Word、Excel、PowerPoint、Outlook 和 OneNote）外，在 Microsoft Endpoint Manager 中分配了 Microsoft Office for macOS 的用户现在还将获得 Microsoft Teams。 Intune 将识别已安装其他 Office for macOS 应用的现有 Mac 设备，并在下次设备使用 Intune 签入时尝试安装 Microsoft Teams。 在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，可以通过选择“应用” > “macOS” > “添加”来查找适用于 macOS 的 Office 365 套件     。 有关详细信息，请参阅[使用 Microsoft Intune 将 Office 365 分配给 macOS 设备](../apps/apps-add-office365-macos.md)。

### <a name="group-targeting-support-for-customization-pane----4722837----"></a>“自定义”窗格的组目标支持 <!-- 4722837  -->
将能够使“自定义”窗格中的设置指向用户组。 在 Intune 门户中，选择“客户端应用” > “自定义”   。 有关更多详细信息，请参阅[如何自定义 Intune 公司门户应用、公司门户网站和 Intune 应用](company-portal-app.md]。

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

### <a name="device-configuration-profile-settings-and-values-will-be-updated-for-windows-platforms---4091122---"></a>将为 Windows 平台更新设备配置文件设置和值<!-- 4091122 -->
为 Windows 平台创建设备配置文件时（“设备”   > “配置文件”   > “创建配置文件”  > 任意“Windows”  平台选项），某些设置及其值与 CSP 不同，可能会令人不解。 将更新这些设置名称及其值，以清晰地反应其功能。

适用于：

- Windows 10 及更高版本的设备配置文件
- Windows Holographic for Business 设备配置文件
- Windows 8.1 设备配置文件
- Windows Phone 8.1 设备配置文件

### <a name="configure-the-microsoft-defender-atp-app-for-macos-----5520115----"></a>配置适用于 macOS 的 Microsoft Defender ATP 应用  <!-- 5520115  -->
很快就可以在 Endpoint Protection 设备配置文件中为运行 macOS 的设备配置 Microsoft Defender ATP 应用的[设置](../protect/endpoint-protection-macos.md)了（转到“设备”   >   “配置文件” >       “创建配置文件”，选择“macOS”作为“平台”，然后选择“Endpoint Protection”作为“配置文件类型”）。 macOS 设备配置将提供 8 项设置。 

macOS 10.13 (High Sierra) 及更高版本支持 Defender ATP，必须在应用这些设置之后才能将 [Microsoft Defender ATP](../apps/apps-advanced-threat-protection-macos.md) 应用部署到设备。  应在部署应用之前将这些设置下发到设备。 不支持 macOS 的 Beta 版本。

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>macOS Endpoint Protection 设备配置策略中新增 FileVault 设置<!-- 5459801   -->
我们将向 [macOS Endpoint Protection](../protect/endpoint-protection-macos.md) 模板中的 FileVault 类别添加新设置：隐藏恢复密钥。 （转到“设备”   >   “配置文件” >       “创建配置文件”，选择“macOS”作为“平台”，然后选择“Endpoint Protection”作为“配置文件类型”）。 此设置将在 FileVault 2 加密过程中向最终用户隐藏个人密钥。 设备用户可随时从 iOS 公司门户应用或公司门户网站查看其加密 macOS 设备的个人恢复密钥。 若要查看个人恢复密钥，用户可以转到设备详细信息，然后单击“获取恢复密钥”  。

此设置在以前创建的策略中不可用。 需要重新创建 FileVault 策略以配置此设置，才能利用它。 

### <a name="send-push-notifications-as-an-action-for-non-compliance----1733150-----"></a>针对不合规以操作形式发送推送通知 <!-- 1733150   -->
对于 iOS 和 Android 平台，我们将添加针对不合规的新操作，该操作将通过公司门户应用发送应用推送通知。 用户可以单击通知，这将启动公司门户应用，然后显示不合规的原因。 管理员可以在 Microsoft Endpoint Manager 管理中心配置此新操作，方法是：转到“设备” > “合规性策略” > “创建策略”，然后选择“操作”即可发送应用推送通知     。

### <a name="pre-release-testing-for-managed-google-play-apps---2681933----"></a>托管的 Google Play 应用的预发布测试<!-- 2681933  -->
使用[Google Play 的应用预发布测试的封闭测试轨道](https://support.google.com/googleplay/android-developer/answer/3131213)的组织将能够使用 Intune 管理这些轨迹。 将可以有选择地将发布到 Google Play 预生产轨道的业务线应用分配给试验组，以便执行测试。 在 Intune 中，还将能够查看是否已向应用发布了预生产生成测试跟踪，并将跟踪分配给 AAD 用户或设备组。 此功能适用于我们当前支持的所有 Android Enterprise 方案（工作配置文件、完全托管和专用）。 在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，可以通过选择“应用” > “Android” > “添加”来添加托管的 Google Play 应用    。 有关详细信息，请参阅[使用 Intune 将托管 Google Play 应用添加到 Android Enterprise 设备](../apps/apps-add-android-for-work.md)。

### <a name="manage-smime-settings-for-outlook-on-android---6517085-----"></a>管理 Android 上 Outlook 的 S/MIME 设置<!-- 6517085   -->
将能够使用应用配置策略在运行 Android Enterprise 的设备上管理 Outlook 的 S/MIME 设置。 还将可以选择是否允许设备用户在 Outlook 设置中启用或禁用 S/MIME。 若要使用适用于 Android 的应用配置策略，请在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，转到“应用” > “应用配置策略” > “添加” > “托管设备”     。

### <a name="additional-options-in-sso-and-sso-app-extension-profiles-on-iosipados-devices---6504155----"></a>iOS/iPadOS 设备上 SSO 和 SSO 应用扩展配置文件中的其他选项<!-- 6504155  -->
在 iOS/iPadOS 设备上，可以：

- 在 SSO 配置文件（“设备” > “配置文件” > “创建配置文件” > “iOS/iPadOS”(针对平台) >“设备功能”(针对配置文件) >“单一登录”），将 Kerberos 主体名称设置为 SSO 配置文件中的安全帐户管理器 (SAM) 帐户名称       。 
- 在 SSO 应用扩展配置文件（“设备” > “配置文件” > “创建配置文件” > “iOS/iPadOS”(针对平台) >“设备功能”(针对配置文件) >“单一登录应用扩展”）中，使用新的 SSO 应用扩展类型，以较少的单击次数配置 iOS/iPadOS Microsoft Azure AD 扩展       ）。 可以为共享设备启用 Azure AD 扩展，并向扩展发送特定于扩展的数据。

适用于：
- iOS/iPadOS 13.0+

有关在 iOS/iPadOS 设备上使用单一登录的详细信息，请参阅[单一登录应用扩展概述](../configuration/device-features-configure.md#single-sign-on-app-extension)和[单一登录设置列表](../configuration/ios-device-features-settings.md#single-sign-on-app-extension)。

<!-- ***********************************************-->
## <a name="device-enrollment"></a>设备注册

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>自带设备可以使用 VPN 进行部署<!--5015344 -->
新的 Autopilot 配置文件“跳过域连接检查”切换允许部署混合 Azure AD Join 设备，而无需使用自己的第三方 Win32 VPN 客户端访问企业网络  。 若要查看新的切换，请前往 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431) > “设备”  > “Windows” > “Windows 注册” > “部署配置文件” > “创建配置文件” > “全新体验 (OOBE)”       。

<!-- ***********************************************-->
## <a name="device-management"></a>设备管理

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>对 BYOD 设备的 PowerShell 脚本支持<!-- 1862833  -->
PowerShell 脚本将支持 Intune 中已注册到 Azure AD 的设备。 有关 PowerShell 的详细信息，请参阅[在 Intune 中的 Windows 10 设备上使用 PowerShell 脚本](../apps/intune-management-extension.md)。 此功能不支持运行 Windows 10 家庭版的设备。

### <a name="script-support-for-macos-devices---4280361----"></a>对 macOS 设备的脚本支持<!-- 4280361  -->
你将能够向 macOS 设备添加和部署脚本。 此支持扩展了你配置 macOS 设备的能力，让你不再限于使用 macOS 设备上的本机 MDM 功能进行配置。

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics 将包括设备详细信息日志<!--6014987  -->
Intune 设备详细信息日志将在“报告” > “Log Analytics”中提供   。 可以关联设备详细信息以生成自定义查询和 Azure 工作簿。

### <a name="push-notification-when-device-ownership-type-is-changed---5575875----"></a>更改设备所有权类型时的推送通知<!-- 5575875  -->
你将能够配置一条推送通知，以便在 Android 和 iOS 公司门户用户的设备所有权类型从“个人”更改为“公司”时，将推送通知发送给他们作为隐私保护。 通过选择“租户管理” > “自定义”，可以在 Microsoft Endpoint Manager 中找到此设置   。 若要了解有关设备所有权如何影响最终用户的详细信息，请参阅[更改设备所有权](../enrollment/corporate-identifiers-add.md#change-device-ownership)。

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



