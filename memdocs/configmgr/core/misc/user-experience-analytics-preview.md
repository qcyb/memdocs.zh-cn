---
title: 终结点分析预览版
titleSuffix: Configuration Manager
description: 终结点分析预览版的说明。
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 00537b90-f6d2-45e9-a9a1-6b3ada466a16
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: da8c52dabf27ddf0992d9f405400b3ac984f2ecc
ms.sourcegitcommit: 0b30c8eb2f5ec2d60661a5e6055fdca8705b4e36
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2020
ms.locfileid: "84455117"
---
# <a name="endpoint-analytics-preview"></a><a name="bkmk_uea"></a>终结点分析预览版

> [!Note]  
> 该信息涉及预览功能，该预览功能可能会在其商业发行之前进行大幅度修改。 对于此处提供的信息，Microsoft 不提供任何明示或暗示的担保。 
>
> 有关对终结点分析的更改的详细信息，请参阅[终结点分析的新增功能](whats-new-endpoint-analytics.md)。 
>
>如果想要加入终结点分析的个人预览版，请[在此表单中](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR9-ZzmlTlbJMh03eDDHtO81UOERLUkMzNFZKSlBaNFNFUVhFSlE0MzNYMS4u)输入详细信息。 预览扩展出现空缺时将向租户发布外部测试版。


## <a name="endpoint-analytics-overview"></a>终结点分析概述

最终用户遇到长时间启动或其他中断并不少见。 这些中断的原因可能在于：

- 旧硬件
- 针对最终用户体验进行了优化的软件配置
- 配置更改和更新引起的问题

这些问题和其他最终用户体验仍然存在，因为 IT 不太了解最终用户体验。 通常情况下，这些问题的唯一可见性来自速度较慢且成本较高的支持渠道，该渠道通常不会提供有关需要优化哪些内容的明确信息。 承担这些问题成本的不仅仅是 IT 支持。 信息工作者处理问题也需要花费大量时间。 降低用户工作效率的性能、可靠性和支持问题也会对组织的底线产生较大影响。

**终结点分析**旨在提高用户工作效率，并通过提供用户体验见解来降低 IT 支持成本。 通过这些见解，IT 可以使用主动支持来优化最终用户体验，并通过评估配置更改对用户的影响来检测用户体验回归。

此初始版本的重点为以下三个方面：

