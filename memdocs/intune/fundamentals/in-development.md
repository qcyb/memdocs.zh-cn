---
title: 开发过程中 - Microsoft Intune
titleSuffix: ''
description: 开发过程中的 Microsoft Intune 功能
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/28/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7827c85585d630f64ba9c6d342b6275fca506b1d
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906961"
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

本文的上次更新日期在上面的标题下方列出  。

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

### <a name="support-for-multiple-accounts-in-company-portal-for-mac---5779449----"></a>支持 Mac 公司门户中的多个帐户<!-- 5779449  -->
macOS 设备上的公司门户现在会缓存用户帐户，使登录更容易。 用户不再需要在每次启动应用程序时登录到公司门户。 此外，如果缓存了多个用户帐户，则公司门户将显示帐户选取器，使用户无需输入其用户名。 

### <a name="auto-update-vpp-available-apps---3640511----"></a>自动更新 VPP 可用应用<!-- 3640511  -->
如果为 VPP 令牌启用了“自动应用更新”功能，则发布为批量购买计划 (VPP) 可用应用的应用会自动更新  。 目前，VPP 可用应用不会自动更新。 最终用户必须转到公司门户，如果发布了更新版本，则重新安装该应用。 但是，必需应用当前支持自动更新。

### <a name="customize-self-service-device-actions-in-the-company-portal--4393379----"></a>自定义公司门户中的自助设备操作<!--4393379  -->
你将能够自定义在公司门户应用和网站中向最终用户显示的可用自助服务设备操作。 为了帮助防止发生意外的设备操作，可以通过选择“租户管理” > “自定义” > “创建” > “隐藏功能”，为公司门户应用配置这些设置     。 提供了以下选项：
- 隐藏公司 Windows 设备上的“删除”按钮  。
- 隐藏公司 Windows 设备上的“重置”按钮  。
- 隐藏公司 iOS 设备上的“重置”按钮  。
- 隐藏公司 iOS 设备上的“删除”按钮  。

