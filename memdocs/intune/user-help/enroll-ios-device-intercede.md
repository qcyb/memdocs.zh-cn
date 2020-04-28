---
title: 通过 Intune 公司门户和 Intercede 注册 iOS 或 iPadOS 设备
description: 了解如何注册 iOS 或 iPadOS 设备，以及如何使用 Intercede 设置派生凭据身份验证。
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
ms.openlocfilehash: b83092521f1ab0058d47d599e7fd9c10c2fd6d35
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "82077761"
---
# <a name="set-up-ios-or-ipados-device-with-company-portal-and-intercede"></a>通过公司门户和 Intercede 设置 iOS 或 iPadOS 设备

通过 Intune 公司门户应用注册设备，以获取对组织的电子邮件、文件和应用的安全移动访问权限。  注册设备后，它将成为托管设备  。 组织可通过移动设备管理 (MDM) 提供程序（如 Intune）为该设备分配策略和应用。  

在注册期间，还需在设备上安装派生凭据。 你的组织可能要求你在访问资源时使用派生凭据作为身份验证方法，或对电子邮件进行签名和加密。 

如果使用智能卡执行以下操作，则可能需要设置派生凭据：

* 登录到学校或工作应用、Wi-Fi 和虚拟专用网络 (VPN)
* 使用 S/MIME 证书对学校或工作电子邮件进行签名和加密  

在本文中，你将：  

* 通过 Intune 公司门户注册 iOS 或 iPadOS 移动设备。  
* 从组织的派生凭据提供程序 [Intercede](https://www.intercede.com/) 获取派生凭据。   


## <a name="what-are-derived-credentials"></a>什么是派生凭据？  
派生凭据是一种派生自智能卡凭据并在设备上安装的证书。 它授予你对工作资源的远程访问权限，同时防止未经授权的用户访问敏感信息。  

派生凭据用于： 
* 对登录到学校或工作应用、Wi-Fi 和 VPN 的学生和员工进行身份验证
* 使用 S/MIME 证书对学校或工作电子邮件进行签名和加密  

派生凭据实现美国国家标准与技术研究院 (NIST) 关于派生个人身份验证 (PIV) 凭据的准则（属于《特殊出版物 (SP) 800-157》）。  

## <a name="prerequisites"></a>必备条件

 若要完成注册，你必须具有：

* 你的学校或工作提供的智能卡
* 可使用智能卡登录的计算机或自助服务网亭的访问权限
* 你的移动设备
* 设备上安装的适用于 iOS 和 iPadOS 的 Intune 公司门户应用


## <a name="enroll-device"></a>注册设备  
1. 打开移动设备上适用于 iOS/iPadOS 的公司门户应用，并使用你的工作帐户登录。  
2. 记下屏幕上出现的代码。  

    ![带有屏幕消息和代码的公司门户应用的示例图像。](./media/copy-code-intercede.png)  
1. 切换到已启用智能卡的设备，然后转到 https://microsoft.com/devicelogin 。 

1. 输入先前记下的代码。
 
2. 插入智能卡进行登录。   

3. 返回到移动设备上的公司门户应用，然后按照屏幕上的说明注册设备。  
4. 注册完成后，公司门户会通知你设置智能卡。 点击通知。 如果没有收到通知，请检查你的电子邮件。   

    ![设备主屏幕上的公司门户推送通知的示例屏幕截图。](./media/action-required-in-app-intercede.png)  

5. “设置移动智能卡访问权限”屏幕  ：  
    a. 点击指向组织设置说明的链接。 如果你的组织未提供其他说明，你将参阅本文。  
    b. 点击“开始”  。  

    ![公司门户的示例屏幕截图，“设置移动智能卡访问权限”屏幕。](./media/smart-card-info-intercede.png)  

6. 切换到支持智能卡的设备或自助服务网亭，并打开 MyID 应用。 使用工作凭据登录。  
7. 选择用于请求 ID 的选项。 
8. 当系统询问要使用的配置文件时，请选择用于通过移动凭据进行激活的选项。 将显示 QR 码。  
9. 返回到你的移动设备。 在“公司门户”>“获取 QR 码”  屏幕上，点击“继续”  。  

    ![公司门户“获取 QR 码”屏幕的示例屏幕截图。](./media/get-qr-code-intercede.png) 
 
10. 点击“使用相机”   > “确定”  。  

    ![请求获得相机访问权限的公司门户提示的示例屏幕截图。](./media/allow-cp-camera-access-intercede.png)  

11. 扫描支持智能卡的设备上的 QR 码图像。 
12. 等待公司门户完成设备设置。  

## <a name="next-steps"></a>后续步骤  
注册完成后，你将可以访问工作资源，如电子邮件、Wi-Fi 和你的组织提供的任何应用。 有关如何在公司门户中获取、搜索、安装和卸载应用的详细信息，请参阅：

* [通过公司门户网站管理应用](manage-apps-cpweb.md)  
* [在设备上使用托管应用](use-managed-apps-on-your-device-ios.md)  

仍需帮助？ 请与公司支持人员联系。 有关联系信息，请查看[公司门户网站](https://go.microsoft.com/fwlink/?linkid=2010980)。
