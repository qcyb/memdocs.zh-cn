---
title: Microsoft Intune 中适用于 Android 的设备限制设置 - Azure | Microsoft Docs
description: 在 Microsoft Intune 中查看可以控制和限制的所有 Android 设备管理员设置的列表。 使用这些设置来控制密码、访问 Google Play、允许或禁止应用、控制浏览器设置、阻止应用、备份到 Google Cloud，以及控制邮件、声音、数据漫游、Wi-Fi 和蓝牙连接选项。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/30/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: chmaguir, chrisbal
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4afc27680c464f67756340ebcb0958887ae6f795
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "80407870"
---
# <a name="android-and-samsung-knox-standard-device-restriction-settings-lists-in-intune"></a>Intune 中 Android 和 Samsung Knox Standard 设备限制设置列表

本文介绍可为运行 Android 的设备配置的所有 Microsoft Intune 设备限制设置。

>[!TIP]
>如果所需设置不可用，可能能够使用[自定义配置文件](custom-settings-android.md)来配置设备。

## <a name="before-you-begin"></a>在开始之前

[创建设备配置文件](device-restrictions-configure.md)。

## <a name="general"></a>常规

- **照相机**：设置为“阻止”可阻止访问设备照相机  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许访问设备的照相机。

  Intune 只管理对设备照相机的访问。 它无法访问图片或视频。

- **复制和粘贴（仅限 Samsung Knox）** ：设置为“阻止”可阻止复制和粘贴  。 设置为“未配置”可允许使用设备上的复制和粘贴功能  。
- **应用间的剪贴板共享（仅限 Samsung Knox）** ：选择“阻止”可阻止使用剪贴板在应用之间进行复制和粘贴  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许在设备上使用复制和粘贴功能。
- **诊断数据提交（仅限 Samsung Knox）** ：设置为“阻止”可阻止用户从设备提交 bug 报告  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许用户提交数据。
- **擦除（仅限 Samsung Knox）** ：允许用户在设备上运行[擦除](../remote-actions/devices-wipe.md)操作。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。
- **地理位置（仅限 Samsung Knox）** ：设置为“阻止”可禁止设备使用位置信息  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许设备使用位置信息。
- **关闭电源（仅限 Samsung Knox）** ：设置为“阻止”可阻止用户关闭设备电源  。 还可阻止配置和使用“擦除设备前的登录失败次数”设置  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许用户关闭设备电源。
- **屏幕捕获（仅限 Samsung Knox）** ：设置为“阻止”可阻止屏幕截图  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许用户以图像形式捕获屏幕内容。
- **语音助手（仅限 Samsung Knox）** ：设置为“阻止”可禁用 S Voice 服务  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许在设备上使用 S Voice 服务和应用。 此设置不适用于 Bixby 或用于朗读屏幕内容的辅助功能的语音助手。
- **YouTube（仅限 Samsung Knox）** ：设置为“阻止”可阻止用户使用 YouTube 应用  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许在设备上使用 YouTube 应用。
- **共享设备（仅限 Samsung Knox）** ：将托管的 Samsung KNOX 标准设备配置为共享。 设置为“允许”可允许用户使用其 Azure AD 凭据登录或注销设备  。 设备仍然受到管理，无论是否正在使用中。

  与 SCEP 证书配置文件一起使用时，此功能允许用户与所有用户共享具有相同应用的设备。 但每个用户都有其自己的 SCEP 用户证书。 用户注销时，会清除所有应用数据。 此功能仅限于 LOB 应用。

  设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能阻止多个用户在设备上使用其 Azure AD 凭据登录公司门户应用。
- **更改日期和时间 (Samsung Knox)** ：设置为“阻止”可阻止用户更改设备上的日期和时间设置  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许用户更改日期和时间设置。

## <a name="password"></a>Password

