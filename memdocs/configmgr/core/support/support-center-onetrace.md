---
title: 支持中心 OneTrace（预览）
titleSuffix: Configuration Manager
description: OneTrace 是一个带有支持中心的新日志查看器，它在 CMTrace 的基础上进行了改进。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4cde43d1-9b09-4601-b389-0776de451b4e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 150090556d63b1bdf0b35dc9b53b450137d7f9d3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707445"
---
# <a name="support-center-onetrace-preview"></a>支持中心 OneTrace（预览）

<!--3555962-->

从版本 1906 开始，OneTrace 是一个带有支持中心的新日志查看器。 它的工作方式与 CMTrace 类似，同时具有以下改进：

- 选项卡式视图
- 可停靠窗口
- 改进了搜索功能
- 无需离开日志视图，即可启用筛选器
- 可以快速识别错误群集的滚动条提示
- 可快速打开大型文件的日志

[![OneTrace 日志查看器的屏幕截图](media/3555962-onetrace.png)](media/3555962-onetrace.png#lightbox)

OneTrace 适用于许多类型的日志文件，如：

- Configuration Manager 客户端日志
- Configuration Manager 服务器日志
- 状态消息
- Windows 10 上的 Windows 更新 ETW 日志文件
- Windows 7 和 Windows 8.1 上的 Windows 更新日志文件

## <a name="prerequisites"></a>必备条件

- .NET Framework 版本 4.6 或更高版本

## <a name="install"></a>安装

OneTrace 与支持中心一起安装。 通过以下路径在站点服务器上找到支持中心安装程序：`cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi`。

默认情况下，OneTrace 应用程序安装在 `C:\Program Files (x86)\Configuration Manager Support Center\CMPowerLogViewer.exe` 中。

> [!Note]  
> 支持中心和 OneTrace 使用 Windows Presentation Foundation (WPF)。 此组件在 Windows PE 中不可用。 继续在具有任务序列部署的启动映像中使用 CMTrace。  

## <a name="log-groups"></a>日志组

<!--5559993-->

从版本 2002 开始，OneTrace 支持可自定义的日志组，与支持中心的功能类似。 日志组允许打开单个方案的所有日志文件。 OneTrace 当前包括以下方案的组：

- 应用程序管理
- 合规性设置（也称为所需的配置管理）
- 软件更新

若要显示日志组，请转到“视图”菜单，然后选择“日志组”   。

![用于应用程序管理的 OneTrace 日志组的屏幕截图](media/5559993-onetrace-log-groups.png)

### <a name="customize-log-groups"></a>自定义日志组

可以通过修改配置 XML 来自定义这些组，该配置默认为以下路径：`C:\Program Files (x86)\Configuration Manager Support Center\LogGroups.xml`。

下面的示例是默认配置文件的一部分：

``` XML
<LogGroups>
  <LogGroup Name="Desired Configuration Management" GroupType="1" GroupFilePath="">
    <LogFile>CIAgent.log</LogFile>
    <LogFile>CIDownloader.log</LogFile>
    <LogFile>CIStateStore.log</LogFile>
    <LogFile>CIStore.log</LogFile>
    <LogFile>CITaskMgr.log</LogFile>
    <LogFile>ccmsdkprovider.log</LogFile>
    <LogFile>DCMAgent.log</LogFile>
    <LogFile>DCMReporting.log</LogFile>
    <LogFile>DcmWmiProvider.log</LogFile>
  </LogGroup>
</LogGroups>
```

`GroupType` 属性接受以下值：

- `0`：未知或其他
- `1`：Configuration Manager 客户端日志
- `2`：Configuration Manager 服务器日志

`GroupFilePath` 属性可以包含日志文件的显式路径。 如果为空，则 OneTrace 依赖于组类型的注册表配置。 例如，如果你设置 `GroupType=1`，则 OneTrace 默认自动在 `C:\Windows\CCM\Logs` 中查找组的日志。 在此示例中，无需指定 `GroupFilePath`。

## <a name="see-also"></a>另请参阅

- [支持中心日志查看器](support-center-ui-reference.md#bkmk_log-viewer)

- [CMTrace](cmtrace.md)
