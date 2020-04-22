---
title: 日志收集器
titleSuffix: Configuration Manager
description: 使用日志收集器工具来帮助对桌面分析进行故障排除
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 349b2a69-af46-481f-afb2-24d98774e852
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c101e45eb794ff73599e9612a5aec991be01ae6c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701715"
---
# <a name="desktop-analytics-log-collector"></a>桌面分析日志收集器

自 Configuration Manager 版本 1906 起，可使用 Configuration Manager 安装目录中的“DesktopAnalyticsLogsCollector.ps1”  工具来帮助对桌面分析设备注册问题进行故障排除。 它会运行一些基本故障排除步骤，并将相关日志收集到单个工作目录中。 你可以与 Microsoft 支持部门共享此内容。


## <a name="prerequisites"></a>必备条件

- 运行 Windows 10、Windows 8.1 或 Windows 7（带 Service Pack 1）的桌面分析客户端

- 以管理用户身份在设备上运行脚本，并“以管理员身份运行”  。

    > [!Tip]
    > 您可以借助此工具使用 Configuration Manager“脚本”  功能。 有关详细信息，请参阅[示例 5：通过 Configuration Manager“脚本”  ](#bkmk_ex5)部署脚本。

- 对于 Windows 7（带 Service Pack 1），PowerShell 版本 4.0 或更高版本
    - [.NET Framework 版本 4.6 或更高版本](https://dotnet.microsoft.com/download/dotnet-framework)

    - Windows Management Framework [版本 4.0](https://support.microsoft.com/help/2819745) (aka.ms/wmf4download) 或[版本 5.1](https://www.microsoft.com/download/details.aspx?id=54616) (aka.ms/wmf5download)

## <a name="usage"></a>用法

从 Configuration Manager 安装内容获取脚本： `SMSSETUP\TOOLS\DesktopAnalyticsLogsCollector\DesktopAnalyticsLogsCollector.ps1`

``` Syntax
DesktopAnalyticsLogsCollector.ps1
    [-LogPath] <String>
    [-LogMode] <Int16>
    [-CollectNetTrace] <Int16>
    [-CollectUTCTrace] <Int16>
```

## <a name="parameters"></a>参数

### `-LogPath`

指定一个本地或 UNC 路径以放置日志和其他输出文件。

**值**：

- 本地路径（最大长度 = 130），例如：`c:\myfolder`

- UNC 路径（最大长度 = 130），例如：`\\myserver\myfolder`

**类型**：字符串

**位置**：1

**默认值**：`$Env:SystemDrive\M365AnalyticsLogs`（当此参数为 Null、空或空格时，该脚本将在系统驱动器下创建“M365AnalyticsLogs”文件夹。）

### `-LogMode`

指定日志的详细级别。

**值**：

- `0`：仅将脚本消息记录到 PowerShell 命令窗口。

- `1`：在输出文件夹和 PowerShell 命令窗口下，将脚本消息记录到两个日志文件。

- `2`：仅将脚本消息记录到输出文件夹下的日志文件。

**类型**：Int16

**位置**：2

**默认值**：`1`（将脚本消息记录到日志文件和 PowerShell 命令窗口。）

### `-CollectNetTrace`

指定脚本是否收集网络跟踪。

**值**：

- `0`：不要启用网络跟踪。

- `1`（任何非零整数值）：启用网络跟踪并收集结果。

**类型**：Int16

**位置**：3

**默认值**：`0`（不要启用网络跟踪）

### `-CollectUTCTrace`

指定脚本是否收集 Windows UTC 跟踪和运行连接诊断。

**值**：

- `0`：不要启用 UTC 跟踪或运行连接诊断。

- `1`（任何非零整数值）：启用 UTC 跟踪，运行连接诊断，并收集结果。

**类型**：Int16

**位置**：4

**默认值**：`0`（不要启用 UTC 跟踪或运行连接诊断）


## <a name="output"></a>输出

此脚本在指定的路径下创建一个“工作文件夹”  。 例如，“M365AnalyticsLogs_yy_MM_dd_HH_mm_ss”  。 它将其所有输出文件放入此工作文件夹中。

如果要让脚本能够写入“日志文件”  ，它将在工作文件夹中生成一个日志文件。 例如，“M365AnalyticsLogs_ yy_MM_dd_HH_mm_ss.txt”  。

该脚本还会在工作文件夹中生成其他“诊断文件”  。 例如：

- `installedKBs.txt`：安装在设备上的 Windows 更新列表
- `appcompat`：应用程序兼容性数据
- `Reg*.txt`：一系列文件，其中包含从 Windows 注册表导出的数据


## <a name="examples"></a>示例

### <a name="example-1-run-script-via-powershell-command-window-with-default-values"></a><a name="bkmk_ex1"></a> 示例 1：通过具有默认值的 PowerShell 命令窗口运行脚本

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1
```

### <a name="example-2-run-script-via-powershell-command-window-with-specified-parameters"></a><a name="bkmk_ex2"></a> 示例 2：通过具有指定参数的 PowerShell 命令窗口运行脚本

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 -LogPath "c:\testABC" -LogMode 0 -CollectNetTrace 0 -CollectUTCTrace 0
```

### <a name="example-3-run-script-via-powershell-command-window-with-specified-parameters-in-position"></a><a name="bkmk_ex3"></a> 示例 3：通过在适当位置具有指定参数的 PowerShell 命令窗口运行脚本

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 "c:\testABC" 2 0 0
```

### <a name="example-4-run-script-via-powershell-command-window-with-specified-parameter-and-verbose-messages"></a><a name="bkmk_ex4"></a> 示例 4：通过具有指定参数和详细消息的 PowerShell 命令窗口运行脚本

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 -LogMode 1 -Verbose
```

### <a name="example-5-deploy-script-via-configuration-manager-scripts"></a><a name="bkmk_ex5"></a> 示例 5：通过 Configuration Manager“脚本”  部署脚本

有关详细信息，请参阅[从 Configuration Manager 控制台创建并运行 PowerShell 脚本](../apps/deploy-use/create-deploy-scripts.md)。

DesktopAnalyticsLogsCollector.ps1 由 Microsoft 进行数字签名。 可能需要将其 Microsoft 代码签名证书作为受信任的发布者添加到目标设备上。

1. 在 Windows 资源管理器中打开该脚本的属性。 切换到“数字签名”  选项卡，然后选择“详细信息”  。

2. 在“常规”  选项卡上，选择“查看证书”  。

    > [!Note]
    > 若要通过其他机制分发证书，请首先将证书导出到文件。 转到“详细信息”  选项卡，然后选择“复制到文件”  。

3. 选择“安装证书”  。 导入此证书，将其置于“受信任的发布者”  商店。


## <a name="see-also"></a>另请参阅

- [桌面分析疑难解答](troubleshooting.md)

- [从 Configuration Manager 控制台创建并运行 PowerShell 脚本](../apps/deploy-use/create-deploy-scripts.md)