- **密码**：设置为“需要”时，用户必须输入密码才能访问设备  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许用户无需输入密码即可访问设备。

    > [!NOTE]
    > 在 MDM 注册期间，Samsung Knox 设备自动要求使用 4 位数的 PIN。 本机 Android 设备可能会自动要求，必须有 PIN 才符合条件访问。

- **最短密码长度**：输入所需的最小字符数，范围为 4-16 个。 例如，输入 `6` 可要求密码长度至少为六个数字或字符。
- **屏幕锁定前的最大非活动分钟数**：输入设备在屏幕自动锁定前必须处于空闲状态的时间长度。 例如，输入 `5` 可在空闲 5 分钟后锁定设备。 值为空或设置为“未配置”时，Intune 不会更改或更新此设置  。

  在设备上，用户设置的时间值不能大于在配置文件中配置的时间。 用户可以设置更低的时间值。 例如，如果配置文件设置为 `15` 分钟，则用户可将值设置为 5 分钟。 用户不得将值设置为 30 分钟。

- **擦除设备前的登录失败次数**：输入设备擦除前允许的错误密码数，从 4-11。 如果为 `0`（零），可能会禁用设备擦除功能。 如果该值为空，Intune 不会更改或更新此设置。
- **密码过期(天)** ：输入在用户必须更改设备密码前，设备密码保持有效的天数（介于 1-365 天之间）。 例如，要使密码在 90 天后过期，请输入 `90`。 密码到期后，系统会提示用户创建新密码。 如果该值为空，Intune 不会更改或更新此设置。
- **所需的密码类型**：输入所需的密码复杂性级别以及是否可以使用生物识别设备。 选项包括：
  - **设备默认值**
  - **低安全性生物识别**：[强与弱生物识别](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html)（打开 Android 的网站）
  - **至少包含数字**：包含数字字符，如 `123456789`。
  - **数字复杂度**：不允许使用重复或连续数字（例如，“1111”或“1234”）。 向设备分配此设置之前，请确保将这些设备上的公司门户更新至最新版本。

    如果设置为“数值复杂度”，并将设置分配给运行 Android 版本早于 5.0 的设备，则以下行为适用  ：

    - 如果公司门户应用运行的版本低于 1704，则不会向设备应用任何 PIN 策略，并且 Microsoft Endpoint Manager 管理中心中会显示错误。
    - 如果公司门户应用运行 1704 版本或更高版本，则只能应用简单的 PIN。 5\.0 以前的 Android 版本不支持此设置。 Microsoft 终结点管理器管理中心未显示任何错误。

  - **至少为字母**：包含字母表中的字母。 不使用数字和符号。
  - **至少包含字母数字**：包括大写字母、小写字母和数字字符。
  - **至少为包含符号的字母数字**：包括大写字母、小写字母、数字字符、标点和符号。

- **防止重用以前的密码**：使用此设置可限制用户创建以前用过的密码。 输入以前用过的不能重用的密码数，从 1 到 24。 例如，输入 `5` 意味着用户不能将其新密码设置为当前密码或以前四个密码中的任何一个。 如果该值为空，Intune 不会更改或更新此设置。
- **指纹解锁（仅限 Samsung Knox）** ：设置为“阻止”可阻止使用指纹解锁设备  。 设置为“未配置”（默认值）时，Intune 不会更改或更新此设置。默认情况下，OS 可能允许用户使用指纹解锁设备  。
- **Smart Lock 和其他信任代理**：设置为“阻止”可阻止 Smart Lock 或其他信任代理调整锁屏界面设置  。 此功能（也称为“信任代理”）可以在设备处于可信任位置时禁用或绕过设备锁屏界面密码。 例如，设备连接到特定的蓝牙设备时或靠近 NFC 标签时使用此功能。 可以使用此设置防止用户配置 Smart Lock。

  设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。

  此设置适用于：

  - Samsung KNOX Standard 5.0+

