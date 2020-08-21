---
title: 报表简介
titleSuffix: Configuration Manager
description: 了解在 Configuration Manager 中管理报表可使用的工具和资源集。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 230be984-d2cd-4d53-bd7a-bc24dd93fc22
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: d28638cdf332adbb1d57526179222bb96d6d5c92
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128063"
---
# <a name="introduction-to-reporting-in-configuration-manager"></a>Configuration Manager 中的报表简介

适用范围：  Configuration Manager (Current Branch)

Configuration Manager 中的报表功能提供一组工具和资源，可帮助你使用 SQL Server Reporting Services (SSRS) 和 Power BI 报表服务器的高级报表功能。 这两个报表平台都提供了丰富的自定义报表创作体验。 报表可帮助你收集、组织和显示有关组织中大量 Configuration Manager 数据的信息。 Configuration Manager 在 Reporting Services 中提供了许多可以在不进行更改的情况下使用的预定义报表。 可以复制和修改默认报表来满足要求，也可以创建自定义报表。

## <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

SQL Server Reporting Services 提供了各种现成可用的工具和服务，帮助你创建、部署和管理组织的报表。 它还具有可用于扩展和自定义报表功能的编程功能。 Reporting Services 是基于服务器的报表平台，它为各种类型的数据源提供综合性报表功能。

Configuration Manager 将 SQL Server Reporting Services 用作其主要报表解决方案。 与 Reporting Services 的集成提供了以下优点：  

- 使用行业标准报告系统查询 Configuration Manager 数据库。  

- 使用 Configuration Manager 报表查看器或报表管理器显示报表，这是基于 Web 连接到报表的连接。  

- 提供高性能、可用性和可伸缩性。  

- 提供用户可以订阅的报表订阅。 例如，经理可每天订阅通过电子邮件发送的报表，其中详细说明软件更新推出的状态。

- 以不同种类的常用格式导出报表。  

