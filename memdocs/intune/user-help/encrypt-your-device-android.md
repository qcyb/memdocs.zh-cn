---
title: 为 Intune 加密 Android 设备 | Microsoft Docs
description: 关于根据 Intune 需要启用 Android 设备加密的步骤
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 03/31/2020
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: d4430e92-04cc-48e9-a77a-81b95a90b6b3
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: d9e074def368927504c3f3c1761ec21b3ab62d22
ms.sourcegitcommit: e17fc618d4c56c38a65c489b73ba27baa133ee7b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80696263"
---
# <a name="encrypting-your-android-device"></a>加密 Android 设备

如果设备丢失或被盗，设备加密可保护文件和文件夹免遭未经授权的访问。 这样，没有密码的用户就无法访问和读取你设备上的数据。 

组织可能会要求你必须先执行以下操作，然后才能访问学校或工作资源：

* [加密设备](#encrypt-device)
* [启用安全启动](#enable-secure-startup)
* [设置启动密码、PIN 或其他身份验证方法](#set-startup-passcode)  

> [!Note]
> 无法对 Huawei、Vivo 和 OPPO 中的某些 Android 设备进行加密。 有关详细信息，请参阅[设备已加密，但应用提示未加密](your-device-appears-encrypted-but-cp-says-otherwise-android.md)。  

## <a name="encrypt-device"></a>加密设备

若要加密设备，请按照以下步骤操作。 设备可能会多次重启。 

加密选项的名称和位置会因设备制造商和 Android 版本而异。 

1. 打开“设置”应用  。
2. 在应用的搜索栏中键入“安全性”  或“加密”  ，以查找相关设置。
3. 点击选项，以加密设备。 按照屏幕上的说明操作。  
4. 出现提示时，设置锁屏界面密码、PIN 或其他身份验证方法（如果组织允许的话）。 
5. 若要重新检查设置，请打开公司门户或 Microsoft Intune 应用。
    * 公司门户用户：选择设备，然后点击“检查设备设置”  。 
    * Microsoft Intune 用户：必须等到页面更新，但是当页面更新后，加密状态应更改为“符合”。 

## <a name="enable-secure-startup"></a>启用安全启动

组织可能要求你启用安全启动作为加密策略的一部分。 此功能要求，必须先输入密码或 PIN，然后才能启动电话，从而进一步保护你的设备。 你可能有其他许多身份验证选项，但这取决于组织是否允许。 

安全启动选项的名称和位置会因设备制造商和 Android 版本而异。 在一些设备上，此设置可能名为“强保护”  。 

1. 打开“设置”应用  。
2. 在应用的搜索栏中，键入“安全启动”  。
3. 依次点击“安全启动”   > “必须提供 PIN 才能打开设备”  。
4. 出现提示时，输入设备 PIN。   
5. 若要重新检查设置，请打开公司门户或 Microsoft Intune 应用。
    * 公司门户用户：选择设备，然后点击“检查设备设置”  。 
    * Microsoft Intune 用户：必须等到页面更新，但是当页面更新后，加密状态应更改为“符合”。  


## <a name="set-startup-passcode"></a>设置启动密码   
在你[加密设备](#encrypt-device)并[启用安全启动](#enable-secure-startup)后，系统会提示你设置设备 PIN、密码或其他身份验证方法（如果组织允许的话）。 无需执行其他步骤。 

若要选择或更改锁屏界面类型，请执行以下操作：

1. 打开“设置”应用  。
2. 在应用的搜索栏中，键入“锁屏”  。
3. 点击“锁屏类型”  。
4. 点击要使用的锁屏类型，然后按照屏幕上的说明操作进行确认。  

## <a name="troubleshoot"></a>故障排除    
**问题**：已禁用加密按钮。   

试一试  ： 
* 确保设备已充满电且已接通电源。 加密可能需要一段时间才能完成，所以需要电池充满电。   

**问题**：出现一条消息，指出仍需要加密设备。  

**要尝试的操作**：
   *  在设备上[设置锁屏界面](#set-startup-passcode)。 
   * [启用安全启动](#enable-secure-startup)。

仍需帮助？ 请联系公司支持人员（访问[公司门户网站](https://go.microsoft.com/fwlink/?linkid=2010980)获取联系信息），或写邮件给 <a href="mailto:wintunedroidfbk@microsoft.com?subject=I'm having trouble with encryption on my Android device&body=Describe the issue you're experiencing here.">Microsoft Android 团队</a>。  
