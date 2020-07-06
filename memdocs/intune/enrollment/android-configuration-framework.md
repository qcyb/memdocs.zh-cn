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
ms.openlocfilehash: 6f0e4452f5209d569e11a782528582f4d5a76045
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2020
ms.locfileid: "85502916"
---
# <a name="android-enterprise-security-configuration-framework"></a>Android Enterprise 安全性配置框架

Android Enterprise 安全配置框架是一系列关于设备符合性和配置策略设置的建议。 这些建议有助于你根据自身的特定需求来定制组织的移动设备安全保护。

有安全意识的组织正在寻求确保移动设备上的企业数据受到保护的方法。 保护此类数据的一种方法是通过设备注册。 设备注册有助于组织：
- 部署符合性策略（如 PIN 强度、越狱/根验证等）。
- 部署配置策略（如 WIFI、证书、VPN）。
- 管理应用生命周期。

为了帮助你设置完整的安全方案，Microsoft 为 [Windows 10 中的安全配置](https://aka.ms/secconframework)引入了新分类。 Intune 也在其 Android Enterprise 安全配置框架中使用了类似的分类。 具体包括为基本安全性、增强安全性和高安全性而建议的设备符合性和设备限制设置。 下面的几篇文章介绍了这种分类：

1. [Android Enterprise 框架部署方法](framework-deployment-methodology.md)：用于部署安全配置框架的建议方法。
2. [Android 设备注册限制](device-enrollment-restrictions.md)：适用于 Android Enterprise 设备的预注册设备限制。
3. [为 Android Enterprise 设备设置应用配置策略](android-app-configuration-policies.md)：在设备上配置应用来禁止个人帐户。
4. [Android Enterprise 工作配置文件安全设置](android-work-profile-security-settings.md)：工作配置文件设备上的基本安全性和高安全性的特定配置设置。
5. [Android Enterprise 完全受管理的安全设置](android-fully-managed-security-settings.md)：完全受管理设备上的基本安全性、增强安全性和高安全性的特定配置设置。

## <a name="android-enterprise-enrollment-modes"></a>Android Enterprise 注册模式

随着 Android 5.0 的推出，Google 引入了 Android Enterprise，其中包括两种注册模式。 Android Enterprise 安全配置框架为这两种模式提供了建议。
- [完全受管理设备（设备所有者）](android-fully-managed-enroll.md)：对于与单个用户关联的企业拥有设备。 此类设备只用于工作，而不是供个人使用。
- [工作配置文件（配置文件所有者）](android-work-profile-enroll.md)：通常，对于 IT 人员希望在工作数据和个人数据之间有明确界限的个人拥有设备。 由 IT 人员控制的策略可确保工作数据无法传输到个人配置文件中。


## <a name="next-steps"></a>后续步骤

[Android Enterprise 框架部署方法](framework-deployment-methodology.md)