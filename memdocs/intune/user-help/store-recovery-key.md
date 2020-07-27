---
title: 通过公司门户网站在 Intune 中存储恢复密钥
description: 从公司门户网站上传和存储设备恢复密钥。
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/17/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: annochiva
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 826515026e578cb993bb706fc61dedb4a80fb3e6
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2020
ms.locfileid: "86464973"
---
# <a name="store-your-personal-filevault-key"></a>存储你的个人 FileVault 密钥 

存储个人加密 macOS 设备的 FileVault 密钥。 除满足加密要求外，将密钥存储在 Intune 中还有助于： 

* 轻松、快速地从任何设备检索或轮换密钥。 
* 如果需要检索或轮换密钥，并且无法访问应用或网站以自行操作，请向支持人员寻求帮助。


## <a name="retrieve-or-rotate-the-key"></a>检索或轮换密钥

如果设备被锁定，可以从以下位置检索密钥：
   
- 公司门户网站
- 适用于 iOS/iPadOS 的公司门户应用 
- 适用于 Android 的公司门户应用
- Intune 应用
 
 具有 Intune 管理员访问权限的 IT 支持人员可以在设备锁定时为你轮换个人恢复密钥。他们还可以查看密钥，但只能查看属于公司拥有的设备。 IT 支持人员无法查看属于个人设备的恢复密钥。   


## <a name="do-i-need-to-store-my-key"></a>是否需要存储密钥？  
IT 支持人员会告诉你是否需要上传个人恢复密钥。 如果你组织的 IT 部门通常与你通信，你可能会收到适用于 iOS/iPadOS 或 Android 的公司门户应用的通知。 

仅当你属于以下类别之一时，我们才建议上传恢复密钥：
* 在向组织注册设备之前对设备进行了加密。 
* 通过 macOS 系统首选项手动加密设备。   

根据组织的策略，可能必须上传密钥才能访问设备上的公司资源。  

## <a name="upload-personal-recovery-key"></a>上传个人恢复密钥 
完成这些步骤，为加密的 Mac 设备保存个人 FileVault 密钥。  


1. 转到[公司门户网站](https://portal.manage.microsoft.com)并使用学校和工作帐户进行登录。 
2. 选择加密的设备。
3. 选择“存储恢复密钥”。  
4. 输入 24 个字符的字母数字 FileVault 密钥。  
5. 再次输入密钥。 选择“保存”。
6. 公司门户将尝试验证、轮换和保存你的个人恢复密钥。 保存密钥后，无需执行进一步操作。 如果你在上传完成之前离开网站，则可以在下次登录时在设备详细信息页面上查看其状态。  

如需详细了解会在此过程中出现的消息，请参阅[公司门户消息](store-recovery-key.md#company-portal-messages)。  

## <a name="company-portal-messages"></a>公司门户消息

|消息  |含义  |
|---------|---------|
|密钥必须匹配。 请检查密钥，然后重试。     | 显示在“确认恢复密钥”框下，让你知道密钥不匹配。 重新键入两个字段中的密钥，然后重试保存。        |
|无法更新设备的恢复密钥。| 在屏幕顶部显示为 Toast 通知，让你知道公司门户无法存储恢复密钥。 有关更多详细信息，请选择你的加密设备。 然后阅读页面顶部的消息，了解后续步骤。 |
|我们无法上传你的恢复密钥。 请检查是否输入了正确的密钥，然后重试。 如果问题仍然存在，请尝试手动轮换密钥。 点击此处了解详细信息。     | 显示在“设备详细信息”页面上，可能意味着以下几点：首先，公司门户无法轮换和保存密钥，因为你输入的密钥不正确。 请验证你是否具有正确的密钥，然后重试。 第二种可能性是你的设备有一段时间没有与你的组织签入。 若要从你的组织同步最新的更新，请选择“设备”>“状态” > “检查访问” 。 然后再次尝试存储恢复密钥。 最后，如果问题仍然存在，这可能意味着你的组织尚未在他们的端上启用 FileVault。 请与你的 IT 支持人员联系，让他们知道你已同步设备，但仍无法存储 FileVault 密钥。         |
|恢复密钥已更新。 如果你已锁定设备并需要检索密钥，请登录公司门户并选择“获取恢复密钥”。    | 显示在“设备详细信息”页上。 你保存的密钥已成功轮换，并存储了新的个人恢复密钥。    |



## <a name="it-pro-support"></a>IT 专业支持

如果你是 IT 支持人员，并且想要为 Mac 设备配置和管理 FileVault 加密，请参阅[通过 Intune 对 macOS 使用 FileVault 磁盘加密](https://docs.microsoft.com/mem/intune/protect/encrypt-devices-filevault)。  

## <a name="next-steps"></a>后续步骤

你始终可以从公司门户网站、Intune 应用以及适用于 iOS 和 Android 的公司门户应用检索密钥，并用它来访问你的 Mac 设备。 若要了解如何检索恢复密钥，请参阅[获取恢复密钥](get-recovery-key-cpweb.md)。

从公司门户网站了解还可以执行的操作。 若要获取操作列表，请参阅[使用 Intune 公司门户网站](using-the-intune-company-portal-website.md)。  

仍需帮助？ 请与 IT 支持人员联系。 有关联系信息，请查看[公司门户网站](https://go.microsoft.com/fwlink/?linkid=2010980)。  
