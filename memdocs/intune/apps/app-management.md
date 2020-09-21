---
title: 什么是 Microsoft Intune 中的应用管理？
titleSuffix: ''
description: 通过 Microsoft Intune 平台了解客户端应用程序的管理功能。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/03/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 1975a2dc-3a14-4cb9-9afb-e2ba01a1c51b
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 68336d252cb3d3d3d49cc0c7a32e49e94ba5cdd7
ms.sourcegitcommit: d6cbd1a1c2926064e074e3431471534eb142c905
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90012657"
---
# <a name="what-is-microsoft-intune-app-management"></a>什么是 Microsoft Intune 应用管理？

IT 管理员可以使用 Microsoft Intune 来管理公司员工使用的客户端应用。 除了此功能外，还可管理设备和保护数据。 管理员的首要任务之一是，确保最终用户能够访问他们在执行工作时所需的应用。 这个目标很有挑战性，因为：
- 有众多的设备平台和应用类型。
- 可能需要管理公司设备和用户个人设备上的应用。
- 必须确保网络和数据的安全性。

此外，还建议分配和管理未向 Intune 注册的设备上的应用。

## <a name="mobile-application-management-mam-basics"></a>移动应用程序管理 (MAM) 基础知识

[Intune 移动应用程序管理](app-lifecycle.md)指的是 Intune 管理功能套件，通过它能够为用户发布、推送、配置、保护、监视和更新移动应用。

