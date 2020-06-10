---
title: 使用维护时段
titleSuffix: Configuration Manager
description: 使用集合和维护时段在 Configuration Manager 中有效管理客户端。
ms.date: 06/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4564ebcb-41a8-4eb0-afdb-2e1f0795cfa2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0b81599c6c5e4dda418b69c6e3c6d3b8cd144253
ms.sourcegitcommit: 92e6d2899b1cf986c29c532d0cd0555cad32bc0c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2020
ms.locfileid: "84428551"
---
# <a name="how-to-use-maintenance-windows-in-configuration-manager"></a>如何在 Configuration Manager 中使用维护时段

适用范围：Configuration Manager (Current Branch)

使用维护时段定义 Configuration Manager 可以在设备上运行影响任务的时间。 维护时段可帮助确保在不影响工作效率的时间进行客户端配置更改。 在软件中心，用户可以在“安装状态”选项卡上看到设备的下一个维护时段。 <!--1358131-->

以下任务支持维护时段：

- 应用程序和包部署

- 软件更新部署

- 符合性设置部署和评估

- 操作系统和自定义任务序列部署

配置维护时段的生效日期、开始和结束时间以及定期模式。 时段的最长持续时间必须小于 24 小时。 控制台不允许一个维护时段超过 24 小时。 例如，如果想要允许在星期六和星期日全天进行维护，请针对这两天创建两个 24 小时维护时段。<!-- MEMDocs#310 -->

默认情况下，不允许在维护时段外进行部署所导致的计算机重启，但可以替代默认设置。 维护时段仅影响部署运行的时间。 配置为下载并在本地运行的部署可以在此时段之外下载内容。

如果客户端是具有维护时段的设备集合的成员，那么只有在允许的最长运行时间未超出时段持续时间时，部署才会运行。 如果部署运行失败，客户端会生成一个警报。 然后，它会在具有可用时间的下一个计划的维护时段重新运行部署。

## <a name="multiple-maintenance-windows"></a>多个维护时段

如果客户端计算机是具有维护时段的多个设备集合的成员，则以下规则适用：  

- 如果维护时段未重叠，则客户端会将它们视为两个独立的维护时段。

- 如果维护时段重叠，则客户端会将它们视为单个时段，即两个时段的所有时间。 例如，你在一个集合上创建两个维护时段。 第一个维护时段有效时间为 6:00 到 7:00，第二个维护时段有效时间为 6:30 到 7:30。 由于它们重叠了30分钟，因此合并后的维护时段的有效持续时间为 90 分钟，即从 6:00 到 7:30。

当用户从软件中心安装应用程序时，客户端会立即启动该应用程序。 它优先执行用户意图，而非管理员意图。

如果目的为“必需”的应用程序部署在非营业时间（由用户在软件中心中配置）内达到其安装期限，客户端将安装应用程序。 它优先于用户意图执行管理员意图。

默认情况下，具有多个维护时段时，客户端仅在“软件更新”类型时段安装软件更新。 它将忽略任何“所有部署”维护时段，除非它们是唯一的类型。 你可以在“软件更新”组中通过以下客户端设置配置此行为：当“软件更新”维护时段可用时，在“所有部署”维护时段中启用软件更新安装。 有关详细信息，请参阅[关于客户端设置](../../deploy/about-client-settings.md#bkmk_SUMMaint)。<!-- SCCMDocs#1317 -->

> [!NOTE]
> 此设置还适用于配置为应用于“任务序列”的维护时段。<!-- SCCMDocs-pr #4596 -->
>
> 如果客户端只有“所有部署”时段可用，它仍会在该时段内安装软件更新或任务序列。

## <a name="configure-maintenance-windows"></a>配置维护时段

1. 在 Configuration Manager 控制台中，转到“资产和符合性”工作区。

1. 选择“设备集合”节点，然后选择一个集合。

    > [!NOTE]
    > 无法为“所有系统”集合创建维护时段。

1. 在功能区“主页”选项卡的“属性”组中，选择“属性”  。

1. 切换到“维护时段”选项卡，然后选择“新建”图标。

    1. 指定“名称”以唯一标识集合的此维护时段。

    1. 配置“时间”设置：

        - 生效日期：维护时段的开始日期。 默认值为当前日期。

        - “开始”和“结束” ：维护时段的开始和结束时间。 它计算时段的“持续时间”。 最短持续时间为五分钟，最大持续时间为 24 小时。 默认持续时间为三小时，从 01:00 到 04:00。

        - 通用协调时间 (UTC)：启用此选项，以使客户端解释 UTC 时区的开始和结束时间。 对于同一集合中的区域或全球分布式设备，此选项会将维护时段同时用于集合中的所有设备。 禁用此选项，以便客户端使用设备的本地时区。 默认情况下禁用此选项。

    1. 配置定期模式。 默认设置是在每周的当前日期执行一次。

    1. 将此计划应用于：默认情况下，时段适用于“所有部署”。 你可以选择“软件更新”或“任务序列”以进一步控制在此时段运行的部署。

        > [!TIP]
        > 如果你在同一集合上配置不同类型的多个维护时段，请确保你了解客户端行为。 有关详细信息，请参阅[多个维护时段](#multiple-maintenance-windows)。

1. 选择“确定”，保存并关闭时段。

集合属性的“维护时段”选项卡显示所有已配置的时段。

## <a name="use-powershell"></a><a name="bkmk_powershell"></a> 使用 PowerShell

PowerShell 可用于配置维护时段。 有关详细信息，请参阅下列文章：

- [Get-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmmaintenancewindow?view=sccm-ps)
- [New-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmmaintenancewindow?view=sccm-ps)
- [Remove-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmmaintenancewindow?view=sccm-ps)
- [Set-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmmaintenancewindow?view=sccm-ps)
