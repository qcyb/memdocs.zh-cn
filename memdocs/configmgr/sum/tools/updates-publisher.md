---
title: 更新发布服务器
titleSuffix: Configuration Manager
description: 使用 System Center Updates Publisher 管理自定义更新
ms.date: 11/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 2200b02b-e76b-4aa7-a77a-6dc5e70f1333
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: dc1e662eb8eca4740e70743d0971e2d65410f3f2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700025"
---
# <a name="system-center-updates-publisher"></a>System Center Updates Publisher

适用范围：  System Center Updates Publisher

System Center Updates Publisher (Updates Publisher) 是一款独立工具，可方便独立软件供应商或业务线应用程序开发者管理自定义更新。 此自定义更新管理包括具有依赖项的更新，例如驱动程序和更新捆绑包。

使用 Updates Publisher，可以执行下列操作：

-   导入外部目录（非 Microsoft 更新目录）中的更新。
-   修改更新定义（包括适用性和部署元数据）。
-   将更新导出到外部目录中。
-   将更新发布到更新服务器。

将更新发布到更新服务器后，可以使用 Configuration Manager 检测这些更新，并将其部署到受管理设备中。

## <a name="workspaces"></a>工作区
打开 Updates Publisher 时，默认打开的是“更新工作区”  的“概述”节点。

![Updates Publisher 控制台](media/console1.png)


Updates Publisher 有四个工作区，可方便整理。


**更新工作区：** 使用此工作区可[创建](create-updates-with-updates-publisher.md)和[管理](manage-updates-with-updates-publisher.md)软件更新和更新捆绑包。 在此工作区中，可以将更新和捆绑包分配给发布项、发布它们，并能将它们导出到另一个 Updates Publisher 存储库中。

**发布项工作区：** 可以在此工作区中[管理发布项](updates-publisher-publications.md)。 发布项是创建的一组更新，以便于简化更新的导出和发布。

管理发布项包括将更新发布到服务器以便客户端能够查找和安装更新、导出更新和捆绑包以供其他 Updates Publisher 安装项使用，或修改发布项的内容或详细信息。

**规则工作区：** 可以在其中[管理适用性规则](updates-publisher-applicability-rules.md)，此类规则可以进行保存，随后与部署的更新结合使用。 规则分为两种类型：

-   可安装规则 - 此类规则有助于确定客户端是否应安装更新。
-   已安装规则 - 此类规则可验证更新是否已安装。

**目录工作区：** 使用此工作区可添加和[管理软件更新目录](updates-publisher-catalogs.md)。 在此工作区中，可以将目录中的软件更新导入 Updates Publisher 存储库。

## <a name="whats-new-in-system-center-updates-publisher"></a>System Center Updates Publisher 中的新增功能

>[!NOTE] 
> System Center Updates Publisher 的最新版本于 2019 年 11 月 6 日发布。 有关详细信息，请参阅[发布历史记录](#release-history)部分。

有一个新的创作模式 System Center Updates Publisher 可帮助你创作更新。 启用创作模式后，“类别工作区”将添加到开始屏幕  。 启用创作模式后，“更新工作区”中也会添加一个新的“Detectoid”按钮   。

### <a name="to-enable-authoring-mode"></a>启用创作模式

1. 在控制台的左上角，单击 Updates Publisher 的“属性”选项卡，然后选择“选项”    。
1. 转到“创作”选项  。
1. 选中“启用创作模式”的复选框  。

![为 Updates Publisher 启用创作模式](media/scup-enable-authoring-mode.png)

### <a name="about-the-categories-workspace"></a>关于类别工作区

通过类别工作区，更新作者可使类别相同的更新保持井然有序。 例如，如果你是原始设备制造商 (OEM)，则你可能想要根据模型或产品线来整理更新。 你可定义多个类别和子类别，但不能定义孙类别，因为你只能定义两个级别。

![类别工作区的屏幕截图](media/scup-categories-workspace.png)

### <a name="assign-an-update-to-a-category"></a>为更新划分类别

创作更新后，可选择该更新，再单击“分类”按钮来将它分配给某个类别  。 你也可右键单击该更新，然后选择“类别”  。

![对更新进行分类的屏幕截图](media/scup-categorize-update.png)

### <a name="about-detectoids"></a>关于 detectoid

启用创作模式后，可创建更新的 detectoid。 当有多个更新使用同一规则（或一组规则）来确定适用性时，detectoid 非常有用。 在这些情况下，你将创建一个 detectoid，并将它分配为更新的必备项。 可向创作的更新分配多个 detectoid。


### <a name="create-a-detectoid"></a>创建 detectoid

1. 打开“更新工作区”  。
1. 在功能区中，单击“Detectoid”按钮  。
1. 按照向导中的提示创建 detectoid。



![使用 detectoid 更新必备项](media/scup-detectoid-as-prerequisite.png)

## <a name="release-history"></a>版本历史记录

- [2019 RTW 版本 6.0.394.0](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/SCUP-adds-support-for-update-categories/ba-p/990111)。 发布于 2019 年 11 月 6 日
- [从 KB4462765 更新汇总版本 6.0.283.0](https://support.microsoft.com/help/4462765/update-rollup-for-system-center-updates-publisher)。 发布于 2018 年 9 月 7 日。
- [2017 RTW 版本 6.0.276.0](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/System-Center-Updates-Publisher-adds-support-for-new-OSes/ba-p/274986)。 发布于 2018 年 3 月 26 日。


## <a name="next-steps"></a>后续步骤
首先进行[安装](install-updates-publisher.md)，然后为 Updates Publisher [配置选项](updates-publisher-options.md)。
