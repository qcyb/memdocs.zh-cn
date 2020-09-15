---
title: 通过 Intune 管理适用于 iOS 和 Android 的 Edge
titleSuffix: ''
description: 对适用于 iOS 和 Android 的 Microsoft Edge 使用 Intune 应用保护和配置策略，确保访问公司网站时，安全措施始终到位。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/03/2020
ms.topic: how-to
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
ms.openlocfilehash: 9391be828452cbda25dd6c4f4ed75cffa2ef687c
ms.sourcegitcommit: b95eac00a0cd979dc88be953623c51dbdc9327c5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2020
ms.locfileid: "89423741"
---
# <a name="manage-web-access-by-using-edge-for-ios-and-android-with-microsoft-intune"></a>将适用于 iOS 和 Android 的 Microsoft Edge 与 Microsoft Intune 结合使用来管理 Web 访问

适用于 iOS 和 Android 的 Microsoft Edge 旨在使用户能够浏览 Web 并支持多身份。 用户可以同时添加工作帐户以及个人帐户以进行浏览。 两个身份完全独立，这类似于其他 Microsoft 移动应用中提供的体验。

iOS 12.0 及更高版本支持适用于 iOS 的 Microsoft Edge。 Android 5 及更高版本支持适用于 Android 的 Microsoft Edge。

> [!NOTE]
> 适用于 iOS 和 Android 的 Microsoft Edge 不会使用用户为设备上的本机浏览器设置的设置，因为适用于 iOS 和 Android 的 Microsoft Edge 无法访问这些设置。

订阅企业移动性 + 安全性套件（包括 Microsoft Intune 和 Azure Active Directory Premium 功能，如条件访问）可获得最丰富和最广泛的 Microsoft 365 数据保护功能。 最基础的层面来说，你需要部署一个条件访问策略，该策略仅允许从移动设备连接到适用于 iOS 和 Android 的 Microsoft Edge，还需要部署 Intune 应用保护策略确保浏览体验受到保护。

> [!NOTE]
> 如果需要在受保护的浏览器中打开 iOS 设备上的新 Web 剪辑（固定的 Web 应用），则将在适用于 iOS 和 Android 的 Microsoft Edge（而不是在 Intune Managed Browser 中）打开它们。 对于较旧的 iOS Web 剪辑，必须重定向这些 Web 剪辑，以确保它们在适用于 iOS 和 Android 的 Microsoft Edge 而不是 Managed Browser 中打开。

## <a name="apply-conditional-access"></a>应用条件访问
组织可以使用 Azure AD 条件访问策略来确保用户只能使用适用于 iOS 和 Android 的 Edge 访问工作或学校内容。 为此，你需要一个面向所有潜在用户的条件访问策略。 有关创建此策略的详细信息，请参阅[通过条件访问要求访问云应用时具有应用保护策略](/azure/active-directory/conditional-access/app-protection-based-conditional-access)。

