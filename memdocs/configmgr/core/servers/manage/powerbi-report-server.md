---
title: 与 Power BI 报表服务器集成
titleSuffix: Configuration Manager
description: 将 Power BI 报表服务器与 Configuration Manager 报告集成，以实现现代化的可视化效果和更好的性能。
ms.date: 04/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 315e2613-dc71-46b1-80cb-26161d08103a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f4089f52d912491b3b1396906fe391c5c334e061
ms.sourcegitcommit: 02635469d684d233fef795d2a15615658e62db10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/16/2020
ms.locfileid: "84814901"
---
# <a name="integrate-with-power-bi-report-server"></a>与 Power BI 报表服务器集成

适用范围：Configuration Manager (Current Branch)

<!--3721603-->

从版本 2002 开始，可以将 [Power BI 报表服务器](https://docs.microsoft.com/power-bi/report-server/get-started)与 Configuration Manager 报告集成。 这种集成提供了现代可视化效果和更好的性能。 它为 Power BI 报表添加了控制台支持，这与 SQL Server Reporting Services 中已存在的报表类似。

保存 Power BI Desktop 报表文件 (.PBIX) 并将它们部署到 Power BI 报表服务器。 此过程与 SQL Server Reporting Services 报表文件 (.RDL) 类似。 你还可以直接从 Configuration Manager 控制台启动浏览器中的报表。

## <a name="prerequisites"></a>必备条件

- Power BI 报表服务器许可证。 有关详细信息，请参阅 [Power BI 报表服务器许可](https://docs.microsoft.com/power-bi/report-server/get-started#licensing-power-bi-report-server)。

- 下载 [Microsoft Power BI 报表服务器 - 2019 年 9 月版](https://www.microsoft.com/download/details.aspx?id=57270)或更高版本。

    > [!NOTE]
    > 请勿立即安装 Power BI 报表服务器。 有关适用于你的环境的过程，请参阅[配置 Reporting Services 点](#configure-the-reporting-services-point)。

- 下载 [Microsoft Power BI Desktop（针对 Power BI 报表服务器进行了优化 - 2019 年 9 月版）](https://www.microsoft.com/download/details.aspx?id=57271)或更高版本。

    > [!IMPORTANT]
    > - 只使用 [Microsoft 下载中心](https://www.microsoft.com/download/)的 Power BI Desktop 版本，不要使用 Microsoft Store 中的版本。
    > - 只使用[声明已“针对 Power BI 报表服务器进行了优化”的 Power BI Desktop](https://docs.microsoft.com/power-bi/report-server/install-powerbi-desktop) 版本。

- Power BI 集成使用相同的基于角色的管理进行报告。
    > [!NOTE]
    > Power BI 报表服务器不支持启用 RBAC 的报表，因此，无论报表的分配范围如何，报表的所有查看器都将看到相同的结果。

## <a name="configure-the-reporting-services-point"></a>配置 Reporting Services 点

此过程因你在站点中是否已有此角色而异。

### <a name="you-have-a-reporting-services-point"></a>有 Reporting Services 点

仅当站点中已有 Reporting Services 点时，才使用此过程。 请在同一服务器上执行此过程的所有步骤：

1. 在报表服务器 Configuration Manager 中，备份“加密密钥” 。 有关详细信息，请参阅 [SSRS 加密密钥 - 备份和还原加密密钥](https://docs.microsoft.com/sql/reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys)。

    > [!WARNING]
    > 如果跳过此步骤，将无法访问 SQL Server Reporting Services 中的任何自定义报表。

1. 从站点中删除 Reporting Services 点角色。

1. 卸载 SQL Server Reporting Services，但保留数据库。

1. 安装 Power BI 报表服务器。

1. 配置 Power BI 报表服务器

    1. 使用以前的报表服务器数据库。

    1. 使用报表服务器 Configuration Manager，还原“加密密钥” 。

1. 在 Configuration Manager 中添加 Reporting Services 点角色。

### <a name="you-dont-have-a-reporting-services-point"></a>没有 Reporting Services 点

仅当站点中还没有 Reporting Services 点时，才使用此过程。 请在同一服务器上执行此过程的所有步骤：

1. 安装 Power BI 报表服务器。

2. 在 Configuration Manager 中添加 Reporting Services 点角色。 有关详细信息，请参阅[配置报表](configuring-reporting.md)。

## <a name="configure-the-configuration-manager-console"></a>配置 Configuration Manager 控制台

1. 在运行 Configuration Manager 控制台的计算机上，将 Configuration Manager 控制台更新为最新版本。

1. 安装 Power BI Desktop。 确保语言相同。

1. 安装完成后，请在打开 Configuration Manager 控制台之前至少启动一次 Power BI Desktop。

## <a name="create-power-bi-reports"></a>创建 Power BI 报表

1. 在 Configuration Manager 控制台中，转到“监视”工作区，展开“报告”，然后选择新的“Power BI 报表”节点  。

1. 在功能区上，选择“创建报表”。 此操作将打开 Power BI Desktop。

1. 在 Power BI Desktop 中创建报表。

    - 在 Power BI Desktop 中，当你连接到数据源时，为连接设置选择“DirectQuery”。

    - 在这些报表中仅使用受支持的 SQL 视图。 有关详细信息，请参阅[在 Configuration Manager 中使用 SQL Server 视图创建自定义报表](../../../develop/core/understand/sqlviews/create-custom-reports-using-sql-server-views.md)。

1. 当报表准备就绪可保存时，请前往“文件”菜单，选择“另存为”，然后选择“Power BI 报表服务器”  。

1. 在“Power BI 报表服务器选择”窗口中，输入 Reporting Services 点的 URL 作为“新报表服务器地址” 。 例如，`https://rsp.contoso.com/Reports`。

在 Configuration Manager 控制台中，可以在 Power BI 报表列表中看到新报表。

## <a name="next-steps"></a>后续步骤

创建报表后，在 Configuration Manager 控制台中执行以下操作：

- 在浏览器中运行：在 Web 浏览器中打开 Power BI 报表。 与其他人共享此 URL，例如：`https://rsp.contoso.com/Reports/POWERBI/ConfigMgr_ABC/Windows%2010/Windows10%20Dashboard?rs:embed=true`

    > [!TIP]
    > 只能在 Web 浏览器中查看这些报表。

- **编辑**：在 Power BI Desktop 中对报表进行更改。 对于现有报表，请使用“保存”选项将更改保存回报表服务器。

有关用于报告的日志文件的详细信息，请参阅[日志文件引用 - 报告](../../plan-design/hierarchy/log-files.md#BKMK_ReportLog)。
