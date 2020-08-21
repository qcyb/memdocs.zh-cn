---
title: 使用软件中心通过网络部署 Windows
titleSuffix: Configuration Manager
description: 从软件中心部署 OS，以使用新版 Windows 来更新现有计算机，或将 Windows 升级到最新版本。
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 919e3636-53fe-4119-ad14-2d03702b391b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6bd10240ebc7ec478efe122bf7f8a45d3afe9f10
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124595"
---
# <a name="use-software-center-to-deploy-windows-over-the-network-with-configuration-manager"></a>在 Configuration Manager 中使用软件中心通过网络部署 Windows

适用范围：  Configuration Manager (Current Branch)

可以创建任务序列来安装软件中心内可用的 OS。 用户可以从软件中心为以下 OS 部署方案运行任务序列：

- [使用新版的 Windows 刷新现有的计算机](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [将 Windows 升级到最新版本](upgrade-windows-to-the-latest-version.md)

- [创建非 OS 部署的任务序列](create-a-task-sequence-for-non-operating-system-deployments.md)

完成其中一个 OS 部署方案中的步骤。 然后使用以下部分来准备在 Software Center 中可用的部署。

## <a name="deploy-the-task-sequence"></a><a name="BKMK_Deploy"></a> 部署任务序列

将任务序列部署到目标集合。 有关详细信息，请参阅 [Deploy a task sequence](deploy-a-task-sequence.md)。

在部署的“部署设置”页中，对于“可用于以下项”设置，请选择以下选项之一：

- 仅 Configuration Manager 客户端

- Configuration Manager 客户端、媒体和 PXE

此外，还要配置部署是必需的还是可用的：

- 必需部署：必需部署让任务序列在软件中心内可用。 它会自动在配置的截止时间启动。

- 可用部署：任务序列在软件中心内可用，用户可以按需安装它。

在你创建部署后，目标集合中的客户端会显示软件中心内的任务序列。

## <a name="next-steps"></a>后续步骤

[有关操作系统部署的用户体验](../understand/user-experience.md#software-center)
