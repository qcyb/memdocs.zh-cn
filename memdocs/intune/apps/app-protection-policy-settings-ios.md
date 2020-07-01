---
title: iOS/iPadOS 应用保护策略设置
titleSuffix: Microsoft Intune
description: 本主题介绍适用于 iOS/iPadOS 设备的 iOS/iPadOS 应用保护策略 (APP) 设置。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/16/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 0f8b08f2-504c-4b38-bea2-b8a4ef0526b8
ms.reviewer: demerson
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6cfd2879c6e764da9a1b758e072f0b80ee434713
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2020
ms.locfileid: "85502657"
---
# <a name="ios-app-protection-policy-settings"></a>iOS 应用保护策略设置
[!INCLUDE [azure_portal](../includes/azure_portal.md)]

本文介绍适用于 iOS/iPadOS 设备的应用保护策略设置。 在设置新策略时，可在 Azure 门户的“设置”窗格中为应用保护策略[配置](app-protection-policies.md)所述的策略设置。

策略设置分为三类：“数据重定位”、“访问要求”和“条件启动”  。 在本文中，术语策略托管应用指使用应用保护策略配置的应用。

> [!IMPORTANT]
> Intune Managed Browser 已停用。 使用 [Microsoft Edge](../apps/manage-microsoft-edge.md) 获取受保护的 Intune 浏览器体验。 

## <a name="data-protection"></a>数据保护

