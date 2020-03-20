---
title: 在 Microsoft Intune 设备中使用批量设备操作。
titleSuffix: ''
description: 使用批量远程设备操作。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 3/12/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8c50f5495aa593dc8904fe6a9120ecd29de693ee
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79349142"
---
# <a name="use-bulk-device-actions"></a>使用批量设备操作

你可以对以下远程操作使用批量设备操作：
- [Autopilot 重置](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot-reset#reset-devices-with-remote-windows-autopilot-reset)
- [自定义通知](custom-notifications.md#send-a-custom-notification-to-a-single-device)
- [删除](devices-wipe.md#delete-devices-from-the-intune-portal)
- [重命名](device-rename.md)
- [重新启动](device-restart.md)
- [同步](device-sync.md)
- [擦除](devices-wipe.md#wipe)

## <a name="use-a-bulk-device-action"></a>使用批量设备操作

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“设备” > “所有设备” > “批量设备操作”    。
![批量设备操作](./media/bulk-device-actions/bulk-device-actions.png)
3. 在“批量设备操作”页上，选择“OS”和“设备操作”    。 某些设备操作有其他选项或其他填充字段。 选择“下一步”  。
4. 在“设备”页上，选择“1 到 100 个设备”>“下一步”   。
5. 在“查看 + 创建”页上，选择“创建”   。

## <a name="next-steps"></a>后续步骤
[设备管理概述。](device-management.md)
