---
title: 桌面分析中的新增功能
titleSuffix: Configuration Manager
description: 桌面分析云服务最近每月发布的新功能摘要。
ms.date: 07/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: fa300181-86cb-4afe-8fbf-895a7572378d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: ec554d755b92d1c710def580a34fdbbddc7b4d45
ms.sourcegitcommit: 2c5fd7c8603b88b753765f3cc298d0a0bacaf521
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85819962"
---
# <a name="whats-new-in-desktop-analytics"></a>桌面分析中的新增功能

了解桌面分析的每月新增功能。

> [!TIP]
> 每月更新最多可能需要三天才能推出。 某些功能可能会在数周内推出，第一周内可能不能供所有客户使用。

若要在此页面更新时收到通知，请将以下 URL 复制并粘贴到 RSS 源阅读器中：`https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+desktop+analytics+-+Configuration+Manager%22&locale=en-us`
<!-- a locale is required for the RSS search string -->

## <a name="july-2020"></a>2020 年 7 月

### <a name="windows-10-version-2004-now-available-in-desktop-analytics"></a>Windows 10 版本 2004，现已在桌面分析中提供

<!-- 7370207 -->

在桌面分析门户中，在监视安全和功能更新时，现在可看到 Windows 10 版本 2004。 创建部署计划时，可以选择 Windows 10 版本 2004 作为目标版本。

### <a name="improved-support-for-viewing-the-portal-from-any-device"></a>改进了对从任何设备查看门户的支持

<!-- 6270240 -->

现在可以使用多种设备在 Microsoft Endpoint Manager 管理中心查看桌面分析门户。 现在，它符合 Web 内容辅助功能准则 (WCAG) 2.1，显示分辨率最低可达 320 x 256 像素。 例如，下图是 Apple iPhone 8 中显示的门户：

:::image type="content" source="media/dashboard-iphone8.png" alt-text="iPhone 8 上的桌面分析门户":::

### <a name="notifications-for-service-impacting-events"></a>影响服务的事件的通知

<!-- 4982509 -->

