---
title: 通过 Microsoft Intune 应用和 DISA Purebred 注册 Android 设备
description: 了解如何注册 Android 设备，以及如何使用 DISA Purebred 设置派生凭据身份验证。
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/15/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: jeyang
ms.suite: ems
ms.custom: intune-enduser
ms.collection: M365-identity-device-management
ms.openlocfilehash: 584392891320f96eed16863225ffb323dc240594
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/27/2020
ms.locfileid: "83880624"
---
# <a name="set-up-android-device-with-the-microsoft-intune-app-and-disa-purebred"></a>使用 Microsoft Intune 应用和 DISA Purebred 设置 Android 设备

通过 Microsoft Intune 应用注册设备，从而在移动设备上安全地访问组织的电子邮件、文件和应用。 注册设备后，它将成为托管设备。 组织可通过移动设备管理 (MDM) 提供程序（如 Intune）为该设备分配策略和应用。  

在注册期间，还需在设备上安装派生凭据。 你的组织可能要求你在访问资源时使用派生凭据作为身份验证方法，或对电子邮件进行签名和加密。

如果使用智能卡执行以下操作，则可能需要设置派生凭据：

* 登录到学校或工作应用、Wi-Fi 和虚拟专用网络 (VPN)
* 使用 S/MIME 证书对学校或工作电子邮件进行签名和加密

在本文中，你将：

