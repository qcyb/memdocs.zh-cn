---
title: 使用软件中心通过网络部署 Windows
titleSuffix: Configuration Manager
description: 可将操作系统部署到软件中心，使用新版 Windows 刷新现有计算机或将 Windows 升级到最新版本。
ms.date: 06/16/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 919e3636-53fe-4119-ad14-2d03702b391b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4b9946f6204c2e95645c932cd4e9aab691f1d95d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709025"
---
# <a name="use-software-center-to-deploy-windows-over-the-network-with-configuration-manager"></a>在 Configuration Manager 中使用软件中心通过网络部署 Windows

适用范围：  Configuration Manager (Current Branch)

你可以使在 Configuration Manager 中安装操作系统的任务序列在软件中心可用。 可以使用以下操作系统部署方案将操作系统部署到软件中心：

-   [使用新版的 Windows 刷新现有的计算机](refresh-an-existing-computer-with-a-new-version-of-windows.md)

-   [将 Windows 升级到最新版本](upgrade-windows-to-the-latest-version.md)

完成其中一个操作系统部署方案中的步骤。 然后使用以下部分来准备在 Software Center 中可用的部署。

## <a name="configure-deployment-settings"></a>配置部署设置  
要使操作系统部署在软件中心中可用，请配置该部署。 可以在部署软件向导的“部署设置”  页或部署属性的“部署设置”  选项卡中配置部署。 对于“可用于以下项目”  设置，请配置“仅 Configuration Manager 客户端”  或“Configuration Manager 客户端、媒体和 PXE”  。 系统部署操作系统后，操作系统显示在目标集合成员的软件中心中。

##  <a name="deploy-the-task-sequence-to-computers"></a><a name="BKMK_Deploy"></a> 将任务序列部署到计算机  
将操作系统部署到目标集合。 有关详细信息，请参阅 [Deploy a task sequence](deploy-a-task-sequence.md)。 在为软件中心部署操作系统时，可以配置部署属性为必需还是可用。

-   **所需部署**：必需部署将使操作系统在软件中心可用，但会按配置的分配计划自动启动。

-   **可用部署**：操作系统将在软件中心内可用，且用户可根据需要进行安装。