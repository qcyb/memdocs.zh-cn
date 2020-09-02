---
title: 分别了解 Intune 和 Azure 设备限制
titleSuffix: ''
description: 了解 Intune 的设备限制和 Azure AD 的设备限制之间的差异。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/12/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 63c9d9e4752e4b0d317667162255e368fc5a099c
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88908548"
---
# <a name="understand-intune-and-azure-ads-device-limit-restrictions"></a>分别了解 Intune 和 Azure AD 的设备限制

可通过以下两种方式配置设备限制：
- Intune 注册
- 已联接 Azure Active Directory (AD) 或已注册 Azure AD

本文说明了何时将基于配置应用这些限制。

## <a name="intune-device-limit-restrictions"></a>Intune 设备限制

Intune 设备限制设置了用户可控制的最大设备数（最大设置为 15）。 若要设置此“设备限制”，请转到 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431) > “设备” > “注册限制”  。 有关详细信息，请参阅[创建设备限制](enrollment-restrictions-set.md#create-a-device-limit-restriction)

## <a name="azure-device-limit-restriction"></a>Azure 设备限制

Azure 设备限制设置了 Azure AD 联接或 Azure AD 注册的最大设备数。 若要设置“每位用户的最大设备数”，请转到“Azure 门户”>“Azure Active Directory” > “设备”  。 有关详细信息，请参阅[配置设备设置](/azure/active-directory/devices/device-management-azure-portal)

## <a name="settings-applied-based-on-user-affinity"></a>基于用户关联应用的设置

如果同时设置了 Intune 和 Azure 设备限制，下表显示基于用户关联设置将应用的内容。

| 设备平台 | 用户关联 | Azure 应用 | Intune 应用 |
| ----- | ----- | ----- | ----- | ----- |
| Android Enterprise 工作配置文件 | 是 | 是 | 是|
| Android Enterprise 专用设备 | 否 | 否 | 否 |
| Android Enterprise 完全托管设备 | 是 | 是 | 是 |
| Android 设备管理员 | 是 | 是 | 是 |
| Android 设备管理员 DEM | 否 | | 否 | 
| iOS/macOS BYOD | 是 | 是 | 是 |
| iOS/macOS 自动设备注册 (ADE) | 是 | 是 | 是 |
| iOS/macOS ADE | 否 | 是 | 否 |
| Windows BYOD | 是 | 是 | 是 |
| 仅 Windows MD | | 是 | 是 |
| 已联接 Windows Azure AD| 是 | 是 | 否 |
| Windows Autopilot | 是 | 是 | 否 |
| 已联接 Windows 混合 Azure AD | 否 | 否 | 是 |
| Windows 共同管理 | 否 | 是 | 否 |
| Windows DEM | 否 | 是 | 否 |
| Windows 批量注册 | 否 | 是 | 否 |


## <a name="android-and-ios-devices"></a>Android 和 iOS 设备

### <a name="ios-or-android-devices-example-1"></a>iOS 或 Android 设备示例 1

- Azure 的每位用户的最大设备数设置为 3。
- Intune 的设备限制设置为 5。
 
**结果：** 最大数量是针对每位用户的。 例如，如果你注册了三个 Intune 设备，则第四个设备的 Azure 注册将会失败，因为设置会限制设备的注册数。

### <a name="ios-or-android-devices-example-2"></a>iOS 或 Android 设备示例 2

- Azure 的“每位用户的最大设备数”设置为 20。
- Intune 的设备限制设置为 2。

**结果：** 你可以成功注册两个设备。 对于任何其他设备，Intune 注册将被阻止。 无用户关联的 ADE 受 Azure 设备注册限制的制约，尽管它不与用户关联。

## <a name="windows-devices"></a>Windows 设备

Intune 设备限制不适用于以下 Windows 注册类型：
- 共同托管的注册
- 组策略对象 (GPO) 注册
- 已联接 Azure AD 的注册
- 已联接 Bulk Azure AD 的注册
- Autopilot 注册
- 设备注册管理员注册

不能对这些注册类型强制执行设备限制，因为它们被视为共享设备方案。 可以在 Azure Active Directory 中为这些注册类型设置硬限制。

对于 Azure 中的设备限制，“每位用户的最大设备数”设置适用于已联接 Azure AD 或已注册 Azure AD 的设备。 此设置不适用于已联接混合 Azure AD 的设备。

### <a name="windows-10-example-1"></a>Windows 10 示例 1

- Azure 的“每位用户的最大设备数”设置为 5。
- Intune 的“设备限制”设置为 3。
- 设备为已联接混合 Azure AD 并自动注册（GPO 已配置）。

**结果：** 由于注册是通过 GPO 推送的，因此 Azure 设备注册限制不适用。  Intune 设备限制也不适用。

### <a name="windows-10-example-2"></a>Windows 10 示例 2

- Azure 的“每位用户的最大设备数”设置为 5。
- Intune 的设备限制设置为 2。
- 通过“设置” > “访问工作或学校帐户” > “连接”，联接设备到本地域并注册  。

**结果：** 只能注册两个设备，否则其将被阻止。 最多可以注册五个设备。


## <a name="next-steps"></a>后续步骤

- [在 Azure 中创建设备限制。](/azure/active-directory/devices/device-management-azure-portal#configure-device-settings)
- [在 Azure 中配置设备设置。](enrollment-restrictions-set.md#create-a-device-limit-restriction)
- [详细了解注册和联接域。](/azure/active-directory/devices/overview#getting-devices-in-azure-ad)