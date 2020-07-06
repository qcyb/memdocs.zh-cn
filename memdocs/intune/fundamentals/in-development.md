---
title: 开发过程中 - Microsoft Intune
titleSuffix: ''
description: 开发过程中的 Microsoft Intune 功能
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/26/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 14b571c069fd2484e7e3fd5f2841f6e5884ecc80
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2020
ms.locfileid: "85502674"
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

### <a name="smime-for-outlook-on-ios-and-android-enterprise-devices-managed-without-enrollment---6517155----"></a>在无需注册即可受管理的 iOS 和 Android Enterprise 设备上为 Outlook 启用 S/MIME<!-- 6517155  -->
你将能够在无需注册即可受管理的 iOS 和 Android Enterprise 设备上使用设备的应用配置策略为 Outlook 启用 S/MIME。 在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)内，依次选择“应用” > “应用配置策略” > “添加” > “托管应用”。 此外，还可以选择是否允许用户在 Outlook 中更改此设置。 若要详细了解 Outlook 配置设置，请参阅 [Microsoft Outlook 配置设置](../apps/app-configuration-policies-outlook.md)。

### <a name="ios-company-portal-will-support-apples-automated-device-enrollment-without-user-affinity---7282707----"></a>iOS 公司门户将支持 Apple 的自动设备注册，而无需用户关联<!-- 7282707  --> 
将支持在设备上使用 Apple 的自动设备注册来注册 iOS 公司门户，而无需分配的用户。 最终用户可以登录 iOS 公司门户，以在无需设备关联即可注册的 iOS/iPadOS 设备上将自己确立为主要用户。 若要详细了解自动设备注册，请参阅[使用 Apple 的自动设备注册自动注册 iOS/iPadOS 设备](../enrollment/device-enrollment-program-enroll-ios.md)。

