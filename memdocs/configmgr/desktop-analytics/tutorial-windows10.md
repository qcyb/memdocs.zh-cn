---
title: 教程 - 部署 Windows 10
titleSuffix: Configuration Manager
description: 有关使用桌面分析和 Configuration Manager 将 Windows 10 部署到试点组的教程。
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: tutorial
ms.assetid: 3e82cd96-0ce0-474a-a597-d65fceadc95a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 15cf7f3621f25a82f0e16d5275369ec93225bbf7
ms.sourcegitcommit: 034226b5a60de49a75c7b54e856814f81c03a112
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "86422828"
---
# <a name="tutorial-deploy-windows-10-to-pilot"></a>教程：将 Windows 10 部署到试点

本教程使用桌面分析和 Configuration Manager 将 Windows 10 部署到试点组。 其中重点介绍云服务的集成，以提供使用本地产品部署 Windows 的见解。 使用桌面分析来确定要用于试点组的最佳设备。 然后使用 Configuration Manager 获取当前的 Windows。

在本教程中，你将了解如何：  

> [!div class="checklist"]  
> * 在 Azure 门户中设置桌面分析  
> * 连接 Configuration Manager 并配置设备设置  
> * 为 Windows 10 创建桌面分析部署计划  
> * 使用 Configuration Manager 将 Windows 10 部署到试点组  

