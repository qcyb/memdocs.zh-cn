---
title: 创建用户数据和配置文件配置项目
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中使用数据和配置文件配置项目来管理文件夹重定向、脱机文件和漫游配置文件。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 9fcbcc81-cd6f-496e-b075-ef1afa2b8ccc
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 51c97ae3cd947e0bdfa82c595cb6446351412d21
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240365"
---
# <a name="create-user-data-and-profiles-configuration-items-in-configuration-manager"></a>在 Configuration Manager 中创建用户数据和配置文件配置项目

适用范围：  Configuration Manager (Current Branch)

Configuration Manager 中的用户数据和配置文件配置项目可为层次结构中的用户管理运行 Windows 8 和更高版本的计算机上的文件夹重定向、脱机文件和漫游配置文件。 例如，你能够：  

- 将用户的 Documents 文件夹重定向到网络共享。  

- 确保当网络连接不可用时，用户的计算机可使用网络上存储的指定文件。  

- 配置用户漫游配置文件中哪些文件在用户日志打开和关闭时与网络共享同步。  

  与 Configuration Manager 中的其他配置项目不同，无需向随后将部署的配置基线添加用户数据和配置文件的配置项目。 而只需使用“部署用户数据和配置文件的配置项目”  对话框直接部署配置项目。  

> [!IMPORTANT]  
>  仅可向用户集合部署用户数据和配置文件的配置项目。  

## <a name="enable-user-data-and-profiles-for-compliance-settings"></a>为符合性设置启用用户数据和配置文件  
 使用以下过程来配置用于用户数据和配置文件符合性设置的默认客户端设置，这些设置将应用于层次结构中的所有计算机。 如果希望这些设置仅应用于某些计算机，请创建一个自定义设备客户端设置，并将其分配给包含要使用用户数据和配置文件符合性设置的计算机的集合。 有关如何创建自定义设备设置的详细信息，请参阅[如何配置客户端设置](../../core/clients/deploy/configure-client-settings.md)。  

1.  在 Configuration Manager 控制台中，单击“管理”   > “客户端设置”   > “默认设置”  。  

4.  在“主页”  选项卡上的“属性”  组中，单击“属性”  。  

5.  在“默认设置”  对话框中，单击“符合性设置”  。  

6.  从“启用用户数据和配置文件”  下拉菜单中，选择“是”  。  

7.  单击“确定”  来关闭“默认设置”  对话框。  

## <a name="create-a-user-data-and-profiles-configuration-item"></a>创建用户数据和配置文件配置项目  

1. 在 Configuration Manager 控制台中，单击“资产和符合性”   > “符合性设置”   > “用户数据和配置文件”  。  

2. 在“主页”  选项卡上的“创建”  组中，单击“创建用户数据和配置文件的配置项目”  。  

3. 在“创建用户数据和配置文件的配置项目向导”  的“常规”  页上，指定以下信息：  

   -   **名称：** 输入配置项目的唯一名称。 最多可以使用 256 个字符。  

   -   **描述：** 提供对配置项目进行概述以及其他有助于识别 Configuration Manager 控制台中相关信息的说明。 最多可以使用 256 个字符。  

   -   **文件夹重定向：** 如果想要为此配置项目配置文件夹重定向设置，请选中此框。  

   -   **脱机文件：** 如果想要为此配置项目配置脱机文件设置，请选中此框。  

   -   **漫游用户策略文件：** 如果想要为此配置项目配置漫游用户策略文件设置，请选中此框。  

4. 在“创建用户数据和配置文件的配置项目向导”  的“文件夹重定向”  页上，指定你希望接收此配置项目的用户的客户端计算机如何管理文件夹重定向。 你可为用户登录的所有设备配置设置，也可仅为用户的主要设备配置设置。 有关文件夹重定向的详细信息，请参阅你的 Windows Server 文档。  

   > [!NOTE]  
   >  仅当你选中向导“常规”  页上的“文件夹重定向”  时，才会显示此页。  

5. 在“创建用户数据和配置文件的配置项目向导”  的“脱机文件”  页上，可以为接受此配置项目并针对脱机文件的行为配置设置的用户启用或禁用脱机文件的使用。 也可指定在用户登录的任何计算机上总是可用的脱机文件。 有关脱机文件的详细信息，请参阅你的 Windows Server 文档。  

   > [!NOTE]  
   >  仅当你选中向导“常规”  页上的“脱机文件”  框时，才会显示此页。  

6. 在“创建用户数据和配置文件的配置项目向导”  的“漫游配置文件”  页上，你可以配置漫游配置文件在用户登录的计算机上是否可用，还可以配置有关这些配置文件的行为方式的进一步信息。 有关漫游配置文件的详细信息，请参阅你的 Windows Server 文档。  

   > [!NOTE]  
   >  仅当你选中向导“常规”  页上的“漫游用户配置文件”  框时，才会显示此页。  

7. 完成向导。  

   新的用户数据和配置文件的配置项目显示在“资产和符合性”  工作区的“用户数据和配置文件”  节点中。  

## <a name="deploy-a-user-data-and-profiles-configuration-item"></a>部署用户数据和配置文件配置项目  

1.  在 Configuration Manager 控制台中，单击“资产和符合性”   > “符合性设置”   > “用户数据和配置文件”  。  

3.  选择要部署的用户数据和配置文件的配置项目，然后，在“主页”  选项卡上的“部署”  组中单击“部署”  。  

4.  在“部署用户数据和配置文件的配置项目”  对话框中，指定以下信息。  

    -   **集合** - 单击“浏览”  以选择要在其中部署配置项目的用户集合。  

        > [!IMPORTANT]  
        >  仅可向用户集合部署用户数据和配置文件的配置项目。  

    -   **在支持时修正非符合性规则** – 启用此选项可自动修正客户端计算机上评估为不符合的任何规则。  

    -   **允许维护时段外的修正** - 如果已为你向其部署配置项目的集合配置了维护时段，请启用此选项以让符合性设置在维护时段外修正值。 有关维护时段的详细信息，请参阅[如何使用维护时段](../../core/clients/manage/collections/use-maintenance-windows.md)。  

    -   **生成警报** - 启用此选项可配置一个警报，如果在指定日期和时间之前配置项目符合性小于指定百分比，则生成该警报。 你也可以指定是否希望将警报发送到 System Center Operations Manager。  

    -   **指定此配置项目的符合性评估计划** - 指定在客户端计算机上对部署的配置项目进行评估所依据的计划。 这可以是简单计划或自定义计划。  

5.  单击“确定”  关闭“部署用户数据和配置文件的配置项目”  对话框并创建部署。  

## <a name="monitor-a-user-data-and-profiles-configuration-item"></a>监视用户数据和配置文件的配置项目  
 监视此类配置项目的方法与监视其他符合性设置的方法相同。  

 有关详细信息，请参阅[如何监视符合性设置](../../compliance/deploy-use/monitor-compliance-settings.md)。  
