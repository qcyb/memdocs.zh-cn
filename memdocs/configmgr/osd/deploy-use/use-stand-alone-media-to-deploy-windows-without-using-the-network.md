---
title: 使用独立介质部署 Windows
titleSuffix: Configuration Manager
description: 在带宽受到限制的情况下，使用 Configuration Manager 中的独立介质来部署 Windows，作为更新、安装或升级计算机的方式。
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 58a0d2ae-de76-401f-b854-7a5243949033
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 51b39e450fb5f8ffd7d83b4122d7514489383dfb
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124646"
---
# <a name="use-standalone-media-to-deploy-windows-without-using-the-network"></a>在不使用网络的情况下使用独立介质部署 Windows

适用范围：  Configuration Manager (Current Branch)

Configuration Manager 中的独立介质包含在计算机上部署 OS 所需的一切。 此介质包含启动映像、OS 映像、任务序列策略、应用程序、驱动程序等。 使用独立介质部署，可以在下列情况下部署操作系统：

- 在无法通过网络复制 OS 映像或其他大型包的环境中。

- 在没有网络连接或具有低带宽网络连接的环境中。

在以下 OS 部署方案中，使用独立介质：

- [使用新版的 Windows 刷新现有的计算机](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [在新计算机（裸机）上安装新版的 Windows](install-new-windows-version-new-computer-bare-metal.md)

- [将 Windows 升级到最新版本](upgrade-windows-to-the-latest-version.md)

完成其中一个 OS 部署方案中的步骤。 然后，根据以下部分来准备并创建独立介质。

## <a name="unsupported-task-sequence-actions"></a>不支持的任务序列操作

当你使用独立介质时，Configuration Manager 不支持以下任务序列操作：

- [自动应用驱动程序](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers)步骤。 不支持自动应用驱动程序目录中的设备驱动程序。 若要使一组特定的驱动程序可用于 Windows 安装程序，请执行[应用驱动程序包](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage)步骤。

- 安装软件更新。

- 在部署 OS 之前安装软件。

- 为了实现用户设备相关性，关联用户与目标计算机。

- 通过[安装包](../understand/task-sequence-steps.md#BKMK_InstallPackage)步骤安装动态包。

- 通过[安装应用程序](../understand/task-sequence-steps.md#BKMK_InstallApplication)步骤安装动态应用程序。

> [!NOTE]
> 如果部署 OS 的任务序列包括“安装包”步骤，并且你在管理中心站点 (CAS) 创建了独立介质，则可能会出错。 当任务序列运行时，CAS 没有必要的客户端配置策略来启用软件分发代理。 在 CreateTsMedia.log 文件中可能会出现以下错误：
>
> `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`
>
> 对于包括“安装包”步骤的独立介质，请在已启用软件分发代理的主站点上创建独立介质。
>
> 或者，编辑任务序列，以在[安装 Windows 和 ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) 步骤后添加[运行命令行](../understand/task-sequence-steps.md#BKMK_RunCommandLine)步骤。 此“运行命令行”步骤在第一步“安装包”运行之前，运行以下 WMI 命令来启用软件分发代理：
>
> ```command
> WMIC /namespace:\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE
> ```

## <a name="configure-deployment-settings"></a>配置部署设置

使用独立介质来启动 OS 部署过程时，配置部署，让 OS 对介质可用。 在部署的“部署设置”页中，对于“可用于以下项”设置，请选择以下选项之一：

- Configuration Manager 客户端、媒体和 PXE

- 仅媒体和 PXE

- 仅媒体和 PXE（隐藏）

## <a name="create-the-standalone-media"></a>创建独立介质

可以指定独立介质是 U 盘，还是 CD/DVD 盘。 将启动此介质的计算机必须支持你选择作为可启动驱动器的选项。 有关详细信息，请参阅[创建独立介质](create-stand-alone-media.md)。

## <a name="install-the-os-from-standalone-media"></a>从独立介质安装 OS

若要安装 OS，请将独立介质插入到计算机，然后启动计算机。

## <a name="next-steps"></a>后续步骤

[有关操作系统部署的用户体验](../understand/user-experience.md#task-sequence-wizard)
