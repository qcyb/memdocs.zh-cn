---
title: 软件更新维护
titleSuffix: Configuration Manager
description: 若要在 Configuration Manager 中维护更新，可以计划 WSUS 清理任务，也可以手动运行它。
author: mestew
ms.date: 12/17/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 4b0e2e90-aac7-4d06-a707-512eee6e576c
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: a327d50a2743f81407530355b6fd5101ce6a8b02
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88696899"
---
# <a name="software-updates-maintenance"></a>软件更新维护

适用范围：  Configuration Manager (Current Branch)

可从 Configuration Manager 控制台和软件更新点组件属性中计划和运行 WSUS 清理任务。 首次选择运行 WSUS 清理任务时，它将在下一次软件更新同步后运行。  

## <a name="to-schedule-and-run-the-wsus-cleanup-job"></a>计划和运行 WSUS 清理作业

通过运行以下步骤来计划 WSUS 清理作业：

1. 在 Configuration Manager 控制台中，导航到“管理”   > “概述”   > “站点配置”   > “站点”  。
2. 选择 Configuration Manager 层次结构顶部的站点。

3. 单击“设置”  组中的  “配置站点组件”，然后单击“软件更新点”  以打开软件更新点组件属性。  

4. 评审“取代行为”  。 如果需要，修改行为。

   ![取代行为屏幕截图](media/supersedence-behavior.png)

5. 单击“取代规则”选项卡，选择“运行 WSUS 清理向导”   。 在版本 1806 中，该选项重命名为“同步后运行 WSUS 清理”  。

6. 单击“确定”（如果运行版本 1806，请单击“关闭”）   。

## <a name="wsus-cleanup-behavior-in-version-1802-and-earlier"></a>版本 1802 及更早版本中的 WSUS 清理行为

在 Configuration Manager 版本 1806 之前，WSUS 清理选项运行以下项：

- 仅限顶层站点的 WSUS 服务器上的 WSUS 清理向导中的“过期更新”选项  。

  ![WSUS 已过期更新清理屏幕截图](media/wsus-cleanup-expired.PNG)

- Configuration Manager 数据库中的软件更新配置项每七天进行一次清理，并从控制台中删除不需要的更新。
  - 如果当前已部署，则此清理不会从 Configuration Manager 控制台中删除过期的更新。

顶层 WSUS 数据库和环境中的所有其他 WSUS 数据库仍需其他维护。 有关详细信息和说明，请参阅 [Microsoft WSUS 和 Configuration Manager SUP 维护](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/)博客文章的完整指南。

## <a name="wsus-cleanup-behavior-starting-in-version-1806"></a>从版本 1806 开始的 WSUS 清理行为

自版本 1806 起，WSUS 清理选项在每次同步后出现，并执行以下清理项：
<!--1357898 -->

- CAS 和主站点上的 WSUS 服务器的“已过期更新”选项  。
  - 用于辅助站点的 WSUS 服务器不会针对过期更新运行 WSUS 清理。
- Configuration Manager 从其数据库构建已取代的更新列表。 该列表基于“软件更新点”组件属性中的取代行为。
  - 符合取代行为标准的更新配置项在 Configuration Manager 控制台中已过期。
  - 在 WSUS 中，对于 CAS 和主站点拒绝更新，但对于辅助站点不拒绝更新。
- Configuration Manager 数据库中的软件更新配置项每七天进行一次清理，并从控制台中删除不需要的更新。
  - 如果当前已部署，则此清理不会从 Configuration Manager 控制台中删除过期的更新。

> [!NOTE]
> “取代更新过期前需等待的月数”基于取代更新的创建日期。 例如，如果将此设置设为 2 个月，则在 WSUS 中已被取代的更新将被拒绝，而在 Configuration Manager 中，如果取代更新存在 2 个月，更新将过期。

需要在辅助站点 WSUS 数据库上手动运行所有 WSUS 维护。 CAS 和主站点上未运行以下“WSUS 服务器清理向导”选项  ：

- 未使用的更新和更新修订
- 未联系服务器的计算机
- 不需要的更新文件

  有关详细信息和说明，请参阅 [Microsoft WSUS 和 Configuration Manager SUP 维护](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/)博客文章的完整指南。

## <a name="wsus-cleanup-behavior-starting-in-version-1810"></a>从版本 1810 开始的 WSUS 清理行为

从版本 1810 开始，可以在软件更新点组件属性中指定独立于非功能更新的功能更新的取代规则。 WSUS 清理选项在每次同步后出现，并执行以下清理项：
<!--2839349,3098809, 2977644-->

