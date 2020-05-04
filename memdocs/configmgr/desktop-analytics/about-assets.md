---
title: 桌面分析中的资产
titleSuffix: Configuration Manager
description: 了解桌面分析中的设备、驱动程序和应用。
ms.date: 01/16/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: d07198cf-49bb-4712-8c63-063b4302cc11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fe1338781cbb16a8485de050a294e34e487a2ecc
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706645"
---
# <a name="assets-in-desktop-analytics"></a>桌面分析中的资产

设备将数据报告到桌面分析后，会提供以下资产的清单：

- 设备
- 已安装的应用  

在服务门户中，在“桌面分析”菜单中选择“资产”  。

## <a name="devices"></a>设备

“设备”  选项卡显示你的组织中注册到桌面分析的所有设备的关键信息。 可以对任何列进行排序或筛选特定值。

> [!NOTE]  
> 如果仪表板未报告你希望为环境显示的设备数，请参阅[桌面分析故障排除](troubleshooting.md)。  

在部署计划中，有更多关于设备的详细信息。 有关详细信息，请参阅[计划资产](about-deployment-plans.md#plan-assets)

## <a name="apps"></a>应用

“应用”  选项卡显示该服务在 Windows 设备上检测到的所有已安装的应用。

“值得注意的”  应用安装在超过 2% 的已注册设备上。

通过设置下列类别之一来配置应用的“重要性”  ：

- 严重
- 重要
- 忽略
- 未评审
- 不重要<!-- 3587232 -->

从列表中选择应用，然后选择“编辑”  。 此操作显示应用的详细信息。 选择“重要性”  下拉菜单，并设置一个值。 你还可以分配“所有者”  。 如果进行了任何更改，请选择“保存”  。

### <a name="automatic-upgrade-decision-of-system-and-store-apps"></a><a name="bkmk_plan-autoapp" /> 系统和应用商店应用的自动升级决策

<!-- 3587232 -->
标识“重要性”和“升级决策”   对于桌面分析工作流中的所有值得注意的应用都非常重要。 为了帮助减少批注这些应用的工作量，某些类型的应用会被自动标记为“不重要”  。 这些应用的部署计划升级决策也会被标记为“就绪”  。 以下应用是兼容的，并且应在升级 Windows 后继续工作：

- Microsoft 发布的系统应用和组件

- 从 Microsoft 应用商店管理和更新的应用

> [!TIP]
> 管理全局级别或按部署计划的任何应用的输入。
>
> 1. 在桌面分析门户的“管理”  菜单中，选择“资产”  。 然后选择“应用”  。
>
> 2. 使用“类型”  和“类别”  列来管理以下应用类别：
>
>    - 对于应用商店应用，将“类型”筛选为“新式”  
>    - 对于系统应用，将“类别”筛选为“后台进程”或“Windows 组件”   

在部署计划中，还可以设置“升级决策”  。 有关详细信息，请参阅[计划资产](about-deployment-plans.md#plan-assets)

### <a name="usage"></a>用法

<!-- 5533890 -->

- 安装总次数  ：此值是在所有已注册桌面分析的设备上安装选定应用的次数。

- 安装百分比  ：此值是选定应用相对于已注册桌面分析的设备总数的安装百分比。

- 过去 30 天内启动了此应用的设备数  ：此值是用户启动了选定应用的设备数。 它只包括过去 30 天内报告使用情况的设备数。 此计数包括在任何 Windows 10 版本上运行桌面分析的所有已注册设备数。 不同的部署计划此计数可能会有所不同。

## <a name="next-steps"></a>后续步骤

- [了解桌面分析部署计划](about-deployment-plans.md)  

- [了解安全和功能更新](about-updates.md)  

- [桌面分析中的兼容性评估](compat-assessment.md)  