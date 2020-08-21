---
title: 管理见解
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 控制台中提供的管理见解功能。
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a79f83be-884c-48e6-94d6-ed0a68c22e2f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: de3c75982e19e6183260a2a5f99f65b9c785d27f
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700508"
---
# <a name="management-insights-in-configuration-manager"></a>Configuration Manager 中的管理见解

适用范围：Configuration Manager (Current Branch)

Configuration Manager 中的管理见解功能提供了环境当前状态的相关信息。 该信息基于对站点数据库中数据的分析。 见解有助于更好地了解环境，并根据见解执行操作。 <!--1353967-->

## <a name="review-management-insights"></a>查看管理见解

若要查看见解，你的帐户需要拥有对“站点”对象的读取访问权限。

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“管理见解”，然后选择“所有见解”。

    > [!NOTE]
    > 选择“管理见解”节点时，它会显示[“管理见解仪表板”](#bkmk_insights)。

1. 打开要查看的管理见解组名称。

1. 在功能区中，选择“显示见解”。

以下四个选项卡可供查看：

- **所有规则**：提供了所选组的完整见解列表。

- **已完成**：列出了不需要采取行动的见解。

- **正在进行**：显示符合部分（但不是全部）先决条件的见解。

- **需要执行操作**：此选项卡列出了需要你采取行动的见解。 选择“更多详细信息”，以显示需要采取行动的具体项。

“先决条件”窗格列出了运行所选见解所需的任何项。

例如，下面的屏幕截图展示了“云服务”组的“所有规则”选项卡示例：

:::image type="content" source="media/management-insights-all-cloud-rules.png" alt-text="管理见解：云服务组的“所有规则”和“先决条件”":::

若要查看详细信息，请依次选择见解和“更多详细信息”。

## <a name="operations"></a>操作

站点每周重新评估一次管理见解的适用性。 若要手动重新评估见解，请右键单击见解，然后选择“重新评估”。

管理见解的日志文件是站点服务器上的 SMS_DataEngine.log。

<!--1357930-->
某些见解会让你采取行动。 依次选择见解、“更多详细信息”和“采取行动”（若有）。 根据见解，此行动包含以下行为之一：

- 在控制台中自动导航到可以采取进一步操作的节点。 例如，如果管理见解建议更改客户端设置，采取行动会转到“客户端设置”节点。 然后通过修改默认或自定义客户端设置对象采取进一步操作。

- 基于查询导航到筛选的视图。 例如，对见解指明的空集合采取行动只会显示集合列表中的这些集合。 然后采取进一步操作，例如删除集合或修改其成员身份规则。

## <a name="management-insights-dashboard"></a><a name="bkmk_insights"></a> 管理见解仪表板

<!--1357979-->

选择“管理见解”节点可以显示图形仪表板。 此仪表板显示了见解状态的概览，让你能够更轻松地查看进度。

使用仪表板顶部的以下筛选器可以细化视图：

- 显示已完成的工作
- 可选
- 建议
- 严重

该仪表板具有以下磁贴：  

- **管理见解索引**：跟踪管理见解的总体进度。 该索引为加权平均值。 关键见解是最有价值的。 此索引为可选见解分配的权重最低。

- **管理见解组**：显示每个组中见解所占的百分比（支持筛选器）。 选择一个组可以向下钻取此组中的特定见解。

- **管理见解优先级**：按优先级显示见解百分比（支持筛选器）。

- 前 10 个适用见解规则：一个包括优先级和状态的见解表。 使用表顶部的“筛选器”字段匹配任何可用列中的字符串。 仪表板按以下顺序对表进行排序：

  - 状态：需要执行操作、已完成、未知  
  - 优先级：重要、建议、可选  
  - 上次更改时间：较早的日期排在前面  

:::image type="content" source="media/1357979-management-insights-dashboard.png" alt-text="管理见解仪表板的屏幕截图" lightbox="media/1357979-management-insights-dashboard.png":::

## <a name="groups-and-insights"></a>组和见解

见解分为以下管理见解组：

- [应用程序](#applications)
- [云服务](#cloud-services)
- [集合](#collections)
- [Configuration Manager 评估](#configuration-manager-assessment)
- [更适合远程工作者](#optimize-for-remote-workers)
- [主动维护](#proactive-maintenance)
- [安全](#security)
- [简化管理](#simplified-management)
- [软件中心](#software-center)
- [软件更新](#software-updates)
- [Windows 10](#windows-10)

> [!NOTE]
> 你的站点可能不会显示以下所有组和见解。 如果你已为此建议配置了站点，一些见解就不会出现。

### <a name="applications"></a>应用程序

应用程序管理见解。

- 没有部署或引用的应用程序：列出环境中没有活动部署或引用的应用程序。 引用包括依赖项、任务序列和虚拟环境。 此见解有助于查找并删除未使用的应用程序，以简化在控制台中显示的应用程序列表。 有关详细信息，请参阅[部署应用程序](../../../apps/deploy-use/deploy-applications.md)。<!-- B585E3FF-585F-4CE9-AE2C-648A7CA2F143 -->

### <a name="cloud-services"></a>云服务

帮助与多种云服务集成，实现设备的现代化管理。

- **评估共同管理准备情况**：有助于了解启用共同管理所需执行的步骤。 此见解有先决条件。 有关详细信息，请参阅[共同管理概述](../../../comanage/overview.md)。<!-- D99F094A-A965-402F-AFE5-EE00CCAF0A12 -->

- 未上传到 Azure AD 的设备：自版本 2002 起，此见解列出了由于你没有为站点配置 HTTPS 而未上传到 Azure Active Directory (Azure AD) 的设备。<!--6268489--> 配置[增强型 HTTP](../../plan-design/hierarchy/enhanced-http.md)，或至少为 HTTPS 启用一个管理点。 如果你已为站点配置了 HTTPS 通信，此见解就不会出现。<!-- 609F03D4-D9B4-4D0D-A67F-9E365F6C0DD0 -->

- 启用云管理网关：云管理网关 (CMG) 提供了一种通过 Internet 管理 Configuration Manager 客户端的简单方法。 通过在 Microsoft Azure 中将 CMG 部署为云服务，可以继续管理在 Internet 上漫游的客户端并向其提供内容。 有了 CMG，就不需要向 Internet 公开其他任何本地基础结构。 有关详细信息，请参阅 [CMG 规划](../../clients/manage/cmg/plan-cloud-management-gateway.md)。<!-- 451B9B3A-D86A-4EF1-ACC3-FE6A207886BA -->

- **将设备启用为加入混合 Azure Active Directory**：使用已建立 Azure AD 联接的设备，用户可以使用自己的域凭据来登录，同时确保设备符合组织的安全性和符合性标准。 有关详细信息，请参阅 [Azure AD 混合标识设计注意事项](/azure/active-directory/hybrid/plan-hybrid-identity-design-considerations-overview)。<!-- 6DC6B149-8B48-45E9-B189-F1E12A62D994 -->

- 没有正确 HTTPS 配置的站点：自版本 2002 起，此见解列出层次结构中未正确配置 HTTPS 的站点。 此配置可防止站点[将集合成员资格结果同步到 Azure AD 组](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync)。 这可能导致 Azure AD 同步无法上传所有设备。 可能无法正常管理这些客户端。<!--6268489--> 配置[增强型 HTTP](../../plan-design/hierarchy/enhanced-http.md)，或至少为 HTTPS 启用一个管理点。 如果你已为站点配置了 HTTPS 通信，此见解就不会出现。<!-- 73884047-3395-430E-B971-F853806D4349 -->

- **将客户端升级到最新版 Windows 10**：Windows 10 版本 1709 或更高版本改进和新式化用户计算体验。 有关详细信息，请参阅[有关采用服务型 Windows 的关键文章](../../understand/configuration-manager-and-windows-as-service.md#key-articles-about-adopting-windows-as-a-service)。<!-- FD2C7B93-E5C6-4DCB-89AF-9EFCFCD01524 -->

### <a name="collections"></a>集合

通过清理和重新配置集合来帮助简化管理的见解。

- **空集合**：列出环境中没有成员的集合。 有关详细信息，请参阅[如何管理集合](../../clients/manage/collections/manage-collections.md)。<!-- 4266054A-695D-4BCA-8000-27BD32F7C006 -->

<!--3555752-->
- **不包含查询规则和直接成员的集合**：若要简化层次结构中的集合列表，请将其删除。<!-- 3C234964-B3F3-49EE-AA13-048CD2021924 -->

- **重新评估开始时间相同的集合**：这些集合与其他集合的重新评估时间相同。 修改重新评估时间，使它们不冲突。<!-- A85B79A6-BA81-404F-8DA4-DD7C87582CCD -->

- 查询时间超过 5 分钟的集合：查看此集合的查询规则。 请考虑修改或删除该集合。<!-- 6AF42536-BDF4-4535-87C1-535AE1B813DA -->

- 以下见解包括可能会导致站点上出现不必要负荷的配置。 审阅这些集合，然后删除它们，或禁用集合规则评估：

  - **没有查询规则且已启用增量更新的集合**<!-- 6A4845AB-6D2C-4F2A-B7AB-EC77C81FD571 -->

  - 无查询规则且启用任何计划的集合<!-- 219B9C45-BD02-4E7E-A29D-B66094366200 -->

  - **没有查询规则且选定计划完整评估的集合**<!-- 8A401207-5A7C-4200-A1DB-990A197458FA -->

### <a name="configuration-manager-assessment"></a>Configuration Manager 评估

<!--3607758-->

从版本 2002 开始，此组由 Microsoft Premier Field Engineering 提供。 这些见解只是 Microsoft 顶级支持在[服务中心](/services-hub/health/getting_started_with_on_demand_assessments)提供的众多检查中的一个例子。

- **Active Directory 安全组发现配置为过于频繁地运行**：通常不需要将 Active Directory 安全组发现配置为以高于每三小时一次的频率运行。 更频繁的配置可能对 Active Directory、网络和 Configuration Manager 的性能造成负面影响。 启用增量同步，而不使用完全同步计划。 有关详细信息，请参阅 [Active Directory 组发现](../deploy/configure/about-discovery-methods.md#bkmk_aboutGroup)。<!-- 4E739B65-AEC9-4B1D-8B36-AC6AC4A72022 -->

- **Active Directory 系统发现配置为过于频繁地运行**：通常不需要将 Active Directory 系统发现配置为以高于每三小时一次的频率运行。 更频繁的配置可能对 Active Directory、网络和 Configuration Manager 的性能造成负面影响。 启用增量同步，而不使用完全同步计划。 有关详细信息，请参阅 [Active Directory 系统发现](../deploy/configure/about-discovery-methods.md#bkmk_aboutSystem)。<!-- 353CAFBC-AC90-4FD3-B3CF-51D6D9FB376C -->

- **Active Directory 用户发现配置为过于频繁地运行**：通常不需要将 Active Directory 用户发现配置为以高于每三小时一次的频率运行。 更频繁的配置可能对 Active Directory、网络和 Configuration Manager 的性能造成负面影响。 启用增量同步，而不使用完全同步计划。 有关详细信息，请参阅 [Active Directory 用户发现](../deploy/configure/about-discovery-methods.md#bkmk_aboutUser)。<!-- 2E742924-7319-4013-B1E1-97DE7EB16B74 -->

- **集合仅限于“所有系统”或“所有用户”** ：查看使用“所有系统”或“所有用户”集合作为限制集合的任何集合。  Configuration Manager 用来自 Active Directory 发现方法的数据更新这些默认集合的成员身份。 这些数据对 Configuration Manager 客户端而言可能不是有效信息。<!-- 2382F0C9-A36D-4079-AB37-E3D8EE47E8D4 -->

- **已禁用检测信号发现**：要使用检测信号发现，需在设备上安装 Configuration Manager 客户端。 这是由客户端启用的唯一发现方法。 所有其他方法都在站点服务器上完成操作。 检测信号发现是保持最新客户端活动状态的基础。 它能确保站点不会意外时站点数据库中的资源记录过时。 有关详细信息，请参阅[检测信号发现](../deploy/configure/about-discovery-methods.md#bkmk_aboutHeartbeat)。<!-- A3089798-DF4E-490A-AF78-4AF474B214CF -->

- **已启用长期运行的集合查询以实现增量更新**：上次增量刷新时间超过 30 秒的集合使用站点服务器和数据库资源，可能会影响 Configuration Manager 整体性能。 有关详细信息，请参阅[集合的最佳做法](../../clients/manage/collections/best-practices-for-collections.md)。<!-- 21F14C0E-008B-47F3-B1E2-19CF79DC97B4 -->

- **减少分发点上的应用程序和包数量**：Microsoft 官方支持在每个分发点上承载总计 10,000 个包和应用程序。 超过此总数可能导致操作问题。 有关详细信息，请参阅[大小和扩展数量 - 分发点](../../plan-design/configs/size-and-scale-numbers.md#distribution-point)。<!-- FFE6906E-932E-4927-8EE0-BA25C37943CB -->

- **辅助站点安装问题**：某些辅助站点的安装状态为“挂起”或“失败”。  这些状态表示你已启动安装，但安装未成功完成。 在辅助站点安装完成之前，客户端可能无法与主站点正常通信。 请检查“监视”工作区并重试安装。 有关详细信息，请参阅[重试失败更新的安装](install-in-console-updates.md#bkmk_retry)。<!-- ED3F5BDD-2F02-44A4-87F4-BB2C1032D4DE -->

- **将所有站点更新到同一版本**：在层次结构中使用同一版本的 Configuration Manager。 此配置可保证所有站点都提供相同的功能。 同一层次结构中不同版本的站点会引入互操作性方案。 Configuration Manager 的更高版本包括新功能，并可解决已知问题。 有关详细信息，请参阅[不同版本之间的互操作性](../../plan-design/hierarchy/interoperability-between-different-versions.md)。<!-- 88C630A5-6D6B-4DDB-95D7-78E12107970D -->

若要详细了解这些见解，请参阅 [Configuration Manager 管理见解的修正步骤](/services-hub/health/remediation-steps-configmgr)。

> [!TIP]
> 如果你已经是 Microsoft 统一支持或 Microsoft 高级支持的客户，请登录到[服务中心](https://serviceshub.microsoft.com/assessments/)以获取其他按需评估。
>
> 有关 Microsoft 服务的详细信息，请参阅[支持解决方案](https://www.microsoft.com/enterprise/services/support)。

### <a name="operating-system-deployment"></a>操作系统部署

<!--6982275-->

自版本 2006 起，以下管理见解有助于你管理任务序列的策略大小。 当任务序列策略的大小超出 32 MB 时，客户端将无法处理此大型策略。 因而客户端将无法运行任务序列部署。

- **大型任务序列可能会导致超过最大策略大小**：若部署这些任务序列，客户端可能会无法处理这些大型策略对象。 请减少任务序列策略的大小，以防止出现潜在的策略处理问题。<!-- D9A15248-832E-4780-8151-ACD1B9E53FE1 -->

- **任务序列策略的总大小超出策略限制**：由于这些任务序列的策略过大，客户端将无法处理。 请减少任务序列策略的大小，以便该部署可以在客户端中运行。<!-- 6568F6A3-D1D8-4E63-940B-FE44F8349802 -->

有关详细信息，请参阅[减少任务序列策略的大小](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#bkmk_policysize)。

在版本 2006 中，以下见解从“主动维护”组移动到此组：

- **未用启动映像**：未引用启动映像来用于 PXE 启动或任务序列。 有关详细信息，请参阅[管理启动映像](../../../osd/get-started/manage-boot-images.md)。<!-- 4C1FBA51-AD56-4CA8-8326-066F65D24F0E -->

### <a name="optimize-for-remote-workers"></a>更适合远程工作者

<!--6982226-->

自版本 2006 起，以下见解有助于你为远程工作者提供更好的体验，并降低基础结构负荷：

- 将 VPN 连接的客户端配置为首选云端内容源：若要减少 VPN 上的流量，请启用边界组选项“首选云端源而不是本地源”。 此选项允许客户端从 Internet 下载内容，而不是通过 VPN 从分发点下载内容。 有关详细信息，请参阅[边界组选项](../deploy/configure/boundary-groups.md#bkmk_bgoptions4)。<!-- 1BFD7A7A-077C-4E8A-9EAA-4559E41D400A -->

- 定义 VPN 边界组：创建 VPN 边界，并将其关联到边界组。 将特定于 VPN 的站点系统关联到组，并配置环境设置。 此见解检查至少一个边界组，其中至少有一个 VPN 边界。 从此见解的属性中，选择“审查操作”，以转到“边界组”节点。 有关详细信息，请参阅 [VPN 边界类型](../deploy/configure/boundaries.md#vpn)。<!-- E44BF0CC-0ADA-4B00-A4DF-4005256DF73E -->

- 对 VPN 连接的客户端禁用对等内容共享：若要防止可能对远程客户端不利的不必要的对等流量，请禁用边界组选项“允许此边界组中的对等下载”。 有关详细信息，请参阅[边界组选项](../deploy/configure/boundary-groups.md#bkmk_bgoptions1)。<!-- 60404B23-96A9-4EE2-B8D6-1F226C2F2F5A -->

### <a name="proactive-maintenance"></a>主动维护

<!--1352184-->
此组中的见解强调了要通过定期维护 Configuration Manager 对象避免的潜在配置问题。

- **未分配有站点系统的边界组**：未分配有站点系统的边界组只能用于站点分配。 有关详细信息，请参阅[配置边界组](../deploy/configure/boundary-groups.md)。<!-- 01E5A4BC-0E31-494E-A553-2B32C410FA5B -->

- **没有成员的边界组**：没有任何成员的边界组不适用于站点分配或内容查找。 有关详细信息，请参阅[配置边界组](../deploy/configure/boundary-groups.md)。<!-- 4f0d37b1-f979-4ba3-b15b-7fe3c915f239 -->

- **未向客户端提供内容的分发点**：在过去 30 天内，分发点未向客户端提供内容。 此数据基于来自其客户端的下载历史记录报告。 有关详细信息，请参阅[安装和配置分发点](../deploy/configure/install-and-configure-distribution-points.md)。<!-- 9A115092-F8D4-4AB7-B846-C09143B9B9B0 -->

- **启用 WSUS 清理**：验证是否已启用对软件更新点组件的属性运行 WSUS 清理的选项。 此选项有助于提高 WSUS 性能。 有关详细信息，请参阅[软件更新维护](../../../sum/deploy-use/software-updates-maintenance.md)。<!-- D43080F1-FE98-4F24-94ED-FEB1C2DDEF50 -->

- **未用配置项目**：配置项目不属于配置基线，且已存在超过 30 天。 有关详细信息，请参阅[创建配置基线](../../../compliance/deploy-use/create-configuration-baselines.md)。<!-- 0597907B-17D4-4EA5-92E4-CCE692E1468D -->

- **将对等缓存源升级到最新版 Configuration Manager 客户端**：<!--1358008--> 确定用作对等缓存源，但尚未从先前的 1806 客户端版本升级的客户端。 先前的 1806 客户端不能用作运行版本 1806 或更高版本的客户端的对等缓存源。 选择“采取措施”打开显示客户端列表的设备视图。<!-- B51C6733-F9FF-46BC-8F5E-624F2CBED719 -->

> [!TIP]
> 在版本 2006 中，“未使用的启动映像”的见解移动到新的[“OS 部署”](#operating-system-deployment)组。

### <a name="security"></a>安全

提高基础结构和设备安全性的见解。

- **已启用 NTLM 回退**：<!--4572953--> 自版本 1906 起，此见解检测是否为站点启用了安全级别较低的 NTLM 身份验证回退方法。 当使用客户端推送方法安装 Configuration Manager 客户端时，站点可以要求进行 Kerberos 相互身份验证。 此增强有助于保护服务器与客户端之间的通信。 有关详细信息，请参阅[如何使用客户端请求安装客户端](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush)。<!-- C16C6826-8209-47A9-BA71-14A8C83E4C35 -->

- **不受支持的反恶意软件客户端版本**：超过 10% 的客户端运行的 System Center Endpoint Protection 版本不受支持。 有关详细信息，请参阅 [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md)。<!-- ACD63321-CF15-4CDD-B1A3-69005887C633 -->

### <a name="simplified-management"></a>简化管理

有助于简化对环境的日常管理的见解。

- **将站点连接到用于 Configuration Manager 更新的 Microsoft 云**：此见解可确保 Configuration Manager 服务连接点在过去七天内连接到 Microsoft 云。 此连接用于下载定期更新内容。 查看 DMPDownloader.log 和 hman.log。 有关详细信息，请参阅 [Internet 访问要求](../../plan-design/network/internet-endpoints.md#bkmk_scp-updates)。<!-- AC662C91-54DF-4B43-B09A-B19D2766144B -->

- **非 CB 客户端版本**：列出版本不是 Current Branch (CB) 内部版本的所有客户端。 有关详细信息，请参阅[升级客户端](../../clients/manage/upgrade/upgrade-clients.md)。<!-- 450090EA-DF71-428C-AB49-6DEBB85A004C -->

- **将客户端更新到支持的 Windows 10 版本**：<!--3897268--> 此见解报告运行不再受支持的 Windows 10 版本的客户端。 它还包括具有服务即将结束（三个月）的 Windows 10 版本的客户端。<!-- 560669D6-1756-4814-9505-C54BDB4930D0 -->

### <a name="software-center"></a>软件中心

关于管理软件中心的见解。

- **将用户定向到软件中心，而不是应用目录**：检查用户是否在过去 14 天内从应用目录安装或请求获取应用。 应用程序目录的主要功能现在包含在软件中心内。 版本 1910 已终止对应用程序目录角色的支持。 有关详细信息，请参阅[已弃用的功能](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md#deprecated-features)。<!-- DB9E65CF-C59C-4B76-B6A0-ADB95D809246 -->

- **使用新版软件中心**：不再支持以前版本的软件中心。 通过在“计算机代理”组中启用客户端设置“使用新的软件中心”，将客户端设置为使用新的软件中心 。 有关详细信息，请参阅[关于客户端设置](../../clients/deploy/about-client-settings.md#use-new-software-center)。<!-- A9BCA10D-834F-4F39-89F5-CDCCE8F80C56 -->

### <a name="software-updates"></a>软件更新

- **客户端设置未配置为允许客户端下载增量内容**：在环境中同步的某些软件更新包括增量内容。 启用客户端设置“在有可用内容时，允许客户端下载增量内容”。 如果不启用此设置，则在部署这些更新，客户端将不必要地下载超出要求的内容。 有关详细信息，请参阅[客户端设置 - 软件更新](../../clients/deploy/about-client-settings.md#software-updates)。<!-- 3E2E9E10-1CDC-47E3-BFC9-3A46AB7FE1BD -->

- **启用“Windows 10 版本 1903 及更高版本”的软件更新产品类别**：Windows 10 版本 1903 及更高版本有一个新的软件更新产品类别。 如果你同步 Windows 10 更新，且装有 Windows 10 版本 1903 或更高版本的客户端，请在软件更新点组件属性中选择“Windows 10 版本 1903 及更高版本”产品类别。 有关详细信息，请参阅[配置要同步的分类和产品](../../../sum/get-started/configure-classifications-and-products.md)。<!-- 16B1152D-6511-4DC7-824E-539B2597F9B0 -->

### <a name="windows-10"></a>Windows 10

与 Windows 10 的部署和服务相关的见解。 当超过一半的客户端运行 Windows 7、Windows 8 或 Windows 8.1 时，才可以使用 Windows 10 管理见解组。

- **配置 Windows 诊断和商业 ID 键**：若要使用桌面分析中的数据，请使用商业 ID 键配置设备并启用诊断数据收集。 将 Windows 10 设备设置为“增强型(有限)”或更高级别。 有关详细信息，请参阅[为桌面分析启用数据共享](../../../desktop-analytics/enable-data-sharing.md)。<!-- B224393F-B255-4C80-A1D1-1014BE1DC7D4 -->