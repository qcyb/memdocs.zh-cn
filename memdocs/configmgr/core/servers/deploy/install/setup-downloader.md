---
title: 安装程序下载程序工具
titleSuffix: Configuration Manager
description: 使用独立工具下载关键安装文件的当前版本以便安装。
ms.date: 05/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bda87fc5-2e4c-4992-98a4-01770365038c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2da8aed5cfe4a478010165445094f1fce4627d9a
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428835"
---
# <a name="setup-downloader-for-configuration-manager"></a>Configuration Manager 的安装程序下载程序

适用范围：Configuration Manager (Current Branch)

运行 Configuration Manager 安装程序以安装或更新站点之前，可以使用安装程序下载程序独立工具来下载更新的安装文件。 运行由要安装的 Configuration Manager 版本提供的该工具。 使用更新的安装程序文件可确保站点安装使用当前版本的关键安装文件。

使用安装程序下载程序时，请指定用于包含文件的文件夹。 用于运行该工具的帐户必须具有对此下载文件夹的“完全控制”权限。 运行安装程序以安装或升级站点时，可以指定以前下载的文件的这一本地副本。 这样一来，在开始安装或升级站点时，安装程序不会连接到 Microsoft。 可将安装程序文件的相同本地副本用于相同版本的其他站点的安装或升级。

安装程序下载程序工具可下载以下类型的文件：

- 必需的先决条件可再发行文件
- 语言包
- 安装程序的最新产品更新

可以使用以下两个选项来运行安装程序下载程序：

- 使用用户界面运行应用程序
- 在命令提示符处运行应用程序，以查看其他命令行选项

如果组织使用防火墙或代理设备限制与 Internet 的网络通信，你必须允许该工具访问 Internet 终结点。 运行该工具的设备需要与服务连接点相同的 Internet 访问权限。 有关详细信息，请参阅 [Internet 访问要求](../../../plan-design/network/internet-endpoints.md#bkmk_scp)。<!-- SCCMDocs#677 -->

## <a name="run-setup-downloader-with-the-user-interface"></a><a name="bkmk_ui"></a> 使用用户界面运行安装程序下载程序

1. 在具有 Internet 访问权限的计算机上，浏览到要安装的 Configuration Manager 版本的安装介质。

1. 在“SMSSETUP\BIN\X64”子文件夹中，运行 Setupdl.exe 。

1. 指定用于存储更新的安装文件的文件夹的路径，然后选择“下载”。 安装程序下载程序将验证当前位于下载文件夹中的文件。 它仅下载缺少的文件或比现有文件更新的文件。 它将创建多个子文件夹，用于存储下载的语言和其他必要组件。

1. 若要查看下载结果，请访问 C:\ConfigMgrSetup.log。

## <a name="run-setup-downloader-from-a-command-prompt"></a><a name="bkmk_cmd"></a> 从命令提示符运行安装程序下载程序

1. 打开命令提示符，更改要安装的 Configuration Manager 版本的安装介质的目录。

1. 将目录更改为“SMSSETUP\BIN\X64”子文件夹，并使用必需的选项运行 Setupdl.exe 。

1. 若要查看下载结果，请访问 C:\ConfigMgrSetup.log。

### <a name="command-line-options"></a>命令行选项

可将以下命令行选项配合“Setupdl.exe”使用：

- **/VERIFY**：验证下载文件夹中的文件（包括语言文件）。 对于过期文件的列表，请查看 C:\ConfigMgrSetup.log。 使用此选项时，不会下载任何文件。

- **/VERIFYLANG**：仅验证下载文件夹中的语言文件。 对于过期语言文件的列表，请查看 C:\ConfigMgrSetup.log。

- **/LANG**：仅将语言文件下载到下载文件夹。

- **/NOUI**：不使用用户界面，启动安装程序下载程序。 使用此选项时，需要下载路径。

- **下载路径**：若要自动启动验证或下载流程，请指定下载文件夹的路径。 使用“/NOUI”选项时，需要下载路径。 如果未指定下载路径，安装程序下载程序会提示你指定路径。 如果文件夹不存在，安装程序下载程序会进行创建。

### <a name="example-commands"></a>示例命令

#### <a name="example-1"></a>示例 1

安装程序下载程序将验证指定下载文件夹中的文件，然后下载文件。

`setupdl.exe C:\Download`

#### <a name="example-2"></a>示例 2

安装程序下载程序仅验证指定下载文件夹中的文件。

`setupdl.exe /VERIFY C:\Download`

#### <a name="example-3"></a>示例 3

安装程序下载程序将验证指定下载文件夹中的文件，然后下载文件。 该工具不会显示任何用户界面。

`setupdl.exe /NOUI C:\Download`

#### <a name="example-4"></a>示例 4

安装程序下载程序将验证指定下载文件夹中的语言文件，然后仅下载语言文件。

`setupdl.exe /LANG C:\Download`

## <a name="copy-setup-downloader-files-to-another-computer"></a><a name="bkmk_cp-files"></a> 将安装程序下载程序文件复制到另一台计算机

1. 在 Windows 资源管理器中，转到以下任一位置：

    - &lt;Configuration Manager installation media>\SMSSETUP\BIN\X64

    - &lt;Configuration Manager installation path>\BIN\X64

1. 将以下文件复制到另一台计算机上的目标文件夹：

    - setupdl.exe

    - .\\&lt;language>\\setupdlres.dll

        > [!NOTE]
        > 此文件位于安装语言的子文件夹。 例如，英语位于 `00000409` 子文件夹。

    设备上的目标文件夹应如下所示：

    - `C:\ConfigManInstall\setupdl.exe`

    - `C:\ConfigManInstall\00000409\setupdlres.dll`

1. 运行目标计算机中的安装程序下载程序。 使用[用户界面](#bkmk_ui)或[命令提示符](#bkmk_cmd)。
