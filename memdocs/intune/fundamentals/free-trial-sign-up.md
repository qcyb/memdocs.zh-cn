---
title: 快速入门 - 免费试用 Microsoft Intune
titleSuffix: ''
description: 在本快速入门中，将创建免费试用版订阅、了解支持的配置和网络要求，并能根据需要配置自己的域名。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/13/2020
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 195931c0-8208-43bd-b0af-b1f8e469a32c
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 778937ed360a2271c342c55bdd03e33ddb5bdb25
ms.sourcegitcommit: 1aeb4a11e89f68e8081d76ab013aef6b291c73c1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2020
ms.locfileid: "88217564"
---
# <a name="quickstart-try-microsoft-intune-for-free"></a>快速入门：免费试用 Microsoft Intune

Microsoft Intune 可帮助你通过管理设备和应用保护员工的企业数据。 在本快速入门中，将创建免费版订阅以在测试环境中试用 Intune。

Intune 通过 Microsoft 终结点管理器管理中心管理的基于云的安全服务提供移动设备管理 (MDM) 和移动应用管理 (MAM)。 使用 Intune，可以确保正确配置、访问和更新员工的企业资源（数据、设备和应用），从而满足公司的符合性策略和要求。

## <a name="prerequisites"></a>必备条件
在设置 Microsoft Intune 之前，请查看以下要求：

- [支持的操作系统和浏览器](supported-devices-browsers.md)
- [网络配置要求和带宽](network-bandwidth-use.md)

## <a name="sign-up-for-a-microsoft-intune-free-trial"></a>注册 Microsoft Intune 免费试用版

可以免费试用 Intune 30 天。 如果已有工作或学校帐户，请使用该帐户进行“登录”，并将 Intune 添加到订阅中  。 否则，也可通过“注册”创建新帐户，以便为组织使用 Intune  。

> [!IMPORTANT]
> 注册新帐户后，不能合并现有的工作或学校帐户。

