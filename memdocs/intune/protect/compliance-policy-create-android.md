---
title: Microsoft Intune 中的 Android 设备符合性设置 - Azure | Microsoft Docs
description: 查看在 Microsoft Intune 中为 Android 设备设置符合性时可以使用的所有设置的列表。 设置密码规则，选择最低或最高操作系统版本，限制特定应用，防止重复使用密码等。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/01/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: e1258fe4-0b5c-4485-8bd1-152090df6345
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3f8cb75907befaa747ebae1718815d9722ff7085
ms.sourcegitcommit: 56bb5419c41c2e150ffed0564350123135ea4592
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/02/2020
ms.locfileid: "82729233"
---
# <a name="android-settings-to-mark-devices-as-compliant-or-not-compliant-using-intune"></a>使用 Intune 将设备标记为符合或不符合的 Android 设置

本文列出并描述了在 Intune 中可针对 Android 设备配置的不同符合性设置。 作为移动设备管理 (MDM) 解决方案的一部分，请使用这些设置将获得 root 权限的（已越狱）设备标记为不符合要求，设置允许的威胁级别，启用 Google Play Protect 等。

此功能适用于：

- Android 设备管理员

作为 Intune 管理员，请使用这些符合性设置来帮助保护组织资源。 若要详细了解符合性策略及其作用，请参阅[设备符合性入门](device-compliance-get-started.md)。

## <a name="before-you-begin"></a>在开始之前

