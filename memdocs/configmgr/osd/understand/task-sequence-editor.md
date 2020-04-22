---
title: 使用任务序列编辑器
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 控制台中使用任务序列编辑器
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: a4e8bb56-ee85-49fd-8b1c-c8f513cec671
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2047ae9e276ac94b633d1dc30814ed641cd34d03
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81691145"
---
# <a name="use-the-task-sequence-editor"></a>使用任务序列编辑器

适用范围：  Configuration Manager (Current Branch)

使用任务序列编辑器在 Configuration Manager 控制台中编辑任务序列  。 使用编辑器可以：  

- 打开任务序列的只读视图

- 在任务序列中添加或删除步骤  

- 更改任务序列的步骤的顺序  

- 添加或删除步骤组  

- 在任务序列之间复制和粘贴步骤

- 设置发生错误时任务序列是否继续的步骤选项  

- 将条件添加到任务序列的步骤和组中  

- 在任务序列中的步骤之间复制和粘贴条件。

- 搜索任务序列以快速查找步骤

需要先创建任务序列，才能对其进行编辑。 有关详细信息，请参阅[管理和创建任务序列](../deploy-use/manage-task-sequences-to-automate-tasks.md)。

## <a name="about-the-task-sequence-editor"></a>关于任务序列编辑器

任务序列编辑器包括以下组件：

![带注释的示例任务序列编辑器窗口的屏幕截图](media/task-sequence-editor.png)

<!-- The following numbered steps correspond to annotations in the above screenshot. Don't change the step numbers without also revising the image! -->

