---
title: 集成 Jamf Pro 云连接器与 Microsoft Intune
titleSuffix: Microsoft Intune
description: 结合使用 Jamf 云连接器与包含 Azure Active Directory 条件访问的 Microsoft Intune 符合性策略，有助于集成和保护受 Jamf 管理的设备。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/13/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: arnab
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f86b418df46069b2a33dd56d06e0e82dbbbf8090
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81538444"
---
# <a name="use-the-jamf-cloud-connector-with-microsoft-intune"></a>结合使用 Jamf 云连接器与 Microsoft Intune

本文可指导你安装 Jamf 云连接器，从而集成 Jamf Pro 与 Microsoft Intune。 云连接器自动执行手动配置集成所需的多个步骤（如[集成 Jamf Pro 与 Intune 以满足符合性要求](../protect/conditional-access-integrate-jamf.md)中所述）。

安装云连接器时：

- 安装程序自动在 Azure 中创建 Jamf Pro 应用程序，而无需手动配置它们。
- 你可以将多个 Jamf Pro 实例与托管 Intune 订阅的同一 Azure 租户集成。

只有在使用云连接器时，才支持将多个 Jamf Pro 实例与一个 Azure 租户连接。 如果你使用手动配置的连接，只有一个 Jamf 实例可以与 Azure 租户集成。

视需要选择使用云连接器：

- 对于尚未与 Jamf 集成的新租户，可以选择按照本文中所述来配置云连接器。 也可以按照[集成 Jamf Pro 与 Intune 以满足符合性要求](../protect/conditional-access-integrate-jamf.md)中所述来手动配置集成
- 对于已有手动配置的租户，可以选择删除相应集成，然后安装云连接器。 本文介绍了如何删除现有集成和安装云连接器。

如果打算替换先前与 Jamf 云连接器的集成：

