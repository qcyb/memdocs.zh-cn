---
title: 使用 CMPivot 获得实时数据
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中使用 CMPivot 实时查询客户端。
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 32e2d6b9-148f-45e2-8083-98c656473f82
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 11b5a58a6d9501b0368fcb0b47bf31df1bd8a6af
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700576"
---
# <a name="cmpivot-for-real-time-data-in-configuration-manager"></a>在 Configuration Manager 中使用 CMPivot 获得实时数据

<!--1358456-->

适用范围：Configuration Manager (Current Branch)

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

- CMPivot 和 [Microsoft Edge](../../../apps/deploy-use/deploy-edge.md) 安装程序通过 Microsoft 代码签名证书进行签名。 如果“受信任的发行者”存储中未列出该证书，则需要添加它。 否则，当 PowerShell 执行策略设置为“AllSigned”时，CMPivot 和 Microsoft Edge 安装程序不会运行。 <!--7585106-->

## <a name="permissions"></a>权限

CMPivot 需要以下权限：

- “SMS 脚本”对象上的“读取权限” 
- “集合”上的“运行脚本”权限 
   - 或者，从版本 1906 开始，可以在“集合”上使用“运行 CMPivot”。
- “清单报表”上的“读取”权限 
- 默认范围。

> [!NOTE]
> - “运行脚本”是“运行 CMPivot”权限的超集。
> - 自版本 1906 起，向 Configuration Manager 的内置安全管理员角色添加了 [CMPivot 的权限](cmpivot-changes.md#bkmk_cmpivot_secadmin1906)。
 
## <a name="limitations"></a>限制

- 在层次结构中，将 Configuration Manager 控制台连接到主站点以运行 CMPivot。 当“启动 CMPivot”操作连接到管理中心站点 (CAS) 时，它不会出现在控制台中。
  - 从 Configuration Manager 版本 1902 开始，就可以从 CAS 运行 CMPivot。 在某些环境中，需要其他权限。 有关详细信息，请参阅[版本 1902 的 CMPivot 更改](cmpivot-changes.md#bkmk_cmpivot1902)。

- CMPivot 仅返回用于将客户端连接到当前站点的数据。  

- 如果集合包含来自其他站点的设备，则 CMPivot 结果仅来自当前站点中的设备。  

- 用户无法自定义实体属性、结果列或设备上的操作。  

- 只有一个 CMPivot 实例可以在运行 Configuration Manager 控制台的计算机上同时运行。  

- 在版本 1806 中，只有在组名为“管理员”时，对“管理员”实体的查询才起作用。 如果组名已本地化，则不起作用。 例如，法语“Administrateurs”。<!--SCCMDocs issue 759-->  


## <a name="start-cmpivot"></a>启动 CMPivot

1. 在 Configuration Manager 控制台中，连接到主站点。 转到“资产和符合性”工作区，并选择“设备集合”节点。 选择目标集合，然后单击功能区中的“启动 CMPivot”，以便启动该工具。 如果看不到此选项，请检查以下配置：  
   - 与站点管理员确认你的帐户具有所需权限。 有关详细信息，请参阅[先决条件](#prerequisites)。  
   - 将控制台连接到主站点。  

2. 界面进一步提供有关使用该工具的信息。  

     - 可在顶部手动输入查询字符串，或单击联机文档中的链接。  

     - 单击其中一个实体将其添加到查询字符串。  

     - 有关表运算符、聚合函数和标量函数的链接，请在 Web 浏览器中打开语言参考文档。 CMPivot 使用 [Kusto 查询语言 (KQL)](/azure/kusto/query/)。  

3. 打开 CMPivot 窗口，查看来自客户端的结果。 关闭 CMPivot 窗口时，会话已完成。
   - 如果已发送查询，客户端仍会向服务器发送状况消息响应。  



## <a name="how-to-use-cmpivot"></a>如何使用 CMPivot

![CMPivot 窗口示例](media/1358456-cmpivot-sample.png)

CMPivot 窗口包含以下元素：  

1. CMPivot 当前定位的集合位于顶部的标题栏和窗口底部的状态栏中。 例如，上面屏幕截图中的“PM_Team_Machines”。  

2. 左侧窗格列出了客户端上可用的实体。 一些实体依赖于 WMI，而其他实体则使用 PowerShell 从客户端获取数据。   

    - 右键单击实体，执行以下操作：  

       - **插入**：将实体添加到当前游标位置的查询中。 查询不会自动运行。 双击某个实体时，此操作是默认操作。 生成查询时，请使用此操作。  

       - **查询全部**：针对此实体运行查询（包含所有属性）。 使用此操作可快速查询单个实体。  

       - **按设备查询**：针对此实体运行查询并对结果进行分组。 例如 `Disk | summarize dcount( Device ) by Name`  

    - 展开实体以查看每个实体可用的特定属性。 双击某个属性，将其添加到当前游标位置的查询。  

3. “主页”选项卡显示有关 CMPivot 的常规信息，包括示例查询和支持文档的链接。  

4. “查询”选项卡显示查询窗格、结果窗格和状态栏。 在上面的屏幕截图示例中选中了“查询”选项卡。  

5. 通过查询窗格，可以在集合中生成或键入要在客户端上运行的查询。  

    - CMPivot 使用 [Kusto 查询语言 (KQL)](/azure/kusto/query/) 子集。  

    - 在查询窗格中剪切、复制或粘贴内容。  
    <!-- markdownlint-disable MD038 -->
    - 默认情况下，此窗格使用 IntelliSense。 例如，如果开始键入 `D`，IntelliSense 会建议以该字母开头的所有实体。 选择一个选项，然后按 Tab 将其插入。 键入一个管道字符和一个空格 `| `，然后 IntelliSense 便会建议所有表运算符。 插入 `summarize` 并键入空格，IntelliSense 会建议所有聚合函数。 有关这些运算符和函数的详细信息，请单击 CMPivot 中的“主页”选项卡。  

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
         - 自版本 2006 起，“透视到”已替换为“设备透视”。 有关详细信息，请参阅[版本 2006 的 CMPivot 更改](cmpivot-changes.md#bkmk_2006)。

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

安全管理员要求尽快对会计部门的所有设备停止并禁用计算机浏览器服务。 可对会计部门中所有设备的集合启动 CMPivot，并在“Service”实体上选择“查询全部” 。 

`Service`

显示结果时，右键单击“Name”列，然后选择“分组依据” 。 

`Service | summarize dcount( Device ) by Name`

在“浏览器”服务的行中，单击“dcount_”列中的超链接数字 。 

`Service | where (Name == 'Browser') | summarize count() by Device`

可以选择多个设备，右键单击所选设备，然后选择“运行脚本”。 此操作将启动“运行脚本”向导，你可以通过该向导运行用于停止和禁用服务的现有脚本。 借助 CMPivot，可以快速响应所有活动计算机的安全事件，并在“运行脚本”向导中查看结果。 然后继续创建配置基线，以修复集合中的其他计算机，因为它们将来会变为活动状态。 

![浏览器服务和“运行脚本”操作的 CMPivot 示例](media/cmpivot-example1.png)


### <a name="example-2-proactively-resolve-application-failures"></a>示例 2：主动解决应用程序故障  

为主动进行操作维护，可每周一次对管理的服务器集合运行 CMPivot，并在“AppCrash”实体上选择“查询所有” 。 右键单击“FileName”列，然后选择“升序排序” 。 一台设备会为 sqlsqm.exe 返回七个结果，时间戳大约为每天 03:00。 你可以在其中一行中选择文件名，右键单击该名称，然后选择“使用必应进行搜索”。 在 Web 浏览器中浏览搜索结果时，可找到有关此问题的 Microsoft 支持文章，其中会包含详细信息和解决方案。 


### <a name="example-3-bios-version"></a>示例 3：BIOS 版本

若要[缓解推测执行端通道漏洞](https://techcommunity.microsoft.com/t5/configuration-manager-blog/additional-guidance-to-mitigate-speculative-execution-side/ba-p/274974)，其中一个要求就是更新系统 BIOS。 首先查询 BIOS 实体。 然后按“Version”属性进行分组 。 再右键单击某个特定值，例如“LENOVO - 1140”，并选择“显示具备以下条件的设备”。  

`Bios | summarize countif( (Version == 'LENOVO - 1140') ) by Device | where (countif_ > 0)`


### <a name="example-4-free-disk-space"></a>示例 4：可用磁盘空间

需要在网络文件服务器上临时存储大型文件，但不确定哪个磁盘拥有足够的容量。 对文件服务器集合启动 CMPivot，并查询“Disk”实体。 修改 CMPivot 的查询以快速返回包含实时存储数据的活动服务器列表：  

`Disk | where (Description == 'Local Fixed Disk') | where isnotnull( FreeSpace ) | order by FreeSpace asc`


## <a name="cmpivot-standalone"></a><a name="bkmk_standalone"></a> CMPivot 独立应用

[!INCLUDE [CMPivot standalone](includes/cmpivot-standalone.md)]


 
## <a name="inside-cmpivot"></a>深入了解 CMPivot

CMPivot 使用 Configuration Manager“快速通道”向客户端发送查询。 其他功能也使用这个从服务器到客户端的信道，例如客户端通知操作、客户端状态和 Endpoint Protection。 客户端通过类似的快速状况消息系统返回结果。 状况消息临时存储在数据库中。 如需深入了解用于客户端通知的端口，请参阅[端口](../../plan-design/hierarchy/ports.md#BKMK_PortsClient-MP)一文。

查询和结果都只是文本。 InstallSoftware 和 Process 实体均返回一些最大的结果集 。 性能测试期间，对于这些查询而言，来自一个客户端的最大状态消息文件大小小于 1 KB。 扩展到包含 50,000 个活动客户端的大型环境后，此一次性查询将在网络上生成不超过 50 MB 的数据。 欢迎页上所有带下划线的项，每个客户端将返回不超过 1k 的信息。

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

- [对 CMPivot 的更改](cmpivot-changes.md)
- [CMPivot 疑难解答](cmpivot-tsg.md)
- [创建并运行 PowerShell 脚本](../../../apps/deploy-use/create-deploy-scripts.md)