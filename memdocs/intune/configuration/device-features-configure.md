---
title: 使用 Microsoft Intune 创建 iOS/iPadOS 或 macOS 设备配置文件 - Azure | Microsoft Docs
description: 使用 Microsoft Intune 添加或创建 iOS、iPadOS 或 macOS 设备配置文件，再配置 AirPrint 设置、主屏幕布局、应用通知、共享设备、单一登录和 Web 内容筛选器设置。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 04/09/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8e72fc48608ebf32f3e32d4a94ab7203ee418d8f
ms.sourcegitcommit: 0f02742301e42daaa30e1bde8694653e1b9e5d2a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2020
ms.locfileid: "82943801"
---
# <a name="add-ios-ipados-or-macos-device-feature-settings-in-intune"></a>使用 Intune 添加 iOS、iPadOS 或 macOS 设备功能设置

Intune 包含许多有助于管理员控制 iOS、iPadOS 和 macOS 设备的功能和设置。 例如，管理员可以：

- 允许用户有权在网络中访问 AirPrint 打印机
- 将应用和文件夹添加到主屏幕，包括添加新页面
- 选择是否以及如何显示应用通知
- 将锁定屏幕配置为显示消息或资产标记，特别是对于共享设备
- 为用户提供安全的单一登录体验，以在应用间共用凭据
- 筛选使用成人语言的网站，并允许或屏蔽特定网站

Intune 使用“配置文件”创建和自定义这些设置，从而满足组织需求。 在配置文件中添加这些功能后，需将此配置文件推送或部署到组织中的 iOS/iPadOS 和 macOS 设备。

本文介绍可配置的不同功能，并演示如何创建设备配置文件。 还可以查看所有适用于 [iOS/iPadOS](ios-device-features-settings.md) 和 [macOS](macos-device-features-settings.md) 设备的设置。

## <a name="airprint"></a>Airprint

Airprint 是允许设备通过无线网络打印到文件的 Apple 功能。 可以在 Intune 中将 AirPrint 信息添加到设备。

