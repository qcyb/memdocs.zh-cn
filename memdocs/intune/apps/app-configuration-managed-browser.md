---
title: 使用受策略保护的浏览器管理公司 Web 访问
titleSuffix: Microsoft Intune
description: 使用由 Intune 分配的受策略保护的浏览器管理公司 Web 浏览和 Web 数据传输。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/28/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 1feca24f-9212-4d5d-afa9-7c171c5e8525
ms.reviewer: ilwu
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure, seoapril2019
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0733ac48aa39f611db43164137d129a3248f13d4
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79342811"
---
# <a name="manage-web-access-using-a-microsoft-intune-policy-protected-browser"></a>使用 Microsoft Intune 受策略保护的浏览器管理 Web 访问

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

通过使用受 Intune 策略保护的浏览器（Microsoft Edge 或 Intune Managed Browser），可以确保始终能够安全地访问公司网站。  使用 Intune 进行配置后，受保护的浏览器可以利用以下功能：

- 应用程序保护策略
- 条件性访问
- 单一登录
- 应用程序配置设置
- Azure 应用程序代理集成

> [!IMPORTANT]
> Intune Managed Browser 将停用。 使用 Microsoft Edge 获取受保护的 Intune 浏览器体验。 

## <a name="microsoft-edge-support"></a>Microsoft Edge 支持

可以使用 Microsoft Edge 支持 iOS/iPadOS 和 Android 设备上的企业方案。 Microsoft Edge 将增加对最终用户体验的改进，支持与 Intune Managed Browser 相同的所有管理方案。 Intune 策略启用的以下 Microsoft Edge 企业功能包括：

- **双重标识** - 用户可以同时添加工作帐户以及个人帐户以进行浏览。 两个标识完全独立，这类似于 Office 365 和 Outlook 中的体系结构和体验。 Intune 管理员将能够为工作帐户中受保护的浏览体验设置所需的策略。 
- **Intune 应用保护策略集成** - 管理员现在可以将应用保护策略定向到 Microsoft Edge，包括控制剪切、复制和粘贴，防止执行屏幕捕获，并确保仅在其他托管应用中打开用户选择的链接。
- **Azure 应用程序代理集成** - 管理员可以控制对 SaaS 应用和 Web 应用的访问，帮助确保仅在安全的 Microsoft Edge 浏览器中运行基于浏览器的应用，不论最终用户是从公司网络连接还是从 Internet 连接。 
- **托管收藏夹和主页快捷方式** - 当最终用户处于其企业环境中时，为了便于访问，管理员可以将 URL 设置为显示在收藏夹下。 管理员可以设置主页快捷方式，该快捷方式将在企业用户在 Microsoft Edge 中打开新页面或新选项卡时显示为主快捷方式。

Microsoft Edge 的 Microsoft Intune 保护策略有助于保护组织的数据和资源。 受 Intune 保护的 Microsoft Edge 可确保公司的资源不仅在本机安装的应用中受保护，而且还在通过 Web 浏览器访问时受保护。

## <a name="getting-started"></a>开始使用

Microsoft Edge 和 Intune Managed Browser 是 Web 浏览器应用，你和你的最终用户可以从公共应用商店中下载它以供组织使用。 

浏览器策略的操作系统要求：
- Android 4 及更高版本，或
- iOS/iPadOS 8.0 及更高版本。

早期版本的 Android 和 iOS/iPadOS 将能够继续使用 Managed Browser，但不能安装新版本的应用，并且可能无法访问所有应用功能。 建议将这些设备更新为受支持的操作系统版本。

>[!NOTE]
>Managed Browser 不支持安全套接字层版本 3 (SSLv3) 加密协议。


## <a name="application-protection-policies-for-protected-browsers"></a>受保护浏览器的应用程序保护策略

由于 Microsof Edge 和 Managed Browser 已与 Intune SDK 集成，因此也可以向其应用应用保护策略，包括：
- 控制剪切、复制和粘贴操作的使用。
- 防止发生屏幕捕获。
- 确保仅在托管应用和浏览器中打开公司链接。

有关详细信息，请参阅[什么是应用保护策略？](app-protection-policy.md)

可将这些设置应用于：

- 已向 Intune 注册的设备
- 注册了其他 MDM 产品的设备
- 非托管设备

