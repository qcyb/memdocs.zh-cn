---
title: 使用 Microsoft Intune 锁定设备 - Azure | Microsoft Docs
description: 在 Microsoft Intune 中使用“远程锁定”操作锁定受 PIN 或密码保护的设备。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 3b67f285-229d-4a0f-ae34-0402a20b4518
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 220a2ac92d46c1279d4498c8673e2ceef28c470f
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2020
ms.locfileid: "86462042"
---
# <a name="remotely-lock-devices-with-intune"></a>使用 Intune 远程锁定设备

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

“远程锁定”设备操作将锁定该设备。 设备所有者必须输入其密码才能解锁设备。 可远程锁定已设置 PIN 或密码的设备。 不能远程锁定没有 PIN 或密码的设备。

## <a name="supported-platforms"></a>受支持的平台

以下平台支持远程锁定：

- Android
- Android 企业展台设备
- Android Enterprise 工作配置文件设备
- Android Enterprise 完全托管设备
- Android Enterprise 公司拥有的工作配置文件设备
- iOS
- macOS
- Windows 10 移动版
- Windows Phone 8.1 及更高版本

以下平台不支持远程锁定：
- Windows 10 桌面版

> [!NOTE]
> 对于 macOS 设备，请设置一个 6 位数的恢复 PIN。 设备锁定时，“设备概述”会显示 PIN，直到发送另一个设备操作。 请确保记下该 PIN，因为它仅在远程锁定命令发送后 30 天内可用。 30 天后，Intune 将不再具有该 PIN。 此外，如果再次为同一设备启动此命令，而原始 PIN 尚未成功用于解锁设备，则会在报告中看到失败状态。 应仅发送此命令一次，记下 PIN，在使用它成功进入 macOS 设备之前，不再尝试将此命令发送到同一设备。


## <a name="remote-lock-a-device"></a>远程锁定设备

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
3. 选择“设备” > “所有设备” 。
4. 在设备列表中选择一个设备，然后选择“远程锁定”操作。

## <a name="next-steps"></a>后续步骤

- 若要查看此操作的状态，请选择“Microsoft Intune” > “设备” > “设备操作”  。 
- 有关有助于管理设备的其他操作，请参阅[可用操作](device-management.md)。