- CAS、主站点和辅助站点上 WSUS 服务器的“已过期更新”选项  。
- Configuration Manager 从其数据库构建已取代的更新列表。 该列表基于“软件更新点”组件属性中的取代行为。
  - 符合取代行为标准的更新配置项在 Configuration Manager 控制台中已过期。
  - 在 WSUS 中拒绝为 CAS、主站点和辅助站点更新。
- Configuration Manager 数据库中的软件更新配置项每七天进行一次清理，并从控制台中删除不需要的更新。
  - 如果当前已部署，则此清理不会从 Configuration Manager 控制台中删除过期的更新。

> [!NOTE]
> “取代更新过期前需等待的月数”基于取代更新的创建日期。 例如，如果将此设置设为 2 个月，则在 WSUS 中已被取代的更新将被拒绝，而在 Configuration Manager 中，如果取代更新存在 2 个月，更新将过期。

CAS、主站点和辅助站点上不运行以下“WSUS 服务器清理向导”选项  ：

- 未使用的更新和更新修订
- 未联系服务器的计算机
- 不需要的更新文件

  有关详细信息和说明，请参阅 [Microsoft WSUS 和 Configuration Manager SUP 维护](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/)博客文章的完整指南。

## <a name="wsus-cleanup-starting-in-version-1906"></a>从版本 1906 开始的 WSUS 清理
<!--41101009-->

 你具有 Configuration Manager 为维护软件更新点正常运行而执行的其他 WSUS 维护任务。 除了可以拒绝 WSUS 中的已到期更新，Configuration Manager 还能向 WSUS 数据库添加非聚集索引，以及从 WSUS 数据库中删除过时的更新。 每次同步后都会进行 WSUS 维护。

### <a name="decline-expired-updates-in-wsus-according-to-supersedence-rules"></a>根据取代规则在 WSUS 中拒绝过期的更新

在 WSUS 中拒绝更新可以从发送到客户端的目录中删除这些更新，从而提升性能。 拒绝配置管理器标记为“已取代”的更新可进一步最小化目录并提升性能。

1. 在 Configuration Manager 控制台中，导航到“管理”   > “概述”   > “站点配置”   > “站点”  。
2. 选择 Configuration Manager 层次结构顶部的站点。
3. 单击“设置”组中的“配置站点组件”  ，再单击“软件更新点”  ，以打开“软件更新点组件属性”。
4. 在“WSUS 维护”  选项卡中，选中“根据取代规则在 WSUS 中拒绝过期的更新”  。

### <a name="add-non-clustered-indexes-to-the-wsus-database-to-improve-wsus-cleanup-performance"></a>将非聚集索引添加到 WSUS 数据库以提高 WSUS 清理性能

添加非聚集索引可提升 Configuration Manager 启动的 WSUS 清理性能。

1. 在 Configuration Manager 控制台中，导航到“管理”   > “概述”   > “站点配置”   > “站点”  。
2. 选择 Configuration Manager 层次结构顶部的站点。
3. 单击“设置”组中的“配置站点组件”  ，再单击“软件更新点”  ，以打开“软件更新点组件属性”。
4. 在“WSUS 维护”  选项卡中，选择“向 WSUS 数据库添加非聚集索引”  。
5. 在 Configuration Manager 使用的各个 SUSDB 上，它向下面的表添加索引：
   - tbLocalizedPropertyForRevision
   - tbRevisionSupersedesUpdate

#### <a name="sql-permissions-for-creating-indexes"></a>用于创建索引的 SQL 权限

