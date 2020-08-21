---
title: 运行状况监视
titleSuffix: Configuration Manager
description: 了解运行状况监视在桌面分析中的工作原理。
ms.date: 01/16/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 343dbe2a-597c-4719-b7ac-45b1f39b49ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: b4663ca5640bcfea4338912ff471a3253b744d5f
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125825"
---
# <a name="health-status-monitoring-in-desktop-analytics"></a>桌面分析中的运行状况监视

当[将更新部署到生产](deploy-prod.md)时，使用桌面分析来帮助监视设备的运行状况。 本文详细说明了运行状况监视的工作原理。

有关如何使用此功能的详细信息，请参阅[监视已更新设备的运行状况](deploy-prod.md#bkmk_monitor)。

![桌面分析的监视运行状况页的屏幕截图](media/monitor-health.png)

> [!NOTE]  
> 桌面分析仅从提供可用作分母的使用情况数据的设备收集运行状况数据。 也就是说，不包括运行 Windows 7 和 Windows 10 且没有被设置为在“可选(受限)”级别共享诊断数据的设备。 如果超过 10% 的运行 Windows 10 的设备被设置为在非“可选(受限)”级别上共享诊断数据，则“监视运行状况”页在横幅区域中显示警告。  

若要查看有关特定应用的详细信息，请在列表中选中它。

## <a name="apps"></a>应用

### <a name="health-status-factors"></a>运行状况因素

![桌面分析中应用的运行状况因素](media/monitor-health-status-factors.png)

桌面分析会监视应用的以下运行状况因素：

- **故障设备百分比**：此特定应用程序在过去两周内发生故障的设备数除以使用该应用程序的设备数。 此视图可让你查看新操作系统版本上的应用稳定性是提高了还是降低了。 桌面分析为以下集计算此百分比：  

  - **更新后**：已更新到部署计划中指定的目标 OS 版本的设备。 为了减少数据不足的资产数量，桌面分析会为所有已更新的设备收集此数据。 此集包括未列入部署计划的那些设备。  

  - **更新前**：操作系统版本早于部署计划指定版本的设备。 此列表不包括运行 Windows 7 的设备。  

  - **商业平均值**：所有商业设备的平均故障率。 此平均值是跨应用的所有版本计算的  。 如果你的版本显示的故障率高于商业平均值，则可能存在更稳定的可用版本。  

- **故障会话百分比**：与前面的内容类似，但会计算过去两周内出现故障的会话的百分比。  

若要确定应用程序的运行状况，桌面分析需要至少 20 台设备中的数据。 否则，它将报告应用“数据不足”  。 该服务根据这些设备的会话故障率来计算运行状况  。 提供的设备故障率仅供参考。 它不用于运行状况计算。

### <a name="usage"></a>用法

<!-- 5533890 -->

- 活动设备数  ：此值是用户在过去两周内启动了选定应用的设备数。 它基于运行目标 Windows 10 版本的选定部署计划中的设备数。

- 会话数  ：此值是用户在目标 Windows 版本中启动选定应用的总次数。

### <a name="additional-tabs"></a>其他选项卡

在应用详细信息页的底部，以下三个选项卡可帮助你进行故障排除：

- **其他版本**：此应用的其他版本的列表。 对于每个版本，它会显示组织内的故障率和商业平均值的相对变化。 如果找到故障率较低的更高应用版本，则更新应用可能会有所帮助。  

    它还显示了版本是否具有高级见解。 有关详细信息，请参阅[兼容性评估](compat-assessment.md)。  

- **常见问题**：按实例计数排列的最常见故障 ID 列表。 故障 ID 标识与故障关联的堆栈跟踪。 在致电应用供应商以寻求支持时，可以使用此 ID。  

- **最近的故障**：应用最近发生故障的设备列表。 可以按故障 ID 和其他条件进行筛选。 在尝试更广泛的部署之前，通过收集日志或在特定设备上尝试修复来使用这些信息进行故障排除。  

如果发现无法解决的严重运行状况回归，请将应用的“升级决策”  改为“不能”  。 此操作阻止将来将更新部署到具有此资产的设备。

## <a name="see-also"></a>另请参阅

- [桌面分析中的兼容性评估](compat-assessment.md)  

- [如何通过桌面分析部署到生产](deploy-prod.md)  
