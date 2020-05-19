---
title: 管理见解
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 控制台中提供的管理见解功能。
ms.date: 05/07/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a79f83be-884c-48e6-94d6-ed0a68c22e2f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 69b2533dd5c86124a6aff9feac7306ecf16c6e5a
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268957"
---
# <a name="management-insights-in-configuration-manager"></a>Configuration Manager 中的管理见解

适用范围：Configuration Manager (Current Branch)

Configuration Manager 中的管理见解功能提供了环境当前状态的相关信息。 该信息基于对站点数据库中数据的分析。 见解有助于更好地了解环境，并根据见解执行操作。 <!--1353967-->

## <a name="review-management-insights"></a>查看管理见解

若要查看规则，帐户需要站点对象的读取权限 。

1. 请打开 Configuration Manager 控制台。  

2. 转到“管理”工作区，展开“管理见解”，然后选择“所有见解”  。  

    > [!Note]  
    > 选择“管理见解”节点时，它会显示[“管理见解仪表板”](#bkmk_insights)。  

3. 打开要查看的管理见解组名称。 在功能区中选择“显示见解”。  

以下四个选项卡可供查看：

- **所有规则**：提供选定管理见解组的完整规则列表。  

- **已完成**：列出无需执行任何操作的规则。  

- **正在进行**：显示已完成部分（但非全部）先决条件的规则。  

- **需要执行操作**：列出需要执行操作的规则。 选择“更多详细信息”，检索需要执行操作的特定项目。  

“先决条件”窗格列出了运行规则所需的项目。

### <a name="all-rules-and-prerequisites-for-the-cloud-services-group"></a>云服务组的所有规则和先决条件

![管理见解 - 云服务组的所有规则和先决条件](./media/Management-insights-all-cloud-rules.png)

选择规则并选择“更多详细信息”，查看规则详细信息。

## <a name="operations"></a>操作

管理见解规则每周重新评估一次适用性。 若要按需重新评估规则，请右键单击该规则并选择“重新评估”。

管理见解规则的日志文件是站点服务器上的 SMS_DataEngine.log。

<!--1357930-->
某些规则允许执行操作。 选择规则，选择“更多详细信息”，然后选择“执行操作”（如果可用） 。

根据规则，此操作会出现以下某一行为：  

- 在控制台中自动导航到可以采取进一步操作的节点。 例如，如果管理见解建议更改客户端设置，执行操作将导航到“客户端设置”节点。 然后通过修改默认或自定义客户端设置对象采取进一步操作。  

- 基于查询导航到筛选的视图。 例如，对空集合规则执行操作只会在集合列表中显示这些集合。 然后采取进一步操作，例如删除集合或修改其成员身份规则。  

## <a name="management-insights-dashboard"></a><a name="bkmk_insights"></a> 管理见解仪表板

<!--1357979-->

“管理见解”节点包括一个图形仪表板。 此仪表板可概要显示规则状态，让你能够更轻松地显示进度。

使用仪表板顶部的以下筛选器可以细化视图：

- 显示已完成的工作
- 可选
- 建议
- 严重

该仪表板具有以下磁贴：  

- **管理见解索引**：跟踪管理见解规则的总体进度。 该索引为加权平均值。 关键规则最为重要。 此索引为可选规则提供的加权最低。  

- **管理见解组**：显示每个组中的规则百分比，支持筛选器。 选择一个组以深入查看此组中的特定规则。  

- **管理见解优先级**：按优先级显示规则百分比，支持筛选器。  

- **所有见解**：一个包括优先级和状态的见解表。 使用表顶部的“筛选器”字段匹配任何可用列中的字符串。 仪表板按以下顺序对表进行排序：

  - 状态：需要执行操作、已完成、未知  
  - 优先级：重要、建议、可选  
  - 上次更改时间：较早的日期排在前面  

![管理见解仪表板的屏幕截图](media/1357979-management-insights-dashboard.png)

## <a name="groups-and-rules"></a>组和规则

规则分为以下管理见解组：

- [应用程序](#applications)
- [云服务](#cloud-services)
- [集合](#collections)
- [Configuration Manager 评估](#configuration-manager-assessment)
- [主动维护](#proactive-maintenance)
- [安全](#security)
- [简化管理](#simplified-management)
- [软件中心](#software-center)
- [Windows 10](#windows-10)

### <a name="applications"></a>应用程序

应用程序管理见解。

- **不具有部署的应用程序**：列出环境中没有活动部署的应用。 此规则有助于查找并删除未使用的应用程序，以简化显示在控制台中的应用程序列表。 有关详细信息，请参阅[部署应用程序](../../../apps/deploy-use/deploy-applications.md)。  

### <a name="cloud-services"></a>云服务

帮助与多种云服务集成，实现设备的现代化管理。

- **评估共同管理准备情况**：有助于了解启用共同管理所需执行的步骤。 此规则具有先决条件。 有关详细信息，请参阅[共同管理概述](../../../comanage/overview.md)。  

- 未上传到 Azure AD 的设备：从版本 2002 开始，此规则列出因站点未正确配置 HTTPS 而未上传到 Azure AD 的设备。<!--6268489--> 配置[增强型 HTTP](../../plan-design/hierarchy/enhanced-http.md)，或至少为 HTTPS 启用一个管理点。 如果已为 HTTPS 通信配置了站点，则不会出现此规则。

- **配置 Azure 服务以用于 Configuration Manager**：此规则有助于将 Configuration Manager 载入 Azure AD，以便客户端能够使用 Azure AD 向站点进行身份验证。 有关详细信息，请参阅[配置 Azure 服务](../deploy/configure/azure-services-wizard.md)。  

- **将设备启用为加入混合 Azure Active Directory**：使用加入 Azure AD 的设备，用户可使用自己的域凭据登录，同时确保设备符合组织的安全性和符合性标准。 有关详细信息，请参阅 [Azure AD 混合标识设计注意事项](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview)。  

- 没有正确 HTTPS 配置的站点：从版本 2002 开始，此规则列出层次结构中未正确配置 HTTPS 的站点。 此配置可防止站点[将集合成员身份结果同步到 Azure Active Directory (Azure AD) 组](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync)。 这可能导致 Azure AD 同步无法上传所有设备。 可能无法正常管理这些客户端。<!--6268489--> 配置[增强型 HTTP](../../plan-design/hierarchy/enhanced-http.md)，或至少为 HTTPS 启用一个管理点。 如果已为 HTTPS 通信配置了站点，则不会出现此规则。

- **将客户端升级到最新版 Windows 10**：Windows 10 版本 1709 或更高版本改进和新式化用户计算体验。 有关详细信息，请参阅[有关采用服务型 Windows 的关键文章](../../understand/configuration-manager-and-windows-as-service.md#key-articles-about-adopting-windows-as-a-service)。  

### <a name="collections"></a>集合

通过清理和重新配置集合来帮助简化管理的见解。

- **空集合**：列出环境中没有成员的集合。 有关详细信息，请参阅[如何管理集合](../../clients/manage/collections/manage-collections.md)。  

从 1902 版开始，包含对管理集合的新规则和建议。<!--3555752--> 利用这些见解来简化管理并提高性能：

- **不包含查询规则和直接成员的集合**：若要简化层次结构中的集合列表，请将其删除。  

- **重新评估开始时间相同的集合**：这些集合与其他集合的重新评估时间相同。 修改重新评估时间，使它们不冲突。  

- 查询时间超过 5 分钟的集合：查看此集合的查询规则。 请考虑修改或删除该集合。

- 以下规则包括可能导致站点上的不必要负载的配置。 查看这些集合，然后将其删除，或禁用规则评估：  

  - **没有查询规则且已启用增量更新的集合**  

  - 无查询规则且启用任何计划的集合  

  - **没有查询规则且选定计划完整评估的集合**  

### <a name="configuration-manager-assessment"></a>Configuration Manager 评估

<!--3607758-->

从版本 2002 开始，此组由 Microsoft Premier Field Engineering 提供。 这些规则只是 Microsoft Premier 在[服务中心](https://docs.microsoft.com/services-hub/health/getting_started_with_on_demand_assessments)提供的众多检查中的一个例子。

- **Active Directory 安全组发现配置为过于频繁地运行**：通常不需要将 Active Directory 安全组发现配置为以高于每三小时一次的频率运行。 更频繁的配置可能对 Active Directory、网络和 Configuration Manager 的性能造成负面影响。 启用增量同步，而不使用完全同步计划。 有关详细信息，请参阅 [Active Directory 组发现](../deploy/configure/about-discovery-methods.md#bkmk_aboutGroup)。

- **Active Directory 系统发现配置为过于频繁地运行**：通常不需要将 Active Directory 系统发现配置为以高于每三小时一次的频率运行。 更频繁的配置可能对 Active Directory、网络和 Configuration Manager 的性能造成负面影响。 启用增量同步，而不使用完全同步计划。 有关详细信息，请参阅 [Active Directory 系统发现](../deploy/configure/about-discovery-methods.md#bkmk_aboutSystem)。

- **Active Directory 用户发现配置为过于频繁地运行**：通常不需要将 Active Directory 用户发现配置为以高于每三小时一次的频率运行。 更频繁的配置可能对 Active Directory、网络和 Configuration Manager 的性能造成负面影响。 启用增量同步，而不使用完全同步计划。 有关详细信息，请参阅 [Active Directory 用户发现](../deploy/configure/about-discovery-methods.md#bkmk_aboutUser)。

- **集合仅限于“所有系统”或“所有用户”** ：查看使用“所有系统”或“所有用户”集合作为限制集合的任何集合。  Configuration Manager 用来自 Active Directory 发现方法的数据更新这些默认集合的成员身份。 这些数据对 Configuration Manager 客户端而言可能不是有效信息。

- **已禁用检测信号发现**：要使用检测信号发现，需在设备上安装 Configuration Manager 客户端。 这是由客户端启用的唯一发现方法。 所有其他方法都在站点服务器上完成操作。 检测信号发现是保持最新客户端活动状态的基础。 它能确保站点不会意外时站点数据库中的资源记录过时。 有关详细信息，请参阅[检测信号发现](../deploy/configure/about-discovery-methods.md#bkmk_aboutHeartbeat)。

- **已启用长期运行的集合查询以实现增量更新**：上次增量刷新时间超过 30 秒的集合使用站点服务器和数据库资源，可能会影响 Configuration Manager 整体性能。 有关详细信息，请参阅[集合的最佳做法](../../clients/manage/collections/best-practices-for-collections.md)。

- **减少分发点上的应用程序和包数量**：Microsoft 官方支持在每个分发点上承载总计 10,000 个包和应用程序。 超过此总数可能导致操作问题。 有关详细信息，请参阅[大小和扩展数量 - 分发点](../../plan-design/configs/size-and-scale-numbers.md#distribution-point)。

- **辅助站点安装问题**：某些辅助站点的安装状态为“挂起”或“失败”。  这些状态表示你已启动安装，但安装未成功完成。 在辅助站点安装完成之前，客户端可能无法与主站点正常通信。 请检查“监视”工作区并重试安装。 有关详细信息，请参阅[重试失败更新的安装](install-in-console-updates.md#bkmk_retry)。

- **将所有站点更新到同一版本**：在层次结构中使用同一版本的 Configuration Manager。 此配置可保证所有站点都提供相同的功能。 同一层次结构中不同版本的站点会引入互操作性方案。 Configuration Manager 的更高版本包括新功能，并可解决已知问题。 有关详细信息，请参阅[不同版本之间的互操作性](../../plan-design/hierarchy/interoperability-between-different-versions.md)。

有关这些规则的详细信息，请参阅 [Configuration Manager 管理见解修正步骤](https://docs.microsoft.com/services-hub/health/remediation-steps-configmgr)。

> [!TIP]
> 如果你已经是 Microsoft 统一支持或 Microsoft 高级支持的客户，请登录到[服务中心](https://serviceshub.microsoft.com/assessments/)以获取其他按需评估。
>
> 有关 Microsoft 服务的详细信息，请参阅[支持解决方案](https://www.microsoft.com/enterprise/services/support)。

### <a name="proactive-maintenance"></a>主动维护

<!--1352184-->
此组中的规则突出显示潜在的配置问题，以通过定期维护 Configuration Manager 对象避免这些问题。

- **未分配有站点系统的边界组**：未分配有站点系统的边界组只能用于站点分配。 有关详细信息，请参阅[配置边界组](../deploy/configure/boundary-groups.md)。  

- **没有成员的边界组**：没有任何成员的边界组不适用于站点分配或内容查找。 有关详细信息，请参阅[配置边界组](../deploy/configure/boundary-groups.md)。  

- **未向客户端提供内容的分发点**：在过去 30 天内，分发点未向客户端提供内容。 此数据基于来自其客户端的下载历史记录报告。 有关详细信息，请参阅[安装和配置分发点](../deploy/configure/install-and-configure-distribution-points.md)。  

- **启用 WSUS 清理**：验证是否已启用对软件更新点组件的属性运行 WSUS 清理的选项。 此选项有助于提高 WSUS 性能。 有关详细信息，请参阅[软件更新维护](../../../sum/deploy-use/software-updates-maintenance.md)。  

- **未用启动映像**：未引用启动映像来用于 PXE 启动或任务序列。 有关详细信息，请参阅[管理启动映像](../../../osd/get-started/manage-boot-images.md)。  

- **未用配置项目**：配置项目不属于配置基线，且已存在超过 30 天。 有关详细信息，请参阅[创建配置基线](../../../compliance/deploy-use/create-configuration-baselines.md)。  

- **将对等缓存源升级到最新版 Configuration Manager 客户端**：确定用作对等缓存源，但尚未从先前的 1806 客户端版本升级的客户端。 先前的 1806 客户端不能用作运行版本 1806 或更高版本的客户端的对等缓存源。 选择“采取措施”打开显示客户端列表的设备视图。<!--1358008-->  

### <a name="security"></a>安全

提高基础结构和设备安全性的见解。

- **已启用 NTLM 回退**：<!--4572953--> 从版本 1906 开始，此规则检测是否为站点启用了安全级别较低的 NTLM 身份验证回退方法。 当使用客户端推送方法安装 Configuration Manager 客户端时，站点可以要求进行 Kerberos 相互身份验证。 此增强有助于保护服务器与客户端之间的通信。 有关详细信息，请参阅[如何使用客户端请求安装客户端](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush)。

- **不受支持的反恶意软件客户端版本**：超过 10% 的客户端运行的 System Center Endpoint Protection 版本不受支持。 有关详细信息，请参阅 [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md)。  

### <a name="simplified-management"></a>简化管理

有助于简化对环境的日常管理的见解。

- **将站点连接到用于 Configuration Manager 更新的 Microsoft 云**：此规则可确保 Configuration Manager 服务连接点在过去七天内已连接到 Microsoft 云。 此连接用于下载定期更新内容。 查看 DMPDownloader.log 和 hman.log。 有关详细信息，请参阅 [Internet 访问要求](../../plan-design/network/internet-endpoints.md#bkmk_scp-updates)。

- **非 CB 客户端版本**：列出版本不是 Current Branch (CB) 内部版本的所有客户端。 有关详细信息，请参阅[升级客户端](../../clients/manage/upgrade/upgrade-clients.md)。  

- **将客户端更新到支持的 Windows 10 版本**：从 1902 版开始，此规则报告运行不再受支持的 Windows 10 版本的客户端。 它还包括具有服务即将结束（三个月）的 Windows 10 版本的客户端。<!--3897268-->  

### <a name="software-center"></a>软件中心

关于管理软件中心的见解。

- **将用户定向到软件中心，而不是应用目录**：检查用户是否在过去 14 天内从应用目录安装或请求获取应用。 应用程序目录的主要功能现在包含在软件中心内。 版本 1910 已终止对应用程序目录角色的支持。 有关详细信息，请参阅[已弃用的功能](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md#deprecated-features)。  

- **使用新版软件中心**：不再支持以前版本的软件中心。 通过在“计算机代理”组中启用客户端设置“使用新的软件中心”，将客户端设置为使用新的软件中心 。 有关详细信息，请参阅[关于客户端设置](../../clients/deploy/about-client-settings.md#use-new-software-center)。  

### <a name="software-updates"></a>软件更新

- **客户端设置未配置为允许客户端下载增量内容**：在环境中同步的某些软件更新包括增量内容。 启用客户端设置“在有可用内容时，允许客户端下载增量内容”。 如果不启用此设置，则在部署这些更新，客户端将不必要地下载超出要求的内容。 有关详细信息，请参阅[客户端设置 - 软件更新](../../clients/deploy/about-client-settings.md#software-updates)。

- **启用“Windows 10 版本 1903 及更高版本”的软件更新产品类别**：Windows 10 版本 1903 及更高版本有一个新的软件更新产品类别。 如果同步 Windows 10 更新且装有 Windows 10 版本 1903 或更高版本的客户端，请在软件更新点组件属性中选择“Windows 10 版本 1903 及更高版本”产品类别。 有关详细信息，请参阅[配置要同步的分类和产品](../../../sum/get-started/configure-classifications-and-products.md)。

### <a name="windows-10"></a>Windows 10

与 Windows 10 的部署和服务相关的见解。 当超过一半的客户端运行 Windows 7、Windows 8 或 Windows 8.1 时，才可以使用 Windows 10 管理见解组。

- **配置 Windows 诊断和商业 ID 键**：若要使用桌面分析中的数据，请使用商业 ID 键配置设备并启用诊断数据收集。 将 Windows 10 设备设置为“增强型(有限)”或更高级别。 有关详细信息，请参阅[为桌面分析启用数据共享](../../../desktop-analytics/enable-data-sharing.md)。

#### <a name="windows-10-management-insights-rules"></a>Windows 10 管理见解规则

![管理见解 - 适用于 Windows 10 的规则](./media/Windows-10-insights-group.png)