>[!NOTE]
>如果用户从应用商店中安装了 Managed Browser，并且 Intune 未托管它，则可将其用作基本的 Web 浏览器，其支持通过 Microsoft MyApps 网站进行单一登录。 用户将被直接转到 MyApps 网站，在其中用户可以看到其预配的所有 SaaS 应用程序。
Intune 未托管 Managed Browser 或 Microsof Edge 期间，无法访问由 Intune 托管的其他应用程序中的数据。 


## <a name="conditional-access-for-protected-browsers"></a>受保护浏览器的条件性访问

Managed Browser 现为条件访问的核准客户端应用。 这意味着可以限制移动浏览器访问 Azure AD 连接的 Web 应用（在此只能使用 Managed Browser），防止从其他任何未受保护的浏览器（例如 Safari 或 Chrome）进行访问。 这种保护可应用于 Azure 资源（如 Exchange Online 和 SharePoint Online）、Microsoft 365 管理中心，甚至本地站点（这些站点已通过 [Azure AD 应用程序代理](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started)向外部用户公开）。 

要限制 Azure AD 连接的 Web 应用在移动平台上使用 Intune Managed Browser，可以创建一个需要核准的客户端应用程序的条件访问策略。 

> [!TIP]  
> 条件访问是一项 Azure Active Directory (Azure AD) 技术。 从 Intune 访问的条件访问节点与从 Azure AD 访问的节点相同   。  

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“设备” > “条件访问” > “新建策略”    。
3. 添加策略名称  。 
4. 在“分配”部分，选择“条件” > “客户端应用”    。 随即显示“客户端应用”窗格。 
5. 单击“配置”下的“是”，将策略应用到特定客户端应用   。
6. 确认“浏览器”已被选为客户端应用  。

    ![Azure AD - Managed Browser - 选择客户端应用](./media/app-configuration-managed-browser/managed-browser-conditional-access-02.png)

    > [!NOTE]
    > 若要限制可访问这些云应用程序的本机应用（非浏览器应用），还可以选择“移动应用和桌面客户端”  。

7. 单击“完成”   > “完成”  。
8. 在“分配”部分，选择“用户和组”，然后选择要向其分配此策略的用户或组   。 单击“完成”  以关闭窗格。
9. 在“分配”部分，选择“云应用或操作”，选择要使用此策略保护的应用   。 单击“完成”  以关闭窗格。
10. 从窗格的“访问控制”部分选择“授予”   。 
11. 单击“授予访问权限”  ，然后单击“需要已批准的客户端应用”  。 
12. 在“授予”窗格上单击“选择”   。 必须将此策略分配给希望只由 Intune Managed Browser 应用访问的云应用。

    ![Azure AD - Managed Browser 条件访问策略](./media/app-configuration-managed-browser/managed-browser-conditional-access-01.png)



配置以上策略后，会强制要求用户使用 Intune Managed Browser 访问已通过此策略保护的 Azure AD 连接的 Web 应用。 如果用户尝试在此方案中使用非管理的浏览器，用户会看到一则通知，指示必须改用 Intune Managed Browser。

Managed Browser 不支持经典条件访问策略。 有关详细信息，请参阅[在 Azure 门户中迁移经典策略](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-migration)。

## <a name="single-sign-on-to-azure-ad-connected-web-apps-in-policy-protected-browsers"></a>在受策略保护的浏览器中单一登录到 Azure AD 连接的 Web 应用

iOS/iPadOS 和 Android 上的 Microsoft Edge 和 Intune Managed Browser 可利用到 Azure AD 连接的所有 Web 应用（SaaS 和本地）的 SSO。 Microsoft Authenticator 应用存在于 iOS/iPadOS 上，或存在于 Android 上的 Intune 公司门户应用上时，受策略保护的浏览器的用户将能够访问 Azure AD 连接的 Web 应用，而不必重新输入其凭据。

SSO 要求使用 iOS/iPadOS 上的 Microsoft Authenticator 应用或 Android 上的 Intune 公司门户对设备进行注册。 如果 Authenticator 应用或 Intune 公司门户的用户的设备尚未由其他应用程序注册，用户在受策略保护的浏览器中导航到一个 Azure AD 连接的 Web 应用时，系统会提示他们注册其设备。 使用 Intune 管理的帐户注册设备后，该帐户将为 Azure AD 连接的 Web 应用启用 SSO。 

