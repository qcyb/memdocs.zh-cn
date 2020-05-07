---
title: 通过 Intune 公司门户和 DISA Purebred 注册 iOS 或 iPadOS 设备
description: 了解如何注册 iOS 或 iPadOS 设备，以及如何使用 DISA Purebred 设置派生凭据身份验证。
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
ms.openlocfilehash: 268ed874be65c9ade7f801b89528d1a23f176ee1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "82077795"
---
# <a name="set-up-ios-or-ipados-device-with-company-portal-and-disa-purebred"></a>通过公司门户和 DISA Purebred 设置 iOS 或 iPadOS 设备  

通过 Intune 公司门户应用注册设备，以获取对组织的电子邮件、文件和应用的安全移动访问权限。 注册设备后，它将成为托管设备  。 组织可通过移动设备管理 (MDM) 提供程序（如 Intune）为该设备分配策略和应用。  

在注册期间，还需在设备上安装派生凭据。 你的组织可能要求你在访问资源时使用派生凭据作为身份验证方法，或对电子邮件进行签名和加密。 

如果使用智能卡执行以下操作，则可能需要设置派生凭据：

* 登录到学校或工作应用、Wi-Fi 和虚拟专用网络 (VPN)
* 使用 S/MIME 证书对学校或工作电子邮件进行签名和加密  

在本文中，你将：  

   * 通过 Intune 公司门户注册 iOS 或 iPadOS 移动设备。  
   * 从组织的派生凭据提供程序 DISA Purebred (https:\//cyber.mil/pki-pke/purebred/) 获取派生凭据。  

## <a name="what-are-derived-credentials"></a>什么是派生凭据？  
派生凭据是一种派生自智能卡凭据并在设备上安装的证书。 它授予你对工作资源的远程访问权限，同时防止未经授权的用户访问敏感信息。  

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

你还需要在安装过程中联系 Purebred 代理或代表。      

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
    b. 单击“打开”以打开 Purebred 应用  。  

    ![公司门户的示例屏幕截图，“设置移动智能卡访问权限”屏幕。](./media/smart-card-open-disa-purebred.png)  
9. 当系统提示你允许公司门户打开“Purebred 注册”应用时，选择“打开”  。   

    ![公司门户提示打开 DISA Purebred 应用的示例屏幕截图。](./media/open-app-prompt-disa-purbred.png)  
10. 当应用运行时，请与组织的 Purebred 代理合作，以配置和下载 Purebred 预注册配置文件。   
11. 请转到“设置”应用 >“常规” > “配置文件与设备管理” > “安装配置文件”，然后点击“安装”     。  
12. 输入设备密码。  
13. 安装配置文件。 你可能需要多次点击“安装”才能开始安装  。 
14. 返回到“Purebred 注册”应用。 请按照 Purebred 代理的说明继续操作。  
 
15. 下载配置文件后，请转到“设置”应用 >“常规” > “配置文件与设备管理” > “安装配置文件”，然后点击“安装”     。   
16.  输入设备密码。
17. 安装配置文件。 你可能需要多次点击“安装”才能开始安装  。 
18. 安装完成后，返回到公司门户应用。  
19.  在“设置移动智能卡访问权限”屏幕上，点击“继续”   。  

20. 从“导入证书”  屏幕中，检索和导入从 DISA Purebred 获取的派生凭据。  

    a. 点击“继续”  。   

    ![公司门户“设置导入证书”屏幕的示例屏幕截图。](./media/import-certificate-disa-purebred.png)  
    b. 转到 iCloud Drive“浏览” > “位置”，然后点击“更多位置”    。  

    ![iCloud Drive 的示例屏幕截图，“浏览”菜单中突出显示了“更多位置”选项。](./media/icloud-drive-more-locations.png)  
    c. 点击开关以启用“Purebred 密钥链”  。  

    ![iCloud Drive 的示例屏幕截图，“浏览”视图，突出显示 Purebred 密钥链开关已启用。](./media/icloud-drive-enable-purebred-keychain.png)   

    d. 点击“Purebred 凭据包”  。  

    ![iOS 屏幕的示例屏幕截图，其中包含可选的“Purebred 凭据包”选项。](./media/purebred-credential-package.png)  
    f. 显示证书列表。 选择一个，然后点击“导入密钥”  。  

    ![可选择证书列表的示例屏幕截图，其中一项已被选中。](./media/import-purebred-keychain.png) 
21. 返回公司门户应用并等待公司门户完成设备设置。   

## <a name="next-steps"></a>后续步骤  
注册完成后，你将可以访问工作资源，如电子邮件、Wi-Fi 和你的组织提供的任何应用。 有关如何在公司门户中获取、搜索、安装和卸载应用的详细信息，请参阅：

* [通过公司门户网站管理应用](manage-apps-cpweb.md)  
* [在设备上使用托管应用](use-managed-apps-on-your-device-ios.md)  

仍需帮助？ 请与公司支持人员联系。 有关联系信息，请查看[公司门户网站](https://go.microsoft.com/fwlink/?linkid=2010980)。
