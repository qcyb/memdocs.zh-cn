---
title: 部署企业版操作系统的方案
titleSuffix: Configuration Manager
description: 了解多种使用 Configuration Manager 部署企业操作系统的方案。
ms.date: 07/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: f74fdb86-c7c2-447f-91f6-b42df6370d7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8304ba7384eba2fc7bfa41d4caf5a256380931c5
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87546631"
---
# <a name="scenarios-to-deploy-enterprise-operating-systems-with-configuration-manager"></a>使用 Configuration Manager 部署企业操作系统的方案

适用范围：  Configuration Manager (Current Branch)

Configuration Manager 中提供了部署以下 OS 部署方案：  

#### <a name="upgrade-windows-to-the-latest-version"></a>将 Windows 升级到最新版本
此方案将在当前正在运行 Windows 7、Windows 8.1 或 Windows 10 的计算机上升级 OS。 此升级过程将保留计算机上的应用程序、设置和用户数据。 没有 Windows ADK 等外部依赖关系。 此过程比传统 OS 部署更快、更具弹性。  

有关详细信息，请参阅[将 Windows 升级到最新版本](upgrade-windows-to-the-latest-version.md)。

#### <a name="windows-autopilot-for-existing-devices"></a>面向现有设备的 Windows Autopilot
<!--3607717, fka 1358333-->
从版本 1810 开始，面向现有设备的 Windows Autopilot 可通过 Windows 10 版本 1809 或更高版本提供。 此功能可重置映像并使用单个 Configuration Manager 任务序列为 Windows Autopilot 用户驱动模式预配 Windows 7 设备。

有关详细信息，请参阅[面向现有设备的 Windows Autopilot](../../../autopilot/existing-devices.md)。

#### <a name="refresh-an-existing-computer-with-a-new-version-of-windows"></a>使用新版本的 Windows 刷新现有的计算机
此方案将对现有计算机进行分区和格式化（擦除），并在该计算机上安装新的 OS。 可以在安装 OS 后迁移设置和用户数据。  

有关详细信息，请参阅[使用新版本的 Windows 刷新现有的计算机](refresh-an-existing-computer-with-a-new-version-of-windows.md)。


#### <a name="install-a-new-version-of-windows-on-a-new-computer-bare-metal"></a>在新计算机（裸机）上安装新版本的 Windows
此方案将在新计算机上安装 OS。 这是 OS 的全新安装，不包括任何设置或用户数据迁移。  

有关详细信息，请参阅[在新计算机（裸机）上安装新版本的 Windows](install-new-windows-version-new-computer-bare-metal.md)。


#### <a name="replace-an-existing-computer-and-transfer-settings"></a>替换现有计算机和传输设置
此方案将在新计算机上安装 OS。 （可选）你可以将设置和用户数据从旧计算机迁移到新计算机。  

有关详细信息，请参阅[替换现有计算机和传输设置](replace-an-existing-computer-and-transfer-settings.md)。