1. 任务序列的名称
2. 搜索。 有关详细信息，请参阅[搜索](#bkmk_search)。
3. 序列中所选组或步骤的属性 

    有关特定步骤的属性和选项的详细信息，请参阅[关于任务序列步骤](task-sequence-steps.md)。

4. 序列中所选组或步骤的选项 

    有关所有步骤的常规选项或特定步骤的选项的详细信息，请参阅[关于任务序列步骤](task-sequence-steps.md)。

    有关如何配置条件的详细信息，请参阅[条件](#bkmk_conditions)。

5. 添加组或步骤 
6. 删除组或步骤 
7. 折叠所有组或展开所有组
8. 移动序列中组或步骤的位置（上移、下移）
9. 任务序列：
    - 查看步骤和组的顺序。
    - 展开或折叠组。
    - 当在某个步骤或组的“选项”中将其禁用时，该步骤或组在序列中将显示为灰色  。
    - 如果某个步骤出现问题，则该步骤的图标将变为红色出错图标。 例如，缺少所需的值。
10. **确定**：保存并关闭
11. **取消**：关闭且不保存更改
12. **应用**：保存更改并保持打开状态

可以使用标准 Windows 控件来调整任务序列编辑器的大小。 若要调整两个主窗格的宽度，请使用鼠标选择任务序列和步骤属性之间的竖条，然后将其向左或向右拖动。

## <a name="view-a-task-sequence"></a><a name="bkmk_view"></a>查看任务序列

1. 在 Configuration Manager 控制台中，转到“软件库”  工作区，展开“操作系统”  ，然后选择“任务序列”  节点。  

2. 在“任务序列”列表中，选择要查看的任务序列  。  

3. 在功能区的“主页”选项卡上，在“任务序列”组中，选择“查看”    。

    > [!TIP]
    > 此操作为默认设置。 双击任务序列可以查看任务序列  。

此操作会以只读模式打开任务序列编辑器。 在此模式下，可以执行以下操作：

- 查看所有组、步骤、属性和选项
- 展开和折叠组
- 搜索任务序列
- 调整编辑器窗口的大小

在只读模式下，无法进行任何更改，包括复制步骤或条件。 此操作也不会锁定用于编辑的任务序列。 有关这些锁的详细信息，请参阅[回收锁定以编辑任务序列](#bkmk_sedo)。

若要更改任务序列，请关闭在只读模式下打开的任务序列编辑器。 然后[编辑](#bkmk_edit)任务序列。

> [!NOTE]  
> 查看或编辑使用创建任务序列向导创建的任务序列时，步骤的名称可能是步骤的操作或类型。 例如，可能会看到名为“分区磁盘 0”的步骤，该名称是类型为[格式化磁盘并分区](task-sequence-steps.md#BKMK_FormatandPartitionDisk)的步骤的操作。 所有任务序列步骤均按其类型记录，并不一定按编辑器中显示的步骤名称记录  。  

## <a name="edit-a-task-sequence"></a><a name="bkmk_edit"></a>编辑任务序列

使用以下过程修改现有任务序列：  

1. 在 Configuration Manager 控制台中，转到“软件库”  工作区，展开“操作系统”  ，然后选择“任务序列”  节点。  

2. 在“任务序列”  列表中，选择要编辑的任务序列。  

3. 在功能区的“主页”选项卡上，在“任务序列”组中，选择“编辑”    。 然后，执行以下任意操作：  

    - **添加步骤**：选择“添加”，选择一个类别，然后选择要添加的步骤  。 例如，若要添加[运行命令行](task-sequence-steps.md#BKMK_RunCommandLine)步骤，可选择“添加”，选择“常规”类别，然后选择“运行命令行”    。 此操作会在当前选定的步骤之后添加步骤。

    - **添加组**：选择“添加”，然后选择“新建组”   。 添加组后，可以向组中添加步骤。  

    - **更改顺序**：选择要重新排序的步骤或组。 然后，使用“上移”或“下移”图标   。 一次只能移动一个步骤或组。 也可通过右键单击组或步骤来执行这些操作。

        可以剪切、复制和粘贴组或步骤。 右键单击该项并选择操作。 还可使用标准的键盘快捷键来执行这些操作：

        - 剪切：Ctrl + X  
        - 复制：Ctrl + C  
        - 粘贴：Ctrl + V  

    - **删除步骤或组**：选择该步骤或组并选择“删除”  。  

4. 单击“确定”保存更改并关闭窗口  。 选择“取消”以放弃更改并关闭窗口  。 选择“应用”保存所做的更改并使任务序列编辑器保持打开状态  。  

有关可用的任务序列步骤列表，请参阅[任务序列步骤](task-sequence-steps.md)。  

> [!IMPORTANT]  
> 如果任务序列对编辑结果的对象进行了任何无关的引用，编辑器将要求你在关闭之前修复引用。 可能的操作包括：  
>
> - 更正引用
> - 从任务序列中删除未引用的对象  
> - 暂时禁用失败的任务序列步骤，直到更正或删除损坏的引用  

可以同时打开多个任务序列编辑器实例。 此行为让你可以比较多个任务序列，或者在这些任务序列之间复制和粘贴步骤。 你可以编辑一个任务序列，并查看另一个任务序列，但无法对同一任务序列同时执行这两项操作   。

## <a name="conditions"></a><a name="bkmk_conditions"></a>条件

使用条件控制任务序列的行为方式。 将条件添加到单个或一组步骤中。 任务序列评估条件后才会在设备中运行步骤。 仅当条件评估结果为符合时才运行该步骤。 如果条件评估结果为不符合，则任务序列会跳过组或步骤。

使用“选项”选项卡来管理条件  ：

![在任务序列编辑器的“选项”选项卡上管理条件](media/4621098-copy-paste-ts-condition.png)

可以使用以下类型的条件：

- **If 语句**：使用 if 语句对条件进行分组  。 可以评估所有条件、任何条件或无条件    。

- **任务序列变量**。 计算任务序列环境中任何内置、操作、自定义或只读[任务序列变量](task-sequence-variables.md)的当前值。 有关详细信息，请参阅[步骤条件](using-task-sequence-variables.md#bkmk_access-condition)。

    > [!NOTE]
    > 在这种情况下，可使用数组变量，但必须指定特定的数组成员。 例如，`OSDAdapter0EnableDHCP` 指定第一个网络适配器是否启用 DHCP  。 有关详细信息，请参阅[数组变量](using-task-sequence-variables.md#bkmk_array)。

- **OS 版本**：评估运行任务序列的设备的 OS 版本。 此列表列出了整个 Configuration Manager 中使用的常规 OS 版本。 若要评估更详细的 OS 版本（如特定版本的 Windows 10），请使用“查询 WMI”条件  。

- **OS 语言**：评估运行任务序列的设备的 OS 语言。 此列表包括 Windows 支持的 257 种语言。

- **文件属性**：评估运行任务序列的设备上的任何文件的版本或时间戳。

- **文件夹属性**：评估运行任务序列的设备上的任何文件夹的时间戳。

- **注册表设置**：评估运行任务序列的设备的任何注册表项值。

- **查询 WMI**：指定要在运行任务序列的设备上进行评估的命名空间和查询。

- **安装的软件**：指定 Windows Installer 文件，以便加载要在运行任务序列的设备上进行匹配的产品信息。 可以与特定产品或任何版本的产品相匹配。

### <a name="cmdlets-for-conditions"></a>用于条件的 Cmdlet

用以下 PowerShell cmdlet 管理条件：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepConditionFile](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionFile?view=sccm-ps)
- [Get-CMTSStepConditionFolder](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionFolder?view=sccm-ps)
- [Get-CMTSStepConditionIfStatement](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionIfStatement?view=sccm-ps)
- [Get-CMTSStepConditionOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionOperatingSystem?view=sccm-ps)
- [Get-CMTSStepConditionQueryWmi](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionQueryWmi?view=sccm-ps)
- [Get-CMTSStepConditionRegistry](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionRegistry?view=sccm-ps)
- [Get-CMTSStepConditionSoftware](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionSoftware?view=sccm-ps)
- [Get-CMTSStepConditionVariable](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionVariable?view=sccm-ps)

### <a name="copy-and-paste-conditions"></a>复制和粘贴条件

<!-- 4621098 -->

若要将条件从一个步骤重复用于另一个步骤，则从版本 1910 开始，现在可以在任务序列编辑器中复制和粘贴条件。 选择要剪切或复制的条件。 如果某个条件有子项，则会复制整个块。 如果剪贴板上有一个条件，则可以使用以下选项粘贴它：

- 在以下对象前粘贴
- 在以下对象后粘贴
- 在以下对象下粘贴（仅适用于嵌套条件）

使用标准键盘快捷方式可进行复制 (CTRL   + C  ) 和剪切 (CTRL   + X  )。 标准的 CTRL   + V  键盘快捷方式可执行“在以下对象后粘贴”  操作。

还可以通过新选项在列表中向上或向下移动条件。

> [!Note]  
> 可以在任务序列中的步骤之间复制和粘贴条件。 不同的任务序列之间不支持此操作。

## <a name="reclaim-lock-for-editing"></a><a name="bkmk_sedo"></a> 回收锁定以进行编辑

<!--3699337-->
如果 Configuration Manager 控制台停止响应，你可能会被锁定而无法做出进一步更改，直到 30 分钟后锁定到期。 此锁定是 Configuration Manager SEDO（分布式对象的序列化编辑）系统的一部分。 有关详细信息，请参阅 [Configuration Manager SEDO](../../develop/core/understand/sedo.md)。

从版本 1906 开始，可以清除对任务序列的锁定。 此操作仅适用于被锁定的用户帐户，并且仅可在站点授予锁定的同一设备上执行。 尝试访问已锁定的任务序列时，现在可以放弃更改，并继续编辑对象  。 锁定过期时这些更改将丢失。

> [!TIP]
> 从版本 1910 开始，可以清除对 Configuration Manager 控制台中任何对象的锁定。 有关详细信息，请参阅[使用 Configuration Manager 控制台](../../core/servers/manage/admin-console.md#bkmk_sedo)。<!--4786915-->

## <a name="search"></a><a name="bkmk_search"></a> 搜索

<!-- 4621085 -->

如果拥有包含许多组和步骤的大型任务序列，则很难找到具体步骤。 从版本 1910 开始，现在可以在任务序列编辑器中进行搜索。 通过此操作，可更快速地找到任务序列中的步骤。

![在任务序列编辑器中搜索](media/4621085-task-sequence-search.png)

输入搜索词即可开始搜索。 可以使用以下类型来确定搜索范围：

- 步骤名称
- 步骤描述
- 步骤类型
- 组名称
- 组说明
- 变量名称
- 条件
- 其他内容，例如，类似变量值或命令行的字符串

默认启用所有作用域。

还可以使用以下属性筛选所有步骤：

- 出错时继续
- 具有条件

默认不启用任何一个筛选器。

搜索时，编辑器窗口以黄色突出显示与搜索条件匹配的步骤。

使用以下键盘快捷方式快速访问这些搜索字段并导航搜索结果：

- **CTRL** + **F**：输入搜索字符串
- **CTRL** + **O**：选择搜索选项以确定搜索结果的范围
- **F3** 或 **Enter**：继续查看结果
- **SHIFT** + **F3**：后退查看结果

## <a name="see-also"></a>另请参阅

- [管理和创建任务序列](../deploy-use/manage-task-sequences-to-automate-tasks.md)

- [关于任务序列步骤](task-sequence-steps.md)

- [如何使用任务序列变量](using-task-sequence-variables.md)

- [使用 Configuration Manager 控制台](../../core/servers/manage/admin-console.md)