- **加密**：选择“必需”，以便对设备上的文件进行加密  。 并非所有设备都支持加密。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 若要配置此设置并正确报告合规性，还需要配置：
  1. **密码**：设置为“需要”  。
  2. **所需的密码类型**：设置为“至少包含数字”  。
  3. **最短密码长度**：设置为至少包含 `4`。

  > [!NOTE]
  > 如果强制执行了加密策略，则 Samsung Knox 设备要求用户设置六个字符的复杂密码作为设备密码。

## <a name="google-play-store"></a>Google Play Store

- **Google Play 商店（仅限 Samsung Knox）** ：设置为“阻止”可阻止用户使用 Google Play 商店  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许用户访问设备上的 Google Play 商店。

## <a name="restricted-apps"></a>受限制的应用

使用这些设置可在设备上允许或阻止特定应用。 Android 和 Samsung Knox Standard 设备上支持此功能。

- **未配置**（默认）：Intune 不会更改或更新此设置。
- **禁止的应用**：列出不允许用户安装和运行的应用（未由 Intune 托管）。 如果用户安装此列表中的某个应用，Intune 会通知你。
- **允许的应用：** 列出允许用户安装的应用。 为了保持兼容性，用户不得安装其他应用。  系统会自动允许由 Intune 管理的应用，包括公司门户应用。
- **应用列表**：**添加**应用：
  - **应用捆绑 ID**：输入应用程序包 ID。
  - **App Store URL**：输入所需应用的 Google Play 商店 URL。 例如，要添加适用于 Android 的 Microsoft 远程桌面应用，请输入 `https://play.google.com/store/apps/details?id=com.microsoft.rdc.android`。

    若要查找应用的 URL，请打开 [Google Play 商店](https://play.google.com/store/apps)，并搜索该应用。 例如，搜索 `Microsoft Remote Desktop Play Store` 或 `Microsoft Planner`。 选择应用并复制 URL。
  
  - **应用名称**：输入所需的名称。 此名称向用户显示。
  - **发布者**（可选）：输入应用的发布者，如 `Microsoft`。

还可以导入包含应用详细信息的 CSV 文件，包括 URL  。 使用 <应用 url  >, <应用名称  >, <应用发行者  > 格式。 或，导出  包含相同格式的受限应用列表的现有列表。

> [!IMPORTANT]
> 使用受限应用设置的设备配置文件必须分配给用户组，而不是设备组。

## <a name="browser"></a>浏览器

- **Web 浏览器（仅限 Samsung Knox）** ：设置为“阻止”可阻止在设备上使用默认 Web 浏览器  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许使用设备的默认 Web 浏览器。
- **自动填充（仅限 Samsung Knox）** ：设置为“阻止”可阻止浏览器自动填充文本  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许自动填充。
- **Cookie（仅限 Samsung Knox）** ：选择如何在设备上处理网站的 cookie。 选项包括：
  - Allow
  - 阻止所有 cookie
  - 允许访问的网站的 cookie
  - 允许当前网站的 cookie
- **JavaScript（仅限 Samsung Knox）** ：设置为“阻止”可阻止在设备上运行浏览器中的 Java 脚本  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许使用这些脚本。
- **弹出窗口（仅限 Samsung Knox）** ：设置为“阻止”将打开弹出窗口阻止程序，以阻止 Web 浏览器中的弹出窗口  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许弹出窗口。

## <a name="allow-or-block-apps"></a>允许或禁止应用

使用这些设置允许、阻止或隐藏在 Samsung Knox Standard 设备上运行特定应用。 用户无法打开或运行隐藏的应用。

选项包括：

- **允许安装的应用(仅限 Samsung Knox Standard)** ：添加用户可以安装的应用。 用户无法安装列表中没有的应用。
- **禁止启动的应用(仅限 Samsung Knox Standard)** ：输入用户不能在其设备上运行的应用。
- **对用户隐藏的应用(仅限 Samsung Knox Standard)** ：输入在设备上隐藏的应用。 用户无法发现或运行这些应用。

对于每个设置，添加你的应用：

- **按包名称添加应用**：输入应用和应用包的名称。 主要用于业务线应用。 
- **按 URL 添加应用**：输入应用名称及其在 Google Play 商店中的 URL。
- **添加应用商店应用**：在 Intune 中管理的现有应用列表中选择一个应用。

## <a name="cloud-and-storage"></a>云和存储

- **Google 备份（仅限 Samsung Knox）** ：设置为“阻止”可阻止设备同步到 Google 备份  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许使用 Google 备份。
- **Google 帐户自动同步（仅限 Samsung Knox）** ：设置为“阻止”可在设备上阻止 Google 帐户自动功能  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许 Google 帐户设置自动同步。
- **可移动存储（仅限 Samsung Knox）** ：设置为“阻止”可阻止设备使用可移动存储  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许设备使用可移动存储，如 SD 卡。
- **对存储卡进行加密（仅限 Samsung Knox）** ：选择“必需”，强制要求必须对存储卡进行加密  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能会允许使用未加密的存储卡。 并非所有设备都支持存储卡加密。 若要进行确认，请咨询设备制造商。

## <a name="cellular-and-connectivity"></a>手机网络和连接性

- **数据漫游（仅限 Samsung Knox）** ：设置为“阻止”可阻止通过手机网络进行数据漫游  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许使用数据漫游。
- **SMS/MMS 消息传递（仅限 Samsung Knox）** ：设置为“阻止”可阻止设备上的文本消息  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许使用 SMS 和 MMS 消息传递。
- **语音拨号（仅限 Samsung Knox）** ：设置为“阻止”可阻止用户在设备上使用语音拨号功能  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许使用语音拨号功能。
- **语音漫游（仅限 Samsung Knox）** ：设置为“阻止”可阻止通过手机网络进行语音漫游  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许使用语音漫游。
- **蓝牙（仅限 Samsung Knox）** ：设置为“阻止”可阻止在设备上使用蓝牙  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许使用蓝牙。
- **NFC（仅限 Samsung Knox）** ：设置为“阻止”可禁用在支持它的设备上使用近场通信 (NFC) 的操作  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许 NFC 操作。
- **Wi-Fi（仅限 Samsung Knox）** ：设置为“阻止”可阻止在设备上使用 Wi-Fi  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许使用 Wi-Fi。
- **Wi-Fi Tethering（仅限 Samsung Knox）** ：设置为“阻止”可阻止使用设备上的 Wi-Fi Tethering  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许使用 Wi-Fi Tethering。

## <a name="kiosk"></a>Kiosk

展台设置仅适用于 Samsung Knox Standard 设备和使用 Intune 管理的应用。

- 添加要在设备处于展台模式时运行的应用。 在展台模式下，仅运行所添加的应用，未添加的应用不会运行。 当设备处于展台模式时，预安装的浏览器不会作为应用运行。 如果需要浏览器，请考虑使用 [Managed Browser](../apps/app-configuration-managed-browser.md)。

  应用选项：

  - **按包名称添加应用**：主要用于业务线应用。 输入应用和应用包的名称。
  - **按 URL 添加应用**：输入应用名称及其在 Google Play 商店中的 URL。
  - **添加应用商店应用**：在 Intune 中管理的现有应用列表中选择一个应用。

- **屏幕睡眠按钮**：选择“阻止”可阻止或隐藏屏幕睡眠按钮  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许在设备上使用屏幕睡眠唤醒按钮。
- **音量按钮**：设置为“阻止”可阻止用户通过禁用音量按钮来调节音量  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许在设备上使用音量按钮。

## <a name="next-steps"></a>后续步骤

[分配配置文件](device-profile-assign.md)并[监视其状态](device-profile-monitor.md)。

还可以为 [Android 企业](device-restrictions-android-for-work.md#dedicated-devices)和 [Windows 10](kiosk-settings.md) 设备创建展台配置文件。
