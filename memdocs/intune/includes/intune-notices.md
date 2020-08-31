---
title: 包含文件
description: 包含文件
author: ErikjeMS
ms.service: microsoft-intune
ms.topic: include
ms.date: 08/10/2020
ms.author: erikje
ms.custom: include file
ms.openlocfilehash: 7027eac119ef36adfdb9a0057a74d276696620b3
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820048"
---
本文中的通知提供了重要信息，可以帮助你为未来的 Intune 更改和功能做好准备。

### <a name="microsoft-intune-ends-support-for-windows-phone-81-and-windows-10-mobile---3544938-3544909---"></a>Microsoft Intune 终止对 Windows Phone 8.1 和 Windows 10 移动版的支持<!-- 3544938, 3544909 -->
Microsoft 对 Windows Phone 8.1 的主要支持于 2017 年 7 月结束，外延支持于 2019 年 6 月结束。 自 2017 年 10 月以来，针对 Windows Phone 8.1 的公司门户应用一直处于支持模式。 此外，Microsoft Intune 已于 2020 年 2 月 20 日结束对 Windows Phone 8.1 的支持。 

Microsoft 对 Windows 10 移动版的主流支持已于 2019 年 12 月结束。 如本支持声明所述，Windows 10 移动版用户将不再有资格从 Microsoft 接收新的安全更新、非安全修补程序、免费的辅助支持选项或联机技术内容更新。 基于对移动 OS 的全面支持，Microsoft Intune 于 2020 年 8 月 10 日结束对 Windows 10 移动版应用的公司门户和 Windows 10 移动版操作系统的支持。

自 8 月 10 日起，Windows Phone 8.1 和 Windows 10 移动版设备的注册将失败，并且从 Intune UI 中删除了 Windows 移动版配置文件类型。 已注册的设备将不再签入 Intune 服务，我们将删除设备和策略数据。

### <a name="end-of-support-for-legacy-pc-management"></a>停止支持旧版 PC 管理

将于 2020 年 10 月 15 日停止支持旧版 PC 管理。 请将设备升级到 Windows 10，并将它们重新注册为“移动设备管理”(MDM) 设备，以便继续由 Intune 托管它们。

