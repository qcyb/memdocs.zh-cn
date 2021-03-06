---
title: 使用 Microsoft Intune 重置设备密码 - Azure | Microsoft Docs
description: 在使用 Intune 进行管理或监视的设备上，使用“删除密码”操作删除或重置密码。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 47181d19-4049-4c7a-a8de-422206c4027e
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9d7e5fc7d16212c40fbbe5c1486ed3be76d2738f
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/27/2020
ms.locfileid: "83983108"
---
# <a name="reset-or-remove-a-device-passcode-in-intune"></a>在 Intune 中重置或删除设备密码

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

本文档讨论了 Android Enterprise（以前称为 Android for Work 或 AfW）设备上的设备级密码重置以及工作配置文件密码重置。 请务必记下这一区别，因为每种要求都有所不同。 设备级密码重置会重置整个设备的密码。 工作配置文件密码重置仅重置 Android 企业设备上用户工作配置文件的密码。

## <a name="supported-platforms-for-device-level-passcode-reset"></a>支持设备级别密码重置的平台

| 平台 | 是否支持？ |
| ---- | ---- |
| 版本在 6.x 及以下的 Android 设备 | 是 |
| 以设备所有者身份注册的 Android 企业设备 | 是 |
| iOS/iPadOS 设备 | 是 |
| 通过用户注册进行注册的 iOS/iPadOS 设备 | 否 |
| 使用工作配置文件注册的 Android 设备 | 否 |
| 版本在 7.0 及以上的 Android 设备 | 否 |
| macOS | 否 |
| Windows | 否 |

对于 Android 设备，这意味着仅在运行 6.x 或更早版本的设备上或在以展台模式运行的 Android Enterprise 设备上支持设备级密码重置。 这是因为 Google 不再支持从设备管理员授权应用中重置 Android 7 设备的密码，这适用于所有 MDM 供应商。

## <a name="supported-platforms-for-android-enterprise-work-profile-passcode-reset"></a>支持 Android 企业工作配置文件密码重置的平台

| 平台 | 是否支持？ |
| ---- | ---- |
| 使用工作配置文件注册并运行 8.0 及更高版本的 Android 企业设备 | 是 |
| 使用工作配置文件注册并运行 7.x 及更早版本的 Android 企业设备 | 否 |
| 运行 7.x 及更早版本的 Android 设备 | 否 |

要创建新的工作配置文件密码，请使用重置密码操作。 此操作会提示重置密码，并仅为工作配置文件创建新的临时密码。 

## <a name="reset-a-passcode"></a>重置密码


1. 使用以下任何角色登录到 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)：Azure Active Directory 全局管理员、Azure Active Directory Intune 服务管理员、支持人员或角色管理员。
2. 依次选择“设备”和“所有设备”   。
3. 从你管理的设备的列表中，选择一个设备，然后选择“重置密码”  。

## <a name="reset-android-work-profile-and-device-owner-passcodes"></a>重置 Android 工作配置文件和设备所有者设备的密码

受支持的使用工作配置文件注册的 Android 企业设备会为最终用户接收新的托管配置文件解锁密码或托管配置文件质询。

对于运行版本 8.x 或更高版本的 Android Enterprise 工作配置文件设备，最终用户会在注册完成后立即收到激活其重置密码的通知。 需提供和设置工作配置文件密码时会显示该通知。 在密码输入后，通知就会消除。

对于运行版本 8.x 或更高版本的 Android Enterprise 设备所有者或工作配置文件设备，在从控制台中选择重置密码后，MEM Intune 管理员会看到临时密码。 必须在设备上输入临时密码。 设备的临时密码将在控制台中显示 7 天。


## <a name="remove-iosipados-passcodes"></a>删除 iOS/iPadOS 密码

系统会从 iOS/iPadOS 设备中删除密码，而不是重置密码。 如果设置了密码符合性策略，则设备会提示用户在“设置”中设置新密码。

## <a name="next-steps"></a>后续步骤

要查看刚执行的操作的状态，请在“设备”中选择“设备操作”   。
