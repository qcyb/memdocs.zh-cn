---
title: 卸载站点
titleSuffix: Configuration Manager
description: 有关删除角色以及卸载站点和层次结构的指南
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d466edd2-97f0-44c1-a73e-d71abbdbf4a8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a90d6f34370b8c3167272bce1a0a673cc5074094
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700525"
---
# <a name="uninstall-roles-sites-and-hierarchies-in-configuration-manager"></a>在 Configuration Manager 中卸载角色、站点和层次结构

适用范围：  Configuration Manager (Current Branch)

可将本文用作指南来卸载 Configuration Manager 站点系统角色、站点或层次结构。

从版本 2002 开始，还可以从层次结构中删除管理中心站点 (CAS)，但保留主站点。

## <a name="site-system-role"></a><a name="bkmk_role"></a> 站点系统角色

由于以下原因，可能需要从站点系统服务器中删除角色：

- 较广泛的基础结构更改，如网络或物理位置
- 对基础服务器解除授权
- 合并角色以降低成本和复杂性
- 重新配置或重新设计站点角色
- 停止使用角色支持的功能

确定需要删除角色时，请先考虑以下问题的答案：

- 站点中是否仍需要该角色？ 如果是，另一个站点系统是否已具有该角色？

- 具有此角色的其他站点系统是否已正确调整大小以支持性能和可用性方面的业务要求？

- 是否所有客户端都已重新配置为使用另一个角色？ 是否依赖于默认客户端行为来回退或发现其他服务器？

### <a name="procedure-to-remove-a-site-system-role"></a>删除站点系统角色的过程

使用以下过程可删除角色：

1. 在 Configuration Manager  控制台中，转到“管理”  工作区。 展开“站点配置”，然后选择“服务器和站点系统角色”节点   。

1. 选择具有要删除的角色的站点系统服务器。 在“站点系统角色”  详细信息窗格中，选择目标角色。

1. 在功能区中“站点角色”  选项卡上的“站点角色”  组中，选择“删除角色”  。 确认要删除角色。

### <a name="additional-information-for-specific-roles"></a>特定角色的其他信息

某些角色可能具有其他步骤和注意事项。

#### <a name="software-update-point"></a>软件更新点

删除软件更新点之后，Configuration Manager 会更新客户端策略以从列表中删除软件更新点。 删除站点中的最后一个软件更新点后，软件更新点列表不包含任何软件更新点。 如果没有可用角色，则软件更新管理实质上在站点上处于禁用状态。

当主站点中有多个软件更新点，而且你删除了作为同步源的软件更新点时，请将站点中的另一个软件更新点选为新的同步源。

## <a name="secondary-site"></a><a name="bkmk_secondary"></a> 辅助站点  