有关可以在 Intune 中配置的设置列表信息，请参阅 [iOS/iPadOS 上的 AirPrint](ios-device-features-settings.md#airprint) 和 [macOS 上的 AirPrint](macos-device-features-settings.md#airprint)。

有关 AirPrint 的详细信息，请参阅 Apple 网站上的[关于 AirPrint](https://support.apple.com/HT201311)。

适用于：

- iOS 7.0 及更高版本
- iPadOS 13.0 及更高版本
- macOS 10.10 及更高版本

## <a name="app-notifications"></a>应用通知

选择 iOS 和 iPadOS 设备上的应用接收通知的方式。 例如，从 Intune 发送应用通知，然后在通知中心、锁屏界面上显示它们，或发出提示音。

有关可以在 Intune 中配置的设置列表信息，请参阅 [iOS/iPadOS 上的应用通知](ios-device-features-settings.md#app-notifications)。

有关此功能的详细信息，请参阅 Apple 网站上的[通知](https://developer.apple.com/notifications/)。

适用于：

- iOS 9.3 及更高版本
- iPadOS 13.0 及更高版本

## <a name="associated-domains"></a>关联域

关联域允许在域（如 `contoso.com`）和应用之间建立关系。 可以使用此功能实现以下操作：

- 在组织的应用和网站之间共享数据和登录凭据。
- 使用基于网站的应用功能，例如单一登录应用扩展、通用链接和密码自动填充。

  例如，创建关联域，以允许密码自动填充推荐与应用关联的网站的凭据，如密码。

有关可以在 Intune 中配置的设置列表的信息，请参阅 [macOS 上的关联域](macos-device-features-settings.md#associated-domains)。

有关此功能的详细信息，请参阅 Apple 网站上的[设置应用的关联域](https://developer.apple.com/documentation/security/password_autofill/setting_up_an_app_s_associated_domains)。

适用于：

- macOS 10.15 及更高版本

## <a name="home-screen-layout"></a>主屏幕布局

这些设置配置 iOS 和 iPadOS 设备的停靠面板和主屏幕中的应用布局和文件夹。 你可以：

- 使用“停靠面板”设置将应用或文件夹添加到屏幕。  例如，在设备停靠面板上显示 Safari 和邮件应用。
- 添加要在主屏幕上显示的页面，以及要在每个页面上显示的应用。  例如，添加 Contoso 页，并在此页面上添加设置应用。 

有关可以在 Intune 中配置的设置列表信息，请参阅 [iOS/iPadOS 上的主屏幕布局](ios-device-features-settings.md#home-screen-layout)。

适用于：

- iOS 9.3 及更高版本
- iPadOS 13.0 及更高版本

## <a name="lock-screen-message"></a>锁屏界面消息

使用这些设置在登录窗口和锁定屏幕中显示自定义消息或文本。 例如，可输入“如果丢失，请送还至…”消息，然后显示资产标记信息。

有关可以在 Intune 中配置的设置列表信息，请参阅 [iOS/iPadOS 上的锁屏界面消息设置](ios-device-features-settings.md#lock-screen-message)。

有关锁屏界面消息的详细信息，请参阅 Apple 网站上的 [LockScreenMessage](https://developer.apple.com/documentation/devicemanagement/lockscreenmessage)。

适用于：

- iOS 9.3 及更高版本
- iPadOS 13.0 及更高版本

## <a name="login-items"></a>登录项

使用此功能选择用户登录到设备时打开的应用、自定义应用、文件和文件夹。

有关可以在 Intune 中配置的设置列表的信息，请参阅 [macOS 上的登录项](macos-device-features-settings.md#login-items)。

适用于：

- macOS 10.13 及更高版本

## <a name="login-window"></a>登录窗口

控制登录屏幕外观以及用户登录前向用户提供的功能。 例如，添加带有自定义消息的横幅，选择是否显示睡眠按钮等。

有关可以在 Intune 中配置的设置列表的信息，请参阅 [macOS 上的登录窗口](macos-device-features-settings.md#login-window)。

适用于：

- macOS 10.7 及更高版本

## <a name="single-sign-on"></a>单一登录

大多数业务线 (LOB) 应用需要某种级别的用户身份验证，才能支持安全性。 在许多情况下，此类身份验证要求用户重复输入相同凭据。 为了提升用户体验，开发人员可以创建使用单一登录 (SSO) 的应用。 使用单一登录减少了用户必须输入凭据的次数。

单一登录配置文件基于 Kerberos。 Kerberos 是一种网络身份验证协议，它使用密钥加密来对客户端-服务器应用程序进行身份验证。 Intune 设置在访问服务器或指定应用时定义 Kerberos 帐户信息，并处理网页和本机应用的 Kerberos 质询。 Apple 建议使用 [Kerberos SSO 应用扩展](#single-sign-on-app-extension)（在本文中）设置，而不是 SSO 设置。  

若要使用单一登录，请务必确保：

- 已将应用编码为，在设备上的单一登录中查找用户凭据存储。
- Intune 配置有 iOS/iPadOS 设备单一登录。

有关可以在 Intune 中配置的设置列表信息，请参阅 [iOS/iPadOS 上的单一登录](ios-device-features-settings.md#single-sign-on)。

适用于：

- iOS 7.0 及更高版本
- iPadOS 13.0 及更高版本

## <a name="single-sign-on-app-extension"></a>单一登录应用扩展

这些设置将配置可为 iOS、iPadOS 和 macOS 设备启用单一登录 (SSO) 的应用扩展。 大多数业务线 (LOB) 应用和组织网站需要某种级别的安全的用户身份验证。 在许多情况下，此类身份验证要求用户重复输入相同凭据。 借助 SSO，用户输入一次凭据后，即可访问应用和网站。 SSO 还为用户提供了更好的身份验证体验，并减少了重复提示输入凭据的次数。

在 Intune 中，使用这些设置配置由组织、标识提供者、Microsoft 或 Apple 创建的 SSO 应用扩展。 SSO 应用扩展将处理对用户的身份验证。 这些设置可配置重定向类型和凭据类型 SSO 应用扩展。

- 重定向类型适用于 OpenID Connect、OAuth 和 SAML2 等新式身份验证协议。 可在 macOS 设备上使用通用的重定向扩展。 对于 iOS/iPadOS 设备，可在 Microsoft 的 Azure AD SSO 扩展（[Microsoft 企业 SSO 插件](https://docs.microsoft.com/azure/active-directory/develop/apple-sso-plugin)）和通用重定向扩展之间进行选择。
- 凭据类型适用于质询与响应身份验证流。 可选择通用凭据扩展或者 Apple 提供的 Kerberos 专属凭据扩展。

有关可以在 Intune 中配置的设置列表信息，请参阅 [iOS/iPadOS SSO 应用扩展](ios-device-features-settings.md#single-sign-on-app-extension)和 [macOS SSO 应用扩展](macos-device-features-settings.md#single-sign-on-app-extension)。

有关开发 SSO 应用扩展的详细信息，请观看 Apple 网站上的[可扩展的企业 SSO](https://developer.apple.com/videos/play/tech-talks/301)。 若要阅读 Apple 的功能说明，请访问[“单一登录扩展”有效负载设置](https://support.apple.com/guide/mdm/single-sign-on-extensions-mdmfd9cdf845/web)。 

> [!NOTE]
> 单一登录应用扩展功能不同于单一登录功能：  
>
> - “单一登录应用扩展”设置适用于 iPadOS 13.0、iOS 13.0 和 macOS 10.15（以及它们的更高版本）  。 单一登录设置适用于 iPadOS 13.0（以及更高版本）和 iOS 7.0 以及更高版本。 
>
> - “单一登录应用扩展”设置定义了供标识提供者或组织使用的扩展，以提供无缝的企业登录体验  。 “单一登录”设置定义了有关用户访问服务器或应用时的 Kerberos 帐户信息  。
>
> - 单一登录应用扩展使用 Apple 操作系统进行身份验证。  因此，它可能会提供比单一登录  更棒的最终用户体验。
>
> - 从开发角度而言，使用单一登录应用扩展，你可以使用任意类型的重定向 SSO 或凭据 SSO 身份验证  。 使用单一登录时，只可以使用 Kerberos SSO 身份验证。 
>
> - Kerberos 单一登录应用扩展由 Apple 开发，内置于 iOS/iPadOS 13.0 + 和 macOS 10.15 + 平台中  。 内置的 Kerberos 扩展可用于将用户登录到支持 Kerberos 身份验证的本机应用和网站。 单一登录不是 Kerberos 的 Apple 实现  。
>
> - 内置的 Kerberos 单一登录应用扩展可以像单一登录一样处理网页和应用的 Kerberos 质询   。 不过，内置的 Kerberos 扩展支持密码更改，并且在企业网络中效果更佳。 在 Kerberos 单一登录应用扩展和单一登录之间进行选择时，由于扩展可以提高性能和功能，因此我们建议使用前者   。

适用于：

- iOS 13.0 及更高版本
- iPadOS 13.0 及更高版本
- macOS 10.15 及更高版本

## <a name="wallpaper"></a>壁纸

将自定义 .png、.jpg 或 .jpeg 图像添加到受监督的 iOS/iPadOS 设备。 例如，使用 Intune 将公司徽标添加到设备的锁屏界面。

有关可以在 Intune 中配置的设置列表信息，请参阅 [iOS/iPadOS 上的壁纸](ios-device-features-settings.md#wallpaper)。

适用于：

- iOS
- iPadOS 13.0 及更高版本

## <a name="web-content-filter"></a>Web 内容筛选器

这些设置使用 Apple 的内置自动筛选算法评估网页，并阻止成人内容和成人语言。 还可以创建允许的 Web 链接和限制的 Web 链接列表。 例如，可以仅允许 `contoso` 网站打开。

有关可以在 Intune 中配置的设置列表信息，请参阅 [iOS/iPadOS 上的 Web 内容筛选器](ios-device-features-settings.md#web-content-filter)。

适用于：

- iOS 7.0 及更高版本
- iPadOS 13.0 及更高版本

## <a name="create-the-profile"></a>创建配置文件

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“设备”   > “配置文件”   > “创建配置文件”  。
3. 输入以下属性：

    - **平台**：选择设备平台。 选项包括：  

        - **iOS/iPadOS**
        - **macOS**

    - **配置文件**：选择“设备功能”  。

4. 选择“创建”。 
5. 在“基本信息”  中，输入以下属性：

    - **名称**：输入策略的描述性名称。 为策略命名，以便稍后可以轻松地识别它们。 例如，策略名称最好是“macOS：配置登录屏幕”  。
    - **描述**：输入策略的说明。 此设置是可选的，但建议进行。

6. 选择“下一步”  。

7. 在“配置设置”  中，根据所选择的平台，可配置的设置有所不同。 选择平台，以了解详细设置：

    - [iOS/iPadOS](ios-device-features-settings.md)
    - [macOS](macos-device-features-settings.md)

8. 选择“下一步”  。
9. 在“作用域标记”（可选）中，分配一个标记以将配置文件筛选到特定 IT 组（如 `US-NC IT Team` 或 `JohnGlenn_ITDepartment`）  。 有关范围标记的详细信息，请参阅[将 RBAC 和范围标记用于分布式 IT](../fundamentals/scope-tags.md)。

    选择“下一步”  。

10. 在“分配”中，选择将接收配置文件的用户或组  。 有关分配配置文件的详细信息，请参阅[分配用户和设备配置文件](device-profile-assign.md)。

    选择“下一步”  。

11. 在“查看并创建”中查看设置  。 选择“创建”时，将保存所做的更改并分配配置文件  。 该策略也会显示在配置文件列表中。

## <a name="next-steps"></a>后续步骤

此时，配置文件创建完成，但它可能尚未执行任何操作。 下一步，[分配配置文件](device-profile-assign.md)并[监视其状态](device-profile-monitor.md)。

查看所有适用于 [iOS/iPadOS](ios-device-features-settings.md) 和 [macOS](macos-device-features-settings.md) 设备的设备功能设置。
