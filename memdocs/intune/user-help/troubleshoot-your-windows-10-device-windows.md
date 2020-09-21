---
title: Windows 10 设备访问学校或工作资源的疑难解答 | Microsoft Intune
description: 解决已注册的 Windows 10 设备的访问或帐户连接问题。
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 09/09/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 4ab630b6-47ff-443b-a2a5-be23388bcea7
searchScope:
- User help
ROBOTS: ''
ms.reviewer: amanh
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 7c96bef7c1be004714f0b06dd47c9c28850118da
ms.sourcegitcommit: d4ed7b4369389fd8ab07d28a7fa507797b6c6e57
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/10/2020
ms.locfileid: "89643424"
---
# <a name="troubleshoot-windows-10-device-access"></a>Windows 10 设备访问的疑难解答
本文介绍如何解决已注册的 Windows 10 设备的访问问题。 

## <a name="check-wi-fi-connection"></a>检查 Wi-Fi 连接  

需要连接到 Wi-Fi 才能访问工作或学校资源。 验证是否已连接到 Wi-Fi，然后再次尝试访问资源。  

## <a name="add-work-or-school-account-in-settings-app"></a>在“设置”应用中添加工作或学校帐户  
以下步骤与你注册设备时使用的步骤相同。 不过，如果你的帐户没有显示在“设置”应用中，你可能需要再次运行这些步骤。  

1. 打开“设置”应用  。 
2. 选择“帐户”  。
3. 下一步取决于你使用的 Windows 10 版本。 
    * 版本 1607 及更高版本：选择 **“访问工作或学校”** 。
    * 版本 1511 及更低版本：选择“工作单位访问”。  
4. 查看是否有你的帐户。 如果未列出，请选择“连接”加号按钮进行添加。 
5. 使用工作单位或学校凭据登录。 
6. 按照屏幕上的提示完成连接。  
7. 完成后，你的帐户将被添加为一个连接。 你将可以访问组织提供的任何资源。   

## <a name="contact-it-support-for-access-requirements"></a>与 IT 支持部门联系以了解访问要求  
如果“设置”应用中列出了你的工作或学校帐户，说明你的设备和帐户已经连接。 与 IT 支持部门联系，以获取有关访问问题的更多帮助。 他们可能已设置一些限制或要求，使你无法访问某些资源。  

## <a name="error-messages"></a>Error messages  

### <a name="we-couldnt-auto-discover-a-management-endpoint-matching-the-username-entered-please-check-your-username-and-try-again-if-you-know-the-url-to-your-management-endpoint-please-enter-it"></a>无法自动发现与所输入用户名匹配的管理终结点。 请检查用户名并重试。 如果你知道指向管理终结点的 URL，请输入它。

**原因**：无法验证你的帐户和提供的 URL（也称为管理终结点）。  

#### <a name="resolution"></a>解决方法
1. 重新输入你的用户名和密码。 
2. 如果这样仍不起作用，请与 IT 支持人员联系以获取正确的 URL（示例： www.yourcompany.onmicrosoft.com）。 
3. 出现提示时，输入所提供的 URL。 

### <a name="it-looks-like-youre-not-connected-make-sure-youre-connected-to-the-network"></a>看起来未连接。 请确保已连接到网络。

**原因**：你的设备未连接到 Wi-Fi，需要连接才能添加工作或学校帐户。     

#### <a name="resolution"></a>解决方法
1. 在设备工具栏或设置中，选择“网络状态”地球图标。
2. 选择“Wi-Fi 网络”>“连接”。  
3. 尝试重新连接你的帐户。  


## <a name="next-steps"></a>后续步骤  

仍需帮助？ 请与 IT 支持人员联系。 有关联系信息，请查看[公司门户网站](https://go.microsoft.com/fwlink/?linkid=2010980)。
