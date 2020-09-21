---
title: Microsoft Intune 中的 iOS/iPadOS 设备功能设置 - Azure | Microsoft Docs
description: 查看 Microsoft Intune 中所有用于为 iOS 和 iPadOS 设备配置 AirPrint、主屏幕布局、应用通知、共享设备、单一登录和 Web 内容筛选器设置的设置。 在设备配置文件中使用这些设置，将 iOS 和 iPadOS 设备配置为在组织中使用 Apple 的这些功能。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 09/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: ''
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6989dc3559a1de950f5d2ec8280894f1f1983b61
ms.sourcegitcommit: cba06c182646cb6dceef304b35230bf728d5133e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90574858"
---
# <a name="ios-and-ipados-device-settings-to-use-common-iosipados-features-in-intune"></a>用于使用 Intune 中常见 iOS/iPadOS 功能的 iOS 和 iPadOS 设备设置

Intune 包括一些内置设置，可便于 iOS/iPadOS 用户在自己的设备上使用各种 Apple 功能。 例如，你可以控制 AirPrint 打印机、将应用和文件夹添加到程序坞和主屏幕页面、显示应用通知、在锁定屏幕上显示资产标记详细信息、使用单一登录身份验证，以及使用证书身份验证。

使用这些功能可以控制 iOS/iPadOS 设备，作为移动设备管理 (MDM) 解决方案的一部分。

本文列出了这些设置，并介绍了每个设置的用途。 有关这些功能的详细信息，请参阅[添加 iOS/iPadOS 或 macOS 设备功能设置](device-features-configure.md)。

## <a name="before-you-begin"></a>在开始之前

[创建 iOS/iPadOS 设备功能配置文件](device-features-configure.md)。

> [!NOTE]
> 这些设置适用于不同的注册类型，其中一些设置应用于所有注册选项。 有关不同注册类型的详细信息，请参阅 [iOS/iPadOS 注册](../enrollment/ios-enroll.md)。

## <a name="airprint"></a>AirPrint

### <a name="settings-apply-to-all-enrollment-types"></a>设置适用范围：所有注册类型

> [!NOTE]
> 请确保将所有打印机添加到同一个配置文件。 Apple 禁止多个 AirPrint 配置文件面向同一设备。

- **IP 地址**：输入打印机的 IPv4 或 IPv6 地址。 如果使用主机名标识打印机，可以通过在“终端”中对打印机执行 ping 操作来获取 IP 地址。 （本文中的）获取 IP 地址和路径提供了更多详细信息。
- **路径**：网络中打印机的路径通常是 `ipp/print`。 （本文中的）获取 IP 地址和路径提供了更多详细信息。
- **端口**：输入 AirPrint 目标的侦听端口。 如果将此属性留空，AirPrint 使用默认端口。 适用于 iOS 11.0 以上版本和 iPadOS 13.0 以上版本。
- **TLS**：“启用”则可使用传输层安全性 (TLS) 确保 AirPrint 连接安全。 适用于 iOS 11.0 以上版本和 iPadOS 13.0 以上版本。

若要添加 AirPrint 服务器，可以执行以下操作：

- **添加**：将 AirPrint 服务器添加到列表中。 可以添加多个 AirPrint 服务器。
- 导入包含此类信息的逗号分隔文件 (.csv)。 或者，“导出”以创建所添加的 AirPrint 服务器的列表。

### <a name="get-server-ip-address-resource-path-and-port"></a>获取服务器 IP 地址、资源路径和端口

必须有打印机的 IP 地址、资源路径和端口，才能添加 AirPrinter 服务器。 下面逐步介绍了如何获取此类信息。

1. 在作为 AirPrint 打印机连接到同一本地网络（子网）的 Mac 上，打开“终端”（路径为“/Applications/Utilities” ）。
2. 在“终端”中，键入“`ippfind`”，再按 Enter。

    记下打印机信息。 例如，可能会返回类似于 `ipp://myprinter.local.:631/ipp/port1` 的内容。 第一部分是打印机名称。 最后一部分 (`ipp/port1`) 是资源路径。

