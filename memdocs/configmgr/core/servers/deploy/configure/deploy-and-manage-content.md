---
title: 部署内容
titleSuffix: Configuration Manager
description: 为 Configuration Manager 安装分发点之后，下面介绍如何开始将内容部署到它们。
ms.date: 05/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d50dcca0-4419-449d-a487-73abcadf328f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: df26fe91f009a1a4f5d3c5a4f4adb5fe45bbd245
ms.sourcegitcommit: 4c129bb04ea4916c78446e89fbff956397cbe828
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/13/2020
ms.locfileid: "83343144"
---
# <a name="deploy-and-manage-content-for-configuration-manager"></a>为 Configuration Manager 部署和管理内容

适用范围：Configuration Manager (Current Branch)

为 Configuration Manager 安装分发点之后，可以开始将内容部署到其中。 通常，内容会在网络上传输到分发点，但是可以通过其他选项使内容到达分发点。 内容传输到分发点之后，可以在分发点上更新、重新分发、删除和验证该内容。  

##  <a name="distribute-content"></a><a name="bkmk_distribute"></a>分发内容  
通常会将内容分发到分发点，以便客户端计算机可以使用。 （对特定部署使用按需内容分发时例外。）在你分发内容时，Configuration Manager 将内容文件存储在包中，然后将此包分发到分发点。 此包的内容是从站点服务器的内容库中拉取。 可以分发的内容类型包括：  

- 应用程序部署类型  

- 包  

- 部署包  

- 驱动程序包  

- 操作系统映像  

- 操作系统安装程序  

- 启动映像  

- 任务序列  

在创建包含源文件的包时（例如应用程序部署类型或部署包），在其上创建包的站点成为包内容源的站点所有者。 Configuration Manager 将源文件从你为对象指定的源文件路径复制到拥有包内容源的站点服务器上的内容库。  然后，Configuration Manager 将信息复制到其他站点。 （有关此方面的详细信息，请参阅[内容库](../../../../core/plan-design/hierarchy/the-content-library.md)。）  

使用下列过程将内容分发到分发点。  

#### <a name="to-distribute-content-on-distribution-points"></a>在分发点上分发内容  

1.  在 Configuration Manager 控制台中，单击“软件库”。  

2.  在“软件库”  工作区中，针对要分发的内容的类型选择以下步骤之一：  

    - **应用程序**：展开“应用程序管理” > “应用程序”，然后选择要分发的应用程序 。  

    - **包**：展开“应用程序管理” >  “包”，然后选择要分发的包 。  

    - **部署包**：展开“软件更新” >  “部署包”，然后选择要分发的部署包 。  

    - **驱动程序包**：展开“操作系统” >  “驱动程序包”，然后选择要分发的驱动程序包 。  

    - **操作系统映像**：展开“操作系统” >  “操作系统映像”，然后选择要分发的操作系统映像 。  

    - **操作系统安装程序**：展开“操作系统” > “操作系统安装程序”，然后选择要分发的操作系统安装程序 。  

    - **启动映像**：展开“操作系统” >  “启动映像”，然后选择要分发的启动映像 。  

    - **任务序列**：展开“操作系统” >  “任务序列”，然后选择要分发的任务序列 。 尽管任务序列不包含内容，但它们有所分发的关联内容依赖关系。  

      > [!NOTE]  
      > 如果修改任务序列，你必须重新分发内容。  

3.  在“主页”  选项卡上的“部署”  组中，单击“分发内容” 。 分发内容向导将打开。  

4.  在“常规”页上，验证所列出的内容是你想要分发的内容，选择你是否想要 Configuration Manager 检测与所选内容关联的内容依赖项并将依赖项添加到分发，然后单击“下一步”。  

    > [!NOTE]  
    > 你可以选择仅为应用程序内容类型配置“检测关联内容依赖项并将其添加到分发”  设置。 Configuration Manager 会自动为任务序列配置此设置，并且不能修改此设置。  

5.  在“内容”  选项卡（如果已经显示）上，验证列出的内容是否为要分发的内容，然后单击“下一步” 。  

    > [!NOTE]  
    > 只有在向导的“常规”  页上选择了“检测关联的内容依赖关系并将其添加到此分发中”  设置后，才会显示“内容”  页。  