1. 参照[场景 2：浏览器应用要求批准的应用具有应用保护策略](/azure/active-directory/conditional-access/app-protection-based-conditional-access#scenario-2-browser-apps-require-approved-apps-with-app-protection-policies)，这允许使用适用于 iOS 和 Android 的 Microsoft Edge，但阻止其他移动设备 Web 浏览器连接到 Office 365 终结点。

   >[!NOTE]
   > 此策略确保移动用户可以从适用于 iOS 和 Android 的 Edge 内访问所有 Microsoft 365 终结点。 此策略还会阻止用户使用 InPrivate 访问 Microsoft 365 终结点。

使用条件访问，你还可以针对通过 [Azure AD 应用程序代理](/azure/active-directory/active-directory-application-proxy-get-started)向外部用户公开的本地站点。

## <a name="create-intune-app-protection-policies"></a>创建 Intune 应用保护策略

应用保护策略 (APP) 定义允许的应用以及这些应用可对组织的数据执行的操作。 APP 中可用的选项使组织能够根据特定需求调整保护。 对于某些组织而言，实现完整方案所需的策略设置可能并不明显。 为了帮助组织确定移动客户端终结点强化的优先级，Microsoft 为其面向 iOS 和 Android 移动应用管理的 APP 数据保护框架引入了分类法。

APP 数据保护框架分为三个不同的配置级别，每个级别基于上一个级别进行构建：

- 企业基本数据保护（级别 1）可确保应用受 PIN 保护和经过加密处理，并执行选择性擦除操作。 对于 Android 设备，此级别验证 Android 设备证明。 这是一个入门级配置，可在 Exchange Online 邮箱策略中提供类似的数据保护控制，并将 IT 和用户群引入 APP。
- 企业增强型数据保护（级别 2）引入了 APP 数据泄露预防机制和最低 OS 要求。 此配置适用于访问工作或学校数据的大多数移动用户。
- 企业高级数据保护（级别 3）引入了高级数据保护机制、增强的PIN 配置和 APP 移动威胁防御。 此配置适用于访问高风险数据的用户。

若要查看每个配置级别的具体建议以及必须受保护的核心应用，请查看[使用应用保护策略的数据保护框架](app-protection-framework.md)。

无论设备是否已注册统一终结点管理 (UEM) 解决方案，都需要使用[如何创建和分配应用保护策略](app-protection-policies.md)中的步骤来为 iOS 和 Android 应用创建 Intune 应用保护策略。 这些策略必须至少满足以下条件：

1. 包括所有 Microsoft 365 移动应用程序（如 Edge、Outlook、OneDrive、Office 或 Teams），因为这样可以确保用户在任何 Microsoft 应用中均能够以安全的方式访问和处理工作或学校数据。

2. 它们将分配给所有用户。 这可确保所有用户都受到保护，不管他们使用的是适用于 iOS 还是 Android 的 Microsoft Edge。

3. 确定哪一个框架级别满足你的要求。 大多数组织应实现企业增强型数据保护（级别 2）中定义的设置，因为这样可以启用数据保护和访问要求控制。

有关可用设置的详细信息，请参阅 [Android 应用保护策略设置](app-protection-policy-settings-android.md) 和 [iOS 应用保护策略设置](app-protection-policy-settings-ios.md)。

> [!IMPORTANT]
> 若要针对未在 Intune 中注册的 Android 设备上的应用应用 Intune 应用保护策略，用户还必须安装 Intune 公司门户。 有关详细信息，请参阅 [Android 应用由应用保护策略托管时会出现的情况](../fundamentals/end-user-mam-apps-android.md)。

## <a name="single-sign-on-to-azure-ad-connected-web-apps-in-policy-protected-browsers"></a>在受策略保护的浏览器中单一登录到 Azure AD 连接的 Web 应用

适用于 iOS 和 Android 的 Microsoft Edge 可以对与 Azure AD 连接的所有 Web 应用（SaaS 和本地）使用单一登录 (SSO)。 SSO 允许用户通过适用于 iOS 和 Android 的 Microsoft Edge 访问与 Azure AD 连接的 Web 应用，而无需重新输入凭据。

SSO 要求设备通过 Microsoft Authenticator 应用（iOS 设备）或 Intune 公司门户（Android）进行注册。 如果用户采用其中一种方式进行注册，当他们在受策略保护的浏览器中转到与 Azure AD 连接的 Web 应用时，系统会提示他们注册设备（仅当设备尚未注册时才会如此）。 使用 Intune 管理的用户帐户注册设备后，该帐户已为 Azure AD 连接的 Web 应用启用 SSO。

> [!NOTE]
> 设备注册是 Azure AD 服务的简单签入。 不需要完整的设备注册，并且不会向 IT 提供设备上的任何其他权限。

## <a name="utilize-app-configuration-to-manage-the-browsing-experience"></a>利用应用配置管理浏览体验

适用于 iOS 和 Android 的 Microsoft Edge 支持允许统一终结点管理（例如允许 Microsoft Endpoint Manager 和管理员自定义应用的行为）的应用设置。

可以通过已注册设备上的移动设备管理 (MDM) OS 通道（iOS 上为 [Managed App Configuration](https://developer.apple.com/library/content/samplecode/sc2279/Introduction/Intro.html) 通道，Android 上为 [Android in the Enterprise](https://developer.android.com/work/managed-configurations) 通道）来交付应用配置，也可以通过 Intune 应用保护策略 (APP) 通道来交付应用配置。 适用于 iOS 和 Android 的 Microsoft Edge 支持以下配置方案：

- 仅允许工作或学校帐户
- 常规应用配置设置
- 数据保护设置

> [!IMPORTANT]
> 对于需要在 Android 上进行设备注册的配置方案，必须在 Android Enterprise 中注册设备，并且必须通过托管的 Google Play 商店部署适用于 Android 的 Microsoft Edge。 有关详细信息，请参阅 [设置 Android Enterprise 工作配置文件设备的注册](../enrollment/android-work-profile-enroll.md)和[为托管的 Android Enterprise 设备添加应用配置策略](app-configuration-policies-use-android.md)。

每个配置方案都强调了其特定要求。 例如，配置方案是否需要进行设备注册以便能够用于任何 UEM 提供程序，或者是否需要 Intune 应用保护策略。

> [!NOTE]
> 使用 Microsoft Endpoint Manager 的情况下，通过 MDM OS 通道交付的应用配置称为托管设备应用配置策略 (ACP)；通过应用保护策略通道交付的应用配置称为托管应用应用配置策略 。

## <a name="only-allow-work-or-school-accounts"></a>仅允许工作或学校帐户

体现 Microsoft 365 价值的关键是遵从最大范围和高度管控客户的数据安全和合规性策略。 一些公司要求捕获其公司环境内的所有通信信息，并确保设备仅用于公司通信。 为了支持这些要求，可以将已注册设备上适用于 iOS 和 Android 的 Microsoft Edge 配置为仅允许在该应用中预配一个公司帐户。

下面的资源详细介绍了如何配置组织允许的帐户模式设置：

- [Android 设置](app-configuration-policies-use-android.md#allow-only-configured-organization-accounts-in-multi-identity-apps)
- [iOS 设置](app-configuration-policies-use-ios.md#allow-only-configured-organization-accounts-in-multi-identity-apps)

此配置方案仅适用于已注册的设备。 但是，它支持所有 UEM 提供程序。 如果未使用 Microsoft Endpoint Manager，则需要参阅 UEM 文档，了解如何部署这些配置项。

## <a name="general-app-configuration-scenarios"></a>常规应用配置方案

适用于 iOS 和 Android 的 Microsoft Edge 使管理员能够为多个应用内设置自定义默认配置。 此功能当前仅在以下情况下提供：适用于 iOS 和 Android 的 Microsoft Edge 具有应用于工作或学校帐户（该帐户已登录到应用）的 Intune 应用保护策略，并且策略设置是通过托管应用的应用配置策略交付的。

> [!IMPORTANT]
> 适用于 Android 的 Microsoft Edge 不支持托管的 Google Play 中可用的 Chromium 设置。

Microsoft Edge 支持以下配置设置：

- 新标签页体验
- 书签体验
- 应用行为体验
- 展台模式体验

无论设备注册状态如何，都可以将这些设置部署到应用。

### <a name="new-tab-page-experiences"></a>新标签页体验

适用于 iOS 和 Android 的 Microsoft Edge 为组织提供了多个选项，用于调整新标签页体验。

#### <a name="organization-logo-and-brand-color"></a>组织徽标和品牌颜色

通过这些设置，可以将适用于 iOS 和 Android 的 Microsoft Edge 的新标签页自定义为：显示组织徽标和品牌颜色作为标签页背景。

若要上传组织徽标和品牌颜色，请先完成以下步骤：
1. 在 [Microsoft Endpoint Manager](https://endpoint.microsoft.com) 中，导航到“租户管理” -> “自定义” -> “公司标识品牌”。
2. 若要设置品牌的徽标，请在“在标头中显示”旁边选择“仅限组织徽标”。 建议使用透明背景徽标。
3. 要设置品牌的背景色，请选择“主题色”。 适用于 iOS 和 Android 的 Microsoft Edge 在新标签页上应用了较浅的颜色底纹，这可确保页面具有更高的可读性。

接下来，使用以下键/值对将组织的品牌纳入到适用于 iOS 和 Android 的 Microsoft Edge 中：

|    Key    |    值    |
|--------------------------------------------------------------------|------------|
|    com.microsoft.intune.mam.managedbrowser.NewTabPage.BrandLogo    |    “true”：显示组织的品牌徽标<br>“false”（默认）：不显示徽标    |
|    com.microsoft.intune.mam.managedbrowser.NewTabPage.BrandColor    |    “true”：显示组织的品牌颜色<br>“false”（默认）：不显示颜色    |

#### <a name="homepage-shortcut"></a>主页快捷方式

你可以使用此设置为适用于 iOS 和 Android 的 Microsoft Edge 配置主页快捷方式。 当用户在适用于 iOS 和 Android 的 Microsoft Edge 中打开新标签页时，你配置的主页快捷方式将显示为搜索栏下方的第一个图标。 用户无法在其托管上下文中编辑或删除此快捷方式。 主页快捷方式将显示组织的名称以便进行区分。 

|    Key    |    值    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.homepage   |    指定有效 URL。 将阻止错误的 URL，这是一项安全措施。<br>例如：`https://www.bing.com`     |

#### <a name="multiple-top-site-shortcuts"></a>多个首要网站快捷方式

与配置主页快捷方式类似，你可以在适用于 iOS 和 Android 的 Microsoft Edge 中的新标签页上配置多个首要网站快捷方式。 用户无法在其托管上下文中编辑或删除此快捷方式。 注意：可以配置总共 8 个快捷方式，包括主页快捷方式。 如果已配置主页快捷方式，则该快捷方式会替代配置的第一个首要网站。 

|    Key    |    值    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.managedTopSites   |    指定一组 URL 的值。 每个顶级网站快捷方式都由标题和 URL 组成。 用字符 `|` 分隔标题和 URL。<br>例如：`GitHub|https://github.com/||LinkedIn|https://www.linkedin.com`    |

#### <a name="industry-news"></a>行业新闻

你可以在适用于 iOS 和 Android 的 Microsoft Edge 中配置新标签页体验，显示与组织相关的行业新闻。 启用此功能时，适用于 iOS 和 Android 的 Microsoft Edge 将使用组织域名聚合来自 Web 的有关组织、组织行业和竞争者的新闻，因此用户可以从适用于 iOS 和 Android 的 Microsoft Edge 集中的新选项卡页查找相关外部新闻。 默认情况下，行业新闻处于关闭状态。 

|    Key    |    值    |
|------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.NewTabPage.IndustryNews    |    “true”：在新选项卡页上显示行业新闻<br>“false”（默认）：在新选项卡页上隐藏行业新闻    |

### <a name="bookmark-experiences"></a>书签体验

适用于 iOS 和 Android 的 Microsoft Edge 为组织提供了多个用于管理书签的选项。

#### <a name="managed-bookmarks"></a>托管书签

为了便于访问，可配置希望用户在使用适用于 iOS 和 Android 的 Microsoft Edge 时可用的书签。

- 书签只显示在工作或学校帐户中，不会公开给个人帐户。
- 用户无法删除或修改书签。
- 书签显示在列表顶部。 用户创建的任何书签显示在这些书签下方。
- 如果已启用应用程序代理重定向，可以使用应用程序代理 Web 应用的内部或外部 URL 添加这些 Web 应用。
- 在将 URL 输入列表时，确保对所有 URL 添加“http://”或“https://”作为前缀。
- 书签是在以 Azure Active Directory 中定义的组织名称命名的文件夹中创建的。

|    Key    |    值    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.bookmarks    |    此配置的值是一个书签列表。 每个书签都由书签标题和书签 URL 组成。 用字符 `|` 分隔标题和 URL。<br> 例如：`Microsoft Bing|https://www.bing.com`<p>若要配置多个书签，可使用双字符 `||` 分隔每对书签。<br>例如：<br>`Microsoft Bing|https://www.bing.com||Contoso|https://www.contoso.com`    |

#### <a name="my-apps-bookmark"></a>“我的应用”书签

默认情况下，适用于 iOS 和 Android 的 Microsoft Edge 内的组织文件夹中为用户配置了“我的应用”书签。

|    Key    |    值    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.MyApps    |    “true”（默认）：在适用于 iOS 和 Android 的 Microsoft Edge 书签中显示“我的应用”<br>“false”：在适用于 iOS 和 Android 的 Microsoft Edge 中隐藏“我的应用”    |

### <a name="app-behavior-experiences"></a>应用行为体验

适用于 iOS 和 Android 的 Microsoft Edge 为组织提供了多个用于应用行为的选项。

#### <a name="default-protocol-handler"></a>默认协议处理程序

默认情况下，当用户未在 URL 中指定协议时，适用于 iOS 和 Android 的 Microsoft Edge 使用 HTTPS 协议处理程序。 通常，这被认为是最佳做法，但你可以禁用它。

|    Key    |    值    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.defaultHTTPS     |     “true”（默认）：默认协议处理程序为 HTTPS<br>“false”：默认协议处理程序为 HTTP     |

#### <a name="disable-data-sharing-for-personalization"></a>禁用旨在提供个性化体验的数据共享

默认情况下，适用于 iOS 和 Android 的 Microsoft Edge 会提示用户允许收集使用情况数据和共享浏览历史记录，以便为他们提供个性化的浏览体验。 组织可以通过阻止向最终用户显示此提示来禁用此数据共享。

|    Key    |    值    |
|----------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.disableShareUsageData    |     “true”：禁止向最终用户显示此提示<br>“false”（默认）：提示用户共享使用情况数据    |
|     com.microsoft.intune.mam.managedbrowser.disableShareBrowsingHistory    |     “true”：禁止向最终用户显示此提示<br>“false”（默认）：提示用户共享浏览历史记录     |

#### <a name="disable-specific-features"></a>禁用特定功能

适用于 iOS 和 Android 的 Microsoft Edge 允许组织禁用某些默认启用的功能。 要禁用这些功能，请配置以下设置：

|    Key    |    值    |
|-----------------------|-----------------------|
|    com.microsoft.intune.mam.managedbrowser.disabledFeatures    |    “password”：禁用为最终用户保存密码的提示<br>“inprivate”：禁用 InPrivate 浏览<p>若要禁用多个功能，请使用 `|` 分隔各值。 例如，`inprivate|password` 将同时禁用 InPrivate 和密码保存。     |

> [!NOTE]
> 适用于 Android 的 Microsoft Edge 不支持禁用密码管理器。

#### <a name="disable-extensions"></a>禁用扩展

可在适用于 Android 的 Microsoft Edge 中禁用扩展框架，以防止用户安装任何应用扩展。 为此，请配置以下设置：

|    Key    |    值    |
|-----------|-------------|
|    com.microsoft.intune.mam.managedbrowser.disableExtensionFramework    |    “true”：禁用扩展框架<br>“false”（默认）：启用扩展框架    |

### <a name="kiosk-mode-experiences-on-android-devices"></a>Android 设备上的展台模式体验

可以使用以下设置将适用于 Android 的 Microsoft Edge 启用为展台应用：

|    Key    |    值    |
|-----------|-------------|
|    com.microsoft.intune.mam.managedbrowser.enableKioskMode    |    “true”：为适用于 Android 的 Microsoft Edge 启用展台模式<br>“false”（默认）：禁用展台模式    |
|    com.microsoft.intune.mam.managedbrowser.showAddressBarInKioskMode    |    “true”：在展台模式下显示地址栏<br> “false”（默认）：在启用展台模式时隐藏地址栏    |
|    com.microsoft.intune.mam.managedbrowser.showBottomBarInKioskMode    |    “true”：在展台模式下显示底部操作栏<br> “false”（默认）：在启用展台模式时隐藏底部操作栏    |

## <a name="data-protection-app-configuration-scenarios"></a>数据保护应用配置方案

当 Microsoft Endpoint Manager 管理适用于 iOS 和 Android 的 Microsoft Edge，Intune 应用保护策略已应用于已登录该应用的工作或学校帐户，并且策略设置通过托管应用的应用配置策略交付时，适用于 iOS 和 Android 的 Microsoft Edge 支持针对以下数据保护设置的应用配置策略：

- 管理帐户同步
- 管理受限网站
- 管理代理配置
- 管理 NTLM 单一登录站点

无论设备注册状态如何，都可以将这些设置部署到应用。

### <a name="manage-account-synchronization"></a>管理帐户同步

默认情况下，Microsoft Edge 同步使用户能够跨所有已登录设备访问浏览数据。 同步支持的数据包括：

- 收藏夹
- 密码
- 地址以及更多内容（自动填充表单项）

同步功能经用户同意启用，用户可以为上面列出的每种数据类型开启或关闭同步。 有关详细信息，请参阅 [Microsoft Edge 同步](/DeployEdge/microsoft-edge-enterprise-sync)。

组织可以在 iOS 和 Android 上禁用 Microsoft Edge 同步。 

|Key  |值  |
|---------|---------|
|com.microsoft.intune.mam.managedbrowser.account.syncDisabled     |“true”（默认）：允许 Microsoft Edge 同步<br>“false”：禁用 Microsoft Edge 同步          |

### <a name="manage-restricted-web-sites"></a>管理受限网站

组织可以在适用于 iOS 和 Android 的 Microsoft Edge 中定义用户可以在工作或学校帐户环境中访问的网站。 如果使用允许列表，用户将只能访问明确列出的站点。 如果使用阻止列表，用户可以访问除明确阻止的站点之外的所有站点。 应仅使用一个允许列表或一个阻止列表，而不能同时使用两者。 如果同时使用两者，则只会遵循允许列表。

组织还可以定义当用户尝试导航到受限网站时会发生的情况。 默认情况下允许过渡。 如果组织允许，可以在个人帐户环境、Azure AD 帐户的 InPrivate 环境中打开受限网站，否则请确认是否完全阻止了该网站。 有关支持的各种方案的详细信息，请参阅 [Microsoft Edge 移动应用中的受限网站过渡](https://techcommunity.microsoft.com/t5/intune-customer-success/restricted-website-transitions-in-microsoft-edge-mobile/ba-p/1381333)。 通过允许过渡体验，在保持公司资源安全的同时，组织的用户也会一直受到保护。

> [!NOTE]
> 适用于 iOS 和 Android 的 Microsoft Edge 仅能在用户直接访问站点时阻止访问。 用户使用中间服务（例如翻译服务）访问站点时，该策略则不会阻止访问。

使用以下键/值对为适用于 iOS 和 Android 的 Microsoft Edge 配置一个允许或阻止站点列表。 

|Key  |值  |
|---------|---------|
|com.microsoft.intune.mam.managedbrowser.AllowListURLs     |键的对应值是 URL 列表。 将要允许的所有 URL 作为单个值输入，并用竖线 `|` 字符分隔。<p>**示例：**<br>`URL1|URL2|URL3`<br>`http://.contoso.com/|https://.bing.com/|https://expenses.contoso.com`         |
|com.microsoft.intune.mam.managedbrowser.BlockListURLs     |键的对应值是 URL 列表。 将要阻止的所有 URL 作为单个值输入，并用竖线 `|` 字符分隔。<br>**示例：**<br>`URL1|URL2|URL3`<br>`http://.contoso.com/|https://.bing.com/|https://expenses.contoso.com`         |
|com.microsoft.intune.mam.managedbrowser.AllowTransitionOnBlock     |“true”（默认）：允许适用于 iOS 和 Android 的 Microsoft Edge 过渡受限制的站点。 如果未禁用个人帐户，系统会提示用户切换到个人环境来打开受限站点，或添加个人帐户。 如果将 com.microsoft.intune.mam.managedbrowser.openInPrivateIfBlocked 设置为 true，则用户将能够在 InPrivate 环境中打开受限制的站点。<p>“false”：阻止适用于 iOS 和 Android 的 Microsoft Edge 过渡用户。 只会向用户显示一条消息，指示已阻止他们尝试访问的网站。         |
|com.microsoft.intune.mam.managedbrowser.openInPrivateIfBlocked     |“true”：允许在 Azure AD 帐户的 InPrivate 环境中打开受限制的站点。 如果 Azure AD 帐户是在适用于 iOS 和 Android 的 Microsoft Edge 中配置的唯一帐户，则会在 InPrivate 环境中自动打开受限制的站点。 如果用户已配置个人帐户，则系统会提示用户在打开 InPrivate 或切换到个人帐户之间进行选择。<p> “false”（默认）：要求在用户的个人帐户中打开受限制的站点。 如果个人帐户处于禁用状态，则阻止站点。<p>为了使此设置生效，com.microsoft.intune.mam.managedbrowser.AllowTransitionOnBlock 必须设置为“true”。          |
|com.microsoft.intune.mam.managedbrowser.durationOfOpenInPrivateSnackBar     | 输入用户将看到 Snack bar 通知“以 InPrivate 模式打开链接。 你的组织要求为此内容使用 InPrivate模式”的秒数。 默认情况下，Snack bar 通知显示 7 秒。

无论定义的允许列表或阻止列表设置如何，都始终允许以下站点：
- `https://*.microsoft.com/*`
- `http://*.microsoft.com/*`
- `https://microsoft.com/*`
- `http://microsoft.com/*`
- `https://*.windowsazure.com/*`
- `https://*.microsoftonline.com/*`
- `https://*.microsoftonline-p.com/*`

#### <a name="url-formats-for-allowed-and-blocked-site-list"></a>允许的和阻止的站点列表的 URL 格式 

可使用多种 URL 格式来构建允许/阻止的站点列表。 下表详细介绍了这些允许的模式。

- 在将 URL 输入列表时，确保对所有 URL 添加“http://”或“https://”作为前缀。
- 可以根据以下允许模式列表中的规则使用通配符 (\*)。
- 通配符只能匹配主机名中的一部分（例如 `news-contoso.com`）或整体部分（例如 `host.contoso.com`）或者由正斜杠分隔的路径的整体部分 (`www.contoso.com/images`)。
- 可以在地址中指定端口号。 如果未指定端口号，则使用以下值：
  - 对于 http，使用端口 80
  - 对于 https，使用端口 443
- 不支持对端口号使用通配符。 例如，不支持 `http://www.contoso.com:*` 和 `http://www.contoso.com:*/`。 

    |    URL    |    详细信息    |    匹配    |    不匹配    |
    |-------------------------------------------|--------------------------------------------------------|-------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
    |    `http://www.contoso.com`    |    匹配单个页面    |    `www.contoso.com`    |    `host.contoso.com`<br>`www.contoso.com/images`<br>`contoso.com/`    |
    |    `http://contoso.com`    |    匹配单个页面    |    `contoso.com/`    |    `host.contoso.com`<br>`www.contoso.com/images`<br>`www.contoso.com`    |
    |    `http://www.contoso.com/*`   |    匹配以 `www.contoso.com` 开头的所有 URL    |    `www.contoso.com`<br>`www.contoso.com/images`<br>`www.contoso.com/videos/tvshows`    |    `host.contoso.com`<br>`host.contoso.com/images`    |
    |    `http://*.contoso.com/*`    |    匹配 `contoso.com` 下的所有子域    |    `developer.contoso.com/resources`<br>`news.contoso.com/images`<br>`news.contoso.com/videos`    |    `contoso.host.com`<br>`news-contoso.com`
    |    `http://*contoso.com/*`    |    匹配以 `contoso.com/` 结尾的所有子域    |    `news-contoso.com`<br>`news-contoso.com.com/daily`    |    `news-contoso.host.com`<br>`news.contoso.com`    |
    `http://www.contoso.com/images`    |    匹配单个文件夹    |    `www.contoso.com/images`    |    `www.contoso.com/images/dogs`    |
    |    `http://www.contoso.com:80`    |    匹配单个页面（使用端口号）    |    `www.contoso.com:80`    |         |
    |    `https://www.contoso.com`    |    匹配单个安全页面    |    `www.contoso.com`    |    `www.contoso.com`    |
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
  - `http://www.contoso.com:*`
  - `http://www.contoso.com: /*`

### <a name="manage-proxy-configuration"></a>管理代理配置

可以将适用于 iOS 和 Android 的 Microsoft Edge 和 [Azure AD 应用程序代理](/azure/active-directory/active-directory-application-proxy-get-started)一起使用，使用户能够在其移动设备上访问 Intranet 站点。 例如： 

- 一个用户使用受 Intune 保护的 Outlook 移动应用。 然后，该用户单击电子邮件中一个指向 Intranet 站点的链接，适用于 iOS 和 Android 的 Microsoft Edge 识别出该站点已通过应用程序代理向用户公开。 将通过应用程序代理对用户进行自动路由，以便在进入 Intranet 站点前进行任何适用的多重身份验证和条件性访问。 该用户现在甚至可以在其移动设备上访问内部网站，而 Outlook 中的链接也如预期一样正常运行。
- 用户在其 iOS 或 Android 设备上打开适用于 iOS 和 Android 的 Microsoft Edge。 如果适用于 iOS 和 Android 的 Microsoft Edge 受 Intune 保护，并且应用程序代理已启用，则用户可使用其习惯使用的内部 URL 转到 Intranet 站点。 适用于 iOS 和 Android 的 Microsoft Edge 识别出这个 Intranet 站点已通过应用程序代理向用户公开。 通过应用程序代理自动对用户进行路由，以便在访问 Intranet 站点前进行身份验证。 

开始之前：

- 通过 Azure AD 应用程序代理设置内部应用程序。
  - 要配置应用程序代理和发布应用程序，请参阅[设置文档](/azure/active-directory/manage-apps/application-proxy)。
- 适用于 iOS 和 Android 的 Microsoft Edge 应用用户必须分配有 [Intune 应用保护策略](app-protection-policy.md)。
- Microsoft 应用必须具有以下应用保护策略：数据传输设置“限制与其他应用的 Web 内容传输”设置为“Microsoft Edge” 。

> [!NOTE]
> 更新后的应用程序代理重定向数据最长可能需要 24 小时才能在适用于 iOS 和 Android 的 Microsoft Edge 中生效。

使用以下键/值对将适用于 iOS 的 Microsoft Edge 作为目标，启用应用程序代理：

|    Key    |    值    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.AppProxyRedirection    |    “true”：启用 Azure AD 应用代理重定向方案<br>“false”（默认）：阻止 Azure AD 应用代理方案    |

> [!NOTE]
> 适用于 Android 的 Microsoft Edge 不使用此键。 相反，只要已登录的 Azure AD 帐户应用了应用保护策略，适用于 Android 的 Microsoft Edge 就会自动使用 Azure AD 应用程序代理配置。

若要深入了解适用于 iOS 和 Android 的 Microsoft Edge 和 Azure AD 应用程序代理如何相继配合使用，以实现本地 Web 应用的无缝（和受保护）访问，请参阅[更好地协作：配合使用 Intune 和 Azure Active Directory，改善用户访问](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/better-together-intune-and-azure-active-directory-team-up-to/ba-p/250254)。 此博客文章提到了 Intune Managed Browser，但该内容也适用于适用于 iOS 和 Android 的 Microsoft Edge。

### <a name="manage-ntlm-single-sign-on-sites"></a>管理 NTLM 单一登录站点

组织可能要求用户使用 NTLM 进行身份验证，以访问 Intranet 网站。 默认情况下，每次用户访问需要 NTLM 身份验证的网站时，系统都会提示用户输入凭据，因为 NTLM 凭据缓存已禁用。 

组织可以为特定网站启用 NTLM 凭据缓存。 对于这些站点，在用户输入凭据并成功进行身份验证之后，凭据会默认缓存 30 天。


|Key  |值  |
|---------|---------|
|com.microsoft.intune.mam.managedbrowser.NTLMSSOURLs     |键的对应值是 URL 列表。 将要允许的所有 URL 作为单个值输入，并用竖线 `|` 字符分隔。<p>**示例：**<br>`URL1|URL2`<br>`http://app.contoso.com/|https://expenses.contoso.com`<p>有关支持的 URL 格式类型的详细信息，请参阅[允许和阻止的站点列表的 URL 格式](#url-formats-for-allowed-and-blocked-site-list)。         |
|com.microsoft.intune.mam.managedbrowser.durationOfNTLMSSO     |缓存凭据的小时数，默认为 720 小时         |

## <a name="deploy-app-configuration-scenarios-with-microsoft-endpoint-manager"></a>使用 Microsoft Endpoint Manager 部署应用配置方案

如果你将 Microsoft Endpoint Manager 用作移动应用管理提供程序，则可通过以下步骤创建托管应用应用程序配置策略。 创建配置后，可以将其设置分配给用户组。

1. 登录 [Microsoft Endpoint Manager](https://endpoint.microsoft.com)。

2. 选择“应用”，然后选择“应用配置策略” 。

3. 在“应用配置策略”边栏选项卡上，选择“添加”，然后选择“托管应用” 。

4. 在“基本信息”部分，输入应用配置设置的“名称”和可选填的“描述” 。

5. 对于“公共应用”，选择“选择公共应用”，然后在“目标应用”边栏选项卡上，通过同时选择“iOS”和“Android”平台应用，选择“适用于 iOS 和 Android 的 Microsoft Edge”。 单击“选择”以保存所选的公共应用。

6. 单击“下一步”即可完成应用配置策略的基本设置。

7. 在“设置”部分，展开“Microsoft Edge 配置设置”。

8. 如果需要管理数据保护设置，请相应地配置所需的设置：

    - 对于“应用程序代理重定向”，请从以下可用选项中进行选择：“启用”“禁用”（默认）。

    - 对于“主页快捷方式 URL”，请指定一个有效的 URL，该 URL 需包括以下前缀之一：“http://”或“https://” 。 将阻止错误的 URL，这是一项安全措施。

    - 对于“托管书签”，请指定一个标题和一个有效的 URL，该 URL 需包括以下前缀之一：“http://”或“https://” 。

    - 对于“允许的 URL”，请指定一个有效的 URL（仅允许这些 URL；其他站点将无法访问）。 有关支持的 URL 格式类型的详细信息，请参阅[允许和阻止的站点列表的 URL 格式](#url-formats-for-allowed-and-blocked-site-list)。

    - 对于“阻止的 URL”，请指定一个有效的 URL（仅阻止这些 URL）。 有关支持的 URL 格式类型的详细信息，请参阅[允许和阻止的站点列表的 URL 格式](#url-formats-for-allowed-and-blocked-site-list)。

    - 对于“重定向到个人环境”，请从以下可用选项中进行选择：“启用”（默认）、“禁用” 。

    > [!NOTE]
    > 当策略中同时定义了允许的 URL 和阻止的 URL 时，仅会遵循允许列表。

9. 如果要添加上述策略未提供的应用配置设置，请展开“常规配置设置”节点，并相应地输入键值对。

10. 完成配置设置后，请单击“下一步”。

11. 在“分配”部分，选择“选择要包含的组” 。 选择要将应用配置策略分配到的 Azure AD 组，然后选择“选择”。

12. 完成分配后，选择“下一步”。

13. 在“创建应用配置策略审阅+创建”边栏选项卡上，查看配置的设置，然后选择“创建”。

新创建的配置策略显示在“应用配置”边栏选项卡上。

## <a name="use-edge-for-ios-and-android-to-access-managed-app-logs"></a>使用适用于 iOS 和 Android 的 Microsoft Edge 访问托管的应用日志

在 iOS 或 Android 设备上安装了适用于 iOS 和 Android 的 Microsoft Edge 的用户可查看所有 Microsoft 已发布应用的管理状态。 他们可以使用以下步骤发送日志，以便排查托管的 iOS 或 Android 应用的故障：

1. 在设备上打开适用于 iOS 和 Android 的 Microsoft Edge。
2. 在地址框中键入 `about:intunehelp`。
3. 适用于 iOS 和 Android 的 Microsoft Edge 会启动故障排除模式。

对于应用日志中存储的设置列表，请参阅[查看客户端应用保护日志](app-protection-policy-settings-log.md)。

若要了解如何在 Android 设备上查看日志，请参阅[通过电子邮件将日志发送给 IT 管理员](../user-help/send-logs-to-your-it-admin-by-email-android.md)。

## <a name="next-steps"></a>后续步骤

- [什么是应用保护策略？](app-protection-policy.md) 
- [Microsoft Intune 的应用配置策略](app-configuration-policies-overview.md)