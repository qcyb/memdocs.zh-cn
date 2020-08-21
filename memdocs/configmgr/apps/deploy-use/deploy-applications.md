---
title: 部署应用程序
titleSuffix: Configuration Manager
description: 创建或模拟将应用程序部署到设备或用户集合
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: how-to
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a4afb066a5f07ff2347bc64b7811c2f09f3bd548
ms.sourcegitcommit: 8fc7f2864c5e3f177e6657b684c5f208d6c2a1b4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2020
ms.locfileid: "88590928"
---
# <a name="deploy-applications-with-configuration-manager"></a>使用 Configuration Manager 部署应用程序

适用范围：  Configuration Manager (Current Branch)

在 Configuration Manager 中，创建或模拟将应用程序部署到设备或用户集合。 此部署向 Configuration Manager 客户端提供有关如何以及何时安装软件的说明。

至少必须为应用程序创建一种部署类型，然后才能部署该应用程序。 有关详细信息，请参阅[创建应用程序](create-applications.md)。

从版本 1906 开始，可以创建一组可以作为单个部署发送到用户或设备集合的应用程序。 有关详细信息，请参阅[创建应用程序组](create-app-groups.md)。

还可以模拟应用程序部署。 该模拟测试部署的适用性，无需安装或卸载应用程序。 模拟部署将评估部署类型的检测方法、要求和依赖关系，然后在“监视”  工作区的“部署”  节点中报告结果。 有关详细信息，请参阅[模拟应用程序部署](simulate-application-deployments.md)。

> [!NOTE]
> 只能模拟所需应用程序的部署，但不能模拟包或软件更新的部署。
>
> 已注册 MDM 的设备不支持模拟部署、用户体验或计划设置。

## <a name="deploy-an-application"></a><a name="bkmk_deploy"></a> 部署应用程序

1. 在 Configuration Manager 控制台中，转到“软件库”工作区，展开“应用程序管理”，然后选择“应用程序”或“应用程序组”节点     。

1. 从列表中选择要部署的应用程序或应用程序组。 在功能区中，选择“部署”。  

