---
title: Android Enterprise 完全受管理的安全配置
titleSuffix: Microsoft Intune
description: 了解针对 Android Enterprise 完全受管理的基本安全性、增强安全性和高安全性建议的设置。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/24/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: rosssmi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 01c8c0ffba349966c99e1cbd90dbdfc10a5c9782
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2020
ms.locfileid: "86461158"
---
# <a name="android-enterprise-fully-managed-security-configurations"></a>Android Enterprise 完全受管理的安全配置

作为 [Android Enterprise 安全配置框架](android-configuration-framework.md)的一部分，为 Android Enterprise 完全受管理的移动用户应用以下设置。 若要详细了解每个策略设置，请参阅[使用 Intune 将设备标记为符合或不符合的 Android Enterprise 设备所有者设置](../protect/compliance-policy-create-android-for-work.md#fully-managed-dedicated-and-corporate-owned-work-profile)和[使用 Intune 允许或限制功能的 Android Enterprise 设备设置](../configuration/device-restrictions-android-for-work.md#fully-managed-dedicated-and-corporate-owned-work-profile)。

在选择设置时，请务必审阅使用方案，并对其进行分类。 然后，按照所选安全性级别对应的指南来配置用户。 可以根据组织需求来调整建议的设置。 请务必让安全团队评估威胁环境、风险胃纳以及对可用性的影响。

对于公司拥有的完全受管理设备，建议使用三种安全配置框架：

- [完全受管理的基本安全性（级别 1）](#fully-managed-basic-security) 
- [完全受管理的增强安全性（级别 2）](#fully-managed-enhanced-security)
- [完全受管理的高安全性（级别 3）](#fully-managed-high-security) 

## <a name="fully-managed-basic-security"></a>完全受管理的基本安全性

对于组织拥有的移动设备，建议的最低安全配置是级别 1。

级别 1 中的策略强制执行合理的数据访问级别，同时最大限度地降低对用户的影响。 这是通过强制执行密码策略、最低操作系统版本、SafetyNet 设备证明和禁用某些设备功能（如 USB 文件传输）来实现的。 

### <a name="device-compliance"></a>设备符合性

| 部分 | 设置 | 值 | 注意 |
| ----- | ----- | ----- | ----- |
| Microsoft Defender ATP | 要求设备不超过计算机风险评分 | 未配置 ||
| 设备运行状况 | 要求设备不高于设备威胁级别 | 未配置||
| 设备运行状况 | SafetyNet 设备证明 | 检查基本完整性和认证设备 | 此设置在最终用户设备上配置 Google 的 SafetyNet 证明。 基本完整性验证设备的完整性。 已取得根权限的设备、模拟器、虚拟设备以及具有篡改迹象的设备无法通过基本完整性检查。<br>基本完整性和认证设备验证设备是否符合 Google 服务的要求。 只有经过 Google 认证的未修改的设备才能通过此检查。 |
| 设备属性 | 最低操作系统版本 | 格式：Major.Minor<br>例如：8.0| Microsoft 建议配置最低 Android 主要版本，以与 Microsoft 应用支持的 Android 版本匹配。 遵循 Android Enterprise 建议的要求的 OEM 和设备必须支持当前交付版本以及一字母升级版。 当前，Android 建议对知识工作者使用 Android 8.0 及更高版本。 有关 Android 的最新建议，请参阅 [Android Enterprise 建议的要求](https://www.android.com/enterprise/recommended/requirements/)。 |
| 设备属性 | 最高操作系统版本 | 未配置 ||
| 设备属性 | 最低安全修补程序级别 | 未配置 | Android 设备可以接收每月安全修补程序，但发布取决于 OEM 和/或运营商。 组织应确保已部署的 Android 设备在实现此设置之前确实收到了安全更新程序。 有关最新的修补程序发布，请参阅 [Android 安全公告](https://source.android.com/security/bulletin/)。 |
| 系统安全 | 需要密码才可解锁移动设备 | 要求 ||
| 系统安全 | 所需的密码类型 | 数字复杂度 | 组织可能需要更新此设置来匹配自己的密码策略。 |
| 系统安全 | 最短密码长度 | 6 | 组织可能需要更新此设置来匹配自己的密码策略。 |
| 系统安全 | 最长经过多少分钟的非活动状态后需要提供密码| 5 | 组织可能需要更新此设置来匹配自己的密码策略。|
| 系统安全 | 密码还剩多少天到期| 未配置 ||
| 系统安全 |    必须有多少个密码后用户才能重用密码 | 未配置 ||
| 系统安全 | 对设备上的数据存储进行加密 | 要求 ||
| 针对非符合性的操作 | 将设备标记为不符合 | 立即 | 默认情况下，此策略配置为将设备标记为不符合。 还可以执行其他操作。 有关详细信息，请参阅[在 Intune 中为不符合要求的设备配置操作](../protect/actions-for-noncompliance.md)。|

### <a name="device-restrictions"></a>设备限制

| 部分 | 设置 | 值 | 注意 |
| ----- | ----- | ----- | ----- |
| 常规 | 屏幕捕获 | 未配置 ||
| 常规 | 照相机 | 未配置 ||
| 常规 | 默认权限策略 | 设备默认值 ||
| 常规 | 日期和时间更改 | 未配置 ||
| 常规 | 卷更改 | 未配置 ||
| 常规 | 恢复出厂设置 | 阻止 ||
| 常规 | 安全启动 | 阻止 ||
| 常规 | 状态栏 | 未配置 ||
| 常规 | 漫游数据服务 | 未配置 ||
| 常规 | Wi-Fi 设置更改 | 未配置 ||
| 常规 | 蓝牙配置 | 未配置 ||
| 常规 | 网络共享和访问热点 | 未配置 ||
| 常规 | USB 存储 | 未配置 ||
| 常规 | USB 文件传输 | 阻止 ||
| 常规 | 外部介质 | 阻止 ||
| 常规 | 使用 NFC 无线发送数据 | 未配置 ||
| 常规 | 调试功能 | 未配置 ||
| 常规 | 麦克风调节 | 未配置 ||
| 常规 | 恢复出厂设置保护电子邮件 | 未配置 ||
| 常规 | 网络安全门 | 未配置 ||
| 常规 | 系统更新 | 自动 ||
| 常规 | 通知窗口 | 未配置 ||
| 常规 | 跳过首次使用提示 | 未配置 ||
| 系统安全 | 对应用进行威胁扫描 |要求 ||
| 设备体验 | 注册配置文件类型 | 完全受管理 ||
| 设备体验 | 将 Microsoft Launcher 设置为默认启动器 | 未配置 | 组织可以选择实现 Microsoft Launcher，以确保在完全受管理设备上提供一致的主屏幕体验。 有关详细信息，请参阅 [如何使用 Intune 在 Android Enterprise 完全受管理设备上设置 Microsoft Launcher](https://techcommunity.microsoft.com/t5/intune-customer-success/how-to-setup-microsoft-launcher-on-android-enterprise-fully/ba-p/1482134) |
| Password | 禁用锁屏界面 | 未配置 ||
| Password | “禁用的锁屏界面”功能 | 未选择任何项 ||
| Password | 所需的密码类型 | 数字复杂度 ||
| Password | 最短密码长度 | 6 ||
| Password | 密码还剩多少天到期 | 未配置 ||
| Password | 必须有多少个密码后用户才能重用密码 | 未配置 ||
| Password | 登录失败多少次后擦除设备 | 10 ||
| 电源设置 | 锁屏界面定时 | 5 ||
| 电源设置 | 设备接通电源时屏幕亮起 | 未配置 ||
| 用户和帐户 | 添加新用户 | 未配置 ||
| 用户和帐户 | 删除用户 | 未配置 ||
| 用户和帐户 | 帐户更改（仅限专用设备） | 未配置 ||
| 用户和帐户 | 个人 Google 帐户 | 未配置 ||
| 用户和帐户 | 用户可以配置凭据 | 阻止 ||
| 应用程序 | 允许从未知源安装 | 未配置 ||
| 应用程序 | 允许访问 Google Play 商店中的所有应用 | 未配置 | 默认情况下，用户无法在完全受管理设备上安装来自 Google Play 商店的个人应用。 如果组织希望允许将完全受管理设备用于个人用途，不妨更改此设置。 |
| 应用程序 | 应用自动更新 | 仅 Wi-Fi | 组织应根据需要调整此设置，因为如果应用更新是通过手机网络进行，可能会产生流量套餐费用。 |

## <a name="fully-managed-enhanced-security"></a>完全受管理的增强安全性

对于用户访问更敏感的信息的公司拥有设备，建议的配置是级别 2。 这些设备如今是企业中的自然目标。 这些设置不需要大量高技能的安全人员。 因此，它们应该对大多数企业组织是可访问的。 通过制定更强的密码策略并禁用用户/帐户功能，此配置扩展了级别 1 中的配置。

级别 2 设置包括针对级别 1 建议的所有策略设置。 不过，下面列出的设置只包括已添加或更改的设置。 这些设置对用户或应用的影响可能稍微大一些。 它们对在移动设备上访问敏感信息的风险用户强制执行更合适的安全性级别。

### <a name="device-compliance"></a>设备符合性

| 部分 | 设置 | 值 | 注意 |
| ----- | ----- | ----- | ----- |
| 系统安全 | 密码还剩多少天到期 | 365 | 组织可能需要更新此设置来匹配自己的密码策略。 |
| 系统安全 |    必须有多少个密码后用户才能重用密码 | 5 | 组织可能需要更新此设置来匹配自己的密码策略。 |

### <a name="device-restrictions"></a>设备限制

| 部分 | 设置 | 值 | 注意 |
| ----- | ----- | ----- | ----- |
| 常规 | 恢复出厂设置保护电子邮件 | Google 帐户电子邮件地址 ||
| 常规 | 电子邮件地址列表（仅限 Google 帐户电子邮件地址选项） | example@gmail.com | 手动更新此策略，以指定可以在设备被擦除后解锁设备的设备管理员的 Google 电子邮件地址。 |
| 设备密码 | 密码还剩多少天到期 | 365 | 组织可能需要更新此设置来匹配自己的密码策略。 |
| 设备密码 | 必须有多少个密码后用户才能重用密码 | 5 | 组织可能需要更新此设置来匹配自己的密码策略。 |
| 设备密码 | 登录失败多少次后擦除设备 | 5 ||
| 用户和帐户 | 添加新用户 | 阻止 ||
| 用户和帐户 | 删除用户 | 阻止 ||
| 用户和帐户 | 个人 Google 帐户 | 阻止 ||

## <a name="fully-managed-high-security"></a>完全受管理的高安全性

对于以下两种情况，建议的配置是级别 3：
- 具有复杂的大型安全组织的组织。
- 将成为对手的唯一目标的特定用户和组。
此类组织通常是资金雄厚且经验丰富的对手的目标。 因此，它们应该受到下面列出的其他约束和控制。

此配置通过以下方式扩展了级别 2：
- 增加最低操作系统版本。
- 通过强制执行最安全的 Microsoft Defender ATP 或移动威胁防御级别，确保设备符合要求。
- 增加最低操作系统版本。
- 强制执行其他设备限制（如在锁屏界面上禁用未编辑的通知）。
- 要求应用始终是最新的。 

在级别 3 中强制执行的策略设置包括针对级别 2 建议的所有策略设置。 下面列出的设置只包括已添加或更改的设置。 这些设置可能对用户或应用产生重大影响。 它们执行更适合于目标组织所面临风险的安全性级别。


### <a name="device-compliance"></a>设备符合性

| 部分 | 设置 | 值 | 注意 |
| ----- | ----- | ----- | ----- |
| Microsoft Defender ATP | 要求设备不超过计算机风险评分 | 清除 | 此设置需要 Microsoft Defender ATP。 有关详细信息，请参阅[在 Intune 中使用条件访问强制执行 Microsoft Defender ATP 的符合性](../protect/advanced-threat-protection.md)。<p> 客户应考虑实现 Microsoft Defender ATP 或移动威胁防御解决方案。 没有必要同时部署它们。 |
| 设备运行状况 | 要求设备不高于设备威胁级别 | 安全 | 此设置需要移动威胁防御产品。 有关详细信息，请参阅[适用于已注册设备的移动威胁防御](../protect/mtd-device-compliance-policy-create.md)。<p>客户应考虑实现 Microsoft Defender ATP 或移动威胁防御解决方案。 没有必要同时部署它们。|
| 设备属性 | 最低操作系统版本 | 格式：Major.Minor<br>例如：10.0| Microsoft 建议配置最低 Android 主要版本，以与 Microsoft 应用支持的 Android 版本匹配。 遵循 Android Enterprise 建议的要求的 OEM 和设备必须支持当前交付版本以及一字母升级版。 当前，Android 建议对知识工作者使用 Android 8.0 及更高版本。 有关 Android 的最新建议，请参阅“Android Enterprise 建议的要求” |

### <a name="device-restrictions"></a>设备限制

| 部分 | 设置 | 值 | 注意 |
| ----- | ----- | ----- | ----- |
| 常规 | 日期和时间更改 | 阻止 ||
| 常规 | 网络共享和访问热点 | 阻止 ||
| 常规 | 使用 NFC 无线发送数据 | 阻止 ||
| 设备密码 | “禁用的锁屏界面”功能 | 信任代理、未编辑的通知 ||
| 应用程序 | 应用自动更新 | 始终 | 组织应根据需要调整此设置，因为如果应用更新是通过手机网络进行，可能会产生流量套餐费用。 |


## <a name="next-steps"></a>后续步骤

管理员可以使用 [Intune 的 PowerShell 脚本](https://github.com/microsoftgraph/powershell-intune-samples)导入示例 [Android Enterprise 安全配置框架 JSON 模板](https://github.com/microsoft/Intune-Config-Frameworks/tree/master/AndroidEnterprise)，从而将以上配置级别纳入部署通道方法中，以用于测试和生产用途。
