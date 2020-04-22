---
title: 高可用性
titleSuffix: Configuration Manager
description: 了解如何使用维持高可用性服务的选项部署 Configuration Manager。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1a38421d-24c1-4fef-bf6c-42fce53109ac
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 32083deb30d3d7345ccad8d31541d3c641eb10c0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707265"
---
# <a name="high-availability-options-for-configuration-manager"></a>Configuration Manager 的高可用性选项

适用范围：  Configuration Manager (Current Branch)

本文介绍如何使用维持高可用性服务的选项部署 Configuration Manager。

以下 Configuration Manager 选项支持高可用性：

- 对任何独立主站点配置额外的处于被动模式的站点服务器。  

- 在主站点和管理中心站点上为站点数据库配置 SQL Server Always On 可用性组。

- 站点支持向客户端提供重要服务的站点系统角色的多个实例。 例如，管理点和分发点。  

- 管理中心站点和主站点支持站点数据库备份。 站点数据库存储站点和客户端的所有配置。 层次结构中的站点共享此配置数据。  

- 内置站点恢复选项可以减少服务器停机时间。 当拥有具有管理中心站点的层次结构时，这些高级选项可简化恢复。  

- 客户端可以自动修正典型问题，而无需管理员干预。  

- 站点会生成关于无法提交最新数据的客户端的警报，从而警告管理员注意潜在问题。  

- Configuration Manager 提供了多个内置报表和仪表板。 在发生服务器或客户端操作问题之前，使用这些来识别问题和趋势。  

Configuration Manager 包含多个提供准实时服务的功能。 如果这些功能对于满足业务需求至关重要，请规划和配置站点和层次结构以实现高可用性。 例如：  

- [客户端通知操作](../../../clients/manage/manage-clients.md)，如重启、启动 Windows Defender 扫描或远程桌面。  

- 用于监视软件更新和终结点保护等功能的基于状态的消息。

- [脚本](../../../../apps/deploy-use/create-deploy-scripts.md)

- [CMPivot](../../manage/cmpivot.md)

Configuration Manager 的其他功能不提供实时服务。 这些功能包括但不限于客户端设置、硬件和软件清单、软件部署和符合性设置。 它们的运行预计会存在一些数据延迟。 大多数涉及临时性服务中断的情景通常不会转变为严重问题。 为最大程度地减少停机时间，请保持操作的自主性并提供高水平的服务，在考虑到高可用性的情况下配置站点和层次结构。  

例如，Configuration Manager 客户端通常使用已知的操作计划和配置以及用于将数据提交至站点以进行处理的计划自动运行。  

- 当客户端无法联系站点时，它们会缓存要提交的数据，直到能够与站点联系为止。  

- 无法联系站点的客户端会继续运行。 它们会使用上次已知的计划和缓存信息，直到他们可以联系站点并接收新策略。 例如，客户端可能会保留以前下载的它们必须运行或安装的应用程序。

- 站点会监视其站点系统和客户端以获取定期状态更新。 当这些组件注册失败时，它可以生成警报。  

- 通过内置报表，可以深入了解正在进行的操作、历史操作和当前趋势。 Configuration Manager 支持基于状态的消息，这些消息提供关于正在进行的操作的准实时信息。  


## <a name="high-availability-for-sites-and-hierarchies"></a><a name="bkmk_snh"></a>站点和层次结构的高可用性  

### <a name="use-a-site-server-in-passive-mode"></a>使用被动模式下的站点服务器

为独立主站点安装处于被动模式的额外站点服务器  。 被动模式下的站点服务器是对主动模式下的现有站点服务器的补充  。 在需要时可立即使用被动模式下的站点服务器。 有关详细信息，请参阅[站点服务器高可用性](site-server-high-availability.md)。  

### <a name="use-a-remote-content-library"></a>使用远程内容库

