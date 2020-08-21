---
title: 安装 Power BI 示例报表
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中安装 Power BI 示例报表
ms.date: 08/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7e9bc22c-67ac-4a86-b613-944a4928e583
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 450c76617cf12a3201aa990c90843cb2e0f0edee
ms.sourcegitcommit: d1bfd5b8481439babc7eae43493f28edaebe647a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2020
ms.locfileid: "88179427"
---
# <a name="install-power-bi-sample-reports"></a>安装 Power BI 示例报表
<!--5679791-->
适用范围：Configuration Manager (Current Branch)

从版本 2002 开始，可以将 [Power BI 报表服务器](https://docs.microsoft.com/power-bi/report-server/get-started)与 Configuration Manager 报告集成。 有一些示例报表可供下载，你可以安装在 Configuration Manager 中。 本文介绍如何在 Configuration Manager 中安装 Power BI 示例报表。

## <a name="prerequisites"></a>必备条件

- Configuration Manager Reporting Services 点与 [Power BI 报表服务器集成](powerbi-report-server.md)

- [Microsoft Power BI Desktop（针对 Power BI 报表服务器进行了优化 - 2019 年 9 月版）](https://www.microsoft.com/download/details.aspx?id=57271)或更高版本

- 建议使用[版本 2002 的更新汇总 (4560496)](https://support.microsoft.com/help/4560496)，但这不是必需的。

    > [!IMPORTANT]
    > 只使用从 [Microsoft 下载中心](https://www.microsoft.com/download/)获取的 Power BI Desktop 版本。 不要使用从 Microsoft Store 获取的版本。
    >
    > 只使用[更适合 Power BI 报表服务器](https://docs.microsoft.com/power-bi/report-server/install-powerbi-desktop)的 Power BI Desktop 版本。

## <a name="download-the-sample-reports"></a>下载示例报表

若要下载示例报表：

1. 从 [Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=101452)下载 Power BI 示例报表。

1. 保存 `ConfigMgrSamplePowerBIReports.exe` 文件。

1. 如果从其他设备下载文件，请将该文件移动到已安装 Microsoft Power BI Desktop（针对 Power BI 报表服务器进行了优化）的计算机。

1. 运行 `ConfigMgrSamplePowerBIReports.exe` 文件以提取 .pbit 文件。

## <a name="install-the-sample-reports"></a>安装示例报表

若要安装示例报表：

1. 在 Power BI 报表服务器上，在根 Configuration Manager 报表文件夹中创建一个名为 `Sample Reports` 的新文件夹。

    :::image type="content" source="media/create-sample-reports-folder.png" alt-text="在根 Configuration Manager 报表文件夹中从 " lightbox="media/create-sample-reports-folder.png"::: 创建示例报表文件夹

1. 启动 Microsoft Power BI Desktop（针对 Power BI 报表服务器进行了优化）。

1. 依次选择“文件”、“打开”，并导航到保存提取的 .pbit 文件的位置。

1. 选择从 `ConfigMgrSamplePowerBIReports.exe` 文件中提取的一个 .pbit 文件。

1. 出现提示时，指定 Configuration Manager 数据库名称和数据库服务器名称，然后选择“加载”。

    在加载或应用数据模型时，如果出现任何错误，请忽略。

    :::image type="content" source="media/sample-report-database.png" alt-text="指定数据库和数据库服务器名称" lightbox="media/sample-report-database.png":::

1. 加载报表数据时，选择“文件” > “另存为”，然后选择“Power BI 报表服务器”。

    :::image type="content" source="media/save-powerbi-report-server.png" alt-text="另存为 Power BI 报表服务器" lightbox="media/save-powerbi-report-server.png":::

1. 将报表保存到在报表点上创建的 `Sample Reports` 文件夹。

    :::image type="content" source="media/save-sample-report.png" alt-text="保存到示例报表文件夹" lightbox="media/save-sample-report.png":::

1. 对于任何其他示例报表，请重复上述步骤。 完成时，请关闭 Microsoft Power BI Desktop（针对 Power BI 报表服务器进行了优化）。

1. 在 Configuration Manager 控制台中，转到“监视” > “Power BI 报表” > “示例报表”。

1. 右键单击其中一个报表，然后选择“在浏览器中运行”来启动该报表。

    :::image type="content" source="media/view-powerbi-report.png" alt-text="从 Configuration Manager 控制台运行示例报表" lightbox="media/view-powerbi-report.png":::
