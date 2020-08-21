---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: 98e3dd75316acfeaf88715b8f80762b1d6c587c6
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128320"
---
<!--This file is shared by the cmpivot.md file and the cmpivot-changes.md file and contains information on how to run CMPivot standalone. H2s or HJ3s are determined by the article for which the include file is used.-->
<!--3555890, 4619340, 4683130 -->

从版本 1906 开始，可以将 CMPivot 用作独立应用。 CMPivot 独立应用仅提供英语版本。 在 Configuration Manager 控制台外部运行 CMPivot，可以查看环境中设备的实时状态。 借助此变化，无需先安装控制台，即可在设备上使用 CMPivot。

> [!Tip]  
> 此功能在版本 1906 中作为[预发行功能](../pre-release-features.md)首次引入。 从版本 2002 开始，此功能不再属于预发行功能。  

可以与其他尚未在计算机上安装控制台的角色（例如支持人员或安全管理员）共享功能强大的 CMPivot。 这些其他角色可以将 CMPivot 与他们传统上使用的其他工具并行使用，以查询 Configuration Manager。 通过共享此类丰富的管理数据，你们可以一起工作，共同主动解决跨角色的业务问题。

#### <a name="install-cmpivot-standalone"></a>安装 CMPivot 独立应用

1. 设置运行 CMPivot 所需的权限。 有关详细信息，请参阅[先决条件](../cmpivot.md#prerequisites)。 如果这些权限适用于用户，则还可以使用[安全管理员角色](../cmpivot-changes.md#bkmk_cmpivot_secadmin1906)。
2. 在下面的路径找到 CMPivot 应用安装程序：`<site install path>\tools\CMPivot\CMPivot.msi`。 可以从此路径运行它，也可以将其复制到其他位置。
3. 运行 CMPivot 独立应用时，系统将要求你连接到站点。 指定管理中心或主站点服务器的完全限定的域名或计算机名。
   - 每次打开 CMPivot 时，系统将提示你连接到站点服务器。
4. 浏览到要在其上运行 CMPivot 的集合，然后运行查询。

   ![浏览到要对其运行查询的集合](../media/3555890-cmpivot-standalone-browse-collection.png)

> [!NOTE]
> - 右键单击操作（例如，“运行脚本”、“资源浏览器”）和 Web 搜索在 CMPivot 独立应用中不可用 。 CMPivot 独立应用的主要用途是独立于 Configuration Manager 基础结构进行查询。 为了帮助安全管理员，CMPivot 独立应用确实包含连接到 Microsoft Defender 安全中心的功能。 <!--5605358-->
> - 自版本 1910 起，可以执行[使用 CMPivot 独立应用的本地设备查询评估](../cmpivot-changes.md#bkmk_local-eval)。 <!--3197353--> 