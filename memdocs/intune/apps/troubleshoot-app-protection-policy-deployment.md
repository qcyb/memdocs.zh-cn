---
title: 如何对 Intune 应用保护策略部署进行故障排除
description: 讨论如何排查在部署 Intune 应用保护策略时可能会遇到的问题。
author: simonxjx
manager: dcscontentpm
localization_priority: Normal
search.appverid:
- MET150
audience: ITPro
ms.date: 4/17/2020
ms.service: microsoft-intune
ms.topic: troubleshooting
ms.author: v-six
ms.custom: CSSTroubleshoot
appliesto:
- Intune
ms.openlocfilehash: 8443ca01a0ca1647e8069fdccf1d71aef74c23d8
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989464"
---
# <a name="troubleshooting-app-protection-policy-deployment-in-intune"></a>Intune 中的应用保护策略部署疑难解答

## <a name="introduction"></a>简介

本文可帮助你了解和排查在 Microsoft Intune 中实施应用保护策略时遇到的问题。 按照适合你的情况的部分操作。

## <a name="basic-steps"></a>基本步骤

### <a name="collect-initial-data"></a>收集初始数据

在开始故障排除之前，应收集一些基本信息，这些信息可帮助你更好地了解问题和更快地找到解决方案。

收集以下信息：

- 未应用哪些策略设置？ 是否应用了任何策略？
- 用户体验怎么样？ 用户是否安装和启动了目标应用？
- 何时开始出现问题？ 应用保护曾经有效吗？
- 哪个平台存在问题 - Android 还是 iOS？
- 有多少用户受到影响？ 所有设备还是只有部分设备受到影响？
- 有多少设备受到影响？ 所有设备还是只有部分设备受到影响？
- 尽管 Intune 应用保护策略不需要移动设备管理 (MDM) 服务，但受影响的用户是否在使用 Intune 或第三方 EMM？
- 所有托管应用还是只有特定应用受到影响？ 例如，具有 [Intune App SDK](../developer/app-sdk-get-started.md) 的 LOB 应用受到影响，但应用商店应用不受影响？

现在，你可以开始根据这些问题的答案进行故障排除。

### <a name="verify-prerequisites"></a>验证先决条件

在故障排除中，接下来是检查是否满足所有先决条件。

尽管可以使用独立于任何 MDM 解决方案的 Intune 应用保护策略，但必须满足以下先决条件：

