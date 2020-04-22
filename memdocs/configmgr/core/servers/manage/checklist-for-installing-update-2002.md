---
title: 版本 2002 的清单
titleSuffix: Configuration Manager
description: 了解更新到 Configuration Manager 版本 2002 之前需要执行的操作。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2993032a-1204-4bd8-b5af-17a980bb0649
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a7f2abac1810b5ab40e3c253b6aee7aa970174d9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708055"
---
# <a name="checklist-for-installing-update-2002-for-configuration-manager"></a>用于为 Configuration Manager 安装更新 2002 的清单

适用范围：  Configuration Manager (Current Branch)

使用 Configuration Manager 的 Current Branch 时，可安装版本为 2002 的控制台内部更新，从之前的版本更新层次结构。 <!-- baseline only statement:-->版本 2002 也可用作[基线介质](updates.md#bkmk_Baselines)，因此，可使用该安装介质安装新层次结构的第一个站点。

若要获取版本 2002 的更新，必须在层次结构的顶级站点上使用服务连接点。 站点系统角色可处于任一模式（联机或脱机）。 若要在服务连接点脱机时下载更新，请[使用服务连接工具](use-the-service-connection-tool.md)。<!-- SCCMDocs#1946 -->

层次结构从 Microsoft 下载更新包之后，可在控制台中找到它。 在“管理”工作区中，选择“更新和维护服务”节点   。

- 当更新列为“可用”  时，此更新即可准备安装。 安装版本 2002 之前，请查看以下[关于安装更新 2002](#about-installing-update-2002) 和[清单](#checklist)的信息，了解在开始更新之前要进行的配置。

- 如果更新显示为“正在下载”且未更改，请查看 hman.log 和 dmpdownloader.log 是否有误    。

  - dmpdownloader.log 可能指示 dmpdownloader 进程要等待一段时间之后才检查更新。 若要重启更新的重分发文件的下载，请在站点服务器上重启 SMS_Executive 服务  。

  - 当代理服务器设置阻止从 `silverlight.dlservice.microsoft.com`、`download.microsoft.com` 和 `go.microsoft.com` 下载时，会出现另一个常见下载问题。

有关安装更新的详细信息，请参阅[控制台内部的更新和维护服务](updates.md#bkmk_inconsole)。

有关 Current Branch 版本的详细信息，请参阅[基线和更新版本](updates.md#bkmk_Baselines)。

## <a name="about-installing-update-2002"></a>关于安装更新 2002

### <a name="sites"></a>站点

在层次结构的顶级站点上安装更新 2002。 从管理中心站点 (CAS) 或从独立主站点启动安装。 在顶级站点安装更新后，子站点具有以下更新行为：

- CAS 完成更新安装之后，子主站点会自动安装更新。 可以使用服务时段控制站点安装更新的时间。 有关详细信息，请参阅[站点服务器的服务时段](service-windows.md)。

- 在主父站点完成更新安装之后，从 Configuration Manager 控制台中手动更新每个辅助站点。 不支持辅助站点服务器的自动更新。

### <a name="site-system-roles"></a>站点系统角色

站点服务器安装更新时，会自动更新所有站点系统角色。 这些角色处于站点服务器上或安装在远程服务器上。 安装更新之前，请确保每个站点系统服务器满足新更新版本的当前先决条件。

### <a name="configuration-manager-consoles"></a>Configuration Manager 控制台

更新完成后首次使用 Configuration Manager 控制台时，系统会提示更新该控制台。 还可以在托管该控制台的计算机上运行 Configuration Manager 安装程序，并选择用于更新该控制台的选项。 请尽快将更新安装到控制台。 有关详细信息，请参阅[安装 Configuration Manager 控制台](../deploy/install/install-consoles.md)。

> [!IMPORTANT]  
> 在 CAS 上安装更新时，应注意以下限制和延迟存在，直到所有子主站点也完成了更新安装：
>
> -  客户端升级不会启动。 这包括客户端和预生产客户端的自动更新。 此外，不能将预生产客户端提升至生产，直到最后一个站点完成更新安装。 最后一个站点完成更新安装后，客户端更新将根据你的配置选择启动。
> - 更新启用的新功能  将不可用。 此行为是为了防止 CAS 将与该功能有关的数据复制到尚未安装针对该功能的支持的站点。 所有主站点安装更新后，此功能将可供使用。
> - CAS 和子主站点之间的复制链接  显示为未升级。 此状态会在更新安装状态中显示为“完成”  状态，并带有监视复制初始化的警告。 在控制台的“监视”工作区中，此状态将显示为“正在配置链接”   。

### <a name="early-update-ring"></a>早期更新圈

<!-- SCCMDocs#1397 -->

<!-- As of December 20, 2019, version 2002 is globally available for all customers to install. If you previously opted in to the early update ring, watch for an update to this current branch version.
 -->

此时，会向早期更新通道发布版本 2002。 若要安装此更新，则必须选择加入。 以下 PowerShell 脚本将层次结构或独立主站点添加到版本 2002 的早期更新通道：

[版本 2002 选择加入脚本](https://go.microsoft.com/fwlink/?linkid=2099733) <!-- This fwlink points to the script package on the Download Center, don't change the link here! Make any changes to the fwlink target -->

Microsoft 对脚本进行数字签名，并将其捆绑到签名的自解压可执行文件内。

> [!Note]  
> 版本 2002 更新仅适用于运行版本 1810 或更高版本的站点。

若要选择加入早期更新圈，请执行以下操作：

1. 打开 Windows PowerShell 并以管理员身份运行 
1. 使用以下语法运行 EnableEarlyUpdateRing2002.ps1 脚本  ：

    `EnableEarlyUpdateRing2002.ps1 <SiteServer_Name> | SiteServer_IP>`

    其中 `SiteServer` 表示管理中心站点或独立主站点。 例如 `EnableEarlyUpdateRing2002.ps1 cmprimary01`

1. 检查更新。 有关详细信息，请参阅[获取可用更新](install-in-console-updates.md#get-available-updates)。

版本 2002 更新现在应该可以在控制台中使用。

> [!Important]  
> 此脚本仅将你的站点添加到版本 2002 的早期更新通道。 这并不是永久更改。

## <a name="checklist"></a>清单

### <a name="all-sites-run-a-supported-version-of-configuration-manager"></a>所有站点都运行 Configuration Manager 的支持版本

层次结构中的每个站点服务器都必须运行相同的 Configuration Manager 版本，然后才能开始安装更新 2002。 若要更新到 2002，必须使用版本 1810 或更高版本。

### <a name="review-the-status-of-your-product-licensing"></a>查看产品许可的状态

必须拥有有效的软件保障 (SA) 协议或等效的订阅权利才能安装此更新。 更新站点时，“许可”页将出现确认“软件保障到期日期”的选项   。

此值是可选的。 可将其指定为许可证到期日期的方便提示。 该日期在安装未来更新时可见。 你可能已在先前设置或安装更新期间指定了此值。 也可以在 Configuration Manager 控制台中指定此值。 在“管理”工作区中，展开“站点配置”，并选择“站点”    。 单击功能区中的“层次结构设置”，并切换到“许可”选项卡   。

有关详细信息，请参阅[许可和分支](../../understand/learn-more-editions.md)。

### <a name="review-microsoft-net-versions"></a>查看 Microsoft.NET 版本

站点安装此更新后，如果未安装所需的最低版本 .NET Framework 4.5，Configuration Manager 将自动安装 .NET Framework 4.5.2。 如果尚未安装此必备组件，站点会将其安装在托管以下站点系统角色之一的每个服务器上：

- 管理点
- 服务连接点
- 注册代理点
- 注册点

此安装可以将站点系统服务器置于重启挂起状态，并向 Configuration Manager 组件状态查看器报告错误。 此外，服务器上的 .NET 应用程序可能会遇到随机故障，直到重新启动服务器。

有关详细信息，请参阅 [站点和站点系统先决条件](../../plan-design/configs/site-and-site-system-prerequisites.md)。

### <a name="review-the-version-of-the-windows-adk-for-windows-10"></a>查看适用于 Windows 10 的 Windows ADK 版本

Windows 10 评估和部署工具包 (ADK) 的版本应受到 Configuration Manager 版本 2002 的支持。 有关受支持的 Windows ADK 版本的详细信息，请参阅 [Windows 10 ADK](../../plan-design/configs/support-for-windows-10.md#windows-10-adk)。 如果需要更新 Windows ADK，请在开始更新 Configuration Manager 前进行此操作。 此顺序可确保默认启动映像自动更新为最新版本的 Windows PE。 更新站点后手动更新任何自定义启动映像。

如果先更新站点，再更新 Windows ADK，请参阅[利用启动映像更新分发点](../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image)。

### <a name="review-sql-server-native-client-version"></a>查看 SQL Server Native Client 版本

安装 SQL Server 2012 Native Client 的最低版本，其中包括对 TLS 1.2 的支持。 有关详细信息，请参阅[先决条件检查列表](../deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)。

### <a name="review-the-site-and-hierarchy-status-for-unresolved-issues"></a>查看站点和层次结构状态以寻找未解决的问题

由于现有的操作问题，站点更新可能会失败。 在更新站点前，请解决以下系统的所有操作问题：  

- 站点服务器  
- 站点数据库服务器  
- 其他服务器上的远程站点系统角色

有关详细信息，请参阅 [使用警报和状态系统](use-alerts-and-the-status-system.md)。

### <a name="review-file-and-data-replication-between-sites"></a>查看站点之间的文件和数据复制

确保站点之间的文件和数据库复制正常运行并处于最新状态。 延迟或积压工作可能会阻止成功更新。

#### <a name="database-replication"></a>数据库复制

对于[数据库复制](../../plan-design/hierarchy/database-replication.md)，在开始更新之前，使用复制链接分析器  (RLA) 来帮助解决问题。 有关详细信息，请参阅[监视数据库复制](monitor-replication.md)。

使用 RLA 回答下列问题：

- 每个组的复制是否处于良好状态？
- 是否有任何链接降级？
- 是否有任何错误？

如果存在积压工作 (backlog)，请稍候，直到清除这些积压工作。如果积压工作 (backlog) 非常多，如数百万条记录，则该链接处于错误状态。 在更新站点前，请解决复制问题。 如果需要进一步的帮助，请联系 Microsoft 支持部门。<!-- 2838129 -->

#### <a name="file-based-replication"></a>基于文件的复制

对于[基于文件的复制](../../plan-design/hierarchy/file-based-replication.md)，检查所有收件箱在发送站点和接收站点上是否存在积压工作 (backlog)。 如果存在大量停滞或挂起的复制作业，请等待直到清除这些作业。<!-- SCCMDocs#1792 -->

- 在发送站点上，查看 sender.log  。
- 在接收站点上，查看 despooler log  。

### <a name="install-all-applicable-critical-windows-updates"></a>安装所有适用的关键 Windows 更新

为 Configuration Manager 安装更新之前，为每个适用的站点系统安装任何关键的 OS 更新。 这些服务器包括站点服务器、站点数据库服务器和远程站点系统角色。 如果安装的更新需要重启，请在开始升级之前重启相应的服务器。

### <a name="disable-database-replicas-for-management-points-at-primary-sites"></a>在主站点上禁用管理点的数据库副本

Configuration Manager 无法成功更新启用了管理点数据库副本的主站点。 为 Configuration Manager 安装更新之前，禁用数据库复制。

有关详细信息，请参阅[管理点的数据库副本](../deploy/configure/database-replicas-for-management-points.md)。

### <a name="set-sql-server-alwayson-availability-groups-to-manual-failover"></a>将 SQL Server AlwaysOn 可用性组设置为手动故障转移

如果使用可用性组，请确保在开始安装更新之前将可用性组设置为手动故障转移。 站点更新后，可以将故障转移还原为自动进行。 有关详细信息，请参阅 [站点数据库的 SQL Server AlwaysOn](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)。

### <a name="disable-site-maintenance-tasks-at-each-site"></a>禁用每个站点的站点维护任务

在安装更新之前，请禁用可能会在更新过程进行时运行的任何站点维护任务。 例如，但不限于：

- 备份站点服务器
- 删除过期的客户端操作
- 删除过期的发现数据

站点数据库维护任务在更新安装过程中运行时，更新安装可能会失败。 在禁用任务之前，请记录该任务的计划，以便在安装更新之后可恢复其配置。

有关详细信息，请参阅 [维护任务](maintenance-tasks.md) 和[维护任务参考](reference-for-maintenance-tasks.md)。

### <a name="temporarily-stop-any-antivirus-software"></a>暂时停止任何防病毒软件

更新站点之前，停止 Configuration Manager 服务器上的防病毒软件。 防病毒软件可能会锁定某些需要更新的文件，这将导致更新失败。 <!--SMS.503481-->

### <a name="create-a-backup-of-the-site-database"></a>创建站点数据库的备份

更新站点之前，在 CAS 和主站点上备份站点数据库。 此备份可确保你拥有可用于灾难恢复的成功备份。

有关详细信息，请参阅 [备份和恢复](backup-and-recovery.md)。

### <a name="back-up-customized-files"></a>备份自定义文件

如果你或第三方产品自定义任何 Configuration Manager 配置文件，请保存自定义项的副本。

例如，将自定义条目添加到 Configuration Manager 安装目录的 `bin\X64` 文件夹中的 osdinjection.xml  文件中。 在更新 Configuration Manager 后，这些自定义项不会保留。 需要重新应用自定义项。

### <a name="plan-for-client-piloting"></a>规划客户端试点

安装还更新客户端的站点更新时，请在更新所有生产客户端之前测试预生产中的新客户端更新。 若要使用此选项，在开始安装更新之前配置站点，以支持预生产的自动升级。

有关详细信息，请参阅 [升级客户端](../../clients/manage/upgrade/upgrade-clients.md) 和[如何在预生产集合中测试客户端升级](../../clients/manage/upgrade/test-client-upgrades.md)。

### <a name="plan-to-use-service-windows"></a>计划使用服务时段

若要定义可向站点服务器安装更新的时间段，请使用服务时段。 它们可以帮助控制层次结构中的站点安装更新的时间。 有关详细信息，请参阅 [站点服务器的服务时段](service-windows.md)。

### <a name="review-supported-extensions"></a>查看支持的扩展

<!--SCCMdocs#587-->
如果使用 Microsoft 或 Microsoft 合作伙伴的其他产品来扩展 Configuration Manager，请确认这些产品是否支持版本 2002。 检查产品供应商的此项信息。 例如，请查看 Microsoft Deployment Toolkit 的[发行说明](../../../mdt/release-notes.md)。

### <a name="remove-intune-subscription-hybrid-mdm"></a>删除 Intune 订阅（混合 MDM）

<!-- SCCMDocs-pr#4253 -->
从 2019 年 9 月 1 日起，混合 MDM 服务产品已停用。 如果 Configuration Manager 站点具有 Microsoft Intune 订阅，则需要将其删除。 有关详细信息，请参阅[删除混合 MDM](../../../mdm/understand/what-happened-to-hybrid.md#remove-hybrid-mdm)。

### <a name="run-the-setup-prerequisite-checker"></a>运行安装程序先决条件检查程序

当控制台将更新列为“可用”  时，可以运行先决条件检查程序，然后再安装更新。 （在站点上安装更新时，会再次运行必备组件检查程序。）

若要从控制台运行先决条件检查，请转到“管理”工作区，并选择“更新和服务”   。 选择“Configuration Manager 2002”更新包，然后在功能区中选择“运行先决条件检查”   。

有关详细信息，请参阅[安装控制台内部更新前](install-in-console-updates.md#bkmk_beforeinstall)中的“安装更新之前运行先决条件检查程序”部分  。

> [!IMPORTANT]  
> 运行先决条件检查程序时，该过程会更新某些用于站点维护任务的产品源文件。 因此，在运行先决条件检查程序之后但在安装更新之前，如果需要执行站点维护任务，可从站点服务器上的 CD.Latest 文件夹运行  **Setupwpf.exe** （Configuration Manager 安装程序）。

### <a name="update-sites"></a>更新站点

现已准备好为层次结构开始更新安装。 有关安装更新的详细信息，请参阅[安装控制台内部更新](install-in-console-updates.md#bkmk_install)。

你有可能计划在常规工作时间外安装更新。 确定过程将对业务操作造成最小影响的时间。 安装更新及其操作会重新安装站点组件和站点系统角色。

有关详细信息，请参阅  [Configuration Manager 更新](updates.md)。

## <a name="post-update-checklist"></a>更新后的清单

更新站点后，使用以下清单可完成常见任务和配置。

### <a name="confirm-version-and-restart-if-necessary"></a>确认版本并重启（如有必要）

确保每个站点服务器和站点系统角色都已更新为版本 2002。 在控制台的“管理”工作区中，将“版本”列添加到“站点”和“分发点”节点     。 如有必要，站点系统角色将自动重新安装以更新到新的版本。

请考虑重新启动初次未成功更新的远程站点系统。 查看站点基础结构，确保适用的站点服务器和远程站点系统服务器已成功重新启动。 通常，仅当 Configuration Manager 安装 .NET 作为站点系统角色的先决条件时，站点服务器才重新启动。

### <a name="confirm-site-to-site-replication-is-active"></a>确认站点到站点复制处于活动状态

在 Configuration Manager 控制台中，转到以下位置以查看状态并确保复制处于活动状态：  

- “监视”工作区、“站点层次结构”节点    

- “监视”工作区、“数据库复制”节点    

有关详细信息，请参阅下列文章：  

- [监视层次结构和复制基础结构](monitor-hierarchy.md)
- [关于复制链接分析器](monitor-replication.md#BKMK_RLA)  

### <a name="update-configuration-manager-consoles"></a>更新 Configuration Manager 控制台

将所有远程 Configuration Manager 控制台更新为相同版本。 系统会在以下情况下提示你更新控制台：  

- 打开控制台。  

- 在控制台中转到新节点。  

### <a name="reconfigure-database-replicas-for-management-points"></a>重新配置管理点的数据库副本

更新主站点之后，为在站点更新之前卸载的管理点重新配置数据库副本。 有关详细信息，请参阅[管理点的数据库副本](../deploy/configure/database-replicas-for-management-points.md)。  

### <a name="reconfigure-sql-server-alwayson-availability-groups"></a>重新配置 SQL Server AlwaysOn 可用性组

如果使用可用性组，请将故障转移配置重置为“自动”。 有关详细信息，请参阅[站点数据库的 SQL Server AlwaysOn](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)。<!-- SCCMDocs #1366 -->

### <a name="reconfigure-any-disabled-maintenance-tasks"></a>重新配置已禁用的所有维护任务

如果安装更新之前在站点上禁用了数据库[维护任务](maintenance-tasks.md)，请重新配置这些任务。 使用更新之前就已经存在的相同设置。  

### <a name="update-clients"></a>更新客户端

如果在安装更新前已配置客户端试点，请按照你创建的计划更新客户端。 有关详细信息，请参阅[如何升级 Windows 计算机的客户端](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md)。  

### <a name="third-party-extensions"></a>第三方扩展

如果使用 Configuration Manager 的任何扩展，请将其更新为最新版本，以支持 Configuration Manager 版本 2002。

### <a name="update-custom-boot-images-and-media"></a>更新自定义启动映像和媒体

<!--SCCMDocs issue 775-->

对使用的所有启动映像使用“更新分发点”操作，无论是默认启动映像还是自定义启动映像  。 此操作可确保客户端能够使用最新版本。 即使没有新的 Windows ADK 版本，Configuration Manager 客户端组件也可能随更新而更改。 如果未更新启动映像和媒体，设备上的任务序列部署可能会失败。

更新站点时，Configuration Manager 会自动更新默认  启动映像。 它不会将更新的内容自动分发到分发点。 准备好在网络中分发此内容时，请对特定启动映像使用更新分发点  操作。

更新站点后，手动更新任何自定义  启动映像。 如有必要，此操作将使用最新的客户端组件更新启动映像，可选择使用当前的 Windows PE 版本重载它，并将内容重新分发到分发点。

有关详细信息，请参阅[使用启动映像更新分发点](../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image)。
