---
title: 服务连接工具
titleSuffix: Configuration Manager
description: 了解该工具使你能够连接到 Configuration Manager 云服务以手动上传使用情况信息。
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
ms.assetid: 6e4964c5-43cb-4372-9a89-b62ae6a4775c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8b56b849be6abd2634e29d35e58494d4d3215857
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126080"
---
# <a name="use-the-service-connection-tool-for-configuration-manager"></a>使用适用于 Configuration Manager 的服务连接工具

适用范围：Configuration Manager (Current Branch)

当服务连接点处于脱机模式时，请使用服务连接工具。 当 Configuration Manager 站点系统服务器未连接到 Internet 时，也可以使用此工具。 该工具有助于随时更新网站的 Configuration Manager 最新更新。

运行此工具时，该工具会连接到 Configuration Manager 云服务，以上传层次结构的使用情况信息并下载更新。 必须上传使用情况数据才能启用云服务，进而为你的环境提供正确的更新。

## <a name="prerequisites"></a>必备条件

- 站点有一个服务连接点，并将其配置为“脱机按需连接”。

- 以管理员身份从命令提示符处运行该工具。 没有用户界面。

- 从服务连接点和可以连接到 Internet 的计算机运行该工具。 其中的每台计算机都需要具有 x64 位操作系统，并且具有以下组件：

  - **Visual C++ Redistributable** x86 和 x64 文件。 默认情况下，Configuration Manager 在托管服务连接点的计算机上安装 x64 版本。 要下载此组件，请参阅[用于 Visual Studio 2013 的 Visual C++ 可再发行组件包](https://www.microsoft.com/download/details.aspx?id=40784)。

  - .NET Framework 4.5.2 或更高版本

- 用于运行此工具的帐户需要具有以下权限：

  - 在托管服务连接点的计算机上为“本地管理员”

  - 具有对站点数据库的读取权限

- 需要通过某种方式在具有 Internet 访问权限的计算机与服务连接点之间传输文件。 例如，有足够的可用空间来存储文件和更新的 U 盘。

## <a name="overview"></a>概述

1. **准备**：在服务连接点上运行该工具。 它会将使用情况数据放入指定位置内的 .cab 文件中。 将数据文件复制到具有 Internet 连接的计算机。

2. **连接**：在具有 Internet 连接的计算机上运行此工具。 它会上传使用情况数据，然后下载 Configuration Manager 更新。 将已下载的更新复制到服务连接点。

    可以一次上传多个数据文件，每个数据文件可来自不同的层次结构。 还可以指定代理服务器以及代理服务器的用户。

3. **导入**：在服务连接点上运行该工具。 它会导入更新，然后将更新添加到站点。 随后可以从 Configuration Manager 控制台查看并[安装这些更新](install-in-console-updates.md)。

### <a name="upload-multiple-data-files"></a>上传多个数据文件

- 将从独立的层次结构中导出的所有数据文件放在同一文件夹中。 为每个文件指定一个唯一名称。 如有必要，可以手动重命名它们。

- 运行此工具来将数据上传到 Microsoft 时，指定包含数据文件的文件夹。

- 运行该工具来导入数据时，该工具将仅导入该层次结构的数据。

### <a name="specify-a-proxy-server"></a>指定代理服务器

如果具有 Internet 连接的计算机需要代理服务器，则该工具支持基本的代理配置。 使用可选参数 -proxyserveruri 和 -proxyusername。  有关详细信息，请参阅[命令行参数](#bkmk_cmd)。

### <a name="specify-the-type-of-updates-to-download"></a>指定要下载的更新的类型

该工具支持用于控制下载的文件的选项。 默认情况下，工具仅下载对站点版本适用的最新可用更新。 此工具不会下载修补程序。

要修改此行为，请使用以下参数之一更改下载哪些文件：

- -downloadall：无论站点是哪种版本，均下载所有更新，包括更新和修补程序。
- -downloadhotfix：无论站点是哪种版本，均下载所有修补程序。
- -downloadsiteversion：下载版本高于站点版本的更新和修补程序。

    > [!IMPORTANT]
    > 由于 Configuration Manager 版本 2002 中的已知问题，默认行为不会按预期方式工作。 更新到版本 2006，或使用 -downloadsiteversion 参数下载版本 2002 所需的更新。<!-- 7594517 -->

有关详细信息，请参阅[命令行参数](#bkmk_cmd)。

> [!TIP]
> 该工具通过数据文件确定站点的版本。 若要验证版本，请在 .cab 文件中查找以站点版本命名的文本文件。

## <a name="use-the-tool"></a>使用此工具  

服务连接工具位于 Configuration Manager 安装介质的以下路径中：`SMSSETUP\TOOLS\ServiceConnectionTool\ServiceConnectionTool.exe`。 始终使用与所用的 Configuration Manager 版本匹配的服务连接工具。 其中的所有文件必须位于同一个文件夹中，这样服务连接工具才能工作。

将 ServiceConnectionTool 文件夹及其所有内容复制到具有 Internet 连接的计算机。

在此过程中，命令行示例使用了以下文件名和文件夹位置。 你无需使用这些路径和文件名。 可以使用与你的环境和首选项匹配的替代项。

- 服务连接点上的 Configuration Manager 安装媒介源文件的路径：`C:\Source`

- 用于存储要在计算机之间传输的数据的 U 盘的路径：`D:\USB\`

- 从站点导出的数据文件的名称：`UsageData.cab`

- 该工具将 Configuration Manager 的已下载更新存储到的空文件夹的名称：`UpdatePacks`

### <a name="prepare"></a>准备

1. 在托管服务连接点的计算机上，以管理员身份打开命令提示符，并将目录更改为此工具的位置。 例如：

    `cd C:\Source\SMSSETUP\TOOLS\ServiceConnectionTool\`

1. 运行以下命令来准备数据文件：

    `ServiceConnectionTool.exe -prepare -usagedatadest D:\USB\UsageData.cab`

    > [!NOTE]
    > 如果将同时从多个层次结构上传数据文件，请为每个数据文件指定一个唯一名称。 如有必要，稍后可以重命名文件。

    文件中的数据基于为站点配置的诊断和使用情况数据的级别。 有关详细信息，请参阅[诊断和使用情况数据概述](../../plan-design/diagnostics/diagnostics-and-usage-data.md)。 可以使用该工具将数据导出到 CSV 文件，来查看内容。 有关详细信息，请参阅 [-export](#-export)。

1. 该工具完成导出使用情况数据后，将数据文件复制到有权访问 Internet 的计算机。

### <a name="connect"></a>连接

1. 在具有 Internet 访问权限的计算机上，以管理员身份打开命令提示符，并将目录更改为此工具的位置。 此位置是整个 ServiceConnectionTool 文件夹的副本。 例如：

    `cd D:\USB\ServiceConnectionTool\`

1. 运行以下命令，以上传数据文件并下载 Configuration Manager 更新：

    `ServiceConnectionTool.exe -connect -usagedatasrc D:\USB -updatepackdest D:\USB\UpdatePacks`

    若要查看更多示例，请参阅[命令行参数](#bkmk_cmd)。

    > [!NOTE]  
    > 运行此命令行时，可能会看到以下错误：
    >
    > “未处理的异常:**System.UnauthorizedAccessException：** 对路径 'C:\Users\jqpublic\AppData\Local\Temp\extractmanifestcab\95F8A562.sql' 的访问被拒绝。”
    >
    > 你可以放心忽略此错误。 可关闭错误窗口以继续操作。

1. 该工具完成下载更新后，将更新复制到服务连接点。

### <a name="import"></a>导入

1. 在托管服务连接点的计算机上，以管理员身份打开命令提示符，并将目录更改为此工具的位置。 例如：

    `cd C:\Source\SMSSETUP\TOOLS\ServiceConnectionTool\`

1. 运行以下命令以导入更新：

    `ServiceConnectionTool.exe -import -updatepacksrc D:\USB\UpdatePacks`

1. 导入完成后，关闭命令提示符。 将仅导入适用的层次结构的更新。

1. 在 Configuration Manager 控制台中，转到“管理”工作区，并选择“更新和维护服务”节点 。 现在即可安装已导入的更新。 有关详细信息，请参阅[安装控制台内部更新](install-in-console-updates.md)。

## <a name="log-files"></a>日志文件

- **ServiceConnectionTool.log**：每次运行服务连接工具时，它都会写入此日志文件。 此日志文件的路径始终与该工具的位置相同。 此日志文件基于所用的参数提供关于工具使用情况的简要详细信息。 每次运行工具时，该工具都将替换现有的任何日志文件。

- **ConfigMgrSetup.log**：在[连接](#connect)阶段期间，该工具会写入此日志文件，它位于系统驱动器的根处。 此日志文件提供更加详细的信息。 例如，该工具下载哪些文件以及哈希检查是否成功。

## <a name="command-line-parameters"></a><a name="bkmk_cmd"></a>命令行参数

此部分按字母顺序列出了服务连接工具的所有可用参数。

### <a name="-connect"></a>-connect

在[连接](#connect)阶段期间，在具有 Internet 访问权限的计算机上使用它。 此参数将连接到 Configuration Manager 云服务，以上传数据文件并下载更新。

它需要以下参数：

- -usagedatasrc：要上传的数据文件的位置
- -updatepackdest：下载的更新的路径

还可以使用以下可选参数：

- -proxyserveruri：代理服务器的 FQDN
- -proxyusername：代理服务器的用户名
- -downloadall：无论站点是哪种版本，均下载所有内容，包括更新和修补程序。
- -downloadhotfix：无论站点是哪种版本，均下载所有修补程序。
- -downloadsiteversion：下载版本高于站点版本的更新和修补程序。

#### <a name="example-of-connect-without-a-proxy-server"></a>不使用代理服务器的连接示例

`ServiceConnectionTool.exe -connect -usagedatasrc D:\USB\ -updatepackdest D:\USB\UpdatePacks`

#### <a name="example-of-connect-with-a-proxy-server"></a>使用代理服务器的连接示例

`ServiceConnectionTool.exe -connect -usagedatasrc D:\USB\Usagedata.cab -updatepackdest D:\USB\UpdatePacks -proxyserveruri itproxy.contoso.com -proxyusername jqpublic`

#### <a name="example-of-connect-to-download-only-site-version-applicable-updates"></a>仅下载站点版本的适用更新的连接示例

`ServiceConnectionTool.exe -connect -downloadsiteversion -usagedatasrc D:\USB -updatepackdest D:\USB\UpdatePacks`

### <a name="-dest"></a>-dest

带有 -export 参数的必需参数，用于指定要导出的 CSV 文件的路径和文件名。 有关详细信息，请参阅 [-export](#-export)。

### <a name="-downloadall"></a>-downloadall

带有 -connect 参数的可选参数，无论站点是哪种版本，它均会下载所有内容，其中包括更新和修补程序。 有关详细信息，请参阅 [-connect](#connect)。

### <a name="-downloadhotfix"></a>-downloadhotfix

带有 -connect 参数的可选参数，无论站点是哪种版本，它均会只下载所有修补程序。 有关详细信息，请参阅 [-connect](#-connect)。

### <a name="-downloadsiteversion"></a>-downloadsiteversion

带有 -connect 参数的可选参数，它只会下载版本高于站点版本的更新和修补程序。 有关详细信息，请参阅 [-connect](#-connect)。

### <a name="-export"></a>-export

在[准备](#prepare)阶段，使用它将使用情况数据导出到 CSV 文件。 在服务连接点上，以管理员身份运行它。 通过此操作，可以在将使用情况数据上传到 Microsoft 之前查看其内容。 它需要使用 -dest 参数来指定 CSV 文件的位置。

#### <a name="example-of-export"></a>导出示例

`-export -dest D:\USB\usagedata.csv`

### <a name="-import"></a>-import

在[导入](#import)阶段，在服务连接点上使用它将更新导入到站点。 它需要使用 -updatepacksrc 参数来指定下载的更新的位置。

#### <a name="example-of-import"></a>导入示例

`ServiceConnectionTool.exe -import -updatepacksrc D:\USB\UpdatePacks`

### <a name="-prepare"></a>-prepare

在[准备](#prepare)阶段，在服务连接点上使用它从站点导出使用情况数据。 它需要使用 -usagedatadest 参数来指定导出的数据文件的位置。

#### <a name="example-of-prepare"></a>准备示例

`ServiceConnectionTool.exe -prepare -usagedatadest D:\USB\UsageData.cab`

### <a name="-proxyserveruri"></a>-proxyserveruri

带有 -connect 参数的可选参数，用于指定代理服务器的 FQDN。 有关详细信息，请参阅 [-connect](#-connect)。

### <a name="-proxyusername"></a>-proxyusername

带有 -connect 参数的可选参数，用于指定要通过代理服务器验证的用户名。 有关详细信息，请参阅 [-connect](#-connect)。

### <a name="-updatepackdest"></a>-updatepackdest

带有 -connect 参数的必需参数，用于指定下载的更新的路径。 有关详细信息，请参阅 [-connect](#-connect)。

### <a name="-updatepacksrc"></a>-updatepacksrc

带有 -import 参数的必需参数，用于指定下载的更新的路径。 有关详细信息，请参阅 [-import](#-import)。

### <a name="-usagedatadest"></a>-usagedatadest

带有 -prepare 参数的必需参数，用于指定导出的数据文件的路径和文件名。 有关详细信息，请参阅 [-prepare](#-prepare)。

## <a name="next-steps"></a>后续步骤

[安装控制台内部更新](install-in-console-updates.md)

[如何查看诊断和使用情况数据](../../plan-design/diagnostics/view-diagnostics-and-usage-data.md)