将站点的内容库移动到提供高可用存储的远程位置。 此功能是实现站点服务器高可用性的必要条件。 有关详细信息，请参阅[内容库](../../../plan-design/hierarchy/the-content-library.md#bkmk_remote)。

### <a name="centralize-content-sources"></a>集中内容源

Configuration Manager 中的所有软件内容都需要网络上的包源位置。 使用集中式、高可用存储来托管所有内容的通用包源位置。

### <a name="use-a-sql-server-always-on-availability-group-to-host-the-site-database"></a>使用 SQL Server Always On 可用性组托管站点数据库

在 SQL Server Always On 可用性组上托管主站点和管理中心站点的站点数据库。 有关详细信息，请参阅[高可用性站点数据库的 SQL Server Always On](sql-server-alwayson-for-a-highly-available-site-database.md)。  

### <a name="use-a-sql-server-cluster-to-host-the-site-database"></a>使用 SQL Server 群集承载站点数据库

对管理中心站点或主站点上的数据库使用 SQL Server 群集时，可以使用 SQL Server 中的内置故障转移支持。  

辅助站点无法使用 SQL Server 群集，并且不支持备份或还原其站点数据库。 可以通过从其父主站点中重新安装辅助站点来恢复辅助站点。  

### <a name="deploy-a-hierarchy-of-sites-with-a-central-administration-site-and-one-or-more-child-primary-sites"></a>使用管理中心站点以及一个或多个子主站点来部署站点层次结构

如果你的站点管理网络的重叠段，则此配置可以提供容错功能。 此配置还提供了额外恢复选项，以使用其他站点中可用共享数据库中的信息在恢复的站点中重建站点数据库。 使用此选项替换故障站点数据库的失败备份或不可用备份。  

### <a name="create-regular-backups-at-central-administration-sites-and-primary-sites"></a>在管理中心站点和主站点创建定期备份

创建和测试常规站点备份时，这可确保拥有恢复站点所需的数据。 还可以练习在最短的时间内恢复站点。  

### <a name="install-multiple-instances-of-site-system-roles"></a>安装站点系统角色的多个实例

安装关键站点系统角色的多个实例时，可为客户端提供冗余的联系点。 例如，在特定服务器脱机的情况下，多个管理点和分发点会提供冗余服务。  

### <a name="install-multiple-instances-of-the-sms-provider-at-a-site"></a>在站点上安装 SMS 提供程序的多个实例

SMS 提供程序为一个或多个 Configuration Manager 控制台提供管理联系点。 要提供联系点冗余以管理站点和层次结构，请安装 SMS 提供程序。  


## <a name="high-availability-for-site-system-roles"></a><a name="bkmk_ssr"></a>站点系统角色的高可用性

在每个站点中，你可以部署站点系统角色，以提供想要客户端在该站点上使用的服务。 站点数据库包含站点和所有客户端的配置信息。 使用一个或多个可用选项提供站点数据库高可用性，并在需要时恢复站点和站点数据库。  

### <a name="redundancy-for-important-site-system-roles"></a>重要站点系统角色的冗余

- 应用程序目录 Web 服务点  

- 应用程序目录网站点  

- 分发点  

- 管理点  

- 软件更新点  

- 状态迁移点  

要为站点和客户端上的报告提供冗余，请安装 Reporting Services 点的多个实例。

对于软件更新点的故障转移支持，请使用 Windows PowerShell 在 Windows 网络负载均衡 (NLB) 群集上安装此角色。  

### <a name="built-in-site-backup"></a>内置站点备份

Configuration Manager 包括内置备份任务，以帮助你按照定期计划备份站点和关键信息。 此外，Configuration Manager 安装向导支持站点还原操作，以帮助还原站点操作。  

### <a name="publishing-to-active-directory-domain-services-and-dns"></a>发布到 Active Directory 域服务和 DNS

配置每个站点以将站点的相关数据发布到 Active Directory 域服务和 DNS。 此发布使客户端能够识别网络上最具可访问性的服务器。 客户端还使用它来确认新站点系统服务器何时可用于提供重要服务，例如管理点。  

### <a name="sms-provider-and-configuration-manager-console"></a>SMS 提供程序和 Configuration Manager 控制台

Configuration Manager 支持在单独的服务器上安装多个 SMS 提供程序作为控制台的多个访问点。 如果一个 SMS 提供程序服务器处于脱机状态，仍然可以查看和管理站点和客户端。  

当 Configuration Manager 控制台连接至站点时，它会连接到该站点中的 SMS 提供程序实例。 系统随机选择 SMS 提供程序的实例。 如果所选的 SMS 提供程序不可用，则可以选择：  

- 将控制台重新连接到该站点。 每个新连接请求都会被随机分配一个 SMS 提供程序的实例。 新连接有可能分配到可用实例。  

- 将控制台连接到不同的 Configuration Manager 站点，并管理该连接中的配置。 此选项会使配置更改略微延迟，延迟时间不超过几分钟。 当站点的 SMS 提供程序处于联机状态时，将 Configuration Manager 控制台直接重新连接到想要管理的站点。  

在多个计算机上安装 Configuration Manager 控制台以供管理员使用。 每个 SMS 提供程序都支持多个控制台的连接。  

### <a name="management-point"></a>管理点

在每个主站点上安装多个管理点，并使站点能够将站点数据发布到 Active Directory 基础结构和 DNS。  

多个管理点有助于通过多个客户端对任何单个管理点的使用进行负载平衡。 此外请考虑为管理点安装一个或多个数据库副本。 此配置会减少管理点的处理器密集型操作。 它还会增加此关键站点系统角色的可用性。  

辅助站点仅支持安装一个管理点，该管理点必须位于辅助站点服务器上。 辅助站点的管理点不被视为具有高可用配置。  

> [!NOTE]  
> 通过本地移动设备管理管理的设备仅连接到主站点上的一个管理点。 在注册过程中，Configuration Manager 将管理点分配给移动设备，并且在以后不会发生更改。 安装多个管理点并为移动设备启用多个管理点时，分配给移动设备客户端的管理点具有不确定性。  
>
> 如果移动设备客户端使用的管理点变得不可用，则必须解决此管理点问题，或者必须擦除移动设备并重新注册移动设备，以便它可以分配给为移动设备启用的操作管理点。  

### <a name="distribution-point"></a>分发点

安装多个分发点，并将内容部署到多个分发点。 为每个边界组添加多个分发点，以确保客户端在其内容请求中获得多个选项。 配置边界组关系，以便它们具有到另一个边界组或云分发点的可预测回退行为。 有关详细信息，请参阅[配置边界组](boundary-groups.md)。  

### <a name="application-catalog-web-service-point-and-application-catalog-website-point"></a>应用程序目录 Web 服务点和应用程序目录网站点

> [!Important]
> 从 Current Branch 版本 1806 开始，不支持应用程序目录的 Silverlight 用户体验。 自版本 1906 起，更新后的客户端自动使用管理点进行用户可用的应用程序部署。 仍然无法安装新的应用程序目录角色。 版本 1910 已终止对应用程序目录角色的支持。  
>
> 有关详细信息，请参阅下列文章：
>
> - [配置软件中心](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [已删除和已弃用的功能](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

安装每个站点系统角色的多个实例。 为获得最佳性能，请在同一站点系统服务器上部署其中一个。  

每个应用程序目录站点系统角色都提供与该角色的其他实例相同的信息，而不管其在层次结构中处于何位置。 当客户端请求应用程序目录，并且你已将客户端配置为自动检测默认应用程序目录网站点时，客户端将定向到可用实例。 根据客户端的当前网络位置，客户端会优先选择本地应用程序目录实例。  

有关此客户端设置和自动检测如何工作的详细信息，请参阅[计算机代理](../../../clients/deploy/about-client-settings.md#computer-agent)客户端设置。  


## <a name="high-availability-for-clients"></a><a name="bkmk_client"></a>客户端的高可用性  

### <a name="client-operations-are-autonomous"></a>客户端操作具有自主性

Configuration Manager 客户端自主性包括以下行为：  

- 客户端不需要与任何特定站点系统服务器不断联系。 它们使用已知的配置按计划执行预配置的操作。  

- 客户端可以使用为客户端提供服务的站点系统角色的任何可用实例。 它们会在找到可用的服务器之前一直尝试联系已知服务器。  

- 客户端可以运行清单、软件部署以及与站点系统服务器直接联系无关的类似计划操作。  

- 配置为使用回退状态点的客户端在无法与管理点通信时可以将详细信息提交到回退状态点。  

### <a name="clients-can-repair-themselves"></a>客户端可以修复自身

客户端可以自动修正大多数典型问题而无需管理员直接干预。  

- 客户端会定期对其状态进行自我评估。 它们使用本地缓存的用于修复的修正步骤和源文件来修正典型问题。  

- 当客户端无法将其状态信息提交至其站点时，站点可能会生成警报。 接收这些警报的管理用户可以立即采取措施以还原客户端的正常操作。  

### <a name="clients-cache-information-to-use-in-the-future"></a>客户端缓存信息以在将来使用

当客户端与管理点通信时，客户端可以获取和缓存以下信息：  

- 客户端设置  

- 客户端计划  

- 关于软件部署的信息以及客户端计划安装的软件的下载信息（如果为此操作配置了部署）。  

当客户端无法联系管理点时，客户端会在本地缓存其要向站点报告的状态、状况和客户端信息。 客户端在与管理点建立联系后会传输此数据。  

### <a name="client-can-submit-status-to-a-fallback-status-point"></a>客户端可以将状态提交到回退状态点

将客户端配置为使用回退状态点时，可以提供其他联系点供客户端提交关于其操作的重要详细信息。 配置为使用回退状态点的客户端会继续将关于其操作的状态发送给该站点系统角色，即使客户端无法与管理点通信也不例外。  

### <a name="central-management-of-client-data-and-client-identity"></a>客户端数据和客户端标识的集中管理

站点数据库（而不是单个客户端）保留有关每个客户端的标识的重要信息，并将该数据与特定计算机或用户关联。  

- 可以卸载和重新安装计算机上的客户端源文件，而不会影响安装客户端的计算机的历史记录。  

- 客户端计算机故障不会影响存储在数据库中的信息的完整性。 此信息可以用于生成报表。  


## <a name="options-for-sites-and-site-system-roles-that-arent-highly-available"></a><a name="bkmk_nonHAoptions"></a> 不具备高可用性的站点和站点系统角色的选项

有几个站点系统不支持站点或层次结构中的多个实例。 此信息可用于帮助为这些站点系统脱机做好准备。  

### <a name="asset-intelligence-synchronization-point-hierarchy"></a>资产智能同步点（层次结构）

此站点系统角色不被视为任务关键角色，它在 Configuration Manager 中提供可选的功能。 如果此站点系统脱机，请使用下列选项之一：  

- 分析站点系统脱机的原因。  

- 从当前服务器中卸载角色，然后在新服务器上安装角色。  

### <a name="endpoint-protection-point-hierarchy"></a>终结点保护点（层次结构）

此站点系统角色不被视为任务关键角色，它在 Configuration Manager 中提供可选的功能。 如果此站点系统脱机，请使用下列选项之一：  

- 分析站点系统脱机的原因。  

- 从当前服务器中卸载角色，然后在新服务器上安装角色。  

### <a name="enrollment-point-site"></a>注册点（站点）

此站点系统角色不被视为任务关键角色，它在 Configuration Manager 中提供可选的功能。 如果此站点系统脱机，请使用下列选项之一：  

- 分析站点系统脱机的原因。  

- 从当前服务器中卸载角色，然后在新服务器上安装角色。  

### <a name="enrollment-proxy-point-site"></a>注册代理点（站点）

此站点系统角色不被视为任务关键角色，它在 Configuration Manager 中提供可选的功能。 但是，可以在一个站点中和在层次结构的多个站点中安装此站点系统角色的多个实例。 如果此站点系统脱机，请使用下列选项之一：  

- 分析站点系统脱机的原因。  

- 从当前服务器中卸载角色，然后在新服务器上安装角色。  

如果在一个站点中具有多台注册代理服务器，则将 DNS 别名用于服务器名称。 如果使用此配置，DNS 轮循机制能在用户注册移动设备时提供一定程度的容错和负载平衡。  

### <a name="fallback-status-point-site-or-hierarchy"></a>回退状态点（站点或层次结构）

此站点系统角色不被视为任务关键角色，它在 Configuration Manager 中提供可选的功能。 如果此站点系统脱机，请使用下列选项之一：  

- 分析站点系统脱机的原因。  

- 从当前服务器中卸载角色，然后在新服务器上安装角色。 由于在客户端安装过程中已将回退状态点分配给客户端，因此需要修改现有客户端以使用新的站点系统服务器。  

### <a name="service-connection-point-hierarchy"></a>服务连接点（层次结构）

虽然此站点系统角色对于使 Configuration Manager Current Branch 保持最新而言至关重要，但通常不会频繁使用它。 如果此系统脱机，请使用下列选项之一：

- 分析站点系统脱机的原因。  

- 从当前服务器中卸载角色，然后在新服务器上安装角色。  


## <a name="see-also"></a>另请参阅

- [支持的配置](../../../plan-design/configs/supported-configurations.md)  

- [推荐硬件](../../../plan-design/configs/recommended-hardware.md)  

- [站点系统服务器支持的操作系统](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md)

- [站点和站点系统先决条件](../../../plan-design/configs/site-and-site-system-prerequisites.md)  

- [站点失败影响](../../manage/site-failure-impacts.md)  
