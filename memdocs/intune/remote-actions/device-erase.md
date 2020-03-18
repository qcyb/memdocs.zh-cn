---
title: 清除 macOS 设备
titleSuffix: Microsoft Intune
description: 了解如何从 macOS 设备中清除所有数据（包括操作系统）。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ab396092-907a-44b7-a157-aabee62176a9
ms.reviewer: coferro
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 650ba81c9e92ce03b67e90cf188435b7dc0800fb
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79338209"
---
# <a name="erase-all-data-from-a-macos-device"></a>从 macOS 设备中清除所有数据

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

可以清除 macOS 设备中的所有数据，包括操作系统。 该设备也会从 Intune 管理中删除。 最终用户不会看到任何警告。

1. 在 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，选择“设备”   > “所有设备”  > 选择要清除的设备。
2. 单击“更多” > “清除”，然后提供 6 位数的恢复 PIN    。 必须将此 PIN 提供给用户，以便其在设备上重新安装操作系统。 请务必记下此 PIN，因为在清除操作完成后它不会显示。
![屏幕截图](./media/device-erase/providepin.png)
3. 单击“确定”以清除设备  。
