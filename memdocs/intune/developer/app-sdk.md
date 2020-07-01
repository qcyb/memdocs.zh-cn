---
title: Intune 应用 SDK 的优点
titleSuffix: Microsoft Intune
description: Intune 应用 SDK 同时适用于 iOS 和 Android 平台，并允许通过 Microsoft Intune 使用移动应用管理功能。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/27/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: cd9f05e7-26e6-45e0-8d38-67d8232b1cae
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: c0a732db0adf9d08bf8a453a365002d8e1f8b22d
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2020
ms.locfileid: "85502708"
---
# <a name="microsoft-intune-app-sdk-overview"></a>Microsoft Intune App SDK 概述
Intune App SDK 可用于 iOS 和 Android，可让应用支持 Intune [应用保护策略](../apps/app-protection-policy.md)。 如果应用应用了应用保护策略，它可以由 Intune 托管，并被 Intune 识别为托管应用。 此 SDK 努力使应用开发者所需的代码更改数量降到最低。 你会发现可以在不改变应用行为的情况下启用大部分 SDK 功能。 为了增强最终用户和 IT 管理员体验，可利用 SDK 的 API 自定义应用行为以支持需要应用参与的功能。

使应用能够支持 Intune 应用保护策略后，IT 管理员可部署这些策略来保护应用内的公司数据。

## <a name="app-protection-features"></a>应用保护功能

以下是可通过 SDK 来启用的 Intune 应用保护功能的示例。

### <a name="control-users-ability-to-move-corporate-files"></a>控制用户移动公司文件的能力
IT 管理员可控制应用中的工作或学校数据可移动到什么位置。 例如，他们可以部署策略来禁止应用将公司数据备份到云。

### <a name="configure-clipboard-restrictions"></a>配置剪贴板限制
IT 管理员可以配置 Intune 托管应用中的剪贴板行为。 例如，IT 管理员可部署策略来防止最终用户将数据从应用剪切或复制并粘贴到非托管的个人应用。

### <a name="enforce-encryption-on-saved-data"></a>对已保存数据强制执行加密
IT 管理员可以强制执行策略，确保对应用保存到设备的数据进行加密。

### <a name="remotely-wipe-corporate-data"></a>远程擦除公司数据
IT 管理员可从 Intune 托管的应用远程擦除企业数据。 此功能基于标识，将仅删除与最终用户的公司标识相关联的文件。 若要执行此操作，此功能要求应用的参与。 应用可指定基于用户设置应进行擦除的标识。 在应用没有指定这些用户设置的情况下，默认行为是擦除应用程序目录，并通知最终用户已删除访问权限。

### <a name="enforce-the-use-of-a-managed-browser"></a>强制使用托管浏览器
IT 管理员可使用 [Intune Managed Browser 应用](../apps/manage-microsoft-edge.md)强制打开应用中的 Web 链接。 此功能可确保企业环境中显示的链接保持在 Intune 管理的应用的域中。

### <a name="enforce-a-pin-policy"></a>强制执行 PIN 策略
IT 管理员可要求最终用户输入 PIN 以访问应用中的公司数据。 这可确保使用应用的用户与最初使用工作或学校帐户登录的用户为同一用户。 最终用户配置其 PIN 时，Intune App SDK 使用 Azure Active Directory 验证最终用户的凭据是否为已注册的 Intune 帐户。

### <a name="require-users-to-sign-in-with-a-work-or-school-account-for-app-access"></a>要求用户使用工作或学校帐户进行登录以访问应用
IT 管理员可以要求用户使用其工作或学校帐户登录以访问该应用。 Intune App SDK 使用 Azure Active Directory 提供单一登录体验，其中一旦输入凭据就将在后续登录中重用该凭据。 我们还支持通过与 Azure Active Directory 联合的标识管理解决方案进行身份验证。

### <a name="check-device-health-and-compliance"></a>检查设备运行状况和合规性
在最终用户访问应用之前，IT 管理员可以检查设备的运行状况及其是否符合 Intune 策略。 在 iOS/iPadOS 上，此策略将检查设备是否已越狱。 在 Android 上，此策略将检查设备是否已获得 root 权限。

### <a name="support-multi-identity"></a>支持多身份
多身份支持功能是 SDK 的一种功能，其允许策略托管（企业）帐户和非托管（个人）帐户在单个应用中共存。

例如，许多用户在 iOS 和 Android 的 Office 移动应用中同时配置公司和个人电子邮件帐户。 当用户使用公司帐户访问数据时，IT 管理员必须确信实施应用保护策略。 但是，当用户访问个人电子邮件帐户时，该数据应在 IT 管理员的控制之外。 Intune App SDK 通过**仅**将应用保护策略应用到应用中的公司标识来实现此功能。

多身份功能有助于解决同时支持个人和工作帐户的应用商店应用带给组织的数据保护问题。
 
### <a name="app-protection-without-device-enrollment"></a>无需设备注册的应用保护

>[!IMPORTANT]
>Intune 应用包装工具、Intune App SDK for Android、Intune App SDK for iOS 和 Intune App SDK Xamarin Bindings 提供无需设备注册的 Intune 应用保护。

许多用户使用个人设备，他们希望在不为其个人设备注册移动设备管理 (MDM) 提供程序的情况下访问公司数据。 由于 MDM 注册要求对设备的全局控制权，而用户对于将其个人设备的控制权交给公司有所顾虑。

无需设备注册的应用保护允许 Microsoft Intune 服务将应用保护策略直接部署到应用，而不依赖设备管理通道来部署策略。

### <a name="on-demand-application-vpn-connections-with-citrix-mvpn"></a>按需应用与 Citrix mVPN 的 VPN 连接 
可以同时使用 Citrix XenMobile MDX 和 Microsoft Intune 来管理设备和应用。 这种组合意味着可在使用 Citrix mVPN 技术的同时通过 Intune 应用保护策略管理应用。 与 Citrix 的集成可用于 Intune App SDK for iOS 和 Intune App SDK for Android，以及适用于 iOS 和 Android 的 Intune 应用包装工具（带 -citrix 标志）。
 
要了解有关 Citrix MDX 的详细信息，请参阅[有关 MDX 工具包](https://docs.citrix.com/en-us/mdx-toolkit/10/about-mdx-toolkit.html)、[适用于 iOS 的 Citrix MDX 应用包装器](https://docs.citrix.com/en-us/mdx-toolkit/10/xmob-mdx-kit-app-wrap-ios.html)和[适用于 Android 的 Citrix MDX 应用包装器](https://docs.citrix.com/en-us/mdx-toolkit/10/xmob-mdx-kit-app-wrap-android.html)。

## <a name="next-steps"></a>后续步骤

- [Microsoft Intune App SDK 入门](app-sdk-get-started.md)。
