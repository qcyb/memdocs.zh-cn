---
title: 管理发布内容
titleSuffix: Configuration Manager
description: 使用 System Center Updates Publisher 将各组软件更新作为发布项进行管理
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: e6c1df1d-7728-4980-9199-bc32cde5439e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0b79e0ec67fa7c1d7ede0af1549c8cda4dd3ee3c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700035"
---
# <a name="manage-publications-in-updates-publisher"></a>管理 Updates Publisher 中的发布项

适用范围：  System Center Updates Publisher

可以使用发布项将各组更新和捆绑包作为一个对象进行管理。 这包括将更新发布到管理服务器，以及将发布项导出为组，以供其他 Updates Publisher 安装项使用。

## <a name="create-publications"></a>创建发布项
发布项的创建方式有两种：

-   在“更新工作区”  中管理更新和捆绑包时，可以将它们[分配](manage-updates-with-updates-publisher.md#assign-updates-and-bundles-to-a-publication)给同一时间创建的新发布项。

-   在“发布项工作区”  中，可以使用功能区中“发布项”  选项卡上的“创建”  按钮。 使用这种方法创建的发布项可供将来使用。 稍后，可以在分配更新时使用此发布项。

## <a name="rename-a-publication"></a>重命名发布项
若要重命名发布项，请从“发布项工作区”  中选择发布项，然后在功能区的“发布项”  选项卡上，选择“编辑”  。

## <a name="change-the-publication-type-of-updates-in-a-publication"></a>在发布项中更改更新的发布项类别
在“发布项工作区”  中，可以修改分配给发布项的更新和捆绑包的**发布项类型**。

1. 选择包含要修改的更新的发布项，然后在“全部 &lt;发布项名称> 成员更新”  列表中选择一个或多个更新或捆绑包。

2. 接下来，在“开始”  选项卡上，选择以下任一选项。 可用选项因已选择的更新的发布项类型而异。

   -   **自动**
   -   **完整内容**
   -   **仅元数据**

更改后，可能需要刷新发布项视图，才能看到新值。

若要了解不同的发布项类型，请参阅[将更新和捆绑包分配给发布项](manage-updates-with-updates-publisher.md#assign-updates-and-bundles-to-a-publication)。

> [!TIP]    
> 设置捆绑包的发布项类型后，捆绑包中的所有软件更新都会使用此捆绑包的发布项类型进行发布。

## <a name="remove-updates-from-a-publication"></a>删除发布项中的更新
若要删除发布项中的更新或捆绑包，请在“发布项工作区”  中选择要修改的发布项，然后选择要删除的更新和捆绑包。 接下来，从功能区的“开始”  选项卡中，选择“删除”  。

从发布项中删除的更新在 Updates Publisher 存储库中仍有。

## <a name="publish-publications"></a>发布发布项
发布更新和捆绑包时，Updates Publisher 会向更新服务器添加这些更新和捆绑包的相关信息（元数据），可能还会添加更新的二进制文件（完整内容），以供部署到设备。

必须先为 Updates Publisher 配置[“更新服务器”](updates-publisher-options.md#update-server)选项，然后才能进行发布。 若要打开此配置选项，请依次转到“更新工作区”  &gt;“概述”  ，然后选择“配置 WSUS 和签名证书”  。 还可以转到 Updates Publisher 选项的“更新服务器”页。

> [!NOTE]   
> Updates Publisher 只能发布大小不超过 375 MB 的更新。

### <a name="to-publish-a-publication"></a>如何发布发布项

1. 转到“发布项工作区”  ，选择包含要发布或导出的一组更新或捆绑包的发布项。 然后，从功能区的“开始”  选项卡中，选择“发布” 

2. 在“发布”  向导的“选择”  页中，可以选择使用新的发布证书对所有更新进行签名，但不能更改发布项类型。

3. 完成向导。

   如果发布失败，将会看到指向 UpdatesPublisher.log 文件的链接，其中介绍了详细信息。

## <a name="export-a-publication"></a>导出发布项
可以从 Updates Publisher 存储库中导出发布项。 这样可以导出分配给相应发布项的更新和捆绑包，并创建更新目录。 然后，可以[添加](updates-publisher-catalogs.md#add-software-update-catalogs)目录，并将其[导入](updates-publisher-catalogs.md#import-updates)其他 Updates Publisher 实例。 还可以[导出](manage-updates-with-updates-publisher.md#export-updates)不属于发布项的更新。

若要导出发布项，请转到“发布项工作区”  ，然后选择包含要导出的更新的发布项。 一次只能选择一个发布项。

选择发布项后，从功能区的“开始”  选项卡中选择“导出”  ，然后提供目录导出的路径和文件名。

还可以视需要导出（添加）从属软件更新。

## <a name="rename-a-publication"></a>重命名发布项
若要重命名发布项，请从“发布项工作区”  中选择发布项，然后在功能区的“发布项”  选项卡上，选择“编辑”  。

## <a name="delete-a-publication"></a>删除发布项
若要删除发布项，请从“发布项工作区”  中选择发布项，然后在功能区的“发布项”  选项卡上，选择“删除”  。

从 Updates Publisher 中删除的发布项中的更新在 Updates Publisher 存储库中仍有。

## <a name="expire-or-reactivate-updates-and-bundles"></a>终止或重新激活更新和捆绑包
可以使用“更新工作区”  选择并终止或重新激活更新和捆绑包。 可以根据需要多次终止和重新激活更新和捆绑包。

-   **若要终止更新或捆绑包**，请在“更新工作区”中选择一个或多个未终止的更新或捆绑包，然后在“开始”  选项卡中选择“终止”  。将更新或捆绑包的终止状态发布到 Configuration Manager 中之前，都可以重新激活。

    必须先终止自定义更新或捆绑包，并将其终止状态发布到 Configuration Manager 中，然后才能将其从 Configuration Manager 中删除。 当更新或捆绑包的终止状态发布到 Configuration Manager 中后，便无法再部署或重新激活更新或捆绑包。

-   **若要重新激活更新或捆绑包**，请在“更新工作区”中选择一个或多个已终止的更新或捆绑包，然后在“开始”  选项卡中选择“重新激活”  。 如果之前已将已终止更新的终止状态发布到 Configuration Manager 中，则无法重新激活。
