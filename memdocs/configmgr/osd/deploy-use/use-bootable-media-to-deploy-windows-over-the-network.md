---
title: 使用可启动媒体通过网络部署 Windows
titleSuffix: Configuration Manager
description: 使用 Configuration Manager 中的可启动媒体在启动目标计算机时部署操作系统。
ms.date: 06/16/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 999b5409-7e72-48d2-8554-4d44427ce383
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 22a3219cdf0bb09061e57f34e52ca7a061f55a2f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709235"
---
# <a name="use-bootable-media-to-deploy-windows-over-the-network-with-configuration-manager"></a>使用可启动媒体与 Configuration Manager 一起通过网络部署 Windows

适用范围：  Configuration Manager (Current Branch)

可以在使用可启动媒体部署启动目标计算机时部署操作系统。 媒体包含指向任务序列的指针、操作系统映像和来自网络的其他所需内容。 当目标计算机启动时，计算机会检索到指针所引用的项。 使用没有内容的可启动媒体可以更新目标，无需在媒体中进行替换。

通过在以下操作系统部署方案中使用多播，可以通过网络部署操作系统：

-   [使用新版的 Windows 刷新现有的计算机](refresh-an-existing-computer-with-a-new-version-of-windows.md)

-   [在新计算机（裸机）上安装新版的 Windows](install-new-windows-version-new-computer-bare-metal.md)  

-   [替换现有计算机和传输设置](replace-an-existing-computer-and-transfer-settings.md)  

完成其中一个操作系统部署方案中的步骤，然后运行以下部分来使用可启动媒体部署操作系统。  

## <a name="configure-deployment-settings"></a>配置部署设置  
当你使用可启动媒体来启动操作系统部署过程时，配置该部署才能使操作系统对媒体可用。 可以在“部署软件向导”的“部署设置”  页或部署属性的“部署设置”  选项卡上设置这一选项。 对于“可用于以下项目”  设置，请配置下述内容之一：

-   Configuration Manager 客户端、媒体和 PXE

-   仅媒体和 PXE

-   仅媒体和 PXE（隐藏）

## <a name="create-the-bootable-media"></a>创建可启动媒体
你可以指定可启动媒体是 U 盘还是 CD/DVD 设备。 启动媒体的计算机必须支持选为可启动驱动器的选项。 有关详细信息，请参阅[创建可启动媒体](create-bootable-media.md)。  

##  <a name="install-the-operating-system-from--bootable-media"></a><a name="BKMK_Deploy"></a> 从可启动媒体安装操作系统  
在计算机的可启动驱动器中插入可启动媒体，然后再启动它以安装操作系统。
