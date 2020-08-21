---
title: Configuration Manager 控制台变更和提示
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 控制台变更和使用提示。
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: 2162d67d-31a9-45b2-bb9e-835f3ac6e6fe
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a0a434f013da48d660efa78f5e2cdca6ced0826d
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700712"
---
# <a name="configuration-manager-console-changes-and-tips"></a>Configuration Manager 控制台变更和提示

适用范围：  Configuration Manager (Current Branch)

请参阅以下信息来了解 Configuration Manager 控制台变更和使用提示：

## <a name="general-tips"></a>一般技巧

### <a name="improvements-to-console-search"></a><a name="bkmk_search"></a> 对控制台搜索的改进
<!--4640570-->
（从版本 1910 中引入） 

- 可以使用“驱动程序包”和“查询”节点中的“所有子文件夹”搜索选项    。<!--2841181,5424892--> 从版本 2002 开始，还可以从“配置项目”和“配置基线”节点使用此选项   。<!--5891241-->

- 如果搜索返回的结果超过 1,000 个，请选择通知栏上的“确定”按钮以查看更多结果  。<!--4640570-->

    ![搜索结果过多的通知栏的屏幕截图](./media/4640570-search-too-many-results.png)

    > [!TIP]
    > 搜索结果的默认限制为 1,000 个。 可以更改此默认值。 在 Configuration Manager 控制台中，转到功能区的“搜索”选项卡  。 在“选项”组中，选择“搜索设置”   。 更改“搜索结果”值  。 越多搜索结果可能需要越长时间才能显示。
    >
    > 默认情况下，其上限为 100,000 个。 要更改此限制，请在以下注册表项中设置 DWORD 值 QueryResultCountMaximum  ：
    >
    > `HKEY_CURRENT_USER\Software\Microsoft\ConfigMgr10\AdminUI`
    >
    > 控制台中的设置对应于相同注册表项中的 QueryResultCountLimit 值  。 管理员可以在 HKLM 配置单元中为设备的所有用户配置这些值。 HKCU 值会替代 HKLM 设置。

### <a name="role-based-administration-for-folders"></a>文件夹的基于角色的管理
<!--3600867-->
（从版本 1906 中引入） 

可以在文件夹上设置安全作用域。 如果有权访问文件夹中的对象，但无权访问文件夹，则无法查看对象。 同样，如果有权访问文件夹，但无权访问该文件夹中的对象，则无法查看对象。 右键单击文件夹，选择“设置安全作用域”  ，然后选择要应用的安全作用域。

### <a name="views-sort-by-integer-values"></a>视图按整数值排序

（从版本 1902 中引入） 

我们改进了各个视图对数据排序的方式。 例如，在“监视”工作区的“部署”节点中，以下列现在按数字而不是字符串值排序   ：  

- 错误数
- 正在进行的数量
- 其他数量
- 成功数
- 未知数量  

### <a name="move-the-warning-for-a-large-number-of-results"></a>移动警告以获得大量结果

（从版本 1902 中引入） 

在控制台中选择返回 1,000 个以上结果的节点时，Configuration Manager 将显示以下警告：

> Configuration Manager 返回了大量结果。 可使用搜索缩小结果范围。 或者，单击此处可查看最多 100000 个结果。

此警告和搜索字段之间现在有额外的空白区域。 此次移动有助于防止无意中选择该警告，从而显示更多结果。

### <a name="send-feedback"></a>发送反馈

（从版本 1806 中引入） 
<!--1357542-->

从控制台提交产品反馈。  

- **发送笑脸**：就喜欢的内容发送反馈  

- **发送皱眉表情**：就不喜欢的内容发送反馈  

- **发送建议**：转到 UserVoice 分享你的观点  

