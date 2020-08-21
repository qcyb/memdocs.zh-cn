---
title: 如何使用任务序列变量
titleSuffix: Configuration Manager
description: 了解如何使用 Configuration Manager 任务序列中的变量。
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: bc7de742-9e5c-4a70-945c-df4153a61cc3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7013ae10de753cbcb664771bd30dc51b259aa390
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697545"
---
# <a name="how-to-use-task-sequence-variables-in-configuration-manager"></a>如何使用 Configuration Manager 中的任务序列变量

适用范围：Configuration Manager (Current Branch)

 Configuration Manager 的 OS 部署功能中的任务序列引擎使用多个变量来控制其行为。 使用这些变量：

- 设置步骤条件  
- 更改特定步骤的行为  
- 在脚本中使用以执行更复杂的操作  

有关所有可用的任务序列变量的引用，请参阅[任务序列变量](task-sequence-variables.md)。

## <a name="types-of-variables"></a><a name="bkmk_types"></a> 变量类型

有多种类型的变量：  

- [内置](#bkmk_built-in)  
- [操作](#bkmk_action)  
- [自定义](#bkmk_custom)  
- [只读](#bkmk_read-only)  
- [数组](#bkmk_array)  

### <a name="built-in-variables"></a><a name="bkmk_built-in"></a> 内置变量

内置变量提供有关任务序列运行环境的信息。 其值可在整个任务序列中使用。 通常情况下，任务序列引擎会在运行任何步骤之前初始化内置变量。

例如，`_SMSTSLogPath` 是一个环境变量，指定 Configuration Manager 组件用于写入日志文件的路径。 任何任务序列步骤均可访问此环境变量。

任务序列会在每个步骤前计算一些变量。 例如，`_SMSTSCurrentActionName` 列出当前步骤的名称。

### <a name="action-variables"></a><a name="bkmk_action"></a> 操作变量

任务序列操作变量指定单个任务序列步骤使用的配置设置。 默认情况下，该步骤在运行之前会先初始化其设置。 仅当相关联的任务序列步骤运行时，这些设置才可用。 运行步骤前，任务序列会将操作变量值添加到环境。 该步骤运行之后，任务序列会从环境中删除该值。

例如，将“运行命令行”步骤添加到任务序列。 此步骤包括 Start In 属性。 任务序列将此属性的默认值存储为 `WorkingDirectory` 变量。 在运行“运行命令行”步骤之前，任务序列会初始化该值。 在运行此步骤时，从 `WorkingDirectory` 值访问 Start In 属性值。 该步骤完成之后，任务序列从环境中删除 `WorkingDirectory` 变量值。 如果任务序列包含另一个“运行命令行”步骤，它将初始化一个新的 `WorkingDirectory` 变量。 此时，任务序列会将变量设置为当前步骤的起始值。 有关详细信息，请参阅 [WorkingDirectory](task-sequence-variables.md#WorkingDirectory)。  

步骤运行时，操作变量的默认值为“present”。 如果设置为新值，该值可供任务序列中的多个步骤使用。 如果重写默认值，新值将保留在环境中。 此新值将覆盖任务序列中其他步骤的默认值。 例如，添加“设置任务序列变量”步骤作为任务序列的第一步。 此步骤将 `WorkingDirectory` 变量设置为 `C:\`。 任务序列中的任何“运行命令行”步骤均使用新的起始目录值。  

某些任务序列步骤将特定操作变量标记为“输出”。 任务序列中的后续步骤会读取这些输出变量。

> [!Note]  
> 并非所有任务序列步骤都具有操作变量。 例如，虽然有与“启用 BitLocker”操作相关联的变量，但没有与“禁用 BitLocker”操作相关联的变量。  

### <a name="custom-variables"></a><a name="bkmk_custom"></a> 自定义变量

这些变量是 Configuration Manager 不会创建的任何变量。 将自己的变量初始化为条件，以便在命令行或脚本中使用。

为新任务序列变量指定名称时，请遵循以下准则：  

- 任务序列变量名称可以包含字母、数字、下划线字符 (`_`) 和连字符 (`-`)。  

- 任务序列变量名称长度至少为 1 个字符，最多为 256 个字符。  

- 用户定义的变量必须以字母（`A-Z` 或 `a-z`）开头。  

- 用户定义的变量名称不能以下划线字符开头。 仅只读任务序列变量的前面使用下划线字符。  

- 任务序列变量名称不区分大小写。 例如，`OSDVAR` 和 `osdvar` 是相同的任务序列变量。  

- 任务序列变量名称不能以空格开头或结尾。 此外还不能有嵌入空格。 变量名称开头或结尾的任何空格会被任务序列忽略。  

对于可以创建的任务序列变量数量没有设定限制。 但是，变量数受任务序列环境大小的限制。 任务序列环境的总大小上限为 8KB。 有关详细信息，请参阅[减少任务序列策略的大小](../deploy-use/manage-task-sequences-to-automate-tasks.md#bkmk_policysize)。

### <a name="read-only-variables"></a><a name="bkmk_read-only"></a> 只读变量

不能更改一些只读变量的值。 通常该名称以下划线字符(`_`) 开头。 任务序列将这些变量用于操作。 只读变量在任务序列环境中可见。

这些变量在脚本或命令行中很有用。 例如，运行命令行，并将输出结果传输到 `_SMSTSLogPath` 中的日志文件，与其他日志文件结合使用。

> [!NOTE]  
> 只读任务序列变量可由任务序列中的步骤读取，但它们无法被设置。 例如，使用只读变量作为“运行命令行”步骤的命令行的一部分。 不能使用“设置任务序列变量”步骤设置只读变量。  

### <a name="array-variables"></a><a name="bkmk_array"></a> 数组变量

任务序列将一些变量存储为数组。 数组中的每个元素都代表单个对象设置。 当设备具有多个要配置的对象时，请使用这些变量。 下列任务序列步骤使用数组变量：

- [应用网络设置](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  

- [格式化磁盘并分区](task-sequence-steps.md#BKMK_FormatandPartitionDisk)  

## <a name="how-to-set-variables"></a><a name="bkmk_set"></a> 如何设置变量

对于自定义变量或并非只读的变量，可以通过以下几种方法来初始化并设置变量的值：  

- [“设置任务序列变量”](#bkmk_set-ts-step)步骤
- [“设置动态变量”](#bkmk_set-dyn-step)步骤
- [“运行 PowerShell 脚本”](#bkmk_run-ps)步骤
- [集合和设备变量](#bkmk_set-coll-var)  
- [TSEnvironment COM 对象](#bkmk_set-com)  
- [预启动命令](#bkmk_set-prestart)  
- [任务序列向导](#bkmk_set-tswiz)
- [任务序列媒体向导](#bkmk_set-media)  

从环境中删除变量的方法与创建变量相同。 要删除一个变量，请将变量值设置为空字符串。  

可以组合多个方法以将任务序列变量设置为相同序列的不同值。 例如，使用任务序列编辑器设置默认值，然后使用脚本设置自定义值。

如果通过不同方法设置相同变量，任务序列引擎将使用以下顺序：  

1. 它首先会计算集合变量。  

2. 特定于设备的变量会重写在集合上设置的相同变量。  

3. 由任务序列过程中的任何方法设置的变量优先于集合或设备变量。  

### <a name="general-limitations-for-task-sequence-variable-values"></a>任务序列变量值的一般限制

- 任务序列变量值不能超过 4,000 个字符。  

- 不能更改只读任务序列变量。 只读变量使用以下划线 (`_`) 字符开头的名称。  

- 任务序列变量值可能区分大小写，具体情况视值的使用情况而定。 大多数情况下，任务序列变量值不区分大小写。 包含密码的变量区分大小写。  

### <a name="set-task-sequence-variable"></a><a name="bkmk_set-ts-step"></a>设置任务序列变量

在任务序列中使用此步骤将单个变量设置为单个值。

有关详细信息，请参阅[设置任务序列变量](task-sequence-steps.md#BKMK_SetTaskSequenceVariable)。

### <a name="set-dynamic-variables"></a><a name="bkmk_set-dyn-step"></a>设置动态变量

在任务序列中使用此步骤设置一个或多个任务序列变量。 在此步骤中定义规则，以确定要使用哪些变量和值。

有关详细信息，请参阅[设置动态变量](task-sequence-steps.md#BKMK_SetDynamicVariables)

### <a name="run-powershell-script"></a><a name="bkmk_run-ps"></a>运行 PowerShell 脚本

<!-- 6315548 -->

在任务序列中使用此步骤，可以使用 PowerShell 脚本来设置任务序列变量。

可以从包中指定脚本名称，也可以直接在步骤中输入 PowerShell 脚本。 然后，使用“输出到任务序列变量”步骤属性，将脚本输出保存到自定义任务序列变量。

若要详细了解此步骤，请参阅[运行 PowerShell 脚本](task-sequence-steps.md#BKMK_RunPowerShellScript)。

> [!NOTE]
> 还可以结合使用 PowerShell 脚本和 TSEnvironment 对象来设置一个或多个变量。 有关详细信息，请参阅 Configuration Manager SDK 中的[如何在运行的任务序列中使用变量](../../develop/osd/how-to-use-task-sequence-variables-in-a-running-task-sequence.md)。

#### <a name="example-scenario-with-run-powershell-script-step"></a>“运行 PowerShell 脚本”步骤的示例方案

由于你的环境中拥有多个国家/地区的用户，因此你想要查询操作系统语言，以设置为多语言特定的“应用操作系统”步骤的条件。

1. 先向任务序列添加“运行 PowerShell 脚本”的实例，再执行“应用操作系统”步骤。

1. 使用“输入 PowerShell 脚本”选项来指定以下命令：

    ```powershell
    (Get-Culture).TwoLetterISOLanguageName
    ```

    若要详细了解此 cmdlet，请参阅 [Get-Culture](/powershell/module/microsoft.powershell.utility/get-culture)。 若要详细了解两字母 ISO 语言名称，请参阅 [ISO 639-1 代码列表](https://wikipedia.org/wiki/List_of_ISO_639-1_codes)。

1. 对于“输出到任务序列变量”选项，指定“`CurrentOSLanguage`”。

    ![“运行 PowerShell 脚本”步骤的示例方案的屏幕截图](media/run-powershell-script-example-language.png)

1. 在英语映像的“应用操作系统”步骤中，创建以下条件：`Task Sequence Variable CurrentOSLanguage equals "en"`

    ![“应用操作系统”步骤的示例条件的屏幕截图](media/condition-custom-task-sequence-variable.png)

    > [!TIP]
    > 若要详细了解如何在步骤中创建条件，请参阅[如何访问变量 - 步骤条件](#bkmk_access-condition)。

1. 保存和部署任务序列。

如果“运行 PowerShell 脚本”步骤在安装了英语版本 Windows 的设备上运行，此命令返回值 `en`。 然后，它将此值保存到自定义变量。 当英语映像的“应用操作系统”步骤在同一设备上运行时，条件的计算结果为 true。 如果你有“应用操作系统”步骤的多个实例对应不同的语言，任务序列会动态地运行与操作系统语言匹配的步骤。

### <a name="collection-and-device-variables"></a><a name="bkmk_set-coll-var"></a> 集合和设备变量

可以为设备和集合定义自定义的任务序列变量。 为设备定义的变量称为“每设备任务序列变量”。 为集合定义的变量称为特定于集合的任务序列变量。 如有冲突，特定于设备的变量优先于特定于集合的变量。 此行为意味着，分配到特定设备的任务序列变量会自动获得比分配到包含该设备的集合的变量更高的优先级。  

例如，设备 XYZ 是集合 ABC 的成员。 将 MyVariable 分配到集合 ABC，值为 1。 同时将 MyVariable 分配到设备 XYZ，值为 2。 分配给 XYZ 的变量优先于分配给集合 ABC 的变量。 当具有此变量的任务序列在 XYZ 上运行时，MyVariable 的值为 2。

可以隐藏特定于设备和特定于集合的变量，以便它们在 Configuration Manager 控制台中不可见。 使用选项“不要在 Configuration Manager 控制台中显示此值”时，控制台中不显示该变量的值。 任务序列日志文件 (smsts.log) 或任务序列调试器也不会显示变量值。 但在变量运行时，任务序列仍可使用该变量。 如果不想再隐藏这些变量，请先删除它们。 然后重新定义变量，而无需选择选项来隐藏它们。  

> [!WARNING]  
> 如果你将变量添加在“运行命令行”步骤的命令行中，则任务序列日志文件会显示包含变量值的完整命令行。 为了防止可能的敏感数据显示在日志文件中，请将任务序列变量“OSDDoNotLogCommand”设置为 `TRUE`。

可以在主站点或管理中心站点上管理因设备而异的变量。 Configuration Manager 不支持一台设备具有 1,000 个以上的已分配变量。  

> [!IMPORTANT]  
> 将特定于集合的变量用于任务序列时，请注意以下行为：  
>
> - 对集合的更改始终会复制到整个层次结构。 对集合变量所做的任何更改不仅应用于当前站点的成员，还会应用于整个层次结构中该集合的所有成员。  
>  
> - 删除集合时，此操作还会删除为集合配置的任务序列变量。  

#### <a name="create-task-sequence-variables-for-a-device"></a>为设备创建任务序列变量

1. 在 Configuration Manager 控制台中，转到“资产和符合性”工作区，并选择“设备”节点 。  

2. 依次选择目标设备和“属性”。  

3. 在“属性”对话框中，切换到“变量”选项卡。  

4. 对于要创建的每个变量，请选择“新建”图标。 指定任务序列变量的名称和值。 若要隐藏变量使其在 Configuration Manager 控制台中不可见，请选择“不在 Configuration Manager 控制台中显示此值”选项。  

5. 将所有变量添加到设备属性之后，选择“确定”。  

#### <a name="create-task-sequence-variables-for-a-collection"></a>为集合创建任务序列变量

1. 在 Configuration Manager 控制台中，转到“资产和符合性”工作区，并选择“设备集合”节点。 选择目标集合，然后选择“属性”。  

2. 在“属性”对话框中，切换到“集合变量”选项卡。  

3. 对于要创建的每个变量，请选择“新建”图标。 指定任务序列变量的名称和值。 若要隐藏变量使其在 Configuration Manager 控制台中不可见，请选择“不在 Configuration Manager 控制台中显示此值”选项。  

4. 根据需要为 Configuration Manager 指定要在评估任务序列变量时使用的优先级。  

5. 将所有变量添加到集合属性之后，选择“确定”。  

### <a name="tsenvironment-com-object"></a><a name="bkmk_set-com"></a> TSEnvironment COM 对象

若要使用脚本中的变量，请使用 TSEnvironment 对象。

有关详细信息，请参阅 Configuration Manager SDK 中的[如何在运行的任务序列中使用变量](../../develop/osd/how-to-use-task-sequence-variables-in-a-running-task-sequence.md)。

### <a name="prestart-command"></a><a name="bkmk_set-prestart"></a> 预启动命令

预启动命令是在用户选择任务序列之前在 Windows PE 中运行的一个脚本或可执行文件。 预启动命令可以查询变量或提示用户输入信息，然后将其保存在环境中。 使用 [TSEnvironment](#bkmk_set-com) COM 对象来读取和写入来自预启动命令的变量。

有关详细信息，请参阅[任务序列媒体的预启动命令](prestart-commands-for-task-sequence-media.md)。

### <a name="task-sequence-wizard"></a><a name="bkmk_set-tswiz"></a> 任务序列向导

从版本 1906 开始，在“任务序列向导”窗口中选择任务序列后，用于编辑任务序列变量的页面中包含一个“编辑”按钮。 可使用可访问的键盘快捷方式编辑变量。 在鼠标不可用的情况下，这一更改会有所帮助。<!-- 4668846 -->

### <a name="task-sequence-media-wizard"></a><a name="bkmk_set-media"></a> 任务序列媒体向导

指定从媒体运行的任务序列的变量。 使用媒体部署 OS 时，添加任务序列变量，并在创建媒体时指定其值。 变量及其值存储在媒体上。  

> [!NOTE]  
> 任务序列存储在独立媒体上。 但是，所有其他类型的媒体，如预留媒体，会从管理点中检索任务序列。  

从媒体运行任务序列时，可以在向导的“自定义”页添加一个变量。

使用媒体变量替代每集合变量或每计算机变量。 如果正在从媒体运行任务序列，则不应用也不使用每计算机变量和每集合变量。  

> [!TIP]  
> 任务序列将包 ID 和预启动命令行写入到运行 Configuration Manager 控制台的计算机上的 CreateTSMedia.log 文件。 此日志文件包括任何任务序列变量的值。 查看此日志文件以验证任务序列变量的值。  

有关详细信息，请参阅[创建任务序列媒体](../deploy-use/create-task-sequence-media.md)。

## <a name="how-to-access-variables"></a><a name="bkmk_access"></a> 如何访问变量

使用上一部分中所述的方法之一指定变量及其值之后，在任务序列中使用它。 例如，访问内置任务序列变量的默认值，或基于变量值设置步骤条件。  

使用以下方法来访问任务序列环境中的变量值：

- [在步骤中使用](#bkmk_access-step)  
- [步骤条件](#bkmk_access-condition)  
- [自定义脚本](#bkmk_access-script)  
- [Windows 安装程序答案文件](#bkmk_access-answer)  
  
### <a name="use-in-a-step"></a><a name="bkmk_access-step"></a> 在步骤中使用

在任务序列步骤中指定设置的变量值。 在任务序列编辑器中编辑步骤，并将变量名称指定为字段值。 将变量名称括在百分号 (`%`) 中。

例如，使用变量名称作为“运行命令行”步骤的“命令行”字段的一部分。 下面的命令行将计算机名称写入文本文件。

`cmd.exe /c %_SMSTSMachineName% > C:\File.txt`

### <a name="step-condition"></a><a name="bkmk_access-condition"></a> 步骤条件

使用内置或自定义任务序列变量作为步骤或组条件的一部分。 在运行步骤或组之前，任务序列会计算变量值。

要添加计算变量值的条件，请执行下列步骤：  

1. 在任务序列编辑器中，选择要添加条件的步骤或组。  

2. 切换到步骤或组的“选项”选项卡。 单击“添加条件”，然后选择“任务序列变量”。  

3. 在“任务序列变量”对话框中，指定以下设置：  

    - **变量**：变量的名称。 例如，`_SMSTSInWinPE`。  

    - **条件**：计算变量值的条件。 例如，等于。  

    - **值**：要检查的变量的值。 例如，`false`。  

上面三个示例构成了测试的常见条件，即任务是否从 Windows PE 的启动映像运行：

> **任务序列变量** `_SMSTSInWinPE equals "false"`

有关此情况，请参阅默认任务序列模板的“捕获文件和设置”组，以安装现有 OS 映像。

若要详细了解条件，请参阅[任务序列编辑器 - 条件](task-sequence-editor.md#bkmk_conditions)。

### <a name="custom-script"></a><a name="bkmk_access-script"></a> 自定义脚本

可以在运行任务序列时使用 Microsoft.SMS.TSEnvironment COM 对象读取和写入变量。

下面的 Windows PowerShell 示例查询 _SMSTSLogPath 变量以获取当前日志位置。 该脚本还设置自定义变量。

```PowerShell
# Create an object to access the task sequence environment
$tsenv = New-Object -ComObject Microsoft.SMS.TSEnvironment

# Query the environment to get an existing variable
# Set a variable for the task sequence log path
$LogPath = $tsenv.Value("_SMSTSLogPath")

# Or, convert all of the variables currently in the environment to PowerShell variables
$tsenv.GetVariables() | % { Set-Variable -Name "$_" -Value "$($tsenv.Value($_))" }

# Write a message to a log file
Write-Output "Hello world!" | Out-File -FilePath "$_SMSTSLogPath\mylog.log" -Encoding "Default" -Append

# Set a custom variable "startTime" to the current time
$tsenv.Value("startTime") = (Get-Date -Format HH:mm:ss) + ".000+000"
```

### <a name="windows-setup-answer-file"></a><a name="bkmk_access-answer"></a> Windows 安装程序答案文件

所提供的 Windows 安装程序答案文件可包含嵌入任务序列变量。 使用窗体 `%varname%`，其中 varname 是变量的名称。 “安装 Windows 和 ConfigMgr”步骤将变量名称字符串替换为实际变量值。 unattend.xml 答案文件的仅数字字段中不能使用这些嵌入的任务序列变量。

有关详细信息，请参阅[安装 Windows 和 ConfigMgr](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr)。

## <a name="see-also"></a>另请参阅

- [任务序列步骤](task-sequence-steps.md)

- [任务序列变量](task-sequence-variables.md)

- [自动执行任务的规划注意事项](../plan-design/planning-considerations-for-automating-tasks.md)

- [任务序列编辑器](task-sequence-editor.md)