---
title: 通过 Intune 管理适用于 iOS 和 Android 的 Office
titleSuffix: ''
description: 对适用于 iOS 和 Android 的 Microsoft Office 使用 Intune 应用保护和配置策略，确保访问协作体验时，安全措施始终到位。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/31/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: smithre4
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ba4bef364f734f9078b7c404e06978b018f4c387
ms.sourcegitcommit: ded11a8b999450f4939dcfc3d1c1adbc35c42168
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/01/2020
ms.locfileid: "89281075"
---
# <a name="manage-collaboration-experiences-using-office-for-ios-and-android-with-microsoft-intune"></a>通过 Microsoft Intune 使用适用于 iOS 和 Android 的 Office 管理协作体验

适用于 iOS 和 Android 的 Office 提供了几个主要优势，包括：

- 将 Word、Excel 和 PowerPoint 结合起来，可减少下载或切换应用的次数，简化了体验。 它需要的手机存储空间远远少于安装单个应用，同时保持已知和使用的现有移动应用的几乎所有功能。
- 集成 Office Lens 技术来解锁相机的强大功能，例如将图像转换为可编辑的 Word 和 Excel 文档，扫描 PDF 文件，以及通过自动数字增强功能捕获白板，使内容更容易阅读。
- 为人们在使用手机工作时经常遇到的常见任务添加新功能，例如快速笔记、签署 PDF 文件、扫描 QR 码以及在设备之间传输文件。

订阅企业移动性 + 安全性套件（包括 Microsoft Intune 和 Azure Active Directory Premium 功能，如条件访问）可获得最丰富和最广泛的 Microsoft 365 数据保护功能。 最基础的层面来说，你需要部署一个条件访问策略，该策略允许从移动设备连接到适用于 iOS 和 Android 的 Office，还需要部署 Intune 应用保护策略确保协作体验受到保护。

## <a name="apply-conditional-access"></a>应用条件访问
组织可以使用 Azure AD 条件访问策略来确保用户只能使用适用于 iOS 和 Android 的 Office 访问工作或学校内容。 为此，你需要一个面向所有潜在用户的条件访问策略。 有关创建此策略的详细信息，请参阅[通过条件访问要求访问云应用时具有应用保护策略](/azure/active-directory/conditional-access/app-protection-based-conditional-access)。

