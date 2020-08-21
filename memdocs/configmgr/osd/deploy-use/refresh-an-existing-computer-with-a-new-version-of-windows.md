---
title: 刷新现有计算机的 OS
titleSuffix: Configuration Manager
description: 可以使用 Configuration Manager 中的几种办法将现有计算机进行分区和格式化，并在计算机上安装新操作系统。
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: b189a346-8c0d-4870-a876-0719fbb0ab04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5972f930e0f8026f0ca1004d797bf34605af201e
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697834"
---
# <a name="refresh-an-existing-computer-with-a-new-version-of-windows"></a>使用新版本的 Windows 刷新现有的计算机

适用范围：  Configuration Manager (Current Branch)

使用 Configuration Manager 对现有计算机进行分区和格式化，然后安装新的 OS。 此过程有时称为“重置映像”  或“擦除和加载”  。 对于此方案，可以在许多不同的部署方法中进行选择，如 PXE、可启动媒体或软件中心。 也可以使用状态迁移点来存储设置，然后将它们还原到新的 OS。

若要选择合适的 OS 部署方案，请参阅[企业操作系统部署方案](scenarios-to-deploy-enterprise-operating-systems.md)。  

## <a name="plan"></a><a name="BKMK_Plan"></a> 计划  

### <a name="plan-for-and-implement-infrastructure-requirements"></a>规划和实现基础结构要求

必须满足几个基础结构要求，然后才能部署 OS。 其中一些要求包括 Windows ADK、用户状态迁移工具 (USMT) 和 Windows 部署服务 (WDS)。 有关详细信息，请参阅 [OS 部署的基础架构要求](../plan-design/infrastructure-requirements-for-operating-system-deployment.md)。  

### <a name="install-a-state-migration-point"></a>安装状态迁移点

若要捕获现有计算机中的设置，并将设置还原到新的 OS，不妨使用状态迁移点。 有关详细信息，请参阅[状态迁移点](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints)。  

## <a name="configure"></a><a name="BKMK_Configure"></a> 配置  

### <a name="prepare-a-boot-image"></a>准备启动映像

启动映像在 Windows PE 环境中启动计算机。 Windows PE 是包含有限组件和服务的最小 OS。 在 Windows PE 中，Configuration Manager 可以在计算机上安装完整的 Windows OS。

有关详细信息，请参阅下列文章：

- [管理启动映像](../get-started/manage-boot-images.md)

- [自定义启动映像](../get-started/customize-boot-images.md)

- [分发内容](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)

### <a name="prepare-an-os-image"></a>准备 OS 映像

OS 映像包含在目标计算机上安装 OS 所必需的文件。

有关详细信息，请参阅下列文章：

- [管理 OS 映像](../get-started/manage-operating-system-images.md)

- [分发内容](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)

### <a name="create-a-task-sequence-to-deploy-an-os"></a>创建用于部署 OS 的任务序列

使用任务序列来自动安装 OS。 可能会有有关任务序列的其他注意事项，具体取决于你所选择的部署方法。

有关详细信息，请参阅下列文章：

- [创建用于安装 OS 的任务序列](create-a-task-sequence-to-install-an-operating-system.md)

- [管理用户状态](../get-started/manage-user-state.md)

## <a name="deploy"></a><a name="BKMK_Deploy"></a> 部署

- 使用下列部署方法之一部署操作系统：  

  - [使用 PXE 通过网络部署 Windows](use-pxe-to-deploy-windows-over-the-network.md)  

  - [使用多播通过网络部署 Windows](use-multicast-to-deploy-windows-over-the-network.md)  

  - [为工厂中的 OEM 或本地 depot 创建映像](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

  - [使用独立媒体部署 Windows，而不使用网络](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

  - [使用可启动媒体通过网络部署 Windows](use-bootable-media-to-deploy-windows-over-the-network.md)  

  - [使用软件中心通过网络部署 Windows](use-software-center-to-deploy-windows-over-the-network.md)  

## <a name="monitor"></a>监视  

有关详细信息，请参阅[监视操作系统部署](monitor-operating-system-deployments.md)。  

> [!Note]
> 如果你为 UEFI 设备重置映像，Windows 启动管理器在启动加载程序中新建条目。 这种行为在你反复为设备重置映像（如在测试环境或学生实验室中）时最为明显。 通常不会影响设备的性能或使用。 如果列表太大，某些特定的硬件设备可能会出现功能问题。 例如，未启动到外部 USB 驱动器，或者无法从列表中选择当前启动条目。 使用 Windows bcdedit  命令清除未用的启动条目。 有关详细信息，请参阅 [BCDEdit /deletevalue](/windows-hardware/drivers/devtest/bcdedit--deletevalue)。<!-- 2841926 -->