---
title: 调试任务序列
titleSuffix: Configuration Manager
description: 使用任务序列调试工具对任务序列进行故障排除。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 4b60b0e1-ffa4-4fd5-864e-70a0546c8b3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 99ed8232a74b038b9b1cde4af257353252454c2b
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125145"
---
# <a name="debug-a-task-sequence"></a>调试任务序列

适用范围：  Configuration Manager (Current Branch)

<!--3612274-->

从版本 1906 开始，任务序列调试器是一种新型故障排除工具。 在调试模式下将任务序列部署到小集合。 这样便可通过可控方式单步执行任务序列，以帮助进行故障排除和调查。 调试器当前与任务序列引擎在同一设备上运行，它不是远程调试器。

> [!Note]  
> 在该 Configuration Manager 版本中，任务序列调试器是预发行功能。 若要启用此功能，请参阅[预发行功能](../../core/servers/manage/pre-release-features.md)。  


## <a name="prerequisites"></a>必备条件

- 更新目标设备上的 Configuration Manager 客户端

- 以本地“管理员”组中的用户身份登录到目标设备  。 仅为管理员运行调试器。

- 更新与任务序列关联的启动映像，以确保其具有最新的客户端版本


## <a name="start-the-tool"></a>启动工具

1. 在 Configuration Manager 工作区中，转到“软件库”工作区，展开“操作系统”，选择“任务序列”    。

1. 选择任务序列。 在功能区的部署组中，选择“调试”  。

    > [!Tip]  
    > 或者，在部署任务序列的集合或计算机对象上将变量“TSDebugMode”设置为 `TRUE` 。 设置了此变量的任何设备都会将部署给它的所有任务序列置于调试模式下。

1. 创建调试部署。 部署设置与常规任务序列部署相同。 有关详细信息，请参阅 [Deploy a task sequence](deploy-a-task-sequence.md#process)。

    > [!Note]  
    > 只能为调试部署选择一个小集合。 它仅显示包含 10 个或更少成员的设备集合。

自版本 1910 开始，使用新的任务序列变量 TSDebugOnError，以便在任务序列返回错误时自动启动调试程序  。<!-- 5012536 --> 有关详细信息，请参阅[任务序列变量 - TSDebugOnError](../understand/task-sequence-variables.md#TSDebugOnError)。

## <a name="use-the-tool"></a>使用此工具

任务序列在设备上运行时，“任务序列调试器”窗口将打开，类似于以下屏幕截图：

![任务序列调试器的屏幕截图](media/3612274-tsdebug.png)

调试器包含以下控件：

- **步骤**：从“当前”位置，仅运行任务序列中的下一步  。  

    > [!Note]  
    > 任务序列处于调试模式时，如果某个步骤返回严重错误，则任务序列不会按正常情况那样失败。 此行为允许你在进行外部更改后重试步骤。

- **运行**：从“当前”  位置，正常运行任务序列到结束或下一个“中断”点  （如果步骤失败）。 使用此操作之前，请确保使用“设置中断”操作设置断点  。

- **设置当前**：在调试器中选择一个步骤，然后选择“设置当前”  。 此操作将“当前”指针移动到该步骤  。 此操作允许跳过步骤或向后移动。  

    > [!Warning]  
    > 当你更改序列中的当前位置时，调试器不会考虑步骤的类型。 某些步骤可能会设置后续步骤进行条件评估时所需的任务序列变量。 如果运行顺序颠倒，某些步骤可能会失败或对设备造成重大损坏。 使用此选项需要自担风险。  

- **设置中断**：在调试器中选择一个步骤，然后选择“设置中断”  。 此操作将在调试器中添加“中断”点  。 “运行”任务序列时，它会在“中断”处停止   。  

    - 使用“运行”操作之前，请设置断点  。

    - 从版本 1910 开始，如果你在调试程序中创建断点，随后任务序列重新启动计算机，则调试程序将在重新启动后保留断点。<!-- 5012509 -->

    - 在版本 1906 中，计算机重新启动后不会保存断点，和[重新启动计算机](../understand/task-sequence-steps.md#BKMK_RestartComputer)步骤的情况一样。 例如，如果从软件中心启动用于映像任务序列的调试器，则不应在 Windows PE 阶段中设置中断。 计算机重新启动到 Windows PE 时，调试器会暂停任务序列，以便可以设置中断。

- **清除所有中断**：删除所有断点。

- **日志文件**：使用 [CMTrace](../../core/support/cmtrace.md) 打开当前任务序列日志文件 smsts.log  。 当任务序列引擎在“等待调试器”时，可以看到日志项目。

- **Cmd 提示**：在 Windows PE 中，打开命令提示符。

- **取消**：关闭调试器，使任务序列失败。

- **退出**：断开并关闭调试器，但任务序列继续正常运行。

“任务序列变量”窗口显示任务序列环境中所有变量的当前值  。 有关详细信息，请参阅[任务序列变量](../understand/task-sequence-variables.md)。 如果结合使用[设置任务序列变量](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable)步骤和选项“不显示此值”，则调试器不会显示变量值  。 无法编辑调试器中的变量值。

> [!Note]
> 某些任务序列变量仅供内部使用，不在参考文档中列出。

任务序列调试器在[重新启动计算机](../understand/task-sequence-steps.md#BKMK_RestartComputer)步骤后继续运行，但需要重新创建断点。 即使任务序列可能没有相应要求，但由于调试器需要用户交互，你仍需要登录到 Windows 才能继续。 如果在一小时后未登录，并在这种情况下继续调试，则任务序列将失败。

它还使用[运行任务序列](../understand/task-sequence-steps.md#child-task-sequence)步骤进入子任务序列。 “调试器”窗口会在显示主要任务序列步骤的同时显示子任务序列步骤。


## <a name="known-issues"></a>已知问题

如果通过多个部署向同一设备执行常规部署和调试部署，则任务序列调试器可能无法启动。


## <a name="see-also"></a>另请参阅

- [关于任务序列步骤](../understand/task-sequence-steps.md)
- [任务序列变量](../understand/task-sequence-variables.md)
- [如何使用任务序列变量](../understand/using-task-sequence-variables.md)
- [部署任务序列](deploy-a-task-sequence.md)
