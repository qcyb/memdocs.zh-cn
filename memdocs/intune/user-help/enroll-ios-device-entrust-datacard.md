---
title: 通过 Intune 公司门户和 Entrust Datacard 注册 iOS 或 iPadOS 设备
description: 注册 iOS 或 iPadOS 设备，以及使用 Entrust Datacard 设置派生凭据身份验证。
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/31/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: tisilver
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 1e1f1c04bed91de3ac193ea3b6a07bde4e8658ba
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81638246"
---
# <a name="set-up-ios-or-ipados-device-with-company-portal-and-entrust-datacard"></a>通过公司门户和 Entrust Datacard 设置 iOS 或 iPadOS 设备

通过 Intune 公司门户应用注册设备，以获取对组织的电子邮件、文件和应用的安全移动访问权限。 注册设备后，它将成为托管设备  。 组织可通过移动设备管理 (MDM) 提供程序（如 Intune）为该设备分配策略和应用。  

在注册期间，还需在设备上安装派生凭据。 你的组织可能要求你在访问资源时使用派生凭据作为身份验证方法，或对电子邮件进行签名和加密。 

如果使用智能卡执行以下操作，则可能需要设置派生凭据：  

* 登录到学校或工作应用、Wi-Fi 和虚拟专用网络 (VPN)
* 使用 S/MIME 证书对学校或工作电子邮件进行签名和加密  

在本文中，你将：  

   * 通过 Intune 公司门户注册 iOS 或 iPadOS 移动设备。  
   * 从组织的派生凭据提供程序 [Entrust Datacard](https://www.entrustdatacard.com/) 获取派生凭据。  

### <a name="what-are-derived-credentials"></a>什么是派生凭据？  
派生凭据是派生自智能卡凭据并在设备上安装的证书。 它授予你对工作资源的远程访问权限，同时防止未经授权的用户访问敏感信息。  

派生凭据用于： 
* 对登录到学校或工作应用、Wi-Fi 和 VPN 的学生和员工进行身份验证
* 使用 S/MIME 证书对学校或工作电子邮件进行签名和加密

派生凭据实现美国国家标准与技术研究院 (NIST) 关于派生个人身份验证 (PIV) 凭据的准则（属于《特殊出版物 (SP) 800-157》）。  

## <a name="prerequisites"></a>必备条件

 若要完成注册，你必须具有：

* 你的学校或工作提供的智能卡
* 可使用智能卡登录的计算机或网亭的访问权限
* 你的移动设备
* 设备上安装的适用于 iOS 和 iPadOS 的 Intune 公司门户应用  


## <a name="enroll-device"></a>注册设备  
1. 打开移动设备上适用于 iOS/iPadOS 的公司门户应用，并使用你的工作帐户登录。  

2. 记下屏幕代码。  

    ![带有屏幕消息和代码的公司门户应用的示例图像。](./media/copy-code-intercede.png)   

3. 切换到已启用智能卡的设备，然后转到 https://microsoft.com/devicelogin 。 
4. 输入先前记下的代码。  

    ![公司门户网站的示例屏幕截图，其中显示了“输入代码”的提示。](./media/enter-code-intercede.png)   

5. 插入智能卡进行登录。   
6. 返回到移动设备上的公司门户应用，然后按照屏幕上的说明注册设备。  
7. 注册完成后，公司门户会通知你设置智能卡。 点击通知。 如果没有收到通知，请检查你的电子邮件。   

    ![设备主屏幕上的公司门户推送通知的示例屏幕截图。](./media/action-required-in-app-intercede.png)  

8. “设置移动智能卡访问权限”屏幕  ：   
    a. 点击指向组织设置说明的链接。 如果你的组织未提供其他说明，你将参阅本文。  
    b. 点击“开始”  。  

    ![公司门户的示例屏幕截图，“设置移动智能卡访问权限”屏幕。](./media/smart-card-info-intercede.png)

9. 切换到已启用智能卡的设备并打开 IdentityGuard。 
10. 找到智能凭据登录区域，然后选择登录按钮。  
11. 当系统提示你选择证书时，选择你的智能卡凭据。 然后选择“确定”  。 
12. 输入智能卡 PIN。  
13. 系统会要求你从操作列表中进行选择。 选择使你可以注册派生移动智能凭据的操作。 链接或按钮可能会显示“我要注册派生移动智能卡凭据”。   
14. 选择已成功下载并安装了启用智能凭据的应用程序。 然后继续到下一个屏幕。   
15. 输入有关派生智能卡凭据的信息。  
    a. 对于标识名称，请输入任何名称，如 Entrust Derived Cred  。  
    b. 在下拉菜单中，选择“委托 IdentityGudard 移动智能凭据”  。  
    c. 继续到下一个屏幕。 将看到一个 QR 码，下面有一个数字密码。  

16. 返回到你的移动设备。 在“公司门户”>“获取 QR 码”  屏幕上，点击“继续”  。 

    ![公司门户“获取 QR 码”屏幕的示例屏幕截图。](./media/get-qr-code-intercede.png)  
17. 点击“使用相机”   > “确定”  。  

    ![请求获得相机访问权限的公司门户提示的示例屏幕截图。](./media/allow-cp-camera-access-intercede.png)  
18. 扫描支持智能卡的设备上的 QR 码图像。  
19. 输入出现在 QR 码下的数字密码。  

    ![公司门户“需要密码”屏幕的输入密码字段的示例屏幕截图。](./media/enter-password-derived-credentials.png)   

20. 等待公司门户完成设备设置。  


## <a name="next-steps"></a>后续步骤  
注册完成后，你将可以访问工作资源，如电子邮件、Wi-Fi 和你的组织提供的任何应用。 有关如何在公司门户中获取、搜索、安装和卸载应用的详细信息，请参阅：

* [通过公司门户网站管理应用](manage-apps-cpweb.md)  
* [在设备上使用托管应用](use-managed-apps-on-your-device-ios.md)  

仍需帮助？ 请与公司支持人员联系。 有关联系信息，请查看[公司门户网站](https://go.microsoft.com/fwlink/?linkid=2010980)。  
