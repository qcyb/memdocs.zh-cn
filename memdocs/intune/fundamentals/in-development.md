---
title: 开发过程中 - Microsoft Intune
titleSuffix: ''
description: 开发过程中的 Microsoft Intune 功能
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 90039e9bb75bcf7c266ac033408f87d37e27ef8d
ms.sourcegitcommit: 7a5196d4d9736c5cd52a23155c479523e52a097d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2020
ms.locfileid: "84436748"
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

### <a name="improvements-to-devices-page-of-iosipados-and-macos-company-portals---6055001----"></a>对 iOS/iPadOS 和 macOS 公司门户“设备”页的改进<!-- 6055001  -->
我们对 iOS/iPadOS 和 Mac 公司门户应用的“设备”页的用户体验进行了一些改进。 我们改进了“设备”页，使其具有更现代的外观和更好的设备信息结构。 通过使用具有定义的节标头的单个列，组织的 iOS/iPadOS 和 macOS 用户能够轻松查看其设备的状态，以确保它们保持安全并保持对组织资源的访问权限。 此外，我们还为设备不合规的用户添加了更为清晰的消息传送和其他故障排除步骤。 有关公司门户的详细信息，请参阅[如何自定义 Intune 公司门户应用、公司门户网站和 Intune 应用](../apps/company-portal-app.md)。

### <a name="improvements-to-the-company-portal-for-macos-enrollment-experience---6444452----"></a>对公司门户中的 macOS 注册体验的改进<!-- 6444452  -->
用于 macOS 注册的公司门户提供的注册过程更简单，与用于 iOS 注册的公司门户高度一致。 设备用户将看到：  
- 流畅的用户界面。  
- 改进的注册清单。  
- 更清晰的设备注册说明。  
- 改进的疑难解答选项。  

有关公司门户的详细信息，请参阅[如何自定义 Intune 公司门户应用、公司门户网站和 Intune 应用](../apps/company-portal-app.md)。

### <a name="use-autonomous-single-app-mode-settings-to-configure-the-ios-company-portal-to-be-a-sign-insign-out-app---7055619----"></a>使用自治单应用模式设置将 iOS 公司门户配置为登录/注销应用<!-- 7055619  -->
你将能够将 iOS 公司门户配置为使用自治单应用模式 (ASAM)。 可以使用 Microsoft Endpoint Manager 控制台中的 ASAM 设置将 iOS 公司门户配置为在注销和登录时进入和退出单应用模式。 当公司门户处于 ASAM 时，用户在登录到公司门户之前将无法使用设备上的任何其他应用或主页按钮。 注销后，公司门户将返回到单应用模式。 

