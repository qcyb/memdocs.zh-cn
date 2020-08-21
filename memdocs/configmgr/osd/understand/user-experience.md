---
title: 操作系统部署的用户体验
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 中操作系统部署的任务序列进度和媒体向导等用户体验。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 58849e40-30d5-4153-84b3-ca4af3a4f09d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7ad20f80f4727fe18947bed05ded6e7b107fab12
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124078"
---
# <a name="user-experiences-for-os-deployment"></a>操作系统部署的用户体验

适用范围：  Configuration Manager (Current Branch)

[部署任务序列](../deploy-use/deploy-a-task-sequence.md)后，用户可以根据情况采用不同的方式与部署进行交互。 本文介绍了操作系统部署的主要用户体验以及如何配置它们：

- 针对影响重大的部署的软件中心用户通知
- PXE 启动体验示例
- 媒体中的任务序列向导
- 任务序列运行时的进度窗口
- 任务序列失败时的错误窗口

## <a name="software-center"></a>软件中心

对于影响重大的部署，可以自定义软件中心显示的消息。 当用户在软件中心打开操作系统部署时，他们会看到类似于以下窗口的消息：

![软件中心中面向最终用户的自定义任务序列通知](../media/user-notification-enduser.png)

有关如何自定义此窗口中的消息的详细信息，请参阅[为高风险部署创建自定义通知](../deploy-use/manage-task-sequences-to-automate-tasks.md#create-a-custom-notification-for-high-risk-deployments)。

还可以在窗口顶部自定义组织名称。 （上面的示例显示的是默认值 `IT Organization`）。 更改“计算机代理”组中的“组织名称”客户端设置   。 有关详细信息，请参阅[关于客户端设置](../../core/clients/deploy/about-client-settings.md#computer-agent)。

<!--
optional vs required
**Allow user to interact** on required deployment?
-->

有关详细信息，请参阅[使用软件中心通过网络部署 Windows](../deploy-use/use-software-center-to-deploy-windows-over-the-network.md)。

## <a name="pxe"></a>PXE

对于 PXE，不同的硬件型号有不同的体验。 若要启动到网络，基于 UEFI 的设备通常使用 `Enter` 键，而基于 BIOS 的设备使用 `F12` 键。

以下示例显示了 Hyper-V Gen1 (BIOS) PXE 体验：

![Hyper-V 虚拟机的 BIOS PXE 屏幕示例](media/hyperv-pxe.png)

设备通过 PXE 成功启动后，其行为与可启动媒体类似。 有关详细信息，请参阅下一节[任务序列向导](#task-sequence-wizard)。

有关详细信息，请参阅[使用 PXE 通过网络部署 Windows](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)。

> [!WARNING]
> 如果使用 PXE 部署，并在配置设备硬件时将网络适配器作为第一个启动设备，则这些设备可以自动启动 OS 部署任务序列而无需用户交互。 部署验证不会管理此配置。 尽管此配置可以简化流程并减少用户交互，但它会增加设备意外重置映像的风险。

## <a name="task-sequence-wizard"></a>任务序列向导

当你使用[任务序列媒体](../deploy-use/create-task-sequence-media.md)时，将运行任务序列向导以引导该过程。

### <a name="welcome-to-the-task-sequence-wizard"></a>欢迎使用任务序列向导

![任务序列向导主页的屏幕截图](media/welcome-task-sequence-wizard.png)

- 如果你对媒体进行密码保护，则用户必须在此欢迎页面上输入密码。

- 选择“配置网络设置”以指定静态 IP 地址或其他自定义网络设置  。 否则，设备默认使用 DHCP。

- 如果网络需要代理，请选择“配置代理设置”  。

### <a name="select-a-task-sequence-to-run"></a>选择要运行的任务序列

如果将多个任务序列部署到设备，则会显示此页面，以供你选择任务序列。 确保为任务序列使用用户可以理解的名称和描述。

![任务序列向导的任务序列选择页面的屏幕截图](media/task-sequence-wizard-select.png)

### <a name="edit-task-sequence-variables"></a>编辑任务序列变量

只要任意任务序列变量的值为空，向导就会显示一个用于编辑变量值的页面。

![任务序列向导的编辑任务序列变量页面的屏幕截图](media/task-sequence-wizard-variables.png)

## <a name="prestart-commands"></a>预启动命令

可以自定义任务序列媒体或启动映像以运行预启动命令。 预启动命令在任务序列开始之前运行。 下面是一些较常见的操作：

- 提示用户输入动态值，例如计算机名称
- 指定网络配置
- 设置用户设备相关性

预启动命令是使用脚本或程序指定的命令行。 此用户体验是该脚本或程序所独有的。

有关详细信息，请参阅下列文章：

- [任务序列媒体的预启动命令](prestart-commands-for-task-sequence-media.md)
- [管理启动映像](../get-started/manage-boot-images.md#customization)
- [任务序列媒体](../deploy-use/create-task-sequence-media.md)

## <a name="task-sequence-progress"></a>任务序列进度

当任务序列运行时，它会显示“安装进度”窗口  ：

![任务序列进度窗口示例](media/task-sequence-progress.png)

- 此窗口始终位于最上面；你可以移动它，但不能将其关闭或最小化。

- 可以在窗口顶部自定义组织名称。 （上面的示例显示的是默认值 `IT Organization`）。 更改“计算机代理”组中的“组织名称”客户端设置   。 有关详细信息，请参阅[关于客户端设置](../../core/clients/deploy/about-client-settings.md#computer-agent)。

    > [!TIP]
    > 任务序列将此值存储在只读变量 [_SMSTSOrgName](task-sequence-variables.md#SMSTSOrgName) 中。

- 可以自定义副标题。 （上面的示例显示的是默认值 `Running: <task sequence name>`。）在任务序列的属性上，为进度通知文本选择“使用自定义文本”选项  。 最多允许 255 个字符。

- **正在运行的操作**：第一行显示当前任务序列步骤的名称。 它下方的进度条显示任务序列的整体完成情况。

- 第二行仅针对某些步骤显示，用于提供更详细的进度。

- 使用任务序列变量 [TSDisableProgressUI](task-sequence-variables.md#TSDisableProgressUI) 来控制任务序列何时显示进度。

    若要完全禁用进度窗口，请在任务序列部署的“用户体验”页面上禁用“显示任务序列进度”选项   。

从版本 2002 开始，任务序列进度窗口包括以下改进：<!--5932692-->

- 显示当前步骤号、步骤总数和完成百分比

- 增加了窗口的宽度，为你提供更多空间，以便更好地在单个行中显示组织名称

![任务序列进度窗口示例](media/2356386-task-sequence-progress.png)

默认情况下，任务序列进度窗口使用现有文本。 如果不进行任何更改，它将延续 1910 及更低版本中的行为方式。 若要显示新的进度信息，请指定任务序列变量 [TSProgressInfoLevel](task-sequence-variables.md#TSProgressInfoLevel)。

计数和完成百分比仅适用于常规指南。 这些值基于任务序列中的步骤总数。 对于更复杂的任务序列，比如包含基于任务序列逻辑按条件运行的步骤的任务序列，进度可能是非线性的。

步骤总数不包括任务序列中的以下各项：

- 组。 此项是其他步骤的容器，而不是步骤本身。

- “运行任务序列”步骤的实例  。 此步骤是其他步骤的容器。

- 显式禁用的步骤。 禁用的步骤不会在任务序列期间运行。

- 自版本 2006 起，它不会对已禁用组中的已启用步骤进行计数。<!--6448412--> 在版本 2002 中，已禁用组中的已启用步骤仍包含在总计数中。

## <a name="task-sequence-error"></a>任务序列错误

如果任务序列失败，它会显示“任务序列错误”窗口。

![任务序列错误窗口示例](media/task-sequence-error.png)

- 可以像在任务序列进度窗口中一样自定义标题信息。

- 它为用户显示任务序列的名称、错误代码和常规消息。 例如：`Task sequence: Upgrade to Windows 10 Enterprise has failed with the error code (0x80004005). For more information, contact your system administrator or helpdesk operator.`

- 超时期限过后，此窗口会自动关闭。 默认情况下，此超时时间为 15 分钟。 可以使用任务序列变量 [SMSTSErrorDialogTimeout](task-sequence-variables.md#SMSTSErrorDialogTimeout) 自定义此值。
