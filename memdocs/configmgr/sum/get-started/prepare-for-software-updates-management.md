---
title: 准备软件更新管理
titleSuffix: Configuration Manager
description: 若要准备管理更新，请完成以下任务以显示 Configuration Manager 控制台中的符合性评估数据。
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 01907900-e28b-4cd7-9479-42906416707b
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: ab22fdcacf7574884f7cfd21859cb4b1aeb8e23f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81699495"
---
# <a name="prepare-for-software-updates-management"></a>准备软件更新管理

适用范围：  Configuration Manager (Current Branch)

在软件更新的符合性评估数据显示在 Configuration Manager 控制台中之前，以及在可以将软件更新部署到客户端计算机之前，必须完成以下部分中的步骤。

## <a name="step-1-install-a-software-update-point"></a>步骤 1：安装软件更新点  
管理中心站点或独立主站点以及主站点上需要软件更新点，以便启用软件更新符合性评估以及将软件更新部署到客户端。 软件更新点在辅助站点上是可选的。 更多详细信息，请参阅 [Install a software update point](install-a-software-update-point.md)（安装软件更新点）  

## <a name="step-2-synchronize-software-updates"></a>步骤 2:同步软件更新
软件更新同步是指检索满足配置条件的软件更新元数据的过程。 同步软件更新后，软件更新才会显示在 Configuration Manager 控制台中。 有关详细信息，请参阅[同步软件更新](synchronize-software-updates.md)。   

## <a name="step-3-configure-classifications-and-products-to-synchronize"></a>步骤 3：配置要同步的分类和产品
在管理中心站点或独立主站点上执行此配置。 第一次同步软件更新后，Configuration Manager 将检索分类和产品的更新列表。 现在，可以在“软件更新点组件”属性中选择新的选项。 配置新的分类和产品后，请重复步骤 2，以启动软件更新同步在新的条件下检索软件更新元数据。 有关详细信息，请参阅 [Configure classifications and products to synchronize](configure-classifications-and-products.md)（配置要同步的分类和产品）。

## <a name="step-4-manage-settings-for-software-updates"></a>步骤 4：管理软件更新的设置
同步软件更新后，在部署软件更新之前请验证 Configuration Manager 客户端设置、组策略配置和软件更新设置。 更多详细信息，请参阅 [Manage settings for software updates](manage-settings-for-software-updates.md)（管理软件更新的设置）。
