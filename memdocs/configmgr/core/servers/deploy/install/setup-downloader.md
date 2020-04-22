---
title: 安装程序下载程序
titleSuffix: Configuration Manager
description: 阅读有关此独立应用程序的信息，该应用程序可确保站点安装使用的是当前版本的关键安装文件。
ms.date: 01/22/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bda87fc5-2e4c-4992-98a4-01770365038c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2fa1899f8e7dc14812f9f9ecf889350a153b2d25
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700565"
---
# <a name="setup-downloader-for-configuration-manager"></a>Configuration Manager 的安装程序下载程序

适用范围：  Configuration Manager (Current Branch)

在运行安装程序安装或升级 Configuration Manager 站点之前，可从要安装的 Configuration Manager 版本中使用安装程序下载程序独立应用程序下载更新的安装程序文件。  

使用更新的安装程序文件可确保站点安装使用当前版本的关键安装文件。 在概述中：   
-   在启动安装程序之前使用安装程序下载程序来下载文件时，指定一个文件夹来放置这些文件。  
-   用来运行安装程序下载程序的帐户必须具有对此下载文件夹的“完全控制”  权限。  
-   运行安装程序以安装或升级站点时，可以指示它使用以前下载文件的本地副本。 这样在开始安装或升级站点时，安装程序无需连接到 Microsoft。  
-   你可将相同的安装程序文件本地副本用于后续站点安装或升级。  

安装程序下载程序下载以下类型的文件：  
-   必需的先决条件可再发行文件  
-   语言包  
-   安装程序的最新产品更新  

可使用两个选项来运行安装程序下载程序：
- 使用用户界面运行应用程序
- 对于命令行选项，请在命令提示符处运行应用程序


## <a name="run-setup-downloader-with-the-user-interface"></a><a name="bkmk_ui"></a> 使用用户界面运行安装程序下载程序  

1.  在具有 Internet 访问的计算机上，打开 Windows 资源管理器，并转到 &lt;ConfigMgrInstallationMedia\>\SMSSETUP\BIN\X64。   

2.  若要打开安装程序下载程序，请双击“Setupdl.exe”  。   

3. 指定将承载更新的安装文件的文件夹的路径，然后单击“下载”  。 安装程序下载程序将验证当前位于下载文件夹中的文件。 它仅下载缺少的文件或比现有文件更新的文件。 安装程序下载程序将创建用于下载的语言的子文件夹和其他所需的子文件夹。  

4.  若要查看下载结果，请打开驱动器 C 的根目录中的“ConfigMgrSetup.log”  文件。  

## <a name="run-setup-downloader-from-a-command-prompt"></a><a name="bkmk_cmd"></a> 从命令提示符运行安装程序下载程序  

1.  在命令提示符窗口中，转到 &lt;Configuration Manager 安装介质\>\SMSSETUP\BIN\X64  。   

2.  若要打开安装程序下载程序，请运行“Setupdl.exe”  。

    可将以下命令行选项配合“Setupdl.exe”  使用：   

    -   **/VERIFY**：此选项可用于验证下载文件夹中的文件（包括语言文件）。 查看驱动器 C 根目录中的 ConfigMgrSetup.log 文件，获取过期文件的列表。 使用此选项时不会下载文件。  

    -   **/VERIFYLANG**：此选项可用于验证下载文件夹中的语言文件。 查看驱动器 C 根目录中的 ConfigMgrSetup.log 文件，获取过期语言文件的列表。

    -   **/LANG**：此选项可用于仅将语言文件下载到下载文件夹。  

    -   **/NOUI**：此选项可用于启动安装程序下载程序，而不显示用户界面。 如果使用此选项，必须指定“下载路径”  作为命令提示符中命令的一部分。  

    -   **&lt;DownloadPath\>** ：可以指定下载文件夹的路径，以自动启动验证或下载流程。 使用“/NOUI”  选项时必须指定下载路径。 如果未指定下载路径，则必须在安装程序下载程序打开时指定该路径。 安装程序下载程序会创建文件夹（如果不存在）。  

    示例命令：

    -   setupdl &lt;DownloadPath\>   

        -   安装程序下载程序将启动，验证指定下载文件夹中的文件，然后仅下载缺少的文件或比现有文件版本更新的文件。     

    -   **setupdl /VERIFY &lt;DownloadPath\>**  

        -   安装程序下载程序将启动并验证指定下载文件夹中的文件。  

    -   **setupdl /NOUI &lt;DownloadPath\>**  

        -   安装程序下载程序将启动，验证指定下载文件夹中的文件，然后仅下载缺少的文件或比现有文件更新的文件。  

    -   **setupdl /LANG  &lt;DownloadPath\>**  

        -   安装程序下载程序将启动，验证指定下载文件夹中的语言文件，然后仅下载缺少的语言文件或比现有文件更新的语言文件。  

    -   **setupdl /VERIFY**  

        -   安装程序下载程序将启动，然后你必须指定下载文件夹的路径。 接下来，单击“验证”  之后，安装程序下载程序将验证下载文件夹中的文件。  

3.  若要查看下载结果，请打开驱动器 C 的根目录中的“ConfigMgrSetup.log”  文件。

## <a name="copy-setup-downloader-files-to-another-computer"></a><a name="bkmk_cp-files"></a> 将安装程序下载程序文件复制到另一台计算机

1. 在 Windows 资源管理器中，转到以下任一位置：

    - &lt;Configuration Manager installation media>\SMSSETUP\BIN\X64 
    - &lt;Configuration Manager installation path>\BIN\X64 
    
1. 将以下文件复制到另一台计算机上的目标文件夹：
    
    - setupdl.exe 
    - .\\&lt;language>\\setupdlres.dll 
      - 此文件位于安装语言的子文件夹。 例如，英语位于 `00000409` 子文件夹。

    例如，设备上的目标文件夹应如下所示：
    - C:\ConfigManInstall\setupdl.exe
    - C:\ConfigManInstall\00000409\setupdlres.dll

1. 如上所述，使用[用户界面](#bkmk_ui)或[命令提示符](#bkmk_cmd)，从计算机启动安装程序下载程序。
