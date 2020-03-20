---
title: 为 Intune 加密 Android 设备 | Microsoft Docs
description: 关于根据 Intune 需要启用 Android 设备加密的步骤
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/19/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: d4430e92-04cc-48e9-a77a-81b95a90b6b3
searchScope:
- User help
ROBOTS: ''
ms.reviewer: arnab
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: ee2d220e308b406251f049e1c17422f89ee36534
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79348778"
---
# <a name="encrypting-your-android-device"></a>加密 Android 设备

如果设备丢失或被盗，设备加密可保护文件和文件夹免遭未经授权的访问。 启用设备加密后，只有拥有正确密码或 PIN 的个人才能登录到你的设备。 

你的组织可能会要求你加密 Android 设备，然后你才能访问学校或工作资源。 默认情况下，一些较新的 Android 设备已加密，开箱即用。  

## <a name="turn-on-encryption"></a>启用加密

如果公司门户或 Microsoft Intune 应用提示你加密设备，请完成以下步骤。 

> [!Note]
> 无法对 Huawei、Vivo 和 OPPO 中的某些 Android 设备进行加密。 请单击[此处](your-device-appears-encrypted-but-cp-says-otherwise-android.md)，查看详细信息。  

1. 设置设备屏幕锁。  
    a. 转到“设置”   > “锁定屏幕和安全性”   > “屏幕锁定类型”  。  
    b. 选择“PIN”、“密码”或“模式”    。  
    c. 按照屏幕上的说明配置锁屏界面。  

2. 返回“锁屏界面和安全”并选择“安全启动”   。
3. 选择“设备打开时需要 PIN” > “确定”   。
4. 输入你的 PIN 以确认并加密你的设备。
5. 打开公司门户或 Microsoft Intune 应用。
    * 公司门户用户：选择设备，然后点击“检查设备设置”  。 
    * Microsoft Intune 用户：必须等到页面更新，但是当页面更新后，加密状态应更改为“符合”。  

运行 Android 4.4 及更低版本的设备可能没有“安全启动”选项  。 在这种情况下，请完成以下步骤来加密你的设备。

1. 转到“设置” > “安全” > “加密设备”    。 不同 Android 设备的屏幕标签有所不同。 如果看不到“加密设备”选项，请在以下项中查看  ：
    * “存储” > “存储加密”  
    * “存储” > “锁屏界面和安全” > “其他安全设置”    

2. 按照屏幕上的说明操作。 在加密期间，设备可以重启几次。
3. 打开公司门户或 Microsoft Intune 应用。
    * 公司门户用户：选择设备，然后点击“检查设备设置”  。  
    * Microsoft Intune 用户：必须等到页面更新，但是当页面更新后，加密状态应更改为“符合”。

## <a name="troubleshoot"></a>故障排除  
**问题**：你已加密设备，并且

- 已禁用加密按钮。
- 出现一条消息，指出仍需要加密。
- 尝试使用公司门户或 Microsoft Intune 应用时，发生错误。

**要尝试的操作**

- 确保设备已充电并已插入。  
- 确保设备上已设置 PIN 或密码。  

仍需帮助？ 请联系公司支持人员（访问[公司门户网站](https://go.microsoft.com/fwlink/?linkid=2010980)获取联系信息），或写邮件给 <a href="mailto:wintunedroidfbk@microsoft.com?subject=I'm having trouble with encryption on my Android device&body=Describe the issue you're experiencing here.">Microsoft Android 团队</a>。  
