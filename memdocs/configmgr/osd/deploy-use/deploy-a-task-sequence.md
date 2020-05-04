---
title: 部署任务序列
titleSuffix: Configuration Manager
description: 使用此信息将任务序列部署到集合中的计算机。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b2abcdb0-72e0-4c70-a4b8-7827480ba5b2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c2347275ffdc194e73cf792d6f83ffa75732f8c4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81691125"
---
# <a name="deploy-a-task-sequence"></a>部署任务序列

适用范围：  Configuration Manager (Current Branch)

创建任务序列并分发引用的内容后，将其部署到设备集合。 使用此操作可以在设备上运行任务序列。 经过部署的任务序列可以自动运行，也可以在由设备的用户安装时运行。

> [!WARNING]  
> 你可以管理高风险任务序列部署的行为。 高风险部署是自动安装、可能产生意外结果的部署。 例如，部署目的为“必需”且部署 OS 的任务序列被认为是高风险部署  。 有关详细信息，请参阅[用于管理高风险部署的设置](../../core/servers/manage/settings-to-manage-high-risk-deployments.md)。  

## <a name="process"></a>过程

使用以下过程将任务序列部署到集合中的计算机。  

> [!NOTE]  
> 任务序列部署的状态消息显示在主站点上的“消息”窗口中，但不会显示在管理中心站点上。  

1. 在 Configuration Manager 控制台中，转到“软件库”  工作区，展开“操作系统”  ，然后选择“任务序列”  节点。  

2. 在“任务序列”  列表中，选择要部署的任务序列。  

3. 在功能区的“主页”  选项卡上，在“部署”  组中，选择“部署”  。  

    > [!NOTE]  
    > 如果“部署”  不可用，则任务序列会有无效的引用。 纠正该引用，然后再次尝试部署任务序列。  