1. 请遵循“步骤 1：为 Office 365 配置 Azure AD 条件访问策略”（[方案 1：Office 365 应用要求批准的应用具有应用保护策略](/azure/active-directory/conditional-access/app-protection-based-conditional-access#scenario-1-office-365-apps-require-approved-apps-with-app-protection-policies)），这允许使用适用于 iOS 和 Android 的 Office，但阻止支持 OAuth 的第三方移动设备客户端连接到 Office 365 终结点。

   >[!NOTE]
   > 此策略可确保移动用户可以使用适用的应用访问所有 Office 终结点。

## <a name="create-intune-app-protection-policies"></a>创建 Intune 应用保护策略

应用保护策略 (APP) 定义允许的应用以及这些应用可对组织的数据执行的操作。 APP 中可用的选项使组织能够根据特定需求调整保护。 对于某些组织而言，实现完整方案所需的策略设置可能并不明显。 为了帮助组织确定移动客户端终结点强化的优先级，Microsoft 为其面向 iOS 和 Android 移动应用管理的 APP 数据保护框架引入了分类法。

APP 数据保护框架分为三个不同的配置级别，每个级别基于上一个级别进行构建：

- 企业基本数据保护（级别 1）可确保应用受 PIN 保护和经过加密处理，并执行选择性擦除操作。 对于 Android 设备，此级别验证 Android 设备证明。 这是一个入门级配置，可在 Exchange Online 邮箱策略中提供类似的数据保护控制，并将 IT 和用户群引入 APP。
- 企业增强型数据保护（级别 2）引入了 APP 数据泄露预防机制和最低 OS 要求。 此配置适用于访问工作或学校数据的大多数移动用户。
- 企业高级数据保护（级别 3）引入了高级数据保护机制、增强的PIN 配置和 APP 移动威胁防御。 此配置适用于访问高风险数据的用户。

若要查看每个配置级别的具体建议以及必须受保护的核心应用，请查看[使用应用保护策略的数据保护框架](app-protection-framework.md)。

无论设备是否已注册统一终结点管理 (UEM) 解决方案，都需要使用[如何创建和分配应用保护策略](app-protection-policies.md)中的步骤来为 iOS 和 Android 应用创建 Intune 应用保护策略。 这些策略必须至少满足以下条件：

1. 包括所有 Microsoft 365 移动应用程序（如 Edge、Outlook、OneDrive、Office 或 Teams），因为这样可以确保用户在任何 Microsoft 应用中均能够以安全的方式访问和处理工作或学校数据。

2. 它们将分配给所有用户。 这可确保所有用户都受到保护，不管他们使用的是适用于 iOS 还是 Android 的 Office。

3. 确定哪一个框架级别满足你的要求。 大多数组织应实现企业增强型数据保护（级别 2）中定义的设置，因为这样可以启用数据保护和访问要求控制。

有关可用设置的详细信息，请参阅 [Android 应用保护策略设置](app-protection-policy-settings-android.md) 和 [iOS 应用保护策略设置](app-protection-policy-settings-ios.md)。

> [!IMPORTANT]
> 若要针对未在 Intune 中注册的 Android 设备上的应用应用 Intune 应用保护策略，用户还必须安装 Intune 公司门户。 有关详细信息，请参阅 [Android 应用由应用保护策略托管时会出现的情况](../fundamentals/end-user-mam-apps-android.md)。

## <a name="utilize-app-configuration"></a>利用应用配置

适用于 iOS 和 Android 的 Office 支持允许统一终结点管理（例如允许 Microsoft Endpoint Manager 和管理员自定义应用的行为）的应用设置。

可以通过已注册设备上的移动设备管理 (MDM) OS 通道（iOS 上为 [Managed App Configuration](https://developer.apple.com/library/content/samplecode/sc2279/Introduction/Intro.html) 通道，Android 上为 [Android in the Enterprise](https://developer.android.com/work/managed-configurations) 通道）来交付应用配置，也可以通过 Intune 应用保护策略 (APP) 通道来交付应用配置。 适用于 iOS 和 Android 的 Office 支持以下配置方案：

- 仅允许工作或学校帐户
- 常规应用配置
- 数据保护设置

> [!IMPORTANT]
> 对于需要在 Android 上进行设备注册的配置方案，必须在 Android Enterprise 中注册设备，并且必须通过托管的 Google Play 商店部署适用于 Android 的 Office。 有关详细信息，请参阅 [设置 Android Enterprise 工作配置文件设备的注册](../enrollment/android-work-profile-enroll.md)和[为托管的 Android Enterprise 设备添加应用配置策略](app-configuration-policies-use-android.md)。

每个配置方案都强调了其特定要求。 例如，配置方案是否需要进行设备注册以便能够用于任何 UEM 提供程序，或者是否需要 Intune 应用保护策略。

> [!NOTE]
> 使用 Microsoft Endpoint Manager 的情况下，通过 MDM OS 通道交付的应用配置称为托管设备应用配置策略 (ACP)；通过应用保护策略通道交付的应用配置称为托管应用应用配置策略 。

## <a name="only-allow-work-or-school-accounts"></a>仅允许工作或学校帐户

体现 Microsoft 365 价值的关键是遵从最大范围和高度管控客户的数据安全和合规性策略。 一些公司要求捕获其公司环境内的所有通信信息，并确保设备仅用于公司通信。 为了支持这些要求，可以将已注册设备上适用于 Android 的 Office 配置为仅允许在该应用中预配一个公司帐户。

下面的资源详细介绍了如何配置组织允许的帐户模式设置：

- [Android 设置](app-configuration-policies-use-android.md#allow-only-configured-organization-accounts-in-multi-identity-apps)

此配置方案仅适用于已注册的设备。 但是，它支持所有 UEM 提供程序。 如果未使用 Microsoft Endpoint Manager，则需要参阅 UEM 文档，了解如何部署这些配置项。

> [!NOTE]
> 目前，只有适用于 Android 的 Office 支持组织允许的帐户模式。

## <a name="general-app-configuration-scenarios"></a>常规应用配置方案

适用于 iOS 和 Android 的 Office 使管理员能够为多个应用内设置自定义默认配置。  如果适用于 iOS 和 Android 的 Office 应用了 Intune 应用保护策略，则无论是通过任意 UEM 提供程序注册的设备还是未注册的设备，均可使用此功能。

> [!NOTE]
> 如果应用保护策略以用户为目标，则建议在“托管应用”注册模型中部署常规应用配置设置。 这样可以确保将应用配置策略同时部署到已注册的设备和未注册的设备。 

Office 支持以下配置设置：

- 管理便笺的创建

### <a name="manage-the-creation-of-sticky-notes"></a>管理便笺的创建

默认情况下，适用于 iOS 和 Android 的 Office 允许用户创建便笺。 对于具有 Exchange Online 邮箱的用户，便笺将同步到用户的邮箱中。 对于具有本地邮箱的用户，这些便笺仅存储在本地设备上。

|    密钥    |    值    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.office.NotesCreationEnabled    |    “true”（默认值）允许为工作或学校帐户创建便笺<br>“false”禁止为工作或学校帐户创建便笺    |


## <a name="data-protection-app-configuration-scenarios"></a>数据保护应用配置方案

当 Microsoft Endpoint Manager 管理适用于 iOS 和 Android 的 Office，且 Intune 应用保护策略已应用于已登录该应用的工作或学校帐户时，适用于 iOS 和 Android 的 Microsoft Edge 支持针对以下数据保护设置的应用配置策略：

- 通过“传输文件”操作管理文件传输
- 通过“共享附近”操作管理文件传输

无论设备注册状态如何，都可以将这些设置部署到应用。

### <a name="manage-file-transfers"></a>管理文件传输

默认情况下，借助适用于 iOS 和 Android 的 Office，用户可以使用各种机制来共享内容：

- 如果文件托管在 OneDrive 或 SharePoint 中，用户可以直接在文件中发起共享请求。
- 用户可以使用“传输文件”操作将文件传输到桌面系统。
- 用户可以使用“共享到附近”操作将文件共享到附近的移动设备。

“传输文件”和“共享到附近”操作只适用于媒体、本地文件和不受应用保护策略保护的文件。 

|    Key    |    值    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.office.ShareNearby.IsAllowed.IntuneMAMOnly    |    “true”（默认）：为工作或学校帐户启用“附近共享”功能<br>“false”：为工作或学校帐户禁用“附近共享”功能    |
|    com.microsoft.office.TransferFiles.IsAllowed.IntuneMAMOnly    |    “true”（默认）：为工作或学校帐户启用“文件传输”功能<br>“false”：为工作或学校帐户禁用“文件传输”功能    |

### <a name="deploy-app-configuration-scenarios-with-microsoft-endpoint-manager"></a>使用 Microsoft Endpoint Manager 部署应用配置方案

如果要将 Microsoft Endpoint Manager 用作移动应用管理提供程序，请参阅[为受管理应用添加应用配置策略（无需设备注册）](app-configuration-policies-managed-app.md)，了解如何为数据保护应用配置方案创建受管理应用配置策略。 创建配置后，可以向用户组分配策略。

## <a name="next-steps"></a>后续步骤

- [什么是应用保护策略？](app-protection-policy.md) 
- [Microsoft Intune 的应用配置策略](app-configuration-policies-overview.md)