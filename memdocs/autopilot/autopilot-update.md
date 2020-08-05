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
ms.openlocfilehash: 34db88c53cdd7db46c126f15bb60a7fd2941a627
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87756350"
---
# <a name="windows-autopilot-update"></a>Windows Autopilot 更新

**适用于**

-   Windows 10 版本 1903

Windows Autopilot 更新使你能够获取最新的 Autopilot 功能和关键问题修复，无需移动到最新的 Windows 操作系统版本。 借助 Autopilot 更新，组织可以保留当前的操作系统版本，但仍可从新的 Autopilot 功能和 bug 修复中获益。
 
在 Autopilot 部署过程中，Windows Autopilot 更新已作为新节点添加到了严重[Windows Zero (ZDP) 更新](https://docs.microsoft.com/windows-hardware/customize/desktop/windows-updates-during-oobe)检查后。 在更新过程中，Windows Autopilot 设备将进入 Windows 更新以检查是否有新的 Autopilot 更新。  如果有可用的 Autopilot 更新，则设备将下载并安装更新，然后自动重新启动。 请参阅以下示例。

   ![Autopilot update 1](images/update1.png)<br>
   ![Autopilot update 2](images/update2.png)<br>
   ![Autopilot update 3](images/update3.png)

下图说明了在全新的 Windows Autopilot update 节点 (OOBE) 时的典型 Windows Autopilot 部署业务流程。

   ![Autopilot 更新流](images/update-flow.png)

## <a name="release-cadence"></a>发布节奏

- 当 Autopilot 更新可用时，它通常会在当月的第4个星期二发布。 如果出现异常，则可以在不同的周发布更新。
- 还将发布知识库 (KB) 文章来记录更新中包含的更改。

有关已发布更新的列表，请参阅[Autopilot 更新历史记录](windows-autopilot-whats-new.md#windows-autopilot-update-history)。

## <a name="see-also"></a>请参阅

[OOBE 期间 Windows 更新](https://docs.microsoft.com/windows-hardware/customize/desktop/windows-updates-during-oobe)<br>
[Windows Autopilot 的新增功能](windows-autopilot-whats-new.md)<br>