---
title: 桌面分析中的更新
titleSuffix: Configuration Manager
description: 了解桌面分析中的安全和功能更新。
ms.date: 08/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 14ae894c-26fb-4fe3-b51d-e80700122df4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ec510414f11aa312e6c1a7d1d5bfa8126f473fe3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706575"
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

如果 Windows 10 设备未使用 Microsoft 帐户进行身份验证，则 Windows 不会报告此数据  。 此身份验证通常作为 Windows 安装程序全新体验 (OOBE) 的一部分完成。<!-- 5148153 -->


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

如果 Windows 10 设备未使用 Microsoft 帐户进行身份验证，则 Windows 不会报告此数据  。 此身份验证通常作为 Windows 安装程序全新体验 (OOBE) 的一部分完成。<!-- 5148153 -->


## <a name="next-steps"></a>后续步骤

- [了解桌面分析资产](about-assets.md)：设备、驱动程序和应用程序  

- [了解部署计划](about-deployment-plans.md)  
