---
title: 配置预先缓存内容
titleSuffix: Configuration Manager
description: 了解客户端如何在用户安装任务序列之前下载 OS 部署内容。
ms.date: 02/26/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 9d1e8252-99e3-48aa-bfa5-0cf4cd6637b2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cf312d1bc706ace1336caed26f3ee31f81abeaa2
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125659"
---
# <a name="configure-pre-cache-content-for-task-sequences"></a>配置任务序列的预先缓存内容

适用范围：Configuration Manager (Current Branch)

<!--1021244-->
对于任务序列的可用部署，可使用预先缓存功能让客户端在用户安装任务序列之前下载相关内容。 客户端可以预先缓存[升级 OS](create-a-task-sequence-to-upgrade-an-operating-system.md) 或[安装 OS 映像](create-a-task-sequence-to-install-an-operating-system.md)的任务序列的内容。

> [!Note]  
> 在版本 1910 中，Configuration Manager 默认启用此功能。 在版本 1906 或更早版本中，Configuration Manager 默认不启用此项可选功能。 必须在使用前启用此功能。 有关详细信息，请参阅[启用更新中的可选功能](../../core/servers/manage/install-in-console-updates.md#bkmk_options)。<!--505213-->  

例如，仅需为所有用户提供就地升级任务序列，并拥有许多体系结构和语言。 在以前的版本中，当用户从软件中心安装可用的任务序列部署时，就会开始下载内容。 此延迟在安装准备启动之前增加了额外时间。 将下载任务序列中引用的所有内容。 此内容包括所有语言和体系结构的 OS 升级包。 如果每个升级包的大小约 3 GB，总内容会非常大。

借助预先缓存内容，可选择让客户端在收到部署后仅下载适用的内容以及引用的所有其他内容。 在用户单击软件中心内的“安装”时，内容便准备就绪。 安装可以快速启动，因为内容位于本地硬盘上。

在 Configuration Manager 版本 1902 及更低版本中，此行为仅适用于 OS 升级包。 该包是你指定匹配体系结构或语言的唯一内容。 例如，如果任务序列还引用多个驱动程序包，则客户端会下载所有驱动程序包。 任务序列引擎在运行任务序列时（而不是提前）评估步骤条件。 客户端使用包属性上的标记来确定要预缓存的内容。

从版本 1906 开始，<!--4224642--> 可以使用预先缓存来减少以下内容类型的带宽消耗：

- OS 升级包
- OS 映像
- 驱动程序包
- 包

## <a name="configure-pre-caching"></a>配置预先缓存

可通过三个步骤配置预先缓存功能：

1. [创建和配置包](#bkmk_createpkg)
2. [使用条件步骤创建任务序列](#bkmk_createts)
3. [部署任务序列并启用预先缓存](#bkmk_deploy)


### <a name="1-create-and-configure-the-packages"></a><a name="bkmk_createpkg"></a> 1.创建和配置包

客户端可评估包的特性，以确定其在预先缓存过程中下载的内容。  

#### <a name="os-upgrade-package"></a>OS 升级包

创建特定体系结构和语言的 [OS 升级包](../get-started/manage-operating-system-upgrade-packages.md)。 在包属性的“数据源”选项卡上指定“体系结构”和“语言”。

#### <a name="os-image"></a>OS 映像

创建特定体系结构和语言的 [OS 映像](../get-started/manage-operating-system-images.md)。 在包属性的“数据源”选项卡上指定“体系结构”和“语言”。

#### <a name="driver-package"></a>驱动程序包

创建特定硬件模型的[驱动程序包](../get-started/manage-drivers.md#BKMK_ManagingDriverPackages)。 在包属性的“常规”选项卡上指定“模型” 。

为了确定在预缓存期间下载哪个驱动程序包，客户端根据 Win32_ComputerSystemProduct WMI 类的“名称”属性评估模型。 

> [!TIP]
> 实际查询使用带有通配符的 `LIKE` 语句：`select * from win32_computersystemproduct where name like "%yourstring%"`。 例如，如果将 `Surface` 指定为模型，则查询可与包含该字符串的所有模型匹配。<!-- 6315551 -->

#### <a name="package"></a>包

创建特定体系结构和语言的[包](../../apps/deploy-use/packages-and-programs.md)。 在包属性的“常规”选项卡上指定“体系结构”和“语言”。


### <a name="2-create-a-task-sequence"></a><a name="bkmk_createts"></a> 2.创建任务序列

为不同的语言和体系结构或驱动程序包的不同硬件型号创建具有条件步骤的任务序列。

|Content|步骤|
|---------|---------|
|OS 升级包|[升级 OS](../understand/task-sequence-steps.md#BKMK_UpgradeOS)|
|OS 映像|[应用 OS 映像](../understand/task-sequence-steps.md#BKMK_ApplyOperatingSystemImage)|
|驱动程序包|[应用驱动程序包](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage)|
|包|[安装包](../understand/task-sequence-steps.md#BKMK_InstallPackage)|

例如，以下“升级 OS”步骤使用英语版本：  

![显示 ENU、DEU 和 JPN 的多个升级 OS 步骤的任务序列编辑器](../media/precacheproperties2.png)

![任务序列编辑器，“选项”选项卡，显示区域设置和 OSArchitecture 的 WMI WQL 查询](../media/precacheoptions2.png)  

> [!Tip]
> 建议为英语（美国）OS 和 64 位体系结构使用以下 WMI 查询：
>
> ```WMI
> SELECT * FROM Win32_OperatingSystem WHERE OSArchitecture LIKE '%64%' AND OSLanguage='1033'
> ```
>
> 首先，通过选择“操作系统语言”条件来添加语言。 然后编辑 WMI 查询以包括体系结构子句。

### <a name="3-deploy-the-task-sequence"></a><a name="bkmk_deploy"></a> 3.部署任务序列

[部署任务序列](deploy-a-task-sequence.md)。 对于预先缓存功能，请配置以下设置：  

- 在“常规”选项卡上，选择“此任务序列的预下载内容”。  

- 在“部署设置”选项卡上，将任务序列配置为“可用” 。  

- 在“计划”选项卡上的“当此部署可用时进行计划”设置处，选择当前所选时间 。 客户端在部署的可用时间预先缓存内容。 目标客户端收到此策略时，可用时间是过去的时间，因此预先缓存下载会立即开始。 如果客户端收到此策略，但可用时间是将来的时间，则客户端在可用时间之前不会开始预先缓存内容。  

- 在“分发点”选项卡上，配置“部署选项”设置。 如果用户开始安装前没有预先缓存内容，则客户端使用这些设置。  

    > [!Important]  
    > 对于安装 OS 映像的任务序列，请不要使用部署选项“运行中的任务序列需要时，从本地下载内容”。 当任务序列在应用 OS 映像之前擦除磁盘时，会删除客户端缓存。 由于内容已消失，任务序列失败。<!-- SCCMDocs-PR #1338 --> 这些部署选项是动态的，基于你为部署选择的其他选项。 有关详细信息，请参阅 [Deploy a task sequence](deploy-a-task-sequence.md#bkmk_deploy-options)。<!-- MEMDocs#328, SCCMDocs#2114 -->

## <a name="user-experience"></a>用户体验

- 客户端收到部署策略时，将在部署的可用时间之后开始预缓存内容。 此内容包含引用的所有包，但仅包含与包上的体系结构和语言属性相匹配的 OS 升级包。  

- 当客户端使部署可供用户使用时，将显示一条通知，告知用户有关新部署的信息。 现在，任务序列在软件中心内可见。 用户可转到软件中心并单击“安装”以开始安装。  

- 如果用户安装任务序列时客户端没有完全预先缓存内容，则客户端使用部署的“部署选项”选项卡上指定的设置。  

## <a name="see-also"></a>另请参阅

- [创建用于升级 OS 的任务序列](create-a-task-sequence-to-upgrade-an-operating-system.md)
- [将 Windows 升级到最新版本的方案](upgrade-windows-to-the-latest-version.md)