- 遵循[删除当前配置的过程](#remove-the-jamf-pro-integration-for-a-previously-configured-tenant)，包括删除 Jamf Pro 的 Enterprise 应用程序，并禁用手动集成。 然后，可以遵循[配置云连接器的过程](#configure-the-cloud-connector-for-a-new-tenant)。
- 无需重新注册设备。 已注册的设备无需进行其他配置即可使用云连接器。
- 请务必在禁用手动集成后的 24 小时内配置云连接器，以确保已注册的设备可以继续报告自己的状态。

若要详细了解 Jamf 云连接器，请参阅 docs.jamf.com 上的[使用云连接器配置 macOS Intune 集成](https://docs.jamf.com/technical-papers/jamf-pro/microsoft-intune/10.17.0/Configuring_the_macOS_Intune_Integration_using_the_Cloud_Connector.html)。

## <a name="prerequisites"></a>必备条件

产品和服务  ：  
- Jamf Pro 10.18 或更高版本
- 拥有条件访问特权的 Jamf Pro 用户帐户  
- Microsoft Intune
- Microsoft Azure AD Premium
- [适用于 macOS 的公司门户应用](https://aka.ms/macoscompanyportal)
- 带有 OS X 10.12 Yosemite 或更高版本的 macOS 设备

网络  ：  
为了能够正确集成 Jamf 和 Intune，以下端口和终结点必须是可以访问的：

- **Intune**：端口 443
- **Apple**：端口 2195、2196 和 5223（向 Intune 推送通知）
- **Jamf**：端口 80 和 5223

- 终结点：
  - login.microsoftonline.com
  - graph.windows.net  
  - *.manage.microsoft.com  

为了让 APNS 在网络上正常运行，必须启用流向以下端口的传出连接，以及来自以下端口的重定向：

- 通过所有客户端网络中的 TCP 端口 5223 和 443 的 Apple 17.0.0.0/8 块。
- Jamf Pro 服务器中的端口 2195 和 2196。

有关这些端口的详细信息，请参阅以下文章：

- [Intune 网络配置要求和带宽](../fundamentals/network-bandwidth-use.md)。
- jamf.com 上的 [Jamf Pro 使用的网络端口](https://www.jamf.com/jamf-nation/articles/34/network-ports-used-by-jamf-pro)。
- support.apple.com 上的 [Apple 软件产品使用的 TCP 和 UDP 端口](https://support.apple.com/HT202944)

**帐户**：  
若要遵循本文中的过程，必须使用拥有以下权限的帐户：

- Jamf Pro 控制台  ：有权管理 Jamf Pro 的帐户
- Microsoft Endpoint Management 管理中心  ：全局管理员
- Azure 门户：  全局管理员

## <a name="remove-the-jamf-pro-integration-for-a-previously-configured-tenant"></a>删除以前配置的租户的 Jamf Pro 集成

请先  遵循以下过程从 Azure 租户中删除手动配置的 Jamf Pro 集成，然后才能配置云连接器。

如果你之前未在 Jamf Pro 和 Intune 之间建立过连接，或者如果你有一个或多个已使用云连接器的连接，请跳过此过程，并开始[为新租户配置云连接器](#configure-the-cloud-connector-for-a-new-tenant)。

### <a name="remove-a-manually-configured-jamf-pro-integration"></a>删除手动配置的 Jamf Pro 集成

1. 登录 Jamf Pro 控制台。

2. 选择“设置”  （右上角的齿轮图标），然后依次转到“全局管理”   > “条件访问”  。

   ![转到“条件访问”](./media/conditional-access-jamf-cloud-connector/navigate-jamf-console-1.png)

3. 选择“编辑”  。

4. 取消选中“为 macOS 启用 Intune 集成”  复选框。

   在取消选中此设置后，连接会被禁用，但会保存配置。

5. 登录 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，然后依次转到“租户管理”   > “合作伙伴设备管理”  。

   在“合作伙伴设备管理”  节点上，删除“为 Jamf 指定 Azure Active Directory 应用程序 ID”  字段中的“应用程序 ID”  ，然后选择“保存”  。

   应用程序 ID 是指，在设置 Jamf Pro 的手动集成时，在 Azure 中创建的 Azure Enterprise 应用程序的 ID。

6. 使用拥有全局管理员权限的帐户来登录 [Azure 门户](https://portal.azure.com/)，然后依次转到“Azure Active Directory”   > “Enterprise 应用程序”  。

   找到两个 Jamf 应用程序，并删除它们。 当你在下一个过程中配置 Jamf 云连接器时，新的应用程序会自动创建。

   ![选择要删除的 Jamf 应用程序](./media/conditional-access-jamf-cloud-connector/delete-jamf-apps.png)

   当你在 Jamf Pro 中禁用集成并删除 Enterprise 应用程序后，“合作伙伴设备管理”  节点显示“已终止”  连接状态。

   ![“已终止”连接状态](./media/conditional-access-jamf-cloud-connector/terminated-connection-status.png)

至此，你已成功删除手动配置的 Jamf Pro 集成，现在可以使用云连接器来设置集成了。 为此，请参阅本文中的[为新租户配置云连接器](#configure-the-cloud-connector-for-a-new-tenant)。

## <a name="configure-the-cloud-connector-for-a-new-tenant"></a>为新租户配置云连接器

在以下情况下，请遵循下面的过程来配置 Jamf 云连接器，以集成 Jamf Pro 和 Microsoft Intune：

- 你没有为 Azure 租户配置 Jamf Pro 和 Intune 之间的任何集成。
- 你已在 Azure 租户中设置了 Jamf Pro 和 Intune 之间的云连接器，并且想要将其他 Jamf 实例与订阅集成。

如果当前已手动配置 Intune 和 Jamf Pro 之间的集成，请先参阅本文中的[删除以前配置的租户的 Jamf Pro 集成](#remove-the-jamf-pro-integration-for-a-previously-configured-tenant)来删除此类集成，再继续操作。 必须先删除手动配置的集成，然后才能成功设置 Jamf 云连接器。

### <a name="create-a-new-connection"></a>新建连接

1. 登录 Jamf Pro 控制台。

2. 选择“设置”  （右上角的齿轮图标），然后依次转到“全局管理”   > “条件访问”  。

   ![转到“条件访问”](./media/conditional-access-jamf-cloud-connector/navigate-jamf-console-1.png)

3. 选择“编辑”  。

4. 选中“为 macOS 启用 Intune 集成”  复选框。
   - 选中此设置可以让 Jamf Pro 将清单更新发送到 Microsoft Intune。
   - 可以取消选中此设置来禁用连接，但会保存配置。

   > [!IMPORTANT]
   > 如果“为 macOS 启用 Intune 集成”  已选中，且“连接类型”  设置为“手动”  ，那么必须先删除此类集成，然后才能继续操作。 请先参阅本文中的[删除以前配置的租户的 Jamf Pro 集成](#remove-the-jamf-pro-integration-for-a-previously-configured-tenant)，再继续操作。

5. 在“连接类型”  下，选择“云连接器”  。

   ![在 Jamf Pro 控制台中选择“云连接器”](./media/conditional-access-jamf-cloud-connector/select-cloud-connector.png)

6. 在“主权云”  弹出菜单中，选择 Microsoft 提供的主权云的位置。

7. 对于 Microsoft Azure 无法识别的计算机，选择以下登陆页面选项之一：
   - “默认 Jamf Pro 设备注册”页  - 根据 macOS 设备的状态，此选项会将用户重定向到 Jamf Pro 设备注册门户（用于向 Jamf Pro 注册），或 Intune 公司门户应用程序（用于向 Azure AD 注册）。
   - “拒绝访问”页 
   - 自定义 URL 

8. 选择“**连接**”。 此时，你会重定向到在 Azure 中注册 Jamf Pro 应用程序。

   当出现提示时，指定 Microsoft Azure 凭据，然后按照屏幕上的说明操作来授予所请求的权限。 你将为云连接器  授予权限，然后再次为云连接器用户注册应用程序  授予权限。 这两个应用程序在 Azure 中都注册为 Enterprise 应用程序。

   在你为这两个应用程序授予权限后，“应用程序 ID”  页打开。

9. 在“应用程序 ID”  页上，选择“复制并打开 Intune”  。

   ![应用程序 ID](./media/conditional-access-jamf-cloud-connector/copy-application-id.png)

   此时，应用程序 ID  会复制到系统剪贴板中以供在下一步中使用，且 Microsoft Endpoint Manager 管理中心  内的“合作伙伴设备管理”  节点打开。 （依次转到“租户管理”   > “合作伙伴设备管理”  ）。

10. 在“合作伙伴设备管理”  节点上，将应用程序 ID  粘贴  到“为 Jamf 指定 Azure Active Directory 应用程序 ID”  字段中，然后选择“保存”  。

    ![配置“合作伙伴设备管理”](./media/conditional-access-jamf-cloud-connector/partner-device-management.png)

11. 返回到 Jamf Pro 中的“应用程序 ID”页，然后选择“确认”  。

12. Jamf Pro 完成并测试配置，然后在“条件访问设置”页上指明连接是否成功。 下图展示了成功示例：

    ![Jamf Pro 中确认了配置成功](./media/conditional-access-jamf-cloud-connector/successful-configuration.png)

13. 在 Microsoft Endpoint Manager 管理中心内，刷新“合作伙伴设备管理”  节点。 连接现在应该显示为“活动”  ：

    ![连接状态为“活动”](./media/conditional-access-jamf-cloud-connector/active-connection-status.png)

当你在 Jamf Pro 和 Microsoft Intune 之间成功建立连接后，Jamf Pro 会将向 Azure AD 注册（向 Azure AD 注册是最终用户工作流）的每台计算机的清单信息发送到 Microsoft Intune。 在 Jamf Pro 中，可以在计算机清单信息的“本地用户帐户”类别中查看用户和计算机的条件访问清单状态。

使用 Jamf 云连接器集成一个 Jamf Pro 实例后，可以遵循此相同的过程，为 Azure 租户中的同一 Intune 订阅配置其他 Jamf Pro 实例。  

## <a name="set-up-compliance-policies-and-register-devices"></a>设置符合性策略并注册设备

配置 Intune 和 Jamf 之间的集成后，需要[将符合性策略应用到 Jamf 托管的设备](../protect/conditional-access-assign-jamf.md)。

## <a name="disconnect-jamf-pro-and-intune"></a>断开 Jamf Pro 和 Intune 的连接

如需删除 Jamf Pro 与 Intune 的集成，请按照以下步骤操作，在 Jamf Pro 控制台中删除连接。此信息既适用于云连接器，也适用于手动配置的集成。

1. 在 Jamf Pro 中，转到“全局管理”   > “条件访问”  。 在“macOS Intune 集成”  选项卡上，选择“编辑”  。

2. 清除“启用适用于 macOS 的 Intune 集成”  复选框。

3. 选择“保存”  。 此时，Jamf Pro 将配置发送到 Intune，集成将被终止

4. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

5. 选择“租户管理”   > “连接器和令牌”   > “合作伙伴设备管理”  ，以验证状态现在是否为“已终止”  。

   > [!NOTE]
   > 组织的 Mac 设备将在控制台中显示的日期（3 个月）删除。

## <a name="get-support-for-the-cloud-connector"></a>获取云连接器方面的支持

由于云连接器会自动创建集成所需的 Azure Enterprise 应用程序，因此你的第一个支持联系点应为 Jamf  。 选项包括：

- `support@jamf.com` 处的电子邮件支持
- 使用 Jamf Nation 处的支持门户： https://www.jamf.com/support/ 


在联系支持人员前，请先执行以下操作：

- 审阅先决条件（如所使用的端口和产品版本）。
- 确认以下两个在 Azure 中创建的 Jamf Pro 应用程序的权限是否未遭修改。 Intune 不支持更改应用程序权限，因为这可能会导致集成失败。

  云连接器用户注册应用程序  ：
  - API 名称：Microsoft Graph
    - 权限：登录和读取用户配置文件
    - 类型：委托
    - 授权方式：管理员同意
    - 授权者：管理员

  云连接器应用程序  ：
  - API 名称：Microsoft Graph（实例 1）
    - 权限：登录和读取用户配置文件
    - 类型：委托
    - 授权方式：管理员同意
    - 授权者：管理员

  - API 名称：Microsoft Graph（实例 2）
    - 权限：读取目录数据
    - 类型：应用程序
    - 授权方式：管理员同意
    - 授权者：管理员

  - API 名称：Intune API
    - 权限：将设备属性发送到 Microsoft Intune
    - 类型：应用程序
    - 授权方式：管理员同意
    - 授权者：管理员

## <a name="common-questions-about-the-jamf-cloud-connector"></a>Jamf 云连接器的常见问题解答

### <a name="what-data-is-shared-via-the-cloud-connector"></a>通过云连接器共享什么数据？

云连接器向 Microsoft Azure 进行身份验证，并将设备清单数据从 Jamf Pro 发送到 Azure。 此外，云连接器还管理 Azure 中的服务发现、令牌交换、通信错误和灾难恢复。

### <a name="where-is-device-inventory-data-stored"></a>设备清单数据存储在哪里？

设备清单数据存储在 Jamf Pro 数据库中。

### <a name="what-credentials-are-stored"></a>存储什么凭据？

未存储任何凭据。 配置云连接器时，管理员必须同意将 Jamf 多租户应用程序和本机 macOS 连接器应用程序添加到自己的 Azure AD 租户。 在多租户应用程序添加后，云连接器便会请求获取访问令牌，用来与 Azure API 交互。 随时都可以在 Microsoft Azure 中撤销应用程序访问权限，以限制访问。

### <a name="how-is-data-encrypted"></a>如何加密数据？

云连接器对在 Jamf Pro 和 Microsoft Azure 之间发送的数据使用传输层安全性 (TLS)。

### <a name="how-does-jamf-know-which-device-is-associated-with-which-instance-of-jamf-pro"></a>Jamf 如何确定哪台设备与哪个 Jamf Pro 实例关联？

Jamf Pro 使用 AWS 中的微服务将设备信息正确路由到正确的实例。

### <a name="can-i-switch-from-using-the-cloud-connector-to-the-manual-connection-type"></a>能否将“连接类型”从“云连接器”切换为“手动”？

是。 可以将“连接类型”更改回“手动”，然后按照手动设置步骤操作。 如有疑问，应向 Jamf 寻求帮助。

### <a name="permissions-were-modified-on-one-or-both-required-apps-cloud-connector-and-cloud-connector-user-registration-app-and-registration-is-not-working-is-this-supported"></a>是否支持修改一个或两个必需应用程序（云连接器  和云连接器用户注册应用程序  ）的权限，导致注册无法正常运行？

不支持修改应用程序的权限。

## <a name="next-steps"></a>后续步骤

- [将符合性策略应用到 Jamf 管理的设备](../protect/conditional-access-assign-jamf.md)
- [Jamf 向 Intune 发送的数据](../protect/data-jamf-sends-to-intune.md)
