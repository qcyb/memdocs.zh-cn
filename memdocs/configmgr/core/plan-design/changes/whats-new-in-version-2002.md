---
title: 2002 版中的新增功能
titleSuffix: Configuration Manager
description: 获取有关 Configuration Manager Current Branch 版本 2002 中引入的更改和新增功能的详细信息。
ms.date: 07/27/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: de718cdc-d0a9-47e2-9c99-8fa2cb25b5f8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 66fcd9b7d4d25decb3aeef7cf38b469363eeb1fa
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128893"
---
# <a name="whats-new-in-version-2002-of-configuration-manager-current-branch"></a>Configuration Manager Current Branch 版本 2002 中的新增功能

适用范围：Configuration Manager (Current Branch)

Configuration Manager Current Branch 的更新 2002 作为控制台内更新提供。 将此更新应用于运行版本 1810 或更高版本的站点。 <!-- baseline only statement:-->安装新站点时，它也可作为基准版本提供。 本文汇总了 Configuration Manager 版本 2002 中的更改和新增功能。

始终查看安装此更新的最新清单。 有关详细信息，请参阅[用于安装更新 2002 的清单](../../servers/manage/checklist-for-installing-update-2002.md)。 更新站点后，还可以查看[更新后清单](../../servers/manage/checklist-for-installing-update-2002.md#post-update-checklist)。

若要利用 Configuration Manager 的新功能，更新站点后，还请将客户端更新到最新版本。 尽管在更新站点和控制台时 Configuration Manager 控制台中会显示新功能，但只有在客户端版本也是最新版本之后，完整方案才能正常运行。

> [!TIP]
> 若要在此页面更新时收到通知，请将以下 URL 复制并粘贴到 RSS 源阅读器中：`https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+2002+-+Configuration+Manager%22&locale=en-us`

## <a name="microsoft-endpoint-manager-tenant-attach"></a><a name="bkmk_tenant"></a> Microsoft Endpoint Manager 租户附加

### <a name="device-sync-and-device-actions"></a><a name="bkmk_attach"></a> 设备同步和设备操作
<!--3555758-->
Microsoft Endpoint Manager 是用于管理所有设备的集成解决方案。 Microsoft 将 Configuration Manager 和 Intune 组合为单个控制台，称为“Microsoft Endpoint Manager 管理中心”。 从此版本开始，可以从该管理中心的“设备”边栏选项卡中将 Configuration Manager 设备上传到云服务并执行操作。

有关详细信息，请参阅 [Microsoft Endpoint Manager 租户附加](../../../tenant-attach/device-sync-actions.md)。

## <a name="site-infrastructure"></a><a name="bkmk_infra"></a>站点基础结构

### <a name="remove-a-central-administration-site"></a>删除管理中心站点
<!-- 3607277 -->

如果层次结构由管理中心站点 (CAS) 和单个子级主站点组成，则现在可以删除 CAS。 此操作可将 Configuration Manager 基础结构简化为单个独立主站点。 它可消除站点到站点复制的复杂性，并将管理任务集中到单个主站点。

有关详细信息，请参阅[删除 CAS](../../servers/deploy/install/remove-central-administration-site.md)。

### <a name="new-management-insight-rules"></a>新管理见解规则

此版本包括以下管理见解规则：

- 由 Microsoft 顶级支持现场工程部门提供的 Configuration Manager 评估组中的九个规则。 这些规则只是 Microsoft 顶级支持在服务中心提供的众多检查中的一个例子。<!-- 3607758 -->

  - Active Directory 安全组发现配置为过于频繁地运行
  - Active Directory 系统发现配置为过于频繁地运行
  - Active Directory 用户发现配置为过于频繁地运行
  - 集合仅限于“所有系统”或“所有用户”
  - 已禁用检测信号发现
  - 已启用长期运行的集合查询以实现增量更新
  - 减少分发点上的应用程序和包数量
  - 辅助站点安装问题
  - 将所有站点更新到同一版本

- 云服务组中的两个附加规则可帮助配置站点以便添加安全 HTTPS 通信：<!-- 6268489 -->

  - 没有正确 HTTPS 配置的站点
  - 未上传到 Azure AD 的设备

有关详细信息，请参阅[管理见解](../../servers/manage/management-insights.md)。

### <a name="improvements-to-administration-service"></a>管理服务的改进

<!-- 5728365 -->

管理服务是 SMS 提供程序的 REST API。 以前，必须实现以下其中一个依赖项：

- 为整个站点启用增强的 HTTP
- 将基于 PKI 的证书手动绑定到托管 SMS 提供程序角色的服务器上的 IIS

从此版本开始，管理服务会自动使用该站点的自签名证书。 此更改有助于减少摩擦，使管理服务更易于使用。 站点始终会生成此证书。 设置为“将 Configuration Manager 生成的证书用于 HTTP 站点系统”的增强 HTTP 站点仅控制站点系统是否使用该证书。 现在，管理服务会忽略此站点设置，因为它始终使用站点的证书，即使没有其他站点系统使用增强的 HTTP 也是如此。 仍可以使用基于 PKI 的服务器身份验证证书。

有关详细信息，请参阅以下新文章：

- [什么是管理服务？](../../../develop/adminservice/overview.md)
- [如何设置管理服务](../../../develop/adminservice/set-up.md)

### <a name="proxy-support-for-azure-active-directory-discovery-and-group-sync"></a>对 Azure Active Directory 发现和组同步的代理支持

<!-- 5913817 -->

站点系统的代理设置（包括身份验证）现在由以下各项使用：

- Azure Active Directory (Azure AD) 用户发现
- Azure AD 用户组发现
- 将集合成员身份结果同步到 Azure Active Directory 组

有关详细信息，请参阅[代理服务器支持](../network/proxy-server-support.md#bkmk_other)。

## <a name="cloud-attached-management"></a><a name="bkmk_cloud"></a>云附加管理

### <a name="critical-status-message-shows-server-connection-errors-to-required-endpoints"></a>严重状态消息显示了所需终结点的服务器连接错误

<!-- 5566763 -->

如果 Configuration Manager 站点服务器无法连接到云服务所需的终结点，则会引发严重状态消息 ID 11488。 站点服务器无法连接到服务时，SMS_SERVICE_CONNECTOR 组件状态将更改为严重。 在 Configuration Manager 控制台的“组件状态”节点中查看详细状态。

### <a name="token-based-authentication-for-cloud-management-gateway"></a>为云管理网关进行基于令牌的身份验证

<!-- 5686290 -->

云管理网关 (CMG) 支持许多类型的客户端，但是即使使用增强的 HTTP，这些客户端也需要客户端身份验证证书。 如果客户端不经常连接到内部网络、无法加入 Azure Active Directory (Azure AD) 且无法安装 PKI 颁发的证书的基于 Internet，则在其上预配此证书要求可能非常困难。

Configuration Manager 通过以下方法扩展其设备支持：

- 在内部网络上注册以获得唯一令牌
- 为基于 Internet 的设备创建批量注册令牌

有关详细信息，请参阅[基于令牌的 CMG 身份验证](../../clients/deploy/deploy-clients-cmg-token.md)。

### <a name="microsoft-endpoint-configuration-manager-cloud-features"></a>Microsoft Endpoint Configuration Manager 云功能

<!--5834830-->

如果可以在 Microsoft Endpoint Manager 管理中心或本地 Configuration Manager 安装的附加云服务中使用基于云的新功能，则现在可以在 Configuration Manager 控制台中选择加入这些新功能。 要详细了解如何在 Configuration Manager 控制台中启用这些功能，请参阅[启用更新中的可选功能](../../servers/manage/install-in-console-updates.md#bkmk_options)。

## <a name="desktop-analytics"></a><a name="bkmk_da"></a> 桌面分析

有关桌面分析云服务每月更改的详细信息，请参阅[桌面分析中的新增功能](../../../desktop-analytics/whats-new.md)。

### <a name="connection-health-dashboard-shows-client-connection-issues"></a>连接运行状况仪表板显示了客户端连接问题

使用 Configuration Manager 中的桌面分析连接运行状况仪表板监视客户端的连接运行状况。 它现在可帮助你在两个领域更轻松地确定客户端代理配置问题：

- **终结点连接性检查**：如果客户端无法访问所需的终结点，你会在仪表板中看到配置警报。 向下钻取以查看客户端因代理配置问题而无法连接到的终结点。<!-- 4963230 -->

- **连接性状态**：如果客户端使用代理服务器访问桌面分析云服务，Configuration Manager 现在会显示来自客户端的代理身份验证问题。 向下钻取以查看由于代理身份验证而无法注册的客户端。<!-- 4963383 -->

有关详细信息，请参阅[监视连接运行状况](../../../desktop-analytics/monitor-connection-health.md)。

## <a name="real-time-management"></a><a name="bkmk_real"></a>实时管理

### <a name="improvements-to-cmpivot"></a>CMPivot 的改进

<!-- 5870934 -->

我们简化了 CMPivot 实体的导航。 现在可以搜索 CMPivot 实体。 还添加了新图标，以轻松地区分实体和实体对象类型。

有关详细信息，请参阅 [CMPivot](../../servers/manage/cmpivot-changes.md#bkmk_2002)。

## <a name="content-management"></a><a name="bkmk_content"></a>内容管理

### <a name="exclude-certain-subnets-for-peer-content-download"></a>为对等内容下载排除某些子网

<!-- 3555777 -->

边界组包括以下对等下载适用的选项：对等下载期间，只能使用同一子网内的对等设备。 如果启用此选项，管理点中的内容位置列表只包含与客户端位于同一子网和边界组中的对等源。 根据网络的配置，现在可以排除某些子网以进行匹配。 例如，你想要包含边界，但要排除特定的 VPN 子网。

有关详细信息，请参阅[边界组选项](../../servers/deploy/configure/boundary-groups.md#bkmk_bgoptions)。

### <a name="proxy-support-for-microsoft-connected-cache"></a>Microsoft 联网缓存的代理支持

<!-- 5856396 -->

如果环境使用未经身份验证的代理服务器进行 Internet 访问，则现在为 Microsoft 联网缓存启用了 Configuration Manager 分发点时，它可以通过该代理进行通信。 有关详细信息，请参阅 [Microsoft Connected Cache](../hierarchy/microsoft-connected-cache.md)。

## <a name="client-management"></a><a name="bkmk_client"></a> 客户端管理

### <a name="client-log-collection"></a>客户端日志收集

<!-- 4226618 -->

现可通过从 Configuration Manager 控制台发送客户端通知操作，触发客户端设备将其客户端日志上传到站点服务器。

有关详细信息，请参阅[客户端通知](../../clients/manage/client-notification.md#client-diagnostics)。

### <a name="wake-up-a-device-from-the-central-administration-site"></a>从管理中心站点唤醒设备

<!-- 6030715 -->

在管理中心站点 (CAS) 的“设备”或“设备集合”节点中，你现在可以使用客户端通知操作唤醒设备。 此操作以前只能在主站点上执行。

有关详细信息，请参阅[如何配置 LAN 唤醒](../../clients/deploy/configure-wake-on-lan.md#bkmk_wol-1810)。

### <a name="improvements-to-support-for-arm64-devices"></a>对 ARM64 设备的支持的改进

<!--5954175-->

可在具有要求规则或适用性列表的对象上的受支持 OS 版本列表中找到“所有 Windows 10 (ARM64)”平台。

> [!NOTE]
> 如果之前选择了顶层 Windows 10 平台，则此操作会自动选择“所有 Windows 10 (64 位)”和“所有 Windows 10 (32 位)”  。 不会自动选择此新平台。 如果要添加“所有 Windows 10 (ARM64)”，请在列表中手动选择它。

要详细了解 Configuration Manager 对 ARM64 设备的支持，请参阅 [ARM64 上的 Windows 10](../configs/support-for-windows-10.md#bkmk_arm64)。

### <a name="track-configuration-item-remediations"></a>跟踪配置项目修正
<!--4261411-->
现在可在配置项目符合性规则上“跟踪修正历史记录(如支持)”。 启用此选项后，客户端上发生的配置项目的任何修正都会生成状态消息。 历史记录存储在 Configuration Manager 数据库中。

有关详细信息，请参阅[为使用 Configuration Manager 客户端管理的 Windows 台式机和服务器计算机创建自定义配置项目](../../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md#bkmk_track)。

<!-- ## <a name="bkmk_comgmt"></a> Co-management -->

## <a name="application-management"></a><a name="bkmk_app"></a>应用程序管理

### <a name="microsoft-edge-management-dashboard"></a>Microsoft Edge 管理仪表板

<!-- 3871913 -->

Microsoft Edge 管理仪表板可让你深入了解 Microsoft Edge 和其他浏览器的使用情况。 在此仪表板中，你可以：

- 查看已安装 Microsoft Edge 的设备数
- 查看安装了不同 Microsoft Edge 版本的客户端数
- 查看跨设备安装的浏览器
- 查看设备的首选浏览器

在“软件库”工作区中，单击“Microsoft Edge 管理”以查看仪表板。 单击“浏览”并选择其他集合，更改关系图数据的集合。 下拉列表中默认包含五个最大的集合。 如果选择的集合不在列表中，则新选择的集合将位于下拉列表中的底部位置。

有关详细信息，请参阅 [Microsoft Edge 管理](../../../apps/deploy-use/deploy-edge.md#bkmk_edge-dash)。

### <a name="improvements-to-microsoft-edge-management"></a>对 Microsoft Edge 管理的改进

<!-- 4561024 -->

你现在可以创建一个设置为接收自动更新而不是禁用自动更新的 Microsoft Edge 应用程序。 此更改允许你选择使用 Configuration Manager 管理 Microsoft Edge 更新或允许 Microsoft Edge 自动更新。 创建应用程序时，选择“Microsoft Edge 设置”页上的“允许 Microsoft Edge 自动更新最终用户设备上的客户端版本”。

有关详细信息，请参阅 [Microsoft Edge 管理](../../../apps/deploy-use/deploy-edge.md#bkmk_autoupdate)。

### <a name="task-sequence-as-an-app-model-deployment-type"></a>作为应用模型部署类型的任务序列

<!-- 3555953 -->

现在可以通过应用程序模型使用任务序列安装复杂的应用程序。 将部署类型添加到作为任务序列的应用，以安装或卸载应用。 此功能提供以下行为：

- 在“软件中心”中使用图标显示应用任务序列。 通过图标，用户可以更轻松地查找和识别应用任务序列。

- 为应用任务序列定义其他元数据，包括本地化信息

有关详细信息，请参阅[创建 Windows 应用程序](../../../apps/get-started/creating-windows-applications.md#bkmk_tsdt)。

## <a name="os-deployment"></a><a name="bkmk_osd"></a> OS 部署

### <a name="bootstrap-a-task-sequence-immediately-after-client-registration"></a>在客户端注册后立即启动任务序列

<!-- 5526972 -->

安装并注册新的 Configuration Manager 客户端，并向其部署任务序列时，很难确定它将在注册后多长时间运行该任务序列。 此版本引入了一个新的客户端安装属性，可使用它在客户端成功注册到站点后在该客户端上启动任务序列。

有关详细信息，请参阅[关于客户端安装属性 - 预配](../../clients/deploy/about-client-installation-properties.md#provisionts)。

### <a name="improvements-to-check-readiness-task-sequence-step"></a>准备情况检查任务序列步骤的改进

<!-- 6005561 -->

现在可以在“准备情况检查”任务序列步骤中验证更多设备属性。 在任务序列中使用此步骤来验证目标计算机是否满足前提条件。

- 当前操作系统的体系结构
- 最低操作系统版本
- 最高操作系统版本
- 最低客户端版本
- 当前操作系统的语言
- 交流电源已接通
- 网络适配器已连接且不是无线

有关详细信息，请参阅[任务序列步骤 - 准备情况检查](../../../osd/understand/task-sequence-steps.md#BKMK_CheckReadiness)。

### <a name="improvements-to-task-sequence-progress"></a>任务序列进度的改进

<!-- 5932692 -->

任务序列进度窗口现在包括以下改进：

- 可以启用它以显示当前步骤编号、步骤总数和完成百分比
- 增加了窗口的宽度，为你提供更多空间，以便更好地在单个行中显示组织名称

有关详细信息，请参阅[操作系统部署的用户体验](../../../osd/understand/user-experience.md#task-sequence-progress)。

### <a name="improvements-to-os-deployment"></a>对 OS 部署的改进

此版本包括对 OS 部署的以下改进：

- 任务序列环境包含了新的只读变量 `_TSSecureBoot`。<!--5842295--> 使用此变量可确定启用了 UEFI 的设备上安全启动的状态。 有关详细信息，请参阅 [_TSSecureBoot](../../../osd/understand/task-sequence-variables.md#TSSecureBoot)。

- 设置任务序列变量来配置“运行命令行”和“运行 PowerShell 脚本”步骤的用户上下文。<!-- 5573175 --> 有关详细信息，请参阅 [SMSTSRunCommandLineAsUser](../../../osd/understand/task-sequence-variables.md#SMSTSRunCommandLineAsUser) 和 [SMSTSRunPowerShellAsUser](../../../osd/understand/task-sequence-variables.md#SMSTSRunPowerShellAsUser)。

- 在“运行 PowerShell 脚本”步骤中，现在可以将“参数”属性设置为变量。<!-- 5690481 --> 有关详细信息，请参阅[运行 PowerShell 脚本](../../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript)。

- Configuration Manager PXE 响应程序现在可向站点服务器发送状态消息。 此更改使你可以更轻松地对使用此服务的 OS 部署进行故障排除。<!-- 5568051 -->

<!-- ## <a name="bkmk_userxp"></a> Software Center -->

## <a name="software-updates"></a><a name="bkmk_sum"></a>软件更新

### <a name="orchestration-groups"></a>业务流程组

<!-- 3098816 -->

创建一个业务流程组，以便更好地控制设备上软件更新的部署。 许多服务器管理员需要认真管理特定工作负载的更新，并在这些工作负载之间实现行为自动化。

业务流程组使你可以灵活地根据百分比、特定数量或显式顺序更新设备。 你还可以在设备运行更新部署之前和之后运行 PowerShell 脚本。

业务流程组的成员可以是任何 Configuration Manager 客户端，而不仅仅是服务器。 业务流程组规则适用于所有软件更新部署到包含业务流程组成员的任何集合的设备。 其他部署行为仍适用。 例如，维护时段和部署计划。

有关详细信息，请参阅[业务流程组](../../../sum/deploy-use/orchestration-groups.md)。

### <a name="evaluate-software-updates-after-a-servicing-stack-update"></a>在服务堆栈更新后评估软件更新

<!-- 4639943 -->

Configuration Manager 现在可检测服务堆栈更新 (SSU) 是否为多个更新安装的一部分。 检测到 SSU 后，系统会先安装它。 安装 SSU 后，将运行软件更新评估周期以安装剩余更新。 此更改允许在服务堆栈更新后安装相关累积更新。 设备不需要在安装之间重启，你也不需要创建其他维护时段。 仅对非用户启动的安装先安装 SSU。 例如，如果用户从软件中心启动多个更新安装，则可能不会先安装 SSU。

有关详细信息，请参阅[规划软件更新](../../../sum/plan-design/plan-for-software-updates.md#bkmk_ssu)。

### <a name="office-365-updates-for-disconnected-software-update-points"></a>用于断开连接的软件更新点的 Office 365 更新

<!-- 4065163 -->

可使用新工具将 Office 365 更新从连接了 Internet 的 WSUS 服务器导入到已断开连接的 Configuration Manager 环境中。 以前，当你导出和导入在已断开连接的环境中更新的软件的元数据时，无法部署 Office 365 更新。 Office 365 更新需要从 Office API 和 Office CDN 下载的其他元数据，这对于已断开连接的环境是不可能的。

有关详细信息，请参阅[从断开连接的软件更新点同步 Office 365 更新](../../../sum/get-started/synchronize-office-updates-disconnected.md)。

<!-- ## <a name="bkmk_o365"></a> Office management -->

## <a name="protection"></a><a name="bkmk_protect"></a> 保护

### <a name="expand-microsoft-defender-advanced-threat-protection-atp-onboarding"></a>扩展 Microsoft Defender 高级威胁防护(ATP) 加入支持
 
<!-- 5229962 -->
Configuration Manager 扩展了对将设备加入 Microsoft Defender ATP 的支持。 有关详细信息，请参阅 [Microsoft Defender 高级威胁防护](../../../protect/deploy-use/defender-advanced-threat-protection.md)。

### <a name="onboard-configuration-manager-clients-to-microsoft-defender-atp-via-the-microsoft-endpoint-manager-admin-center"></a><a name="bkmk_atp"></a> 通过 Microsoft Endpoint Manager 管理中心将 Configuration Manager 客户端加入 Microsoft Defender ATP
<!--5691658-->
现在可以将 Microsoft Defender ATP 终结点检测和响应 (EDR) 加入策略部署到 Configuration Manager 托管客户端。 这些客户端不需要 Azure AD 或 MDM 注册，并且策略是针对 ConfigMgr 集合而不是 Azure AD 组。

此功能使客户可以通过单一管理体验（Microsoft Endpoint Manager 管理中心）来管理 Intune MDM 和 Configuration Manager 客户端 EDR/ATP 加入。 有关详细信息，请参阅 [Intune 中关于终结点安全的终结点检测和响应策略](../../../../intune/protect/endpoint-security-edr-policy.md)。

> [!Important]
> 必须在环境中安装修补程序汇总 [KB4563473](https://support.microsoft.com/help/4563473)，才能使用此功能。

### <a name="improvements-to-bitlocker-management"></a>对 BitLocker 管理的改进

- BitLocker 管理策略现在包含其他设置，包括固定驱动器和可移动驱动器的策略。<!-- 5925683 --> 有关详细信息，请参阅 [BitLocker 设置参考](../../../protect/tech-ref/bitlocker/settings.md)。

- 在 Configuration Manager 当前分支版本 1910 中，要集成 BitLocker 恢复服务，需要使用 HTTPS 启用管理点。 需要 HTTPS 连接才能加密网络中从 Configuration Manager 客户端到管理点的恢复密钥。 对于许多客户而言，为 HTTPS 配置管理点和所有客户端可能比较困难。

    从此版本开始，只有托管恢复服务的 IIS 网站才需要满足 HTTPS 要求，而不是整个管理点角色都需要满足。 此更改放宽了证书要求，并且仍会加密传输中的恢复密钥。<!-- 5925660 --> 有关详细信息，请参阅[加密恢复数据](../../../protect/deploy-use/bitlocker/encrypt-recovery-data.md)。

## <a name="reporting"></a><a name="bkmk_report"></a>报表

### <a name="integrate-with-power-bi-report-server"></a>与 Power BI 报表服务器集成

<!-- 3721603 -->

你现在可以将 Power BI 报表服务器与 Configuration Manager 报告集成。 这种集成提供了现代可视化效果和更好的性能。 它为 Power BI 报表添加了控制台支持，这与 SQL Server Reporting Services 中已存在的报表类似。

有关详细信息，请参阅[与 Power BI 报表服务器集成](../../servers/manage/powerbi-report-server.md)。

## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Configuration Manager 控制台

### <a name="show-boundary-groups-for-devices"></a>显示设备的边界组

<!--6521835-->

为了帮助你通过边界组更好地对设备行为进行故障排除，现在可以查看特定设备的边界组。 在“设备”节点中，或在显示某个“设备集合”的成员时，将新的“边界组”列添加到列表视图中  。

有关详细信息，请参阅[边界组](../../servers/deploy/configure/boundary-groups.md#bkmk_show-boundary)。

### <a name="send-a-smile-improvements"></a>发送笑脸改进

<!-- 5891852 -->

使用“发送笑脸”或“发送哭脸”时，提交反馈后将创建一条状态消息。 此改进将记录以下内容：

- 提交反馈的时间
- 提交反馈的人员
- 反馈 ID
- 反馈是否提交成功

ID 为 53900 的状态消息表示提交成功，而 53901 表示提交失败。

有关详细信息，请参阅[产品反馈](../../understand/find-help.md#BKMK_1806Feedback)。

### <a name="search-all-subfolders-for-configuration-items-and-configuration-baselines"></a>搜索配置项目和配置基线的所有子文件夹

<!--5891241-->

与以前的版本中的改进类似，可以从“配置项目”和“配置基线”节点使用“所有子文件夹”搜索选项  。

### <a name="community-hub"></a>社区中心

<!--3555935, 3555936-->

（2020 年 6 月首次引入）

多年来，IT 管理员社区积累了丰富的知识。 我们打造了 Configuration Manager 社区中心，以方便彼此共享，而不必从头开始重新创建脚本和报告等项目。 通过借鉴其他人的工作，你可以节省工作小时数。 社区中心支持你和其他人在相互借鉴各自工作的基础上生成内容，从而发展创造力。 GitHub 已构建面向全行业的共享流程和工具。 现在，社区中心将直接在 Configuration Manager 控制台中利用这些工具，作为推动新社区发展的基础组件。 在初始版本中，社区中心内提供的内容将仅由 Microsoft 上传。

有关详细信息，请参阅[社区中心和 GitHub](../../servers/manage/community-hub.md)。

## <a name="tools"></a><a name="bkmk_tools"></a> 工具

### <a name="onetrace-log-groups"></a>OneTrace 日志组

<!-- 5559993 -->

OneTrace 现在支持可自定义的日志组，与支持中心的功能类似。 日志组允许打开单个方案的所有日志文件。 OneTrace 当前包括以下方案的组：

- 应用程序管理
- 合规性设置（也称为所需的配置管理）
- 软件更新

有关详细信息，请参阅[支持中心 OneTrace](../../support/support-center-onetrace.md)。

### <a name="improvements-to-extend-and-migrate-on-premises-site-to-microsoft-azure"></a><a name="bkmk_extend"></a>对扩展本地站点并将其迁移到 Microsoft Azure 的改进
<!--5665775, 6307931-->
用于扩展本地站点并将其迁移到 Microsoft Azure 的工具现在支持在单个 Azure 虚拟机上预配多个站点系统角色。 初始 Azure 虚拟机部署完成后，可以添加站点系统角色。

有关详细信息，请参阅[将本地站点扩展并迁移到 Microsoft Azure](../../support/azure-migration-tool.md#bkmk_add_role)。

## <a name="other-updates"></a>其他更新

从此版本开始，以下功能不再是[预发行版](../../servers/manage/pre-release-features.md)：

- [Azure Active Directory 用户组发现](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco)<!--3611956-->
- [将集合成员身份结果同步到 Azure Active Directory](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync)<!--3607475-->
- [CMPivot 独立应用](../../servers/manage/cmpivot.md#bkmk_standalone)<!--3555890/4692885-->
- [适用于共同托管设备的客户端应用](../../../comanage/workloads.md#client-apps)（以前称为适用于共同托管设备的移动应用）<!-- 1357892/3600959 -->

有关 Configuration Manager 的 Windows PowerShell cmdlet 更改的详细信息，请参阅 [PowerShell 版本 2002 发行说明](https://docs.microsoft.com/powershell/sccm/2002-release-notes?view=sccm-ps)。

有关对管理服务 REST API 的更改的详细信息，请参阅[管理服务发行说明](../../../develop/adminservice/release-notes.md#bkmk_2002)。

除了新增功能外，这一版还有其他变化（如缺陷修复）。 有关详细信息，请参阅 [Configuration Manager Current Branch（版本 2002）的更改摘要](https://support.microsoft.com/help/4556203)。

从 2020 年 7 月 15 日开始，以下更新汇总 (4560496) 在控制台中可用：[Microsoft Endpoint Configuration Manager 版本 2002 的更新汇总](https://support.microsoft.com/help/4560496)。

### <a name="hotfixes"></a>修补程序

以下附加修补程序可用于解决特定问题：

| ID | 标题 | 日期 | 控制台内部 |
|---------|---------|---------|---------|
| [4575339](https://support.microsoft.com/help/4575339) | 设备在 Microsoft Endpoint Configuration Manager 管理中心出现两次 | 2020 年 7 月 23 日 | 否 |
| [4575774](https://support.microsoft.com/help/4575774) | New-CMTSStepPrestartCheck cmdlet 在 Configuration Manager 版本 2002 中失败 | 2020 年 7 月 24 日 | 否 |
| [4576782](https://support.microsoft.com/help/4576782) | 在 Microsoft Endpoint Manager 管理中心内，“应用程序”边栏选项卡超时 | 2020 年 8 月11 日 | 否 |

<!--
> [!NOTE]
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->

## <a name="next-steps"></a>后续步骤

<!-- At this time, version 2002 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-2002.md#early-update-ring). -->

自 2020 年 5 月 11 日起，版本 2002 公开发布，可供所有用户安装。

准备好安装此版本时，请参阅[安装 Configuration Manager 的更新](../../servers/manage/updates.md)和[用于安装更新 2002 的清单](../../servers/manage/checklist-for-installing-update-2002.md)。

> [!TIP]
> 若要安装新站点，请使用 Configuration Manager 的基准版本。
>
> 了解详细信息：
>
> - [安装新站点](../../servers/deploy/install/installing-sites.md)
> - [基准和更新版本](../../servers/manage/updates.md#bkmk_Baselines)

关于已知的重要问题，请参阅[发行说明](../../servers/deploy/install/release-notes.md)。

更新站点后，还可以查看[更新后清单](../../servers/manage/checklist-for-installing-update-2002.md#post-update-checklist)。