3. 在“终端”中，键入“`ping myprinter.local`”，再按 Enter。

   记下 IP 地址。 例如，可能会返回类似于 `PING myprinter.local (10.50.25.21)` 的内容。

4. 使用 IP 地址和资源路径值。 在此示例中，IP 地址为 `10.50.25.21`，资源路径为 `/ipp/port1`。

## <a name="home-screen-layout"></a>主屏幕布局

此功能适用于：

- iOS 9.3 或更高版本
- iPadOS 13.0 及更高版本

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>设置适用范围：自动设备注册（监督）

> [!NOTE]
> 仅向停靠、页面或页面上的文件夹添加一个应用。 在所有位置添加相同的应用可防止该应用在设备上显示，并可能显示报告错误。
>
> 例如，如果将相机应用添加到停靠和页面，则不会显示相机应用，并且报告可能会显示策略错误。 若要将相机应用添加到主屏幕布局中，请仅选择停靠或页面，而不是同时选择两者。

### <a name="dock"></a>程序坞

使用“程序坞”设置最多可以向屏幕的程序坞添加六个项或文件夹。 许多设备支持添加的项数更少。 例如，iPhone 设备最多支持添加四个项。 在此示例中，设备上仅显示你添加的前四个项。

最多可以对设备程序坞添加六个项（应用和文件夹加起来）。

- **添加**：将应用或文件夹添加到设备上的扩展坞。
- **类型**：添加应用或文件夹 ：

  - **应用**：选择此选项可向屏幕上的程序坞添加应用。 输入：

    - **应用名称**：输入应用程序的名称。 此名称用于在 Microsoft 终结点管理器管理中心内的引用。 它不会显示在 iOS/iPadOS 设备上。
    - **应用捆绑 ID**：输入应用的捆绑 ID。 有关示例，请参阅[内置 iOS/iPadOS 应用的捆绑 ID](bundle-ids-built-in-ios-apps.md)。

  - **文件夹**：选择此选项可向屏幕上的程序坞添加文件夹。

    添加到文件夹中页面的应用按照列表中的相同顺序从左向右排列。 如果添加的应用数超过了页面能够容纳的量，应用会移到其他页面。

    - **文件夹名称**：输入文件夹的名称。 该名称将显示在用户的设备上。
    - **页面列表**：添加页面，并输入以下属性：

      - **页面名称**：输入页面名称。 此名称用于在 Microsoft 终结点管理器管理中心内的引用。 它不会显示在 iOS/iPadOS 设备上。
      - **应用名称**：输入应用程序的名称。 此名称用于在 Microsoft 终结点管理器管理中心内的引用。 它不会显示在 iOS/iPadOS 设备上。
      - **应用捆绑 ID**：输入应用的捆绑 ID。 有关示例，请参阅[内置 iOS/iPadOS 应用的捆绑 ID](bundle-ids-built-in-ios-apps.md)。

      最多可以对设备程序坞添加 20 个页面。

> [!NOTE]
> 如果你使用“主屏幕布局”设置添加页面或将页面和应用添加到程序坞，主屏幕和页面上的图标就会被锁定。 无法移动或删除它们。 此行为可能是根据 iOS/iPadOS 和 Apple 的 MDM 策略特意设计的。

#### <a name="example"></a>示例

在下面的示例中，程序坞屏幕显示“Safari”、“邮件”和“股市”应用。 “邮件”应用被选为显示自己的属性：

> [!div class="mx-imgBorder"]
> ![Intune 中的示例 iOS/iPadOS 主屏幕布局程序坞设置](./media/ios-device-features-settings/dock-screen-mail-app.png)

在你向 iPhone 分配策略后，程序坞如下图所示：

> [!div class="mx-imgBorder"]
> ![iPhone 上的示例 iOS/iPadOS 程序坞布局](./media/ios-device-features-settings/bAgCe8F.png)

### <a name="pages"></a>页面

