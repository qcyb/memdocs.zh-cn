---
title: 对 CMPivot 的更改
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 版本之间对 CMPivot 所做的更改。
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: a49a9564-0863-44c3-991e-a8e271fed586
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 20b23cec74ae3d201bc81fe1834e87e7eb8fcc13
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129504"
---
# <a name="changes-to-cmpivot"></a>对 CMPivot 的更改

请参阅以下信息来了解 Configuration Manager 版本之间对 [CMPivot](cmpivot.md) 所做的更改：

## <a name="cmpivot-changes-for-version-2006"></a><a name="bkmk_2006"></a> 版本 2006 的 CMPivot 更改
<!--6518631-->

自版本 2006 起，对 CMPivot 进行了以下改进：

- 聚合了 [CMPivot 独立应用](cmpivot.md#bkmk_standalone)和从管理控制台启动的 CMPivot。 从管理控制台启动 CMPivot 时，它使用与 CMPivot 独立版相同的基础技术来进行场景奇偶校验。

- 改进了 CMPivot 中的键盘导航。

- 可以在“设备”节点中的单台或多台设备中运行 CMPivot，而不必选择设备集合。 此项改进使用户（例如作为支持人员角色的人员）可以在预先创建的集合之外为特定设备轻松创建 CMPivot 查询。
   - 选择设备集合中的单台或多台设备，然后选择“启动 CMPivot”。

- 在查询列表视图中返回设备后，可以在单台或多台设备上选择“设备透视”，然后只对这些设备进行透视和查询，以便进一步钻取。 此更改允许你进行钻取，而无需查询原始集合中的更大设备集。 “透视到”已替换为“设备透视”。
   - 在现有的 CMPivot 操作中，从输出中选择单台或多台设备。 右键单击，然后使用“设备透视”选项进行透视。 此操作启动限定为只包含你所选设备的单独 CMPivot 实例。 这样就可以更轻松地对所需设备进行透视和查询，而无需为它们创建集合。

- 当你为单台设备运行 CMPivot 时，设备名会列在窗口顶部。 对于多台设备，所选设备的数量会列在窗口顶部。
- 删除了“查询摘要”选项卡中的“创建集合”选项，因为 CMPivot 不再需要对集合进行查询。 执行“设备透视”，以打开限定为只包含你要执行查询的设备的新 CMPivot 实例。 主菜单上仍有“创建集合”。

![使用 CMPivot 对多台设备进行设备透视](./media/6518631-cmpivot-multi-select.png)


## <a name="cmpivot-changes-for-version-2002"></a><a name="bkmk_2002"></a> 版本 2002 的 CMPivot 更改
<!--5870934-->
我们简化了 CMPivot 实体的导航。 从 Configuration Manager 版本 2002 开始，可以搜索 CMPivot 实体。 还添加了新图标，以轻松地区分实体和实体对象类型。

![搜索 CMPivot 实体](./media/5870934-search-cmpivot-entities.png)


## <a name="cmpivot-changes-for-version-1910"></a><a name="bkmk_cmpivot1910"></a> 版本 1910 的 CMPivot 更改
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
在 Configuration Manager 控制台外使用 CMPivot 时，可以仅查询本地设备，而无需 Configuration Manager 基础结构。 现在可以利用 CMPivot Azure Log Analytics 查询快速查看本地设备上的 WMI 信息。 还可以在较大的环境中运行 CMPivot 查询之前对其进行验证和优化。 CMPivot 独立应用仅提供英语版本。 若要详细了解 CMPivot 独立应用，请参阅 [CMPivot 独立应用](#bkmk_standalone)。

#### <a name="known-issues-for-local-device-query-evaluation"></a>本地设备查询评估的已知问题

 - 如果在“此电脑”上查询你无权访问的 WMI 实体（例如锁定的 WMI 类），则可能会在 CMPivot 中出现故障。 使用具有提升权限的帐户运行 CMPivot 以查询这些实体。 <!--5753242-->
- 如果在“此电脑”上查询非 WMI 实体，你将看到“无效的命名空间”或不明确的异常 。
- 从“开始”菜单快捷方式运行 CMPivot 独立应用，而不是直接从可执行文件的路径运行。 <!--5787962-->

### <a name="other-enhancements"></a><a name="bkmk_Other"></a> 其他增强功能

- 可以使用新的 `like` 运算符执行正则表达式类型查询。 例如：<!--3056858-->
  
   ```kusto
   //Find BIOS manufacture that contains any word like Micro, such as Microsoft
   Bios
   | where Manufacturer like '%Micro%'
   ```

- 我们已将 CcmLog() 和 EventLog() 实体更新为在默认情况下仅查看最近 24 小时内的消息 。 通过传入可选的时间跨度可以覆盖此行为。 例如，以下查询将查看最近 1 小时内的事件：

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

- 从“导出”菜单中，选择新选项“查询链接到剪贴板” 。<!-- 5431577 --> 此操作会将链接复制到剪贴板，以便与他人共享。 例如：

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
    > 要使此链接正常工作，请[安装 CMPivot 独立版本](#bkmk_standalone)。

- 在查询结果中，如果设备已在 Microsoft Defender 高级威胁防护 (ATP) 中注册，请右键单击该设备以启动 Microsoft Defender 安全中心在线门户。

### <a name="known-issues-for-cmpivot-in-version-1910"></a>版本 1910 中 CMPivot 的已知问题

- 当达到限制时，不显示最大结果横幅。 <!--5431427-->
  - 每个客户端每次查询的数据大小限制为 128 KB。
  - 如果查询的结果超过 128 KB，可能会截断结果。

## <a name="cmpivot-changes-for-version-1906"></a><a name="bkmk_cmpivot1906"></a> 版本 1906 的 CMPivot 更改

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

CMPivot 中已存在呈现运算符。 已添加对多序列和“with”语句的支持。 有关详细信息，请参阅[示例](#bkmk_cmpivot_examples1906)部分和 Kusto 的[联接运算符](https://docs.microsoft.com/azure/kusto/query/joinoperator)一文。

#### <a name="limitations-for-joins"></a>联接的限制

1. 联接列始终在“Device”字段上隐式完成。
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

从版本 1906 开始，已向 Configuration Manager 的内置安全管理员角色添加以下权限：

 - 读取 SMS 脚本
 - 在集合上运行 CMPivot
 - 读取清单报表

>[!NOTE]
> “运行脚本”是“运行 CMPivot”权限的超集。

### <a name="cmpivot-standalone"></a><a name="bkmk_standalone"></a> CMPivot 独立应用

[!INCLUDE [CMPivot standalone](includes/cmpivot-standalone.md)] 

## <a name="cmpivot-changes-for-version-1902"></a><a name="bkmk_cmpivot1902"></a> 版本 1902 的 CMPivot 更改
<!--3610960-->
从 Configuration Manager 版本 1902 开始，可以在层次结构中从管理中心站点 (CAS) 运行 CMPivot。 主站点仍可处理与客户端的通信。 从管理中心站点运行 CMPivot 时，它将通过高速消息订阅通道与主站点通信。 该通信不依赖于站点之间的标准 SQL 复制。

当 SQL 或提供程序不在同一台计算机上时，或在 SQL Always On 配置的情况下，在 CAS 上运行 CMPivot 将需要其他权限。 使用这些远程配置，即可为 CMPivot 配置“双跃点方案”。

若要在这种“双跃点方案”中让 CMPivot 使用 CAS，可以定义约束委派。 若要了解此配置的安全隐患，请阅读 [Kerberos 约束委派](https://docs.microsoft.com/windows-server/security/kerberos/kerberos-constrained-delegation-overview)一文。 Kerberos 需要使用计算机之间的所有跃点。<!--5746133--> 如果正在使用或未使用 CAS 并置多个远程配置（例如 SQL 或 SMS 提供程序），或有多个受信任林，则可能需要权限设置组合。 下面是你可能需要遵循的步骤：

### <a name="cas-has-a-remote-sql-server"></a>CAS 具有远程 SQL Server

1. 请转到每个主站点的 SQL Server。
   1. 将 CAS 远程 SQL Server 和 CAS 站点服务器添加到 [Configmgr_DviewAccess](../../plan-design/hierarchy/accounts.md#configmgr_dviewaccess) 组。
   ![主站点 SQL Server 上的 Configmgr_DviewAccess 组](media/cmpivot-dviewaccess-group.png)
1. 转到 Active Directory 用户和计算机。
   1. 对于每个主站点服务器，请右键单击并选择“属性”。
      1. 在委托选项卡上，选择第三个选项，“仅信任此计算机委派指定的服务”。 
      1. 选择“仅使用 Kerberos”。
      1. 使用端口和实例添加 CAS SQL Server 服务。
      1. 请确保这些更改与公司安全策略保持一致！
   1. 对于 CAS 站点，请右键单击并选择“属性”。
      1. 在委托选项卡上，选择第三个选项，“仅信任此计算机委派指定的服务”。 
      1. 选择“仅使用 Kerberos”。
      1. 使用端口和实例添加每个主站点的 SQL Server 服务。
      1. 请确保这些更改与公司安全策略保持一致！

   ![双跃点的 CMPivot AD 委派示例](media/cmpivot-ad-delegation.png)

### <a name="cas-has-a-remote-provider"></a>CAS 具有远程提供程序

1. 请转到每个主站点的 SQL Server。
   1. 将 CAS 提供程序计算机帐户和 CAS 站点服务器添加到 [Configmgr_DviewAccess](../../plan-design/hierarchy/accounts.md#configmgr_dviewaccess) 组。
1. 转到 Active Directory 用户和计算机。
   1. 选择 CAS 提供程序计算机，右键单击并选择“属性”。
      1. 在委托选项卡上，选择第三个选项，“仅信任此计算机委派指定的服务”。 
      1. 选择“仅使用 Kerberos”。
      1. 使用端口和实例添加每个主站点的 SQL Server 服务。
      1. 请确保这些更改与公司安全策略保持一致！
   1. 选择 CAS 站点服务器，右键单击并选择“属性”。
      1. 在委托选项卡上，选择第三个选项，“仅信任此计算机委派指定的服务”。 
      1. 选择“仅使用 Kerberos”。
      1. 使用端口和实例添加每个主站点的 SQL Server 服务。
      1. 请确保这些更改与公司安全策略保持一致！
1. 重启 CAS 远程提供程序计算机。

### <a name="sql-always-on"></a>SQL Always On

1. 请转到每个主站点的 SQL Server。
   1. 将 CAS 站点服务器添加到 [Configmgr_DviewAccess](../../plan-design/hierarchy/accounts.md#configmgr_dviewaccess) 组。
1. 转到 Active Directory 用户和计算机。
   1. 对于每个主站点服务器，请右键单击并选择“属性”。
      1. 在委托选项卡上，选择第三个选项，“仅信任此计算机委派指定的服务”。 
      1. 选择“仅使用 Kerberos”。
      1. 使用端口和实例为 SQL 节点添加 CAS SQL Server 服务帐户。
      1. 请确保这些更改与公司安全策略保持一致！
   1. 选择 CAS 站点服务器，右键单击并选择“属性”。
      1. 在委托选项卡上，选择第三个选项，“仅信任此计算机委派指定的服务”。 
      1. 选择“仅使用 Kerberos”。
      1. 使用端口和实例添加每个主站点的 SQL Server 服务。
      1. 请确保这些更改与公司安全策略保持一致！
1. 请确保 [SPN 发布](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/listeners-client-connectivity-application-failover?view=sql-server-2017#SPNs)使用 CAS SQL 侦听器名称和每个主 SQL 侦听器名称。
1. 重启主 SQL Server。
1. 重启 CAS 站点服务器和 CAS SQL Server。


## <a name="cmpivot-changes-for-version-1810"></a><a name="bkmk_cmpivot"></a> 版本 1810 的 CMPivot 更改
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
- 在“查询摘要”选项卡上，选择“故障”或“脱机”设备的计数，然后选择“创建集合”选项。 使用此选项，可通过修正部署轻松定位这些设备。
   - 版本 2006 删除了此选项，因为 CMPivot 不再需要对集合进行查询。
- 通过单击文件夹图标保存收藏夹查询。
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
要呈现时间图，请使用新的 bin() 运算符对某段时间的事件进行分组。 以下查询显示过去七天内设备启动的时间：

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

选择 CMPivot 窗口底部的“查询摘要”选项卡。 此状态可帮助你识别离线的客户端，或排查可能发生的故障。 在“计数”列中选择一个值以打开具有该状态的特定设备的列表。 

例如，选择状态为“故障”的设备的计数。 请查看特定的错误消息，并导出这些设备列表。 如果错误是无法识别的特定 cmdlet，请使用导出的设备列表创建集合以部署 Windows PowerShell 更新。  

### <a name="cmpivot-audit-status-messages"></a>CMPivot 审核状态消息

从版本 1810 开始，运行 CMPivot 时，MessageID 40805 会创建审核状态消息。 可通过转到“监视” > “系统状态” > “状态消息查询”  查看状态消息。 可为指定用户运行所有审核状态消息，为指定站点运行所有审核状态消息，或创建自己的状态消息查询 。

消息使用以下格式：

MessageId 40805:User &lt;UserName> ran script &lt;Script-Guid> with hash &lt;Script-Hash> on collection &lt;Collection-ID>。

- 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 是 CMPivot 的 Script-Guid。
- 可以在客户端的 scripts.log 文件中查看 Script-Hash。
- 也可以查看存储在客户端脚本存储中的哈希。 客户端上的文件名为 &lt;Script-Guid>_&lt;Script-Hash>。
    - 示例文件名：C:\Windows\CCM\ScriptStore\7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14_abc1d23e45678901fabc123d456ce789fa1b2cd3e456789123fab4c56789d0123.ps
   

![CMPivot 审核状态消息示例](media/cmpivot-audit-status-message.png)

## <a name="next-steps"></a>后续步骤
 
[CMPivot 疑难解答](cmpivot-tsg.md)