MAM 允许你在应用程序中管理和保护组织的数据。 通过无需注册的 MAM (MAM-WE)，可以在几乎任何[设备](app-management.md#app-management-capabilities-by-platform)上管理包含敏感数据的工作或学校相关应用，包括自带设备办公 (BYOD) 场景下的个人设备。   许多高效工作型应用，例如 Microsoft Office 应用
，都可以通过 Intune MAM 进行管理。 请参阅可供公众使用的 [Microsoft Intune 保护的应用](apps-supported-intune-apps.md)的官方列表。

Intune MAM 支持两种配置：

- **Intune MDM + MAM**：IT 管理员仅可在已进行 Intune 移动设备管理 (MDM) 注册的设备上使用 MAM 和应用保护策略管理应用。 若要使用 MDM + MAM 管理应用，客户应使用 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中的 Intune。
- **无需设备注册的 MAM**：无需设备注册的 MAM 或 MAM-WE 使 IT 管理员可以在未进行 Intune MDM 注册的设备上使用 MAM 和应用保护策略管理应用。 这意味着可以在进行了第三方 EMM 提供程序注册的设备上通过 Intune 管理应用。 若要使用 MAM-WE 管理应用，客户应使用 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中的 Intune。 此外，可以在已注册第三方企业移动性管理 (EMM) 提供程序或完全未注册 MDM 的设备上通过 Intune 管理应用。 有关 BYOD 和 Microsoft EMS 的详细信息，请参阅[用于通过 Microsoft 企业移动性 + 安全性 (EMS) 启用 BYOD 的技术决策](../fundamentals/byod-technology-decisions.md)。

## <a name="app-management-capabilities-by-platform"></a>按平台分类的应用管理功能

Intune 提供各种功能，用于在设备上获取所需的应用，以便在其中运行。 下表提供了有关应用管理功能的摘要。

| 应用管理功能 | Android/Android Enterprise | iOS/iPadOS | macOS | Windows 10 |
|-------------------------- | -------------------------- | ---------- | ----- | ---------- |
| 向设备和用户添加和分配应用 | 是 | 是 | 是 | 是 |
| 将应用分配到未注册 Intune 的设备 | 是 | 是 | 否 | 否 |  |
| 使用应用配置策略来控制应用的启动行为 | 是 | 是 | 否 | 否 |
| 使用移动应用预配策略续订过期应用 | 否 | 是 | 否 | 否 |
| 使用应用保护策略来保护应用中的公司数据 | 是 | 是 | 否 | 否 <sup>1</sup> |
| 仅从已安装应用中删除公司数据（应用选择性擦除） | 是 | 是 | 否 | 是 |
| 监视应用分配 | 是 | 是 | 是 | 是 |
| 分配和跟踪从应用商店批量购买的应用 | 否 | 否 | 否 | 是 |
| 强制在设备上安装的应用（必需）<sup>2</sup> | 是 | 是 | 是 | 是 |
| 从公司门户的设备上进行可选安装（可用安装） | 是 <sup>3</sup> | 是 | 是 | 是 |
| 安装 Web 版应用快捷方式（Web 链接） | 是 <sup>4</sup> | 是 | 是 | 是 |
| 内部（业务线）应用 | 是 | 是 | 是 | 是 |
| 来自应用商店的应用 | 是 | 是 | 否 | 是 |
| 更新应用 | 是 | 是 | 否 | 是 |

<sup>1</sup>请考虑使用 [Windows 信息保护](../protect/windows-information-protection-configure.md)来保护运行 Windows 10 的设备上的应用。<br>
<sup>2</sup> 仅适用于由 Intune 管理的设备。<br>
<sup>3</sup> Intune 支持 Android Enterprise 设备上托管 Google Play 商店中的可用应用。<br>
<sup>4</sup> Intune 不提供在标准 Android Enterprise 设备上以 Web 链接的形式安装应用的快捷方式。 但是，为[多应用专用 Android Enterprise 设备](../configuration/device-restrictions-android-for-work.md#device-experience)提供了 Web 链接支持。 


## <a name="get-started"></a>入门

可以在“应用”  工作负荷中找到大多数应用的相关信息，可通过执行以下操作进行访问：

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
3. 选择“应用”  。

    ![“应用”工作负荷窗格](./media/app-management/apps-workload.png)

“应用”工作负荷提供用于访问常用应用信息和功能的链接。 

“应用”工作负荷导航菜单顶部提供常用应用详细信息：
- **概述**：选择此选项可查看租户名称、MDM 机构、租户位置、帐户状态、应用安装状态和应用保护策略状态。
- **所有应用**：选择此选项可显示所有可用应用的列表。 可以从此页面添加其他应用。 此外，可以查看每个应用的状态，以及每个应用是否进行了分配。 有关详细信息，请参阅[添加应用](apps-add.md)和[分配应用](apps-deploy.md)。
- **监视器应用**
    - **应用许可证**：查看、分配和监视从应用商店批量购买的应用。 有关详细信息，请参阅 [iOS 批量采购计划 (VPP) 应用](vpp-apps-ios.md)和[适用于企业的 Microsoft Store 批量采购的应用](windows-store-for-business.md)。
    - 发现的应用：  查看由 Intune 分配或安装在设备上的应用。 有关详细信息，请参阅 [Intune 发现的应用](app-discovered-apps.md)。
    - 应用安装状态  ：查看你创建的应用分配的状态。 有关详细信息，请参阅[使用 Microsoft Intune 监视应用信息和分配](apps-monitor.md#device-and-user-status-graphs)。
    - **应用保护状态**：查看所选用户的应用保护策略的状态。
- 按平台  ：选择这些平台可按平台查看可用应用。
    - Windows
    - iOS
    - macOS
    - Android
- **策略**：
    - **应用保护策略**：选择此选项可将设置与应用关联，并帮助保护其使用的公司数据。 例如，可以限制某应用与其他应用进行通信的功能，或者可能要求用户输入 PIN 才能访问公司应用。 有关详细信息，请参阅[应用保护策略](app-protection-policies.md)。
    - **应用配置策略**：选择此选项可提供用户在运行应用时可能需要的设置。 有关详细信息，请参阅[应用配置策略](app-configuration-policies-use-ios.md)、[iOS 应用配置策略](app-configuration-policies-use-ios.md)和 [Android 应用配置策略](app-configuration-policies-overview.md)。
    - **** iOS 应用预配配置文件：
iOS 应用包含一个预配配置文件和一个证书签名的代码。 证书过期后，应用无法再运行。 Intune 提供了一些工具，用于将新的预配配置文件策略主动分配到安装了即将到期应用的设备。 有关详细信息，请参阅 [iOS 应用预配配置文件](app-provisioning-profile-ios.md)。
    - S 模式补充策略  ：选择此选项可授权其他应用程序在托管 S 模式设备上运行。 有关详细信息，请参阅 [S 模式补充策略](apps-win32-s-mode.md)。
    - Office 应用策略：选择此选项可为连接到 Microsoft 365 服务的 Office 移动应用创建移动应用管理策略。 此外，还可以通过为启用了混合现代身份验证的 iOS/iPadOS 和 Android 的 Outlook 创建 Intune 应用保护策略来保护对 Exchange 本地邮箱的访问。 必须满足使用 Office 应用策略的要求。 有关要求的详细信息，请参阅[使用 Office 云策略服务的要求](https://docs.microsoft.com/deployoffice/overview-office-cloud-policy-service#requirements-for-using-the-office-cloud-policy-service)。 连接到本地 Exchange 或 SharePoint 服务的其他应用不支持应用保护策略。 要了解相关信息，请参阅[适用于 Microsoft 365 企业应用版的 Office 云策略服务概述](https://docs.microsoft.com/deployoffice/overview-office-cloud-policy-service)。
    - 策略集  ：选择此选项可创建你创建的应用、策略和其他管理对象的可分配集合。 有关详细信息，请参阅[策略集](../fundamentals/policy-sets.md)。
- 其他  ：   
    - **应用选择性擦除**：选择此选项将从选定用户的设备中仅删除公司数据。 有关详细信息，请参阅[应用选择性擦除](apps-selective-wipe.md)。
    - **应用类别**：添加、固定和删除应用类别名称。
    - 电子书  ：一些应用商店允许你为想要在公司使用的应用或书籍购买多个许可证。 有关系详细信息，请参阅[使用 Microsoft Intune 管理批量购买的应用和书籍](vpp-apps.md)。
- **帮助和支持**：排查问题、请求获取支持或查看 Intune 状态。 有关详细信息，请参阅[排除问题](../fundamentals/help-desk-operators.md)。

### <a name="try-the-interactive-guide"></a>尝试交互式指南
[使用 Microsoft Endpoint Manager 管理并保护移动和桌面应用程序](https://mslearn.cloudguides.com/guides/Manage%20and%20protect%20mobile%20and%20desktop%20applications%20with%20Microsoft%20Endpoint%20Manager)交互式指南将引导您浏览 Microsoft Endpoint Manager 管理中心，并展示如何管理在 Intune 中注册的设备、使用策略强制实现合规性以及保护组织的数据。</br></br>

<div align=”center”>
<iframe allowfullscreen width="95%" height="450" src="https://mslearn.cloudguides.com/guides/Manage%20and%20protect%20mobile%20and%20desktop%20applications%20with%20Microsoft%20Endpoint%20Manager" frameborder="0" scrolling="no" loading="lazy"/></iframe>
</div>

## <a name="additional-information"></a>其他信息
控制台中的以下各项提供与应用相关的功能：
- **适用于企业的 Microsoft Store**：设置到适用于企业的 Microsoft 应用商店的集成。 然后，可将购买的应用程序同步到 Intune，对其进行分配，并跟踪许可证使用情况。 有关详细信息，请参阅[适用于企业的 Microsoft Store 批量采购的应用](windows-store-for-business.md)。
- **Windows 企业证书**：应用或查看用于将业务线应用分发到托管 Windows 设备的代码签名证书的状态。
- **Windows Symantec 证书**：应用或查看 Symantec 代码签名证书的状态。
- **Windows 旁加载密钥**：添加 Windows 旁加载密钥，可用于将应用直接安装到设备，而无需从 Windows 应用商店发布和下载应用。 有关详细信息，请参阅[旁加载 Windows 应用](app-sideload-windows.md)。
- Apple VPP 令牌  ：应用并查看 iOS/iPadOS 批量采购计划 (VPP) 许可证。 有关详细信息，请参阅[批量购买的 iOS/iPadOS 应用](vpp-apps-ios.md)。
- 托管的 Google Play  ：托管 Google Play 是 Google 的企业应用商店，并且是适用于 Android Enterprise 的应用程序的唯一供应商。 有关详细信息，请参阅[使用 Intune 将托管 Google Play 应用添加到 Android Enterprise 设备](apps-add-android-for-work.md)。
- **自定义**：自定义公司门户，向其提供公司品牌。 有关详细信息，请参阅[公司门户配置](company-portal-app.md)。

若要详细了解应用，请参阅[向 Microsoft Intune 添加应用](../apps/apps-add.md)。

## <a name="next-steps"></a>后续步骤

- [向 Microsoft Intune 添加应用](apps-add.md)