> [!NOTE]
> 设备注册是 Azure AD 服务的简单签入。 不需要完整的设备注册，并且不会向 IT 提供设备上的任何其他权限。

## <a name="create-a-protected-browser-app-configuration"></a>创建受保护的浏览器应用配置

>[!IMPORTANT]
>对于要应用的应用配置，用户的受保护浏览器或设备上的其他应用必须已由 [Intune 应用保护策略](app-protection-policy.md)托管。

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“应用”   > “应用配置策略”   > “添加”   > “托管应用”  。
3. 在“创建应用配置策略”窗格的“基本信息”页上，输入应用配置设置的“名称”和可选“描述”     。
4. 选择“选择公共应用”  ，然后选择适用于 iOS/iPadOS 或适用于 Android（或适用于两者）的“Managed Browser”  和/或“Edge”  。
5. 单击“选择”  以返回到“创建应用配置策略”  窗格。
6. 单击“下一步”以显示“设置”页面   。
7. 在“设置”  页面上，定义键值对以为应用提供配置。 请参阅本文的后续部分，了解可以定义的不同键值对。
8. 单击“下一步”  以显示“分配”  页，然后单击“选择要包括的组”  和/或“选择要排除的组”  。
9. 单击“下一步”  以显示“查看 + 创建”页  。
10. 查看应用配置策略后，单击“创建”  。

创建新配置后，其显示在“应用配置策略”  窗格上。


## <a name="assign-the-configuration-settings-you-created"></a>分配已创建的配置设置

将这些设置分配到 Azure AD 用户组。 如果用户安装了受保护的目标浏览器应用，则应用将按指定的设置进行管理。

1. 在 Intune 移动应用程序管理仪表板的“应用”窗格上，选择“应用配置策略”   。
2. 在应用配置列表中，选择一个想要分配的配置。
3. 在下一个窗格上，选择“分配”  。
4. 在“分配”窗格上，选择想要将应用配置分配到的 Azure AD 组，然后选择“确定”   。

## <a name="how-to-set-microsoft-edge-as-the-protected-browser-for-your-organization"></a>如何将 Microsoft Edge 设置为组织的受保护的浏览器

此设置允许配置将用户转到 Microsoft Edge 还是 Intune Managed Browser（假设应用保护策略同时面向这两个浏览器）。 **此应用程序配置策略设置应面向打开 Web 链接的 Intune 托管的应用。** 

如果将此设置设为“True”：

- 从此设置面向的 Intune 托管应用打开链接时，会将用户转到 Microsoft Edge。 
- 若用户还没有安装此应用，则无论用户是否已下载 Intune Managed Browser，都会提示用户从应用商店下载 Microsoft Edge。

如果将此设置设为“False”：

- 如果用户已同时下载 Managed Browser 和 Microsoft Edge，则会启动 Managed Browser。  
- 如果用户已下载 Managed Browser 或 Microsoft Edge，则会启动相应的浏览器应用。   
- 若用户未下载这两种浏览器应用，将提示用户下载 Managed Browser。

使用上面的过程创建 Microsoft Edge 应用配置。 从“配置”窗格上选择“配置设置”时，提供以下键值对（步骤 9）：  

| Key                              |  值   |
|----------------------------------|----------|
| **com.microsoft.intune.useEdge** | true  |

> [!NOTE]
> 在管理 Microsoft Edge 和应用配置指定的关联应用的应用保护策略中，确保设置了以下数据保护策略设置：
> - 将组织数据发送到其他应用：**策略托管应用**
> - 限制使用其他应用传输 Web 内容：**策略托管浏览器**

## <a name="how-to-configure-application-proxy-settings-for-protected-browsers"></a>如何为受保护的浏览器配置应用程序代理设置

可将 Microsoft Edge、Intune Managed Browser 和 [Azure AD 应用程序代理]( https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started)配合使用，以支持 iOS/iPadOS 和 Android 设备用户实现以下方案：