1. 转到 [Microsoft Intune 试用版](https://go.microsoft.com/fwlink/?linkid=2019088)页面并填写表格。

    ![Microsoft Intune 试用版帐户注册网页的屏幕截图](./media/free-trial-sign-up/account-sign-up-site-full-browser.png)

    如果大多数 IT 操作和用户都不位于你所在的区域，则可能需要在“国家或地区”下选择该区域设置  。 Azure 使用你的区域信息来提供正确的服务。 此设置以后无法更改。

2. 用公司名称加上“.onmicrosoft.com”来创建自己的帐户  。 

    ![Intune 试用版帐户新凭据进程的屏幕截图](./media/free-trial-sign-up/account-sign-up-site-user-id.png)

    如果想使用组织自己的自定义域名，但不使用“.onmicrosoft.com”，则可以在本文后面介绍的 Microsoft 365 管理中心进行更改  。

3. 在注册过程结束时查看新帐户信息。

    ![帐户信息的图像](./media/free-trial-sign-up/intune-end-of-sign-up-process.png) 

## <a name="sign-in-to-intune-in-the-microsoft-endpoint-manager"></a>在 Microsoft 终结点管理器中登录到 Intune

如果尚未登录到门户，请完成以下步骤：

1. 打开新的浏览器窗口，在地址栏中输入 https://endpoint.microsoft.com。 
2. 使用上述步骤中提供的用户 ID 登录 (yourID@yourdomain.onmicrosoft.com)。

    ![门户登录页的图像](./media/free-trial-sign-up/azure-portal-signin.png)

注册试用版时，还将收到一份电子邮件消息，其中包含你在注册过程中提供的帐户信息和电子邮件地址。 该电子邮件用于确认试用版处于活动状态。

> [!TIP]
> 使用 Microsoft 终结点管理器时，在常规模式而不是隐私模式下使用浏览器，可能会获得更好的效果。

## <a name="confirm-the-mdm-authority-in-intune"></a>在 Intune 中确认 MDM 机构

默认情况下，当你创建免费试用版时，将设置 MDM 机构。 可以通过以下步骤确认是否已设置 MDM 机构：

1. 如果尚未登录，请登录到 Microsoft 终结点管理器。
2. 单击“租户管理”  。
3. 查看租户详细信息。 MDM 机构  应设置为“Microsoft Intune”  。

如果登录到 Microsoft 终结点管理器后，看到一个橙色横幅，指示尚未设置 MDM 机构，此时可以激活它。 移动设备管理 (MDM) 机构设置决定了管理设备的方式。 必须先设置 MDM 机构，然后用户才能注册设备来进行管理。

### <a name="to-set-the-mdm-authority-to-intune-follow-these-steps"></a>要将 MDM 机构设置为 Intune，请执行以下步骤：

1. 打开新的浏览器窗口，在地址栏中输入 https://portal.azure.com。 
2. 选择“所有服务” > “Microsoft Intune”。
3. 选择表示尚未启用设备管理的横幅，或者如果没有立即看到横幅，请选择“设备注册”  。 如果尚未启用设备管理，将显示“选择 MDM 机构”边栏选项卡  。

    > [!NOTE]
    > 如果已设置 MDM 机构，“设备注册”边栏选项卡将显示 MDM 机构值  。 如果尚未设置 MDM 机构，则仅显示橙色横幅。 

    ![“选择 MDM 机构”边栏选项卡的图像](./media/free-trial-sign-up/choose-mdm-authority.png) 

4. 如果未设置 MDM 机构，在“选择 MDM 机构”下，将 MDM 机构设置为“Intune MDM 机构”   。

有关 MDM 机构的更多信息，请参阅[设置移动设备管理机构](mdm-authority-set.md)。

## <a name="configure-your-custom-domain-name-optional"></a>配置自定义域名（可选）

如上所述，若想使用组织自己的自定义域名，但不使用“.onmicrosoft.com”，则可以在 Microsoft 365 管理中心进行更改  。 通过以下步骤可以添加、验证和配置你的自定义域名。  

> [!IMPORTANT]
> 无法重命名或删除域名的初始  部分“onmicrosoft.com”  。 但可以添加、验证或删除用于 Intune 的自定义域名，以保证业务标识清晰  。 有关详细信息，请参阅[配置自定义域名](custom-domain-name-configure.md)。

1. 转到 [Microsoft 365 管理中心](https://admin.microsoft.com)并使用管理员帐户登录。

2. 在导航窗格中，选择“设置” > “域” > “添加域”。

3. 输入自定义域名。 然后选择“下一步”  。

   ![Microsoft 365 管理中心的屏幕截图 - 添加域名](./media/free-trial-sign-up/domain-custom-add.png)

4. 验证你是否是上一步中输入的域的所有者。 
    
    若选择“通过电子邮件发送代码”，会将向域中已注册的联系人发送电子邮件  。 收到电子邮件后，请复制该代码，并将其输入标为“在此键入验证码”的字段  。 如果验证码匹配，该域将添加至你的租户。 显示的电子邮件可能看起来不太熟悉。 某些注册机构隐藏了实际的电子邮件地址。 此外，电子邮件地址可能与在注册域名时提供的地址不同。

   ![Microsoft 365 管理中心的屏幕截图 - 验证域名](./media/free-trial-sign-up/domain-custom-verify.png)

   > [!NOTE]
   > 有关 TXT 记录验证的详细信息，请参阅[在 Office 365 的任何 DNS 托管提供商处创建 DNS 记录](https://support.office.com/article/Create-DNS-records-at-any-DNS-hosting-provider-for-Office-365-7B7B075D-79F9-4E37-8A9E-FB60C1D95166)。

## <a name="admin-experiences"></a>管理员体验

两个最常使用的门户：
- Microsoft 终结点管理器管理中心 ([https://endpoint.microsoft.com/](https://endpoint.microsoft.com/)) 可用于浏览 [Intune 功能](what-is-intune.md)。 这是管理员使用 Intune 的位置。
- 如果没有使用 Azure Active Directory 来添加和管理用户，可以在 Microsoft 365 管理中心 ([https://admin.microsoft.com](https://admin.microsoft.com)) 执行此类操作。 还可以管理帐户的帐单和支持等其他方面。

## <a name="next-steps"></a>后续步骤

在本快速入门中，已创建免费版订阅以在测试环境中试用 Intune。 有关设置 Intune 的详细信息，请参阅[设置 Intune](setup-steps.md)。

要完成这一系列的 Intune 快速入门，请继续学习下一篇快速入门。

> [!div class="nextstepaction"]
> [快速入门：创建用户并为其分配许可证](quickstart-create-user.md)