4. 在“常规”页面上，指定以下信息  。  

    - **任务序列**：指定要部署的任务序列。 默认情况下，此框显示所选的任务序列。  

    - **集合**：选择包含要运行任务序列的计算机的集合。  

        不要部署将 OS 安装到不适合的集合（例如所有数据中心服务器集合）的任务序列。 请确保所选集合仅包含要运行任务序列的那些计算机。  

        有关高风险部署的详细信息，请参阅[高风险部署](#bkmk_high-risk)。

    - **使用与此集合关联的默认分发点组**：将任务序列内容存储在集合默认分发点组上。 如果未将所选集合与分发点组关联，则此选项为灰色。  

    - **为依赖关系自动分发内容**：如果任何引用的内容具有依赖项，则该站点也会将从属内容发送到分发点。  

    - **此任务序列的预下载内容**：有关详细信息，请参阅[配置预缓存内容](configure-precache-content.md)。  

    - **选择部署模板**：为任务序列保存和指定部署模板。<!--1357391-->  

        > [!IMPORTANT]  
        > 某些项目未保存在模板中。<!--510610--> 确保在运行部署向导时应用以下各项：  
        >
        > - 软件安装
        > - 计划
        > - 预下载内容

    - **备注(可选)** ：指定描述此任务序列部署的其他信息。  

5. 在“部署设置”页上，指定以下信息  ：  

    - **目的**：从下拉列表中，选择下列选项之一：  

        - **可用**：用户会在软件中心看到该任务序列，并可根据需要进行安装。  

        - **必需**：Configuration Manager 将自动根据配置计划自动运行任务序列。 如果任务序列未隐藏，则用户仍可以跟踪其部署状态。 在截止时间之前，用户还可通过软件中心安装任务序列。  

        > [!NOTE]
        > 如果多个用户登录设备，软件中心内可能无法显示包和任务序列部署。  

    - **可用于以下项目**：指定任务序列是否可用于以下任一类型：  

        - 仅 Configuration Manager 客户端  
        - Configuration Manager 客户端、媒体和 PXE  
        - 仅媒体和 PXE  
        - 仅媒体和 PXE（隐藏）  

        > [!IMPORTANT]  
        > 将“仅媒体和 PXE (隐藏)”  设置用于自动化任务序列部署。 要让计算机在无用户干预的情况下自动启动到该部署，请选择“允许无人参与的操作系统部署”  ，并将 SMSTSPreferredAdvertID  变量设置为媒体的一部分。 有关任务序列变量的详细信息，请参阅[任务序列变量](../understand/task-sequence-variables.md#SMSTSPreferredAdvertID)。  

    - **发送唤醒数据包**：如果部署为“必需”并选择此选项，则在客户端运行部署前，该站点会将唤醒数据包发送到计算机  。 此数据包可在到达安装截止时间时将计算机从休眠中唤醒。 使用此选项前，必须针对“LAN 唤醒”配置计算机和网络。 有关详细信息，请参阅[计划如何唤醒客户端](../../core/clients/deploy/plan/plan-wake-up-clients.md)。  

    - 允许客户端使用按流量计费的 Internet 连接在安装截止时间之后下载内容，这可能会导致附加成本  ：此选项仅适用于所需部署  。 如果你的自定义任务序列安装应用程序但不部署 OS，则可以指定是否允许客户端在安装截止日期之后下载内容（如果客户端使用按流量计费的 Internet 连接）。 Internet 提供商有时根据你在按流量计费的 Internet 连接上使用的数据量计费。  

        > [!NOTE]  
        > 虽然使用按流量计费的 Internet 连接可能对不部署 OS 的任务序列有效，但不支持这种连接。  

6. 在“计划”  页上，指定以下信息：  

    > [!IMPORTANT]  
    > Windows PE 客户端从 PXE 或启动媒体启动时，客户端不会评估部署计划。 这些计划包括启动、过期，和截止时间。 仅部署从完整的 Windows OS 启动的客户端部署中的计划。 请考虑使用其他方法（例如维护窗口）来控制部署到从 Windows PE 启动的客户端的活动任务序列。  

    - **计划此部署将在何时变为可用**：指定任务序列可以在目标计算机上运行的日期和时间。 选择“UTC”  选项后，任务序列可同时用于多台计算机。 否则，根据每台计算机的本地时间，部署可以在不同时间使用。  

        如果启动时间早于所需时间，则客户端会在启动时间下载任务序列内容。  

    - **计划此部署将在何时过期**：指定任务序列在目标计算机上过期的日期和时间。 选择“UTC”  选项后，任务序列会同时在多台目标计算机上过期。 否则，根据每台计算机的本地时间，部署会在不同时间过期。  

    - **分配计划**：对于“必需”部署，请指定客户端何时运行任务序列  。 你可以添加多个计划。 分配计划可以具有以下配置之一：  

        - 特定日期和时间  
        - 每月、每周，或自定义的定期模式  
        - 尽快  
        - 登录或注销事件  

        > [!NOTE]  
        > 如果为必需部署计划一个启动时间，该时间要早于任务序列可用的日期和时间，Configuration Manager 会在指定的启动时间内下载内容。 即使计划在以后提供任务序列，也会发生此行为。<!--SCCMDocs issue 777-->  

    - **重新运行行为**：指定重新运行任务序列的时间。 选择下列选项之一：  

        - **从不重新运行已部署的程序**：如果客户端之前已运行了任务序列，则它不会重新运行。 即使任务序列最初失败或者任务序列文件已更改，此任务序列也不会重新运行。  

        - **始终重新运行程序**：计划部署时，任务序列始终在客户端上重新运行。 即使已成功运行，任务序列也将重新运行。 如果使用在其中例行更新任务序列的定期部署，则此设置非常有用。  

            > [!IMPORTANT]  
            > 默认情况下选择此选项。 但是，在分配必需部署之前没有任何影响。 用户始终可以重新运行可用的部署。  

        - **如果上次尝试失败则重新运行**：只有在以前未成功运行的情况下，才在计划部署时重新运行任务序列。 此设置对必需部署非常有用。 如果上次运行尝试失败，它会根据分配计划自动尝试重新运行。  

        - **如果上次尝试成功则重新运行**：仅当它上次在客户端成功运行时才重新运行任务序列。 如果你使用在其中例行更新任务序列的定期部署，并且每个更新都要求成功安装以前的更新，则此设置很有用。  

        > [!NOTE]  
        > 用户可以重新运行可用的任务序列部署。 在生产环境中部署可用的任务序列之前，首先测试如果用户多次重新运行任务序列会发生什么情况。  

7. 在“用户体验”  页上，指定下列信息：  

    - **允许用户独立于分配运行程序**：指定用户是否可以在分配计划以外运行所需的部署。 对于可用部署，始终启用此选项。  

    - **显示任务序列进度**：指定 Configuration Manager 客户端是否显示任务序列的进度。  

    - **软件安装**：指定在计划的时间之后是否允许用户在已配置的维护时段之外安装软件。  

    - **系统重启（如果要求完成安装）** ：指定是否允许用户在晚于分配时间的已配置维护时段之外安装软件后重启计算机。  

    - **Windows Embedded 设备的写入筛选器处理**：此设置控制通过写入筛选器启用的 Windows Embedded 设备的安装行为。 选择此选项可在安装截止时间或维护时段提交更改。 选择此选项后需要重启，然后所作更改才能保留在设备上。 否则，应用程序将安装到临时覆盖，并稍后提交。 将任务序列部署到 Windows Embedded 设备时，确保设备是配置了维护时段的集合的成员。  

    - **允许任务序列针对 Internet 上的客户端运行**：指定是否允许在基于 Internet 的客户端上运行任务序列。 此设置不支持需要启动媒体的操作，例如安装操作系统。 请将此选项仅用于一般软件安装或在标准 OS 中执行操作的基于通用脚本的任务序列。  

        - 此设置支持通过云管理网关从 Windows 10 就地升级任务序列部署到基于 Internet 的客户端。 有关详细信息，请参阅[通过 CMG 部署 Windows 10 就地升级](#deploy-windows-10-in-place-upgrade-via-cmg)。  

8. 在“警报”  页上，为此任务序列部署指定所需的警报设置。  

9. 在“分发点”  页上，指定下列信息：  

    - **部署选项**：指定下列选项之一：  

        > [!NOTE]  
        > 如果使用多播部署 OS，则在需要时或者在运行任务序列之前将内容下载到计算机。  

        - **运行中任务序列需要时，从本地下载内容**：指定客户端在任务序列需要内容时从分发点下载内容。 客户端启动任务序列。 当任务序列中的步骤需要内容时，会在步骤运行之前下载它。  

        - **启动任务序列之前本地下载所有内容**：指定客户端在运行任务序列之前从分发点下载所有内容。 如果指定任务序列可用于 PXE 和启动媒体部署，则“部署设置”  页不会显示此选项。  

        - **需要时通过运行任务序列从分发点直接访问内容**：指定客户端从分发点运行内容。 只有当与任务序列关联的所有包都能够使用分发点上的包共享时才可以使用此选项。 要使内容能够使用包共享，请参阅每个包的“属性”  中的“数据访问”  选项卡。  

            > [!IMPORTANT]  
            > 为了最大限度地确保安全，请选择“运行中任务序列需要时，从本地下载内容”或“启动任务序列之前本地下载所有内容”选项   。 选择其中任何一个选项后，Configuration Manager 会对包进行哈希处理，便于确保包的完整性。 选择“需要时通过运行任务序列从分发点直接访问内容”  选项后，Configuration Manager 不会在运行指定的程序之前验证包哈希。 由于站点无法确保包完整性，因此具有管理权限的用户可能会改变或篡改包内容。  

    - **在没有本地分发点可用的情况下使用远程分发点**：指定客户端是否可以使用来自相邻边界组的分发点来下载任务序列所需的内容。  

    - **允许客户端使用默认站点边界组分发点**：指定在无法从当前或相邻边界组中的分发点获得内容时，客户端是否应从站点默认边界组中的分发点下载内容。  

        > [!Note]  
        > 从版本 1810 开始，当设备运行任务序列并且需要获取内容时，它可以使用类似于 Configuration Manager 客户端的边界组行为。 有关更多详细信息，请参阅[对边界组的任务序列支持](../../core/servers/deploy/configure/boundary-groups.md#bkmk_bgr-osd)。<!--1359025-->  

10. 若要保存这些设置以便再次使用，请在“摘要”选项卡上选择“另存为模板”   。 为模板提供名称，然后选择要保存的设置。  

11. 完成向导。  

## <a name="deploy-windows-10-in-place-upgrade-via-cmg"></a>通过 CMG 部署 Windows 10 就地升级

<!-- 1357149 -->
Windows 10 就地升级任务序列支持部署到通过[云管理网关](../../core/clients/manage/cmg/plan-cloud-management-gateway.md) (CMG) 托管的 Internet 客户端。 此功能可让远程用户更轻松地升级到 Windows 10，无需连接 Intranet。

确保就地升级任务序列引用的所有内容均分发到内容已启用的 CMG。 （启用 [CMG 设置](../../core/clients/manage/cmg/setup-cloud-management-gateway.md#settings)：允许 CMG 充当云分发点，并提供 Azure 存储中的内容  。）你还可使用[云分发点](../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md)。 否则设备无法运行任务序列。

在部署升级任务序列时，请使用以下设置：

- 部署“用户体验”选项卡上的“允许任务序列针对 Internet 上的客户端运行”  。  

- 在部署的“分发点”选项卡上选择以下选项之一：

  - 运行中任务序列需要时，从本地下载内容  。 从版本 1910 开始，任务序列引擎可以按需从启用内容的 CMG 或云分发点下载包。 此更改为基于 Internet 的设备的 Windows 10 就地升级部署提供了更大的灵活性。<!--3601238-->

  - 启动任务序列之前在本地下载所有内容  。 在 Configuration Manager 版本 1906 及更低版本中，其他选项（例如“运行任务序列时，如需要则在本地下载内容”）不适用于此方案  。 任务序列引擎无法从云源下载内容。 启动任务序列之前，Configuration Manager 客户端必须从云资源下载内容。 为满足你的要求，必要时仍可在 1910 版本中使用此选项。

- （可选  ）部署“常规”选项卡上的“此任务序列的预下载内容”  。 有关详细信息，请参阅[配置预缓存内容](configure-precache-content.md)。  

> [!NOTE]
> 从软件中心启动任务序列。 此方案不支持 Windows PE、PXE 或任务序列媒体。

## <a name="high-risk-deployments"></a><a name="bkmk_high-risk"></a>高风险部署

部署高风险部署（例如 OS）时，“选择集合”窗口将仅显示满足在站点属性中配置的部署验证设置的自定义集合  。 高风险部署始终局限于自定义集合、你所创建的集合和内置“未知计算机”  集合。 创建高风险部署时，无法选择“所有系统”等内置集合  。 若要查看所含客户端少于配置的最大大小的全部自定义集合，请禁用“隐藏成员数大于站点最低大小配置的集合”  选项。 有关详细信息，请参阅[用于管理高风险部署的设置](../../core/servers/manage/settings-to-manage-high-risk-deployments.md)。  

部署验证设置基于集合的当前成员身份。 部署任务序列后，Configuration Manager 不重新评估高风险部署设置的集合成员身份。  

例如，假设将“默认大小”  设置为 100，将“最大大小”  设置为 1000。 创建高风险部署时，“选择集合”窗口仅显示包含的客户端少于 100 个的集合  。 如果清除“隐藏成员数大于站点最低大小配置的集合”设置，则该窗口显示包含的客户端少于 1000 个的集合  。  

选择包含站点角色的集合时，以下行为适用：  

- 如果集合包含站点系统服务器，而你将部署验证设置配置为阻止具有站点系统服务器的集合，则会出现错误。 你将无法继续创建部署。  

- 如果以下一项标准适用，“部署软件向导”将显示高风险警告。 继续操作需要同意创建高风险部署。 站点会生成审核状态消息。  

  - 如果集合包含站点系统服务器，而你将部署验证设置配置为对具有站点系统服务器的集合发出警告  

  - 如果集合超过默认大小值

  - 如果集合包含服务器  

## <a name="see-also"></a>另请参阅

[管理任务序列来自动执行任务](manage-task-sequences-to-automate-tasks.md)