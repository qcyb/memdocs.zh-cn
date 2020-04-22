---
title: Surface 设备仪表板
titleSuffix: Configuration Manager
description: 使用仪表板查看有关 Surface 设备的信息。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 7397fc17-3ae8-4525-8386-aea8a9cffa06
ms.openlocfilehash: 08baf595199bdda121f897d507de97cb7e93e620
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696345"
---
# <a name="surface-device-dashboard-in-configuration-manager"></a>Configuration Manager 中的 Surface 设备仪表板

适用范围：  Configuration Manager (Current Branch)

从 1802 版开始，可通过 Surface 设备仪表板快速了解在环境中找到的 Surface 设备的相关信息。 <!--1355788-->

## <a name="open-the-surface-device-dashboard"></a>打开 Surface 设备仪表板

若要打开 Surface 设备仪表板，请使用以下步骤： 

1. 打开 Configuration Manager 控制台。 
2. 单击“监视”  节点。 
3. 若要加载仪表板，请单击“Surface 设备”  。

**Surface 设备仪表板**
![Surface 设备仪表板](media/Surface-device-dashboard.PNG)



## <a name="reviewing-information-in-the-surface-device-dashboard"></a>查看 Surface 设备仪表板中的信息

Surface 设备仪表板针对你的环境显示三个图表。 

- **Surface 设备所占百分比**：提供 Surface 设备在你的环境中所占的百分比。

    ![Surface 设备所占百分比图表](media/Percent-Surface-Devices.PNG)
- **Surface 型号**：显示每种 Surface 型号的设备数量。 
  - 将鼠标悬停在某个图表部分上方将显示所选型号的 Surface 设备所占的百分比。 

       ![Surface 型号图表](media/Surface-Models-Hover.PNG)
  - 单击某个图表部分将转到该型号的设备列表。 
      ![Surface 型号设备列表](media/Surface-Model-Device-List.PNG)

- **前五个固件版本**：显示包含环境中前五个固件型号的图表。 
  - 将鼠标悬停在某个图表部分上方将显示所选固件版本的 Surface 设备的数量。 自 Configuration Manager 版本 1806 起，单击某个图表部分即可显示相关设备的列表。 <!--1358654-->
     ![Surface 型号设备列表](media/Surface-Firmware-Hover.PNG)


## <a name="more-information"></a>更多信息

有关 Surface 设备的详细信息，请参阅：
- [Surface]( https://go.microsoft.com/fwlink/?linkid=861998) 网站。

有关在 Configuration Manager 中部署 Surface 固件更新的详细信息，请参阅：
- [如何在 Configuration Manager 中管理 Surface 驱动程序更新]( https://support.microsoft.com/help/4098906)。




