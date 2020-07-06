---
title: Android Enterprise 安全性配置框架
titleSuffix: Microsoft Intune
description: 了解针对 Android Enterprise 设备基本安全性和高安全性建议的限制和设置。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/24/2020
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
ms.openlocfilehash: 6ecd15ea98ff9fa5ff0ff6ff570e644a8dcf5003
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2020
ms.locfileid: "85502920"
---
# <a name="android-enterprise-security-configuration-framework-app-configuration-policies"></a>Android Enterprise 安全配置框架应用配置策略

作为 [Android Enterprise 安全配置框架](android-configuration-framework.md)的一部分，必须为 Android Enterprise 设备正确设置应用配置策略。

Android Enterprise 工作配置文件设备旨在用于隔离工作数据和个人数据。 Android Enterprise 完全受管理设备仅设计用于工作数据或学校数据。 因此，部署在这些设备上的 Microsoft 应用必须配置为禁止个人帐户。

## <a name="disallow-personal-accounts-for-microsoft-apps-on-android-enterprise-devices"></a>禁止在 Android Enterprise 设备上对 Microsoft 应用使用个人帐户

1. 将应用添加到托管 Google Play。 有关详细信息，请参阅[使用 Intune 将托管 Google Play 应用添加到 Android Enterprise 设备](../apps/apps-add-android-for-work.md)。
2. 为每个托管 Google Play 应用创建策略，如[为受管理 Android Enterprise 设备添加应用配置策略]()中所述。
3. 在每个策略中创建以下单个键：

    | Key | 值 |
    | --- | --- |
    | com.microsoft.intune.mam.AllowedAccountUPNs | 一个或多个；分隔的 UPN。<br>仅允许此键定义的托管用户帐户。<br>对于已注册 Intune 的设备，{{userprincipalname}} 令牌可用于表示已注册的用户帐户。 |


## <a name="next-steps"></a>后续步骤
应用 [Android Enterprise 工作配置文件安全设置](android-work-profile-security-settings.md)或 [Android Enterprise 完全受管理的安全设置](android-fully-managed-security-settings.md)。