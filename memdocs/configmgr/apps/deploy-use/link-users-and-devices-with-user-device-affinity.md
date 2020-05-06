---
title: 将用户和设备与用户设备相关性相链接
titleSuffix: Configuration Manager
description: 将用户和设备与用户设备相关性相链接，并自动将应用部署到与用户关联的所有设备。
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 5b30b0d5-722d-4d4b-9ed7-5a43de315461
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2e74f969016d79254ceb8e8323b6e3914969ecc7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689265"
---
# <a name="link-users-and-devices-with-user-device-affinity-in-configuration-manager"></a>在 Configuration Manager 中将用户和设备与用户设备相关性相链接

适用范围：  Configuration Manager (Current Branch)

Configuration Manager 中的用户设备相关性将一个用户与一个或多个设备关联。 利用此行为，在将应用程序部署到某用户时无需知道该用户的设备名称。 你将应用程序部署到该用户，而不是部署到该用户的每个设备。 之后，用户设备相关性会自动确保在所有与该用户关联的设备上安装应用程序。  

定义用户每天用于工作的主要设备。 当在用户和设备之间创建相关性时，你会获得更多的软件部署选项。 例如，某用户需要 Microsoft Visio，那么，你可以使用 Windows Installer 部署将它安装在该用户的主要设备上。 但是，在不是主要设备的设备上，可能要将 Visio 部署为虚拟应用程序。 你也可在用户未登录时使用用户设备相关性在用户设备上预部署软件。 然后，当用户登录时，应用已安装并准备好运行。  

仅管理计算机的用户设备相关性信息。 Configuration Manager 会自动为它注册的移动设备管理用户设备相关性。  

## <a name="manually-set-up-user-device-affinity"></a>手动设置用户设备相关性  

1. 在 Configuration Manager 控制台中，转到“资产和符合性”工作区，并选择“设备”节点   。  

1. 选择设备。 在功能区的“主页”  选项卡上的“设备”  组中，选择“编辑主要用户”  。  

1. 在“编辑主要用户”  对话框中，搜索并选择要添加为所选设备的主要用户的用户。 选择“添加”  。  

    > [!NOTE]  
    > “主要用户”  列表显示已成为此设备的主要用户的用户，以及使用了哪种方法来指定每项用户 - 设备关系。  

## <a name="set-up-primary-devices-for-a-user"></a>设置用户的主要设备  

1. 在 Configuration Manager 控制台中，转到“资产和符合性”工作区，然后选择“用户”节点   。  

1. 选择用户。 在功能区的“设备”  选项卡中，选择“编辑主要设备”  。  

1. 在“编辑主要设备”  对话框中，搜索并选择要添加为所选用户的主要设备的设备。 选择“添加”  。  

    > [!NOTE]  
    > “主要设备”  列表显示已设置为此用户的主要设备的设备，以及使用了哪种方法来指定每项用户-设备关系。  

## <a name="automatically-create-user-device-affinities-windows-pcs-only"></a>自动创建用户设备相关性（仅针对 Windows PC）

Configuration Manager 从 Windows 事件日志中读取有关用户登录事件的数据。 若要自动创建用户设备相关性，请在客户端计算机上启用本地安全策略中的这两个选项，以便将登录事件存储在 Windows 事件日志中：  

- **审核帐户登录事件**  
- **审核登录事件**  

要配置这些设置，请使用 Windows 组策略。  

> [!IMPORTANT]  
> 如果错误导致 Windows 事件日志生成大量条目，则可能将创建新的事件日志。 如果出现此行为，现有的登录事件可能无法供 Configuration Manager 使用。  

### <a name="set-up-the-site-to-automatically-create-user-device-affinities"></a>将站点设置为自动创建用户设备相关性  

1. 在 Configuration Manager 控制台中，转到“管理”  工作区，然后选择“客户端设置”  节点。  

1. 若要修改默认客户端设置，请选择“默认客户端设置”  。 在功能区的“主页”选项卡上的“属性”组中，选择“属性”    。

    若要创建自定义客户端代理设置，请在功能区的“主页”  选项卡上，选择“创建”  组中的“创建自定义客户端设备设置”  。

    > [!NOTE]  
    > 如果修改默认的客户端设置，则站点会将它们部署到层次结构中的所有计算机。 有关详细信息，请参阅[如何配置客户端设置](../../core/clients/deploy/configure-client-settings.md)。  

1. 在“用户和设备相关性”  组中，设置以下设置：  

    - 用户设备相关性阈值(分钟)  ：设置在站点创建用户设备相关性前设备的使用分钟数。  

    - **用户设备相关性阈值(天)** ：设置网站测量的基于使用情况的相关性阈值的天数。  

    - 利用使用情况数据自动配置用户设备相关性  ：选择“True”  可允许站点自动创建用户设备相关性。 如果选择“假”  ，则你必须手动批准所有的用户设备相关性分配。  

    > [!TIP]  
    > 例如，如果将“用户设备相关性阈值(分钟)”  指定为 60  分钟，并将“用户设备相关性阈值(天)”  指定为 5  天，那么，用户必须在 5 天内使用设备至少 60 分钟，才能自动创建用户设备相关性。  

