---
title: 在新计算机上安装 Windows
titleSuffix: Configuration Manager
description: 通过 PXE、OEM 或独立介质在新计算机（裸机）上使用 Configuration Manager 安装操作系统。
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: f5ad22d5-7df1-49c6-8a0f-db1c3f0cda19
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7eb880b6cb6f45de06b602bc9caa8ca7b98022d5
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125076"
---
# <a name="install-a-new-version-of-windows-on-a-new-computer-bare-metal-with-configuration-manager"></a>使用 Configuration Manager 在新计算机（裸机）上安装新版本的 Windows

适用范围：  Configuration Manager (Current Branch)

本主题提供了在 Configuration Manager 中在新计算机上安装操作系统的常规步骤。 对于此方案，可以从许多不同的部署方法中选择，如 PXE、OEM、或独立媒体。 如果不确定这是否是正确的操作系统部署方案，请参阅[部署企业版操作系统的方案](scenarios-to-deploy-enterprise-operating-systems.md)。  

采用以下部分内容，使用新版本的 Windows 来刷新现有计算机。  

##  <a name="plan"></a><a name="BKMK_Plan"></a> 计划  

-   **规划和实现基础结构要求**  

     在你可以部署操作系统前，有几个必须实施到位的基础结构要求，例如 Windows ADK、Windows 部署服务 (WDS) 以及支持的硬盘配置等。有关详细信息，请参阅[操作系统部署的基础架构要求](../plan-design/infrastructure-requirements-for-operating-system-deployment.md)。

##  <a name="configure"></a><a name="BKMK_Configure"></a> 配置  

1.  **准备启动映像**  

     启动映像将启动 Windows PE 环境（具有有限组件和服务的最小操作系统）中的计算机，然后在该计算机上安装完整的 Windows 操作系统。   在部署操作系统时，必须选择要使用的启动映像并将其分发到分发点。 使用以下方法来准备启动映像：  

    -   若要了解有关启动映像的详细信息，请参阅[管理启动映像](../get-started/manage-boot-images.md)。  

    -   有关如何自定义启动映像的详细信息，请参阅[自定义启动映像](../get-started/customize-boot-images.md)。  

    -   将启动映像分发到分发点 有关详细信息，请参阅 [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)。  

2.  **准备操作系统映像**  

     操作系统映像包含在目标计算机上安装操作系统所必需的文件。 使用以下方法来准备操作系统映像：  

    -   若要了解有关如何创建操作系统映像的详细信息，请参阅[管理操作系统映像](../get-started/manage-operating-system-images.md)。

    -   将操作系统映像分发到分发点。 有关详细信息，请参阅[分发内容](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)。  

    > [!NOTE]
    > 也可以通过 OS 升级包从安装源文件执行 Windows 的新安装，但改为使用 OS 映像，如 install.wim  。
    >
    > 仍支持通过 OS 升级包来部署 Windows 的新安装，但这取决于驱动程序是否与此方法兼容。 从 OS 升级包安装 Windows 时，仍在 Windows PE 中安装驱动程序，而不仅仅是在 Windows PE 中注入。 某些驱动程序在 Windows PE 中时并不兼容安装。 在 Windows PE 中安装时，如果驱动程序与之不兼容，则改为使用 OS 映像。  

3.  **创建任务序列以通过网络部署操作系统**  

     使用任务序列以通过网络自动安装操作系统 使用[创建用于安装操作系统的任务序列](create-a-task-sequence-to-install-an-operating-system.md)中的步骤来创建部署操作系统的任务序列。 可能会有有关任务序列的其他注意事项，具体取决于你所选择的部署方法。  

##  <a name="deploy"></a><a name="BKMK_Deploy"></a> 部署  

-   使用下列部署方法之一部署操作系统：  

    -   [使用 PXE 通过网络部署 Windows](use-pxe-to-deploy-windows-over-the-network.md)  

    -   [使用多播通过网络部署 Windows](use-multicast-to-deploy-windows-over-the-network.md)  

    -   [为工厂中的 OEM 或本地 depot 创建映像](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

    -   [使用独立媒体部署 Windows，而不使用网络](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

    -   [使用可启动媒体通过网络部署 Windows](use-bootable-media-to-deploy-windows-over-the-network.md)  

## <a name="monitor"></a>监视  

-   **监视任务序列部署**  

     若要监视用于安装操作系统的任务序列部署，请参阅[监视操作系统部署](monitor-operating-system-deployments.md)。  
