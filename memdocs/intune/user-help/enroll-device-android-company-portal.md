---
title: 通过 Intune 公司门户注册 Android 设备 | Microsoft Docs
description: 介绍如何通过 Intune 公司门户注册 Android 设备
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/01/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 0ed3a002-7533-4001-ae24-e10b64b66620
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 2ef0cf3909442cec818fd775bef4f848d6be5a83
ms.sourcegitcommit: b90d51f7ce09750e024b97baf6950a87902a727c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86022307"
---
# <a name="enroll-your-device-with-company-portal"></a>通过公司门户注册设备  
注册个人或公司拥有的 Android 设备，以安全访问公司电子邮件、应用和数据。 公司门户支持 Android 设备，包括运行 Android 4.4 及更高版本的 Samsung Knox。  
</br>
> [!VIDEO https://www.youtube.com/embed/k0Q_sGLSx6o?rel=0]

> [!NOTE]
> Samsung Knox 是一种安全解决方案，一些 Samsung 设备用它来提供本机 Android 无法提供的额外保护。 若要检查是否是 Samsung Knox 设备，请依次转到“设置” > “关于设备” 。 如果其中没有列出“Knox 版本”，表明使用的是本机 Android 设备。

## <a name="enroll-device"></a>注册设备  
请务必[从 Google Play](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal) 安装 Intune 公司门户应用。 有关在中华人民共和国提供应用的商店列表，请参阅[在中华人民共和国安装公司门户应用](install-company-portal-android-china.md)。

注册过程中，系统可能会要求你选择最能说明如何使用设备的类别。 公司支持人员使用你的答案来检查可以访问的应用。  

1. 打开公司门户应用并使用工作或学校帐户登录。  

2. 如果系统提示你接受组织的条款和条件，请点击“全部接受”。  

   ![公司门户的示例图像，“条款”屏幕，其中突出显示了“全部接受”按钮。](./media/accept-terms-1911.png)  


3. 查看组织可以看到的内容和看不到的内容。 然后点击“继续”。


    ![公司门户的示例图像，“我们关注你的隐私”屏幕，其中突出显示“继续”按钮。](./media/android-privacy-screen-1911.png)  
4. 查看后续步骤中将执行的操作。 然后点击“下一步”。  

    ![公司门户的示例图像，“后续步骤”屏幕，其中突出显示了“下一步”按钮。](./media/android-whats-next-1911.png)  


5. 由于 Android 版本不同，系统可能会提示你允许访问设备的特定部分。 这些提示是 Google 要求的，不受 Microsoft 控制。  

    点击“允许”以授予下列权限：  
    * **允许公司门户发起和管理电话呼叫**：此权限使你的设备能够与 Intune（组织的设备管理提供商）共享其国际移动工作站设备标识 (IMEI) 号码。 允许此权限是安全的。 Microsoft 绝不会发起或管理电话呼叫。  
    * **允许公司门户访问你的联系人**：此权限允许公司门户应用创建、使用和管理你的工作帐户。  允许此权限是安全的。 Microsoft 绝不会访问你的联系人。 

    如果拒绝权限，则下次登录到公司门户时，系统会再次进行提示。 要关闭这些消息，请选择“不再询问”。 若要管理应用权限，请转到“设置”应用 >“应用” > “公司门户” > “权限” > “手机”   。  

6. 激活设备管理应用。 

    公司门户需要设备管理员权限才能安全地管理设备。 通过激活应用，你的组织可以识别可能存在的安全问题（例如，多次尝试解锁设备失败），然后做出相应的响应。  

    ![“激活设备管理员”屏幕的示例图像，其中突出显示了“激活”按钮。](./media/activate-device-administrator-1911.png)  

> [!NOTE]
> Microsoft 不会控制此屏幕上的消息。 我们了解到，它的措辞似乎有些激烈。 公司门户无法指定与组织相关的限制和访问权限。 如果你对组织使用应用的方式有疑问，请联系你的 IT 支持人员。 请转到[公司门户网站](https://go.microsoft.com/fwlink/?linkid=2010980)，查找组织的联系人信息。  


7. 你的设备将开始注册。 如果你使用的是 Samsung Knox 设备，则系统会提示你先查看并确认 ELM Agent 隐私策略。   

    ![注册过程中的“Samsung Knox 隐私策略”屏幕的示例图像。](./media/and-enroll-7-knox-privacy-policy.png)  

8. 在“公司访问设置”屏幕上，检查你的设备是否已注册。 然后点击“继续”。  

    ![公司门户的示例图像，“公司访问设置”屏幕，其中显示已完成设备托管。](./media/update-settings-1911.png)  

9. 组织可能会要求你更新设备设置。 点击“解决”以调整设置。 更新设置完成后，请点击“继续”。  

   ![公司门户的示例图像，“更新设备设置”屏幕，其中突出显示了“解决并继续”按钮。](./media/resolve-settings-1911.png)  

10. 设置完成后，点击“完成”。    

    ![公司门户的示例图像，“公司访问设置”屏幕，其中显示设置已完成并突出显示“完成”按钮。](./media/android-enrollment-done-1911.png) 

## <a name="next-steps"></a>后续步骤  

你需转到“设置” > “安全性”，然后打开“未知源”才能尝试安装学校或工作应用  。 如果在尝试安装应用时未打开此选项，则会看到以下消息：“安装已阻止。 出于安全性考虑，你的设置已被设置为阻止安装未知来源的应用。” 可以点击消息上的“设置”，直接转到“未知源” 。  

> [!Note]
> 如果组织使用的是电信费用管理软件，则还需要完成其他几个步骤才能完全注册设备。 请单击[此处](enroll-your-device-with-telecom-expense-management-android.md)，查看详细信息。

如果尝试在 Intune 中注册设备时遇到错误，则可以[向公司支持人员发送电子邮件](send-logs-to-your-it-admin-by-email-android.md)。  

仍需帮助？ 请与公司支持人员联系。 有关联系信息，请查看[公司门户网站](https://go.microsoft.com/fwlink/?linkid=2010980)。  