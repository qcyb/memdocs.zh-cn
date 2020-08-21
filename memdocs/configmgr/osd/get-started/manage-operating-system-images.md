---
title: 管理 OS 映像
titleSuffix: Configuration Manager
description: 了解用于管理存储在 Windows 映像 (WIM) 文件中的 OS 映像的方法。
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: fab13949-371c-4a4c-978e-471db1e54966
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2f8b8a45ff83ce903f5737c94144e6ca5ab50826
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697647"
---
# <a name="manage-os-images-with-configuration-manager"></a>使用 Configuration Manager 管理 OS 映像

适用范围：  Configuration Manager (Current Branch)

Configuration Manager 中的 OS 映像以 Windows 映像 (WIM) 文件格式存储。 这些映像是一系列压缩的引用文件和文件夹，这些引用文件和文件夹用于在计算机上安装和配置新 OS。 许多 OS 部署方案都需要 OS 映像。


## <a name="os-image-types"></a>OS 映像类型

可以使用[默认 OS 映像](#default-image)或者从配置的[引用计算机](#bkmk_capture)生成 OS 映像。 生成引用计算机时，可以向 OS 添加 OS 文件、驱动程序、支持文件、软件更新、工具和应用程序。 然后捕获它以创建映像文件。

### <a name="default-image"></a>默认映像

Windows 安装文件包含默认 OS 映像。 此映像是包含一组标准驱动程序的基本 OS 映像。 使用默认 OS 映像时，请使用任务序列步骤安装应用，并在设备上安装 OS 后进行其他配置。 在 Windows 源文件中找到默认 OS 映像：`\Sources\install.wim`。  

#### <a name="default-image-advantages"></a>默认映像的优点

- 映像大小小于捕获的映像。  

- 使用任务序列步骤安装应用和配置可更加灵活。 例如，无需对设备重置映像，即可更改按任务序列安装的配置和应用。  

#### <a name="default-image-disadvantages"></a>默认映像的缺点

- OS 安装可能更耗时。 应用程序的安装和其他配置发生在 OS 安装完成后。  


### <a name="captured-image-from-a-reference-computer"></a><a name="bkmk_capture"></a> 从引用计算机捕获的映像

要创建自定义的 OS 映像，请使用所需的 OS 生成引用计算机。 然后安装应用程序并配置设置。 从引用计算机捕获 OS 映像以创建 WIM 文件。 手动生成引用计算机，或者使用任务序列自动执行部分或全部生成步骤。 有关详细信息，请参阅[自定义 OS 映像](customize-operating-system-images.md)。  

#### <a name="captured-image-advantages"></a>捕获的映像优点

- 安装速度可以比使用默认映像更快。 例如，可以使用捕获的 OS 映像预先安装应用程序。 稍后无需再使用任务序列步骤安装这些相同的应用程序。  

#### <a name="captured-image-disadvantages"></a>捕获的映像缺点

- 图像大小可能大于默认图像。  

- 在应用程序和工具需要更新时必须创建新映像。  


## <a name="add-an-os-image"></a><a name="BKMK_AddOSImages"></a> 添加 OS 映像  

在使用 OS 映像之前，请将其添加到 Configuration Manager 站点。

1. 在 Configuration Manager 控制台中，转到“软件库”工作区，展开“操作系统”，然后选择“操作系统映像”节点    。  

2. 在功能区“主页”选项卡的“创建”组中，选择“添加操作系统映像”    。 此操作将启动“添加操作系统映像向导”。  

3. 在“数据源”页上，指定以下信息  ：

    - OS 映像文件的网络路径  。 例如，`\\server\share\path\image.wim`。

    - 选择“从指定 WIM 文件中提取特定的映像索引”，然后从列表中选择映像索引  。<!--3719699--> 从版本 1902 开始，此选项自动导入单个索引，而不是文件中的所有映像索引。 使用此选项会使得映像文件更小，以及脱机维护更快。 它还支持[优化映像服务](#bkmk_resetbase)的过程，适用于应用软件更新后更小的映像文件。  

        > [!Note]  
        > Configuration Manager 不会修改源映像文件。 它将在同一源目录中创建新映像文件。
        >
        > 对于超大映像文件（例如超过 60 GB），此提取过程可能会失败。 DISM 错误为 `Not enough storage is available to process this command.`，Configuration Manager 使用的命令行位于 smsprov.log 和 dism.log 中。 手动运行同一命令，然后导入映像。<!-- SCCMDocs-pr issue 3502 -->  

    - 从版本 1906 开始，如果要在客户端上预缓存内容，请指定映像的“体系结构”  和“语言”  。 有关详细信息，请参阅[配置预缓存内容](../deploy-use/configure-precache-content.md)。<!--4224642-->  

4. 在“常规”页面上，指定以下信息  。 当你有多个 OS 映像时，可利用这些信息对其进行识别。  

    - **名称**：映像的唯一名称。 默认情况下，名称来自 WIM 文件名。  

    - **版本**：可选的版本标识符。 此属性不必是映像的 OS 版本。 它通常为组织的包的版本。  

    - **注释**：可选的简要说明。  

5. 完成向导。  

有关与此控制台向导的等效 PowerShell cmdlet，请参阅 [New-CMOperatingSystemImage](/powershell/module/configurationmanager/new-cmoperatingsystemimage?view=sccm-ps)。

接下来，将 OS 映像分发到分发点。  


## <a name="distribute-content-to-distribution-points"></a><a name="BKMK_DistributeBootImages"></a> 将内容分发到分发点  

将 OS 映像分发到其他内容所分发到的相同分发点。 在部署任务序列之前，请将 OS 映像分发到至少一个分发点。 有关详细信息，请参阅[分发内容](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)。  


[!INCLUDE [Apply software updates to an image](includes/wim-apply-updates.md)]


## <a name="prepare-the-os-image-for-multicast-deployments"></a><a name="BKMK_OSImageMulticast"></a> 为多播部署准备 OS 映像  

使用多播部署，可以使多台计算机同时下载 OS 映像。 映像通过分发点多播给客户端，而不是每个客户端通过单独连接从分发点下载映像的副本。 选择采用 OS 部署方法[使用多播通过网络来部署 Windows](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md) 时，请将 OS 映像配置为支持多播。 然后将映像分发到启用了多播的分发点。

1. 在 Configuration Manager 控制台中，转到“软件库”工作区，展开“操作系统”，然后选择“操作系统映像”节点    。  

2. 选择要分发到启用了多播的分发点的 OS 映像。  

3. 在功能区“主页”  选项卡的“属性”  组中，选择“属性”  。  

4. 切换到“分发设置”选项卡，并配置以下选项  ：  

    - **允许通过多播传输此包（仅 WinPE）** ：选择此选项使 Configuration Manager 使用多播同时部署多个 OS 映像。  

    - **加密多播包**：指定站点在将图像发送到分发点之前是否对其进行加密。 如果映像中包含敏感信息，请使用此选项。 如果映像未加密，则其内容会以明文形式在网络上可见。 于是，未经授权的用户可以截获并查看映像内容。  

    - **仅通过多播传输此包**：指定是否希望分发点仅在多播会话期间部署映像。  

         如果选择“仅通过多播传输此包”，则还必须将任务序列部署选项制定为“运行的任务序列需要时从本地下载内容”   。 有关详细信息，请参阅 [Deploy a task sequence](../deploy-use/deploy-a-task-sequence.md)。  

5. 选择“确定”以保存设置并关闭映像属性  。