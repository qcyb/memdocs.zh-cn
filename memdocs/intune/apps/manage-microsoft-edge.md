---
title: 通过 Intune 管理适用于 iOS 和 Android 的 Microsoft Edge
titleSuffix: ''
description: 结合使用 Intune 应用保护策略和 Microsoft Edge，确保公司的网站始终在安全措施到位的情况下被访问。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/19/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 3fb2f050-ec94-42ab-be05-c3d4101148bb
ms.reviewer: ilwu
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b25d5439aa9d0842cbbee24b5e8759d00f371d4b
ms.sourcegitcommit: e2877d21dfd70c4029c247275fa2b38e76bd22b8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/31/2020
ms.locfileid: "80407723"
---
# <a name="manage-web-access-by-using-microsoft-edge-with-microsoft-intune"></a>结合使用 Microsoft Edge 和 Microsoft Intune 来管理 Web 访问

将 Intune 应用保护策略和 Microsoft Edge 结合使用，可帮助确保始终在具有足够安全措施的情况下访问公司网站。 提供了 Intune 策略启用的以下 Microsoft Edge 企业功能：

- **双重标识。** 用户可以同时添加工作帐户以及个人帐户以进行浏览。 两个标识完全独立，这类似于 Office 365 和 Outlook 中的体系结构和体验。 Intune 管理员可以为工作帐户中受保护的浏览体验设置所需的策略。
- **Intune 应用保护策略集成。** 由于 Microsoft Edge 已与 Intune SDK 集成，因此可以针对性地使用应用保护策略，防止数据丢失。 这些功能包括控制剪切、复制和粘贴，阻止屏幕捕获，以及确保用户选择的链接仅在其他托管应用中打开。
- **Azure 应用程序代理集成。** 可控制对软件即服务 (SaaS) 应用和 Web 应用的访问。 这有助于确保仅在安全的 Microsoft Edge 浏览器中运行基于浏览器的应用，不论最终用户是从公司网络连接还是从 Internet 连接。
- **应用程序配置。** 可利用应用程序配置设置来加强组织的安全状况，并为最终用户配置易用功能。 例如，可定义书签、主页快捷方式、允许或阻止的站点和 Azure Active Directory (Azure AD) 应用程序代理。

Microsoft Edge 的 Microsoft Intune 保护策略有助于保护组织的数据和资源。 结合使用这些策略和 Microsoft Edge，可确保公司的资源不仅在本机安装的应用中受保护，而且还在通过 Web 浏览器访问时受保护。

## <a name="getting-started"></a>开始使用

你与你的最终用户可从公共应用商店下载 Microsoft Edge 供组织使用。 浏览器策略的操作系统要求如下：
- Android 4 及更高版本
- iOS 8.0 及更高版本

## <a name="application-protection-policies-for-microsoft-edge"></a>Microsoft Edge 的应用程序保护策略

由于 Microsoft Edge 已与 Intune SDK 集成，因此你可向其应用应用保护策略。

可将这些设置应用于：
- 已注册 Intune 的设备。
- 已注册其他移动设备管理产品的设备。
- 非托管设备。

如果 Microsoft Edge 不是 Intune 策略的目标，用户就无法使用它来访问其他 Intune 托管应用程序（如 Office 应用）中的数据。 

   >[!NOTE]
   > 应用另存为策略以阻止下载图像时，为 Microsoft Edge 禁用长按。

## <a name="conditional-access-for-microsoft-edge"></a>Microsoft Edge 的条件访问

可使用 Azure AD 条件访问重定向用户，使其只能通过 Microsoft Edge 访问公司内容。 这将移动浏览器对 Azure AD 连接的 Web 应用的访问限制为受策略保护的 Microsoft Edge。 这会阻止从任何其他未受保护的浏览器（例如 Safari 或 Chrome）进行访问。 可以将条件访问应用于 Azure 资源（如 Exchange Online 和 SharePoint Online）、Microsoft 365 管理中心，甚至本地站点（这些站点已通过 [Azure AD 应用程序代理](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started)向外部用户公开）。

> [!NOTE]
> 如果需要在 iOS 设备上受保护的浏览器中打开新 Web 剪辑（固定的 Web 应用），将在 Microsoft Edge（而不是在 Intune Managed Browser 中）打开它们。 对于较旧的 iOS Web 剪辑，必须重定向这些 Web 剪辑，以确保它们在 Microsoft Edge 而不是 Managed Browser 中打开。

