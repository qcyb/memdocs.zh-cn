---
title: Android Enterprise 安全配置工作配置文件
titleSuffix: Microsoft Intune
description: 了解针对 Android Enterprise 设备基本安全性和高安全性建议的限制和设置。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 09/01/2020
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
ms.openlocfilehash: b661068515069b1bc4c20acdc1c9ad00a12fe7dd
ms.sourcegitcommit: 75d6ea42a0f473dc5020ae7fcb667c9bdde7bd97
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/01/2020
ms.locfileid: "89286197"
---
# <a name="android-enterprise-work-profile-security-configurations"></a>Android Enterprise 工作配置文件安全配置

作为 [Android Enterprise 安全配置框架](android-configuration-framework.md)的一部分，为 Android Enterprise 工作配置文件移动用户应用以下设置。 若要详细了解每个策略设置，请参阅[使用 Intune 将设备标记为符合或不符合的 Android Enterprise 设置](../protect/compliance-policy-create-android-for-work.md#work-profile)和[使用 Intune 允许或限制功能的 Android Enterprise 设备设置](../configuration/device-restrictions-android-for-work.md#work-profile-only)。

在选择设置时，请务必审阅使用方案，并对其进行分类。 然后，按照所选安全性级别对应的指南来配置用户。 可以根据组织需求来调整建议的设置。 请务必让安全团队评估威胁环境、风险胃纳以及对可用性的影响。

对于个人拥有的工作配置文件设备，建议使用两种安全配置框架：

- [工作配置文件基本安全性（级别 1）](#work-profile-basic-security) 
- [工作配置文件高安全性（级别 3）](#work-profile-high-security) 

> [!Note]
> 鉴于可用于 Android Enterprise 工作配置文件设备的设置，没有增强安全性（级别 2）产品/服务。 可用的设置不能说明级别 1 与级别 2 之间的差异。

## <a name="work-profile-basic-security"></a>工作配置文件基本安全性

对于用户访问工作或学校数据的个人设备，建议的最低安全配置是级别 1。 此配置可应用于大多数移动用户。 某些控制可能会影响用户体验。

### <a name="device-compliance"></a>设备符合性

| 部分 | 设置 | 值 | 注意 |
| ----- | ----- | ----- | ----- |
| Microsoft Defender ATP | 要求设备不超过计算机风险评分 | 未配置 ||
| 设备运行状况 | 取得 root 权限的设备 | 阻止 ||
| 设备运行状况 | 要求设备不高于设备威胁级别 | 未配置||
| 设备运行状况 | 配置 Google Play Services | 要求 ||
| 设备运行状况 | 最新的安全提供程序 | 要求 ||
| 设备运行状况 | SafetyNet 设备证明 | 检查基本完整性和认证设备 | 此设置在最终用户设备上配置 Google 的 SafetyNet 证明。 基本完整性验证设备的完整性。 已取得根权限的设备、模拟器、虚拟设备以及具有篡改迹象的设备无法通过基本完整性检查。<p>基本完整性和认证设备验证设备是否符合 Google 服务的要求。 只有经过 Google 认证的未修改的设备才能通过此检查。 |
| 设备属性 | 最低操作系统版本 | 格式：Major.Minor<br>例如：5.0| Microsoft 建议配置最低 Android 主要版本，以与 Microsoft 应用支持的 Android 版本匹配。 遵循 Android Enterprise 建议的要求的 OEM 和设备必须支持当前交付版本以及一字母升级版。 当前，Android 建议对知识工作者使用 Android 8.0 及更高版本。 有关 Android 的最新建议，请参阅 [Android Enterprise 建议的要求](https://www.android.com/enterprise/recommended/requirements/)。 |
| 设备属性 | 最高操作系统版本 | 未配置 ||
| 系统安全 | 需要密码才可解锁移动设备 | 要求 ||
| 系统安全 | 所需的密码类型 | 数字复杂度 | 组织可能需要更新此设置来匹配自己的密码策略。 |
| 系统安全 | 最短密码长度 | 6 | 组织可能需要更新此设置来匹配自己的密码策略。 |
| 系统安全 | 最长经过多少分钟的非活动状态后需要提供密码| 5 | 组织可能需要更新此设置来匹配自己的密码策略。|
| 系统安全 | 密码还剩多少天到期| 未配置 | 组织可能需要更新此设置来匹配自己的密码策略。 |
| 系统安全 | 阻止使用的旧密码的数量 | 未配置 | 组织可能需要更新此设置来匹配自己的密码策略。 |
| 系统安全 | 对设备上的数据存储进行加密 | 要求 ||
| 系统安全 | 阻止来自未知源的应用 | 阻止 ||
| 系统安全 | 公司门户应用运行时完整性 | 要求 ||
| 系统安全 | 在设备上阻止进行 USB 调试 | 阻止 | 虽然此设置阻止使用 USB 设备进行调试，但它也禁用了收集日志的功能，这些日志可能对故障排除很有用。 |
| 系统安全 | 最低安全修补程序级别 | 未配置 | Android 设备可以接收每月安全修补程序，但发布取决于 OEM 和/或运营商。 组织应确保已部署的 Android 设备在实现此设置之前确实收到了安全更新程序。 有关最新的修补程序发布，请参阅 [Android 安全公告](https://source.android.com/security/bulletin/)。 |
| 针对非符合性的操作 | 将设备标记为不符合 | 立即 | 默认情况下，此策略配置为将设备标记为不符合。 还可以执行其他操作。 有关详细信息，请参阅[在 Intune 中为不符合要求的设备配置操作](../protect/actions-for-noncompliance.md)。|

### <a name="device-restrictions"></a>设备限制

| 部分 | 设置 | 值 | 注意 |
| ----- | ----- | ----- | ----- |
| 工作配置文件设置 | 在工作配置文件和个人配置文件之间进行复制和粘贴 | 阻止 ||
| 工作配置文件设置 | 工作配置文件和个人配置文件之间的数据共享 | 工作配置文件中的应用可处理来自个人配置文件的共享请求 ||
| 工作配置文件设置 | 设备锁定时显示的工作配置文件通知 | 未配置 | 阻止此设置可确保敏感数据不会在工作配置文件通知中公开（这可能会影响可用性）。 |
| 工作配置文件设置 | 默认应用权限 | 设备默认值 | 管理员需要审阅并调整自己要部署的应用所授予的权限。 |
| 工作配置文件设置 | 添加和删除帐户 | 阻止 ||
| 工作配置文件设置 | 通过蓝牙共享联系人 | 启用 | 默认情况下，无法在其他设备上访问工作联系人，如通过蓝牙集成共享联系人的汽车。 启用此设置可改进免手动用户体验。 不过，蓝牙设备可能会在首次连接时缓存联系人。 在实现此设置时，组织应考虑平衡可用性方案和数据保护问题。 |
| 工作配置文件设置 | 屏幕捕获 | 阻止 ||
| 工作配置文件设置 | 在个人资料中显示工作联系人呼叫方 ID | 未配置 ||
| 工作配置文件设置 | 从个人配置文件中搜索工作联系人 | 未配置 | 阻止用户从个人配置文件中访问工作联系人可能会影响某些可用性方案，如个人配置文件中的短信和拨号器体验。 在实现此设置时，组织应考虑平衡可用性方案和数据保护问题。 |
| 工作配置文件设置 | 照相机 | 未配置 ||
| 工作配置文件设置 | 允许来自工作配置文件应用的小组件 | 启用 ||
| 工作配置文件设置 | 需要工作配置文件密码 | 要求 ||
| 工作配置文件设置 | 最短密码长度 | 6 | 组织可能需要更新此设置来匹配自己的密码策略。 |
| 工作配置文件设置 | 最长经过多少分钟的非活动状态后锁定工作配置文件| 5 | 组织可能需要更新此设置来匹配自己的密码策略。 |
| 工作配置文件设置 | 登录失败多少次后擦除工作配置文件| 10 | 组织可能需要更新此设置来匹配自己的密码策略。 |
| 工作配置文件设置 | 密码过期（天数） | 未配置 | 组织可能需要更新此设置来匹配自己的密码策略。 |
| 工作配置文件设置 | 所需的密码类型 | 数字复杂度 ||
| 工作配置文件设置 | 防止重用以前的密码 | 未配置 | 组织可能需要更新此设置来匹配自己的密码策略。|
| 工作配置文件设置 | 人脸解锁 | 未配置 ||
| 工作配置文件设置 | 指纹解锁 | 未配置 ||
| 工作配置文件设置 | 虹膜解锁 | 未配置 ||
| 工作配置文件设置 | Smart Lock 和其他信任代理 | 未配置 |||
| 设备密码 | 最短密码长度 | 6 | 组织可能需要更新此设置来匹配自己的密码策略。 |
| 设备密码 | 最长经过多少分钟的非活动状态后锁定屏幕 | 5 | 组织可能需要更新此设置来匹配自己的密码策略。 |
| 设备密码 | 登录失败多少次后擦除设备 | 10 | 此设置触发的是工作配置文件擦除，而不是设备擦除。 |
| 设备密码 | 密码过期（天数） | 未配置 | 组织可能需要更新此设置来匹配自己的密码策略。 |
| 设备密码 | 所需的密码类型 | 数字复杂度 ||
| 设备密码 | 防止重用以前的密码 | 未配置 | 组织可能需要更新此设置来匹配自己的密码策略。 |
| 设备密码 | 指纹解锁 | 未配置 ||
| 设备密码 | Smart Lock 和其他信任代理 | 未配置 ||
| 系统安全 | 对应用进行威胁扫描 | 要求 | 此设置确保为最终用户设备启用 Google 的“验证应用”扫描。 如果配置了此设置，将阻止最终用户访问，直至他们在其 Android 设备上启用 Google 的应用扫描设置。 |
| 系统安全 | 防止在个人配置文件中安装来自未知源的应用 | 阻止 ||

> [!Note]
> 在 Android Enterprise 工作配置文件启用后，默认配置“一个锁”来合并设备密码和工作配置文件密码。 如果必要，在工作配置文件设置下，可以禁用“一个锁”来分离工作配置文件密码和设备密码。

## <a name="work-profile-high-security"></a>工作配置文件高安全性

对于风险特别高的用户或组使用的设备，建议的配置是级别 3。 例如，处理高度敏感数据的用户未经授权披露这些数据会造成相当大的物质损失。 很可能成为资金雄厚且经验丰富的对手的目标的组织应该受到以下所述的附加约束。 此配置通过以下方式扩展了级别 1 中的配置：
- 实现移动威胁防御或 Microsoft Defender ATP。
- 限制工作配置文件数据方案。
- 制定更强的密码策略。

在级别 3 中强制执行的策略设置包括针对级别 1 建议的所有策略设置。 不过，下面列出的设置只包括已添加或更改的设置。 这些设置对用户或应用的影响可能稍微大一些。 它们对在移动设备上访问敏感信息的风险用户强制执行更合适的安全性级别。

### <a name="device-compliance"></a>设备符合性

| 部分 | 设置 | 值 | 注意 |
| ----- | ----- | ----- | ----- |
| Microsoft Defender ATP | 要求设备不超过计算机风险评分 | 清除 | 此设置需要 Microsoft Defender ATP。 有关详细信息，请参阅[在 Intune 中使用条件访问强制执行 Microsoft Defender ATP 的符合性](../protect/advanced-threat-protection.md)。<p>客户应考虑实现 Microsoft Defender ATP 或移动威胁防御解决方案。 没有必要同时部署它们。 |
| 设备运行状况 | 要求设备不高于设备威胁级别 | 安全 | 此设置需要移动威胁防御产品。 有关详细信息，请参阅[适用于已注册设备的移动威胁防御](../protect/mtd-device-compliance-policy-create.md)。<p>客户应考虑实现 Microsoft Defender ATP 或移动威胁防御解决方案。 没有必要同时部署它们。|
| 设备属性 | 最低操作系统版本 | 格式：Major.Minor<br>例如：8.0| Microsoft 建议配置最低 Android 主要版本，以与 Microsoft 应用支持的 Android 版本匹配。 遵循 Android Enterprise 建议的要求的 OEM 和设备必须支持当前交付版本以及一字母升级版。 当前，Android 建议对知识工作者使用 Android 8.0 及更高版本。 有关 Android 的最新建议，请参阅“Android Enterprise 建议的要求” |
| 系统安全 | 密码还剩多少天到期 | 365 | 组织可能需要更新此设置来匹配自己的密码策略。 |
| 系统安全 | 阻止使用的旧密码的数量 | 5 | 组织可能需要更新此设置来匹配自己的密码策略。 |


### <a name="device-restrictions"></a>设备限制

| 部分 | 设置 | 值 | 注意 |
| ----- | ----- | ----- | ----- |
| 工作配置文件设置 | 设备锁定时显示的工作配置文件通知 | 阻止 | 阻止此设置可确保敏感数据不会在工作配置文件通知中公开（这可能会影响可用性）。 |
| 工作配置文件设置 | 通过蓝牙共享联系人 | 未配置 | 默认情况下，无法在其他设备上访问工作联系人，如通过蓝牙集成共享联系人的汽车。 启用此设置可改进免手动用户体验。 不过，蓝牙设备可能会在首次连接时缓存联系人。 在实现此设置时，组织应考虑平衡可用性方案和数据保护问题。 |
| 工作配置文件设置 | 从个人配置文件中搜索工作联系人 | 阻止 | 阻止用户从个人配置文件中访问工作联系人可能会影响某些可用性方案，如个人配置文件中的短信和拨号器体验。 在实现此设置时，组织应考虑平衡可用性方案和数据保护问题。 |
| 工作配置文件设置 | 允许来自工作配置文件应用的小组件 | 未配置 ||
| 工作配置文件设置 | 登录失败多少次后擦除工作配置文件 | 5 | 组织可能需要更新此设置来匹配自己的密码策略。 |
| 工作配置文件设置 | 密码过期（天数） | 365 | 组织可能需要更新此设置来匹配自己的密码策略。 |
| 工作配置文件设置 | 防止重用以前的密码 | 5 | 组织可能需要更新此设置来匹配自己的密码策略。 |
| 工作配置文件设置 | Smart Lock 和其他信任代理 | 阻止 ||
| 设备密码 | 登录失败多少次后擦除设备 | 5 | 此设置触发的是工作配置文件擦除，而不是设备擦除。 |
| 设备密码 | 密码过期（天数） | 365 | 组织可能需要更新此设置来匹配自己的密码策略。 |
| 设备密码 | 防止重用以前的密码 | 5 | 组织可能需要更新此设置来匹配自己的密码策略。 |

## <a name="next-steps"></a>后续步骤

管理员可以使用 [Intune 的 PowerShell 脚本](https://github.com/microsoftgraph/powershell-intune-samples)导入示例 [Android Enterprise 安全配置框架 JSON 模板](https://github.com/microsoft/Intune-Config-Frameworks/tree/master/AndroidEnterprise)，从而将以上配置级别纳入部署通道方法中，以用于测试和生产用途。
