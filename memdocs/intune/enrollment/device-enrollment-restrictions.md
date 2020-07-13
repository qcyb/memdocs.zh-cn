---
title: Android Enterprise 安全配置框架的设备注册限制
titleSuffix: Microsoft Intune
description: Android Enterprise 安全配置框架的设备注册限制。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/02/2020
ms.topic: how-to
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
ms.openlocfilehash: 6629f416dbbc9555514dfc305db8f224f6b76526
ms.sourcegitcommit: e713f8f4ba2ff453031c9dfc5bfd105ab5d00cd9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/08/2020
ms.locfileid: "86088439"
---
# <a name="android-enterprise-device-enrollment-restrictions"></a>Android Enterprise 设备注册限制

在为 [Android Enterprise 安全配置框架](android-configuration-framework.md)注册设备之前，组织必须先配置相应的限制。 这些限制确保用户只能注册

- 已批准的设备。
- 指定数量的设备。
- 具有指定平台的设备。
- 具有指定操作系统的设备。
- 来自指定制造商的设备。

若要详细了解设备注册限制，请参阅[设置注册限制](enrollment-restrictions-set.md)。

## <a name="work-profile-basic-level-1-security-restrictions"></a>工作配置文件基本安全性（级别 1）限制

对于 Android Enterprise 工作配置文件基本安全性（级别 1），必须实现以下设备限制：

| 类型 | 平台 | 版本 | 允许个人设备 |
|--------|--------|--------|--------|
| Android Enterprise | Allow | Android 5.0 及更高版本。<p>Microsoft 建议配置最低 Android 主要版本，以与 Microsoft 应用支持的 Android 版本匹配。 遵循 Android Enterprise 建议的要求的 OEM 和设备必须支持当前交付版本以及一字母升级版。   当前，Android 建议对知识工作者使用 Android 8.0 及更高版本。 有关详细信息，请参阅 [Android Enterprise 建议的要求](https://www.android.com/enterprise/recommended/requirements/)。 | 是 |
| Android 设备管理员| 阻止 | 所有版本 | 是 |

## <a name="work-profile-high-level-3-security-restrictions"></a>工作配置文件高安全性（级别 3）限制
对于 Android Enterprise 工作配置文件高安全性（级别 3），应实现以下设备限制：

| 类型 | 平台 | 版本 | 允许个人设备 |
|--------|--------|--------|--------|
| Android Enterprise | Allow | Android 8.0 及更高版本 | 是 |
| Android 设备管理员| 阻止 | 所有版本 | 是 |

## <a name="fully-managed-security-restrictions"></a>完全受管理的安全限制
通过审阅[注册完全受管理的设备](android-fully-managed-enroll.md#enroll-the-fully-managed-devices)，确保组织支持 Android Enterprise 完全受管理设备注册。 

## <a name="conditional-access-policies"></a>条件性访问策略
组织可以使用 Azure AD 条件访问策略来确保用户只能在已注册的 Android 设备上访问工作和学校内容。 为此，你需要一个面向所有潜在用户的条件访问策略。 有关创建此策略的详细信息，请参阅[通过条件访问要求访问云应用时具有受管理的设备](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices)。 

遵循[方案：iOS 和 Android 设备需要设备注册](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices#scenario-require-device-enrollment-for-ios-and-android-devices)中的步骤，这确保只有合规的已注册移动设备可以连接到 Office 365 终结点。

## <a name="next-steps"></a>后续步骤

[设置应用配置策略](android-app-configuration-policies.md)
