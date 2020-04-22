---
title: 产品和许可常见问题解答
titleSuffix: Configuration Manager
description: 查找 Configuration Manager 产品和许可常见问题的答案。
ms.date: 02/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ee8d611f-aa0c-4efd-b0ad-dbd14d0a0623
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 63e53c502e67d2bfbfc5f8a706006c6ec14f8fcd
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706835"
---
# <a name="frequently-asked-questions-for-configuration-manager-branches-and-licensing"></a>Configuration Manager 分支和许可的常见问题解答

适用范围：  Configuration Manager (Current Branch) 和 System Center Configuration Manager (Long-Term Servicing Branch)

此常见问题解答涉及通过 Microsoft 批量许可计划提供的 Configuration Manager Current Branch 和 Long-Term Servicing Branch (LTSB) 版本的常见许可问题。 本文仅供参考。 它不会取代或替换任何涉及 Configuration Manager 许可的文档。 有关详细信息，请参阅[产品术语](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=53)。 产品术语描述批量许可中所有 Microsoft 产品的使用条款。

### <a name="whats-current-branch"></a><a name="bkmk_cb"></a>什么是 Current Branch？

Current Branch 是提供活动服务模型的 Configuration Manager 的生产就绪版本。 这种服务模型类似于使用 Windows 10 的体验。 此方法支持以云节奏迁移并希望加快创新速度的客户。 通过 Current Branch 服务模型，可继续接收新功能。 因此，只有具有 Configuration Manager 许可证上的可用软件保障或等效订阅权限的客户才能安装和使用 Configuration Manager 的 Current Branch。

### <a name="whats-the-long-term-servicing-branch-ltsb"></a><a name="bkmk_ltsb"></a>什么是 Long Term Servicing Branch (LTSB)？  

