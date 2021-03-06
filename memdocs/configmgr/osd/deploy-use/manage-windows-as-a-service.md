---
title: 将 Windows 作为一项服务来管理
titleSuffix: Configuration Manager
description: 使用 Configuration Manager 查看 Windows 即服务 (WaaS) 的状态，创建维护服务计划以形成部署环，以及在 Windows 10 客户端即将结束支持时查看警报。
ms.date: 03/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: da1e687b-28f6-43c4-b14a-ff2b76e60d24
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9a682ec0b3d438a26429486f119d641fd150404f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690325"
---
# <a name="manage-windows-as-a-service-using-configuration-manager"></a>使用 Configuration Manager 将 Windows 作为服务进行管理

适用范围：  Configuration Manager (Current Branch)

在 Configuration Manager 中，可以查看环境中 Windows 即服务 (WaaS) 的状态。 创建维护服务计划以形成部署环，并在新的内部版本发布时，确保 Windows 10 系统保持最新。 此外，还可以在 Windows 10 客户端即将结束对半年频道内部版本的支持时查看警报。

有关 Windows 10 维护服务选项的详细信息，请参阅 [Windows 即服务概述](/windows/deployment/update/waas-overview#servicing-channels)。

使用以下部分将 Windows 作为服务进行管理。

## <a name="prerequisites"></a><a name="BKMK_Prerequisites"></a> 先决条件

若要在 Windows 10 维护服务仪表板中查看数据，必须执行以下操作：

- Windows 10 计算机必须搭配使用 Configuration Manager 软件更新和 Windows Server Update Services (WSUS) 以进行软件更新管理。 当计算机使用适用于企业的 Windows 更新（或 Windows 预览体验计划）进行软件更新管理时，不会在 Windows 10 维护服务计划中评估该计算机。 有关详细信息，请参阅 [在 Windows 10 中与 Windows Update for Business 集成](../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md)。

- 使用受支持的 WSUS 版本：
  - WSUS 10.0.14393（Windows Server 2016 中的角色）
  - WSUS 10.0.17763（Windows Server 2019 中的角色）（需要使用 Configuration Manager 1810 或更高版本）
  - WSUS 6.2 和 6.3（Windows Server 2012 和 Windows Server 2012 R2 中的角色）
    - 必须在 WSUS 6.2 和 6.3 上安装 [KB 3095113 和 KB 3159706（或等效更新）](../../sum/plan-design/prerequisites-for-software-updates.md#BKMK_wsus2012)。

- 启用检测信号发现。 可使用发现找到 Windows 10 维护仪表板中显示的数据。 有关详细信息，请参阅 [Configure Heartbeat Discovery](../../core/servers/deploy/configure/configure-discovery-methods.md#BKMK_ConfigHBDisc)。

    可在以下属性中发现和存储下面的 Windows 10 频道和内部版本信息：  

    - **操作系统准备情况分支**：指定操作系统通道。 例如，**0** = 半年频道 - 定向(不延迟更新)，**1** = 半年频道(延迟更新)，**2** = 长期服务频道(LTSC)

    - **操作系统版本**：指定操作系统内部版本。 例如，**10.0.10240** (RTM) 或 **10.0.10586**（版本 1511）

- 必须安装服务连接点并将其配置为“联机，持续连接”  模式，才能在 Windows 10 维护服务仪表板上查看数据。 处于脱机模式时，在获取 Configuration Manager 维护服务更新之前，不会在仪表板中看到数据更新。 有关详细信息，请参阅[关于服务连接点](../../core/servers/deploy/configure/about-the-service-connection-point.md)。

- 必须在运行 Configuration Manager 控制台的计算机上安装 Internet Explorer 9 或更高版本。

- 必须配置和同步软件更新。 选择“升级”  分类并同步软件更新之后，才能在 Configuration Manager 控制台中使用 Windows 10 功能升级。 有关详细信息，请参阅[准备软件更新管理](../../sum/get-started/prepare-for-software-updates-management.md)。

- 从 Configuration Manager 1902 版开始，验证“为功能更新指定线程优先级”  [客户端设置](../../core/clients/deploy/about-client-settings.md#bkmk_thread-priority)以确保它适合你的环境。

- 从 Configuration Manager 1906 版开始，验证“为功能更新启用动态更新”  [客户端设置](../../core/clients/deploy/about-client-settings.md#bkmk_du)以确保它适合你的环境。 <!--4062619-->

## <a name="windows-10-servicing-dashboard"></a><a name="BKMK_ServicingDashboard"></a> Windows 10 维护服务仪表板

Windows 10 维护服务仪表板提供了有关环境中的 Windows 10 计算机和活动维护服务计划的信息以及符合性信息等。 Windows 10 维护服务仪表板中的数据依赖于安装服务连接点。 该仪表板具有以下磁贴：

- **“Windows 10 使用情况”磁贴**：提供 Windows 10 公共内部版本的细分。 将 Windows 预览体验计划内部版本以及你尚未告知站点的任何内部版本列出“其他”  。 服务连接点会下载告知其 Windows 内部版本的元数据，然后将此数据与发现数据进行比较。

- **“Windows 10 更新通道”磁贴**：按通道和就绪状态提供 Windows 10 的细分。 LTSC 段包括所有 LTSC 版本。 第一个磁贴对特定版本进行细分，例如 Windows 10 LTSC 2015。

- **“创建服务计划”磁贴**：提供创建维护服务计划的快速方法。 指定名称、集合（仅显示从小到大的前 10 个集合）、部署包（仅显示最近修改的前 10 个包）和就绪状态。 其他设置使用默认值。 单击“高级设置”以启动“创建维护服务计划向导”，可在该向导中配置所有服务计划设置  。

- **“已过期”磁贴**：显示运行已超过其使用期限的 Windows 10 版本的设备的百分比。 Configuration Manager 从服务连接点下载的元数据确定百分比，并将其与发现数据比较。 超过其使用期限的内部版本将不再接收月度累计更新（包括安全更新）。 应将此类别中的计算机升级到下一个内部版本。 Configuration Manager 将进一成为整数。 例如，如果你有 10,000 台计算机，而只有一台运行已过期的内部版本，则该磁贴显示 1%。

- **“即将过期”磁贴**：显示运行接近使用期限（将在约四个月内过期）的内部版本的计算机的百分比，与“已过期”磁贴类似  。 Configuration Manager 将进一成为整数。

- **“警报”磁贴**：显示活动警报。

- **“服务计划监视”磁贴**：显示已创建的维护服务计划，以及每个计划的符合性图表。 该磁贴提供维护服务计划部署当前状态的简要概述。 如果较早的部署环满足你对符合性的期望，则可以选择较晚的维护服务计划（部署环）然后单击“立即部署”  ，而不必等待自动触发维护服务计划规则。

- **“Windows 10 内部版本”磁贴**：显示固定的映像时间线，它提供当前发布的 Windows 10 内部版本的概述，以及内部版本转换为各种状态的大致时间。 从 Configuration Manager 1902 版开始，已删除此磁贴，因为[产品生命周期仪表板](../../core/clients/manage/asset-intelligence/product-lifecycle-dashboard.md)中提供了更详细的信息。 <!--3446861-->

> [!IMPORTANT]
> Windows 10 维护服务仪表板中显示的信息（例如 Windows 10 版本的支持使用期限）是出于方便考虑而提供的，仅供公司内部使用。 不应仅依赖此信息来确认更新符合性。 请务必验证所提供信息的准确性。

## <a name="drill-through-required-updates"></a>钻取必需更新
<!--4224414-->
（从版本 1906 中引入） 

可深入查看符合性统计信息，了解哪些设备需要特定 Windows 10 功能更新。 若要查看设备列表，需要具有查看更新和设备所属集合的权限。 向下钻取设备列表：

1. 转到“软件库” > “Windows 10 维护服务” > “所有 Windows 10 更新”    。
1. 选择至少一台设备所需的任何更新。
1. 查看“摘要”选项卡，找到“统计信息”下的饼图   。
1. 选择饼图旁的“查看所需更新”超链接以深入查看设备列表  。
1. 此操作将转到“设备”下的临时节点，可以在其中查看需要更新的设备  。 还可对节点执行操作，例如从列表创建新集合。

## <a name="servicing-plan-workflow"></a>维护服务计划工作流

Configuration Manager 中的 Windows 10 维护服务计划非常类似于软件更新的自动部署规则。 可使用以下 Configuration Manager 评估的条件创建维护服务计划：

- **升级分类**：仅限评估“升级”分类中的更新  。

- **就绪状态**：将比较维护服务计划中定义的就绪状态与升级的就绪状态。 服务连接点检查更新时，将检索升级的元数据。

- **时间延迟**：在维护服务计划中，你为“Microsoft 发布新升级后，你希望等待多少天再在新环境中进行部署”指定的天数  。 如果当前日期晚于发布日期加上配置的天数，Configuration Manager 会评估是否在部署中包含升级。

  当升级符合条件时，维护服务计划会将升级添加到部署包并将包分发到分发点，然后基于在维护服务计划中配置的设置将升级部署到集合。 你可以在 Windows 10 维护服务仪表板上的“服务计划监视”磁贴中监视部署。 有关详细信息，请参阅[监视软件更新](../../sum/deploy-use/monitor-software-updates.md)。

> [!NOTE]
> Windows 10 版本 1903 以及更高版本作为独立产品添加到 Microsoft 更新，而不像早期版本那样属于 Windows 10 产品   。 这项更改需要你执行许多手动步骤，才可确保客户端显示这些更新。 我们已采取措施减少了需要手动对 Configuration Manager 版本 1906 中的新产品执行操作的步骤数量。 有关详细信息，请参阅[配置 Windows 10 各版本的产品](../../sum/get-started/configure-classifications-and-products.md#windows-10-version-1903-and-later)。<!--4682946-->

## <a name="windows-10-servicing-plan"></a><a name="BKMK_ServicingPlan"></a> Windows 10 维护服务计划

部署 Windows 10 半年频道时，可以创建一个或多个维护服务计划，以定义环境所需的部署环，然后在 Windows 10 维护服务仪表板中监视它们。 维护服务计划仅使用“升级”软件更新分类，而不使用 Windows 10 的累积更新。  这些更新仍需要使用软件更新工作流进行部署。 维修服务计划的最终用户体验与软件更新体验相同，包括你在维护服务计划中配置的设置。  

> [!NOTE]
> 可以使用任务序列来为每个 Windows 10 内部版本部署升级，但这样做需要进行更多手动操作。 你需要将更新的源文件作为操作系统升级包导入，然后创建任务序列并将其部署到适当计算机组。 但是，任务序列提供其他自定义选项，如部署前和部署后操作。

可以从 Windows 10 维护服务仪表板创建基本维护服务计划。 指定名称、集合（仅显示从小到大的前 10 个集合）、部署包（仅显示最近修改的前 10 个包）和就绪状态后，Configuration Manager 会使用其他设置的默认值创建维护服务计划。 也可以启动“创建维护服务计划向导”来配置所有设置。 使用“创建使用维护服务计划向导”，通过以下过程创建维护服务计划。  

> [!NOTE]  
> 你可以管理高风险部署的行为。 高风险部署是自动安装、可能产生意外结果的部署。 例如，其用途为 **必需** 部署 Windows 10 的任务序列被认为是高风险部署。 有关详细信息，请参阅[用于管理高风险部署的设置](../../core/servers/manage/settings-to-manage-high-risk-deployments.md)。

### <a name="to-create-a-windows-10-servicing-plan"></a>创建 Windows 10 维护服务计划

1. 在 Configuration Manager 控制台中，单击“软件库”  。

1. 在“软件库”工作区中，展开“Windows 10 维护服务”  ，然后单击“维护服务计划”  。

1. 在“主页”  选项卡上的“创建”  组中，单击“创建维护服务计划”  。 将打开“创建维护服务计划向导”。

1. 在“常规”  页上，配置下列设置：

    - **名称**：指定维护服务计划的名称。 此名称必须唯一并且有助于描述规则的目的，并且应与 Configuration Manager 站点中的其他名称区分开来。

    - **描述**：指定维护服务计划的描述。 描述应概述维护服务计划和任何其他相关信息，帮助在 Configuration Manager 站点内的其他项中标识和区分该计划。 描述字段是可选字段，最多不超过 256 个字符，默认情况下具有空白值。

1. 在“维护服务计划”页上，指定“目标集合”  。 集合的成员将接收维护服务计划中定义的 Windows 10 升级。

    - 部署高风险部署（例如维护服务计划）时，“选择集合”  窗口仅显示满足在站点属性中配置的部署验证设置的自定义集合。

    - 高风险部署始终局限于自定义集合、你所创建的集合和内置“未知计算机”  集合。 创建高风险部署时，无法选择“所有系统”等内置集合  。 取消选中“隐藏成员数大于站点最低大小配置的集合”  以查看所含客户端少于配置的最大大小的全部自定义集合。 有关详细信息，请参阅[用于管理高风险部署的设置](../../core/servers/manage/settings-to-manage-high-risk-deployments.md)。

    - 部署验证设置基于集合的当前成员身份。 部署维护服务计划后，不会重新评估高风险部署设置的集合成员身份。

      - 例如，假设将“默认大小”  设置为 100，将“最大大小”  设置为 1000。 当创建高风险部署时，“选择集合”  窗口仅显示包含的客户端少于 100 个的集合。 如果清除“隐藏成员数大于站点最低大小配置的集合”  设置，则该窗口将显示其客户端少于 1000 个的集合。  
      选择包含站点角色的集合时，以下标准适用：
        - 如果集合包含站点系统服务器，而你在部署验证设置中配置为阻止具有站点系统服务器的集合，则将出现错误且无法继续操作。
        - 如果集合包含站点系统服务器，而你在部署验证设置中配置为在集合具有站点系统服务器、超过默认大小值或包含服务器时发出警告，则部署软件向导将显示高风险警告。 你必须同意创建高风险部署，这时将创建审核状态消息。

1. 在“部署环”页上配置下列设置：

   - **指定此维护服务计划应该应用的 Windows 就绪状态**：选择下列选项之一：

      - **半年频道(定向)** ：在此维护服务模型中，功能更新在 Microsoft 发布后便可使用。

      - **半年频道**：此维护服务频道通常用于广泛部署。 不久以后，半年频道中的 Windows 10 客户端将获得与定向频道中的设备相同的 Windows 10 内部版本。

        有关维护服务频道和最适合你的选项的详细信息，请参阅[维护服务频道](/windows/deployment/update/waas-overview#servicing-channels)。

   - **Microsoft 发布新升级后，你希望等待多少天再在新环境中进行部署**：如果当前日期晚于发布日期加上为此设置配置的天数，Configuration Manager 会评估是否在部署中包含升级。

1. 在“升级”页面上，配置搜索条件以筛选添加到服务计划的升级。 只有满足指定条件的升级项才会添加到关联部署中。 可用属性筛选器如下： <!--3098809, 3113836, 3204570 -->

   - **体系结构**（从 1810 版开始）
   - **语言**
   - **产品类别**（从 1810 版开始）
   - **必需**
      > [!IMPORTANT]
      > 建议将“所需”  字段的值设置为“>=1”  ，作为搜索条件的一部分。 使用此条件可确保只向服务计划添加适用的更新。
   - **被取代**（从 1810 版开始）
   - **标题**

    单击“预览”  可查看符合指定条件的升级。

1. 在“部署计划”页上配置下列设置：

   - **计划评估**：指定 Configuration Manager 是使用 UTC 还是使用运行 Configuration Manager 控制台的计算机的本地时间来计算可用的时间和安装截止时间。

       > [!NOTE]
       > 选择本地时间，并为“软件可用时间”  或“安装截止时间”  选择“尽快”  时，将使用运行 Configuration Manager 控制台的计算机上的当前时间来计算更新可用的时间或在客户端上安装更新的时间。 如果客户端位于其他时区，当客户端的时间达到评估时间时将发生这些操作。

   - **软件可用时间**：选择以下设置之一以指定向客户端提供软件更新的时间：

        - **尽快**：选择此设置以尽快向客户端计算机提供部署中所包括的软件更新。 创建部署并选择此设置后，Configuration Manager 将更新客户端策略。 然后在下一个客户端策略轮询周期，客户端将注意部署并且可以获得可安装的更新。

        - **特定时间**：选择此设置以在特定日期和时间向客户端计算机提供部署中所包括的软件更新。 创建部署并启用此设置后，Configuration Manager 将更新客户端策略。 然后在下一个客户端策略轮询周期，客户端将注意部署。 但是，在配置的日期和时间之后，部署中的软件更新才可用于安装。

   - **安装截止时间**：选择以下设置之一以指定部署中的软件更新的安装截止时间：

        - **尽快**：选择此设置以尽快自动安装部署中的软件更新。

        - **特定时间**：选择此设置以在特定日期和时间自动安装部署中的软件更新。 通过将已配置的“特定时间”  间隔添加到“软件可用时间”  ，Configuration Manager 可确定安装软件更新的截止时间。

           > [!NOTE]
           > 实际安装截止时间是显示的截止时间加上随机的一段时间（最多为 2 小时）。 这可以减少目标集合中同时在部署中安装软件更新的所有客户端计算机的潜在影响。
           >
           > 你可以配置“计算机代理”  客户端设置，“禁用截止时间随机化”  ，以对所需的更新禁用安装随机化延迟。 有关详细信息，请参阅 [Computer Agent](../../core/clients/deploy/about-client-settings.md#computer-agent)。

        - **根据用户首选项延迟对此部署的强制操作，最长延迟到客户端上定义的宽限期**：选择此选项，遵守[部署截止日期后强制的宽限期(小时)](../../core/clients/deploy/about-client-settings.md#grace-period-for-enforcement-after-deployment-deadline-hours)  。

1. 在“用户体验”页上，请配置下列设置：  

    - **用户通知**：指定是否在配置的“可用时间”在客户端计算机上软件中心中显示软件更新通知，以及是否在客户端计算机上显示用户通知  。

    - **截止时间行为**：指定到达更新部署的截止时间时要发生的行为。 指定是否在部署中安装更新。 另外，指定是否在安装更新后执行系统重启而不考虑配置的维护时段。 有关维护时段的详细信息，请参阅[如何使用维护时段](../../core/clients/manage/collections/use-maintenance-windows.md)。  

    - **设备重启行为**：指定安装更新后是否在服务器和工作站上抑制系统重启，以及是否需要重启系统以完成安装。

    - **Windows Embedded 设备的写入筛选器处理**：将更新部署到启用了写入筛选器的 Windows Embedded 设备时，可指定将更新安装在临时覆盖区上并稍后提交更改，或者在安装截止时或在维护时段内提交更改。 如果在安装截止时或在维护时段内提交更改，则需要重新启动，而且更改将保留在设备上。
        - 将更新部署到 Windows Embedded 设备时，确保设备是配置了维护时段的集合的成员。

    - **重启时软件更新部署重新评估行为**：要在重启后强制执行其他更新部署评估周期，请选择“如果此部署中的任何更新需要重启系统，请在重启后运行更新部署评估周期”选项  。

1. 在“部署包”页上，选择现有部署包、不选择任何包，或者配置下列设置来创建新的部署包：

    1. **名称**：指定部署包的名称。 该名称必须是描述包内容的唯一名称。 限制为不超过 50 个字符。

    1. **描述**：指定提供有关该部署包的信息的说明。 该说明仅限于 127 个字符。

    1. **包源**：指定软件更新源文件的位置。 键入源位置的网络路径，例如 \\\server\\sharename\\path，或单击“浏览”来查找网络位置   。 在继续进入到下一页之前，为部署包源文件创建共享文件夹。
        - 其他软件部署包不能使用你指定的部署包源位置。
        - SMS 提供程序计算机帐户和运行向导下载软件更新的用户都必须对下载位置具有“写”  NTFS 权限。 应仔细限制对此下载位置的访问，以减少攻击者篡改软件更新源文件的风险。
        - 在 Configuration Manager 创建部署包之后，可在部署包属性中更改包源位置。 但是，如果你执行此操作，则必须首先将原始包源中的内容复制到新包源位置。

    1. **发送优先级**：指定部署包的发送优先级。 Configuration Manager 在将包发送到分发点时将使用部署包的发送优先级。 部署包按优先级顺序发送：高、中或低。 具有相同优先级的包按照其创建顺序发送。 如果没有积压工作 (backlog)，则立即处理包，而不考虑优先级。

    1. **启用二进制差异复制**：如果要使用二进制差异复制，请启用此选项。

1. 在“分发点”页上，指定承载更新文件的分发点或分发点组。 有关分发点的详细信息，请参阅[配置分发点](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs)。

    > [!NOTE]
    > 只有当你在创建新的软件更新部署包时才能使用本页。  

1. 在“下载位置”页上，指定是从 Internet 还是从本地网络下载更新文件。 配置下列设置：

    - **从 Internet 下载软件更新**：选择此设置以从 Internet 上的指定位置下载更新。 默认情况下将启用此设置。

    - **从本地网络上的位置下载软件更新**：选择此设置以从本地目录或共享文件夹中下载更新。 运行向导的计算机无法访问 Internet 时，此设置很有用。 能够访问 Internet 的任何计算机可以先下载更新，然后将它们存储在可从运行向导的计算机中访问的本地网络上的某个位置。

1. 在“语言选择”页上，为已选定要下载的更新选择语言。 只有在提供了与所选语言对应的更新时才下载更新。 非语言特定的更新可随时下载。 默认情况下，向导会选择你已在软件更新点属性中配置的语言。 在继续进入下一页之前，必须选择至少一种语言。 如果仅选择更新不支持的语言，则更新的下载将失败。

1. 在“摘要”页上查看设置，然后单击“下一步”  以创建维护服务计划。  

完成向导后，将运行维护服务计划。 它会将符合指定条件的更新添加到软件更新组中，将更新下载到站点服务器上的内容库，将更新分发到已配置的分发点，然后将软件更新组部署到目标集合中的客户端。

## <a name="modify-a-servicing-plan"></a><a name="BKMK_ModifyServicingPlan"></a> 修改维护服务计划

从 Windows 10 维护服务仪表板创建基本维护服务计划后，或需要更改现有维护服务计划的设置时，可以转到维护服务计划属性。

> [!NOTE]
> 创建维护服务计划时，可在向导中不可用的维护计划的属性中配置设置。 向导对以下设置使用默认设置：下载设置、部署设置和警报。  

使用以下过程来修改维护服务计划的属性。 

### <a name="to-modify-the-properties-of-a-servicing-plan"></a>修改维护服务计划的属性

1. 在 Configuration Manager 控制台中，单击“软件库”  。

1. 在“软件库”工作区中，展开“Windows 10 维护服务”，单击“维护服务计划”，然后选择要修改的维护服务计划   。

1. 在“主页”  选项卡上，单击“属性”  以打开所选维护服务计划的属性。

    以下设置可在向导中未配置的维护服务计划属性中使用：

    **部署设置**：在“部署设置”选项卡上，配置以下设置：

    - **使用 LAN 唤醒来唤醒客户端进行必需的部署**：指定在截止时间是否启用 LAN 唤醒，以将唤醒数据包发送到需要部署中的一个或多个软件更新的计算机。 在安装截止时间处于睡眠模式的任何计算机都会被唤醒，以便启动软件更新安装。 处于睡眠模式且不需要部署中的任何软件更新的客户端不会启动。 默认情况下禁用此设置。

        > [!WARNING]
        > 必须针对“LAN 唤醒”配置计算机和网络，然后才能使用此选项。

    - **详细信息级别**：指定客户端计算机报告的状态消息的详细信息级别。

    **下载设置**：在“下载设置”选项卡上，配置以下设置：

    - 指定当客户端连接到慢速网络或正在使用回退内容位置时，是否下载和安装软件更新。

    - 指定当软件更新的内容在首选分发点上不可用时客户端是否下载和安装回退分发点中的软件更新。

    - **允许客户端与同一子网上的其他客户端共享内容**：指定是否为内容下载启用 BranchCache。 有关 BranchCache 的详细信息，请参阅[内容管理的基本概念](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache)。

    - 指定在分发点上没有软件更新的情况下是否让客户端从 Microsoft 更新下载软件更新。
        > [!IMPORTANT]
        > 不要将此设置用于 Windows 10 维护服务更新。 Configuration Manager（至少到版本 1610）无法从 Microsoft 更新下载 Windows 10 维护服务更新。

    - 指定是否允许客户端在安装截止日期之后下载内容（如果客户端使用按流量计费的 Internet 连接）。 Internet 提供商有时根据你在按流量计费的 Internet 连接上发送和接收的数据量计费。

    **警报**：在“警报”选项卡上，配置 Configuration Manager 和 System Center Operations Manager 为此部署生成警报的方式。
    - 你可以从“软件库”  工作区的“软件更新”  节点中查看最新软件更新警报。

## <a name="next-steps"></a>后续步骤

有关详细信息，请参阅 [Configuration Manager 即服务和 Windows 即服务的基础知识](../../core/understand/configuration-manager-and-windows-as-service.md)。