- 用户必须分配有 Intune 许可证。
- 用户必须属于应用保护策略所针对的安全组。 同一应用保护策略必须面向所使用的特定应用。
- 对于 Android 设备，需要使用公司门户应用来接收应用保护策略。
- 如果使用 [Word、Excel 或 PowerPoint](https://products.office.com/business/office) 应用，则必须满足以下附加要求：
    - 用户必须具有链接到其 Azure Active Directory (Azure AD) 帐户的 [Microsoft 365 商业或企业应用版](https://products.office.com/business/compare-more-office-365-for-business-plans)许可证。 订阅必须包括移动设备上的 Office 应用，可以包括 [OneDrive for Business](https://onedrive.live.com/about/business/) 云存储帐户。 可按照这些[说明](https://support.office.com/article/Assign-or-remove-licenses-for-Office-365-for-business-997596b5-4173-4627-b915-36abac6786dc)在 [Microsoft 365 管理中心](https://admin.microsoft.com)分配 Office 365 许可证。
    - 用户必须具有使用“另存为”这一精细功能进行配置的托管位置  。 此命令位于“保存组织数据的副本”应用程序保护策略设置下  。 例如，如果托管位置为 [OneDrive](https://onedrive.live.com/about/)，则应在用户的 Word、Excel 或 PowerPoint 应用中对 OneDrive 应用进行配置。
    - 如果托管位置为 OneDrive，则部署到用户的应用保护策略必须针对该应用。

  > [!NOTE]
  > Office 移动应用当前仅支持 SharePoint Online，不支持本地 SharePoint。

- 如果将 Intune 应用保护策略与本地资源（Microsoft Skype for Business 和 Microsoft Exchange Server）一起使用，则必须启用[适用于 Skype for Business 和 Exchange 的混合新式验证 (HMA)](https://docs.microsoft.com/office365/enterprise/hybrid-modern-auth-overview)。

Intune 应用保护策略要求应用与 [Intune App SDK](../developer/app-sdk-get-started.md) 之间的用户标识保持一致。 只能通过新式验证才能保证两者一致。 在某些情况下，应用可以在本地配置中运行，无需新式验证。 但是，结果不一致或不能保证。

要详细了解如何启用适用于 Skype for Business 混合和本地配置的 HMA，请参阅以下文章：

- **混合**<br>
[正式发布适用于 SfB 和 Exchange 的混合新式验证](https://techcommunity.microsoft.com/t5/Skype-for-Business-Blog/Hybrid-Modern-Auth-for-SfB-and-Exchange-goes-GA/ba-p/134756)

- **本地**<br>
[使用 AAD 实现适用于 SfB OnPrem 的新式验证](https://techcommunity.microsoft.com/t5/Skype-for-Business-Blog/Modern-Auth-for-SfB-OnPrem-with-AAD/ba-p/180910)

### <a name="check-app-protection-policy-status"></a>检查应用保护策略状态

要查看应用保护状态，请执行以下步骤：

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“应用” > “监视” > “应用保护状态”，然后选择“分配的用户”磁贴     。
3. 在  “应用报告”页上，选择  “选择用户”以显示用户和组的列表。
4. 搜索并从列表中选择一名受影响的用户，然后勾选“选择用户”  。 在“应用报表”窗格顶部，可以看到用户是否已获得应用保护授权且是否具有 O365 许可证。 还可以查看该用户所有设备的应用状态。
5. 记下重要信息，例如目标应用、设备类型、策略、设备签入状态和上次同步时间。

> [!NOTE]
> 仅当在工作环境中使用应用时，应用保护策略才适用。 例如，当用户使用工作帐户访问应用时。

有关详细信息，请参阅[如何在 Microsoft Intune 中验证应用保护策略设置](../apps/app-protection-policies-validate.md)。

### <a name="verify-that-user-identity-is-consistent-between-app-and-intune-app-sdk"></a>验证应用与 Intune App SDK 之间的用户标识是否一致

在大多数情况下，用户使用其用户主体名称 (UPN) 登录到帐户。 但是，在某些环境（例如本地方案）中，用户可能使用其他形式的登录凭据。 在这些情况下，你可能会发现应用中使用的 UPN 与 Azure AD 中的 UPN 对象不一致。 发生此问题时，应用保护策略不会按预期方式进行应用。

Microsoft 推荐的最佳做法是将 UPN 与主 SMTP 地址相匹配。 通过此做法，用户可以通过一致的标识登录到托管应用、Intune 应用保护和其他 Azure AD 资源。 有关详细信息，请参阅 [Azure AD UserPrincipalName 填充](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-userprincipalname)。

如果你的环境需要备用登录方法，请参阅[配置备用登录 ID](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configuring-alternate-login-id)，特别是[备用 ID 的混合新式验证](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configuring-alternate-login-id#hybrid-modern-authentication-with-alternate-id)。

### <a name="verify-that-the-user-is-targeted"></a>验证是否以用户为目标

Intune 应用保护策略必须以用户为目标。 如果某应用保护策略未分配给用户或用户组，则不会应用该策略。

要验证是否已将策略应用于目标用户，请按照以下步骤操作：

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“应用” > “监视器” > “应用保护状态”，然后选择“用户状态”磁贴（基于设备操作系统平台）     。
在打开的“应用报表”窗格中，勾选“选择用户”来搜索用户   。
3. 从列表中选择一个用户。 你可以查看该用户的详细信息。

将策略分配给用户组时，请确保该用户在该用户组中。 为此，请执行以下步骤：

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“组”>“所有组”，然后搜索并选择用于应用保护策略分配的组  。
3. 在“管理”部分下，选择“成员”   。
4. 如果受影响的用户未列出，请查看[使用 Azure Active Directory 组管理应用和资源访问权限](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-manage-groups)以及你的组成员身份规则。 确保受影响的用户包含在组中。
5. 确保受影响的用户不在策略的任何排除的组中。

> [!IMPORTANT]
> - Intune 应用保护策略必须分配给用户组，而不是设备组。
> - 如果受影响的设备使用 Apple 设备注册计划 (DEP)，请确保已启用“用户关联“  。 对需要在 DEP 下进行用户身份验证的应用而言，用户关联是必须的。
> - 如果受影响的设备使用 Android Enterprise，则只有工作配置文件支持应用保护策略。


### <a name="verify-that-the-managed-app-is-targeted"></a>验证是否以托管应用为目标

配置 Intune 应用保护策略时，目标应用必须使用 [Intune App SDK](../developer/app-sdk-get-started.md)。 否则，应用保护策略可能无法正常工作。

请确保 [Microsoft Intune 受保护的应用](../apps/apps-supported-intune-apps.md)中列出了目标应用。 对于 LOB 或自定义应用，请验证应用是否使用最新版本的 [Intune App SDK](../developer/app-sdk-get-started.md)。 注意以下事项：

对于 iOS 来说，该做法非常重要，因为每个版本都包含一些修补程序，这些修补程序会影响这些策略的应用方式及其工作原理。 有关详细信息，请参阅 [Intune App SDK iOS 版本](https://github.com/msintuneappsdk/ms-intune-app-sdk-ios/releases)。
对于 Android，这一做法并不重要。 但是，用户必须安装最新版本的公司门户应用，因为该应用将充当策略代理。

> [!NOTE]
> 从 2019 年 9 月起，Intune 将支持具有 Intune App SDK 8.1.1 及更高版本的 iOS 应用。 使用 8.1.1 之前的 SDK 版本构建的应用将不再受到支持。 

## <a name="more-information"></a>更多信息

### <a name="special-requirements-for-intune-mdm-managed-devices"></a>Intune MDM 托管设备的特殊要求

创建应用保护策略时，可以将其定位到所有应用类型或以下应用类型：

- 非托管设备上的应用
- Intune 托管设备上的应用
- Android 工作配置文件中的应用

> [!NOTE] 
> 若要指定应用类型，请将“针对所有应用类型”设置为“否”，然后从“应用类型”列表中进行选择    。

对于 iOS，需要以下附加[应用配置设置](../apps/app-configuration-policies-use-ios.md)才能将应用保护策略 (APP) 设置定位到 Intune 注册设备上的应用：

- 必须为所有 MDM（Intune 或第三方 EMM）托管应用程序配置“IntuneMAMUPN”  。 有关详细信息，请参阅“为 Microsoft Intune 或第三方 EMM 配置用户 UPN 设置”。
- 必须为所有第三方和 LOB MDM 托管应用程序配置“IntuneMAMDeviceID”  。
- 必须将“IntuneMAMDeviceID”配置为设备 ID 令牌  。 例如 key=IntuneMAMDeviceID，value={{deviceID}}。 有关详细信息，请参阅[为受管理 iOS 设备添加应用配置策略](../apps/app-configuration-policies-use-ios.md)。
- 如果仅配置了“IntuneMAMDeviceID”值，则 Intune 应用会将设备视为非托管设备  。

### <a name="scenario-policy-changes-are-not-working"></a>方案：策略更改无效
[Intune App SDK](../developer/app-sdk-get-started.md) 会定期检查是否出现策略更改。 但是，此过程可能会因以下原因而延迟：

- 该应用尚未通过服务签入。
- 已从设备中删除公司门户应用。

Intune 应用保护策略依赖于用户标识。 因此，需要使用工作或学校帐户登录到应用的有效登录以及与服务的一致连接。 如果用户尚未登录到应用，或已从设备中删除公司门户应用，则不会应用策略更新。

此外，对应用保护策略的更改和更新可能需要 8 个小时才能应用。 如果适用，则关闭所有应用并重启设备通常会强制尽快应用策略更新。

要查看应用保护状态，请执行以下步骤：

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“应用” > “监视” > “应用保护状态”，然后选择“分配的用户”磁贴     。
3. 在“应用报表”页面上，勾选“选择用户”以打开用户和组的列表  。
4. 搜索并从列表中选择一名受影响的用户，然后勾选“选择用户”  。
5. 查看当前应用的策略，包括状态和上次同步时间。
6. 如果状态为“未签入”，或者显示表明最近没有同步，请检查用户是否具有一致的网络连接  。 对于 Android 用户，请确保已安装最新版本的公司门户应用。

> [!IMPORTANT]
> [Intune App SDK](../developer/app-sdk-get-started.md) 每 30 分钟检查一次选择性擦除。 但是，对已登录用户的现有策略进行的更改可能 8 个小时都不会显示。 要加快此过程，请让用户注销应用，然后再重新登录或重启设备。

Intune 应用保护策略包括多标识支持。 Intune 可以将应用保护策略仅应用于已登录到应用的工作或学校帐户。 但是，每台设备仅支持一个工作或学校帐户。

### <a name="scenario-the-policy-is-applied-but-ios-users-can-still-transfer-work-files-to-unmanaged-apps"></a>方案：应用策略后，iOS 用户仍可将工作文件传输到非托管应用
适用于 iOS 设备的“打开方式管理”(![打开方式按钮](media/troubleshoot-app-protection/troubleshoot-app-protection.jpg)) 功能可将文件传输限制为仅在使用 MDM 通道部署的应用之间进行  。 用户可能能够将工作文件从 OneDrive 和 Exchange 等托管位置传输到非托管应用或位置，具体取决于配置。 iOS 的“打开方式管理”功能可在其他数据传输方法之外使用  。 因此，它不受“另存为”和“复制/粘贴”设置的影响   。

可将 Intune 应用保护策略与 iOS 的“打开方式管理”功能结合使用，从而通过以下方式保护公司数据  ：

- **不由 MDM 解决方案管理的员工自带设备**：可以将应用保护策略设置设置为“仅允许应用将数据传输到策略托管应用”  。 通过这种方式配置，策略托管应用中的“打开方式”行为只会将其他策略托管应用作为共享选项提供  。 例如，如果用户尝试在本机邮件应用中，通过 OneDrive 以附件形式发送受保护的文件，则该文件将无法阅读。

- **由 MDM 解决方案管理的设备**：对于在 Intune 或第三方 MDM 解决方案中注册的设备，使用应用保护策略的应用和通过 MDM 部署的其他托管 iOS 应用之间的数据共享由 Intune 应用和 iOS 的“打开方式管理”功能控制  。<br/><br/>
若要确保使用 MDM 解决方案部署的应用也与 Intune 应用保护策略相关联，请按照[配置用户 UPN 设置](../apps/data-transfer-between-apps-manage-ios.md#configure-user-upn-setting-for-microsoft-intune-or-third-party-emm)中的说明来配置用户 UPN 设置。<br/><br/>若要指定数据传输到其他应用的方式，请启用“将组织数据发送到其他应用”，然后选择首选的共享级别  。<br/><br/>若要指定应用从其他应用接收数据的方式，请启用“从其他应用接收数据”，然后选择首选的数据接收级别  。

要详细了解如何接收和共享应用数据，请参阅[数据重定位设置](../apps/app-protection-policy-settings-ios.md#data-protection)。

有关详细信息，请参阅[如何在 Microsoft Intune 中管理 iOS 应用之间的数据传输](../apps/data-transfer-between-apps-manage-ios.md)。

## <a name="references"></a>参考

如果仍在寻找相关问题的解决方案，或者想要详细了解 Intune，请在 [Microsoft Intune 论坛](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune&filter=alltypes&sort=lastpostdesc)中发布问题。 许多支持工程师、MVP 和开发团队成员会访问该论坛。 因此，这是找到具备你所需信息的人员的好机会。

要打开针对 Microsoft Intune 产品支持团队的支持请求，请参阅[如何获取 Microsoft Intune 支持](../fundamentals/get-support.md)。

要详细了解 Intune 应用保护策略，请参阅以下文章：

- [移动应用程序管理疑难解答](../apps/troubleshoot-mam.md)
- [有关 MAM 和应用保护的常见问题](../apps/mam-faq.md)
- [支持提示：使用本地设备上的日志文件对 Intune 应用保护策略进行故障排除](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Troubleshooting-Intune-app-protection-policy-using/ba-p/330372)

要了解所有最新资讯、信息和技术提示，请访问我们的官方博客：

- [Microsoft Intune 支持团队博客](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess)
- [Microsoft 企业移动性和安全性博客](https://cloudblogs.microsoft.com/enterprisemobility)

## <a name="next-steps"></a>后续步骤

- 有关其他 Intune 疑难解答信息，请参阅[使用疑难解答门户为公司用户提供帮助](../fundamentals/help-desk-operators.md)。 
- 了解 Microsoft Intune 中的任何已知问题。 有关详细信息，请参阅 [Intune 客户成功](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess)。
- 需要更多帮助？ 请参阅[如何获取对 Microsoft Intune 的支持](../fundamentals/get-support.md)。