有关详细信息，请参阅[产品反馈](../../understand/find-help.md#BKMK_1806Feedback)。


## <a name="assets-and-compliance-workspace"></a>资产和符合性工作区

### <a name="real-time-actions-from-device-lists"></a>设备列表中的实时操作
<!--4616810-->
（从版本 1906 中引入） 

有多种方法可以在“资产和符合性”工作区中的“设备”节点下显示设备列表   。

- 在“资产和符合性”工作区中，选择“设备集合”节点。 选择设备集合，然后选择“显示成员”操作。 此操作将打开“设备”节点的子节点，其中包含该集合的设备列表。  

  - 选择集合子节点时，现在可以从功能区的集合组中启动“CMPivot”。  

- 在“监视”工作区中，选择“部署”节点 。 选择部署，然后在功能区中选择“查看状态”操作。 在部署状态窗格中，双击总资产，以向下钻取到设备列表。  

  - 在此列表中选择设备时，现在可以从功能区的“设备”组中启动“CMPivot”和“运行脚本”   。  


### <a name="collections-tab-in-devices-node"></a>设备节点中的“集合”选项卡
<!--4616810-->
（从版本 1906 中引入） 

在“资产和符合性”工作区中，转到“设备”节点，然后选择设备   。 在详细信息窗格中，切换到新的“集合”选项卡。此选项卡列出包含此设备的集合。 

> [!Note]  
> - 此选项卡当前在“设备集合”节点下的设备子节点中不可用。 例如，在集合上选择“显示成员”选项时，此选项卡不可用。
> - 对于某些用户而言，此选项卡可能无法按预期方式填充。 若要查看设备所属的完整集合列表，你必须具有“完全权限管理员”安全角色。 这是一个已知问题。 <!--5107309--> <!--5107309-->


### <a name="add-smbios-guid-column-to-device-and-device-collection-nodes"></a>将 SMBIOS GUID 列添加到设备和设备集合节点

（从版本 1906 中引入） 

<!--4526580-->
在设备和设备集合节点中，现在可以为“SMBIOS GUID”添加新列    。 此值与 System Resource 类的“BIOS GUID”属性相同。 它是设备硬件的唯一标识符。

### <a name="search-device-views-using-mac-address"></a>使用 MAC 地址搜索设备视图

<!--3600878-->
（从版本 1902 中引入） 

可以在 Configuration Manager 控制台的设备视图中搜索 MAC 地址。 此属性在 OS 部署管理员排查基于 PXE 部署的问题时很有用。 查看设备列表时，请向视图添加“MAC 地址”列  。 使用搜索字段添加“MAC 地址”搜索条件  。

### <a name="view-users-for-a-device"></a>查看设备的用户

自 1806 版起，“设备”节点中提供了以下列  ：  

- **主要用户** <!--1357280-->  

- **当前登录的用户** <!--1358202-->  

    > [!NOTE]  
    > 查看当前登录的用户需要[用户发现](../deploy/configure/configure-discovery-methods.md#bkmk_config-adud)和[用户设备相关性](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)。  

若要详细了解如何显示非默认列，请参阅[如何使用管理控制台](admin-console.md#columns)。

### <a name="improvement-to-device-search-performance"></a>设备搜索性能的改进

<!-- 3614690 -->
从 1806 版开始，在设备集合中进行搜索时，它不会针对所有对象属性搜索关键字。 如果搜索内容不精确，则会搜索以下四个属性：

- 名称
- 主要用户
- 当前登录的用户
- 上一个登录用户名

此行为显著缩短了按名称搜索所需的时间（尤其是在大型环境中）。 按特定条件进行的自定义搜索不受此更改的影响。


## <a name="software-library-workspace"></a>软件库工作区

### <a name="order-by-program-name-in-task-sequence"></a>按任务序列中的程序名称进行排序
<!--4616810-->
（从版本 1906 中引入） 

在“软件库”工作区中，展开“操作系统”，选择“任务序列”节点    。 编辑任务序列，然后选择或添加[安装包](../../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage)步骤。 如果包包含多个程序，则下拉列表现在按字母顺序对程序进行排序。

### <a name="task-sequences-tab-in-applications-node"></a>应用程序节点中的“任务序列”选项卡
<!--4616810-->
（从版本 1906 中引入） 

在“软件库”工作区中，展开“应用程序管理”，转到“应用程序”节点，然后选择应用程序    。 在详细信息窗格中，切换到新的“任务序列”选项卡  。此选项卡列出了引用此应用程序的任务序列。

### <a name="drill-through-required-updates"></a>钻取必需更新
<!--4224414-->
（从版本 1906 中引入） 

1. 请转到 Configuration Manager 控制台中的以下位置之一：

   - “软件库” > “软件更新” > “所有软件更新”   
   - “软件库” > “Windows 10 维护服务” > “所有 Windows 10 更新”  
   - “软件库” > “Office 365 客户端管理” > “Office 365 更新”   

1. 选择至少一台设备所需的任何更新。
1. 查看“摘要”选项卡，找到“统计信息”下的饼图 。
1. 选择饼图旁的“查看所需更新”超链接以深入查看设备列表。
1. 此操作将转到“设备”下的临时节点，可以在其中查看需要更新的设备。 还可对节点执行操作，例如从列表创建新集合。

> [!NOTE]
> 自 2020 年 4 月 21 日起，Office 365 专业增强版已重命名为 Microsoft 365 企业应用版  。 有关详细信息，请参阅 [Office 365 专业增强版的名称变更](/deployoffice/name-change)。 在控制台更新期间，你可能仍会看到 Configuration Manager 控制台和支持文档中引用的是旧名称。

### <a name="maximize-the-browse-registry-window"></a>将浏览注册表窗口最大化

<!--3594151 includes all MMS 1902 console changes-->
（从版本 1902 中引入） 

1. 在“软件库”工作区，展开“应用程序管理”，然后选择“应用程序”节点    。
1. 选择具有检测方法的部署类型的应用程序。 例如，Windows Installer 检测方法。
1. 在详细信息窗格中，切换到“部署类型”选项卡  。
1. 打开部署类型的属性，然后切换到“检测方法”选项卡  。选择“添加子句”  。
1. 将“设置类型”更改为“注册表”，然后选择“浏览”以打开“浏览注册表”窗口     。 可将此窗口最大化。  

### <a name="edit-a-task-sequence-by-default"></a>默认情况下编辑任务序列

（从版本 1902 中引入） 

在“软件库”工作区中，展开“操作系统”，选择“任务序列”节点    。 打开默认序列时，默认操作是“编辑”  。 默认操作以前为“属性”  。  

### <a name="go-to-the-collection-from-an-application-deployment"></a>从应用程序部署转到集合

（从版本 1902 中引入） 

1. 在“软件库”工作区，展开“应用程序管理”，然后选择“应用程序”节点    。
1. 选择应用程序。 在详细信息窗格中，切换到“部署”选项卡  。
1. 选择部署，然后在“部署”选项卡的功能区中选择新的“集合”选项  。此操作将视图切换到作为部署目标的集合。
   - 在此视图中右键单击部署上的上下文菜单也可以执行此操作。


## <a name="monitoring-workspace"></a>监视工作区

### <a name="correct-names-for-client-operations"></a>正确的客户端操作名称
<!--4616810-->
（从版本 1906 中引入） 

在“监视”工作区中，选择“客户端操作”   。 现在，“切换到下一个软件更新点”操作已正确命名  。

### <a name="show-collection-name-for-scripts"></a>显示脚本的集合名称
<!--4616810-->
（从版本 1906 中引入） 

在“监视”工作区中，选择“脚本状态”节点   。 除了列出 ID 之外，还列出了“集合名称”  。

### <a name="remove-content-from-monitoring-status"></a>从监视状态中删除内容

（从版本 1902 中引入） 

1. 在“监视”工作区中，展开“分发状态”，然后选择“内容状态”    。
1. 选择列表中的项，然后选择功能区中的“查看状态”选项  。
1. 在“资产详细信息”窗格中，右键单击分发点，然后选择新选项“删除”  。 此操作会从选定的分发点中删除此内容。

### <a name="copy-details-in-monitoring-views"></a>复制监视视图中的详细信息

（从版本 1806 中引入） 
<!--1357856-->
从“资产详细信息”窗格复制以下监视节点中的信息  ：  

- 内容分发状态   

- 部署状态   

![部署状态视图，复制资产详细信息](media/1810-deployment-status.PNG)

## <a name="administration-workspace"></a>管理工作区

<!--4223683-->
从版本 1906 开始，可以启用“安全”  节点下的某些节点以使用管理服务。 此项更改使控制台可以通过 HTTPS 而不是 WMI 来与 SMS 提供程序进行通信。 有关详细信息，请参阅[设置管理服务](../../../develop/adminservice/set-up.md#bkmk_console)。

## <a name="next-steps"></a>后续步骤

- [使用控制台](admin-console.md)
- [控制台通知](admin-console-notifications.md)
- [辅助功能](../../understand/accessibility-features.md)