有关详细信息，请参阅[公司门户中的用户自助设备操作](../apps/company-portal-app.md#user-self-service-device-actions-from-the-company-portal)。

### <a name="unified-delivery-of-azure-ad-enterprise-or-office-online-applications-in-the-company-portal--4404429---"></a>在公司门户中统一交付 Azure AD 企业版或 Office Online 应用程序<!--4404429 -->
你将能够在公司门户中切换（“隐藏”或“显示”）显示 Azure AD 企业版或 Office Online 应用程序   。 每个用户将从所选的 Microsoft 服务中看到整个应用程序目录。 默认情况下，每个附加的应用源会设置为“隐藏”  。 此功能将首先在 2005 版本中的公司门户网站中生效，并应兼容 Windows、iOS/iPadOS 和 macOS 公司门户中的支持。 在 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，选择“租户管理” > “自定义”，查找此未来设置   。 如需了解相关信息，请参阅[如何自定义 Intune 公司门户应用、公司门户网站和 Intune 应用](../apps/company-portal-app.md)。

### <a name="search-the-intune-docs-from-the-company-portal---1736480---"></a>从公司门户搜索 Intune 文档<!-- 1736480 -->
现在可以从 macOS 应用的公司门户直接搜索 Intune 文档。 在菜单栏中，选择“帮助” > “搜索”，然后输入搜索的关键字以快速找到问题的答案   。

### <a name="company-portal-for-android-will-guide-users-to-get-apps-after-work-profile-enrollment----6103999----"></a>适用于 Android 的公司门户会指导用户在注册了工作配置文件后获取应用 <!-- 6103999  -->
我们正在改进公司门户中的应用内指南，使用户能够更轻松地查找和安装应用。  在工作配置文件管理中注册后，用户将看到一条消息，内容是他们可在 Google Play 的徽章版本中找到建议的应用。 用户还将在左侧的公司门户抽屉中看到一个新的“获取应用”链接  。 为给这些新体验和改进体验腾出位置，将删除“应用”选项卡  。 

### <a name="android-company-portal-user-experience---5736084---"></a>Android 公司门户用户体验<!-- 5736084 -->
在 2005 版本的 Android 公司门户中，收到应用保护策略发出的警告、阻止或擦除命令的 Android 设备的最终用户将看到新的用户体验。 最终用户将看到一条完整的页面消息，其中描述了警告、阻止或擦除的原因，以及解决此问题的步骤，并且不再看到当前的对话框体验。 有关详细信息，请参阅[适用于 Android 设备的应用保护体验](../apps/app-protection-policy.md#app-protection-experience-for-android-devices)和 [Microsoft Intune 中的 Android 应用保护策略设置](../apps/app-protection-policy-settings-android.md)。


<!-- ***********************************************-->
## <a name="device-configuration"></a>设备配置

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

### <a name="configure-system-extensions-on-macos-devices---6255624----"></a>在 macOS 设备上配置系统扩展<!-- 6255624  -->
在 macOS 设备上，你可以创建一个内核扩展配置文件，在内核级别配置设置（“设备” > “配置文件” >  平台的“macOS”> 配置文件的“内核扩展”）     。 Apple 最终会弃用内核扩展，并在将来的版本中将它们替换为系统扩展。 系统扩展在用户空间中运行，并且不会向内核授予访问权限。 目的是为了提高安全性并提供更多的最终用户控制，同时在内核级别限制攻击。 内核扩展和系统扩展都允许用户安装可扩展操作系统的本机功能的应用扩展。

在 Intune 中，你可以同时配置内核扩展和系统扩展（“设备” > “配置文件” >  平台的“macOS”> 配置文件的“内核扩展”）     。 内核扩展适用于 10.13.2 和更高版本。 系统扩展适用于 10.15 和更高版本。 从 macOS 10.15 到 macOS 10.15.4，内核扩展和系统扩展可并行运行。 

要了解 macOS 设备上的内核扩展，请参阅[添加 macOS 内核扩展](../configuration/kernel-extensions-overview-macos.md)。

适用于：
- macOS 10.15 及更高版本

<!-- ***********************************************-->
## <a name="device-enrollment"></a>设备注册

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>自带设备可以使用 VPN 进行部署<!--5015344 -->
此功能可能会延迟。

### <a name="automated-device-sync-interval-down-to-12-hours--3077535---"></a>自动设备同步间隔缩短到 12 小时<!--3077535 -->
对于 Apple 的自动设备注册，Intune 和 Apple Business Manager 之间的自动设备同步间隔将从 24 小时缩短到 12 小时。 有关同步的详细信息，请参阅[同步托管设备](../enrollment/device-enrollment-program-enroll-ios.md#sync-managed-devices)。

### <a name="autopilot-support-for-hololens-2-devices--6305220--"></a>Hololens 2 设备的 Autopilot 支持<!--6305220-->
Windows Autopilot 将支持 Hololens 2 设备。 有关在 Intune 中使用 Autopilot 的详细信息，请参阅[使用 Windows Autopilot 在 Intune 中注册 Windows 设备](../enrollment/enrollment-autopilot.md)。

### <a name="enrollment-restrictions-will-support-scope-tags--4209550---"></a>注册限制将支持作用域标记<!--4209550 -->
你将能够向注册限制分配作用域标记。 为此，请转到 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431) > “设备” > “注册限制” > “创建限制”    。 创建任一一种限制，然后将看到“作用域标记”页  。

### <a name="shared-ipads-for-business--6367326---"></a>适用于企业的共享 iPad<!--6367326 -->
你将能够使用 Intune 和 Apple Business Manager 轻松、安全地设置共享 iPad，使多个员工可以共享设备。 Apple 的[共享 iPad](https://developer.apple.com/education/shared-ipad/) 可以为多个用户提供个性化的体验，同时保留用户数据。 借助托管 Apple ID，用户在登录组织中的任何共享 iPad 后即可访问他们的应用、数据和设置。 共享 iPad 使用联合标识。

为了了解此功能，请转到[Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431) > “设备” > “iOS” > “iOS 注册” > “注册计划令牌”> 选择令牌** >“配置文件” > “创建配置文件” > “iOS”        。 在“管理设置”页上，选择“不使用用户关联注册”，你会看到“共享 iPad”选项    。

**适用于：** iPadOS 13.4 及更高版本。 此版本添加了对使用共享 iPad 的临时会话的支持，因此用户不使用托管 Apple ID 也可访问设备。 注销后，设备会清除所有用户数据，以便立即准备投入使用，因此无需擦除设备。 

<!-- ***********************************************-->
## <a name="device-management"></a>设备管理

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>对 BYOD 设备的 PowerShell 脚本支持<!-- 1862833  -->
PowerShell 脚本将支持 Intune 中已注册到 Azure AD 的设备。 有关 PowerShell 的详细信息，请参阅[在 Intune 中的 Windows 10 设备上使用 PowerShell 脚本](../apps/intune-management-extension.md)。 此功能不支持运行 Windows 10 家庭版的设备。

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics 将包括设备详细信息日志<!--6014987  -->
Intune 设备详细信息日志将在“报告” > “Log Analytics”中提供   。 可以关联设备详细信息以生成自定义查询和 Azure 工作簿。


### <a name="macos-script-support---6376978----"></a>macOS 脚本支持<!-- 6376978  -->
macOS 的脚本支持现已正式发布。 此外，我们将添加对用户分配的脚本和已注册 Apple 自动设备注册（原名“设备注册计划”）的 macOS 设备的支持。 有关详细信息，请参阅[在 Intune 中的 macOS 设备上使用 Shell 脚本](../apps/macos-shell-scripts.md)。

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>监视和故障排除

### <a name="power-bi-compliance-report-template-v20---636958----"></a>Power BI 合规性报告模板 V2.0<!-- 636958  -->
管理员能够将 Power BI 合规性报表模板的版本从 V1.0 更新到 V2.0。 V2.0 将包含改进的设计，以及模板中显示的计算和数据的更改。 如需了解相关信息，请参阅[使用 Power BI 连接到数据仓库](../developer/reports-proc-get-a-link-powerbi.md)。

<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
## <a name="security"></a>安全

### <a name="derived-credentials-support-for-disa-purebred-on-android-devices--4839592---"></a>派生凭据支持在 Android 设备上使用 DISA Purebred<!--4839592 -->
你将能够在 Android Enterprise 完全托管设备上使用“DISA Purebred”作为[派生凭据](../protect/derived-credentials.md)提供程序（“租户管理” > “连接器和令牌” > “派生凭据”）     。 现将支持为 DISA Purebred 检索派生凭据。 你将能够使用派生凭据进行应用身份验证、Wi-Fi、VPN 或 S/MIME 签名，并/或通过支持该凭据的应用进行加密。 

在 4 月，Intune 新增支持将 Entrust Datacard 和 Intercede 用作派生凭据的提供程序   。 

### <a name="privacy-preferences-settings-for-macos-devices---2934232---"></a>macOS 设备的隐私首选项设置<!-- 2934232 --> 
随着 macOS Catalina 10.15 的发布，Apple 添加了新的安全和隐私增强功能。 默认情况下，应用程序和进程只有取得用户许可才能访问特定数据。 如果用户不提供许可，则应用程序和进程可能无法正常工作。 Intune 即将添加对以下设置的支持：对于运行 macOS 10.14 及更高版本的设备，允许 IT 管理员代表最终用户授予或不授予数据访问许可。 这些设置将确保应用程序和进行继续正常工作，并减少向最终用户显示的提示。


### <a name="duplicate-your-policies-in-endpoint-security---5892558-----"></a>在终结点安全性中复制策略<!-- 5892558   -->
你将能够选择已在 Microsoft 终结点管理器管理中心的“终结点安全性”节点中创建的策略，然后复制该策略以创建副本。  你将能够复制的策略包括你为以下项目创建的策略： 

- 防病毒
- 磁盘加密
- 防火墙
- 终结点检测和响应
- 攻击面减少
- 帐户保护

复制操作将创建原始策略的副本，然后可以重命名和编辑该副本。 副本不包含原始策略的分配。

### <a name="send-push-notifications-as-an-action-for-non-compliance----1733150-----"></a>针对不合规以操作形式发送推送通知 <!-- 1733150   -->
对于 iOS 和 Android 平台，我们将添加针对不合规的新操作，该操作将通过公司门户应用发送应用推送通知。 用户可以单击通知，这将启动公司门户应用，然后显示不合规的原因。 管理员可以在 Microsoft Endpoint Manager 管理中心配置此新操作，方法是：转到“设备” > “合规性策略” > “创建策略”，然后选择“操作”即可发送应用推送通知     。 

### <a name="new-profile-for-endpoint-security-firewall-policy---5653324-----"></a>终结点安全性防火墙策略的新配置文件<!-- 5653324   -->
作为预览版，我们将在 Intune 的终结点安全性的防火墙策略中添加适用于 Windows 10 和更高版本的附加配置文件（“终结点安全性” > “防火墙” > “创建策略”> 选择“Windows 10 和更高版本”）     。 

此新配置文件的每个实例最多支持 150 条自定义 Microsoft Defender 防火墙规则  。 利用 Microsoft Defender 防火墙规则配置文件，你可以定义粒度 Windows 防火墙规则以允许或阻止 Windows 10 中的端口和应用程序。

<!-- ***********************************************-->
## <a name="notices"></a>通知

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>另请参阅

有关最近开发的详细信息，请参阅 [Microsoft Intune 中的新增功能](whats-new.md)。