除了在[对层次结构解除授权](#bkmk_hierarchy)时以外，删除辅助站点的主要原因是较广泛的基础结构更改，如网络或物理位置。 还需查看[选择辅助站点](../../../plan-design/hierarchy/design-a-hierarchy-of-sites.md#BKMK_ChooseSecondary)的原因。

确定需要删除辅助站点时，请先考虑以下问题的答案：

- 是否从站点服务器中删除了所有站点系统角色？

- 是否有与辅助站点关联的任何边界或边界组？ 在删除站点之前重新配置边界。

- 是否有客户端仍处于该位置？

- 是否配置了其他内容管理选项（如[对等缓存](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#peer-caching-technologies)）？

### <a name="options-to-delete-secondary-sites"></a>用于删除辅助站点的选项

无法将辅助站点移动或重新分配到其他主站点。 从直接父站点中删除辅助站点时，请选择是要卸载还是删除它。

#### <a name="uninstall-the-secondary-site"></a>卸载辅助站点

使用此选项可删除可从网络中访问的正常运行的辅助站点。 此选项会从辅助站点服务器中卸载 Configuration Manager。 然后，它会从 Configuration Manager 站点中删除有关站点及其资源的所有信息。

如果 Configuration Manager 为辅助站点安装了 SQL Server Express，则 Configuration Manager 也会卸载 SQL Express。 如果是在安装辅助站点之前安装的 SQL Server Express，则 Configuration Manager 不会卸载 SQL Server Express。

#### <a name="delete-the-secondary-site"></a>删除辅助站点

可在以下情况中使用此选项：

- 安装失败

- 卸载之后，Configuration Manager 控制台仍会显示辅助站点

    此选项会从 Configuration Manager 层次结构中删除有关站点及其资源的所有信息，但不对站点服务器进行任何更改。

    > [!TIP]
    >  也可使用层次结构维护工具和 /DELSITE  选项来删除辅助站点。 有关详细信息，请参阅[层次结构维护工具 (Preinst.exe)](../../manage/hierarchy-maintenance-tool-preinst.exe.md)。

### <a name="prerequisites-to-delete-a-secondary-site"></a>删除辅助站点的先决条件

运行 Configuration Manager 安装程序的管理用户需要以下安全权限：

- 辅助站点服务器上的本地“管理员”  权限

- 如果主站点数据库服务器是主站点服务器的远程服务器，则为主站点的远程站点数据库服务器上的本地“管理员”  权限。

- 父主站点上的“基础结构管理员”  或“完全权限管理员”  安全角色

- 辅助站点数据库上的 Sysadmin  权限

### <a name="procedure-to-delete-a-secondary-site"></a>删除辅助站点的过程

使用以下过程可卸载或删除辅助站点：

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“站点配置”，然后选择“站点”节点    。

1. 选择要删除的辅助站点服务器。 在功能区的“主页”  选项卡上的“站点”  组中，选择“删除”  。

1. 在“常规”  页上，选择是卸载还是删除辅助站点。

1.  完成向导。

## <a name="primary-site"></a><a name="bkmk_primary"></a> 主站点  

由于以下原因，你可能需要从层次结构中卸载主站点：

- 合并站点以降低成本和复杂性
- 重新配置或重新设计层次结构的站点

在卸载将[分布式视图](../../../plan-design/hierarchy/database-replication.md#bkmk_distviews)用于指向 CAS 的复制链接的子级主站点之前，请先在层次结构中关闭分布式视图。 有关详细信息，请参阅 [卸载配置为具有分布式视图的主站点](#bkmk_distviews)。

### <a name="plan-to-uninstall-a-primary-site"></a><a name="bkmk_pri-plan"></a> 计划卸载主站点

卸载主站点之前，请查看以下任务：

- 查看边界、边界组和回退关系。 如果将客户端分配到新站点，但不更改边界，则可以将它们视为漫游。 有关详细信息，请参阅[定义站点边界和边界组](../configure/define-site-boundaries-and-boundary-groups.md)。

- 确保将所有活动客户端重新分配到层次结构中的其他主站点。 否则，在卸载站点之后，客户端将不受管理。 有关详细信息，请参阅[如何向站点分配客户端](../../../clients/deploy/assign-clients-to-a-site.md)。

  - 查看站点角色的列表，以确保新站点提供相同级别的服务。

  - 确保已正确调整在其他站点中具有此角色的其他站点系统的大小。 它们需要通过其他客户端来支持性能和可用性方面的业务要求。

  - 如果此站点具有大量客户端，请分阶段重新分配它们。 在客户端刷新完整清单和其他特定于站点的数据时，监视数据库复制。 如果管理软件更新，则客户端会分配到新的软件更新点。 此行为会导致完整扫描以实现更新合规性。

  - 客户端重新分配可能会影响依赖于清单数据的报表和查询，以及基于状态的合规性。 请考虑在转换过程中临时调整任何客户端周期。

  - 查看所有客户端分配方法，以确保不引用此主站点。

- 检查层次结构中任何主动使用的对象是否具有对站点代码的静态引用。 例如，集合查询、任务序列或管理脚本。

- 如果层次结构对自动站点分配使用[回退站点](../configure/boundary-group-procedures.md#bkmk_site-fallback)，请确保它不引用此主站点。

- 重新配置任何可能引用静态站点代码的[客户端安装方法](../../../clients/deploy/plan/client-installation-methods.md)。

- 如果此主站点具有任何特定于站点的云附加服务，请确保删除它们。 如果仍需要云资源，请将它们移动到层次结构中的其他主站点。 从要卸载的主站点中删除它们，然后将它们添加到其他主站点。

- 如果此主站点对层次结构具有任何[发现方法](../configure/run-discovery.md)，请将它们移动到其他站点。

- 停用任何基于站点的[操作系统部署介质](../../../../osd/deploy-use/create-task-sequence-media.md)。

- 从站点和站点服务器中删除所有站点系统角色。 有关详细信息，请参阅[卸载站点系统角色](#bkmk_role)。 尽管此准备步骤不是必需的，但它可帮助在卸载站点之前识别任何其他依赖项。

- 卸载此主站点下的任何辅助站点。 有关详细信息，请参阅[辅助站点](#bkmk_secondary)。

### <a name="prerequisites-to-uninstall-a-primary-site"></a><a name="bkmk_pri-prereq"></a> 卸载主站点的先决条件

运行 Configuration Manager 安装程序的管理用户需要以下安全权限：

- CAS 服务器上的本地“管理员”  权限

- 如果 CAS 数据库服务器是站点服务器的远程服务器，则为 CAS 的远程站点数据库服务器上的本地“管理员”  权限。

- CAS 站点数据库上的 Sysadmin  权限

- 主站点服务器上的本地“管理员”  权限

- 如果主站点数据库服务器是主站点服务器的远程服务器，则为主站点的远程站点数据库服务器上的本地“管理员”  权限。

- CAS 上的“基础结构管理员”  或“完全权限管理员”  安全角色

### <a name="procedure-to-uninstall-a-primary-site"></a><a name="bkmk_pri-process"></a> 卸载主站点的过程

运行 Configuration Manager 安装程序来卸载没有关联辅助站点的主站点。 使用以下过程可卸载主站点：

> [!TIP]
> 如果主站点服务器不再可用，请使用 CAS 上的层次结构维护工具从站点数据库中删除主站点。 有关详细信息，请参阅[层次结构维护工具 (Preinst.exe)](../../manage/hierarchy-maintenance-tool-preinst.exe.md)。

1. 通过使用以下方法之一在主站点服务器上启动 Configuration Manager 安装程序：

    - 在“开始”  菜单上，选择“Configuration Manager 安装程序”  。

    - 在 Configuration Manager 安装介质  的目录中，打开 `\SMSSETUP\BIN\X64\setup.exe`。 确保此版本与站点版本相同。

    - 在安装  Configuration Manager 的目录中，打开 `\BIN\X64\setup.exe`。

1. 查看“准备工作”  页上的信息。

1. 在“开始使用”  页上，选择“卸载 Configuration Manager 站点”  。

    > [!IMPORTANT]  
    >  如果辅助站点附加到主站点，则你必须删除辅助站点，然后才能卸载主站点。  

1. 在“卸载 Configuration Manager 站点”  页上，以下两个选项在默认情况下处于启用状态：

    - 从主站点服务器中删除站点数据库
    - 删除 Configuration Manager 控制台

1. 选择“是”  以确认卸载 Configuration Manager 主站点。

### <a name="uninstall-a-primary-site-that-uses-distributed-views"></a><a name="bkmk_distviews"></a> 卸载使用分布式视图的主站点

1. 卸载子级主站点之前，请关闭层次结构中 CAS 与主站点之间的每个链接上的分布式视图。

1. 在每个链接上关闭分布式视图之后，请确认主站点中的数据在 CAS 上完成重新初始化。 若要监视数据的初始化，请参阅[监视复制](../../manage/monitor-replication.md)。

1. 在数据使用 CAS 成功重新初始化之后，可以[卸载主站点](#bkmk_pri-process)。

1. 成功卸载主站点后，可以在从 CAS 到其他主站点的链接上重新配置分布式视图。

    > [!IMPORTANT]
    > 如果在卸载主站点后才在每个站点上关闭分布式视图，或者之后才在 CAS 上成功重新初始化主站点中的数据，则数据复制可能会失败。

## <a name="decommission-a-hierarchy"></a><a name="bkmk_hierarchy"></a> 对层次结构解除授权

由于合并、收购、测试环境或其他业务要求，某些组织具有多个层次结构。 如果将管理合并到单个层次结构，则此操作可以帮助降低成本和复杂性。 对层次结构解除授权的另一个原因是要迁移到仅限云的管理服务（如 Microsoft Intune），并且已准备好删除本地基础结构。

要取消标记具有多个站点的层次结构，删除的顺序非常重要。 从卸载层次结构底部的站点开始，然后向上移动：

1. 删除连接到主站点的辅助站点。
2. 卸载主站点。
3. 卸载所有主站点之后，可以卸载 CAS。

有关详细信息，请参阅以下各节：

- [删除辅助站点](#bkmk_secondary)
- [卸载主站点](#bkmk_primary)
- [卸载 CAS](#bkmk_uninstall-cas)

### <a name="uninstall-the-cas"></a><a name="bkmk_uninstall-cas"></a> 卸载 CAS

对层次结构解除授权的最后一个步骤是卸载 CAS。 运行 Configuration Manager 安装程序来卸载没有子级主站点的 CAS。

#### <a name="prerequisites-to-uninstall-the-cas"></a>卸载 CAS 的先决条件

运行 Configuration Manager 安装程序的管理用户需要以下安全权限：

- CAS 服务器上的本地“管理员”  权限

- 如果 CAS 数据库服务器是站点服务器的远程服务器，则为 CAS 的远程站点数据库服务器上的本地“管理员”  权限。

#### <a name="procedure-to-uninstall-the-cas"></a>卸载 CAS 的过程

1. 使用以下方法之一在 CAS 服务器上启动 Configuration Manager 安装程序：

    - 在“开始”  菜单上，选择“Configuration Manager 安装程序”  。

    - 在 Configuration Manager 安装介质  的目录中，打开 `\SMSSETUP\BIN\X64\setup.exe`。 确保此版本与站点版本相同。

    - 在安装  Configuration Manager 的目录中，打开 `\BIN\X64\setup.exe`。

1. 查看“准备工作”  页上的信息。

1. 在“开始使用”  页上，选择“卸载 Configuration Manager 站点”  。

    > [!IMPORTANT]  
    >  先删除所有子级主站点，然后才能卸载 CAS。  

1. 在“卸载 Configuration Manager 站点”  页上，以下两个选项在默认情况下处于启用状态：

    - 从 CAS 服务器中删除站点数据库
    - 删除 Configuration Manager 控制台

1. 选择“是”  以确认卸载 Configuration Manager 管理中心站点 (CAS)。

## <a name="remove-the-cas"></a><a name="bkmk_remove-cas"></a> 删除 CAS

<!-- 3607277 -->

从版本 2002 开始，如果层次结构由 CAS 和单个子级主站点组成，则可以删除 CAS。 此操作可将 Configuration Manager 基础结构简化为单个独立主站点。 它可消除站点到站点复制的复杂性，并将管理任务集中到单个站点。

有关详细信息，请参阅[删除 CAS](remove-central-administration-site.md)。