若要将 Azure AD 连接的 Web 应用限制为在 iOS 和 Android 上使用 Microsoft Edge，请执行以下操作：
1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 在 Intune 节点下，选择“条件访问”   > “新建策略”  。
3. 从窗格的“访问控制”部分选择“授予”   。
4. 选择“需要已批准的客户端应用”  。
5. 在“授予”窗格上选择“选择”   。 必须将此策略分配给希望只由 Intune Managed Browser 应用访问的云应用。

    ![条件访问策略的屏幕截图 - 授予](./media/manage-microsoft-edge/manage-microsoft-edge-01.png)

6. 在“分配”部分，选择“条件” > “应用”   。 此时将显示“应用”  窗格。
7. 在“配置”下选择“是”，将策略应用到特定客户端应用   。
8. 确认“浏览器”已被选为客户端应用  。

    ![条件访问策略的屏幕截图 - 选择客户端应用](./media/manage-microsoft-edge/manage-microsoft-edge-02.png)

    > [!NOTE]
    > 若要限制可访问这些云应用程序的本机应用（非浏览器应用），还可以选择“移动应用和桌面客户端”  。

9. 在“分配”部分，选择“用户和组”，然后选择要向其分配此策略的用户或组   。

10. 在“分配”部分，选择“云应用”，选择要使用此策略保护的应用   。

配置以上策略后，会强制要求用户使用 Microsoft Edge 访问已通过此策略保护的 Azure AD 连接的 Web 应用。 如果用户尝试在此情况下使用非托管浏览器，他们会收到一条消息，指示他们必须使用 Microsoft Edge。

> [!TIP]
> 条件访问是一项 Azure AD 技术。 从 Intune 访问的条件访问节点与从 Azure AD 访问的节点相同。

## <a name="single-sign-on-to-azure-ad-connected-web-apps-in-policy-protected-browsers"></a>在受策略保护的浏览器中单一登录到 Azure AD 连接的 Web 应用

iOS 和 Android 上的 Microsoft Edge 可利用到 Azure AD 连接的所有 Web 应用（SaaS 和本地）的单一登录 (SSO)。 SSO 允许用户通过 Microsoft Edge 访问 Azure AD 连接的 Web 应用，而无需重新输入其凭据。

SSO 要求设备通过 Microsoft Authenticator 应用（iOS 设备）或 Intune 公司门户（Android）进行注册。 当用户具有这两个选项之一时，系统会提示他们在转到受策略保护的浏览器中的 Azure AD 连接的 Web 应用时注册其设备。 （这仅在设备尚未注册时适用。）使用 Intune 管理的用户帐户注册设备后，该帐户已为 Azure AD 连接的 Web 应用启用 SSO。

> [!NOTE]
> 设备注册是 Azure AD 服务的简单签入。 不需要完整的设备注册，并且不会向 IT 提供设备上的任何其他权限。

## <a name="create-a-protected-browser-app-configuration"></a>创建受保护的浏览器应用配置

若要创建适用于 Microsoft Edge 的应用配置，请执行以下操作：

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“应用”   > “应用配置策略”   > “添加”  。
3. 在“添加配置策略”窗格上，输入应用配置设置的“名称”和可选“描述”    。
4. 对于“设备注册”类型，选择“托管应用”   。
5. 选择“选择所需应用”  。 然后在“目标应用”窗格上，选择适用于 iOS/iPadOS 或适用于 Android（或适用于两者）的“Managed Browser”或“Microsoft Edge”    。
6. 选择“确定”，返回到“添加配置策略”窗格   。
7. 选择“配置设置”  。 在“配置”  窗格上，定义键值对来为 Microsoft Edge 提供配置。 请参阅本文的后续部分，了解可以定义的不同键值对。

    > [!NOTE]
    > Microsoft Edge 使用与 Managed Browser 相同的键值对。 在 Android 上，Microsoft Edge 必须以应用保护策略为目标才能使应用配置策略生效。

8. 完成后，选择“确定”  。
9. 在“添加配置策略”窗格上，选择“添加”   。<br>
    创建新配置后，其显示在“应用配置”  窗格上。

## <a name="assign-the-configuration-settings-you-created"></a>分配已创建的配置设置 