添加要在主屏幕上显示的页面，以及要在每个页面上显示的应用。 添加到页面中的应用按照列表中的相同顺序从左向右排列。 如果添加的应用数超过了页面能够容纳的量，应用会移到其他页面。

> [!TIP]
> 若要对任何主屏幕和页面列表中的项重新排序，可以拖放这些项。

最多可以在设备上添加 40 个页面。

- **页面列表**：添加页面，并输入以下属性：

  - **页面名称**：输入页面名称。 此名称用于在 Microsoft 终结点管理器管理中心内的引用，而不会显示在 iOS/iPadOS 设备上。

  最多可以在设备上添加 60 个项（应用和文件夹加起来）。

  - **添加**：将应用或文件夹添加到设备上的页面。

    - **类型**：添加应用或文件夹 ：

      - **应用**：选择此选项可向屏幕上的页面添加应用。 此外请输入：

        - **应用名称**：输入应用程序的名称。 此名称用于在 Microsoft 终结点管理器管理中心内的引用。 它不会显示在 iOS/iPadOS 设备上。
        - **应用捆绑 ID**：输入应用的捆绑 ID。 有关示例，请参阅[内置 iOS/iPadOS 应用的捆绑 ID](bundle-ids-built-in-ios-apps.md)。

      - **文件夹**：选择此选项可向屏幕上的程序坞添加文件夹。

        添加到文件夹中页面的应用按照列表中的相同顺序从左向右排列。 如果添加的应用数超过了页面能够容纳的量，应用会移到其他页面。

        - **文件夹名称**：输入文件夹的名称。 此名称在设备上向用户显示。
        - **添加**：将页面添加到文件夹。 同时输入以下属性：

          - **页面名称**：输入页面名称。 此名称用于在 Microsoft 终结点管理器管理中心内的引用。 它不会显示在 iOS/iPadOS 设备上。
          - **应用名称**：输入应用程序的名称。 此名称用于在 Microsoft 终结点管理器管理中心内的引用。 它不会显示在 iOS/iPadOS 设备上。
          - **应用捆绑 ID**：输入应用的捆绑 ID。 有关示例，请参阅[内置 iOS/iPadOS 应用的捆绑 ID](bundle-ids-built-in-ios-apps.md)。

#### <a name="example"></a>示例

在下面的示例中，添加了名为“Contoso”的新页面。 此页面显示“查找朋友”和“设置”应用：

> [!div class="mx-imgBorder"]
> ![Intune 中的 iOS/iPadOS 主屏幕布局新页面设置和示例](./media/ios-device-features-settings/page-find-friends-settings-apps.png)

“设置”应用被选为显示自己的属性：

> [!div class="mx-imgBorder"]
> ![Intune 中的 iOS/iPadOS 主屏幕布局设置应用属性示例](./media/ios-device-features-settings/page-settings-app-properties.png)

在你向 iPhone 分配策略后，页面如下图所示：

> [!div class="mx-imgBorder"]
> ![Intune 中已修改主屏幕的 iOS/iPadOS 设备](./media/ios-device-features-settings/Bd37PHa.png)

## <a name="app-notifications"></a>应用通知

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>设置适用范围：自动设备注册（监督）

