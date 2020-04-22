---
title: 配置分类和产品
titleSuffix: Configuration Manager
description: 按照以下步骤在 Configuration Manager 控制台中配置要同步的软件更新分类和产品。
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 11/18/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 5ddde4e6-d553-4182-b752-6bc8b4a26745
ms.openlocfilehash: 97f25823b20e7cafa7a8f4d9e5f4be84c3e34392
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696935"
---
# <a name="configure-classifications-and-products-to-synchronize"></a>配置要同步的分类和产品  

适用范围：  Configuration Manager (Current Branch)

在 Configuration Manager 中，将根据你在软件更新点组件属性中指定的设置在同步过程期间检索软件更新元数据。 首次同步软件更新后，或者当发布新产品和分类时，必须转到这些属性以选择新项。 使用下列过程来配置要同步的分类和产品。  

> [!NOTE]  
> 请仅在顶层站点上使用本部分中的过程。  

## <a name="to-configure-classifications-and-products-to-synchronize"></a>配置要同步的分类和产品  

1. 在 **Configuration Manager** 控制台中，导航到“管理”   > “站点配置”   > “站点”  。

2. 选择管理中心站点或独立主站点。  

3. 在“主页”  选项卡上的“设置”  组中，单击“配置站点组件”  ，再单击“软件更新点”  。