- 用户下载并登录到 Microsoft Outlook 应用。 将自动应用 Intune 应用保护策略。 它们对保存的数据进行加密，并阻止用户将公司文件传输到设备上的非托管应用或位置。 当用户接下来单击 Outlook 中 Intranet 站点的链接时，可以指定在受保护的浏览器应用程序中而不是在另一个浏览器中打开链接。 受保护的浏览器识别出这个 Intranet 站点已通过应用程序代理向用户公开。 将通过应用程序代理对用户进行自动路由，以便在进入 Intranet 站点前进行任何适用的多重身份验证和条件性访问。 之前在用户处于远程访问状态时，可能找不到该站点，现在用户可正常访问该网站且 Outlook 中的链接也按预期工作。
- 远程用户打开受保护的浏览器应用程序，并使用内部 URL 导航到 Intranet 站点。 受保护的浏览器识别出这个 Intranet 站点已通过应用程序代理向用户公开。 将通过应用程序代理对用户进行自动路由，以便在进入 Intranet 站点前进行任何适用的多重身份验证和条件性访问。 之前在用户处于远程访问状态时，可能找不到该站点，现在用户可正常访问。

### <a name="before-you-start"></a>开始之前

- 通过 Azure AD 应用程序代理设置内部应用程序。
  - 要配置应用程序代理和发布应用程序，请参阅[设置文档](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy)。 
  - [必须向重定向针对的企业应用程序分配用户](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy-add-on-premises-application#add-a-user-for-testing)。 即使将应用程序的预身份验证设置为直通模式，以及即使已在应用程序代理设置中禁用用户分配要求，也必须执行此操作。
- 必须使用 Managed Browser 应用的最低版本 1.2.0。
- Managed Browser 或 Microsof Edge 应用的用户具有分配给该应用的 [Intune 应用保护策略](app-protection-policy.md)。

    > [!NOTE]
    > 更新的应用程序代理重定向数据最长可能需要 24 小时才能在 Managed Browser 和 Microsoft Edge 中生效。


#### <a name="step-1-enable-automatic-redirection-to-a-protected-browser-from-outlook"></a>步骤 1：从 Outlook 启用指向受保护的浏览器的自动重定向
Outlook 必须配置可启用**将 Web 内容限制为仅在 Managed Browser 中显示**这一设置的应用保护策略。

#### <a name="step-2-assign-an-app-configuration-policy-assigned-for-the-protected-browser"></a>步骤 2:为受保护的浏览器分配一个应用配置策略
此过程将 Managed Browser 或 Microsof Edge 应用配置为使用应用代理重定向。 

在策略的配置设置中打开“Edge”选项卡，为应用程序代理重定向值选择“启用”。   启用此设置时，用户即可以访问通过 Azure 应用程序代理发布的公司链接和本地 Web 应用。

若要深入了解 Managed Browser、Microsoft Edge 和 Azure AD 应用程序代理如何相继配合使用，以实现本地 Web 应用的无缝（和受保护）访问，请参阅“企业移动性 + 安全性”博客文章[更好地协作：配合使用 Intune 和 Azure Active Directory，改善用户访问](https://cloudblogs.microsoft.com/enterprisemobility/2017/07/06/better-together-intune-and-azure-active-directory-team-up-to-improve-user-access)。

## <a name="how-to-configure-the-homepage-for-a-protected-browser"></a>如何配置受保护浏览器的主页

使用此设置可配置用户启动受保护的浏览器或创建新选项卡时看到的主页。 
- 此设置将在 Managed Browser 中显示网页。  Edge 将改为显示主页快捷方式。
- 主页快捷方式图标显示为搜索控件下的图标。  无法对其进行编辑或删除。
- 主页快捷方式将显示组织的名称以便进行区分。  它将始终显示为第一个图标。

使用该过程创建 Microsoft Edge 或 Managed Browser 应用配置，提供以下键值对：

|                                Key                                |                                                           值                                                            |
|-------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
| <strong>com.microsoft.intune.mam.managedbrowser.homepage</strong> | 指定有效 URL。 将阻止错误的 URL，这是一项安全措施。<br>示例：`https://www.bing.com` |

## <a name="how-to-configure-bookmarks-for-a-protected-browser"></a>如何配置受保护的浏览器的书签

使用此设置可配置一组可供 Microsoft Edge 或 Managed Browser 用户使用的书签。

- 用户无法删除或修改这些书签
- 这些书签显示在列表顶部。 用户创建的任何书签都会显示在这些书签下方。
- 如果已启用应用代理重定向，可以使用应用代理 Web 应用的内部或外部 URL 添加应用。

使用该过程创建 Microsoft Edge 或 Managed Browser 应用配置，提供以下键值对：

|                                Key                                 |                                                                                                                                                                                                                                                         值                                                                                                                                                                                                                                                          |
|--------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <strong>com.microsoft.intune.mam.managedbrowser.bookmarks</strong> | 此配置的值是一个书签列表。 每个书签都由书签标题和书签 URL 组成。 用字符 <strong>&#124;</strong> 分隔标题和 URL。<br><br>例如：<br> <code>Microsoft Bing&#124;https://www.bing.com</code><br><br>若要配置多个书签，可使用双字符 <strong>&#124;&#124;</strong> 分隔每对书签<br><br>例如：<br> <code>Bing&#124;https://www.bing.com&#124;&#124;Contoso&#124;https://www.contoso.com</code> |

## <a name="how-to-specify-allowed-and-blocked-urls-for-a-protected-browser"></a>如何为受保护的浏览器指定允许和阻止的 URL

使用该过程创建 Microsoft Edge 或 Managed Browser 应用配置，提供以下键值对：

|Key|值|
|-|-|
|选择：<br><ul><li>指定允许的 URL（仅允许这些 URL；无法访问其他站点）：<br> com.microsoft.intune.mam.managedbrowser.AllowListURLs <br><br></li><li>指定阻止的 URL（可访问其他所有站点）：<br>**com.microsoft.intune.mam.managedbrowser.BlockListURLs**</li></ul>|键的对应值是 URL 列表。 将所有要允许或阻止的 URL 输入为单个值，以管道字符 **&#124;** 分隔。<br><br>例如：<br><br><code>URL1&#124;URL2&#124;URL3</code><br><code>http://*.contoso.com/*&#124;https://*.bing.com/*&#124;https://expenses.contoso.com</code>|

>[!IMPORTANT]
>不要同时指定这两个键。 如果两个键同时针对同一个用户，则使用允许键，因为它是限制性最强的选项。
>此外，务必不要阻止重要的页面，例如你的公司网站。

### <a name="url-format-for-allowed-and-blocked-urls"></a>允许的 URL 和阻止的 URL 的格式
使用以下信息来了解有关指定允许和阻止列表中的 URL 时允许使用的格式和通配符：

- 可以根据以下允许模式列表中的规则使用通配符 ( **&#42;** )：

- 在将 URL 输入列表时，确保对所有 URL 添加 **“http”** 或 **“https”** 作为前缀。

- 可以在地址中指定端口号。 如果未指定端口号，则使用以下值：

  - 对于 http，使用端口 80

  - 对于 https，使用端口 443

  不支持对端口号使用通配符。 例如，不支持 `http://www.contoso.com:;` 和 `http://www.contoso.com: /;`。

- 使用下表了解指定 URL 时可以使用的允许模式：

|                  URL                  |                     详细信息                      |                                                匹配                                                |                                不匹配                                 |
|---------------------------------------|--------------------------------------------------|-------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------|
|        `http://www.contoso.com`         |              匹配单个页面               |                                            `www.contoso.com`                                            |  `host.contoso.com`<br /><br />`www.contoso.com/images`<br /><br />`contoso.com`/   |
|          `http://contoso.com`           |              匹配单个页面               |                                             `contoso.com/`                                              | `host.contoso.com`<br /><br />`www.contoso.com/images`<br /><br />`www.contoso.com` |
|    `http://www.contoso.com/&#42;`     | 匹配以 `www.contoso.com` 开头的所有 URL |      `www.contoso.com`<br /><br />`www.contoso.com/images`<br /><br />`www.contoso.com/videos/tvshows`      |              `host.contoso.com`<br /><br />`host.contoso.com/images`              |
|    `http://*.contoso.com/*`     |     匹配 contoso.com 下的所有子域     | `developer.contoso.com/resources`<br /><br />`news.contoso.com/images`<br /><br />`news.contoso.com/videos` |                               `contoso.host.com`                                |
|     `http://www.contoso.com/images`     |             匹配单个文件夹              |                                        `www.contoso.com/images`                                         |                          `www.contoso.com/images/dogs`                          |
|       `http://www.contoso.com:80`       |  匹配单个页面（使用端口号）   |                                       `http://www.contoso.com:80`                                       |                                                                               |
|        `https://www.contoso.com`        |          匹配单个安全页面           |                                        `https://www.contoso.com`                                        |                            `http://www.contoso.com`                             |
| `http://www.contoso.com/images/&#42;` |    匹配单个文件夹和所有子文件夹    |                  `www.contoso.com/images/dogs`<br /><br />`www.contoso.com/images/cats`                   |                            `www.contoso.com/videos`                             |

- 以下是一些你不能指定的输入的示例：

  - `*.com`

  - `*.contoso/*`

  - `www.contoso.com/*images`

  - `www.contoso.com/*images*pigs`

  - `www.contoso.com/page*`

  - IP 地址

  - `https://*`

  - `http://*`

  - `http://www.contoso.com:*`

  - `http://www.contoso.com: /*`
  
## <a name="soft-transitions-from-work-to-personal-accounts"></a>从工作帐户软转换到个人帐户

双重标识模型是 Microsoft Edge 移动设备企业体验的支柱，即 Microsoft Edge 同时支持工作和个人标识。 与 Office 365 和 Outlook 应用一样，此双重标识模型允许最终用户使用 Microsoft Edge 完成所有的浏览需求，并可以根据管理员定义的内容策略在两种体验之间轻松转换。 Microsoft Edge 不会影响在个人上下文中进行浏览，它会将公司信息完全包含到工作上下文。 

用户尝试打开指向组织不允许的站点的链接时（如报刊文章等），他们可以在完全独立于工作上下文的个人上下文中完成此操作，这是此模型的优势之一。 默认情况下会启用这些软转换。 

使用该过程创建 Microsoft Edge 或 Managed Browser 应用配置，提供以下键值对：

| Key                                                                | 值                                                 |
|--------------------------------------------------------------------|-------------------------------------------------------|
| **com.microsoft.intune.mam.managedbrowser.AllowTransitionOnBlock** | False 将阻止这些软转换发生  |

## <a name="how-to-access-to-managed-app-logs-using-the-managed-browser-on-ios"></a>如何在 iOS 上使用 Managed Browser 访问托管应用日志

在 iOS/iPadOS 设备上安装了 Managed Browser 的最终用户可查看所有 Microsoft 已发布应用的管理状态。 他们还可针对托管 iOS/iPadOS 应用的疑难问题发送日志。

1. 打开 iOS/iPadOS 设置  。
2. 选择托管的“Browser”应用程序设置  。
3. 切换“启用 Intune 诊断”，以便在疑难解答模式中设置浏览器  。
4. 打开托管的“Browser”  。 单击“查看 Intune 应用状态”以查看各个应用程序策略设置  。
5. 按“开始”和“共享日志”或“向 Microsoft 发送日志”，向 IT 管理员或 Microsoft 发送疑难解答日志    。

还可以在应用中以疑难解答模式打开 Browser。

1. 打开 Managed Browser。
2. 在地址框中键入 `about:intunehelp`。
Browser 将启动疑难解答模式。

对于应用日志中存储的设置列表，请参阅[在 Managed Browser 中查看应用保护日志](app-protection-policy-settings-log.md)。

## <a name="security-and-privacy-for-the-managed-browser"></a>Managed Browser 的安全和隐私

- Managed Browser 不使用用户在设备上对内置浏览器进行的设置。 Managed Browser 无法访问这些设置。

- 如果配置与 Managed Browser 关联的一个应用保护策略中的选项**访问需要简单 PIN** 或**访问需要公司凭据**，且用户选择了身份验证页面上的帮助链接，那么无论是否已将这些用户添加到策略中的阻止列表中，他们都可以浏览任何 Internet 站点。

- Managed Browser 仅能在直接访问站点时阻止访问。 使用中间服务（例如翻译服务）访问站点时，该策略则不会阻止访问。

- 在判断是否允许通过身份验证和访问 Intune 文档时， **&#42;.microsoft.com** 不在允许或阻止列表设置的约束范围之内。 始终允许。

### <a name="turn-off-usage-data"></a>关闭用法数据
Microsoft 会自动收集有关性能和 Managed Browser 使用情况的匿名数据，以改进 Microsoft 产品和服务。 用户可通过使用设备上的**用法数据**设置关闭数据收集。 不具有对此数据的收集的控制。

- 在 iOS/iPadOS 设备上，如果用户访问的网站的证书已过期或不受信任，则无法打开该网站。

## <a name="next-steps"></a>后续步骤

- [什么是应用保护策略？](app-protection-policy.md) 
