---
title: 如何部署到试点
titleSuffix: Configuration Manager
description: 关于部署到桌面分析试点组的操作指南。
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 637fbd8e-b8ea-4c7e-95ee-a60a323c496e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 3aa722415248ad9275c6ad065f0120bfe78d3ce4
ms.sourcegitcommit: 8a023e941d90c107c9769a1f7519875a31ef9393
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/03/2020
ms.locfileid: "84311214"
---
# <a name="how-to-deploy-to-pilot-with-desktop-analytics"></a>如何通过桌面分析部署到试点

桌面分析的优点之一是可帮助识别提供最广泛因素的最小设备集。 它侧重于对 Windows 升级和更新的试点最为重要的因素。 确保试点更成功可以让你更快、更自信地迁移以在生产环境中广泛部署。  

[!INCLUDE [Definition of pilot and production](includes/define-pilot-prod.md)]

## <a name="identify-devices"></a>确定设备

第一步是确定要包含在试点中的设备。 桌面分析基于报告的数据推荐设备，你可以在此列表中包括或替换设备。

1. 转到[“桌面分析门户”](https://aka.ms/desktopanalytics)并在“管理组”中选择“部署计划”。

1. 选择部署计划。

1. 在部署计划菜单的“准备”组中，选择“确定试点”。

你将看到来自桌面分析的数据，其中显示了为获得最佳覆盖范围推荐包含的设备数。 此算法主要基于重要和关键应用的使用以及硬件配置的广度。

对于其他推荐设备列表，请执行以下操作：

- “全部添加到试点”：将所有推荐设备添加到试点组
- “添加到试点”：仅添加单个设备
- “替换”试点中的任何特定设备

将“建议”中的设备添加到“包括”试点列表中时，试点中关键和重要资产的覆盖范围和冗余程度会增加 。 较高的冗余程度意味着涵盖的资产中有很大一部分设备包含在试点中。

## <a name="global-pilot"></a><a name="bkmk_GlobalPilot"></a> 全局试点

您还可以在系统范围内决定将哪些 Configuration Manager 集合包括在试点中或从中排除。 在主桌面分析菜单中，在“全局设置”组中，选择“全局试点”。

如果将多个 Configuration Manager 层次结构连接到同一桌面分析实例，则在全局试点配置中，集合名称将采用层次结构的显示名称作为前缀。 该名称是 Configuration Manager 控制台中桌面分析连接上的“显示名称”属性。<!-- 4814075 -->

> [!NOTE]
> 必须有 Configuration Manager 版本 1910 或更高版本，才能支持多个层次结构。

- 请勿在桌面分析中包含其注册设备数超过注册设备总数 20% 的集合。 如果包含大型集合，门户会显示警告。 你可包含多个小型集合而不收到警告，但仍请注意试点中的设备数。 <!-- 6079184 -->

- 为获得有关特定 Configuration Manager 层次结构中部署计划的准确试点建议，请只包含该层次结构中的集合。

### <a name="example"></a>示例

- 在 Configuration Manager 中配置桌面分析连接以对准“全部系统”集合。 此操作可将所有客户端注册到服务。

- 还可配置其他集合以便与桌面分析同步：

  - 所有 Windows 10 客户端（3,000 台设备）

  - 所有 IT 设备（共 200 台设备，其中 150 台运行 Windows 10）

  - CEO 办公室（20 台设备）

- 在“全局试点”设置中，包括“所有 Windows 10 客户端”集合 。 排除“CEO 办公室”集合。

- 创建部署计划，并选择“所有 IT 设备”集合作为你的目标组 。 你希望此部署计划仅用于 IT 部门的设备。

- “包含的试点设备”列表中有目标组的 “所有 IT 设备”中和全局试点“包含”列表的“所有 Windows 10 客户端”中的部分设备。 该列表中有 150 台设备，因为所有 IT 设备中只有 150 台设备在运行 Windows 10。

- “其他推荐设备”列表包括“目标组”中的一组设备，它们可为你的重要资产提供最大覆盖和冗余。 桌面分析会从此列表中排除全局试点“排除”列表中的任何设备：CEO 办公室。

## <a name="address-issues"></a>解决问题

使用桌面分析门户查看报告的可能会妨碍部署的任何资产问题。 然后批准、拒绝或修改建议的修补程序。 在试点部署开始之前，所有项都必须标记“就绪”或“就绪（带修正）”。

1. 转到[“桌面分析门户”](https://aka.ms/desktopanalytics)并在“管理组”中选择“部署计划”。  

2. 选择部署计划。  

3. 在部署计划菜单的“准备”组中，选择“准备试点”。  

4. 在“应用”选项卡上，查看需要输入的应用。  

5. 对于每个应用，请选择应用名称。 在信息窗格中，查看建议，然后选择升级决策。 如果选择“未评审”或“无法”，则桌面分析不会在试点部署中包含带此应用的设备。 如果选择“就绪(带修正)”，请使用“修正说明”来捕获解决问题所需采取的措施，例如“重新安装”或“找到制造商推荐的版本”  。

6. 对其他资产重复此评审。  

要详细了解此评审过程的相关帮助，请参阅[兼容性评估](compat-assessment.md)。

## <a name="create-software"></a>创建软件

在可以部署 Windows 之前，请先在 Configuration Manager 中创建软件对象。 有关详细信息，请参阅 [Windows 10 就地升级任务序列](../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md)。

## <a name="deploy-to-pilot-devices"></a>部署到试点设备

Configuration Manager 使用桌面分析中的数据来为试点和生产部署创建集合。 这些集合位于“资产和符合性”工作区的“设备集合”节点中的“部署计划”文件夹。

> [!IMPORTANT]
> 这些集合由用于桌面分析部署计划的 Configuration Manager 管理。 不支持手动更改。 如果删除其中一个集合，则桌面分析将不起作用，并且你必须再次[连接 Configuration Manager](connect-configmgr.md)。<!--7208090-->

若要确保设备在每个部署阶段后正常运行，请使用以下步骤来创建桌面分析集成的分阶段部署：

1. 在 Configuration Manager 控制台中，转到“软件库”，展开“桌面分析服务”，然后选择“部署计划”节点  。  

2. 选择部署计划，然后在功能区中选择“部署计划详细信息”。  

3. 在功能区中选择“创建分阶段部署”。 此操作可启动“创建分阶段部署”向导。

    > [!Tip]  
    > 如果要只为试点集合创建经典任务序列部署，请在“试点状态”磁贴中选择“部署”。 此操作可启动“部署软件”向导。 有关详细信息，请参阅 [Deploy a task sequence](../osd/deploy-use/deploy-a-task-sequence.md)。  

4. 输入部署的名称，并选择要使用的任务序列。 使用选项“自动创建默认的两阶段部署”，然后配置以下集合：  

    - **第一阶段集合**：查找并选择此部署计划的“试点”集合。 此集合的标准命名约定是 `<deployment plan name> (Pilot)`。

    - **第二阶段集合**：查找并选择此部署计划的“生产”集合。 此集合的标准命名约定是 `<deployment plan name> (Production)`。

    > [!Note]  
    > 通过桌面分析集成，Configuration Manager 会自动为部署计划创建试点和生产集合。 在你可以使用它们之前，这些集合可能要花费一些时间进行同步。 有关详细信息，请参阅[排除故障 - 数据延迟](troubleshooting.md#data-latency)。<!-- 4984639 -->
    >
    > 这些集合是为桌面分析部署计划设备保留的。 不支持手动更改此类集合。<!-- 3866460, SCCMDocs-pr 3544 -->  

5. 完成向导以配置分阶段部署。 有关详细信息，请参阅[创建分阶段部署](../osd/deploy-use/create-phased-deployment-for-task-sequence.md)。

    > [!Note]  
    > 使用默认设置以便**在延迟时间段（以天为单位）后自动开始此阶段**。 必须满足以下条件才能开始第二阶段：
    >
    > 1. 第一阶段达到“部署成功百分比”的成功标准。 可在分阶段部署上配置此设置。
    > 1. 你需要在桌面分析中查看并做出升级决策，以将重要和关键资产标记为“就绪”。 有关详细信息，请参阅[查看需要升级决策的资产](deploy-prod.md#bkmk_review)。
    > 1. 桌面分析同步到 Configuration Manager 集合任何满足“就绪”条件的生产设备。

> [!Important]  
> 这些集合在其成员身份更改时会继续同步。 例如，如果你发现资产问题并将其标记为“无法”，则具有该资产的设备将不再满足“就绪”标准。 将从生产部署集合中删除这些设备。

## <a name="monitor"></a>监视

### <a name="configuration-manager-console"></a>Configuration Manager 控制台

打开部署计划。 “准备升级决策 - 总体状态”磁贴提供了部署计划状态摘要。 此状态适用于试点和生产集合。 设备可以划分为以下类别之一：

- **最新**：设备已升级到此部署计划的目标 Windows 版本

- **升级决策完成**：以下状态之一：

  - 设备所包含的值得注意的资产“就绪”或“就绪（带修正）” 

  - 设备状态为“已阻止”、“替换设备”[](about-deployment-plans.md#plan-assets)或“重新安装设备”

- **未评审**：设备所包含的值得注意的资产“未评审”或“正在评审”

设备状态会在进行以下操作时在“试点状态”和“生产状态”磁贴中更新：

- 对兼容性评估进行更改
- 设备已升级到 Windows 的目标版本
- 你的部署进度

你还可以使用与任何其他任务序列部署相同的 Configuration Manager 部署监控。 有关详细信息，请参阅[监视操作系统部署](../osd/deploy-use/monitor-operating-system-deployments.md)。

### <a name="desktop-analytics-portal"></a>桌面分析门户

使用[桌面分析门户](https://aka.ms/desktopanalytics)查看任何部署计划的状态。 选择部署计划，然后选择“计划概述”。

![桌面分析中部署计划概述的屏幕截图](media/deployment-plan-overview.png)

选择“试点”磁贴。 它汇总了试点部署的当前状态。 此磁贴还显示未开始、正在进行、已完成或返回问题的设备数量数据。

任何报告错误或其他问题的设备也会在右侧的“试点详细信息”区域中列出。 要获取所报告问题的详细信息，请选择“查看”。 此操作会将视图更改为“部署状态”页

“部署状态”页按下列类别列出设备：

- 未启动
- 正在进行
- 完成
- 需引起注意 - 设备
- 需引起注意 - 问题

“需引起注意”类别显示相同的信息，但以不同的方式进行排序。

在任一视图中选择特定列表可详细了解检测到的问题。

解决这些部署问题时，仪表板将继续显示设备的进度。 它会随着设备从“需引起注意”移动到“已完成”完成更新。

## <a name="next-steps"></a>后续步骤

让试点运行一段时间，以收集操作数据。 鼓励试点设备的用户测试应用。

当试点部署达到你的成功条件时，请转到下一篇文章来部署到生产。
> [!div class="nextstepaction"]  
> [部署到生产](deploy-prod.md)  