桌面分析门户现在可以显示通知横幅。 通过这些通知，Microsoft 可以向你传达重要事件和问题。 例如，服务的已知问题、数据延迟或新的先决条件。 有关详细信息，请参阅[服务通知](troubleshooting.md#service-notifications)。

## <a name="june-2020"></a>2020 年 6 月

### <a name="improvement-to-prerequisites"></a>对必备组件的改进

桌面分析不再要求在 Azure Active Directory (Azure AD) 租户中部署 Office 365 服务。 Azure AD 中的 Office 365 客户端管理员应用现在为桌面分析应用，用于从服务中启用 Configuration Manager 检索信息和状态 。

## <a name="may-2020"></a>2020 年 5 月

### <a name="reduce-the-number-of-apps-for-review"></a>减少要审阅的应用数量

<!-- 5542186 -->

为了帮助合并和减少门户中“资产”页上显示的应用数量，它现在合并了具有相同名称和发布者的应用的所有版本。 “值得注意的应用”磁贴中的应用计数反映了此设置。 例如，它没有列出数百个 Microsoft Edge 实例，而是列出所有版本的一个实例。 可以对所有版本只做一次决策。 如需对特定应用版本做出决策，此行为是可配置的。

有关详细信息，请参阅[关于资产 - 应用](about-assets.md#apps)。

## <a name="march-2020"></a>2020 年 3 月

### <a name="support-for-multiple-hierarchies"></a>支持多个层次结构

<!-- 4814075, 6079184 -->

你现可使用桌面分析的单个商业 ID 将多个 Configuration Manager 层次结构连接到一个 Azure Active Directory 租户。 该门户对来自不同层次结构的设备进行分类，改进了全局试点和部署计划的体验。

- 配置全局试点时，如果纳入的集合中的注册设备数超过注册设备总数的 20%，则该门户会显示一则警告。
- 创建部署计划时，如果选择对多个层次结构使用集合，该门户也会显示一则警告。

> [!NOTE]
> 必须有 Configuration Manager 版本 1910 或更高版本，才能支持多个层次结构。

有关详细信息，请参阅下列文章：

- [全局试点](deploy-pilot.md#bkmk_GlobalPilot)
- [如何创建部署计划](create-deployment-plans.md)

### <a name="identify-compatibility-safeguards"></a>确定兼容性防护

<!-- 5746559 -->

Windows 兼容性数据通过防护措施对一些应用和驱动程序进行分类，这可能导致 Windows 10 的更新失败或回滚。 而现在，桌面分析可帮助你提前确定这些防护措施，让你能够在部署更新之前对资产进行修正。 有关详细信息，请参阅[兼容性评估 - 防护](compat-assessment.md#safeguards)。

## <a name="january-2020"></a>2020 年 1 月

### <a name="additional-app-usage-detail"></a>其他应用使用情况详细信息

<!-- 5533890 -->

选择应用以查看详细信息时，“详细信息”窗格现在包含其他使用情况信息。 你可以使用此数据来帮助了解应用的安装范围，以及用户经常使用应用的设备。 有关详细信息，请参阅[关于资产 - 应用使用情况](about-assets.md#usage)。

### <a name="provide-feedback-on-desktop-analytics"></a>提供有关桌面分析的反馈

<!-- 5451636 -->

选择门户右上角的“发送笑脸”图标，可分享你对于桌面分析的反馈。 有关详细信息，请参阅[分享产品反馈](get-support.md#bkmk_feedback)。

## <a name="october-2019"></a>2019 年 10 月

### <a name="improvements-to-compatibility-recommendations"></a>兼容性建议的改进

<!-- 3594545 -->

当检测到 Windows 升级将完全或部分删除应用程序或驱动程序时，桌面分析现在会提供更多详细信息。 有关详细信息，请参阅[兼容性评估](compat-assessment.md#asset-is-removed-during-upgrade)。

### <a name="migrate-from-windows-analytics-to-existing-tenant"></a>从 Windows Analytics 迁移到现有租户

<!-- 5202803 -->

你现在可以在加入桌面分析后从现有 Windows Analytics 工作区迁移输入。

## <a name="september-2019"></a>2019 年 9 月

### <a name="migrate-inputs-from-windows-analytics"></a>从 Windows Analytics 迁移输入

<!-- 4252663 -->

在加入期间，你现在可以从现有的 Windows Analytics 工作区迁移输入。

### <a name="offboard-from-desktop-analytics"></a>从桌面分析登出

<!-- 4972396 -->

如果在环境中设置了桌面分析，但想要停止使用该服务，现在可以关闭你的帐户。 如果在 90 天内改变主意，则可以重新激活该帐户。 有关详细信息，请参阅[如何关闭帐户](account-close.md)。

## <a name="august-2019"></a>2019 年 8 月

### <a name="reset-your-account"></a>重置你的帐户

<!-- 3733897 -->

如果你在环境中设置了桌面分析，但想要通过加入和注册来重新开始，现在就可以重置。 有关该过程的详细信息，请参阅[重置帐户](account-reset.md)。

### <a name="automatic-upgrade-decision-of-system-and-store-apps"></a>系统和应用商店应用的自动升级决策

<!-- 3587232 -->

为了帮助减少批注值得注意的应用的工作量，某些类型的应用会被自动标记为“不重要”。 这些应用的部署计划升级决策也会被标记为“就绪”。 以下应用是兼容的，并且应在升级 Windows 后继续工作：

- Microsoft 发布的系统应用和组件

- 从 Microsoft Store 管理和更新的应用

有关详细信息，请参阅[系统和应用商店应用的自动升级决策](about-assets.md#bkmk_plan-autoapp)。

## <a name="whats-new-in-configuration-manager"></a>Configuration Manager 中的新增功能

桌面分析文档始终指的是最新版 Configuration Manager current branch 中的功能。 有关 Configuration Manager 中最新更改的详细信息，请参阅以下文章：

<!-- - [What's new in version 1910](../core/plan-design/changes/whats-new-in-version-1910.md#bkmk_da) -->

- [版本 1906 中的新增功能](../core/plan-design/changes/whats-new-in-version-1906.md#bkmk_da)

## <a name="deprecated-features"></a>已弃用的功能

当 Microsoft 计划删除桌面分析服务的重要功能时，此更改将作为 Configuration Manager 弃用的功能提前进行发布。 有关详细信息，请参阅[已弃用的功能](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md#deprecated-features)。
