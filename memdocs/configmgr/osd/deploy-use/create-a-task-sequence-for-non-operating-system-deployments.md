---
title: 创建非 OS 部署的任务序列
titleSuffix: Configuration Manager
description: 创建不用于部署 OS 的任务序列，例如分发软件或自动执行任务
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 92aaec8a-8751-442a-b64b-62ab05b5bf50
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1c5ef6d4a17623428f299ff9df676dcba49e7f0c
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88698144"
---
# <a name="create-a-task-sequence-for-non-os-deployments"></a>创建非 OS 部署的任务序列

适用范围：  Configuration Manager (Current Branch)

Configuration Manager 中的任务序列用于自动在环境中执行不同类型的任务。 这些任务经过测试主要设计用于部署操作系统。 Configuration Manager 具有许多其他功能，这些功能应作为用于以下场景的主要技术：

- [应用程序安装](../../apps/understand/introduction-to-application-management.md)

    > [!NOTE]
    > 从版本 2002 开始，可以通过应用程序模型使用任务序列安装复杂的应用程序。 将部署类型添加到作为任务序列的应用，以安装或卸载应用。 有关详细信息，请参阅[创建 Windows 应用程序](../../apps/get-started/creating-windows-applications.md#bkmk_tsdt)。<!-- 3555953 -->

- [软件更新安装](../../sum/understand/software-updates-introduction.md)

- [设置配置](../../compliance/understand/ensure-device-compliance.md)

另外，还可以考虑使用诸如 [Orchestrator](/system-center/orchestrator/) 和 [Service Management Automation](/system-center/sma/) 等其他 Microsoft System Center 自动化技术。  

任务序列的强大功能在于其灵活性以及使用方式。 它们可以配置客户端设置、分发软件、更新驱动程序、编辑用户状态以及执行与 OS 部署无关的其他任务。 你可以创建自定义任务序列以添加任意数量的任务。 Configuration Manager 中支持使用非 OS 部署的自定义任务序列。 但是，如果任务序列导致不必要或不一致的结果，请设法简化操作：

- 使用更简单的步骤
- 将操作划分为多个任务序列
- 采用分阶段方法创建和测试任务序列

## <a name="supported-steps"></a>支持的步骤

支持将以下步骤用于非 OS 部署自定义任务序列：  

- [检查准备情况](../understand/task-sequence-steps.md#BKMK_CheckReadiness)  

- [连接到网络文件夹](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)  

- [下载包内容](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)  

- [安装应用程序](../understand/task-sequence-steps.md#BKMK_InstallApplication)  

- [安装包](../understand/task-sequence-steps.md#BKMK_InstallPackage)  

- [安装软件更新](../understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

- [重启计算机](../understand/task-sequence-steps.md#BKMK_RestartComputer)  

- [运行命令行](../understand/task-sequence-steps.md#BKMK_RunCommandLine)  

- [运行 PowerShell 脚本](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript)  

- [运行任务序列](../understand/task-sequence-steps.md#child-task-sequence)  

- [设置动态变量](../understand/task-sequence-steps.md#BKMK_SetDynamicVariables)  

- [设置任务序列变量](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable)  

## <a name="next-steps"></a>后续步骤

[创建自定义任务序列](create-a-custom-task-sequence.md)