[了解详细信息](https://go.microsoft.com/fwlink/?linkid=2107122)

### <a name="move-to-the-microsoft-endpoint-manager-admin-center-for-all-your-intune-management"></a>转到 Microsoft Endpoint Manager 管理中心进行所有 Intune 管理
在去年 3 月发布的 MC208118 中，我们针对“Microsoft Endpoint Manager - Intune 管理”推出了一个新的简单 URL：[https://endpoint.microsoft.com](https://endpoint.microsoft.com)。 Microsoft Endpoint Manager 是一个集成有 Microsoft Intune 和 Configuration Manager 的统一平台。 从 2020 年 8 月 1 日起，我们将删除位于 [https://portal.azure.com](https://portal.azure.com) 的 Intune 管理，并建议你改用 [https://endpoint.microsoft.com](https://endpoint.microsoft.com) 处理你的所有终结点管理。 


### <a name="decreasing-support-for-android-device-administrator--7371518--"></a>减少对 Android 设备管理员的支持<!--7371518-->
Android 设备管理员管理在 Android 2.2 中作为一种管理 Android 设备的方法发布。 然后从 Android 5 开始，发布了 [Android Enterprise](../enrollment/connect-intune-android-enterprise.md) 的更现代的管理框架（适用于能够可靠连接到 Google 移动服务的设备）。 Google 通过在新的 Android 版本中减少对管理的支持来鼓励转移设备管理员管理。

#### <a name="how-does-this-affect-me"></a>这对我有何影响？
由于 Google 的这些变化，到 2020 年 10 月，受影响的设备管理员管理的设备将不再具有广泛的管理功能。 

> [!NOTE]
> 这一日期之前被传达为 2020 年第四季度，但根据 [Google 提供的最新信息](https://www.blog.google/products/android-enterprise/da-migration/)，该日期已被删除。

##### <a name="device-types-that-will-be-impacted"></a>将受影响的设备类型
减少对设备管理员的支持会对某些设备产生影响，这些设备通常满足以下所有三个条件：
- 已注册到设备管理员管理。
- 运行 Android 10 或更高版本。
- 不是 Samsung 设备。

如果设备属于以下任何一种情况，则不会受到影响：
- 未注册到设备管理员管理。
- 运行低于 Android 10 的 Android 版本。
- 是 Samsung 设备。 Samsung Knox 设备在此期间不受影响，因为通过 Intune 与 Knox 平台的集成提供了扩展支持。 这为你提供了额外的时间来计划过渡到 Samsung 设备的设备管理员管理。

##### <a name="settings-that-will-be-impacted"></a>将受影响的设置
[Google 减少了对设备管理员的支持](https://developers.google.com/android/work/device-admin-deprecation)以防止在受影响的设备上应用这些设置的配置。

###### <a name="configuration-profile-device-restriction-settings"></a>配置配置文件设备限制设置

- 阻止使用“相机”
- 设置“最短密码长度”
- 设置“擦除设备前的登录失败次数”（不适用于未设置密码的设备，但适用于具有密码的设备）
- 设置“密码过期(天)”
- 设置“所需的密码类型”
- 设置“防止重用以前的密码”
- 阻止“Smart Lock 和其他信任代理”

###### <a name="compliance-policy-settings"></a>合规性策略设置

- 设置“所需的密码类型”
- 设置“最短密码长度”
- 设置“密码到期前的天数”
- 设置“阻止重用的曾用密码数”


![Android 合规性策略页的屏幕截图](../fundamentals/media/notices/android-compliance-settings.png)

###### <a name="additional-impacts-based-on-android-os-version"></a>基于 Android OS 版本的其他影响

**Android 10**：对于运行 Android 10 及更高版本的所有设备管理员管理的设备（包括 Samsung），Google 限制了设备管理员管理代理（如公司门户）访问设备标识符信息的能力。 在设备更新到 Android 10 或更高版本后，此限制将影响以下 Intune 功能：
- VPN 的网络访问控制将不再有效
- 使用 IMEI 或序列号将设备识别为公司拥有的设备将不会自动将设备标记为公司拥有的设备
- 在 Intune 中，IMEI 和序列号将不再对 IT 管理员可见

**Android 11**：我们目前正在最新的开发者 beta 版本上测试 Android 11 支持，以评估它是否会对设备管理员管理的设备造成影响。

#### <a name="user-experience-of-impacted-settings-on-impacted-devices"></a>受影响设备上受影响设置的用户体验

受影响的配置设置：
- 对于已应用设置的已注册设备，将继续强制实施受影响的配置设置。
- 对于新注册的设备、新分配的设置和更新的设置，将不会强制实施受影响的配置设置（但仍将强制实施所有其他配置设置）。

受影响的合规性设置：
- 对于已经注册并应用了设置的设备，受影响的合规性设置仍将在“更新设备设置”页面上显示为不合规的原因，设备将不合规，并且仍将在“设置”应用中强制执行密码要求。
- 对于新注册的设备、新分配的设置和更新的设置，受影响的合规性设置仍将在“更新设备设置”页面上显示为不符合的原因，并且设备将不合规，但在设置应用程序中不会强制执行更严格的密码要求。

#### <a name="cause-of-impact"></a>影响的原因 
设备将在 2020 年 10 月开始受到影响。 届时，我们将发布一个公司门户应用更新，该更新会将公司门户 API 的目标从级别 28 增加级别 29（[根据 Google 要求](https://www.blog.google/products/android-enterprise/da-migration/)）。 

届时，用户完成以下两项操作后，非 Samsung 制造的设备管理员管理的设备将受到影响：
- 更新到 Android 10 或更高版本。
- 将公司门户应用更新为面向 API 级别 29 的版本。

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>我需要如何准备应对此项变化？
为避免在即将到来的 2020 年 10 月出现功能降低的情况，建议采取如下操作：
- **新建注册**：将新设备载入 [Android Enterprise](../enrollment/connect-intune-android-enterprise.md) 管理（如果可用）和/或[应用保护策略](../apps/app-protection-policies.md)。 避免将新设备载入设备管理员管理中。 
- **先前注册的设备**：如果设备管理员管理的设备正在运行 Android 10 或更高版本，或者可以更新到 Android 10 或更高版本（特别是在不是 Samsung 设备的情况下），请将其从设备管理员管理移到 [Android Enterprise](../enrollment/connect-intune-android-enterprise.md) 管理和/或[应用保护策略](../apps/app-protection-policies.md)。 可以利用简化的流[将 Android 设备从设备管理员移到工作配置文件管理](../enrollment/android-move-device-admin-work-profile.md)。

#### <a name="additional-information"></a>其他信息
- [将 Android 设备从设备管理员移到工作配置文件管理](../enrollment/android-move-device-admin-work-profile.md)
- [设置 Android Enterprise 工作配置文件设备的注册](../enrollment/android-work-profile-enroll.md)
- [设置 Android Enterprise 专用设备的注册](../enrollment/android-kiosk-enroll.md)
- [设置 Android Enterprise 完全托管设备的注册](../enrollment/android-fully-managed-enroll.md)
- [如何创建分配应用保护策略](../apps/app-protection-policies.md)
- [如何在无法访问 Google 移动服务的环境中使用 Intune](../apps/manage-without-gms.md)
- [了解 Android Enterprise 设备上的应用保护策略和工作配置文件](../apps/android-deployment-scenarios-app-protection-work-profiles.md)
- [关于设备管理员弃用的须知内容的 Google 博客](https://www.blog.google/products/android-enterprise/da-migration/)
- [从设备管理员迁移到 Android Enterprise 的 Google 指南](http://static.googleusercontent.com/media/android.com/en/enterprise/static/2016/pdfs/enterprise/Android-Enterprise-Migration-Bluebook_2019.pdf)
- [弃用设备管理员 API 的 Google 文档](https://developers.google.com/android/work/device-admin-deprecation)


### <a name="plan-for-change-intune-enrollment-flow-update-for-apples-automated-device-enrollment-for-iosipados"></a>更改计划：Apple 的适用于 iOS/iPadOS 的自动设备注册的 Intune 注册流更新
在 7 月的公司门户发布中，我们将更改 Apple 自动设备注册（以前称为 DEP）的 iOS/iPadOS 注册流。 此注册流更改仅在“通过用户关联进行注册”流期间出现。 以前，如果在配置过程中将“安装公司门户”设置为“否”，用户仍然可以从应用商店安装公司门户应用，然后通过该应用触发注册，用户需要在其中添加适当的序列号。 在即将发布的公司门户版本中，我们将删除序列号确认屏幕。 相反，你需要创建相应的应用配置策略，与公司门户一起发送，以确保用户能够成功注册，或者能够在配置过程中将“安装公司门户”设置为“是”。 
 - 有关详细信息，请参阅[此处](https://techcommunity.microsoft.com/t5/intune-customer-success/intune-enrollment-flow-update-for-apple-s-automated-device/ba-p/1431629)的帖子。
