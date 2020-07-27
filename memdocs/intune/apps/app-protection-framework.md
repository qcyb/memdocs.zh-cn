---
title: 使用应用保护策略的数据保护框架
titleSuffix: Microsoft Intune
description: 了解应用保护策略 (APP) 如何可确保组织数据在托管应用中保持安全或受到控制（无论设备是否注册）。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/09/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: smithre4
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: 444fb116150cf3d7a3ab4dcfe4eb450b20119df0
ms.sourcegitcommit: 86c2c438fd2d87f775f23a7302794565f6800cdb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "86410923"
---
# <a name="data-protection-framework-using-app-protection-policies"></a>使用应用保护策略的数据保护框架 

随着越来越多的组织实现用于访问工作或学校数据的移动设备策略，防范数据泄露变得极其重要。 用于防范数据泄露的 Intune 移动应用程序管理解决方案是应用保护策略 (APP)。 APP 是可确保组织数据在托管应用中保持安全或受到控制（无论设备是否注册）的规则。 有关详细信息，请参阅[应用保护策略概述](app-protection-policy.md)。

配置应用保护策略时，各种设置和选项的数量使组织可以根据其特定需求定制保护。 由于这种灵活性，实现完整方案所需的策略设置排列可能并不明显。 为了帮助组织确定客户端终结点强化工作的优先顺序，Microsoft 为 [Windows 10 中的安全配置](https://aka.ms/secconframework)引入了新的分类，而 Intune 将类似的分类用于 APP 数据保护框架来进行移动应用管理。  

APP 数据保护配置框架分为三个不同的配置方案：

- 级别 1 企业基本数据保护 – Microsoft 建议将此配置作为企业设备的最低数据保护配置。

- 级别 2 企业增强型数据保护 – 对于用户访问敏感或机密信息的设备，Microsoft 建议使用此配置。 此配置适用于访问工作或学校数据的大多数移动用户。 某些控制可能会影响用户体验。

- 级别 3 企业高数据保护 - 对于具有较大或较复杂的安全团队的组织所运行的设备，或对于面临独特高风险的特定用户或组（处理高度敏感数据的用户，而未经授权的披露会给组织造成相当大的物质损失），Microsoft 建议使用此配置。 可能会被资金雄厚且经验丰富的对手作为目标的组织应努力实现这种配置。

## <a name="app-data-protection-framework-deployment-methodology"></a>APP 数据保护框架部署方法

与任何新软件、功能或设置的部署一样，Microsoft 建议在部署 APP 数据保护框架之前，投资一种圈形方法来测试验证。 定义部署圈通常是一次性事件（或至少不太频繁），但 IT 应重新访问这些组，以确保排序仍正确。

Microsoft 建议对 APP 数据保护框架采用以下部署圈方法：

| 部署圈  | 租户  | 评估团队  | 输出  | 时间线  |
|--------------------|------------------------|-------------------------------------------------------------------|----------------------------------------------------------|----------------------------------------|
| 质量保证  | 预生产租户  | 移动功能所有者、安全性、风险评估、隐私、UX  | 功能方案验证、草稿文档  | 0-30 天  |
| 预览  | 生产租户  | 移动功能所有者、UX  | 最终用户方案验证、面向用户的文档  | 7-14 天，后期保证质量  |
| 生产  | 生产租户  | 移动功能所有者、IT 支持人员  | 不适用  | 7 天到数周，后期预览  |

如上表所示，应首先在预生产环境中执行对应用保护策略进行的所有更改，以了解策略设置影响。 测试完成后，更改可以移动到生产环境中，并应用于一部分生产用户（通常是 IT 部门和其他适用组）。 最后，可以完成向移动用户社区其余部分的推出。 根据更改有关的影响的规模，推出到生产可能需要较长时间。 如果没有用户影响，则更改应快速推出，而如果更改会导致用户影响，则推出可能需要减慢速度，因为需要将更改传达给用户群体。

测试对 APP 进行的更改时，请注意[交付时间](app-protection-policy-delivery.md)。 可以监视针对给定用户的 APP 交付状态。 有关详细信息，请参阅[如何监视应用保护策略](app-protection-policies-monitor.md)。

可以使用 Microsoft Edge 和 URL about:Intunehelp，在设备上验证每个应用的单独 APP 设置。 有关详细信息，请参阅[查看客户端应用保护日志](app-protection-policy-settings-log.md)和[使用适用于 iOS 和 Android 的 Microsoft Edge 访问托管的应用日志](manage-microsoft-edge.md#use-edge-for-ios-and-android-to-access-managed-app-logs)。

## <a name="app-data-protection-framework-settings"></a>APP 数据保护框架设置

应为适用的应用启用以下应用保护策略设置，并将这些设置分配给所有移动用户。 有关每个策略设置的详细信息，请参阅 [iOS 应用保护策略设置](app-protection-policy-settings-ios.md)和 [Android 应用保护策略设置](app-protection-policy-settings-android.md)。

Microsoft 建议对使用方案进行查看和分类，然后使用针对该级别的规范性指导配置用户。 与任何框架一样，相应级别中的设置可能需要基于组织的需要进行调整，因为数据保护必须评估威胁环境、风险偏好以及对可用性的影响。  

### <a name="conditional-access-policies"></a>条件访问策略
为了确保只有支持应用保护策略的应用才能访问工作或学校帐户数据，必须使用 Azure Active Directory 条件访问策略。 请参阅“方案1：Office 365 应用需要批准的应用和应用保护策略”（位于[需要应用保护策略，才能使用条件访问进行云应用访问](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access)中），了解实现特定策略的步骤。

### <a name="apps-to-include-in-the-app-protection-policies"></a>要包含在应用保护策略中的应用  

对于每个应用保护策略，都应包含以下核心 Microsoft 应用：

- Edge
- Excel
- Office
- OneDrive
- OneNote
- Outlook
- PowerPoint
- Microsoft Teams
- 微软待办
- Word
- Microsoft SharePoint

策略应包含基于业务需求的其他 Microsoft 应用、在组织内使用的集成 Intune SDK 的其他第三方公共应用，以及集成 [Intune SDK](../developer/app-sdk.md)（或已包装）的业务线应用。

### <a name="level-1-enterprise-basic-data-protection"></a>级别 1 企业基本数据保护

级别 1 是企业移动设备的最低数据保护配置。 此配置要求使用 PIN 访问工作或学校数据、对工作或学校帐户数据进行加密并提供有选择地擦除学校或工作数据的功能，替代了对基本 Exchange Online 设备访问策略的需求。 但是，与 Exchange Online 设备访问策略不同，以下应用保护策略设置适用于在策略中选择的所有应用，从而可确保在移动消息方案之外保护数据访问。

级别 1 中的策略实施合理的数据访问级别，同时最大程度降低对用户的影响，可在 Microsoft 终结点管理器中创建应用保护策略时反映默认数据保护和访问要求设置。  

#### <a name="data-protection"></a>数据保护

| 设置 | 设置描述 |             值  |             平台        |
|-----------------|--------------------------------------------------------|-----------------------|----------------------------------------|
| 数据传输 |             将组织数据备份到…  |             Allow  |             iOS/iPadOS、Android        |
| 数据传输 |       将组织数据发送到其他应用  |             所有应用  |             iOS/iPadOS、Android        |
| 数据传输 |       从其他应用接收数据  |             所有应用  |             iOS/iPadOS、Android        |
| 数据传输 |       限制在应用间进行剪切、复制和粘贴  |             任何应用  |             iOS/iPadOS、Android        |
| 数据传输 |       第三方键盘  |             Allow  |             iOS/iPadOS        |
| 数据传输 |       批准的键盘  |             不需要  |             Android        |
| 数据传输 |       屏幕捕获和 Google 助手  |             Allow  |             Android        |
| 加密 |             对组织数据进行加密  |             要求  |             iOS/iPadOS、Android        |
| 加密 |       对已注册设备上的组织数据进行加密  |             要求  |             Android        |
| 功能  |             将应用与本机联系人应用进行同步  |             Allow  |             iOS/iPadOS、Android        |
| 功能  |       打印组织数据  |             Allow  |             iOS/iPadOS、Android        |
| 功能  |       限制使用其他应用传输 Web 内容  |             任何应用  |             iOS/iPadOS、Android        |
| 功能  |       组织数据通知  |             Allow  |             iOS/iPadOS、Android        |

#### <a name="access-requirements"></a>访问要求 

| 设置  | 值  | 平台  | 注意  |
|----------------------------------------------------------------|---------------|----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 需要 PIN 才能进行访问  | 要求  | iOS/iPadOS、Android  |   |
| PIN 类型  | 数字  | iOS/iPadOS、Android  |   |
| 简单 PIN  | Allow  | iOS/iPadOS、Android  |   |
| 选择最小 PIN 长度  | 4  | iOS/iPadOS、Android  |   |
| 使用生物识别，而不是 PIN 进行访问  | Allow  | iOS/iPadOS、Android  |   |
| 替代生物识别，而不是 PIN 进行访问  | 要求  | iOS/iPadOS、Android  |   |
| 超时(活动状态的分钟数)  | 720  | iOS/iPadOS、Android  |   |
| 使用 Face ID，而不是 PIN 进行访问  | Allow  | iOS/iPadOS  |   |
| PIN 重置间隔的天数  | 否  | iOS/iPadOS、Android  |   |
| 应用 PIN(设置了设备 PIN 时)  | 要求  | iOS/iPadOS、Android  | 如果设备已在 Intune 中注册，则在通过设备合规性策略实施强设备 PIN 时，管理员可以考虑将此设置为“不需要”。  |
| 用于访问的工作或学校帐户凭据  | 不需要  | iOS/iPadOS、Android  |   |
| 在（非活动状态的分钟数）后重新检查访问要求  | 30  | iOS/iPadOS、Android  |   |

#### <a name="conditional-launch"></a>条件启动 

| 设置 | 设置描述 |          值/操作  |          平台        | 注意 |
|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 应用条件 |       最大 PIN 尝试次数  |          5/重置 PIN  |          iOS/iPadOS、Android  |                  |
| 应用条件 |       脱机宽限期  |          720/阻止访问(分钟)  |          iOS/iPadOS、Android  |                  |
| 应用条件 |       脱机宽限期  |          90/擦除数据(天)  |          iOS/iPadOS、Android  |                  |
| 设备条件  |       已越狱/获得 root 权限的设备  |        不适用/阻止访问  |          iOS/iPadOS、Android  |                  |
| 设备条件  |       SafetyNet 设备证明  |          基本完整性和认证设备/阻止访问  |          Android  |          <p>此设置在最终用户设备上配置 Google 的 SafetyNet 证明。 基本完整性验证设备的完整性。 已取得根权限的设备、模拟器、虚拟设备以及具有篡改迹象的设备无法通过基本完整性检查。 </p><p> “基本完整性和认证设备”验证设备与 Google 服务的兼容性。 只有经过 Google 认证的未修改的设备才能通过此检查。</p>  |
| 设备条件  |       要求对应用进行威胁扫描  |        不适用/阻止访问  |          Android  |          此设置确保为最终用户设备启用 Google 的“验证应用”扫描。 如果配置了此设置，将阻止最终用户访问，直至他们在其 Android 设备上启用 Google 的应用扫描设置。        |

#### <a name="level-2-enterprise-enhanced-data-protection"></a>级别 2 企业增强数据保护

对于用户访问更敏感信息的设备，级别 2 是建议作为其标准的数据保护配置。 这些设备如今是企业中的自然目标。 这些建议并不假设有大量的高技能安全从业人员，因此大多数企业组织都应该可使用这些建议。 此配置通过限制数据传输方案以及要求最低操作系统版本来扩展级别 1 中的配置。

级别 2 中实施的策略设置包括针对级别 1 建议的所有策略设置，但仅列出了已添加或已更改的以下设置，以实现比级别 1 更多的控制和更复杂的配置。 尽管这些设置可能会对用户或应用程序产生稍高的影响，但它们会实施与在移动设备上访问敏感信息的用户所面临的风险更为相称的数据保护级别。

#### <a name="data-protection"></a>数据保护

| 设置 | 设置描述 |             值  |             平台        | 注意 |
|---------------|----------------------------------------------------------|-----------------------------------------------|---------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 数据传输 |       将组织数据备份到…  |          阻止  |          iOS/iPadOS、Android  |                  |
| 数据传输 |       将组织数据发送到其他应用  |          策略托管应用  |          iOS/iPadOS、Android  |          <p>使用 iOS/iPadOS 时，管理员可以将此值配置为“策略托管应用”、“具有 OS 共享的策略托管应用”或“具有‘打开方式/共享’筛选的策略托管应用”。 </p><p>当设备还向 Intune 进行注册时，可以使用“具有 OS 共享的策略托管应用”。 此设置允许将数据传输到其他策略托管应用，以及将文件传输到由 Intune 托管的其他应用。 </p><p>具有“打开方式/共享”筛选功能的策略托管应用会筛选“OS 打开方式/共享”对话框，以仅显示策略托管应用。 </p><p> 有关详细信息，请参阅 [iOS 应用保护策略设置](app-protection-policy-settings-ios.md)。</p> |
| 数据传输 |       选择要豁免的应用  |          Default / skype;app-settings;calshow;itms;itmss;itms-apps;itms-appss;itms-services;  |          iOS/iPadOS  |                  |
| 数据传输 |       保存组织数据的副本  |          阻止  |          iOS/iPadOS、Android  |                  |
| 数据传输 |       允许用户将副本保存到所选的服务  |          OneDrive for Business、SharePoint Online |          iOS/iPadOS、Android  |                  |
| 数据传输 |       将电信数据传输到  |          所有应用 |          iOS/iPadOS、Android  |                  |
| 数据传输 |       限制在应用间进行剪切、复制和粘贴  |          带粘贴的策略托管应用  |          iOS/iPadOS、Android  |                  |
| 数据传输 |       屏幕捕获和 Google 助手  |          阻止  |          Android  |                  |
| 功能 |       限制使用其他应用传输 Web 内容  |          Microsoft Edge  |          iOS/iPadOS、Android  |                  |
| 功能 |       组织数据通知  |          阻止组织数据  |          iOS/iPadOS、Android  |          有关支持此设置的应用的列表，请参阅 [iOS 应用保护策略设置](app-protection-policy-settings-ios.md)和 [Android 应用保护策略设置](app-protection-policy-settings-android.md)。       |

#### <a name="conditional-launch"></a>条件启动

| 设置 | 设置描述 |          值/操作  |          平台        | 注意 |
|--------------------|----------------------------|-----------------------------------------------------------|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 设备条件  |       最低 OS 版本  |          *格式：主要版本号.次要版本号.内部版本号 <br>示例：* 12.4.6 / 阻止访问 |          iOS/iPadOS        | Microsoft 建议配置最低 iOS 主要版本，以便与 Microsoft 应用支持的 iOS 版本匹配。   Microsoft 应用支持 N-1 方法，其中 N 是当前 iOS 主要发行版本。 对于次要版本和内部版本值，Microsoft 建议确保设备通过相应的安全更新保持最新状态。 请参阅 [Apple 安全更新](https://support.apple.com/en-us/HT201222)以获取 Apple 的最新建议 |
| 设备条件  |       最低 OS 版本  |          *格式：主要版本号.次要版本号<br>   示例：* 5.0 / 阻止访问   |          Android        | Microsoft 建议配置最低 Android 主要版本，以便与 Microsoft 应用支持的 Android 版本匹配。 遵循 Android Enterprise 建议要求的 OEM 和设备必须支持当前交付版本 + 一个字母升级。   当前，Android 建议对知识工作者使用 Android 8.0 及更高版本。   请参阅 [Android Enterprise 建议要求](https://www.android.com/enterprise/recommended/requirements/)以了解 Android 的最新建议 |
| 设备条件  |       最低修补程序版本  |          *格式： YYYY-MM-DD <br> 示例：2020-01-01*/阻止访问  |          Android        | Android 设备可以接收每月安全修补程序，但发布依赖于 OEM 和/或运营商。 组织应确保已部署的 Android 设备在实现此设置之前收到安全更新。 有关最新修补程序版本，请参阅 [Android 安全公告](https://source.android.com/security/bulletin/)。  |

#### <a name="level-3-enterprise-high-data-protection"></a>级别 3 企业高数据保护 

对于具有大型和复杂安全组织的组织，或者对于将作为对手唯一目标的特定用户和组，级别 3 是建议作为标准的数据保护配置。 这类组织通常是资金雄厚且经验丰富的对手的目标，因此值得实施所介绍的其他约束和控制。 此配置通过限制其他数据传输方案、增加 PIN 配置的复杂性以及添加移动威胁检测，来扩展级别 2 中的配置。  

级别 3 中实施的策略设置包括针对级别 2 建议的所有策略设置，但仅列出了已添加或已更改的以下设置，以实现比级别 2 更多的控制和更复杂的配置。 这些策略设置可能会对用户或应用程序造成显著影响，从而实施与目标组织所面临的风险相称的安全级别。  

#### <a name="data-protection"></a>数据保护

| 设置 | 设置描述 |             值  |             平台        | 注意 |
|---------------|---------------------------------------|----------------------------------------|--------------------------------------|---------------------------------------------------------------------------------------------------------|
| 数据传输 |       将电信数据传输到  |          任何由策略管理的拨号应用 |          Android  | 管理员还可以将此设置配置为使用不支持应用保护策略的拨号应用，方法是选择特定拨号应用并提供拨号应用包 ID 和拨号应用名称值  。   |
| 数据传输 |       将电信数据传输到  |          特定拨号应用 |          iOS/iPadOS  |  |
| 数据传输 |       拨号应用 URL 方案  |          *replace_with_dialer_app_url_scheme* |          iOS/iPadOS  | 在 iOS/iPadOS 上，此值必须替换为所使用的自定义拨号应用的 URL 方案。 如果 URL 方案未知，请联系应用开发人员以获取详细信息。 有关 URL 方案的详细信息，请参阅[为应用定义自定义 URL 方案](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/defining_a_custom_url_scheme_for_your_app)。|
| 数据传输 |       从其他应用接收数据  |          策略托管应用  |          iOS/iPadOS、Android         |  |
| 数据传输 |       第三方键盘  |          阻止  |          iOS/iPadOS        | 在 iOS/iPadOS 上，这会阻止所有第三方键盘在应用中正常工作。  |
| 数据传输 |       批准的键盘  |          要求  |          Android        |  |
| 数据传输 |       选择待批准的键盘  |          添加/删除键盘  |          Android        | 使用 Android 时，必须选择键盘，才能基于已部署的 Android 设备进行使用。  |
| 功能 |       打印组织数据  |          阻止  |          iOS/iPadOS、Android         |  |

#### <a name="access-requirements"></a>访问要求

|       设置  |          值  |          平台  |
|-----------------------------------------------------------|--------------------|---------------------------------|
|       简单 PIN  |          阻止  |          iOS/iPadOS、Android  |
|       选择最小 PIN 长度  |          6  |          iOS/iPadOS、Android  |
|       PIN 重置间隔的天数  |          是  |          iOS/iPadOS、Android  |
|       天数  |          365  |          iOS/iPadOS、Android  |

#### <a name="conditional-launch"></a>条件启动

| 设置 | 设置描述 |          值/操作  |          平台        | 注意 |
|----------------------------|--------------------------------------|-------------------|---------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 设备条件  |       最低 OS 版本  |          *格式：主要版本号.次要版本号<br>   示例：8.0*/阻止访问   |          Android        | Microsoft 建议配置最低 Android 主要版本，以便与 Microsoft 应用支持的 Android 版本匹配。 遵循 Android Enterprise 建议要求的 OEM 和设备必须支持当前交付版本 + 一个字母升级。   当前，Android 建议对知识工作者使用 Android 8.0 及更高版本。   请参阅 [Android Enterprise 建议要求](https://www.android.com/enterprise/recommended/requirements/)以了解 Android 的最新建议 |
|       设备条件  |          已越狱/获得 root 权限的设备  |        不适用/擦除数据  |          iOS/iPadOS、Android        |  |
|       设备条件  |          允许的最大威胁级别  |          安全/阻止访问  |          iOS/iPadOS、Android        | <p>可以使用移动威胁防御检查未注册设备是否存在威胁。 有关详细信息，请参阅[适用于未注册设备的移动威胁防御](https://aka.ms/mtdmamdocs)。      </p><p>     如果设备进行了注册，则可以跳过此设置，以便部署适用于已注册设备的移动威胁防御。 有关详细信息，请参阅[适用于已注册设备的移动威胁防御](../protect/mtd-device-compliance-policy-create.md)。</p> |

## <a name="next-steps"></a>后续步骤

管理员可以使用 [Intune 的 PowerShell 脚本](https://github.com/microsoftgraph/powershell-intune-samples)导入示例 [Intune 应用保护策略配置框架 JSON](https://github.com/microsoft/Intune-Config-Frameworks/tree/master/AppProtectionPolicies) 模板，从而将以上配置级别纳入其部署圈方法中，以便用于测试和生产。

## <a name="see-also"></a>另请参阅

- [如何使用 Microsoft Intune 创建和部署应用保护策略](app-protection-policies.md)
- [Microsoft Intune 中提供的 Android 应用保护策略设置](app-protection-policy-settings-android.md)
- [Microsoft Intune 中提供的 iOS/iPadOS 应用保护策略设置](app-protection-policy-settings-ios.md)
- 第三方应用（例如 Salesforce 移动应用）与 Intune 一起以特定的方式来保护公司数据。 若要详细了解 Salesforce 应用专门与 Intune 合作的方式（包括 MDM 应用配置设置），请参阅 [Salesforce 应用和 Microsoft Intune](https://gallery.technet.microsoft.com/Salesforce-App-and-Intune-c47d44ee/file/188000/1/Salesforce%20App%20and%20Intune%20for%20external.pdf)。
