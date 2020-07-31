---
title: 监视 Microsoft Intune 中的 Microsoft Defender 高级威胁防护 (ATP) 集成 - Azure | Microsoft Docs
description: 通过 Intune 监视 Microsoft Defender 高级威胁防护 (Microsoft Defender ATP)，包括设备合规性和载入状态。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/23/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: cedb255a575d4b6ea04dd684b5592748e63397c8
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "87264509"
---
# <a name="monitor-device-status-when-you-integrate-microsoft-defender-atp-with-intune"></a>将 Microsoft Defender ATP 与 Intune 集成时监视设备状态

集成 Microsoft Intune 和 Microsoft Defender 高级威胁防护 (ATP) 时，可以在 Microsoft Endpoint Manager 管理中心查看有关设备合规性和载入的信息。

## <a name="monitor-device-compliance"></a>监视设备符合性

监视具有 Microsoft Defender ATP 合规性策略的设备状态。

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 选择“设备” > “监视器” > “策略符合性”。

3. 在列表中找到 Microsoft Defender ATP 策略，并查看符合策略和不符合策略的设备。

还可以对同一位置的不符合设备使用“操作”报表：

- 选择“设备” > “监视” > “不符合设备”。

有关报表的详细信息，请参阅 [Intune 报表](../fundamentals/reports.md)。

## <a name="view-onboarding-status"></a>查看载入状态

若要查看 Intune 托管设备的载入状态，请转到“终结点安全性” > “Microsoft Defender ATP”。  在此页中，还可以创建设备配置文件，以便将更多设备载入 Microsoft Defender ATP。

## <a name="next-steps"></a>后续步骤

[使用 Intune 中的条件访问强制执行 Microsoft Defender ATP 的合规性](../protect/advanced-threat-protection.md)
