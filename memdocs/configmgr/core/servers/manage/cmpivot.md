---
title: 使用 CMPivot 获得实时数据
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中使用 CMPivot 实时查询客户端。
ms.date: 04/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 32e2d6b9-148f-45e2-8083-98c656473f82
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: dcd441c7f35748f42adc8824c68ec703291a13e0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702085"
---
# <a name="cmpivot-for-real-time-data-in-configuration-manager"></a>在 Configuration Manager 中使用 CMPivot 获得实时数据

<!--1358456-->

适用范围：  Configuration Manager (Current Branch)

Configuration Manager 总是提供设备数据的大型集中式存储，客户可将其用于报告目的。 该站点通常每周都会收集这些数据。 从 1806 版开始，CMPivot 这种新的控制台中实用工具现提供对环境中设备实时状态的访问。 它立即对目标集合中的所有连接设备运行查询，并返回结果。 可以在工具中对此数据进行筛选和分组。 通过提供来自联机客户端的实时数据，可以更快地回答业务问题、解决问题并对安全事件作出响应。

例如，在[缓解推测执行端通道漏洞](https://techcommunity.microsoft.com/t5/configuration-manager-blog/additional-guidance-to-mitigate-speculative-execution-side/ba-p/274974)中，其中一个要求是更新系统 BIOS。 可以使用 CMPivot 来快速查询系统 BIOS 信息，并查找不符合要求的客户端。

 > [!IMPORTANT]  
 > - 某些安全软件可能会阻止 c:\windows\ccm\scriptstore 中运行的脚本。 这会阻止 CMPivot 查询的成功执行。 运行 CMPivot PowerShell 时，某些安全软件可能还会生成审核事件或警报。
 > - 某些反恶意软件可能会无意中触发针对 Configuration Manager 运行脚本或 CMPivot 功能的事件。 建议排除 %windir%\CCM\ScriptStore，以便反恶意软件允许这些功能在不受干扰的情况下运行。


## <a name="prerequisites"></a>必备条件

若要使用 CMPivot，需要以下组件：

- 将目标设备升级到 Configuration Manager 客户端的最新版本。  

- 目标客户端至少需要 PowerShell 版本 4。

- 若要收集有关以下实体的数据，目标客户端需要 PowerShell 5.0 版：  
  - Administrators
  - 连接
  - IPConfig
  - SMBConfig


- CMPivot 的权限：
  - “SMS 脚本”对象上的“读取权限”  
  - “集合”上的“运行脚本”权限  
    - 或者，从版本 1906 开始，可以在“集合”  上使用“运行 CMPivot”  。
  - “清单报表”上的“读取”权限  
  - 默认范围。

>[!NOTE]
> “运行脚本”  是“运行 CMPivot”  权限的超集。
 
## <a name="limitations"></a>限制

- 在层次结构中，将 Configuration Manager 控制台连接到主站点以运行 CMPivot  。 当“启动 CMPivot”操作连接到管理中心站点 (CAS) 时，它不会出现在控制台中  。
  - 从 Configuration Manager 版本 1902 开始，就可以从 CAS 运行 CMPivot。 在某些环境中，需要其他权限。 有关详细信息，请参阅[从版本 1902 开始的 CMPivot](#bkmk_cmpivot1902)。

- CMPivot 仅返回用于将客户端连接到当前站点的数据。  

- 如果集合包含来自其他站点的设备，则 CMPivot 结果仅来自当前站点中的设备。  

- 用户无法自定义实体属性、结果列或设备上的操作。  

- 只有一个 CMPivot 实例可以在运行 Configuration Manager 控制台的计算机上同时运行。  

- 在版本 1806 中，只有在组名为“管理员”时，对“管理员”  实体的查询才起作用。 如果组名已本地化，则不起作用。 例如，法语“Administrateurs”。<!--SCCMDocs issue 759-->  


## <a name="start-cmpivot"></a>启动 CMPivot

1. 在 Configuration Manager 控制台中，连接到主站点。 转到“资产和符合性”  工作区，并选择“设备集合”  节点。 选择目标集合，然后单击功能区中的“启动 CMPivot”  ，以便启动该工具。  

    > [!Tip]  
    > 如果看不到此选项，请检查以下配置：  
    > 
    > - 与站点管理员确认你的帐户具有所需权限。 有关详细信息，请参阅[先决条件](#prerequisites)。  
    > 
    > - 将控制台连接到主站点  。  

2. 界面进一步提供有关使用该工具的信息。  

     - 可在顶部手动输入查询字符串，或单击联机文档中的链接。  

     - 单击其中一个实体  将其添加到查询字符串。  

     - 有关表运算符  、聚合函数  和标量函数  的链接，请在 Web 浏览器中打开语言参考文档。 CMPivot 使用 [Kusto 查询语言 (KQL)](https://docs.microsoft.com/azure/kusto/query/)。  

3. 打开 CMPivot 窗口，查看来自客户端的结果。 关闭 CMPivot 窗口时，会话已完成。  

    > [!Note]  
    > 如果已发送查询，客户端仍会向服务器发送状况消息响应。  



## <a name="how-to-use-cmpivot"></a>如何使用 CMPivot

![CMPivot 窗口示例](media/1358456-cmpivot-sample.png)

CMPivot 窗口包含以下元素：  

1. CMPivot 当前定位的集合位于顶部的标题栏和窗口底部的状态栏中。 例如，上面屏幕截图中的“PM_Team_Machines”。  

2. 左侧窗格列出了客户端上可用的实体  。 一些实体依赖于 WMI，而其他实体则使用 PowerShell 从客户端获取数据。   

    - 右键单击实体，执行以下操作：  

       - **插入**：将实体添加到当前游标位置的查询中。 查询不会自动运行。 双击某个实体时，此操作是默认操作。 生成查询时，请使用此操作。  

       - **查询全部**：针对此实体运行查询（包含所有属性）。 使用此操作可快速查询单个实体。  

       - **按设备查询**：针对此实体运行查询并对结果进行分组。 例如 `Disk | summarize dcount( Device ) by Name`  

    - 展开实体以查看每个实体可用的特定属性。 双击某个属性，将其添加到当前游标位置的查询。  

3. “主页”选项卡显示有关 CMPivot 的常规信息，包括示例查询和支持文档的链接  。  

4. “查询”选项卡显示查询窗格、结果窗格和状态栏  。 在上面的屏幕截图示例中选中了“查询”选项卡。  

5. 通过查询窗格，可以在集合中生成或键入要在客户端上运行的查询。  

    - CMPivot 使用 [Kusto 查询语言 (KQL)](https://docs.microsoft.com/azure/kusto/query/) 子集。  

    - 在查询窗格中剪切、复制或粘贴内容。  
    <!-- markdownlint-disable MD038 -->
    - 默认情况下，此窗格使用 IntelliSense。 例如，如果开始键入 `D`，IntelliSense 会建议以该字母开头的所有实体。 选择一个选项，然后按 Tab 将其插入。 键入一个管道字符和一个空格 `| `，然后 IntelliSense 便会建议所有表运算符。 插入 `summarize` 并键入空格，IntelliSense 会建议所有聚合函数。 有关这些运算符和函数的详细信息，请单击 CMPivot 中的“主页”选项卡  。  

    - 查询窗格还提供以下选项：  

        - 运行该查询。  

        - 在查询历史记录列表中前后移动。  

        - 创建直属成员资格集合。  

        - 将查询结果导出到 CSV 或剪贴板。  

6. 结果窗格会显示活动客户端针对查询返回的数据。  

   - 可用的列视实体和查询而定。  

   - 单击列名以按照该属性对结果进行排序。  

   - 右键单击任何列名，按照该列中的相同信息对结果进行分组，或者排序。  

   - 右键单击设备名称，在设备上执行以下附加操作：  

      - **切换到**：查询此设备上的其他实体。  

      - **运行脚本**：启动“运行脚本”向导，在此设备上运行现有 PowerShell 脚本。 有关详细信息，请参阅[运行脚本](../../../apps/deploy-use/create-deploy-scripts.md#run-a-script)。  

      - **远程控制**：在此设备上启动 Configuration Manager 远程控制会话。 有关详细信息，请参阅[如何远程管理 Windows 客户端计算机](../../clients/manage/remote-control/remotely-administer-a-windows-client-computer.md)。  

      - **资源浏览器**：启动此设备的 Configuration Manager 资源浏览器。 有关详细信息，请参阅[查看硬件清单](../../clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md)或[查看软件清单](../../clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md)。  

   - 右键单击任何非设备单元格，以执行以下附加操作：  

     - **复制**：将单元格的文本复制到剪贴板。  

     - **显示具备以下条件的设备**：查询具有此属性值的设备。 例如，从 `OS` 查询的结果中，在“版本”行中的单元格上选择此选项：`OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ > 0)`  

     - **显示不具备以下条件的设备**：查询没有此属性值的设备。 例如，从 `OS` 查询的结果中，在“版本”行中的单元格上选择此选项：`OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ == 0) | project Device`  

     - **使用必应进行搜索**：使用此值作为查询字符串，启动默认 Web 浏览器以转到 https://www.bing.com 。  

   - 单击任何超链接文本，可转到针对该特定信息的视图。  

   - 结果窗格显示的行不会超过 20,000 个。 调整查询以进一步筛选数据，或者在较小的集合上重新启动 CMPivot。  

7. 状态栏显示以下信息（从左到右）：  

   - 目标集合的当前查询状态。 此状态包括：  
     - 完成查询的活动客户端数量 (3)  
     - 客户端总数 (5)  
     - 脱机客户端数量 (2)  
     - 返回失败的任何客户端 (0)  

       例如：`Query completed on 3 of 5 clients (2 clients offline and 0 failure)`  

   - 客户端操作的 ID。 例如：`id(16780221)`  

   - 当前集合。 例如：`PM_Team_Machines`  

   - 结果窗格中的总行数。 例如 `1 objects`  



## <a name="example-scenarios"></a>方案示例

以下部分提供了有关如何在环境中使用 CMPivot 的示例：


### <a name="example-1-stop-a-running-service"></a>示例 1：停止正在运行的服务

安全管理员要求尽快对会计部门的所有设备停止并禁用计算机浏览器服务。 可对会计部门中所有设备的集合启动 CMPivot，并在“Service”实体上选择“查询全部”   。 

`Service`

显示结果时，右键单击“Name”列，然后选择“分组依据”   。 

`Service | summarize dcount( Device ) by Name`

在“浏览器”服务的行中，单击“dcount_”列中的超链接数字   。 

`Service | where (Name == 'Browser') | summarize count() by Device`

可以选择多个设备，右键单击所选设备，然后选择“运行脚本”  。 此操作将启动“运行脚本”向导，你可以通过该向导运行用于停止和禁用服务的现有脚本。 借助 CMPivot，可以快速响应所有活动计算机的安全事件，并在“运行脚本”向导中查看结果。 然后继续创建配置基线，以修复集合中的其他计算机，因为它们将来会变为活动状态。 

![浏览器服务和“运行脚本”操作的 CMPivot 示例](media/cmpivot-example1.png)


### <a name="example-2-proactively-resolve-application-failures"></a>示例 2：主动解决应用程序故障  

为主动进行操作维护，可每周一次对管理的服务器集合运行 CMPivot，并在“AppCrash”实体上选择“查询所有”   。 右键单击“FileName”列，然后选择“升序排序”   。 一台设备会为 sqlsqm.exe 返回七个结果，时间戳大约为每天 03:00。 你可以在其中一行中选择文件名，右键单击该名称，然后选择“使用必应进行搜索”  。 在 Web 浏览器中浏览搜索结果时，可找到有关此问题的 Microsoft 支持文章，其中会包含详细信息和解决方案。 


### <a name="example-3-bios-version"></a>示例 3：BIOS 版本

若要[缓解推测执行端通道漏洞](https://techcommunity.microsoft.com/t5/configuration-manager-blog/additional-guidance-to-mitigate-speculative-execution-side/ba-p/274974)，其中一个要求就是更新系统 BIOS。 首先查询 BIOS 实体  。 然后按“Version”属性进行分组   。 再右键单击某个特定值，例如“LENOVO - 1140”，并选择“显示具备以下条件的设备”  。  

`Bios | summarize countif( (Version == 'LENOVO - 1140') ) by Device | where (countif_ > 0)`


### <a name="example-4-free-disk-space"></a>示例 4：可用磁盘空间

需要在网络文件服务器上临时存储大型文件，但不确定哪个磁盘拥有足够的容量。 对文件服务器集合启动 CMPivot，并查询“Disk”实体  。 修改 CMPivot 的查询以快速返回包含实时存储数据的活动服务器列表：  

`Disk | where (Description == 'Local Fixed Disk') | where isnotnull( FreeSpace ) | order by FreeSpace asc`


## <a name="cmpivot-starting-in-version-1810"></a><a name="bkmk_cmpivot"></a> 从版本 1810 开始的 CMPivot
<!--1359068, 3607759-->

从 Configuration Manager 版本 1810 开始，CMPivot 就包括以下改进：

- [CMPivot 实用工具和性能](#bkmk_cmpivot-perf)
- [标量函数](#bkmk_cmpivot-functions)  
- [呈现可视化效果](#bkmk_cmpivot-charts)  
- [硬件清单](#bkmk_cmpivot-hinv)  
- [标量运算符](#bkmk_cmpivot-operators)  
- [查询摘要](#bkmk_cmpivot-summary)  
- [审核状态消息](#cmpivot-audit-status-messages)

### <a name="cmpivot-utility-and-performance"></a><a name="bkmk_cmpivot-perf"></a> CMPivot 实用工具和性能

- CMPivot 最多返回 100,000 个单元格而不是 20,000 行。
  - 如果实体有 5 个属性，即表示将显示 5 列和最多 20,000 行。
  - 对于有 10 个属性的实体，最多显示 10,000 行。
  - 显示的总数据将小于或等于 100,000 个单元格。
- 在“查询摘要”选项卡上，选择“故障”或“脱机”设备的计数，然后选择“创建集合”选项。  使用此选项，可通过修正部署轻松定位这些设备。
- 通过单击文件夹图标保存收藏夹查询  。
   ![在 CMPivot 中保存收藏夹查询的示例](media/cmpivot-favorite.png)

- 更新至 1810 版本的客户端会通过快速信道将不超过 80 KB 的输出返回到站点。
  - 这一更改提高了查看脚本或查询输出的性能。
  - 如果脚本或查询输出大于 80 KB，客户端会通过状态消息发送数据。
  - 如果客户端未更新至 1810 客户端版本，它将继续使用状态消息。

- 启动 CMPivot 时，可能会看到以下错误：**由于脚本版本不兼容，现在无法使用 CMPivot。这个问题可能是因为层次结构正在升级站点所导致的。等待升级完成，然后重试。**

  - 如果看到此消息，则表示：
    - 安全作用域设置不正确。
    - 升级过程中存在一些问题。
    - 基础 CMPivot 脚本不兼容。


### <a name="scalar-functions"></a><a name="bkmk_cmpivot-functions"></a>标量函数
CMPivot 支持下列标量函数：
- **ago()** ：从当前的 UTC 时钟时间减去给定的时间跨度  
- **datetime_diff()** :计算两个日期/时间值之间的日历间隔  
- **now()** ：返回当前 UTC 时钟时间  
- **bin()** ：将值舍入为给定装箱大小的整数倍数  

> [!Note]  
> 日期/时间数据类型表示某个时刻，通常表示为当天的日期和时间。 时间值以 1 秒为单位进行测量。 日期/时间值始终位于 UTC 时区中。 始终采用 ISO 8601 格式表示日期时间文本，例如 `yyyy-mm-dd HH:MM:ss`  

#### <a name="examples"></a>示例
- `datetime(2015-12-31 23:59:59.9)`：特定的日期时间文本   
- `now()`：当前时间  
- `ago(1d)`：当前时间减去一天  


### <a name="rendering-visualizations"></a><a name="bkmk_cmpivot-charts"></a> 呈现可视化效果

CMPivot 现在包括对 KQL [render 运算符](https://docs.microsoft.com/azure/kusto/query/renderoperator)的基本支持。 此支持包括以下类型：  
- **条形图**：第一列是 x 轴，可以为文本、日期/时间或数值。 第二个列必须是数字，并显示为水平条带。  
- **柱形图**：与条形图类似，带有垂直条带而不是水平条带。  
- **饼图**：第一列是颜色轴，第二列是数值。  
- **时间图**：折线图。 第一列是 x 轴，且应为日期/时间。 第二列是 y 轴。  

#### <a name="example-bar-chart"></a>示例：条形图
以下查询以条形图呈现最近使用的应用程序：

``` Kusto
CCMRecentlyUsedApplications
| summarize dcount( Device ) by ProductName
| top 10 by dcount_
| render barchart
```

![CMPivot 条形图可视化效果示例](media/1359068-cmpivot-barchart.png)

#### <a name="example-time-chart"></a>示例：时间图
要呈现时间图，请使用新的 bin() 运算符对某段时间的事件进行分组  。 以下查询显示过去七天内设备启动的时间：

``` Kusto
OperatingSystem
| where LastBootUpTime <= ago(7d)
| summarize count() by bin(LastBootUpTime,1d)
| render timechart
```

![CMPivot 时间图可视化效果示例](media/1359068-cmpivot-timechart.png)

#### <a name="example-pie-chart"></a>示例：饼图
以下查询显示饼图中的所有 OS 版本：

``` Kusto
OperatingSystem
| summarize count() by Caption
| render piechart
```

![CMPivot 饼图可视化效果示例](media/1359068-cmpivot-piechart.png)


### <a name="hardware-inventory"></a><a name="bkmk_cmpivot-hinv"></a>硬件清单
使用 CMPivot 查询任何硬件清单类。 这些类包括对硬件清单所做的任何自定义扩展。 CMPivot 立即返回存储在站点数据库中的上次硬件清单扫描的缓存结果。 同时，它会根据需要使用来自任何在线客户端的实时数据更新结果。

结果表或图表中数据的颜色饱和度表示数据是实时的还是缓存的。 例如，深蓝色是来自在线客户端的实时数据。 浅蓝色是缓存数据。

#### <a name="example"></a>示例

``` Kusto
LogicalDisk
| summarize sum( FreeSpace ) by Device
| order by sum_ desc
| render columnchart
```

![带柱形图可视化效果的 CMPivot 清单查询示例](media/1359068-cmpivot-inventory.png)

#### <a name="limitations"></a>限制
- 以下硬件清单实体不受支持：  
    - 数组属性，例如 IP 地址  
    - Real32/Real64 <!--example?-->  
    - 嵌入的对象属性 <!--example?-->  
- 清单实体名称必须以字符开头
- 不能通过创建具有相同名称的清单实体覆盖内置实体  


### <a name="scalar-operators"></a><a name="bkmk_cmpivot-operators"></a>标量运算符
CMPivot 包括以下标量运算符：  

> [!Note]  
> - LHS：运算符左侧的字符串  
> - RHS：运算符右侧的字符串  


|运算符|说明|示例（生成 true）|
|--------|-----------|---------------------|
|==|等于|`"aBc" == "aBc"`|
|!=|不等于|`"abc" != "ABC"`|
|like|LHS 包含 RHS 的匹配项|`"FabriKam" like "%Brik%"`|
|!like|LHS 不包含 RHS 的匹配项|`"Fabrikam" !like "%xyz%"`|
|包含|RHS 以 LHS 子序列的形式存在|`"FabriKam" contains "BRik"`|
|!contains|LHS 中未出现 RHS|`"Fabrikam" !contains "xyz"`|
|startswith|RHS 是 LHS 的初始子序列|`"Fabrikam" startswith "fab"`|
|!startswith|RHS 不是 LHS 的初始子序列|`"Fabrikam" !startswith "kam"`|
|endswith|RHS 是 LHS 的闭合子序列|`"Fabrikam" endswith "Kam"`|
|!endswith|RHS 不是 LHS 的闭合子序列|`"Fabrikam" !endswith "brik"`|


### <a name="query-summary"></a><a name="bkmk_cmpivot-summary"></a>查询摘要

选择 CMPivot 窗口底部的“查询摘要”选项卡  。 此状态可帮助你识别离线的客户端，或排查可能发生的故障。 在“计数”列中选择一个值以打开具有该状态的特定设备的列表。 

例如，选择状态为“故障”的设备的计数。 请查看特定的错误消息，并导出这些设备列表。 如果错误是无法识别的特定 cmdlet，请使用导出的设备列表创建集合以部署 Windows PowerShell 更新。  

### <a name="cmpivot-audit-status-messages"></a>CMPivot 审核状态消息

从版本 1810 开始，运行 CMPivot 时，MessageID 40805 会创建审核状态消息  。 可通过转到“监视” > “系统状态” > “状态消息查询”    查看状态消息。 可为指定用户运行所有审核状态消息，为指定站点运行所有审核状态消息，或创建自己的状态消息查询   。

消息使用以下格式：

MessageId 40805:User &lt;UserName> ran script &lt;Script-Guid> with hash &lt;Script-Hash> on collection &lt;Collection-ID>。

- 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 是 CMPivot 的 Script-Guid。
- 可以在客户端的 scripts.log 文件中查看 Script-Hash。
- 也可以查看存储在客户端脚本存储中的哈希。 客户端上的文件名为 &lt;Script-Guid>_&lt;Script-Hash>。
    - 示例文件名：C:\Windows\CCM\ScriptStore\7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14_abc1d23e45678901fabc123d456ce789fa1b2cd3e456789123fab4c56789d0123.ps
   

![CMPivot 审核状态消息示例](media/cmpivot-audit-status-message.png)

## <a name="cmpivot-starting-in-version-1902"></a><a name="bkmk_cmpivot1902"></a> 从版本 1902 开始的 CMPivot
<!--3610960-->
从 Configuration Manager 版本 1902 开始，可以在层次结构中从管理中心站点 (CAS) 运行 CMPivot。 主站点仍可处理与客户端的通信。 从管理中心站点运行 CMPivot 时，它将通过高速消息订阅通道与主站点通信。 该通信不依赖于站点之间的标准 SQL 复制。

当 SQL 或提供程序不在同一台计算机上时，或在 SQL Always On 配置的情况下，在 CAS 上运行 CMPivot 将需要其他权限。 使用这些远程配置，即可为 CMPivot 配置“双跃点方案”。

若要在这种“双跃点方案”中让 CMPivot 使用 CAS，可以定义约束委派。 若要了解此配置的安全隐患，请阅读 [Kerberos 约束委派](https://docs.microsoft.com/windows-server/security/kerberos/kerberos-constrained-delegation-overview)一文。 Kerberos 需要使用计算机之间的所有跃点。<!--5746133--> 如果正在使用或未使用 CAS 并置多个远程配置（例如 SQL 或 SMS 提供程序），或有多个受信任林，则可能需要权限设置组合。 下面是你可能需要遵循的步骤：

### <a name="cas-has-a-remote-sql-server"></a>CAS 具有远程 SQL Server

1. 请转到每个主站点的 SQL Server。
   1. 将 CAS 远程 SQL Server 和 CAS 站点服务器添加到 [Configmgr_DviewAccess](../../plan-design/hierarchy/accounts.md#configmgr_dviewaccess) 组。
   ![主站点 SQL Server 上的 Configmgr_DviewAccess 组](media/cmpivot-dviewaccess-group.png)
1. 转到 Active Directory 用户和计算机。
   1. 对于每个主站点服务器，请右键单击并选择“属性”  。
      1. 在委托选项卡上，选择第三个选项，“仅信任此计算机委派指定的服务”  。 
      1. 选择“仅使用 Kerberos”  。
      1. 使用端口和实例添加 CAS SQL Server 服务。
      1. 请确保这些更改与公司安全策略保持一致！
   1. 对于 CAS 站点，请右键单击并选择“属性”  。
      1. 在委托选项卡上，选择第三个选项，“仅信任此计算机委派指定的服务”  。 
      1. 选择“仅使用 Kerberos”  。
      1. 使用端口和实例添加每个主站点的 SQL Server 服务。
      1. 请确保这些更改与公司安全策略保持一致！

   ![双跃点的 CMPivot AD 委派示例](media/cmpivot-ad-delegation.png)

### <a name="cas-has-a-remote-provider"></a>CAS 具有远程提供程序

1. 请转到每个主站点的 SQL Server。
   1. 将 CAS 提供程序计算机帐户和 CAS 站点服务器添加到 [Configmgr_DviewAccess](../../plan-design/hierarchy/accounts.md#configmgr_dviewaccess) 组。
1. 转到 Active Directory 用户和计算机。
   1. 选择 CAS 提供程序计算机，右键单击并选择“属性”  。
      1. 在委托选项卡上，选择第三个选项，“仅信任此计算机委派指定的服务”  。 
      1. 选择“仅使用 Kerberos”  。
      1. 使用端口和实例添加每个主站点的 SQL Server 服务。
      1. 请确保这些更改与公司安全策略保持一致！
   1. 选择 CAS 站点服务器，右键单击并选择“属性”  。
      1. 在委托选项卡上，选择第三个选项，“仅信任此计算机委派指定的服务”  。 
      1. 选择“仅使用 Kerberos”  。
      1. 使用端口和实例添加每个主站点的 SQL Server 服务。
      1. 请确保这些更改与公司安全策略保持一致！
1. 重启 CAS 远程提供程序计算机。

### <a name="sql-always-on"></a>SQL Always On

1. 请转到每个主站点的 SQL Server。
   1. 将 CAS 站点服务器添加到 [Configmgr_DviewAccess](../../plan-design/hierarchy/accounts.md#configmgr_dviewaccess) 组。
1. 转到 Active Directory 用户和计算机。
   1. 对于每个主站点服务器，请右键单击并选择“属性”  。
      1. 在委托选项卡上，选择第三个选项，“仅信任此计算机委派指定的服务”  。 
      1. 选择“仅使用 Kerberos”  。
      1. 使用端口和实例为 SQL 节点添加 CAS SQL Server 服务帐户。
      1. 请确保这些更改与公司安全策略保持一致！
   1. 选择 CAS 站点服务器，右键单击并选择“属性”  。
      1. 在委托选项卡上，选择第三个选项，“仅信任此计算机委派指定的服务”  。 
      1. 选择“仅使用 Kerberos”  。
      1. 使用端口和实例添加每个主站点的 SQL Server 服务。
      1. 请确保这些更改与公司安全策略保持一致！
1. 请确保 [SPN 发布](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/listeners-client-connectivity-application-failover?view=sql-server-2017#SPNs)使用 CAS SQL 侦听器名称和每个主 SQL 侦听器名称。
1. 重启主 SQL Server。
1. 重启 CAS 站点服务器和 CAS SQL Server。

## <a name="cmpivot-starting-in-version-1906"></a><a name="bkmk_cmpivot1906"></a> 从版本 1906 开始的 CMPivot

从版本 1906 开始，已向 CMPivot 添加以下项：

- [联接、其他运算符和聚合器](#bkmk_cmpivot_joins)
- [已向安全管理员角色添加 CMPivot 权限](#bkmk_cmpivot_secadmin1906)
- [CMPivot 独立应用](#bkmk_standalone)

### <a name="add-joins-additional-operators-and-aggregators-in-cmpivot"></a><a name="bkmk_cmpivot_joins"></a> 在 CMPivot 中添加联接、其他运算符和聚合器
<!--4054074-->
你现在有更多的算术运算符和聚合器，还可以添加查询联接（例如可以同时使用注册表和文件）。 已添加以下项：

#### <a name="table-operators"></a>表运算符

|表运算符| 说明|
|-----|-----|
| [联接](https://docs.microsoft.com/azure/kusto/query/joinoperator)| 通过匹配同一设备的行来合并两个表的行，以便形成新的表|
|呈现|将结果呈现为图形输出|

CMPivot 中已存在呈现运算符。 已添加对多序列和“with”语句的支持  。 有关详细信息，请参阅[示例](#bkmk_cmpivot_examples1906)部分和 Kusto 的[联接运算符](https://docs.microsoft.com/azure/kusto/query/joinoperator)一文。

#### <a name="limitations-for-joins"></a>联接的限制

1. 联接列始终在“Device”字段上隐式完成  。
1. 每个查询最多可使用 5 个联接。
1. 最多可使用 64 个合并列。

#### <a name="scalar-operators"></a>标量运算符

|运算符| 说明|示例|
|-----|-----|-----|
| + | 添加| `2 + 1, now() + 1d`|
| - |  减| `2 - 1, now() - 1d`|
| * | 乘| `2 * 2`|
| / | 除 | `2 / 1`|
| % | 取模 | `2 % 1`

#### <a name="aggregation-functions"></a>聚合函数

|函数| 说明|
|-----|-----|
| percentile()| 针对由 Expr 定义的填充，返回其中指定的最接近排名百分位数的估计值|
| sumif() | 返回谓词计算结果为 True 的 Expr 总和|

#### <a name="scalar-functions"></a>标量函数

|函数| 说明|
|-----|-----|
| case()| 计算谓词的列表，并返回满足其谓词的第一个结果表达式 |
| iff() | 计算第一个参数，并根据谓词计算结果为 True（第二个）还是 False（第三个），返回第二个或第三个参数的值|
 | indexof() | 该函数报告输入字符串中指定字符串第一次出现时从零开始的索引|
| strcat() | 连接 1 个到 64 个自变量 |
| strlen()| 返回输入字符串的长度（以字符为单位）|
| substring() | 从源字符串中提取从某个索引开始到字符串结尾的 substring |
| tostring() | 将输入转换为字符串操作 |

#### <a name="examples"></a><a name="bkmk_cmpivot_examples1906"></a> 示例

- 显示设备、制造商、模型和 OSVersion：

   ``` Kusto
   ComputerSystem
   | project Device, Manufacturer, Model
   | join (OperatingSystem | project Device, OSVersion=Caption)
   ```

- 显示设备的启动时间图：

   ``` Kusto
   SystemBootData
   | where Device == 'MyDevice'
   | project SystemStartTime, BootDuration, OSStart=EventLogStart, GPDuration, UpdateDuration
   | order by SystemStartTime desc
   | render barchart with (kind=stacked, title='Boot times for MyDevice', ytitle='Time (ms)')
   ```

   ![以毫秒为单位显示设备启动时间的堆积条形图](./media/4054074-render-using-with-statement.png)

### <a name="added-cmpivot-permissions-to-the-security-administrator-role"></a><a name="bkmk_cmpivot_secadmin1906"></a> 已向安全管理员角色添加 CMPivot 权限
<!--4683130-->

从版本 1906 开始，已向 Configuration Manager 的内置安全管理员角色添加以下权限  ：

 - 读取  SMS 脚本
 - 在集合上运行 CMPivot 
 - 读取清单报表 

>[!NOTE]
> “运行脚本”  是“运行 CMPivot”  权限的超集。
 

### <a name="cmpivot-standalone"></a><a name="bkmk_standalone"></a> CMPivot 独立应用
<!--3555890, 4619340, 4683130 -->

从版本 1906 开始，可以将 CMPivot 用作独立应用。 CMPivot 独立应用仅提供英语版本。 在 Configuration Manager 控制台外部运行 CMPivot，可以查看环境中设备的实时状态。 借助此变化，无需先安装控制台，即可在设备上使用 CMPivot。

> [!Tip]  
> 此功能在版本 1906 中作为[预发行功能](pre-release-features.md)首次引入。 从版本 2002 开始，此功能不再属于预发行功能。  

可以与其他尚未在计算机上安装控制台的角色（例如支持人员或安全管理员）共享功能强大的 CMPivot。 这些其他角色可以将 CMPivot 与他们传统上使用的其他工具并行使用，以查询 Configuration Manager。 通过共享此类丰富的管理数据，你们可以一起工作，共同主动解决跨角色的业务问题。

#### <a name="install-cmpivot-standalone"></a>安装 CMPivot 独立应用

1. 设置运行 CMPivot 所需的权限。 有关详细信息，请参阅[先决条件](#prerequisites)。 如果这些权限适用于用户，则还可以使用[安全管理员角色](#bkmk_cmpivot_secadmin1906)。
2. 在下面的路径找到 CMPivot 应用安装程序：`<site install path>\tools\CMPivot\CMPivot.msi`。 可以从此路径运行它，也可以将其复制到其他位置。
3. 运行 CMPivot 独立应用时，系统将要求你连接到站点。 指定管理中心或主站点服务器的完全限定的域名或计算机名。
   - 每次打开 CMPivot 时，系统将提示你连接到站点服务器。
4. 浏览到要在其上运行 CMPivot 的集合，然后运行查询。

   ![浏览到要对其运行查询的集合](./media/3555890-cmpivot-standalone-browse-collection.png)

> [!NOTE]
> 右键单击操作（例如，“运行脚本”、“资源浏览器”）和 Web 搜索在 CMPivot 独立应用中不可用   。 CMPivot 独立应用的主要用途是独立于 Configuration Manager 基础结构进行查询。 为帮助安全管理员，CMPivot 独立应用确实包含连接到 Microsoft Defender 安全中心的功能。 <!--5605358-->

## <a name="cmpivot-starting-in-version-1910"></a><a name="bkmk_cmpivot1910"></a> 从版本 1910 开始的 CMPivot
<!--5410930, 3197353-->
从版本 1910 开始，CMPivot 进行了显著的优化，以减少服务器上的网络流量和负载。 此外，还添加了一些实体和实体增强功能，以帮助进行故障排除和搜寻。 版本 1910 中为 CMPivot 引入了以下更改：

- [对 CMPivot 引擎的优化](#bkmk_optimization)
- 其他实体和实体增强功能：
  - Windows 事件日志 ([WinEvent](#bkmk_WinEvent))
  - 文件内容 ([FileContent](#bkmk_File))
  - 由进程加载的 dll ([ProcessModule](#bkmk_ProcessModule))
  - Azure Active Directory 信息 ([AADStatus](#bkmk_AadStatus))
  - Endpoint Protection 状态 ([EPStatus](#bkmk_EPStatus))
- [使用 CMPivot 独立应用的本地设备查询评估](#bkmk_local-eval)
- [CMPivot 的其他增强功能](#bkmk_Other)


### <a name="optimizations-to-the-cmpivot-engine"></a><a name="bkmk_optimization"></a> 对 CMPivot 引擎的优化
<!--3197353-->
为了减少服务器上的网络流量和负载，CMPivot 在版本 1910 中进行了优化。 许多查询操作现在直接在客户端上执行，而不是在服务器上执行。 此更改还意味着某些 CMPivot 操作从第一个查询返回的数据最少。 如果决定钻取数据以获取更多信息，则可能会运行一个新查询以从客户端获取其他数据。 例如，以前运行“汇总计数”查询时，会向服务器返回一个大型数据集。  虽然返回大型数据集可立即进行向下钻取，但很多时候只需要汇总计数即可。 在版本 1910 中，当选择钻取到特定客户端时，会发生另一个数据集合，以返回你请求的其他数据。 此更改有助于改善针对大量客户端进行查询的性能和可伸缩性。 <!--3197353, 5458337-->

#### <a name="examples"></a>示例

CMPivot 优化大大减少了运行 CMPivot 查询所需的网络和服务器 CPU 负载。 通过这些优化，现在可以实时筛选千兆字节的客户端数据。 以下查询说明了这些优化：

- 搜索企业中所有客户端的所有事件日志中的身份验证失败。

   ``` Kusto
   EventLog('Security')
   | where  EventID == 4673
   | summarize count() by Device
   | order by count_ desc
   ```

- 按哈希搜素文件。

   ``` Kusto
   Device
   | join kind=leftouter ( File('%windir%\\system32\\*.exe')
   | where SHA256Hash == 'A92056D772260B39A876D01552496B2F8B4610A0B1E084952FE1176784E2CE77')
   | project Device, MalwareFound = iif( isnull(FileName), 'No', 'Yes')
   ```

### <a name="wineventlognametimespan"></a><a name="bkmk_WinEvent"></a> WinEvent(\<logname>,[\<timespan>])

该实体用于从事件日志和事件跟踪日志文件中获取事件。 该实体从 Windows 事件日志技术生成的事件日志中获取数据。 该实体还获取由 Windows 事件跟踪 (ETW) 生成的日志文件中的事件。 默认情况下，WinEvent 会查看最近 24 小时内发生的事件。 但是，可以通过包含时间跨度来覆盖 24 小时默认值。

``` Kusto
WinEvent('Microsoft-Windows-HelloForBusiness/Operational', 1d)
| where LevelDisplayName =='Error'
| summarize count() by Device
```

### <a name="filecontentfilename"></a><a name="bkmk_File"></a> FileContent(\<filename>)

FileContent 用于获取文本文件的内容。

``` Kusto
FileContent('c:\\windows\\SMSCFG.ini')
| where Content startswith  'SMS Unique Identifier='
| project Device, SMSId= substring(Content,22)
```

### <a name="processmoduleprocessname"></a><a name="bkmk_ProcessModule"></a> ProcessModule(\<processname>)  

该实体用于枚举给定进程加载的模块 (dll)。 在搜寻合法进程中隐藏的恶意软件时，ProcessModule 非常有用。  

``` Kusto
ProcessModule('powershell')
| summarize count() by ModuleName
| order by count_ desc
```

### <a name="aadstatus"></a><a name="bkmk_AadStatus"></a> AadStatus

该实体可用于从设备获取当前 Azure Active Directory 的标识信息。

``` Kusto
AadStatus
| project Device, IsAADJoined=iif( isnull(DeviceId),'No','Yes')
| summarize DeviceCount=count() by IsAADJoined
| render piechart
```

### <a name="epstatus"></a><a name="bkmk_EPStatus"></a> EPStatus

EPStatus 用于获取计算机上安装的反恶意软件的状态。

``` Kusto
EPStatus
| project Device, QuickScanAge=datetime_diff('day',now(),QuickScanEndTime)
| summarize DeviceCount=count() by QuickScanAge
| order by QuickScanAge
| render barchart
```

### <a name="local-device-query-evaluation-using-cmpivot-standalone"></a><a name="bkmk_local-eval"></a> 使用 CMPivot 独立应用的本地设备查询评估
<!--3197353-->
在 Configuration Manager 控制台外使用 CMPivot 时，可以仅查询本地设备，而无需 Configuration Manager 基础结构。 现在可以利用 CMPivot Azure Log Analytics 查询快速查看本地设备上的 WMI 信息。 还可以在较大的环境中运行 CMPivot 查询之前对其进行验证和优化。 CMPivot 独立应用仅提供英语版本。 有关安装 CMPivot 独立应用的详细信息，请参阅[安装 CMPivot 独立应用](#install-cmpivot-standalone)。

#### <a name="known-issues-for-local-device-query-evaluation"></a>本地设备查询评估的已知问题

 - 如果在“此电脑”上查询你无权访问的 WMI 实体（例如锁定的 WMI 类），则可能会在 CMPivot 中出现故障  。 使用具有提升权限的帐户运行 CMPivot 以查询这些实体。 <!--5753242-->
- 如果在“此电脑”上查询非 WMI 实体，你将看到“无效的命名空间”或不明确的异常   。
- 从“开始”菜单快捷方式运行 CMPivot 独立应用，而不是直接从可执行文件的路径运行。 <!--5787962-->

### <a name="other-enhancements"></a><a name="bkmk_Other"></a> 其他增强功能

- 可以使用新的 `like` 运算符执行正则表达式类型查询。 例如：<!--3056858-->
  
   ```kusto
   //Find BIOS manufacture that contains any word like Micro, such as Microsoft
   Bios
   | where Manufacturer like '%Micro%'
   ```

- 我们已将 CcmLog() 和 EventLog() 实体更新为在默认情况下仅查看最近 24 小时内的消息   。 通过传入可选的时间跨度可以覆盖此行为。 例如，以下查询将查看最近 1 小时内的事件：

   ```kusto
   CcmLog('Scripts',1h)
   ```

- **File()** 实体已更新为收集有关隐藏文件和系统文件的信息，并包含 MD5 哈希。 虽然 MD5 哈希不像 SHA256 哈希那么准确，但它通常是大多数恶意软件公告中的常见哈希。  

- 您可以在查询中添加注释。<!-- 5431463 --> 共享查询时，此行为很有用。 例如：

    ``` Kusto
    //Get the top ten devices sorted by user
    Device
    | top 10 by UserName
    ```

- CMPivot 会自动连接到最后一个站点。<!-- 5420395 --> 启动 CMPivot 后，可以根据需要连接到新站点。

- 从“导出”菜单中，选择新选项“查询链接到剪贴板”   。<!-- 5431577 --> 此操作会将链接复制到剪贴板，以便与他人共享。 例如：

    `cmpivot:Ly8gU2FtcGxlIHF1ZXJ5DQpPcGVyYXRpbmdTeXN0ZW0NCnwgc3VtbWFyaXplIGNvdW50KCkgYnkgQ2FwdGlvbg0KfCBvcmRlciBieSBjb3VudF8gYXNjDQp8IHJlbmRlciBiYXJjaGFydA==`

    此链接将打开 CMPivot 独立版本并包含以下查询：

    ``` Kusto
    // Sample query
    OperatingSystem
    | summarize count() by Caption
    | order by count_ asc
    | render barchart
    ```

    > [!TIP]
    > 要使此链接正常工作，请[安装 CMPivot 独立版本](#install-cmpivot-standalone)。

- 在查询结果中，如果设备已在 Microsoft Defender 高级威胁防护 (ATP) 中注册，请右键单击该设备以启动 Microsoft Defender 安全中心在线门户  。

### <a name="known-issues-for-cmpivot-in-version-1910"></a>版本 1910 中 CMPivot 的已知问题

- 当达到限制时，不显示最大结果横幅。 <!--5431427-->
  - 每个客户端每次查询的数据大小限制为 128 KB。
  - 如果查询的结果超过 128 KB，可能会截断结果。
  
## <a name="cmpivot-starting-in-version-2002"></a><a name="bkmk_2002"></a> 从版本 2002 开始的 CMPivot
<!--5870934-->
我们简化了 CMPivot 实体的导航。 从 Configuration Manager 版本 2002 开始，可以搜索 CMPivot 实体。 还添加了新图标，以轻松地区分实体和实体对象类型。

![搜索 CMPivot 实体](./media/5870934-search-cmpivot-entities.png)

 
## <a name="inside-cmpivot"></a>深入了解 CMPivot

CMPivot 使用 Configuration Manager“快速通道”向客户端发送查询。 其他功能也使用这个从服务器到客户端的信道，例如客户端通知操作、客户端状态和 Endpoint Protection。 客户端通过类似的快速状况消息系统返回结果。 状况消息临时存储在数据库中。 如需深入了解用于客户端通知的端口，请参阅[端口](../../plan-design/hierarchy/ports.md#BKMK_PortsClient-MP)一文。

查询和结果都只是文本。 InstallSoftware 和 Process 实体均返回一些最大的结果集   。 性能测试期间，对于这些查询而言，来自一个客户端的最大状态消息文件大小小于 1 KB  。 扩展到包含 50,000 个活动客户端的大型环境后，此一次性查询将在网络上生成不超过 50 MB 的数据。 欢迎页上所有带下划线的项，每个客户端将返回不超过 1k 的信息。

![CMPivot 带下划线的实体示例](media/cmpivot-underlined-entities.png)

从 Configuration Manager 1810 开始，CMPivot 可以查询硬件清单数据，包括扩展的硬件清单类。 这些新实体（欢迎页上不带下划线的实体）可能返回更大的数据集，具体取决于给定硬件清单属性定义的数据量。 例如，“InstalledExecutable”实体可能会为每个客户端返回多个 MB 数据，具体取决于查询的特定数据。 使用 CMPivot 从更大的集合中返回更大的硬件清单数据集时，请注意性能和可伸缩性。

查询在一小时后超时。 例如，一个集合有 500 台设备，450 个客户端当前处于联机状态。 这些活动设备接收查询后，几乎可以立即返回结果。 如果打开 CMPivot 窗口，当其他 50 个客户端联机时，它们也会收到查询并返回结果。 

## <a name="log-files"></a>日志文件

 CMPivot 交互将记录到以下日志文件：

 服务器端：
- SmsProv.log
- BgbServer.log
- StateSys.log

 客户端：
- CCMNotificationAgent.log
- Scripts.log
- StateMessage.log

有关详细信息，请参阅[日志文件](../../plan-design/hierarchy/log-files.md)和[CMPivot 疑难解答](cmpivot-tsg.md)。

## <a name="next-steps"></a>后续步骤
 
[CMPivot 疑难解答](cmpivot-tsg.md)

[创建并运行 PowerShell 脚本](../../../apps/deploy-use/create-deploy-scripts.md)