在 Configuration Manager 自动创建用户设备相关性之后，会继续监视用户设备相关性阈值。 如果用户使用设备的时间降到所设置的阈值以下，则站点将删除用户设备相关性。 将“用户设备相关性阈值(天)”  设置为不少于 7 天的值。 这种配置避免了以下情况：在用户未登录期间（例如周末）自动配置的用户设备相关性可能会丢失。  


## <a name="import-user-device-affinities-from-a-file"></a>从文件导入用户设备相关性

若要一次创建许多关系，请导入具有多个用户设备相关性详细信息的文件。 请确保目标设备已由站点发现，且以资源形式存在于 Configuration Manager 数据库中。  

1. 在 Configuration Manager 控制台中，转到“资产和符合性”工作区，然后选择“用户”或“设备”节点    。  

1. 在功能区的“主页”  选项卡上的“创建”  组中，选择“导入用户设备相关性”  。  

1. 在“导入用户设备相关性向导”的“选择映射”  页上，设置下列信息：  

    - **文件名**。 指定逗号分隔值 (CSV) 文件，该文件包含要创建用户设备相关性的用户和设备的列表。 在该文件中，每个用户和设备对都必须位于各自的行中，其值由逗号分隔。 使用此格式：`<domain>\<username>,<device NetBIOS name>`  

    - **此文件有供参考的列标题**。 如果 .csv 文件有首行标题，请选择此选项。 站点在导入期间忽略标题行。  

1. 如果导入的文件在每行上包含两个以上的项目，则使用“列”  和“分配”  来指定哪些列代表用户和设备，以及在导入过程中要忽略哪些列。  

1. 完成向导。  


## <a name="let-users-create-their-own-device-affinities"></a>让用户创建自己的设备相关性

将用户设置为在软件中心内创建自己的用户设备相关性。

### <a name="set-up-the-site-to-allow-user-created-user-device-affinity-requests"></a>将站点设置为允许用户创建的用户设备相关性请求  

1  在 Configuration Manager 控制台中，转到“管理”  工作区，然后选择“客户端设置”  节点。  

1. 若要修改默认客户端设置，请选择“默认客户端设置”  。 在功能区的“主页”选项卡上的“属性”组中，选择“属性”    。

    若要创建自定义客户端代理设置，请在功能区的“主页”  选项卡上，选择“创建”  组中的“创建自定义客户端用户设置”  。

    > [!NOTE]  
    > 如果修改默认的客户端设置，则站点会将它们部署到层次结构中的所有计算机。 有关详细信息，请参阅[配置客户端设置](../../core/clients/deploy/configure-client-settings.md)。  

1. 在“用户和设备相关性”  组中，启用“允许用户定义其主要设备”  设置。  

### <a name="set-up-a-user-device-affinity-in-software-center"></a>在软件中心中设置用户设备相关性

自版本 1902 起，使用软件中心设置相关性。

1. 在软件中心内，转到“选项”  选项卡。

1. 在“工作信息”  部分中，选择“我经常使用此计算机工作”  选项。

### <a name="set-up-a-user-device-affinity-in-the-application-catalog"></a>在应用程序目录中设置用户设备相关性

> [!Important]
> 从 Current Branch 版本 1806 开始，不支持应用程序目录的 Silverlight 用户体验。 自版本 1906 起，更新后的客户端自动使用管理点进行用户可用的应用程序部署。 仍然无法安装新的应用程序目录角色。 版本 1910 已终止对应用程序目录角色的支持。  
>
> 有关详细信息，请参阅下列文章：
>
> - [配置软件中心](../plan-design/plan-for-software-center.md#bkmk_userex)
> - [已删除和已弃用的功能](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

1. 在“应用程序目录”中，选择“我的系统”  。  

1. 选择“我经常使用此计算机工作”  选项。  


## <a name="manage-user-device-affinity-requests-from-users"></a>管理来自用户的用户设备相关性请求

如果禁用客户端设置“利用使用情况数据自动配置用户设备相关性”  ，必须手动批准所有用户设备相关性分配。  

### <a name="approve-or-reject-a-user-device-affinity-request"></a>批准或拒绝用户设备相关性请求  

1. 在 Configuration Manager 控制台中，转到“资产和符合性”  工作区。  

1. 选择要为其管理相关性请求的用户或设备集合。  

1. 在功能区的“主页”  选项卡上的“集合”  组中，选择“管理相关性请求”  。  

1. 在“管理用户设备相关性请求”  对话框中，选择一个相关性请求，然后选择“批准”  或“拒绝”  。  


## <a name="next-steps"></a>后续步骤

也可以使用 Microsoft Intune 来查找注册设备的主要用户。 有关详细信息，请参阅 Intune 文档中的[查找 Intune 设备的主要用户](https://docs.microsoft.com/intune/find-primary-user)。
