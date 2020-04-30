---
title: 将 Jamf Pro 与 Microsoft Intune 集成来满足符合性要求
titleSuffix: Microsoft Intune
description: 通过将 Microsoft Intune 符合性策略与 Azure Active Directory 条件访问相结合，可帮助集成由 Jamf 管理的设备并确保安全。
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
ms.assetid: 4b6dcbcc-4661-4463-9a36-698d673502c6
ms.reviewer: arnab
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: e5b568a90d4077c32a88044beea746907613eb0e
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81525727"
---
# <a name="integrate-jamf-pro-with-intune-for-compliance"></a>将 Jamf Pro 与 Intune 集成以实现合规

你的组织使用 [Jamf Pro](https://www.jamf.com) 管理 macOS 设备时，可以将 Microsoft Intune 符合性策略用于 Azure Active Directory (Azure AD) 条件访问，从而确保组织中的设备满足符合性要求，然后才能访问公司资源。 若要将 Jamf Pro 与 Intune 集成，你有两个选项：

- **手动配置集成** - 使用本文中的信息来手动配置与 Intune 的 Jamf 集成。
- **使用 Jamf 云连接器**（推荐）- 使用[将 Jamf 云连接器与 Microsoft Intune 协同使用](../protect/conditional-access-jamf-cloud-connector.md)中的信息来安装 Jamf 云连接器，以便将 Jamf Pro 与 Microsoft Intune 集成  。 云连接器自动执行手动配置集成时所需的多个步骤。


将 Jamf Pro 与 Intune 集成时，可以通过 Azure AD 将 macOS 设备中的清单数据与 Intune 同步。 Intune 的符合性引擎随后会分析清单数据以生成报表。 可将 Intune 的分析与有关设备用户的 Azure AD 标识的智能结合使用，以通过条件访问来驱动强制执行。 符合条件访问策略的设备可以访问受保护的公司资源。

配置集成后，将在使用 Jamf 管理的设备上[配置 Jamf 和 Intune 以使用条件访问强制实现符合性](conditional-access-assign-jamf.md)。

## <a name="prerequisites"></a>必备条件

### <a name="products-and-services"></a>产品和服务

需要满足以下要求才能通过 Jamf Pro 配置条件访问：

- Jamf Pro 10.1.0 或更高版本
- [适用于 macOS 的公司门户应用](https://aka.ms/macoscompanyportal)
- 带有 OS X 10.12 Yosemite 或更高版本的 macOS 设备

### <a name="network-ports"></a>网络端口

<!-- source: https://support.microsoft.com/en-us/help/4519171/troubleshoot-problems-when-integrating-jamf-with-microsoft-intune -->
要使 Jamf 和 Intune 正确集成，应可访问以下端口：

- **Intune**：端口 443
- **Apple**：端口 2195、2196 和 5223（向 Intune 推送通知）
- **Jamf**：端口 80 和 5223

若要允许 APNS 在网络上正常运行，还必须启用与以下位置的传出连接，以及来自以下位置的重定向：

- 通过所有客户端网络中的 TCP 端口 5223 和 443 的 Apple 17.0.0.0/8 块。
- Jamf Pro 服务器中的端口 2195 和 2196。  

有关这些端口的详细信息，请参阅以下文章：

- [Intune 网络配置要求和带宽](../fundamentals/network-bandwidth-use.md)。
- jamf.com 上的 [Jamf Pro 使用的网络端口](https://www.jamf.com/jamf-nation/articles/34/network-ports-used-by-jamf-pro)。
- support.apple.com 上的 [Apple 软件产品使用的 TCP 和 UDP 端口](https://support.apple.com/HT202944)

## <a name="connect-intune-to-jamf-pro"></a>将 Intune 连接到 Jamf Pro

若要将 Intune 与 Jamf Pro 连接：

1. 在 Azure 中创建新的应用程序。
2. 启用 Intune 以与 Jamf Pro 集成。
3. 在 Jamf Pro 中配置条件访问。

### <a name="create-an-application-in-azure-active-directory"></a>在 Azure Active Directory 中创建应用程序

1. 在 [Azure 门户](https://portal.azure.com)中转到“Azure Active Directory” > “应用注册”，然后选择“新建注册”    。

2. 在“注册应用程序”  页上，指定以下详细信息：

   - 在“名称”  部分中，输入一个有意义的应用程序名称，例如“Jamf 条件访问”  。
   - 对于“支持的帐户类型”  部分，选择“任何组织目录中的帐户”  。
   - 对于“重定向 URI”  ，保留 Web 的默认值，然后指定 Jamf Pro 实例的 URL。

3. 选择“注册”  创建应用程序并打开新应用的“概述”页  。

4. 在应用的“概述”  页上，复制“应用程序(客户端)ID”  值并记录该值以供将来使用。 后续过程中将需要此值。

5. 选择“管理”下的“证书和密码”   。 选择“新建客户端密码”  按钮。 输入“说明”中的值，选择“截止期限”的任何选项，然后选择“添加”    。

   > [!IMPORTANT]
   > 在离开此页面之前，复制客户端密码的值并记录该值以供将来使用。 后续过程中将需要此值。 此值不再可用，无需重新创建应用注册。

6. 选择“管理”下的“API 权限”   。 

7. 在“API 权限”页上，通过选择每个现有权限旁边的“...”图标来删除此应用的所有权限  。 请注意，这是必需的；如果此应用注册中有任何意外的额外权限，集成将不会成功。

8. 接下来，我们将添加更新设备属性的权限。 在“API 权限”页的左上角，选择“添加权限”以添加新的权限   。 

9. 在“请求获取 API 权限”  页上，选择“Intune”  ，然后选择“应用程序权限”  。 仅选中 update_device_attributes 对应的复选框，然后保存新权限  。

10. 接下来，选择“API 权限”页左上角的“向 \<的租户> 授予管理员同意权限”，向此应用授予管理员同意权限   。 你可能需要在新窗口中对你的帐户重新进行身份验证，并按照提示授予应用程序访问权限。  

11. 通过单击页面顶部的“刷新”按钮来刷新页面  。 确认是否针对 update_device_attributes 权限授予了管理员同意  。 

12. 成功注册应用后，API 权限应只包含一个名为 update_device_attributes 的权限，并且应如下所示  ：

   ![成功的权限](./media/conditional-access-integrate-jamf/sucessfull-app-registration.png)

   将完成 Azure AD 中的应用注册过程。

    > [!NOTE]
    > 如果客户端密码过期，则必须在 Azure 中创建一个新的客户端密码，然后更新 Jamf Pro 中的条件访问数据。 Azure 允许同时具有旧密钥和新密钥，以防止服务中断。

### <a name="enable-intune-to-integrate-with-jamf-pro"></a>启用 Intune 以与 Jamf Pro 集成

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 选择“租户管理”   > “连接器和令牌”   > “合作伙伴设备管理”  。

3. 通过将上一步骤中保存的应用程序 ID 粘贴到“为 Jamf 指定 Azure Active Directory 应用 ID”字段来启用 Jamf 的符合性连接器   。

4. 选择“保存”  。

### <a name="configure-microsoft-intune-integration-in-jamf-pro"></a>在 Jamf Pro 中配置 Microsoft Intune 集成

1. 在 Jamf Pro 控制台中激活连接：

   1. 打开 Jamf Pro 控制台并导航到“全局管理”   > “条件访问”  。 单击“macOS Intune 集成”选项卡上的“编辑”按钮   。
   2. 选中“启用适用于 macOS 的 Intune 集成”复选框  。
   3. 提供在 Azure AD 中创建应用时保存的有关 Azure 租户的必要信息，包括“位置”、  “域名”、  “应用程序 ID”  和“客户端密码”的值  。
   4. 选择“保存”  。 Jamf Pro 将测试设置并验证是否成功。

   返回到 Intune 中的“合作伙伴设备管理”  页完成配置。

2. 在 Intune 中，转到“合作伙伴设备管理”  页。 在“连接器设置”  下，为分配配置组：

   - 选择“包括”  ，并指定要向 Jamf 注册 macOS 的目标用户组。
   - 使用“排除”以选择不会向 Jamf 注册而是将其 Mac 直接注册到 Intune 的用户组  。

   “排除”  覆盖”包括”  ，这意味着在两个组中的任何设备都将从 Jamf 中排除，并直接注册到 Intune。

   >[!NOTE]
   > 此包括和排除用户组的方法将影响用户的注册体验。 任何已在 Jamf 或 Intune 中注册 Mac 随后定向到注册其他 MDM 的用户必须取消注册其设备，然后在设备管理正常工作之前通过新的 MDM 重新注册。

3. 选择“评估”  ，以根据组配置确定将向 Jamf 注册的设备数。

4. 准备好应用配置时，选择“保存”  。

5. 若要继续，接下来需使用[用于为 Mac 部署公司门户的 Jamf](conditional-access-assign-jamf.md#deploy-the-company-portal-app-for-macos-in-jamf-pro)，以便用户可以将其设备注册到 Intune。

## <a name="set-up-compliance-policies-and-register-devices"></a>设置符合性策略并注册设备

配置 Intune 和 Jamf 之间的集成后，需要[将符合性策略应用到 Jamf 托管的设备](conditional-access-assign-jamf.md)。

## <a name="disconnect-jamf-pro-and-intune"></a>断开 Jamf Pro 和 Intune 的连接

如需删除 Jamf Pro 与 Intune 的集成，请使用以下步骤从 Jamf Pro 控制台中删除连接。此信息既适用于手动配置的集成，也适用于使用云连接器实现的集成。

1. 在 Jamf Pro 中，转到“全局管理”   > “条件访问”  。 在“macOS Intune 集成”  选项卡上，选择“编辑”  。

2. 清除“启用适用于 macOS 的 Intune 集成”  复选框。

3. 选择“保存”  。 Jamf Pro 将配置发送到 Intune，并且将终止集成。

4. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

5. 选择“租户管理”   > “连接器和令牌”   > “合作伙伴设备管理”  ，以验证状态现在是否为“已终止”  。

   > [!NOTE]
   > 组织的 Mac 设备将在控制台中显示的日期（3 个月）删除。

## <a name="next-steps"></a>后续步骤

- [将符合性策略应用到 Jamf 管理的设备](conditional-access-assign-jamf.md)
- [Jamf 向 Intune 发送的数据](data-jamf-sends-to-intune.md)
