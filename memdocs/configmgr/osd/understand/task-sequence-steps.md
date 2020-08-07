---
title: 任务序列步骤
titleSuffix: Configuration Manager
description: 了解可添加到 Configuration Manager 任务序列的步骤。
ms.date: 07/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 7c888a6f-8e37-4be5-8edb-832b218f266d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 61070d98c5b7d453f493cf7ea2995705ee43f325
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87546614"
---
# <a name="task-sequence-steps"></a>任务序列步骤

适用范围：Configuration Manager (Current Branch)

以下任务序列步骤可添加到 Configuration Manager 任务序列中。 有关详细信息，请参阅[使用任务序列编辑器](task-sequence-editor.md)。  

## <a name="common-settings"></a>通用设置

以下设置常见于所有任务序列步骤：

### <a name="properties-for-all-steps"></a>所有步骤的属性

- **名称**：任务序列编辑器要求指定一个短名称，用于描述此步骤。 添加新步骤时，任务序列编辑器默认将名称设置为“Type”。 名称的长度不能超过 50 个字符。  

- **描述**：（可选）指定有关此步骤的更多详细信息。 说明的长度不能超过 256 个字符。  

本文的其余部分将介绍每个任务序列步骤的“属性”选项卡上的其他设置。

### <a name="options-for-all-steps"></a>所有步骤的选项

- **禁用此步骤**：任务序列在计算机上运行时，会跳过此步骤。 此步骤的图标在任务序列编辑器中灰显。  