### <a name="win32-app-installation-notifications-and-the-company-portal---7485945----"></a>Win32 应用安装通知和公司门户<!-- 7485945  -->
最终用户将能够决定 [ Microsoft Intune Web 公司门户](https://portal.manage.microsoft.com/)中显示的应用程序应该是由公司门户应用打开，还是由 Web 公司门户打开。 仅当最终用户已安装公司门户应用，且在浏览器之外启动了 Web 公司门户应用程序时，此选项才可用。

### <a name="the-company-portal-adds-configuration-manager-application-support---4297660---"></a>公司门户现已开始支持 Configuration Manager 应用程序<!-- 4297660 -->
公司门户现在支持 Configuration Manager 应用程序。 借助此功能，最终用户可以在公司门户中同时看到 Configuration Manager 和 Intune 为共同受管理客户部署的应用程序。 此支持有助于管理员整合不同的最终用户门户体验。 有关详细信息，请参阅[在共同受管理设备上使用公司门户应用](https://docs.microsoft.com/mem/configmgr/core/get-started/2020/technical-preview-2006#bkmk_portal)。

<!-- ***********************************************-->
## <a name="device-configuration"></a>设备配置

### <a name="set-device-compliance-state-from-third-party-mdm-partners---6361689-----"></a>从第三方 MDM 合作伙伴设置设备合规状态<!-- 6361689   -->
拥有第三方 MDM 解决方案的 Microsoft 365 客户将能够通过与 Microsoft Intune 设备合规性服务的集成，为 iOS 和 Android 上的 Microsoft 365 应用强制实施条件访问策略。 第三方 MDM 供应商将利用 Intune 设备合规性服务向 Intune 发送设备合规性数据。 然后，Intune 将评估以确定设备是否受信任，并在 Azure AD 中设置条件访问属性。  客户将需要从 Microsoft Endpoint Manager 管理中心或 Azure AD 门户设置 Azure AD 条件访问策略。  


### <a name="new-vpn-settings-for-windows-10-and-newer-devices---6602122----"></a>使用 Windows 10 及更高版本的设备的新 VPN 设置<!-- 6602122  -->
使用 IKEv2 连接类型创建 VPN 配置文件时，可以配置新设置（“设备” > “配置文件” > “创建配置文件” >  针对平台选择“Windows 10 和更高版本”> 针对配置文件选择“VPN”>“基础 VPN”）：

- 设备隧道：允许设备自动连接到 VPN，而无需任何用户交互（包括用户登录）。 此功能要求你启用“始终可用”，并使用“计算机证书”作为身份验证方法。
- 加密套件设置：配置用于保护 IKE 和子安全关联的算法，它们允许你匹配客户端和服务器设置。

若要查看可配置的设置，请转到[使用 Intune 添加 VPN 连接的Windows 设备设置](../configuration/vpn-settings-windows-10.md)。

适用于：
- Windows 10 及更高版本

### <a name="new-features-for-managed-home-screen-on-android-enterprise-device-owner-dedicated-devices-cosu---7414175-7133328-7133720-7134873-7135184----"></a>新增了针对 Android Enterprise 设备所有者专用设备 (COSU) 上托管主屏幕的功能<!-- 7414175 7133328 7133720 7134873 7135184  -->
在 Android Enterprise 设备上，管理员将能够使用设备配置文件在使用多应用展台模式的专用设备上自定义托管主屏幕（依次选择“设备” > “配置文件” > “创建配置文件” > “Android Enterprise”（作为平台）>“仅限设备所有者” > “设备限制”（作为配置文件）>“设备体验”）。

具体而言，你可以：

- 自定义图标、更改屏幕方向，并在锁屏提醒图标上显示应用通知 <!--7414175-->
- 隐藏“托管设置”入口点 <!--7133328-->
- 更轻松地访问调试菜单 <!--7133720-->
- 创建 Wi-Fi 网络的白名单 <!-- 7134873-->
- 更轻松地访问设备信息 <!-- 7135184-->

有关详细信息，请参阅[便于允许或限制功能的 Android Enterprise 设备设置](../configuration/device-restrictions-android-for-work.md)。

适用于：

- Android Enterprise 设备所有者专用设备 (COSU)

<!-- ***********************************************-->
## <a name="device-enrollment"></a>设备注册

### <a name="corporate-owned-personally-enabled-devices-preview--4442275---"></a>由个人启用的企业拥有设备（预览）<!--4442275 -->
Intune 将支持 Android Enterprise 企业拥有设备，其中包含适用于 OS 版本 Android 8 及更高版本的工作配置文件。 包含工作配置文件的企业拥有设备是 Android Enterprise 解决方案集中的企业管理方案之一。 此方案适用于供企业和个人使用的单用户设备。 这种由个人启用的企业拥有 (COPE) 设备方案：

- 提供工作和个人配置文件容器化
- 为管理员提供设备级控制
- 保证最终用户的个人数据和应用程序一直私密化

第一个公共预览版将包括正式发布版中包含的一小部分功能。 其他功能将滚动添加。 第一个预览版中将提供的功能包括：

- 注册：管理员可以使用不会到期的唯一令牌创建多个注册配置文件。 设备注册可通过 NFC、令牌输入、QR 码、零接触或 Knox 移动注册来完成。
- 设备配置：现有完全受管理的专用设备设置的子集。
- 设备符合性：目前可用于完全受管理设备的符合性策略。
- 设备操作：删除设备（恢复出厂设置）、重新启动设备和锁定设备。  
- 应用管理：应用分配、应用配置和关联的报告功能 
- 条件性访问



<!-- ***********************************************-->
## <a name="device-management"></a>设备管理

### <a name="device-compliance-logs-now-in-english--6014904---"></a>设备符合性日志现在采用英语<!--6014904 -->
IntuneDeviceComplianceOrg 日志只有 ComplianceState、OwnerType 和 DeviceHealthThreatLevel 的枚举。 在以后的更新中，这些日志的列中将有英语信息。

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

### <a name="updates-to-the-remote-lock-action-for-macos-devices--7032805---"></a>更新 macOS 设备的远程锁定操作<!--7032805 -->
对 macOS 设备的远程锁定操作的更新将包括：
- 恢复 PIN 将在删除前提前 30 天（而不是 7 天）显示。
- 如果管理员打开了另一个浏览器，并尝试从不同的标签页或浏览器再次触发命令，那么 Intune 将会允许命令完成。 不过，报告状态将设置为“失败”，而不是生成新的 PIN。
- 如果上一个远程锁定命令仍处于挂起状态，或如果设备尚未签回，则管理员将无法发出另一个命令。
这些更改旨在防止正确的 PIN 在多个远程锁定命令后被覆盖。

### <a name="deploy-software-updates-to-macos-devices----3194876---"></a>将软件更新部署到 macOS 设备 <!-- 3194876 -->
你将能够把软件更新部署到 macOS 设备组。 此功能包括关键更新、固件更新、配置文件更新和其他更新。 你将能够在下一次设备签入时发送更新，或选择每周计划在你设置的时间范围内外部署更新。 当你想要在非标准工作时间更新设备时，或者当支持人员已满员时，这会很有帮助。 你还将获得所有已部署更新的 macOS 设备的详细报告。 可以按设备向下钻取报告，以查看特定更新的状态。

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>监视和故障排除

### <a name="additional-data-warehouse-v10-properties---6125732-----"></a>其他 Data Warehouse v1.0 属性<!-- 6125732   -->
通过 Intune Data Warehouse v1.0，可以使用其他属性。 以下属性现在通过 [devices](../developer/reports-ref-devices.md#devices) 实体公开：
- `ethernetMacAddress` - 此设备的唯一网络标识符。
- `office365Version` - 设备上安装的 Office 365 版本。

以下属性现在通过 [devicePropertyHistories](../developer/reports-ref-devices.md#devicepropertyhistories) 实体公开：
- `physicalMemoryInBytes` - 物理内存（以字节为单位）。
- `totalStorageSpaceInBytes` - 总存储容量（以字节为单位）。

有关详细信息，请参阅 [Microsoft Intune 数据仓库 API](../developer/reports-nav-intune-data-warehouse.md)。

### <a name="power-bi-compliance-report-template-v20---636958----"></a>Power BI 合规性报告模板 V2.0<!-- 636958  -->
管理员能够将 Power BI 合规性报表模板的版本从 V1.0 更新到 V2.0。 V2.0 将包括改进后的设计，以及对作为模板一部分出现的计算和数据的更改。 如需了解相关信息，请参阅[使用 Power BI 连接到数据仓库](../developer/reports-proc-get-a-link-powerbi.md)。

<!-- ***********************************************-->
## <a name="role-based-access-control"></a>基于角色的访问控制

### <a name="scope-tag-support-for-customization-policies--6182440---"></a>自定义策略的范围标记支持<!--6182440 -->
你将能够向自定义策略分配范围标记。 为此，请依次转到 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431) > “租户管理”> “自定义”，其中将显示“范围标记”配置选项。

### <a name="assign-profile-and-update-profile-permission-changes--7177586---"></a>“分配配置文件”和“更新配置文件”权限更改<!--7177586 -->
基于角色的访问控制权限将针对“分配配置文件”和“更新配置文件”进行更改：
- 分配配置文件：拥有此权限的管理员还将能够把配置文件分配给令牌，并将默认配置文件分配给令牌。
- 更新配置文件：拥有此权限的管理员将能够只更新现有配置文件。

<!-- ***********************************************-->
## <a name="security"></a>安全

### <a name="app-protection-policy-support-for-symantec-endpoint-security-and-check-point-sandblast----4452423-4731168---"></a>针对 Symantec Endpoint Security 和 Check Point Sandblast 的应用保护策略支持<!--  4452423, 4731168 -->

2019 年 10 月，Intune 应用保护策略新增了使用来自某些 Microsoft 威胁防御合作伙伴（MTD 合作伙伴）的数据的功能。 我们将开始支持以下合作伙伴，以使用应用保护策略来阻止或根据设备运行状况选择性地擦除用户的企业数据：

- Android、iOS 和 iPadOS 上的 Check Point Sandblast
- Android、iOS 和 iPadOS 上的 Symantec Endpoint Security

若要了解如何将应用保护策略与 MTD 合作伙伴配合使用，请参阅[使用 Intune 创建移动威胁防御应用保护策略](../protect/mtd-app-protection-policy.md)。

### <a name="store-the-recovery-key-for-a-macos-device-that-was-encrypted-with-filevault-before-enrolling-with-intune--5239424-----"></a>存储在向 Intune 注册之前已经使用 FileVault 加密的 macOS 设备的恢复密钥<!--5239424   -->
不久，没有使用来自 Intune 的 FileVault 策略进行加密的或在向 Intune 注册之前已加密的 macOS 设备的最终用户将无需解密设备，因此 Intune 可以重新对其进行加密。 相反，当前加密可以保持不变，用户可以转到公司门户网站，在其中用户可以选择“存储恢复密钥”，以提交加密 macOS 设备的个人恢复密钥。 在有效密钥提交后，Intune 就会轮换个人密钥来生成新的密钥，用户仍可通过公司门户网站、iOS/公司门户、Android 公司门户或 Intune 应用使用此密钥。 然后，如果用户被锁在 macOS 设备之外，就可以从任何设备访问这些位置来查看此密钥。

### <a name="hide-the-personal-recovery-key-from-a-device-user-during-macos-filevault-disk-encryption----5475632----"></a>在 macOS FileVault 磁盘加密期间向设备用户隐藏个人恢复密钥<!--  5475632  -->
我们即将向 FileVault 的终结点安全磁盘加密策略（“终结点安全” > “磁盘加密” > “创建配置文件” > “macOS” > “FileVault”）添加名为“隐藏恢复密钥”的新设置。 如果你启用这一新设置，Intune 就会在加密期间向 macOS 设备的用户隐藏个人恢复密钥。 通过在此期间隐藏密钥，你可以确保它的安全性，因为用户在等待设备加密时无法将密钥记录下来。 相反，如果需要恢复，用户可以随时使用任何设备通过 Intune 公司门户网站查看其个人恢复密钥。

### <a name="improved-view-of-security-baseline-details-for-devices---5536846-----"></a>改进了设备的安全基线详细信息视图<!-- 5536846   -->
我们正在努力改进你在向下钻取设备详细信息（“终结点安全” > “设备”）时看到的安全基线设置详细信息。  对于每个分配的安全基线，你将能够查看每个设置的详细信息的简单列表，其中包括设置类别、设置名称以及相应设备上每个设置的状态。

### <a name="manage-source-locations-for-definition-updates-with-endpoint-security-antivirus-policy-for-windows-10-devices---6347801----"></a>使用 Windows 10 设备的终结点安全防病毒策略管理定义更新的源位置<!-- 6347801  -->  
我们即将向 Windows 10 设备的终结点安全防病毒策略的“更新”类别（“终结点安全”>“防病毒”****>“创建策略” > “Windows 10 及更高版本” > “Microsoft Defender 防病毒”）添加两个新设置，这可以帮助你管理设备如何获取更新定义。

有了这两个新设置，可以将 UNC 文件共享添加为定义更新的下载源位置，并定义联系不同源位置的顺序。 这两个新设置将管理以下 Defender CSP：

- [signatureupdatefilesharessources](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-signatureupdatefilesharessources)
- [signatureupdatefallbackorder](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-signatureupdatefallbackorder)

### <a name="endpoint-detection-and-response-policy-for-onboarding-tenant-attached-devices-to-mdatp-is-moving-out-of-preview---7303816-----"></a>用于将“租户附加”设备加入到 MDATP 的终结点检测和响应策略即将退出预览版<!-- 7303816   -->
作为 Intune 中终结点安全的一部分，用于 Configuration Manager 管理的设备的终结点检测和响应 (EDR) 策略支持将很快退出预览版，并成为正式发布版（“终结点安全” > “终结点检测和响应” > “创建策略” > “Windows 10 和 Windows Server”）。 配置 [Configuration Manager 的租户附加](../../configmgr/tenant-attach/device-sync-actions.md)时，可以使用 EDR 策略将 Configuration Manager 管理的设备加入到 Microsoft Defender 高级威胁防护 (Microsoft Defender ATP)。 

### <a name="improvements-for-the-security-baselines-node---7433136-----"></a>改进安全基线节点<!-- 7433136   -->
为了提高 Microsoft Endpoint Manager 管理中心内安全基线节点的可用性，我们将为每个基线删除“概述”选项卡，而将打开基线“配置文件”选项卡（“终结点安全” > “安全基线” > “基线”）。

每个基线的“概述”页面显示图表和磁贴，它们聚合了你部署的上一个基线版本的结果。 此类信息与你向下钻取版本来查看更多详情时看到的信息是相同的。 在“概述”页面删除后，你在直接向下钻取版本时仍能看到这些图表和聚合详细信息。  

### <a name="firewall-rule-migration-tool-preview---6423187----"></a>防火墙规则迁移工具（预览）<!-- 6423187  -->
作为公共预览版，我们正在开发基于 PowerShell 的工具来迁移 Windows Defender 防火墙规则。 当你安装并运行此工具时，它会自动为 Intune 创建基于当前配置的 Windows 10 客户端的终结点安全防火墙规则策略。

### <a name="new-settings-for-the-device-control-profile-in-endpoint-security-attack-surface-reduction-policy--7032084---"></a>在终结点安全“攻击面减少”策略的“设备控制”配置文件中新增设置<!--7032084 -->
我们即将向终结点安全“攻击面减少”策略的“设备控制”配置文件（“终结点安全” > “攻击面减少” > “创建策略” > “Windows 10 及更高版本” > “设备控制”）添加一些 Windows 10 设备设置。 

新设置将与“设备配置”的[“设备限制”配置文件](../configuration/device-restrictions-windows-10.md)中可用的设置相同。 要添加到“设备控制”配置文件的设置应包括各种蓝牙设置。  


<!-- ***********************************************-->
## <a name="notices"></a>通知

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>另请参阅

有关最近开发的详细信息，请参阅 [Microsoft Intune 中的新增功能](whats-new.md)。
