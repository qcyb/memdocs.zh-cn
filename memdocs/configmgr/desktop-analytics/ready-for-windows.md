---
title: Ready for Windows
titleSuffix: Configuration Manager
description: 关于 Ready for Windows 网站的停用
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 3f09226c-4ca7-4e43-9ae8-5ee6e78e6bc2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ROBOTS: NOINDEX
ms.openlocfilehash: 18e703691696a2cfc02a5b9715fb6062360229e2
ms.sourcegitcommit: 22e1095a41213372c52d85c58b18cbabaf2300ac
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2020
ms.locfileid: "85353456"
---
# <a name="ready-for-modern-desktop-retirement-faq"></a>Ready for modern desktop 停用常见问题

<!-- placeholder -->

## <a name="ready-for-windows-adoption-status"></a>Ready for Windows 采用状态

“采用状态”依据为，来自与 Microsoft 共享数据的商业设备的信息。 状态与软件供应商提供的支持声明集成。

桌面分析为在商业设备中找到的每个版本的资产提供采用状态。 此状态不包括使用者设备或不共享数据的设备中的数据。 此状态可能不代表所有 Windows 10 设备的采用率。

可能的类别包括：

- **已广泛采用**：至少有 100,000 个商用 Windows 10 设备已安装此应用。

- **已采用**：至少有 10,000 个商用 Windows 10 设备已安装此应用。

- **数据不足**：很少有商用 Windows 10 设备共享此应用的信息，Microsoft 无法对其采用情况进行分类。

- **联系开发人员**：此版本的应用可能存在兼容性问题。 Microsoft 建议联系软件提供商以了解详细信息。

- **未知**：没有针对此应用程序的这一版本的可用信息。 可能有针对此应用程序的其他版本的可用信息。

## <a name="general"></a>常规

### <a name="what-happened-to-the-ready-for-windows-website"></a>Ready for Windows 网站发生了什么情况？

许多客户在获取 Windows 10 和 Office 365 ProPlus 并保持最新状态方面面临着挑战。 主要的挑战是测试应用程序，因为此过程通常需要手动完成。 IT 管理员和应用程序所有者要不断分析现有应用程序并解决出现的任何问题，这需要花费很长时间。

“Ready for modern desktop”目录列出了在运行 Windows 10 和 Office 365 ProPlus 的商业设备上受支持且已在使用的软件解决方案。 该目录可帮助 IT 经理考虑最新版本的 Windows 10 和 Office 365 的部署。

