---
title: Windows Autopilot 更新
ms.reviewer: ''
manager: laurawi
description: Windows Autopilot 更新
keywords: Autopilot、update、Windows 10
ms.prod: w10
ms.mktglfcycl: deploy
ms.sitesec: library
ms.pagetype: deploy
ms.localizationpriority: medium
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: a677dec0d722f0ef17a8c16248a41dea1b0be947
ms.sourcegitcommit: 42882de75c8a984ba35951b1165c424a7e0ba42e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89068117"
---
# <a name="windows-autopilot-update"></a>Windows Autopilot 更新

**适用于**

- Windows 10 版本 1903

Windows Autopilot update 会将最新的 Autopilot 功能和修补程序安装到组织的 Autopilot 设备上。 设备不会移动到最新的 Windows 操作系统版本。 借助 Autopilot update，你可以保留设备的最新操作系统版本，还可以从新的 Autopilot 功能和 bug 修复中获益。

Windows Autopilot 更新过程在严重 [Windows Zero (ZDP) 更新](/windows-hardware/customize/desktop/windows-updates-during-oobe) 检查后发生。 在更新过程中，设备会检查 Windows 更新是否有新的 Autopilot 更新。 如果有可用的 Autopilot 更新，则设备会下载并安装更新，然后自动重新启动。 请参阅以下示例。

 ![Autopilot update 1](images/update1.png)<br>
 ![Autopilot update 2](images/update2.png)<br>
 ![Autopilot update 3](images/update3.png)

下图说明了在全新的 Windows Autopilot update 节点 (OOBE) 时的典型 Windows Autopilot 部署业务流程。

 ![Autopilot 更新流](images/update-flow.png)

## <a name="release-cadence"></a>发布节奏

- 当 Autopilot 更新可用时，它通常会在该月的第四个星期二发布。 如果出现异常，则可以在不同的周发布更新。
- 还将发布知识库 (KB) 文章来记录更新中包含的更改。

有关已发布更新的列表，请参阅 [Autopilot 更新历史记录](windows-autopilot-whats-new.md#windows-autopilot-update-history)。

## <a name="see-also"></a>另请参阅

[OOBE 期间 Windows 更新](/windows-hardware/customize/desktop/windows-updates-during-oobe)<br>
[Windows Autopilot 的新增功能](windows-autopilot-whats-new.md)<br>