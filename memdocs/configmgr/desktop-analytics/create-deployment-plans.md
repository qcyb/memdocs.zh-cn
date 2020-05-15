---
title: 如何创建部署计划
titleSuffix: Configuration Manager
description: 关于在桌面分析中创建部署计划的操作指南。
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 8e0e8496-136b-461f-8239-cc19c6b78c3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: ac9b5ddd85904c90709a9450d6d2a9ffd379ddb9
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268753"
---
# <a name="how-to-create-deployment-plans-in-desktop-analytics"></a>如何在桌面分析中创建部署计划

本文提供在桌面分析中创建部署计划的步骤。 在开始之前，请先[了解部署计划](about-deployment-plans.md)。

## <a name="create-a-plan-for-windows-10"></a>为 Windows 10 创建计划

按照本节中的步骤使用桌面分析来创建部署 Windows 10 的计划。

1. 打开[桌面分析门户](https://aka.ms/desktopanalytics)。 使用至少具有“工作区参与者”  权限的凭据。  

2. 在“管理”组中选择“部署计划”  。  

3. 在“部署计划”  窗格中，选择“创建”  。  

4. 在“创建部署计划”  窗格中，配置下列设置：  

    - **名称**：部署计划的唯一名称  

    - **产品和版本**：选择要部署的 Windows 10 版本。 Microsoft 建议创建使用最新版本的部署计划。  

    - **设备组**：选择同一个层次结构中的一个或多个组。 这些组是从 Configuration Manager 同步的[集合](connect-configmgr.md#bkmk_Collections)。

        如果将多个 Configuration Manager 层次结构连接到同一桌面分析实例，则在全局试点配置中，集合名称将采用层次结构的显示名称作为前缀。 该名称是 Configuration Manager 控制台中桌面分析连接上的“显示名称”属性  。<!-- 4814075 -->

        > [!NOTE]
        > 必须有 Configuration Manager 版本 1910 或更高版本，才能支持多个层次结构。
        >
        > 如果选择对多个层次结构使用集合，该门户也会显示一则警告。 无法使用来自多个层次结构的集合创建部署计划。<!-- 4814075 -->

    - **就绪规则**：这些规则可帮助确定哪些设备符合升级条件。 有关详细信息，请参阅[就绪规则](#readiness-rules)。  

    - **完成日期**：选择将 Windows 完全部署到所有目标设备的截止日期。  

5. 选择“创建”。  新计划在进行处理时显示在部署计划的列表中。 若要加快处理过程，可请求按需进行数据刷新。 有关详细信息，请参阅[桌面分析常见问题](faq.md#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal)。  

6. 通过选择部署计划的名称将其打开。  

7. 在部署计划菜单上的“准备”  组中，选择“确定重要性”  。  

    1. 在“应用”  选项卡上，选择仅显示“未评审”资产  。  

    2. 选择每个应用，然后选择“编辑”  。 可以选择同时编辑多个应用。  

    3. 从“重要性”  列表中选择一个重要性级别。 如果希望桌面分析在试点期间验证应用，请选择“严重”  或“重要”  。 它不会验证标记为“不重要”  的应用。 分配重要性级别时，评估其[兼容性](compat-assessment.md)和其他计划见解。  

        分配重要性级别时，还可以选择升级决策。  

    4. 完成后选择“保存”  。  

8. 在部署计划菜单上的“准备”  组中，选择“确定试点”  。  

    1. 查看针对试点推荐的设备。  

    2. 选择每个设备，并选择“添加到试点”  。 如果不同意此建议，请选择“替换”  。  

        有关桌面分析如何进行这些建议的详细信息，请选择“确定试点”  窗格右上角的信息图标。

## <a name="readiness-rules"></a>就绪规则

这些规则可帮助确定哪些设备符合就地升级条件。 可以在创建部署计划时设置这些规则，或在以后编辑它们。

更改就绪规则：

1. 在桌面分析门户中，选择部署计划。
1. 在名称旁边，选择“编辑”  。
1. 选择“就绪规则”  。
1. 选择 **Windows OS**。
1. 根据需要进行更改，然后选择“保存”  。

对于 **Windows OS** 升级，有两个可用的规则：设备驱动程序和 Windows 应用程序。

### <a name="device-drivers"></a>设备驱动程序

配置设备是否从 Windows 更新获取驱动程序。 默认情况下，此值为“关闭”  。 当使用适用于企业的 Windows 更新来管理更新（包括驱动程序）时，启用此规则。 如果使用 Configuration Manager 来管理软件更新，请将此规则设置为“关闭”  。

### <a name="windows-applications"></a>Windows 应用程序

桌面分析显示为“值得注意”  的应用基于安装计数下限阈值。 在部署计划的就绪规则中设置此阈值。 默认情况下，此阈值为 2.0%  。 可以将值从 `0.0` 更改为 `10.0`。


## <a name="next-steps"></a>后续步骤

转到下一篇文章以部署到试点设备。
> [!div class="nextstepaction"]  
> [部署到试点](deploy-pilot.md)  
