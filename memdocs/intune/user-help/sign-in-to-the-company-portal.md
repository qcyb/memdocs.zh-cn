---
title: 如何登录公司门户应用 | Microsoft Docs
description: 了解如何在多个平台上登录到公司门户应用。
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 12/31/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: cfd214bc-f072-4808-af2e-a3cbf7af9bca
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 4088185da2c01cfa7fd343203f7452d2796c4466
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79335817"
---
# <a name="sign-in-to-company-portal"></a>登录公司门户  

可通过三种方式登录公司门户应用：

* 使用工作电子邮件地址和密码登录。  
* 使用基于证书的身份验证登录。  
* 从另一台设备登录。    


## <a name="sign-in-with-your-email-address-and-password"></a>使用电子邮件地址和密码登录
以下步骤显示来自适用于 iOS 的公司门户的屏幕截图。  

1. 在设备上打开应用，点击“登录”  。  

   ![公司门户登录页面的示例屏幕截图。](./media/intune-ios-cp-signin-1908.png)


2. 输入“工作或学校帐户”，然后单击“下一步”   。

   ![提示用户只提供电子邮件地址，而不是在同一屏幕上同时提供电子邮件和密码。](./media/cp_ios_aad_signin_after_1804_002.png)

3. 输入密码，然后点击“登录”  。

   ![在接受其电子邮件地址之后，提示用户输入密码。](./media/cp_ios_aad_signin_after_1804_003.png)

4. 此应用会验证你的凭据。 完成后，你可以访问组织的资源并安装可用应用。  

   ![在经过身份验证过程后，公司门户应用进行登录，并显示加载栏。](./media/cp_ios_aad_signin_after_1804_004.png)

## <a name="sign-in-with-certificate-based-authentication"></a>使用基于证书的身份验证登录
仅当组织允许进行基于证书的身份验证，并且你有可供使用的证书，你才会看到此登录选项。  

1. 在设备上打开公司门户应用。  

2. 输入**工作或学校账户**。  

3. 点击“使用证书登录”  链接。  

4. 点击“继续”  以使用该证书。  

## <a name="sign-in-from-another-device"></a>从另一台设备登录

如果公司使用智能卡访问用户的电脑，则用户很可能必须从另一台设备登录来进行身份验证。  

1. 在设备上打开公司门户应用。 请确保它便是用于访问工作资源的设备。       

1. 选择“从另一台设备登录”  。  

   ![公司门户的登录页提示用户输入电子邮件地址。  显示“下一步”按钮和“从另一台设备登录”链接。 此外还有转向“无法访问帐户？”的链接。 底部的链接指向 Microsoft 隐私和 Cookie 信息。](./media/cp_ios_aad_signin_after_1804_005.png)

2. 会收到用于登录公司门户的一次性唯一验证码。 复制代码。

   ![通过使用工作计算机的唯一密码访问 https://microsoft.com/devicelogin 页面，然后使用验证码进行登录可获得说明。](./media/cp_ios_aad_signin_after_1804_006.png)

3. 在其他设备（用于进行身份验证的设备）上，打开浏览器并转到 [https://microsoft.com/devicelogin](https://microsoft.com/devicelogin)。 输入或粘贴代码。  

   ![用户工作计算机上用户浏览器的图像，而不是公司门户应用的图像。 显示的“设备登录”页将提示用户输入他们在公司门户应用中收到的验证码。](../fundamentals/media/whats-new-app-ui/cp_ios_aad_signin_from_another_device_after_1704_004.png)

4. 选择“继续”  以允许公司门户登录你的工作设备。   

   ![用户已将唯一代码输入到字段中，“设备登录”站点要求确认 Intune 公司门户是接收授权以进行登录的正确应用。](../fundamentals/media/whats-new-app-ui/cp_ios_aad_signin_from_another_device_after_1704_005.png) 

5. 验证码经验证后，便可关闭窗口。  

   ![确认页显示用户现在已登录其设备上的公司门户应用，可以关闭此页。](../fundamentals/media/whats-new-app-ui/cp_ios_aad_signin_from_another_device_after_1704_006.png)

6. 公司门户应用会使你在工作设备上登录。  

   ![通过身份验证过程后，公司门户应用登录，并通过一个加载条提示进程。](./media/cp_ios_aad_signin_after_1804_007.png)

仍需帮助？ 请与公司支持人员联系。 有关联系信息，请查看[公司门户网站](https://go.microsoft.com/fwlink/?linkid=2010980)。  
