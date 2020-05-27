---
title: 配置自定义域名
titleSuffix: Microsoft Intune
description: 向你的 Microsoft Intune 订阅添加自定义域名
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 06/26/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 2382f36f-13d8-4a32-81ad-6cfa604889c3
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 572519d8ddf3558f1573f26b84fd6217108a24b3
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988010"
---
# <a name="configure-a-custom-domain-name"></a>配置自定义域名

本主题指导管理员如何使用 Microsoft Intune 创建 DNS CNAME 以简化和自定义其登录体验。

组织注册 Microsoft 基于云的服务（如 Intune）时，你将获得一个 Azure Active Directory (AD) 中托管的初始域名，其形式如下所示：your-domain.onmicrosoft.com  。 在此示例中，your-domain 是你在注册时选择的域名  。 onmicrosoft.com 是分配给订阅中所添加帐户的后缀  。 可通过为组织配置自定义域来访问 Intune，而不是使用订阅提供的域名。

在创建用户帐户或同步本地 Active Directory 之前，我们强烈建议你决定是仅使用 .onmicrosoft.com 域还是添加一个或多个自定义域名。 要简化用户管理，请在添加用户前先设置自定义域。 通过设置客户域，用户就能使用访问其他域资源所用的凭据进行登录。

在向 Microsoft 订阅基于云的服务时，该服务的实例将成为为你基于的云服务提供身份和目录服务的 Microsoft [Azure AD 租户](https://technet.microsoft.com/library/jj573650.aspx#BKMK_WhatIsAnAzureADTenant)。 由于将 Intune 配置为使用组织自定义域名的任务对于其他 Azure AD 租户都相同，因此你可以使用[添加你的域](https://azure.microsoft.com/documentation/articles/active-directory-add-domain/)中的信息和过程。

> [!TIP]
> 若要深入了解自定义域，请参阅 [Azure Active Directory 中自定义域名的概念性概述](https://azure.microsoft.com/documentation/articles/active-directory-add-domain-concepts/)。

无法重命名或删除初始 onmicrosoft.com 域名。 可以添加、验证或删除用于 Intune 的自定义域名，以保证业务标识清晰。

## <a name="to-add-and-verify-your-custom-domain"></a>添加和验证自定义域

1. 转到 [Microsoft 365 管理中心](https://admin.microsoft.com/)并登录到管理员帐户。

2. 在导航窗格中，选择“设置”&gt;“域”   。

3. 选择“添加域”  ，然后键入你的自定义域名。 选择“下一步”  。
   ![Microsoft 365 管理中心屏幕截图，其中已选择“设置”>“域”，且正在添加新域名](./media/custom-domain-name-configure/domain-custom-add.png)
4. “验证域”  对话框将打开，为你提供用于在 DNS 托管提供者中创建 TXT 记录的值。
    - **GoDaddy 用户**：Microsoft 365 管理中心将你重定向到 GoDaddy 的登录页。 输入你的凭据并接受域更改权限协议后，自动创建 TXT 记录。 你还可以[创建 TXT 记录](https://support.office.com/article/Create-DNS-records-at-GoDaddy-for-Office-365-f40a9185-b6d5-4a80-bb31-aa3bb0cab48a)。
    - **Register.com 用户**：按照[分步说明](https://support.office.com/article/Create-DNS-records-at-Register-com-for-Office-365-55bd8c38-3316-48ae-a368-4959b2c1684e#BKMK_verify)创建 TXT 记录。
5. [可能需要为 Intune 注册创建其他 DNS 记录](../enrollment/windows-enroll.md#simplify-windows-enrollment-without-azure-ad-premium)。

也可在 [Azure Active Directory 中执行](https://azure.microsoft.com/documentation/articles/active-directory-add-domain/)添加和验证自定义域的步骤。

可了解更多[关于 Office 365 中的初始 onmicrosoft.com 域](https://support.office.com/article/About-your-initial-onmicrosoft-com-domain-in-Office-365-B9FC3018-8844-43F3-8DB1-1B3A8E9CFD5A)的信息

可了解更多关于如何通过创建将注册重定向到 Intune 服务器的 DNS CNAME 来[简化 Windows 注册（不使用 Azure AD Premium）](../enrollment/windows-enroll.md#simplify-windows-enrollment-without-azure-ad-premium)的信息。