4. 在“分类”  选项卡上，指定要为其同步软件更新的软件更新分类。  

    每个软件更新都是利用更新分类定义的，此分类能帮助组织不同的更新类型。 同步过程中，将对指定的分类的软件更新元数据进行同步。 Configuration Manager 使你可将软件更新与下列更新分类进行同步：  

     - **关键更新**：指定为特定问题广泛发布的修复，旨在解决与安全无关的关键 bug。  
     - **定义更新**：指定广泛发布且频率较高的软件更新，其中包含对产品的定义数据库的新增内容。  
     - **功能包**：指定新的产品功能，该功能首次在产品版本以外分发，而且通常包含在下一个完整的产品版本中。  
     - **安全更新**：指定一个广泛发布的修复程序，旨在修复特定于产品的安全相关漏洞。  
     - **服务包**：指定一个经过测试、逐渐累积的集合，其中包含所有的修补程序、安全更新、关键更新和应用于某个产品的更新。 此外，服务包可能还包含旨在解决产品发布以来内部发现的问题的其他修补程序。  
     - **工具**：指定可帮助完成一项或多项任务的实用程序或功能。  
     - **更新汇总**：指定为便于部署而一起打包的修补程序、安全更新、关键更新和其他更新的经过测试的累积集合。 更新汇总通常解决特定领域的问题，例如安全性或产品组件问题。  
     - **更新**：指定广泛发布的针对特定问题的修补程序。 更新解决了非关键且与安全无关的 bug。  
     - **升级**：为 Windows 10 特性和功能指定升级。 软件更新点和站点必须运行最低具有[修补程序 3095113](https://support.microsoft.com/kb/3095113) 的 WSUS 6.2 来获取“升级”  分类。 有关安装此更新以及其他“升级”更新的详细信息，请参阅[软件更新的先决条件](../plan-design/prerequisites-for-software-updates.md#BKMK_wsus2012)  。

    > [!NOTE]
    > 可以选中“包括 Microsoft Surface 驱动程序和固件更新”复选框来同步 Microsoft Surface 驱动程序  。<!--1098490--> 有关详细信息，请参阅[包括 Microsoft Surface 驱动程序和固件更新](#bkmk_Surface)一节。

5. 在“产品”  选项卡上，指定要为其同步软件更新的产品，然后单击“关闭”  。  

    - Configuration Manager 存储产品和产品系列的列表，你在初次安装软件更新点时可以从此列表中进行选择。 如果某些产品和产品系列是在发布 Configuration Manager 之后发布的，那么，在完成软件更新同步（这将更新可供你从中进行选择的可用产品和产品系列的列表）之前，可能无法选择它们。  

    - 每个软件更新的元数据都定义了更新适用于的产品。 产品是指特定版本的操作系统或应用程序，例如 Microsoft Windows Server 2012。 产品家族是指从中派生单个产品的基本操作系统或应用程序。 产品系列的示例是 Windows，而 Windows Server 2012 是其成员之一。 可以指定产品系列或产品系列中的各个产品。 选择的产品越多，同步软件更新所需的时间就越长。  

    - 当软件更新适用于多个产品，且至少选中其中一个产品进行同步时，所有产品都将在 Configuration Manager 控制台中显示，即使未选中某些产品也是如此。 例如，Windows Server 2012 是你选择的唯一操作系统，而且软件更新适用于 Windows 8 和 Windows Server 2012，那么，这两个产品都会显示在 Configuration Manager 控制台中。  

    > [!NOTE]  
    > Windows 10 版本 1903 以及更高版本作为独立产品添加到 Microsoft 更新，而不像早期版本那样属于 Windows 10 产品   。 这项更改需要你执行许多手动步骤，才可确保客户端显示这些更新。 我们已采取措施减少了需要手动对 Configuration Manager 版本 1906 中的新产品执行操作的步骤数量。 <!--4682946-->
    >
    > 更新至 Configuration Manager 1906 版，并选择了 Windows 10 产品进行同步后，系统将自动执行以下操作  ：
    > - 已添加 Windows 10 1903 版以及更高版本产品用于进行同步操作  。
    > - 包含 Windows 10 产品的[自动部署规则](../deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process)将更新为包含 Windows 10 1903 版和更高版本   。
    > - [维护服务计划](../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow)将更新为包含 Windows 10 1903 版和更高版本产品  。

## <a name="include-microsoft-surface-drivers-and-firmware-updates"></a><a name="bkmk_Surface"></a> 包括 Microsoft Surface 驱动程序和固件更新

可以选中“包括 Microsoft Surface 驱动程序和固件更新”复选框来同步 Microsoft Surface 驱动程序  。<!--1098490--> 所有软件更新点必须运行安装有累积更新 [KB4025339](https://support.microsoft.com/help/4025339) 的 Windows Server 2016 或更高版本，才能成功同步 Surface 驱动程序。 如果启用 Surface 驱动程序后，在运行 Windows Server 2012 的计算机上启用软件更新点，则驱动程序更新的扫描结果不准确。 这会导致在 Configuration Manager 控制台和 Configuration Manager 报表中显示不正确的符合性数据。  

- 此功能在 1706 版中首次引入，属于[预发行功能](../../core/servers/manage/pre-release-features.md)。 从版本 1710 开始，此功能不再属于预发行功能。  
- 默认情况下，Configuration Manager 不启用此项可选功能。 必须在使用前启用此功能。 有关详细信息，请参阅[启用更新中的可选功能](../../core/servers/manage/install-in-console-updates.md#bkmk_options)。<!--505213-->  
- ARM 设备的驱动程序不支持同步。

## <a name="configuring-products-for-versions-of-windows-10"></a>配置 Windows 10 各版本的产品

### <a name="windows-10-version-1909"></a>Windows 10 版本 1909

Windows 10 版本 1909 与 Windows 10 版本 1903 使用的是同一种常用核心操作系统。 这两个版本都具有相同的累积更新。 有关 Windows 10 版本 1909 的详细信息，请参阅 [Windows 10 版本 1909 分发选项](https://aka.ms/1909mechanics)博客文章。

为确保 Windows 10 版本 1909 和 Windows 10 版本 1903 客户端都是从 Configuration Manager 安装更新，请执行以下操作：

- 为 Windows 10 的 1909 和 1903 版本批准更新。
  - 对于每个 OS 版本，更新具有不同的名称和适用性规则。
  - 按 OS 的版本和体系结构批准每个更新可维持管理员的正常批准流程。
- Windows 10 的 1909 和 1903 版本的累积更新安装文件相同。
  - Configuration Manager 将只会下载一次更新源文件。

#### <a name="feature-updates-for-windows-10-version-1909"></a>Windows 10 版本 1909 的功能更新

批准 Windows 10 版本 1909 的功能更新时，会看到多个不同选项：

- Windows 10 版本 1903 客户端可使用 2019 年 11 月 12 日发布的[启用包](https://support.microsoft.com/en-us/help/4517245/feature-update-via-windows-10-version-1909-enablement-package)。
  - 启用包是可快速安装的小型文件，用于激活 Windows 10 版本 1909 功能和重启设备。
  - 启用包的先决条件包括以下内容：
    - 2019 年 10 月 8 日发布的最小累积更新 [KB4517389](https://www.catalog.update.microsoft.com/Search.aspx?q=KB4517389)。
    - 2019 年 9 月 24 日发布的最小服务堆栈更新 [KB4520390](https://www.catalog.update.microsoft.com/Search.aspx?q=KB4520390)。
  - 此更新与其他任何功能更新一样，无法从 `https:\\catalog.update.microsoft.com` 导入。
  - 如果选中“Windows 10 版本 1903 和更高版本”产品和“升级”分类进行同步，更新将自动与 WSUS 同步   。
  - 在 Configuration Manager 控制台中，转到“软件库”工作区，展开“Windows 10 维护服务”，然后选择“全部 Windows 10 更新”节点    。 搜索术语“enablement”或“4517245”。

    > [!TIP]
    > 由于这些是功能更新，因此它们不在“全部软件更新”节点中  。

- Windows 10 版本 1809 和更低版本的客户端通过单一直接功能更新进行升级。
  - 这与之前在 Windows 10 中完成的其他所有功能更新安装一样。

> [!NOTE]
> 无论使用哪个路径进行安装，Windows 10 版本 1909 的启用包和惯用功能更新都将在报表中显示为“已安装”。

### <a name="windows-10-version-1903-and-later"></a>Windows 10 版本 1903 及更高版本

Windows 10 1903 版以及更高版本都已经作为其自身产品添加到 Microsoft 更新中，而不像早期版本那样作为 Windows 10 产品的一部分进行添加   。 这项更改需要你执行许多手动步骤，才可确保客户端显示这些更新。 我们已采取措施减少了需要手动对 Configuration Manager 版本 1906 中的新产品执行操作的步骤数量。 <!--4682946-->

#### <a name="windows-10-version-1903-and-later-with-configuration-manager-version-1906"></a>Windows 10 版本 1903 和更高版本以及 Configuration Manager 版本 1906
更新至 Configuration Manager 1906 版，并选择了 Windows 10 产品进行同步后，系统将自动执行以下操作  ：
- 已添加 Windows 10 1903 版以及更高版本产品用于进行同步操作  。
- 包含 Windows 10 产品的[自动部署规则](../deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process)将更新为包含 Windows 10 1903 版和更高版本   。
- [维护服务计划](../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow)将更新为包含 Windows 10 1903 版和更高版本产品  。

#### <a name="windows-10-version-1903-and-later-with-configuration-manager-version-1902"></a>Windows 10 版本 1903 和更高版本以及 Configuration Manager 版本 1902
如果使用的是 Windows 10 版本 1903 客户端以及 Configuration Manager 1902，则需要：
- 选择 Windows 10 1903 版以及更高版本产品用于进行同步操作  。
- 更新 Windows 10 版本 1903 客户端的所有[自动部署规则](../deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process)。
- 更新 Windows 10 版本 1903 客户端的[维护服务计划](../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow)。

## <a name="windows-insider-program"></a><a name="bkmk_WIfB"></a> Windows 预览体验计划
<!--3556023-->
从 2019 年 9 月起，你可以通过 Configuration Manager 来维护和更新运行 Windows Insider Preview 内部版本的设备。 此更改意味着，你可以管理这些设备，而无需更改正常流程或启用适用于企业的 Windows 更新。 像对待任何其他 Windows 10 更新或升级一样，你可以将 Windows Insider Preview 内部版本的功能更新和累积更新下载到 Configuration Manager。 有关详细信息，请参阅[将预发行 Windows 10 功能更新发布到 WSUS](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/Publishing-pre-release-Windows-10-feature-updates-to-WSUS/ba-p/845054) 博客文章。

若要详细了解对 Configuration Manager 中 Windows 预览体验计划的支持，请参阅[对 Windows 10 的支持](../../core/plan-design/configs/support-for-windows-10.md#bkmk_WIfB-support)。

### <a name="prerequisites"></a>必备条件

- 为[软件更新管理](../plan-design/plan-for-software-updates.md)配置的 Configuration Manager 版本 1906 或更高版本。
- 运行 [Windows 预览体验计划预览版版本](https://docs.microsoft.com/windows-insider/at-work-pro/wip-4-biz-get-started)的 Windows 10 设备。
- 包含 Windows 预览体验计划设备的集合。

### <a name="enable-windows-insider-upgrades-and-updates"></a>启用 Windows 预览体验计划升级和更新

需要为 Windows 预览体验计划升级和更新启用产品和分类。 Windows 预览体验计划的功能更新、累积更新和其他更新位于 Windows 预览体验计划预发行版产品类别中  。

1. 在 **Configuration Manager** 控制台中，导航到“管理”   > “站点配置”   > “站点”  。
2. 选择管理中心站点或独立主站点。  
3. 在“主页”  选项卡上的“设置”  组中，单击“配置站点组件”  ，再单击“软件更新点”  。
4. 在“产品”选项卡中，确保选中以下产品进行同步  ：
    - Windows 预览体验计划预发行版
    - Windows 10 版本 1903 及更高版本
5. 在“分类”选项卡中，确保选中以下分类进行同步  ：
    - 升级
    - 安全更新
    - 更新（可选）
6. 单击“确定”  关闭“软件更新点组件属性”  。

### <a name="upgrading-windows-insider-devices"></a>升级 Windows 预览体验计划设备

同步 Windows 预览体验计划的升级后，可以在“软件库” > “Windows 10 维护服务” > 全部 Windows 10 更新”中进行查看    。

![Windows 10 维护服务的 Windows 预览体验计划功能更新](media/3556023-windows-insiders-pre-release-feature-update.png)

与其他任何升级一样，将 Windows 预览体验计划的功能更新部署到目标集合。 但部署这些功能更新时，建议记住以下项：

- 这些升级将适用于所有具有相匹配体系结构、版本和语言的 Windows 10 客户端 1903 或更低版本。
- 存在许可条款，部署时必须接受条款才能安装。
- 请考虑使用[客户端设置中的线程优先级](../../core/clients/deploy/about-client-settings.md#bkmk_thread-priority)。
- 动态更新会直接通过 Microsoft 更新自动安装最新累积更新等关键更新。 此行为始于 Windows 10 版本 1903 的功能更新。 
  - 可以显式[禁用客户端设置中的动态更新](../../core/clients/deploy/about-client-settings.md#bkmk_du)或采用 [setupconfig.ini 文件](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options)。 
  - 有关详细信息，请参阅 [Windows 10 动态更新](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/The-benefits-of-Windows-10-Dynamic-Update/ba-p/467847)博客文章。

有关如何部署升级的详细信息，请参阅[管理 Windows 即服务](../../osd/deploy-use/manage-windows-as-a-service.md)。


### <a name="keeping-insider-devices-up-to-date"></a>使预览体验成员设备保持最新

Windows 预览体验计划的累积更新将可适用于 WSUS，经扩展后可适用于 Configuration Manager。 这些累积更新的发布频率与 Windows 10 版本 1903 累积更新的发布频率相似。 Windows 预览体验计划累积更新位于“Windows 预览体验计划预发行版”产品类别中，并归类为“安全更新程序”或“更新”    。 可以按常规软件更新流程（如按[自动部署规则](../deploy-use/automatically-deploy-software-updates.md)或[分阶段部署](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json)）部署 Windows 预览体验计划的累积更新。

## <a name="extended-security-updates-and-configuration-manager"></a><a name="bkmk_ESU"></a> 扩展的安全更新和 Configuration Manager

如果客户需要运行某些已停止支持的 Microsoft 旧产品，[扩展的安全更新 (ESU)](https://support.microsoft.com/help/4497181/lifecycle-faq-extended-security-updates) 计划则是他们的终极选项。 它包括关键和/或重要安全更新（根据 [Microsoft 安全响应中心 (MSRC)](https://www.microsoft.com/msrc) 的定义），并且在超出产品的外延支持结束日期后最多可保存三年。

不支持将超出其支持生命周期的产品与 Configuration Manager 一起使用。 它包括 ESU 计划包含的所有产品。 例如，Windows 7。 通过 ESU 计划发布的安全更新将发布到 Windows Server Update Services (WSUS)。 这些更新将在 Configuration Manager 控制台中显示。 尽管不再支持将 ESU 计划包含的产品与 Configuration Manager 一起使用，但仍可使用 [Configuration Manager 当前分支的最新版本](../../core/servers/manage/updates.md#version-details)部署并安装通过此计划发布的 Windows 安全更新。 最新发行版还可用于将 Windows 10 部署到运行 Windows 7 的设备。

将不再在 ESU 计划包含的操作系统上测试与 Windows 软件更新管理或 OS 部署无关的客户端管理功能，并且不保证它们会继续工作。 强烈建议尽快升级或迁移到操作系统的最新版本，以获得客户端管理支持。


## <a name="next-steps"></a>后续步骤

启动软件更新同步以根据新条件检索软件更新。 有关详细信息，请参阅[同步软件更新](synchronize-software-updates.md)。
