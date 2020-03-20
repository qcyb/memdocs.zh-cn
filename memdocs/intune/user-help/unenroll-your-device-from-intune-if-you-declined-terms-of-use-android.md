---
title: 拒绝“使用条款”后删除对设备的管理 | Microsoft Intune
description: ''
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 03/23/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 4278f000-0258-4de5-93a1-195b48e5061e
searchScope:
- User help
ROBOTS: ''
ms.reviewer: chrisbal
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 1c3b448726d52a838299e7be7a68611f460c4929
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79335453"
---
# <a name="remove-your-device-from-management-if-you-declined-terms-of-use"></a>拒绝“使用条款”后删除对设备的管理

如果在尝试登录到公司门户应用时拒绝了使用条款，则在将来的尝试中将无法登录到公司门户应用，因此需要使用这些“解决方法”说明来从 Intune 删除设备。

卸载公司门户应用时，同时将从 Intune 删除设备。 设备将无法再访问公司资源。 若要深入了解删除对设备的管理后会发生什么情况，请参阅[从 Intune 取消注册设备会发生什么情况？](what-happens-if-you-unenroll-your-device-from-intune-android.md)。

你需转到“设备管理员”  设置，并关闭“公司门户”  才能卸载公司门户应用。 由于你拥有的 Android 设备的不同，操作步骤可能也有些许不同。

## <a name="removing-the-device-from-the-company-portal-app"></a>从公司门户应用删除设备

若要从 Intune 删除设备并卸载公司门户应用，请执行以下操作：

1. 转到“设置”&gt;“安全”&amp;“屏幕锁定”&gt;“设备管理员”    。

    完成此步骤将立即取消注册你的设备。

2. 取消勾选“公司门户”  旁边的复选框或将其关闭。

    现在即可卸载公司门户应用。

## <a name="removing-data-collected-by-the-company-portal-app"></a>删除由公司门户应用收集的数据

若要删除 Android 适用的公司门户应用存储在设备上的所有数据，请执行以下操作：

- 在“应用程序”中单击该应用，然后单击“清除数据”按钮以清除应用数据
- 删除文件夹“\storage\internal storage\Android\data\com.microsoft.windowsintune.companyportal”


仍需帮助？ 请联系公司支持人员（访问[公司门户网站](https://go.microsoft.com/fwlink/?linkid=2010980)获取联系信息），或写邮件给 <a href="mailto:wintunedroidfbk@microsoft.com?subject=I'm having unenrolling my Android device&body=Describe the issue you're experiencing here.">Microsoft Android 团队</a>。