有关详细信息，请参阅[什么是 SQL Server Reporting Services (SSRS)？](https://docs.microsoft.com/sql/reporting-services/create-deploy-and-manage-mobile-and-paginated-reports?view=sql-server-ver15)

## <a name="power-bi-report-server"></a>Power BI 报表服务器

<!-- 3721603 -->

从版本 2002 开始，将 Power BI 报表服务器与 Configuration Manager 报告集成。 这种集成提供了现代可视化效果和更好的性能。 它为 Power BI 报表添加了控制台支持，这与 SQL Server Reporting Services 中已存在的报表类似。 有关详细信息，请参阅[与 Power BI 报表服务器集成](powerbi-report-server.md)。

Power BI 报表服务器是本地报表服务器，包含用于显示和管理报表的 Web 门户。 它包含可创建 Power BI 报表、分页报表、移动报表和 KPI 的工具。 有关详细信息，请参阅[什么是 Power BI 报表服务器？](https://docs.microsoft.com/power-bi/report-server/get-started)。

## <a name="reporting-services-point"></a>Reporting Services 点

Reporting Services 点是在运行 Microsoft SQL Server Reporting Services 的服务器上添加的站点系统角色。 Reporting Services 点执行以下功能：

- 将 Configuration Manager 报表定义复制到 Reporting Services
- 基于报表类别创建报表文件夹
- 为报表文件夹和报表设置安全策略。 这些策略基于 Configuration Manager 管理用户的基于角色的权限。 Reporting Services 点按 10 分钟的间隔连接到 Reporting Services 以重新应用更改的安全策略。

有关如何规划和安装 Reporting Services 点的详细信息，请参阅以下文章：

- [报表规划](planning-for-reporting.md)

- [配置报表](configuring-reporting.md)

## <a name="configuration-manager-reports"></a>Configuration Manager 报表

Configuration Manager 为 50 多个报表文件夹中的 400 多个报表提供报表定义。 在 Reporting Services 点安装过程中，它会将它们复制到 SQL Server Reporting Services 中的根报表文件夹。 Configuration Manager 控制台会显示报表，并根据报表类别在子文件夹中组织它们。

报表不会在 Configuration Manager 层次结构中向上或向下传播。 它们仅对在其中创建它们的站点的数据库运行。 因为 Configuration Manager 在整个层次结构中复制全局数据，所以用户可以在报表中访问层次结构范围的信息。 当报表从站点数据库中检索数据时，它可以访问当前站点和子站点的站点数据，以及层次结构中每个站点的全局数据。

与其他 Configuration Manager 对象一样，管理用户必须具有合适的权限来运行或修改报表。 为了运行报表，管理用户必须具有对对象的“运行报表”  权限。 为了创建或修改报表，管理用户必须具有对对象的“修改报表”  权限。

### <a name="create-and-modify-reports"></a>创建和修改报表

对于基于 Reporting Services 的报表，Configuration Manager 使用 Microsoft SQL Server 报表生成器作为创作和编辑基于模型和 SQL 的报表的专用工具。 在 Configuration Manager 控制台中创建或编辑报表时，会打开报表生成器。 有关详细信息，请参阅[报表的操作和维护](operations-and-maintenance-for-reporting.md)。

从版本 2002 开始，为了创建或编辑 Power BI 报表，控制台与 Power BI Desktop 集成。 有关详细信息，请参阅[创建 Power BI 报表](powerbi-report-server.md#create-power-bi-reports)。

### <a name="run-reports"></a>运行报表

在 Configuration Manager 控制台中运行基于 Reporting Services 的报表时，报表查看器将会打开并连接到 Reporting Services。 指定任何所需报表参数后，那么 Reporting Services 会检索数据并在查看器中显示结果。 你也可以连接到 SQL Services Reporting Services，连接到站点的数据源，以及运行报表。

从版本 2002 开始，当你运行基于 Power BI 的报表时，它会在 Web 浏览器中打开。

### <a name="report-prompts"></a>报表提示

可以在创建或修改报表时配置报表提示或参数。 可创建报表提示以限制报表检索的数据或确定报表检索的目标数据。 一个报表可以包含多个提示。 确保提示名称唯一且只包含符合标识符的 SQL Server 规则的字母数字字符。

运行报表时，提示会请求输入所需参数的值。 它会基于参数值检索报表数据。 例如，特定计算机的计算机信息  报表会提示输入计算机名称。 Reporting Services 将指定的值传递给在报表的 SQL 语句中定义的变量。

### <a name="report-links"></a>报表链接

Configuration Manager 中的报表链接用于在源报表中轻松访问其他数据。 例如，它可以链接到有关源报表中每个项目的更多详细信息。 如果目标报表需要运行一个或多个提示，则源报表必须包含一个具有每个提示的合适值的列。

链接需要指定列号以及提示的值。 例如：

- 有一个报表列出站点最近发现的计算机。
- 从该报表链接到另一个报表，后者列出站点针对特定计算机收到的最后一个消息。
- 可创建链接，并指定源报表中的列 `2` 包含计算机名称。 对于目标报表，此值是必需的提示。
- 运行源报表，链接图标会出现在每个数据行的左侧。
- 选择某行上的图标，报表查看器会针对该行传递指定列中的值，将该值作为目标报表的提示值。

只能为报表配置一个链接，并且该链接只能连接到单个目标报表。

> [!WARNING]  
> 如果将目标报表移到其他报表文件夹，则目标报表的位置会发生更改。 Configuration Manager 不会使用新位置自动更新源报表中的报表链接，链接在源报表中将不工作。

## <a name="report-folders"></a>报表文件夹

报表文件夹提供了一种对 Configuration Manager 在 Reporting Services 中存储的报表进行排序和筛选的方法。 当有许多报表要管理时，报表文件夹十分有用。 安装 Reporting Services 点时，它会将报表复制到 Reporting Services 并组织成 50 多个报表文件夹。 报表文件夹是只读的。 无法在 Configuration Manager 控制台中修改它们。

## <a name="report-subscriptions"></a>报表订阅

Reporting Services 中的报表订阅是一个定期请求，此请求用于请求在特定时间提供报表或者响应某个事件。 需在订阅中指定应用程序文件格式。 订阅提供按需运行报表的一种替代方法。 按需报表要求你在每次想要查看报表时有效地选择报表。 相比之下，订阅可用于进行计划，然后自动提供报表。

可以在 Configuration Manager 控制台中管理报表订阅。 报表服务器会处理订阅。 它使用部署在服务器上的传递扩展插件分发订阅。 默认情况下，你可以创建订阅以将报表发送到共享文件夹或发送到电子邮件地址。

有关详细信息，请参阅[管理报表订阅](operations-and-maintenance-for-reporting.md#bkmk_subscription)。

## <a name="report-builder"></a>报表生成器

对于基于 Reporting Services 的报表，Configuration Manager 使用 Microsoft SQL Server 报表生成器作为创作和编辑基于模型和 SQL 的报表的专用工具。 如果在 Configuration Manager 控制台中创建或编辑报表，则会打开报表生成器。 首次创建或修改报表时，会自动安装报表生成器。 当运行或编辑报表时，会打开与安装的 SQL Server 版本关联的报表生成器版本。  

 报表生成器安装会为 20 多种语言添加支持。 运行报表生成器时，它会以本地计算机的操作系统的语言来显示数据。 如果报表生成器不支持该语言，则会用英语显示数据。 报表生成器支持 SQL Server Reporting Services 的所有功能，包括以下功能：

- 提供了直观的报表创作环境，其外观类似于 Microsoft 365 Apps。  

- 提供了 SQL Server 报表定义语言 (RDL) 的灵活报表布局。  

- 提供了各种形式的数据可视化，包括图表和仪表。  

- 提供了格式丰富的文本框。  

- 导出到 Microsoft Word 格式。  

你还可以直接从 SQL Server Reporting Services 打开报表生成器。

## <a name="report-models-in-sql-server-reporting-services"></a>SQL Server Reporting Services 中的报表模型

SQL Reporting Services 使用报表模型帮助从 Configuration Manager 数据库中选择要包含在基于模型的报表中的项目。 生成报表时，报表模型仅公开指定视图和项目以供选择。 要创建基于模型的报表，至少必须有一个报表模型可用。

报表模型具有以下功能：

- 为数据库字段和视图提供逻辑业务名称。 若要生成报表，无需要了解 Configuration Manager 数据库结构。

- 对项目进行逻辑分组。  

- 定义项目之间的关系。  

- 保护模型元素，以便管理用户只能看到他们有权查看的数据。

虽然 Configuration Manager 提供了样本报表模型，但也可以定义报表模型来满足自己的业务要求。 有关如何创建报表模型的详细信息，请参阅[创建自定义报表模型](creating-custom-report-models-in-sql-server-reporting-services.md)。

## <a name="next-steps"></a>后续步骤

[报表规划](planning-for-reporting.md)