将这些设置分配给 Azure AD 用户组。 如果用户安装了受保护的目标浏览器应用，则应用将按指定的设置进行管理。

1. 在 Intune 移动应用程序管理仪表板的“应用”窗格上，选择“应用配置策略”   。
2. 在应用配置列表中，选择一个想要分配的配置。
3. 在下一个窗格上，选择“分配”  。
4. 在“分配”窗格上，选择想要向其分配应用配置的 Azure AD 组，然后选择“确定”   。

## <a name="direct-users-to-microsoft-edge-instead-of-the-intune-managed-browser"></a>将用户定向到 Microsoft Edge，而不是 Intune Managed Browser 

Intune Managed Browser 和 Microsoft Edge 都可用作受策略保护的浏览器。 为引导用户使用正确的浏览器应用，请使用以下配置设置将所有 Intune 托管应用（例如 Outlook、OneDrive 和 SharePoint）设为目标：

|    Key    |    值    |
|------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
|    `com.microsoft.intune.useEdge`    |    值 `true` 将引导用户下载和使用 Microsoft Edge。<br>值 `false` 将引导用户使用 Intune Managed Browser。    |

如果未设置此应用配置值，以下逻辑将定义打开企业链接所使用的浏览器。 

在 Android 上：
- 如果用户已在设备上同时下载 Intune Managed Browser 和 Microsoft Edge，则会启动 Intune Managed Browser。 
- 如果设备上只下载了 Microsoft Edge，并且针对的是 Intune 策略，则会启动 Microsoft Edge。
- 如果设备上只有 Managed Browser 且针对的是 Intune 策略，则会启动 Managed Browser。

在 iOS/iPadOS 上，适用于已集成 Intune SDK for iOS v 的应用。 9.0.9+ 的 Intune SDK 的应用：
- 如果设备上同时存在 Managed Browser 和 Microsoft Edge，则会启动 Intune Managed Browser。  
- 如果设备上只有 Microsoft Edge，并且针对的是 Intune 策略，则会启动 Microsoft Edge。
- 如果设备上只有 Managed Browser 且针对的是 Intune 策略，则会启动 Managed Browser。

## <a name="configure-application-proxy-settings-for-microsoft-edge"></a>为 Microsoft Edge 配置应用程序代理设置

可以将 Microsoft Edge 和 [Azure AD 应用程序代理](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started)一起使用，使用户能够在其移动设备上访问 Intranet 站点。 

以下是 Azure AD 应用程序代理支持的一些场景示例： 

- 一个用户使用受 Intune 保护的 Outlook 移动应用。 然后，该用户单击电子邮件中的一个指向 Intranet 站点的链接，Microsoft Edge 识别出该站点已通过应用程序代理向用户公开。 将通过应用程序代理对用户进行自动路由，以便在进入 Intranet 站点前进行任何适用的多重身份验证和条件性访问。 该用户现在甚至可以在其移动设备上访问内部网站，而 Outlook 中的链接也如预期一样正常运行。
- 用户在其 iOS 或 Android 设备上打开 Microsoft Edge。 如果 Microsoft Edge 受 Intune 保护，并且应用程序代理已启用，则用户可使用其习惯使用的内部 URL 转到 Intranet 站点。 Microsoft Edge 识别出这个 Intranet 站点已通过应用程序代理向用户公开。 通过应用程序代理自动对用户进行路由，以便在访问 Intranet 站点前进行身份验证。 

### <a name="before-you-start"></a>开始之前

- 通过 Azure AD 应用程序代理设置内部应用程序。
  - 要配置应用程序代理和发布应用程序，请参阅[设置文档](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy)。
- Microsoft Edge 应用必须分配 [Intune 应用保护策略](app-protection-policy.md)。

> [!NOTE]
> 更新的应用程序代理重定向数据最长可能需要 24 小时才能在 Managed Browser 和 Microsoft Edge 中生效。

#### <a name="step-1-enable-automatic-redirection-to-microsoft-edge-from-outlook"></a>步骤 1：从 Outlook 启用指向 Microsoft Edge 的自动重定向
为 Outlook 配置应用保护策略，该策略启用“使用策略托管浏览器共享 Web 内容”  设置。

![应用保护策略的屏幕截图 - 使用策略托管浏览器共享 Web 内容](./media/manage-microsoft-edge/manage-microsoft-edge-03.png)

