---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 07/13/2020
ms.openlocfilehash: 80302a1c369c36a08cc1a55e20cf339dbc8d2883
ms.sourcegitcommit: 6d987bb69d0eb9955a3003202864f58d6aaa426a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/14/2020
ms.locfileid: "86381037"
---
<!--This file is shared by the CMPivot overview articles for both Microsoft Endpoint Manager tenant attach and Configuration Manager-->

## <a name="queries"></a>查询

查询可以用于搜索术语、识别趋势、分析模式，以及提供基于数据的许多其他见解。 CMPivot 使用 [Azure Log Analytics](https://docs.microsoft.com/azure/kusto/query) 数据流模型的子集处理表格表达式语句。 表格表达式语句的典型结构是客户端实体和表格数据运算符（如筛选器和投影）的组合。 组合用管道字符 (|) 表示，为语句提供了一种规则形式，从左到右直观显示表格数据流。 每个运算符都“从管道”接受一个表格数据集，从运算符正文接受其他输入（包括其他表格数据集），然后向其后的下一个运算符发出表格数据集，如下所示：`entity | operator1 | operator2 | ...`

在下面的示例中，实体是 `CCMRecentlyUsedApplications`（对最近使用的应用程序的引用），运算符为 where（根据某些因记录而异的谓词，从其输入中筛选出记录）：

```
CCMRecentlyUsedApplications | where CompanyName like '%Microsoft%' | project CompanyName, ExplorerFileName, LastUsedTime, LaunchCount, FolderPath
```

## <a name="entities"></a>实体

实体是可以从客户端查询的对象。 目前支持以下实体：


|实体|说明|
|---|---|
|AadStatus|Azure Active Directory 的状态|
|Administrators|本地管理员组的成员|
|AppCrash|最近的应用程序崩溃报告|
|AppVClientApplication|AppV 客户端应用程序|
|AppVClientPackage|AppV 客户端包|
|AutoStartSoftware|随操作系统自动启动或在操作系统启动后立即启动的软件|
|基板|基板|
|电池|电池|
|BIOS|系统 BIOS 信息|
|BitLocker|BitLocker|
|BitLockerEncryptionDetails|BitLocker Encryption Details|
|BitLockerPolicy|BitLocker 策略|
|BootConfiguration|启动配置|
|BrowserHelperObject|浏览器帮助程序对象|
|BrowserUsage|浏览器使用情况|
|CcmLog()|Ccm 日志文件中 24 小时内生成的行（默认）|
|CCMRAX|CCM_RAX|
|CCMRecentlyUsedApplications|最近使用的应用程序|
|CCMWebAppInstallInfo|Web 应用程序|
|CDROM|CDROM 驱动器|
|ClientEvents|客户端事件|
|ComputerSystem|计算机系统|
|ComputerSystemEx|计算机系统扩展|
|ComputerSystemProduct|计算机系统产品|
|ConnectedDevice|已连接的设备|
|连接|进/出设备的活动 TCP 连接|
|“桌面”|“桌面”|
|DesktopMonitor|桌面监视器|
|设备|设备基本信息|
|磁盘和分区|运行 Windows 的计算机系统上的本地存储设备信息|
|DMA|DMA|
|DMAChannel|DMA 通道|
|DriverVxD|驱动程序 - VxD|
|EmbeddedDeviceInformation|嵌入式设备信息|
|环境|环境|
|EPStatus|计算机上反恶意软件的状态|
|EventLog()|事件日志中 24 小时内生成的事件（默认）|
|File()|关于特定文件的信息|
|FileShare|活动文件共享信息|
|固件|固件|
|IDEController|IDE 控制器|
|InstalledExecutable|已安装可执行文件|
|InstalledSoftware|设备上安装的应用程序|
|IPConfig|获取网络配置，包括可用界面、IP 地址和 DNS 服务器|
|IRQTable|IRQ 表|
|键盘|键盘|
|LoadOrderGroup|加载顺序组|
|LogicalDisk|逻辑磁盘|
|MDMDevDetail|设备信息|
|内存|内存|
|调制解调器|调制解调器|
|母板|母板|
|NetworkAdapter|网络适配器|
|NetworkAdapterConfiguration|网络适配器配置|
|NetworkClient|网络客户端|
|NetworkLoginProfile|网络登录配置文件|
|NTEventlogFile|NT 事件日志文件|
|Office365ProPlusConfigurations|Office 365 专业增强版配置|
|OfficeAddin|Office 外接程序|
|OfficeClientMetric|Office 客户端指标|
|OfficeDeviceSummary|Office 设备摘要|
|OfficeDocumentMetric|Office 文档指标|
|OfficeDocumentSolution|Office 文档解决方案|
|OfficeMacroError|Office 宏错误|
|OfficeProductInfo|Office 产品信息|
|OfficeVbaRuleViolation|Office Vba 规则冲突|
|OfficeVbaSummary|Office VBA 扫描摘要|
|OperatingSystem|操作系统|
|OperatingSystemEx|操作系统扩展|
|OperatingSystemRecoveryConfiguration|操作系统恢复配置|
|OptionalFeature|可选功能|
|操作系统|操作系统基本信息|
|PageFileSetting|页面文件设置|
|ParallelPort|并行端口|
|分区|磁盘分区|
|PCMCIAController|PCMCIA 控制器|
|物理磁盘|物理磁盘|
|PhysicalMemory|物理内存|
|PNPDEVICEDRIVER|PNP 设备驱动程序|
|PointingDevice|指针设备|
|PortableBattery|便携式电池|
|端口|端口|
|PowerCapabilities|电源功能|
|PowerClientOptOutSettings|电源管理排除设置|
|PowerConfigurations|电源配置|
|PowerManagementDaily|每日电源管理数据|
|PowerManagementInsomniaReasons|电源失眠原因|
|PowerManagementMonthly|每月电源管理数据|
|PowerSettings|电源设置|
|PrinterConfiguration|打印机配置|
|PrinterDevice|打印机设备|
|PrintJobs|打印作业|
|过程|操作系统上的进程|
|ProcessModule()|指定进程已加载的模块|
|处理器|处理器|
|ProtectedVolumeInformation|受保护的卷信息|
|协议|协议|
|QuickFixEngineering|快速修补工程|
|SCSIController|SCSI 控制器|
|SerialPortConfiguration|串行端口配置|
|SerialPorts|串行端口|
|ServerFeature|服务器功能|
|服务|运行 Windows 的计算机系统上的服务|
|服务|服务|
|共享|共享|
|SMBConfig|设备的 SMB 配置|
|SMSAdvancedClientPorts|Configuration Manager 客户端端口|
|SMSAdvancedClientSSLConfigurations|Configuration Manager 客户端 SSL 配置|
|SMSAdvancedClientState|Configuration Manager 客户端状态|
|SMSDefaultBrowser|默认浏览器|
|SMSSoftwareTag|软件标记|
|SMSWindows8Application|Windows 应用|
|SMSWindows8ApplicationUserInfo|Windows 应用用户信息|
|SoftwareShortcut|软件快捷方式|
|SoftwareUpdate|软件更新适用但未安装在设备上|
|SoundDevices|声音设备|
|SWLicensingProduct|软件授权产品|
|SWLicensingService|软件授权服务|
|SystemAccount|系统帐户|
|SystemBootData|系统启动数据|
|SystemBootSummary|系统启动摘要|
|SystemConsoleUsage|系统控制台使用情况|
|SystemConsoleUser|系统控制台用户|
|SystemDevices|系统设备|
|SystemDrivers|系统驱动程序|
|SystemEnclosure|系统机箱|
|TapeDrive|磁带驱动器|
|TimeZone|时区|
|TPM|TPM|
|TPMStatus|TPM 状态|
|TSIssuedLicense|TS 颁发的许可证|
|TSLicenseKeyPack|TS 许可证密钥包|
|UninterruptiblePowerSupply|不间断电源|
|USBController|USB 控制器|
|USBDevice|USB 设备|
|用户|与设备建立了活动连接的用户帐户|
|USMFolderRedirectionHealth|文件夹重定向运行状况|
|USMUserProfile|用户配置文件运行状况|
|VideoController|视频控制器|
|VirtualMachine|虚拟机|
|VirtualMachine64|虚拟机 (64)|
|Volume|Volume|
|WindowsUpdate|Windows 更新|
|WindowsUpdateAgentVersion|Windows 更新代理版本|
|WinEvent()|Windows 事件日志中 24 小时内生成的事件（默认）|
|WriteFilterState|写入筛选器状态|

## <a name="table-operators"></a>表运算符

可以使用表运算符来筛选、汇总和转换数据流。 目前支持以下运算符：

|表运算符|说明|
|---|---|
|计数|返回包含记录数的单一记录表|
|distinct|生成一个表，其中包含输入表中所提供列的非重复组合|
|join|通过匹配同一设备的行来合并两个表的行，以便形成新的表|
|order by|按一个或多个列对输入表中的行进行排序|
|project|选择要包括、重命名或删除的列，并插入新计算的列|
|summarize|生成一个表，其中聚合了输入表的内容|
|take|返回指定的行数|
|top|返回按指定列排序的前 N 个记录|
|where|筛选表格以仅显示满足谓词的行子集|

## <a name="scalar-operators"></a>标量运算符

下表对运算符进行了汇总：

|运算符|说明|示例
|---|---|---|
|==|Equal|`1 == 1, 'aBc' == 'AbC'`|
|!=|Not Equal|`1 != 2, 'abc' != 'abcd'`|
|< |Less|`1 < 2, 'abc' < 'DEF'`|
|> |Greater|`2 > 1, 'xyz' > 'XYZ'`|
|<=|Less or Equal|`1 <= 2, 'abc' <= 'abc'`|
|>=|Greater or Equal|`2 >= 1, 'abc' >= 'ABC'`|
|+|添加|`2 + 1, now() + 1d`|
|-|减|`2 - 1, now() - 1h`|
|*|乘|`2 * 2`|
|/|除|`2 / 1`|
|%|取模|`2 % 1`|
|like|左侧 (LHS) 包含右侧 (RHS) 的匹配项|`'abc' like '%B%'`|
|!like|LHS 不包含 RHS 的匹配项|`'abc' !like '_d_'`|
|包含|RHS 以 LHS 子序列的形式存在|`'abc' contains 'b'`|
|!contains|LHS 中未出现 RHS|`'team' !contains 'i'`|
|startswith|RHS 是 LHS 的初始子序列|`'team' startswith 'tea'`|
|!startswith|RHS 不是 LHS 的初始子序列|`'abc' !startswith 'bc'`|
|endswith|RHS 是 LHS 的闭合子序列|`'abc' endswith 'bc'`|
|!endswith|RHS 不是 LHS 的闭合子序列|`'abc' !endswith 'a'`|
|以及|当且仅当 RHS 和 LHS 均为 true 时返回 true|`(1 == 1) and (2 == 2)`|
|或|当且仅当 RHS 或 LHS 为 true 时返回 true|`(1 == 1) or (1 == 2)`|

## <a name="aggregation-functions"></a>聚合函数

聚合函数可与表运算符结合使用以计算汇总值。 目前支持以下聚合函数：

|函数|说明|
|---|---|
|avg()|返回组中所有值的平均值|
|count()|返回每个摘要组的记录计数|
|countif()|返回谓词计算结果为 true 的行数|
|dcount()|返回组中非重复值的数目|
|max()|返回组内的最大值|
|min()|返回组内的最小值|
|percentile()|针对由 Expr 定义的填充，返回其中指定的最接近排名百分位数的估计值|
|sum()|返回组中所有值的和|
|sumif()|返回谓词计算结果为 True 的 Expr 总和|

## <a name="scalar-functions"></a>标量函数

可以在表达式中使用标量函数。 目前支持以下标量函数：

|函数|说明|
|---|---|
|ago()|从当前的 UTC 时钟时间减去给定的时间跨度|
|bin()|将值舍入为给定装箱大小倍数的一个日期时间数字|
|case()|计算谓词的列表，并返回满足其谓词的第一个结果表达式|
|datetime_add()|计算新的日期时间，方法是将指定日期部分与指定数量相乘，然后加上指定日期时间|
|datetime_diff()|计算两个日期时间值之间的差值|
|iif()|计算第一个参数，并根据谓词计算结果为 True（第二个）还是 False（第三个），返回第二个或第三个参数的值|
|indexof()|该函数报告输入字符串中指定字符串第一次出现时从零开始的索引|
|isnotnull()|计算其唯一参数并返回一个布尔值，指示该参数的计算结果是否为非 null 值|
|isnull()|计算其唯一参数并返回一个布尔值，指示该参数的计算结果是否为 null 值|
|now()|返回当前 UTC 时钟时间|
|strcat()|连接 1 个到 64 个自变量|
|strlen()|返回输入字符串的长度（以字符为单位）|
|substring()|从源字符串中提取从某个索引开始到字符串结尾的 substring|
|tostring()|将输入转换为字符串表示形式|

## <a name="additional-entities-operators-and-functions-for-cmpivot-from-configuration-manager"></a><a name="bkmk_onprem_only"></a> Configuration Manager 中 CMPivot 的其他实体、运算符和函数

> [!Important]
> 从 Microsoft Endpoint Manager 管理中心运行 CMPivot 时，不支持这些项。

|类型|项目|说明|
|--|--|---|
|实体|AccountSID|帐户 SID|
|实体|FileContent()|特定文件的内容|
|实体|NAPClient|NAP 客户端|
|实体|NAPSystemHealthAgent|NAP系统健康代理|
|实体|Registry()|特定注册表项的所有值<!--7371183-->|
|表运算符|呈现|将结果呈现为图形输出|
