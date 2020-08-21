---
title: Office 365 客户端管理仪表板
titleSuffix: Configuration Manager
description: 在“Office 365 客户端管理”仪表板中审阅 Microsoft 365 Apps 客户端信息
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 08/11/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 69f234a2-b04b-445a-b81f-6b4acfc00eaf
ms.openlocfilehash: ce3947c8ca3c562869fdfed2ddba4d9b160902be
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129353"
---
# <a name="office-365-client-management-dashboard"></a>Office 365 客户端管理仪表板

适用范围：  Configuration Manager (Current Branch)

> [!Note]
> 自 2020 年 4 月 21 日起，Office 365 专业增强版已重命名为 Microsoft 365 企业应用版  。 有关详细信息，请参阅 [Office 365 专业增强版的名称变更](https://docs.microsoft.com/deployoffice/name-change)。 在控制台更新期间，你可能仍会看到 Configuration Manager 控制台和支持文档中引用的是旧名称。

自 Configuration Manager 版本 1802 起，可以在“Office 365 客户端管理”仪表板中审阅 Microsoft 365 Apps 客户端信息。 选中图形部分时，Office 365 客户端管理仪表板会显示相关设备的列表。 <!--1357281 -->

## <a name="prerequisites"></a>必备条件

### <a name="enable-hardware-inventory"></a>启用硬件清单

Office 365 客户端管理仪表板中显示的数据来自硬件清单。 启用硬件清单，并选择“Office 365 ProPlus 配置”  硬件清单类，以便在仪表板中显示数据。
 
1. 启用硬件清单（如果尚未启用）。 有关详细信息，请参阅[配置硬件清单](../../core/clients/manage/inventory/configure-hardware-inventory.md)。
2. 在 Configuration Manager 控制台中，导航到“管理”   > “客户端设置”   > “默认客户端设置”  。  
3. 在“主页”  选项卡上的“属性”  组中，单击“属性”  。  
4. 在**默认客户端设置**对话框中，单击**硬件清单**。  
5. 在**设备设置**列表中，单击**设置类**。  
6. 在“硬件清单类”  对话框中，选择“Office 365 ProPlus 配置”  。  
7. 单击**确定**以保存所做的更改并关闭**硬件清单类**对话框。

Office 365 客户端管理仪表板在硬件清单得到报告的同时开始显示数据。

### <a name="connectivity-for-top-level-site-server"></a>顶层站点服务器的连接

（版本 1906 中作为先决条件引入） 

顶层站点服务器需要访问以下终结点才能下载就绪情况文件：

`https://contentstorage.osi.office.net/sccmreadinessppe/sot_sccm_addinreadiness.cab`

> [!NOTE]
> 在这些情况下，客户端设备不需要 Internet 连接。

### <a name="enable-data-collection-for-microsoft-365-apps"></a>为 Microsoft 365 Apps 启用数据收集

（版本 1910 中作为先决条件引入） 

自版本 1910 起，需要为 Microsoft 365 Apps 启用数据收集，以便在“Office 365 专业增强版(试点)和运行状况”仪表板中填充信息。 数据存储在 Configuration Manager 站点数据库中，不会发送给 Microsoft。

此数据不同于[从 Microsoft 365 Apps 发送到 Microsoft 的诊断数据](https://docs.microsoft.com/deployoffice/privacy/overview-privacy-controls#diagnostic-data-sent-from-office-365-proplus-to-microsoft)中介绍的诊断数据。

可以使用组策略或编辑注册表来启用数据收集功能。

#### <a name="enable-data-collection-from-group-policy"></a>通过组策略启用数据收集功能

1. 下载最新的[来自 Microsoft 下载中心的管理模板文件](https://www.microsoft.com/download/details.aspx?id=49030)。
2. 启用 `User Configuration\Policies\Administrative Templates\Microsoft Office 2016\Telemetry Dashboard` 下方的“启用遥测数据收集功能”策略设置  。
    - 或者，通过 [Office 云策略服务](https://docs.microsoft.com/DeployOffice/overview-office-cloud-policy-service)应用策略设置。
    - Office 遥测仪表板也使用该策略设置，但无需为该数据收集功能部署该仪表板。

#### <a name="enable-data-collection-from-the-registry"></a>通过注册表启用数据收集功能

以下命令演示如何通过注册表启用数据收集功能：

```cmd
reg add HKCU\Software\Policies\Microsoft\office\16.0\OSM /v EnableLogging /t REG_DWORD /d 1
```

## <a name="viewing-the-office-365-client-management-dashboard"></a>查看 Office 365 客户端管理仪表板

若要在 Configuration Manager 控制台中查看 Office 365 客户端管理仪表板，请依次转到“软件库”   > “概述”   > “Office 365 客户端管理”  。 在仪表板顶部，使用“集合”  下拉列表设置按特定集合的成员筛选仪表板数据。 自 Configuration Manager 版本 1802 起，当你选择图形部分时，仪表板会显示相关设备的列表。

Office 365 客户端管理仪表板提供以下信息的相关图表：

- Microsoft 365 Apps 客户端数量
- Microsoft 365 Apps 客户端版本
- Microsoft 365 Apps 客户端语言
- Microsoft 365 Apps 客户端通道：有关详细信息，请参阅 [Microsoft 365 Apps 更新通道概述](/DeployOffice/overview-of-update-channels-for-office-365-proplus)。


## <a name="integration-for-microsoft-365-apps-readiness"></a><a name="bkmk_o365_readiness"></a> 集成“Microsoft 365 Apps 就绪情况”
<!--3735402-->
自 Configuration Manager 版本 1902 起，可以使用仪表板来识别具有高置信度且可以升级到 Microsoft 365 Apps 的设备。 通过此集成，可深入了解环境中加载项和宏可能存在的兼容性问题。 然后，使用 Configuration Manager 将 Microsoft 365 Apps 部署到就绪的设备。

Office 365 客户端管理仪表板包含新磁贴“Office 365 专业增强版升级就绪情况”  。 此磁贴是处于以下状态的设备的条形图：
- 未评估
- 升级准备就绪
- 需要评审

选择一个状态，钻取到设备列表。 此准备情况报表显示更多设备相关详细信息。 它包括关于加载项和宏的兼容性状态的列。

### <a name="prerequisites-for-microsoft-365-apps-readiness-integration"></a>集成“Microsoft 365 Apps 就绪情况”的先决条件

- 在客户端设置中启用硬件清单。 有关详细信息，请参阅[先决条件](#prerequisites)部分。  

- 设备需要连接到 Office 内容分发网络 (CDN) 才能下载加载项就绪情况文件。 有关详细信息，请参阅[内容分发网络](https://docs.microsoft.com/office365/enterprise/content-delivery-networks)。 如果设备无法下载此文件，说明加载项状态为“需要审核”  。  

    > [!Note]  
    > 此功能没有数据发送给 Microsoft。  

### <a name="detailed-macro-readiness"></a><a name="bkmk_ort"></a>详细的宏就绪情况

默认情况下，扫描代理会查看每个设备上最近使用的 (MRU) 文件列表。 它对此列表中支持宏的文件计数。 这些文件包括下列类型：
- 启用宏的 Office 文件格式，例如启用了宏的 Excel 工作簿 (.xlsm) 或启用了宏的 Word 文档 (.docm)  
- 不指示是否有宏内容的旧版 Office 格式。 例如，Excel 97-2003 工作簿 (.xls)。

如需详细了解有关宏兼容性的信息，请部署 Readiness Toolkit for Office，以便分析宏文件中的代码  。 它会检查是否存在任何潜在的兼容性问题。 例如，文件是否使用了较新版 Office 中已更改的功能。 运行 Readiness Toolkit for Office 并选择“本计算机上最近使用过的 Office 文档和已安装的加载项”选项后，或在命令行中使用 `-mru` 标志后，Configuration Manager 的硬件清单代理即可获取结果  。 这些额外的数据可提高设备就绪情况计算的准确度。 有关详细信息，请参阅[使用 Readiness Toolkit for Office 评估 Microsoft 365 Apps 的应用程序兼容性](https://aka.ms/readinesstoolkit)。

请注意，无需在每个目标设备上安装 Readiness Toolkit 来进行扫描。 可以使用以下示例命令行选项扫描每个预期设备。  输出标志是必需的，但文件将不会用于在仪表板中生成结果，因此可以选择任何有效位置。

```cmd
ReadinessReportCreator.exe -mru -output c:\temp -silent
```

有关详细信息，请参阅[获取企业中多个用户的就绪情况信息](/deployoffice/use-the-readiness-toolkit-to-assess-application-compatibility-for-office-365-pro#getting-readiness-information-for-multiple-users-in-an-enterprise)。

## <a name="microsoft-365-apps-readiness-dashboard"></a><a name="bkmk_readiness-dash"></a>“Microsoft 365 Apps 就绪情况”仪表板

（从版本 1906 中引入） 

<!--4021125-->
为了帮助你确定哪些设备可以升级到 Microsoft 365 Apps，自版本 1906 起我们推出了就绪情况仪表板。 它包括 Configuration Manager 当前分支版本 1902 中发布的“Office 365 专业增强版升级就绪情况”  磁贴。 此仪表板上的以下新磁贴有助于评估加载项和宏就绪情况：

- 部署
- 设备就绪情况
- 加载项就绪情况
- 加载项支持语句
- 版本数排名靠前的加载项
- 包含宏的设备数
- 宏就绪情况
- 宏公告

以下视频录制的是 Ignite 2019 大会的一场研讨会，其中详细介绍了以下内容：

> [!VIDEO https://medius.studios.ms/Embed/Video-nc/IG19-BRK3090]

[在 Configuration Manager 中使用 Office 就绪情况进行兼容性评估和 Microsoft Office 365 专业增强版升级的最佳实践](https://myignite.techcommunity.microsoft.com/sessions/79338?source=sessions)

### <a name="using-the-microsoft-365-apps-upgrade-readiness-dashboard"></a>使用“Microsoft 365 Apps 升级就绪情况”仪表板

在确保满足[先决条件](#prerequisites)之后，请按以下说明使用仪表板：
 
1. 在 Configuration Manager 控制台中，转到“软件库”工作区，展开“Office 365 客户端管理”   。
1. 选择“Microsoft 365 Apps 升级就绪情况”节点。
1. 更改“集合”和“目标 Office 体系结构”，以更改仪表板中的信息   。

[![“Microsoft 365 Apps 升级就绪情况”仪表板](./media/4021125-office-365-upgrade-readiness-dashboard.png)](./media/4021125-office-365-upgrade-readiness-dashboard.png#lightbox)

[![“Microsoft 365 Apps 升级就绪情况”仪表板上的加载项](./media/4021125-office-365-to-add-ins.png)](./media/4021125-office-365-to-add-ins.png#lightbox)

[![“Microsoft 365 Apps 升级就绪情况”仪表板上的宏公告](./media/4021125-office-365-macro-advisories.png)](./media/4021125-office-365-macro-advisories.png#lightbox)

### <a name="device-readiness-information"></a>设备就绪情况信息

评估每个设备上的加载项和宏清单后，设备会根据信息进行分组。 状态为“升级准备就绪”的设备不太可能出现任何兼容性问题  。

选择图表上的“升级准备就绪”类别会显示有关限定集合中设备的更多详细信息  。 可以查看设备列表，按需求进行选择，然后根据选择新建设备集合。 使用新集合来通过 Configuration Manager 部署 Microsoft 365 Apps。

可能存在兼容性风险的设备会被标记为“需要审核”  。 在将这些设备升级到 Microsoft 365 Apps 之前，可能需要先对它们采取行动。 例如，可以将关键加载项更新为较新版本。

### <a name="add-in-information"></a>加载项信息

 每个设备都会收集所有已安装加载项的清单。 然后，将此清单与 Microsoft 在 Microsoft 365 Apps 上拥有的关于加载项性能的信息进行比较。 如果发现某加载项在升级后会引发问题，则所有具有该加载项的设备都将被标记，以供审核。

### <a name="macro-information"></a>宏信息

Configuration Manager 可查看每个设备上最近使用过的文件。 它对此列表中支持宏的文件进行计数，其中包括以下类型：

- 启用宏的 Office 文件格式。
- 不指示是否有宏内容的旧版 Office 格式。

此报表可用于确定哪些设备最近使用过可能包含宏的文件。 然后可以使用 Configuration Manager 部署 Readiness Toolkit for Office，以扫描需要更多详细信息的任何设备，并检查是否存在潜在的兼容性问题  。 例如，文件是否使用了最近版本 Microsoft 365 Apps 中更改的功能。

有关如何执行扫描的详细信息，请参阅[详细的宏就绪情况](#bkmk_ort)。

## <a name="office-365-proplus-pilot-and-health-dashboard"></a><a name="bkmk_pilot"></a>Office 365 专业增强版试点和运行状况仪表板
<!--4488272, 4488301-->
（从版本 1910 中引入） 

自版本 1910 起，“Office 365 专业增强版(试点)和运行状况”仪表板有助于你计划、引导和执行 Microsoft 365 Apps 部署。 此仪表板为装有 Microsoft 365 Apps 的设备提供了运行状况见解，以帮助你发现可能会影响部署计划的问题。 Office 365 专业增强版试点和运行状况仪表板根据加载项清单提供了试点设备建议  。 该仪表板具有以下磁贴：

- 生成试点
- 建议的试点设备
- 部署试点
- 发送运行状况数据的设备
- 设备不满足运行状况目标
- 加载项不满足运行状况目标
- 宏不满足运行状况目标

### <a name="using-the-office-365-proplus-pilot-and-health-dashboard"></a>使用 Office 365 专业增强版试点和运行状况仪表板

在确保满足[先决条件](#prerequisites)之后，请按以下说明使用仪表板：

1. 在 Configuration Manager 控制台中，转到“软件库”工作区，展开“Office 365 客户端管理”   。
1. 选择“Office 365 试点和运行状况”节点  。

![Office 365 专业增强版试点和运行状况仪表板](./media/4488272-office-365-pro-plus-pilot.png)


### <a name="generate-pilot"></a>生成试点

单击按钮，通过限定集合生成试点建议。 启动该操作后，后台任务便会开始计算试点集合。 限定集合必须包含至少一个具有非专业增强版的 Office 版本的设备。

### <a name="recommended-pilot-devices"></a>建议的试点设备

建议的试点设备是最小的一组设备，表示生成试点时所使用的限定集合中所有已安装的加载项  。 向下钻取以获取这些设备的列表。 然后根据需要使用详细信息从试点中排除任何设备。 如果你的所有加载项都已经安装在 Microsoft 365 Apps 设备上，那么装有这些加载项的设备将不会包括在计算中。 这也意味着，你可能不会在试点集合中得到任何结果，因为安装了 Microsoft 365 Apps 的设备上已有你的所有加载项。

### <a name="deploy-pilot"></a>部署试点

接受试点设备后，使用分阶段部署向导将 Microsoft 365 Apps 部署到试点集合。 管理员可以在向导中定义试点和限定集合以管理部署。

### <a name="health-data"></a>运行状况数据

安装 Microsoft 365 Apps 后，在试点设备上启用运行状况数据。 通过运行状况数据，可以深入了解不满足运行状况目标的加载项和宏。 “准备好部署的设备”图表通过使用运行状况见解标识准备好部署的非试点设备  。 从“发送运行状况数据的设备”图表获取发送运行状况数据的设备的计数  。

### <a name="devices-not-meeting-health-goals"></a>设备不满足运行状况目标

此磁贴汇总了出现加载项和/或宏问题的设备。

### <a name="add-ins-not-meeting-health-goals"></a>加载项不满足运行状况目标

- 加载失败：加载项未能启动。
- 故障：加载项在运行时失败。
- 错误：加载项报告了一个错误。
- 多个问题：加载项有以上问题之一。

### <a name="macros-not-meeting-health-goals"></a>宏不满足运行状况目标

- 加载失败：未能加载文档。
- 运行时错误：宏运行时发生错误。 这些错误可能依赖于输入，因此可能不会始终出现。
- 编译错误：宏未正确编译，因此不会尝试运行。
- 多个问题：宏有以上问题之一。

> [!NOTE]
> 宏清单中填充了适用于 Office 和最近使用的数据文件的 Readiness Toolkit 中的数据。 宏运行状况填充了运行状况数据。 由于数据源不同，宏运行状况状态可能是“需要审阅”，而宏清单的状态为“未扫描”   。 <!--5922845-->

### <a name="known-issues"></a>已知问题

“部署试点”磁贴存在已知问题  。 目前不能用于部署到试点。 解决方法是使用分阶段部署向导部署应用程序的现有工作流。 <!--5525871-->

## <a name="next-steps"></a>后续步骤

[使用 Configuration Manager 管理 Microsoft 365 Apps 更新](manage-office-365-proplus-updates.md)