6.  在“内容目标”  页上，单击“添加” ，选择以下其中一项，然后执行相关的步骤：  

    - **集合**：选择“用户集合”或“设备集合”，单击与一个或多个分发点组关联的集合，然后单击“确定”  。  

        > [!NOTE]  
        > 仅显示与分发点组关联的集合。 有关将集合与分发点组进行关联的详细信息，请参阅[为 Configuration Manager 安装和配置分发点](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md)主题中的[管理分发点组](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage)。  

    - **分发点**：选择现有分发点，然后单击“确定” 。 未显示以前接收内容的分发点。  

    - **分发点组**：选择现有分发点组，然后单击“确定”。 未显示以前接收内容的分发点组。  

    添加完内容目标时，单击“下一步” 。  

7.  在“摘要”  页上，先查看分发设置，然后再继续。 要将内容分发到所选目标，请单击“下一步” 。  

8.  “进度”  页会显示分发进度。  

9. “确认”  页显示是否已成功将内容分配到分发点。 要监视内容分发，请参阅[使用 Configuration Manager 监视分发的内容](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md)。  

##  <a name="use-prestaged-content"></a><a name="bkmk_prestage"></a>使用预安排内容  
你可以预留应用程序和包类型的内容文件：  

- 在 Configuration Manager 控制台中，选择需要的内容，然后使用“创建预留的内容文件向导”创建压缩的预安排内容文件，其中包含所选内容的文件和关联的元数据。  

- 然后，你可以在站点服务器、辅助站点或分发点中手动导入内容。  

- 在站点服务器上导入预留内容文件时，会将内容文件添加到站点服务器上的内容库，然后在站点服务器数据库中注册内容文件。  

- 在分发点上导入预留内容文件时，会将内容文件添加到分发点上的内容库，并且向站点服务器发送状态消息，以通知站点内容在分发点上可用。  

**预安排内容的限制和注意事项：**  

