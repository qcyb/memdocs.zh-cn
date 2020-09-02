---
title: 在移动设备上安装 Mobile Threat Defense
description: 了解什么是移动威胁防御应用，以及如何进行设置。
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/20/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.custom: intune-enduser, contperfq1
ms.collection: ''
ms.openlocfilehash: 37b7006ef912d87276c11e09cb6db0c0f14059c4
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193906"
---
# <a name="install-mobile-threat-defense-app"></a>安装移动威胁防御应用  

> [!TIP]
> 市场上有各种各样的 MTD 应用。 你的组织应告诉你要使用哪一个。 如果系统提示你安装 MTD 应用，并且没有立即重定向到设置或安装应用，请联系 IT 支持人员寻求帮助。  

作为组织安全要求的一部分，你可能需要安装移动威胁防御 (MTD) 供应商应用。 此类应用可检测并提醒你设备上的威胁，例如可疑的应用、网络或 OS 漏洞。  

如果没有要求的 MTD 应用，则会阻止你使用工作或学校帐户登录受保护的托管应用（如 Microsoft Excel 或 OneDrive）。 本文介绍[如何安装 MTD 应用](set-up-mobile-threat-defense.md#set-up-mtd-app)以及重新获取访问权限。    

## <a name="mtd-apps-for-ios"></a>适用于 iOS 的 MTD 应用
以下 MTD 应用通常用于 iOS 设备。 选择应用以在 App Store 中打开其列表。   

* [Lookout for Work](https://go.microsoft.com/fwlink/?linkid=2139367)
* [Symantec Endpoint Protection (SEP) Mobile](https://go.microsoft.com/fwlink/?linkid=2139141)
* [Sandblast Mobile Protect](https://go.microsoft.com/fwlink/?linkid=2139231)
* [Zimperium zIPS](https://go.microsoft.com/fwlink/?linkid=2139232)


## <a name="mtd-apps-for-android"></a>适用于 Android 的 MTD 应用 
以下 MTD 应用通常用于 Android 设备。 选择应用以在 Google Play 中打开其列表。  

* [Lookout for Work](https://go.microsoft.com/fwlink/?linkid=2139453)
* [Symantec Endpoint Protection (SEP) Mobile](https://go.microsoft.com/fwlink/?linkid=2139454)
* [SandBlast Mobile Protect](https://go.microsoft.com/fwlink/?linkid=2139455)
* [Zimperium mobile IPS (zIPS)](https://go.microsoft.com/fwlink/?linkid=2139142)  


## <a name="information-your-organization-can-see"></a>组织可以查看的信息   

组织无法查看个人应用中的任何数据，如文本、电子邮件和图片。 MTD 应用会将有关应用的信息（如名称和版本）报告给你的组织。 报告的实际信息取决于公司使用的 MTD 供应商。 你的组织可能会看到：   

* 应用名称  
* 应用 ID：在 Google Play 中标识应用的唯一名称。  
* 应用版本和短版本号：应用的特定发行版号。  
* 应用程序包和动态大小：应用在设备中使用的空间大小。 


## <a name="set-up-mtd-app"></a>设置 MTD 应用 
当你登录到受保护的应用时，系统会提示你安装 MTD 应用。 按照屏幕上的步骤完成安装并获取对受保护的应用的访问权限。 

有关更多上下文，请参阅本部分中的 [iOS](set-up-mobile-threat-defense.md#ios-setup) 或 [Android](set-up-mobile-threat-defense.md#android-setup) 说明。 这些是补充性步骤，并不是为了替换屏幕上显示的说明。 

如果系统提示你安装 MTD 应用但你不确定要安装哪一种，请联系 IT 支持人员寻求帮助。  

### <a name="device-registration"></a>设备注册  
只有设备注册才能确认你的身份，才能将你的学校或工作帐户连接到设备。 如果你的设备未注册，则在安装 MTD 应用之前，系统会自动指导你完成屏幕上的这些步骤。   

有关设备注册的详细信息，请参阅[在组织的网络上注册个人设备](/azure/active-directory/user-help/user-help-register-device-on-network)。  

### <a name="ios-setup"></a>iOS 设置  
这些步骤从**获取访问权限**屏幕上开始，该屏幕在你登录到受保护的应用后会显示。  

1. 在“获取访问权限”屏幕上，按照说明安装组织要求的 MTD 应用  。   
2. 返回到“获取访问权限”屏幕并选择“打开”   。  
3. MTD 应用要求打开 Microsoft Authenticator 的权限。 选择“打开”  。 
4. 选择工作帐户进行登录。 
5. 等待 MTD 应用扫描设备的安全威胁。 
6. 返回到你最初尝试访问的学校或工作应用。 此时，你的组织可能会提示你配置其他应用安全要求，例如创建 PIN。   
7. 现在应该可以访问应用。 如果仍被阻止：  
    * 在“获取访问权限”屏幕上，选择“重新检查”   。  
    * 转到 MTD 应用并检查现有的威胁。 完成建议步骤以解决威胁并重新获得访问权限。    

### <a name="android-setup"></a>Android 安装程序 
这些步骤从**获取访问权限**屏幕上开始，该屏幕在你登录到受保护的应用后会显示。  

1. 在“获取访问权限”屏幕上，按照说明安装组织要求的 MTD 应用  。  
2. 返回到“获取访问权限”屏幕并选择“打开”   。  
3. MTD 应用要求访问设备的特定区域的权限（如果需要）。 为了使此应用正常运行，必须“允许”访问联系人  。 请求的权限将因 MTD 供应商而异。  
4. 选择工作帐户进行登录。  
5. 等待 MTD 应用扫描设备的安全威胁。  
6. 返回到你最初尝试访问的学校或工作应用。 此时，你的组织可能会提示你配置其他应用安全要求，例如创建 PIN。  
7. 现在应该可以访问应用。 如果仍被阻止：  
    * 在“获取访问权限”屏幕上，选择“重新检查”   。  
    * 转到 MTD 应用并检查现有的威胁。 完成建议步骤以解决威胁并重新获得访问权限。  


## <a name="resolving-a-threat"></a>解决威胁
如果检测到威胁超出组织定义的威胁级别，你的组织可以：  
   
* 阻止访问：登录到你的工作或学校帐户时，阻止使用组织的受保护应用。  
* 擦除数据：从组织的一个或多个受保护的应用删除你的工作或学校数据。  

若要解决威胁并重新获取对受保护的应用的访问权限，请执行以下步骤：  

1. 在你的设备上打开 MTD 应用。     
2. 通读应用中的威胁详细信息，其中介绍了如果不解决，该威胁可能会如何影响你的设备，以及如何解决该威胁。 
3. 在设备上进行所需的更改后，返回到 MTD 应用并启动新扫描。 重复上述步骤，直到解决所有威胁。 你的更改可能需要几分钟时间才能与组织同步。 这些更改同步后，你将会重新获取对受保护的应用的访问权限。 

## <a name="get-support"></a>获取支持
请转到[公司门户网站](https://go.microsoft.com/fwlink/?linkid=2010980)，查找组织的联系人信息。 请联系他们以获得帮助：

* 确定要使用的 MTD 应用  
* 安装  
* 安装失败  
* 检测/解决威胁  
* 卸载 MTD 应用   
 

### <a name="share-app-logs-with-it-support"></a>与 IT 支持人员共享应用日志  
你还可以将应用日志发送给你的 IT 支持人员，为他们提供有关安装失败的更多上下文。  
* Android 用户：从公司门户[上传并通过电子邮件发送日志](./send-logs-to-your-it-admin-by-email-android.md)。   

* iOS 设备用户：从适用于 iOS 的 Microsoft Edge [检索并发送日志](/intune/apps/manage-microsoft-edge#use-microsoft-edge-to-access-managed-app-logs)。  


## <a name="next-steps"></a>后续步骤  

请参阅以下文章，详细了解托管应用的工作原理、如何获取它们以及如何识别正在使用的应用。  

* [在 Android 设备上使用托管应用](use-managed-apps-on-your-device-android.md)
* [在 iOS 设备上使用托管应用](use-managed-apps-on-your-device-ios.md)  

仍需帮助？ 请与公司支持人员联系。 有关联系信息，请查看[公司门户网站](https://go.microsoft.com/fwlink/?linkid=2010980)。