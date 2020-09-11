---
title: 支持的 SQL Server 版本
titleSuffix: Configuration Manager
description: 获取托管 Configuration Manager 站点数据库的 SQL Server 版本和配置要求。
ms.date: 06/24/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 35e237b6-9f7b-4189-90e7-8eca92ae7d3d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5043967a640b937784c22ea2b74269a2f2043ba9
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607640"
---
# <a name="supported-sql-server-versions-for-configuration-manager"></a>Configuration Manager 支持的 SQL Server 版本

适用范围：Configuration Manager (Current Branch)

每个 Configuration Manager 站点都需要受支持的 SQL Server 版本和配置来托管站点数据库。  

## <a name="sql-server-instances-and-locations"></a><a name="bkmk_Instances"></a> SQL Server 实例和位置

### <a name="central-administration-site-and-primary-sites"></a>管理中心站点和主站点

站点数据库必须使用 SQL Server 的完整安装。  

SQL Server 可位于以下位置：  

- 站点服务器计算机。  
- 远离站点服务器的计算机。  

支持以下实例：  

- SQL Server 的默认或已命名实例。  
- 多个实例配置。  
- SQL Server 群集。 请参阅[使用 SQL Server 群集托管站点数据库](../../servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md)。
- SQL Server AlwaysOn 可用性组。 有关详细信息，请参阅[高可用性站点数据库的 SQL Server AlwaysOn](../../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)。

### <a name="secondary-sites"></a>辅助站点

站点数据库可使用完整安装的 SQL Server 或 SQL Server Express 的默认实例。  

SQL Server 必须位于站点服务器计算机上。  

### <a name="limitations-to-support"></a>支持限制

不支持下列配置：

- 网络负载均衡 (NLB) 群集配置中的 SQL Server 群集
- 群集共享卷 (CSV) 上的 SQL Server 群集
- SQL Server 数据库镜像技术和对等复制

SQL Server 事务复制仅支持将对象复制到配置为使用[数据库副本](../../servers/deploy/configure/database-replicas-for-management-points.md)的管理点。  

## <a name="supported-versions-of-sql-server"></a><a name="bkmk_SQLVersions"></a> 支持的 SQL Server 版本

在含有多个网站的层次结构中，各个网站可以使用不同版本的 SQL Server 托管网站数据库。 只要满足以下各项：

- Configuration Manager 支持你使用的 SQL Server 版本。
- Microsoft 仍支持你使用的 SQL Server 版本。
- SQL Server 支持在两个 SQL Server 版本之间进行复制。 有关详细信息，请参阅 [SQL Server 复制向后兼容性](/sql/relational-databases/replication/replication-backward-compatibility)。

