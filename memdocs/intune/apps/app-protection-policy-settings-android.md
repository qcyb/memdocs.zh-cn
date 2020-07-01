---
title: Android 应用保护策略设置
titleSuffix: Microsoft Intune
description: 本主题介绍适用于 Android 设备的应用保护策略设置。
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
ms.assetid: 9e9ef9f5-1215-4df1-b690-6b21a5a631f8
ms.reviewer: demerson
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ec80e0cde433f21474a53acf66dbef5ddca206bc
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2020
ms.locfileid: "85502640"
---
# <a name="android-app-protection-policy-settings-in-microsoft-intune"></a>Microsoft Intune 中的 Android 应用保护策略设置
本文介绍适用于 Android 设备的应用保护策略设置。 可在 Azure 门户的“设置”窗格中为应用保护策略[配置](app-protection-policies.md)所述的策略设置。
策略设置分为三类：数据保护设置、访问要求和条件启动。 在本文中，术语策略托管应用指使用应用保护策略配置的应用。

> [!IMPORTANT]
> 设备上需具备 Intune 公司门户，以接收 Android 设备的应用保护策略。 有关详细信息，请参阅 [Intune 公司门户访问应用要求](../fundamentals/end-user-mam-apps-android.md)。
>
> Intune Managed Browser 已停用。 使用 [Microsoft Edge](../apps/manage-microsoft-edge.md) 获取受保护的 Intune 浏览器体验。 

