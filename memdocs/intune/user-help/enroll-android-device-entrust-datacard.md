---
title: 通过 Microsoft Intune 应用和 Entrust Datacard 注册 Android 设备
description: 通过 Entrust Datacard 注册 Android 设备，并设置派生凭据身份验证。
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/17/2020
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: jeyang
ms.suite: ems
ms.custom: intune-enduser
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5bff61c63e9845dc6d90333fb99534235e388db6
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81616094"
---
# <a name="set-up-android-device-with-company-portal-and-entrust-datacard"></a>通过公司门户和 Entrust Datacard 设置 Android 设备

通过 Microsoft Intune 应用注册设备，从而在移动设备上安全地访问组织的电子邮件、文件和应用。 注册设备后，它将成为托管设备  。 组织可通过移动设备管理 (MDM) 提供程序（如 Intune）为该设备分配策略和应用。

在注册期间，还需在设备上安装派生凭据。 你的组织可能要求你在访问资源时使用派生凭据作为身份验证方法，或对电子邮件进行签名和加密。

如果使用智能卡执行以下操作，则可能需要设置派生凭据：

* 登录到学校或工作应用、Wi-Fi 和虚拟专用网络 (VPN)
* 使用 S/MIME 证书对学校或工作电子邮件进行签名和加密

在本文中，你将：