- **当分发点位于站点服务器上时**，请不要为预安排内容启用分发点。 请改用[如何在站点服务器上的分发点上预留内容](#bkmk_dpsiteserver)中的过程。  

- **当分发点被配置为请求分发点时**，请不要为预安排内容启用分发点。 分发点的预留内容配置替代请求分发点配置。 为预留内容配置的请求分发点不从源分发点中请求内容，也不从站点服务器中接收内容。  

- **必须先在分发点上创建内容库，然后才能将内容预留到分发点**。 将内容预留到分发点之前，至少在网络上分发一次内容。  

- **预留具有长包源路径（例如超过 140 个字符）的包的内容时**，提取内容命令行工具可能无法将该包的内容成功提取到内容库中。  

有关何时预安排内容文件的信息，请参阅[管理用于内容管理的网络带宽](../../../plan-design/hierarchy/manage-network-bandwidth.md)主题中的*预安排内容*。  

使用下列部分来预留内容。  

###  <a name="step-1-create-a-prestaged-content-file"></a><a name="BKMK_CreatePrestagedContentFile"></a>步骤 1：创建预留内容文件  
你可以创建压缩的预安排内容文件，其中包含在 Configuration Manager 控制台中选择的内容的文件和关联的元数据。 使用以下过程创建预留的内容文件。  

##### <a name="to-create-a-prestaged-content-file"></a>创建预留的内容文件  

1.  在 Configuration Manager 控制台中，单击“软件库” 。  

2.  在“软件库”  工作区中，针对要预留的内容的类型选择以下步骤之一：  

    - **应用程序**：展开“应用程序管理”，单击“应用程序”，然后选择要预留的应用程序 。  

    - **包**：展开“应用程序管理”，单击“包”，然后选择要预留的包 。  

    - **驱动程序包**：展开“操作系统”，单击“驱动程序包”，然后选择要预留的驱动程序包 。  

    - **操作系统映像**：展开“操作系统”，单击“操作系统映像包”，然后选择要预留的操作系统映像包 。  

    - **操作系统安装程序**：展开“操作系统”，单击“操作系统安装程序”，然后选择要预留的操作系统安装程序 。  

    - **启动映像**：展开“操作系统”，单击“启动映像”，然后选择要预留的启动映像 。  

    - **任务序列**：展开“操作系统”，单击“任务序列”，然后选择要预留的任务序列 。  

3.  在“主页”  选项卡上的“部署”  组中，单击“创建预留的内容文件” 。 创建预留内容文件向导将会打开。  

    > [!NOTE]  
    > **对于应用程序：** 在“主页”选项卡的“应用程序”组中，单击“创建预留的内容文件”  。  
    >   
    > **对于包：** 在“主页”选项卡的 &lt;PackageName> 组中，单击“创建预留的内容文件”。  

4.  在“常规”  页上，单击“浏览” ，选择预留的内容文件的位置，指定文件的名称，然后单击“保存” 。 你在主站点服务器、辅助站点服务器或分发点上使用此预留内容文件以导入内容和元数据。  

5.  对于应用程序，选择“导出所有依赖项”，以使 Configuration Manager 检测与应用程序关联的依赖项并将其添加到预安排内容文件。 默认情况下选择了此设置。  

6.  在“管理员备注” 中，输入关于预留的内容文件的可选备注，然后单击“下一步” 。  

7.  在“内容”  页上，验证列出的内容是否为想要添加到预留内容文件中的内容，然后单击“下一步” 。  

8.  在“内容位置”  页上，为预留的内容文件指定要从中检索内容文件的分发点。 你可以选择多个分发点以检索内容。 内容位置部分中列出了分发点。 “内容”  列显示在每个分发点上可用的所选包或应用程序的数量。 Configuration Manager 从列表中的第一个分发点开始检索所选内容，然后在列表中向下移动以检索预安排内容文件所需的其余内容。 单击“上移”  或“下移”  ，以更改分发点的优先级顺序。 如果列表中的分发点不包含所有所选内容，则必须将包含内容的分发点添加到列表中，或者退出向导，将内容至少分发到一个分发点，然后重启向导。  

9. 在“摘要”  页上，确认详细信息。 你可以返回到以前的页面并进行更改。 单击“下一步”  创建预留的内容文件。  

10. “进度”  页显示要添加到预留的内容文件中的内容。  

11. 在“完成”  页上，验证是否已成功创建了预留的内容文件，然后单击“关闭” 。  

###  <a name="step-2-assign-the-content-to-distribution-points"></a><a name="BKMK_AssignContentToDistributionPoint"></a>步骤 2：将内容分配到分发点  
 预留内容文件后，请将内容分配到分发点。  

> [!NOTE]  
> 如果使用预留的内容文件在站点服务器上恢复内容库，并且不必在分发点上预留内容文件，则可以跳过此过程。  

 使用以下过程将预留的内容文件中的内容分配给分发点。  

> [!IMPORTANT]  
> 验证想要预留的分发点是否被配置为预留分发点，或者是否已使用网络将内容分发给这些分发点。  

##### <a name="to-assign-the-content-to-distribution-points"></a>将内容分配到分发点  

1.  在 Configuration Manager 控制台中，单击“软件库”。  

2.  在“软件库”  工作区中，针对创建预留内容文件时选择的内容的类型选择以下步骤之一：  

    - **应用程序**：展开“应用程序管理”，单击“应用程序”，然后选择预留的应用程序 。  

    - **包**：展开“应用程序管理”，单击“包”，然后选择预留的包 。  

    - **部署包**：展开“软件更新”，单击“部署包”，然后选择预留的部署包 。  

    - **驱动程序包**：展开“操作系统”，单击“驱动程序包”，然后选择预留的驱动程序包 。  

    - **操作系统映像**：展开“操作系统”，单击“操作系统映像”，然后选择预留的操作系统映像 。  

    - **操作系统安装程序**：展开“操作系统”，单击“操作系统安装程序”，然后选择预留的操作系统安装程序 。  

    - **启动映像**：展开“操作系统”，单击“启动映像”，然后选择预留的启动映像 。  

3.  在“主页”  选项卡上的“部署”  组中，单击“分发内容” 。 分发内容向导将打开。  

4.  在“常规”页上，验证所列出的内容是你预留的内容，选择你是否想要 Configuration Manager 检查与所选内容关联的内容依赖项并将依赖项添加到分发，然后单击“下一步”。  

    > [!NOTE]  
    > 你可以选择仅为应用程序内容类型配置“检测关联内容依赖项并将其添加到分发”  设置。 Configuration Manager 会自动为任务序列配置此设置，并且不能修改此设置。  

5.  在“内容”  页（如果已经显示）上，验证列出的内容是否为想要分发的内容，然后单击“下一步” 。  

    > [!NOTE]  
    > 只有在向导的“常规”  页上选择了“检测关联的内容依赖关系并将其添加到此分发中”  设置后，才会显示“内容”  页。  

6.  在“内容目标”  页上，单击“添加” ，选择包含要预留的分发点的以下其中一项，然后执行相关的步骤：  

    - **集合**：选择“用户集合”或“设备集合”，单击与一个或多个分发点组关联的集合，然后单击“确定”  。  

      > [!NOTE]  
      > 仅显示与分发点组关联的集合。  有关详细信息，请参阅[为 Configuration Manager 安装和配置分发点](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md)主题中的[管理分发点组](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage)。  

    - **分发点**：选择现有分发点，然后单击“确定” 。 未显示以前接收内容的分发点。  

    - **分发点组**：选择现有分发点组，然后单击“确定”。 未显示以前接收内容的分发点组。  

    添加完内容目标时，单击“下一步” 。  

7.  在“摘要”  页上，先查看分发设置，然后再继续。 要将内容分发到所选目标，请单击“下一步” 。  

8.  “进度”  页会显示分发进度。  

9. “确认”  页显示是否已成功将内容分配到分发点。 要监视内容分发，请参阅[使用 Configuration Manager 监视分发的内容](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md)。  

###  <a name="step-3-extract-the-content-from-the-prestaged-content-file"></a><a name="BKMK_ExportContentFromPrestagedContentFile"></a>步骤 3：从预留内容文件中提取内容  
创建预留内容文件并将内容分配到分发点之后，你可以将内容文件提取到站点服务器或分发点上的内容库。 通常，你已将预留内容文件复制到便携式驱动器（例如 USB 驱动器）或将内容刻录到媒体（例如 DVD），并使其在需要内容的站点服务器或分发点的位置中可用。  

使用以下过程，通过“提取内容”命令行工具从预留内容文件中手动导出内容文件。  

> [!IMPORTANT]  
> 当你运行“提取内容”命令行工具时，该工具将在创建预留内容文件时创建一个临时文件。 然后，将文件复制到目标文件夹并删除临时文件。 你必须有足够的磁盘空间来容纳此临时文件，否则过程将失败。 将在以下位置中创建临时文件：  
>   
> - 将在你指定为预留内容文件的目标文件夹的同一文件夹中创建临时文件。  

> [!IMPORTANT]  
> 运行“提取内容”命令行工具的用户在你从中提取预安排内容的计算机上必须有**管理员**权限。  

##### <a name="to-extract-the-content-files-from-the-prestaged-content-file"></a>从预留内容文件中提取内容文件  

1.  将预留内容文件复制到你要从中提取内容的计算机。  

2.  将“提取内容”命令行工具从 &lt;Configuration Manager 安装路径>\bin\\&lt;平台> 复制到你要从中提取预安排内容文件的计算机。  

3.  打开命令提示符，并导航到预留内容文件和“提取内容”工具的文件夹位置。  

    > [!NOTE]  
    > 你可以在站点服务器、辅助站点服务器或分发点上提取一个或多个预留内容文件。  

4.  键入 **extractcontent /P:** &lt;预留文件位置> **\\** &lt;预留文件名>  **/S** 以导入单一文件。  

    键入 **extractcontent /P:** &lt;预留文件位置>  **/S** 以导入指定文件夹中的所有预留文件。  

    例如，键入 **extractcontent /P:D:\PrestagedFiles\MyPrestagedFile.pkgx /S** ，其中 `D:\PrestagedFiles\` 是预留文件位置，`MyPrestagedFile.pkgx` 是预留文件名称，`/S` 告知 Configuration Manager 仅提取比当前位于分发点上的内容文件新的内容文件。  

    在站点服务器上提取预留内容文件时，会将内容文件添加到站点服务器上的内容库，然后在站点服务器数据库中注册内容可用性。 在分发点上导出预留内容文件时，会将内容文件添加到分发点上的内容库，并且分发点将向父主站点服务器发送状态消息，然后在站点数据库中注册内容可用性。  

    > [!IMPORTANT]  
    > 在以下方案中，当内容更新为新版本时，你必须更新从预留内容文件中提取的内容：  
    >   
    >  1.  你为包的版本 1 创建预留内容文件。  
    >  2.  你使用版本 2 更新包的源文件。  
    >  3.  你在分发点上提取预留内容文件（包的版本 1）。  
    >   
    > Configuration Manager 不会自动将包版本 2 分发到分发点。 你必须创建包含新文件版本的新预留内容文件，然后提取内容，更新分发点以分发已更改的文件，或者重新分发包中的所有文件。  

###  <a name="how-to-prestage-content-on-a-distribution-point-on-a-site-server"></a><a name="bkmk_dpsiteserver"></a>如何在站点服务器上的分发点上预留内容  
当在站点服务器上安装分发点时，必须使用以下过程来成功预留内容。 这是因为内容库中已存在这些内容文件。  

如果没有为预安排内容启用分发点，或者如果分发点不在站点服务器上，请参阅本主题中的[使用预安排内容](#bkmk_prestage)部分。  

##### <a name="to-prestage-content-on-distribution-points-located-on-a-site-server"></a>在位于站点服务器上的分发点上预留内容  

1.  使用以下步骤确认没有为预留的内容启用分发点。  

    1.  在 Configuration Manager 控制台中，单击“管理”。  

    2.  在“管理”  工作区中，单击“分发点” ，然后选择位于站点服务器上的分发点。  

    3.  在“主页”选项卡上的“属性”组中，单击“属性”。  

    4.  在“常规”  选项卡上，确认未选中“为预留的内容启用此分发点”  复选框。  

2.  按本主题[步骤 1：创建预留的内容文件](#BKMK_CreatePrestagedContentFile)部分所述创建预留的内容文件。  

3.  按本主题[步骤 2：将内容分配到分发点](#BKMK_AssignContentToDistributionPoint)部分所述将内容分配到分发点。  

4.  在站点服务器上，按本主题[步骤 3：从预留的内容文件中提取内容](#BKMK_ExportContentFromPrestagedContentFile)部分所述从预留的内容文件中提取内容。  

    > [!NOTE]  
    > 如果分发点位于辅助站点上，则等待至少 10 分钟，然后使用连接到父主站点的 Configuration Manager 控制台将内容分配到辅助站点上的分发点。  

##  <a name="manage-the-content-you-have-distributed"></a><a name="bkmk_manage"></a>管理已分发的内容  
你具有以下用于管理内容的选项：  
- [更新内容](#update-content)
- [重新分发内容](#redistribute-content)
- [删除内容](#remove-content)
- [验证内容](#validate-content)

### <a name="update-content"></a>更新内容
当通过添加新文件或使用较新版本替换现有文件更新了部署的源文件位置时，可以使用“更新分发点”或“更新内容”操作更新分发点上的内容文件：  
- 内容文件是从原始包源位置复制到拥有包内容源的站点上的内容库
- 包版本将递增  
- 站点服务器上和分发点上内容库的每个实例仅更新已更改的文件  

> [!WARNING]  
> 应用程序的包版本始终为 1。 当你更新应用程序部署类型的内容时，Configuration Manager 将为该部署类型创建新的内容 ID，并且包将引用该新内容 ID。  

#### <a name="to-update-content-on-distribution-points"></a>更新分发点上的内容  

1.  在 Configuration Manager 控制台中，单击“软件库”。  

2.  在“软件库”  工作区中，针对要分发的内容的类型选择以下步骤之一：  

    - **应用程序**：展开“应用程序管理” > “应用程序”，然后选择要分发的应用程序 。 单击“部署类型”  选项卡，然后选择要更新的部署类型。  

    - **包**：展开“应用程序管理” > “包”，然后选择要更新的包 。  

    - **部署包**：展开“软件更新” > “部署包”，然后选择要更新的部署包 。  

    - **驱动程序包**：展开“软件更新” > “驱动程序包”，然后选择要更新的驱动程序包 。  

    - **操作系统映像**：展开“操作系统” > “操作系统映像”，然后选择要更新的操作系统映像 。  

    - **操作系统安装程序**：展开“操作系统” > “操作系统安装程序”，然后选择要更新的操作系统安装程序 。  

    - **启动映像**：展开“操作系统” >  “启动映像”，然后选择要更新的启动映像 。  

3.  在“主页”  选项卡上的“部署”  组中，单击“更新分发点” ，然后单击“确定”  确认你要更新内容。  

    > [!NOTE]  
    > 要更新应用程序的内容，请单击“部署类型”  选项卡，右键单击部署类型，单击“更新内容” ，然后单击“确定”  确认你要刷新内容。  

    > [!NOTE]  
    > 在更新启动映像的内容时，管理分发点向导将打开。 查看“摘要”  页上的信息，然后完成向导以更新内容。  

### <a name="redistribute-content"></a>重新分发内容
你可以重新分发包以将包中的所有内容文件复制到分发点或分发点组，从而覆盖现有文件。  

使用此操作来修复包中的内容文件或在初始分发失败时重新发送内容。 可通过以下项目重新分发包：  

- 包属性  
- 分发点属性  
- 分发点组属性。  


#### <a name="to-redistribute-content-from-package-properties"></a>从包属性中重新分发内容  

1.  在 Configuration Manager 控制台中，单击“软件库”。  

2.  在“软件库”  工作区中，针对要分发的内容的类型选择以下步骤之一：  

    - **应用程序**：展开“应用程序管理” >  “应用程序”，然后选择要重新分发的应用程序 。  

    - **包**：展开“应用程序管理” > “包”，然后选择要重新分发的包 。  

    - **部署包**：展开“软件更新” >  “部署包”，然后选择要重新分发的部署包 。  

    - **驱动程序包**：展开“操作系统” > “驱动程序包”，然后选择要重新分发的驱动程序包 。  

    - **操作系统映像**：展开“操作系统” > “操作系统映像”，然后选择要重新分发的操作系统映像 。  

    - **操作系统安装程序**：展开“操作系统” > “操作系统安装程序”，然后选择要重新分发的操作系统安装程序 。  

    - **启动映像**：展开“操作系统” >  “启动映像”，然后选择要重新分发的启动映像 。  

3.  在“主页”选项卡上的“属性”组中，单击“属性”。  

4.  单击“内容位置”  选项卡，选择要在其中重新分发内容的分发点或分发点组，单击“重新分发” ，然后单击“确定” 。  

#### <a name="to-redistribute-content-from-distribution-point-properties"></a>从分发点属性重新分发内容  

1.  在 Configuration Manager 控制台中，单击“管理”。  

2.  在“管理”  工作区中，单击“分发点” ，然后选择要在其中重新分发内容的分发点。  

3.  在“主页”选项卡上的“属性”组中，单击“属性”。  

4.  单击“内容”  选项卡，选择要重新分发的内容，单击“重新分发” ，然后单击“确定” 。  

#### <a name="to-redistribute-content-from-distribution-point-group-properties"></a>从分发点组属性中重新分发内容  

1.  在 Configuration Manager 控制台中，单击“管理”。  

2.  在“管理”  工作区中，单击“分发点组” ，然后选择要在其中重新分发内容的分发点组。  

3.  在“主页”选项卡上的“属性”组中，单击“属性”。  

4.  单击“内容”  选项卡，选择要重新分发的内容，单击“重新分发” ，然后单击“确定” 。  

    > [!IMPORTANT]  
    > 包中的内容会重新分发到分发点组内的所有分发点。  


#### <a name="use-the-sdk-to-force-replication-of-content"></a>使用 SDK 强制复制内容
可以使用 Configuration Manager SDK 的 **RetryContentReplication** Windows Management Instrumentation (WMI) 类方法强制分发管理器将内容从源位置复制到内容库中。  

仅在正常的内容复制出现问题（通常使用控制台的监视节点来确认）之后必须重新分发内容时，使用此方法强制进行复制。   

有关此 SDK 选项的详细信息，请参阅 [SMS_CM_UpdatePackages 类中的 RetryContentReplication 方法](../../../../develop/reference/sum/retrycontentreplication-method-in-class-sms_cm_updatepackages.md)。

### <a name="remove-content"></a>删除内容
不再需要分发点上的内容时，可以删除分发点上的内容文件。  

- 包属性  
- 分发点属性  
- 分发点组属性。  

但是，如果内容与分发到相同分发点上的另一个包关联，则无法删除此内容。  

#### <a name="to-remove-package-content-files-from-distribution-points"></a>从分发点中删除包内容文件  

1.  在 Configuration Manager 控制台中，单击“软件库”。  

2.  在“软件库”  工作区中，针对要删除的内容的类型选择以下步骤之一：  

    - **应用程序**：展开“应用程序管理” > “应用程序”，然后选择要删除的应用程序 。  

    - **包**：展开“应用程序管理” > “包”，然后选择要删除的包 。  

    - **部署包**：展开“软件更新” > “部署包”，然后选择要删除的部署包 。  

    - **驱动程序包**：展开“操作系统” > “驱动程序包”，然后选择要删除的驱动程序包 。  

    - **操作系统映像**：展开“操作系统” > “操作系统映像”，然后选择要删除的操作系统映像 。  

    - **操作系统安装程序**：展开“操作系统” > “操作系统安装程序”，然后选择要删除的操作系统安装程序 。  

    - **启动映像**：展开“操作系统” > “启动映像”，然后选择要删除的启动映像 。  

3.  在“主页”选项卡上的“属性”组中，单击“属性”。  

4.  单击“内容位置”  选项卡，选择要从其中删除内容的分发点或分发点组，单击“删除” ，然后单击“确定” 。  

#### <a name="to-remove-package-content-from-distribution-point-properties"></a>从分发点属性中删除包内容  

1.  在 Configuration Manager 控制台中，单击“管理”。  

2.  在“管理”  工作区中，单击“分发点” ，然后选择要在其中删除内容的分发点。  

3.  在“主页”选项卡上的“属性”组中，单击“属性”。  

4.  单击“内容”  选项卡，选择要删除的内容，单击“删除” ，然后单击“确定” 。  

#### <a name="to-remove-content-from-distribution-point-group-properties"></a>从分发点组属性中删除内容  

1.  在 Configuration Manager 控制台中，单击“管理”。  

2.  在“管理”  工作区中，单击“分发点组” ，然后选择要在其中删除内容的分发点组。  

3.  在“主页”选项卡上的“属性”组中，单击“属性”。  

4.  单击“内容”  选项卡，选择要删除的内容，单击“删除” ，然后单击“确定” 。  


### <a name="validate-content"></a>验证内容
内容验证过程验证分发点上内容文件的完整性。 你可以按计划启用内容验证，或者可以从分发点和包的属性中手动启动内容验证。  

当内容验证过程开始时，Configuration Manager 将验证分发点上的内容文件，且如果文件哈希并非分发点上的文件所需的，则 Configuration Manager 将创建一个可在“监视”工作区查看的状态消息。  

有关配置内容验证计划的详细信息，请参阅[为 Configuration Manager 安装和配置分发点](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md)主题中的[分发点配置](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs)。  


#### <a name="to-initiate-content-validation-for-all-content-on-a-distribution-point"></a>启动对分发点上所有内容的内容验证  

1.  在 Configuration Manager 控制台中，单击“管理”。  

2.  在“管理”  工作区中，单击“分发点” ，然后选择要在其中验证内容的分发点。  

3.  在“主页”选项卡上的“属性”组中，单击“属性”。  

4.  在“内容”  选项卡上，选择要在其中验证内容的包，单击“验证” ，单击“确定” ，然后单击“确定” 。 内容验证过程将针对分发点上的包启动。  

5.  要查看内容验证过程的结果，请在“监视”  工作区中展开“分发状态” ，并单击“内容状态”  节点。 将显示每种包类型（例如，应用程序、软件更新包以及启动映像）的内容。 有关监视内容状态的详细信息，请参阅[使用 Configuration Manager 监视分发的内容](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md)。  

#### <a name="to-initiate-content-validation-for-a-package"></a>针对某个包启动内容验证  

1.  在 Configuration Manager 控制台中，单击“软件库”。  

2.  在“软件库”  工作区中，针对要验证的内容的类型选择以下步骤之一：  

    - **应用程序**：展开“应用程序管理” > “应用程序”，然后选择要验证的应用程序 。  

    - **包**：展开“应用程序管理” > “包”，然后选择要验证的包 。  

    - **部署包**：展开“软件更新” > “部署包”，然后选择要验证的部署包 。  

    - **驱动程序包**：展开“操作系统” > “驱动程序包”，然后选择要验证的驱动程序包 。  

    - **操作系统映像**：展开“操作系统” > “操作系统映像”，然后选择要验证的操作系统映像 。  

    - **操作系统安装程序**：展开“操作系统” >  “操作系统安装程序”，然后选择要验证的操作系统安装程序 。  

    - **启动映像**：展开“操作系统” > “启动映像”，然后选择要预留的启动映像 。  

3.  在“主页”选项卡上的“属性”组中，单击“属性”。  

4.  在“内容位置”  选项卡上，选择要在其中验证内容的分发点或分发点组，单击“验证” ，单击“确定” ，然后单击“确定” 。 内容验证过程将针对所选分发点或分发点组上的内容启动。  

5.  要查看内容验证过程的结果，请在“监视”  工作区中展开“分发状态” ，并单击“内容状态”  节点。 将显示每种包类型（例如，应用程序、软件更新包以及启动映像）的内容。 有关监视内容状态的详细信息，请参阅[使用 Configuration Manager 监视分发的内容](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md)。  
