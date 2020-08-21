---
title: 使用可启动媒体通过网络部署 Windows
titleSuffix: Configuration Manager
description: 当目标计算机启动时，使用 Configuration Manager 中的可启动介质部署来部署 OS。
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 999b5409-7e72-48d2-8554-4d44427ce383
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: db28c89e88ba08f92618c6d5fde1d1516b74afe4
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124750"
---
# <a name="use-bootable-media-to-deploy-windows-over-the-network-with-configuration-manager"></a>使用可启动媒体与 Configuration Manager 一起通过网络部署 Windows

适用范围：  Configuration Manager (Current Branch)

可启动介质只包含启动映像和指向任务序列的指针。 它从网络上下载 OS 映像和其他引用的内容。 由于可启动介质没有包含太多内容，因此你可以更新任务序列和大多数内容，而不必替换介质。

在下面的方案中，使用启动介质通过网络部署操作系统：

- [使用新版的 Windows 刷新现有的计算机](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [在新计算机（裸机）上安装新版的 Windows](install-new-windows-version-new-computer-bare-metal.md)

- [替换现有计算机和传输设置](replace-an-existing-computer-and-transfer-settings.md)

完成其中一个 OS 部署方案中的步骤，然后根据以下部分来使用可启动介质部署 OS。

## <a name="configure-deployment-settings"></a>配置部署设置

使用可启动介质来启动 OS 部署过程时，配置任务序列部署，让 OS 对介质可用。 在部署的“部署设置”页上，设置此选项。 对于“可用于以下项目”  设置，请选择以下选项之一：

- Configuration Manager 客户端、媒体和 PXE

- 仅媒体和 PXE

- 仅媒体和 PXE（隐藏）

有关详细信息，请参阅 [Deploy a task sequence](deploy-a-task-sequence.md)。

## <a name="create-the-bootable-media"></a>创建可启动媒体

创建可启动介质时，指定它是 U 盘，还是 CD/DVD 盘。 启动媒体的计算机必须支持选为可启动驱动器的选项。 有关详细信息，请参阅[创建可启动媒体](create-bootable-media.md)。

## <a name="install-the-os-from-bootable-media"></a><a name="BKMK_Deploy"></a> 从可启动介质安装 OS

若要安装 OS，请插入可启动介质，然后启动计算机。

## <a name="support-for-cloud-based-content"></a>支持基于云的内容

<!--6209223-->

自版本 2006 起，可启动介质可以下载基于云的内容。 例如，你向远程办公用户发送一个 USB 密钥来重置其设备映像。 或者是一个安装了本地 PXE 服务器，但你希望设备尽量优先使用云服务的办公室。 启动媒体和 PXE 部署现在可以从基于云的源获取大型 OS 部署内容，而不必再费力地通过 WAN 下载。 例如，允许共享内容的云管理网关 (CMG)。

> [!NOTE]
> 设备仍需要与管理点建立 Intranet 连接。

当任务序列运行时，它从基于云的源下载内容。 在客户端上查看“smsts.log”。

### <a name="prerequisites"></a>先决条件

- 在“云服务”组中启用以下客户端设置：“允许访问云分发点”。 请确保将客户端设置部署到目标客户端。 有关详细信息，请参阅[关于客户端设置 - 云服务](../../core/clients/deploy/about-client-settings.md#cloud-services)。

- 对于客户端所在的边界组：

  - 关联已启用内容的 CMG 或云分发点站点系统。 有关详细信息，请参阅[配置边界组](../../core/servers/deploy/configure/boundary-group-procedures.md#bkmk_config)。

  - 启用以下选项：“首选基于云的源而非本地源”。 有关详细信息，请参阅[对等下载适用的边界组选项](../../core/servers/deploy/configure/boundary-groups.md#bkmk_bgoptions)。

- 将任务序列引用的内容分发到启用了内容的 CMG 或云分发点。

## <a name="next-steps"></a>后续步骤

[有关操作系统部署的用户体验](../understand/user-experience.md#task-sequence-wizard)
