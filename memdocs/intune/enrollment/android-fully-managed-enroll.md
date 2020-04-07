---
title: 设置适用于 Android Enterprise 完全托管设备的 Intune 注册
titleSuffix: Microsoft Intune
description: 了解如何在 Intune 中注册 Android Enterprise 完全托管设备。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 1/15/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 89d299edfb9542591eaabcf42d0b2069bbde4331
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2020
ms.locfileid: "80327316"
---
# <a name="set-up-intune-enrollment-of-android-enterprise-fully-managed-devices"></a>设置 Android Enterprise 完全托管设备的 Intune 注册 

Android Enterprise 完全托管设备是与单个用户关联的企业自有设备，它们专门用于工作而非个人用途。 管理员可以管理整个设备，强制执行工作配置文件不可用的策略控制，例如：
- 仅允许从托管的 Google Play 安装应用。
- 阻止卸载托管应用。
- 防止用户出厂重置设备等。

Intune 可帮助将应用和设置部署到 Android Enterprise 完全托管设备等 Android Enterprise 设备。 有关 Android Enterprise 的特定详细信息，请参阅 [Android Enterprise 要求](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012)。

## <a name="technical-requirements"></a>技术要求

必须拥有 Intune 独立租户，才能管理 Android Enterprise 完全托管设备。 完全托管的设备管理在旧版 Silverlight 管理控制台中不可用。

设备必须满足以下要求才能作为 Android Enterprise 完全托管设备进行管理：

- Android OS 版本 6.0 及更高版本。
- 设备必须运行具有 Google Mobile Services (GMS) 连接性的 Android 版本。 设备必须有可用的 GMS，并且必须能连接到 GMS。

如果满足上述要求，则设备制造商/OEM 不受限制。

## <a name="set-up-android-enterprise-fully-managed-device-management"></a>设置 Android Enterprise 完全托管设备管理

要设置 Android Enterprise 完全托管设备管理，请执行以下步骤：

1. 要准备管理移动设备，必须将[移动设备管理 (MDM) 机构设置为“Microsoft Intune”  ](../fundamentals/mdm-authority-set.md)。 第一次设置 Intune 以进行移动设备管理时，只需设置一次此项。
2. [将 Intune 租户帐户连接到 Android Enterprise 帐户](connect-intune-android-enterprise.md)。
3. [启用公司所拥有的用户设备](#enable-corporate-owned-user-devices)
4. [注册完全托管的设备](#enroll-the-fully-managed-devices)。

### <a name="enable-corporate-owned-user-devices"></a>启用公司所拥有的用户设备

1. 登录到 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，选择“设备” > “Android” > “Android 注册”  > “公司拥有的完全托管用户设备”     。
2. 在“允许用户注册公司所有的用户设备”下，选择“是”   。

> [!NOTE]
> 如果你定义了一个 Azure AD 条件访问策略，该策略使用“要求设备标记为符合策略”控件，并且适用于所有云应用、Android 和浏览器，则必须将 Microsoft Intune 云应用排除在该策略之外      。 这是因为 Android 安装进程使用 Chrome 选项卡在注册过程中对用户进行身份认证。 有关详细信息，请参阅 [Azure AD 条件访问文档](https://docs.microsoft.com/azure/active-directory/conditional-access/)。

如果此设置设置为“是”，将提供 Intune 租户的注册令牌（随机字符串）和 QR 码  。 此单个注册令牌对所有用户有效，并且不会过期。 根据设备的 Android OS 和版本，可使用令牌或 QR 码注册设备。

## <a name="enroll-the-fully-managed-devices"></a>注册完全托管的设备
现在可以[注册完全托管的设备](android-dedicated-devices-fully-managed-enroll.md)。

## <a name="next-steps"></a>后续步骤
- [添加 Android Enterprise 完全托管设备配置策略](../configuration/device-restrictions-android-for-work.md#device-owner-only)
- [配置 Android Enterprise 完全托管设备的应用配置策略](../apps/app-configuration-policies-use-android.md)