* 通过 Intune 应用注册 Android 移动设备
* 通过安装来自组织派生凭据提供程序 [Entrust Datacard](https://www.entrustdatacard.com/) 的派生凭据来设置智能卡

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
* 运行 Android 7.0 或更高版本的新设备或已出厂重置的设备
* 设备上安装的 Microsoft Intune 应用

## <a name="enroll-device"></a>注册设备  

1. 打开新的或恢复出厂设置设备。  
2. 在“欢迎使用”屏幕上，选择语言  。 如果系统指示使用 QR 码或 NFC 注册，请按照与该方法匹配的以下步骤操作。  
     * NFC：针对程序员设备点击 NFC 支持的设备，以连接到组织的网络。 按照屏幕上的提示操作。 访问 Chrome 的服务条款屏幕时，请继续执行步骤 5。  

     * QR 码：完成 [QR 码注册](#qr-code-enrollment)中的步骤。  

     如果系统指示使用其他方法，请继续执行步骤 3。    

3. 连接 Wi-Fi，然后点击“下一步”  。 按照与注册方法匹配的步骤操作。 

    * 令牌：转到 Google 登录屏幕后，完成[令牌注册](#token-enrollment)中的步骤。  
    * Google Zero Touch：连接到 Wi-Fi 后，组织会识别你的设备。 继续执行步骤 4 并按照屏幕上的提示进行操作，直到设置完成。    
 
       ![Google 条款屏幕的示例图像，如果使用的是 Google Zero Touch，其中会突出显示“接受并继续”按钮。](./media/google-zero-touch-intune-app-01.png)   
   
4. 查看 Google 的条款。 然后点击“接受并继续”  。  

      ![Google 条款屏幕的示例图像，其中突出显示“接受并继续”按钮。](./media/fully-managed-intune-app-04.png)   

5. 查看 Chrome 的服务条款。 然后点击“接受并继续”  。  

   ![Chrome 服务条款屏幕的示例图像，其中突出显示“接受并继续”按钮。](./media/fully-managed-intune-app-06.png)   

6. 在登录屏幕上，依次点击“登录选项”和“从其他设备登录”   。 

7. 记下屏幕代码。  

8. 切换到支持智能卡的设备，并转到屏幕上显示的网址。 

9. 输入先前记下的代码。

   > [!div class="mx-imgBorder"]
   > ![公司门户网站上“输入代码”提示的屏幕截图。](./media/enter-code-intercede.png)

10. 插入智能卡进行登录。  

11. 在登录屏幕上，选择工作或学校帐户。 然后切换回移动设备。 

12. 根据组织的要求，系统可能会提示更新设置（如锁屏或加密）。 如果看到这些提示，请点击“设置”并按照屏幕上的说明进行操作  。  

       ![“设置工作电话”屏幕的示例图像，其中突出显示“设置”按钮。](./media/fully-managed-intune-app-10.png)   

13. 若要在设备上安装工作应用，请点击“安装”  。 安装完成后，点击“下一步”  。  

       ![“设置工作电话”屏幕的示例图像，其中突出显示“安装”按钮。](./media/fully-managed-intune-app-11.png)    

14. 点击“启动”，打开 Microsoft Intune 应用  。 

    ![“设置工作电话”屏幕的示例图像，其中突出显示了“开始”按钮。](./media/fully-managed-intune-app-17.png)   
 
15. 返回到移动设备上的 Intune 应用，然后按照屏幕上的说明进行操作，直到注册完成。 

    ![设置访问权限、注册设备屏幕的示例图像，其中突出显示“完成”按钮。](./media/fully-managed-intune-app-19.png)   

16. 继续到本文中的[设置智能卡](enroll-android-device-entrust-datacard.md#set-up-smart-card)部分，完成设备设置。  

### <a name="qr-code-enrollment"></a>QR 码设备注册  
在本节中，将扫描公司提供的 QR 码。  完成后，你将重定向回设备注册步骤。     
  
1. 在“欢迎”屏幕上，点击屏幕五次，才能启动 QR 码安装  。  

   ![设备安装“欢迎”屏幕的示例图像，其中突出显示点击屏幕的说明。](./media/qr-code-intune-app-01.png)  

2. 按照屏幕上的任何说明连接到 Wi-Fi。  
3. 如果设备没有安装 QR 码扫描仪，安装屏幕将显示安装扫描仪时的进程。 等待安装完成。  
4. 系统出现提示时，扫描组织提供的注册配置文件 QR 码。  
5. 返回步骤 4 [注册设备](#enroll-device)，继续执行安装。  

### <a name="token-enrollment"></a>令牌注册  
在本节中，输入公司提供的令牌。 完成后，你将重定向回设备注册步骤。  

1. 在 Google 登录屏幕上，在“电子邮件或电话”框中，键入“afw#setup”   。 点击“下一步”  。 

   ![“Google 登录”屏幕的示例图像，其中显示键入到字段中的“afw#setup”。](./media/token-intune-app-01.png)   

2. 为“Android 设备策略”应用选择“安装”   。 继续完成安装。 可能需要查看并接受其他条款，具体取决于你的设备。    

3. 在“注册此设备”屏幕上，选择“下一步”   。  

4. 选择“输入条形码”  。  

5. 在“扫描或输入条形码”屏幕上，键入组织提供的条形码  。  然后单击 **“下一步”** 。  

   ![“扫描或输入条形码”屏幕的示例图像，其中突出显示“下一步”按钮。](./media/token-intune-app-04.png)  

6. 返回步骤 4 [注册设备](#enroll-device)，继续执行安装。

## <a name="set-up-smart-card"></a>设置智能卡  

1. 注册完成后，Intune 应用会通知你设置智能卡。 点击通知。 如果没有收到通知，请检查你的电子邮件。

   > [!div class="mx-imgBorder"]
   > ![设备主屏幕上的公司门户推送通知的示例屏幕截图。](./media/action-required-in-app-android.png)

2. 在“设置智能卡”屏幕上  ：

   1. 点击指向组织设置说明的链接。 如果你的组织未提供其他说明，你将参阅本文。

   2. 点击“开始”  。 

   > [!div class="mx-imgBorder"]
   > ![公司门户中“设置移动智能卡访问权限”屏幕的示例屏幕截图。](./media/smart-card-open-entrust-android.png)

3. 切换到已启用智能卡的设备并打开 IdentityGuard。

4. 找到智能凭据登录区域，然后选择登录按钮。

5. 当系统提示你选择证书时，选择你的智能卡凭据。 然后选择“确定”  。

6. 输入智能卡 PIN。

7. 系统会要求你从操作列表中进行选择。 选择使你可以注册派生移动智能凭据的操作。 链接或按钮可能会显示“我要注册派生移动智能卡凭据”。 

8. 选择已成功下载并安装了启用智能凭据的应用程序。 然后继续到下一个屏幕。

9. 输入派生的智能卡凭据的相关信息：

    1. 对于标识名称，请输入任何名称，如 Entrust Derived Cred  。  
    2. 在下拉菜单中，选择“Entrust IdentityGuard 移动智能凭据”  。

    3. 继续到下一个屏幕。 将看到一个 QR 码，下面有一个数字密码。

10. 返回到 Android 设备。 在 Intune 应用 >“获取 QR 码”屏幕上，点击“下一步”   。

    > [!div class="mx-imgBorder"]
    > ![公司门户中“获取 QR 码”屏幕的示例屏幕截图。](./media/get-qr-code-entrust-android.png)

11. 如果系统提示你允许 Intune 应用使用你的相机，请点击“允许”  。

12. 扫描支持智能卡的设备上的 QR 码图像。

13. 在“需要密码”屏幕上，输入 QR 码下显示的密码  。

    > [!div class="mx-imgBorder"]
    > ![公司门户网站中“需要密码”屏幕的示例屏幕截图。](./media/password-required-entrust-android.png)  

14. Intune 应用将开始下载和安装访问工作或学校资源所需的证书。 此过程可能需要一些时间，具体取决于 Internet 连接情况。 请不要在此期间关闭应用。

    > [!div class="mx-imgBorder"]
    > ![公司门户中“下载和安装证书”屏幕的示例屏幕截图](./media/install-certificates-entrust-android.png)

15. 处理所有证书后，请等待 Intune 应用完成设备的设置。 看到“设置完成!”屏幕时，  即表示设置已完成。

    > [!div class="mx-imgBorder"]
    > ![“设置完成”屏幕的示例屏幕截图](./media/all-set-android.png)

## <a name="next-steps"></a>后续步骤

注册完成后，你将可以访问工作资源，如电子邮件、Wi-Fi 和你的组织提供的任何应用。 要详细了解如何在 Intune 应用中获取、搜索、安装和卸载应用，请参阅：

* [在设备上使用托管应用](use-managed-apps-on-your-device-android.md)  
* [通过公司门户网站管理应用](manage-apps-cpweb.md)  

仍需帮助？ 请与公司支持人员联系。 有关联系信息，请查看[公司门户网站](https://go.microsoft.com/fwlink/?linkid=2010980)。