要在 Microsoft Endpoint Manager 中将公司门户配置为 ASAM，请选择“设备” > “配置文件” > “创建配置文件”。 选择“iOS/iPadOS”作为平台，并选择“设备限制”作为配置文件。 在“配置设置”选项卡中，选择“自治单应用模式”。 将“应用名称”设置为 `Company Portal`，并将“应用程序包 ID”设置为 `com.app.CompanyPortal`。 有关详细信息，请参阅[自治单应用模式 (ASAM)](../configuration/device-restrictions-ios.md#autonomous-single-app-mode-asam) 和[单应用模式](https://support.apple.com/guide/mdm/single-app-mode-mdm80a981/1/web/1)。

<!-- ***********************************************-->
## <a name="device-configuration"></a>设备配置

### <a name="set-device-compliance-state-from-third-party-mdm-partners---6361689-----"></a>从第三方 MDM 合作伙伴设置设备合规状态<!-- 6361689   -->
你将很快就能允许在 Azure Active Directory (Azure AD) 中设置由第三方移动设备管理 (MDM) 合作伙伴管理的 iOS 或 Android 设备的合规状态。

为合作伙伴合规性配置 Intune 后，由第三方 MDM 合作伙伴管理的设备的合规性数据将发送到 Intune，以进行合规性评估。 然后，将结果传递到 Azure AD，其中的合规性数据用于为这些设备强制执行条件访问策略。

将很快包含对以下合作伙伴的支持：
- VMware WorkspaceONE（以前称为 AirWatch）

若要启用设备合规性合作伙伴，需要在 Microsoft Endpoint Manager 管理中心中使用新节点：“租户管理” > “连接器和令牌” > “合作伙伴合规性管理”，你将在其中选择“添加合规合作伙伴”。

### <a name="add-a-link-to-your-company-portal-support-website-to-emails-for-noncompliance---7225498------"></a>将指向公司门户支持网站的链接添加到设备不合规的用户的电子邮件中<!-- 7225498    -->
我们正在将新设置添加到电子邮件通知模板，该模板会将指向公司门户网站的链接添加到发送给设备不合规的用户的电子邮件通知中。 （“终结点安全性” > “设备合规性” > “通知” > “创建通知”）。  由于使用不合规的设备而收到电子邮件的用户可以使用该链接打开网站，以详细了解其设备不合规的原因。

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>macOS Endpoint Protection 设备配置策略中新增 FileVault 设置<!-- 5459801   -->
我们将向 [macOS Endpoint Protection](../protect/endpoint-protection-macos.md) 模板中的 FileVault 类别添加新设置：隐藏恢复密钥。 （转到“设备” > “配置文件” >  “创建配置文件”，选择“macOS”作为“平台”，然后选择“Endpoint Protection”作为“配置文件类型”）。 此设置将在 FileVault 2 加密过程中向最终用户隐藏个人密钥。 设备用户可随时从 iOS 公司门户应用或公司门户网站查看其加密 macOS 设备的个人恢复密钥。 若要查看个人恢复密钥，用户可以转到设备详细信息，然后单击“获取恢复密钥”。

此设置在以前创建的策略中不可用。 需要重新创建 FileVault 策略以配置此设置，才能利用它。 

### <a name="configure-content-caching-on-macos-devices---7106872---"></a>在 macOS 设备上配置内容缓存<!-- 7106872 -->
在 macOS 设备上，可以创建配置内容缓存的配置文件（“设备” > “配置文件” > “创建配置文件” >  针对平台选择“macOS” > 针对配置文件选择“设备功能”）。 使用这些设置可以删除缓存，允许共享缓存，设置磁盘上的缓存限制等。

有关内容缓存的详细信息，请参阅 [ContentCaching](https://developer.apple.com/documentation/devicemanagement/contentcaching)（打开 Apple 的网站）。

若要查看当前可配置的设置，请转到 [Intune 中的 macOS 设备功能设置](../configuration/macos-device-features-settings.md)。

适用于：
- macOS

### <a name="new-vpn-settings-for-windows-10-and-newer-devices---6602122----"></a>使用 Windows 10 及更高版本的设备的新 VPN 设置<!-- 6602122  -->
使用 IKEv2 连接类型创建 VPN 配置文件时，可以配置新设置（“设备” > “配置文件” > “创建配置文件” >  针对平台选择“Windows 10 和更高版本”> 针对配置文件选择“VPN”>“基础 VPN”）：

- 设备隧道：允许设备自动连接到 VPN，无需任何用户交互（包括用户登录）。 此功能要求你启用“始终可用”，并使用“计算机证书”作为身份验证方法。
- 加密套件设置：配置用于保护 IKE 和子安全关联的算法，它们允许你匹配客户端和服务器设置。

若要查看可配置的设置，请转到[使用 Intune 添加 VPN 连接的Windows 设备设置](../configuration/vpn-settings-windows-10.md)。

适用于：
- Windows 10 及更高版本

### <a name="block-shared-ipad-temporary-sessions-on-shared-ipad-devices---6613794---"></a>阻止共享 iPad 设备上的共享 iPad 临时会话<!-- 6613794 -->
在 Intune 中，有一个新的“阻止共享 iPad 临时会话”设置，可阻止共享 iPad 设备上的临时会话（“设备” > “配置文件” > “创建配置文件”： >  针对平台选择“iOS/iPadOS”> 针对配置文件类型选择“设备限制”>“共享 iPad”）。 启用后，最终用户无法使用来宾帐户。 他们必须使用其管理的 Apple ID 和密码登录设备。 

有关可配置的设置的详细信息，请参阅[允许或限制功能的 iOS 和 iPadOS 设备设置](../configuration/device-restrictions-ios.md)。

适用于：
- 运行 iOS/iPadOS 13.4 及更高版本的共享 iPad 设备

### <a name="use-microsoft-launcher-as-the-default-launcher-for-fully-managed-android-enterprise-devices---4927976----"></a>使用微软桌面作为完全托管的 Android Enterprise 设备的默认启动程序<!-- 4927976  -->
在 Android Enterprise 设备所有者设备上，可以将微软桌面设置为完全托管的设备的默认启动程序（“设备” > “配置文件” > “创建配置文件” >  针对平台选择“Android Enterprise”>“设备所有者” >  针对配置文件选择“设备限制”>“设备体验”）。 若要配置所有其他微软桌面设置，请使用应用配置策略。 

此外，还有一些其他 UI 更新，包括将“专用设备”重命名为“设备体验”。

要查看可以限制的所有设置，请参阅[使用 Intune 允许或限制功能的 Android Enterprise 设备设置](../configuration/device-restrictions-android-for-work.md)。 

适用于：
- Android Enterprise 设备所有者完全托管的设备 (COBO)

### <a name="add-new-schema-settings-and-search-for-existing-schema-settings-using-oemconfig-on-android-enterprise---6394386----"></a>添加新架构设置，并使用 Android Enterprise 上的 OEMConfig 搜索现有架构设置<!-- 6394386  -->
在 Intune 中，可以使用 OEMConfig 来管理 Android Enterprise 设备上的设置（“设备” > “配置文件” > “创建配置文件” >  针对平台选择“Android Enterprise”> 针对配置文件选择“OEMConfig”）。 使用“配置设计器”时，将显示应用架构中的属性。 现在可在“配置设计器”中执行以下操作：
- 向应用架构添加新设置。
- 在应用架构中搜索新设置和现有设置。

若要详细了解 Intune 中的 OEMConfig 配置文件，请参阅[通过 Microsoft Intune 中的 OEMConfig 使用和管理 Android Enterprise 设备](../configuration/android-oem-configuration-overview.md)。

适用于：
- Android Enterprise

<!-- ***********************************************-->
## <a name="device-enrollment"></a>设备注册

### <a name="automated-device-enrollment-sync-errors---6988214---"></a>自动设备注册同步错误<!-- 6988214 -->
将为 iOS/iPadOS 和 macOS 设备报告新错误，包括：
- 电话号码中的字符无效或该字段为空。 
- 配置文件的配置名称无效或为空。 
- 游标值无效/过期或找不到游标。
- 令牌被拒绝或已过期。 
- 部门字段为空或长度过长。 
- Apple 找不到配置文件，需要创建一个新配置文件。 
- 删除的 Apple Business Manager 设备的计数将添加到“概览”页，可以在其中看到设备状态。

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>自带设备可以使用 VPN 进行部署<!--5015344 -->
使用新的 Autopilot 配置文件“跳过域连接检查”切换，可以部署混合 Azure AD 联接设备，而无需使用自己的第三方 Win32 VPN 客户端访问企业网络。 若要查看新的切换，请前往 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431) > “设备”  > “Windows” > “Windows 注册” > “部署配置文件” > “创建配置文件” > “全新体验 (OOBE)”     。

### <a name="shared-ipads-for-business--6367326---"></a>适用于企业的共享 iPad<!--6367326 -->
你将能够使用 Intune 和 Apple Business Manager 轻松、安全地设置共享 iPad，使多个员工可以共享设备。 Apple 的[共享 iPad](https://developer.apple.com/education/shared-ipad/) 可以为多个用户提供个性化的体验，同时保留用户数据。 借助托管 Apple ID，用户在登录组织中的任何共享 iPad 后即可访问他们的应用、数据和设置。 共享 iPad 使用联合标识。

为了解此功能，请转到 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431) > “设备” > “iOS” > “iOS 注册” > “注册计划令牌”>“选择令牌”>“配置文件” > “创建配置文件” > “iOS”。 在“管理设置”页上，选择“不使用用户关联注册”，你会看到“共享 iPad”选项  。

**适用于：** iPadOS 13.4 及更高版本。 此版本添加了对使用共享 iPad 的临时会话的支持，因此用户不使用托管 Apple ID 也可访问设备。 注销后，设备会清除所有用户数据，以便立即准备投入使用，因此无需擦除设备。 

<!-- ***********************************************-->
## <a name="device-management"></a>设备管理

### <a name="change-primary-user-on-co-managed-devices--7319183---"></a>更改共同管理的设备上的主要用户<!--7319183 -->
你将能够为共同管理的 Windows 设备更改设备的主要用户。 有关如何查找和更改主要用户的详细信息，请参阅[查找 Intune 设备的主要用户](../remote-actions/find-primary-user.md)。

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>对 BYOD 设备的 PowerShell 脚本支持<!-- 1862833  -->
PowerShell 脚本将支持 Intune 中已注册到 Azure AD 的设备。 有关 PowerShell 的详细信息，请参阅[在 Intune 中的 Windows 10 设备上使用 PowerShell 脚本](../apps/intune-management-extension.md)。 此功能不支持运行 Windows 10 家庭版的设备。

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics 将包括设备详细信息日志<!--6014987  -->
Intune 设备详细信息日志将在“报告” > “Log Analytics”中提供 。 可以关联设备详细信息以生成自定义查询和 Azure 工作簿。

### <a name="setting-the-intune-primary-user-also-sets-the-azure-ad-owner-property--7319227---"></a>设置 Intune 主要用户还会设置 Azure AD 所有者属性<!--7319227 -->
这一即将发布的功能在设置 Intune 主要用户的同时，还将自动设置新注册的混合 Azure AD 联接设备上的所有者属性。 有关主要用户的详细信息，请参阅[查找 Intune 设备的主要用户](../remote-actions/find-primary-user.md)。

这是对注册过程的更改，并且仅适用于新注册的设备。 对于现有混合 Azure AD 联接设备，必须手动更新 Azure AD 所有者属性。 为此，可以使用[更改主要用户功能](../remote-actions/find-primary-user.md#change-a-devices-primary-user)或[脚本](https://github.com/microsoftgraph/powershell-intune-samples/tree/master/ManagedDevices)。

当 Windows 10 设备建立混合 Azure Active Directory 联接时，该设备的第一个用户将成为 Endpoint Manager 中的主要用户。  当前，未在相应的 Azure AD 设备对象上设置该用户。 在将 Azure AD 门户中的“所有者”属性与 Microsoft Endpoint Manager 管理中心中的“主要用户”属性进行比较时，这会导致不一致。 Azure AD 所有者属性用于保护对 BitLocker 恢复密钥的访问。 该属性未在混合 Azure AD 联接设备上填充。 此限制可防止从 Azure AD 设置 BitLocker 恢复的自助服务。 这一即将推出的功能可解决此限制。

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

### <a name="remote-lock-pin-availability-for-macos-devices--7281557--"></a>macOS 设备远程锁定固定的可用时间<!--7281557-->
macOS 设备远程锁定固定的可用时间将从 7 天增至 30 天。

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
<!--## Security-->


<!-- ***********************************************-->
## <a name="notices"></a>通知

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>另请参阅

有关最近开发的详细信息，请参阅 [Microsoft Intune 中的新增功能](whats-new.md)。
