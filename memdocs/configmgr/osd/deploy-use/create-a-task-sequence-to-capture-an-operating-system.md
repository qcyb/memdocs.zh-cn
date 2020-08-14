---
title: 创建用于捕获 OS 的任务序列
titleSuffix: Configuration Manager
description: “构建和捕获”任务序列将构建可以包括特定驱动程序和软件更新，以及 OS 的引用计算机。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 25e4ac68-0e78-4bbe-b8fc-3898b372c4e8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 349ae2b8d574904d25f6f23bfb1707bb11df8af0
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125502"
---
# <a name="create-a-task-sequence-to-capture-an-os"></a>创建用于捕获 OS 的任务序列

适用范围：  Configuration Manager (Current Branch)

在使用任务序列将 OS 部署到 Configuration Manager 中的计算机时，该计算机会安装你在任务序列中指定的 OS 映像。 可以自定义 OS 映像，使它包含特定的驱动程序、应用程序和软件更新。 首先使用构建和捕获任务序列来构建引用计算机。 然后，从该引用计算机捕获 OS 映像。 如果已具有可进行捕获的引用计算机，则创建用于捕获 OS 的自定义任务序列。

## <a name="about-the-build-and-capture-task-sequence"></a><a name="BKMK_BuildCaptureTS"></a>关于构建和捕获任务序列

构建和捕获任务序列：

- 对引用计算机进行分区和格式化
- 安装 OS
- 安装 Configuration Manager 客户端
- 安装应用程序
- 应用软件更新
- 从引用计算机捕获 OS

在分发点上与任务序列（如应用程序）相关联的包必须可用，然后才能部署构建和捕获任务序列。

## <a name="requirements"></a><a name="BKMK_CreatePackages"></a>要求

在创建任务序列以安装 OS 之前，请确保已准备好了以下组件：  

### <a name="required"></a>必需

- [启动映像](../get-started/manage-boot-images.md)

- [OS 映像](../get-started/manage-operating-system-images.md)

### <a name="required-if-used"></a>必需（若使用）

