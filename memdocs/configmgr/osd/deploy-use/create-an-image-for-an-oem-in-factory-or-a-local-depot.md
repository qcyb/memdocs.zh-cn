---
title: 为工厂中的 OEM 或本地仓库创建映像
titleSuffix: Configuration Manager
description: 在将 OS 部署到未完全预配的计算机时，使用预留介质部署可减少网络流量。
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: a7d3df90-062d-4d57-9e9d-e137d3e7cd7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 15145cccf73e517d0e49444fbdaf834de342865e
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125434"
---
# <a name="create-an-image-for-an-oem-in-factory-or-a-local-depot-with-configuration-manager"></a>使用 Configuration Manager 为工厂中的 OEM 或本地 depot 创建映像

适用范围：  Configuration Manager (Current Branch)

通过 Configuration Manager 中的预留介质部署，可以将 OS 部署到未完全预配的计算机。 预留介质是 Windows 映像 (WIM) 文件。 制造商 (OEM) 可以将它安装在裸机计算机上，你也可以将它用于与生产环境分开的暂存中心。

这种部署方法可以减少网络流量，因为启动映像和 OS 映像已经在目标计算机上。 可以指定预留介质中也包含应用程序、包和驱动程序包。 在计算机上安装 OS 后，任务序列先检查预留缓存中是否有应用程序、包或驱动程序包。 如果找不到必要的内容，或者有更高的版本可联机获取，则任务序列会从分发点下载内容。

在以下 OS 部署方案中，使用预留介质：

- [在新计算机（裸机）上安装新版的 Windows](install-new-windows-version-new-computer-bare-metal.md)

- [替换现有计算机和传输设置](replace-an-existing-computer-and-transfer-settings.md)

完成其中一个 OS 部署方案中的步骤。 然后，根据以下部分来准备并创建预留介质。

## <a name="configure-deployment-settings"></a>配置部署设置

在部署的“部署设置”页中，对于“可用于以下项”设置，请选择以下选项之一：

- Configuration Manager 客户端、媒体和 PXE

- 仅媒体和 PXE

- 仅媒体和 PXE（隐藏）

## <a name="create-the-prestaged-media"></a>创建预留媒体

创建要发送到的 OEM 或本地 depot 的预留媒体文件。 有关详细信息，请参阅[使用 Configuration Manager 创建预留媒体](create-prestaged-media.md)。

## <a name="send-the-prestaged-media-file"></a>发送预留介质文件

将介质发送到 OEM 或本地仓库，以预留在计算机上。 它们将映像文件应用到计算机上的格式化硬盘。

## <a name="deliver-the-computer"></a>交付计算机

当你将计算机交付给用户，并第一次打开它时：

1. 计算机使用预留的启动映像启动。

1. 它检查预留介质上的哈希，以确保它是有效的。

1. 计算机连接到可用任务序列的管理点，以完成此过程。

## <a name="next-steps"></a>后续步骤

[有关操作系统部署的用户体验](../understand/user-experience.md)
