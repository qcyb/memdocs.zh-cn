---
title: 升级到 Windows 10
titleSuffix: Configuration Manager
description: 了解如何使用 Configuration Manager 将操作系统从 Windows 7 或更高版本升级到 Windows 10。
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: c21eec87-ad1c-4465-8e45-5feb60b92707
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a9ed8e1ece27117993761a3ce52c462e94e9f79a
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124767"
---
# <a name="upgrade-windows-to-the-latest-version-with-configuration-manager"></a>使用 Configuration Manager 将 Windows 升级到最新版本

适用范围：  Configuration Manager (Current Branch)

本文介绍在 Configuration Manager 中升级计算机操作系统的步骤。 你可以在不同的部署方法（如独立媒体或软件中心）中进行选择。 “就地升级”方案具有以下特点：  

- 将 OS 升级到 Windows 10 或 Windows Server 2016 及更高版本

- 保留计算机上的应用程序、设置和用户数据

- 没有 Windows ADK 等外部依赖关系

- 比传统操作系统部署更快、更具弹性

> [!Note]  
> Windows 10 就地升级任务序列支持部署到通过[云管理网关](../../core/clients/manage/cmg/plan-cloud-management-gateway.md)托管的 Internet 客户端。 此功能可让远程用户更轻松地升级到 Windows 10，无需连接 Intranet。 有关详细信息，请参阅[通过 CMG 部署 Windows 10 就地升级](deploy-a-task-sequence.md#deploy-windows-10-in-place-upgrade-via-cmg)。 <!-- 1357149 -->


## <a name="supported-versions"></a>支持的版本

### <a name="upgrade-version"></a>升级版本

只创建用于升级到以下 OS 版本的 OS 升级包：

- Windows 10
- Windows Server 2016
- Windows Server 2019

### <a name="original-version"></a>原始版本

设备必须运行以下 OS 版本之一，才能定目标到 OS 升级任务序列：

#### <a name="windows-client"></a>Windows 客户端

- Windows 7
- Windows 8.1
- 旧版 Windows 10。 例如，可以将 1809 版本的 Windows 10 升级到 1903 版本的 Windows 10。  

有关详细信息，请参阅 [Windows 10 升级路径](https://docs.microsoft.com/windows/deployment/upgrade/windows-10-upgrade-paths)。

#### <a name="windows-server"></a>Windows Server

- Windows Server 2012
- Windows Server 2012 R2
- 旧版 Windows Server 2016
- 旧版 Windows Server 2019

若要详细了解 Windows Server 支持的升级路径，请参阅 [Windows Server 2016 支持的升级路径](https://docs.microsoft.com/windows-server/get-started/supported-upgrade-paths#upgrading-previous-retail-versions-of-windows-server-to-windows-server-2016)和 [Windows Server 升级中心](https://aka.ms/upgradecenter)。


## <a name="plan"></a><a name="BKMK_Plan"></a> 计划  

### <a name="task-sequence-requirements-and-limitations"></a>任务序列要求和限制

查看使用任务序列升级操作系统时的要求和限制，以确保其满足你的需要：  

- 仅添加与操作系统升级的核心任务相关的任务序列步骤。 这些步骤主要包括安装包、应用程序或更新。 还会用到用于运行命令行、PowerShell 或设置动态变量的步骤。  

- 审阅计算机上安装的驱动器和应用程序。 在部署升级任务序列前，请确保驱动器与 Windows 10 兼容。  

以下任务与就地升级不兼容。 它们需要使用传统的操作系统部署：  

- 更改计算机域成员身份或更新本地管理员组。  

- 在计算机上实现基础更改，例如：

  - 更改磁盘分区
  - 将系统体系结构从 x86 改为 x64
  - 实现 UEFI。 （有关可选操作的更多信息，请参阅[在就地升级过程中从 BIOS 转换到 UEFI](task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu)。）
  - 修改基本操作系统语言  

- 你有自定义要求，包括使用自定义基本映像、使用第三方磁盘加密或要求 WinPE 脱机操作。  

### <a name="infrastructure-requirements"></a>基础结构要求  

该升级方案的唯一先决条件是具备可用的分发点。 分发操作系统升级包和任务序列中包含的任何其他包。 有关详细信息，请参阅[安装或修改分发点](../../core/servers/deploy/configure/install-and-configure-distribution-points.md)。


## <a name="configure"></a><a name="BKMK_Configure"></a> 配置  

### <a name="prepare-the-os-upgrade-package"></a>准备 OS 升级包  

Windows 10 升级包包含在目标计算机上升级操作系统所必需的源文件。 此升级包的版本、体系结构和语言必须与将升级的客户端的相同。 有关详细信息，请参阅[管理 OS 升级包](../get-started/manage-operating-system-upgrade-packages.md)。  

### <a name="create-a-task-sequence-to-upgrade-the-os"></a>创建用于升级操作系统的任务序列  

使用[创建用于升级操作系统的任务序列](create-a-task-sequence-to-upgrade-an-operating-system.md)中的步骤自动升级操作系统。  

> [!NOTE]  
> 通常使用[创建用于升级操作系统的任务序列](create-a-task-sequence-to-upgrade-an-operating-system.md)中的步骤来创建任务序列，将操作系统升级到 Windows 10。 任务序列包括“升级操作系统”步骤以及用于处理端到端升级过程的其他建议步骤和组  。
>
> 可以创建自定义任务序列，并添加[“升级 OS”](../understand/task-sequence-steps.md#BKMK_UpgradeOS)步骤。 这是将操作系统升级到 Windows 10 所需的唯一步骤。 如果选择此方法，还要在“升级操作系统”步骤后添加[重启计算机](../understand/task-sequence-steps.md#BKMK_RestartComputer)步骤才能完成升级  。 请务必使用“当前安装的默认操作系统”  设置，将计算机重启到已安装的操作系统而不是 Windows PE。  


## <a name="deploy"></a><a name="BKMK_Deploy"></a> 部署  

使用下列部署方法之一部署操作系统：  

- [使用软件中心通过网络部署 Windows](use-software-center-to-deploy-windows-over-the-network.md)  

- [使用独立媒体部署 Windows，而不使用网络](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

  > [!IMPORTANT]  
  > 使用独立媒体时，必须在任务序列中添加启动映像。 此配置让任务序列在任务序列媒体向导中可用。


## <a name="monitor"></a>监视  

若要监视任务序列部署以升级操作系统，请参阅[监视操作系统部署](monitor-operating-system-deployments.md)。  