- [驱动程序包](../get-started/manage-drivers.md)，该程序包包含用于支持引用计算机上硬件的必要 Windows 驱动程序。 有关管理驱动程序的任务序列步骤的详细信息，请参阅[使用任务序列安装设备驱动器](../get-started/manage-drivers.md#BKMK_TSDrivers)。

- [软件更新](../../sum/get-started/synchronize-software-updates.md)

- [应用程序](../../apps/deploy-use/create-applications.md)

## <a name="create-a-build-and-capture-task-sequence"></a><a name="BKMK_CreateBuildCaptureTS"></a> 创建一个构建和捕获任务序列

使用下列过程使用任务序列构建引用计算机和捕获 OS。

1. 在 Configuration Manager 控制台中，转到“软件库”  工作区，展开“操作系统”  ，然后选择“任务序列”  节点。  

1. 在功能区的“主页”选项卡上的“创建”组中，选择“创建任务序列”以启动创建任务序列向导    。  

1. 在“创建新的任务序列”  页上，选择“构建并捕获引用操作系统映像包”  。  

1. 在“任务序列信息”页上，指定以下设置  ：  

    - **任务序列名称**：指定用于标识任务序列的名称。  

    - **描述**：为任务序列指定可选描述。 例如，描述任务序列创建的 OS。

    - **启动映像**：指定要用于此任务序列的启动映像。  

        > [!IMPORTANT]  
        > 启动映像的体系结构必须与目标计算机的硬件体系结构兼容。  

1. 在“安装 Windows”页面上，指定以下设置  ：  

    - **映像包**：指定 OS 映像包，此包包含安装 OS 所需的文件。  

    - **映像索引**：指定要在映像中安装的 OS 的索引。 如果 OS 映像包含多个版本，则选择你想要安装的版本。  

    - **产品密钥**：如有必要，可以指定要安装的 Windows OS 的产品密钥。 你可以指定编码的批量许可证密钥和标准产品密钥。 如果使用非编码的产品密钥，请通过短划线 (`-`) 将每 5 个字符划分为一组。 例如：`XXXXX-XXXXX-XXXXX-XXXXX-XXXXX`  

    - **服务器授权模式**：如有必要，指定服务器许可证为“每席位”  、“每服务器”  或未指定许可证。 如果服务器许可证为“每服务器”  ，则还需指定服务器连接的最大数量。  

    - 指定如何为部署的 OS 配置管理员帐户：  

        - **随机生成本地管理员密码并在所有支持的平台上禁用帐户**：为本地管理员帐户创建随机密码。 设置 Windows 时禁用该帐户。

        - **启用帐户并指定本地管理员密码**：在部署此 OS 的所有计算机上为本地管理员帐户使用相同的密码。

1. 在“配置网络”页上，指定以下设置  ：

    - **加入工作组**：指定是否在部署 OS 时将目标计算机添加到工作组。  

    - **加入域**：指定是否在部署 OS 时将目标计算机添加到域。 在“域”  中，指定域的名称。  

        > [!IMPORTANT]  
        > 你可以浏览以在本地林中查找域。 指定远程林的域名。

        你还可以指定组织单位 (OU)。 这是一项可选设置，指定在其中创建计算机帐户的 OU 的 LDAP X.500 可分辨名称（如果尚未存在）。  

    - **帐户**：指定具有加入指定域的权限的帐户的用户名和密码。 例如：`domain\user` 或 `%variable%`。  

        > [!IMPORTANT]  
        > 如果打算在部署期间迁移域设置或工作组设置，请确保在此处输入相应的域凭据。  

1. 在“安装 Configuration Manager”页面上，指定 Configuration Manager 客户端包  。 此包包含用于安装 Configuration Manager 客户端的源文件。 此外，还要指定安装该客户端所需的任何其他属性。  

    有关详细信息，请参阅[关于客户端安装属性](../../core/clients/deploy/about-client-installation-properties.md)。

1. 在“包括更新”  页上，指定是安装必需的软件更新、所有软件更新还是不安装软件更新。 如果指定要安装软件更新，Configuration Manager 将只会安装以包含目标计算机的集合为目标的那些软件更新。  

1. 在“安装应用程序”  页上，指定要安装在目标计算机上的应用程序。 如果指定多个应用程序，你也可以指定任务序列在特定应用程序的安装失败时继续进行。  

    > [!NOTE]
    > 向导中接着会显示“系统准备”页面，但已不再使用此设置了  。 选择“下一步”继续操作  。

1. 在“映像属性”页面上，指定以下 OS 映像的设置  ：

    - **创建者**：指定要记为 OS 映像创建者的用户的名称。  

    - **版本**：指定与 OS 映像关联的版本号。 此属性无需是 OS 版本，因为站点会单独存储该值。

    - **描述**：指定 OS 映像的说明。  

1. 在“捕获映像”页面上，指定以下设置  ：

    - **路径**：指定共享网络文件夹，Configuration Manager 应将输出映像文件 (.wim) 存储在此文件夹中。 此文件包含以你在此向导中指定的设置为基础的 OS 映像。 如果指定包含现有 .WIM 文件的文件夹，它则会被覆盖。  

    - **帐户**：指定对存储映像的网络共享具有权限的 Windows 帐户。  

1. 完成向导。  

若要将额外的步骤添加到任务序列中，请选择该任务序列，然后选择“编辑”  。 有关如何编辑任务序列的信息，请参阅[使用任务序列编辑器](../understand/task-sequence-editor.md)。  

采用以下其中一种方式将任务序列部署到引用计算机：  

- 如果引用计算机已为 Configuration Manager 客户端，则将构建和捕获任务序列部署到包含引用计算机的集合。 有关详细信息，请参阅 [Deploy a task sequence](deploy-a-task-sequence.md)。

- 如果引用计算机不是 Configuration Manager 客户端，或者如果想手动在引用计算机上运行任务序列，则请使用“创建任务序列媒体向导”以创建可启动媒体  。 有关详细信息，请参阅[创建可启动媒体](create-bootable-media.md)。  

捕获映像后，可以将它部署到其他计算机。 有关如何部署捕获的 OS 映像的详细信息，请参阅[创建用于安装 OS 的任务序列](create-a-task-sequence-to-install-an-operating-system.md)。  

## <a name="capture-from-an-existing-reference-computer"></a><a name="BKMK_CaptureExistingRefComputer"></a> 从现有引用计算机捕获

如果已具有可随时用于捕获的引用计算机，则创建仅用于从引用计算机捕获 OS 的任务序列。 使用“捕获操作系统映像”任务序列步骤可从引用计算机捕获一个或多个映像，并将它们存储在指定网络共享上的映像文件 (wim) 文件中  。 在 Windows PE 中使用启动映像启动引用计算机。 任务序列将引用计算机上的每个硬盘驱动器捕获为 .wim 文件中的单独映像。 如果引用计算机有多个驱动器，则生成的 .wim 文件对于每个卷将包含单独的映像。 其仅捕获格式化为 NTFS 或 FAT32 的卷。 其他格式的卷或 USB 卷会被忽略。  

使用以下过程从现有引用计算机中捕获 OS 映像：

1. 在 Configuration Manager 控制台中，转到“软件库”  工作区，展开“操作系统”  ，然后选择“任务序列”  节点。  

1. 在功能区的“主页”选项卡上的“创建”组中，选择“创建任务序列”    。 此操作会启动“创建任务序列向导”。  

1. 在“创建新的任务序列”  页面上，选择“创建新的自定义任务序列”  。  

1. 在“任务序列信息”页面上，指定任务序列的名称  。 可以选择为任务序列添加描述。  

1. 指定任务序列的启动映像。 Configuration Manager 使用此启动映像通过 Windows PE 来启动引用计算机。 有关详细信息，请参阅[管理启动映像](../get-started/manage-boot-images.md)。  

1. 完成向导。  

1. 在“任务序列”节点中，选择新任务序列  。 然后在功能区的“主页”选项卡上，在“任务序列”组中，选择“编辑”    。 此操作会打开任务序列编辑器。  

1. 引用计算机上安装了 Configuration Manager 客户端时：

    转到“添加”菜单，选择“映像”，然后选择[准备 ConfigMgr 客户端以便捕获](../understand/task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture)   。 此步骤通用于引用计算机上的 Configuration Manager 客户端。

    > [!Note]  
    > 任务序列不支持卸载 Configuration Manager 客户端。

1. 转到“添加”菜单，选择“映像”，然后选择[准备 Windows 以便捕获](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture)   。 此步骤运行 Sysprep，然后将计算机重新启动到为该任务序列指定的 Windows PE 启动映像。 为了成功完成此操作，请勿将引用计算机加入域。

1. 转到“添加”菜单，选择“映像”，然后选择[捕获操作系统映像](../understand/task-sequence-steps.md#BKMK_CaptureOperatingSystemImage)   。 此步骤仅通过 Windows PE 运行以捕获引用计算机上的硬盘驱动器。 配置下列设置：

    - **名称**和**描述**：（可选）可以更改任务序列步骤的名称并提供说明。  

    - **目标**：指定存储输出 .WIM 文件的共享网络文件夹。 此文件包含以你使用此向导指定的设置为基础的 OS 映像。 如果指定包含现有 .WIM 文件的文件夹，它则会被覆盖。  

    - **描述**、**版本**和**创建者**：（可选）提供有关将捕获的映像的详细信息。  

    - **捕获操作系统映像帐户**：指定对你指定的网络共享具有访问权限的 Windows 帐户。 单击“设置”以指定该 Windows 帐户的名称  。  

选择“确定”  保存更改，并关闭“任务序列编辑器”。  

采用以下其中一种方式将任务序列部署到引用计算机：  

- 如果引用计算机已为 Configuration Manager 客户端，则将捕获任务序列部署到包含引用计算机的集合。 有关详细信息，请参阅 [Deploy a task sequence](deploy-a-task-sequence.md)。

- 如果引用计算机不是 Configuration Manager 客户端，或者如果想手动在引用计算机上运行任务序列，则请使用“创建任务序列媒体向导”以创建可捕获媒体  。 有关详细信息，请参阅[创建捕获媒体](create-capture-media.md)。  

捕获映像后，可以将它部署到其他计算机。 有关如何部署捕获的 OS 映像的详细信息，请参阅[创建用于安装 OS 的任务序列](create-a-task-sequence-to-install-an-operating-system.md)。

## <a name="example-task-sequence"></a><a name="BKMK_BuildandCaptureTSExample"></a> 任务序列示例

使用下表作为创建任务序列以构建和捕获 OS 映像时的指导。 该表将帮助你决定任务序列步骤的常规顺序，以及如何将这些步骤组织并构建成逻辑组。 所创建的任务序列可能与此示例不同。 它可能会包含更多或更少的步骤和组。

> [!NOTE]  
> 始终使用“创建任务序列向导”来创建此类型的任务序列。
>
> 向导会向任务序列添加步骤，这些步骤的名称与你手动添加相同步骤时看到的名称略有不同。

### <a name="group-build-the-reference-machine"></a>组：构建引用计算机

此组包含构建引用计算机所需的操作。

|任务序列步骤|说明|  
|-------------------------------|---------------|  
|**在 Windows PE 中重新启动**|针对分配给该任务序列的启动映像重启目标计算机。 此步骤会向用户显示一则消息，指出将重新启动计算机以便可以继续安装。<br /><br />此步骤使用只读 `_SMSTSInWinPE` 任务序列变量。 如果相关联的值等于 `false`，则任务序列步骤将继续。|
|**对磁盘 0 分区 - BIOS**|在 BIOS 模式下对目标计算机上的硬盘驱动器进行分区和格式化。 默认磁盘编号为 `0`。<br /><br />此步骤会使用几个只读的任务序列变量。 例如，它仅在 Configuration Manager 客户端缓存不存在时运行，并且在计算机配置为 UEFI 时不会运行。|
|**对磁盘 0 分区 - UEFI**|在 UEFI 模式下对目标计算机上的硬盘驱动器进行分区和格式化。 默认磁盘编号为 `0`。<br /><br />此步骤会使用几个只读的任务序列变量。 例如，它仅在 Configuration Manager 客户端缓存不存在时运行，以及仅在计算机配置为 UEFI 时运行。|
|**应用操作系统**|在目标计算机上安装指定的 OS 映像。 此步骤先删除卷上的所有文件，但 Configuration Manager 特定的控制文件除外。 然后，它会将 WIM 文件中包含的所有卷映像应用到目标计算机上的相应顺序磁盘卷。|
|**应用 Windows 设置**|配置目标计算机的 Windows 设置。|
|**应用网络设置**|指定目标计算机的网络或工作组配置信息。|
|**应用设备驱动程序**|在此 OS 部署过程中匹配并安装驱动程序。 有关详细信息，请参阅[自动应用驱动程序](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers)。<br /><br />此步骤使用只读 `_SMSTSMediaType` 任务序列变量。 如果关联的值不等于 `FullMedia`，此步骤则不会运行。|
|**安装 Windows 和 Configuration Manager**|安装 Configuration Manager 客户端软件。 Configuration Manager 安装和注册 Configuration Manager 客户端 GUID。 将所有必要的安装属性包含在内  。|
|**安装更新**|指定如何在目标计算机上安装软件更新。 在运行此步骤时，才会评估目标计算机是否有适用的软件更新。 届时，评估与任何其他 Configuration Manager 管理的客户端类似。 有关详细信息，请参阅[安装软件更新](../understand/install-software-updates.md)。<br /><br />此步骤使用只读 `_SMSTSMediaType` 任务序列变量。 如果关联的值不等于 `FullMedia`，此步骤则不会运行。|
|**安装应用程序**|指定要在引用计算机上安装的任何应用程序。|

### <a name="group-capture-the-reference-machine"></a>组：捕获引用计算机

此组包含准备和捕获引用计算机的必需步骤。

|任务序列步骤|说明|  
|-------------------------------|---------------|  
|**准备 Configuration Manager 客户端**|通用化引用计算机上的 Configuration Manager 客户端。|
|**准备 OS**|运行 Sysprep 以通用化 Windows。 随后，它将计算机重启到为该任务序列指定的 Windows PE 启动映像。|
|**捕获引用计算机**|将映像捕获到指定的网络共享和 .WIM 文件。|

> [!IMPORTANT]
> 从引用计算机捕获映像后，请勿从该引用计算机捕获其他的 OS 映像。 初始配置过程中会创建注册表项。 请在每次捕获操作 OS 时创建新引用计算机。 如果计划使用同一引用计算机来创建将来的 OS 映像，请首先卸载 Configuration Manager客户端，然后重新安装它。

## <a name="next-steps"></a>后续步骤

[部署企业版操作系统的方法](methods-to-deploy-enterprise-operating-systems.md)
