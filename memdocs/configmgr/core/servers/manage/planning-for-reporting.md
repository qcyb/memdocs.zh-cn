---
title: 报表规划
titleSuffix: Configuration Manager
description: 从安装详细信息到安全性和网络带宽，规划 Configuration Manager 中的报表至关重要。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ff920c84-d5c8-458c-b67f-bc7219b05690
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 2621a6a364734a1146700aa8eef8fded3a6e58ab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694365"
---
# <a name="plan-for-reporting-in-configuration-manager"></a>在 Configuration Manager 中规划报表

适用范围：  Configuration Manager (Current Branch)

Configuration Manager 中的报表功能提供一组工具和资源，可帮助你使用 SQL Server Reporting Services 或 Power BI 报表服务器的高级报表功能。 使用以下部分协助规划 Configuration Manager 中的报表。

## <a name="where-to-install-the-reporting-services-point"></a>Reporting Services 点的安装位置

当在站点中运行 Configuration Manager 报表时，报表可以访问所连接的站点数据库中的信息。 使用下列部分来帮助你确定 Reporting Services 点的安装位置和要使用的数据源。

> [!NOTE]
> 有关在 Configuration Manager 中规划站点系统的详细信息，请参阅[添加站点系统角色](../deploy/configure/add-site-system-roles.md)。

### <a name="supported-site-system-servers"></a>支持的站点系统服务器

你可以在管理中心站点 (CAS) 或主站点上安装 Reporting Services 点。 这适用于一个站点上的多个站点系统，以及层次结构中的其他站点。 Configuration Manager 不支持辅助站点上的 Reporting Services 点。 站点上的第一个 Reporting Services 点设置为默认报表服务器。 可在一个站点中添加更多的 Reporting Services 点，但 Configuration Manager 报表主要使用每个站点上的默认报表服务器。 可以在站点服务器或远程站点系统上安装 Reporting Services 点。 为了获得最佳性能，请使用远程站点系统服务器上的 SQL Server Reporting Services。

### <a name="data-replication-considerations"></a>数据复制注意事项

请考虑下列因素，以帮助你确定 Reporting Services 点的安装位置：

- 使用 CAS 数据库作为报表数据源的 Reporting Services 点可以访问 Configuration Manager 层次结构中的所有全局数据和站点数据。 如果需要包含层次结构中多个站点的站点数据的报表，请考虑在 CAS 上的站点系统中安装 Reporting Services 点。 然后，将其数据库用作报表数据源。

- 使用子主站点数据库作为报表数据源的 Reporting Services 点只能访问本地主站点和所有子辅助站点的全局数据及站点数据。 Configuration Manager 层次结构中其他主站点的站点数据不会复制到此主站点。 Reporting Services 无法访问其他主站点的站点数据。 如果需要包含特定主站点的站点数据或全局数据的报表，但不希望用户能够访问其他主站点中的站点数据，请在主站点上的站点系统中安装 Reporting Services 点。 然后，使用主站点的数据库作为报表数据源。

有关全局数据和站点数据的详细信息，请参阅[数据类型](../../plan-design/hierarchy/database-replication.md#types-of-data)。

### <a name="network-bandwidth-considerations"></a>网络带宽注意事项

根据站点的配置方式，同一站点中的站点系统会使用服务器消息块 (SMB)、HTTP 或 HTTPS 相互通信。 Configuration Manager 不会管理此通信。 此通信随时可能发生，且不受网络带宽控制。 在站点系统上安装 Reporting Services 点角色前，请查看可用的网络带宽。

有关规划站点系统的详细信息，请参阅[添加站点系统角色](../deploy/configure/add-site-system-roles.md)。

## <a name="plan-for-role-based-administration"></a>规划基于角色的管理

报表安全与 Configuration Manager 中的其他角色很相似，具体而言，可以将安全角色和权限分配给管理用户。 管理用户只能运行和修改他们具有相应安全权限的报表。 若要在 Configuration Manager 控制台中运行报表，用户需要对**站点**权限的**读取**权限，以及针对特定对象配置的权限。

与 Configuration Manager 中的其他对象不同，在 Configuration Manager 控制台中为管理用户设置的安全权限也会在 Reporting Services 中进行配置。 在 Configuration Manager 控制台中配置安全权限时，Reporting Services 点会连接到 Reporting Services 并为报表设置适当的权限。

例如，**软件更新管理员**安全角色具有**运行报表**和**修改报表**权限。 具有**软件更新管理员**角色的用户只能运行和修改软件更新的报表。 Configuration Manager 控制台不会向此角色显示其他对象的报表。 此行为的例外是，某些报表并未与特定的 Configuration Manager 安全对象关联。 对于这些报表，管理用户必须具有“站点”  权限的“读取”  权才能运行报表，以及“站点”  权限的“修改”  权才能修改报表。  

> [!IMPORTANT]
> 所属的域与 Reporting Services 点帐户所属的域不同的用户需要在两个域之间建立双向信任，才能成功运行报表。

对于基于角色的管理，报表已完全启用。 Configuration Manager 根据运行报表的用户的权限对所有包含的报表的数据进行筛选。 具有特定角色的用户只能查看为其角色定义的信息。

有关报表的安全权限的详细信息，请参阅[配置报表](configuring-reporting.md)。

有关 Configuration Manager 中规划站点系统的详细信息，请参阅[配置基于角色的管理](../deploy/configure/configure-role-based-administration.md)。

## <a name="reporting-recommendations"></a>报表建议

Configuration Manager 中的报表需要考虑以下建议和提示：

- 为了获得最佳性能，请在远程站点系统上安装 Reporting Services 点。 尽管可以在站点服务器上进行安装，但在远程站点系统上安装 Reporting Services 点时性能最佳。 当此角色执行后台处理时，它可以与其他角色争用系统资源。 站点和角色性能需要考虑许多因素，但通常情况下，此配置可提高报表和整体站点性能。

- 优化 SQL Server Reporting Services 查询。 通常情况下，所有报表延迟都因运行查询和检索结果需要花费时间而导致。 查询分析器和探查器等 Microsoft SQL Server 工具可帮助优化查询。

- 将报表订阅处理安排在标准工作时间之外运行。 如果可能，在非工作时间处理订阅可最大限度地减少 Configuration Manager 站点数据库服务器上的 CPU 处理。 这种方案还可改善不可预测报表请求的可用性。

- 站点更新会保留内置报表。 如果修改标准报表，则当站点更新时，它会用下划线前缀 (`_`) 对报表进行重命名。 此行为可以确保站点更新时不会用标准报告覆盖已修改的报表。

## <a name="security-and-privacy"></a>安全和隐私

Configuration Manager 报表显示在标准 Configuration Manager 管理操作过程中收集的信息。 例如，你可以显示 Configuration Manager 已从发现或清单中收集的信息的报表。 报表还可以包含客户端管理操作的当前状态信息，例如正在部署软件和正在检查符合性。

有关 Configuration Manager 操作（可能生成可在报表中查看的数据）的任何安全建议和隐私信息的详细信息，请参阅 [Configuration Manager 的安全和隐私](../../plan-design/security/security-and-privacy.md)。  

## <a name="next-steps"></a>后续步骤

[报表的先决条件](prerequisites-for-reporting.md)