IT 经理提供的反馈是，他们希望这些见解与他们已经用来进行部署计划的工具集成在一起。 在 Configuration Manager 中使用[桌面分析](https://aka.ms/dadocs)和 [Office 365 ProPlus 就绪功能](https://docs.microsoft.com/deployoffice/readiness-tools#office-365-proplus-readiness-features-in-configuration-manager-current-branch)来计划和管理 Windows 10 和 Office 365 ProPlus 升级项目。 

> [!Note]
> 自 2020 年 4 月 21 日起，Office 365 专业增强版已重命名为 Microsoft 365 企业应用版。 有关详细信息，请参阅 [Office 365 专业增强版的名称变更](https://docs.microsoft.com/deployoffice/name-change)。 在控制台更新期间，你可能仍会看到 Configuration Manager 控制台和支持文档中引用的是旧名称。

### <a name="what-is-desktop-analytics"></a>什么是桌面分析？

[桌面分析](https://aka.ms/dadocs)是一项基于云的服务，可与 Configuration Manager 集成。 该服务为你提供见解和情报，让你在了解更多信息的情况下决定 Windows 客户端终结点的更新是否就绪。 它将特定于组织的数据与连接到 Microsoft 的云服务的数百万个 Windows 设备的聚合见解合并在一起。

-    全面了解组织中管理的终结点、应用程序和驱动程序。

-    评估应用程序和驱动程序与最新 Windows 功能更新的兼容性。 接收针对已知问题的缓解建议，以及针对业务线应用程序的高级见解。

-    使用 Microsoft 云中的人工智能 (AI) 优化充分代表你整个环境的试点设备集。

### <a name="why-should-i-use-desktop-analytics-for-my-windows-deployment-plans"></a>为什么应将桌面分析用于我的 Windows 部署计划？

桌面分析提供以下好处：

-    **设备和软件清单**：关键因素（如应用和 Windows 版本）清单。

-    **试点识别**：识别覆盖最广泛因素的最小设备集。 它侧重于对 Windows 升级和更新的试点最为重要的因素。 确保试点更成功可以让你继续更快、更自信地在生产环境中广泛部署。

-    **问题识别**：使用聚合的市场数据以及环境中的数据，该服务可预测获取并保持 Windows 最新状态的潜在问题。 然后，它会建议可能的缓解措施。

-    **Configuration Manager 集成**：它在云中启用现有本地基础结构。 使用此数据和分析在设备上部署和管理 Windows。

### <a name="what-does-the-ready-for-windows-status-mean-in-desktop-analytics"></a>在桌面分析中“Ready for Windows”状态指的是什么？

“采用状态”基于与 Microsoft 共享数据的商业设备的信息。 状态与软件供应商提供的支持声明集成。

桌面分析为在商业设备中找到的每个版本的资产提供采用状态。 此状态不包括使用者设备或不共享数据的设备中的数据。 此状态可能不代表所有 Windows 10 设备的采用率。

有关详细信息，请参阅[兼容性评估](compat-assessment.md)。

### <a name="what-assets-get-the-ready-for-windows-status-in-desktop-analytics"></a>哪些资产在桌面分析中获得“Ready for Windows”状态？ 

在以下情况下，资产会在桌面分析中显示“Ready for Windows”状态：

-    软件提供商声明支持解决方案。
-    客户将其部署在与 Microsoft 共享信息的大量商业 Windows 10 设备上。
-    资产与商业用户相关。

### <a name="what-additional-insights-do-i-get-in-desktop-analytics"></a>我会在桌面分析中获得哪些其他见解？

桌面分析提供[设备及其已安装应用](about-assets.md)的清单，以及关于业务线应用的[高级见解](compat-assessment.md#advanced-insights)。 

## <a name="software-providers"></a>软件提供商

### <a name="can-i-still-list-my-software-solution-in-desktop-analytics"></a>我是否仍然可以在桌面分析中列出我的软件解决方案？

发布你的产品适用于 32 位或 64 位 Windows 10 或 Office 365 ProPlus 的支持声明。 若要在桌面分析中展示你的解决方案，请联系你的 Microsoft 联系人。

### <a name="how-can-listing-my-solutions-benefit-me"></a>列出我的解决方案可给我带来哪些好处？

有成千上万的 IT 管理员通过 Configuration Manager 和桌面分析管理数百万台设备。 他们使用这些工具自信地计划并将其组织升级到最新版本的 Windows 10 和 Office 365 ProPlus。 他们还使用它们来制定软件解决方案的购买决策。

Microsoft 将软件供应商提供的支持声明与它们从商业设备接收的采用情况信息集成在一起。 然后，世界各地的组织可在桌面分析和 Office 准备工具中使用此数据。 

如果你的支持声明未与资产正确关联，请咨询你的 Microsoft 联系人。

### <a name="can-i-see-detailed-performance-metrics-on-my-assets"></a>能否在资产上查看详细的性能指标？

通过开发人员中心使用运行状况和指标报表评估解决方案的性能： 

- [Windows 应用商店](https://docs.microsoft.com/windows/uwp/publish/health-report)
- [桌面](https://docs.microsoft.com/windows/desktop/appxpkg/windows-desktop-application-program)
- [Office 外接程序](https://docs.microsoft.com/office/dev/store/update-unpublish-and-view-metrics) 

### <a name="how-can-i-develop-compatible-assets-for-windows-10-and-office-365-proplus"></a>如何为 Windows 10 和 Office 365 ProPlus 开发兼容的资产？

确保你的桌面应用程序现在与 Windows 10 兼容，并在将来保持与 Windows 10 兼容。 有关详细信息，请参阅[面向开发人员的应用程序兼容性](https://developer.microsoft.com/windows/desktop/app-compatibility)。

如果为 Office 365 ProPlus 开发解决方案，请参阅 [Office 中的 COM、VSTO 和 VBA 外接程序开发最佳做法](https://docs.microsoft.com/visualstudio/vsto/development-best-practices-for-com-vsto-and-vba-add-ins-in-office)。
