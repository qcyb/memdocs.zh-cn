---
title: 1910 版中的新增功能
titleSuffix: Configuration Manager
description: 获取有关 Configuration Manager Current Branch 版本 1910 中引入的更改和新增功能的详细信息。
ms.date: 01/22/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3e1ddb65-1193-46ce-a7c0-a48dfd9fd833
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 6406a208de448e40e1d686440f41610266cde042
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700293"
---
# <a name="whats-new-in-version-1910-of-configuration-manager-current-branch"></a>Configuration Manager Current Branch 版本 1910 中的新增功能

适用范围：Configuration Manager (Current Branch)

Configuration Manager Current Branch 的更新 1910 作为控制台内更新提供。 将此更新应用于运行版本 1806 或更高版本的站点。 <!-- baseline only statement:When installing a new site, it's also available as a baseline version.--> 本文汇总了 Configuration Manager 版本 1910 中的更改和新增功能。

始终查看安装此更新的最新清单。 有关详细信息，请参阅[用于安装更新 1910 的清单](../../servers/manage/checklist-for-installing-update-1910.md)。 更新站点后，还可以查看[更新后清单](../../servers/manage/checklist-for-installing-update-1910.md#post-update-checklist)。

若要利用 Configuration Manager 的新功能，更新站点后，还请将客户端更新到最新版本。 尽管在更新站点和控制台时 Configuration Manager 控制台中会显示新功能，但只有在客户端版本也是最新版本之后，完整方案才能正常运行。

> [!TIP]
> 若要在此页面更新时收到通知，请将以下 URL 复制并粘贴到 RSS 源阅读器中：`https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1910+-+Configuration+Manager%22&locale=en-us`

## <a name="microsoft-endpoint-configuration-manager"></a><a name="bkmk_mem"></a> Microsoft Endpoint Configuration Manager

<!--4960084-->

Configuration Manager 现在是 Microsoft Endpoint Manager 的一部分。

![Microsoft Endpoint Configuration Manager](media/4960084-endpoint-manager-logo.png)

Microsoft Endpoint Manager 是用于管理所有设备的集成解决方案。 只通过简化授权 Microsoft 就可以将 Configuration Manager 和 Intune 组合在一起。 继续利用现有的 Configuration Manager 投资，同时按照自己的进度获取 Microsoft 云的优势。

以下 Microsoft 管理解决方案现已成为 Microsoft Endpoint Manager 品牌的一部分：

- [Configuration Manager](/configmgr)
- [Intune](/intune)
- [桌面分析](../../../desktop-analytics/overview.md)
- [Autopilot](/intune/enrollment/enrollment-autopilot)
- [设备管理管理员控制台](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/microsoft-intune-rolls-out-an-improved-streamlined-endpoint/ba-p/937760)中的其他功能

有关详细信息，请参阅以下 Microsoft 公司副总裁 Brad Anderson 发布的关于 Microsoft 365 的帖子：

- [公告博客文章](https://aka.ms/cmannounce)
- [远见报告](https://aka.ms/MEMVisionPaper)
- [公告摘要视频](https://youtu.be/GS7oNPInFuw)

### <a name="what-things-change-in-configuration-manager-with-microsoft-endpoint-manager"></a>使用 Microsoft Endpoint Manager 在 Configuration Manager 中有什么变化？

在版本 1910 中，除了名称更改之外，Configuration Manager 的功能仍然相同。 某些名称更改可能会影响以下组件的使用：

- **Configuration Manager 控制台**：在“Microsoft Endpoint Manager”文件夹中的 Windows“开始”菜单下，找到控制台和“远程控制查看器”的快捷方式 。

- **软件中心**：在“Microsoft Endpoint Manager”文件夹中的 Windows“开始”菜单下，找到软件中心快捷方式。

![Microsoft Endpoint Manager“开始”菜单图标](media/microsoft-endpoint-manager-start-menu.png)

确保更新你维护的任何内部文档，以包括这些新位置。

> [!TIP]
> 在 Windows 10 中，打开“开始”菜单时，键入名称即可找到图标。 例如，输入 `Configuration Manager` 或 `Software Center`。

## <a name="site-infrastructure"></a><a name="bkmk_infra"></a>站点基础结构

### <a name="reclaim-sedo-lock"></a>回收 SEDO 锁定

<!--4786915-->

从[当前分支版本 1906](whats-new-in-version-1906.md#reclaim-sedo-lock-for-task-sequences) 开始，可以清除对任务序列的锁定。 现在可以清除对 Configuration Manager 控制台中任何对象的锁定。

有关详细信息，请参阅[使用 Configuration Manager 控制台](../../servers/manage/admin-console.md#bkmk_sedo)。

### <a name="extend-and-migrate-on-premises-site-to-microsoft-azure"></a>将本地站点扩展并迁移到 Microsoft Azure
<!--3556022-->

此新工具可帮助你以编程方式为 Configuration Manager 创建 Azure 虚拟机 (VM)。 它可以使用默认设置站点角色（如被动站点服务器、管理点和分发点）进行安装。 验证新角色后，将其用作其他站点系统以实现高可用性。 你还可以删除本地站点系统角色，仅保留 Azure VM 角色。

有关详细信息，请参阅[将本地站点扩展并迁移到 Microsoft Azure](../../support/azure-migration-tool.md)。

<!-- ## <a name="bkmk_cloud"></a> Cloud-attached management -->

## <a name="desktop-analytics"></a><a name="bkmk_da"></a> 桌面分析

有关桌面分析云服务每月更改的详细信息，请参阅[桌面分析中的新增功能](../../../desktop-analytics/whats-new.md)。

## <a name="real-time-management"></a><a name="bkmk_real"></a>实时管理

### <a name="optimizations-to-the-cmpivot-engine"></a>对 CMPivot 引擎的优化
<!--3197353-->
我们新增了对 CMPivot 引擎的一些重要优化。 现在可以将更多处理内容推送到 ConfigMgr 客户端。 这些优化大大减少了运行 CMPivot 查询所需的网络和服务器 CPU 负载。 通过这些优化，现在可以实时筛选千兆字节的客户端数据。 

有关详细信息，请参阅 [CMPivot 引擎的优化](../../servers/manage/cmpivot-changes.md#bkmk_optimization)。

### <a name="additional-cmpivot-entities-and-enhancements"></a>其他 CMPivot 实体和增强功能
<!--5410930-->
我们添加了一些新的 CMPivot 实体和实体增强功能，以帮助进行故障排除和搜寻。 我们包含了以下要查询的实体：

- Windows 事件日志 ([WinEvent](../../servers/manage/cmpivot-changes.md#bkmk_WinEvent))
- 文件内容 ([FileContent](../../servers/manage/cmpivot-changes.md#bkmk_File))
- 由进程加载的 DLL ([ProcessModule](../../servers/manage/cmpivot-changes.md#bkmk_ProcessModule))
- Azure Active Directory 信息 ([AADStatus](../../servers/manage/cmpivot-changes.md#bkmk_AadStatus))
- Endpoint Protection 状态 ([EPStatus](../../servers/manage/cmpivot-changes.md#bkmk_EPStatus))

此版本还包括 CMPivot 的多个[其他增强功能](../../servers/manage/cmpivot-changes.md#bkmk_Other)。 有关详细信息，请参阅[从版本 1910 开始的 CMPivot](../../servers/manage/cmpivot-changes.md#bkmk_cmpivot1910)。

## <a name="content-management"></a><a name="bkmk_content"></a>内容管理

### <a name="microsoft-connected-cache-support-for-intune-win32-apps"></a>支持 Intune Win32 应用的 Microsoft Connected Cache

<!--5032900-->

在 Configuration Manager 分发点上启用 Microsoft 互联缓存后，现在可以为共同管理的客户端提供 Microsoft Intune Win32 应用。

有关详细信息，请参阅 [Configuration Manager 中的 Microsoft Connected Cache](../hierarchy/microsoft-connected-cache.md#bkmk_intune)。

> [!NOTE]
> Configuration Manager Current Branch 版本 1906 包括[传递优化网络内缓存](../hierarchy/microsoft-connected-cache.md)，它是一项安装于 Windows Server 的应用程序，目前仍在开发中。 从 Current Branch 版本 1910 开始，此功能现在称为“Microsoft Connected Cache”。
>
> 在 Configuration Manager 分发点上安装互联缓存后，会将传递优化服务流量卸载到本地源。 互联缓存通过有效地在字节范围级别缓存内容来实现此行为。

## <a name="client-management"></a><a name="bkmk_client"></a> 客户端管理

### <a name="include-custom-configuration-baselines-as-part-of-compliance-policy-assessment"></a>将自定义配置基线包含在合规性策略评估中
<!--3608345-->

现在可以将自定义配置基线评估添加为合规性策略评估规则。 创建或编辑配置基线时，现在可以使用“将此基线作为合规性策略的一部分进行评估”严格。 添加或编辑合规性策略规则时，有一个名为“在合规性策略评估中包含配置的基线”的条件。

对于共同管理的设备，当你配置 Intune 以将 Configuration Manager 合规性评估结果作为总体合规性状态的一部分时，此信息将发送到 Azure Active Directory。 然后，你可以使用它对 Office 365 资源进行条件访问。

有关详细信息，请参阅[将自定义配置基线包含在合规性策略评估中](../../../compliance/deploy-use/create-configuration-baselines.md#bkmk_CAbaselines)。

### <a name="enable-user-policy-for-windows-10-enterprise-multi-session"></a>为 Windows 10 企业版多会话启用用户策略

<!--4737447-->

Configuration Manager 当前分支版本 1906 引入了对 [Windows 虚拟桌面](../configs/supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop)的支持。 此 Microsoft Azure 环境支持多个操作系统版本，其中一些版本允许多个并发活动用户会话。 例如，Windows 10 企业版多会话是其中一个操作系统版本。

如果这些多会话设备中需要用户策略，并且接受任何潜在的性能影响，则可以立即配置客户端设置以启用用户策略。 在“客户端策略”组中，配置“为多个用户会话启用用户策略”设置 。

有关详细信息，请参阅[如何配置客户端设置](../../clients/deploy/configure-client-settings.md)。


<!-- ## <a name="bkmk_comgmt"></a> Co-management -->


## <a name="application-management"></a><a name="bkmk_app"></a>应用程序管理

### <a name="deploy-microsoft-edge-version-77-and-later"></a>部署 Microsoft Edge 版本 77 及更高版本
<!--4561024-->
全新的 Microsoft Edge 已准备好应用于业务。 现在即可为你的用户部署 Microsoft Edge 版本 77 及更高版本。 管理员可以选择 Beta、Dev 或 Stable 通道，以及要部署的 Microsoft Edge 客户端版本。

有关更多详细信息，请参阅[部署 Microsoft Edge 版本 77 及更高版本](../../../apps/deploy-use/deploy-edge.md)。

### <a name="improvements-to-application-groups"></a>对应用程序组的改进

<!--4760058-->

从当前分支版本 1906 开始，可以创建一组可以作为单个部署发送到设备集合的应用程序。 此版本改进了以下功能：

- 用户可以在软件中心选择“卸载”应用组。
- 可以将应用组部署到用户集合。

有关更多一般信息，请参阅[创建应用程序组](../../../apps/deploy-use/create-app-groups.md)。


## <a name="os-deployment"></a><a name="bkmk_osd"></a> OS 部署

### <a name="improvements-to-the-task-sequence-editor"></a>对运行任务序列编辑器的改进

 任务序列编辑器包括以下改进：

- **搜索任务序列编辑器：**<!--4621085--> 如果拥有包含许多组和步骤的大型任务序列，则很难找到具体步骤。 现在可以在任务序列编辑器中搜索。 通过此操作，可更快速地找到任务序列中的步骤。
- **复制和粘贴任务序列条件：**<!--4621098--> 如果想要将条件从一个任务序列步骤重复用于另一个任务序列步骤，则现在可以在任务序列编辑器中复制和粘贴条件。

有关详细信息，请参阅关于如何[使用任务序列编辑器](../../../osd/understand/task-sequence-editor.md)的新文章。

### <a name="task-sequence-performance-improvements-power-plans"></a>任务序列性能改进：电源计划

<!--3555926-->

现在可以使用高性能电源计划运行任务序列。 此选项可提高任务序列的总体速度。 它将 Windows 配置为使用其内置的高性能电源计划，该计划提供最高性能，但电源消耗会变高。

有关详细信息，请参阅[电源计划的性能改进](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#bkmk_perf)。

### <a name="task-sequence-download-on-demand-over-the-internet"></a>通过 Internet 按需进行任务序列下载

<!--3601238-->

你可以使用任务序列通过云管理网关 (CMG) 部署 Windows 10 就地升级。 但是，在启动任务序列之前，该部署要求在本地下载所有内容。

从此版本开始，任务序列引擎可以按需从启用内容的 CMG 或云分发点下载包。 此更改为基于 Internet 的设备的 Windows 10 就地升级部署提供了更大的灵活性。

有关详细信息，请参阅[通过 CMG 部署 Windows 10 就地升级](../../../osd/deploy-use/deploy-a-task-sequence.md#deploy-windows-10-in-place-upgrade-via-cmg)。

### <a name="improvements-to-os-deployment"></a>对 OS 部署的改进

此版本包括对 OS 部署的以下改进。

#### <a name="boot-image-keyboard-layout"></a>启动映像键盘布局

<!--4910348-->

为启动映像配置默认键盘布局。 在启动映像的“自定义”选项卡上，使用“在 WinPE 中设置默认键盘布局”新选项 。 如果选择 zh-cn 以外的其他语言，Configuration Manager 仍会在可用输入区域设置中包含 zh-cn。 在设备上，初始键盘布局为选定的区域设置，但用户可以将设备切换为 zh-cn（如果需要）。

有关详细信息，请参阅[管理启动映像](../../../osd/get-started/manage-boot-images.md#customization)。

#### <a name="import-a-single-index-of-an-os-upgrade-package"></a>导入 OS 升级包的单个索引

<!--4931110-->

导入 OS 升级包时，可以使用“从所选升级包的 install.wim 文件中提取特定映像索引”选项。 此行为类似于 [OS 映像](../../../osd/get-started/manage-operating-system-images.md#BKMK_AddOSImages)，但它会覆盖 OS 升级包中的现有 install.wim。 它会将映像索引提取到临时位置，然后将其移动到原始源目录。

有关详细信息，请参阅[管理 OS 升级包](../../../osd/get-started/manage-operating-system-upgrade-packages.md#BKMK_AddOSUpgradePkgs)。

#### <a name="output-the-results-of-a-run-command-line-step-to-a-variable-during-a-task-sequence"></a>在任务序列期间将运行命令行步骤的结果输出到变量

<!--user story 4977616/bug 4798352-->

“运行命令行”步骤现在包含“输出到任务序列变量”选项 。 启用此选项时，任务序列会将命令的输出保存到你指定的自定义任务序列变量。

有关详细信息，请参阅[运行命令行](../../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine)

#### <a name="improvements-to-task-sequence-debugger"></a>任务序列调试程序的改进

此版本包括对任务序列调试程序的以下改进：

- 使用新的任务序列变量 TSDebugOnError，以便在任务序列返回错误时自动启动调试程序。<!-- 5012536 -->
- 如果你在调试程序中创建断点，随后任务序列重新启动计算机，则调试程序将在重新启动后保留断点。<!-- 5012509 -->

有关详细信息，请参阅[任务序列调试器](../../../osd/deploy-use/debug-task-sequence.md)和[任务序列变量 - TSDebugOnError](../../../osd/understand/task-sequence-variables.md#TSDebugOnError)。

#### <a name="improved-language-support-in-task-sequence"></a>任务序列中语言支持改进

<!--5411057, 5138936-->

此版本添加了 OS 部署期间对语言配置的控制。 如果已应用这些语言设置，则此更改可帮助简化 OS 部署任务序列。 无需对每种语言使用多个步骤或单独的脚本，只需对内置“应用 Windows 设置”步骤且具有该语言条件的每种语言使用一个实例。

使用“应用 Windows 设置”任务序列步骤配置以下新设置：

- 输入区域设置（默认键盘布局）
- 系统区域设置
- UI 语言
- UI 语言回退
- 用户区域设置

有关详细信息，请参阅 [应用 Windows 设置](../../../osd/understand/task-sequence-steps.md#BKMK_ApplyWindowsSettings)。

#### <a name="new-variable-for-windows-10-in-place-upgrade"></a>用于 Windows 10 就地升级的新变量

<!--4680263-->

若要在 Windows 安装完成时解决高性能设备上 Windows 10 就地升级任务序列的计时问题，现在可以设置新的任务序列变量“SetupCompletePause”。 在将以秒为单位的值分配给此变量时，Windows 安装过程会在启动任务序列之前延迟该时长。 此超时向 Configuration Manager 客户端提供了额外的时间来进行初始化。

有关详细信息，请参阅[任务序列变量 - SetupCompletePause](../../../osd/understand/task-sequence-variables.md#SetupCompletePause)。

<!-- ## <a name="bkmk_userxp"></a> Software Center -->

## <a name="software-updates"></a><a name="bkmk_sum"></a>软件更新

### <a name="additional-options-for-third-party-update-catalogs"></a>针对第三方更新目录的其他选项
<!--4469002-->
现在，你可以更精细地控制第三方更新目录的同步。 从 Configuration Manager 版本 1910 开始，你可以单独配置每个目录的同步计划。 使用包含已分类更新的目录时，可以将同步配置为仅包含特定类别的更新，以免同步整个目录。 使用已分类目录，当你确信将部署类别时，可以将其配置为自动下载并发布到 Windows Server Update Services (WSUS)。

有关详细信息，请参阅[启用第三方更新](../../../sum/deploy-use/third-party-software-updates.md#bkmk_1910)。

### <a name="use-delivery-optimization-for-all-windows-updates"></a>对所有 Windows 更新使用传递优化
<!--4699118-->
以前，只能对快速更新使用传递优化。 使用 Configuration Manager 版本 1910，现在可以使用传递优化为运行 Windows 10 版本 1709 或更高版本的客户端分发所有 Windows 更新内容。

有关详情，请参阅：
- [优化 Windows 10 更新传递](../../../sum/deploy-use/optimize-windows-10-update-delivery.md#bkmk_DO-1910)
- [软件更新的客户端设置](../../clients/deploy/about-client-settings.md#software-updates)
- [用于传递优化的客户端设置](../../clients/deploy/about-client-settings.md#delivery-optimization)

### <a name="additional-software-update-filter-for-adrs"></a>ADR 的附加软件更新筛选器
<!--4852033-->
现在可以将“已部署”用作自动部署规则的更新筛选器 (ADR)。 此筛选器可帮助确定可能需要部署到试点或测试集合的新更新。

有关详细信息，请参阅[自动部署软件更新](../../../sum/deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process)。

## <a name="office-management"></a><a name="bkmk_o365"></a>Office 管理


### <a name="office-365-proplus-pilot-and-health-dashboard"></a>Office 365 专业增强版试点和运行状况仪表板
<!--4488272, 4488301-->

“Office 365 专业增强版试点和运行状况仪表板”有助于你计划、引导和部署 Office 365 专业增强版。 仪表板为具有 Office 365 专业增强版的设备提供运行状况见解，以帮助找出可能影响部署计划的问题。 Office 365 专业增强版试点和运行状况仪表板根据加载项清单提供了试点设备建议。

有关详细信息，请参阅 [Office 365 专业增强版试点和运行状况仪表板](../../../sum/deploy-use/office-365-dashboard.md#bkmk_pilot)。

## <a name="protection"></a><a name="bkmk_protect"></a> 保护

### <a name="bitlocker-management"></a>BitLocker 管理

<!--3601034-->

Configuration Manager 现在为 BitLocker 驱动器加密提供以下管理功能：

- 将 BitLocker 客户端部署到托管 Windows 设备。
- 管理设备加密策略。
- 生成相容性报告。
- 使用管理和监视网站进行密钥恢复。
- 访问用户自助服务门户。

有关详细信息，请参阅[规划 BitLocker 管理](../../../protect/plan-design/bitlocker-management.md)。

## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Configuration Manager 控制台

### <a name="view-active-consoles-and-message-administrators-through-console-connections"></a>通过控制台连接查看活动控制台和消息管理员
<!--4923997-->
我们对控制台连接进行了以下改进：

- 能够通过 Configuration Manager Microsoft Teams 向其他管理员发送消息。
- “上次控制台检测信号”列已替换“上次连接时间”列 。
  - 前台打开的控制台每 10 分钟发送一次检测信号，以帮助确定当前哪些控制台连接处于活动状态。

有关详细信息，请参阅[查看最近连接的控制台](../../servers/manage/admin-console.md#bkmk_viewconnected)和[消息管理员](../../servers/manage/admin-console.md#bkmk_message)。

### <a name="client-diagnostics-actions"></a>客户端诊断操作

<!--4433455-->

Configuration Manager 控制台中提供了“客户端诊断”的新设备操作：

- **启用详细日志记录：** 将 CCM 组件的全局日志级别更改为详细，并启用调试日志记录。
- **禁用详细日志记录：** 将全局日志级别更改为默认值，并禁用调试日志记录。

有关详细信息，请参阅[客户端诊断](../../clients/manage/client-notification.md#client-diagnostics)。

### <a name="improvements-to-console-search"></a>对控制台搜索的改进
<!--4640570-->

此版本包括对 Configuration Manager 控制台搜索的以下改进：

- 现在可以使用“驱动程序包”和“查询”节点中的“所有子文件夹”搜索选项  。<!--2841181,5424892-->
- 如果搜索返回的结果超过 1,000 个，请选择通知栏上的“确定”以查看更多结果。<!--4640570-->

## <a name="other-updates"></a>其他更新

有关 Configuration Manager 的 Windows PowerShell cmdlet 更改的详细信息，请参阅 [PowerShell 版本 1910 发行说明](/powershell/sccm/1910-release-notes?view=sccm-ps)。

有关对管理服务 REST API 的更改的详细信息，请参阅[管理服务发行说明](../../../develop/adminservice/release-notes.md#bkmk_1910)。

除了新增功能外，这一版还有其他变化（如缺陷修复）。 有关详细信息，请参阅 [Configuration Manager Current Branch（版本 1910）的更改摘要](https://support.microsoft.com/help/4535776)。

<!--
As of this version, the following features are no longer pre-release:
- [SMS Provider administration service](../hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service)
- [Device Guard management](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md)
-->
以下更新汇总 (4537079) 于 2020 年 2 月 18 日起在控制台中提供：[Microsoft Endpoint Configuration Manager Current Branch（版本 1910）的更新汇总](https://support.microsoft.com/help/4537079)。



<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4552181](https://support.microsoft.com/help/4552181) | Content distribution stalls in Configuration Manager current branch, version 1910 | 16 March 2020 | No |
| [4552430](https://support.microsoft.com/help/4552430) | Third-party update category synchronization resets to default in Configuration Manager | 18 March 2020 | No |

> [!NOTE]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->

## <a name="next-steps"></a>后续步骤

<!-- At this time, version 1910 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-1910.md#early-update-ring). -->
自 2019 年 12 月 20 日起，版本 1910 公开发布，可供所有用户安装。

准备好安装此版本时，请参阅[安装 Configuration Manager 的更新](../../servers/manage/updates.md)和[用于安装更新 1910 的清单](../../servers/manage/checklist-for-installing-update-1910.md)。

> [!TIP]
> 若要安装新站点，请使用 Configuration Manager 的基准版本。
>
> 了解详细信息：
>
> - [安装新站点](../../servers/deploy/install/installing-sites.md) 
> - [基准和更新版本](../../servers/manage/updates.md#bkmk_Baselines) 

关于已知的重要问题，请参阅[发行说明](../../servers/deploy/install/release-notes.md)。

更新站点后，还可以查看[更新后清单](../../servers/manage/checklist-for-installing-update-1910.md#post-update-checklist)。