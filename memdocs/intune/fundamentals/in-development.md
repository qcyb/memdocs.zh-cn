---
title: 开发过程中 - Microsoft Intune
titleSuffix: ''
description: 开发过程中的 Microsoft Intune 功能
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6f2bb971da483cd86e143673b57e8e5e09f943a5
ms.sourcegitcommit: 9a700a72735f9a316bdb51c44f86f9cc3bfb7be2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83764197"
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

### <a name="company-portal-for-android-will-guide-users-to-get-apps-after-work-profile-enrollment----6103999----"></a>适用于 Android 的公司门户会指导用户在注册了工作配置文件后获取应用 <!-- 6103999  -->
我们正在改进公司门户中的应用内指南，使用户能够更轻松地查找和安装应用。  在工作配置文件管理中注册后，用户将看到一条消息，内容是他们可在 Google Play 的徽章版本中找到建议的应用。 用户还将在左侧的公司门户抽屉中看到一个新的“获取应用”链接  。 为给这些新体验和改进体验腾出位置，将删除“应用”选项卡  。 

<!-- ***********************************************-->
## <a name="device-configuration"></a>设备配置

### <a name="device-configuration-profile-settings-and-values-will-be-updated-for-windows-platforms---4091122---"></a>将为 Windows 平台更新设备配置文件设置和值<!-- 4091122 -->
为 Windows 平台创建设备配置文件时（“设备”   > “配置文件”   > “创建配置文件”  > 任意“Windows”  平台选项），某些设置及其值与 CSP 不同，可能会令人不解。 将更新这些设置名称及其值，以清晰地反应其功能。

适用于：

- Windows 10 及更高版本的设备配置文件
- Windows Holographic for Business 设备配置文件
- Windows 8.1 设备配置文件
- Windows Phone 8.1 设备配置文件

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>macOS Endpoint Protection 设备配置策略中新增 FileVault 设置<!-- 5459801   -->
我们将向 [macOS Endpoint Protection](../protect/endpoint-protection-macos.md) 模板中的 FileVault 类别添加新设置：隐藏恢复密钥。 （转到“设备”   >   “配置文件” >       “创建配置文件”，选择“macOS”作为“平台”，然后选择“Endpoint Protection”作为“配置文件类型”）。 此设置将在 FileVault 2 加密过程中向最终用户隐藏个人密钥。 设备用户可随时从 iOS 公司门户应用或公司门户网站查看其加密 macOS 设备的个人恢复密钥。 若要查看个人恢复密钥，用户可以转到设备详细信息，然后单击“获取恢复密钥”  。

此设置在以前创建的策略中不可用。 需要重新创建 FileVault 策略以配置此设置，才能利用它。 


<!-- ***********************************************-->
## <a name="device-enrollment"></a>设备注册

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>自带设备可以使用 VPN 进行部署<!--5015344 -->
此功能可能会延迟。

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


### <a name="duplicate-your-policies-in-endpoint-security---5892558-----"></a>在终结点安全性中复制策略<!-- 5892558   -->
你将能够选择已在 Microsoft 终结点管理器管理中心的“终结点安全性”节点中创建的策略，然后复制该策略以创建副本。  你将能够复制的策略包括你为以下项目创建的策略： 

- 防病毒
- 磁盘加密
- 防火墙
- 终结点检测和响应
- 攻击面减少
- 帐户保护

复制操作将创建原始策略的副本，然后可以重命名和编辑该副本。 副本不包含原始策略的分配。

### <a name="new-profile-for-endpoint-security-firewall-policy---5653324-----"></a>终结点安全性防火墙策略的新配置文件<!-- 5653324   -->
作为预览版，我们将在 Intune 的终结点安全性的防火墙策略中添加适用于 Windows 10 和更高版本的附加配置文件（“终结点安全性” > “防火墙” > “创建策略”> 选择“Windows 10 和更高版本”）     。 

此新配置文件的每个实例最多支持 150 条自定义 Microsoft Defender 防火墙规则  。 利用 Microsoft Defender 防火墙规则配置文件，你可以定义粒度 Windows 防火墙规则以允许或阻止 Windows 10 中的端口和应用程序。

<!-- ***********************************************-->
## <a name="notices"></a>通知

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>另请参阅

有关最近开发的详细信息，请参阅 [Microsoft Intune 中的新增功能](whats-new.md)。



