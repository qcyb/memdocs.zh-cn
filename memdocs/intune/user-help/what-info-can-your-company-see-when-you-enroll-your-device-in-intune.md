---
title: 注册你的设备时，你的公司可以看到哪些信息？
description: 介绍 IT 人员在托管设备上能看到和不能看到的内容。
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 06/11/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 12655728-a1af-4d89-97bc-925fe36c0dc4
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.collection: ''
ms.openlocfilehash: 740d9b68a0101e04e6bf690d09ecce7eaff4509e
ms.sourcegitcommit: 3217778ebe7fd0318810696e8931e427a85da897
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2020
ms.locfileid: "85107318"
---
# <a name="what-information-can-my-organization-see-when-i-enroll-my-device"></a>在我注册自己的设备时，我的组织可以看到哪些信息？

向 Microsoft Intune 注册设备时，组织看不到你的个人信息。 注册设备时，将为组织授予查看设备上特定信息的权限，如设备型号和序列号。 组织可使用此信息来帮助保护设备上的公司数据。

**你的组织永远看不到的内容：**

- 调用和 Web 浏览历史记录
- 电子邮件和短信
- 联系人
- 日历
- 密码
- 图片，包括照片应用中的照片或本机照片
- 文件

**你的组织始终可以看到的内容：**

- 设备型号（如 Google Pixel）
- 设备制造商（如 Microsoft）
- 操作系统和版本，如 iOS 12.0.1
- 应用清单和应用名称（如 Microsoft Word）。 在个人设备上，组织只能看到托管应用清单。 在公司拥有的设备上，组织可以查看所有应用广告资源。
- 设备所有者
- 设备名称
- 设备序列号
- IMEI

 > [!NOTE]
 > 对于 Android Enterprise 完全托管设备和专用设备，你将无法看到所有应用清单。
 
 > [!NOTE]
 > 按照以下方式之一安装时，应用被视为“托管应用”：
 > 1. 在 Intune 管理员发布应用为“可用”后，用户从公司门户应用进行安装。
 > 2. Intune 管理员发布应用为“必需”，并且应用已安装在设备上。 
 >
 > 如果你是组织中的 IT 管理员或支持人员，并且想要了解 Intune 中应用管理的详细信息，请参阅[了解非托管应用、托管应用和 MAM 应用的功能](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/understanding-the-capabilities-of-unmanaged-apps-managed-apps/ba-p/249164)。
    
**组织可能会看到的信息：**

- 电话号码：对于公司拥有的设备，公司可看到完整的电话号码。 对于个人拥有的设备，组织只能看到电话号码的最后四位数字。 可以在相应设备的“设备详细信息”页，查看每个设备的所有权类型。
- 设备存储空间：如果无法安装所需的应用，组织可以查看设备的存储空间，以确定空间是否不足。  
- 位置：对于公司拥有的设备，组织可以查看丢失设备的位置。 对于个人拥有的设备，组织永远看不到设备的位置，除非他们试图查找丢失的、受监督的 iOS 设备。 访问 [Apple iOS 文档](https://go.microsoft.com/fwlink/?linkid=853816)以详细了解受监督的设备。  
- 应用清单详细信息：如果组织使用 Mobile Threat Defense，则可以查看有关 iOS 设备中的应用的详细信息。 了解[移动威胁防御](set-up-mobile-threat-defense.md)的详细信息。 否则，对于个人拥有的设备，组织只能查看托管的应用清单。 对于公司拥有的设备，组织可以查看所有应用广告资源。
- 网络信息：可能向组织支持人员提供有关 Android 设备网络连接信息。 例如，如果组织要求设备在某个建筑物内使用，则设备将标识所连接的网络。 
