---
title: 适用于 Windows Phone 8.1 的 Microsoft Intune 设备限制设置
titleSuffix: ''
description: 了解可用于控制运行 Windows Phone 8.1 的设备中设备设置和功能的 Intune 设置。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 24fd2085839df35a486fcfa4cf817944b0d19944
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556245"
---
# <a name="microsoft-intune-windows-phone-81-device-restriction-settings"></a>Microsoft Intune Windows Phone 8.1 设备限制设置

本文介绍可为运行 Windows Phone 8.1 的设备配置的 Microsoft Intune 设备限制设置。

## <a name="before-you-begin"></a>在开始之前

[创建 Windows Phone 8.1 设备限制配置文件](device-restrictions-configure.md)。

## <a name="general"></a>常规

- **照相机**：设置为“阻止”可阻止访问设备照相机。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。

  Intune 只管理对设备照相机的访问。 它无法访问图片或视频。

- **复制和粘贴**：设置为“阻止”可阻止在设备上的应用之间使用复制粘贴。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。
- **可移动存储**：设置为“阻止”可阻止在设备（如 SD 卡）上使用外部存储设备。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。
- **地理位置**：设置为“阻止”可阻止打开设备上的位置服务。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。
- **Microsoft 帐户**：设置为“阻止”可阻止用户将 Microsoft 帐户与设备关联。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。
- **屏幕捕获**：设置为“阻止”可阻止获取设备上的屏幕截图。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。
- **诊断数据提交**：设置为“阻止”可阻止设备向 Microsoft 发送诊断和使用遥测数据。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。
- **自定义电子邮件帐户同步**：设置为“阻止”可阻止设备连接到非 Microsoft 电子邮件帐户。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。

## <a name="password"></a>Password

- **密码**：设置为“需要”时，强制用户输入密码才能访问设备。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。 仅适用于本地帐户。 域帐户密码仍由 Active Directory (AD) 和 Azure AD 配置。
  - **所需的密码类型**：选择密码类型。 选项包括：
    - **设备默认值**：密码可以包含数字和字母。
    - **字母数字**：密码必须是数字和字母的混合。
    - **数字**：密码必须仅为数字。
  - **最短密码长度**：输入所需的最小字符数，范围为 4-16 个。 例如，输入 `6` 可要求密码长度至少为六个字符。
  - **简单密码**：设置为“阻止”可阻止用户创建简单密码，如 `1234` 或 `1111`。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。
  - **擦除设备前的登录失败次数**：输入设备擦除前允许的错误密码数。
  - **屏幕锁定前的最大非活动分钟数**：输入设备在屏幕自动锁定前必须处于空闲状态的时间长度。 例如，输入 `5` 可在空闲 5 分钟后锁定设备。 设置为“未配置”或保留为空时，Intune 不会更改或更新此设置。
  - **密码过期(天)** ：输入在用户必须更改设备密码之前密码保持有效的天数（介于 1-255 天之间）。 例如，要使密码在 90 天后过期，请输入 `90`。 如果该值为空，Intune 不会更改或更新此设置。
  - **防止重用以前的密码**：输入以前用过的不能重用的密码数，从 1 到 24。 例如，输入 `5` 意味着用户不能将其新密码设置为当前密码或以前四个密码中的任何一个。 如果该值为空，Intune 不会更改或更新此设置。
- **加密**：设置为“需要”，需要对设备进行加密，包括文件。 并非所有设备都支持加密。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。 若要配置此设置并正确报告合规性，还需要配置：
  - **需要密码**：设置为“需要”。
  - **所需的密码类型**：设置为“至少包含数字”。
  - **最短密码长度**：设置为至少包含 `4`。

## <a name="app-store"></a>App Store

- **App Store**：设置为“阻止”可阻止用户访问 App Store。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。

## <a name="restricted-apps"></a>受限制的应用

在受限制的应用列表中，可以配置以下列表之一：

- **已阻止的应用**：列出用户不得安装和运行的应用（未由 Intune 托管）。
- **允许的应用**：列出允许用户安装的应用。 自动允许由 Intune 托管的应用。

若要配置列表，请单击“添加”，然后指定所选应用的名称、应用发布者（可选）和该应用在应用商店中的 URL。

### <a name="how-to-specify-the-url-to-an-app-in-the-store"></a>如何指定应用商店中应用的 URL

若要在允许和阻止的的应用列表中指定应用 URL，请使用以下格式：

在 [Windows Phone 应用商店](https://www.microsoft.com/store/apps/windows-phone)页面中，搜索想要使用的应用。

打开应用页面，并将该 URL 复制到剪贴板。 你现在可以在允许或阻止的应用列表中使用此 URL 作为 URL。

例如：在 Microsoft Store 中搜索 Skype 应用。 要使用的 URL 为 `http://www.windowsphone.com/store/app/skype/c3f8e570-68b3-4d6a-bdbb-c0a3f4360a51`。

### <a name="additional-options"></a>其他选项

还可以单击“导入”，填充 csv 文件中的列表（格式为 <应用 URL>,<应用名称>,<应用发布者>），或单击“导出”，创建包含受限制应用列表内容且格式相同的 csv 文件。

## <a name="browser"></a>浏览器

- **Web 浏览器**：设置为“阻止”可关闭设备上的内置 Web 浏览器。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。

## <a name="cellular-and-connectivity"></a>手机网络和连接性

- **Wi-Fi**：设置为“阻止”可禁用设备的 Wi-Fi 功能。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。
- **Wi-Fi Tethering**：设置为“阻止”可阻止使用设备上的 Wi-Fi Tethering。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。
- **自动连接到 Wi-Fi 热点**：允许设备自动连接到免费的 Wi-Fi 热点并自动接受任何使用条款。
- **Wi-Fi 热点报告**：设置为“阻止”可阻止设备发送 Wi-Fi 热点连接信息。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。
- **NFC**：设置为“阻止”可禁用在支持它的设备上使用近场通信 (NFC) 的操作。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。
- **蓝牙**：选择“阻止”可阻止用户启用蓝牙。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。

## <a name="next-steps"></a>后续步骤

有关设备限制配置文件的一般概述，请参阅[在 Microsoft Intune 中配置设备限制设置](device-restrictions-configure.md)。
