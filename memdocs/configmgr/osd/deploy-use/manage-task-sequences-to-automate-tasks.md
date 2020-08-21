---
title: 管理任务序列
titleSuffix: Configuration Manager
description: 创建、编辑、部署、导入和导出任务序列，在环境中管理任务并自动执行任务。
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: a1f099f1-e9b5-4189-88b3-f53e3b4e4add
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 609f5d010018fa23dd4a533b2f1079f07d8c2283
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125059"
---
# <a name="manage-task-sequences-to-automate-tasks"></a>管理任务序列来自动执行任务

适用范围：Configuration Manager (Current Branch)

使用任务序列在 Configuration Manager 环境中自动执行步骤。 这些步骤可将 OS 映像部署到目标计算机，通过一组 OS 安装文件生成和捕获 OS 映像，并捕获和还原用户状态信息。 任务序列位于 Configuration Manager 控制台中。 在“软件库”工作区中，展开“操作系统”，并选择“任务序列”  。 将“任务序列”节点（包括所创建的子文件夹）复制到整个 Configuration Manager 层次结构。 有关计划的信息，请参阅[计划自动执行任务时的考虑事项](../plan-design/planning-considerations-for-automating-tasks.md)。  

## <a name="create"></a><a name="BKMK_CreateTaskSequence"></a>创建

通过使用创建任务序列向导来创建任务序列。 此向导可创建下列类型的任务序列：  

- [用于安装 OS 的任务序列](create-a-task-sequence-to-install-an-operating-system.md)：创建安装 OS 的步骤。 它还包括迁移用户数据、包含软件更新和安装应用程序的选项。

- [用于升级 OS 的任务序列](create-a-task-sequence-to-upgrade-an-operating-system.md)：创建升级 OS 的步骤。 它还包括包含软件更新和安装应用程序的选项。

- [捕获 OS 的任务序列](create-a-task-sequence-to-capture-an-operating-system.md)：创建从引用计算机构建和捕获 OS 的步骤。 在捕获映像之前，可以在引用计算机上包括软件更新和安装应用程序。

- [用于捕获和还原用户状态的任务序列](create-a-task-sequence-to-capture-and-restore-user-state.md)：将相关步骤添加到现有任务序列，以捕获和还原用户状态数据。

- [自定义任务序列](create-a-custom-task-sequence.md)：此类型不会给任务序列添加任何步骤。 创建此任务序列后，编辑并添加步骤。

## <a name="edit"></a><a name="BKMK_ModifyTaskSequence"></a>编辑  

通过添加或删除步骤、添加或删除组或者更改步骤的顺序来修改任务序列。 有关详细信息，请参阅[使用任务序列编辑器](../understand/task-sequence-editor.md)。

## <a name="reduce-the-size-of-task-sequence-policy"></a><a name="bkmk_policysize"></a> 减少任务序列策略的大小

<!--6982275-->
当任务序列策略的大小超出 32 MB 时，客户端将无法处理此大型策略。 因而客户端将无法运行任务序列部署。

存储在站点数据库中的任务序列的大小较小，但如果过大，仍可能会导致问题。 当客户端处理整个任务序列策略时，扩展的大小可能导致 32 MB 以上的问题。