> [!NOTE]
> 查看现有部署的属性时，以下各节对应于部署属性窗口的选项卡：  
>
> - [常规](#bkmk_deploy-general)
> - [内容](#bkmk_deploy-content)
> - [部署设置](#bkmk_deploy-settings)
> - [日程安排](#bkmk_deploy-sched)
> - [用户体验](#bkmk_deploy-ux)
> - [警报](#bkmk_deploy-alerts)

### <a name="deployment-general-information"></a><a name="bkmk_deploy-general"></a> 部署常规信息 

在“部署软件”向导的“常规”  页上，指定以下信息：  

- **软件**：此值显示要部署的应用程序。 选择“浏览”，以选择其他应用程序。  

- **集合**：选择“浏览”，以选择此应用程序部署的目标集合。

- **使用与此集合关联的默认分发点组**：将应用程序内容存储在集合默认分发点组上。 如果未将所选集合与分发点组关联，则此选项为灰色。  

- **为依赖关系自动分发内容**：如果应用程序中的任何部署类型具有依赖项，则该站点也会将从属应用程序内容发送到分发点。  

    >[!NOTE]
    > 如果在部署了主应用程序之后更新从属应用程序，则该站点不会自动分发依赖项的任何新内容。

- **备注(可选)** ：可选，为此部署输入描述。

### <a name="deployment-content-options"></a><a name="bkmk_deploy-content"></a> 部署“内容”选项 

在“内容”页上，选择“添加”，以将此应用程序的内容分发到分发点或分发点组。

如果在“常规”页上选择“使用与此集合关联的默认分发点”选项，则会自动填充此选项  。 只有应用程序管理员安全角色的成员可以修改它  。

如果已分发应用程序内容，则它们显示在此处。

### <a name="deployment-settings"></a><a name="bkmk_deploy-settings"></a> 部署设置 

在“部署设置”页上，指定以下信息  ：  

- **操作**：从下拉列表，选择此部署的目的，“安装”或“卸载”应用程序   。  

    > [!NOTE]  
    > 如果在同一设备上创建安装应用的部署以及另一个卸载相同应用的部署，则“安装”部署优先    。  

    创建后，无法更改部署操作。  

- **目的**：从下拉列表中，选择下列选项之一：  

  - **可用**：用户可在软件中心查看该应用程序。 可以按需安装。  

  - **必需**：客户端根据设置的计划自动安装应用。 如果应用程序未隐藏，则用户可跟踪其部署状态。 在截止时间之前，用户还可通过软件中心安装应用程序。  

    > [!NOTE]  
    > 将部署操作设置为“卸载”时，部署目的将自动设置为“必需”   。 无法更改此行为。  

- **允许最终用户尝试修复此应用程序**：从版本 1810 开始，如果使用修复命令行创建应用程序，则启用此选项。 用户会在软件中心内看到一个用于修复  应用程序的选项。<!--1357866-->  

- **将软件预部署到用户的主要设备**：如果部署针对的是用户，则请选择此选项，将应用程序部署到该用户的主要设备。 在该部署运行之前，此设置不需要用户登录。 如果用户必须与安装进行交互，请勿选择此选项。 只有当部署是“必需”时，此选项才可用  。  

- **发送唤醒数据包**：如果部署为“必需”，则 Configuration Manager 在客户端运行部署前，会将唤醒数据包发送到计算机  。 此包可在安装截止时将计算机从休眠中唤醒。 使用此选项前，必须针对“LAN 唤醒”配置计算机和网络。 有关详细信息，请参阅[计划如何唤醒客户端](../../core/clients/deploy/plan/plan-wake-up-clients.md)。  

- **允许客户端使用按流量计费的 Internet 连接在安装截止时间之后下载内容，这可能会导致附加成本**：只有当部署的目的是“必须”  时，此选项才可用。  

- **自动升级此应用程序的任何取代版本**：客户端使用取代应用程序升级应用程序的任何取代版本。

    > [!NOTE]
    > 无论管理员是否批准，此选项都可用。 如果管理员已批准已取代的版本，则无需批准要取代的版本。 批准仅用于新请求，不用于取代升级。<!--515824-->  
    >
    > 对于“可用”  安装目的，可启用或禁用此选项。 <!--1351266-->

#### <a name="approval-settings"></a><a name="bkmk_approval"></a> 批准设置

应用程序批准行为取决于是否启用推荐的可选功能“批准每台设备的用户的应用程序请求”  。

- **管理员必须在设备上批准对此应用程序的请求**：如果启用可选功能，在用户可以在所请求的设备上安装应用程序之前，管理员会批准对该应用程序的任何用户请求。 如果管理员批准请求，则用户只能在该设备上安装应用程序。 用户必须提交另一个请求才能在另一台设备上安装应用程序。 如果部署目的为“必需”或者应用程序部署到了设备集合，则此选项为灰色  。

- **如果用户请求此应用程序，则需要管理员批准**：如果不启用可选功能，在用户可以安装应用程序之前，管理员会批准对该应用程序的任何用户请求。 如果部署目的为“必需”或者应用程序部署到了设备集合，则此选项为灰色  。  

有关详细信息，请参阅[批准应用程序](app-approval.md)。

#### <a name="deployment-properties-deployment-settings"></a>部署属性“部署设置” 

查看部署属性时，如果部署类型技术支持，“部署设置”选项卡上会显示以下选项  ：

**自动关闭在“部署类型属性”对话框的“安装行为”选项卡中指定的任何运行中的可执行文件**。 有关详细信息，请参阅[在安装应用程序之前检查正在运行的可执行文件](#bkmk_exe-check)。

### <a name="deployment-scheduling-settings"></a><a name="bkmk_deploy-sched"></a> 部署“计划”设置 

在“计划”页上，设置何时部署此应用程序或将其提供给客户端设备  。

默认情况下，Configuration Manager 立即向客户端提供部署策略。 如果要创建部署，但希望之后才可用于客户端，请配置“计划可用的应用程序”选项  。 然后选择日期和时间，包括是基于 UTC 还是客户端的本地时间。

如果部署为“必需”，还将指定“安装截止时间”   。 默认情况下，此截止时间越早越好。

例如，需要部署新的业务线应用程序。 所有用户都需要在特定的时间内安装它，但你希望为用户提供尽早选择启用的选项。 还需要确保站点已将内容分发到所有分发点。 计划从今天起五天内提供应用程序。 此计划可提供时间来分发内容并确认其状态。 然后，从今天开始设置每个月的安装截止时间。 在五天内可用时，用户将在软件中心看到应用程序。 如果不执行任何操作，客户端会在安装截止时间内自动安装应用程序。

如果部署的应用程序取代另一个应用程序，可以设置安装截止时间，届时用户会收到新应用程序。 设置“安装截止时间”以升级具有取代应用程序的用户  。

#### <a name="delay-enforcement-with-a-grace-period"></a>在宽限期内延迟执行

可能会希望为用户提供更多时间（超出所设置的任何截止时间）来安装所需的应用程序  。 当计算机长时间关闭并需要安装许多应用程序时，通常需要此行为。 例如，用户休假回来时，由于客户端安装的部署已过期，因此需要等待很长的时间。 若要帮助解决此问题，请定义强制的宽限期。

- 首先，在客户端设置中，通过“部署截止日期后强制的宽限期（小时）”属性来配置此宽限期  。 有关详细信息，请参阅[计算机代理](../../core/clients/deploy/about-client-settings.md#computer-agent)组。 指定一个介于 1 和 120 之间的值   。  

- 在所需应用程序部署的“计划”页上，启用“根据用户首选项延迟此部署的强制执行，延迟时间以客户端设置中定义的宽限期为依据”选项   。 强制宽限期适用于启用此选项的所有部署，并针对部署了客户端设置的设备。

在截止时间之后，客户端将在用户配置的第一个非业务窗口中安装应用程序，用户以该宽限期为依据配置了该窗口。 但是，用户仍可打开软件中心并在任何时间安装该应用程序。 一旦过了宽限期，对于未完成的部署，强制将恢复为正常行为。

:::image type="content" source="media/grace-period.svg" alt-text="宽限期时间线图":::

<!-- SCCMDocs issue #1599 -->

> [!NOTE]
> 大多数情况下，此功能可解决用户外出时设备电源关闭的情况。 从技术上讲，宽限期从客户端在部署截止时间后获取策略开始。 如果停止 Configuration Manager 客户端服务 (CcmExec)，然后在部署截止时间后的某个时间重新启动该服务，则会发生相同的行为。

### <a name="deployment-user-experience-settings"></a><a name="bkmk_deploy-ux"></a> 部署“用户体验”设置 

在“用户体验”页上，指定有关用户如何与应用程序安装交互的信息  。

- **用户通知**：指定是否在已配置的可用时间期间在软件中心上显示通知。 此设置还控制是否通知客户端计算机上的用户。 对于可用部署，无法选择“在软件中心和所有通知中隐藏”选项  。  

  - **需要更改软件时，向用户显示一个对话框窗口而不是 toast 通知**<!--3555947-->：从版本 1902 开始，选择此选项可使用户体验更具侵入性。 它仅适用于所需的部署。 有关详细信息，请参阅[为软件中心制定计划](../plan-design/plan-for-software-center.md#bkmk_impact)。

- “软件安装”和“系统重启”   ：只能为所需部署配置这些设置。 指定部署达到任何已定义的维护时段外的截止时间时的行为。 有关维护时段的详细信息，请参阅[如何使用维护时段](../../core/clients/manage/collections/use-maintenance-windows.md)。  

- **Windows Embedded 设备的写入筛选器处理**：此设置控制通过写入筛选器启用的 Windows Embedded 设备的安装行为。 选择此选项可在安装截止时间或维护时段提交更改。 选择此选项后需要重启，然后所作更改才能保留在设备上。 否则，应用程序将安装到临时覆盖，并稍后提交。  

  - 将软件更新部署到 Windows Embedded 设备时，请确保设备是配置了维护时段的集合的成员。 有关维护时段和 Windows Embedded 设备的详细信息，请参阅[创建 Windows Embedded 应用程序](../get-started/creating-windows-embedded-applications.md)。  

### <a name="deployment-alerts"></a><a name="bkmk_deploy-alerts"></a> 部署“警报” 

在“警报”页面上，配置 Configuration Manager 为此部署生成警报的方式  。 如果还在使用 System Center Operations Manager，也请配置其警报。 只能为所需部署配置一些警报。

## <a name="create-a-phased-deployment"></a><a name="bkmk_phased"></a> 创建分阶段部署

<!--1358147-->
通过分阶段部署，可以根据可自定义条件和组进行协调安排，有序推出软件。 例如，将应用程序部署到试点集合，然后根据成功条件自动继续推出。

有关详细信息，请参阅下列文章：  

- [创建分阶段部署](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/mem/configmgr/apps/toc.json&bc=/mem/configmgr/apps/breadcrumb/toc.json)  

- [管理和监视分阶段部署](../../osd/deploy-use/manage-monitor-phased-deployments.md?toc=/mem/configmgr/apps/toc.json&bc=/mem/configmgr/apps/breadcrumb/toc.json)  

## <a name="delete-a-deployment"></a><a name="bkmk_delete"></a> 删除部署

1. 在 Configuration Manager 控制台中，转到“软件库”工作区，展开“应用程序管理”，然后选择“应用程序”或“应用程序组”节点     。  

1. 选择其中包含要删除的部署的应用程序或应用程序组。  

1. 切换到细节窗格的“部署”选项卡，然后选择部署  。  

1. 在功能区的“部署”组的“部署”选项卡上，选择“删除”。  

删除应用程序部署时，不会删除客户端已安装的应用程序的任何实例。 要删除这些应用程序，请将应用程序部署到计算机以“卸载”  。 如果你删除了应用程序部署，应用程序就不会再显示在软件中心内。 当你从部署的目标集合中删除资源时，也会发生相同的行为。

## <a name="user-notifications-for-required-deployments"></a><a name="bkmk_notify"></a> 所需部署的用户通知

用户接收所需软件并选择“推迟并提醒我”设置时，他们可以从以下选项中选择  ：  

- **以后**：指定根据客户端设置中配置的通知设置安排通知。  

- **固定时间**：指定在选定时间之后再次显示通知。 例如，如果选择 30 分钟，则通知在 30 分钟后再次显示。  

:::image type="content" source="media/ComputerAgentSettings.png" alt-text="默认客户端设置中的计算机代理组":::

最长推迟时间始终基于沿部署时间轴推移的客户端设置中配置的通知值。 例如：  

- 在“计算机代理”页上，将“部署截止时间大于 24 小时，每(小时)提醒用户”设置配置为 10 小时   。  

- 客户端将在部署截止时间前 24 小时之前显示通知对话框。  

- 该对话框显示推迟选项，但不会超过 10 小时。  

- 随着部署截止时间的临近，该对话框显示更少选项。 这些选项会与部署时间轴的每个组件的相关客户端代理设置相一致。  

对于高风险部署（如用于部署 OS 的任务序列），用户通知体验的干扰性更强。 这不是临时性的任务栏通知，每次通知需要维护关键软件时，将显示如下所示的对话框：

:::image type="content" source="media/client-toast-notification.png" alt-text="所需软件对话框会通知你关键的软件维护":::

## <a name="check-for-running-executable-files"></a><a name="bkmk_exe-check"></a> 检查运行的可执行文件

配置部署以检查某些可执行文件是否正在客户端上运行。 使用此选项检查可能中断应用程序安装的进程。 如果其中一个可执行文件正在客户端上运行，则客户端会阻止部署类型的安装。 在客户端安装部署类型之前，用户必须关闭正在运行的可执行文件。 对于所需部署，客户端可自动关闭正在运行的可执行文件。

1. 打开部署类型的“属性”。

1. 切换到“安装行为”选项卡，然后单击“添加”。

1. 在“添加可执行文件”窗口中，输入目标可执行文件的名称。 或者，可以为应用程序输入友好名称，以帮助在列表中识别它。

1. 选择“确定”，以保存和关闭部署类型的“属性”窗口。

1. 部署应用程序时，选择“自动关闭在‘部署类型属性’对话框的‘安装行为’选项卡中指定的任何运行中的可执行文件”选项  。 此选项位于部署属性的“部署设置”选项卡上  。  

> [!NOTE]
> 如果将应用程序配置为检查运行中的可执行文件，并将其纳入[安装应用程序](../../osd/understand/task-sequence-steps.md#BKMK_InstallApplication)任务序列步骤，则该任务序列将无法安装它。 如果未将此任务序列步骤配置为“出现错误时继续运行”，则整个任务序列将失败。

### <a name="client-behaviors-and-user-notifications"></a>客户端行为和用户通知

客户端收到部署后，将应用以下行为：  

- 如果应用程序已部署为“可用”，用户尝试安装它时，客户端会提示其先关闭指定的正在运行的可执行文件，然后才能继续安装  。  

- 如果应用程序已部署为“必需”，且指定“自动关闭在‘部署类型属性’对话框中的‘安装行为’选项卡中指定的任何正在运行的可执行文件”，则客户端显示通知   。 它通知用户达到应用程序安装截止时间时，指定的可执行文件自动关闭。  

  - 计划客户端设置的“计算机代理”组中的这些对话  。 有关详细信息，请参阅[计算机代理](../../core/clients/deploy/about-client-settings.md#computer-agent)。  

  - 如果不希望该用户看到这些消息，请选择部署属性的“用户体验”选项卡上的“在软件中心和所有通知中隐藏”选项   。 有关详细信息，请参阅[部署用户体验设置](#bkmk_deploy-ux)。  

- 如果应用程序已部署为“必需”，且未指定“自动关闭在‘部署类型属性’对话框中的‘安装行为’选项卡中指定的任何正在运行的可执行文件”，如果正在运行一个或多个指定的应用程序，则应用安装失败   。  

## <a name="deploy-user-available-applications"></a>部署用户可用的应用程序

当你将应用程序作为“可用”部署到用户集合时，用户可以浏览软件中心，并安装所需的应用。 对于本地域加入客户端，软件中心使用用户的域凭据从管理点获取可用应用程序的列表。

对于基于 Internet 和/或已建立 Azure Active Directory (Azure AD) 联接的客户端，还有一些额外的要求。

### <a name="azure-ad-joined-devices"></a>已加入 Azure AD 的设备
<!-- 1322613 -->

如果你将应用程序作为“可用”部署给用户，用户可以在 Azure AD 设备上通过软件中心浏览和安装它们。 配置以下先决条件来启用此方案：

- 在管理点上启用 HTTPS  

- 将站点与 [Azure AD](../../core/servers/deploy/configure/azure-services-wizard.md) 集成以实现**云管理**  

  - 配置 [Azure AD 用户发现](../../core/servers/deploy/configure/configure-discovery-methods.md#azureaadisc)  

- 将应用程序以可用方式部署到 Azure AD 的用户集合中  

- 在[计算机代理](../../core/clients/deploy/about-client-settings.md#computer-agent)组中启用客户端设置“使用新的软件中心”   

- 客户端 OS 必须是 Windows 10，并加入到 Azure AD。 已加入纯云域或混合 Azure AD。  

- 若要支持基于 Internet 的客户端：  

  - [云管理网关](../../core/clients/manage/cmg/plan-cloud-management-gateway.md) (CMG)

  - 将任何应用程序内容分发到已启用内容的 CMG 或[云分发点](../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md)  

  - 启用客户端设置：[客户端策略](../../core/clients/deploy/about-client-settings.md#client-policy)组中的“从 Internet 客户端启用用户策略请求”   

- 支持 Intranet 上的客户端：  

  - 将已启用内容的 CMG 或云分发点添加到客户端使用的边界组  

  - 客户端必须解析已启用 HTTPS 的管理点的完全限定的域名 (FQDN)  

  > [!NOTE]
  > 对于在 Intranet 上检测到、但通过云管理网关 (CMG) 进行通信的客户端，在 Configuration Manager 版本 2002 及更低版本中，软件中心使用 Windows 身份验证。 过去无法尝试通过 CMG 获取用户可用的应用的列表。 自版本 2006 起，它对已建立 Azure AD 联接的设备使用 Azure Active Directory (Azure AD) 标识。 这些设备可以是云加入或混合加入。<!--6935376-->

## <a name="next-steps"></a>后续步骤

- [监视应用程序](monitor-applications-from-the-console.md)
- [排除应用程序部署故障](troubleshoot-application-deployment.md)
- [应用程序的管理任务](management-tasks-applications.md)
- [软件中心用户指导](../../core/understand/software-center.md)
