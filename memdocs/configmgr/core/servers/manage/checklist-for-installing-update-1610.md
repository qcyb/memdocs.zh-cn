---
title: 1610 清单
titleSuffix: Configuration Manager
description: 了解更新到 Configuration Manager 版本 1610 之前需要执行的操作。
ms.date: 06/6/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7b411cb0-4fd1-41f2-a2f6-33738a5bde96
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 25d0302c4c35f2c66ce06febde63809b4a11116c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688775"
---
# <a name="checklist-for-installing-update-1610-for-configuration-manager"></a>用于为 Configuration Manager 安装更新 1610 的清单

适用范围：  Configuration Manager (Current Branch)

使用 Configuration Manager 的 Current Branch 时，可安装版本为 1610 的控制台内部更新，从版本 1606 更新层次结构。 如果层次结构运行版本 1511、1602 或 1606，则可更新到版本 1610。

若要获取版本 1610 的更新，必须在层次结构的顶层站点上使用服务连接点站点系统角色。 其可处于联机或脱机模式。 层次结构从 Microsoft 下载更新包之后，可在“管理”&gt;“概述”&gt;“云服务”&gt;“更新和维护服务”  下的控制台中找到它。

-   当更新列为“可用”  时，此更新即可准备安装。 安装版本 1610, 之前，请查看以下[关于安装更新 1610](#about-installing-update-1610)和[清单](#checklist)信息，了解在开始更新之前要进行的配置。

-   如果更新显示为“正在下载”  且未更改，请查看 **hman.log** 和 **dmpdownloader.log** 是否有误。

    -   通常情况下，还可以在站点服务器上重启 **SMS_Executive** 服务，以重启更新重新分发文件的下载。

    -   当代理服务器设置阻止从 `silverlight.dlservice.microsoft.com` 和 `download.microsoft.com` 下载时，会出现另一个常见下载问题。

有关安装更新的详细信息，请参阅[控制台内部的更新和维护服务](updates.md#bkmk_inconsole)。

有关 Current Branch 版本的信息，请参阅 [Configuration Manager 更新](updates.md)中的[基线和更新版本](updates.md#bkmk_Baselines)。

## <a name="about-installing-update-1610"></a>关于安装更新 1610

**站点：**  
只能在层次结构的顶层站点上安装更新 1610。 这意味着你需要从管理中心站点（如果有）或从独立主站点启动安装。 在顶层站点安装更新后，子站点具有以下更新行为：

-   管理中心站点完成更新安装之后，子主站点会自动启动更新。 可以使用服务时段控制站点安装更新的时间。 版本 1606 之前，服务时段被称为维护时段。 有关详细信息，请参阅[站点服务器的服务时段](service-windows.md)。

-   在主父站点完成更新安装之后，必须从 Configuration Manager 控制台中手动更新辅助站点。 不支持辅助站点服务器的自动更新。

**站点系统角色：**  
站点服务器安装更新时，站点服务器上安装的站点系统角色和远程计算机上安装的那些角色会自动更新。 因此，安装更新之前，请确保每个站点系统服务器满足使用新更新版本进行操作的任何新的先决条件。

**Configuration Manager 控制台：**    
更新完成后首次使用 Configuration Manager 控制台时，系统会提示更新该控制台。 为此，必须在承载该控制台的计算机上运行 Configuration Manager 安装程序，并选择用于更新该控制台的选项。 我们建议不要延迟将更新安装到该控制台。



## <a name="checklist"></a>清单

**确保所有站点都运行受支持的 Configuration Manager 版本：** 层次结构中的每个站点服务器都必须运行相同的 Configuration Manager 版本，然后才能开始安装更新 1610：版本 1511、1602 或 1606。

**查看软件保障的状态或等效订阅权限：**    
必须具有有效的软件保障 (SA) 协议才能安装更新 1610。 安装版本 1610 时，可在“许可”  选项卡上选择确认“软件保障到期日期”  。

这是一个可选值，可将其指定为许可证到期日期的方便提示，在安装未来更新时显示。 如果从版本 1606 基线介质安装 Configuration Manager，则之前可能在安装时指定此值或在站点安装后，在“层次结构设置”  的“许可证”  选项卡上指定此值。

有关详细信息，请参阅 [Configuration Manager 的许可和分支](../../understand/learn-more-editions.md)。

**查看站点系统服务器上已安装的 Microsoft .NET 版本：** 如果尚未安装 .NET Framework 4.5 或更高版本，则站点安装更新 1610 时，Configuration Manager 将在承载以下任一站点系统角色的每台计算机上自动安装 .NET Framework 4.5.2：

-   注册代理点
-   注册点
-   管理点
-   服务连接点

此安装可以将站点系统服务器置于重启挂起状态，并向 Configuration Manager 组件状态查看器报告错误。 此外，服务器上的 .NET 应用程序可能会遇到随机故障，直到重启服务器。

有关详细信息，请参阅[站点和站点系统先决条件](../../plan-design/configs/site-and-site-system-prerequisites.md)。

**查看站点和层次结构状态，并确认没有未解决的问题：** 更新站点之前，请解决远程计算机上安装的站点服务器、站点数据库服务器和站点系统角色的所有操作问题。 由于现有的操作问题，站点更新可能会失败。

有关详细信息，请参阅[使用 Configuration Manager 的警报和状态系统](use-alerts-and-the-status-system.md)。

**查看站点之间的文件和数据复制**：确保站点之间的文件和数据库复制正常运行并且处于最新状态。 延迟或积压工作可能会阻止顺利、成功更新。
对于数据库复制，可以在开始更新之前，使用复制链接分析器来帮助解决问题。

有关详细信息，请参阅[监视数据库复制](monitor-replication.md)主题中的[复制链接分析器](monitor-replication.md#BKMK_RLA)。

**为承载站点、站点数据库服务器和远程站点系统角色的计算机上的操作系统，安装所有合适的关键更新：** 为 Configuration Manager 安装更新之前，为每个适用的站点系统安装任何关键的更新。 如果安装的更新需要重启，请在启动 Configuration Manager 更新之前重启合适的计算机。

**在主站点上禁用管理点数据库副本：**    
Configuration Manager 无法成功更新启用了管理点数据库副本的主站点。 安装 Configuration Manager 的更新之前禁用数据库复制。

有关详细信息，请参阅 [Configuration Manager 管理点的数据库副本](../deploy/configure/database-replicas-for-management-points.md)。

**将 SQL Server AlwaysOn 可用性组设置为手动故障转移：**    
在安装更新（例如版本 1610）之前，请确保将可用性组设置为手动故障转移。 站点更新后，可以将故障转移还原为自动进行故障转移。 有关详细信息，请参阅[站点数据库的 SQL Server AlwaysOn](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)。

**重新配置使用 NLB 的软件更新点：**    
Configuration Manager 无法更新使用网络负载均衡 (NLB) 群集来托管软件更新点的站点。

如果为软件更新点使用 NLB 群集，请使用 Windows PowerShell 删除 NLB 群集。
有关详细信息，请参阅[规划软件更新](../../../sum/plan-design/plan-for-software-updates.md)。

**在站点升级安装的过程中，禁用每个站点上的所有站点维护任务：**    
在安装更新之前，请禁用可能会在更新过程进行时运行的任何站点维护任务。 这包括但不限于以下各项：

-   备份站点服务器
-   删除过期的客户端操作
-   删除过期的发现数据

站点数据库维护任务在更新安装过程中运行时，更新安装可能会失败。 在禁用任务之前，请记录该任务的计划，以便在安装更新之后可恢复其配置。

有关详细信息，请参阅 [Configuration Manager 的维护任务](maintenance-tasks.md)和 [Configuration Manager 维护任务参考](reference-for-maintenance-tasks.md)。

**暂时停止 Configuration Manager 服务器上的任何防病毒软件：** 更新站点之前，请确保已停止 Configuration Manager 服务器上的防病毒软件。 <!--SMS.503481-->

**在管理中心站点和主站点上创建站点数据库备份：** 更新站点之前，请备份站点数据库，以确保具有用于灾难恢复的成功备份。

有关详细信息，请参阅 [Configuration Manager 的备份和恢复](backup-and-recovery.md)。

<!-- Removed from update guidance 6/6/2017
**Test the database upgrade on a copy of the most recent site database backup:** 
Before you update a Configuration Manager central administration site or primary site, test the site database upgrade process on a copy of the site database.

-   We recommend that you test the site database upgrade process because when you upgrade a site, the site database might be modified.

-   Although a test database upgrade is not required, it can identify problems for the upgrade before your production database is affected.

-   A failed site database upgrade can render your site database inoperable and might require a site recovery to restore functionality.

-   Although the site database is shared between sites in a hierarchy, plan to test the database at each applicable site before you upgrade that site.

-   If you use database replicas for management points at a primary site, disable replication before you create the backup of the site database.

Configuration Manager does not support the backup of secondary sites nor does it support the test upgrade of a secondary site database.

Do not run a test database upgrade on the production site database. Doing so updates the site database and could render your site inoperable. For more information, see [Step 2: Test the database upgrade before installing an update](install-in-console-updates.md#bkmk_step2) from **Before you install an in-console update**.
-->

**规划客户端试点：**    
安装更新客户端的更新后，可以在新的客户端更新部署和升级所有活动的客户端之前在预生产中对其进行测试。

若要利用此选项，在开始安装更新之前必须配置站点，以支持预生产的自动升级。

有关详细信息，请参阅[升级客户端](../../clients/manage/upgrade/upgrade-clients.md)和[如何在预生产集合中测试客户端升级](../../clients/manage/upgrade/test-client-upgrades.md)。

**计划使用服务时段控制站点服务器安装更新的时间：**    
可使用服务时段定义时间段，在该时段内可安装站点服务器的更新。

这可以帮助你控制层次结构中的站点安装更新的时间。 版本 1606 之前，服务时段被称为维护时段。 有关详细信息，请参阅[站点服务器的服务时段](service-windows.md)。

**运行安装程序先决条件检查程序：**    
当更新在控制台中列为“可用”  时，可以独立运行先决条件检查程序，然后再安装更新。 （在站点上安装更新时，会再次运行必备组件检查程序。）

若要从控制台运行先决条件检查，请转到“管理”>“概述”>“云服务”>“更新和维护服务”。  然后，右键单击“Configuration Manager 1610 更新包”  ，然后选择“运行先决条件检查”  。

有关启动并监视先决条件检查的详细信息，请参阅  [安装 Configuration Manager 控制台内部更新](install-in-console-updates.md)主题中的“步骤 3：安装更新之前运行先决条件检查程序”。

> [!IMPORTANT]  
> 必备组件检查程序作为更新安装的一部分运行或独立运行时，该过程会更新某些用于站点维护任务的产品源文件。 因此，在运行先决条件检查程序后且安装 1610 更新前，如果需要执行站点维护任务，可从站点服务器上的 CD.Latest 文件夹运行 **Setupwpf.exe**（Configuration Manager 安装程序）。

**更新站点：** 现已准备好可以为层次结构开始更新安装。 有关安装更新的信息，请参阅[安装控制台内部更新](install-in-console-updates.md#bkmk_install)

我们建议计划在正常业务时间之外为每个站点安装更新，此时安装更新的过程以及其重新安装站点组件和站点系统角色的操作对业务运营的影响最小。

有关详细信息，请参阅  [Configuration Manager 更新](updates.md)。