LTSB 是 Configuration Manager 的生产就绪版本。 它适用于允许软件保障或等效订阅权限过期的客户。 与 Current Branch 相比，LTSB 的[功能缩减](introduction-to-the-ltsb.md#features-that-arent-available)。 允许软件保障或等效订阅权限过期的客户必须卸载 Configuration Manager 的 Current Branch。 如果客户对 Configuration Manager 具有永久许可权限，则可在过期时安装并使用 Configuration Manager 最新版的 LTSB 版本。

### <a name="what-do-the-acronyms-sa-and-lsa-mean-in-regard-to-configuration-manager"></a><a name="bkmk_licensing-acronyms"></a> 首字母缩写词 SA 和 L&SA 在 Configuration Manager 中的含义是什么   ？

软件保障  (SA) 和许可证和软件保障  (L&SA) 是授权使用 Configuration Manager 的许可选项。 SA 选项适用于从之前的协议续订 SA 范围的客户。 L&SA 选项适用于购买新的许可证和 SA 范围的客户。

- **软件保障 (SA)** ：客户必须在 Configuration Manager 许可证上具有可用 SA 或具有等效的订阅权限，才可安装和使用 Configuration Manager 的 Current Branch。

  虽然对于某些 Microsoft 产品来说 SA 是可选选项，但获取使用 Configuration Manager Current Branch 的权限的唯一方法是使用 SA 或等效订阅权限  。 有关详细信息，请参阅[软件保障常见问题解答](https://www.microsoft.com/licensing/licensing-programs/FAQ-Software-Assurance.aspx)。

- **Microsoft 许可证和软件保障 (L&SA)** ：购买新的 Configuration Manager 许可证的客户必须获取 L&SA（许可证和 SA 范围）。

  - SA 授予使用 Current Branch 的权限。

  - 如果 SA 过期，你仍拥有 Configuration Manager 的许可证，但无法再使用 Current Branch。 有关详细信息，请参阅[如果 SA 过期且拥有 L&SA，我可使用的功能是什么？](#bkmk_sa-expires)

有关许可证产品/服务的详细信息，请参阅[购买方式](https://www.microsoft.com/Licensing/licensing-programs/licensing-programs)和[许可产品条款](https://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=64)。  

### <a name="what-are-equivalent-subscriptions"></a><a name="bkmk_equiv-sub"></a> 什么是等效订阅  ？

等效订阅指[企业移动性 + 安全性](https://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=51) (EMS) 或 [Microsoft 365 企业版](https://www.microsoft.com/microsoft-365/enterprise)等计划。 可能还涉及其他计划，但以上计划是最常见的。 Microsoft 批量许可产品条款将这些计划称为“管理许可证的等效许可证”。

以下计划包含 Configuration Manager：

- Intune 用户订阅许可证 (USL)
- EMS E3
- EMS E5
- Microsoft 365 E3
- Microsoft 365 E5
- Microsoft 365 F1

<!-- Sources:
https://www.microsoft.com/microsoft-365/compare-all-microsoft-365-plans
https://www.microsoft.com/microsoft-365/enterprise-mobility-security/compare-plans-and-pricing
-->

> [!IMPORTANT]
> [Microsoft 365 商业版](https://www.microsoft.com/microsoft-365/business)计划不包含 Configuration Manager。

### <a name="does-anything-change-with-the-rebrand-to-microsoft-endpoint-manager"></a><a name="bkmk_mem"></a> 重新绑定到 Microsoft Endpoint Manager 后有什么变化吗？

是。 2019 年 12 月 1 日开始，如果你已获得 Configuration Manager 的许可，则还会自动获得 Intune 的许可，可以在[共同管理](../../comanage/overview.md)中注册 Windows 电脑。 此更改使你可更轻松地使用 Microsoft Endpoint Manager 管理 Windows 设备。

现已推出新的许可证，它允许具有软件保障的 Configuration Manager 客户获得 Intune 电脑管理权限，而无需购买额外的 Intune 许可证进行共同管理。 不再需要购买个人 Intune 许可证，并将它们分配给用户。

- 由 Configuration Manager 管理并加入共同管理的设备与 Intune 独立管理的电脑几乎具有相同的权限。 但是，在重置后，不能使用 AutopIlot 对其进行重新设置。

- 使用其他方式注册到 Intune 的 Windows 10 设备需要完整的 Intune 许可证。

- 如果要使用 Intune 管理 iOS、Android 或 macOS 设备，则需要通过独立 Intune 许可证、Microsoft 企业移动性 + 安全性 (EMS) 或 Microsoft 365 进行相应的 Intune 订阅。

- 以前对 System Center Configuration Manager 的许可仍然适用于 Microsoft Endpoint Configuration Manager。 如果安装新站点，请使用现有产品密钥。

### <a name="i-have-enterprise-mobility--security-and-it-expired-what-must-i-do-now"></a><a name="bkmk_ems-expires"></a>我拥有企业移动性 + 安全性，但已过期，现在必须执行什么操作？  

EMS 授予使用 Configuration Manager Current Branch 和 Long-Term Service Branch 的权限。 这些权限过期时，你不再有权使用任一分支且必须卸载。  

### <a name="if-my-sa-expires-and-i-had-lsa-what-do-i-get"></a><a name="bkmk_sa-expires"></a>如果 SA 过期且拥有 L&SA，我可使用的功能是什么？

如果 SA 在 2016 年 10 月 1 日后过期，可保留使用 LTSB 的永久许可证，具体取决于你是从什么计划下获取 L&SA。 如果当前使用 Current Branch，必须将其卸载，然后安装 LTSB。 不支持从 Current Branch 迁移到或转换为 LTSB。

如果 SA 在 2016 年 10 月 1 日前过期并保留了 Configuration Manager 的永久许可证，则继续使用的唯一选择是安装和使用 System Center 2012 R2 Configuration Manager 及其可用的服务包。 SA 过期时需要卸载 Current Branch，并重新安装该产品的早期版本。 不支持从 Configuration Manager Current Branch 迁移到或降级为 Configuration Manager 的早期版本。

如果使用 System Center Endpoint Protection，且 SA 已过期，则必须将其卸载。 System Center Endpoint Protection 不提供  L（许可证）权限，也不提供永久权限。<!--506238-->

### <a name="do-i-own-the-current-branch"></a><a name="bkmk_owncb"></a>我是否“拥有”Current Branch？

不能。 当你具有可用 SA 时，有权使用 Current Branch。 例如，通过 L&SA  ，当 SA  过期时，你仅具有 L（许可证）  权限，这不包括使用 Current Branch 的权限。 如果 L 提供永久权限，可以使用 Configuration Manager LTSB 代替 Current Branch。 如果 SA 在 2016 年 10 月 1 日之前过期，还可以使用 System Center 2012 R2 Configuration Manager。

### <a name="can-i-purchase-configuration-manager-standalone-without-sa"></a><a name="bkmk_standalone"></a>是否可以单独购买 Configuration Manager，而不购买 SA？

不能。 获取使用 Configuration Manager 权限的唯一方法是获取具有 SA 的许可证或通过等效订阅获取许可证。 开发人员计划（如 MSDN）中提供的 Configuration Manager 用于开发和测试目的，但不用作生产用途。

### <a name="does-a-non-production-environment-for-testing-or-development-require-an-explicit-license"></a><a name="bkmk_lab"></a> 用于测试或开发的非生产环境是否需要明确的许可？

<!-- SCCMDocs#1848 -->

- 如果使用与生产环境相同的当前分支软件，则需要明确的许可。 请咨询你的帐户团队，确定你的特定许可协议是否包含多个环境中的多个实例。

- 某些开发人员计划（如 MSDN）提供了 Configuration Manager 等产品，以用于开发和测试，但不用作生产用途。

- 对于临时环境，可以使用[评估版](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection) 180 天。

- 对于实验室环境，可以使用[技术预览分支](../get-started/technical-preview.md)。 技术预览与当前分支具有相同功能，但在缩放和受支持的平台方面存在一些限制。

### <a name="do-i-have-rights-to-install-any-update-in-the-configuration-manager-console"></a><a name="bkmk_update-rights"></a> 我是否有权在 Configuration Manager 控制台中安装任何更新？

如果你拥有可用 SA  ，则有权安装它。

如果没有可用 SA，卸载 Current Branch，然后安装 Configuration Manager 的 LTSB。 LTSB 不会接收 Configuration Manager 增量版本的更新，但会接收基于支持生命周期的安全更新。

### <a name="i-have-purchased-ems-or-microsoft-365-through-a-cloud-solution-provider-csp-do-i-have-rights-to-use-configuration-manager"></a><a name="bkmk_csp"></a>我通过云解决方案提供商 (CSP) 购买了 EMS 或 Microsoft 365，是否有权使用 Configuration Manager？

是，你有权使用 Configuration Manager 来管理 EMS 许可证所涵盖的客户端。 首先下载并安装[测试版软件](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection)。 然后联系 Microsoft 支持部门获取许可证密钥。<!--issue472--> 当你与 Microsoft 支持部门交流时，要求他们引用内部文章 ID 4033838。<!-- SCCMDocs issue 493 -->

### <a name="is-my-subscription-end-date-the-same-as-an-sa-expiration-date"></a><a name="bkmk_expiration-date"></a>订阅结束日期是否与 SA 过期日期相同？

如果 SA  或订阅处于可用状态，则有权使用 Configuration Manager Current Branch。 可用订阅等效于具有可用 SA，但没有永久“L”（许可证）   。 订阅结束后，卸载 Current Branch。 此时，你无权使用 LTSB。  

### <a name="what-are-the-use-rights-associated-with-the-sql-technology-provided-with-configuration-manager"></a><a name="bkmk_sql"></a>随 Configuration Manager 一起提供的 SQL 技术关联的使用权限有哪些？

Configuration Manager 包括 SQL Server 技术。 针对这些产品的 Microsoft 许可条款允许仅使用 SQL Server 技术来支持 Configuration Manager 组件。 不需要使用 SQL Server 客户端访问许可证。

Configuration Manager 附带的 SQL 功能的批准使用权限包括：

- 站点数据库角色
- 软件更新点的 Windows Server Update Services (WSUS) 角色
- 报表点的 SQL Server Reporting Services (SSRS) 角色
- 数据仓库服务点角色
- 管理点的数据库副本角色

Configuration Manager 附带的 SQL Server 许可证支持你安装的每个 SQL Server 实例以托管 Configuration Manager 的数据库。 但是，在使用此许可证时，只有上述列表中的 Configuration Manager 的数据库可以在该 SQL Server 上运行。 如果任何其他 Microsoft 或第三方产品的数据库共享 SQL Server，则必须拥有该 SQL Server 实例的单独许可证。
 <!-- sms500967 -->

### <a name="does-on-premises-mobile-device-management-mdm-require-an-intune-subscription"></a><a name="bkmk_opmdm"></a>本地移动设备管理 (MDM) 是否需要 Intune 订阅？

在版本 1806 和更早版本中，若要使用本地 MDM，需要 Microsoft Intune 订阅。 仅跟踪设备授权时需要订阅，订阅不用于管理或储存设备的管理信息。 所有管理数据均使用本地 Configuration Manager 基础结构存储在组织中。  

从版本 1810 开始，新的本地 MDM 部署不再需要 Intune 连接。<!--3607730, fka 1359124--> 组织仍需要 Intune 许可证才能使用此功能。 有关详细信息，请参阅 [Intune 支持博客文章](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150)。
