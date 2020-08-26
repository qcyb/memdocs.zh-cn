---
title: 开发过程中 - Microsoft Intune
titleSuffix: ''
description: 开发过程中的 Microsoft Intune 功能
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/06/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0d443cb784c19956f52347a10f4123c622ab82a8
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820049"
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

### <a name="the-windows-company-portal-adds-configuration-manager-application-support---4297660---"></a>Windows 公司门户现已开始支持 Configuration Manager 应用程序<!-- 4297660 -->
Windows 公司门户现在支持 Configuration Manager 应用程序。 借助此功能，最终用户可以在 Windows 公司门户中同时看到 Configuration Manager 和 Intune 为共同受管理客户部署的应用程序。 此支持有助于管理员整合不同的最终用户门户体验。 有关详细信息，请参阅[在共同受管理设备上使用公司门户应用](https://docs.microsoft.com/mem/configmgr/core/get-started/2020/technical-preview-2006#bkmk_portal)。

<!-- ***********************************************-->
## <a name="device-configuration"></a>设备配置

### <a name="create-pkcs-certificate-profiles-for-android-enterprise-fully-managed-devices-cobo---4839686---"></a>为 Android Enterprise 完全托管设备创建 PKCS 证书配置文件 (COBO)<!-- 4839686 -->
你可以创建 PKCS 证书配置文件，以便将证书部署到 Android Enterprise 设备所有者和工作配置文件设备（“设备” > “配置文件” > “创建配置文件” > “Android Enterprise”>“仅限设备所有者”，或“Android Enterprise”>“仅限工作配置文件”[针对平台]>“PKCS”[针对配置文件]）。

不久，你将能够为 Android Enterprise 完全托管设备创建 PKCS 证书配置文件。 Intune PFX 证书连接器是必需的。 如果不使用 SCEP 并且只使用 PKCS，则可以在安装新的 PFX 连接器后删除 NDES 连接器。 新的 PFX 连接器导入 PFX 文件，并将 PKCS 证书部署到所有平台。

有关 PKCS 证书的详细信息，请参阅[配置 PKCS 证书并用于 Intune](../protect/certficates-pfx-configure.md)。

适用于：
- Android Enterprise 完全托管 (COBO)

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

### <a name="deploy-software-updates-to-macos-devices----3194876---"></a>将软件更新部署到 macOS 设备 <!-- 3194876 -->
你将能够把软件更新部署到 macOS 设备组。 此功能包括关键更新、固件更新、配置文件更新和其他更新。 你将能够在下一次设备签入时发送更新，或选择每周计划在你设置的时间范围内外部署更新。 当你想要在非标准工作时间更新设备时，或者当支持人员已满员时，这会很有帮助。 你还将获得所有已部署更新的 macOS 设备的详细报告。 可以按设备向下钻取报告，以查看特定更新的状态。

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


<!-- ***********************************************-->
## <a name="notices"></a>通知

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>另请参阅

有关最近开发的详细信息，请参阅 [Microsoft Intune 中的新增功能](whats-new.md)。