- **添加**：添加应用通知：

  > [!div class="mx-imgBorder"]
  > ![在 Intune 中的 iOS/iPadOS 配置文件内添加应用通知](./media/ios-device-features-settings/ios-ipados-app-notifications.png)

  - **应用捆绑 ID**：输入要添加的应用的“应用捆绑 ID”。 有关示例，请参阅[内置 iOS/iPadOS 应用的捆绑 ID](bundle-ids-built-in-ios-apps.md)。
  - **应用名称**：输入要添加的应用的名称。 此名称用于在 Microsoft 终结点管理器管理中心内的引用。 它不会显示在设备上。
  - **发布者**：输入要添加的应用的发布者。 此名称用于在 Microsoft 终结点管理器管理中心内的引用。 它不会显示在设备上。
  - **通知**：选择“启用”或“禁用”可启用或禁用应用向设备发送通知 。
    - **在通知中心内显示**：选择“启用”可允许应用在设备通知中心内显示通知。 选择“禁用”可阻止应用在设备通知中心内显示通知。
    - **在锁定屏幕中显示**：选择“启用”可在设备锁定屏幕上显示应用通知。 选择“禁用”可阻止应用在锁定屏幕中显示通知。
    - **警报类型**：解锁设备后，选择通知的显示方式。 选项包括：
      - **无**：不显示通知。
      - **横幅**：短暂显示包含通知的横幅。
      - **模式**：显示通知，并且用户必须先手动关闭通知，然后才能继续使用设备。
    - **应用图标上的通知提醒**：选择“启用”可向应用图标添加通知提醒。 通知提醒表示应用已发送通知。
    - **声音**：选择“启用”可在通知送达时播放声音。

## <a name="lock-screen-message"></a>锁屏界面消息

此功能适用于：

- iOS 9.3 及更高版本
- iPadOS 13.0 及更高版本

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>设置适用范围：自动设备注册（监督）

- **资产标记信息：** 输入有关该设备资产标记的信息。 例如，输入 `Owned by Contoso Corp` 或 `Serial Number: {{serialnumber}}`。

  输入的文本显示在设备上的登录窗口和锁定屏幕中。

