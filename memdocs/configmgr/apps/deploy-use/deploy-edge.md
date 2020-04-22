---
title: 部署并更新 Microsoft Edge 版本 77 及更高版本
titleSuffix: Configuration Manager
description: 如何在 Configuration Manager 中部署并更新 Microsoft Edge 版本 77 及更高版本
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 73b420be-5d6a-483a-be66-c4d274437508
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2c3a542355dfa01e5f4f5be12f7b1bac10f30250
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689515"
---
# <a name="microsoft-edge-management"></a>Microsoft Edge 管理

适用范围：  Configuration Manager (Current Branch)

全新的 Microsoft Edge 已准备好应用于业务。 从 Configuration Manager 版本 1910 开始，现可为你的用户部署 [Microsoft Edge 版本 77 及更高版本](https://docs.microsoft.com/deployedge/)。 PowerShell 脚本用于安装选定 Edge 版本。 此脚本还为 Edge 禁用自动更新，这样就能使用 Configuration Manager 管理它们。

## <a name="deploy-microsoft-edge"></a><a name="bkmk_Microsoft_Edge"></a> 部署 Microsoft Edge
<!--4561024-->
管理员可以选择 Beta、Dev 或 Stable 通道，以及要部署的 Microsoft Edge 客户端版本。 每个版本都包含来自客户和社区的经验学习和改进。

### <a name="prerequisites-for-deploying"></a>部署先决条件

对于目标为 Microsoft Edge 部署的客户端：

- PowerShell [执行策略](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_execution_policies)不能设置为“受限”。
  - 执行 PowerShell 以执行安装。

运行 Configuration Manager 控制台的设备需要能够访问以下终结点：

|位置|用途|
|---|---|
|`https://edgeupdates.microsoft.com/api/products?view=enterprise`|Microsoft Edge 的版本信息|
|`http://dl.delivery.mp.microsoft.com`|Microsoft Edge 版本的内容|

### <a name="verify-microsoft-edge-update-policies"></a><a name="bkmk_autoupdate"></a> 验证 Microsoft Edge 更新策略

#### <a name="configuration-manager-version-1910"></a>Configuration Manager 版本 1910

在版本 1910 中，当部署 Microsoft Edge 时，安装脚本会关闭 Microsoft Edge 的自动更新，因此可通过 Configuration Manager 对其进行管理。 可以使用组策略来更改此行为。 有关详细信息，请参阅[计划 Microsoft Edge 部署](https://docs.microsoft.com/deployedge/deploy-edge-plan-deployment#define-and-configure-policies)和 [Microsoft Edge 更新策略](https://docs.microsoft.com/DeployEdge/microsoft-edge-update-policies)。

#### <a name="configuration-manager-version-2002-and-later"></a>Configuration Manager 版本 2002 及更高版本
<!--4561024-->
从版本 2002 开始，可以创建 Microsoft Edge 应用程序，并将其设置为接收自动更新而不是禁用自动更新。 此更改允许你选择使用 Configuration Manager 管理 Microsoft Edge 更新或允许 Microsoft Edge 自动更新。 创建应用程序时，选择“Microsoft Edge 设置”页上的“允许 Microsoft Edge 自动更新最终用户设备上的客户端版本”   。 如果以前使用过组策略来更改此行为，组策略将在安装 Microsoft Edge 的过程中覆盖由 Configuration Manager 进行的设置。

[![Microsoft Edge 自动更新设置](./media/4561024-autoupdate-edge.png)](./media/4561024-autoupdate-edge.png#lightbox)

### <a name="create-a-deployment"></a>创建部署

使用内置应用程序体验创建 Microsoft Edge 应用程序，使 Microsoft Edge 更易于管理：

1. 在控制台中的“软件库”下存在一个名为“Microsoft Edge 管理”的新节点   。
1. 从功能区中选择“创建 Microsoft Edge 应用程序”，或右键单击“Microsoft Edge 管理”节点   。

   ![“Microsoft Edge 管理”节点右键单击操作](./media/4561024-create-microsoft-edge-application.png)

1. 在向导的“应用程序设置”页上，指定应用内容的名称、说明和位置  。 确保指定的内容位置文件夹为空。
1. 在“Microsoft Edge 设置”页面上，选择  ：
   - 要部署的通道
   - 要部署的版本
   - 是否“允许 Microsoft Edge 自动更新最终用户设备上的客户端版本”（版本 2002 中已添加） 
1. 在“部署”页上，确定是否要部署该应用程序  。 如果选择“是”，则可以指定应用程序的部署设置  。 有关部署设置的详细信息，请参阅[部署应用程序](deploy-applications.md#bkmk_deploy-general)。
1. 在客户端设备上的“软件中心”中，用户可以查看和安装该应用程序  。

   ![部署向导中的“Microsoft Edge 设置”页](./media/4561024-software-center-install-edge.png)

### <a name="log-files-for-deployment"></a>部署日志文件

|位置|日志|用途|
|---|---|---|
| 站点服务器|SMSProv.log|如果应用或部署创建失败，则显示详细信息。|
| [变化不定](../../core/plan-design/hierarchy/log-files.md)|PatchDownloader.log| 如果内容下载失败，则显示详细信息|
| 客户端|  AppEnforce.log|显示安装信息|

## <a name="update-microsoft-edge"></a>更新 Microsoft Edge
<!--4831871-->

从 Configuration Manager 版本 1910 开始，“Microsoft Edge 管理”下将显示名为“所有 Microsoft Edge 更新”的节点   。 此节点有助于管理所有 Microsoft Edge 通道的更新。<!--initial edge updates released Jan 15,2020-->

1. 若要获取 Microsoft Edge 的更新，请选中“更新”分类和“Microsoft Edge 产品”以[进行同步](../../sum/get-started/configure-classifications-and-products.md)   。

   [![在软件更新点属性中选择 Microsoft Edge 产品](./media/4831871-microsoft-edge-product-sup.png)](./media/4831871-microsoft-edge-product-sup.png#lightbox)

1. 在“软件库”工作区中，展开“Microsoft Edge 管理”，然后单击“所有 Microsoft Edge 更新”节点    。

1. 如果需要，请单击功能区中的“同步软件更新”，开始同步  。 有关详细信息，请参阅[同步软件更新](../../sum/get-started/synchronize-software-updates.md)。

   ![所有 Microsoft Edge 更新节点](./media/4831871-all-microsoft-edge-updates.png)

1. 管理和部署 Microsoft Edge 更新，方式与任何其他更新一样，例如将其添加到[自动部署规则](../../sum/deploy-use/automatically-deploy-software-updates.md)中。 可以通过“所有 Microsoft Edge 更新”节点执行的一些常见更新任务包括  ：

   - [创建分阶段部署](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)
   - [手动部署软件更新](../../sum/deploy-use/manually-deploy-software-updates.md)
   - [下载软件更新](../../sum/deploy-use/download-software-updates.md)

## <a name="microsoft-edge-management-dashboard"></a><a name="bkmk_edge-dash"></a> Microsoft Edge 管理仪表板
<!--3871913-->
（从版本 2002 中引入） 

从 Configuration Manager 2002 开始，Microsoft Edge 管理仪表板可让你深入了解 Microsoft Edge 和其他浏览器的使用情况。 在此仪表板中，你可以：

- 查看已安装 Microsoft Edge 的设备数
- 查看安装了不同 Microsoft Edge 版本的客户端数。
   - 此图表不包括 Canary 通道。
- 查看跨设备安装的浏览器
- 查看设备的首选浏览器 <!--5907383-->
   - 目前对于 2002 版本，此图表为空。

### <a name="prerequisites-for-the-dashboard"></a>仪表板的先决条件

在下面的 Microsoft Edge 管理仪表板中的[硬件清单](../../core/clients/manage/inventory/extend-hardware-inventory.md)类中启用以下属性：

- **已安装的软件 - 资产智能 (SMS_InstalledSoftware)**
   - 软件代码
   - 产品名称
   - 产品版本

- **默认浏览器 (SMS_DefaultBrowser)**
   - 浏览器程序 ID

- **SMS_BrowserUsage (SMS_BrowserUsage)**
   - BrowserName
   - UsagePercentage

### <a name="view-the-dashboard"></a>查看仪表板

在“软件库”工作区中，单击“Microsoft Edge 管理”以查看仪表板   。 单击“浏览”并选择其他集合，更改关系图数据的集合  。 下拉列表中默认包含五个最大的集合。 如果选择的集合不在列表中，则新选择的集合将位于下拉列表中的底部位置。

[![Microsoft Edge 管理仪表板](./media/3871913-microsoft-edge-dashboard.png)](./media/3871913-microsoft-edge-dashboard.png#lightbox)

## <a name="next-steps"></a>后续步骤

[监视应用程序](monitor-applications-from-the-console.md)

[监视软件更新](../../sum/deploy-use/monitor-software-updates.md)

[管理和监视分阶段部署](../../osd/deploy-use/manage-monitor-phased-deployments.md)