如果 WSUS 数据库位于远程 SQL Server 中，则可能需要在 SQL 中添加用于创建索引的权限。 用于连接到 WSUS 数据库和创建索引的帐户可能会有所不同。 如果指定[软件更新点属性中的 WSUS 服务器连接帐户](../get-started/install-a-software-update-point.md#wsus-server-connection-account)，请确保该连接帐户具有 SQL 权限。 如果未指定 WSUS 服务器连接帐户，则站点服务器的计算机帐户需要 SQL 权限。

- 必须对表或视图拥有 `ALTER` 权限，才能创建索引。 帐户必须是 `sysadmin` 固定服务器角色的成员，或是 `db_ddladmin` 和 `db_owner` 固定数据库角色的成员。 若要详细了解如何创建索引和权限，请参阅 [CREATE INDEX (Transact-SQL)](/sql/t-sql/statements/create-index-transact-sql?view=sql-server-2017#permissions)。
- 必须向帐户授予 `CONNECT SQL` 服务器权限。 有关详细信息，请参阅 [GRANT 服务器权限 (Transact-SQL)](/sql/t-sql/statements/grant-server-permissions-transact-sql?view=sql-server-2017)。

> [!NOTE]  
>  如果 WSUS 数据库位于使用非默认端口的远程 SQL Server 上，可能无法添加索引。 在这种情况下，可以[使用 SQL Server Configuration Manager 创建服务器别名](/sql/database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client?view=sql-server-2017)。 在别名已添加且 Configuration Manager 可以连接到 WSUS 数据库后，索引便会添加。

### <a name="remove-obsolete-updates-from-the-wsus-database"></a>从 WSUS 数据库中删除过时的更新

过时更新是 WSUS 数据库中未使用的更新和更新修订。 一般而言，如果更新不再存在于 [Microsoft 更新目录](https://www.catalog.update.microsoft.com/)中，则该更新将视为已过时，其他更新就不再需要将其作为先决条件或依赖项。

1. 在 Configuration Manager 控制台中，导航到“管理”   > “概述”   > “站点配置”   > “站点”  。
2. 选择 Configuration Manager 层次结构顶部的站点。
3. 单击“设置”组中的“配置站点组件”  ，再单击“软件更新点”  ，以打开“软件更新点组件属性”。
4. 在“WSUS 维护”选项卡上，选择“从 WSUS 数据库中删除过时更新”   。
   - 允许在停止前，运行过时更新删除最长 30 分钟。 它将在下一次同步发生后再次启动。  

#### <a name="sql-permissions-for-removing-obsolete-updates"></a>用于删除过时更新的 SQL 权限

当 WSUS 数据库位于远程 SQL 服务器上时，站点服务器的计算机帐户需要拥有以下 SQL 权限：

- `db_datareader` 和 `db_datawriter` 固定数据库角色。 有关详细信息，请参阅[数据库级别角色](/sql/relational-databases/security/authentication-access/database-level-roles?view=sql-server-2017#fixed-database-roles)。
- 必须向站点服务器的计算机帐户授予 `CONNECT SQL` 服务器权限。 有关详细信息，请参阅 [GRANT 服务器权限 (Transact-SQL)](/sql/t-sql/statements/grant-server-permissions-transact-sql?view=sql-server-2017)。

#### <a name="wsus-cleanup-wizard"></a>WSUS 清理向导

从版本 1906 起，CAS、主站点和辅助站点上不运行以下“WSUS 服务器清理向导”选项  ：

- 未联系服务器的计算机
- 不需要的更新文件

  有关详细信息和说明，请参阅 [Microsoft WSUS 和 Configuration Manager SUP 维护](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/)博客文章的完整指南。


### <a name="known-issues-for-version-1906"></a>版本 1906 的已知问题

请考虑以下情形：
<!--5418148-->
- 你使用的是 Configuration Manager 版本 1906
- 因此具有使用 Windows 内部数据库的远程软件更新点
- 在“软件更新点组件属性”的“WSUS 维护”选项卡下，可以选择以下任一项   ：
   - 将非聚集索引添加到 WSUS 数据库
   - 从 WSUS 数据库中删除过时的更新

在这种情况下，Configuration Manager 无法使用 Windows 内部数据库对远程软件更新点执行上述 WSUS 维护任务。 导致此问题是因为 Windows 内部数据库不允许远程连接。 站点服务器上的 `WSyncMgr.log` 中将显示以下错误：

```text
Indexing Failed. Could not connect to SUSDB.
SqlException thrown while connect to SUSDB in Server: <SUP.CONTOSO.COM>. Error Message: A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible. Verify that the instance name is correct and that SQL Server is configured to allow remote connections. (provider: Named Pipes Provider, error: 40 - Could not open a connection to SQL Server)
...
Could not Delete Obselete Updates because ConfigManager could not connect to SUSDB: A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible. Verify that the instance name is correct and that SQL Server is configured to allow remote connections. (provider: Named Pipes Provider, error: 40 - Could not open a connection to SQL Server) UpdateServer: <SUP.CONTOSO.COM>
```

若要解决此问题，可以使用 Windows 内部数据库为远程软件更新点自动执行 WSUS 维护。 有关详细信息和详细步骤，请参阅 [Microsoft WSUS 和 Configuration Manager SUP 维护的完整指南](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint)。

## <a name="updates-cleanup-log-entries"></a>更新清理日志条目

可通过查看以下条目的 wsyncmgr.log 来验证此清理：

- 看到此日志项目时，WSUS 中已取代更新的拒绝已完成：`Cleanup processed <number> total updates and declined <number>`
- 看到此项目时，WSUS 清理开始：`Calling WSUS Cleanup.`
- 看到此项目时，已完成对已过期更新的 WSUS 清理：`Successfully completed WSUS Cleanup.`
- 看到此项目时，Configuration Manager 过期更新配置项清理开始：`Deleting old expired updates...`
- 看到此项目时，Configuration Manager 过期更新配置项清理已完成：`Deleted <number> expired updates total`