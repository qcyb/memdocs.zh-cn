---
title: 使用 Microsoft Intune 设置 Windows 设备的注册
titleSuffix: ''
description: 设置 Windows 设备的注册。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/22/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: f94dbc2e-a855-487e-af6e-8d08fabe6c3d
ms.reviewer: spshumwa
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9104716c469168a5ab2c5c1b49caf14071150db1
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988908"
---
# <a name="set-up-enrollment-for-windows-devices"></a>设置 Windows 设备的注册

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

本文可帮助 IT 管理员为用户简化 Windows 注册过程。 [设置 Intune](../fundamentals/setup-steps.md) 之后，用户使用其工作或学校帐户进行[登录](https://docs.microsoft.com/mem/intune/user-help/windows-enrollment-company-portal)即可注册 Windows 设备。  

Intune 管理员可通过以下方式简化注册：

- [启用自动注册](#enable-windows-10-automatic-enrollment)（需要 Azure AD Premium）
- [CNAME 注册](#simplify-windows-enrollment-without-azure-ad-premium)
- [启用批量注册](windows-bulk-enroll.md)（需要 Azure AD Premium 和 Windows 配置设计器）

两个因素决定了简化 Windows 设备注册的方式：

- **是否使用 Azure Active Directory Premium？** <br>[Azure AD Premium](https://docs.microsoft.com/azure/active-directory/active-directory-get-started-premium) 随附企业移动性 + 安全性和其他许可计划。
- **用户将注册什么版本的 Windows 客户端？** <br>可通过添加工作或学校帐户自动注册 Windows 10 设备。 早期版本必须使用公司门户应用进行注册。

||**Azure AD Premium**|**其他 AD**|
|----------|---------------|---------------|  
|**Windows 10**|[自动注册](#enable-windows-10-automatic-enrollment) |用户注册|
|**早期 Windows 版本**|用户注册|用户注册|

能够使用自动注册的组织还可通过使用 Windows 配置设计器应用来配置[批量注册设备](windows-bulk-enroll.md)。

## <a name="device-enrollment-prerequisites"></a>设备注册先决条件

在管理员可以向 Intune 注册设备以进行管理之前，应已将许可证分配到管理员的帐户。 [了解如何为设备注册分配许可证](../fundamentals/licenses-assign.md)

## <a name="multi-user-support"></a>多用户支持

Intune 支持满足以下两项的设备上的多个用户：

- 运行 Windows 10 创意者更新
- 已加入 Azure Active Directory 域。

当标准用户使用其 Azure AD 凭据登录时，将接收到分配给其用户名的应用和策略。 只有设备的[主要用户](../remote-actions/find-primary-user.md)才能使用公司门户来实现自助服务方案，例如安装应用和执行设备操作（删除、重置）。 对于未分配主要用户的共享 Windows 10 设备，仍可使用公司门户来安装可用应用。

[!INCLUDE [AAD-enrollment](../includes/win10-automatic-enrollment-aad.md)]

## <a name="simplify-windows-enrollment-without-azure-ad-premium"></a>简化 Windows 注册（不使用 Azure AD Premium）
为简化注册，可创建将注册请求重定向到 Intune 服务器的域名服务器 (DNS) 别名（CNAME 记录类型）。 否则，尝试连接到 Intune 的用户必须在注册期间输入 Intune 服务器名称。

**第 1 步：创建 CNAME**（可选）<br>
为公司的域创建 CNAME DNS 资源记录。 例如，如果你的公司网站为 contoso.com，则可在 DNS 中创建将 EnterpriseEnrollment.contoso.com 重定向到 enterpriseenrollment-s.manage.microsoft.com 的 CNAME。

虽然可选择性创建 CNAME DNS 条目，但 CNAME 记录可简化用户的注册。 如果找不到注册 CNAME 记录，系统会提示用户手动输入 MDM 服务器名称 enrollment.manage.microsoft.com。

|类型|主机名|指向|TTL|
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.company_domain.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 小时|
|CNAME|EnterpriseRegistration.company_domain.com|EnterpriseRegistration.windows.net|1 小时|

若公司使用多个 UPN 后缀，你需要为每个域名创建一个 CNAME，并将每个 CNAME 指向 EnterpriseEnrollment-s.manage.microsoft.com。 例如，Contoso 的用户使用以下格式作为其电子邮件/UPN：

- name@contoso.com
- name@us.contoso.com
- name@eu.contoso.com

Contoso DNS 管理员应创建以下 CNAME：

|类型|主机名|指向|TTL|  
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 小时|
|CNAME|EnterpriseEnrollment.us.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 小时|
|CNAME|EnterpriseEnrollment.eu.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 小时|

`EnterpriseEnrollment-s.manage.microsoft.com` - 支持从电子邮件的域名重定向到具有域识别的 Intune 服务

对 DNS 记录所做的更改可能最多需要 72 小时才能进行传播。 无法在 Intune 中验证 DNS 更改，直到 DNS 记录开始进行传播。

## <a name="additional-endpoints-are-used-but-no-longer-supported"></a>已使用其他终结点，但不再受支持
EnterpriseEnrollment-s.manage.microsoft.com 是注册的首选 FQDN。 客户过去曾使用过另外两个终结点，这些终结点仍在工作，但不再受支持。 EnterpriseEnrollment.manage.microsoft.com（无 -s）和 manage.microsoft.com 两者都作为自动发现服务器的目标，但用户必须在确认消息上单击“确定”。 如果指向 EnterpriseEnrollment-s.manage.microsoft.com，则用户不必执行额外的确认步骤，因此这是推荐的配置

## <a name="alternate-methods-of-redirection-are-not-supported"></a>不支持重定向的备用方法
不支持使用 CNAME 配置以外的方法。 例如，不支持使用代理服务器将 enterpriseenrollment.contoso.com/EnrollmentServer/Discovery.svc 重定向到 enterpriseenrollment-s.manage.microsoft.com/EnrollmentServer/Discovery.svc 或 manage.microsoft.com/EnrollmentServer/Discovery.svc。

**步骤 2：验证 CNAME**（可选）<br>
1. 在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，选择“设备” > “Windows” > “Windows 注册” > “CNAME 验证”   。
2. 在“域”框中，输入公司网站，然后选择“测试” 。

## <a name="tell-users-how-to-enroll-windows-devices"></a>告知用户如何注册 Windows 设备
告诉用户如何注册其 Windows 设备以及在纳入管理之后会出现的情况。

> [!NOTE]
> 最终用户必须通过 Microsoft Edge 访问公司门户网站，才能查看为特定版本的 Windows 分配的 Windows 应用。 Google Chrome、Mozilla Firefox 和 Internet Explorer 等其他浏览器不支持该类型的筛选。

有关最终用户注册说明，请参阅[在 Intune 中注册 Windows 设备](../user-help/windows-enrollment-company-portal.md)。 还可让用户查看 [IT 管理员可以在我的设备上看到什么](../user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune.md)。

>[!IMPORTANT]
> 如果尚未启用自动 MDM 注册，但是具有已加入到 Azure AD 的 Windows 10 设备，则注册后可在 Intune 控制台中看到两条记录。 确保具有已加入 Azure AD 的设备的用户使用相同的帐户转到“帐户” > “访问工作或学校”和“连接”后，即可停止此操作  。 

若要详细了解最终用户任务，请参阅 [Microsoft Intune 最终用户体验的相关资源](../fundamentals/end-user-educate.md)。

## <a name="registration-and-enrollment-cnames"></a>注册 CNAME
Azure Active Directory 具有不同的 CNAME，适用于 iOS/iPadOS、Android 和 Windows 设备的设备注册。 Intune 条件访问需要注册设备，也称为“工作区加入”。 如果计划使用条件性访问，还应为每个公司名称配置 EnterpriseRegistration CNAME。

| 类型 | 主机名 | 指向 | TTL |
| --- | --- | --- | --- |
| 名称 | EnterpriseRegistration. company_domain.com | EnterpriseRegistration.windows.net | 1 小时|

有关设备注册的详细信息，请参阅[使用 Azure 门户管理设备标识](https://docs.microsoft.com/azure/active-directory/devices/device-management-azure-portal)

## <a name="windows-10-auto-enrollment-and-device-registration"></a>Windows 10 自动注册和设备注册

此部分适用于美国政府云客户。

虽然可选择性创建 CNAME DNS 条目，但 CNAME 记录可简化用户的注册。 如果找不到注册 CNAME 记录，系统会提示用户手动输入 MDM 服务器名称 enrollment.manage.microsoft.us。

| 类型 | 主机名 | 指向 | TTL |
| --- | --- | --- | --- |
| CNAME | EnterpriseEnrollment.company_domain.com | EnterpriseEnrollment-s.manage.microsoft.us | 1 小时|
|CNAME | EnterpriseRegistration.company_domain.com | EnterpriseRegistration.windows.net | 1 小时 |


## <a name="next-steps"></a>后续步骤

- [在 Azure 上使用 Intune 管理 Windows 设备时的注意事项](../fundamentals/intune-legacy-pc-client.md)。
