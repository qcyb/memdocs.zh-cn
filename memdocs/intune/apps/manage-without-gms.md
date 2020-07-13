---
title: 如何在无法访问 Google 移动服务的环境中使用 Intune
titleSuffix: Microsoft Intune
description: 了解如何在无法访问 Google 移动服务的环境中使用 Intune。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7955afb2aef88e3787546843cc477bce22369a4d
ms.sourcegitcommit: b90d51f7ce09750e024b97baf6950a87902a727c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86022375"
---
# <a name="how-to-use-intune-in-environments-without-google-mobile-services"></a>如何在无法访问 Google 移动服务的环境中使用 Intune

Microsoft Intune 在管理 Android 设备时使用 Google 移动服务 (GMS) 与 Microsoft Intune 公司门户通信。 在某些情况下，设备可能暂时或永久无法访问 GMS。 例如，设备可能在交付时没有安装 GMS，或者设备可能连接到的是无法访问 GMS 的封闭网络。 本文档总结了在无法访问 GMS 的环境中安装并使用 Intune 来管理 Android 设备时可能会观察到的差异和限制。

## <a name="install-the-intune-company-portal-app-without-access-to-the-google-play-store"></a>在无法访问 Google Play 商店的情况下安装 Intune 公司门户应用 

### <a name="for-users-outside-of-peoples-republic-of-china"></a>面向中华人民共和国以外的用户

如果无法访问 Google Play，Android 设备可以下载并旁加载 [面向 Android 的 Microsoft Intune 公司门户](https://www.microsoft.com/en-us/download/details.aspx?id=49140)应用。 以这种方式进行安装，应用不会自动接收更新或修复程序。 请务必定期手动更新和修补应用。 

### <a name="for-users-in-peoples-republic-of-china"></a>面向中华人民共和国的用户

由于目前在中华人民共和国无法访问 Google Play 商店，因此 Android 设备必须从中国的应用市场获取应用。 有关详细信息，请参阅[在中华人民共和国安装公司门户应用](../user-help/install-company-portal-android-china.md)。

## <a name="limitations-of-intune-device-administrator-management-when-gms-is-unavailable"></a>无法访问 GMS 时的 Intune 设备管理员管理限制 

### <a name="unavailable-intune-features"></a>不可用的 Intune 功能

一些 Intune 功能依赖 GMS 组件（如 Google Play 商店或 Google Play Services）。 由于这些组件在无法访问 GMS 的环境中不可用，因此 Intune 管理员控制台中的以下功能可能不可用。  

| 方案  | 功能  |
|-----------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 设备合规性策略  | 在创建或编辑面向 Android 设备管理员的合规性策略时，“Google Play 保护机制”下列出的所有选项都不可用。  |
| 应用保护策略（条件启动）  | “SafetyNet 设备证明”和“要求对应用进行威胁扫描”设备条件无法用于条件启动。  |
| 客户端应用  | 类型为“Android”的应用不可用。 请改用业务线应用来部署和管理应用。  |
| 移动威胁防御  | 请与你的 MTD 供应商合作，以了解他们的解决方案是否与 Intune 集成、是否可用于相应区域以及是否依赖 GMS。  |

### <a name="some-tasks-may-be-delayed"></a>有些任务可能会延迟 

在可访问 GMS 的环境中，Intune 依赖推送通知来加速完成任务。 例如，如果你尝试远程擦除设备，通知通常会在几秒钟内推送到设备。 在无法访问 GMS 的情况下，推送通知也可能不可用。 因此，Intune 必须等到下次设备签入时间，才能完成任务。  

已注册的 Android 设备每 8 小时向 Intune 报告一次。 例如，如果设备在下午 1:00 向 Intune 报告，而远程任务的发布时间是下午 1:05，那么 Intune 会在晚上 9:00 与设备联系，以完成任务。 

以下任务最长可能需要 8 小时才能完成： 

Intune 控制台：
- 完全擦除
- 选择性擦除
- 新的或更新的应用部署
- 远程锁定
- 密码重置

面向 Android 的 Intune 公司门户应用：
- 远程设备删除
- 设备重置
- 安装可用的业务线应用

Intune 公司门户网站：
- 设备删除（本地和远程）
- 设备重置
- 设备密码重置

如果设备是最近注册的，则会更频繁地运行合规性、不合规性和配置签入。 若要详细了解设备签入，请参阅 [Microsoft Intune 中设备策略和配置文件的常见疑问、问题和解决方法](../configuration/device-profile-troubleshoot.md)。 

## <a name="next-steps"></a>后续步骤

- [使用 Microsoft Intune 将应用分配到组](../apps/apps-deploy.md)
