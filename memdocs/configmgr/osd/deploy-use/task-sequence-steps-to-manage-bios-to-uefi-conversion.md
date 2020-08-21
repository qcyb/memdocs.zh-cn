---
title: 将 BIOS 转换为 UEFI
titleSuffix: Configuration Manager
description: 了解如何自定义 OS 部署任务序列，以便为转换到 UEFI 准备 FAT32 分区。
ms.date: 05/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: bd3df04a-902f-4e91-89eb-5584b47d9efa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bf108cec074129f9b70e7cd2658cf2b1c8c10bc2
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697902"
---
# <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>管理 BIOS 转换为 UEFI 所采用的任务序列步骤

Windows 10 提供了许多需要启用 UEFI 的设备的新安全功能。 你可能拥有支持 UEFI 的较新的 Windows 设备，但正在使用旧版 BIOS。 以前，将设备转换为 UEFI 需要你转到每台设备、对硬盘重新分区并重新配置固件。

通过 Configuration Manager，你可以自动化以下操作：

- 准备硬盘驱动器以便从 BIOS 转换为 UEFI
- 在就地升级过程中从 BIOS 转换为 UEFI
- 在硬件清单中收集 UEFI 信息

## <a name="hardware-inventory-collects-uefi-information"></a>硬件清单将收集 UEFI 信息

硬件清单类 (SMS_Firmware) 和属性 (UEFI) 可帮助确定是否以 UEFI 模式启动计算机 。 如果以 UEFI 模式启动计算机，则 **UEFI** 属性设为 **TRUE**。 硬件清单默认启用此类。 有关硬件清单的详细信息，请参阅[如何配置硬件清单](../../core/clients/manage/inventory/configure-hardware-inventory.md)。

## <a name="create-a-custom-task-sequence-to-prepare-the-hard-drive"></a>创建自定义任务序列以准备硬盘驱动器

你可以使用 TSUEFIDrive 变量自定义 OS 部署任务序列。 “重启计算机”步骤会准备硬件驱动器上的 FAT32 分区，以便转换为 UEFI。 以下过程提供了有关如何创建任务序列步骤以执行此操作的示例。

### <a name="prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>为转换到 UEFI 准备 FAT32 分区

在现有的用于安装 OS 的任务序列中，添加一个新组，并包含将 BIOS 转换为 UEFI 的步骤。

1. 在捕获文件和设置之后，并在安装 OS 之前，创建新的任务序列组。 例如，在“捕获文件和设置”组之后创建名为“BIOS-to-UEFI”的组。

1. 在新组的“选项”选项卡中，添加一个新的任务序列变量作为条件。 设置“_SMSTSBootUEFI not equal true”。 在此条件下，任务序列仅在 BIOS 设备上运行这些步骤。

    :::image type="content" source="media/bios-to-uefi-group.png" alt-text="BIOS 转 UEFI 组的条件":::

1. 在新组中，添加“重启计算机”任务序列步骤。 在“指定重启后要运行的内容”中，选择“已选择分配给此任务序列的启动映像” 。 此操作将在 Windows PE 中重启计算机。

1. 在“选项”选项卡中，添加一个任务序列变量作为条件。 设置“_SMSTSInWinPE equals false”。 在此条件下，如果计算机已使用 Windows PE，则任务序列不会运行此步骤。

    :::image type="content" source="media/restart-in-windows-pe.png" alt-text="“重启计算机”步骤的条件":::

1. 添加以下步骤：启动可将固件从 BIOS 转换为 UEFI 的 OEM 工具。 此步骤通常为“运行命令行”，其中包含用于运行 OEM 工具的命令。

1. 添加“格式化磁盘并分区”任务序列步骤。 在此步骤中，配置以下选项：

    1. 创建要在在安装 OS 前转换为 UEFI 的 FAT32 分区。 对于“磁盘类型”，选择“GPT” 。

        :::image type="content" source="media/format-and-partition-disk.png" alt-text="“格式化磁盘并分区”步骤的配置":::

    1. 转到 FAT32 分区的属性。 在“变量”字段中，输入 `TSUEFIDrive`。 当任务序列检测到此变量时，它将为 UEFI 转换准备分区，准备就绪后会重启计算机。

        :::image type="content" source="media/partition-properties.png" alt-text="FAT32 分区属性的配置":::

    1. 创建 NTFS 分区，任务序列使用此分区保存其状态和存储日志文件。

1. 添加另一个“重启计算机”任务序列步骤。 在“指定重启后要运行的内容”中，选择“已选择分配给此任务序列的启动映像”以在 Windows PE 中启动计算机。

    > [!TIP]
    > 默认情况下，EFI 分区的大小为 500 MB。 在某些环境中，启动映像过大而无法存储在此分区中。 若要解决此问题，请增加 EFI 分区的大小。 例如，将其大小设为 1 GB。<!-- SCCMDocs#1024 -->

## <a name="convert-from-bios-to-uefi-during-in-place-upgrade"></a><a name="bkmk_ipu"></a> 就地升级过程中从 BIOS 转换为 UEFI

Windows 10 包括一个简单的转换工具，MBR2GPT。 它自动化了对启用 UEFI 的硬件进行硬盘重新分区的过程。 可将转换工具集成到 Windows 10 的就地升级过程中。 将此工具与升级任务序列和用于将固件从 BIOS 转换为 UEFI 的 OEM 工具结合使用。

### <a name="requirements"></a>要求

- 支持的 Windows 10 版本
- 支持 UEFI 的计算机
- 将计算机固件从 BIOS 转换为 UEFI 的 OEM工具

### <a name="process-to-convert-from-bios-to-uefi-during-an-in-place-upgrade-task-sequence"></a>就地升级任务序列期间从 BIOS 转换为 UEFI 的过程

1. [创建用于升级 OS 的任务序列](create-a-task-sequence-to-upgrade-an-operating-system.md)

1. 编辑任务序列。 在“后处理”组中，进行以下更改：

    1. 添加“运行命令行”步骤。 指定 MBR2GPT 工具的命令行。 在完整的 OS 中运行时，将其配置为在不修改或删除数据的情况下将磁盘从 MBR 转换为 GPT。 在命令行中，输入以下命令：`MBR2GPT.exe /convert /disk:0 /AllowFullOS`

    > [!TIP]
    > 你也可以选择在 Windows PE 中运行 MBR2GPT.EXE 工具，而不是在完整的 OS 中运行。 添加以下步骤：在运行 MBR2GPT.EXE 工具的步骤前以 Windows PE 模式重启计算机。 然后从命令行删除“/AllowFullOS”选项。

    有关该工具和可用选项的详细信息，请参阅 [MBR2GPT.EXE](/windows/deployment/mbr-to-gpt)。

    1. 添加以下步骤：运行可将固件从 BIOS 转换为 UEFI 的 OEM 工具。 此步骤通常为“运行命令行”，其中包含运行 OEM 工具的命令行。

    1. 添加“重启计算机”步骤，并选择“当前安装的默认操作系统” 。

1. 部署任务序列。