- [**推荐软件**](#bkmk_uea_rs)：提供最佳用户体验的建议
- [**主动修正脚本**](#bkmk_uea_prs)：在最终用户发现问题之前解决常见的支持问题
- [**启动性能**](#bkmk_uea_bp)：帮助 IT 使用户在无需长时间的启动和登录延迟的情况下快速从开机状态进入工作状态

此版本只是开始。 在初始版本发布后不久，我们将迅速推出针对其他关键用户体验的新见解。 有关对终结点分析的更改的详细信息，请参阅[终结点分析的新增功能](whats-new-endpoint-analytics.md)。

## <a name="getting-started"></a><a name="bkmk_uea_prereq"></a> 入门

若要开始使用终结点分析，请验证先决条件，然后开始收集数据。 

### <a name="technical-prerequisites"></a>技术先决条件

对于此预览版，可以通过 Configuration Manager 或 Microsoft Intune 来注册设备。 

#### <a name="to-enroll-devices-via-intune-this-preview-requires"></a><a name="bkmk_uea__intune_prereq"></a>要通过 Intune 注册设备，此预览版要求：
- 运行 Windows 10 的 Intune 注册设备
- 启动性能见解仅适用于运行 Windows 10 企业版（目前不支持家庭版和专业版）版本 1903 或更高版本的设备，并且设备必须已联接 Azure AD 或混合 Azure AD。 当前尚不支持已加入工作区的计算机。
- 从设备到 Microsoft 公有云的网络连接。 有关详细信息，请参阅[终结点](#bkmk_uea_endpoints)。
- 需要拥有 [Intune 服务管理员角色](https://docs.microsoft.com/intune/fundamentals/role-based-access-control)才能[开始收集数据](#bkmk_uea_start)。
   - 单击“启动”，即表示你同意并确认，你的客户数据可能存储在配置 Microsoft Intune 租户时所选位置的外部。
   - 单击“开始”以收集数据后，其他只读角色可以查看数据。

#### <a name="to-enroll-devices-via-configuration-manager-this-preview-requires"></a><a name="bkmk_uea__cm_prereq"></a>要通过 Configuration Manager 注册设备，此预览版要求：
- Configuration Manager 版本 2002 或更高版本
- 客户端已升级到版本 2002 或更高版本
- 已启用 [Microsoft Endpoint Manager 租户附加](https://docs.microsoft.com/mem/configmgr/tenant-attach/device-sync-actions)，且带有北美或欧洲 Azure 租户位置（我们将很快扩展到其他区域）

#### <a name="proactive-remediation-scripting-requires"></a><a name="bkmk_uea__prs_prereq"></a>主动修正脚本要求：
无论是通过 Intune 还是 Configuration Manager 注册设备，[**主动修正脚本**](#bkmk_uea_prs)都具有以下要求：
- 设备必须已联接 Azure AD 或混合 Azure AD，且必须满足下列条件之一：
- 一台由 Intune 管理的 Windows 10 企业版、专业版或教育版设备
- 一台[共同管理](../../comanage/overview.md)的设备，它正在运行 Windows 10 企业版 1607 或更高版本且其[客户端应用工作负载](../../comanage/workloads.md#client-apps)指向 Intune。
- 一台[共同管理](../../comanage/overview.md)的设备，它正在运行 Windows 10 企业版 1903 或更高版本且其[客户端应用工作负载](../../comanage/workloads.md#client-apps)指向 Configuration Manager。

### <a name="licensing-prerequisites"></a>许可先决条件

终结点分析包含在以下计划中： 

- [企业移动性 + 安全性 E3](https://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=51) 或更高版本
- [Microsoft 365 企业版 E3](https://www.microsoft.com/en-us/microsoft-365/enterprise?rtc=1) 或更高版本。

主动修正还需要受管理设备拥有以下许可证之一：
- Windows 10 企业版 E3 或 E5（包含在 Microsoft 365 F3、E3 或 E5 中）
- Windows 10 教育版 A3 或 A5（包含在 Microsoft 365 A3 或 A5 中）
- Windows 虚拟桌面访问 E3 或 E5

### <a name="permissions"></a>权限

#### <a name="endpoint-analytics-permissions"></a>终结点分析权限

以下权限用于终结点分析：
- “设备配置”类别下的“读取”权限 。
- “组织”类别下的“读取”权限 。 <!--temporary for pp-->
- 适用于“终结点分析”类别下的用户角色的权限。

只读用户只需在“设备配置”和“终结点分析”类别下拥有“读取”权限  。 Intune 管理员通常需要所有权限。

#### <a name="proactive-remediations-permissions"></a>主动修正权限

对于主动修正，用户需要在“设备配置”类别下拥有适合其角色的权限。  如果用户仅使用“主动修正”，则无需具备“终结点分析”类别中的权限。

在首次使用主动修正之前，需要 [Intune 服务管理员](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#intune-service-administrator-permissions)确认许可要求。

## <a name="start-gathering-data"></a><a name="bkmk_uea_start"></a> 开始收集数据
- 若要只注册 Intune 托管设备，请跳到[在终结点分析门户中加入](#bkmk_uea_onboard)部分。

- 若要注册 Configuration Manager 托管设备，需要按照以下步骤操作：
   - [在 Configuration Manager 中启用终结点分析数据收集](#bkmk_uea_cm_enroll)
   - [在 Configuration Manager 中启用数据上传](#bkmk_uea_cm_upload)
   - [在终结点分析门户中加入](#bkmk_uea_onboard)  

### <a name="enroll-devices-managed-by-configuration-manager"></a><a name="bkmk_uea_cm_enroll"></a> 注册 Configuration Manager 托管设备
<!--6051638, 5924760-->
注册 Configuration Manager 设备前，请先验证[先决条件](#bkmk_uea_prereq)，其中包括启用 [Microsoft Endpoint Manager 租户附加](https://docs.microsoft.com/mem/configmgr/tenant-attach/device-sync-actions)。 

#### <a name="enable-endpoint-analytics-data-collection-in-configuration-manager"></a><a name="bkmk_uea_cm_enable"></a> 在 Configuration Manager 中启用终结点分析数据收集

1. 在 Configuration Manager 控制台中，依次转到“管理” > “客户端设置” > “默认客户端设置”。
1. 右键单击并选择“属性”，然后选择“计算机代理”设置。
1. 将“启用终结点分析数据收集”设置为“是”。
   > [!Important] 
   > 如果已有部署到设备的自定义客户端代理设置，则需要更新此自定义设置中的“启用终结点分析数据收集”选项，然后将它重新部署到计算机以便生效。

#### <a name="enable-data-upload-in-configuration-manager"></a><a name="bkmk_uea_cm_upload"></a> 在 Configuration Manager 中启用数据上传

1. 在 Configuration Manager 控制台中，依次转到“管理” > “云服务” > “共同管理”。
1. 选择“CoMgmtSettingsProd”，然后单击“属性”。
1. 在“配置上传”选项卡选中，选中选项“为已上传到 Microsoft Endpoint Manager 的设备启用终结点分析”

   :::image type="content" source="media/6051638-configure-upload-configmgr.png" alt-text="为已上传到 Microsoft Endpoint Manager 的设备启用终结点分析" lightbox="media/6051638-configure-upload-configmgr.png":::

### <a name="onboard-in-the-endpoint-analytics-portal"></a><a name="bkmk_uea_onboard"></a> 在终结点分析门户中加入
Configuration Manager 托管设备和 Intune 托管设备都需要从终结点分析门户中加入。

1. 转到 `https://endpoint.microsoft.com/#blade/Microsoft_Intune_Enrollment/UXAnalyticsMenu`
1. 单击“开始” 。 这将自动分配一个配置文件，用于从所有符合条件的设备收集启动性能数据。 稍后，你可以[更改分配的设备](#bkmk_uea_profile)。 重启启动后，从 Intune 注册设备填充启动性能数据可能需要 24 小时。
   - 有关常见问题的详细信息，请参阅[启动性能设备注册故障排除](#bkmk_uea_enrollment_tshooter)。

## <a name="overview-page"></a>“概述”页面

数据准备就绪后，会在“概述”页上看到一些信息，详细说明如下：

- “用户体验分数”是”推荐软件”和”启动性能分数”的 50/50 加权平均值。 随着时间的推移，我们将扩展一组子分数。

- 可以通过设置基线来比较当前分数与其他分数。
  - 如[基准](#bkmk_uea_baselines)部分所述，“商业中间值”有一个内置基线，以了解如何与典型企业进行比较。 可以基于当前指标创建新基线，这样就可以随着时间的推移跟踪进度或查看回归。
   - 显示的基线标记用于总分数和子分数。 如果任何分数的回归超出了所选基线的可配置阈值，分数将显示为红色，并将顶级分数标记为“需要注意”。
  - “数据不足”状态意味着你没有足够的设备报告来提供有意义的分数。 目前需要至少 5 台设备。

- 使用“筛选器”可以查看部分设备或用户的分数。 但是，在此预览版中未启用筛选器功能。

- “见解和建议”是用于提高分数的优先级列表。 导航到“最佳实践”或“推荐软件”时，此列表将筛选到子节点的上下文中。

[![终结点分析概述页](media/overview-page.png)](media/overview-page.png#lightbox)

## <a name="recommended-software"></a><a name="bkmk_uea_rs"></a> 推荐软件

> [!Important]  
> Endpoint Analytics 计算所有 Intune 托管设备的软件采用分数，无论它们是否已注册 Endpoint Analytics。

某些软件可以改进最终用户体验，而与较低级别的运行状况指标无关。 例如，Windows 10 的 Net Promoter 分数远远高于 Windows 7。 软件采用分数是 0 到 100 之间的一个数字，表示已部署各种推荐软件的设备百分比的加权平均值。 Windows 的当前权重高于其他指标，因为用户更频繁地与它们进行交互。 以下对这些指标进行了介绍： 

[![终结点分析推荐软件页](media/recommended-software.png)](media/recommended-software.png#lightbox)

### <a name="windows-10"></a><a name="bkmk_uea_win10"></a> Windows 10

与早期版本的 Windows 相比，Windows 10 提供了更好的用户体验。 有关详细信息，请参阅 [TEI 白皮书](https://vc2prod.blob.core.windows.net/vc-resources/TEIStudies/TEI%20of%20Windows%2010.pdf)。

此指标测量 Windows 10 上的设备相对于旧版本 Windows 上的设备的比例。

从较旧版本的 Windows 移动设备时，建议的修正操作是使用[桌面分析](../../desktop-analytics/overview.md)创建部署计划。

### <a name="autopilot"></a><a name="bkmk_uea_ap"></a> Autopilot

通过减少即装即用体验 (OOBE) 中的屏幕数量并提供默认内容，Microsoft Autopilot 为 Windows 10 电脑提供比本机体验更简单的初始预配体验，以确保员工设备在恢复出厂设置和重置时正确预配。

此指标测量注册 Autopilot 的 Windows 10 设备的百分比。

建议的修正操作是使用 [Microsoft Intune](https://docs.microsoft.com/intune/enrollment-autopilot) 在 Autopilot 中注册现有设备。

### <a name="azure-active-directory"></a><a name="bkmk_uea_aad"></a> Azure Active Directory

Azure Active Directory (Azure AD) 为用户提供许多生产力优势，包括设备范围内应用和服务的单一登录、Windows Hello 登录、BitLocker 自助恢复以及公司数据漫游。

此指标测量在 Azure AD 中注册的设备的百分比。

已在 Azure AD 中注册了 Microsoft-Intune 托管设备。 针对 Configuration Manager 托管的设备的建议修正操作是[在 Azure AD 中进行注册](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains)或[共同管理这些设备](../../comanage/overview.md)。 共同管理的设备还可以提高云管理分数。

### <a name="cloud-management"></a><a name="bkmk_uea_intune"></a> 云管理

Microsoft Intune 为用户提供诸多生产力优势，包括在离开公司网络时也能访问公司资源，并消除了对组策略的需求和性能开销，从而改进了最终用户体验。 此指标测量 Microsoft Intune 中注册的电脑的百分比。 请参阅有关 [Microsoft 如何为员工实现此内容](https://www.microsoft.com/en-us/itshowcase/managing-windows-10-devices-with-microsoft-intune)的信息。

对于由尚未在 Intune 中注册的 Configuration Manager 所托管的设备，建议的修正操作为[共同管理设备](../../comanage/overview.md)。

### <a name="no-commercial-median"></a><a name="bkmk_uea_np"></a> 无商业中间值

“商业中间值”的内置基线当前没有上述部分中列出的子分数的指标。

## <a name="startup-performance"></a><a name="bkmk_uea_bp"></a> 启动性能

> [!NOTE]
> 如果未看到所有设备中的启动性能数据，请参阅[对启动性能设备注册进行故障排除](#bkmk_uea_enrollment_tshooter)。

启动性能分数帮助 IT 使用户在无需长时间的启动和登录延迟的情况下快速从开机状态进入工作状态。 启动分数为介于 0 到 100 之间的数字。 此分数是启动分数和登录分数的加权平均值，按如下方式进行计算：

- **启动分数**：基于从开机到登录的时间。 我们查看每个设备的上次启动时间（不包括更新阶段），然后从 0（差）到 100（出色）对其进行评分。 这些分数的平均值是为了提供总体租户启动分数。
- **登录分数**：基于从输入凭据到用户可以访问响应桌面的时间（这意味着桌面已呈现，并且 CPU 使用率至少有 2 秒钟时间下降到 50% 以下）。 我们查看每台设备的上次登录时间（不包括第一次登录或功能更新后立即登录），然后从 0（差）到 100（出色）对其进行评分。 这些分数的平均值是为了提供总体租户启动分数。

[![终结点分析启动性能页](media/startup-performance.png)](media/startup-performance.png#lightbox)

### <a name="insights"></a>见解

“启动性能”页还提供了“见解和建议”的优先级列表，如以下部分所述：

#### <a name="hard-disk-drives"></a><a name="bkmk_uea_hdd"></a> 硬盘驱动器

启动性能提供了有关启动驱动器为硬盘的设备数量的见解。 硬盘驱动器的启动时间通常比固态驱动器长三到四倍。 我们还报告了预期改进，以启动通过转移到固态硬盘可获得的性能。

单击查看拥有硬盘驱动器的设备列表。 建议的操作是将这些设备升级到固态驱动器。

#### <a name="group-policy"></a><a name="bkmk_uea_gp"></a> 组策略

启动性能提供对因组策略引起的启动和登录时间延迟的设备数的见解。 单击进入“设备”视图。 视图按组策略时间排序，因此你可以查看受影响的设备以进行进一步的故障排除。

如果单击特定设备，可以看到其启动和登录历史记录。 历史记录可帮助你确定问题是否是回归以及可能发生的时间。

尽管有很多关于如何优化组策略性能的文章，但你也可以选择迁移到云管理。 通过迁移到云管理，你可以使用 [Intune 安全基线](https://docs.microsoft.com/intune/protect/security-baselines)和即将发布的策略分析工具。

#### <a name="slow-boot-and-sign-in-times"></a><a name="bkmk_uea_sb"></a> 长时启动和登录

启动性能提供了有关启动或登录时间较长的设备数的见解。 启动分数或登录分数为“0”意味着速度缓慢。 单击进入“设备”视图。 这些设备分别按核心启动时间或核心登录时间排序，因此你可以查看受影响的设备，以便进一步进行故障排除。

如果单击特定设备，可以看到其启动和登录历史记录。 历史记录可帮助你确定问题是否是回归以及可能发生的时间。

### <a name="reporting-tabs"></a>报表选项卡

“启动性能”页具有为见解提供支持的报表选项卡，其中包括：
1. 模型性能。 借助此选项卡，你可按设备型号查看引导和登录性能，这有助于确定性能问题是否只限于特定型号。
1. 设备性能。 此选项卡提供所有设备的引导和登录指标。 可按特定指标（例如 GP 登录时间）进行排序，以查看哪些设备的该指标得分最差，从而帮助进行故障排除。 还可以按名称搜索设备。 如果单击浏览设备，可查看其引导和登录历史记录，这有助于确定近期性能是否有所退化
1. 启动进程。 启动进程会增加用户等待桌面响应的时间，从而对用户体验产生负面影响。 此选项卡（如果可见；我们仍在开发此功能，因此仅向部分用户发布了外部测试版）将显示哪些进程正影响登录“进入响应桌面的时间”阶段；也就是说，在桌面呈现后将 CPU 保持在 50% 以上。 此表仅列出了影响租户中至少 10 台设备的进程。  

## <a name="proactive-remediations"></a><a name="bkmk_uea_prs"></a> 主动修正

主动修正为脚本包，它可以在用户意识到问题之前检测并修复用户设备上的常见支持问题。 这些修正有助于减少支持调用。 你可自行创建脚本包，也可部署我们编写并在我们的环境中使用的某个脚本包，以减少支持票证。

每个脚本包都由一个检测脚本、一个修正脚本和元数据组成。 通过 Intune，你将能够部署这些脚本包，并查看报表了解其有效性。 我们正在积极地开发新的脚本包，并希望了解你使用这些脚本包的体验。 如果对脚本包有任何反馈，请联系你的终结点分析预览版联系人。

### <a name="get-the-detection-and-remediation-scripts"></a><a name="bkmk_uea_prs_ps1"></a> 获取检测和修正脚本

1. 从本文底部的 [PowerShell 脚本](#bkmk_uea_ps_scripts)部分复制脚本。
    - 名称以 `det` 开头的脚本文件是检测脚本。 修正脚本以 `rem` 开始。
    - 有关脚本的说明，请参阅[脚本说明](#bkmk_uea_scripts)。
1. 使用提供的名称保存每个脚本。 此名称也位于每个脚本顶部的注释中。
    - 你可以使用不同的脚本名称，但它不与[脚本说明](#bkmk_uea_scripts)部分中列出的名称相匹配。


### <a name="deploying-and-monitoring-scripts"></a><a name="bkmk_uea_prs_deploy"></a> 部署和监视脚本
Microsoft Intune 管理扩展服务从 Intune 获取并运行脚本。 脚本每 24 小时重新运行一次。 要部署和监视脚本，请按照以下说明操作：

1. 在控制台中转到“主动修正”节点。
1. 单击“创建脚本包”按钮创建脚本包。
     [![终结点分析主动修正页。选择创建链接。](media/proactive-remediations-create.png)](media/proactive-remediations-create.png#lightbox)
1. 在“基础”步骤中，为脚本包指定“名称”，并且可以选择“说明”。 可以编辑“发布者”字段，但默认为你的租户名称。 无法编辑“版本”。 
1. 在“设置”步骤中，将下载的脚本中的文本复制到“检测脚本”和“修正脚本”字段。 
   - 需要在同一个包中包含相应的检测和修正脚本。 例如，`Detect_stale_Group_Policies.ps1` 检测脚本对应 `Remediate_stale_GroupPolicies.ps1` 修正脚本。
       [![终结点分析主动修正脚本设置页。](media/proactive-remediations-script-settings.png)](media/proactive-remediations-script-settings.png#lightbox)
1. 使用以下建议的配置完成“设置”页上的选项：
   - **使用登录凭据运行此脚本**：这取决于脚本。 有关详细信息，请参阅[脚本说明](#bkmk_uea_scripts)。
   - **强制执行脚本签名检查**：否
   - **在 64 位 PowerShell 中运行脚本**：否
1. 单击“下一步”，然后分配所需的任何范围标记。
1. 在“分配”步骤中，选择要将脚本包部署到其中的设备组。
1. 为部署完成“审核+创建”步骤。
1. 在“报表” > “终结点分析 - 主动修正”中，可以查看检测和修正状态概述 。
       [![终结点分析主动修正报表，概述页。](media/proactive-remediations-report-overview.png)](media/proactive-remediations-report-overview.png#lightbox)
1. 单击“设备状态”以获取部署中每个设备的状态详细信息。
       [![终结点分析主动修正设备状态。](media/proactive-remediations-device-status.png)](media/proactive-remediations-device-status.png#lightbox)


## <a name="endpoint-analytics-settings"></a><a name="bkmk_uea_set"></a> 终结点分析设置

从“设置”页中，可以选择“常规”或“基线”。 下面介绍了其中每个设置：

### <a name="general"></a><a name="bkmk_uea_gen"></a>常规

通过“设置”中的“常规”页面，可以查看是否已启用 Intune 启动性能数据收集。 默认情况下，单击“开始”启用用户体验分析时，默认情况下会自动为所有设备启用该功能。 可以选择转到“Intune 数据收集策略”节点来更改收集启动和登录记录的设备集。


#### <a name="intune-data-collection-policy"></a><a name="bkmk_uea_profile"></a> Intune 数据收集策略

要将此设置分配给设备的子集，请[创建配置文件](/intune/configuration/device-profile-create#create-the-profile)，并提供以下信息： 

  - **名称**：输入配置文件的描述性名称，如“Intune 数据收集策略”
   
  - **描述**：输入配置文件的说明。 此设置是可选的，但建议进行。
    
  - **平台**：选择“Windows 10 及更高版本”
   
  - **配置文件类型**：选择“Windows 运行状况监视”
   
  - 配置“设置”：
   
       - **运行状况监视**：选择“启用”从 Windows 10 设备收集事件信息
    
    - **范围**：选择“启动性能” 

  - 使用[范围标记](/intune/configuration/device-profile-create#scope-tags)[适用性规则](/intune/configuration/device-profile-create#applicability-rules)，将配置文件筛选到特定 IT 组或满足特定条件的组中的设备。

> [!NOTE]
> 有一个占位符，用于说明如何配置 Configuration Manager 数据连接器。 但是，此功能尚未在此初始个人预览版中实现。

  [![终结点分析常规设置页](media/settings-general.png)](media/settings-general.png#lightbox)

### <a name="baseline-management"></a><a name="bkmk_uea_baselines"></a> 基线管理

可以通过设置基线将当前分数和子分数与其他分数进行比较。

1. “商业中间值”有一个内置基线，这允许你将分数与典型企业进行比较。
1. 可以基于当前指标创建新基线，这样就可以随着时间的推移跟踪进度或查看回归。 单击“新建”按钮，并为新基线指定名称。 建议使用包含日期的名称，便于更轻松地从“报表”页的下拉列表中进行选择。
1. 每个租户的基线数限制为 100。 可以删除不再需要的旧基线。
1. 如果当前指标低于报表中的当前基线，则会将其标记为红色，并显示为回归。 因为每天指标波动纯属正常现象，所以你可以设置一个回归阈值，默认为 10%。 使用此阈值时，只有当指标回归超过 10%，才将其标记为回归。

   [![终结点分析基线设置页](media/settings-baseline.png)](media/settings-baseline.png#lightbox)

## <a name="troubleshooting"></a><a name="bkmk_uea_tshoot"></a> 故障排除

以下部分可用于帮助对可能遇到的问题进行故障排除。

### <a name="troubleshooting-startup-performance-device-enrollment"></a><a name="bkmk_uea_enrollment_tshooter"></a>对启动性能设备注册进行故障排除

如果概述页显示的启动性能分数为零，并带有显示其正在等待数据的横幅，或者如果启动性能的设备性能选项卡显示的设备数量少于预期，则可以采取一些步骤来对问题进行故障排除。

首先，以下简要总结了启动性能数据收集的限制：
1. 设备必须为 Windows 10 版本 1903 或更高版本。
2. 设备必须已联接 Azure AD。 我们目前不支持已加入工作区的设备，但正在积极研究将此功能添加到 Windows 的可行性。
3. 设备必须为 Windows 10 企业版。 目前不支持 Windows 10 家庭版和专业版，但正在积极研究将此功能添加到 Windows 的可行性。

请注意，这些问题对来自即将发布的 Configuration Manager 连接器的数据不适用；无论版本或目录配置如何，该连接器都可从任何 Configuration Manager 的客户端电脑收集数据。

其次，以下是用于故障排除的快速排查清单：
1. 确保将 Windows 运行状况监视配置文件设置为针对要获取性能数据的所有设备。 可以从终结点分析设置页中找到此配置文件的链接，也可以像导航到其他 Intune 配置文件一样导航到该配置文件。 查看分配选项卡，确保已将其分配给预期的设备集。 
1. 查看哪些设备已成功完成数据收集配置。 也可以在配置文件概述页中查看此信息。  
   - 存在一个已知问题，即客户可能会看到配置文件分配错误，其中受影响的设备显示错误代码 `-2016281112 (Remediation failed)`。 我们正在积极调查此问题。
1. 启用数据收集后，必须重启已成功完成数据收集配置的设备，然后，必须等待最多 24 小时才能看到设备在设备性能选项卡中显示。
1. 如果设备已成功完成数据收集配置，随后又重启，但在 24 小时后仍看不到它，则可能是因为该设备无法到达我们的收集终结点。 如果公司使用代理服务器并且尚未在代理中启用终结点，则可能会发生此问题。 有关详细信息，请参阅[终结点故障排除](#bkmk_uea_endpoints)。

### <a name="data-collection-for-intune-managed-devices"></a>从 Intune 托管设备收集数据

终结点分析利用 Windows 10 和 Windows Server 互连用户体验和遥测组件 (DiagTrack) 从 Intune 托管的设备收集数据。 确保设备上的“已连接的用户体验和遥测”服务正在运行。

#### <a name="endpoints"></a><a name="bkmk_uea_endpoints"></a> 终结点

若要向终结点分析注册设备，需要将所需功能数据发送给 Microsoft。 如果你的环境使用代理服务器，请使用此信息来帮助配置代理。

若要启用功能数据共享，请将代理服务器配置为允许以下终结点：

> [!Important]  
> 对于隐私和数据完整性，Windows 在与所需功能数据共享终结点通信时将检查 Microsoft SSL 证书（证书固定）。 无法进行 SSL 拦截和检查。 若要使用终结点分析，请从 SSL 检查中排除这些终结点。<!-- BUG 4647542 -->

| 终结点  | 函数  |
|-----------|-----------|
| `https://*.events.data.microsoft.com` | 用于将[必需的功能数据](#bkmk_uea_datacollection)发送到 Intune 数据收集终结点。 |
| `https://graph.windows.net` | 用于在将层次结构附加到终结点分析时自动检索设置（担任 Configuration Manager 服务器角色时）。 有关详细信息，请参阅[配置站点系统服务器的代理](../plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server)。 |
| `https://*.manage.microsoft.com` | 用于使设备收集和设备与终结点分析同步（仅限担任 Configuration Manager 服务器角色的情况）。 有关详细信息，请参阅[配置站点系统服务器的代理](../plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server)。 |


#### <a name="proxy-server-authentication"></a>代理服务器身份验证

如果你的组织使用代理服务器身份验证进行 Internet 访问，请确保它不会因为身份验证而阻止数据。 如果你的代理不允许设备发送此数据，则它们不会显示在桌面分析中。

##### <a name="bypass-recommended"></a>免验证（推荐）

将代理服务器配置为不要求对数据共享终结点的流量进行代理身份验证。 此选项是最全面的解决方案。 适用于所有 Windows 10 版本。  

##### <a name="user-proxy-authentication"></a>用户代理身份验证

将设备配置为使用登录用户的上下文进行代理身份验证。 此方法需要以下配置：

- 设备具有受支持的 Windows 版本的最新质量更新

- 在 Windows 设置的“网络和 Internet”组中的“代理设置”中配置用户级代理（WinINET 代理）。 还可以使用旧版”Internet 选项”控制面板。

- 确保用户拥有访问数据共享终结点的代理权限。 此选项要求设备具有拥有代理权限的控制台用户，因此无法将此方法用于无外设设备。

> [!IMPORTANT]
> 用户代理身份验证方法与使用 Microsoft Defender 高级威胁防护不兼容。 出现此行为是因为，此身份验证依赖于设置为 `0` 的 DisableEnterpriseAuthProxy 注册表项，而 Microsoft Defender ATP 要求将其设置为 `1`。 有关详细信息，请参阅[在 Microsoft Defender ATP 中配置计算机代理和 Internet 连接设置](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/configure-proxy-internet-windows-defender-advanced-threat-protection)。

##### <a name="device-proxy-authentication"></a>设备代理身份验证

此方法支持以下方案：

- 无外设的设备，其中无用户进行登录或该设备的用户无法访问 Internet

- 不使用 Windows 集成身份验证的经验证的代理

- 如果你同时还使用了 Microsoft Defender 高级威胁防护

此方法是最复杂的方法，因为它需要以下配置：

- 确保设备可以通过 WinHTTP 在本地系统上下文中访问代理服务器。 使用下列选项之一来配置此行为：

  - 命令行 `netsh winhttp set proxy`

  - Web 代理自动发现 (WPAD) 协议

  - 透明代理

  - 使用以下组策略设置配置设备范围内的 WinINET 代理：**按每台计算机（而不是每个用户）配置代理设置** (ProxySettingsPerUser = `1`)

  - 路由的连接，或使用网络地址转换 (NAT) 的连接

- 配置代理服务器以允许 Active Directory 中的计算机帐户访问数据终结点。 此配置要求代理服务器支持 Windows 集成身份验证。  


## <a name="frequently-asked-questions"></a><a name="bkmk_uea_faq"></a>常见问题

### <a name="will-my-endpoint-analytics-data-migrate-if-i-move-my-intune-tenant-to-a-different-tenant-location"></a>如果将我的 Intune 租户移到其他租户位置，会迁移我的终结点分析数据吗？

如果将你的 Intune 租户迁移到其他位置，则在迁移时终结点分析解决方案中的所有数据都将丢失。 如果设备仍保持正确注册状态，由于终结点会持续向终结点分析报告，因此，迁移后发生的所有事件都将自动上传到新租户位置，且报告将开始重新填充。 

### <a name="why-are-the-scripts-exiting-with-a-code-of-1"></a>为什么脚本退出时的代码为 1？

脚本退出时附带代码 1 指示 Intune 应进行修正。 在这种情况下，退出带有 1 的检测脚本意味着需要进行修正。 许多仅以 CM 运行的脚本包可能会显示符合，但在退出时会附带代码 1。 对于这些脚本，退出时附带代码 1 并不是什么令人担忧的事情，但你可能需要验证设备是否正确进行了修正。

### <a name="why-did-the-update-stale-group-policies-script-return-with-error-0x87d00321"></a>为什么更新过时的组策略脚本返回错误 0x87D00321？

0x87D00321 是脚本执行超时错误。 此错误通常发生在远程连接的计算机上。 可能的缓解措施可能是仅部署到具有内部网络连接的动态计算机集合中。

## <a name="script-descriptions"></a><a name="bkmk_uea_scripts"></a> 脚本说明

此表显示了脚本名称、说明、检测、修正和可配置的项目。 名称以 `Detect` 开头的脚本文件是检测脚本。 修正脚本以 `Remediate` 开始。 可以从本文的下一节中复制这些脚本。

|脚本名称|说明|
|---|---|
|**更新过时的组策略** </br>`Detect_stale_Group_Policies.ps1` </br> `Remediate_stale_GroupPolicies.ps1`| 检测上次组策略刷新是否超过 `7 days` 之前。  </br>通过在检测脚本中更改 `$numDays` 的值来自定义 7 天阈值。 </br></br>通过运行 `gpupdate /target:computer /force` 和 `gpupdate /target:user /force` 进行修正  </br> </br>通过组策略提供证书和配置，有助于减少与网络连接相关的支持调用。 </br> </br> **使用登录凭据运行脚本**：是|
|**重新启动 Office 即点即用服务** </br> `Detect_Click_To_Run_Service_State.ps1` </br> `Remediate_Click_To_Run_Service_State.ps1`| 检测即点即用服务是否设置为自动启动，以及服务是否已停止。 </br> </br> 通过将服务设置为自动启动并在服务停止时启动服务进行补救。 </br></br> 可帮助解决 Win32 Microsoft 365 企业应用版无法启动的问题，因为即点即用服务已停止。 </br> </br> **使用登录凭据运行脚本**：否|
|**检查网络证书** </br>`Detect_Expired_Issuer_Certificates.ps1` </br>`Remediate_Expired_Issuer_Certificates.ps1`|检测 CA 在计算机或用户的个人存储区中颁发的已过期或即将过期的证书。 </br> 通过在检测脚本中更改 `$strMatch` 的值来指定 CA。 将 `$expiringDays` 指定为 0 以查找过期证书，或指定另一个天数来查找即将过期的证书。  </br></br>通过向用户引发 toast 通知进行修正。 </br> 指定 `$Title` 和 `$msgText` 值以及你希望用户看到的消息标题和文本。 </br> </br> 通知用户可能需要续订的过期证书。 </br> </br> **使用登录凭据运行脚本**：否|
|**清除过时证书** </br>`Detect_Expired_User_Certificates.ps1` </br> `Remediate_Expired_User_Certificates.ps1`| 检测由当前用户的个人存储区中的 CA 颁发的过期证书。 </br> 通过在检测脚本中更改 `$certCN` 的值来指定 CA。 </br> </br> 通过从当前用户的个人存储区中删除 CA 颁发的过期证书进行修正。 </br> 通过更改修正脚本中 `$certCN` 的值来指定 CA。 </br> </br> 从当前用户的个人存储区中查找并删除 CA 颁发的过期证书。 </br> </br> **使用登录凭据运行脚本**：是|

## <a name="powershell-scripts"></a><a name="bkmk_uea_ps_scripts"></a> PowerShell 脚本

### <a name="detect_stale_group_policiesps1"></a>Detect_stale_Group_Policies.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_stale_Group_Policies.ps1
# Description:     Detect if Group Policy has been updated within number of days
# Notes:           Remediate if "Match", $numDays default value of 7, change as appropriate
#
#=============================================================================================================================

# Define Variables
$numDays = 7

try {
    $gpResult = gpresult /R | Select-String -pattern "Last time Group Policy was applied:" | Select-Object -last 1

    if ($gpResult){
    [int]$lastGPUpdateDays = (New-TimeSpan -Start $lastGPUpdateDate -End (Get-Date)).Days
        if ($lastGPUpdateDays -gt $numDays){
            #We want within last $numDays so we get "Match"
            Write-Host "Match"
            exit 1
        }
        else {
            #Script succeeds but > $numDays since last update so remediate
            #Exit 1 for Intune and "Match" for ConfigMan
            Write-Host "No_Match"
            exit 0
        }
    }
}
catch {
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="remediate_stale_grouppoliciesps1"></a>Remediate_stale_GroupPolicies.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_stale_GroupPolicies.ps1
# Description:     This script triggers Group Policy update
# Notes:           No variable substitution needed
#
#=============================================================================================================================

try{
    $compGP = gpupdate /target:computer /force | out-string
    $userGP = gpupdate /target:user /force | out-string
    exit 0
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="detect_click_to_run_service_stateps1"></a>Detect_Click_To_Run_Service_State.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_Click_To_Run_Service_State.ps1
# Description:     Detect if Office 16 installed and if "Click to Run Service" is running.
# Notes:           No variable substitution should be necessary
#
#=============================================================================================================================

# Define Variables
$curSvcStat,$svcCTRSvc,$errMsg = "","",""

# Main script
If (-not (Test-Path -Path 'hklm:\Software\Microsoft\Office\16.0')){
    Return "Office 16.0 (or greater) not present on this machine"
    exit 0   
} 

Try{        
    $svcCTRSvc = Get-Service "ClickToRunSvc"
    $curSvcStat = $svcCTRSvc.Status
}

Catch{    
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}

If ($curSvcStat -eq "Running"){
    Write-Output $curSvcStat
    exit 0                        
}
Else{
    If($curSvcStat -eq "Stopped"){
    Write-Output $curSvcStat
    exit 1     
    }
}
Else{
    Write-Error "Error: " + $errMsg
    exit 1
}
```

### <a name="remediate_click_to_run_service_stateps1"></a>Remediate_Click_To_Run_Service_State.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_Click_To_Run_Service_State.ps1
# Description:     Start the "Click to Run Service" and change its startup type to Automatic
#       Notes:     No variable substitution needed
#
#=============================================================================================================================

# Define Variables
$svcCur = "ClickToRunSvc"
$curSvcStat,$svcCTRSvc,$errMsg = "","",""
$ctr = 0

# Main script
# Make sure nothing has changed since detection, the service exists and is stopped
Try{        
    $svcCTRSvc = Get-Service "ClickToRunSvc"
    $curSvcStat = $svcCTRSvc.Status
    }

Catch{    
    $errMsg = $_.Exception.Message
    }
        
# If the service got started between detection and now (nested if) then return
# If the service got uninstalled or corrupted between detection and now (else) then return the "Error: " + the error
If ($curSvcStat -ne "Stopped"){
    If ($curSvcStat -eq "Running"){
        return
    }
    Else{
        return "Error: " + $errMsg
    }
}

# Service should be there and stopped, change the startup type and start
Try{        
    Set-Service $svcCur -StartupType Automatic
    Start-Service $svcCur
    $svcCTRSvc = Get-Service $svcCur
    $curSvcStat = $svcCTRSvc.Status
        While ($curSvcStat.Equals("Stopped")){
            Start-Sleep -Seconds 5
            ctr++
            if(ctr == 12){
                Return "Service could not be started after 60 seconds"
                break
            }
        }
    }

Catch{    
    $errMsg = $_.Exception.Message
    Return $errMsg
    }

Return $curSvcStat
```

### <a name="detect_expired_issuer_certificatesps1"></a>Detect_Expired_Issuer_Certificates.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_Expired_Issuer_Certificates.ps1
# Description:     Detect expired certificates issued by "CN=<your CA here>" in either Machine
#                  or User certificate store
# Notes:           Change the value of the variable $strMatch from "CN=<your CA here>" to "CN=..."
#                  For testing purposes the value of the variable $expiringDays can be changed to a positive integer
#                  Don't change the $results variable
#
#=============================================================================================================================

# Define Variables
$results = @()
$expiringDays = 0
$strMatch = "CN=<your CA here>"

try
{
    $results = @(Get-ChildItem -Path Cert:\LocalMachine\My -Recurse -ExpiringInDays $expiringDays | where {$_.Issuer -match $strMatch})
    $results += @(Get-ChildItem -Path Cert:\CurrentUser\My -Recurse -ExpiringInDays $expiringDays | where {$_.Issuer -match $strMatch}) 
    if (($results -ne $null)){
        #Below necessary for Intune as of 10/2019 will only remediate Exit Code 1
        Write-Host "Match"
        Return $results.count
        exit 1
    }
    else{
        #No matching certificates, do not remediate
        Write-Host "No_Match"        
        exit 0
    }   
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="remediate_expired_issuer_certificatesps1"></a>Remediate_Expired_Issuer_Certificates.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_Expired_Issuer_Certificates.ps1
# Description:     Raise a Toast Notification if expired certificates issued by "CN=..."
#                  to user or machine on the machine where detection script found them. No remediation action besides
#                  the Toast is taken.
# Notes:           Change the values of the variables $Title and $msgText
#
#=============================================================================================================================

## Raise toast to have user contact whoever is specified in the $msgText

# Define Variables
$delExpCert = 0
$Title = "Title"
$msgText = "message"

# Main script
[Windows.UI.Notifications.ToastNotificationManager, Windows.UI.Notifications, ContentType = WindowsRuntime] | Out-Null
[Windows.UI.Notifications.ToastNotification, Windows.UI.Notifications, ContentType = WindowsRuntime] | Out-Null
[Windows.Data.Xml.Dom.XmlDocument, Windows.Data.Xml.Dom.XmlDocument, ContentType = WindowsRuntime] | Out-Null

$APP_ID = '{1AC14E77-02E7-4E5D-B744-2EB1AE5198B7}\WindowsPowerShell\v1.0\powershell.exe'

$template = @"
<toast>
    <visual>
        <binding template="ToastText02">
            <text id="1">$Title</text>
            <text id="2">$msgText</text>
        </binding>
    </visual>
</toast>
"@

$xml = New-Object Windows.Data.Xml.Dom.XmlDocument
$xml.LoadXml($template)
$toast = New-Object Windows.UI.Notifications.ToastNotification $xml
[Windows.UI.Notifications.ToastNotificationManager]::CreateToastNotifier($APP_ID).Show($toast)
```

### <a name="detect_expired_user_certificatesps1"></a>Detect_Expired_User_Certificates.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_Expired_User_Certificates.ps1
# Description:     Detect expired certificates issued by "CN=<your CA here>" to User
# Notes:           Change the value of the variable $certCN from "CN=<your CA here>" to "CN=...".
#                  Don't change $results
#
#=============================================================================================================================

# Define Variables
$results = 0
$certCN = "CN=<your CA here>"

try
{   
    $results = Get-ChildItem -Path Cert:\CurrentUser\My -Recurse -ExpiringInDays 0 | where {$_.Issuer -eq($certCN)}
    if (($results -ne $null)){
        #Below necessary for Intune as of 10/2019 will only remediate Exit Code 1
        Write-Host "Match"
        Return $results.count
        exit 1
    }
    else{
        Write-Host "No_Match"
        exit 0
    }    
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="remediate_expired_user_certificatesps1"></a>Remediate_Expired_User_Certificates.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_Expired_User_Certificates.ps1
# Description:     Remove expired certificates issued by "CN=<your CA here>" to User
# Notes:           Change the value of the variable $certCN from "CN=<your CA here>" to "CN=..."
#
#=============================================================================================================================

# Define Variables
$certCN = "CN=<your CA here>"

try
{
    Get-ChildItem -Path cert:\CurrentUser -Recurse -ExpiringInDays 0 | where {$_.Issuer -eq($certCN)} | Remove-Item
    exit 0
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

## <a name="endpoint-analytics-data-privacy"></a><a name="bkmk_uea_privacy"></a>终结点分析数据隐私

### <a name="data-flow"></a>数据流

下图显示了各个设备中的所需功能数据如何通过数据服务、暂时存储流向租户。 数据流经我们现有的企业管道，无需依赖于 Windows 诊断数据。

[![用户体验数据流关系图](media/dataflow.png)](media/dataflow.png#lightbox)

1. 为注册的设备配置“Intune 数据收集”策略。 默认情况下，当你选择“开始”终结点分析时，此策略将分配给“所有设备”。 不过，你可以随时[更改分配](#bkmk_uea_set)，以分配到设备的子集或者不分配到任何设备。

2. 设备发送所需的功能数据。

    - 对于具有指定策略的 Intune 设备，从 Intune 管理扩展发送数据。 有关详细信息，请参阅[系统要求](#bkmk_uea_prereq)。
    - 对于 Configuration Manager 托管设备，数据也可以通过 ConfigMgr 连接器流向 Microsoft 终结点管理。 ConfigMgr 连接器已连接到云。 它只需要连接到 Intune 租户，而不会启用共同管理。

> [!Note]  
> 启动期间会生成计算设备启动分数所需的数据。 根据电源设置和用户行为，为设备正确分配策略后，可能要在几周后才会在管理控制台上显示启动分数。  

3. Microsoft 终结点管理服务使用 MS Graph API 处理每个设备的数据，并在管理控制台中发布所有单个设备和组织聚合的结果。

端到端的平均延迟时间大约为 12 小时，并由执行日常处理所需的时间决定。 数据流的所有其他部分都是近实时的。

### <a name="data-collection"></a><a name="bkmk_uea_datacollection"></a>数据收集

目前，终结点分析的基本功能是收集与启动性能记录相关的信息，此类信息分为[识别信息](https://docs.microsoft.com/mem/intune/protect/privacy-data-collect#identified-data)和[假名信息](https://docs.microsoft.com/mem/intune/protect/privacy-data-collect#pseudonymized-data)这两种类别。 我们将逐渐添加其他功能，收集的数据将随需要而变化。 当前收集的主要数据点：

#### <a name="identified-data"></a>标识数据

- 硬件清单信息
  - **make：** 设备制造商
  - **model：** 设备型号
  - **deviceClass：** 设备分类。 例如，桌面、服务器或移动。
  - **Country：** 设备区域设置
- 应用程序清单，例如
  - **名称：** Windows
  - **版本：** 当前 OS 版本。
  
#### <a name="pseudonymized-data"></a>使用假名的数据

- 与用户和/或设备绑定的诊断、性能和使用情况数据
  - **logOnId**
  - **bootId：** 系统启动 ID
  - **coreBootTimeInMilliseconds：** 核心启动时间
  - **totalBootTimeInMilliseconds：** 总启动时间
  - **updateTimeInMilliseconds：** OS 更新完成的时间
  - **gpLogonDurationInMilliseconds**：处理组策略的时间
  - **desktopShownDurationInMilliseconds：** 桌面 (explorer.exe) 的加载时间
  - **desktopUsableDurationInMilliseconds：** 桌面 (explorer.exe) 可用的时间
  - **topProcesses：** 在启动过程中加载的进程列表，其中包含名称、CPU 使用情况统计信息和应用详细信息（名称、发布者、版本）。 例如 *{\"ProcessName\":\"svchost\"、\"CpuUsage\":43、\"ProcessFullPath\":\"C:\\\\Windows\\\\System32\\\\svchost.exe\"\"ProductName\":\"Microsoft&reg; Windows&reg; Operating System\"、\"Publisher\":\"Microsoft Corporation\"、\"ProductVersion\":\"10.0.18362.1\"}*
- 没有与设备或用户绑定的设备数据（如果此数据与某个设备或用户绑定，Intune 会将其视为标识数据）
  - **ID：** Windows 更新使用的唯一设备 ID
  - **localId：** 设备的本地定义的唯一 ID。 这不是用户可读的设备名称。 它最有可能等于存储在 HKLM\Software\Microsoft\SQMClient\MachineId 中的值。
  - **aaddeviceid：** Azure Active Directory 设备 ID
  - **orgId：** 代表 Microsoft O365 租户的唯一 GUID
  
> [!Important]  
> [Microsoft Intune 隐私声明](https://docs.microsoft.com/legal/intune/microsoft-intune-privacy-statement)中介绍了数据处理策略。 我们仅使用你的客户数据提供你注册的服务。 如加入过程中所述，我们将所有注册组织的分数匿名化并进行汇总，以使基准保持最新。


### <a name="resources"></a>资源

相关隐私方面的详细信息，请参阅以下文章：

- [Microsoft Intune 隐私声明](https://docs.microsoft.com/legal/intune/microsoft-intune-privacy-statement)
- [Windows 10 和隐私合规性](https://docs.microsoft.com/windows/privacy/windows-10-and-privacy-compliance)
- [许可条款和文档](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31)  
- [Microsoft Azure 数据中心的安全和隐私](https://azure.microsoft.com/global-infrastructure/)  
- [受信任云中的置信度](https://azure.microsoft.com/overview/trusted-cloud/)  
- [信任中心](https://www.microsoft.com/trustcenter)  
