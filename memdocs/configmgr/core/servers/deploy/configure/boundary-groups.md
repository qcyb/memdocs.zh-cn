---
title: 配置边界组
titleSuffix: Configuration Manager
description: 通过使用边界组以逻辑方式对称为边界的相关网络位置进行整理，帮助客户端查找站点系统
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5db2926f-f03e-49c7-b44b-e89b1a5a6779
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7a925c29b5d186f3ca6f320741f5ca602b0bbb79
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128386"
---
# <a name="configure-boundary-groups-for-configuration-manager"></a>为 Configuration Manager 配置边界组

适用范围：Configuration Manager (Current Branch)

使用 Configuration Manager 中的边界组以逻辑方式对相关网络位置（[边界](boundaries.md)）进行整理，以便更轻松地管理基础结构。 使用边界组之前应向其分配边界。

默认情况下，Configuration Manager 在每个站点创建默认站点边界组。

若要配置边界组，请将边界（网络位置）和站点系统角色（如分发点）关联到边界组。 此配置有助于将客户端关联到站点系统服务器，例如位于网络上的客户端附近的分发点。

要提高服务器的可用性，使其可用于更广泛的网络位置，请向多个边界组分配相同的边界和相同的服务器。

客户端使用边界组来执行以下操作：  

- 自动站点分配  
- 查找可以提供包括以下某种服务的站点系统服务器：

  - 内容位置的的分发点  
  - 软件更新点  
  - 状态迁移点  

    > [!NOTE]
    > 状态迁移点不使用回退关系。 有关详细信息，请参阅[回退](#fallback)。

  - 首选管理点  

    > [!NOTE]  
    > 如果使用首选管理点，则为层次结构启用此选项，但不是从边界组配置中启用。 有关详细信息，请参阅[启用对首选管理点的使用](boundary-group-procedures.md#bkmk_proc-prefer)。  

  - 云管理网关（从版本 1902 开始）

## <a name="boundary-groups-and-relationships"></a>边界组和关系

对于层次结构中的每个边界组，你可以分配：

- 一个或多个边界。 客户端的**当前**边界组是一个网络位置，定义为分配给特定边界组的边界。 一个客户端可具有多个当前边界组。  

- 一个或多个站点系统角色。 客户端始终可以使用与它们当前边界组关联的角色。 根据其他配置，它们可使用附加边界组中的角色。  

对于你创建的每个边界组，你可以配置指向另一个边界组的单向链接。 此链接称为**关系**。 链接的边界组称为**邻居**边界组。 边界组可以具有多个关系，每个关系都有特定的邻居边界组。

当客户端在其当前边界组中找不到可用的站点系统时，每个关系的配置可确定它何时开始搜索相邻边界组。 对其他组的这一搜索称为**回退**。

有关详细信息，请参阅以下过程：  

- [创建边界组](boundary-group-procedures.md#bkmk_create)  
- [配置边界组](boundary-group-procedures.md#bkmk_config)  

### <a name="show-boundary-groups-for-devices"></a><a name="bkmk_show-boundary"></a> 显示设备的边界组

<!--6521835-->

从版本 2002 开始，为了帮助你通过边界组更好地识别设备行为并进行故障排除，可以查看特定设备的边界组。 在“设备”节点中，或在显示某个“设备集合”的成员时，将新的“边界组”列添加到列表视图中  。

- 如果某个设备属于多个边界组，则该值为以逗号分隔的边界组名称列表。

- 数据会在客户端向站点发出位置请求时更新，或者最多 24 小时更新一次。

- 如果客户端在漫游且不是边界组的成员，则该值为空白。

> [!NOTE]
> 此信息为站点数据，并且仅在主站点上可用。 在将 Configuration Manager 连接到管理中心站点时，不会看到此列的值。

## <a name="fallback"></a>回退

若要防止客户端在其当前边界组中找不到可用站点系统时出现问题，请为回退行为定义边界组之间的关系。 回退允许客户端将搜索范围扩展到附加的边界组，以查找可用的站点系统。

关系在边界组属性“关系”选项卡上配置。在配置关系时，你将定义指向邻居边界组的链接。 对于每种受支持的站点系统角色，可配置独立的设置以回退到该相邻边界组。 有关详细信息，请参阅[配置回退行为](boundary-group-procedures.md#bkmk_bg-fallback)。

例如，在配置特定边界组的关系时，可将分发点的回退设置为在 20 分钟后发生。 默认为 120 分钟。有关更广泛的示例，请参阅[使用边界组的示例](#example-of-using-boundary-groups)。

如果客户端在其当前边界组中找不到可用的站点系统角色，它会使用以分钟为单位的回退时间。 此回退时间用于确定客户端何时开始搜索与相邻边界组关联的可用站点系统。  

当客户端找不到可用的站点系统，会开始从相邻边界组搜索位置。 此行为会扩大可用站点系统池。 边界组的配置及其关系定义了客户端对该可用站点系统池的使用。

- 一个边界组可具有多个关系。 通过此配置，可以将每种站点系统配置为在不同的时间段之后回退到不同的相邻边界组。  

- 客户端仅回退到直接与其当前边界组相邻的边界组。  

- 当某个客户端是多个边界组的成员时，当前边界组即被定义为该客户端的所有边界组的联合。 该客户端会回退到任何这些原始边界组的相邻边界组。  

> [!NOTE]
> 状态迁移点角色不使用回退关系。 如果将状态迁移点和分发点角色都添加到同一站点系统服务器，则不要在其边界组上配置回退。 如果需要对分发点使用边界组回退，请在其他站点系统服务器上添加状态迁移点角色。<!-- 2838807 -->

### <a name="the-default-site-boundary-group"></a>默认站点边界组

可以创建自己的边界组，且每个站点都有一个 Configuration Manager 创建的默认站点边界组。 此组命名为 **Default-Site-Boundary-Group&lt;sitecode>** 。 例如，站点 ABC 的组将被命名为“Default-Site-Boundary-Group&lt;ABC>”。

对于你创建的每个边界组，Configuration Manager 自动在层次结构中创建指向每个默认站点边界组的隐式链接。  

- 隐式链接是一个默认回退选项，从当前边界组到站点默认边界组。 默认回退时间为 120 分钟。  

- 对于不在与任何边界组关联的边界中的客户端：若要识别有效的站点系统角色，请使用已分配站点中的默认站点边界组。  

管理默认站点边界组的回退：  

- 打开站点默认边界组的属性，更改“默认行为”选项卡上的值。将在此处所做的更改应用到*所有*指向此边界组的隐式链接。 在你从另一个边界组配置显式链接到此默认站点边界组时，可以覆盖这些默认设置。  

- 打开自定义边界组的属性。 将显式链接的值更改为默认站点边界组。 为回退或块回退设置以分钟为单位的新的时间时，所做的更改会影响你正在配置的链接。 显式链接的配置会覆盖默认站点边界组“默认行为”选项卡上的设置。  

## <a name="site-assignment"></a>站点分配  

你可以使用客户端的分配的站点配置每个边界组。  

- 使用自动站点分配的新安装的客户端将加入包含客户端当前网络位置的边界组的分配的站点。  

- 分配到站点后，当更改其网络位置时，客户端不会更改其站点分配。 例如，客户端漫游到新的网络位置。 此位置是具有不同站点分配的边界组中的某个边界。 客户端的分配站点不会更改。  

- 当 Active Directory 系统发现发现新资源时，站点将依据边界组的边界对资源的网络信息进行评估。 此过程将新资源与分配的站点关联，以供客户端请求安装方法使用。  

- 当边界是多个边界组（这些边界组具有不同的分配的站点）的成员时，客户端会随机选择其中一个站点。  

- 对分配了边界组的站点的更改仅适用于新的站点分配操作。 以前分配给某个站点的客户端不会根据对边界组配置（或它们自身网络位置）的更改重新评估其站点分配。  

有关客户端站点分配的详细信息，请参阅[对计算机使用自动站点分配](../../../clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment)。  

有关如何配置站点分配的详细信息，请参阅以下过程：

- [配置站点分配，并选择站点系统服务器](boundary-group-procedures.md#bkmk_references)
- [为自动站点分配配置回退站点](boundary-group-procedures.md#bkmk_site-fallback)

## <a name="distribution-points"></a>分发点

当客户端请求分发点的位置时，Configuration Manager 会向客户端发送一个站点系统列表。 这些站点系统采用与包含客户端当前网络位置的每个边界组相关联的适当类型：

- 在软件分发过程中，客户端请求用于在有效内容源上部署内容的位置。 此位置可能是分发点或对等缓存源。  

- **在操作系统部署期间**，客户端请求用以发送或接收其状态迁移信息的位置。  

  - 客户端基于边界组行为获取内容。 有关更多详细信息，请参阅[对边界组的任务序列支持](#bkmk_bgr-osd)。  

在内容部署期间，如果客户端请求的内容在其当前边界组的某个源中找不到，该客户端会继续请求该内容。 它会尝试搜索其当前边界组中的其他内容源，直至达到相邻或默认站点边界组的回退时间。 如果客户端仍未找到内容，它将会扩展其内容源的搜索范围，以包括相邻边界组。

如果将内容配置为按需分发，并且在客户端请求时在分发点上不可用，则该站点开始将内容传输到该分发点。 客户端可能会在回退为使用相邻边界组之前找到该服务器作为内容源。

### <a name="client-installation"></a><a name="bkmk_ccmsetup"></a> 客户端安装

Configuration Manager 客户端安装程序 ccmsetup 可以从本地源或通过管理点获取安装内容。 它的初始行为取决于用于安装客户端的命令行参数：<!-- MEMDocs#286 -->

- 如果你不使用 /mp 或 /source 参数，ccmsetup 会尝试从 Active Directory 或 DNS 获取管理点列表。
- 如果你只指定 /source，它会强制从指定路径进行安装。 而不会发现管理点。 如果在指定路径找不到 ccmsetup.cab，ccmsetup 就会失败。
- 如果你同时指定 /mp 和 /source，它会检查指定管理点及其发现的任何管理点。 如果找不到有效的管理点，它就会回退到指定源路径。

若要详细了解这些 ccmsetup 参数，请参阅[客户端安装参数和属性](../../../clients/deploy/about-client-installation-properties.md)。

<!--1358840-->
当 ccmsetup 联系管理点来查找必要内容时，管理点会根据边界组配置来返回分发点。 如果在边界组中定义了关系，则管理点可按以下顺序返回分发点：

1. 当前边界组  
2. 相邻边界组  
3. 站点默认边界组  

> [!Note]  
> 客户端安装进程不使用回退时间。 为了尽快找到内容，它会立即回退到下一个边界组。
>
> 在 Configuration Manager 的早期版本中，管理点在此过程中仅返回客户端当前边界组中的分发点。 如果没有可用内容，安装进程会回退，以从管理点下载内容。 无法回退到其他边界组中可能具有必要内容的分发点。

### <a name="task-sequence-support-for-boundary-groups"></a><a name="bkmk_bgr-osd"></a> 对边界组的任务序列支持

<!--1359025-->
当设备运行任务序列并且需要获取内容时，它可以使用类似于 Configuration Manager 客户端的边界组行为。

可以使用任务序列部署的“分发点”页面上的以下设置配置此行为：

- **在没有本地分发点可用的情况下使用远程分发点**：对于此部署，任务序列可以回退到相邻边界组中的分发点。  

- **允许客户端使用来自默认站点边界组的分发点**：对于此部署，任务序列可以回退到默认站点边界组中的分发点。  

若要使用这一新行为，请确保将客户端更新到最新版本。

#### <a name="location-priority"></a>位置优先级  

任务序列会按以下顺序尝试获取内容：  

1. 对等缓存源  

2. 当前边界组中的分发点  

3. 相邻边界组中的分发点  

    > [!Important]  
    > 由于任务序列处理的实时特性，它不会等待相邻边界组的故障转移时间。 它会使用故障转移时间来确定相邻边界组的优先级。 例如，如果任务序列无法从其当前边界组中的分发点获取内容，它会立即尝试故障转移时间最短的相邻边界组中的分发点。 如果该进程失败，它会故障转移到具有较长故障转移时间的相邻边界组中的分发点。  

4. 站点默认边界组中的分发点  

任务序列日志文件 smsts.log 显示了它基于部署属性使用的位置源优先级。

### <a name="boundary-group-options-for-peer-downloads"></a><a name="bkmk_bgoptions"></a>对等下载适用的边界组选项

<!--1356193, 1358749-->
边界组包含以下附加设置，让用户可以更好地控制环境中的内容分发：  

- [允许在此边界组中进行对等下载](#bkmk_bgoptions1)  

- [对等下载期间，只能使用同一子网内的对等设备](#bkmk_bgoptions2)  

- [优先选择具有相同子网的对等点的分发点](#bkmk_bgoptions3)  

- [优先选择分发点上的云分发点](#bkmk_bgoptions4)  

有关如何配置这些设置的详细信息，请参阅[配置边界组](boundary-group-procedures.md#bkmk_config)。

如果设备在多个边界组中，则以下行为适用于这些设置：

- 允许在此边界组中进行对等下载：如果在任何一个边界组中禁用此功能，则客户端不会使用交付优化。
- 对等下载期间，只能使用同一子网内的对等点：如果在任何一个边界组中启用了此设置，则此设置生效。
- 优先选择分发点而非同一子网内的对等点：如果在任何一个边界组中启用了此设置，则此设置生效。
- 首选基于云的源而非本地源：如果在任何一个边界组中启用了此设置，则此设置生效。

#### <a name="allow-peer-downloads-in-this-boundary-group"></a><a name="bkmk_bgoptions1"></a> 允许在此边界组中进行对等下载

默认情况下将启用此设置。 管理点向客户端提供包含对等源的内容位置的列表。 此设置还会影响[交付优化](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization)组 ID 的应用。  

有两个应考虑禁用此选项的常见场景：  

- 如果你拥有的边界组包括来自地理上分散的位置（例如 VPN）的边界， 两个客户端可能位于同一边界组中，因为它们都通过 VPN 连接，但位于不适合对等共享内容的极其不同的位置。  

- 如果将单个较大的而且不引用任何分发点的边界组用于站点分配。  

> [!IMPORTANT]
> 如果设备在多个边界组中，请确保在设备的所有边界组中启用此设置。 否则，客户端不会使用交付优化。 例如，它不会设置 DOGroupID 注册表项。

#### <a name="during-peer-downloads-only-use-peers-within-the-same-subnet"></a><a name="bkmk_bgoptions2"></a> 对等下载期间，只能使用同一子网内的对等设备

此设置取决于前面的选项。 如果启用此选项，管理点将仅包含与客户端在同一子网中的内容位置列表对等源。

启用此选项的常见场景：

- 内容分发的边界组设计包含一个与其他较小边界组重叠的大型边界组。 使用此新设置，管理点向客户端提供的内容源列表仅包含来自同一子网的对等源。

- 你拥有的单个大型边界组适用于所有远程办公室位置。 启用此选项，客户端仅在远程办公室位置的子网内共享内容，而不是冒险在位置之间共享内容。

从版本 2002 开始，根据网络的配置，可以排除某些子网以进行匹配。 例如，你想要包含边界，但要排除特定的 VPN 子网。 默认情况下，Configuration Manager 排除默认 Teredo 子网 (`2001:0000:%`)。<!--3555777-->

> [!NOTE]
> 在版本 2002 中，[扩展独立主站点](../install/prerequisites-for-installing-sites.md#bkmk_expand)以添加管理中心站点 (CAS) 时，子网排除列表会恢复为默认值。 若要解决此问题，在站点扩展后，运行 PowerShell 脚本以自定义 CAS 上的子网排除列表。<!-- 6309068 -->

将子网排除列表导入为以逗号分隔的子网字符串。 使用百分号 (`%`) 作为通配符。 在顶级站点服务器上，设置或读取 SMS_SCI_Component 类中 SMS_HIERARCHY_MANAGER 组件的 SubnetExclusionList 嵌入式属性  。 有关详细信息，请参阅 [SMS_SCI_Component 服务器 WMI 类](../../../../develop/reference/core/servers/configure/sms_sci_component-server-wmi-class.md)。

##### <a name="sample-powershell-script-to-update-the-subnet-exclusion-list"></a>用于更新子网排除列表的示例 PowerShell 脚本

下面的脚本是更改此值的示例方法。 在 `2001:0000:%,172.16.16.0` 之后将子网追加到 **PropertyValue** 变量。 这是一个逗号分隔的字符串。 在层次结构中的顶层站点服务器上运行此脚本。

```PowerShell
$PropertyValue = "2001:0000:%,172.16.16.0"
$PropertyName = "SubnetExclusionList"

$providerMachine = Get-WmiObject -Class "SMS_ProviderLocation" -Namespace "root\sms"

if ($providerMachine -is [system.array])
{
    $providerMachine=$providerMachine[0]
}

$SiteCode = $providerMachine.SiteCode

$component = Get-WmiObject -Query 'select comp.* from sms_sci_component comp join SMS_SCI_SiteDefinition sdef on sdef.SiteCode=comp.SiteCode where sdef.ParentSiteCode="" and comp.componentname="SMS_HIERARCHY_MANAGER"' -ComputerName $providerMachine.Machine -Namespace root\sms\site_$SiteCode
$properties = $component.props

Write-host "Updating property for site " $SiteCode

foreach ($property in $properties)
{
  if ($property.propertyname -like $PropertyName)
  {
    Write-host "Current value for SubnetExclusionList is  " $property.value1
    $property.value1 = $PropertyValue
    Write-host "Updating value for SubnetExclusionList to " $property.value1
    break
  }
}

$component.props = $properties
$component.put()
```

> [!NOTE]
> 默认情况下，Configuration Manager 在此列表中包含 Teredo 子网。 更改列表时，请始终先查看现有值。 将其他子网追加到列表，然后设置新值。

#### <a name="prefer-distribution-points-over-peers-with-the-same-subnet"></a><a name="bkmk_bgoptions3"></a> 优先选择具有相同子网的对等点的分发点

默认情况下，管理点会优先考虑内容位置列表顶部的对等缓存源。 此设置会反转与对等缓存源位于同一子网的客户端的优先级。

> [!TIP]
> 此行为适用于 Configuration Manager 客户端。 它不适用于任务序列下载内容的情况。 任务序列运行时，它优先选择对等缓存源而不是分发点。<!-- SCCMDocs#1376 -->

#### <a name="prefer-cloud-distribution-points-over-distribution-points"></a><a name="bkmk_bgoptions4"></a> 优先选择分发点上的云分发点

如果你的分支机构具有更快的 Internet 链接，你现在可以优先考虑云内容。  

在版本 1902 中，此设置现在标题为“首选基于云的源而非本地源”。 基于云的源包括：<!-- SCCMDocs#1529 -->

- 云分发点
- Microsoft 更新（在版本 1902 中添加）

## <a name="software-update-points"></a><a name="bkmk_sup"></a> 软件更新点 

客户端使用边界组来查找新的软件更新点。 若要控制客户端可以找到哪些服务器，请将各个软件更新点添加到不同的边界组。

如果将所有现有软件更新点添加到默认站点边界组，则客户端会从可用服务器池中选择软件更新点。 此行为类似于 Configuration Manager Current Branch 的早期版本。 对于控制选择和回退行为，请将单个软件更新点添加到不同的边界组。

如果安装新站点，则不会将软件更新点添加到默认站点边界组。 将软件更新点分配给边界组，以便客户端可以查找并使用它们。

### <a name="fallback-for-software-update-points"></a>软件更新点的回退

软件更新点的回退配置和其他站点系统角色一样，但有以下注意事项：  

#### <a name="new-clients-use-boundary-groups-to-select-software-update-points"></a>新的客户端使用边界组来选择软件更新点

当安装新客户端，它们会从那些与已配置的边界组关联的服务器中选择软件更新点。 此行为将取代以前的行为，即客户端从共享客户端林的服务器列表中随机选择一个软件更新点。

#### <a name="clients-continue-to-use-a-last-known-good-software-update-point-until-they-fallback-to-find-a-new-one"></a>客户端继续使用上次已知良好的软件更新点，直到它们回退并找到新的软件更新点

已有软件更新点的客户端继续使用该点，直到无法连接它为止。 此行为包括继续使用与客户端当前边界组无关联的软件更新点。

此行为是有意为之。 即使现有软件更新点不在客户端的当前边界组中，客户端仍会继续使用它。 当软件更新点发生更改时，客户端会与新服务器同步数据，这会导致占用大量网络。 如果所有客户端同时切换到新服务器，则转换延迟有助于避免网络饱和。

#### <a name="a-client-always-tries-to-reach-its-last-known-good-software-update-point-for-120-minutes-before-starting-fallback"></a>在开始回退之前，客户端在 120 分钟内始终尝试连接其上次已知良好的软件更新点

120 分钟后，如果客户端未建立联系，那么它将开始回退。 开始回退时，客户端在其当前边界组中接收所有软件更新点的列表。 可根据回退配置使用相邻边界组和站点默认边界组中的其他软件更新点。

### <a name="fallback-configurations-for-software-update-points"></a>软件更新点的回退配置

可以将软件更新点的“回退时间(分钟)”配置为小于 120 分钟。 但是，客户端仍试图在 120 分钟内连接其原始软件更新点。 然后，它将搜索范围扩展到其他服务器。 边界组回退时间从客户端第一次无法连接其原始服务器时开始。 当客户端扩展其搜索范围时，站点会提供配置为少于 120 分钟的所有边界组。

若要阻止软件更新点回退到相邻边界组，请将该设置配置为“永不回退”。

如果在两个小时内无法连接到其原始服务器，则客户端使用更短循环建立到新的软件更新点的连接。 此行为使客户端能够快速搜索潜在软件更新点的扩展列表。

#### <a name="example"></a>示例

在边界组 A 中配置软件更新点以便在 10 分钟后回退。 将边界组 B 的相同设置配置为 130 分钟。 边界组 Z 中的客户端无法连接其上次已知良好的软件更新点。

- 在接下来 120 分钟内，客户端尝试仅连接边界组 Z 中的原始服务器。10 分钟后，Configuration Manager 将边界组 A 中的软件更新点添加到可用服务器池。 但是，在最初的 120 分钟时段内，客户端不会尝试联系它们也不会联系任何其他服务器。  

- 尝试在 120 分钟内联系原始软件更新点后，客户端会扩展其搜索范围。 它会将其当前边界组中的服务器以及配置为 120 分钟或更短时间的所有相邻边界组中的服务器添加到可用的软件更新点池中。 池中包括边界组 A 中先前添加到可用服务器池的服务器。  

- 再过 10 分钟后，客户端会扩展搜索范围，以包括边界组 B 的软件更新点。客户端首次连接上次已知良好的软件更新点失败后的总时间为 130 分钟。  

### <a name="manually-switch-to-a-new-software-update-point"></a>手动切换到新的软件更新点

除了使用回退之外，还可以使用“客户端通知”手动强制设备切换到新的软件更新点。

切换到新服务器时，设备使用回退来查找新的服务器。 客户端在下一个软件更新扫描周期中切换到新的软件更新点。<!-- SCCMDocs#1537 -->

请查看边界组配置。 确保软件更新点位于正确的边界组后，再开始进行此更改。

有关详细信息，请参阅[将客户端手动切换到新的软件更新点](../../../../sum/plan-design/plan-for-software-updates.md#BKMK_ManuallySwitchSUPs)。

### <a name="intranet-clients-can-use-a-cmg-software-update-point"></a><a name="bkmk_cmg-sup"></a>Intranet 客户端可以使用 CMG 软件更新点
<!--7102873-->
自版本 2006 起，Intranet 客户端可以访问 CMG 软件更新点，但前提是 Intranet 客户端已分配到边界组，且在软件更新点上[启用了“允许 Configuration Manager 云管理网关流量”选项](../../../clients/manage/cmg/setup-cloud-management-gateway.md#bkmk_role)。 在以下情况下，可以允许 Intranet 设备对 CMG 软件更新点进行扫描：

- Internet 计算机连接到 VPN 时，将继续通过 Internet 对 CMG 软件更新点进行扫描。
- 如果边界组的唯一软件更新点是 CMG 软件更新点，则所有 Intranet 和 Internet 设备将对其进行扫描。

## <a name="management-points"></a>管理点

<!-- 1324594 -->
为边界组之间的管理点配置回退关系。 此行为可以更好地控制客户端使用的管理点。 在边界组属性的“关系”选项卡上，有一个管理点列。 在添加新回退边界组时，当前管理点的回退时间始终为零 (0)。 对于站点默认边界组上的“默认行为”，此行为是相同的。

之前，当安全网络中有一个受保护的管理点时，会出现一个常见问题。 主要网络上的客户端会收到策略，其中包括此受保护的管理点，即使它们无法通过防火墙与管理点进行通信。 若要立即解决此问题，请使用“从不回退”选项，以确保客户端仅回退到它们可以与之通信的管理点。

> [!Note]  
> 如果你在站点默认边界组中启用分发点进行回退，且管理点与分发点位于同一位置，那么站点还会将此管理点添加到站点默认边界组。<!--VSO 2841292-->  

如果客户端在未分配任何管理点的边界组中，站点会向客户端提供管理点的完整列表。 此行为可确保客户端始终收到管理点列表。

在客户端安装 (ccmsetup.exe) 过程中，管理点边界组回退不会更改行为。 如果命令行未使用 /MP 参数指定初始管理点，新的客户端将收到完整的可用管理点列表。 在其初始启动过程中，客户端使用它可以访问的第一个管理点。 一旦客户端注册站点，它便会收到通过此新行为正确排序的管理点列表。

有关客户端在安装期间获取内容的行为的详细信息，请参阅[客户端安装](#bkmk_ccmsetup)。

在客户端升级期间，如果未指定 /MP 命令行参数，客户端会查询诸如 Active Directory 和 WMI 之类的源以获取任何可用的管理点。 客户端升级与边界组配置不匹配。 <!--VSO 2841292-->  

对于要使用此功能的客户端，请启用以下设置：“层次结构设置”中的“客户端首选使用边界组中指定的管理点” 。

> [!Note]  
> 操作系统部署过程不了解管理点的边界组。  

### <a name="troubleshooting"></a>疑难解答

在“LocationServices.log”中出现新条目。 “Locality”属性标识以下状态之一：

- **0**：Unknown  

- **1**：指定的管理点仅位于回退的站点默认边界组中  

- **2**：指定的管理点位于远程或相邻边界组中。 当相邻和站点默认边界组中都存在管理点时，locality 为 2。  

- **3**：指定的管理点位于本地或当前边界组中。 如果当前边界组以及相邻或站点默认边界组中均存在管理点，locality 为 3。 如果在“层次结构设置”中未启用首选管理点设置，locality 始终为 3，而不考虑管理点位于哪个边界组。  

客户端首先使用本地管理点 (locality 3)，第二个为远程管理点 (locality 2)，然后使用回退 (locality 1)。

如果客户端在 10 分钟内收到五个错误，并且无法与当前边界组中的管理点进行通信，它将尝试联系相邻边界组或站点默认边界组中的管理点。 如果当前边界组中的管理点稍后重新联机，客户端将在下一个刷新周期返回到本地管理点。 刷新周期为 24 小时，或当 Configuration Manager 代理服务重新启动时。

## <a name="preferred-management-points"></a><a name="bkmk_preferred"></a> 首选管理点

> [!Note]
> 此层次结构设置的行为（“客户端首选使用边界组中指定的管理点”）在 1802 版中有所变化。 当你启用此设置时，Configuration Manager 会对分配的管理点使用边界组功能。 有关详细信息，请参阅[管理点](#management-points)。

首选管理点使客户端能够识别与当前网络位置（边界）关联的管理点。  

- 客户端先尝试使用已分配站点中的首选管理点，然后再使用已分配站点中未配置为首选的管理点。  

- 若要使用此选项，请在“层次结构设置”中启用“客户端首选使用边界组中指定的管理点”。 然后在各个主站点上配置边界组。 包括应与该边界组的相关边界关联的管理点。 有关详细信息，请参阅[启用对首选管理点的使用](boundary-group-procedures.md#bkmk_proc-prefer)。  

- 如果你配置了首选管理点，客户端在整理其管理点列表时，会将首选管理点放在该列表的顶部。 该列表包含客户端已分配站点中的所有管理点。  

> [!NOTE]  
> 客户端漫游意味着它会更改自己的网络位置。 例如，将笔记本电脑携带到远程办公地点时。 当客户端漫游时，它可能会先使用本地站点中的管理点，然后再尝试使用其已分配站点中的服务器。 由已分配站点中的服务器组成的这个列表中包含首选管理点。 有关详细信息，请参阅[了解客户端如何查找站点资源和服务](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)。  

## <a name="overlapping-boundaries"></a>重叠边界  

Configuration Manager 对于内容位置支持重叠边界配置。 当客户端网络位置属于多个边界组时：

- 当客户端请求内容时，Configuration Manager 向客户端发送包含该内容的所有分发点的列表。  

- 当客户端请求服务器发送或接收其状态迁移信息时，Configuration Manager 向客户端发送与包括客户端当前网络位置的边界组关联的所有状态迁移点的列表。  

此行为使客户端能够选择从中传输内容或站点迁移信息的最近的服务器。  

## <a name="example-of-using-boundary-groups"></a>使用边界组的示例

以下示例使用客户端从分发点进行内容搜索。 此示例可以应用于使用边界组的其他站点系统角色。

创建三个边界组，使其不共享边界或站点系统服务器：  

- 组 BG_A，包含 DP_A1 和 DP_A2 分发点  

- 组 BG_B，包含 DP_B1 和 DP_B2 分发点  

- 组 BG_C，包含 DP_C1 和 DP_C2 分发点  

仅向 BG_A 边界组添加客户端的网络位置作为边界。 然后配置从该边界组到其他两个边界组的关系：  

- 将第一个*相邻*组 (BG_B) 的分发点配置为 10 分钟后使用。 此组包含分发点 DP_B1 和 DP_B2。 这两个分发点都很好地连接到第一组边界位置。  

- 将第二个*相邻*组 (BG_C) 配置为 20 分钟后使用。 此组包含分发点 DP_C1 和 DP_C2。 这两个分发点都从其他两个边界组跨越 WAN。  

- 此外，向默认站点边界组添加站点服务器上的另一个分发点。 此服务器是优先级最低的内容源位置，但它位于所有边界组的中心位置。

    边界组和回退时间的示例：

    ![边界组和回退时间的示例](media/BG_Fallback.png)  

使用该配置：  

- 客户端开始从其*当前*边界组 (BG_A) 中的分发点搜索内容。 每个分发点搜索两分钟，然后切换到边界组中的下一个分发点。 有效的内容源位置的客户端池包括 DP_A1 和 DP_A2。  

- 如果在搜索 10 分钟之后客户端无法从其当前边界组找到内容，然后，它将向它的搜索添加 BG_B 边界组中的分发点。 然后，它继续从合并服务器池的某个分发点中搜索内容。 该池现在包含 BG_A 和 BG_B 边界组中的服务器。 客户端继续对每个分发点进行为时两分钟的访问，然后切换到池中的下一个服务器。 有效的内容源位置的客户端池包括 DP_A1、DP_A2、DP_B1 和 DP_B2。  

- 再过 10 分钟（总共 20 分钟）后，如果客户端仍未在分发点中找到内容，它会对池进行扩展，以便包含第二个相邻组（边界组 BG_C）中的可用服务器。 客户端现在需要搜索 6 个分发点：DP_A1、DP_A2、DP_B2、DP_B2、DP_C1 和 DP_C2。 它继续每隔两分钟切换到一个新的分发点，直到找到内容为止。  

- 如果客户端在总共 120 分钟后还未找到内容，它将回退，以便将默认站点边界组纳入其继续搜索的一部分。 现在，池中包含这三个已配置的边界组中的所有分发点，并且最后一个分发点位于站点服务器上。 然后，客户端继续执行对内容的搜索，并每隔两分钟对分发点进行更改直到找到内容。  

通过将不同的相邻组配置为在不同的时间可用，可控制何时添加特定分发点作为内容源位置。 对于在其他任何位置都找不到的内容，客户端使用回退到默认站点边界组作为其安全保障。

## <a name="changes-from-prior-versions"></a>以前版本中的更改

以下是 Configuration Manager Current Branch 中对边界组以及客户端查找内容的方式的关键更改。 这些更改许多都和概念协同工作。

### <a name="configurations-for-fast-or-slow-are-removed"></a>已删除对于快速或慢速的配置

不能再将单独的分发点配置为快速或慢速。 相反，每个与边界组相关联的站点系统都将视为相同的系统。 由于有此更改，边界组属性的“引用”选项卡不再支持快速或慢速的配置。  

### <a name="new-default-boundary-group-at-each-site"></a>每个站点的新默认边界组

每个主站点都具有一个名为“Default-Site-Boundary-Group&lt;sitecode>”的新默认边界组。 当客户端不在分配给边界组的网络位置时，它会从分配的站点中使用与默认组相关联的站点系统。 计划使用此边界组作为回退内容位置概念的替换。

#### <a name="allow-fallback-source-locations-for-content-is-removed"></a>已删除“允许内容源位置回退”

不能再将分发点显式配置为用于回退。 已从控制台中删除配置此设置的选项。

此外，已更改应用程序部署类型上的**允许客户端使用内容的回退源位置**的设置结果。 部署类型上的此设置现在允许客户端使用默认站点边界组作为内容源位置。

#### <a name="boundary-groups-relationships"></a>边界组关系

可以将每个边界组链接到一个或多个其他边界组。 这些链接就会形成关系，并在名为“关系”的新边界组属性选项卡上进行配置：  

- 客户端直接与之关联的每个边界组都称为**当前**边界组。  

- 由于客户端的当前边界组和另一个组之间存在关联，因此，客户端可以使用的任何边界组都称为“相邻边界组”。  

- 在“关系”选项卡上，添加要用作*相邻*边界组的边界组。 还可以配置回退时间（分钟）。 当客户端在*当前*组的某个分发点中找不到内容时，此时间便作为客户端开始从*相邻*边界组中搜索内容位置的时间。  

    添加或更改边界组配置时，可以阻止从正在配置的当前组回退到该特定的边界组。  

若要使用新配置，请定义从一个边界组到另一个边界组的显式关联（链接）。 以相同的时间（分钟）配置该关联组中的所有分发点。 当客户端在其*当前*边界组中找不到内容源时，配置的时间可确定客户端开始从其相邻边界组搜索内容源的时间。

除了显式配置的边界组外，每个边界组都具有指向默认站点边界组的隐式链接。 该链接在 120 分钟后变为活动状态。 接着，默认站点边界组变为相邻边界组。 此行为允许客户端将与该边界组关联的分发点用作内容源位置。

此行为替换以前称为内容回退的行为。 通过将默认站点边界组显式关联到*当前*组，可覆盖此默认行为（120 分钟）。 设置以分钟为单位的特定时间，或完全阻止使用回退。

### <a name="clients-try-to-get-content-from-each-distribution-point-for-up-to-two-minutes"></a>客户端尝试从每个分发点获取内容，用时长达 2 分钟

客户端搜索内容源位置时，会尝试对每个分发点进行 2 分钟的访问，然后再尝试访问另一个分发点。 此行为与以前版本有所不同，在以前版本中，客户端尝试连接到分发点的时间长达 2 小时。

- 客户端从客户端的一个或多个*当前*边界组中的可用服务器池中随机选择第一个分发点。  

- 两分钟后，如果客户端找不到内容，它将切换到新的分发点并尝试从该服务器获取内容。 每隔两分钟重复此过程，直到客户端找到内容或到达其池中的最后一个服务器。  

- 如果客户端在达到回退至相邻边界组的时段之前无法从当前池中找到有效的内容源位置，客户端就会将该相邻组的分发点添加到当前列表的末尾。 然后，它会搜索扩展的源位置组，其中包含这两个边界组中的分发点。  

    > [!TIP]  
    > 当你创建从当前边界组到默认站点边界组的显式链接，并定义比链接到相邻边界组的回退时间更短的回退时间时，客户端会在添加相邻组之前先从默认站点边界组开始搜索源位置。  

- 客户端无法从池中的最后一个服务器获取内容时，它将再次开始该过程。  

## <a name="see-also"></a>另请参阅

- [边界组的过程](boundary-group-procedures.md)  

- [关于边界](boundaries.md)  

- [内容管理的基本概念](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md)  
