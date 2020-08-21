---
title: 使用多播通过网络来部署 Windows
titleSuffix: Configuration Manager
description: 在 Configuration Manager 环境中使用多播，以便多台计算机可以同时下载 OS 映像。
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 4cafb7fc-380b-41b1-b83e-045aebfb7131
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9f580467ccb26209ed20666733e30959bbf50128
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124699"
---
# <a name="use-multicast-to-deploy-windows-over-the-network-with-configuration-manager"></a>在 Configuration Manager 中使用多播通过网络部署 Windows

适用范围：  Configuration Manager (Current Branch)

多播是一种网络优化方法，可以在多个客户端可能同时下载相同的 OS 映像时使用。 当你使用多播时，多台计算机同时下载 OS 映像，因为分发点对它进行了多播。 此行为不是每个客户端通过单独的连接从分发点下载映像的副本。

在以下 OS 部署方案中，使用多播通过网络部署操作系统：

- [使用新版的 Windows 刷新现有的计算机](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [在新计算机（裸机）上安装新版的 Windows](install-new-windows-version-new-computer-bare-metal.md)

完成其中一个 OS 部署方案中的步骤。 然后，根据以下部分来支持多播。

## <a name="configure-distribution-points-for-multicast"></a><a name="BKMK_Configure"></a> 为分发点配置多播

若要使用多播，请配置至少一个分发点来支持多播。 有关详细信息，请参阅[安装和配置分发点](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-multicast)。

有关支持多播所需的端口列表，请参阅[端口](../../core/plan-design/hierarchy/ports.md#BKMK_PortsClient-DP2)。

## <a name="prepare-an-os-image-for-multicast"></a>为 OS 映像准备多播

需要将 OS 映像配置为支持多播。 有关详细信息，请参阅[为 OS 映像准备多播部署](../get-started/manage-operating-system-images.md#BKMK_OSImageMulticast)。

## <a name="deploy-the-task-sequence"></a><a name="BKMK_Deploy"></a> 部署任务序列

将 OS 部署到目标集合。 有关详细信息，请参阅 [Deploy a task sequence](deploy-a-task-sequence.md)。

## <a name="next-steps"></a>后续步骤

[有关操作系统部署的用户体验](../understand/user-experience.md)
