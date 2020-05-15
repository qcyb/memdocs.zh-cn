---
title: 桌面分析中的更新
titleSuffix: Configuration Manager
description: 了解桌面分析中的安全和功能更新。
ms.date: 04/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 14ae894c-26fb-4fe3-b51d-e80700122df4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 1c79db413f8e37424b84d98d51fb584d168e3819
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268923"
---
# <a name="updates-in-desktop-analytics"></a>桌面分析中的更新

在桌面分析门户中，查看安全和功能更新的状态。 在桌面分析主菜单的监视器组中选择这些节点。 这些节点可让你深入了解环境中这些更新的状态。


## <a name="security-updates"></a>安全更新

若要查看安全更新的当前状态，请在桌面分析的“监视器”部分中选择“安全更新”   ：

![桌面分析的安全更新节点](media/security-updates.png)

此视图汇总了运行 Windows 10 的设备的安全更新  。 条形图中的设备按以下标签分类：

#### <a name="latest"></a>最新

设备运行的是该版本和频道的最新安全更新。

#### <a name="latest-1"></a>最新 1

设备运行的安全更新比该频道上的最新可用更新早一个版本。

#### <a name="older"></a>更早

设备运行的安全更新早于最新 1。

#### <a name="not-measured"></a>未测量

桌面分析尚未评估设备。 此状态包括运行 Windows 7、Windows 8.1 的设备或注册 Windows 预览体验计划的 Windows 10 设备。  

要查看安全更新的采用趋势，请针对特定版本的 Windows 选择“查看详细信息”  。 堆积面积图按一段时间内安装的安全更新对设备进行分类。

要查看安全更新的部署状态，请选择“全部查看”  。 此视图按下列类别列出设备：

- 未启动
- 正在进行
- 完成
- 需要注意 - 设备（按设备名称排序）
- 需要注意 - 问题（按问题类型排序）

要显示具有指出服务仍在处理的新信息的设备，请选择“查看最新数据”  。 桌面分析将在下次完全数据刷新后显示此信息。

  > [!IMPORTANT]
  > 桌面分析选项“查看最新数据”  已弃用。 此操作将在桌面分析服务的未来版本中删除。 有关详细信息，请参阅[已弃用的功能](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)。<!--7080949-->  

## <a name="feature-updates"></a>功能更新

若要查看功能更新的当前状态，请在桌面分析的“监视器”部分中选择“功能更新”   ：

![桌面分析的功能更新节点](media/feature-updates.png)

此视图汇总了运行 Windows 10 的设备的功能更新  。

有关服务期的详细信息，请参阅 [Windows 生命周期简报](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)  

条形图中的设备按以下标签分类：

#### <a name="in-service"></a>服务中

设备运行的是该版本和频道的最新功能更新。  

#### <a name="near-end-of-service"></a>即将结束服务

设备运行的是将在 90 内后结束服务的功能更新。

#### <a name="end-of-service"></a>服务结束

设备运行的是已过服务结束日期的功能更新。 这些日期特定于 Windows 的企业版和教育版。 它们不适用于家庭版、专业版、专业教育版或专业工作站版。 有关详细信息，请参阅 [Windows 生命周期简报](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)。

#### <a name="not-measured"></a>未测量

桌面分析尚未评估设备。 此状态包括运行 Windows 7、Windows 8.1 的设备或注册 Windows 预览体验计划的 Windows 10 设备。

选择该磁贴可查看功能更新的采用趋势。 堆积面积图按一段时间内安装的功能更新对设备进行分类。

## <a name="next-steps"></a>后续步骤

- [了解桌面分析资产](about-assets.md)：设备、驱动程序和应用程序  

- [了解部署计划](about-deployment-plans.md)  