[创建合规性策略](create-compliance-policy.md#create-the-policy)。 对于“平台”，请选择“Android 设备管理员”   。

## <a name="microsoft-defender-atp"></a>Microsoft Defender ATP

- **要求设备不超过计算机风险评分**  

  为 Microsoft Defender ATP 评估的设备选择允许的最高计算机风险分数。 超过此分数的设备将标记为不合规。
  - **未配置**（默认） 
  - **清除**
  - **低**
  - **中等**
  - **高**

## <a name="device-health"></a>设备运行状况

- **由设备管理员管理的设备**  
  Android Enterprise 取代“设备管理员”功能  。

  - **未配置**（默认） 
  - **阻止** - 阻止设备管理员将引导用户转到 Android Enterprise 工作配置文件管理以重新获得访问权限。

- **取得 root 权限的设备**  
  阻止取得 root 权限的设备获得公司访问权限。 （Android 4.0 及更高版本支持此合规性检查。）

  - **未配置**（默认）- 不会评估此设置的符合性和不符合性  。
  - **阻止** - 将已取得 Root 权限（已越狱）的设备标记为不符合。

- **要求设备不高于设备威胁级别**  
  使用此设置，可以将连接的移动威胁防御服务中的风险评估视为合规性条件。

  - **未配置**（默认）- 不会评估此设置的符合性和不符合性  。
  - **安全** - 此选项是最安全的，设备不能具有任何威胁。 如果设备被检测到具有任一级别的威胁，则会被评估为不符合。
  - **低** - 若设备上仅存在低级威胁，则将其评为合规。 低级以上的任意威胁都将使设备不合规。
  - **中** - 如果设备上存在的威胁为低级或中级，设备也将被评估为符合策略。 如果设备被检测到存在高级威胁，则会被确定为不符合要求。
  - **高** - 此选项是最不安全的，允许所有威胁级别。 如果将此解决方案仅用作报告目的，则可能有用。

### <a name="google-play-protect"></a>Google Play Protect

- **配置 Google Play Services**  
  可通过 Google Play Services 进行安全更新，它是已获得认证的 Google 设备上的很多安全功能的基本依赖项。

  - **未配置**（默认）- 不会评估此设置的符合性和不符合性  。  
  - **必需** - 要求安装并启用 Google Play Services 应用程序。  

- **最新的安全提供程序**

  - **未配置**（默认）- 不会评估此设置的符合性和不符合性  。
  - **必需** - 要求最新的安全提供程序可以保护设备免受已知的漏洞攻击。

- **对应用进行威胁扫描**

  - **未配置**（默认）- 不会评估此设置的符合性和不符合性  。
  - **必需** - 要求启用 Android“验证应用”功能。 

  > [!NOTE]
  > 在旧版 Android 平台上，此功能是符合性设置。 Intune 只能检查在设备级别是否启用了此设置。

- **SafetyNet 设备证明**  
  输入必须满足的 [SafetyNet 证明](https://developer.android.com/training/safetynet/attestation.html)级别。 选项包括：

  - **未配置**（默认）- 不会评估此设置的符合性和不符合性  。
  - 检查基本完整性 
  - 检查基本完整性和已认证的设备 

> [!NOTE]
> 若要使用应用保护策略配置 Google Play Protect 设置，请参阅 Android 上的 [Intune 应用保护策略设置](../apps/app-protection-policy-settings-android.md#conditional-launch)。

## <a name="device-properties"></a>设备属性

### <a name="operating-system-version"></a>操作系统版本

- **最低操作系统版本**  
  设备不满足最低操作系统版本要求时，它将被报告为不符合要求。 将显示一个链接，链接中包含有关如何升级的信息。 最终用户可以选择升级其设备，然后访问公司资源。

  默认情况下，没有配置任何版本  。

- **最高操作系统版本**  
  如果设备使用的 OS 版本高于在规则中指定的版本，对公司资源的访问受阻。 会要求用户联系其 IT 管理员。除非变更规则以允许该操作系统版本，否则该设备无法访问公司资源。

  默认情况下，没有配置任何版本  。

## <a name="system-security"></a>系统安全

### <a name="password"></a>Password

- **需要密码才可解锁移动设备**  
  在 Android 4.0 及更高版本或 KNOX 4.0 及更高版本上受支持  。

  此设置指定在允许访问用户移动设备上的信息之前是否要求用户输入密码。 建议的值：要求  

  - **未配置**（默认）- 不会评估此设置的符合性和不符合性  。
  - **必需** - 用户必须输入密码后才能访问其设备。

- **所需的密码类型**  
  在 Android 4.0 及更高版本或 KNOX 4.0 及更高版本上受支持  。

  选择密码是应仅包含数值字符，还是应混合使用数字和其他字符。

  - **设备默认值** - 若要评估密码合规性，请确保选择除设备默认值之外的密码强度  。
  - **低安全性生物识别**
  - **至少为数字**
  - **复杂数字** - 不允许使用 `1111` 或 `1234` 等重复或连续数字。
  - **至少为字母**
  - **至少包含字母数字**
  - **至少为字母数字与符号**

  根据此设置的配置，可以使用以下一个或多个选项：

  - **最短密码长度**  
    在 Android 4.0 及更高版本或 KNOX 4.0 及更高版本上受支持  。

    输入用户密码必须包含的最少位数或最少字符数。

  - **需要提供密码之前处于非活动状态的最大分钟数**  
    在 Android 4.0 及更高版本或 KNOX 4.0 及更高版本上受支持  。

    输入用户必须重新输入密码前的空闲时间。 如果选择“未配置”（默认值），则不会评估此设置的符合性或不符合性  。

  - **密码到期前的天数**  
  在 Android 4.0 及更高版本或 KNOX 4.0 及更高版本上受支持  。

  选择密码过期之前的天数，过期后用户必须新建创建一个密码。

  - **阻止重用的曾用密码数**  
    输入最近使用的不能重用的密码数。 使用此设置限制用户创建以前用过的密码。 （支持 Android 4.0 及更高版本，或 KNOX 4.0 及更高版本。）

### <a name="encryption"></a>加密

- **加密设备上的数据存储**  
  在 Android 4.0 及更高版本或 KNOX 4.0 及更高版本上受支持  。

  - **未配置**（默认）- 不会评估此设置的符合性和不符合性  。
  - **要求** - 加密设备上的数据存储。 选择“需要密码解锁移动设备”  设置时将加密设备。

### <a name="device-security"></a>设备安全性

- **阻止来自未知源的应用**  
  在 Android 4.0 到 Android 7.x 之间受支持。  在 Android 8.0 及更高版本中不受支持

  - **未配置**（默认）- 不会评估此设置的符合性和不符合性。 
  - **阻止** - 阻止启用了“安全性”>“未知源”源的设备（在 Android 4.0 到 Android 7.x 中受支持。   在 Android 8.0 及更高版本中不受支持）。

  若要旁加载应用，必须允许未知源。 如果没有旁加载 Android 应用，请将此功能设置为“阻止”以启用此符合性策略  。

  > [!IMPORTANT]
  > 旁加载应用程序需要启用“阻止来自未知源的应用”  设置。 仅未在设备上旁加载 Android 应用时，才强制执行此符合性策略。

- **公司门户应用运行时完整性**
  - **未配置**（默认）- 不会评估此设置的符合性和不符合性  。
  - **必需** - 选择“必需”  以确认公司门户应用满足以下所有要求：

    - 已安装默认运行时环境
    - 已正确签名
    - 未处于调试模式
    - 已从已知源安装

- **在设备上阻止进行 USB 调试**  
  （在 Android 4.2 或更高版本上受支持） 

  - **未配置**（默认）- 不会评估此设置的符合性和不符合性  。
  - **阻止** - 阻止设备使用 USB 调试功能。

- **最低安全修补程序级别**  
  （在 Android 6.0 或更高版本上受支持） 

  选择设备可具有的最旧的安全修补程序级别。 不满足此修补程序级别的设备将不符合要求。 输入的日期格式必须为 `YYYY-MM-DD`。

  默认情况下，没有配置任何日期  。

- **受限制的应用**  
  为应限制的应用输入“应用名称”和“应用程序包 ID”，然后选择“添加”    。 安装了至少一个受限制的应用的设备将被标记为不符合。

## <a name="next-steps"></a>后续步骤

- [为不符合要求的设备添加操作](actions-for-noncompliance.md)并[使用范围标记来筛选策略](../fundamentals/scope-tags.md)。
- [监视符合性策略](compliance-policy-monitor.md)。
- 请参阅[适用于Android Enterprise 设备的符合性策略设置](compliance-policy-create-android-for-work.md)。