- **锁屏脚注：** 输入一个可帮助在设备丢失或被盗时将其找回的注释。 可以输入所需的任何文本。 例如，输入类似于 `If found, call Contoso at ...` 的内容。

  设备令牌还可以用于向这些字段添加特定于设备的信息。 例如，若要显示序列号，请输入 `Serial Number: {{serialnumber}}` 或 `Device ID: {{DEVICEID}}`。 在锁屏上，文本显示类似于 `Serial Number 123456789ABC`。 输入变量时，请务必使用大括号 `{{ }}`。 [应用配置令牌](../apps/app-configuration-policies-use-ios.md#tokens-used-in-the-property-list)包含可用变量的列表。 还可以使用 `DEVICENAME` 或任何其他特定于设备的值。

  > [!NOTE]
  > 变量不在 UI 中进行验证，且区分大小写。 因此，可能会看到使用不正确输入保存的配置文件。 例如，如果输入 `{{DeviceID}}` 而不是 `{{deviceid}}` 或“{{DEVICEID}}”，则显示文本字符串而不是设备的唯一 ID。 请确保输入正确的信息。 支持全部小写或全部大写的变量，但不支持混合使用。 

## <a name="single-sign-on"></a>单一登录

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>设置适用范围：设备注册、自动设备注册（受监督）

- **领域**：输入 URL 的域部分。 例如，输入 `contoso.com`。
- **Kerberos 主体名称**：Intune 为 Azure AD 中的每个用户查找此属性。 然后，Intune 先填充相应字段（如“UPN”），再生成在设备上安装的 XML。 选项包括：

  - **未配置**：Intune 不会更改或更新此设置。 默认情况下，将配置文件部署到设备时，操作系统将提示用户提供 Kerberos 主体名称。 MDM 安装 SSO 配置文件时需要使用主体名称。
  - **用户主体名称**：将按以下方式分析用户主体名称 (UPN)：

    > [!div class="mx-imgBorder"]
    > ![Intune 中的 iOS/iPadOS 用户名 SSO 属性](./media/ios-device-features-settings/User-name-attribute.png)

    还可以使用在“领域”文本框中键入的文本覆盖该领域。

    例如，Contoso 有多个区域，包括欧洲、亚洲和北美。 Contoso 希望亚洲用户使用 SSO，且应用要求采用 `username@asia.contoso.com` 格式的 UPN。 在你选择“用户主体名称”后，系统从 Azure AD 中获取每个用户的领域，即 `contoso.com`。 因此，对于亚洲用户，选择“用户主体名称”，再输入“`asia.contoso.com`”。 用户的 UPN 变成 `username@asia.contoso.com`，而不是 `username@contoso.com`。

  - **Intune 设备 ID**：Intune 自动选择 Intune 设备 ID。

    默认情况下，应用只需使用设备 ID。 但如果应用使用领域和设备 ID，则你可在“领域”文本框中键入领域。

    > [!NOTE]
    > 如果使用设备 ID，则默认将领域留空。

  - **Azure AD 设备 ID**
  - **SAM 帐户名**：Intune 将填充本地安全帐户管理器 (SAM) 帐户名。


- **应用**：在用户设备上添加可使用单一登录的应用。

  `AppIdentifierMatches` 数组必须包含与应用捆绑 ID 匹配的字符串。 这些字符串可以是完全匹配项（如 `com.contoso.myapp`），也可以使用 \* 通配符输入捆绑 ID 的前缀匹配项。 通配符必须位于句点字符 (.) 后面，并只能在字符串末尾出现一次（如 `com.contoso.*`）。 如果包括通配符，则程序包 ID 以前缀开头的任何应用都将被授予对帐户的访问权限。

  使用应用名称输入一个用户友好名称，帮助识别捆绑 ID。

- **URL 前缀**：添加组织中任何要求用户进行单一登录身份验证的 URL。

  例如，用户连接到任何这些站点时，iOS/iPadOS 设备会使用单一登录凭据。 用户不需要输入任何其他凭据。 如果已启用多重身份验证，用户必须输入第二重身份验证凭据。

  > [!NOTE]
  > 这些 URL 必须采用正确格式化的 FQDN。 Apple 要求这些 URL 必须采用 `http://<yourURL.domain>` 格式。

  匹配模式的 URL 必须以 `http://` 或 `https://` 开头。 由于运行的是简单字符串匹配，因此 `http://www.contoso.com/` URL 前缀与 `http://www.contoso.com:80/` 不匹配。 在 iOS 10.0 以上版本和 iPadOS 13.0 以上版本中，可使用一个通配符 \* 输入所有匹配值。 例如，`http://*.contoso.com/` 同时匹配 `http://store.contoso.com/` 和 `http://www.contoso.com`。

  `http://.com` 和 `https://.com` 模式分别匹配所有 HTTP 和 HTTPS URL。

- **续订证书**：如果使用证书（而不是密码）进行身份验证，选择现有 SCEP 或 PFX 证书作为身份验证证书。 通常，此证书是针对其他配置文件（如 VPN、Wi-Fi 或电子邮件）部署到用户的相同证书。

## <a name="web-content-filter"></a>Web 内容筛选器

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>设置适用范围：自动设备注册（监督）

- **筛选器类型**：选择以允许特定网站。 选项包括：

  - **配置 URL**：使用 Apple 的内置 Web 筛选器来查找成人术语，包括猥亵和露骨色情语言。 此功能在网页加载时评估每个网页，并发现和阻止不适合的内容。 还可以添加不希望筛选器检查的 URL。 或屏蔽特定 URL，无论 Apple 的筛选器设置如何。

    - **允许的 URL**：添加要允许的 URL。 这些 URL 可绕过 Apple 的 Web 筛选器。

        > [!NOTE]
        > 输入的 URL 是你不希望 Apple Web 筛选器评估的 URL。 这些 URL 不是允许的网站列表。 若要创建允许的网站列表，请将“筛选器类型”设置为“仅特定网站”。

    - **屏蔽的 URL**：添加要阻止打开的 URL，无论 Apple Web 筛选器设置如何。

  - **仅特定网站**（仅适用于 Safari Web 浏览器）：这些 URL 会添加到 Safari 浏览器的书签中。 用户只能访问这些网站；无法打开其他任何网站。 仅在知道用户可以访问的 URL 的确切列表时使用此选项。

    - **URL**：输入要允许的网站的 URL。 例如，输入 `https://www.contoso.com`。
    - **书签路径**：Apple 更改了此设置。 所有书签都将进入“已批准的站点”文件夹。 书签不会进入你输入的书签路径。
    - **标题**：输入书签的描述性标题。

    如果未输入任何 URL，则用户无法访问任何网站（`microsoft.com`、`microsoft.net` 和 `apple.com` 除外）。 Intune 自动允许这些 URL。

## <a name="single-sign-on-app-extension"></a>单一登录应用扩展

此功能适用于：

- iOS 13.0 及更高版本
- iPadOS 13.0 及更高版本

### <a name="settings-apply-to-all-enrollment-types"></a>设置适用范围：所有注册类型

- **SSO 应用扩展类型**：选择 SSO 应用扩展的类型。 选项包括：

  - **未配置**：Intune 不会更改或更新此设置。 默认情况下，操作系统不会使用应用扩展。 若要禁用应用扩展，可将 SSO 应用扩展类型切换为“未配置”。
  - **Microsoft Azure AD**：使用 Microsoft 企业 SSO 插件，它是一个重定向类型的 SSO 应用扩展。 此插件为所有支持 [Apple 企业单一登录](https://developer.apple.com/documentation/authenticationservices)功能的应用程序提供 Active Directory 帐户的 SSO。 使用此 SSO 应用扩展类型可在使用 Azure AD 进行身份验证的 Microsoft 应用、组织应用和网站上启用 SSO。

    SSO 插件充当高级身份验证代理，可改进安全性和用户体验。 对于使用 Microsoft Authenticator 应用进行身份验证的所有应用，都将继续获取具有[适用于 Apple 设备的 Microsoft 企业 SSO 插件](/azure/active-directory/develop/apple-sso-plugin)的 SSO。

    > [!IMPORTANT]
    > 要通过 Microsoft Azure AD SSO 应用扩展类型实现 SSO，请先在设备上安装 iOS/iPadOS 版 Microsoft Authenticator 应用。 Authenticator 应用将 Microsoft 企业 SSO 插件传递到设备，MDM SSO 应用扩展设置会激活该插件。 在设备上安装 Authenticator 和 SSO 应用扩展配置文件后，用户必须在设备上输入其凭据才能登录和建立会话。 然后，该会话可在不同的应用程序中使用，而无需用户再次进行身份验证。 有关 Authenticator 的详细信息，请参阅[什么是 Microsoft Authenticator 应用](/azure/active-directory/user-help/user-help-auth-app-overview)。

  - **重定向**：使用通用的可自定义重定向应用扩展，通过新式身份验证流使用 SSO。 确保你知道组织应用扩展的扩展 ID。
  - **凭据**：使用通用的可自定义凭据应用扩展，通过质询和响应身份验证流来使用 SSO。 确保你知道组织应用扩展的扩展 ID。
  - **Kerberos**：使用 Apple 的内置 Kerberos 扩展，该扩展包含在 iOS 13.0 以上版本和 iPadOS 13.0 以上版本中。 此选项是“凭据”应用扩展的 Kerberos 特定版本。

  > [!TIP]
  > 使用“重定向”和“凭据”类型，可以添加自己的配置值以传递扩展。 如果使用的是“凭据”，请考虑使用 Apple 在“Kerberos”类型中提供的内置配置设置。

- **共享设备模式**（仅用于 Microsoft Azure AD）：如果要将 Microsoft 企业 SSO 插件部署到已配置支持 Azure AD 共享设备模式功能的 iOS/iPadOS 设备，请选择“启用”。 通过共享模式下的设备，多名用户可以全局方式在支持共享设备模式的应用程序中登录和注销。 设置为“未配置”时，Intune 不会更改或更新此设置。 默认情况下，iOS/iPadOS 设备不会在多名用户之间共享。

  要详细了解共享设备模式及其启用方式，请参阅[共享设备模式概述](/azure/active-directory/develop/msal-shared-devices)以及[适用于 iOS 设备的共享设备模式](/azure/active-directory/develop/msal-ios-shared-devices)。  

  此功能适用于：
  
  - iOS/iPadOS 13.5 及更高版本

- **扩展 ID**（“重定向”和“凭据”）：输入可标识 SSO 应用扩展的程序包标识符，如 `com.apple.extensiblesso`。

- **团队 ID**（“重定向”和“凭据”）：输入 SSO 应用扩展的团队标识符。 团队标识符是由 Apple 生成的 10 个字符的字母数字（包含数字和字母）字符串，如 `ABCDE12345`。 不需要团队 ID。

  [找到你的团队 ID](https://help.apple.com/developer-account/#/dev55c3c710c)（打开 Apple 网站）提供了详细信息。

- **领域**（“重定向”和“Kerberos”）：输入身份验证领域的名称。 领域名称应为大写形式，如 `CONTOSO.COM`。 通常情况下，你的领域名称与 DNS 域名相同，但全部为大写形式。

- **域**（“凭据”和“Kerberos”）：输入可通过 SSO 进行身份验证的站点的域名或主机名。 例如，如果你的网站是 `mysite.contoso.com`，则 `mysite` 为主机名，`contoso.com` 为域名。 当用户连接到这些站点中的任何一个时，应用扩展会处理身份验证质询。 通过此身份验证，用户可以使用 Face ID、Touch ID 或 Apple PIN 码/密码登录。

  - 单一登录应用扩展 Intune 配置文件中的所有域都必须是唯一的。 即使使用的是不同类型的 SSO 应用扩展，也不能在任何登录应用扩展配置文件中使用重复的域。
  - 这些域不区分大小写。

- **URL**（仅用于“重定向”）：输入标识提供者的 URL 前缀，重定向应用扩展将代表它们使用 SSO。 当用户重定向到这些 URL 时，SSO 应用扩展会介入并提示 SSO。

  - Intune 单一登录应用扩展配置文件中的所有 URL 都必须是唯一的。 即使使用的是不同类型的 SSO 应用扩展，也不能在任何 SSO 应用扩展配置文件中使用重复的域。
  - URL 必须以 `http://` 或 `https://` 开头。

- **其他配置**（Microsoft Azure AD、“重定向”和“凭据”）：输入要传递到 SSO 应用扩展的其他扩展特定数据：
  - **密钥**：输入要添加的项的名称，如 `user name`。 `AppAllowList` 区分大小写。 请确保准确输入“AppAllowList”。 
  - **类型**：输入数据的类型。 选项包括：

    - 字符串
    - 布尔值：在“配置值”中，输入 `True` 或 `False`。
    - 整数：在“配置值”中，输入一个数字。

  - **值**：输入数据。

  - **添加**：选择此项可添加配置密钥。

- **密钥链用法**（仅用于“Kerberos”）：设置为“阻止”可阻止在密钥链中保存和存储密码。 如果被阻止，系统不会提示用户保存其密码，并且用户在 Kerberos 票证过期时需要重新输入密码。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。 默认情况下，OS 可能允许保存密码并将其存储在密钥链中。 票证过期时，系统不会提示用户重新输入其密码。
- **Face ID、Touch ID 或密码**（仅用于“Kerberos”）：如果选择“需要”，则强制用户在需要凭据以刷新 Kerberos 票证时输入其 Face ID、Touch ID 或设备密码。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。 默认情况下，OS 可能不需要用户使用生物特征或设备密码来刷新 Kerberos 票证。 如果“密钥链用法”被阻止，则此设置不适用。
- **默认领域**（仅用于“Kerberos”）：选择“启用”可将入的“领域”值设置为默认领域 。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。 默认情况下，OS 可能未设置默认领域。

  > [!TIP]
  > - 如果要在组织中配置多个 Kerberos SSO 应用扩展，请“启用”此设置。
  > - 如果要使用多个领域，请“启用”此设置。 它将你输入的“领域”值设置为默认领域。
  > - 如果只有一个领域，请将其保留为“未配置”（默认设置）。

- **主体名称**（仅用于“Kerberos”）：输入 Kerberos 主体的用户名。 不需要加上领域名称。 例如，在 `user@contoso.com` 中，`user` 是主体名称，`contoso.com` 是领域名称。

  > [!TIP]
  > - 还可以通过输入大括号 `{{ }}` 来使用主体名称中的变量。 例如，若要显示用户名，请输入 `Username: {{username}}`。 
  > - 不过，请注意变量替换，因为变量未在 UI 中验证，并且它们区分大小写。 请确保输入正确的信息。

- **Active Directory 站点代码**（仅用于“Kerberos”）：输入 Kerberos 扩展应使用的 Active Directory 站点的名称。 可能不需要更改此值，因为 Kerberos 扩展可能会自动查找 Active Directory 站点代码。
- **缓存名称**（仅用于“Kerberos”）：输入 Kerberos 缓存的通用安全服务 (GSS) 名称。 很可能不需要设置此值。
- **应用捆绑包 ID**（Microsoft Azure AD、Kerberos）：输入应通过设备上的扩展获得单一登录的其他应用的捆绑 ID。

  如果你使用的是 Microsoft Azure AD SSO 应用扩展类型，则这些应用将使用 Microsoft 企业 SSO 插件来对用户进行身份验证，而无需登录。 如果你输入的应用捆绑包 ID 不使用任何 Microsoft 库（例如 Microsoft 身份验证库（MSAL）），则它有权使用 Microsoft Azure AD SSO应用扩展。 与 Microsoft 库相比，这些应用可能不会带来相同的无缝体验。 如果是使用 MSAL 身份验证的旧版应用或不使用最新 Microsoft 库的应用，则必须添加到此列表，才能正常使用 Microsoft Azure SSO 应用扩展。  

  如果你使用的是 Kerberos SSO 应用扩展类型，则这些应用将有权访问 Kerberos 票证授予票证（身份验证票证），并在用户访问他们有权访问的服务时对其进行身份验证。

- **域领域映射**（仅用于“Kerberos”）：添加应映射到领域的域 DNS 后缀。 当主机的 DNS 名称与领域名称不匹配时，使用此设置。 很可能不需要创建此自定义域到领域的映射。
- **PKINIT 证书**（仅用于“Kerberos”）：选择可用于 Kerberos 身份验证的初始身份验证 (PKINIT) 证书的公钥加密。 可以从已在 Intune 中添加的 [PKCS](../protect/certficates-pfx-configure.md) 或 [SCEP](../protect/certificates-scep-configure.md) 证书中进行选择。 有关证书的详细信息，请参阅[在 Microsoft Intune 中使用证书进行身份验证](../protect/certificates-configure.md)。

## <a name="wallpaper"></a>壁纸

无映像的配置文件分配给具有现有映像的设备时，可能会遇到意外行为。 例如，创建无映像的配置文件。 此配置文件分配给已有映像的设备。 在此方案中，映像可能会变为设备默认值，或者初始映像可能保留在设备上。 此行为受 Apple 的 MDM 平台控制和限制。

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>设置适用范围：自动设备注册（监督）

- **壁纸显示位置**：选择要在设备上显示图像的位置。 选项包括：
  - **未配置**：Intune 不会更改或更新此设置。 自定义图像不会添加到设备。 默认情况下，OS 可能会设置自己的映像。
  - **锁定屏幕**：向锁定屏幕添加图像。
  - **主屏幕**：向主屏幕添加图像。
  - **锁定屏幕和主屏幕**：在锁定屏幕和主屏幕上使用相同的图像。
- **壁纸图像**：上传要使用的现有 .png、.jpg 或 .jpeg 图像。 请确保文件小于 750KB。 还可以删除已添加的图像。

> [!TIP]
> 若要在锁定屏幕和主屏幕上显示不同的图像，请创建包含锁定屏幕图像的配置文件， 以及另一个包含主屏幕图像的配置文件。 将两个配置文件分配到 iOS/iPadOS 用户组或设备组。

## <a name="next-steps"></a>后续步骤

[分配配置文件](device-profile-assign.md)并[监视其状态](device-profile-monitor.md)。

还可以为 [macOS](macos-device-features-settings.md) 设备创建设备功能配置文件。