自版本 2006 起，若要检查客户端上是否有 32-MB 任务序列策略大小，请使用[管理见解](../../core/servers/manage/management-insights.md#operating-system-deployment)。

若要帮助减少任务序列部署策略的总大小，请执行以下操作：

- 将功能段分隔到子任务序列，并使用[运行任务序列](../understand/task-sequence-steps.md#child-task-sequence)步骤。 每个任务序列的策略大小限制分别为 32 MB。

    > [!NOTE]
    > 减少任务序列中的步骤和组的总数，对策略大小影响甚微。 通常策略中每个步骤的大小为几 KB。 将各个步骤组移到子任务序列的效果更好。

- 部署与任务序列面向同一个集合时，减少其中的软件更新数量。

- 通过程序包引用脚本，而不要在[运行 PowerShell 脚本](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript)步骤中输入脚本。

- 任务序列环境运行时，对它的大小限制为 8 KB。 检查自定义任务序列变量的使用情况，这也会影响策略大小。

- 最后一个方法是，将复杂动态任务序列拆分为单独的任务序列，其中包含到不同集合的各种部署。

## <a name="software-center-properties"></a><a name="bkmk_prop-general"></a> 软件中心属性

使用以下过程配置软件中心中显示的任务序列的详细信息。 这些详细信息仅供参考。  

1. 在 Configuration Manager 工作区中，转到“软件库”工作区，展开“操作系统”，选择“任务序列”  。  

2. 选择要编辑的任务序列，然后选择“属性”。  

3. 在“常规”选项卡上，可使用软件中心的以下设置：  

    - **需要重启**：让用户了解安装期间是否需要重启。  

    - **下载大小 (MB)** ：指定任务序列在软件中心中显示多少兆字节。  

    - **预计运行时间（分钟）** ：指定任务序列在软件中心显示的预计运行时间（以分钟为单位）。  

## <a name="advanced-settings"></a><a name="bkmk_prop-advanced"></a>高级设置

按照以下步骤在 Configuration Manager 客户端上配置任务序列的行为。  

1. 在 Configuration Manager 工作区中，转到“软件库”工作区，展开“操作系统”，选择“任务序列”  。  

2. 选择要编辑的任务序列，然后选择“属性”。  

3. 在“高级”选项卡上，有下列可用设置：  

    - **首先运行其他程序**：选择此选项，可在此任务序列之前在其他包中运行一个程序。 默认情况下，此复选框已清除。 不需要单独部署指定要首先运行的程序。  

        > [!IMPORTANT]
        > 此设置仅适用于在完整 OS 中运行的任务序列。 如果使用 PXE 或启动媒体启动任务序列，Configuration Manager 将忽略此设置。  

        - **包**：浏览包含要在此任务序列之前运行的程序的包。  

        - **程序**：选择要在此任务序列之前运行的程序。  

        > [!NOTE]  
        > 如果所选程序在客户端上运行失败，则任务序列不会运行。 如果所选程序成功运行，则它不会再次运行，即使在同一客户端上重新运行了任务序列。  

    - **取消任务序列通知**：选择此选项可隐藏“新软件可用”Toast 通知。 “新软件”图标仍会显示在软件中心的通知区域中。 默认情况下禁用此选项。  

    - **在部署此任务序列的计算机上禁用该任务序列**：如果选择此选项时，Configuration Manager 会暂时禁用包含此任务序列的所有部署。 也会将任务序列从可运行部署列表中删除。 在启用之前，不会运行任务序列。 默认情况下禁用此选项。  

    - **允许的最长运行时间**：指定预计任务序列在目标计算机上运行的最长时间（分钟）。 使用等于或大于零的整数。 默认情况下，此值为 120 分钟。  

        > [!IMPORTANT]  
        > 当将维护时段用于部署此任务序列的集合时，如果“最大允许运行时间”大于计划的维护时段，就可能出现冲突。 如果最大运行时间设置为 0，任务序列将在维护时段启动。 维护时段关闭后，它将继续运行，直到完成或失败。 因此，最大运行时间设置为“0”的任务序列可能运行到维护时段结束后。 如果将最大运行时间设置为具体时段（不为“0”），且此时段大于任何可用维护时段的长度，那么该任务序列不会运行。 有关详细信息，请参阅[如何使用维护时段](../../core/clients/manage/collections/use-maintenance-windows.md)。  

        如果值设置为“0”，则 Configuration Manager 会将最大允许运行时间计算为 12 小时（720 分钟）以监视进度。 但是，只要倒计时持续时间不超过维护时段值，任务序列便会启动。  

        > [!NOTE]
        > 当它达到最大运行时间时，如果你不允许用户与必需部署进行交互，Configuration Manager 就会停止此任务序列。 如果任务序列本身未停止，则达到最大允许运行时间后，Configuration Manager 将停止监视任务序列。

    - **使用启动映像**：可在运行任务序列时使用选定的启动映像。 选择“浏览”可选择其他启动映像。 清除此选项，可在运行任务序列时禁用选定的启动映像。  

    - **此任务序列可以在任何平台上运行**：如果选择此选项，则 Configuration Manager 在任务序列运行时不会检查目标计算机的平台类型。 默认情况下选择此选项。  

    - **此任务序列仅可以在指定的客户端平台上运行**：此选项指定此任务序列可以在其上运行的处理器、OS 版本和服务包。 选择此选项时，还必须从列表中至少选择一个平台。 默认情况下不选择任何平台。 Configuration Manager 在评估集合中的哪些目标计算机将接收部署的任务序列时，使用此信息。  

        > [!NOTE]  
        > 从启动媒体或 PXE 运行任务序列时，Configuration Manager 将忽略此选项。 任务序列的运行方式就如同“此程序可以在任何平台上运行”选项处于选中状态。  

## <a name="high-impact-settings"></a>“影响重大”设置

将任务序列配置为“影响重大”，并自定义用户在运行任务序列时收到的消息。

> [!WARNING]
> 如果使用 PXE 部署，并在配置设备硬件时将网络适配器作为第一个启动设备，则这些设备可以自动启动 OS 部署任务序列而无需用户交互。 部署验证不会管理此配置。 尽管此配置可以简化流程并减少用户交互，但它会增加设备意外重置映像的风险。

### <a name="set-a-task-sequence-as-a-high-impact-task-sequence"></a>将任务序列设置为影响重大的任务序列

使用下列过程将任务序列设置为“影响重大”。

> [!NOTE]  
> 任何符合特定条件的任务序列都将自动定义为“影响重大”。 有关详细信息，请参阅[管理高风险部署](../../core/servers/manage/settings-to-manage-high-risk-deployments.md)。

1. 在 Configuration Manager 工作区中，转到“软件库”工作区，展开“操作系统”，选择“任务序列”  。  

2. 选择要编辑的任务序列，然后选择“属性”。  

3. 在“用户通知”选项卡上，选择“这是影响重大的任务序列”。  

### <a name="create-a-custom-notification-for-high-risk-deployments"></a>创建高风险部署的自定义通知

使用以下过程为影响重大的部署创建自定义通知。

1. 在 Configuration Manager 工作区中，转到“软件库”工作区，展开“操作系统”，选择“任务序列”  。  

2. 选择要编辑的任务序列，然后选择“属性”。  

3. 在“用户通知”选项卡上，选择“使用自定义文本”。  

    > [!NOTE]
    > 只能在已选择选项“这是影响重大的任务序列”时设置用户通知文本。  

4. 配置下列设置：  

    > [!Note]  
    > 每个文本框的最大限制为 255 个字符。  

    - **用户通知标题文本**：指定在软件中心用户通知上显示的蓝色文本。 例如，在默认用户通知中，本部分包含“确认想要升级此计算机上的操作系统”。  

    - **用户通知消息文本**：三个文本框提供自定义通知的正文。 所有文本框都需要添加文本。  

        - 第一个文本框：指定文本的主要正文，通常包含针对用户的说明。 例如，在默认用户通知中，本部分包含“操作系统升级需要一些时间，并且计算机可能会多次重启”。  

        - 第二个文本框：指定文本主要正文下的粗体文本。 例如，在默认用户通知中，本部分包含“此就地升级将安装新的操作系统并自动迁移你的应用、数据和设置”。  

        - 第三个文本框：指定粗体文本下的最后一行文本。 例如，在默认用户通知中，本部分包含“单击‘安装’以开始。 否则，单击‘取消’”的内容。  

#### <a name="example"></a>示例

假设在属性中配置以下自定义通知。

![任务序列属性的自定义“用户通知”选项卡](../media/user-notification.png)

当最终用户从软件中心打开安装时，将显示以下通知消息。

![软件中心中面向最终用户的自定义任务序列通知](../media/user-notification-enduser.png)

## <a name="performance-improvements-for-power-plans"></a><a name="bkmk_perf"></a> 电源计划的性能改进

<!--3555926-->

从版本 1910 开始，现在可以使用高性能电源计划运行任务序列。 此选项可提高任务序列的总体速度。 它将 Windows 配置为使用其内置的高性能电源计划，该计划提供最高性能，但电源消耗会变高。 对于新的任务序列，此选项默认启用。

启动任务序列后，在大多数情况下会记录当前启用的电源计划。 然后，会将当前电源计划切换到 Windows 默认高性能计划。 如果任务序列重新启动计算机，则会重复此过程。 在任务序列结束时，会将电源计划重置为存储的值。 此功能适用于 Windows 和 Windows PE，但不影响虚拟机。

- 如果在 Windows PE 中启动任务序列，则该任务序列不会记录当前启用的电源计划以供后续重用。

- 重置计算机映像（擦除和加载）的 OS 部署任务序列不会保留旧版 OS 的电源计划设置。 任务序列结束时，它会还原默认的“均衡”电源计划。

> [!Important]
> 若要利用 Configuration Manager 的此项新功能，更新站点后，请将客户端更新到最新版本。 另请更新启动映像以包含最新的客户端组件。 尽管在更新站点和控制台时 Configuration Manager 控制台中会显示新功能，但只有在客户端版本也是最新版本之后，完整方案才能正常运行。

1. 在 Configuration Manager 控制台中，转到“软件库”工作区。 展开“操作系统”，然后选择“任务序列”节点 。

1. 创建或选择现有任务序列，然后选择“属性”。

1. 切换到“性能”选项卡。

1. 启用“作为高性能电源计划运行”选项。

> [!Warning]
> 请注意低性能硬件上的此设置。 长时间运行大量系统操作可能会损伤低端硬件。 与硬件制造商联系以获取具体指导。

### <a name="known-issue"></a>已知问题

<!-- 5554928 -->

通常，在你更改任务序列属性中的设置时，它会更新所有现有部署。 当你在任务序列属性中更改此性能设置时，它不会影响任务序列的任何现有部署。 要启用或禁用此设置以提高性能，请创建新的任务序列部署。
<!-- MEMDocs#437, SCCMDocs#2107 -->

## <a name="distribute-referenced-content"></a><a name="BKMK_DistributeTS"></a>分发引用的内容  

在客户端运行引用内容的任务序列之前，将该内容分发到分发点。 你可以随时选择任务序列并分发其内容，以便为分发建立一个新的引用包列表。 如果使用更新的内容更改任务序列，则在内容可供客户端使用之前重新分发此内容。 使用以下过程来分发任务序列引用的内容。  

### <a name="process-to-distribute-referenced-content-to-distribution-points"></a>将引用的内容分发到分发点的过程  

1. 在 Configuration Manager 控制台中，转到“软件库”工作区，展开“操作系统”，然后选择“任务序列”节点。  

2. 在“任务序列”列表中，选择要分发的任务序列。  

3. 在功能区的“主页”选项卡上，在“部署”组中，选择“分发内容”。 此操作会启动“分发内容向导”。  

4. 在“常规”页上，验证是否为分发选择了正确的任务序列。  

5. 在“内容”页上，验证要分发的内容（例如任务序列引用的启动映像）。  

6. 在“内容目标”页上，指定要在其中分发任务序列内容的集合、分发点或分发点组。  

    > [!IMPORTANT]  
    > 如果所选任务序列引用已分发到特定分发点的内容，则向导不会列出该分发点。  

7. 完成向导。  

还可以预留任务序列中引用的内容。 Configuration Manager 创建压缩的预安排内容文件，该文件包含所选内容的文件、关联依赖项和关联元数据。 然后在站点服务器、辅助站点或分发点中手动导入内容。 有关如何预留内容文件的详细信息，请参阅[预留内容](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage)。  

## <a name="deploy"></a><a name="BKMK_DeployTS"></a> 部署  

有关详细信息，请参阅 [Deploy a task sequence](deploy-a-task-sequence.md)。

## <a name="export-and-import"></a><a name="BKMK_ExportImport"></a>导出和导入  

导出和导入任务序列（包含或不包含相关对象）。 此引用的内容包括以下对象：  

- OS 映像  
- 启动映像  
- 包（如客户端安装包）  
- 驱动程序包  
- 具有依赖项的应用程序  

导出和导入任务序列时，请考虑以下几点：  

- Configuration Manager 不会在任务序列中导出密码。 如果导出和导入包含密码的任务序列，则编辑导入的任务序列，以重新输入任何密码。 请查看以下可能包含密码的步骤：  

  - [加入域或工作组](../understand/task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)  
  - [连接到网络文件夹](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)  
  - [运行命令行](../understand/task-sequence-steps.md#BKMK_RunCommandLine)  

- 使用“设置动态变量”步骤导出任务序列时，Configuration Manager 不会为配置了“机密值”设置的变量导出值。 导入任务序列后，请重新输入这些变量的值。  

- 如果你具有多个主站点，请在管理中心站点导入任务序列。  

### <a name="process-to-export-task-sequences"></a>导出任务序列的过程  

1. 在 Configuration Manager 控制台中，转到“软件库”工作区，展开“操作系统”，然后选择“任务序列”节点。  

2. 在“任务序列”列表中，选择要导出的任务序列。 如果选择多个任务序列，它们将全部存储在一个导出文件上。  

3. 在功能区的“主页”选项卡上，在“任务序列”组中，选择“导出”  。 此操作会启动“导出任务序列向导”。  

4. 在“常规”  页上，指定下列设置：  

    - **文件**：指定导出文件的位置和名称。 如果直接输入文件名，请确保在文件名中包括 .zip 扩展名。 如果浏览导出文件，则向导会自动添加此文件扩展名。  

    - 如果不想导出任务序列依赖项，请取消选中“导出所有任务序列依赖项”选项。 默认情况下，向导会扫描所有相关对象并与任务序列一起导出它们。 这包括应用程序的任何依赖项。  

    - 如果不想将包源中的内容复制到导出位置，请取消选中“导出所选任务序列和依赖项的所有内容”选项。 如果选择此选项，“导入任务序列向导”会使用导入路径作为新包源位置。  

    - **管理员备注**：添加要导出的任务序列的说明。  

5. 完成向导。  

该向导会创建以下输出文件：  

- 如果不导出内容，则为一个 .zip 文件。  

- 如果导出内容，则为一个 .zip 文件和一个名为 *export*_files 的文件夹，其中 *export* 是包含导出内容的 .zip 文件的名称。  

如果导出任务序列时包括内容，请确保复制 .zip 文件和 export_files 文件夹，否则导入将失败。  

### <a name="process-to-import-task-sequences"></a>导入任务序列的过程  

1. 在 Configuration Manager 控制台中，转到“软件库”工作区，展开“操作系统”，然后选择“任务序列”节点。  

2. 在功能区的“主页”选项卡上，在“创建”组中，选择“导入任务序列”  。 此操作会启动“导入任务序列向导”。  

3. 在功能区的“常规”页上，指定导出的 .zip 文件。  

4. 在“文件内容”页上，为要导入的每个对象选择所需的操作。 此页显示已找到的 Configuration Manager 要导入的所有对象。  

    - 如果从未导入对象，请选择“新建”。  

    - 如果以前导入过对象，请选择下列操作之一：  

        - **忽略重复项**（默认值）：此操作不导入对象。 而是由向导将现有对象链接到任务序列。  

        - **覆盖**：此操作用导入的对象覆盖现有对象。 对于应用程序，你可以添加修订以更新现有应用程序或创建新应用程序。  

5. 完成向导。  

导入任务序列之后，请编辑任务序列以指定原始任务序列中的任何密码。 出于安全原因，不会导出密码。  

## <a name="return-to-previous-page-on-failure"></a>发生故障时返回到上一页面

如果运行任务序列时发生故障，可以返回到任务序列向导的上一页面。 在以前版本的 Configuration Manager 中，出现故障时必须重启任务序列。 在以下应用场景中使用“上一页”按钮：

- 当计算机在 Windows PE 中启动时，任务序列可用之前可能会先显示任务序列启动对话框。 在此应用场景中选择“下一步”时，会显示任务序列的最后一页，同时显示一条消息，指示无可用的任务序列。 现在，可选择“上一页”以再次搜索可用任务序列。 在出现可用任务序列之前，可重复此过程。  

- 运行任务序列但分发点上尚无可用从属内容包时，任务序列会失败。 如果缺少的内容尚未分发，请立即将其分发。 或等待分发点提供该内容。 然后选择“上一页”，让任务序列再次搜索该内容。

## <a name="collection-and-device-variables"></a><a name="BKMK_CreateTSVariables"></a> 集合和设备变量

可以为计算机和集合定义自定义的任务序列变量。 为计算机定义的变量称为特定于计算机的任务序列变量。 为集合定义的变量称为特定于集合的任务序列变量。 有关详细信息，请参阅[集合和设备变量](../understand/using-task-sequence-variables.md#bkmk_set-coll-var)。

## <a name="additional-actions"></a><a name="BKMK_AdditionalActionsTS"></a>其他操作  

选择任务序列时，可以使用其他操作来管理任务序列。  

### <a name="edit"></a>编辑

有关详细信息，请参阅[使用任务序列编辑器](../understand/task-sequence-editor.md#bkmk_edit)。

### <a name="enable"></a>启用

启用任务序列，以便其能在客户端运行。 不需要在启用后重新部署任务序列。  

### <a name="disable"></a>禁用

禁用任务序列，使其无法在计算机上运行。 可以部署禁用的任务序列，但在启用之前计算机不会运行任务序列。  

### <a name="export"></a>导出

有关详细信息，请参阅[导出和导入任务序列](#BKMK_ExportImport)。

### <a name="copy"></a>复制

为所选的任务序列创建副本。 在根据现有任务序列创建新的任务序列时，此操作很有用。

为某个文件夹中的任务序列创建副本时，副本会在该文件夹中列出，直至你刷新任务序列节点为止。 刷新后，副本将出现在根文件夹中。  

### <a name="refresh"></a>刷新

刷新所选任务序列的详细信息。

### <a name="delete"></a>删除

删除所选的任务序列。

### <a name="create-phased-deployment"></a>创建分阶段部署

有关详细信息，请参阅[创建分阶段部署](create-phased-deployment-for-task-sequence.md)。

### <a name="deploy"></a>部署

有关详细信息，请参阅 [Deploy a task sequence](deploy-a-task-sequence.md)。

### <a name="distribute-content"></a>分发内容

启动“分发内容向导”将引用的内容发送到分发点。

### <a name="create-prestaged-content-file"></a>创建预留的内容文件

启动“创建预留的内容文件向导”以预留任务序列内容。 有关如何创建预留的内容文件的信息，请参阅[预安排内容](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage)。

### <a name="move"></a>移动

将所选的任务序列移动到“任务序列”节点中的另一个文件夹。

### <a name="set-security-scopes"></a>设置安全作用域

选择所选任务序列的安全作用域。 有关详细信息，请参阅 [安全作用域](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope)。

### <a name="properties"></a>属性

有关详细信息，请参阅[配置软件中心属性](#bkmk_prop-general)并[配置高级任务序列设置](#bkmk_prop-advanced)。

### <a name="view"></a>查看

<!--3633146-->
从版本 1902 开始，任务序列上的“查看”操作是默认设置。 通过此操作可以查看任务序列的步骤，而无需将其锁定以进行编辑。 有关详细信息，请参阅[使用任务序列编辑器](../understand/task-sequence-editor.md#bkmk_view)。

## <a name="see-also"></a>另请参阅

- [部署企业版操作系统的方案](scenarios-to-deploy-enterprise-operating-systems.md)

- [使用任务序列编辑器](../understand/task-sequence-editor.md)

- [部署任务序列](deploy-a-task-sequence.md)

- [任务序列步骤](../understand/task-sequence-steps.md)

- [集合和设备变量](../understand/using-task-sequence-variables.md#bkmk_set-coll-var)

- [创建分阶段部署](create-phased-deployment-for-task-sequence.md)