- **出错时继续**：如果在运行该步骤时出现错误，继续执行任务序列。 有关详细信息，请参阅[计划自动执行任务时的考虑事项](../plan-design/planning-considerations-for-automating-tasks.md#BKMK_TSGroups)。  

- **添加条件**：任务序列判断这些条件语句，以确定其是否运行该步骤。 有关使用任务序列变量作为条件的示例，请参阅[如何使用任务序列变量](using-task-sequence-variables.md#bkmk_access-condition)。 若要详细了解条件，请参阅[任务序列编辑器 - 条件](task-sequence-editor.md#bkmk_conditions)。

有关特定任务序列步骤的以下各节介绍了“选项”选项卡上的其他可能设置。



## <a name="apply-data-image"></a><a name="BKMK_ApplyDataImage"></a>应用数据映像

使用本步骤将数据映像复制到指定目标分区。  

此步骤仅可在 Windows PE 中运行。 它不会在完整的 OS 中运行。

选择任务序列编辑器中的“添加”，选择“映像”，然后选择“应用数据映像”以添加此步骤。

### <a name="variables-for-apply-data-image"></a>“应用数据映像”的变量

在此步骤中使用以下任务序列变量：  

- [OSDDataImageIndex](task-sequence-variables.md#OSDDataImageIndex)  
- [OSDWipeDestinationPartition](task-sequence-variables.md#OSDWipeDestinationPartition)  

### <a name="cmdlets-for-apply-data-image"></a>“应用数据映像”的 cmdlet

使用以下 PowerShell cmdlet 管理此步骤：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyDataImage](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepApplyDataImage?view=sccm-ps)
- [New-CMTSStepApplyDataImage](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepApplyDataImage?view=sccm-ps)
- [Remove-CMTSStepApplyDataImage](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepApplyDataImage?view=sccm-ps)
- [Set-CMTSStepApplyDataImage](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepApplyDataImage?view=sccm-ps)

### <a name="properties-for-apply-data-image"></a>“应用数据映像”的属性

在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="image-package"></a>映像包

选择“浏览”以指定供此任务序列使用的“映像包” 。 在“选择包”对话框中选择要安装的包。 每个现有映像包的关联属性信息显示在对话框的底部。 使用下拉列表，从所选的“映像包”中选择要安装的“映像”。  

> [!NOTE]  
> 此任务序列操作将映像视为数据文件。 此操作不会执行任何安装来将映像作为 OS 进行启动。  

#### <a name="destination"></a>目标

配置下列选项之一：

- **下一个可用分区**：使用此任务序列中尚未被“应用操作系统”或“应用数据映像”步骤作为目标的下一个顺序分区 。  

- **特定磁盘和分区**：选择“磁盘”编号（从 0 开始）和“分区”编号（从 1 开始） 。  

- **特定逻辑驱动器号**：指定 Windows PE 分配给分区的“驱动器号”。 此驱动器号可不同于新部署的 OS 分配的驱动器号。  

- **变量中存储的逻辑驱动器号**：指定包含 Windows PE 分配给分区的驱动器号的任务序列变量。 对于“格式化磁盘并分区”任务序列步骤，此变量通常在“分区属性”对话框的“高级”部分中设置。  

#### <a name="delete-all-content-on-the-partition-before-applying-the-image"></a>应用映像之前删除分区中的所有内容  

指定任务序列在安装映像前删除目标分区中的所有文件。 如果不删除分区内容，则此操作可用于将其他内容应用到以前的目标分区。  



## <a name="apply-driver-package"></a><a name="BKMK_ApplyDriverPackage"></a>应用驱动程序包  

使用此步骤可下载驱动程序包中的所有驱动程序，并将其安装在 Windows OS 上。

“应用驱动程序包”任务序列步骤使 Windows 可以使用驱动程序包中的所有设备驱动程序。 将此步骤添加到“应用操作系统”与“安装 Windows 和 ConfigMgr”步骤之间，使包中的驱动程序可以用于 Windows 。 “应用驱动程序包”任务序列步骤也可以与独立媒体部署方案配合使用。  

将类似的设备驱动程序放入驱动程序包，并将其分发到合适的分发点。 例如，将一个制造商的所有驱动程序放入一个驱动程序包。 然后将该程序包分发到关联计算机可以对其进行访问的分发点。

“应用驱动程序包”步骤可用于独立媒体。 此步骤也可用于安装一组特定的驱动程序。 这些类型的驱动程序包括 Windows 即插即用扫描检测不到的设备，例如网络打印机。  

此任务序列步骤仅可在 Windows PE 中运行。 它不会在完整的 OS 中运行。

选择任务序列编辑器中的“添加”，选择“驱动程序”，然后选择“应用驱动程序包”以添加此步骤。

> [!TIP]
> 有关 Configuration Manager 中的驱动程序的概述，请参阅[使用任务序列安装驱动程序](../get-started/manage-drivers.md#BKMK_TSDrivers)。
>
> 在用户安装任务序列前，使用内容预缓存功能下载适用的驱动程序包。 有关详细信息，请参阅[配置预缓存内容](../deploy-use/configure-precache-content.md)。

### <a name="variables-for-apply-driver-package"></a>“应用驱动程序包”的变量

在此步骤中使用以下任务序列变量：  

- [OSDApplyDriverBootCriticalContentUniqueID](task-sequence-variables.md#OSDApplyDriverBootCriticalContentUniqueID)  
- [OSDApplyDriverBootCriticalHardwareComponent](task-sequence-variables.md#OSDApplyDriverBootCriticalHardwareComponent)  
- [OSDApplyDriverBootCriticalID](task-sequence-variables.md#OSDApplyDriverBootCriticalID)  
- [OSDApplyDriverBootCriticalINFFile](task-sequence-variables.md#OSDApplyDriverBootCriticalINFFile)  
- [OSDInstallDriversAdditionalOptions](task-sequence-variables.md#OSDInstallDriversAdditionalOptions)<!--516679/2840016-->

### <a name="cmdlets-for-apply-driver-package"></a>“应用驱动程序包”的 cmdlet

使用以下 PowerShell cmdlet 管理此步骤：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyDriverPackage](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepApplyDriverPackage?view=sccm-ps)
- [New-CMTSStepApplyDriverPackage](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepApplyDriverPackage?view=sccm-ps)
- [Remove-CMTSStepApplyDriverPackage](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepApplyDriverPackage?view=sccm-ps)
- [Set-CMTSStepApplyDriverPackage](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepApplyDriverPackage?view=sccm-ps)

### <a name="properties-for-apply-driver-package"></a>“应用驱动程序包”的属性

在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="driver-package"></a>驱动程序包

指定包含所需的设备驱动程序的驱动程序包。 选择“浏览”以启动“选择包”对话框。 选择要应用的现有驱动程序包。 关联的包属性显示在对话框底部。  

#### <a name="install-driver-package-via-running-dism-with-recurse-option"></a>通过运行具有递归选项的 DISM 安装驱动程序包

Windows 应用驱动程序包时，选择此选项可将 `/recurse` 参数添加到 DISM 命令行。

启用此选项后，还可以指定其他 DISM 命令行参数。 使用 [OSDInstallDriversAdditionalOptions](task-sequence-variables.md#OSDInstallDriversAdditionalOptions) 任务序列变量包含更多选项。 有关详细信息，请参阅 [Windows 10 DISM 命令行选项](https://docs.microsoft.com/windows-hardware/manufacture/desktop/deployment-image-servicing-and-management--dism--command-line-options)。<!-- SCCMDocs#2125 -->

#### <a name="select-the-mass-storage-driver-within-the-package-that-needs-to-be-installed-before-setup-on-pre-windows-vista-operating-systems"></a>选择包中需要安装的大容量存储驱动程序，然后在 Windows Vista 以前的操作系统上安装

指定安装经典 OS 时所需的任何大容量存储驱动程序。  

##### <a name="driver"></a>驱动程序

选择要在安装经典 OS 前安装的大容量存储驱动程序文件。 下拉列表根据指定包填充。  

##### <a name="model"></a>型号

指定 Windows Vista 之前的 OS 部署需要的启动关键设备。  

#### <a name="do-unattended-installation-of-unsigned-drivers-on-version-of-windows-where-this-is-allowed"></a>在 Windows 版本上对未签名的驱动程序执行允许的无人参与安装

此选项允许 Windows 安装没有数字签名的驱动程序。  



## <a name="apply-network-settings"></a><a name="BKMK_ApplyNetworkSettings"></a>应用网络设置  

使用此步骤指定目标计算机的网络或工作组配置信息。 任务序列将这些值存储在相应的答案文件中。 Windows 安装程序在“安装 Windows 和 ConfigMgr”操作过程中使用该答案文件。  

此任务序列步骤仅可在 Windows PE 中运行。 它不会在完整的 OS 中运行。

选择任务序列编辑器中的“添加”，选择“设置”，然后选择“应用网络设置”以添加此步骤。

> [!NOTE]
> 如果在任务序列中包含此步骤的多个实例，则条件不适用。 任务序列中此步骤的最后一个实例的设置会应用于设备。 若要解决此问题，请将每个步骤包括在单独的组中，并在组中包含条件。

### <a name="variables-for-apply-network-settings"></a>“应用网络设置”的变量

在此步骤中使用以下任务序列变量：  

- [OSDAdapter](task-sequence-variables.md#OSDAdapter)  
- [OSDAdapterCount](task-sequence-variables.md#OSDAdapterCount)  
- [OSDDNSDomain](task-sequence-variables.md#OSDDNSDomain)  
- [OSDDNSSuffixSearchOrder](task-sequence-variables.md#OSDDNSSuffixSearchOrder)  
- [OSDDomainName](task-sequence-variables.md#OSDDomainName)  
- [OSDDomainOUName](task-sequence-variables.md#OSDDomainOUName)  
- [OSDEnableTCPIPFiltering](task-sequence-variables.md#OSDEnableTCPIPFiltering)  
- [OSDJoinAccount](task-sequence-variables.md#OSDJoinAccount)  
- [OSDJoinPassword](task-sequence-variables.md#OSDJoinPassword)  
- [OSDWorkgroupName](task-sequence-variables.md#OSDWorkgroupName)  

### <a name="cmdlets-for-apply-network-settings"></a>“应用网络设置”的 cmdlet

使用以下 PowerShell cmdlet 管理此步骤：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyNetworkSetting](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepApplyNetworkSetting?view=sccm-ps)
- [New-CMTSStepApplyNetworkSetting](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepApplyNetworkSetting?view=sccm-ps)
- [Remove-CMTSStepApplyNetworkSetting](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepApplyNetworkSetting?view=sccm-ps)
- [Set-CMTSStepApplyNetworkSetting](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepApplyNetworkSetting?view=sccm-ps)

### <a name="properties-for-apply-network-settings"></a>“应用网络设置”的属性

在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="join-a-workgroup"></a>加入工作组

选择此选项，使目标计算机加入指定的工作组。 在“工作组”行中输入工作组的名称。 此值可被“捕获网络设置”任务序列步骤所捕获的值替代。

#### <a name="join-a-domain"></a>加入域

选择此选项以将目标计算机加入指定的域。 指定或浏览到域，如 `fabricam.com`。 指定或浏览到组织单位的轻型目录访问协议 (LDAP) 路径。 例如： `LDAP//OU=computers, DC=Fabricam.com, C=com`。  

#### <a name="account"></a>帐户

选择“设置”以指定拥有将计算机加入域所需权限的帐户。 在“Windows 用户帐户”对话框中，使用下列格式输入用户名：`Domain\User`。 有关详细信息，请参阅[域连接帐户](../../core/plan-design/hierarchy/accounts.md#task-sequence-domain-join-account)。

#### <a name="adapter-settings"></a>适配器设置

指定计算机中每个网络适配器的网络配置。 选择“新建”以打开“网络设置”对话框，然后指定网络设置。

- 如果还使用“捕获网络设置”步骤，任务序列会将先前捕获的设置应用到网络适配器。
- 如果任务序列先前没有捕获网络设置，则会应用在此步骤中指定的设置。
- 任务序列将按 Windows 设备枚举顺序将这些设置应用到网络适配器。  
- 任务序列不会立即将此步骤中指定的设置应用到计算机。



## <a name="apply-operating-system-image"></a><a name="BKMK_ApplyOperatingSystemImage"></a>应用操作系统映像  

使用此步骤，在目标计算机上安装 OS。

在“应用操作系统”操作运行之后，它会将 OSDTargetSystemDrive 变量设置为包含 OS 文件的分区的驱动器号。  

此任务序列步骤仅可在 Windows PE 中运行。 它不会在完整的 OS 中运行。

选择任务序列编辑器中的“添加”，选择“映像”，然后选择“应用操作系统映像”以添加此步骤。

> [!TIP]
> 从 Windows 10 1709 版开始，媒体包括多个版本。 如果要将任务序列配置为使用 OS 升级包或 OS 映像，请务必选择[支持的版本](../../core/plan-design/configs/support-for-windows-10.md#windows-10-as-a-client)。  
>
> 在用户安装任务序列前，使用内容预缓存功能下载适用的操作系统升级包。 有关详细信息，请参阅[配置预缓存内容](../deploy-use/configure-precache-content.md)。
>
> “安装 Windows 和 ConfigMgr”步骤开始安装 Windows。

### <a name="variables-for-apply-os-image"></a>“应用操作系统映像”的变量

在此步骤中使用以下任务序列变量：  

- [OSDConfigFileName](task-sequence-variables.md#OSDConfigFileName)  
- [OSDImageIndex](task-sequence-variables.md#OSDImageIndex)  
- [OSDTargetSystemDrive](task-sequence-variables.md#OSDTargetSystemDrive)  

### <a name="cmdlets-for-apply-os-image"></a>“应用操作系统映像”的 cmdlet

使用以下 PowerShell cmdlet 管理此步骤：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepApplyOperatingSystem?view=sccm-ps)
- [New-CMTSStepApplyOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepApplyOperatingSystem?view=sccm-ps)
- [Remove-CMTSStepApplyOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepApplyOperatingSystem?view=sccm-ps)
- [Set-CMTSStepApplyOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepApplyOperatingSystem?view=sccm-ps)

### <a name="behaviors-for-apply-os-image"></a>“应用操作系统映像”的行为

此步骤执行不同的操作，具体取决于使用操作系统映像还是操作系统升级包。  

#### <a name="os-image-actions"></a>OS 映像操作

使用 OS 映像时，“应用操作系统映像”步骤将执行以下操作：  

1. 删除目标卷中的所有内容，\_SMSTSUserStatePath 变量指定的文件夹中的文件除外。  

2. 将指定的 .wim 文件的内容提取到指定目标分区。  

3. 准备答案文件：  

    1. 为部署的 OS 创建新的默认 Windows 安装程序答案文件（sysprep.inf 或 unattend.xml）。  

    2. 合并用户提供的答案文件中的所有值。  

4. 将 Windows 启动加载程序复制到活动分区中。  

5. 设置 boot.ini 或启动配置数据库 (BCD) 来引用新安装的 OS。  

#### <a name="os-upgrade-package-actions"></a>OS 升级包操作

使用 OS 升级包时，“应用操作系统映像”步骤将执行以下操作：  

1. 删除目标卷中的所有内容，\_SMSTSUserStatePath 变量指定的文件夹中的文件除外。  

2. 准备答案文件：  

    1. 使用 Configuration Manager 创建的标准值创建全新的答案文件。  

    2. 合并用户提供的答案文件中的所有值。  

### <a name="properties-for-apply-os-image"></a>“应用操作系统映像”的属性

在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="apply-operating-system-from-a-captured-image"></a>从捕获的映像应用操作系统

安装捕获的 OS 映像。 选择“浏览”以打开“选择包”对话框。 然后选择要安装的现有映像包。 如果指定的映像包关联了多个映像，请从下拉列表选择将用于此部署的关联映像。 可以通过选中每个现有映像来查看有关该映像的基本信息。  

#### <a name="apply-operating-system-image-from-an-original-installation-source"></a>从原始安装源应用操作系统映像

使用 OS 升级包安装 OS，这也是原始安装源。 选择“浏览”以打开“选择操作系统升级包”对话框 。 然后选择要使用的现有 OS 升级包。 可以通过选中每个现有映像源来查看有关该映像的基本信息。 关联映像源属性显示在对话框底部的结果窗格中。 如果指定的包关联了多个版本，请使用下拉列表选择要使用的“版本”。  

> [!NOTE]  
> 操作系统升级包主要用于就地升级，而不用于 Windows 的全新安装。 在部署 Windows 的全新安装时，请使用“从捕获的映像应用操作系统”选项和安装源文件中的 install.wim 。
>
> 仍支持通过操作系统升级包来部署 Windows 的新安装，但这取决于驱动程序是否与此方法兼容。 从 OS 升级包安装 Windows 时，仍在 Windows PE 中安装驱动程序，而不仅仅是在 Windows PE 中注入。 在 Windows PE 中安装时，某些驱动程序与之不兼容。
>
> 如果在 Windows PE 中安装时驱动程序不兼容，则使用原始安装源文件中的 install.wim 创建操作系统映像 。 然后改为通过“从捕获的映像应用操作系统”选项部署。

#### <a name="use-an-unattended-or-sysprep-answer-file-for-a-custom-installation"></a>使用无人参与或 Sysprep 答案文件进行自定义安装

使用此选项提供 Windows 安装程序答案文件（unattend.xml、unattend.txt 或 sysprep.inf），取决于 OS 版本和安装方法。 你指定的文件可以包含 Windows 答案文件支持的任何标准的配置选项。 例如，可以使用它指定默认的 Internet Explorer 主页。 指定包含答案文件的包以及包中文件的关联路径。  

> [!NOTE]  
> 你提供的 Windows 安装程序答案文件可以包含形式为 `%varname%` 的嵌入任务序列变量，其中 varname 是指变量的名称。 “安装 Windows 和 ConfigMgr”步骤将变量字符串替换为实际变量值。 unattend.xml 答案文件的仅数字字段中不能使用这些嵌入的任务序列变量。  

如果不提供 Windows 安装程序答案文件，此任务序列将自动生成一个答案文件。  

#### <a name="destination"></a>目标

配置下列选项之一：  

- **下一个可用分区**：使用此任务序列中尚未被“应用操作系统”或“应用数据映像”步骤作为目标的下一个顺序分区 。  

- **特定磁盘和分区**：选择“磁盘”编号（从 0 开始）和“分区”编号（从 1 开始） 。  

- **特定逻辑驱动器号**：指定 Windows PE 分配给分区的“驱动器号”。 此驱动器号可不同于新部署的 OS 分配的驱动器号。  

- **变量中存储的逻辑驱动器号**：指定包含 Windows PE 分配给分区的驱动器号的任务序列变量。 对于“格式化磁盘并分区”任务序列步骤，此变量通常在“分区属性”对话框的“高级”部分中设置。  

### <a name="options-for-apply-os-image"></a>“应用操作系统映像”的选项

除默认选项外，还可配置此任务序列步骤的“选项”选项卡上的以下其他设置：  

#### <a name="access-content-directly-from-the-distribution-point"></a>直接从分发点访问内容

将任务序列配置为直接从分发点访问 OS 映像。 例如，在部署操作系统到存储容量有限的嵌入式设备时使用此选项。 选择此选项后，同时在 OS 映像属性的“数据访问”选项卡上配置包共享设置。  

> [!NOTE]  
> 此设置替代在“部署软件向导”的“分发点”页上配置的部署选项 。 此替代仅适用于此步骤指定的 OS 映像，而非所有任务序列内容。  

> [!IMPORTANT]  
> 为了最大限度地确保安全，强烈建议不要选择此选项。 此选项主要用于存储容量有限的设备。 此选项并不意味着有助于提高任务序列的速度。 选择此选项后，不会为操作系统包验证包哈希。 因此无法确保包完整性，因为具有管理权限的用户可能改变或篡改包内容。



## <a name="apply-windows-settings"></a><a name="BKMK_ApplyWindowsSettings"></a>应用 Windows 设置

使用此步骤配置目标计算机的 Windows 设置。 任务序列将这些值存储在相应的答案文件中。 Windows 安装程序在“安装 Windows 和 ConfigMgr”步骤过程中使用该答案文件。  

此任务序列步骤仅可在 Windows PE 中运行。 它不会在完整的 OS 中运行。  

选择任务序列编辑器中的“添加”，选择“设置”，然后选择“应用 Windows 设置”以添加此步骤。

### <a name="variables-for-apply-windows-settings"></a>“应用 Windows 设置”的变量

在此步骤中使用以下任务序列变量：  

- [OSDComputerName](task-sequence-variables.md#OSDComputerName-input)  
- [OSDLocalAdminPassword](task-sequence-variables.md#OSDLocalAdminPassword)  
- [OSDProductKey](task-sequence-variables.md#OSDProductKey)  
- [OSDRandomAdminPassword](task-sequence-variables.md#OSDRandomAdminPassword)  
- [OSDRegisteredOrgName](task-sequence-variables.md#OSDRegisteredOrgName-input)  
- [OSDRegisteredUserName](task-sequence-variables.md#OSDRegisteredUserName)  
- [OSDServerLicenseConnectionLimit](task-sequence-variables.md#OSDServerLicenseConnectionLimit)  
- [OSDServerLicenseMode](task-sequence-variables.md#OSDServerLicenseMode)  
- [OSDTimeZone](task-sequence-variables.md#OSDTimeZone-input)  
- [OSDWindowsSettingsInputLocale](task-sequence-variables.md#OSDWindowsSettingsInputLocale)
- [OSDWindowsSettingsSystemLocale](task-sequence-variables.md#OSDWindowsSettingsSystemLocale)
- [OSDWindowsSettingsUILanguage](task-sequence-variables.md#OSDWindowsSettingsUILanguage)
- [OSDWindowsSettingsUILanguageFallback](task-sequence-variables.md#OSDWindowsSettingsUILanguageFallback)
- [OSDWindowsSettingsUserLocale](task-sequence-variables.md#OSDWindowsSettingsUserLocale)

### <a name="cmdlets-for-apply-windows-settings"></a>“应用 Windows 设置”的 cmdlet

使用以下 PowerShell cmdlet 管理此步骤：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyWindowsSetting](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepApplyWindowsSetting?view=sccm-ps)
- [New-CMTSStepApplyWindowsSetting](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepApplyWindowsSetting?view=sccm-ps)
- [Remove-CMTSStepApplyWindowsSetting](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepApplyWindowsSetting?view=sccm-ps)
- [Set-CMTSStepApplyWindowsSetting](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepApplyWindowsSetting?view=sccm-ps)

### <a name="properties-for-apply-windows-settings"></a>“应用 Windows 设置”的属性

在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="user-name"></a>用户名

指定与目标计算机关联的已注册用户名。 此值可被“捕获 Windows 设置”任务序列步骤所捕获的值替代。  

#### <a name="organization-name"></a>组织名称

指定与目标计算机关联的已注册组织名称。 此值可被“捕获 Windows 设置”任务序列步骤所捕获的值替代。  

#### <a name="product-key"></a>产品密钥  

指定用于目标计算机上的 Windows 安装的产品密钥。  

#### <a name="server-licensing"></a>服务器授权

指定授权模式。

- 选择“每服务器”或“每用户”作为授权模式。  
- 如果选择“每服务器”，则还需要指定每个许可协议将允许的最大连接数。  
- 如果目标计算机不是服务器或你不想指定授权模式，请选择“不指定”。  

#### <a name="maximum-connections"></a>最大连接数

> [!NOTE]
> 此设置仅适用于不再受支持的旧版本的 Windows。<!-- #4833 -->

#### <a name="randomly-generate-the-local-administrator-password-and-disable-the-account-on-all-supported-platforms-recommended"></a>随机生成本地管理员密码并在所有支持的平台上禁用帐户（推荐）  

选择此选项，将本地管理员密码设为随机生成的字符串。 此选项还会对支持此功能的平台禁用本地管理员帐户。  

#### <a name="enable-the-account-and-specify-the-local-administrator-password"></a>启用帐户并指定本地管理员密码  

选择此选项，以使用指定密码启用本地管理员帐户。 在“密码”行上输入密码，并在“确认密码”行上确认密码。  

#### <a name="time-zone"></a>时区

指定要在目标计算机上配置的时区。 此值可被“捕获 Windows 设置”任务序列步骤所捕获的值替代。  

#### <a name="language-settings"></a>语言设置

<!--5411057, 5138936-->

自版本 1910 起，在 OS 部署期间控制语言配置。 如果已应用这些语言设置，则此更改可帮助简化 OS 部署任务序列。 无需对每种语言使用多个步骤或单独的脚本，只需对该步骤且具有该语言条件的每种语言使用一个实例。

配置下列设置：

- 输入区域设置（默认键盘布局）
- 系统区域设置
- UI 语言
- UI 语言回退
- 用户区域设置

有关这些 Windows 安装程序答案文件值的详细信息，请参阅 [Microsoft-Windows-International-Core](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core)。

> [!NOTE]
> 如果你创建自定义 Windows 安装程序答案文件 (unattend.xml)，此步骤会覆盖任何现有值。 若要自动化这些设置的动态过程，请使用相关的任务序列变量。 例如，[OSDWindowsSettingsInputLocale](task-sequence-variables.md#OSDWindowsSettingsInputLocale)。 

## <a name="auto-apply-drivers"></a><a name="BKMK_AutoApplyDrivers"></a>自动应用驱动程序

使用此步骤匹配并安装驱动程序，作为 OS 部署的一部分。  

> [!IMPORTANT]  
> 独立媒体无法使用“自动应用驱动程序”步骤。 此方案中，任务序列未连接到 Configuration Manager 站点。  

此任务序列步骤仅可在 Windows PE 中运行。 它不会在完整的 OS 中运行。

选择任务序列编辑器中的“添加”，选择“驱动程序”，然后选择“自动应用驱动程序”以添加此步骤。

> [!TIP]
> 有关 Configuration Manager 中的驱动程序的概述，请参阅[使用任务序列安装驱动程序](../get-started/manage-drivers.md#BKMK_TSDrivers)。

### <a name="behaviors-for-auto-apply-drivers"></a>“自动应用驱动程序”的行为

“自动应用驱动程序”任务序列步骤执行以下操作：  

1. 扫描硬件并为系统上存在的所有设备查找即插即用 ID。  

2. 将设备列表以及设备的即插即用 ID 发送到管理点。 管理点从驱动程序目录中为每个硬件设备返回兼容的驱动程序列表。 列表包括所有嵌入的驱动程序，而不管它们位于哪个驱动程序包，还包括具有指定驱动程序类别标记的驱动程序。  

3. 对于每个硬件设备，任务序列会选择最适合的驱动程序。 此驱动程序适用于已部署的 OS，位于可访问的分发点。  

4. 任务序列从分发点下载选定的驱动程序，并将驱动程序暂存于目标 OS 上。  

    1. 在使用 OS 映像时，任务序列将驱动程序置于 OS 驱动程序存储区。  

    2. 当使用 OS 升级包作为原始安装源，任务序列会使用驱动程序的位置来配置 Windows 安装程序。  

5. 在任务序列的“安装 Windows 和 ConfigMgr”步骤过程中，Windows 安装程序会查找此步骤暂存的驱动程序。  

### <a name="variables-for-auto-apply-drivers"></a>“自动应用驱动程序”的变量

在此步骤中使用以下任务序列变量：  

- [OSDAutoApplyDriverBestMatch](task-sequence-variables.md#OSDAutoApplyDriverBestMatch)  
- [OSDAutoApplyDriverCategoryList](task-sequence-variables.md#OSDAutoApplyDriverCategoryList)  
- [SMSTSDriverRequestConnectTimeOut](task-sequence-variables.md#SMSTSDriverRequestConnectTimeOut)  
- [SMSTSDriverRequestReceiveTimeOut](task-sequence-variables.md#SMSTSDriverRequestReceiveTimeOut)  
- [SMSTSDriverRequestResolveTimeOut](task-sequence-variables.md#SMSTSDriverRequestResolveTimeOut)  
- [SMSTSDriverRequestSendTimeOut](task-sequence-variables.md#SMSTSDriverRequestSendTimeOut)  

### <a name="cmdlets-for-auto-apply-drivers"></a>“自动应用驱动程序”的 cmdlet

使用以下 PowerShell cmdlet 管理此步骤：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepAutoApplyDriver](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepAutoApplyDriver?view=sccm-ps)
- [New-CMTSStepAutoApplyDriver](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepAutoApplyDriver?view=sccm-ps)
- [Remove-CMTSStepAutoApplyDriver](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepAutoApplyDriver?view=sccm-ps)
- [Set-CMTSStepAutoApplyDriver](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepAutoApplyDriver?view=sccm-ps)

### <a name="properties-for-auto-apply-drivers"></a>“自动应用驱动程序”的属性

在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="install-only-the-best-matched-compatible-drivers"></a>仅安装最匹配的兼容驱动程序

指定任务序列步骤为检测到的每个硬件设备仅安装最匹配的驱动程序。  

#### <a name="install-all-compatible-drivers"></a>安装所有兼容的驱动程序

任务序列安装与每个检测到的硬件设备兼容的所有驱动程序。 然后，Windows 安装程序选择最适合的驱动程序。 此选项占用更多网络带宽和磁盘空间。 任务序列下载更多驱动程序，但 Windows 可选择更好的驱动程序。  

#### <a name="consider-drivers-from-all-categories"></a>考虑所有类别的驱动程序

任务序列搜索所有驱动程序类别，寻找适合的设备驱动程序。  

#### <a name="limit-driver-matching-to-only-consider-drivers-in-selected-categories"></a>将驱动程序匹配限制为仅考虑所选类别的驱动程序

任务序列在指定驱动程序类别中搜索，寻找适合的设备驱动程序。  

如果选择多个类别，则会返回存在于任何类别中的所有匹配驱动程序。 它相当于 `OR` 操作。<!-- SCCMDocs issue 851 -->

#### <a name="do-unattended-installation-of-unsigned-drivers-on-versions-of-windows-where-this-is-allowed"></a>在 Windows 版本上对未签名的驱动程序执行允许的无人参与安装

此选项允许 Windows 安装没有数字签名的驱动程序。  

> [!IMPORTANT]  
> 此选项不适用于不能配置驱动程序签名策略的操作系统。  



## <a name="capture-network-settings"></a><a name="BKMK_CaptureNetworkSettings"></a>捕获网络设置

使用此步骤从运行该任务序列的计算机捕获 Microsoft 网络设置。 任务序列将这些设置保存在任务序列变量中。 这些设置替代“应用网络设置”步骤中配置的默认设置。  

此任务序列步骤仅可在完整的 OS 中运行。 不可在 Windows PE 中运行。  

选择任务序列编辑器中的“添加”，选择“设置”，然后选择“捕获网络设置”以添加此步骤。

### <a name="variables-for-capture-network-settings"></a>“捕获网络设置”的变量

在此步骤中使用以下任务序列变量：  

- [OSDMigrateAdapterSettings](task-sequence-variables.md#OSDMigrateAdapterSettings)  
- [OSDMigrateNetworkMembership](task-sequence-variables.md#OSDMigrateNetworkMembership)  

### <a name="cmdlets-for-capture-network-settings"></a>“捕获网络设置”的 cmdlet

使用以下 PowerShell cmdlet 管理此步骤：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepCaptureNetworkSettings](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepCaptureNetworkSettings?view=sccm-ps)
- [New-CMTSStepCaptureNetworkSettings](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepCaptureNetworkSettings?view=sccm-ps)
- [Remove-CMTSStepCaptureNetworkSettings](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepCaptureNetworkSettings?view=sccm-ps)
- [Set-CMTSStepCaptureNetworkSettings](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepCaptureNetworkSettings?view=sccm-ps)

### <a name="properties-for-capture-network-settings"></a>“捕获网络设置”的属性

在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="migrate-domain-and-workgroup-membership"></a>迁移域和工作组成员身份

捕获目标计算机的域和工作组成员身份信息。  

#### <a name="migrate-network-adapter-configuration"></a>迁移网络适配器配置

捕获目标计算机的网络适配器配置。 它捕获以下信息：

- 全局网络设置  
- 适配器数  
- 以下网络设置与每个适配器相关联：DNS、WINS、IP 和端口筛选器



## <a name="capture-operating-system-image"></a><a name="BKMK_CaptureOperatingSystemImage"></a>捕获操作系统映像

此步骤从引用计算机中捕获一个或多个映像。 任务序列在指定的网络共享中创建 Windows 映像 (.wim) 文件。 随后可以使用“添加操作系统映像包”向导将此映像导入 Configuration Manager 中，以便用于基于映像的 OS 部署。  

Configuration Manager 将引用计算机上的每个卷（驱动器）捕获为 .wim 文件中的单独映像。 如果引用计算机有多个卷，则生成的 .wim 文件对于每个卷将包含单独的映像。 此步骤仅捕获格式化为 NTFS 或 FAT32 的卷。 其他格式的卷和 USB 卷会被忽略。  

引用计算机上安装的 OS 必须是 Configuration Manager 支持的 Windows 版本。 使用 SysPrep 工具在引用计算机上准备 OS。 安装的 OS 卷和启动卷必须是相同的卷。  

指定对选定网络共享具有写入权限的帐户。 有关此捕获 OS 映像帐户的详细信息，请参阅[帐户](../../core/plan-design/hierarchy/accounts.md#capture-os-image-account)。

此任务序列步骤仅可在 Windows PE 中运行。 它不会在完整的 OS 中运行。

选择任务序列编辑器中的“添加”，选择“映像”，然后选择“捕获操作系统映像”以添加此步骤。

### <a name="variables-for-capture-os-image"></a>“捕获操作系统映像”的变量

在此步骤中使用以下任务序列变量：  

- [OSDCaptureAccount](task-sequence-variables.md#OSDCaptureAccount)  
- [OSDCaptureAccountPassword](task-sequence-variables.md#OSDCaptureAccountPassword)  
- [OSDCaptureDestination](task-sequence-variables.md#OSDCaptureDestination)  
- [OSDImageCreator](task-sequence-variables.md#OSDImageCreator)  
- [OSDImageDescription](task-sequence-variables.md#OSDImageDescription)  
- [OSDImageVersion](task-sequence-variables.md#OSDImageVersion)  
- [OSDTargetSystemRoot](task-sequence-variables.md#OSDTargetSystemRoot-input)  

### <a name="cmdlets-for-capture-os-image"></a>“捕获操作系统映像”的 cmdlet

使用以下 PowerShell cmdlet 管理此步骤：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepCaptureSystemImage](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepCaptureSystemImage?view=sccm-ps)
- [New-CMTSStepCaptureSystemImage](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepCaptureSystemImage?view=sccm-ps)
- [Remove-CMTSStepCaptureSystemImage](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepCaptureSystemImage?view=sccm-ps)
- [Set-CMTSStepCaptureSystemImage](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepCaptureSystemImage?view=sccm-ps)

### <a name="properties-for-capture-os-image"></a>“捕获操作系统映像”的属性

在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="target"></a>目标  

Configuration Manager 在存储捕获的 OS 映像时所使用位置的文件系统路径。  

#### <a name="description"></a>说明  

存储在映像文件中的捕获的 OS 映像的用户定义的描述（可选）。  

#### <a name="version"></a>版本  

向捕获的 OS 映像分配的用户定义的版本号（可选）。 此值可以是字母和数字的任意组合。 它存储在映像文件中。  

#### <a name="created-by"></a>创建者  

创建 OS 映像的用户的名称（可选）。 它存储在映像文件中。  

#### <a name="capture-operating-system-image-account"></a>捕获操作系统映像帐户  

输入对指定的网络共享具有访问权限的 Windows 帐户。 选择“设置”以指定 Windows 帐户的名称。  



## <a name="capture-user-state"></a><a name="BKMK_CaptureUserState"></a>捕获用户状态

此步骤使用用户状态迁移工具 (USMT) 从运行该任务序列的计算机捕获用户状态和设置。 此任务序列步骤与“还原用户状态”任务序列步骤一起使用。 此步骤终使用由 Configuration Manager 生成并管理的加密密钥加密 USMT 状态存储。  

有关部署操作系统时管理用户状态的详细信息，请参阅[管理用户状态](../get-started/manage-user-state.md)。  

如果要将用户状态设置保存到状态迁移点或从其还原设置，可以将此步骤与“请求状态存储”和“发布状态存储”步骤一起使用。  

此步骤提供对最常用 USMT 选项的受限子网的控制。 使用 OSDMigrateAdditionalCaptureOptions 任务序列变量指定其他命令行选项。  

此任务序列步骤仅可在 Windows PE 中运行。 它不会在完整的 OS 中运行。  

选择任务序列编辑器中的“添加”，选择“用户状态”，然后选择“捕获用户状态”以添加此步骤。

### <a name="variables-for-capture-user-state"></a>“捕获用户状态”的变量

在此步骤中使用以下任务序列变量：  

- [_OSDMigrateUsmtPackageID](task-sequence-variables.md#OSDMigrateUsmtPackageID)  
- [OSDMigrateAdditionalCaptureOptions](task-sequence-variables.md#OSDMigrateAdditionalCaptureOptions)  
- [OSDMigrateConfigFiles](task-sequence-variables.md#OSDMigrateConfigFiles)  
- [OSDMigrateContinueOnLockedFiles](task-sequence-variables.md#OSDMigrateContinueOnLockedFiles)  
- [OSDMigrateEnableVerboseLogging](task-sequence-variables.md#OSDMigrateEnableVerboseLogging)  
- [OSDMigrateMode](task-sequence-variables.md#OSDMigrateMode)  
- [OSDMigrateSkipEncryptedFiles](task-sequence-variables.md#OSDMigrateSkipEncryptedFiles)  
- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)  

### <a name="cmdlets-for-capture-user-state"></a>“捕获用户状态”的 cmdlet

使用以下 PowerShell cmdlet 管理此步骤：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepCaptureUserState](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepCaptureUserState?view=sccm-ps)
- [New-CMTSStepCaptureUserState](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepCaptureUserState?view=sccm-ps)
- [Remove-CMTSStepCaptureUserState](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepCaptureUserState?view=sccm-ps)
- [Set-CMTSStepCaptureUserState](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepCaptureUserState?view=sccm-ps)

### <a name="properties-for-capture-user-state"></a>“捕获用户状态”的属性

在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="user-state-migration-tool-package"></a>用户状态迁移工具包

指定包含用户状态迁移工具 (USMT) 的包。 任务序列使用此版 USMT 捕获用户状态和设置。 此包不需要程序。 指定包含 32 位或 64 位版本 USMT 的包。 USMT 的体系结构取决于任务序列将从其中捕获状态的 OS 的体系结构。  

#### <a name="capture-all-user-profiles-with-standard-options"></a>使用标准选项捕获所有用户配置文件

迁移所有用户配置文件信息。 此选项为默认设置。  

如果选择此选项，但在“还原用户状态”步骤中未选择“还原本地计算机用户配置文件”，任务序列将失败。 Configuration Manager 无法在不向新帐户分配密码的情况下迁移这些帐户。

如果使用“新建任务序列”向导的“安装现有映像包”选项，生成的任务序列将默认为“使用标准选项捕获所有用户配置文件”  。 此默认任务序列不会选择“还原本地计算机用户配置文件”选项，也不会选择非域用户帐户。  

选择“还原本地计算机用户配置文件”，并为要迁移的帐户提供密码。 在手动创建的任务序列中，此设置可在“还原用户状态”步骤下找到。 在由新建任务序列向导创建的任务序列中，可在步骤“还原用户文件和设置”向导页面下方找到此设置。  

如果没有本地用户帐户，此设置不适用。  

#### <a name="customize-how-user-profiles-are-captured"></a>自定义如何捕获用户配置文件

选择此选项以指定迁移的自定义配置文件。 选择“文件”以选择 USMT 要在此步骤中使用的配置文件。 指定一个自定义 .xml 文件，该文件包含定义要迁移的用户状态文件的规则。  

#### <a name="click-here-to-select-configuration-files"></a>单击此处选择配置文件

选择此选项以便在想要用于捕获用户配置文件的 USMT 包中选择配置文件。 选择“文件”按钮以启动“配置文件”对话框。 要指定配置文件，请在“文件名”行中输入文件名称并选择“添加”按钮。  

#### <a name="enable-verbose-logging"></a>启用详细日志记录

启用此选项以生成更详细的日志文件信息。 捕获状态时，任务序列默认生成日志 ScanState.log 并存储在任务序列日志文件夹 `%WinDir%\ccm\logs` 中。  

#### <a name="skip-files-using-encrypted-file-system"></a>使用加密文件系统跳过文件

启用此选项可跳过捕获使用加密文件系统 (EFS) 加密过的文件。 这些文件包括用户配置文件。 根据 OS 和 USMT 版本，还原后可能无法读取加密文件。 有关详细信息，请参阅 USMT 文档。  

#### <a name="copy-by-using-file-system-access"></a>使用文件系统访问进行复制

启用此选项以指定任何以下设置：  

- **如果无法捕获某些文件则继续**：启用此设置以在无法捕获某些文件时继续迁移过程。 如果禁用此选项，且无法捕获某个文件，此步骤将失败。 默认情况下会启用此选项。  

- **通过使用链接而不是通过复制文件以本地方式进行捕获**：启用此设置以使用 NTFS 硬链接来捕获文件。  

    有关使用硬链接迁移数据的详细信息，请参阅 [硬链接迁移存储](https://docs.microsoft.com/windows/deployment/usmt/usmt-hard-link-migration-store)。  

- **在脱机模式下进行捕获（仅 Windows PE）** ：启用此设置可在 Windows PE 而不是整个 OS 中捕获用户状态。  

#### <a name="capture-by-using-volume-copy-shadow-services-vss"></a>使用卷影复制服务 (VSS) 进行捕获

通过此选项，你可捕获文件，即使文件被锁定由其他应用程序编辑也无妨。  



## <a name="capture-windows-settings"></a><a name="BKMK_CaptureWindowsSettings"></a>捕获 Windows 设置

使用此步骤从运行该任务序列的计算机捕获 Windows 设置。 任务序列将这些设置保存在任务序列变量中。 这些捕获的设置将替代“应用 Windows 设置”步骤中配置的默认设置。  

此任务序列步骤在 Windows PE 或完整 OS 中运行。  

选择任务序列编辑器中的“添加”，选择“设置”，然后选择“捕获 Windows 设置”以添加此步骤。

### <a name="variables-for-capture-windows-settings"></a>“捕获 Windows 设置”的变量

在此步骤中使用以下任务序列变量：  

- [OSDComputerName](task-sequence-variables.md#OSDComputerName-output)  
- [OSDMigrateComputerName](task-sequence-variables.md#OSDMigrateComputerName)  
- [OSDMigrateRegistrationInfo](task-sequence-variables.md#OSDMigrateRegistrationInfo)  
- [OSDMigrateTimeZone](task-sequence-variables.md#OSDMigrateTimeZone)  
- [OSDRegisteredOrgName](task-sequence-variables.md#OSDRegisteredOrgName-output)  
- [OSDTimeZone](task-sequence-variables.md#OSDTimeZone-output)  

### <a name="cmdlets-for-capture-windows-settings"></a>“捕获 Windows 设置”的 cmdlet

使用以下 PowerShell cmdlet 管理此步骤：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepCaptureWindowsSettings](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepCaptureWindowsSettings?view=sccm-ps)
- [New-CMTSStepCaptureWindowsSettings](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepCaptureWindowsSettings?view=sccm-ps)
- [Remove-CMTSStepCaptureWindowsSettings](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepCaptureWindowsSettings?view=sccm-ps)
- [Set-CMTSStepCaptureWindowsSettings](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepCaptureWindowsSettings?view=sccm-ps)

### <a name="properties-for-capture-windows-settings"></a>“捕获 Windows 设置”的属性

在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="migrate-computer-name"></a>迁移计算机名称

捕获计算机的 NetBIOS 计算机名称。  

#### <a name="migrate-registered-user-and-organization-names"></a>迁移注册用户和组织名称

捕获计算机中已注册的用户和组织名称。  

#### <a name="migrate-time-zone"></a>迁移时区

捕获计算机上的时区设置。  



## <a name="check-readiness"></a><a name="BKMK_CheckReadiness"></a>检查准备情况

使用此步骤验证目标计算机是否满足指定的部署先决条件。  

选择任务序列编辑器中的“添加”，选择“常规”，然后选择“检查就绪情况”以添加此步骤。

从版本 2002 开始，此步骤包含八项新检查。 默认不会在该步骤的新实例或现有实例中选择这些新检查。<!--6005561--> 有关每项检查的详细信息，请参阅下文特定部分。

- **当前操作系统的体系结构**
- **最低操作系统版本**
- **最高操作系统版本**
- **最低客户端版本**
- **当前操作系统的语言**
- 交流电源已接通
- 网络适配器已连接
  - 网络适配器不是无线网络

> [!IMPORTANT]
> 若要利用 Configuration Manager 的此项新功能，更新站点后，还请将客户端更新到最新版本。 尽管在更新站点和控制台时 Configuration Manager 控制台中会显示新功能，但只有在客户端版本也是最新版本之后，完整方案才能正常运行。

smsts.log 包含所有检查的结果。 如果一个检查失败，则任务序列引擎将继续评估其他检查。 在完成所有检查之前，该步骤不会失败。 如果至少有一个检查失败，该步骤会失败，并返回错误代码 4316。 此错误代码表示“此操作所需的资源不存在。”

### <a name="variables-for-check-readiness"></a>“检查准备情况”的变量

在此步骤中使用以下任务序列变量：  

- [_TS_CRMEMORY](task-sequence-variables.md#TSCRMEMORY)
- [_TS_CRSPEED](task-sequence-variables.md#TSCRSPEED)
- [_TS_CRDISK](task-sequence-variables.md#TSCRDISK)
- [_TS_CROSTYPE](task-sequence-variables.md#TSCROSTYPE)
- [_TS_CRARCH](task-sequence-variables.md#TSCRARCH)
- [_TS_CRMINOSVER](task-sequence-variables.md#TSCRMINOSVER)
- [_TS_CRMAXOSVER](task-sequence-variables.md#TSCRMAXOSVER)
- [_TS_CRCLIENTMINVER](task-sequence-variables.md#TSCRCLIENTMINVER)
- [_TS_CROSLANGUAGE](task-sequence-variables.md#TSCROSLANGUAGE)
- [_TS_CRACPOWER](task-sequence-variables.md#TSCRACPOWER)
- [_TS_CRNETWORK](task-sequence-variables.md#TSCRNETWORK)
- [_TS_CRWIRED](task-sequence-variables.md#TSCRWIRED)

### <a name="cmdlets-for-check-readiness"></a>“检查准备情况”的 cmdlet

使用以下 PowerShell cmdlet 管理此步骤：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPrestartCheck](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepPrestartCheck?view=sccm-ps)
- [New-CMTSStepPrestartCheck](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepPrestartCheck?view=sccm-ps)
- [Remove-CMTSStepPrestartCheck](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepPrestartCheck?view=sccm-ps)
- [Set-CMTSStepPrestartCheck](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepPrestartCheck?view=sccm-ps)

### <a name="properties-for-check-readiness"></a>“检查准备情况”的属性

在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="minimum-memory-mb"></a>最小内存 (MB)

验证内存量（以兆字节 (MB) 计算），是满足还是超过指定的量。 步骤默认启用此设置。  

#### <a name="minimum-processor-speed-mhz"></a>最低处理器速度( MHz)  

验证处理器的速度（以兆赫兹 (MHz) 计算），是满足还是超过指定的量。 步骤默认启用此设置。  

#### <a name="minimum-free-disk-space-mb"></a>最小可用磁盘空间 (MB)

验证可用磁盘空间（以兆字节 (MB) 计算），是满足还是超过指定的量。  

#### <a name="current-os-to-be-refreshed-is"></a>要刷新的当前操作系统为

验证目标计算机上安装的 OS 是否满足指定的要求。 此步骤将该设置默认设置为“客户端”。  

#### <a name="architecture-of-current-os"></a>当前操作系统的体系结构

从版本 2002 开始，验证当前操作系统是 32 位还是 64 位 。

#### <a name="minimum-os-version"></a>最低操作系统版本

从版本 2002 开始，验证当前操作系统运行的版本是否高于指定版本。 使用主要版本、次要版本和内部版本号指定版本。 例如，`10.0.16299`。

#### <a name="maximum-os-version"></a>最高操作系统版本

从版本 2002 开始，验证当前操作系统运行的版本是否低于指定版本。 使用主要版本、次要版本和内部版本号指定版本。 例如，`10.0.18356`。

#### <a name="minimum-client-version"></a>最低客户端版本

从版本 2002 开始，验证 Configuration Manager 客户端版本是否至少为指定版本。 采用以下格式指定客户端版本：`5.00.8913.1005`。

#### <a name="language-of-current-os"></a>当前操作系统的语言

从版本 2002 开始，验证当前操作系统的语言是否与指定的语言匹配。 选择语言名称，该步骤会比较关联的语言代码。 此检查将你选择的语言与客户端上 **Win32_OperatingSystem** WMI 类的 **OSLanguage** 属性进行比较。

#### <a name="ac-power-plugged-in"></a>交流电源已接通

从版本 2002 开始，验证设备是否已接通电源，而不是接通电池。

#### <a name="network-adapter-connected"></a>网络适配器已连接

从版本 2002 开始，验证设备是否具有已连接到网络的网络适配器。 还可以选择依赖关系检查来验证并确保**网络适配器不是无线网络适配器**。

### <a name="options-for-check-readiness"></a>“检查准备情况”的选项

> [!NOTE]  
> 如果启用此步骤的“选项”选项卡上的“出错时继续”，则仅记录就绪情况检查结果 。 如果检查失败，任务序列不会停止。  



## <a name="connect-to-network-folder"></a><a name="BKMK_ConnectToNetworkFolder"></a>连接到网络文件夹

使用此步骤创建与共享网络文件夹的连接。  

此任务序列步骤在完整 OS 或 Windows PE 中运行。  

选择任务序列编辑器中的“添加”，选择“常规”，然后选择“连接到网络文件夹”以添加此步骤。

### <a name="variables-for-connect-to-network-folder"></a>“连接到网络文件夹”的变量

在此步骤中使用以下任务序列变量：  

- [SMSConnectNetworkFolderAccount](task-sequence-variables.md#SMSConnectNetworkFolderAccount)  
- [SMSConnectNetworkFolderDriveLetter](task-sequence-variables.md#SMSConnectNetworkFolderDriveLetter)  
- [SMSConnectNetworkFolderPassword](task-sequence-variables.md#SMSConnectNetworkFolderPassword)  
- [SMSConnectNetworkFolderPath](task-sequence-variables.md#SMSConnectNetworkFolderPath)  

### <a name="cmdlets-for-connect-to-network-folder"></a>“连接到网络文件夹”的 cmdlet

使用以下 PowerShell cmdlet 管理此步骤：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepConnectNetworkFolder](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConnectNetworkFolder?view=sccm-ps)
- [New-CMTSStepConnectNetworkFolder](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepConnectNetworkFolder?view=sccm-ps)
- [Remove-CMTSStepConnectNetworkFolder](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepConnectNetworkFolder?view=sccm-ps)
- [Set-CMTSStepConnectNetworkFolder](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepConnectNetworkFolder?view=sccm-ps)

### <a name="properties-for-connect-to-network-folder"></a>“连接到网络文件夹”的属性

在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="path"></a>路径  

选择“浏览”以指定网络文件夹路径。 使用格式 `\\server\share`。

#### <a name="drive"></a>驱动器  

选择分配给此连接的本地驱动器号。

#### <a name="account"></a>帐户

选择“设置”以指定有权连接到此网络文件夹的用户帐户。 有关任务序列网络文件夹连接帐户的详细信息，请参阅[帐户](../../core/plan-design/hierarchy/accounts.md#task-sequence-network-folder-connection-account)。



## <a name="disable-bitlocker"></a><a name="BKMK_DisableBitLocker"></a>禁用 BitLocker

使用此步骤，在当前 OS 驱动器或指定驱动器上禁用 BitLocker 加密。 此操作使得密钥保护程序在硬盘驱动器上以明文形式显示。 但是不会解密该驱动器的内容。 此操作几乎顷刻就能完成。  

> [!NOTE]  
> BitLocker 驱动器加密提供磁盘卷内容的低级加密。  

如果加密了多个驱动器，则需在任何数据驱动器上禁用 BitLocker，才能在 OS 驱动器上禁用 BitLocker。  

此步骤仅可在完整的 OS 中运行。 不可在 Windows PE 中运行。  

选择任务序列编辑器中的“添加”，选择“磁盘”，然后选择“禁用 BitLocker”以添加此步骤。

### <a name="variables-for-disable-bitlocker"></a>“禁用 BitLocker”的变量

自版本 1906 起，对此步骤使用以下任务序列变量：  

- [OSDBitLockerRebootCount](task-sequence-variables.md#OSDBitLockerRebootCount)  
- [OSDBitLockerRebootCountOverride](task-sequence-variables.md#OSDBitLockerRebootCountOverride)  

### <a name="cmdlets-for-disable-bitlocker"></a>“禁用 BitLocker”的 cmdlet

使用以下 PowerShell cmdlet 管理此步骤：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepDisableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepDisableBitLocker?view=sccm-ps)
- [New-CMTSStepDisableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepDisableBitLocker?view=sccm-ps)
- [Remove-CMTSStepDisableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepDisableBitLocker?view=sccm-ps)
- [Set-CMTSStepDisableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepDisableBitLocker?view=sccm-ps)

### <a name="properties-for-disable-bitlocker"></a>“禁用 BitLocker”的属性

在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="current-operating-system-drive"></a>当前操作系统驱动器

在当前 OS 驱动器上禁用 BitLocker。  

#### <a name="specific-drive"></a>特定驱动器  

在特定驱动器上禁用 BitLocker。 使用下拉列表指定禁用 BitLocker 的驱动器。  

#### <a name="resume-protection-after-windows-has-been-restarted-the-specified-number-of-times"></a>在 Windows 重启达指定次数后恢复保护

<!-- 4512937 -->
从版本 1906 开始，使用此选项可指定禁用 BitLocker 的重启次数。 将值设置为 1（默认值）和 15 之间，而不是添加此步骤的多个实例。

可以使用任务序列变量 [OSDBitLockerRebootCount](task-sequence-variables.md#OSDBitLockerRebootCount) 和 [OSDBitLockerRebootCountOverride](task-sequence-variables.md#OSDBitLockerRebootCountOverride) 设置和修改此行为。


## <a name="download-package-content"></a><a name="BKMK_DownloadPackageContent"></a>下载包内容

使用此步骤下载以下任何包类型：  

- OS 映像  
- OS 升级包  
- 驱动程序包  
- 包  
- 启动印象<sup>[注释 1](#bkmk_note1)</sup>  

此步骤适用于任务序列，从而在以下方案中升级 OS：  

- 若要使用可同时用于 x86 平台和 x64 平台的单一升级任务序列。 包括“准备升级”组中的两个“下载包内容”步骤 。 在“选项”选项卡上指定条件，以检测客户端体系结构并仅下载适当的 OS 升级包。 配置每个“下载包内容”步骤，使其使用相同的变量。 将该变量用于“升级操作系统”步骤中的媒体路径。  

- 若要动态下载适用的驱动程序包，请使用两个“下载包内容”步骤以及检测每个驱动程序包的相应硬件类型的条件。 配置每个“下载包内容”步骤，使其使用相同的变量。 将该变量用于“升级操作系统”步骤的驱动程序部分中的“预留内容”变量 。  

> [!NOTE]  
> 在部署包含此步骤的任务序列时，请勿在部署软件向导的“分发点”页上为“部署选项”选择“在启动任务序列之前在本地下载所有内容”或“直接从分发点访问内容”。  

此步骤在完整 OS 或 Windows PE 中运行。 Windows PE 中不提供将包保存在 Configuration Manager 客户端缓存中的选项。

> [!NOTE]  
> 不支持将“下载包内容”任务用于独立媒体。 有关详细信息，请参阅[不支持用于独立媒体的操作](../deploy-use/create-stand-alone-media.md#unsupported-actions-for-stand-alone-media)。  

选择任务序列编辑器中的“添加”，选择“软件”，然后选择“下载包内容”以添加此步骤。

### <a name="cmdlets-for-download-package-content"></a>“下载包内容”的 cmdlet

使用以下 PowerShell cmdlet 管理此步骤：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepDownloadPackageContent](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepDownloadPackageContent?view=sccm-ps)
- [New-CMTSStepDownloadPackageContent](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepDownloadPackageContent?view=sccm-ps)
- [Remove-CMTSStepDownloadPackageContent](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepDownloadPackageContent?view=sccm-ps)
- [Set-CMTSStepDownloadPackageContent](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepDownloadPackageContent?view=sccm-ps)

### <a name="properties-for-download-package-content"></a>“下载包内容”的属性

在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="select-package"></a>选择包  

选择图标并选择要下载的包。 选择一个包后，再次选择该图标以选择另一个包。  

#### <a name="place-into-the-following-location"></a>置于下列位置

选择将包保存在下列位置之一：  

- **任务序列工作目录**：此位置也称为任务序列缓存。  

- **Configuration Manager 客户端缓存**：使用此选项可在客户端缓存中存储内容。 默认情况下，此路径为 `%WinDir%\ccmcache`。  

- **自定义路径**：任务序列引擎首先会将包下载到任务序列工作目录。 然后将内容移动到指定的路径。 任务序列引擎会将包 ID 附加到路径中。  

#### <a name="save-path-as-a-variable"></a>将路径另存为一个变量

将包路径保存到自定义任务序列变量。 然后在另一个任务序列步骤中使用此变量。

Configuration Manager 向变量名称中添加数字后缀。 例如，指定变量 `%MyContent%` 作为自定义变量。 它是任务序列存储此步骤中所有引用内容的位置的根。 此内容可能包含多个包。 引用该变量时，添加数字后缀。 有关第一个包，请参阅 `%MyContent01%`。 在子序列步骤（如“升级操作系统”）中引用变量时，将使用 `%MyContent02%` 或 `%MyContent03%`，其中的数字对应“下载包内容”步骤罗列包的顺序。  

#### <a name="if-a-package-download-fails-continue-downloading-other-packages-in-the-list"></a>如果包下载失败，继续下载列表中的其他包

如果任务序列未能下载某个包，会开始下载列表中的下一个包。  

### <a name="note-1-use-of-boot-images-in-the-download-package-content-step"></a><a name="bkmk_note1"></a> 注释 1：在“下载包内容”步骤中使用启动映像

适用于 1910 和更高版本<!-- SCCMDocs-pr #4202 -->

如果将[任务序列属性](../deploy-use/manage-task-sequences-to-automate-tasks.md#bkmk_prop-advanced)配置为“使用启动映像”，向此步骤添加启动映像是多余的。 仅当未在任务序列的属性中指定时，才向此步骤添加启动映像。

#### <a name="example-use-case"></a>示例用例

- 用于预下载内容的单个任务序列：
  - 无关联的启动映像。
  - 仅在完整 OS 中运行，可能无用户交互。
  - 使用多个带有条件的“下载包内容”步骤。 根据特定的语言和体系结构，它会将内容下载到客户端缓存，以供 OS 部署任务序列使用。
  - 此任务序列只有一个实例，其中包含所有可能的内容选项。

- 多 OS 部署任务序列：
  - 常规 OS 部署任务序列。
  - 在它的属性中引用了启动映像。
  - 此任务序列有多个实例，根据体系结构和语言的需要使用不同的启动映像

## <a name="enable-bitlocker"></a><a name="BKMK_EnableBitLocker"></a>启用 BitLocker

使用此步骤在硬盘驱动器的至少两个分区上启用 BitLocker 加密。 第一个活动分区包含 Windows 启动代码。 另一个分区包含 OS。 启动分区必须保持为未加密状态。  

在 Windows PE 中，使用“预设置 BitLocker”步骤可在驱动器上启用 BitLocker。 有关详细信息，请参阅[预设置 BitLocker](#BKMK_PreProvisionBitLocker)。  

> [!NOTE]  
> BitLocker 驱动器加密提供磁盘卷内容的低级加密。  

此步骤仅可在完整的 OS 中运行。 不可在 Windows PE 中运行。

选择任务序列编辑器中的“添加”，选择“磁盘”，然后选择“启用 BitLocker”以添加此步骤。

当指定“仅 TPM”、“USB 上的 TPM 和启动密钥”或“TPM 和 PIN”时，受信任的平台模块 (TPM) 必须处于以下状态，然后才能运行“启用 BitLocker”步骤   ：  

- Enabled  
- 已激活  
- 允许的所有权  

此步骤将完成剩余的 TPM 初始化。 余下的步骤无需实际操作或重新启动。 “启用 BitLocker”步骤（如有必要）以透明方式完成下列剩余的 TPM 初始化步骤：  

- 创建认可密钥对  
- 创建所有者授权值和 Active Directory 的证书，后者必须已扩展为支持此值  
- 取得所有权  
- 创建存储根密钥，或在已存在但不兼容时重置  

如果希望任务序列等待“启用 BitLocker”完成驱动器加密过程，则选择“等待”选项 。 如果不选择“等待”选项，则驱动器加密过程在后台进行。 任务序列即时执行下一步骤。  

BitLocker 可用于加密单个计算机系统上的多个驱动器（OS 和数据驱动器）。 若要加密数据驱动器，首先加密 OS 驱动器并完成加密过程。 需执行此操作的原因是 OS 驱动器存储数据驱动器的密钥保护程序。 如果加密相同任务序列中的 OS 和数据驱动器，请在“启用 BitLocker”步骤中为 OS 驱动器选择“等待”选项。  

如果硬盘已加密，但 BitLocker 处于禁用状态，则“启用 BitLocker”步骤会重新启用密钥保护程序，并快速完成。 在这种情况下不需要重新加密硬盘。  

### <a name="variables-for-enable-bitlocker"></a>“启用 BitLocker”的变量

在此步骤中使用以下任务序列变量：  

- [OSDBitLockerRecoveryPassword](task-sequence-variables.md#OSDBitLockerRecoveryPassword)  
- [OSDBitLockerStartupKey](task-sequence-variables.md#OSDBitLockerStartupKey)  

### <a name="cmdlets-for-enable-bitlocker"></a>“启用 BitLocker”的 cmdlet

使用以下 PowerShell cmdlet 管理此步骤：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepEnableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepEnableBitLocker?view=sccm-ps)
- [New-CMTSStepEnableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepEnableBitLocker?view=sccm-ps)
- [Remove-CMTSStepEnableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepEnableBitLocker?view=sccm-ps)
- [Set-CMTSStepEnableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepEnableBitLocker?view=sccm-ps)

### <a name="properties-for-enable-bitlocker"></a>“启用 BitLocker”的属性

在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="choose-the-drive-to-encrypt"></a>选择要加密的驱动器

指定要加密的驱动器。 若要加密当前 OS 驱动器，请选择“当前操作系统驱动器”。 然后配置下列密钥管理选项：  

- **仅 TPM**：选择此选项，以仅使用受信任的平台模块 (TPM)。  

- **仅 USB 上的启动密钥**：选择此选项以使用存储在 USB 闪存驱动器上的启动密钥。 选择此选项时，BitLocker 将锁定正常启动过程，直至含有 BitLocker 启动密钥的 USB 设备连接到计算机。  

- **USB 上的 TPM 和启动密钥**：选择此选项以使用存储在 USB 闪存驱动器上的 TPM 和启动密钥。 选择此选项时，BitLocker 将锁定正常启动过程，直至含有 BitLocker 启动密钥的 USB 设备连接到计算机。  

- **TPM 和 PIN**：选择此选项以使用 TPM 和个人标识号 (PIN)。 当选择此选项时，BitLocker 将锁定正常启动过程，直至用户提供 PIN。  

要加密特定非 OS 数据驱动器，请选择“特定驱动器”。 然后从列表中选择驱动器。  

#### <a name="use-full-disk-encryption"></a>使用全磁盘加密

<!--SCCMDocs-pr issue 2671-->
默认情况下，此步骤仅加密驱动器上的已用空间。 建议使用此默认行为，因为它更加快速高效。 如果贵组织需要在安装期间加密整个驱动器，请启用此选项。 Windows 安装程序会等待整个驱动器加密，所需时间较长（尤其是在大型驱动器上）。

> [!TIP]
> 自版本 1910 起，可以创建和部署使用完整磁盘加密的 BitLocker 管理策略。 若要在任务序列部署 OS 后管理设备上的 BitLocker，请启用此选项。 有关详细信息，请参阅[规划 BitLocker 管理](../../protect/plan-design/bitlocker-management.md)。

#### <a name="choose-where-to-create-the-recovery-key"></a>选择要创建恢复密钥的位置

要在 Active Directory 中指定 BitLocker 创建和托管恢复密码的位置，请选择“在 Active Directory 中”。 此选项要求为 BitLocker 密钥托管扩展 Active Directory。 然后，BitLocker 可以在 Active Directory 中保存关联的恢复信息。 选择“请勿创建恢复密钥”，可以不创建密码。 创建密码为建议选项。  

#### <a name="wait-for-bitlocker-to-complete-the-drive-encryption-process-on-all-drives-before-continuing-task-sequence-execution"></a>等待 BitLocker 完成所有驱动器上的驱动器加密过程之后，继续执行任务序列

选择此选项以允许在运行任务序列中的下一步骤之前完成 BitLocker 驱动器加密。 如果选择此选项，则在用户能够登录到计算机之前，BitLocker 将对整个磁盘卷加密。  

加密大型硬盘时，加密过程可能需要数小时才能完成。 不选择此选项将允许立即处理任务序列。  



## <a name="format-and-partition-disk"></a><a name="BKMK_FormatandPartitionDisk"></a>格式化磁盘并分区

使用此步骤对目标计算机上的特定磁盘进行格式化和分区。  

> [!IMPORTANT]  
> 你为此步骤指定的所有设置均应用于单个特定磁盘。 若要对目标计算机上的另一个磁盘进行格式化和分区，则向该任务序列再添加一个“格式化磁盘并分区”步骤。  

此步骤仅可在 Windows PE 中运行。 它不会在完整的 OS 中运行。  

选择任务序列编辑器中的“添加”，选择“磁盘”，然后选择“格式化磁盘并分区”以添加此步骤。

### <a name="variables-for-format-and-partition-disk"></a>“格式化磁盘并分区”的变量

在此步骤中使用以下任务序列变量：  

- [OSDDiskIndex](task-sequence-variables.md#OSDDiskIndex)  
- [OSDGPTBootDisk](task-sequence-variables.md#OSDGPTBootDisk)  
- [OSDPartitions](task-sequence-variables.md#OSDPartitions)  
- [OSDPartitionStyle](task-sequence-variables.md#OSDPartitionStyle)  

### <a name="cmdlets-for-format-and-partition-disk"></a>“格式化磁盘并分区”的 cmdlet

使用以下 PowerShell cmdlet 管理此步骤：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPartitionDisk](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtssteppartitiondisk?view=sccm-ps)
- [New-CMTSStepPartitionDisk](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtssteppartitiondisk?view=sccm-ps)
- [Remove-CMTSStepPartitionDisk](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtssteppartitiondisk?view=sccm-ps)
- [Set-CMTSStepPartitionDisk](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtssteppartitiondisk?view=sccm-ps)

### <a name="properties-for-format-and-partition-disk"></a>“格式化磁盘并分区”的属性

在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="disk-number"></a>磁盘编号

要进行格式化的磁盘的物理磁盘编号。 该编号取决于 Windows 磁盘枚举排序。  

#### <a name="disk-type"></a>磁盘类型

要格式化的磁盘类型。 可以从下拉列表中选择两个选项：

- **标准 (MBR)** ：主启动记录  
- **GPT**：GUID 分区表  

> [!NOTE]  
> 如果将磁盘类型从“标准 (MBR)”更改为“GPT”，并且分区布局包含扩展分区，则任务序列将从布局中删除所有扩展分区和逻辑分区 。 任务序列编辑器会在更改磁盘类型前提示确认此操作。  

#### <a name="volume"></a>Volume

指定有关任务序列要创建的分区或卷的信息，包括以下属性：  

- 名称  
- 剩余磁盘空间  

若要创建新分区，请选择“新建”以启动“分区属性”对话框。 指定分区类型和大小，以及是否为启动分区。 若要修改现有分区，请选择要修改的分区，然后选择“属性”按钮。 有关如何配置硬盘分区的详细信息，请参阅下列其中一篇文章：  

- [基于 UEFI/GPT 的硬盘分区](https://docs.microsoft.com/windows-hardware/manufacture/desktop/configure-uefigpt-based-hard-drive-partitions)  
- [基于 BIOS/MBR 的硬盘分区](https://docs.microsoft.com/windows-hardware/manufacture/desktop/configure-biosmbr-based-hard-drive-partitions)  

若要删除分区，请选择分区，然后选择“删除”。  



## <a name="install-application"></a><a name="BKMK_InstallApplication"></a>安装应用程序

此步骤安装指定的应用程序或一组由任务序列变量动态列表定义的应用程序。 当任务序列运行此步骤时，应用程序安装会立即开始而不等待策略轮询间隔。  

应用程序必须符合以下条件：  

- 应用程序的部署类型必须是 Windows Installer 或脚本安装程序。 不支持 Windows 应用程序包（.appx 文件）部署类型。  

- 它必须在本地系统帐户而非用户帐户下运行。  

- 它不得与桌面进行交互。 该程序必须无提示运行或在无人参与模式下运行。  

- 它本身不能启动重新启动。 该应用程序必须使用标准的重新启动代码 (3010) 请求重新启动。 此行为可确保此步骤正确处理重新启动。 如果应用程序返回 3010 退出代码，则任务序列引擎将重启计算机。 重新启动后，任务序列自动继续。  

> [!Note]
> 如果应用[检查是否有可执行文件正在运行](../../apps/deploy-use/deploy-applications.md#bkmk_exe-check)，任务序列将无法安装它。 如果你未将此步骤配置为在出错时继续运行，那么整个任务序列失败。

当此步骤运行时，应用程序将检查部署类型的要求规则和检测方法的适用性。 根据此检查的结果，应用程序将安装适用的部署类型。 如果部署类型包含依赖关系，则对该依赖部署类型进行评估并将其作为此步骤的一部分进行安装。 独立媒体不支持应用程序依赖关系。  

> [!NOTE]  
> 要安装取代另一应用程序的应用程序，被取代的应用程序的内容文件必须可用。 否则任务序列步骤将失败。 例如，在客户端或捕获的映像中安装 Microsoft Visio 2010。 当运行“安装应用程序”步骤安装 Microsoft Visio 2013 时，Microsoft Visio 2010（被取代的应用程序）的内容文件必须在分发点上可用。 如果某个客户端或捕获映像未安装 Microsoft Visio，任务序列会安装 Microsoft Visio 2013，而不会检查 Microsoft Visio 2010 内容文件。  
>
> 如果你停用被取代的应用，并且在任务序列中引用新应用，那么任务序列无法启动。
此行为是有意为之：任务序列需要所有应用引用。<!-- SCCMDocs 1711 -->  

此任务序列步骤仅可在完整的 OS 中运行。 不可在 Windows PE 中运行。  

选择任务序列编辑器中的“添加”，选择“软件”，然后选择“安装应用程序”以添加此步骤。

### <a name="variables-for-install-application"></a>“安装应用程序”的变量

在此步骤中使用以下任务序列变量：  

- [_TSAppInstallStatus](task-sequence-variables.md#TSAppInstallStatus)  
- [SMSTSMPListRequestTimeoutEnabled](task-sequence-variables.md#SMSTSMPListRequestTimeoutEnabled)  
- [SMSTSMPListRequestTimeout](task-sequence-variables.md#SMSTSMPListRequestTimeout)  
- [TSErrorOnWarning](task-sequence-variables.md#TSErrorOnWarning)  

> [!NOTE]  
> 如果客户端无法利用定位服务检索管理点列表，则使用 SMSTSMPListRequestTimeoutEnabled 和 SMSTSMPListRequestTimeout 任务序列变量。 这些变量指定任务序列重试安装应用程序之前要等待的毫秒数。 有关详细信息，请参阅[任务序列变量](task-sequence-variables.md)。

### <a name="cmdlets-for-install-application"></a>“安装应用程序”的 cmdlet

使用以下 PowerShell cmdlet 管理此步骤：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepInstallApplication](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepinstallapplication?view=sccm-ps)
- [New-CMTSStepInstallApplication](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepinstallapplication?view=sccm-ps)
- [Remove-CMTSStepInstallApplication](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepinstallapplication?view=sccm-ps)
- [Set-CMTSStepInstallApplication](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepinstallapplication?view=sccm-ps)

### <a name="properties-for-install-application"></a>“安装应用程序”的属性

在此步骤的“属性”选项卡上，配置此部分描述的设置。  

#### <a name="install-the-following-applications"></a>安装以下应用程序

任务序列按指定顺序安装这些应用程序。  

Configuration Manager 将筛选出任何禁用的或具有以下设置的应用程序：  

- 仅当用户登录时  
- 使用用户权限运行  

这些应用程序不会出现在“选择要安装的应用程序”对话框中。

#### <a name="install-applications-according-to-dynamic-variable-list"></a>根据动态变量列表安装应用程序

任务序列使用此基本变量名安装应用程序。 基本变量名称适用于为集合或计算机定义的任务序列变量。 这些变量指定任务序列为该集合或计算机安装的应用程序。 每个变量名称都由其通用的基名称和一个数字后缀（从 01 开始）组成。 每个变量的值都必须包含应用程序的名称，且没有其他任何内容。  

对于要使用动态变量列表安装的应用程序，请在应用程序“属性”的“常规”选项卡中启用以下设置 ：**允许通过“安装应用程序”任务序列操作安装此应用程序，而不是手动部署**。  

> [!NOTE]  
> 对于独立媒体部署，无法使用动态变量列表安装应用程序。  

例如，要使用名为“AA01”的任务序列变量安装单个应用程序，需指定以下变量：  

|变量名称|变量值：|  
|-------------------|--------------------|  
|AA01|Microsoft Office|  

要安装两个应用程序，需指定以下变量：  

|变量名称|变量值：|  
|-------------------|--------------------|  
|AA01|Microsoft Lync|  
|AA02|Microsoft Office|  

以下条件会影响任务序列安装的应用程序：  

- 如果变量的值中包含应用程序名称之外的其他任何信息。 任务序列不会安装应用程序，并继续执行操作。  

- 如果任务序列未找到带指定基本名称和“01”后缀的变量，任务序列不会安装任何应用程序。  

> [!Important]  
> 这些值区分大小写。 例如，“install”不同于“Install”。 如果需要更改值，任务序列编辑器无法检测大小写变化。 同时进行另一项编辑（例如，修改步骤说明）。<!--509714-->

#### <a name="if-an-application-fails-continue-installing-other-applications-in-the-list"></a>如果应用程序失败，继续安装列表中的其他应用程序

此设置指定在单个应用程序安装失败时该步骤继续。 如果指定此设置，则任务序列将继续，不考虑任何安装错误。 如果未指定此设置且安装失败，步骤将立即结束。  

#### <a name="clear-application-content-from-cache-after-installing"></a>安装后从缓存中清除应用程序内容

<!--4485675-->
自版本 1906 起，在此步骤运行后，从客户端缓存中删除应用内容。 对于具有小型硬盘的设备，或在连续安装大量大型应用时，这一行为是有帮助的。


### <a name="options-for-install-application"></a>“安装应用程序”的选项

> [!NOTE]  
> 在此步骤的“选项”选项卡上选择“出错时继续”时，该任务序列将在应用程序安装失败时继续 。 如果不启用此选项，任务序列失败且不安装剩余的应用程序。  

除默认选项外，还可配置此任务序列步骤的“选项”选项卡上的以下其他设置：  

#### <a name="retry-this-step-if-computer-unexpectedly-restarts"></a>如果计算机意外重启，请重试此步骤

如果安装其中一个应用程序时意外重启计算机，请重试此步骤。 两次重试此步骤后将默认启用此设置。 可以指定 1 到 5 次重试。  



## <a name="install-package"></a><a name="BKMK_InstallPackage"></a>安装包

作为任务序列的一部分，使用此步骤安装软件包。 此步骤运行时，安装会立即开始而不等待策略轮询间隔。  

包必须符合以下条件：  

- 它必须在本地系统帐户而非用户帐户下运行。  

- 它不应与桌面进行交互。 该程序必须无提示运行或在无人参与模式下运行。  

- 它本身不能启动重新启动。 该软件必须使用标准的重新启动代码 (3010) 请求重新启动。 此行为可确保任务序列正确处理重新启动。 如果该软件不返回 3010 退出代码，则任务序列引擎将重启计算机。 重新启动后，任务序列自动继续。  

部署 OS 时不支持使用“首先运行其他程序”选项安装从属程序的程序。 如果启用了选项“首先运行其他程序”，且其从属程序已在目标计算机上运行，则将运行从属程序且任务序列将继续。 但是，如果从属程序尚未在目标计算机上运行，则任务序列步骤将失败。  

> [!NOTE]  
> 管理中心站点并没有任务序列期间启用软件分发代理所需的必要客户端配置策略。 当你在管理中心站点为任务序列创建独立媒体，而任务序列包含“安装包”  步骤时，CreateTsMedia.log 文件可能会出现以下错误：  
>
> `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`  
>
> 对于包括“安装包”步骤的独立媒体，请在已启用软件分发代理的主站点创建独立媒体。 或者，在“安装 Windows 和 ConfigMgr”步骤后及第一个“安装包”步骤前添加一个“运行命令行”步骤  。 “运行命令行”步骤运行 WMIC 命令，以便在第一个“安装包”步骤之前启用软件分发代理 。 在“运行命令行”步骤中使用以下命令：  
>
> `WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE`  
>
> 有关创建独立媒体的详细信息，请参阅[创建独立媒体](../deploy-use/create-stand-alone-media.md)。  

此任务序列步骤仅可在完整的 OS 中运行。 不可在 Windows PE 中运行。  

选择任务序列编辑器中的“添加”，选择“软件”，然后选择“安装包”以添加此步骤。

### <a name="variables-for-install-package"></a>“安装包”的变量

在此步骤中使用以下任务序列变量：  

- [OSDDoNotLogCommand](task-sequence-variables.md#OSDDoNotLogCommand) <!--1358493-->  

### <a name="cmdlets-for-install-package"></a>“安装包”的 cmdlet

使用以下 PowerShell cmdlet 管理此步骤：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepInstallSoftware](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepinstallsoftware?view=sccm-ps)
- [New-CMTSStepInstallSoftware](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepinstallsoftware?view=sccm-ps)
- [Remove-CMTSStepInstallSoftware](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepinstallsoftware?view=sccm-ps)
- [Set-CMTSStepInstallSoftware](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepinstallsoftware?view=sccm-ps)

> [!TIP]
> 在用户安装任务序列前，使用内容预缓存功能下载适用的操作系统升级包。 有关详细信息，请参阅[配置预缓存内容](../deploy-use/configure-precache-content.md)。

### <a name="properties-for-install-package"></a>“安装包”的属性

在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="install-a-single-software-package"></a>安装单个软件包

此设置会指定一个 Configuration Manager 软件包。 该步骤要等到安装完成后才开始。  

#### <a name="install-software-packages-according-to-dynamic-variable-list"></a>根据动态变量列表安装软件包

任务序列将使用此基本变量名称安装包。 基本变量名称适用于为集合或计算机定义的任务序列变量。 这些变量指定任务序列将为该集合或计算机安装的包。 每个变量名称都由其通用的基名称和一个数字后缀（从 001 开始）组成。 每个变量的值都必须包含包 ID 和软件名称，以冒号分隔。  

对于要使用动态变量列表安装的软件，请在包“属性”的“高级”选项卡中启用以下设置 ：**允许在不部署的情况下从“安装包”任务序列安装此程序**。  

> [!NOTE]  
> 对于独立媒体部署，无法使用动态变量列表安装软件包。  

例如，要使用名为 AA001 的任务序列变量安装单个软件包，需指定以下变量：  

|变量名称|变量值：|  
|-------------------|--------------------|  
|AA001|CEN00054:Install|  

要安装两三个软件包，需指定以下变量：  

|变量名称|变量值：|  
|-------------------|--------------------|  
|AA001|CEN00054:Install|  
|AA002|CEN00107:Install Silent|  
|AA003|CEN00031:Install|  

以下条件可影响任务序列所安装的包：  

- 如果变量的值未以正确的格式创建，或者未指定有效的包 ID 和名称，则软件安装将失败。  

- 如果包 ID 含有小写字符，则软件安装将失败。  

- 如果任务序列未找到带指定基本名称和“001”后缀的变量，任务序列不会安装任何包。 任务序列将继续。  

> [!Important]  
> 这些值区分大小写。 例如，“install”不同于“Install”。 如果需要更改值，任务序列编辑器无法检测大小写变化。 同时进行另一项编辑（例如，修改步骤说明）。<!--509714-->

#### <a name="if-installation-of-a-software-package-fails-continue-installing-other-packages-in-the-list"></a>如果软件包安装失败，则继续安装列表中的其他包

此设置指定在单个软件包安装失败时该步骤继续。 如果指定此设置，则任务序列将继续，不考虑任何安装错误。 如果未指定此设置且安装失败，步骤将立即结束。  



## <a name="install-software-updates"></a><a name="BKMK_InstallSoftwareUpdates"></a>安装软件更新

使用此步骤在目标计算机上安装软件更新。 在运行此任务序列步骤时，才会评估目标计算机是否有适用的软件更新。 那时，会与其他 Configuration Manager 客户端一样评估目标计算机是否有合适的软件更新。 对于此安装软件更新的步骤，首先向目标计算机所属的集合部署更新。  

> [!IMPORTANT]  
> 对于最佳性能，安装最新版 Windows 更新代理。  

此任务序列步骤仅可在完整的 OS 中运行。 不可在 Windows PE 中运行。

选择任务序列编辑器中的“添加”，选择“软件”，然后选择“安装软件更新”以添加此步骤。

### <a name="variables-for-install-software-updates"></a>“安装软件更新”的变量

在此步骤中使用以下任务序列变量：  

- [SMSInstallUpdateTarget](task-sequence-variables.md#SMSInstallUpdateTarget)  
- [SMSTSMPListRequestTimeoutEnabled](task-sequence-variables.md#SMSTSMPListRequestTimeoutEnabled)  
- [SMSTSMPListRequestTimeout](task-sequence-variables.md#SMSTSMPListRequestTimeout)  
- [SMSTSSoftwareUpdateScanTimeout](task-sequence-variables.md#SMSTSSoftwareUpdateScanTimeout)  
- [SMSTSWaitForSecondReboot](task-sequence-variables.md#SMSTSWaitForSecondReboot)  

> [!NOTE]  
> 如果客户端无法利用定位服务检索管理点列表，则使用 SMSTSMPListRequestTimeoutEnabled 和 SMSTSMPListRequestTimeout 变量。 这些变量指定任务序列重试安装应用程序或软件更新之前要等待的毫秒数。 有关详细信息，请参阅[任务序列变量](task-sequence-variables.md)。  

### <a name="cmdlets-for-install-software-updates"></a>“安装软件更新”的 cmdlet

使用以下 PowerShell cmdlet 管理此步骤：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepInstallUpdate](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepinstallupdate?view=sccm-ps)
- [New-CMTSStepInstallUpdate](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepinstallupdate?view=sccm-ps)
- [Remove-CMTSStepInstallUpdate](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepinstallupdate?view=sccm-ps)
- [Set-CMTSStepInstallUpdate](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepinstallupdate?view=sccm-ps)

有关此步骤的更多建议和技术流程图，请参阅[安装软件更新](install-software-updates.md)。

### <a name="properties-for-install-software-updates"></a>“安装软件更新”的属性

在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="required-for-installation---mandatory-software-updates-only"></a>安装要求 - 仅必需的软件更新

选择此选项，在管理员定义的安装截止日期前安装所有必需的软件更新。  

#### <a name="available-for-installation---all-software-updates"></a>可供安装 - 所有软件更新

选择此选项以安装所有可用的软件更新。 先向计算机所属的集合部署这些更新。 任务序列将在目标计算机上安装所有可用的软件更新。  

#### <a name="evaluate-software-updates-from-cached-scan-results"></a>根据缓存的扫描结果评估软件更新

默认情况下，此步骤使用从 Windows 更新代理中缓存的扫描结果。 禁用此选项以指示 Windows 更新代理从软件更新点下载最新目录。 如果使用任务序列[捕获和生成 OS 映像](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md)，则启用此选项。 此方案中可能包含大量软件更新。

其中许多更新具有依赖项。 例如，在更新 XYZ 显示为适用之前安装更新。 当禁用此设置并将任务序列部署到大量客户端时，它们将同时连接到软件更新点。 此行为会在更新目录处理和下载过程中导致性能问题。

在大多数情况下，使用默认设置来使用缓存的扫描结果。

SMSTSSoftwareUpdateScanTimeout 变量控制着此步骤期间的软件更新扫描超时。 默认值为 60 分钟。 有关详细信息，请参阅[任务序列变量](task-sequence-variables.md#SMSTSSoftwareUpdateScanTimeout)。

### <a name="options-for-install-software-updates"></a>“安装软件更新”的选项

除默认选项外，还可配置此任务序列步骤的“选项”选项卡上的以下其他设置：  

#### <a name="retry-this-step-if-computer-unexpectedly-restarts"></a>如果计算机意外重启，请重试此步骤

如果其中一个更新意外重启计算机，请重试此步骤。 两次重试此步骤后将默认启用此设置。 可以指定 1 到 5 次重试。  

> [!NOTE]  
> 配置 SMSTSWaitForSecondReboot 变量，以指定此方案中任务序列在计算机重启后暂停的秒数。 有关详细信息，请参阅[任务序列变量](task-sequence-variables.md#SMSTSWaitForSecondReboot)。  



## <a name="join-domain-or-workgroup"></a><a name="BKMK_JoinDomainorWorkgroup"></a>加入域或工作组

使用此步骤将目标计算机添加到工作组或域。  

此任务序列步骤仅可在完整的 OS 中运行。 不可在 Windows PE 中运行。

选择任务序列编辑器中的“添加”，选择“常规”，然后选择“加入域或工作组”以添加此步骤。

### <a name="variables-for-join-domain-or-workgroup"></a>“加入域或工作组”的变量

在此步骤中使用以下任务序列变量：  

- [OSDJoinAccount](task-sequence-variables.md#OSDJoinAccount)  
- [OSDJoinDomainName](task-sequence-variables.md#OSDJoinDomainName)  
- [OSDJoinDomainOUName](task-sequence-variables.md#OSDJoinDomainOUName)  
- [OSDJoinPassword](task-sequence-variables.md#OSDJoinPassword)  
- [OSDJoinSkipReboot](task-sequence-variables.md#OSDJoinSkipReboot)  
- [OSDJoinType](task-sequence-variables.md#OSDJoinType)  
- [OSDJoinWorkgroupName](task-sequence-variables.md#OSDJoinWorkgroupName)  

### <a name="cmdlets-for-join-domain-or-workgroup"></a>“加入域或工作组”的 cmdlet

使用以下 PowerShell cmdlet 管理此步骤：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepJoinDomainWorkgroup](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepJoinDomainWorkgroup?view=sccm-ps)
- [New-CMTSStepJoinDomainWorkgroup](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepJoinDomainWorkgroup?view=sccm-ps)
- [Remove-CMTSStepJoinDomainWorkgroup](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepJoinDomainWorkgroup?view=sccm-ps)
- [Set-CMTSStepJoinDomainWorkgroup](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepJoinDomainWorkgroup?view=sccm-ps)

### <a name="properties-for-join-domain-or-workgroup"></a>“加入域或工作组”的属性

在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="join-a-workgroup"></a>加入工作组

选择此选项，使目标计算机加入指定的工作组。 如果计算机当前是某个域的成员，选择此选项将导致计算机重新启动。  

#### <a name="join-a-domain"></a>加入域

选择此选项以将目标计算机加入指定的域。  

（可选）在指定的域中输入或浏览查找计算机要加入的组织单位 (OU)。 如果计算机当前是某个其他域或某个工作组的成员，此选项将导致计算机重新启动。 如果计算机已是其他 OU 的成员，由于 Active Directory 域服务不允许通过此方法更改 OU，Windows 安装程序会忽略此设置。  

#### <a name="enter-the-account-which-has-permission-to-join-the-domain"></a>输入有权限加入域的帐户

选择“设置”以输入有权加入域的帐户的用户名和密码。 使用后述格式输入帐户：`Domain\account`。 有关任务序列域加入帐户的详细信息，请参阅[帐户](../../core/plan-design/hierarchy/accounts.md#task-sequence-domain-join-account)。  



## <a name="prepare-configmgr-client-for-capture"></a><a name="BKMK_PrepareConfigMgrClientforCapture"></a>准备 ConfigMgr 客户端以便捕获

使用此步骤删除或配置引用计算机上的 Configuration Manager 客户端。 此操作让计算机做好准备以进行捕获，作为映像创建过程的一部分。

此步骤现在将完全删除 Configuration Manager 客户端，而不是仅删除密钥信息。 任务序列每次部署捕获的 OS 映像时，都将安装新的 Configuration Manager 客户端。  

> [!Note]  
> 任务序列引擎仅在执行“生成并捕获引用操作系统映像”任务序列期间才会删除客户端。 其他捕获方法执行期间，如捕获媒体或自定义任务序列等，任务序列不会删除客户端。  

此任务序列步骤仅可在完整的 OS 中运行。 不可在 Windows PE 中运行。  

选择任务序列编辑器中的“添加”，选择“映像”，然后选择“准备 ConfigMgr 客户端以便捕获”以添加此步骤。

### <a name="cmdlets-for-prepare-configmgr-client-for-capture"></a>“准备 ConfigMgr 客户端以便捕获”的 cmdlet

使用以下 PowerShell cmdlet 管理此步骤：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPrepareConfigMgrClient](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepPrepareConfigMgrClient?view=sccm-ps)
- [New-CMTSStepPrepareConfigMgrClient](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepPrepareConfigMgrClient?view=sccm-ps)
- [Remove-CMTSStepPrepareConfigMgrClient](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepPrepareConfigMgrClient?view=sccm-ps)
- [Set-CMTSStepPrepareConfigMgrClient](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepPrepareConfigMgrClient?view=sccm-ps)



## <a name="prepare-windows-for-capture"></a><a name="BKMK_PrepareWindowsforCapture"></a>准备 Windows 以便捕获

使用此步骤来指定捕获引用计算机上的 OS 映像时要使用的 Sysprep 选项。 此步骤运行 Sysprep，然后将计算机重新启动到为该任务序列指定的 Windows PE 启动映像。 如果引用计算机已加入域，此操作将失败。  

此步骤仅可在完整的 OS 中运行。 不可在 Windows PE 中运行。

选择任务序列编辑器中的“添加”，选择“映像”，然后选择“准备 Windows 以便捕获”以添加此步骤。

### <a name="variables-for-prepare-windows-for-capture"></a>“准备 Windows 以便捕获”的变量

在此步骤中使用以下任务序列变量：  

- [OSDKeepActivation](task-sequence-variables.md#OSDKeepActivation)  
- [OSDTargetSystemRoot](task-sequence-variables.md#OSDTargetSystemRoot-output)  

### <a name="cmdlets-for-prepare-windows-for-capture"></a>“准备 Windows 以便捕获”的 cmdlet

使用以下 PowerShell cmdlet 管理此步骤：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPrepareWindows](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepPrepareWindows?view=sccm-ps)
- [New-CMTSStepPrepareWindows](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepPrepareWindows?view=sccm-ps)
- [Remove-CMTSStepPrepareWindows](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepPrepareWindows?view=sccm-ps)
- [Set-CMTSStepPrepareWindows](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepPrepareWindows?view=sccm-ps)

### <a name="properties-for-prepare-windows-for-capture"></a>“准备 Windows 以便捕获”的属性

在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="automatically-build-mass-storage-driver-list"></a>自动生成大容量存储驱动程序列表

选择此选项以便 Sysprep 从引用计算机自动生成大容量存储驱动程序列表。 此选项在引用计算机上的 sysprep.inf 文件中启用“生成大容量存储驱动程序”选项。 有关此设置的详细信息，请参阅 Sysprep 文档。  

#### <a name="do-not-reset-activation-flag"></a>不重置激活标志

选择此选项以阻止 Sysprep 重置产品激活标志。  

#### <a name="shutdown-the-computer-after-running-this-action"></a>运行此操作后关闭计算机

<!--SCCMDocs-pr issue 2695-->
此选项指示 Sysprep 关闭计算机，代替其默认重启行为。

[适用于现有设备的 Windows Autopilot](../../../autopilot/existing-devices.md) 任务序列将此步骤与此选项配合使用。

- 如果想要任务序列刷新设备，然后立即开始适用于 Autopilot 的 OOBE，请禁用此选项。  

- 启用此选项可在映像创建后关闭设备。 然后，可以向第一次启用此选项开始适用于 Autopilot 的 OOBE 的用户交付此设备。  



## <a name="pre-provision-bitlocker"></a><a name="BKMK_PreProvisionBitLocker"></a>预设置 BitLocker

在 Windows PE 中，使用此步骤将在驱动器上启用 BitLocker。 默认情况下，由于仅加密使用的磁盘空间，因此加密时间要短得多。 安装 OS 后，使用 [启用 BitLocker](#BKMK_EnableBitLocker) 步骤应用密钥管理选项。

> [!IMPORTANT]
> 预先预配 BitLocker 要求计算机具有受支持且已启用的受信任平台模块 (TPM)。

此步骤仅可在 Windows PE 中运行。 它不会在完整的 OS 中运行。  

选择任务序列编辑器中的“添加”，选择“磁盘”，然后选择“预配 BitLocker”以添加此步骤。

### <a name="cmdlets-for-pre-provision-bitlocker"></a>“预先预配 BitLocker”的 cmdlet

使用以下 PowerShell cmdlet 管理此步骤：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepOfflineEnableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepOfflineEnableBitLocker?view=sccm-ps)
- [New-CMTSStepOfflineEnableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepOfflineEnableBitLocker?view=sccm-ps)
- [Remove-CMTSStepOfflineEnableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepOfflineEnableBitLocker?view=sccm-ps)
- [Set-CMTSStepOfflineEnableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepOfflineEnableBitLocker?view=sccm-ps)

### <a name="properties-for-pre-provision-bitlocker"></a>“预先预配 BitLocker”的属性

在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="apply-bitlocker-to-the-specified-drive"></a>将 BitLocker 应用于指定的驱动器

指定要为其启用 BitLocker 的驱动器。 BitLocker 仅加密驱动器上使用的空间。  

#### <a name="use-full-disk-encryption"></a>使用全磁盘加密

<!--SCCMDocs-pr issue 2671-->
默认情况下，此步骤仅加密驱动器上的已用空间。 建议使用此默认行为，因为它更加快速高效。 如果贵组织需要在安装期间加密整个驱动器，请启用此选项。 Windows 安装程序会等待整个驱动器加密，所需时间较长（尤其是在大型驱动器上）。

#### <a name="skip-this-step-for-computers-that-do-not-have-a-tpm-or-when-tpm-is-not-enabled"></a>对于没有 TPM 或 未启用 TPM 的计算机跳过此步骤

选择此选项可跳过针对某类计算机的驱动器加密操作，这类计算机不包含受支持且已启用的 TPM。 例如，可在将 OS 部署到虚拟机时使用此选项。  



## <a name="release-state-store"></a><a name="BKMK_ReleaseStateStore"></a>发布状态存储

使用此步骤通知状态迁移点，捕获或还原操作已完成。 将此步骤与“请求状态存储”、“捕获用户状态”和“还原用户状态”等步骤结合使用  。 可通过使用状态迁移点和用户状态迁移工具 (USMT)，使用这些步骤迁移用户状态数据。  

有关部署操作系统时管理用户状态的详细信息，请参阅[管理用户状态](../get-started/manage-user-state.md)。  

如果使用“请求状态存储”步骤请求访问状态迁移点以捕获用户状态，此步骤将通知状态迁移点捕获过程已完成。 然后，状态迁移点将用户状态数据标记为可还原。 状态迁移点设置用户状态数据的访问控制权限，以便仅还原的计算机具有只读访问权限。  

如果使用“请求状态存储”步骤请求访问状态迁移点以还原用户状态，此步骤将通知状态迁移点还原过程已完成。 然后，状态迁移点将激活其配置的数据保留配置。  

> [!IMPORTANT]  
> 为“请求状态存储”和“发布状态存储”步骤之间的所有步骤设置“出错时继续”。 每个“请求状态存储”步骤必须有一个匹配的“发布状态存储”步骤 。  

此步骤仅可在完整的 OS 中运行。 不可在 Windows PE 中运行。

选择任务序列编辑器中的“添加”，选择“用户状态”，然后选择“发布状态存储”以添加此步骤。

### <a name="variables-for-release-state-store"></a>“发布状态存储”的变量

在此步骤中使用以下任务序列变量：  

- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)  

### <a name="cmdlets-for-release-state-store"></a>“发布状态存储”的 cmdlet

使用以下 PowerShell cmdlet 管理此步骤：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepReleaseStateStore](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepReleaseStateStore?view=sccm-ps)
- [New-CMTSStepReleaseStateStore](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepReleaseStateStore?view=sccm-ps)
- [Remove-CMTSStepReleaseStateStore](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepReleaseStateStore?view=sccm-ps)
- [Set-CMTSStepReleaseStateStore](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepReleaseStateStore?view=sccm-ps)

### <a name="properties-for-release-state-store"></a>“发布状态存储”的属性

此步骤不需要“属性”选项卡上的任何设置。



## <a name="request-state-store"></a><a name="BKMK_RequestStateStore"></a>请求状态存储

使用此步骤可以在捕获或还原状态时请求对状态迁移点的访问权限。  

有关部署操作系统时管理用户状态的详细信息，请参阅[管理用户状态](../get-started/manage-user-state.md)。  

将此步骤与“发布状态存储”、“捕获用户状态”和“还原用户状态”等步骤结合使用  。 可通过使用状态迁移点和用户状态迁移工具 (USMT) 使用这些步骤迁移计算机状态。  

> [!NOTE]  
> 新建状态迁移点时，用户状态存储最多可能需要一小时才能使用。 要促进可用性，请调整状态迁移点上的任何属性设置以触发站点控制文件更新。  

此步骤在完整 OS 和脱机 USMT Windows PE 中运行。

选择任务序列编辑器中的“添加”，选择“用户状态”，然后选择“请求状态存储”以添加此步骤。

### <a name="variables-for-request-state-store"></a>“请求状态存储”的变量

在此步骤中使用以下任务序列变量：  

- [OSDStateFallbackToNAA](task-sequence-variables.md#OSDStateFallbackToNAA)  
- [OSDStateSMPRetryCount](task-sequence-variables.md#OSDStateSMPRetryCount)  
- [OSDStateSMPRetryTime](task-sequence-variables.md#OSDStateSMPRetryTime)  
- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)  

### <a name="cmdlets-for-request-state-store"></a>“请求状态存储”的 cmdlet

使用以下 PowerShell cmdlet 管理此步骤：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRequestStateStore](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepRequestStateStore?view=sccm-ps)
- [New-CMTSStepRequestStateStore](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepRequestStateStore?view=sccm-ps)
- [Remove-CMTSStepRequestStateStore](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepRequestStateStore?view=sccm-ps)
- [Set-CMTSStepRequestStateStore](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepRequestStateStore?view=sccm-ps)

### <a name="properties-for-request-state-store"></a>“请求状态存储”的属性

在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="capture-state-from-the-computer"></a>从计算机捕获状态

查找满足状态迁移点设置中所配置的最低要求的状态迁移点。 例如，“最大客户端数”和“最小可用磁盘空间量” 。 此选项不保证在状态迁移时有足够空间可用。 此选项将请求访问状态迁移点，以便从计算机捕获用户状态和设置。  

如果 Configuration Manager 站点具有多个活动状态迁移点，此步骤将查找具有可用磁盘空间的状态迁移点。 任务序列将查询管理点，以便获得状态迁移点列表，然后计算每个点，直到找到满足最低要求的迁移点。  

#### <a name="restore-state-from-another-computer"></a>从另一台计算机还原状态

请求访问状态迁移点，以便将先前捕获的用户状态和设置还原到目标计算机。  

如果具有多个状态迁移点，此步骤将查找具有目标计算机状态的状态迁移点。  

#### <a name="number-of-retries"></a>重试次数

此步骤在失败之前尝试查找合适状态迁移点的次数。  

#### <a name="retry-delay-in-seconds"></a>重试延迟（秒）

任务序列步骤在重试尝试之间等待的秒数。  

#### <a name="if-computer-account-fails-to-connect-to-a-state-store-use-the-network-access-account"></a>如果计算机帐户无法连接到状态存储，请使用网络访问帐户

如果任务序列无法使用计算机帐户访问状态迁移点，则使用网络访问帐户凭据进行连接。 此选项不太安全，因为其他计算机可以使用网络访问帐户来访问已存储的状态。 如果目标计算机未加入域，则必选此选项。  



## <a name="restart-computer"></a><a name="BKMK_RestartComputer"></a>重新启动计算机

使用此步骤重启运行任务序列的计算机。 重新启动之后，计算机将自动地继续运行任务序列中的下一个步骤。  

可以在完整 OS 或 Windows PE 中运行此步骤。

选择任务序列编辑器中的“添加”，选择“常规”，然后选择“重启计算机”以添加此步骤。

### <a name="variables-for-restart-computer"></a>“重启计算机”的变量

在此步骤中使用以下任务序列变量：  

- [SMSRebootMessage](task-sequence-variables.md#SMSRebootMessage)  
- [SMSRebootTimeout](task-sequence-variables.md#SMSRebootTimeout)  

### <a name="cmdlets-for-restart-computer"></a>“重启计算机”的 cmdlet

使用以下 PowerShell cmdlet 管理此步骤：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepReboot](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepreboot?view=sccm-ps)
- [New-CMTSStepReboot](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepreboot?view=sccm-ps)
- [Remove-CMTSStepReboot](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepreboot?view=sccm-ps)
- [Set-CMTSStepReboot](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepreboot?view=sccm-ps)

### <a name="properties-for-restart-computer"></a>“重启计算机”的属性

在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="the-boot-image-assigned-to-this-task-sequence"></a>分配给此任务序列的启动映像

对目标计算机选择此选项以使用分配给该任务序列的启动映像。 在 Windows PE 中，任务序列使用启动映像运行后续步骤。  

#### <a name="the-currently-installed-default-operating-system"></a>当前安装的默认操作系统

对目标计算机选择此选项以重新启动到安装的 OS。  

#### <a name="notify-the-user-before-restarting"></a>重新启动之前通知用户

选择此选项以在目标计算机重新启动前向用户显示通知。 步骤默认选择此选项。  

#### <a name="notification-message"></a>通知消息

输入在目标计算机重新启动之前向用户显示的通知消息。  

#### <a name="message-display-time-out"></a>消息显示超时

指定在目标计算机重新启动之前的时间量（秒）。 默认值为 60 秒。  



## <a name="restore-user-state"></a><a name="BKMK_RestoreUserState"></a>还原用户状态

使用此步骤来启动用户状态迁移工具 (USMT) 将用户状态和设置还原到目标计算机。 将此步骤与“捕获用户状态”步骤结合使用。  

有关部署操作系统时管理用户状态的详细信息，请参阅[管理用户状态](../get-started/manage-user-state.md)。  

将此步骤与“请求状态存储”和“发布状态存储”步骤结合使用，以使用状态迁移点保存或还原状态设置 。 此选项始终使用由 Configuration Manager 生成并管理的加密密钥解密 USMT 状态存储。  

“还原用户状态”步骤提供对最常用 USMT 选项的受限子网的控制。 为其他命令行选项指定 OSDMigrateAdditionalRestoreOptions 变量。  

> [!IMPORTANT]  
> 如果将此步骤用于与 OS 部署方案无关的目的，请在“还原用户状态”步骤之后（紧接着）添加[重启计算机](#BKMK_RestartComputer)步骤。  

此步骤仅可在完整的 OS 中运行。 不可在 Windows PE 中运行。

选择任务序列编辑器中的“添加”，选择“用户状态”，然后选择“还原用户状态”以添加此步骤。

### <a name="variables-for-restore-user-state"></a>“还原用户状态”的变量

在此步骤中使用以下任务序列变量：  

- [_OSDMigrateUsmtRestorePackageID](task-sequence-variables.md#OSDMigrateUsmtRestorePackageID)  
- [OSDMigrateAdditionalRestoreOptions](task-sequence-variables.md#OSDMigrateAdditionalRestoreOptions)  
- [OSDMigrateContinueOnRestore](task-sequence-variables.md#OSDMigrateContinueOnRestore)  
- [OSDMigrateEnableVerboseLogging](task-sequence-variables.md#OSDMigrateEnableVerboseLogging)  
- [OSDMigrateLocalAccounts](task-sequence-variables.md#OSDMigrateLocalAccounts)  
- [OSDMigrateLocalAccountPassword](task-sequence-variables.md#OSDMigrateLocalAccountPassword)  
- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)  

### <a name="cmdlets-for-restore-user-state"></a>“还原用户状态”的 cmdlet

使用以下 PowerShell cmdlet 管理此步骤：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRestoreUserState](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepRestoreUserState?view=sccm-ps)
- [New-CMTSStepRestoreUserState](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepRestoreUserState?view=sccm-ps)
- [Remove-CMTSStepRestoreUserState](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepRestoreUserState?view=sccm-ps)
- [Set-CMTSStepRestoreUserState](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepRestoreUserState?view=sccm-ps)

### <a name="properties-for-restore-user-state"></a>“还原用户状态”的属性

在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="user-state-migration-tool-package"></a>用户状态迁移工具包

指定包，该包包含此步骤要使用的 USMT 版本。 此包不需要程序。 步骤运行时，任务序列使用指定的包中的 USMT 版本。 指定包含 32 位或 64 位版本 USMT 的包。 USMT 的体系结构取决于任务序列将向其还原状态的 OS 的体系结构。

#### <a name="restore-all-captured-user-profiles-with-standard-options"></a>使用标准选项还原所有捕获的用户配置文件

使用标准选项还原捕获的用户配置文件。 要自定义 USMT 还原的选项，请选择“自定义用户配置文件捕获”。  

#### <a name="customize-how-user-profiles-are-restored"></a>自定义如何还原用户配置文件

允许你自定义想要还原到目标计算机的文件。 选择“文件”以指定想要用于还原用户配置文件的 USMT 包中的配置文件。 要添加配置文件，请在“文件名”框中输入文件的名称，然后选择“添加”。 “文件”窗格列出 USMT 使用的配置文件。 指定的 .xml 文件用于定义 USMT 还原的用户文件。  

#### <a name="restore-local-computer-user-profiles"></a>还原本地计算机用户配置文件

还原本地计算机用户配置文件。 这些配置文件不适用于域用户。 向已还原的本地用户帐户分配新密码。 USMT 无法迁移原始密码。 在“密码”  框中输入新密码，然后在“确认密码”  框中确认该密码。  

#### <a name="continue-if-some-files-cannot-be-restored"></a>如果无法还原某些文件则继续

继续还原用户状态和设置，即使 USMT 无法还原某些文件。 步骤默认启用此选项。 如果还原文件时禁用此选项且 USMT 遇到错误，此步骤将立即失败。 USMT 不会还原所有文件。

#### <a name="enable-verbose-logging"></a>启用详细日志记录

启用此选项以生成更详细的日志文件信息。 还原状态时，任务序列将生成日志 Loadstate.log 并默认存储在 `%WinDir%\ccm\logs` 文件夹的任务序列日志文件夹中。  



## <a name="run-command-line"></a><a name="BKMK_RunCommandLine"></a>运行命令行

使用此步骤运行指定命令行。  

正在运行的命令必须满足以下条件：  

- 它不应与桌面进行交互。 该命令必须无提示运行或在无人参与模式下运行。  

- 它本身不能启动重新启动。 该命令必须使用标准的重启代码 (3010) 请求重启。 此行为可确保任务序列正确处理重新启动。 如果该命令不返回 3010 退出代码，则任务序列引擎将重启计算机。 重新启动后，任务序列自动继续。

可以在完整 OS 或 Windows PE 中运行此步骤。

选择任务序列编辑器中的“添加”，选择“常规”，然后选择“运行命令行”以添加此步骤。

### <a name="variables-for-run-command-line"></a>“运行命令行”的变量

在此步骤中使用以下任务序列变量：  

- [OSDDoNotLogCommand](task-sequence-variables.md#OSDDoNotLogCommand)（从版本 1902 开始）<!--3654172-->  
- [SMSTSDisableWow64Redirection](task-sequence-variables.md#SMSTSDisableWow64Redirection)  
- [SMSTSRunCommandLineUserName](task-sequence-variables.md#SMSTSRunCommandLineUserName)  
- [SMSTSRunCommandLineUserPassword](task-sequence-variables.md#SMSTSRunCommandLineUserPassword)  
- [SMSTSRunCommandLineAsUser](task-sequence-variables.md#SMSTSRunCommandLineAsUser)（从版本 2002 开始）<!-- 5573175 -->
- [WorkingDirectory](task-sequence-variables.md#WorkingDirectory)  

### <a name="cmdlets-for-run-command-line"></a>“运行命令行”的 cmdlet

使用以下 PowerShell cmdlet 管理此步骤：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRunCommandLine](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepruncommandline?view=sccm-ps)
- [New-CMTSStepRunCommandLine](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepruncommandline?view=sccm-ps)
- [Remove-CMTSStepRunCommandLine](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepruncommandline?view=sccm-ps)
- [Set-CMTSStepRunCommandLine](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepruncommandline?view=sccm-ps)

### <a name="properties-for-run-command-line"></a>“运行命令行”的属性

在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="command-line"></a>命令行

指定任务序列运行的命令行。 此字段为必需字段。 包括文件扩展名，例如 .vbs 和 .exe。 包括所有必需的设置文件和命令行选项。  

如果没有指定文件扩展名，则 Configuration Manager 会尝试查找 .com、.exe 和 .bat。 如果文件扩展名不是可执行文件类型，则 Configuration Manager 会尝试应用本地关联。 例如，如果命令行为 readme.gif，则 Configuration Manager 会启动目标计算机上指定的应用程序来打开 .gif 文件。  

例如：  

`setup.exe /a`  

`cmd.exe /c copy Jan98.dat c:\sales\Jan98.dat`  

> [!NOTE]  
> 若要成功运行，在命令行操作之前使用 cmd.exe /c 命令。 这些操作的示例包括输出重定向、管道和复制命令。  

#### <a name="output-to-task-sequence-variable"></a>输出到任务序列变量

<!--user story 4977616/bug 4798352-->

从版本 1910 开始，将命令输出保存到自定义任务序列变量。

> [!Note]  
> Configuration Manager 将此输出限制为最后 1000 个字符。

#### <a name="disable-64-bit-file-system-redirection"></a>禁用 64 位文件系统重定向

64 位操作系统默认使用 WOW64 文件系统重定向程序运行命令行。 此行为可正确找到 32 位版本的 OS 可执行文件和库。 选择此选项可禁用 WOW64 文件系统重定向程序。 Windows 使用本机 64 位版本的 OS 可执行文件和库来运行命令。 如果在 32 位 OS 上运行，此选项没有任何影响。  

#### <a name="start-in"></a>开始于

指定程序的可执行文件夹，最多 127 个字符。 此文件夹可以是目标计算机上的绝对路径，也可以是包含包的分发点文件夹的相对路径。 此字段是可选的。  

例如：  

`c:\officexp`  

`i386`  

> [!NOTE]  
> 可使用“浏览”按钮浏览本地计算机上的文件和文件夹。 选择的任何内容还必须在目标计算机上。 它必须在相同的位置，并具有相同的文件名和文件夹名称。  

#### <a name="package"></a>包

当在命令行上指定了目标计算机上尚不存在的文件或程序时，请选择此选项以指定包含所需文件的 Configuration Manager 包。 此包不需要程序。 如果指定的文件在目标计算机上，则不需要此选项。  

#### <a name="time-out"></a>超时

指定表示 Configuration Manager 将允许命令行运行的时间长度的值。 此值的范围为 1 分钟至 999 分钟。 默认值为 15 分钟。 默认情况下禁用此选项。  

> [!IMPORTANT]  
> 如果输入的值未提供足够时间来成功完成指定命令，此步骤将失败。 整个任务序列可能失败，具体取决于步骤或组条件。 如果超时过期，Configuration Manager 将终止命令行进程。  

#### <a name="run-this-step-as-the-following-account"></a>作为以下帐户运行此步骤

指定作为本地系统帐户之外的其他 Windows 用户帐户运行的命令行。  

> [!NOTE]  
> 若要在安装 OS 后使用其他帐户运行简单脚本或命令，则首先向计算机添加该帐户。 此外，可能需要还原 Windows 用户配置文件才能运行更复杂的程序，如 Windows Installer。  

#### <a name="account"></a>帐户

指定此步骤运行命令行时要使用的 Windows 用户帐户。 命令行将使用指定帐户的权限运行。 选择“设置”以指定本地用户或域帐户。 有关任务序列运行方式帐户的详细信息，请参阅[帐户](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account)。

> [!IMPORTANT]  
> 如果此步骤指定用户帐户并在 Windows PE 中运行，操作将失败。 Windows PE 无法加入域。 smsts.log 文件将记录这一失败。  

### <a name="options-for-run-command-line"></a>“运行命令行”的选项

除默认选项外，还可配置此任务序列步骤的“选项”选项卡上的以下其他设置：  

#### <a name="success-codes"></a>成功代码

添加该脚本中的其他退出代码，该步骤应评估为成功。



## <a name="run-powershell-script"></a><a name="BKMK_RunPowerShellScript"></a>运行 PowerShell 脚本

使用此步骤运行指定的 Windows PowerShell 脚本。  

脚本必须满足以下条件：  

- 它不应与桌面进行交互。 该脚本必须无提示运行或在无人参与模式下运行。  

- 它本身不能启动重新启动。 该脚本必须使用标准的重启代码 (3010) 请求重启。 此行为可确保任务序列正确处理重新启动。 如果该脚本不返回 3010 退出代码，则任务序列引擎将重启计算机。 重新启动后，任务序列自动继续。

可以在完整 OS 或 Windows PE 中运行此步骤。 若要在 Windows PE 中运行此步骤，请在启动映像中启用 PowerShell。 从启动映像属性中的“可选组件”选项卡中启用 WinPE-PowerShell 组件。 有关如何修改启动映像的详细信息，请参阅[管理启动映像](../get-started/manage-boot-images.md)。  

> [!NOTE]  
> 默认情况下，Windows Embedded 操作系统上未启用 PowerShell。  

> [!WARNING]
> 某些反恶意软件可能会无意中触发针对 Configuration Manager 运行 PowerShell 脚本任务序列步骤的事件。 建议排除 %windir%\temp\smstspowershellscripts，以便反恶意软件允许这些脚本在不受干扰的情况下运行。

选择任务序列编辑器中的“添加”，选择“常规”，然后选择“运行 PowerShell 脚本”以添加此步骤。

### <a name="variables-for-run-powershell-script"></a>“运行 PowerShell 脚本”的变量

在此步骤中使用以下任务序列变量：  

- [OSDLogPowerShellParameters](task-sequence-variables.md#OSDLogPowerShellParameters)（从版本 1902 开始）<!--3556028-->  
- [SMSTSRunPowerShellAsUser](task-sequence-variables.md#SMSTSRunPowerShellAsUser)（从版本 2002 开始）<!-- 5573175 -->
- [SMSTSRunPowerShellUserName](task-sequence-variables.md#SMSTSRunPowerShellUserName)  
- [SMSTSRunPowerShellUserPassword](task-sequence-variables.md#SMSTSRunPowerShellUserPassword)  

### <a name="cmdlets-for-run-powershell-script"></a>“运行 PowerShell 脚本”的 cmdlet

使用以下 PowerShell cmdlet 管理此步骤：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRunPowerShellScript](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtssteprunpowershellscript?view=sccm-ps)
- [New-CMTSStepRunPowerShellScript](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtssteprunpowershellscript?view=sccm-ps)
- [Remove-CMTSStepRunPowerShellScript](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtssteprunpowershellscript?view=sccm-ps)
- [Set-CMTSStepRunPowerShellScript](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtssteprunpowershellscript?view=sccm-ps)

> [!Note]  
> 使用采用 Unicode 格式的已签名 PowerShell 脚本。 默认的 ANSI 格式不适用于这一步。

### <a name="properties-for-run-powershell-script"></a>“运行 PowerShell 脚本”的属性

在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="package"></a>包

指定包含 PowerShell 脚本的 Configuration Manager 包。 一个包可以包含多个 PowerShell 脚本。  

#### <a name="script-name"></a>脚本名称

指定要运行的 PowerShell 脚本的名称。 此字段为必需字段。  

#### <a name="enter-a-powershell-script"></a>输入 PowerShell 脚本

<!-- 3556028 -->
从版本 1902 开始，在此步骤中直接输入 Windows PowerShell 代码。 使用此功能，可以在任务序列期间运行 PowerShell 命令，而无需先使用脚本创建和分发包。

添加或编辑脚本时，PowerShell 脚本窗口提供以下操作：  

- 直接编辑脚本  

- 从文件打开现有的脚本  

- 浏览到 Configuration Manager 中现有的已批准[脚本](../../apps/deploy-use/create-deploy-scripts.md)

> [!Important]  
> 若要利用 Configuration Manager 的此项新功能，更新站点后，还请将客户端更新到最新版本。 尽管在更新站点和控制台时 Configuration Manager 控制台中会显示新功能，但只有在客户端版本也是最新版本之后，完整方案才能正常运行。

#### <a name="parameters"></a>参数

指定要传递给 PowerShell 脚本的参数。 这些参数与命令行中的 PowerShell 脚本参数相同。  

提供脚本使用的参数，而不是为 Windows PowerShell 命令行。  
以下示例包含有效的参数：  

`-MyParameter1 MyValue1 -MyParameter2 MyValue2`  

以下示例包含无效的参数。 前两项是 Windows PowerShell 命令行参数（-NoLogo 和 -ExecutionPolicy Unrestricted） 。 脚本不会使用这些参数。  

`-NoLogo -ExecutionPolicy Unrestricted -File MyScript.ps1 -MyParameter1 MyValue1 -MyParameter2 MyValue2`

<!-- SCCMDocs-pr issue 3561 -->
如果参数值包括特殊字符，请使用单引号 (`'`)括住该值。 使用双引号 (`"`) 可能会导致任务序列步骤不正确地处理参数。

例如：`-Arg1 '%TSVar1%' -Arg2 '%TSVar2%'`

从版本 2002 开始，将此属性设置为变量。<!-- 5690481 --> 例如，如果指定 `%MyScriptVariable%`，则当任务序列运行脚本时，它会将此自定义变量的值添加到 PowerShell 命令行。

#### <a name="powershell-execution-policy"></a>PowerShell 执行策略

确定允许在计算机上运行的 PowerShell 脚本（如果有）。 选择以下其中一个执行策略：  

- **AllSigned**：只能运行由受信任的发布者签发的脚本  

- **Undefined**：请勿定义任何执行策略  

- **Bypass**：加载所有配置文件并运行所有脚本。 如果从 Internet 下载未签名的脚本，Windows PowerShell 不会在运行脚本前提示需要权限。  

> [!IMPORTANT]  
> PowerShell 1.0 不支持未定义和旁路执行策略。  

#### <a name="output-to-task-sequence-variable"></a>输出到任务序列变量

<!-- 3556028 -->
从版本 1902 开始，将脚本输出保存到自定义任务序列变量。

> [!Note]  
> 从版本 1910 起，Configuration Manager 将此输出限制为最后 1000 个字符。

有关如何使用此步骤属性的示例，请参阅[如何设置变量](using-task-sequence-variables.md#bkmk_run-ps)。

#### <a name="start-in"></a>开始于

<!-- 3556028 -->
从版本 1902 开始，指定脚本的起始文件夹，最多 127 个字符。 此文件夹可以是目标计算机上的绝对路径，也可以是包含包的分发点文件夹的相对路径。 此字段是可选的。  

> [!NOTE]  
> 可使用“浏览”按钮浏览本地计算机上的文件和文件夹。 选择的任何内容还必须在目标计算机上。 它必须在相同的位置，并具有相同的文件名和文件夹名称。  

#### <a name="time-out"></a>超时

<!-- 3556028 -->
从版本 1902 开始，指定可表示 Configuration Manager 允许 PowerShell 脚本运行的时长的值。 此值的范围为 1 分钟至 999 分钟。 默认值为 15 分钟。 默认情况下禁用此选项。  

> [!IMPORTANT]  
> 如果输入的值未提供足够时间来成功完成指定脚本，此步骤将失败。 整个任务序列可能失败，具体取决于步骤或组条件。 如果超时过期，Configuration Manager 将终止 PowerShell 进程。  

#### <a name="run-this-step-as-the-following-account"></a>作为以下帐户运行此步骤

<!-- 3556028 -->
从版本 1902 开始，指定 PowerShell 脚本作为除本地系统帐户之外的其他 Windows 用户帐户运行。  

> [!NOTE]  
> 若要在安装 OS 后使用其他帐户运行简单脚本或命令，则首先向计算机添加该帐户。 此外，可能需要还原 Windows 用户配置文件才能运行更复杂的操作。  

#### <a name="account"></a>帐户

<!-- 3556028 -->
从版本 1902 开始，指定此步骤用于运行 PowerShell 脚本的 Windows 用户帐户。 指定帐户必须是系统上的本地管理员，并且脚本是使用此帐户的权限进行运行。 选择“设置”以指定本地用户或域帐户。 有关任务序列运行方式帐户的详细信息，请参阅[帐户](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account)。

> [!IMPORTANT]  
> 如果此步骤指定用户帐户并在 Windows PE 中运行，操作将失败。 Windows PE 无法加入域。 smsts.log 文件将记录这一失败。  

### <a name="options-for-run-powershell-script"></a>“运行 PowerShell 脚本”的选项

除默认选项外，还可配置此任务序列步骤的“选项”选项卡上的以下其他设置：  

#### <a name="success-codes"></a>成功代码

<!-- 3556028 -->
从版本 1902 开始，添加该脚本中该步骤应将其评估为成功的其他退出代码。



## <a name="run-task-sequence"></a><a name="child-task-sequence"></a> 运行任务序列

> [!Note]  
> 在版本 1910 中，Configuration Manager 默认启用此功能。 在版本 1906 或更早版本中，Configuration Manager 默认情况下不启用此项可选功能。 在使用前启用此功能。 有关详细信息，请参阅[启用更新中的可选功能](../../core/servers/manage/install-in-console-updates.md#bkmk_options)。

此步骤运行另一个任务序列。 这将创建任务序列之间的父子关系。 使用子任务序列，可以创建更模块化、可重复使用的任务序列。

选择任务序列编辑器中的“添加”，选择“常规”，然后选择“运行任务序列”以添加此步骤。

### <a name="specifications-and-limitations-for-run-task-sequence"></a>“运行任务序列”的规范和限制

将子任务序列添加到任务序列时，请考虑以下几点：  

- 父和子任务序列有效地组合成客户端运行的单个策略。  

- 该环境是全局环境。 如果父任务序列设置一个变量，然后子任务序列更改该变量，将保留最新值。 如果子任务序列新建一个变量，则可用于父任务序列的其余部分。  

- 对于单个任务序列操作，状态消息均按正常发送。  

- 任务序列将条目写入 smsts.log 文件，包括在子任务序列启动时使其清晰明确的新日志条目。  

<!--the following points are from SCCMdocs issue #1079-->

- 不能选择具有启动映像引用的任务序列。 对于需要启动映像的任何部署，请在父任务序列上指定它。  

- 如果禁用子任务序列，部署将失败。 不能使用“出错时继续”选项来解决此限制。  

- 如果子任务序列包含被视为“高影响力”的步骤，软件中心不会检测到它并会显示“高影响力”通知。 在“用户通知”选项卡上修改父任务序列的属性，以指定“这是具有高影响力的任务序列”。  

- 如果子任务序列缺少包引用，那么查看父任务序列不会检测到此状态。 如果编辑父任务序列，则在对父任务序列进行更改时，它会检测子任务序列中缺少的任何引用。  

### <a name="cmdlets-for-run-task-sequence"></a>“运行任务序列”的 cmdlet

自版本 1906 起，使用以下 PowerShell cmdlet 管理此步骤：<!-- 2839943, SCCMDocs#1118 -->

- **Get-CMTSStepRunTaskSequence**
- **New-CMTSStepRunTaskSequence**
- **Remove-CMTSStepRunTaskSequence**
- **Set-CMTSStepRunTaskSequence**

有关详细信息，请参阅 [1906 发行说明 - 新 cmdlet](https://docs.microsoft.com/powershell/sccm/1906-release-notes?view=sccm-ps#new-cmdlets)。

### <a name="properties-for-run-task-sequence"></a>“运行任务序列”的属性

在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="select-task-sequence-to-run"></a>选择要运行的任务序列

选择“浏览”，并选择子任务序列。 “选择任务序列”对话框不会显示父任务序列。



## <a name="set-dynamic-variables"></a><a name="BKMK_SetDynamicVariables"></a>设置动态变量

使用此步骤来执行以下操作：  

1. 从计算机及其环境中收集信息。 然后为指定的任务序列变量设置信息。  

2. 评估定义的规则。 基于评估为 true 的规则设置任务序列变量。  

可以在完整 OS 或 Windows PE 中运行此步骤。  

选择任务序列编辑器中的“添加”，选择“常规”，然后选择“设置动态变量”以添加此步骤。

### <a name="variables-for-set-dynamic-variables"></a>“设置动态变量”的变量

任务序列自动设置以下只读任务序列变量：  

- [\_SMSTSMake](task-sequence-variables.md#SMSTSMake)  
- [\_SMSTSModel](task-sequence-variables.md#SMSTSModel)  
- [\_SMSTSMacAddresses](task-sequence-variables.md#SMSTSMacAddresses)  
- [\_SMSTSIPAddresses](task-sequence-variables.md#SMSTSIPAddresses)  
- [\_SMSTSSerialNumber](task-sequence-variables.md#SMSTSSerialNumber)  
- [\_SMSTSAssetTag](task-sequence-variables.md#SMSTSAssetTag)  
- [\_SMSTSUUID](task-sequence-variables.md#SMSTSUUID)  

### <a name="cmdlets-for-set-dynamic-variables"></a>“设置动态变量”的 cmdlet

使用以下 PowerShell cmdlet 管理此步骤：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepSetDynamicVariable](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepsetdynamicvariable?view=sccm-ps)
- [New-CMTSStepSetDynamicVariable](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepsetdynamicvariable?view=sccm-ps)
- [Remove-CMTSStepSetDynamicVariable](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepsetdynamicvariable?view=sccm-ps)
- [Set-CMTSStepSetDynamicVariable](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepsetdynamicvariable?view=sccm-ps)

### <a name="properties-for-set-dynamic-variables"></a>“设置动态变量”的属性

在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="dynamic-rules-and-variables"></a>动态规则和变量

若要设置在任务序列中使用的动态变量，请添加规则。 然后为规则中指定的每个变量设置一个值。 此外，还需在不添加规则的情况下添加一个或多个变量。 添加规则时，可以从以下类别中进行选择：  

- **计算机**：评估硬件资产标记、UUID、序列号或 MAC 地址的值。 根据需要，设置多个值。 如果任何值为 true，则规则评估为 true。 例如，如果设备序列号为 5892087 且 MAC 地址为 22-A4-5A-13-78-26，则下面的规则评估为 true：  

    `IF Serial Number = 5892087 OR MAC address = 26-78-13-5A-A4-22 THEN`  

- **位置**：评估默认网关的值  

- **品牌和型号**：评估计算机的品牌和型号的值。 品牌和型号均必须评估为 true，规则才能评估为 true。

    指定一个星号 (`*`) 和问号 (`?`) 作为通配符字符。 星号匹配多个字符，问号匹配单个字符。 例如，字符串 `DELL*900?` 同时匹配 `DELL-ABC-9001` 和 `DELL9009`。  

- **任务序列变量**：添加要评估的任务序列变量、条件和值。 当为变量设置的值符合指定条件时，规则评估为 true。  

    指定为规则设置的一个或多个变量，该规则评估为 true，或设置变量而无需使用规则。 选择现有变量或创建自定义变量。  

    - **现有任务序列变量**：从现有任务序列变量的列表中选择一个或多个变量。 不可选择数组变量。  

    - **自定义任务序列变量**：定义自定义任务序列变量。 你也可指定现有任务序列变量。 此设置有助于指定现有变量数组，如 OSDAdapter，因为变量数组不在现有任务序列变量的列表中。  

为规则选择变量后，为每个变量提供一个值。 规则评估为 true 时，则变量设置为指定的值。 对于每个变量，可以选择“机密值”  来隐藏该变量的值。 默认情况下，某些现有变量隐藏值，例如 OSDCaptureAccountPassword 变量。  

> [!IMPORTANT]  
> 当使用“设置动态变量”步骤导入任务序列时，Configuration Manager 删除标记为“机密值”的所有变量值 。 导入任务序列后请重新输入动态变量的值。  



## <a name="set-task-sequence-variable"></a><a name="BKMK_SetTaskSequenceVariable"></a>设置任务序列变量

使用此步骤来设置与该任务序列配合使用的变量的值。  

可以在完整 OS 或 Windows PE 中运行此步骤。

选择任务序列编辑器中的“添加”，选择“常规”，然后选择“设置任务序列变量”以添加此步骤。

### <a name="variables-for-set-task-sequence-variable"></a>“设置任务序列变量”的变量

任务序列变量由任务序列操作读取，并指定这些操作的行为。 有关特定任务序列变量以及如何使用它们的详细信息，请参阅以下文章：  

- [如何使用任务序列变量](using-task-sequence-variables.md)  
- [任务序列变量](task-sequence-variables.md)  

### <a name="cmdlets-for-set-task-sequence-variable"></a>“设置任务序列变量”的 cmdlet

使用以下 PowerShell cmdlet 管理此步骤：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepSetVariable](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepsetvariable?view=sccm-ps)
- [New-CMTSStepSetVariable](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepsetvariable?view=sccm-ps)
- [Remove-CMTSStepSetVariable](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepsetvariable?view=sccm-ps)
- [Set-CMTSStepSetVariable](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepsetvariable?view=sccm-ps)

### <a name="properties-for-set-task-sequence-variable"></a>“设置任务序列变量”的属性

在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="task-sequence-variable"></a>任务序列变量：

指定任务序列内置或活动变量的名称，或者指定用户定义的变量名。  

#### <a name="do-not-display-this-value"></a>不显示此值

<!--1358330-->
启用此选项来屏蔽存储在任务序列变量中的敏感数据。 例如，指定密码时。

> [!Note]  
> 启用此选项，然后设置任务序列变量的值。 否则，变量值不会按预期设置，这可能会在任务序列运行时导致异常行为。<!--SCCMdocs issue #800-->

#### <a name="value"></a>值  

任务序列将变量设置为此值。 使用语法 `%varname%` 将此任务序列变量设置为另一任务序列变量的值。  



## <a name="setup-windows-and-configmgr"></a><a name="BKMK_SetupWindowsandConfigMgr"></a>安装 Windows 和 ConfigMgr

使用此步骤执行从 Windows PE 到新 OS 的转换。 此任务序列步骤是在部署任何 OS 时都必需的部分。 该步骤会将 Configuration Manager 客户端安装到新 OS 中，并为任务序列在新 OS 中继续执行做好准备。  

此步骤负责将任务序列从 Windows PE 转换为完整 OS。 由于有这种转换，此步骤在 Windows PE 和完整 OS 中都可以运行。 不过，由于转换是在 Windows PE 中启动的，因此只能在任务序列的 Windows PE 部分中添加转换。  

此步骤使用 Windows PE 安装目录 `X:\Windows` 替换 sysprep.inf 或 unattend.xml 目录变量，例如 `%WINDIR%` 和 `%ProgramFiles%`。 任务序列会忽略使用这些环境变量指定的变量。  

选择任务序列编辑器中的“添加”，选择“映像”，然后选择“安装 Windows 和 ConfigMgr”以添加此步骤。

### <a name="behaviors-for-setup-windows-and-configmgr"></a>“安装 Windows 和 ConfigMgr”的行为

此步骤将执行以下操作：  

#### <a name="preliminaries-windows-pe"></a>初步操作：Windows PE  

1. 替换 unattend.xml 文件中的任务序列变量。  

2. 下载包含 Configuration Manager 客户端的包。 将包添加到部署的映像。  

#### <a name="set-up-windows"></a>设置 Windows  

- 基于映像的安装  

    1. 如果存在，请禁用映像中的 Configuration Manager 客户端。 换言之，为 Configuration Manager 客户端服务禁用“自动启动”。  

    2. 更新已部署映像中的注册表，使用与引用计算机上相同的驱动器号启动已部署的 OS。  

    3. 重新启动到部署的 OS。  

    4. Windows 最小化安装使用先前指定的已禁用所有最终用户交互的 sysprep.inf 或 unattend.xml 答案文件运行。 如果使用“应用网络设置”步骤加入域，则该信息位于答案文件。 Windows 最小化安装会将计算机加入域。  

- 基于 Setup.exe 的安装。 运行 Setup.exe 会执行典型的 Windows 安装过程：  

    1. 将“应用操作系统”步骤中指定的 OS 升级包复制到硬盘驱动器。  

    2. 重新启动到新部署的 OS。  

    3. Windows 最小化安装使用先前指定的已禁用所有用户界面设置的 sysprep.inf 或 unattend.xml 答案文件运行。 如果使用“应用网络设置”步骤加入域，则该信息位于答案文件。 Windows 最小化安装会将计算机加入域。  

#### <a name="set-up-the-configuration-manager-client"></a>安装 Configuration Manager 客户端  

1. Windows 最小化安装结束后，任务序列将使用 setupcomplete.cmd 继续运行。 有关详细信息，请参阅[在安装完成后运行脚本 (SetupComplete.cmd)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/add-a-custom-script-to-windows-setup#run-a-script-after-setup-is-complete-setupcompletecmd)。  

2. 根据在“应用 Windows 设置”步骤中选择的选项，启用或禁用本地管理员帐户。  

3. 使用先前下载的包以及此步骤中指定的安装属性，安装 Configuration Manager 客户端。 客户端以“设置模式”进行安装。 此模式防止客户端在任务序列完成之前处理新策略请求。 有关详细信息，请参阅[预配模式](provisioning-mode.md)。  

4. 等待客户端完全可以操作。  

#### <a name="the-step-completes"></a>步骤完成

任务序列继续运行下一个步骤。  

> [!Note]  
> 在任务序列完成之前，通常不会处理 Windows 组策略。 此行为在不同版本的 Windows 之间保持一致。 任务序列期间的其他自定义操作可能会触发组策略评估。 若要详细了解操作顺序，请参阅[在安装完成后运行脚本 (SetupComplete.cmd)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/add-a-custom-script-to-windows-setup#run-a-script-after-setup-is-complete-setupcompletecmd)。 <!-- 2841304 -->


### <a name="variables-for-setup-windows-and-configmgr"></a>“安装 Windows 和 ConfigMgr”的变量

在此步骤中使用以下任务序列变量：  

- [SMSClientInstallProperties](task-sequence-variables.md#SMSClientInstallProperties)  

### <a name="cmdlets-for-setup-windows-and-configmgr"></a>“安装 Windows 和 ConfigMgr”的 cmdlet

使用以下 PowerShell cmdlet 管理此步骤：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepSetupWindowsAndConfigMgr](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepsetupwindowsandconfigmgr?view=sccm-ps)
- [New-CMTSStepSetupWindowsAndConfigMgr](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepsetupwindowsandconfigmgr?view=sccm-ps)
- [Remove-CMTSStepSetupWindowsAndConfigMgr](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepsetupwindowsandconfigmgr?view=sccm-ps)
- [Set-CMTSStepSetupWindowsAndConfigMgr](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepsetupwindowsandconfigmgr?view=sccm-ps)

### <a name="properties-for-setup-windows-and-configmgr"></a>“安装 Windows 和 ConfigMgr”的属性

在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="client-package"></a>客户端包

选择“浏览”，然后选择此步骤要使用的 Configuration Manager 客户端安装包。  

#### <a name="use-pre-production-client-package-when-available"></a>如果可用，使用预生产客户端包

如有可用的预生产客户端包，并且该计算机是试点集合的成员，则任务序列使用此包而非生产客户端包。 预生产客户端是在生产环境中用于测试的较新版本。 选择“浏览”，然后选择此步骤要使用的预生产客户端安装包。  

#### <a name="installation-properties"></a>安装属性

任务序列步骤自动指定站点分配和默认配置。 使用此字段来指定安装客户端时使用的任何其他安装属性。 要输入多个安装属性，请使用空格分隔。  

指定要在客户端安装过程中使用的命令行选项。 例如，输入 `/skipprereq: silverlight.exe` 以通知 CCMSetup.exe 不安装 Microsoft Silverlight 必备组件。 有关 CCMSetup.exe 的可用命令行选项的详细信息，请参阅[关于客户端安装属性](../../core/clients/deploy/about-client-installation-properties.md)。  

### <a name="options-for-setup-windows-and-configmgr"></a>“安装 Windows 和 ConfigMgr”的选项

> [!NOTE]  
> 请勿启用“选项”选项卡上的“出错时继续”。如果此步骤出错，不管是否启用此设置，任务序列都将失败。  



## <a name="upgrade-operating-system"></a><a name="BKMK_UpgradeOS"></a>升级操作系统

使用此步骤将较旧版本的 Windows 升级到较新版本的 Windows 10。  

此任务序列步骤仅可在完整的 OS 中运行。 不可在 Windows PE 中运行。  

选择任务序列编辑器中的“添加”，选择“映像”，然后选择“升级操作系统”以添加此步骤。

> [!TIP]
> 从 Windows 10 1709 版开始，媒体包括多个版本。 如果要将任务序列配置为使用 OS 升级包或 OS 映像，请务必选择[支持的版本](../../core/plan-design/configs/support-for-windows-10.md#windows-10-as-a-client)。  
>
> 在用户安装任务序列前，使用内容预缓存功能下载适用的操作系统升级包。 有关详细信息，请参阅[配置预缓存内容](../deploy-use/configure-precache-content.md)。

### <a name="variables-for-upgrade-os"></a>“升级操作系统”的变量

在此步骤中使用以下任务序列变量：  

- [_SMSTSOSUpgradeActionReturnCode](task-sequence-variables.md#SMSTSOSUpgradeActionReturnCode)  
- [SetupCompletePause](task-sequence-variables.md#SetupCompletePause)
- [OSDSetupAdditionalUpgradeOptions](task-sequence-variables.md#OSDSetupAdditionalUpgradeOptions)  

### <a name="cmdlets-for-upgrade-os"></a>“升级操作系统”的 cmdlet

使用以下 PowerShell cmdlet 管理此步骤：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepUpgradeOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepUpgradeOperatingSystem?view=sccm-ps)
- [New-CMTSStepUpgradeOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepUpgradeOperatingSystem?view=sccm-ps)
- [Remove-CMTSStepUpgradeOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepUpgradeOperatingSystem?view=sccm-ps)
- [Set-CMTSStepUpgradeOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepUpgradeOperatingSystem?view=sccm-ps)

### <a name="properties-for-upgrade-os"></a>“升级操作系统”的属性

在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="upgrade-package"></a>升级包

选择此选项以指定用于升级的 Windows 10 OS 升级包。  

#### <a name="source-path"></a>源路径

指定 Windows 安装程序要使用的 Windows 10 媒体的本地或网络路径。 此设置对应于 Windows 安装程序命令行选项 `/InstallFrom`。

还可以指定一个变量，例如 `%MyContentPath%` 或 `%DPC01%`。 将变量用作源路径时，必须在任务序列中提前设置其值。 例如，使用[下载包内容](#BKMK_DownloadPackageContent)步骤，为 OS 升级包的位置指定一个变量。 然后，在此步骤中将该变量用作源路径。  

#### <a name="edition"></a>版本

指定要用于升级的 OS 媒体的版本。  

#### <a name="product-key"></a>产品密钥

指定要用于升级过程的产品密钥。  

#### <a name="provide-the-following-driver-content-to-windows-setup-during-upgrade"></a>在升级过程中向 Windows 安装程序提供以下驱动程序内容

升级过程中将驱动程序添加到目标计算机。 驱动程序必须与 Windows 10 兼容。 此设置对应于 Windows 安装程序命令行选项 `/InstallDriver`。 有关详细信息，请参阅 [Windows 安装程序命令行选项](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#installdrivers)。

指定下列选项之一：  

- **驱动程序包**：选择“浏览”并从列表中选择现有的驱动程序包。

- **预留内容**：选择此选项以指定驱动程序内容的位置。 可以指定本地文件夹、网络路径或任务序列变量。 将变量用作源路径时，必须在任务序列中提前设置其值。 例如，通过使用[下载包内容](task-sequence-steps.md#BKMK_DownloadPackageContent)步骤。  

> [!TIP]
> 如果要为多种类型的硬件提供动态内容，请执行以下操作：
>
> - 将此步骤的多个实例与硬件类型的条件和单独的驱动程序内容配合使用。
>
> - 使用[下载包内容](task-sequence-steps.md#BKMK_DownloadPackageContent)步骤的多个实例。 将内容放在公用位置，然后使用“预留内容”选项。 此方法的优势在于任务序列只有一个**升级操作系统**步骤。

#### <a name="time-out-minutes"></a>超时（分钟）

指定 Configuration Manager 执行此步骤失败前的分钟数。 如果 Windows 安装程序停止进程但未终止，则此选项非常有用。  

#### <a name="perform-windows-setup-compatibility-scan-without-starting-upgrade"></a>不启动升级而执行 Windows 安装程序兼容性扫描

在不启动升级进程的情况下执行 Windows 安装程序兼容性扫描。 此设置对应于 Windows 安装程序命令行选项 `/Compat ScanOnly`。 使用此选项部署整个 OS 升级包。

<!--SCCMDocs-pr issue 2812-->
当启用此选项时，此步骤不会将 Configuration Manager 客户端置于预配模式。 Windows 安装程序在后台以无提示方式运行，且客户端将继续正常工作。 有关详细信息，请参阅[预配模式](provisioning-mode.md)。

安装程序将退出代码作为扫描结果返回。 下表提供了一些常见的退出代码：  

|退出代码|详细信息|  
|-|-|  
|MOSETUP_E_COMPAT_SCANONLY (0xC1900210)|不存在兼容性问题（“成功”）。|  
|MOSETUP_E_COMPAT_INSTALLREQ_BLOCK (0xC1900208)|可操作的兼容性问题。|  
|MOSETUP_E_COMPAT_MIGCHOICE_BLOCK (0xC1900204)|所选的迁移选项不可用。 例如，从 Enterprise 升级到 Professional。|  
|MOSETUP_E_COMPAT_SYSREQ_BLOCK (0xC1900200)|不适合 Windows 10。|  
|MOSETUP_E_COMPAT_INSTALLDISKSPACE_BLOCK (0xC190020E)|可用磁盘空间不足。|  

有关此参数的详细信息，请参阅 [Windows 安装程序命令行选项](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#compat)。  

#### <a name="ignore-any-dismissible-compatibility-messages"></a>忽略任何不重要的兼容性消息

指定安装程序完成安装，忽略任何不重要的兼容性消息。 此设置对应于 Windows 安装程序命令行选项 `/Compat IgnoreWarning`。  

#### <a name="dynamically-update-windows-setup-with-windows-update"></a>通过 Windows Update 动态更新 Windows 安装程序

使安装程序能够执行动态更新操作，例如搜索、下载和安装更新。 此设置对应于 Windows 安装程序命令行选项 `/DynamicUpdate`。 此设置与 Configuration Manager 软件更新不兼容。 如果要使用独立 Windows Server Update Services (WSUS) 或适用于企业的 Windows 更新管理更新，可启用此选项。  

#### <a name="override-policy-and-use-default-microsoft-update"></a>替代策略并使用默认 Windows 更新

临时实时覆盖本地策略以运行动态更新操作。 计算机从 Windows 更新获取更新。
