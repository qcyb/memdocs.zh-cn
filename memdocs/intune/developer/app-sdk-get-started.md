---
title: Microsoft Intune App SDK 入门
description: 通过 Microsoft Intune 快速启用移动应用进行移动应用程序管理 (MAM)。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/02/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 38ebd3f5-cfcc-4204-8a75-6e2f162cd7c1
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8189a23c2f07ebce03716ecf111c0130942b8b68
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79343019"
---
# <a name="get-started-with-the-microsoft-intune-app-sdk"></a>Microsoft Intune App SDK 入门

本指南将帮助通过 Microsoft Intune 快速启用移动应用以支持应用保护策略。 先去了解 [Intune App SDK 概述](app-sdk.md)中介绍的 Intune App SDK 优点可能会很有帮助。

Intune App SDK 支持跨 iOS 或 Android 的类似方案，旨在跨平台为 IT 管理员创造一致的体验。 但是由于平台差异和限制，某些功能的支持存在细微差异。

## <a name="register-your-store-app-with-microsoft"></a>向 Microsoft 注册应用商店应用

### <a name="if-your-app-is-internal-to-your-organization-and-will-not-be-publicly-available"></a>如果应用位于组织内部且非公用：

则无需注册应用 __ 。 对于由公司编写或为公司编写的内部[业务线 (LOB) 应用](../apps/apps-add.md#app-types-in-microsoft-intune)，IT 管理员将在内部部署该应用。 Intune 将检测已使用 SDK 构建的应用，并允许 IT 管理员对其应用保护策略。 可跳到[启用 iOS 或 Android 应用的应用保护策略](#enable-your-ios-or-android-app-for-app-protection-policy)部分。

### <a name="if-your-app-will-be-released-to-a-public-app-store-like-the-apple-app-store-or-google-play"></a>如果应用将被发布到公共应用商店（例如Apple App Store 或 Google Play）：

则 _**必须**_ 首先向 Microsoft Intune 注册应用并同意注册条款。 然后，IT 管理员可将应用保护策略应用到托管应用，该应用将被列为[受 Intune 保护的合作伙伴应用](../apps/apps-supported-intune-apps.md#partner-apps)。

除非已完成注册并已由 Microsoft Intune 团队确认，否则 Intune 管理员不能向应用深层链接应用应用保护策略。 Microsoft 还会将你的应用添加到其 [Microsoft Intune 合作伙伴页](https://www.microsoft.com/cloud-platform/microsoft-intune-apps)。 在该页面中，将显示应用的图标，表明它支持 Intune 应用保护策略。

### <a name="the-registration-process"></a>注册过程
要开始注册过程，且如果尚未使用 Microsoft 联系人，请填写 [Microsoft Intune 应用程序合作伙伴问卷](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR80SNPjnVA1KsGiZ89UxSdVUMEpZNUFEUzdENENOVEdRMjM5UEpWWjJFVi4u)。

我们将使用调查表答复中列出的电子邮件地址来联系你并继续注册过程。 此外，如果我们有任何问题，我们会使用你的注册电子邮件地址与你联系。

> [!NOTE]
> 在调查表中以及通过与 Microsoft Intune 团队的电子邮件通信收集到的所有信息都会遵循 [Microsoft 隐私声明](https://www.microsoft.com/privacystatement/default.aspx)。

**注册过程中会出现的情况**：

1. 提交调查表后，我们会通过你的注册电子邮件地址联系你，以确认成功接收或请求提供其他信息以完成注册。

2. 接收到所有必要信息后，我们将发送 Microsoft Intune 应用合作伙伴协议供你签名。 此协议描述了你的公司在成为 Microsoft Intune 应用合作伙伴之前必须接受的条款。

3. 向 Microsoft Intune 服务成功注册应用后以及在 [Microsoft Intune 合作伙伴](https://www.microsoft.com/cloud-platform/microsoft-intune-apps)站点上推荐你的应用时会予以通知。

4. 最后，会将你的应用的深层链接添加到下个月的 Intune 服务更新中。 例如，如果注册信息在七月完成，则会在八月中旬支持深层链接。

深层链接是指向公共应用商店中应用的列表的链接。 如果应用的深层链接在将来发生更改，则需要重新注册应用。

> [!NOTE]
> 如果使用新版本的 Intune App SDK 更新应用，则必须告知我们。

## <a name="download-the-sdk-files"></a>下载 SDK 文件

用于本机 iOS 和 Android 的 Intune App SDK 都托管于 Microsoft GitHub 帐户。 下面的公共存储库具有适用于本机 iOS 和 Android 的 SDK 文件，分别为：

* [用于 iOS 的 Intune 应用 SDK](https://github.com/msintuneappsdk/ms-intune-app-sdk-ios)
* [用于 Android 的 Intune 应用 SDK](https://github.com/msintuneappsdk/ms-intune-app-sdk-android)

如果应用是 Xamarin 应用，请使用此 SDK 变量：

* [Intune App SDK Xamarin Bindings](https://github.com/msintuneappsdk/intune-app-sdk-xamarin)

注册可用于从存储库中分叉和拉取的 GitHub 帐户是一个好办法。 GitHub 可让开发人员与我们的产品团队进行沟通、开展问题并快速接收回复、查看发行说明并向 Microsoft 提供反馈。 有关 Intune App SDK GitHub 方面的疑问，请联系 msintuneappsdk@microsoft.com。

## <a name="enable-your-ios-or-android-app-for-app-protection-policy"></a>启用 iOS 或 Android 应用的应用保护策略

需要参阅以下开发人员指南中的一个来帮助将 Intune App SDK 集成到应用：

* **[Intune App SDK for iOS 开发人员指南](app-sdk-ios.md)** ：本文档将指导逐步完成使用 Intune App SDK 启用本机 iOS 应用的过程。

* **[Intune App SDK for Android 开发人员指南](app-sdk-android.md)** ：本文档将指导逐步完成使用 Intune App SDK 启用本机 Android 应用的过程。

* **[Intune App SDK Xamarin Bindings 指南](app-sdk-xamarin.md)** ：此文档可帮助使用 Intune 应用保护策略适用的 Xamarin 来生成 iOS 和 Android 应用。



## <a name="enable-your-ios-or-android-app-for-app-based-conditional-access"></a>为 iOS 或 Android 应用启用基于应用的条件访问

除了为应用启用应用保护策略外，还需要为应用启用以下策略，这样应用才能正常使用基于 Azure ActiveDirectory (AAD) 应用的条件访问：

* 使用 [Azure ActiveDirectory 身份验证库](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-libraries)构建应用并对其启用 AAD 代理身份验证。

* iOS 和 Android 平台上的应用的 [AAD 客户端 ID](https://docs.microsoft.com/azure/app-service/app-service-mobile-how-to-configure-active-directory-authentication#configure-a-native-client-application) 必须是唯一的。

## <a name="configure-telemetry-for-your-app"></a>配置应用遥测

Microsoft Intune 收集应用的使用情况统计数据。

* **用于 iOS 的 Intune 应用 SDK**：默认情况下，SDK 会记录有关使用事件的 SDK 遥测数据。 会将此数据发送到 Microsoft Intune。

  * 如果选择不从应用将 SDK 遥测数据发送到 Microsoft Intune，则必须通过在 IntuneMAMSettings 字典中将属性 `MAMTelemetryDisabled` 设置为“YES”，来禁用遥测数据传输。

* **Intune App SDK for Android**：Intune App SDK for Android 不会控制应用中的数据集合。 默认情况下，公司门户应用会记录遥测数据。 会将此数据发送到 Microsoft Intune。 根据 Microsoft 策略，我们不会收集任何个人身份信息 (PII)。 

  * 如果最终用户选择不发送此数据，则必须在“公司门户”应用的“设置”下关闭遥测。 有关详细信息，请参阅[关闭 Microsoft 使用情况数据收集](https://docs.microsoft.com/user-help/turn-off-microsoft-usage-data-collection-android)。 

## <a name="line-of-business-app-version-numbers"></a>业务线应用版本号

现在，Intune 中的业务线应用会显示 iOS 和 Android 应用的版本号。 版本号会在 Azure 门户、应用列表和应用概述边栏选项卡中显示。 最终用户可在公司门户应用和 Web 门户中查看应用的版本号。

### <a name="full-version-number"></a>完整版本号

完整版本号标识应用的特定版本。 该号码显示为“版本号(内部版本号)”   。 例如：2.2(2.2.17560800)。 

完整版本号包含两个部分：

- **版本**  
  版本号是应用的发行版号（可人工读取）。 最终用户使用版本号确定应用的不同发行版。

- **内部版本号**  
  内部版本号是一个内部号码，可在应用检测中使用，并可用于以编程方式管理应用。 内部版本号是指应用的迭代，应用可引用代码中的更改。

### <a name="version-and-build-number-in-android-and-ios"></a>Android 和 iOS 中的版本号和内部版本号

Android 和 iOS 都使用应用相关的版本号和内部版本号。 但是，这两个操作系统都具有特定于 OS 的含义。 下表说明了这些术语之间的关联。

开发用于 Intune 的业务线应用程序时，请务必使用版本号和内部版本号。 Intune 应用管理功能依赖于有意义的 CFBundleVersion（适用于 iOS）和 PackageVersionCode（适用于 Android）   。 这些号码都包括在应用清单中。 

Intune|iOS|Android|说明|
|---|---|---|---|
版本号|CFBundleShortVersionString|PackageVersionName |此号码为最终用户指示应用的特定版本。|
内部版本号|CFBundleVersion|PackageVersionCode |此号码用于指示应用代码中的迭代。|

#### <a name="ios"></a>iOS

- **CFBundleShortVersionString**  
  指定程序包的发行版本号。 此号码表示应用的发行版本。 最终用户使用此号码引用应用。
- **CFBundleVersion**  
  程序包的内部版本，它标识程序包的迭代。 此号码可标识发行或未发行的程序包。 此号码用于应用检测。

#### <a name="android"></a>Android

- **PackageVersionName**  
  向用户显示的版本号。 可将此属性设置为原始字符串或对字符串资源的引用。 字符串仅用于向用户显示。
- **PackageVersionCode**  
  内部版本号。 此号码仅用于确定某个版本是否比另一个版本新，数字越大表示版本越新。 这不是向用户显示的版本号 

## <a name="next-steps-after-integration"></a>集成后的后续步骤

### <a name="test-your-app"></a>测试应用程序
完成将 iOS 或 Android 应用与 Intune App SDK 集成的必需步骤后，需确保所有应用保护策略都已针对用户和 IT 管理员启用并正常工作。若要测试已集成的应用，则需查看以下文档：

* **Microsoft Intune 测试帐户**：若要就 Intune 应用保护功能对 Intune 托管的应用进行测试，将需要 Microsoft Intune 帐户。

  * 如果启用 Intune 应用保护策略 iOS 或 Android 应用商店应用的 ISV，则在使用 Microsoft Intune 完成注册（如注册步骤中所述）后，会收到促销代码。 促销代码允许你注册具有 1 年延期使用的 Microsoft Intune 试用。

  * 如果你正在开发一套不会发送到应用商店的业务应用，则你应能够通过你的组织访问 Microsoft Intune。 你还可以在 [Microsoft Intune](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=40BE278A-DFD1-470a-9EF7-9F2596EA7FF9&dl=INTUNE_A&ali=1#0) 中注册为期 1 个月的免费试用。

  * 如果使用最终用户帐户在移动设备上测试应用，请确保已使用管理员帐户登录 Microsoft 365 管理中心网站，并向该帐户授予 Intune 许可证，请参阅[分配 Microsoft Intune 许可证](../fundamentals/licenses-assign.md)。

* **Intune 应用保护策略**：若要针对所有 Intune 应用保护策略对应用进行测试，则应了解针对每个策略设置，应用的预期行为。 请参阅 [iOS 应用保护策略](../apps/app-protection-policy-settings-ios.md)和 [Android 应用保护策略](../apps/app-protection-policy-settings-android.md)的说明。 如果应用已集成 Intune SDK，但未在可面向应用的列表中列出，则在选择“自定义应用”时，你可以在文本框中指定应用的程序包 ID (iOS) 或包名称 (Android)。 

* **疑难解答**：如果在手动测试应用的安装用户体验时遇到任何问题，请参阅[应用安装问题疑难解答](../apps/troubleshoot-app-install.md)。 

### <a name="give-your-app-access-to-the-intune-app-protection-service-optional"></a>向 Intune 应用保护服务提供应用访问权限（可选）

如果应用正在使用其自己的自定义 Azure Active Directory (AAD) 设置进行身份验证，则应为公共应用商店应用以及内部 LOB 应用执行以下步骤。 如果应用正在使用 Intune SDK 默认客户端 ID，则不需要执行这些步骤  。 

一旦在 Azure 租户内注册应用并在“所有应用程序”下显示该应用  ，就必须向 Intune 应用保护服务（以前称为 MAM 服务）提供应用访问权限。 在 Azure 门户中：

1. 转到“Azure Active Directory”边栏选项卡  。
2. 在“应用注册”下，转到为应用程序设置的列表  。
3. 单击“+ 添加权限”  。
4. 单击“我的组织使用的 API”  。 
5. 在搜索框中，输入“Microsoft 移动应用程序管理”  。
6. 在“委托的权限”  下，选择“DeviceManagementManagedApps.ReadWrite:读取和写入用户的应用管理数据”  复选框。
7. 单击“添加权限”  。

> [!NOTE]
> 如果应用由于访问此资源（https\://intunemam.microsoftonline.com）出错而限制你登录，必须使用应用的客户端 ID 将注释发送到 msintuneappsdk@microsoft.com。 目前这是一个手动的审批过程。

### <a name="badge-your-app-optional"></a>标记应用（可选）

在验证 Intune 应用保护策略可在应用中正常工作后，可使用 Intune 应用保护徽标来标记应用图标。

此标记向 IT 管理员、最终用户以及潜在的 Intune 客户提供指示，即应用使用 Intune 应用保护策略。 它可促使 Intune 客户采用你的应用。

该标记是一个“公文包”图标，如下例中所示：

![Intune 应用保护策略 - 标记示例 1](./media/app-sdk-get-started/badge-example-1.png) ![Intune 应用保护策略 - 标记示例 2](./media/app-sdk-get-started/badge-example-2.png)

**标记应用时的所需条件**:

* 一个图像处理应用程序，可读取 **.eps** 文件，或一个 Adobe 应用程序，可以读取 **.ai** 文件。

* 可在 Microsoft Intune GitHub 上找到 [Intune 应用标记资产和指导原则](https://github.com/msintuneappsdk/intune-app-partner-badge)。
