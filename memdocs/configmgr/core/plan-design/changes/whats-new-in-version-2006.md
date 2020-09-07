---
title: 2006 版中的新增功能
titleSuffix: Configuration Manager
description: 详细了解 Configuration Manager Current Branch 版本 2006 中引入的更改和新功能。
ms.date: 09/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4b071746-61e1-404b-8053-60978de028a7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3c061236202e685a6b59eeca3254a80cc1ddabf9
ms.sourcegitcommit: 9d5c7a5e6ec430dc02d6d345028f6b29f6579b20
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89385356"
---
# <a name="whats-new-in-version-2006-of-configuration-manager-current-branch"></a>Configuration Manager Current Branch 版本 2006 的新变化

适用范围：  Configuration Manager (Current Branch)

用于 Configuration Manager Current Branch 的更新 2006 作为控制台内更新提供。 将此更新应用于运行版本 1810 或更高版本的站点。 <!-- baseline only statement:When installing a new site, it's also available as a baseline version. -->本文总结了 Configuration Manager 版本 2006 中的更改和新功能。

始终查看安装此更新的最新清单。 有关详细信息，请参阅[用于安装更新 2006 的清单](../../servers/manage/checklist-for-installing-update-2006.md)。 更新站点后，还可以查看[更新后清单](../../servers/manage/checklist-for-installing-update-2006.md#post-update-checklist)。

若要利用 Configuration Manager 的新功能，更新站点后，还请将客户端更新到最新版本。 尽管在更新站点和控制台时 Configuration Manager 控制台中会显示新功能，但只有在客户端版本也是最新版本之后，完整方案才能正常运行。

> [!TIP]
> 若要在此页面更新时收到通知，请将以下 URL 复制并粘贴到 RSS 源阅读器中：`https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+2006+-+Configuration+Manager%22&locale=en-us`

## <a name="microsoft-endpoint-manager-tenant-attach"></a><a name="bkmk_tenant"></a> Microsoft Endpoint Manager 租户附加

### <a name="tenant-attach-microsoft-defender-antivirus-policies-in-the-microsoft-endpoint-manager-admin-center"></a><a name="bkmk_atp"></a> 租户附加：Microsoft Endpoint Manager 管理中心的 Microsoft Defender 防病毒
<!--4812909-->
现可在 Microsoft Endpoint Manager 控制台中创建 Microsoft Defender 防病毒策略，并将它们部署到 Configuration Manager 集合。 有关详细说明和可用的设置，请参阅以下文章：
- [租户附加：从管理中心将 Configuration Manager 客户端加入 Microsoft Defender ATP（预览）](../../../tenant-attach/atp-onboard.md)
- [租户附加：从管理中心部署终结点安全性防病毒策略（预览）](../../../tenant-attach/deploy-antivirus-policy.md)
- [Microsoft Intune 中租户附加设备的 Microsoft Defender 防病毒策略的设置](../../../../intune/protect/antivirus-microsoft-defender-settings-windows-tenant-attach.md?toc=/mem/configmgr/tenant-attach/toc.json&bc=/mem/configmgr/tenant-attach/breadcrumb/toc.json)。 

### <a name="install-applications-from-the-admin-center"></a>从管理中心安装应用程序
<!--7518897, 6024389-->
可以从 Microsoft Endpoint Manager 管理中心为租户附加的设备实时启动应用程序安装。 自 Configuration Manager 版本 2006 起，可用于设备的应用程序列表还包括部署到设备的当前登录用户的应用程序。 有关详细信息，请参阅[租户附加：从管理中心安装应用程序](../../../tenant-attach/applications.md)中的说明进行操作。  

### <a name="import-previously-created-azure-ad-application-during-tenant-attach-onboarding"></a> 在租户附加加入期间导入以前创建的 Azure AD 应用程序
<!--6479246-->
在新加入期间，管理员可以在加入租户附加的过程中指定以前创建的应用程序。 有关详细信息，请参阅 [Microsoft Endpoint Manager 租户附加：设备同步和设备操作](../../../tenant-attach/device-sync-actions.md#bkmk_aad_app)。

## <a name="endpoint-analytics"></a><a name="bkmk_ea"></a> 终结点分析

### <a name="endpoint-analytics-data-collection-enabled-by-default"></a>终结点分析数据收集是默认启用的
<!--7065447, 7741111-->
“启用终结点分析数据收集”客户端设置现在是默认启用的。 借助此设置，托管终结点可以将数据（如启动性能见解）发送到 Configuration Manager 站点服务器。 此更改只影响本地数据收集。 除非[在 Configuration Manager 中启用数据上传](../../../../analytics/enroll-configmgr.md#bkmk_cm_upload)，否则终结点分析数据不会上传到 Microsoft Endpoint Manager 管理中心。 新的默认值适用于默认客户端设置以及在升级到版本 2006 后创建的任何自定义客户端设置。

- 若要从版本 2002 升级到版本 2006，现有的自定义客户端设置值将被保留。 在 Configuration Manager 版本 2002 中，“启用终结点分析数据收集”的默认值为“否”。
- 若要从 Configuration Manager 版本 1910 或更低版本升级到版本 2006，则任何包含“计算机代理”设置组的预先存在的自定义客户端设置将继承“启用终结点分析数据收集”的新默认值“是”。

有关详细信息，请参阅[在 Configuration Manager 中配置终结点分析数据收集](../../../../analytics/enroll-configmgr.md#bkmk_cm_upload)。

## <a name="site-infrastructure"></a><a name="bkmk_infra"></a>站点基础结构

### <a name="vpn-boundary-type"></a> VPN 边界类型

<!--7020519-->

为简化远程客户端管理，现在可以为 VPN 创建一个新的边界类型。 过去，必须根据 IP 地址或子网为 VPN 客户端创建边界。 由于子网配置或 VPN 设计方面的原因，此配置可能具有挑战性或不可能实现。

现在，当客户端发送位置请求时，它会包含有关其网络配置的其他信息。 根据此信息，服务器确定客户端是否在 VPN 上。

有关详细信息，请参阅[定义边界](../../servers/deploy/configure/boundaries.md)。

### <a name="management-insights-to-optimize-for-remote-workers"></a>针对远程工作者进行优化的管理见解

<!--6982226-->

此版本新增了一组管理见解，即“更适合远程工作者”。 这些新见解可帮助你为远程工作者创造更好的体验并降低基础结构负载。 此版本中的见解主要侧重于 VPN：

- **定义 VPN 边界组**
- **将 VPN 连接的客户端配置为首选基于云的内容源**
- **对 VPN 连接的客户端禁用对等内容共享**

有关详细信息，请参阅[管理见解](../../servers/manage/management-insights.md)。

### <a name="improved-support-for-windows-virtual-desktop"></a>改进了对 Windows 虚拟桌面的支持

<!--6527576-->

可在具有要求规则或适用性列表的对象上的受支持 OS 版本列表中找到“Windows 10 企业版多会话”平台。

有关 Configuration Manager 对 Windows 虚拟桌面的支持的详细信息，请参阅[客户端和设备支持的 OS 版本](../configs/supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop)。

### <a name="intranet-clients-can-use-a-cmg-software-update-point"></a>Intranet 客户端可以使用 CMG 软件更新点
<!--7102873-->
Intranet 客户端现在可以在分配到边界组后访问 CMG 软件更新点。 有关详细信息，请参阅[配置边界组](../../servers/deploy/configure/boundary-groups.md#bkmk_cmg-sup)。

## <a name="cloud-attached-management"></a><a name="bkmk_cloud"></a>云附加管理

### <a name="use-the-company-portal-app-on-co-managed-devices"></a> 在共同管理的设备上使用公司门户应用

<!--CMADO-3601237,INADO-4297660-->

公司门户现在是 Microsoft Endpoint Manager 的跨平台应用门户体验。 通过将共同管理的设备配置为同时使用公司门户，你可以在所有设备上提供一致的用户体验。

有关详细信息，请参阅[在共同受管理设备上使用公司门户应用](../../../comanage/company-portal.md)。

### <a name="use-microsoft-azure-china-21vianet-for-co-management"></a>使用 Microsoft Azure 中国世纪互联进行共同管理
<!--7133238-->
在启用共同管理时，现在可以选择“Azure 中国云”作为 Azure 环境。 有关详细信息，请参阅[如何启用共同管理](../../../comanage/how-to-enable.md)。

### <a name="notification-for-azure-ad-app-secret-key-expiration"></a>Azure AD 应用密钥过期通知

<!--6386392-->

如果你将 Azure 服务配置为云附加你的站点，则 Configuration Manager 控制台现在会对以下情况显示通知：

- 一个或多个 Azure AD 应用密钥即将过期时
- 一个或多个 Azure AD 应用密钥已过期时

有关详细信息，请参阅[续订密钥](../../servers/deploy/configure/azure-services-wizard.md#bkmk_renew)。

### <a name="desktop-analytics"></a>桌面分析

有关桌面分析云服务每月更改的详细信息，请参阅[桌面分析中的新增功能](../../../desktop-analytics/whats-new.md)。

#### <a name="change-to-diagnostic-data-labels"></a>更改了诊断数据标签

<!-- 7363467 -->

为了更好地满足 Windows 诊断数据的桌面分析需求，这些设置新增了标签：

| 版本 2006 及更高版本 | 版本 2002 及更低版本 |
|---------|---------|
| 必需 | 基本 |
| 可选(受限) | 增强(受限) |
| 不适用 | 增强版 |
| 可选 | 完全 |

如果你之前在“增强”级别配置过任何设备，那么当你升级到版本 2006 时，这些设备将恢复为“可选(受限)”。 然后，它们将向 Microsoft 发送更少的数据。 此更改应该不会影响桌面分析中显示的内容。

有关详细信息，请参阅[为桌面分析启用数据共享](../../../desktop-analytics/enable-data-sharing.md)。

## <a name="real-time-management"></a><a name="bkmk_real"></a>实时管理

### <a name="improvements-to-cmpivot"></a>CMPivot 的改进
<!--6518631-->
对 CMPivot 进行了以下改进：

- 聚合了控制台中的 CMPivot 和 CMPivot 独立应用
- 可以在单台或多台设备中运行 CMPivot，而不必选择或创建集合
- 从 CMPivot 查询结果中，可以选择单台或多台设备，然后启动限定为包含你所选设备的单独 CMPivot 实例。

有关详细信息，请参阅[自版本 2006 起的 CMPivot](../../servers/manage/cmpivot-changes.md#bkmk_2006)。

## <a name="client-management"></a><a name="bkmk_client"></a> 客户端管理

### <a name="install-and-upgrade-the-client-on-a-metered-connection"></a> 使用按流量计费的连接来安装和升级客户端

<!--6976145-->

以前，如果设备连接到按流量计费的网络，则不会安装新客户端。 仅在允许所有客户端通信时才会升级现有客户端。 对于经常在按流量计费的网络上漫游的设备，它们将不受管理或使用较旧的客户端版本。 自此版本起，当你将客户端设置“客户端通过按流量计费的 Internet 连接进行通信”设置为“允许”或“限制”时，可以安装和升级客户端。 借助此行为，可以不断更新客户端，但仍管理通过按流量计费的网络进行的客户端通信。

若要为新客户端安装定义行为，有一个新的 ccmsetup 参数“/AllowMetered”。 如果针对 ccmsetup 允许客户端在按流量计费的网络上进行通信，该客户端将下载内容、向站点注册并下载初始策略。 其他客户端通信都将遵循该策略中的客户端设置配置。

有关详细信息，请参阅下列文章：

- [关于客户端设置](../../clients/deploy/about-client-settings.md#client-communication-on-metered-internet-connections)
- [关于客户端安装参数和属性](../../clients/deploy/about-client-installation-properties.md#allowmetered)

### <a name="improvements-to-managing-device-restarts"></a>对管理设备重启的改进

<!--3601213-->

Configuration Manager 提供了许多选项来管理设备重启和重启通知。 现在可以配置客户端设置，以防设备在部署需要时自动重启。 此设置让你在独特的情况下有更多的控制。 由于“Configuration Manager 可强制设备重启”客户端设置是默认启用的，因此 Configuration Manager 仍可强制设备重启。 此设置只适用于需要重启的应用程序、软件更新和包部署。

有关详细信息，请参阅[设备重启通知](../../clients/deploy/device-restart-notifications.md)。

## <a name="application-management"></a><a name="bkmk_app"></a>应用程序管理

### <a name="improvements-to-available-apps-via-cmg"></a>通过 CMG 改进可用应用

<!--6935376-->
此版本修复了软件中心和 Azure Active Directory (Azure AD) 身份验证的问题。 过去，对于在 intranet 上检测到但通过云管理网关 (CMG) 进行通信的客户端，软件中心使用 Windows 身份验证。 过去无法尝试获取用户可用的应用的列表。 现在，它为加入到 Azure AD 的设备使用了 Azure Active Directory (Azure AD) 标识。 这些设备可以是云加入或混合加入。

有关详细信息，请参阅[部署用户可用的应用](../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications)。

### <a name="microsoft-365-apps-for-enterprise"></a>Microsoft 365 企业应用版
<!--6298093-->
Office 365 专业增强版已于 2020 年 4 月 21 日更名为 Microsoft 365 企业应用版。 自版本 2006 起，引入了以下更改：

- Configuration Manager 控制台已更新，使用了新名称。
  - Microsoft 365 应用版的更新通道名称也已更改。
- 向控制台添加了横幅通知，以便在一个或多个自动部署规则在 Microsoft 365 应用版更新的标题条件中引用过时的通道名称时发送通知。

有关详细信息，请参阅 [Microsoft 365 Apps 通道名称](../../../sum/deploy-use/manage-office-365-proplus-updates.md#bkmk_channel)和[“Microsoft 365 Apps 就绪情况”仪表板](../../../sum/deploy-use/office-365-dashboard.md#bkmk_readiness-dash)。

## <a name="os-deployment"></a><a name="bkmk_osd"></a> OS 部署

### <a name="task-sequence-media-support-for-cloud-based-content"></a> 任务序列媒体对基于云的内容的支持

<!--6209223-->

任务序列媒体现在可以下载基于云的内容。 例如，你向远程办公用户发送一个 USB 密钥来重置其设备映像。 或者是一个安装了本地 PXE 服务器，但你希望设备尽量优先使用云服务的办公室。 启动媒体和 PXE 部署现在可以从基于云的源获取大型 OS 部署内容，而不必再费力地通过 WAN 下载。 例如，允许共享内容的云管理网关 (CMG)。

> [!NOTE]
> 设备仍需要与管理点建立 Intranet 连接。

有关详细信息，请参阅[使用可启动介质通过网络部署 Windows](../../../osd/deploy-use/use-bootable-media-to-deploy-windows-over-the-network.md#support-for-cloud-based-content)。

### <a name="improvements-to-task-sequences-via-cmg"></a> 通过 CMG 改进任务序列

此版本包含以下改进，可将任务序列部署到通过云管理网关 (CMG) 进行通信的设备：

- 支持 OS 部署<!--6997525-->：对于使用启动映像来部署 OS 的任务序列，你可以将其部署到通过 CMG 进行通信的设备。 用户需要从软件中心启动任务序列。 有关详细信息，请参阅[计划 CMG - 规范](../../clients/manage/cmg/plan-cloud-management-gateway.md#specifications)。

- 此版本修复了 Configuration Manager 当前分支版本 2002 的两个[已知问题](../../servers/deploy/install/release-notes.md#task-sequences-cant-run-over-cmg)。<!-- 6983320 --> 现在可以在以下情况下在通过 CMG 通信的设备上运行任务序列：

  - 使用[批量注册令牌](../../clients/deploy/deploy-clients-cmg-token.md)注册的工作组设备

  - 将站点配置为[增强型 HTTP](../hierarchy/enhanced-http.md)，并将管理点配置为 HTTP

### <a name="improvements-to-bitlocker-task-sequence-steps"></a>BitLocker 任务序列步骤的改进

<!--6995601-->

现在可以在“启用 BitLocker”和“预配 BitLocker”任务序列步骤上指定磁盘加密模式。 默认情况下，这些步骤将继续使用 OS 版本的默认加密方法。

“启用 BitLocker”步骤现在还包括“对于没有 TPM 或未启用 TPM 的计算机，跳过此步骤”设置。 如果你启用这项设置，此步骤会在没有 TPM 或没有初始化 TPM 的设备上记录错误，而任务序列会继续执行。 借助此设置，可以更轻松地在无法完全支持 BitLocker 的设备上管理任务序列行为。

有关详细信息，请参阅[任务序列步骤](../../../osd/understand/task-sequence-steps.md)。

### <a name="management-insight-rules-for-os-deployment"></a>操作系统部署的管理见解规则

<!--6982275-->

当任务序列策略的大小超出 32 MB 时，客户端将无法处理此大型策略。 因而客户端将无法运行任务序列部署。 为了帮助你管理任务序列的策略大小，此版本包括以下管理见解：

- **大型任务序列可能会导致超过策略大小上限**

- **任务序列的总策略大小超出策略限制**

> [!TIP]
> 这些规则位于一个用于“操作系统部署”的新组中。  用于**未使用的启动映像**的已有规则现在也位于此组中。

有关详细信息，请参阅[管理见解](../../servers/manage/management-insights.md#operating-system-deployment)。

### <a name="improvements-to-os-deployment"></a>对 OS 部署的改进

此版本对 OS 部署进行了以下额外的改进：

- 使用任务序列变量来指定[格式化磁盘并分区](../../../osd/understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk)步骤的目标。 这个新的变量选项支持具有动态行为的更复杂的任务序列。 例如，自定义脚本可以检测磁盘并根据硬件类型设置变量。 然后，可以使用此步骤的多个实例来配置不同的硬件类型和分区。<!--6610288-->

- [检查就绪情况](../../../osd/understand/task-sequence-steps.md#BKMK_CheckReadiness)步骤现在包含用于确定设备是否使用 UEFI 的检查。 它还包含新增的只读任务序列变量 _TS_CRUEFI。<!--6452769-->

- 如果启用[任务序列进度窗口](../../../osd/understand/user-experience.md#task-sequence-progress)以显示更多详细进度信息，则它现在不会计算已禁用组中的已启用步骤。 此更改有助于使进度估计更加精确。<!--6448412-->

- 之前，在将设备升级到 Windows 10 的任务序列中，在最后的 Windows 配置阶段之一会打开命令提示符窗口。 此窗口位于 Windows 全新体验 (OOBE) 之上，用户可以通过与它交互来中断升级过程。 现在，Configuration Manager 中的 SetupCompleteTemplate.cmd 和 SetupRollbackTemplate.cmd 脚本进行了更改来隐藏此命令提示符窗口。<!--2837795-->

- 一些客户使用 IProgressUI::ShowMessage 方法生成自定义任务序列接口，但它不返回用户响应值。 此版本添加了 [IProgressUI::ShowMessageEx](../../../develop/reference/core/clients/client-classes/iprogressui--showmessageex-method.md) 方法。 此新方法类似于现有方法，但还包括一个新的整数结果变量 pResult。<!--6448458-->

## <a name="protection"></a>保护

### <a name="cmg-support-for-endpoint-protection-policies"></a>对终结点保护策略的 CMG 支持

<!--4773948-->

在云管理网关 (CMG) 具有受支持的终结点保护策略时，设备需要访问本地域控制器。 从此版本开始，通过 CMG 进行通信的客户端可以立即应用终结点保护策略，而无需与 Active Directory 建立活动连接。

有关详细信息，请参阅 [CMG 对 Configuration Manager 功能的支持](../../clients/manage/cmg/plan-cloud-management-gateway.md#support-for-configuration-manager-features)。

### <a name="bitlocker-management-support-for-hierarchies"></a>对层次结构的 BitLocker 管理支持

<!-- 5925693 -->

现在可以在管理中心站点安装 BitLocker 自助服务门户以及管理和监视网站。

有关详细信息，请参阅[创建 BitLocker 门户](../../../protect/deploy-use/bitlocker/setup-websites.md)。

## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Configuration Manager 控制台

### <a name="community-hub-and-github"></a>社区中心和 GitHub
<!--3555935, 3555936, deep link included 4224406-->

（2020 年 6 月首次引入）

多年来，IT 管理员社区积累了丰富的知识。 我们打造了 Configuration Manager 社区中心，以方便彼此共享，而不必从头开始重新创建脚本和报告等项目。 通过借鉴其他人的工作，你可以节省工作小时数。 社区中心支持你和其他人在相互借鉴各自工作的基础上生成内容，从而发展创造力。 GitHub 已构建面向全行业的共享流程和工具。 现在，社区中心将直接在 Configuration Manager 控制台中利用这些工具，作为推动新社区发展的基础组件。 在初始版本中，社区中心内提供的内容将仅由 Microsoft 上传。 

有关详细信息，请参阅[社区中心和 GitHub](../../servers/manage/community-hub.md)。

### <a name="direct-links-to-community-hub-items"></a><a name="bkmk_deeplink"></a> 指向社区中心项的直接链接
<!--4224406-->
可以使用直接链接轻松转到并引用 Configuration Manager 控制台“社区中心”节点内的项。 有关详细信息，请参阅[指向社区中心项的直接链接](../../servers/manage/community-hub.md#bkmk_deeplink)。

### <a name="notifications-from-microsoft"></a>来自 Microsoft 的通知
<!--3953121-->
现在可以选择在 Configuration Manager 控制台中接收来自 Microsoft 的通知。 这些通知可帮助你及时了解新功能或功能更新、对 Configuration Manager 和附加服务所做的更改，以及需要修正操作的问题。

有关详细信息，请参阅[配置站点以接收来自 Microsoft 的消息](../../servers/manage/admin-console-notifications.md#bkmk_msft)。

### <a name="power-bi-sample-reports"></a>Power BI 示例报表
<!--5679791-->

（2020 年 6 月首次引入）

如果你将 Power BI 报表服务器与 Configuration Manager 报表集成在一起，现在就可以使用示例 Power BI 报表了。 下载并安装以下示例报表：

- 软件更新符合性状态
- 软件更新部署状态

有关详细信息，请参阅[安装 Power BI 示例报表](../../servers/manage/powerbi-sample-reports.md)。

<!-- Unused sections in this release:
## Reporting
## <a name="bkmk_userxp"></a> User experience
## <a name="bkmk_sum"></a> Software updates
## Office management
## <a name="bkmk_content"></a> Content management
## <a name="bkmk_comgmt"></a> Co-management
-->

## <a name="deprecated-operating-systems"></a><a name="bkmk_deprecated"></a> 弃用的操作系统

在[已删除和已启用的项](deprecated/removed-and-deprecated.md)中实施支持更改之前，先了解这些更改。

版本 2006 不再支持以下客户端 OS 版本（在版本 1906 中首次引入）：  

- Windows CE 7.0
- Windows 10 移动版
- Windows 10 移动企业版

## <a name="other-updates"></a>其他更新

<!--
Starting with this version, the following features are no longer [pre-release](../../servers/manage/pre-release-features.md):

### Azure Active Directory user group discovery](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco)<!--3611956
-->

若要详细了解 Configuration Manager 的 Windows PowerShell cmdlet 更改，请参阅 [PowerShell 版本 2006 发行说明](/powershell/sccm/2006-release-notes?view=sccm-ps)。

有关对管理服务 REST API 的更改的详细信息，请参阅[管理服务发行说明](../../../develop/adminservice/release-notes.md#bkmk_2006)。

除了新增功能外，这一版还有其他变化（如缺陷修复）。 有关详细信息，请参阅 [Configuration Manager Current Branch（版本 2006）的更改摘要](https://support.microsoft.com/help/4578830)。

<!--
The following update rollup (4517869) is available in the console starting on October 1, 2019: [Update rollup for Configuration Manager current branch, version 1906](https://support.microsoft.com/help/4517869).

-->

<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificate does not renew in Configuration Manager | 18 January 2019 | Yes |

> [!NOTE]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->

## <a name="next-steps"></a>后续步骤

<!-- At this time, version 2006 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-2006.md#early-update-ring). -->

自 2020 年 8 月 31 日起，版本 2006 公开发布，可供所有用户安装。

如果你已准备好安装此版本，请参阅[安装 Configuration Manager 更新](../../servers/manage/updates.md)和[用于安装更新 2006 的清单](../../servers/manage/checklist-for-installing-update-2006.md)。

> [!TIP]
> 若要安装新站点，请使用 Configuration Manager 的基准版本。
>
> 了解详细信息：
>
> - [安装新站点](../../servers/deploy/install/installing-sites.md)
> - [基准和更新版本](../../servers/manage/updates.md#bkmk_Baselines)

关于已知的重要问题，请参阅[发行说明](../../servers/deploy/install/release-notes.md)。

更新站点后，还可以查看[更新后清单](../../servers/manage/checklist-for-installing-update-2006.md#post-update-checklist)。
