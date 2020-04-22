---
title: 关于升级、更新和安装
titleSuffix: Configuration Manager
description: 了解在管理 Configuration Manager 基础结构时，“安装”、“更新”和“升级”三个术语之间的差异。
ms.date: 04/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 17fab17f-304d-4f6a-87c7-30ab4f5521ed
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5af92990a0158172a441b052cdc2210e98fda9d5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706715"
---
# <a name="about-upgrade-update-and-install-for-site-and-hierarchy-infrastructure"></a>关于站点和层次结构基础结构的升级、更新和安装

适用范围：  Configuration Manager (Current Branch)

管理 Configuration Manager 站点和层次结构基础结构时，术语“升级”、“更新”和“安装”用于描述三种不同概念    。

## <a name="upgrade"></a>Upgrade

如果要将 Configuration Manager 2012 站点或层次结构转换为运行 Configuration Manager Current Branch 的站点或层次结构，则使用“升级”或“就地升级”   。

如果要将 System Center 2012 Configuration Manager 升级为 Configuration Manager Current Branch，请继续使用同一服务器托管站点和站点服务器，并保留 Configuration Manager 的现有数据和配置。  这不同于[迁移](../migration/migrate-data-between-hierarchies.md)，迁移是一种在使用安装到新硬件的 Configuration Manager Current Branch 站点的同时，保留托管设备相关配置和数据的方式。

有关详细信息，请参阅[升级到 Configuration Manager](../servers/deploy/install/upgrade-to-configuration-manager.md)。



## <a name="update"></a>更新
“更新”用于安装 Configuration Manager 的控制台中更新，还用于带外更新，带外更新指无法从 Configuration Manager 控制台中传递的更新  。 控制台中更新可修改 Current Branch 站点（或 Technical Preview 站点）的版本，使其可运行更高版本。 例如，如果站点运行版本 1806，你可以安装版本 1810 的更新。 更新还可以安装已知问题的修补程序，无需修改站点版本。      

通常情况下，更新会将安全修补程序、质量改进和新功能添加到现有部署。 如果使用 Technical Preview Branch，则更新可安装更新版本的 Technical Preview。
- 从层次结构的顶层站点开始，选择安装控制台中更新的时间。
- 可安装能从控制台中获取的任何更新。 例如，如果站点运行版本 1802，并且同时提供了 1806 和 1810，你应考虑安装版本 1810，因为每个版本都包括了以前发布的版本中首次提供的功能。
- 顶层站点完成安装新更新后，子主站点将自动启动更新过程。 但是，可设置[服务时段](../servers/manage/service-windows.md)以控制更新的执行时间。
- 辅助站点不会自动安装更新。 相反，请从 Configuration Manager 控制台中手动启动更新。

有关详细信息，请参阅 [Configuration Manager 的更新](../servers/manage/updates.md)和 [Configuration Manager 的 Technical Preview](../get-started/technical-preview.md)。



## <a name="install"></a>安装
如果要从零开始创建新的 Configuration Manager 层次结构，或将额外站点添加到现有层次结构，则使用“安装”  。  

安装新的主站点或中心管理站点时，使用的 setup.exe 及其相关源文件的位置取决于你的安装方案。

有关详细信息，请参阅[安装站点的准备工作](../servers/deploy/install/prepare-to-install-sites.md)。
