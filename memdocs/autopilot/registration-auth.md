---
title: Windows Autopilot 客户许可
description: 了解云服务提供商 (CSP) 合作伙伴或 OEM 如何获取客户授权，以代表客户注册 Windows Autopilot 设备。
keywords: mdm, 设置, windows, windows 10, oobe, 管理, 部署, autopilot, ztd, 零接触, 合作伙伴, msfb, intune
ms.reviewer: mniehaus
manager: laurawi
ms.technology: windows
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: db2dc86b4f7cb514f3ceca4d37bf387db31c13f4
ms.sourcegitcommit: e533cdf8722156a66b1cc46f710def96587345d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90568548"
---
# <a name="windows-autopilot-customer-consent"></a>Windows Autopilot 客户许可

**适用于：Windows 10**

本文介绍了云服务提供商如何 (CSP) 合作伙伴 (直接帐单、间接提供商或间接经销商) ，或者 OEM 可以获取客户授权，以代表客户注册 Windows Autopilot 设备。

## <a name="csp-authorization"></a>CSP 授权

CSP 合作伙伴可以根据以下限制，获取客户授权，以代表客户注册 Windows Autopilot 设备：

<table>
<tr><td>直接 CSP<td>获取客户用于注册设备的直接授权。
<tr><td>间接 CSP 提供程序<td>获取隐式权限，以便通过其 CSP 分销商合作伙伴与客户的关系注册设备。 间接 CSP 提供商通过 Microsoft 合作伙伴中心注册设备。
<tr><td>间接 CSP 分销商<td>获取客户用于注册设备的直接授权。 同时，其间接 CSP 提供商伙伴也会获得授权，这意味着间接提供商或间接经销商可以为客户注册设备。 但是，间接 CSP 分销商必须通过 MPC UI 注册设备， (手动) 上传 CSV 文件。 间接 CSP 提供程序可以使用 MPC Api 注册设备。
</table>

### <a name="steps"></a>步骤

要使 CSP 为客户注册 Windows Autopilot 设备，客户必须首先使用以下过程授予该 CSP 合作伙伴权限：

1. CSP 向客户发送链接，请求授权/同意代表他们注册/管理设备。 为此，请执行以下操作：
    1. CSP 登录到 Microsoft 合作伙伴中心。
    2. 在顶部菜单中单击 " **仪表板** "。
    3. 单击侧边菜单上的 " **客户** "。
    4. 单击 " **请求分销商关系** " 链接：

        ![请求分销商关系](images/csp1.png)
 
    5. 选中指出是否需要委派的管理员权限的复选框：
 
        ![委托的权限](images/csp2.png)

        > [!NOTE]
        > 根据你的合作伙伴，在请求此许可时，他们可能会请求委派的管理员权限 (的) 。 如果可能，更好的做法是使用本文档)  (中所示的较新的中转过程。 如果没有，你可以从 Microsoft 管理中心或 Microsoft 365 管理门户轻松删除其 "状态" 状态： https://docs.microsoft.com/partner-center/customers_revoke_admin_privileges
    6. 通过电子邮件将上述模板发送给客户。

2. 具有 Microsoft 管理中心全局管理员权限的客户单击电子邮件中的链接。 该链接会将其带到以下 Microsoft 365 管理中心页面：

    ![截图接受协议和授权合作伙伴页面委派管理权限](images/csp3a.png)

    如果客户请求委派的管理员权限 (") ，则会看到上述图像。 页面显示请求的管理员角色。 如果客户未请求委派的管理员权限，则会看到以下页面：

    ![截图接受协议和授权合作伙伴页](images/csp3b.png) 

    > [!NOTE]
    > 如果用户没有全局管理员权限，单击该链接，将看到类似于以下内容的消息：

    ![权限页的截图](images/csp4.png)

3. 客户选中 " **是"** 复选框，然后选择 " **接受** " 按钮。 授权立即进行。
4. 若要检查授权请求是否已完成，CSP 可以在其 MPC 帐户中检查 **客户** 列表。 如果客户在列表中，则请求已完成。 例如：

    ![客户](images/csp5.png)

## <a name="oem-authorization"></a>OEM 授权

每个 OEM 都具有唯一的链接，可提供给其各自的客户，OEM 可以通过从 Microsoft 请求该链接 msoemops@microsoft.com 。

1. OEM 电子邮件链接到其客户。
2. 使用 Business (MSfB Microsoft Store 的客户) 全局管理员权限单击电子邮件中的链接，该链接将直接转到以下 MSfB 页面：

    ![接受合作伙伴邀请页面的截图](images/csp6.png)

    > [!NOTE]
    > 如果用户没有全局管理员权限，单击该链接，将看到类似于以下内容的消息：

    ![截图 of MSfB 权限必需页](images/csp7.png)

3. 客户选中 " **是"** 复选框，然后选择 " **接受** " 按钮。 授权立即进行。

    > [!NOTE]
    > 完成此过程后，管理员当前不可能删除 OEM。 若要删除 OEM 或撤销其权限，请将请求发送到 msoemops@microsoft.com

4. OEM 可以使用验证设备提交数据 API 来验证是否已完成同意。 最新版本的 API 白皮书 p 中讨论了此 API。 14ff [https://devicepartner.microsoft.com/assets/detail/windows-autopilot-integration-with-oem-api-design-whitepaper-docx](https://devicepartner.microsoft.com/assets/detail/windows-autopilot-integration-with-oem-api-design-whitepaper-docx) 。 **注意**：仅 Microsoft 设备合作伙伴可以访问此链接。 如本文中所述，在尝试注册设备之前，建议 OEM 合作伙伴运行 API 检查以确认它们是否已收到客户同意，这是建议的最佳做法。 此检查可帮助避免注册过程中的错误。

    > [!NOTE]
    > 在 OEM 授权注册过程中，不会向 OEM 授予委派的管理员权限。

## <a name="summary"></a>“摘要”

在此过程的这一阶段，不再涉及 Microsoft，同意交换直接在 OEM 与客户之间进行。 而且，只要单击按钮，就会立即立即进行。