#### <a name="step-2-set-the-app-configuration-setting-to-enable-app-proxy"></a>步骤 2:设置应用配置设置以启用应用代理
使用以下键/值对将 Microsoft Edge 作为目标，为 Microsoft Edge 启用应用程序代理：

|    Key    |    值    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.AppProxyRedirection    |    是    |

若要深入了解 Microsoft Edge 和 Azure AD 应用程序代理如何相继配合使用，以实现本地 Web 应用的无缝（和受保护）访问，请参阅[更好地协作：配合使用 Intune 和 Azure Active Directory，改善用户访问](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/better-together-intune-and-azure-active-directory-team-up-to/ba-p/250254)。 此博客文章参考了 Intune Managed Browser，但该内容也适用于 Microsoft Edge。

## <a name="configure-a-homepage-shortcut-for-microsoft-edge"></a>为 Microsoft Edge 配置主页快捷方式

通过此设置可为 Microsoft Edge 配置主页快捷方式。 用户在 Microsoft Edge 中打开一个新选项卡时，配置的主页快捷方式将显示为搜索栏下的第一个图标。 用户无法在其托管上下文中编辑或删除此快捷方式。 主页快捷方式将显示组织的名称以便进行区分。 

使用以下键/值对来配置主页快捷方式：

|    Key    |    值    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.homepage   |    指定有效 URL。 将阻止错误的 URL，这是一项安全措施。<br>示例：   <`https://www.bing.com`>     |

## <a name="configure-multiple-top-site-shortcuts-for-new-tab-pages-in-microsoft-edge"></a>为 Microsoft Edge 中的新选项卡页配置多个顶级网站快捷方式 
与配置主页快捷方式类似，你可以在 Microsoft Edge 的新选项卡页上配置多个顶级网站快捷方式。 用户无法在其托管上下文中编辑或删除此快捷方式。 注意：可以配置总共 8 个快捷方式，包括主页快捷方式。 如果已配置主页快捷方式，则该快捷方式会替代配置的第一个首要网站。 

|    Key    |    值    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.managedTopSites   |    指定一组 URL 的值。 每个顶级网站快捷方式都由标题和 URL 组成。 用字符 `|` 分隔标题和 URL。 例如： <br> `GitHub | https://github.com/||LinkedIn|https://www.linkedin.com`    |

## <a name="configure-your-organizations-logo-and-brand-color-for-new-tab-pages-in-microsoft-edge"></a>为 Microsoft Edge 中的新标签页配置组织徽标和品牌颜色

通过这些设置，可以将 Microsoft Edge 的新标签页自定义为，显示组织徽标和品牌颜色作为标签页背景。

若要上传组织徽标和品牌颜色，请先完成以下步骤：
- 在 Azure 门户中，导航到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)  -> “租户管理” -> “自定义” -> “公司标识品牌”    。
- 若要设置品牌徽标，请选择“显示”下的“仅公司徽标”。 建议使用透明背景徽标。 
- 若要设置品牌背景色，请选择“显示”下的“主题颜色”。 Microsoft Edge 在新标签页上应用较浅的颜色底纹，这可确保标签页的高可读性。 

接下来，使用以下键/值对将组织品牌拉取到 Microsoft Edge 中：

|    Key    |    值    |
|--------------------------------------------------------------------|------------|
|    com.microsoft.intune.mam.managedbrowser.NewTabPage.BrandLogo    |    True    |
|    com.microsoft.intune.mam.managedbrowser.NewTabPage.BrandColor    |    True    |

## <a name="display-relevant-industry-news-on-new-tab-pages"></a>在新选项卡页上显示相关行业新闻

可以在 Microsoft Edge 移动中配置新选项卡页体验，以便显示与组织相关的行业新闻。 启用此功能时，Microsoft Edge 移动将使用组织域名聚合来自 Web 的有关组织、组织行业和竞争者的新闻，因此用户可以从 Microsoft Edge 集中的选项卡页查找相关外部新闻。 默认情况下，行业新闻处于关闭状态，可以使用它为组织选择加入它。 

|    Key    |    值    |
|------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.NewTabPage.IndustryNews    |    如果为 true，  将在 Microsoft Edge 移动版“新选项卡”页上显示行业新闻。<p>False  （默认值）将从新选项卡页隐藏行业新闻。    |

## <a name="configure-managed-bookmarks-for-microsoft-edge"></a>为 Microsoft Edge 配置托管书签

