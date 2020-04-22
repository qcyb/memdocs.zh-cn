---
title: 你的 Android 设备似乎已加密 | Microsoft Docs
description: 解决公司门户和 Microsoft Intune 应用中的加密状态问题
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/14/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ba593c08-1a78-4013-8525-b45a948772ec
searchScope:
- User help
ROBOTS: ''
ms.reviewer: arnab
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 4fd08ba190654db5678766e34e3340330dcf3ca8
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "79346087"
---
# <a name="device-encrypted-but-apps-say-otherwise"></a>设备已加密，但应用却指示未加密

如果公司门户或 Microsoft Intune 应用指示你的设备未加密，但你确定设备已加密，请尝试执行本文中的步骤。  

## <a name="add-a-startup-pin"></a>添加启动 PIN

某些 Android 设备需要创建启动 PIN，确保设备安全。 此设置的位置位于设备的“设置”应用中  。 在不同的设备上，设置的名称和位置可能会有所不同。 例如，在 Samsung Galaxy S7 上，该设置称为“安全启动”  。 若要启用该设置并创建密码，请转到“设置” **“锁定屏幕和安全”** “安全启动” >    >   。  

## <a name="encrypt-the-entire-device"></a>加密整个设备

本节仅适用于公司门户应用。 某些设备支持选择加密整个设备或仅加密已用空间。 请选择“加密整个设备”选项。 如果选择“仅加密已用空间”：

1. [从公司门户中删除此设备](unenroll-your-device-from-intune-android.md)。
2. 解密已用空间。  
3. 加密整个设备。  
4. 重新注册设备。  

## <a name="downgrade-your-version-of-android"></a>降级 Android 版本

本节仅适用于公司门户应用。 如果设备提供降级到 Android 6.0 及更高版本的选项，请进行降级。 如果尝试进行设备降级，将存在数据丢失的风险。 若要避免此风险，建议联系公司支持人员解决此问题。 在[公司门户网站](https://go.microsoft.com/fwlink/?linkid=2010980)上获取公司支持人员的联系信息。  

## <a name="specific-manufacturer-issues"></a>特定制造商问题

一些 Android 设备（版本 7.0 及更高版本）会以与某些 Android 平台标准不同的方式加密数据。 这些加密方法将设备信息置于风险之中。 因此，这些设备不受支持。

有关受支持的 Android 设备的非详尽列表，请参阅 [Intune 中受支持的操作系统和浏览器](https://docs.microsoft.com/intune/fundamentals/supported-devices-browsers#supported-samsung-knox-standard-devices)一文。 如果你的设备未列于其中，请咨询设备制造商或与你的支持人员联系。

> [!Note]
> Microsoft 将与制造商协作以解决我们在测试中发现的，或用户上报的任何问题。 每当有新的信息可用时，我们会更新本文。

## <a name="update-devices"></a>更新设备

如果尚未将设备更新到最新版本的 Android，请转到设备的“设置”应用，并选择“更新”   。  

## <a name="next-steps"></a>后续步骤

仍需帮助？ 请联系公司支持人员（访问[公司门户网站](https://go.microsoft.com/fwlink/?linkid=2010980)获取联系信息），或写邮件给 <a href="mailto:wintunedroidfbk@microsoft.com?subject=I'm having trouble with enrolling my Android device&body=Describe the issue you're experiencing here.">Microsoft Android 团队</a>。  
