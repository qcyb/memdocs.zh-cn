---
title: 管理高风险部署
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中配置部署验证站点设置，以便在管理员创建高风险部署时发出警告。
ms.date: 02/26/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8d37b983-a964-402c-819d-2512ed2d463b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3f1498c383f9b02f7f322de3ba5708351e84c3b7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703295"
---
# <a name="settings-to-manage-high-risk-deployments-for-configuration-manager"></a>用于管理 Configuration Manager 的高风险部署的设置

适用范围：  Configuration Manager (Current Branch)

使用 Configuration Manager，可以配置部署验证站点设置  。 这些设置在管理员创建高风险任务序列部署时发出警告。 其中一项高风险部署是：  

- 自动安装的部署  

- 可能产生意外结果  

例如，其用途为“必需”的部署操作系统的任务序列被认为是高风险部署  。  

> [!WARNING]
> 如果使用 PXE 部署，并在配置设备硬件时将网络适配器作为第一个启动设备，则这些设备可以自动启动 OS 部署任务序列而无需用户交互。 部署验证不会管理此配置。 尽管此配置可以简化流程并减少用户交互，但它会增加设备意外重置映像的风险。

## <a name="deployment-verification-settings"></a><a name="bkmk_settings"></a>部署验证设置

若要降低不需要的高风险部署的风险，可以在这些部署验证设置中配置大小限制：  

- **集合大小限制**：创建部署时，隐藏包含的客户端数多于限制的集合。  

  - **默认大小**：创建部署时，此设置默认隐藏包含的客户端数多于此限制的集合。 创建部署时，仍然可以查看这些集合，但会默认隐藏这些集合。 默认值为 100  。 要忽略此设置，请输入值 0  。  

  - **最大大小**：创建部署时，此设置总是隐藏客户端数多于此限制的集合。 默认值为 0，将忽略此设置  。 “最大大小”  值必须大于“默认大小”  值。  

    例如，将“默认大小”  设置为 100，将“最大大小”  设置为 1000。 创建高风险部署时，“选择集合”窗口仅显示包含的客户端数少于 100 个的集合  。 如果清除“隐藏成员数大于站点最低大小配置的集合”设置，则该窗口显示包含的客户端数少于 1000 的集合  。  

- **包含站点系统服务器的集合**：目标集合包含具有站点系统角色的计算机时，创建部署前将阻止部署或要求验证。 部署被阻止时，选择一个符合部署验证条件的不同集合，以继续创建部署。  

> [!NOTE]
> 高风险部署始终局限于自定义集合、你所创建的集合和内置“未知计算机”  集合。 创建高风险部署时，无法选择“所有系统”等内置集合  。  

## <a name="configure-deployment-verification"></a>配置部署验证

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“站点配置”，选择“站点”，然后选择要配置的主站点    。

2. 单击功能区中的“属性”，然后切换到“部署验证”选项卡   。

3. 配置要使用的[设置](#bkmk_settings)，然后选择“确定”以保存配置并关闭属性  。

## <a name="next-steps"></a>后续步骤

[管理任务序列 - “影响重大”设置](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#high-impact-settings)

[卸载站点和层次结构](../deploy/configure/configure-sites-and-hierarchies.md)