对于 SQL Server 2016 和更早版本，对每个 SQL 版本和 Service Pack 的支持均遵循 [Microsoft 生命周期策略](https://aka.ms/sqllifecycle)。 对特定 SQL Server Service Pack 的支持包括累积更新，除非中断对基本 Service Pack 版本的后向兼容性。 从 SQL Server 2017 开始，将不会发布 Service Pack，因为它遵循[新式服务模型](/archive/blogs/sqlreleaseservices/announcing-the-modern-servicing-model-for-sql-server)。 SQL Server 团队建议在累积更新发布时进行持续的[主动安装](/archive/blogs/sqlreleaseservices/announcing-updates-to-the-sql-server-incremental-servicing-model-ism)。

除非另行指定，否则 Configuration Manager 的所有活动版本均支持以下版本的 SQL Server。 如果添加了对新 SQL Server 版本的支持，则将显示添加该支持的 Configuration Manager 版本。 同样，如果弃用支持，则查找有关受影响的 Configuration Manager 版本的详细信息。

> [!IMPORTANT]  
> 为管理中心站点上的数据库使用 SQL Server Standard 时，会限制层次结构可支持的客户端总数。 请参阅 [调整大小和扩展数量](size-and-scale-numbers.md)。

### <a name="sql-server-2019-standard-enterprise"></a>SQL Server 2019：Standard、Enterprise

自 Configuration Manager 版本 1910 起，可以将此版本与累积更新 5 (CU5) 或更高版本结合使用，但前提是累积更新版本受到 SQL 生命周期支持。 CU5 是 SQL Server 2019 的最低要求，因为它解决了[标量 UDF 内联](/sql/relational-databases/user-defined-functions/scalar-udf-inlining)问题。

此版本的 SQL 可用于以下站点：

- 管理中心站点
- 主站点
- 辅助站点

<!--
#### Known issue with SQL Server 2019

There's a known issue<!--6436234 with the new [scalar UDF inlining](/sql/relational-databases/user-defined-functions/scalar-udf-inlining) feature in SQL 2019. To work around this issue and disable UDF lining, run the following script on the SQL 2019 server:

```sql
ALTER DATABASE SCOPED CONFIGURATION SET TSQL_SCALAR_UDF_INLINING = OFF  
```

While not always necessary, you may need to restart the SQL server after you run this script. For more information, see [Disabling Scalar UDF Inlining without changing the compatibility level](/sql/relational-databases/user-defined-functions/scalar-udf-inlining#disabling-scalar-udf-inlining-without-changing-the-compatibility-level).

You can safely disable this SQL feature for the site database server because Configuration Manager doesn't use it.

If you don't disable scalar UDF inlining in SQL 2019, the site server will randomly fail to query the site database. For example, you'll see the following errors in **hman.log**:

```hman.log
*** [HY000][0][Microsoft][SQL Server Native Client 11.0]Unspecified error occurred on SQL Server. Connection may have been terminated by the server.
*** select dbo.fnGetSiteMode(dbo.fnGetSiteCode())
*** [HY000][596][Microsoft][SQL Server Native Client 11.0][SQL Server]Cannot continue the execution because the session is in the kill state.
Failed to execute SQL command select dbo.fnGetSiteMode(dbo.fnGetSiteCode())
```

You may see similar errors in other logs, such as **SmsAdminUI.log**.

SQL Server version 2019 logs the following error:

`Microsoft SQL Server reported SQL message 596, severity 21: [HY000][596][Microsoft][SQL Server Native Client 11.0][SQL Server]Cannot continue the execution because the session is in the kill state.`

You'll also see crash dumps (`.mdump` files) from SQL in its log directory, which by default is `C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\Log`.
-->

### <a name="sql-server-2017-standard-enterprise"></a>SQL Server 2017：Standard、Enterprise

只要 SQL 生命周期支持累积更新版本，就可以将此版本与[累积更新版本 2](https://support.microsoft.com/help/4052574) 或更高版本一起使用。 此版本的 SQL 可用于以下站点：

- 管理中心站点  
- 主站点  
- 辅助站点  
  <!--SMS.498506-->

### <a name="sql-server-2016-standard-enterprise"></a>SQL Server 2016：Standard、Enterprise  
<!--514985-->
可以将此版本与 SQL 生命周期支持的最小 Service Pack 和累积更新一起使用。 此版本的 SQL 可用于以下站点：

- 管理中心站点  
- 主站点  
- 辅助站点  

### <a name="sql-server-2014-standard-enterprise"></a>SQL Server 2014：Standard、Enterprise

可以将此版本与 SQL 生命周期支持的最小 Service Pack 和累积更新一起使用。 此版本的 SQL 可用于以下站点：

- 管理中心站点  
- 主站点  
- 辅助站点

### <a name="sql-server-2012-standard-enterprise"></a>SQL Server 2012：Standard、Enterprise

可以将此版本与 SQL 生命周期支持的最小 Service Pack 和累积更新一起使用。 此版本的 SQL 可用于以下站点：

- 管理中心站点  
- 主站点  
- 辅助站点  

### <a name="sql-server-2017-express"></a>SQL Server 2017 Express

只要 SQL 生命周期支持累积更新版本，就可以将此版本与[累积更新版本 2](https://support.microsoft.com/help/4052574) 或更高版本一起使用。 此版本的 SQL 可用于以下站点：

- 辅助站点
<!--SMS.498506-->

### <a name="sql-server-2016-express"></a>SQL Server 2016 Express

可以将此版本与 SQL 生命周期支持的最小 Service Pack 和累积更新一起使用。 此版本的 SQL 可用于以下站点：

- 辅助站点

### <a name="sql-server-2014-express"></a>SQL Server 2014 Express

可以将此版本与 SQL 生命周期支持的最小 Service Pack 和累积更新一起使用。 此版本的 SQL 可用于以下站点：

- 辅助站点  

### <a name="sql-server-2012-express"></a>SQL Server 2012 Express

可以将此版本与 SQL 生命周期支持的最小 Service Pack 和累积更新一起使用。 此版本的 SQL 可用于以下站点：

- 辅助站点  

## <a name="required-configurations-for-sql-server"></a><a name="bkmk_SQLConfig"></a> SQL Server 所需的配置

用于站点数据库（包括 SQL Server Express）的 SQL Server 的所有安装都需要以下配置。 Configuration Manager 将 SQL Server Express 作为辅助站点安装的一部分进行安装时，将自动创建这些配置。  

### <a name="sql-server-architecture-version"></a>SQL Server 体系结构版本

Configuration Manager 需要 64 位版本的 SQL Server 以托管站点数据库。  

### <a name="database-collation"></a>数据库排序规则

在每个站点上，用于站点和站点数据库的 SQL Server 实例必须使用以下排序规则：**SQL_Latin1_General_CP1_CI_AS**。  

对于中国 GB18030 标准，Configuration Manager 支持此排序规则的两个例外情况。 有关详细信息，请参阅[国际支持](../hierarchy/international-support.md)。  

### <a name="database-compatibility-level"></a>数据库兼容性级别

Configuration Manager 要求站点数据库的兼容性级别不低于 Configuration Manager 版本支持的最低 SQL Server 版本。 例如，从版本 1702 开始，需要有高于或等于 110 的[数据库兼容性级别](/sql/relational-databases/databases/view-or-change-the-compatibility-level-of-a-database)。 <!-- SMS.506266-->

### <a name="sql-server-features"></a>SQL Server 功能

仅“数据库引擎服务”  功能是每个站点服务器所必需的。  

Configuration Manager 数据库复制不需要“SQL Server 复制”功能。 但是，当你使用[管理点的数据库副本](../../servers/deploy/configure/database-replicas-for-management-points.md)时，则需进行此 SQL Server 配置。  

### <a name="windows-authentication"></a>Windows 身份验证

Configuration Manager 需要“Windows 身份验证”来验证与数据库的连接。  

### <a name="sql-server-instance"></a>SQL Server 实例

为每个站点使用专用的 SQL Server 实例。 此实例可以为命名实例或默认实例。  

### <a name="sql-server-memory"></a>SQL Server 内存

使用 SQL Server Management Studio 保留用于 SQL Server 的内存。 在“服务器内存选项”下设置“最小服务器内存” 。 有关如何配置此设置的详细信息，请参阅 [SQL Server 内存服务器配置选项](/sql/database-engine/configure-windows/server-memory-server-configuration-options)。  

- **对于作为站点服务器安装在同一计算机上的数据库服务器**：将用于 SQL Server 的内存限制为，可用的可寻址系统内存的 50% 到 80%。  

- **对于专用的数据库服务器（远离站点服务器）** ：将用于 SQL Server 的内存限制为，可用的可寻址系统内存的 80% 到 90%。  

- 对于使用中的每个 SQL Server 实例的缓冲池内存预留：  

  - 对于中央管理站点：至少设置 8 GB。  
  - 对于主站点：至少设置 8 GB。  
  - 对于辅助站点：至少设置 4 GB。  

### <a name="sql-nested-triggers"></a>SQL 嵌套触发器

必须启用 SQL 嵌套触发器。 有关详细信息，请参阅[配置嵌套触发器服务器配置选项](/sql/database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option)

### <a name="sql-server-clr-integration"></a>SQL Server CLR 集成

站点数据库要求启用 SQL Server 公共语言运行时 (CLR)。 此选项在 Configuration Manager 安装时会自动启用。 有关 CLR 的详细信息，请参阅 [SQL Server CLR 集成简介](/dotnet/framework/data/adonet/sql/introduction-to-sql-server-clr-integration)  

### <a name="sql-server-service-broker-ssb"></a>SQL Server Service Broker (SSB)

站点间复制和单个主站点都需要 SQL Server Service Broker。

### <a name="trustworthy-setting"></a>可信设置

Configuration Manager 会自动启用 SQL [可信数据库属性](/sql/relational-databases/security/trustworthy-database-property)。 Configuration Manager 要求此属性为“打开”。

## <a name="optional-configurations-for-sql-server"></a><a name="bkmk_optional"></a> SQL Server 可选配置

以下配置对使用完整 SQL Server 安装的每个数据库是可选的。  

### <a name="sql-server-service"></a>SQL Server 服务

你可以将 SQL Server 服务配置为使用以下账户运行：  

- 低权限域用户帐户：  

  - 此配置是最佳做法，并且可能要求你手动注册该帐户的服务主体名称 (SPN)。  

- 运行 SQL Server 的计算机的**本地系统**帐户：  

  - 使用本地系统帐户简化配置过程。  
  - 使用本地系统帐户时，Configuration Manager 将自动注册 SQL Server 服务的 SPN。  
  - 为 SQL Server 服务使用本地系统帐户不是 SQL Server 最佳做法。  

运行 SQL Server 的计算机不使用其本地系统帐户运行 SQL Server 服务时，配置帐户的 SPN，该帐户在 Active Directory 域服务中运行 SQL Server 服务。 （使用系统帐户时，将为你自动注册 SPN。）

有关站点数据库 SPN 的信息，请参阅[管理站点数据库服务器的 SPN](../../servers/manage/modify-your-infrastructure.md#bkmk_SPN)。  

有关如何更改 SQL Server 服务使用的帐户的信息，请参阅 [SCM 服务 - 更改服务启动帐户](/sql/database-engine/configure-windows/scm-services-change-the-service-startup-account)。  

### <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

SQL Server Reporting Services 是安装可运行报表的 Reporting Services 点的必需条件。 配置管理器支持用于报表和站点数据库的 SQL Server 版本相同。

有关详细信息，请参阅[在配置管理器中报表的先决条件](../../servers/manage/prerequisites-for-reporting.md)。

> [!IMPORTANT]  
> 将以前版本的 SQL Server 升级后，可能会看到以下错误：*报表生成器不存在*。  
> 要修复此错误，必须重新安装 Reporting Services 点站点系统角色。  

### <a name="data-warehouse-service-point"></a>数据仓库服务点

数据仓库使用单独的数据库。 可以将它托管在站点数据库服务器或单独的 SQL Server 上。 有关详细信息，请参阅[配置管理器的数据仓库服务点](../../servers/manage/data-warehouse.md)。

### <a name="sql-server-ports"></a>SQL Server 端口

对于与 SQL Server 数据库引擎的通信和站点间复制，可以使用默认的 SQL Server 端口配置，也可以指定自定义端口：  

- **站点间通信**使用 SQL Server Service Broker，它默认使用端口 TCP 4022。  
- SQL Server 数据库引擎与各种 Configuration Manager 站点系统角色之间的站点内通信默认使用端口 TCP 1433。 下列站点系统角色直接与 SQL Server 数据库进行通信：  

  - 管理点  
  - SMS 提供程序计算机  
  - Reporting Services 点  
  - 站点服务器  

运行 SQL Server 的计算机托管多个站点中的数据库时，每个数据库必须使用独立的 SQL Server 实例。 此外，每个实例必须配置为使用一组唯一的端口。  

> [!WARNING]  
> Configuration Manager 不支持动态端口。 由于 SQL Server 命名实例默认情况下使用动态端口来连接到数据库引擎，因此，在使用命名实例时，必须手动配置要用于站点内通信的静态端口。  

如果在运行 SQL Server 的计算机上启用防火墙，请确保将防火墙配置为不阻止你的部署使用的端口，以及位于与 SQL Server 通信的计算机之间的网络上任何位置处的端口。  

有关如何将 SQL Server 配置为使用特定端口的示例，请参阅[将服务器配置为侦听特定的 TCP 端口](/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port)。  

## <a name="upgrade-options-for-sql-server"></a>SQL Server 的升级选项

如果需要升级 SQL Server 版本，请使用以下方法（难度从简单到复杂）：  

- [就地升级 SQL Server](../../servers/manage/upgrade-on-premises-infrastructure.md#to-upgrade-sql-server-on-the-site-database-server)（推荐）  

- 在新计算机上安装新版本的 SQL Server，然后使用 Configuration Manager 设置的[数据库移动选项](../../servers/manage/modify-your-infrastructure.md#bkmk_dbconfig)将站点服务器指向新的 SQL Server  

- 使用[备份和恢复](../../servers/manage/backup-and-recovery.md)。 支持在 SQL 升级方案中使用备份和恢复。 在查看[恢复站点前的注意事项](../../servers/manage/recover-sites.md#considerations-before-recovering-a-site)时，可以忽略 SQL 版本控制要求。