### <a name="data-transfer"></a>数据传输
| 设置 | 如何使用 | 默认值 |
|------|----------|-------|
| **将组织数据备份到 iTunes 和 iCloud 备份** | 选择“阻止”，阻止此应用将工作或学校数据备份到 iTunes 和 iCloud。 选择“允许”，允许此应用将工作或学校数据备份到 iTunes 和 iCloud。 | **允许**  |
| 将组织数据发送到其他应用 | 指定哪些应用可从此应用接收数据： <ul><li>**所有应用**：允许传输到任何应用。 接收应用能够读取和编辑数据。</li><li>**无**：不允许将数据传输到任何应用，包括其他策略托管应用。 如果用户执行托管的打开位置功能并传输文档，则数据将被加密且不可读。</li><li> **策略托管应用**：仅允许传输到其他策略托管应用。 <p><p>**注意:** _用户可以在允许共享到非托管应用的未注册设备或已注册设备上，通过打开位置或共享扩展将内容传输到非托管应用。传输的数据由 Intune 加密，非托管应用无法读取。_</li><li>**具有 OS 共享功能的策略托管应用**：仅允许将数据传输到其他策略托管应用，以及将文件传输到已注册设备上的其他 MDM 托管应用。 <p><p>**注意:** “具有 OS 共享功能的策略托管应用”值仅适用于 MDM 注册设备 _。如果此设置针对未注册设备上的用户，则会应用“策略托管应用”值的行为。用户可以通过打开位置或共享扩展将未加密的内容传输到 iOS MDM allowOpenFromManagedtoUnmanaged 设置允许的任何应用程序。有关此 iOS/iPadOS MDM 设置的详细信息，请参阅 https://developer.apple.com/business/documentation/Configuration-Profile-Reference.pdf 。_<p><p></li><li>**具有“打开方式/共享”筛选功能的策略托管应用**：仅允许传输到其他策略托管应用，并筛选 OS“打开方式/共享”对话框，以仅显示策略托管应用。 若要配置“打开方式/共享”对话框的筛选，充当文件/文档源的应用和可打开此文件/文档的应用均需具有用于 iOS 8.1.1 版本或更高版本的 Intune SDK。 <p><p>**注意:** _如果应用支持 Intune 专用数据类型，则用户可以通过打开方式或共享扩展将内容传输到非托管应用。传输的数据由 Intune 加密，非托管应用无法读取。_</li></ul><br>此外，当设置为“策略托管应用”或“无”时，Spotlight 搜索（启用在应用内搜索数据）和 Siri 快捷方式 iOS 功能会受到阻止。 <p><p>此策略也适用于 iOS/iPadOS 通用链接。 通用 Web 链接由“在 Intune Managed Browser 中打开应用链接”策略设置托管。 <p> 默认情况下，Intune 允许向一些豁免应用和服务传输数据。 此外，如果需要允许将数据传输到不支持 Intune APP 的应用，则可以创建自己的豁免项目。 有关详细信息，请参阅[数据传输豁免](#data-transfer-exemptions)。 | **所有应用** |
| <ul><ui>**选择要豁免的应用** | 为上一选项选择“策略托管应用”时，此选项才可用。   |   |
| <ul><ui>**保存组织数据的副本** | 选择“阻止”，在此应用中禁用使用“另存为”选项。 如果想要允许使用“另存为”，请选择“允许”。 <br><br>**注意:** *Microsoft Excel、OneNote、Outlook、PowerPoint 和 Word 支持此设置。它还可以受第三方和 LOB 应用支持*。 <br><br> 如果设置为“阻止”，可以配置以下设置“允许用户将副本保存到所选的服务” 。   | <br><br> **允许**   |
| <ul><ui><ul><ui>**允许用户将副本保存到所选的服务** | 用户可以保存到所选的服务（OneDrive for Business、SharePoint 和本地存储）中。 将阻止所有其他服务。| **未选择任何项**  |
|<ul><ui>**将电信数据传输到** | 通常，当用户在应用中选择超链接的电话号码时，会打开一个拨号应用，预填充了该电话号码并随时可供拨打。 对于此设置，选择当从策略托管的应用启动电话号码时要如何处理此类型的内容传输：<ul><li>**无，不在应用之间传输此数据**：如果检测到电话号码，不传输通信数据。</li><li>**特定拨号应用**：当检测到电话号码时，允许特定的拨号应用启动联系人。</li><li>**任何拨号应用**：当检测到电话号码时，允许使用任何拨号应用启动联系人。</li></ul>| **任何拨号应用** |  
|<ul><ui><ul><ui>**拨号器应用 URL 方案** | 选择任何拨号应用后，必须提供用于在 iOS 设备上启动拨号应用的拨号应用 URL 方案。 有关详细信息，请参阅有关[电话链接](https://developer.apple.com/library/archive/featuredarticles/iPhoneURLScheme_Reference/PhoneLinks/PhoneLinks.html#//apple_ref/doc/uid/TP40007899-CH6-SW1)的 Apple 文档。 | **空** |
| **从其他应用接收数据** | 指定哪些应用可将数据传输到此应用： <ul><li>**所有应用**：允许从任何应用传输的数据。</li><li>**无**：不允许从任何应用传输数据，包括其他策略托管应用。</li><li>**策略托管应用**：仅允许从其他策略托管应用进行传输。</li><li>**所有包含传入组织数据的应用**：允许从任何应用传输的数据。 将所有不带用户标识的传入数据视为组织中的数据。 该数据将使用由 `IntuneMAMUPN` 设置定义的 MDM 注册用户标识进行标记。<p><p>**注意:** “所有包含传入组织数据的应用”值仅适用于 MDM 注册设备 _。如果此设置针对未注册设备上的用户，则会应用“任何应用”值的行为_。</li></ul> Intune 可能会允许从一些豁免应用和服务传输数据。 有关应用和服务的完整列表，请参阅[数据传输豁免](#data-transfer-exemptions)。 非注册 iOS/iPadOS 设备上已启用多标识 MAM 的应用程序会忽略此策略，并允许所有传入数据。<br><br> | **所有应用**    |
| **限制在其他应用间进行剪切、复制和粘贴** | 指定剪切、复制和粘贴操作何时可用于此应用。 选择： <ul><li>**阻止**：不允许在此应用和任何其他应用间进行剪切、复制和粘贴操作。</li><li>**策略托管应用**：允许在此应用和其他策略托管应用间进行剪切、复制和粘贴操作。</li><li>**带粘贴的策略托管应用**：允许在此应用和其他策略托管应用间进行剪切或复制。 允许将任何应用中的数据粘贴到此应用。</li><li>**任何应用**：不限制从此应用和对此应用进行剪切、复制和粘贴。</ul> | **任何应用**   |
| <ul><ui>**剪切和复制任何应用的字符限制** | 指定可从组织数据和帐户中剪切或复制的字符数。  这允许将指定数量的字符共享到任何应用程序，而不受“限制使用其他应用剪切、复制和粘贴”设置的限制。<p>默认值 = 0<p>**注意**：*要求应用具有 Intune SDK 版本 9.0.14 或更高版本*。  | **0**   |
| **第三方键盘** | 选择“阻止”来阻止在托管应用程序中使用第三方键盘。<p>启用此设置后，用户将收到一次性消息，说明禁止使用第三方键盘。 用户首次需要使用键盘与组织数据进行交互时，将会出现此消息。 使用托管应用程序时，只能使用标准的 iOS/iPadOS 键盘，所有其他键盘选项都将禁用。 此设置将影响多身份应用程序的组织和个人帐户。 此设置不影响在非托管应用程序中使用第三方键盘。<p>**注意:** 此功能要求应用使用 Intune SDK 版本12.0.16 或更高版本。 如果应用的 SDK 版本范围从 8.0.14 到（包括）12.0.15，则不会为多身份应用正确应用此功能。 有关更多详细信息，请参阅[已知问题：个人帐户的 iOS/iPadOS 中不阻止第三方键盘](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Updated-Known-issue-Third-party-keyboards-are-not-blocked-in-iOS/ba-p/339486)。 | **允许**  |

### <a name="encryption"></a>加密
| 设置 | 如何使用 | 默认值 |
|------|----------|-------|
| **对组织数据进行加密** | 选择“需要”，在此应用中启用工作或学校数据加密。  Intune 强制实施 iOS/iPadOS 设备加密，以在设备锁定时保护应用数据。  应用程序可使用 Intune APP SDK 加密选择性地加密应用数据。  Intune APP SDK 使用 iOS/iPadOS 加密方法将 256 位 AES 加密应用到应用数据。 <br><br> 启用此设置时，用户可能需要设置并使用 PIN 才能访问其设备。 如果没有设备 PIN 并且需要加密，则将通过“组织要求先启用设备 PIN 才能访问此应用”消息提示用户设置 PIN。 <br><br> 转到[官方 Apple 文档](https://support.apple.com/en-us/HT202739)，查看哪些 iOS/iPadOS 加密模块由 FIPS 140-2 认证。 | **需要**  |


### <a name="functionality"></a>功能
| 设置 | 如何使用 | 默认值 |
|------|----------|-------|
| **使用本机联系人应用同步应用** |  选择“阻止”，阻止应用将数据保存到设备上的本机“联系人”应用。 如果选择“允许”，应用可以将数据保存到设备上的本机“联系人”应用。 <br><br>执行选择性擦除以从应用删除工作或学校数据时，将删除从应用直接同步到本机“联系人”应用的联系人。 无法擦除从本机通讯簿同步到另一个外部源中的任何联系人。 目前仅适用于 Microsoft Outlook 应用。   | **允许**  |
| **打印组织数据** | 选择“阻止”，阻止应用打印工作或学校数据。 如果将此设置保留为“允许”（默认值），用户将能够导出和打印所有组织数据。  | **允许**  |
| **限制使用其他应用传输 Web 内容** | 指定如何从策略管理的应用中打开 Web 内容（http/https 链接）。 选择： <ul><li>**任何应用**：允许在任何应用中使用 Web 链接。</li><li>**Intune Managed Browser**：仅允许在 Intune Managed Browser 中打开 Web 内容。 此浏览器是策略托管的浏览器。</li><li>**Microsoft Edge**：仅允许在 Microsoft Edge 中打开 Web 内容。 此浏览器是策略托管的浏览器。</li><li>**非托管浏览器**：允许 Web 内容仅在“非托管浏览器协议”设置定义的非托管浏览器中打开。 Web 内容在目标浏览器中处于非托管状态。<br>**注意**：要求应用具有 Intune SDK 版本 11.0.9 或更高版本。</li></ul> 如果正使用 Intune 管理设备，请参阅[使用 Microsoft Intune 的 Managed Browser 策略管理 Internet 访问](manage-microsoft-edge.md)。<br><br>如果需要策略托管的浏览器，但未安装，系统将提示最终用户安装 Microsoft Edge。<p>如果需要使用策略托管的浏览器，请通过“允许应用向其他应用传送数据”策略设置管理 iOS/iPadOS 通用链接。 <p>**Intune 设备注册**<br>如果使用 Intune 管理设备，请参阅“使用 Microsoft Intune 的托管浏览器策略管理 Internet 访问”。 <p>**策略托管的 Microsoft Edge**<br>移动设备（iOS/iPadOS 和 Android）的 Microsoft Edge 浏览器支持 Intune 应用保护策略。 在 Microsoft Edge 浏览器应用程序中使用其企业 Azure AD 帐户登录的用户将受 Intune 保护。 Microsoft Edge 浏览器集成了 Intune SDK 并支持其除阻止以外的所有数据保护策略：<br><ul><li>**另存为**：Microsoft Edge 浏览器不允许用户向云存储提供商（如 OneDrive）添加直接的应用内连接。</li><li>**联系人同步**：Microsoft Edge 浏览器不会保存到本地联系人列表。</li></ul><br>**注意**：*Intune SDK 无法确定目标应用是否为浏览器。在 iOS/iPadOS 设备上，不允许使用其他托管浏览器应用。*    | 未配置  |
|<ul><ui>**非托管浏览器协议** | 输入单个非托管浏览器的协议。 策略托管应用程序的 Web 内容（http/https 链接）将在支持此协议的任何浏览器中打开。 Web 内容在目标浏览器中处于非托管状态。 <br><br>只有当你想要与特定浏览器共享受保护的内容，但又不允许使用 Intune 应用保护策略，才能使用此功能。 必须与浏览器供应商联系，确定所需的浏览器支持协议。<br><br>**注意**：*只包含协议前缀。如果浏览器需要 `mybrowser://www.microsoft.com` 格式的链接，请输入 `mybrowser`。*<br>链接将转换为：<br><ul><li>`http://www.microsoft.com` > `mybrowser://www.microsoft.com`</li><li>`https://www.microsoft.com` > `mybrowsers://www.microsoft.com`</li></ul> | **空**  |
| **组织数据通知** | 指定如何针对组织帐户通过 OS 通知共享组织数据。 此策略设置将影响本地设备和任何连接的设备，如可穿戴设备和智能扬声器。 应用可能会提供其他控件来自定义通知行为，或者可以选择不接受所有值。 选择： <ul><li>**阻止**：不共享通知。</li><ul><li>如果应用程序不支持，则将允许通知。</li></ul><li>**阻止组织数据**：例如，不在通知中共享组织数据。</li><UL><li>“你有新邮件”；“你有个会议”。</li><li>如果应用程序不支持，通知将被阻止。</li></ul><li>**允许**：在通知中共享组织数据。</li></ul> <p>**注意**：*此设置需要应用支持。此时，Outlook for iOS 版本 4.34.0 或更高版本支持此设置。* | **允许**   |
> [!NOTE]  
> 无数据保护设置可以控制 iOS/iPadOS 设备上由 Apple 托管的打开方式功能。 要使用“管理 Apple 打开方式”，请参阅[使用 Microsoft Intune 管理 iOS/iPadOS 应用之间的数据传输](data-transfer-between-apps-manage-ios.md)。

## <a name="data-transfer-exemptions"></a>数据传输豁免

有一些豁免应用和平台服务，Intune 应用保护策略可能会允许在某些情况下向其或从其传输数据。 此列表可能会更改以反映有利于安全工作效率的服务和应用。

| 应用/服务名称 | 说明 |
| ---- | --- |
|<code>tel; telprompt</code> | 本机电话应用 |
| <code>skype</code> | Skype |
| <code>app-settings</code> | 设备设置 |
| <code>itms; itmss; itms-apps; itms-appss; itms-services</code> | App Store |
| <code>calshow</code> | 本机日历 |


## <a name="access-requirements"></a>访问要求

| 设置 | 如何使用 | 默认值 |
|------|----------|-------|
| **需要 PIN 才能进行访问** | 选择“需要”，要求使用 PIN 才能使用此应用。 用户首次在工作或学校环境中运行应用时，将提示其设置此 PIN。 无论在联机或脱机情况下工作，PIN 始终有效。    <br><br> 可以使用“需要 PIN 才能进行访问”部分下提供的设置配置 PIN 强度。   | **需要** |
| <ul><ui> PIN 类型 | 在访问应用了应用保护策略的应用之前，为数值或密码类型 PIN 设置要求。 数值要求只涉及数字，而密码则可采用至少 1 个字母或至少 1 个特殊字符进行定义。  <br><br> **注意:** *要配置密码类型，应用需具有 Intune SDK 版本 7.1.12 或更高版本。数值类型没有任何 Intune SDK 版本限制。允许的特殊字符包括 iOS/iPadOS 英语键盘上的特殊字符和符号*。  | **数字**  |
| <ul><ui> **简单 PIN** | 选择“允许”，允许用户使用 1234、1111、abcd 或 aaaa 等简单的 PIN 序列。 选择“阻止”，阻止用户使用简单的序列。 在 3 个字符滑动窗口中检查简单的序列。 如果配置了“阻止”，则不会接受 1235 或 1112 作为由最终用户设置的 PIN，但允许采用 1122。 <br><br>**注意**：如果配置了密码类型 PIN，并且“允许使用简单 PIN”已设置为“是”，用户在其 PIN 中则需要至少 1 个字母或至少 1 个特殊字符 *。如果配置了密码类型 PIN，并且“允许简单 PIN”已设置为“否”，用户在其 PIN 中则需要至少 1 个数字和 1 个字母以及至少 1 个特殊字符 *。   |**允许**  |
| <ul><ui> **选择最小 PIN 长度** | 指定 PIN 序列必须包含的最小位数。  | **4**  |
| <ul><ui> **使用 Touch ID，而不是 PIN 进行访问 (iOS 8 +)** | 选择“允许”，允许用户使用 [Touch ID](https://support.apple.com/HT201371) 而非 PIN 进行应用访问。    | **允许**  |
|<ul><ui><ul><ui>**超时后使用 PIN 覆盖 Touch ID**|  要使用此设置，请选择“需要”，然后配置非活动超时。  |**需要**  |
| <ul><ui><ul><ui><ul><ui> **超时(非活动状态的分钟数)** |  指定在密码或数值 PIN（如配置所示）将覆盖指纹或人脸访问方法前要等待的时间（以分钟为单位）。 此超时值应大于“在(非活动状态的分钟数)后重新检查访问要求”下的指定值。  |**30**  |
| <ul><ui><ul><ui>**使用 Face ID，而不是 PIN 进行访问 (iOS 11+)** | 选择“允许”，允许用户使用面部识别技术对 iOS/iPadOS 设备上的用户进行身份验证。 如果允许，必须使用 Face ID 来访问 Face ID 功能设备上的应用。    | **允许**  |
| <ul><ui>**PIN 重置间隔的天数** | 选择“是”，要求用户在一段时间（以天为单位）后更改其应用 PIN。  <br><br>如果设置为“是”，然后配置 PIN 重置所需的间隔天数。 |**否**  |  
| <ul><ui><ul><ui> **天数** | 配置 PIN 重置所需的间隔天数。  |**90**  |
| <ul><ui>**设置设备 PIN 时的应用 PIN** | 选择“禁用”，如果在已配置公司门户的已注册设备上检测到设备锁，则禁用应用 PIN。<br><br> **注意:** 要求应用具有 Intune SDK 版本 7.0.1 或更高版本。  <br><br>在 iOS/iPadOS 设备上，可让用户使用 [Touch ID](https://support.apple.com/HT201371) 或 [Face ID](https://support.apple.com/HT208109) 而非 PIN 来证明其身份。 Intune 使用 [LocalAuthentication](https://developer.apple.com/documentation/localauthentication/) API 对使用 Touch ID 和 Face ID 的用户进行身份验证。 若要了解有关 Touch ID 和 Face ID 的详细信息，请参阅 [iOS 安全指南](https://www.apple.com/business/docs/iOS_Security_Guide.pdf)。  <br><br> 用户尝试通过其工作或学校帐户使用此应用时，系统会提示他们提供其指纹标识或面部标识，而不是输入 PIN。 启用此设置时，如果使用工作或学校帐户，应用切换器的预览图像将模糊显示。  |  **启用** |  
| **用于访问的工作或学校帐户凭据** | 选择“需要”，要求用户使用其工作或学校帐户而非输入 PIN 进行登录以访问应用。 如果将此设置为“需要”，并且 PIN 或生物识别提示已打开，则会显示公司凭据以及 PIN 或生物识别提示。  | **不需要** |
| **在(非活动状态的分钟数)后重新检查访问要求** | 配置应用要求用户再次指定访问要求之前必须经过的非活动状态的分钟数。 <br><br> 例如，如果管理员在策略中启用 PIN 并阻止取得 root 权限的设备，用户打开 Intune 托管应用时，则必须输入 PIN，并且必须在未取得 root 权限的设备上使用此应用。 使用此设置时，用户在与配置值相等的一段时间内无需在任何 Intune 托管应用上再次输入 PIN 或再次经历 root 检测检查。  <br><br>**注意:** 在 iOS/iPadOS 上，同一发布者的所有 Intune 托管应用均共享此 PIN *。应用离开设备主屏幕后，就会重置特定 PIN 的 PIN 计时器。在此设置中定义的超时期限内，用户无需在共享 PIN 的任何 Intune 托管应用上输入此 PIN。此策略设置格式支持正整数。*     | **30** |

> [!NOTE]
> 要详细了解在“访问权限”部分配置给同一组应用和用户的多个 Intune 应用保护设置如何在 iOS/iPadOS 上运行，请参阅 [Intune MAM 常见问题](mam-faq.md#app-experience-on-ios)和[在 Intune 中使用应用保护策略访问操作选择性地擦除数据](app-protection-policies-access-actions.md)。

## <a name="conditional-launch"></a>条件启动
配置条件启动设置以设置访问保护策略的登录安全要求。 

默认情况下，向多个设置提供已预配置的值和操作。 可以删除某些设置，例如“最低 OS 版本”。 此外，还可以从“选择一个”下拉列表中选择其他设置。 

| 设置 | 如何使用 |  
|---------|------------| 
| **最低 OS 版本** | 指定要使用此应用所需的最低 iOS/iPadOS 操作系统版本。 *操作*包括： <br><ul><li>**警告** - 如果设备上的 iOS/iPadOS 版本不符合此要求，用户将看到一个通知。 可忽略此通知。 </li></ul> <ul><li>**阻止访问** - 如果设备上的 iOS/iPadOS 版本不符合此要求，将阻止用户访问。</li></ul> <ul><li>**擦除数据** - 从设备中擦除与应用程序关联的用户帐户。  </li></ul> </li></ul>此项可以出现多次，每个实例支持不同的操作。<br><br> 此策略设置格式支持 major.minor、major.minor.build 或 major.minor.build.revision。 <br><br>**注意:** 要求应用具有 Intune SDK 版本 7.0.1 或更高版本。 |
| **最大 PIN 尝试次数** | 指定用户在执行配置操作之前必须成功输入其 PIN 的尝试次数。 此策略设置格式支持正整数。 *操作*包括： <br><ul><li>**重置 PIN** - 用户必须重置其 PIN。</li></ul> <ul><li>**擦除数据** - 从设备中擦除与应用程序关联的用户帐户。  </li></ul></li></ul> 默认值 = 5 |
| **脱机宽限期** | MAM 应用可以脱机运行的分钟数。 指定重新检查应用访问要求之前的时间（以分钟为单位）。 *操作*包括： <br><ul><li>**阻止访问（分钟数）** - MAM 应用可以脱机运行的分钟数。 指定重新检查应用访问要求之前的时间（以分钟为单位）。 配置期限过期后，应用将阻止对工作或学校数据的访问，直到网络访问可用为止。 此策略设置格式支持正整数。<br><br>默认值 = 720 分钟（12 小时） </li></ul> <ul><li>**擦除数据（天数）** - 经过数天（由管理员定义）的脱机运行后，应用会要求用户连接到网络并重新进行身份验证。 如果用户身份验证成功，则可继续访问其数据，且将重置脱机时间间隔。  如果用户未能通过身份验证，则应用会对用户帐户和数据执行选择性擦除。  请参阅[如何仅擦除 Intune 托管应用中的企业数据](apps-selective-wipe.md)，详细了解选择性擦除所删除的数据。 此策略设置格式支持正整数。 <br><br> 默认值 = 90 天 </li></ul>  此项可以出现多次，每个实例支持不同的操作。 |
| **已越狱/获得 root 权限的设备** | 此设置没有可设置的值。 *操作*包括： <br><ul><li>**阻止访问** - 阻止在已越狱或已取得 root 权限的设备上运行此应用。 用户仍能够将此应用用于个人任务，但必须使用其他设备才能访问此应用中的工作或学校数据。</li></ul> <ul><li>**擦除数据** - 从设备中擦除与应用程序关联的用户帐户。 </li></ul> |
| **最低应用版本** | 指定最低操作系统值的值。 *操作*包括： <br><ul><li>**警告** - 如果设备上的应用版本不符合此要求，用户将会看到一个通知。 可忽略此通知。</li></ul> <ul><li>**阻止访问** - 如果设备上的应用版本不符合此要求，用户将会看到一个通知。 </li></ul> <ul><li>**擦除数据** - 从设备中擦除与应用程序关联的用户帐户。 </li></ul> </li></ul>   由于应用之间通常拥有不同的版本控制方案，因此，请创建针对一个应用的一个最低应用版本策略（例如 Outlook 版本策略）。<br><br> 此项可以出现多次，每个实例支持不同的操作。<br><br> 此策略设置格式支持 major.minor、major.minor.build 或 major.minor.build.revision。<br><br> **注意:** 要求应用具有 Intune SDK 版本 7.0.1 或更高版本。<br><br> 此外，还可以配置最终用户可获取更新业务线 (LOB) 应用版本的位置。 最终用户将在“最低应用版本”条件启动对话框中看到此项，系统将提示最终用户更新到 LOB 应用的最低版本。 在 iOS/iPadOS 上，此功能要求应用与 Intune SDK for iOS v. 10.0.7 或更高版本集成（或使用包装工具包装）。 若要配置最终用户应更新 LOB 应用的位置，应用需要使用键 `com.microsoft.intune.myappstore` 发送给它的托管[应用配置策略](app-configuration-policies-managed-app.md)。 发送的值将定义最终用户从哪个应用商店中下载应用。 如果应用是通过公司门户部署的，则值必须为 `CompanyPortal`。 对于任何其他应用商店，必须输入完整的 URL。 |
| **最低 SDK 版本** | 指定 Intune SDK 版本的分钟值。 *操作*包括： <br><ul><li>阻止访问 - 如果应用的 Intune 应用保护策略 SDK 版本不符合此要求，将阻止用户访问。 </li></ul><ul><li>**擦除数据** - 从设备中擦除与应用程序关联的用户帐户。 </li></ul></li></ul>若要详细了解 Intune 应用保护策略 SDK，请参阅 [Intune App SDK 概述](../developer/app-sdk.md) 由于各应用通常具有不同的 Intune SDK 版本，因此，请创建针对一个应用的一个最低 Intune SDK 版本的策略（例如适用于 Outlook 的 Intune SDK 版本策略）。 <br><br> 此项可以出现多次，每个实例支持不同的操作。|
| **设备型号** | 指定模型标识符的分号分隔列表。 这些值不区分大小写。 *操作*包括： <br><ul><li>**允许指定项（阻止非指定项）** - 仅与指定设备型号匹配的设备才能使用该应用。 所有其他设备型号将被阻止。 </li></ul> <ul><li>**允许指定项（擦除非指定项）** - 从设备中擦除与应用程序关联的用户帐户。</li></ul> 若要详细了解如何使用此设置，请参阅[条件启动操作](app-protection-policies-access-actions.md#ios-policy-settings)。 |
| **允许的最大设备威胁级别** | 应用保护策略可以利用 Intune-MTD 连接器。 指定使用此应用可接受的最高威胁级别。 威胁由最终用户设备上选择的移动威胁防御 (MTD) 供应商应用确定。 指定安全、低、中或高   。 “安全”要求设备上没有任何威胁，是可配置的限制性最强的值，而“高”实质上要求存在 Intune 到 MTD 的活动连接 。 *操作*包括： <br><ul><li>**阻止访问** - 如果你选择的移动威胁防御 (MTD) 供应商应用确定最终用户设备上的威胁级别不满足此要求，则将阻止用户访问。</li></ul><ul><li>**擦除数据** - 从设备中擦除与应用程序关联的用户帐户。</li></ul>**注意:** 要求应用具有 Intune SDK 版本 12.0.15 或更高版本。 <br><br> 有关使用此设置的详细信息，请参阅[为未注册的设备启用 MTD](../protect/mtd-enable-unenrolled-devices.md)。 |

### <a name="learn-more"></a>了解详细信息
- 了解 [Microsoft 应用中的 LinkedIn 信息和功能](https://go.microsoft.com/fwlink/?linkid=850740)。
- 在 [Office 365 产品指南页](https://products.office.com/business/office-365-roadmap?filters=%26freeformsearch=linkedin#abc)了解 LinkedIn 帐户连接版本。 
- 了解[配置 LinkedIn 帐户连接](https://docs.microsoft.com/azure/active-directory/linkedin-integration)。
- 有关用户的 LinkedIn 和 Microsoft 工作或学校帐户之间共享的数据的详细信息，请参阅[工作或学校的 Microsoft 应用程序中的 LinkedIn](https://www.linkedin.com/help/linkedin/answer/84077)。
