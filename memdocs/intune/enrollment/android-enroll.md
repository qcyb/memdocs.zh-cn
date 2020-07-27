---
title: 在 Intune 中注册 Android 设备
titleSuffix: Microsoft Intune
description: 了解如何在 Intune 中注册 Android 设备。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 7/23/2019
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: f276d98c-b077-452a-8835-41919d674db5
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: d8506661c49fa4f9c8481a3caa96883c91e6d8bb
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2020
ms.locfileid: "86461753"
---
# <a name="enroll-android-devices"></a>注册 Android 设备

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Intune 管理员可按以下方式注册 Android 设备：
- Android Enterprise（提供了一组注册选项，为用户提供最新且安全的功能）：
    - [**Android Enterprise 工作配置文件**](android-work-profile-enroll.md)：已被授予访问公司数据权限的个人设备。 管理员可以管理工作帐户、应用和数据。 设备上的个人数据与工作数据分开，管理员不控制个人设置或数据。 
    - [**Android Enterprise 专用设备**](android-kiosk-enroll.md)：公司所有的单一用途设备，如数字签名、票证打印或库存管理。 管理员会将设备的用途限制为有限的一组应用和 Web 链接。 它还可以防止用户在设备上添加其他应用或执行其他操作。
    - [**Android Enterprise 完全托管设备**](android-fully-managed-enroll.md)：公司所有的单个用户设备，专门用于工作并非个人用途。 管理员可以管理整个设备，强制执行工作配置文件不可用的策略控制。
    - [**Android Enterprise 公司拥有的工作配置文件**](android-corporate-owned-work-profile-enroll.md)：适用于供公司和个人使用的单用户设备。
- [**Android 设备管理员**](android-enroll-device-administrator.md)，包括 Samsung Knox 标准版设备和 [Zebra 设备](../configuration/android-zebra-mx-overview.md)。 

## <a name="prerequisites"></a>必备条件

若准备管理移动设备，必须将移动设备管理 MDM 机构设置为“Microsoft Intune”。 请参阅[设置 MDM 机构](../fundamentals/mdm-authority-set.md)，了解有关说明。 第一次设置 Intune 以进行移动设备管理时，只需设置一次此项目。

对于 Android Enterprise，请参阅以下来自 Google 的支持文章，以确保 Android Enterprise 可用于你所在的国家或地区： https://support.google.com/work/android/answer/6270910

对于由 Zebra Technologies 制造的设备，你可能需要根据特定设备的功能授予公司门户额外的权限。 [Zebra 设备上的移动性扩展](../configuration/android-zebra-mx-overview.md)具有更多详细信息。

对于 Samsung Knox 标准版设备，存在[更多先决条件](android-samsung-knox-mobile-enroll.md)。

## <a name="next-steps"></a>后续步骤

- [设置 Android Enterprise 工作配置文件注册](android-work-profile-enroll.md)
- [设置 Android Enterprise 专用设备注册](android-kiosk-enroll.md)
- [设置 Android Enterprise 完全托管设备注册](android-fully-managed-enroll.md)
- [设置 Android 设备管理员注册](android-enroll-device-administrator.md)