如果没有 Azure 订阅，请在开始之前创建一个[免费帐户](https://azure.microsoft.com/free)。 正确配置后，使用桌面分析不会产生任何 Azure 费用。

桌面分析使用 Azure 订阅中的 Log Analytics 工作区。 工作区实质上是包括帐户信息以及该帐户的简单配置信息的容器。 有关详细信息，请参阅[管理工作区](https://docs.microsoft.com/azure/log-analytics/log-analytics-manage-access?toc=/azure/azure-monitor/toc.json)。



## <a name="prerequisites"></a>必备条件

在开始本教程之前，请确保符合以下先决条件：  

- 有效的 Azure 订阅，具有[全局管理员](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#company-administrator-permissions)权限。  

    有关详细信息，请参阅[桌面分析先决条件](overview.md#prerequisites)。

- 包含更新汇总 (4500571) 的 Configuration Manager 版本 1902 或更高版本，具有“完全权限管理员”角色  

- 最新版的 Windows 10 的安装介质

- 至少一个具有以下配置的 Windows 10 设备：  

    - Windows 10 版本 1709 或更高版本，但低于你计划使用的安装介质版本

    - 最新的 Windows 10 累积质量更新  

    - 包含更新汇总 (4500571) 的 Configuration Manager 客户端版本 1902 或更高版本  

- 业务审批，在试点设备上将 Windows 诊断数据级别配置为“增强(受限)”  

    有关详细信息，请参阅[桌面分析隐私](privacy.md)。

- 从设备到以下 Internet 终结点的网络连接：

    - `https://v10c.events.data.microsoft.com`  
    - `https://settings-win.data.microsoft.com`  
    - `http://adl.windows.com`  
    - `https://watson.telemetry.microsoft.com`  
    - `https://umwatsonc.events.data.microsoft.com`  
    - `https://ceuswatcab01.blob.core.windows.net`  
    - `https://ceuswatcab02.blob.core.windows.net`  
    - `https://eaus2watcab01.blob.core.windows.net`  
    - `https://eaus2watcab02.blob.core.windows.net`  
    - `https://weus2watcab01.blob.core.windows.net`  
    - `https://weus2watcab02.blob.core.windows.net`  
    - `https://kmwatsonc.events.data.microsoft.com`  
    - `https://oca.telemetry.microsoft.com`  
    - `https://login.live.com`  
    - `https://graph.windows.net`（仅限在 Configuration Manager 服务器角色上）
    - `https://*.manage.microsoft.com`（仅限在 Configuration Manager 服务器角色上）

    有关详细信息，请参阅[如何启用桌面分析的数据共享](enable-data-sharing.md#endpoints)。  

> [!Important]  
> 这些先决条件适用于本教程。 有关 Configuration Manager 的桌面分析一般先决条件的详细信息，请参阅[先决条件](overview.md#prerequisites)。  



## <a name="set-up-desktop-analytics"></a>设置桌面分析

使用此过程登录桌面分析并在订阅中对其进行配置。 此过程是为组织设置桌面分析的一次性过程。  

1. 以具有“全局管理员”权限的用户身份，在 Microsoft 365 设备管理中打开[桌面分析门户](https://aka.ms/desktopanalytics)。 选择“启动”。  

2. 在“接受服务协议”页上，查看服务协议，然后选择“接受”。  

3. 在“确认订阅”页上，必需的合格许可证列表适用于桌面分析的 Windows 设备运行状况功能。 选择“下一步”继续操作。  

4. 在“授予用户访问权限”页上：

    - **允许桌面分析代表你管理目录角色**：桌面分析自动向“工作区所有者”分配“桌面分析管理员”角色 。 如果这些组已是“全局管理员”，则不会发生任何更改。  

        如果未选择此选项，桌面分析仍会将用户添加为安全组的成员。 “全局管理员”需要为用户手动分配“桌面分析管理员”角色。  

        有关在 Azure Active Directory 中分配管理员角色权限以及分配给“桌面分析管理员”的权限的详细信息，请参阅 [Azure Active Directory 中的管理员角色权限](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles)。  

    - 桌面分析在 Azure Active Directory 中预先配置“工作区所有者”安全组，以创建和管理工作区和部署计划。 

        若要将用户添加到组，请在“输入用户名或电子邮件地址”部分键入其名称或电子邮件地址。 完成后，选择“下一步”。

5. 在“设置工作区”页面上：  

    > [!Note]  
    > 若要完成此步骤，用户需要“工作区所有者”权限以及对 Azure 订阅和资源组的其他访问权限。 有关详细信息，请参阅[先决条件](overview.md#prerequisites)。  

    - 选择 Azure 订阅。  

    - 若要将现有工作区用于桌面分析，请选中它，然后继续下一步。  

    - 若要创建桌面分析工作区，请选择“添加工作区”。  

        1. 输入工作区名称。  

        2. 选择下拉列表以“选择此工作区的 Azure 订阅名称”，然后选择此工作区的 Azure 订阅。  

        3. “新建资源组”或“使用现有” 。  

        4. 从列表中选择“区域”，然后选择“添加”。  

6. 选择新的或现有工作区，然后选择“设置为桌面分析工作区”。  然后，在“确认并授予访问权限”对话框中选择“继续” 。  

7. 在新浏览器选项卡中，选取一个用于登录的帐户。 选择“代表组织同意”，然后选择“接受”。  


    > [!Note]  
    > 此同意是为 MALogAnalyticsReader 应用程序分配工作区的 Log Analytics 阅读者角色。 桌面分析需要此应用程序角色。 有关详细信息，请参阅 [MALogAnalyticsReader 应用程序角色](troubleshooting.md#bkmk_MALogAnalyticsReader)。  

8. 返回到“设置工作区”页面，选择“下一步” 。  

9. 在“最后几步”页上，选择“转到桌面分析”。 Azure 门户显示桌面分析主页。  



## <a name="connect-configuration-manager"></a>连接 Configuration Manager

使用此过程更新 Configuration Manager、连接到桌面分析并配置设备设置。 此过程是将层次结构连接到云服务的一次性过程。  

### <a name="update-configuration-manager"></a>更新 Configuration Manager

安装 Configuration Manager 版本 1902 更新汇总 (4500571)，以支持与桌面分析的集成。 有关此更新的详细信息，请参阅 [Configuration Manager Current Branch（版本 1902）更新汇总](https://support.microsoft.com/help/4500571)。

1. 使用版本 1902 的更新汇总更新站点。 有关详细信息，请参阅[安装控制台内部更新](../core/servers/manage/install-in-console-updates.md)。  

2. 更新客户端。 若要简化此过程，请考虑使用自动客户端升级。 有关详细信息，请参阅[升级客户端](../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade)。  


### <a name="connect-to-the-service"></a>连接到服务

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“Azure 服务”节点  。 在功能区中选择“配置 Azure 服务”。  

2. 在 Azure 服务向导的“Azure 服务”页上，配置以下设置：  

    - 指定 Configuration Manager 中的对象名称  

    - 指定可选说明以帮助标识服务  

    - 从可用服务列表中选择“桌面分析”  
  
   选择“下一步”。  

3. 在“应用”页上，选择相应的“Azure 环境”。 然后选择“浏览”以查找 Web 应用。

4. 选择“创建”，为桌面分析连接轻松添加 Azure AD 应用。

5. 在“创建服务器应用程序”窗口中配置以下设置：  

    - **应用程序名称**：Azure AD 中应用的易记名称。

    - **主页 URL**：Configuration Manager 不使用此值，但是 Azure AD 需要它。 默认情况下，此值为 `https://ConfigMgrService`。  

    - **应用 ID URI**：此值在 Azure AD 租户中必须是唯一的。 它在 Configuration Manager 客户端用于请求访问服务的访问令牌中。 默认情况下，此值为 `https://ConfigMgrService`。  

    - **密钥有效期**：从下拉列表中选择“1 年”或“2 年” 。 默认值为一年。  

    选择“登录”。 成功完成 Azure 身份验证后，该页面会显示 Azure AD 租户名称以供参考。

    > [!Note]  
    > 以“全局管理员”身份完成此步骤。Configuration Manager 不保存这些凭据。 此角色不需要 Configuration Manager 中的权限，其帐户也不需要与运行 Azure 服务向导的帐户相同。  

    选择“确定”以在 Azure AD 中创建 Web 应用，并关闭“创建服务器应用程序”对话框。 在“服务器应用”对话框中，选择“确定”。 然后，在 Azure 服务向导的“应用”页上选择“下一步”。  

6. 在“诊断数据”页上配置下列设置：  

    - **商业 ID**：此值应自动填充你的组织 ID。  

    - **Windows 10 诊断数据级别**：至少选择“增强(受限)”。  

    - **允许诊断数据中含有设备名称**：选择“启用”  
  
   选择“下一步”。 “可用功能”页显示了根据上一页的诊断数据设置提供的桌面分析功能。 选择“下一步”。  

7. 在“集合”页上，配置下列设置：  

    - **显示名称**：桌面分析门户使用此名称显示此 Configuration Manager 连接。 使用它来区分不同的层次结构。 例如，“测试实验室”或“生产”。  

    - **目标集合**：此集合包括 Configuration Manager 使用你的商业 ID 和诊断数据设置配置的所有设备。 它是 Configuration Manager 连接到桌面分析服务的完整设备集。  

    - **目标集合中的设备使用经用户身份验证的代理进行出站通信**：默认情况下，此值为“否”。 如果你的环境需要，请设置为“是”。  

    - **选择要与桌面分析同步的特定集合**：选择“添加”以包括其他集合。 这些集合可在桌面分析门户中用于按照部署计划分组。 确保包括试点和试点排除集合。  

        这些集合在其成员身份更改时会继续同步。 例如，你的部署计划使用具有 Windows 7 成员身份规则的集合。 当这些设备升级到 Windows 10，在 Configuration Manager 评估集合成员身份时，这些设备将退出集合和部署计划。  

8. 完成向导。  

Configuration Manager 创建设置策略以配置目标集合中的设备。 此策略包括允许设备向 Microsoft 发送数据的诊断数据设置。 默认情况下，客户端每小时更新一次策略。 接收到新设置后，可能需要几个小时才能在桌面分析中使用这些数据。

> [!Note]  
> 有关这些设置的详细信息，请参阅 [Windows 设置](enroll-devices.md#windows-settings)。  

监视桌面分析的设备配置。 在 Configuration Manager 控制台中，转到“软件库”工作区，展开“桌面分析服务”节点，然后选择“连接运行状况”仪表板  。  

Configuration Manager 会在创建连接的 60 分钟内同步集合。 在桌面分析门户中，转到“全局试点”，并查看 Configuration Manager 设备集合。 门户的其余部分可能需要 2 到 3 天才能显示完整数据。 有关详细信息，请参阅[数据延迟](troubleshooting.md#data-latency)。

## <a name="create-a-desktop-analytics-deployment-plan"></a>创建桌面分析部署计划

使用此过程在桌面分析中创建部署计划。

1. 打开[桌面分析门户](https://aka.ms/desktopanalytics)。 使用至少具有“工作区参与者”权限的凭据。  

2. 在“管理”组中选择“部署计划”。  

3. 在“部署计划”窗格中，选择“创建”。  

4. 在“创建部署计划”窗格中，配置下列设置：  

    - **名称**：部署计划的唯一名称，例如 `Windows 10 pilot`  

    - **产品和版本**：选择要部署的 Windows 10 版本。 Microsoft 建议创建使用最新版本的部署计划。

    - **设备组**：从 Configuration Manager 选项卡中选择一个或多个组，然后选择“设置为目标组”。 这些组是从 Configuration Manager 同步的集合。  

    - **就绪规则**：这些规则可帮助确定哪些设备符合升级条件。 选择“Windows OS”并配置以下设置：  

        - **我的计算机自动从 Windows 更新获取驱动程序**：默认设置为“关闭”，在使用 Configuration Manager 进行部署时建议使用此设置。  

        - **为应用定义低安装计数阈值**：默认设置为 `2%`。 低于此阈值的应用会自动设置为“低安装计数”。 在试点期间，桌面分析不会验证这些加载项。  

            如果应用安装在超过此阈值的计算机上，则部署计划会将应用标记为“值得注意”。 然后可以决定在试点阶段测试的重要性。  

    - **完成日期**：选择将 Windows 完全部署到所有目标设备的截止日期。  

5. 选择“创建”。 新计划在进行处理时显示在部署计划的列表中。 若要加快处理过程，可请求按需进行数据刷新。 有关详细信息，请参阅[桌面分析常见问题](faq.md#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal)。

6. 通过选择部署计划的名称将其打开。  

7. 在部署计划菜单上的“准备”组中，选择“确定重要性”。  

    1. 在“应用”选项卡上，选择仅显示“未评审”资产。  

    2. 选择每个应用，然后选择“编辑”。 可以选择同时编辑多个应用。  

    3. 从“重要性”列表中选择一个重要性级别。 如果希望桌面分析在试点期间验证应用，请选择“严重”或“重要”。 它不会验证标记为“不重要”的应用。 分配重要性级别时，评估其[兼容性](compat-assessment.md)和其他计划见解。  

        分配重要性级别时，还可以选择升级决策。  

    4. 完成后选择“保存”。  

8. 在部署计划菜单上的“准备”组中，选择“确定试点”。  

    1. 查看针对试点推荐的设备。  

    2. 选择每个设备，并选择“添加到试点”。 如果不同意此建议，请选择“替换”。  

        有关桌面分析如何进行这些建议的详细信息，请选择“确定试点”窗格右上角的信息图标。



## <a name="deploy-windows-10-in-configuration-manager"></a>在 Configuration Manager 中部署 Windows 10

使用此过程在 Configuration Manager 中将 Windows 10 部署到试点组。

- 如果还没有，请先[创建适用于 Windows 10 的 OS 升级包](#bkmk_create-package)  

- 如果还没有，请[创建适用于 Windows 10 的 OS 任务序列](#bkmk_create-ts)  

- 使用桌面分析部署计划[部署任务序列](#bkmk_deploy-ts)  

- 从目标设备上的软件中心[安装任务序列](#bkmk_install-ts)  

<!-- 
- [Monitor](#bkmk_monitor-ts) status in Configuration Manager  
 -->

### <a name="create-an-os-upgrade-package-for-windows-10"></a><a name="bkmk_create-package"></a> 为 Windows 10 创建 OS 升级包

1. 在 Configuration Manager 控制台中，转到“软件库”工作区，展开“操作系统”，然后选择“操作系统升级包”节点  。  

2. 在功能区的“主页”选项卡上的“创建”组中，选择“添加操作系统升级包”  。 此操作将启动“添加操作系统升级向导”。  

3. 在“数据源”页上，指定 OS 升级包的安装源文件的网络路径 。 例如，`\\server\share\path`。  

    > [!NOTE]  
    > 安装源文件包含 setup.exe 和其他文件以及用于安装 OS 的文件夹。  

4. 在“常规”页上，指定 OS 升级包的唯一名称 。  

5. 完成“添加操作系统升级程序包向导”。  

#### <a name="distribute-content"></a>分发内容

接下来，将 OS 升级包分发到分发点。  

1. 在列表中选择 OS 升级包。 在功能区的“主页”选项卡上，在“部署”组中，选择“分发内容”。 分发内容向导将打开。  

2. 在“常规”页上，验证所列内容是否为要分发的内容，然后选择“下一步”。  

3. 在“内容目标”页上，选择“添加”，然后选择“分发点”  。 选择现有分发点，然后选择“确定”。 添加完内容目标时，选择“下一步”。  

4. 完成“分发内容向导”。  


### <a name="create-an-os-upgrade-task-sequence-for-windows-10"></a><a name="bkmk_create-ts"></a> 为 Windows 10 创建 OS 升级任务序列

1. 在 Configuration Manager 控制台中，转到“软件库”工作区，展开“操作系统”，然后选择“任务序列”  。  

2. 在功能区的“主页”选项卡上的“创建”组中，选择“创建任务序列”  。  

3. 在创建任务序列向导的“创建新的任务序列”页上，选择“通过升级包升级操作系统”，然后选择“下一步”  。  

4. 在“任务序列信息”页上，指定用于标识任务序列的任务序列名称。  

5. 在“升级 Windows 操作系统”页上，指定以下设置，然后选择“下一步” ：  

    - **升级包**：指定包含 OS 升级源文件的升级包。  

    - **版本索引**：如果包中有多个 OS 版本索引可用，请选择所需的版本索引。 默认情况下，该向导会选择第一个索引。  

    - **产品密钥**：指定要安装的 OS 的 Windows 产品密钥。 请指定编码的批量许可证密钥或标准产品密钥。 如果使用标准产品密钥，请用短划线 (-) 将每五个字符分隔为一组。 例如：XXXXX-XXXXX-XXXXX-XXXXX-XXXXX。 在对批量许可证版本进行升级时，则可能不需要产品密钥。  

        > [!Note]  
        > 此产品密钥可以是多次激活密钥 (MAK) 或通用批量授权密钥 (GVLK)。 GVLK 也叫密钥管理服务 (KMS) 客户端安装密钥。 有关详细信息，请参阅[规划批量激活](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client)。 如需 KMS 客户端设置密钥的列表，请参阅 Windows Server 激活指南的[附录 A](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys)。

6. 在“包括更新”页上，选择“下一步”以不安装任何软件更新。  

7. 在“安装应用程序”页上，选择“下一步”以不安装任何应用程序。

8. 完成“创建任务序列向导”。  


### <a name="deploy-the-task-sequence-using-the-desktop-analytics-deployment-plan"></a><a name="bkmk_deploy-ts"></a> 使用桌面分析部署计划部署任务序列

1. 在 Configuration Manager 控制台中，转到“软件库”，展开“桌面分析服务”，然后选择“部署计划”节点  。  

2. 选择 Windows 10 试点部署计划，然后在功能区中选择“部署计划详细信息”。  

3. 在“试点状态”磁贴中，从下拉列表中选择“任务序列”，然后选择“部署”。  

4. 在“部署软件向导”的“常规”页上，选择“软件”字段旁边的“浏览”。 选择 Windows 10 就地升级任务序列，然后选择“下一步”。  

    > [!Note]  
    > 通过桌面分析集成，Configuration Manager 会自动为部署计划创建试点和生产集合。 在你可以使用它们之前，这些集合可能要花费一些时间进行同步。 有关详细信息，请参阅[排除故障 - 数据延迟](troubleshooting.md#data-latency)。<!-- 4984639 -->
    >
    > 此集合是为桌面分析部署计划设备保留的。 不支持手动更改此集合。<!-- 3866460, SCCMDocs-pr 3544 -->  

5. 在“内容”页上，选择“添加”，然后选择“分发点”  。 选择用于托管安装内容的可用分发点，然后选择“确定”。 然后选择“下一步”。  

6. 在“部署设置”页上，选择“下一步”以接受默认设置。 （可用安装。）  

7. 在“计划”页上，选择“下一步”以接受默认设置。 （尽快提供。）  

8. 在“用户体验”页上，选择“下一步”以接受默认设置。 （在软件中心显示，且仅显示计算机重新启动通知。）  

9. 在“警报”页上，选择“下一步”以接受默认设置。  

10. 完成向导。  


### <a name="install-the-task-sequence-from-software-center"></a><a name="bkmk_install-ts"></a> 从软件中心安装任务序列

1. 登录到属于试点部署计划的成员的设备。  

2. 打开软件中心并安装适用于 Windows 10 的可用操作系统。  


<!--
### <a name="bkmk_monitor-app"></a> Monitor status in Configuration Manager
-->


## <a name="next-steps"></a>后续步骤

转到下一篇文章，以详细了解桌面分析桌面计划。
> [!div class="nextstepaction"]  
> [部署计划](about-deployment-plans.md)