## <a name="data-protection"></a>数据保护 
### <a name="data-transfer"></a>数据传输
| 设置 | 如何使用 | 默认值 |
|------|------|------|
| **将组织数据备份到 Android 备份服务** | 选择“阻止”可阻止此应用将工作或学校数据备份到 [Android 备份服务](https://developer.android.com/google/backup/index.html)。<br><br> 选择“允许”可允许此应用备份工作或学校数据。| **允许** |
| **将组织数据发送到其他应用** | 指定哪些应用可从此应用接收数据： <ul><li> **策略托管应用**：仅允许传输到其他策略托管应用。</li> <li>**所有应用**：允许传输到任何应用。 </li> <li>**无**：不允许将数据传输到任何应用，包括其他策略托管应用。</li></ul> <p>默认情况下，Intune 允许向一些豁免应用和服务传输数据。 此外，如果需要允许将数据传输到不支持 Intune APP 的应用，则可以创建自己的豁免项目。 有关详细信息，请参阅[数据传输豁免](app-protection-policy-settings-android.md#data-transfer-exemptions)。<p>此策略也适用于 Android 应用链接。  通用 Web 链接由“在 Intune Managed Browser 中打开应用链接”策略设置托管。<p><div class="NOTE"><p>备注</p><p>Intune 目前不支持 Android Instant Apps 功能。 Intune 将阻止进/出该应用的任何数据连接。 有关详细信息，请参阅 Android 开发人员文档中的 [Android Instant Apps](https://developer.android.com/topic/instant-apps/index.html)。</p><p>如果“将组织数据发送到其他应用”配置为“所有应用”，则可能仍会通过 OS 共享将文本数据传输到剪贴板 。</p></div> | **所有应用** | 
|<ul><ui>**选择要豁免的应用** | 为上一选项选择“策略托管应用”时，此选项才可用。 | |
|<ul><ui>**保存组织数据的副本** | 选择“阻止”，在此应用中禁用使用“另存为”选项。 如果想要允许使用“另存为”，则选择“允许”。 **注意:** Microsoft Excel、OneNote、PowerPoint 和 Word 支持此设置。它也可能受第三方和 LOB 应用支持。| **允许** |  
|<ul><ui><ul><ui>**允许用户将副本保存到所选的服务** |用户可以保存到所选的服务（OneDrive for Business、SharePoint 和本地存储）中。 将阻止所有其他服务。  | **未选择任何项** |
|<ul><ui>**将电信数据传输到** | 通常，当用户在应用中选择超链接的电话号码时，会打开一个拨号应用，预填充了该电话号码并随时可供拨打。 对于此设置，选择当从策略托管的应用启动电话号码时要如何处理此类型的内容传输：<ul><li>**无，不在应用之间传输此数据**：如果检测到电话号码，不传输通信数据。</li><li>**特定拨号应用**：当检测到电话号码时，允许特定的拨号应用启动联系人。</li><li>**任何由策略管理的拨号应用**：当检测到电话号码时，允许任何任何策略托管的拨号应用启动联系人。</li><li>**任何拨号应用**：当检测到电话号码时，允许使用任何拨号应用启动联系人。</li></ul>| **任何拨号应用** |  
|<ul><ui><ul><ui>**拨号器应用包 ID** | 选择了特定的拨号应用后，必须提供[应用包 ID](../apps/app-configuration-vpn-ae.md#get-the-app-package-id)。 | **空** |
|<ul><ui><ul><ui>**拨号应用名称** | 选择了特定的拨号应用后，必须提供拨号应用的名称。 | **空** |
| **从其他应用接收数据** | 指定哪些应用可将数据传输到此应用： <ul><li>**策略托管应用**：仅允许从其他策略托管应用进行传输。</li><li>**所有应用**：允许从任何应用传输的数据。</li><li>**无**：不允许从任何应用传输数据，包括其他策略托管应用。 </li></ul> <p>Intune 可能会允许从一些豁免应用和服务传输数据。 有关应用和服务的完整列表，请参阅[数据传输豁免](app-protection-policy-settings-android.md#data-transfer-exemptions)。 | **所有应用** |
| **限制在其他应用间进行剪切、复制和粘贴** | 指定剪切、复制和粘贴操作何时可用于此应用。 选择： <ul><li>**阻止**：不允许在此应用和任何其他应用间进行剪切、复制和粘贴操作。</li><li>**策略托管应用**：允许在此应用和其他策略托管应用间进行剪切、复制和粘贴操作。</li><li>**带粘贴的策略托管应用**：允许在此应用和其他策略托管应用间进行剪切或复制。 允许将任何应用中的数据粘贴到此应用。</li><li>**任何应用**：不限制从此应用和对此应用进行剪切、复制和粘贴。 | **任何应用** |
| <ul><ui>**剪切和复制任何应用的字符限制** | 指定可从组织数据和帐户中剪切或复制的字符数。  这样便可以在其他情况下会受到“限制与其他应用进行剪切、复制和粘贴”设置的限制时，共享指定数量的字符。<p>默认值 = 0<p>**注意**：需要 Intune 公司门户版本 5.0.4364.0 或更高版本。  | **0** |
| **屏幕捕获和 Google 助手** | 选择“阻止”，则使用此应用时，会阻止设备的屏幕捕获和“Google 助手”功能 。 选择“允许”还会在通过工作或学校帐户使用此应用时，导致应用切换器预览图像模糊。| **阻止** |
| **批准的键盘**  | 选择“需要”，然后指定此策略的批准的键盘列表。 <p>未使用批准键盘的用户会收到一条提示，要求下载并安装批准的键盘，然后才能使用受保护的应用。 此设置要求应用拥有适用于 Android 的 Intune SDK 版本 6.2.0 或更高版本。 | **不需要** |
| <ul><ui>**选择待批准的键盘** | 为上一选项选择“需要”时，此选项才可用。 选择“选择”以管理可用于受此策略保护的应用的键盘和输入法列表。 可以向列表中添加更多键盘，以及删除任何默认选项。 必须至少有一个批准的键盘才能保存设置。 要添加键盘，请指定： <ul><li>**名称**：标识键盘且对用户可见的易记名称。 </li><li>**包 ID**：Google Play 商店中的应用的包 ID。 例如，如果 Play 商店中应用的 URL 为 `https://play.google.com/store/details?id=com.contoskeyboard.android.prod`，则包 ID 为`com.contosokeyboard.android.prod`。 此包 ID 以简单链接的形式提供给用户，以便用户可以从 Google Play 下载键盘。 <p><div class="NOTE"><p>备注</p><p>被分配了多个应用保护策略的用户只能使用所有策略通用的批准键盘。</p> | |

### <a name="encryption"></a>加密
| 设置 | 如何使用 | 默认值 |
|------|------|------|
| **对组织数据进行加密** | 选择“需要”，在此应用中启用工作或学校数据加密。 Intune 使用 OpenSSL 256 位 AES 加密方案和 Android Keystore 系统安全加密应用数据。 数据在文件 I/O 任务期间同步加密。 设备存储中的内容始终处于加密状态。 新文件将使用 256 位密钥进行加密。 现有的 128 位加密文件将尝试迁移到 256 位密钥，但无法保证该过程。 使用 128 位密钥加密的文件将仍然可读。 <br><br> 加密方法已经过 FIPS 140-2 验证；有关详细信息，请参阅 [OpenSSL FIPS 库和 Android 指南](https://wiki.openssl.org/images/7/76/OpenSSL_FIPS_Library_and_Android_Guide.pdf)。     |  **需要**|  
| <ul><ui>**对已注册设备上的组织数据进行加密** | 选择“需要”，以使用 Intune 应用层加密对所有设备上的组织数据强制执行加密。 选择“不需要”，不使用 Intune 应用层加密对已注册设备上的组织数据强制执行加密。| **需要** |


### <a name="functionality"></a>功能
| 设置 | 如何使用 | 默认值 |
|------|------|------|
| **使用本机联系人应用同步应用** | 选择“阻止”，阻止应用将数据保存到设备上的本机“联系人”应用。 如果选择“允许”，应用可将数据保存到设备上的本机“联系人”应用。 <br><br>执行选择性擦除以从应用删除工作或学校数据时，将删除从应用直接同步到本机“联系人”应用的联系人。 无法擦除从本机通讯簿同步到另一个外部源中的任何联系人。 目前仅适用于 Microsoft Outlook 应用。 | **允许** |
| **打印组织数据** | 选择“阻止”，阻止应用打印工作或学校数据。 如果将此设置保留为“允许”（默认值），用户将能够导出和打印所有组织数据。 | **允许** |
|**限制使用其他应用传输 Web 内容** | 指定如何从策略管理的应用中打开 Web 内容（http/https 链接）。 选择： <ul><li>**任何应用**：允许在任何应用中使用 Web 链接。</li><li>**Intune Managed Browser**：仅允许在 Intune Managed Browser 中打开 Web 内容。 此浏览器是策略托管的浏览器。</li><li>**Microsoft Edge**：仅允许在 Microsoft Edge 中打开 Web 内容。 此浏览器是策略托管的浏览器。</li><li>**非托管浏览器**：允许 Web 内容仅在“非托管浏览器协议”设置定义的非托管浏览器中打开。 Web 内容在目标浏览器中处于非托管状态。<br>**注意**：需要 Intune 公司门户版本 5.0.4415.0 或更高版本。</li><br><br>**策略托管的浏览器**<br>在 Android 上，如果未安装 Intune Managed Browser 和 Microsoft Edge，最终用户可以从支持 http/https 链接的其他策略托管应用中进行选择。<p>如果需要策略托管的浏览器，但未安装，系统将提示最终用户安装 Microsoft Edge。<p>如果需要使用策略托管的浏览器，则将由“允许应用向其他应用传送数据”策略设置管理 Android 应用链接。<p>**Intune 设备注册**<br>如果正使用 Intune 管理设备，请参阅[使用 Microsoft Intune 的托管浏览器策略管理 Internet 访问](manage-microsoft-edge.md)。<p>**策略托管的 Microsoft Edge**<br>移动设备（iOS/iPadOS 和 Android）的 Microsoft Edge 浏览器支持 Intune 应用保护策略。 在 Microsoft Edge 浏览器应用程序中使用其企业 Azure AD 帐户登录的用户将受 Intune 保护。 Microsoft Edge 浏览器集成了 APP SDK 并支持其除阻止以外的所有数据保护策略：<br><ul><li>**另存为**：Microsoft Edge 浏览器不允许用户向云存储提供商（如 OneDrive）添加直接的应用内连接。</li><li>**联系人同步**：Microsoft Edge 浏览器不会保存到本地联系人列表。</li></ul>**注意:** APP SDK 无法确定目标应用是否为浏览器。在 Android 设备上，允许使用支持 http/https 意向的其他托管浏览器应用。 | 未配置 |
|<ul><ui>**非托管浏览器 ID** | 输入单个浏览器的应用程序 ID。 策略托管应用程序的 Web 内容（http/https 链接）将在指定的浏览器中打开。  Web 内容在目标浏览器中处于非托管状态。 | **空** |
|<ul><ui>**非托管浏览器名称** | 输入与“非托管浏览器 ID” 关联的浏览器的应用程序名称。 如果未安装指定的浏览器，将向用户显示此名称。  | **空** |
| **组织数据通知** | 指定针对组织帐户通过 OS 通知共享的组织数据量。 此策略设置将影响本地设备和任何连接的设备，如可穿戴设备和智能扬声器。 应用可能会提供其他控件来自定义通知行为，或者可以选择不接受所有值。 选择： <ul><li>**阻止**：不共享通知。</li><ul><li>如果应用程序不支持，则将允许通知。</li></ul><li>**阻止组织数据**：不要在通知中共享组织数据。 例如“你有新邮件”，“你有个会议”。</li><UL><li>如果应用程序不支持，通知将被阻止。</li></ul><li>**允许**：在通知中共享组织数据</li></ul> <p>**注意**：*此设置需要应用支持。* 适用于 Android 4.0.95 或更高版本的 Outlook 支持此设置。 | **允许**   |

## <a name="data-transfer-exemptions"></a>数据传输豁免

有一些豁免应用和平台服务，Intune 应用保护策略会允许向其或从其传输数据。 例如，Android 上所有 Intune 托管的应用都必须能够将数据传输至 Google 文本到语音转换或从中接收数据，这样使移动设备屏幕上的文本可以被朗读出来。 此列表可能会更改以反映有利于安全工作效率的服务和应用。

### <a name="full-exemptions"></a>完全豁免

  完全允许这些应用和服务向 Intune 托管应用传输数据或从其接收数据。

  |应用/服务名称 | 说明 |
  | ------ | ---- |
  | com.android.phone | 本机电话应用
  | com.android.vending | Google Play Store |
  | com.android.documentsui | Android 文档选取器|
  | com.google.android.webview | [WebView](https://developer.android.com/reference/android/webkit/WebView.html)，这是包括 Outlook 在内的许多应用所必需的。 |
  | com.android.webview |[Webview](https://developer.android.com/reference/android/webkit/WebView.html)，这是包括 Outlook 在内的许多应用所必需的。|
  | com.google.android.tts | Google 文本到语音转换 |
  | com.android.providers.settings | Android 系统设置 |
  | com.android.settings | Android 系统设置 |
  | com.azure.authenticator | Azure 验证器应用，这是在许多情况下成功进行身份验证所必需的。 |
  | com.microsoft.windowsintune.companyportal | Intune 公司门户|

### <a name="conditional-exemptions"></a>有条件的豁免
  只有在某些条件下，才允许这些应用和服务向 Intune 托管应用传输数据或从其接收数据。

  |应用/服务名称 | 说明 | 豁免条件|
  | ------ | ---- | --- |
  | com.android.chrome | Google Chrome 浏览器 | Chrome 用于 Android 7.0 及更高版本上的某些 WebView 组件，并且永远不会从视图中隐藏。 但是，该应用发出和收到的数据流始终受限。  |
  | com.skype.raider | Skype | Skype 应用仅允许执行引发电话呼叫的某些操作。 |
  | com.android.providers.media | Android 媒体内容提供程序 | 媒体内容提供程序仅允许铃声选择操作。 |
  | com.google.android.gms;com.google.android.gsf | Google Play Services 包 | 这些包允许 Google Cloud Messaging 操作，例如推送通知。 |
  | com.google.android.apps.maps | Google 地图 | 允许使用地址进行导航 |

有关详细信息，请参阅[应用的数据传输策略例外情况](app-protection-policies-exception.md)。

## <a name="access-requirements"></a>访问要求

| 设置 | 如何使用 |  
|------|------| 
| **需要 PIN 才能进行访问** | 选择“需要”，要求使用 PIN 才能使用此应用。 用户首次在工作或学校环境中运行应用时，将提示其设置此 PIN。 <br><br> 默认值 = **需要**<br><br> 可以使用“需要 PIN 才能进行访问”部分下提供的设置配置 PIN 强度。
| <ul><ui>**PIN 类型** | 在访问应用了应用保护策略的应用之前，为数值或密码类型 PIN 设置要求。 数值要求只涉及数字，而密码则可采用至少 1 个字母或至少 1 个特殊字符进行定义。 <br><br> 默认值 = 数值<br><br> **注意:** 允许的特殊字符包括 Android 英语键盘上的特殊字符和符号。 |
| <ul><ui> **简单 PIN** | 选择“允许”，允许用户使用 1234、1111、abcd 或 aaaa 等简单的 PIN 序列   。 选择“阻止”，阻止用户使用简单的序列。 在 3 个字符滑动窗口中检查简单的序列。 如果配置了“阻止”，则不会接受 1235 或 1112 作为由最终用户设置的 PIN，但允许采用 1122。 <br><br>默认值 = **允许** <br><br>**注意:** 如果配置了密码类型 PIN，并且“简单 PIN”设置为“允许”，用户在其 PIN 中则需要使用至少 1 个字母或至少 1 个特殊字符。 如果配置了密码类型 PIN，并且“简单 PIN”设置为“阻止”，用户在其 PIN 中则需要使用至少 1 个数字和 1 个字母以及至少 1 个特殊字符 。 </li> |
| <ul><ui> **选择最小 PIN 长度** | 指定 PIN 序列必须包含的最小位数。 <br><br>默认值 = 4 | 
| <ul><ui> **用于访问的指纹而非 PIN (Android 6.0+)** | 选择“允许”，允许用户使用[指纹身份验证](https://developer.android.com/about/versions/marshmallow/android-6.0.html#fingerprint-authentication)而非 PIN 进行应用访问。 <br><br>默认值 = **允许** <br><br>**注意:** 此功能支持 Android 设备上的通用生物识别控件。 不支持特定于 OEM 的生物识别设置，如 Samsung Pass。 <br><br>在 Android 设备上，可让用户通过 [Android 指纹身份验证](https://developer.android.com/about/versions/marshmallow/android-6.0.html#fingerprint-authentication)而非 PIN 证明其身份。 用户尝试通过其工作或学校帐户使用此应用时，系统会提示他们提供其指纹标识，而不是输入 PIN。 <br><br> Android 工作配置文件注册设备要求为强制执行的“访问时使用指纹替代 PIN”策略注册单独的指纹。 此策略仅对在 Android 工作配置文件中安装的策略托管应用有效。 在公司门户注册以创建 Android 工作配置文件后，必须在设备中注册单独的指纹。 有关使用 Android 工作配置文件的工作配置文件指纹的详细信息，请参阅[锁定工作配置文件](https://support.google.com/work/android/answer/7029958)。 |
| <ul><ui>**超时后使用 PIN 替代指纹**| 要使用此设置，请选择“需要”，然后配置非活动超时。 <br><br>默认值 = **需要** |
| <ul><ui><ul><ui> **超时(非活动状态的分钟数)**| 指定密码或数值 PIN（如配置所示）将覆盖指纹的使用的时间（以分钟为单位）。 此超时值应大于“在(非活动状态的分钟数)后重新检查访问要求”下的指定值。<br><br>默认值 = 30 |
| <ul><ui>**PIN 重置间隔的天数** | 选择“是”，要求用户在一段时间（以天为单位）后更改其应用 PIN。  <br><br>如果设置为“是”，然后配置 PIN 重置所需的间隔天数。 <br><br> 默认值 = 否  |  
| <ul><ui><ul><ui> **天数** | 配置 PIN 重置所需的间隔天数。 <br><br> 默认值 = **90**  |
| <ul><ui>**选择要保留的以前的 PIN 值的数目** | 此设置指定 Intune 要保留的以前的 PIN 的数量。 新的 PIN 须不同于 Intune 所保留的。 <br><br> 默认值 = **0** | 
| <ul><ui>**设置设备 PIN 时的应用 PIN** | 选择“不需要”，如果在已配置公司门户的已注册设备上检测到设备锁，则禁用应用 PIN。 <br><br> 默认值 = **需要**。 | 
| **用于访问的工作或学校帐户凭据** | 选择“需要”，要求用户使用其工作或学校帐户而非输入 PIN 进行登录以访问应用。 设置为“需要”并且 PIN 或生物识别提示已打开时，将同时显示公司凭据以及 PIN 或生物识别提示。 <br><br>默认值 = **不需要** |
| **在(非活动状态的分钟数)后重新检查访问要求** | 配置下列设置： <ul><li>**超时**：这是重新检查访问要求（在前面的策略中定义）之前的分钟数。 例如，如果管理员在策略中启用 PIN 并阻止取得 root 权限的设备，用户打开 Intune 托管应用时，则必须输入 PIN，并且必须在未取得 root 权限的设备上使用此应用。 使用此设置时，用户在与配置值相等的一段时间内无需在任何 Intune 托管应用上再次输入 PIN 或再次经历 root 检测检查。  <br><br>此策略设置格式支持正整数。 <br><br> 默认值 = 30 分钟 <br><br> **注意:** 在 Android 上，所有 Intune 托管应用均共享此 PIN。 应用离开设备主屏幕后，就会重置 PIN 计时器。 在此设置中定义的超时期限内，用户无需在共享 PIN 的任何 Intune 托管应用上输入此 PIN。 <br><br></li> |

> [!NOTE]  
> 要详细了解在“访问权限”部分配置给同一组应用和用户的多个 Intune 应用保护设置如何在 Android 上运行，请参阅 [Intune MAM 常见问题](mam-faq.md)和[在 Intune 中使用应用保护策略访问操作选择性地擦除数据](app-protection-policies-access-actions.md)。


## <a name="conditional-launch"></a>条件启动
配置条件启动设置以设置访问保护策略的登录安全要求。 

默认情况下，向多个设置提供已预配置的值和操作。 可以删除“最小 OS 版本”等某些设置。 此外，还可以从“选择一个”下拉列表中选择其他设置。 

| 设置 | 如何使用 |  
|---------|------------| 
| **最大 PIN 尝试次数** | 指定用户在执行配置操作之前必须成功输入其 PIN 的尝试次数。 此策略设置格式支持正整数。 *操作*包括： <br><ul><li>**重置 PIN** - 用户必须重置其 PIN。</li></ul> <ul><li>**擦除数据** - 从设备中擦除与应用程序关联的用户帐户。  </li></ul> </li></ul> 默认值 = 5 |
| **脱机宽限期** | MAM 应用可以脱机运行的分钟数。 指定重新检查应用访问要求之前的时间（以分钟为单位）。 *操作*包括： <br><ul><li>**阻止访问（分钟数）** - MAM 应用可以脱机运行的分钟数。 指定重新检查应用访问要求之前的时间（以分钟为单位）。 此期限到期后，该应用需要对 Azure Active Directory (Azure AD) 进行用户身份验证，以便该应用可以继续运行。 <br><br>此策略设置格式支持正整数。 <br><br>默认值 = 720 分钟（12 小时） </li></ul> <ul><li>**擦除数据（天数）** - 经过数天（由管理员定义）的脱机运行后，应用会要求用户连接到网络并重新进行身份验证。 如果用户身份验证成功，则可继续访问其数据，且将重置脱机时间间隔。  如果用户未能通过身份验证，则应用会对用户帐户和数据执行选择性擦除。 有关详细信息，请参阅[如何仅擦除 Intune 托管应用中的企业数据](apps-selective-wipe.md)。</li></ul> 此策略设置格式支持正整数。 <br><br>  默认值 = 90 天 </li></ul> <br><br>  此项可以出现多次，每个实例支持不同的操作。 |   
| **已越狱/获得 root 权限的设备** |此设置没有可设置的值。 *操作*包括： <br><ul><li>**阻止访问** - 阻止在已越狱或已取得 root 权限的设备上运行此应用。 用户仍能够将此应用用于个人任务，但必须使用其他设备才能访问此应用中的工作或学校数据。</li></ul> <ul><li>**擦除数据** - 从设备中擦除与应用程序关联的用户帐户。  </li></ul> |
| **最低 OS 版本** | 指定要使用此应用所需的最低 Android 操作系统版本。 *操作*包括： <br><ul><li>**警告** - 如果设备上的 Android 版本不符合此要求，用户将看到一个通知。 可忽略此通知。  </li></ul> <ul><li>**阻止访问** - 如果设备上的 Android 版本不符合此要求，将阻止用户访问。</li></ul> <ul><li>**擦除数据** - 从设备中擦除与应用程序关联的用户帐户。  </li></ul> </li></ul>此策略设置格式支持 major.minor、major.minor.build 或 major.minor.build.revision。 |
| **最低应用版本** | 指定最低操作系统值的值。 *操作*包括： <br><ul><li>**警告** - 如果设备上的应用版本不符合此要求，用户将会看到一个通知。 可忽略此通知。</li></ul> <ul><li>**阻止访问** - 如果设备上的应用版本不符合此要求，用户将会看到一个通知。 </li></ul> <ul><li>**擦除数据** - 从设备中擦除与应用程序关联的用户帐户。 </li></ul> </li></ul> 由于应用之间通常拥有不同的版本控制方案，因此，请创建针对一个应用的一个最低应用版本策略（例如 Outlook 版本策略）。<br><br> 此项可以出现多次，每个实例支持不同的操作。<br><br> 此策略设置格式支持 major.minor、major.minor.build 或 major.minor.build.revision。<br><br> 此外，还可以配置最终用户可获取更新业务线 (LOB) 应用版本的位置。 最终用户将在“最低应用版本”条件启动对话框中看到此项，系统将提示最终用户更新到 LOB 应用的最低版本。 在 Android 上，此功能使用公司门户。 若要配置最终用户应更新 LOB 应用的位置，应用需要使用键 `com.microsoft.intune.myappstore` 发送给它的托管[应用配置策略](app-configuration-policies-managed-app.md)。 发送的值将定义最终用户从哪个应用商店中下载应用。 如果应用是通过公司门户部署的，则值必须为 `CompanyPortal`。 对于任何其他应用商店，必须输入完整的 URL。 |
| **最低修补程序版本** | 要求设备具有由 Google 发布的最低 Android 安全修补程序。  <br><ul><li>**警告** - 如果设备上的 Android 版本不符合此要求，用户将看到一个通知。 可忽略此通知。  </li></ul> <ul><li>**阻止访问** - 如果设备上的 Android 版本不符合此要求，将阻止用户访问。</li></ul> <ul><li>**擦除数据** - 从设备中擦除与应用程序关联的用户帐户。  </li></ul></li></ul> 此策略设置支持日期格式 YYYY-MM-DD。 |
| **设备制造商** | 指定以分号分隔的制造商列表。 这些值不区分大小写。 *操作*包括： <br><ul><li>**允许指定项（阻止非指定项）** - 仅与指定制造商匹配的设备才能使用该应用。 所有其他设备将被阻止。 </li></ul> <ul><li>**允许指定项（擦除非指定项）** - 从设备中擦除与应用程序关联的用户帐户。 </li></ul> 若要详细了解如何使用此设置，请参阅[条件启动操作](app-protection-policies-access-actions.md#android-policy-settings)。 |
| **SafetyNet 设备证明** | 应用保护策略支持 Google Play Protect 的某些 API。 具体而言，此设置在最终用户设备上配置 Google 的 SafetyNet 证明。 指定“基本完整性”或“基本完整性和认证设备” 。 “基本完整性”描述设备的总体完整性。 已取得根权限的设备、模拟器、虚拟设备以及具有篡改迹象的设备无法通过基本完整性检查。 “基本完整性和认证设备”描述设备与 Google 服务的兼容性。 只有经过 Google 认证的未修改的设备才能通过此检查。 *操作*包括： <br><ul><li>**警告** - 如果基于配置的值，设备未通过 Google 的 SafetyNet 证明扫描检查，用户会看到一条通知。 可忽略此通知。 </li></ul><ul><li>**阻止访问** - 如果基于配置的值，设备未通过 Google 的 SafetyNet 证明扫描检查，会阻止用户访问。 </li></ul> <ul><li>**擦除数据** - 从设备中擦除与应用程序关联的用户帐户。 </li></ul> </li></ul> 有关此设置的常见问题，请参阅[有关 MAM 和应用保护的常见问题解答](mam-faq.md#app-experience-on-android)。 |
| **要求对应用进行威胁扫描** | 应用保护策略支持 Google Play Protect 的某些 API。 具体而言，此设置确保为最终用户设备启用 Google 的“验证应用”扫描。 如果配置了此设置，将阻止最终用户访问，直至他们在其 Android 设备上启用 Google 的应用扫描设置。 *操作*包括： <br><ul><li>**警告** - 如果未在设备上启用 Google 的验证应用扫描，用户会看到一条通知。 可忽略此通知。 </li></ul><ul><li>**阻止访问** - 如果未在设备上启用 Google 的验证应用扫描，会阻止用户访问。 </li></ul></li></ul> Google 的验证应用扫描结果显示在控制台的“可能有害的应用”报告中。 |
| **最小公司门户版本** | 通过使用最小公司门户版本，可以指定在最终用户设备上强制执行的公司门户的特定最低定义版本。 使用此条件启动设置，可以在不满足每个值时将值设置为“阻止访问”、“擦除数据”和“警告”作为可能的操作  。 此值的可能格式遵循 [主版本].[次版本]、[主版本].[次版本].[内部版本] 或 [主版本].[次版本].[内部版本].[修订版本]  。 假设某些最终用户可能不希望立即强制更新应用，则在配置此设置时，“警告”选项可能是理想的选择。 Google Play 商店能够很好地仅为应用更新发送增量字节，但在更新数据时，仍可能有大量数据是用户不想使用的。 强制执行更新并下载更新的应用可能会导致更新时产生意外的数据费用。 有关详细信息，请参阅 [Android 策略设置](app-protection-policies-access-actions.md#android-policy-settings)。 |
| **允许的最大设备威胁级别** | 应用保护策略可以利用 Intune-MTD 连接器。 指定使用此应用可接受的最高威胁级别。 威胁由最终用户设备上选择的移动威胁防御 (MTD) 供应商应用确定。 指定安全、低、中或高   。 “安全”要求设备上没有任何威胁，是可配置的限制性最强的值，而“高”实质上要求存在 Intune 到 MTD 的活动连接 。 *操作*包括： <br><ul><li>**阻止访问** - 如果你选择的移动威胁防御 (MTD) 供应商应用确定最终用户设备上的威胁级别不满足此要求，则将阻止用户访问。</li></ul> <ul><li>**擦除数据** - 从设备中擦除与应用程序关联的用户帐户。</li></ul>有关使用此设置的详细信息，请参阅[在 Intune 中为未注册的设备启用移动威胁防御连接器](../protect/mtd-enable-unenrolled-devices.md)。 |