* 通过 Intune 应用注册 Android 移动设备
* 通过安装来自组织的派生凭据提供程序 [DISA Purebred](https://public.cyber.mil/pki-pke/purebred/) 的派生凭据来设置智能卡

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
* 已在设备上安装 Purebred 应用（应用应在设备设置后立即自动安装。 如果没有自动安装，请与 IT 支持人员联系。）

你还需要在安装过程中联系 Purebred 代理或代表。

## <a name="enroll-device"></a>注册设备  

1. 打开新的或恢复出厂设置设备。  
2. 在“欢迎使用”屏幕上，选择语言。 如果系统指示使用 QR 码或 NFC 注册，请按照与该方法匹配的以下步骤操作。  
     * NFC：针对程序员设备点击 NFC 支持的设备，以连接到组织的网络。 按照屏幕上的提示操作。 访问 Chrome 的服务条款屏幕时，请继续执行步骤 5。  

     * QR 码：完成 [QR 码注册](#qr-code-enrollment)中的步骤。  

     如果系统指示使用其他方法，请继续执行步骤 3。    

3. 连接 Wi-Fi，然后点击“下一步”。 按照与注册方法匹配的步骤操作。 

    * 令牌：转到 Google 登录屏幕后，完成[令牌注册](#token-enrollment)中的步骤。  
    * Google Zero Touch：连接到 Wi-Fi 后，组织会识别你的设备。 继续执行步骤 4 并按照屏幕上的提示进行操作，直到设置完成。    
 
       ![Google 条款屏幕的示例图像，如果使用的是 Google Zero Touch，其中会突出显示“接受并继续”按钮。](./media/google-zero-touch-intune-app-01.png)   
   
4. 查看 Google 的条款。 然后点击“接受并继续”。  

      ![Google 条款屏幕的示例图像，其中突出显示“接受并继续”按钮。](./media/fully-managed-intune-app-04.png)   

5. 查看 Chrome 的服务条款。 然后点击“接受并继续”。  

   ![Chrome 服务条款屏幕的示例图像，其中突出显示“接受并继续”按钮。](./media/fully-managed-intune-app-06.png)   

6. 在登录屏幕上，依次点击“登录选项”和“从其他设备登录” 。 

7. 记下屏幕代码。  

8. 切换到支持智能卡的设备，并转到屏幕上显示的网址。 

9. 输入先前记下的代码。

   > [!div class="mx-imgBorder"]
   > ![公司门户网站上“输入代码”提示的屏幕截图。](./media/enter-code-intercede.png)

10. 插入智能卡进行登录。 

11. 在登录屏幕上，选择工作或学校帐户。 然后切换回移动设备。 

12. 根据组织的要求，系统可能会提示更新设置（如锁屏或加密）。 如果看到这些提示，请点击“设置”并按照屏幕上的说明进行操作。  

       ![“设置工作电话”屏幕的示例图像，其中突出显示“设置”按钮。](./media/fully-managed-intune-app-10.png)   

13. 若要在设备上安装工作应用，请点击“安装”。 安装完成后，点击“下一步”。  

       ![“设置工作电话”屏幕的示例图像，其中突出显示“安装”按钮。](./media/fully-managed-intune-app-11.png)   

14. 点击“启动”，打开 Microsoft Intune 应用。 

    ![“设置工作电话”屏幕的示例图像，其中突出显示了“开始”按钮。](./media/fully-managed-intune-app-17.png)   

15. 返回到移动设备上的 Intune 应用，然后按照屏幕上的说明进行操作，直到注册完成。 

    ![设置访问权限、注册设备屏幕的示例图像，其中突出显示“完成”按钮。](./media/fully-managed-intune-app-19.png)   

16. 继续到本文中的[设置智能卡](enroll-android-device-disa-purebred.md#set-up-smart-card)部分，完成设备设置。  

### <a name="qr-code-enrollment"></a>QR 码设备注册  
在本节中，将扫描公司提供的 QR 码。  完成后，你将重定向回设备注册步骤。     
  
1. 在“欢迎”屏幕上，点击屏幕五次，才能启动 QR 码安装。  

   ![设备安装“欢迎”屏幕的示例图像，其中突出显示点击屏幕的说明。](./media/qr-code-intune-app-01.png)  

2. 按照屏幕上的任何说明连接到 Wi-Fi。  
3. 如果设备没有安装 QR 码扫描仪，安装屏幕将显示安装扫描仪时的进程。 等待安装完成。  
4. 系统出现提示时，扫描组织提供的注册配置文件 QR 码。  
5. 返回步骤 4 [注册设备](#enroll-device)，继续执行安装。  

### <a name="token-enrollment"></a>令牌注册  
在本节中，输入公司提供的令牌。 完成后，你将重定向回设备注册步骤。  

1. 在 Google 登录屏幕上，在“电子邮件或电话”框中，键入“afw#setup” 。 点击“下一步”。 

   ![“Google 登录”屏幕的示例图像，其中显示键入到字段中的“afw#setup”。](./media/token-intune-app-01.png)   

2. 为“Android 设备策略”应用选择“安装” 。 继续完成安装。 可能需要查看并接受其他条款，具体取决于你的设备。    

3. 在“注册此设备”屏幕上，选择“下一步” 。  

4. 选择“输入条形码”。  

5. 在“扫描或输入条形码”屏幕上，键入组织提供的条形码。  然后单击 **“下一步”** 。  

   ![“扫描或输入条形码”屏幕的示例图像，其中突出显示“下一步”按钮。](./media/token-intune-app-04.png)  

6. 返回步骤 4 [注册设备](#enroll-device)，继续执行安装。


## <a name="set-up-smart-card"></a>设置智能卡  

> [!NOTE]
> 需要使用 Purebred 应用才能完成这些步骤，该应用将在注册后自动安装在设备上。 若在等待一段时间后仍未安装应用，请联系 IT 支持人员。  

1. 注册完成后，Intune 应用会通知你设置智能卡。 点击通知。 如果没有收到通知，请检查你的电子邮件。

   > [!div class="mx-imgBorder"]
   > ![设备主屏幕上的 Intune 应用推送通知的屏幕截图。](./media/action-required-in-app-android.png)

2. 在“设置智能卡”屏幕上：

   1. 点击指向组织设置说明的链接并查看这些内容。 如果你的组织未提供其他说明，你将参阅本文。

   2. 点击“开始”。   

   > [!div class="mx-imgBorder"]
   > ![Intune 应用中“设置智能卡”屏幕的屏幕截图。](./media/smart-card-open-disa-purebred-android.png)

3. 在“获取证书”屏幕上，点击“启动 Purebred”以打开 Purebred 应用 。 （该应用应自动安装在你的设备上。 若设备上没有该应用，请与支持人员联系。）  

   > [!div class="mx-imgBorder"]
   > ![Intune 应用提示打开 DISA Purebred 应用的屏幕截图。](./media/open-app-prompt-disa-purbred-android.png)  

4. Purebred 应用可能需要你授予其他权限才能正常运行。 在出现提示时，请点击“允许”或“始终允许” 。 要详细了解为什么需要这些权限，请咨询支持人员或 Purebred 代理。  

5. 进入 Purebred 应用后，请与组织的 Purebred 代理合作下载并安装访问工作或学校资源所需的证书。

    > [!IMPORTANT]
    > 在此过程中，若出现提示，请点击“确定”或“安装” 。 请勿更改系统提示安装的任何证书颁发机构 (CA) 或证书的名称。    

6. 安装完成后，你将收到一条通知，其中指出证书已准备就绪。 点击通知以返回 Intune 应用。

    > [!div class="mx-imgBorder"]
    > ![“允许访问证书”屏幕的屏幕截图](./media/certificates-ready-prompt-disa-purbred-android.png)

7. 在“允许访问证书”屏幕中，你将授予 Intune 应用访问从 DISA Purebred 获取的派生凭据的权限。 此步骤确保组织能在你访问受保护的工作或学校资源时验证你的身份。  

    1. 点击“下一步”。

       > [!div class="mx-imgBorder"]
       > ![“证书已准备就绪”提示的屏幕截图](./media/certificates-access-disa-purbred-android.png)

    2. 当系统提示你“选择证书”时，请勿更改已选择的选项。 系统已选择正确的证书，因此只需点击“选择”或“确定”即可 。  

       > [!div class="mx-imgBorder"]
       > ![“选择证书”提示的屏幕截图](./media/choose-certificates-prompt-disa-purbred-android.png)

    3. 你的派生凭据由多个证书组成，因此可能会出现多次“选择证书”提示。 请重复上述步骤，直到不再出现提示。  

8. 处理所有证书后，请等待 Intune 应用完成设备的设置。 看到“设置完成!”屏幕时， 即表示设置已完成。  

    > [!div class="mx-imgBorder"]
    > ![“设置完成”屏幕的屏幕截图](./media/all-set-android.png)

## <a name="next-steps"></a>后续步骤

注册完成后，你将可以访问工作资源，如电子邮件、Wi-Fi 和你的组织提供的任何应用。 要详细了解如何在 Intune 应用中获取、搜索、安装和卸载应用，请参阅：

* [在设备上使用托管应用](use-managed-apps-on-your-device-android.md)  
* [通过公司门户网站管理应用](manage-apps-cpweb.md)  


仍需帮助？ 请与公司支持人员联系。 有关联系信息，请查看[公司门户网站](https://go.microsoft.com/fwlink/?linkid=2010980)。