为了便于访问，可配置希望用户在使用 Microsoft Edge 时可用的书签。 

下面是一些详细信息：

- 这些书签仅在用户使用 Microsoft Edge 的[企业模式](https://docs.microsoft.com/intune/apps/app-configuration-managed-browser#how-to-configure-bookmarks-for-a-protected-browser)时才会显示。 
- 用户无法删除或修改这些书签。
- 这些书签显示在列表顶部。 用户创建的任何书签显示在这些书签下方。
- 如果已启用应用程序代理重定向，可以使用应用程序代理 Web 应用的内部或外部 URL 添加这些 Web 应用。
- 在将 URL 输入列表时，确保对所有 URL 添加“http://”  或“https://”  作为前缀。

使用以下键/值对来配置托管书签：

|    Key    |    值    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.bookmarks    |    此配置的值是一个书签列表。 每个书签都由书签标题和书签 URL 组成。 用字符 `|` 分隔标题和 URL。      例如：<br>`Microsoft Bing|https://www.bing.com`<br>若要配置多个书签，可使用双字符 `||` 分隔每对书签。<p>例如：<br>`Microsoft Bing|https://www.bing.com||Contoso|https://www.contoso.com`    |

## <a name="display-myapps-within-microsoft-edge-bookmarks"></a>在 Microsoft Edge 书签内显示 MyApps

默认情况下，用户可在 Microsoft Edge 书签内的某个文件夹中看到为他们配置的 MyApps 站点。 该文件夹标有组织的名称。

|    Key    |    值    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.MyApps    |    **true**：在 Microsoft Edge 书签内显示 MyApps。<p>**False**：在 Microsoft Edge 书签内隐藏 MyApps。    |
    
## <a name="use-https-protocol-as-default"></a>使用 HTTPS 协议作为默认值

当用户未指定时，可以将 Microsoft Edge mobile 配置为默认使用 HTTPS 协议。 通常，这被视为最佳做法。 使用以下键/值对启用 HTTPS 作为默认协议：

|    Key    |    值    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    `com.microsoft.intune.mam.managedbrowser.defaultHTTPS`     |     **true**：将默认协议设置为使用 HTTPS     |


## <a name="specify-allowed-or-blocked-sites-list-for-microsoft-edge"></a>为 Microsoft Edge 指定允许或阻止的站点列表
可使用应用配置来定义用户在使用其工作配置文件时可访问的站点。 如果使用允许列表，用户只能访问已显式列出的站点。 如果使用阻止列表，用户可以访问除已显式阻止的站点以外的所有站点。 应仅使用一个允许列表或一个阻止列表，而不能同时使用两者。 如果同时使用两者，将遵循允许列表。  

使用以下键/值对为 Microsoft Edge 配置一个允许或阻止站点列表。 

|    Key    |    值    |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    选择：<p>1.指定允许的 URL（仅允许这些 URL；无法访问其他站点）：<br>`com.microsoft.intune.mam.managedbrowser.AllowListURLs`<p>2.指定阻止的 URL（可访问其他所有站点）：<br>`com.microsoft.intune.mam.managedbrowser.BlockListURLs`    |    键的对应值是 URL 列表。 将要允许或阻止的所有 URL 作为单个值输入，并用竖线 `|` 字符分隔。<br>**示例：**<br>`URL1|URL2|URL3`<br>`http://.contoso.com/|https://.bing.com/|https://expenses.contoso.com`  |

无论定义的允许列表或阻止列表设置如何，都始终允许以下站点：
- `https://*.microsoft.com/*`
- `http://*.microsoft.com/*`
- `https://microsoft.com/*`
- `http://microsoft.com/*`
- `https://*.windowsazure.com/*`
- `https://*.microsoftonline.com/*`
- `https://*.microsoftonline-p.com/*`

### <a name="url-formats-for-allowed-and-blocked-site-list"></a>允许的和阻止的站点列表的 URL 格式 
可使用多种 URL 格式来构建允许/阻止的站点列表。 下表详细介绍了这些允许的模式。 开始之前，请注意以下几点： 
- 在将 URL 输入列表时，确保对所有 URL 添加“http://”  或“https://”  作为前缀。
- 可以根据以下允许模式列表中的规则使用通配符 (\*)。
- 通配符只能匹配主机名中的整体部分（由句点分隔）或路径的整体部分（由正斜杠分隔）。 例如，不支持 `http://*contoso.com`  。
- 可以在地址中指定端口号。 如果未指定端口号，则使用以下值：
  - 对于 http，使用端口 80
  - 对于 https，使用端口 443
- 不支持对端口号使用通配符  。 例如，不支持 `http://www.contoso.com:*` 和 `http://www.contoso.com:*/`。 

    |    URL    |    详细信息    |    匹配    |    不匹配    |
    |-------------------------------------------|--------------------------------------------------------|-------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
    |    `http://www.contoso.com`    |    匹配单个页面    |    `www.contoso.com`    |    `host.contoso.com`<br>`www.contoso.com/images`<br>`contoso.com/`    |
    |    `http://contoso.com`    |    匹配单个页面    |    `contoso.com/`    |    `host.contoso.com`<br>`www.contoso.com/images`<br>`www.contoso.com`    |
    |    `http://www.contoso.com/*;`   |    匹配以 `www.contoso.com` 开头的所有 URL    |    `www.contoso.com`<br>`www.contoso.com/images`<br>`www.contoso.com/videos/tvshows`    |    `host.contoso.com`<br>`host.contoso.com/images`    |
    |    `http://*.contoso.com/*`    |    匹配 `contoso.com` 下的所有子域    |    `developer.contoso.com/resources`<br>`news.contoso.com/images`<br>`news.contoso.com/videos`    |    `contoso.host.com`
    |    `http://*contoso.com/*`    |    匹配以 `contoso.com/` 结尾的所有子域    |    `http://news-contoso.com`<br>`http://news-contoso.com.com/daily`    |    `http://news-contoso.host.com`    |
    `http://www.contoso.com/images`    |    匹配单个文件夹    |    `www.contoso.com/images`    |    `www.contoso.com/images/dogs`    |
    |    `http://www.contoso.com:80`    |    匹配单个页面（使用端口号）    |    `http://www.contoso.com:80`    |         |
    |    `https://www.contoso.com`    |    匹配单个安全页面    |    `https://www.contoso.com`    |    `http://www.contoso.com`    |
    |    `http://www.contoso.com/images/*`    |    匹配单个文件夹和所有子文件夹    |    `www.contoso.com/images/dogs`<br>`www.contoso.com/images/cats`    |    `www.contoso.com/videos`    |
  
- 以下是一些不能指定的输入的示例：
  - `*.com`
  - `*.contoso/*`
  - `www.contoso.com/*images`
  - `www.contoso.com/*images*pigs`
  - `www.contoso.com/page*`
  - IP 地址
  - `https://*`
  - `http://*`
  - `https://*contoso.com`
  - `http://www.contoso.com:*`
  - `http://www.contoso.com: /*`

## <a name="transition-users-to-their-personal-context-when-trying-to-access-a-blocked-site"></a>尝试访问被阻止的网站时，将用户转换到其个人上下文

借助内置于 Microsoft Edge 的双重标识模型，可为最终用户提供比 Intune Managed Browser 中可实现的体验更加灵活的体验。 当用户在 Microsoft Edge 中点击阻止站点时，可以提示他们在其个人上下文（而不是其工作上下文）中打开链接。 这样能够使他们受到保护，同时保护公司资源安全。 例如，如果通过 Outlook 向用户发送指向新闻文章的链接，则可以在其个人上下文或 InPrivate 选项卡中打开该链接。其工作上下文不允许访问新闻网站。 默认情况下，这些转换是允许的。

使用以下键/值对来配置是否允许这些软转换：

|    Key    |    值    |
|-------------------------------------------------------------------|-------------------------------------------------------|
|    `com.microsoft.intune.mam.managedbrowser.AllowTransitionOnBlock`    |    **true**（默认值）：允许 Microsoft Edge 将用户转换到其个人上下文以打开阻止的站点。<p>**False**：阻止 Microsoft Edge 转换用户。 只会向用户显示一条消息，指示已阻止他们尝试访问的网站。    |

## <a name="open-restricted-links-directly-in-inprivate-tab-pages"></a>直接在 InPrivate 选项卡页中打开受限链接

可以配置是否应该在 InPrivate 浏览中直接打开受限链接，这为用户提供了更无缝的浏览体验。 为此，用户可以跳过必须转换到其个人上下文来查看网站的步骤。 InPrivate 浏览被视为不受托管，因此用户在使用 InPrivate 浏览模式时将无法访问。  注意：若要使此设置生效，还必须将上面的设置 `com.microsoft.intune.mam.managedbrowser.AllowTransitionOnBlock` 配置为 true  。

|    Key    |    值    |
|----------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    `com.microsoft.intune.mam.managedbrowser.openInPrivateIfBlocked`    |    **true**：将直接在“InPrivate”选项卡中打开网站，而不会提示用户将其切换到其个人帐户。 <p> **False**（默认值）：将阻止 Microsoft Edge 中的站点，并要求用户切换到其个人帐户进行查看。    |


## <a name="disable-microsoft-edge-features-to-customize-the-end-user-experience-for-your-organizations-needs"></a>禁用 Microsoft Edge 功能，为你的组织的需求自定义最终用户体验

### <a name="disable-prompts-to-share-usage-data-for-personalization"></a>禁用用于个性化的共享使用情况数据的提示 

默认情况下，Microsoft Edge 会提示用户提供使用情况数据收集，以个性化他们的浏览体验。 可以通过阻止向最终用户显示此提示来禁用共享此数据。 

|    Key    |    值    |
|----------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    `com.microsoft.intune.mam.managedbrowser.disableShareUsageData`    |     **true**：将禁止向最终用户显示此提示。    |

### <a name="disable-prompts-to-share-browsing-history"></a>禁用用于共享浏览历史记录的提示 

默认情况下，Microsoft Edge 会提示用户提供浏览历史数据收集，以个性化他们的浏览体验。 可以通过阻止向最终用户显示此提示来禁用共享此数据。

|    Key    |    值    |
|----------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     `com.microsoft.intune.mam.managedbrowser.disableShareBrowsingHistory`    |     **true**：将禁止向最终用户显示此提示。     |

### <a name="disable-prompts-that-offer-to-save-passwords"></a>禁用提供保存密码的提示

默认情况下，iOS 上的 Microsoft Edge 会询问是否将用户密码保存到密钥链。 如果想为组织禁用此提示，请配置以下设置：

|    Key    |    值    |
|-----------------------|-----------------------|
|    `com.microsoft.intune.mam.managedbrowser.disableFeatures`    |    **密码**：将禁用提供为最终用户保存密码的提示。    |

### <a name="disable-users-from-adding-extensions-to-microsoft-edge"></a>禁止用户向 Microsoft Edge 添加扩展 

可在 Microsoft Edge 中禁用扩展框架，以防止用户安装任何扩展应用。 为此，请配置以下设置：

|    Key    |    值    |
|-----------|-------------|
|    `com.microsoft.intune.mam.managedbrowser.disableExtensionFramework`    |    **true**：禁用扩展框架    |

### <a name="disable-inprivate-browsing-and-microsoft-accounts-to-restrict-browsing-to-work-only-contexts"></a>禁用 InPrivate 浏览和 Microsoft 帐户，将浏览限制为仅工作上下文

如果你的组织在高度管控的行业中运行，或者使用基于应用的 VPN 来允许用户使用 Microsoft Edge 访问工作资源，则可选择在 Microsoft Edge 内禁用被视为非工作环境的 InPrivate 浏览。 

|    Key    |    值    |
|-----------|-------------|
|    `com.microsoft.intune.mam.managedbrowser.disableFeatures`    |    **inprivate**：禁用 InPrivate 浏览。   |

### <a name="restrict-microsoft-edge-use-to-allowed-accounts-only"></a>将 Microsoft Edge 使用限制为仅允许帐户

除了阻止 InPrivate 和 MSA 浏览，还可以在用户使用其 AAD 帐户登录时，仅允许使用 Microsoft Edge。 此功能仅适用于已注册 MDM 的用户。 可在此处了解有关配置此设置的详细信息：

>[!NOTE]
> 可以使用 `com.microsoft.intune.mam.managedbrowser.disableFeatures` 同时禁用多个功能。 例如，若要同时禁用 InPrivate 和密码，请使用 `inprivate| password`。

## <a name="configure-microsoft-edge-as-a-kiosk-app-on-android-devices"></a>在 Android 设备上将 Microsoft Edge 配置为展台应用

### <a name="enable-microsoft-edge-as-a-kiosk-app"></a>将 Microsoft Edge 作为展台应用启用
若要将 Microsoft Edge 作为展台应用启用，请先配置下面的父设置：

|    Key    |    值    |
|-----------|-------------|
|    `com.microsoft.intune.mam.managedbrowser.enableKioskMode`    |    **true**：为 Microsoft Edge 启用展台配置    |

### <a name="show-address-bar-in-kiosk-mode"></a>在展台模式下显示地址栏
若要在展台模式下显示 Microsoft Edge 中的地址栏，请配置以下设置：

|    Key    |    值    |
|-----------|-------------|
|    `com.microsoft.intune.mam.managedbrowser.showAddressBarInKioskMode`    |    **true**：显示地址栏。 <br> **false**：（默认值）隐藏地址栏。    |

### <a name="show-bottom-action-bar-in-kiosk-mode"></a>在展台模式下显示底部操作栏
|    Key    |    值    |
|-----------|-------------|
|    `com.microsoft.intune.mam.managedbrowser.showBottomBarInKioskMode`    |    **true**：在 Microsoft Edge 中显示底部操作栏。 <br> **false**：（默认值）隐藏底部栏。    |


## <a name="use-microsoft-edge-to-access-managed-app-logs"></a>使用 Microsoft Edge 访问托管的应用日志


在 iOS 或 Android 设备上安装了 Microsoft Edge 的用户可查看所有 Microsoft 已发布应用的管理状态。 他们可以使用以下步骤发送日志，以便排查托管的 iOS 或 Android 应用的故障：

1. 在设备上打开 Microsoft Edge。
2. 在地址框中键入 `about:intunehelp`。
3. Microsoft Edge 将启动疑难解答模式。

对于应用日志中存储的设置列表，请参阅[在 Managed Browser 中查看应用保护日志](app-protection-policy-settings-log.md)。

若要了解如何在 Android 设备上查看日志，请参阅[通过电子邮件将日志发送给 IT 管理员](https://docs.microsoft.com/mem/intune/user-help/send-logs-to-your-it-admin-by-email-android)。

## <a name="security-and-privacy-for-microsoft-edge"></a>Microsoft Edge 的安全和隐私

下面是 Microsoft Edge 的其他安全和隐私注意事项：

- Microsoft Edge 不使用用户在其设备上为本机浏览器 https://docs.microsoft.com/en-us/intune/apps/app-configuration-policies-use-android#allow-only-configured-organization-accounts-in-multi-identity-apps 设置的设置，因为 Microsoft Edge 无法访问这些设置。
- 可以在与 Microsoft Edge 关联的应用保护策略中配置“访问需要简单 PIN”或“访问需要公司凭据”选项   。 如果用户选择身份验证页上的帮助链接，则可以浏览任何 Internet 站点，而不考虑它们是否已添加到策略中的阻止列表。
- Microsoft Edge 仅能在用户直接访问站点时阻止访问。 用户使用中间服务（例如翻译服务）访问站点时，该策略则不会阻止访问。
- 若要允许身份验证和访问 Intune 文档，请从允许或阻止列表设置中移除 *.microsoft.com  。 始终允许。
- 用户可以关闭数据收集。 Microsoft 会自动收集有关性能和 Managed Browser 使用情况的匿名数据，以改进 Microsoft 产品和服务。 用户可通过使用设备上的**用法数据**设置关闭数据收集。 不具有对此数据的收集的控制。 在 iOS 设备上，如果用户访问的网站的证书已过期或不受信任，则无法打开该网站。

## <a name="restrict-microsoft-edge-use-to-a-work-or-school-account"></a>将 Microsoft Edge 限制用于工作或学校帐户

体现 Microsoft 365 价值的关键是遵从最大范围和高度管控客户的数据安全和合规性策略。 一些公司要求捕获其公司环境内的所有通信信息，并确保设备仅用于公司通信。 为了支持这些要求，可以将已注册设备上的适用于 iOS 和 Android 的 Edge 配置为仅允许在适用于 iOS 和 Android 的 Edge 中预配一个公司帐户。

下面的资源详细介绍了如何配置组织允许的帐户模式设置：

- [Android 设置](app-configuration-policies-use-android.md#allow-only-configured-organization-accounts-in-multi-identity-apps)
- [iOS 设置](app-configuration-policies-use-ios.md#allow-only-configured-organization-accounts-in-multi-identity-apps)

## <a name="next-steps"></a>后续步骤

- [什么是应用保护策略？](app-protection-policy.md) 
