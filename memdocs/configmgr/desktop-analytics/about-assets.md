---
title: 桌面分析中的资产
titleSuffix: Configuration Manager
description: 了解桌面分析中的设备、驱动程序和应用。
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: d07198cf-49bb-4712-8c63-063b4302cc11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: d5900fd4cb4fdebea23e626ffbe17c5289712b31
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268906"
---
# <a name="assets-in-desktop-analytics"></a>桌面分析中的资产

设备将数据报告到桌面分析后，会提供以下资产的清单：

- 设备
- 已安装的应用  

在服务门户中，在“桌面分析”菜单中选择“资产”。

## <a name="devices"></a>设备

“设备”选项卡显示你的组织中注册到桌面分析的所有设备的关键信息。 可以对任何列进行排序或筛选特定值。

> [!NOTE]  
> 如果仪表板未报告你希望为环境显示的设备数，请参阅[桌面分析故障排除](troubleshooting.md)。  

在部署计划中，有更多关于设备的详细信息。 有关详细信息，请参阅[计划资产](about-deployment-plans.md#plan-assets)

## <a name="apps"></a>应用

“应用”选项卡显示该服务在 Windows 设备上检测到的所有已安装的应用。

“值得注意的”应用安装在超过 2% 的已注册设备上。

“应用版本详细信息”设置默认处于禁用状态，所以此选项卡合并了具有相同名称和发布者的应用的所有版本。<!-- 5542186 --> 此默认行为有助于减少所显示的应用总数，进而有助于减少对应用进行注释所需的工作量。 “值得注意的应用”磁贴中的应用计数也反映了此设置。 例如，它没有列出数百个 Microsoft Edge 实例，而是列出所有版本的一个实例。 可以对所有版本只做一次决策。 如需对特定应用版本做出决策，请启用此设置。 还可以在使用部署计划时配置此设置。 有关详细信息，请参阅[计划资产](about-deployment-plans.md#plan-assets)。

从列表中选择应用，然后选择“编辑”。 此操作显示应用的详细信息。 选择“重要性”下拉菜单，并设置一个值。 你还可以分配“所有者”。 如果进行了任何更改，请选择“保存”。

通过设置下列类别之一来配置应用的“重要性”：

- 严重
- 重要
- 忽略
- 未评审
- 不重要<!-- 3587232 -->

当“应用版本详细信息”设置处于禁用状态时，“应用详细信息”窗格显示它合并的应用版本和语言的数量。 你保存的对应用详细信息的任何更改会应用于所有版本。 例如，设置“重要性”或“所有者”。 有些值会显示“多个”，这表示在所有版本中没有一个一致的值。

### <a name="automatic-upgrade-decision-of-system-and-store-apps"></a><a name="bkmk_plan-autoapp" /> 系统和应用商店应用的自动升级决策

<!-- 3587232 -->
标识“重要性”和“升级决策” 对于桌面分析工作流中的所有值得注意的应用都非常重要。 为了帮助减少批注这些应用的工作量，某些类型的应用会被自动标记为“不重要”。 这些应用的部署计划升级决策也会被标记为“就绪”。 以下应用是兼容的，并且应在升级 Windows 后继续工作：

- Microsoft 发布的系统应用和组件

- 从 Microsoft 应用商店管理和更新的应用

> [!TIP]
> 管理全局级别或按部署计划的任何应用的输入。
>
> 1. 在桌面分析门户的“管理”菜单中，选择“资产”。 然后选择“应用”。
>
> 2. 使用“类型”和“类别”列来管理以下应用类别：
>
>    - 对于应用商店应用，将“类型”筛选为“新式” 
>    - 对于系统应用，将“类别”筛选为“后台进程”或“Windows 组件”  

在部署计划中，还可以设置“升级决策”。 有关详细信息，请参阅[计划资产](about-deployment-plans.md#plan-assets)。

### <a name="usage"></a>用法

<!-- 5533890 -->

- 安装总次数：此值是在所有已注册桌面分析的设备上安装选定应用的次数。

- 安装百分比：此值是选定应用相对于已注册桌面分析的设备总数的安装百分比。

- 过去 30 天内启动了此应用的设备数：此值是用户启动了选定应用的设备数。 它只包括过去 30 天内报告使用情况的设备数。 此计数包括在任何 Windows 10 版本上运行桌面分析的所有已注册设备数。 不同的部署计划此计数可能会有所不同。

## <a name="next-steps"></a>后续步骤

- [了解桌面分析部署计划](about-deployment-plans.md)  

- [了解安全和功能更新](about-updates.md)  

- [桌面分析中的兼容性评估](compat-assessment.md)  
