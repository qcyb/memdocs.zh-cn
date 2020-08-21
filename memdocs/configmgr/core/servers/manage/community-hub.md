---
title: 社区中心和 GitHub
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中启用和使用社区中心
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 88cead9a-64fe-471e-b57c-81707cefe46c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ae0abdd4a159759037768c8f27d5643bdf612f6e
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128165"
---
# <a name="community-hub-and-github"></a>社区中心和 GitHub
<!--3555935, 3555936-->

多年来，IT 管理员社区积累了丰富的知识。 我们打造了 Configuration Manager 社区中心，以方便 IT 管理员彼此共享，而不必从头开始重新创建脚本和报告等项目。 通过借鉴其他人的工作，你可以节省工作小时数。 社区中心支持你和其他人在相互借鉴各自工作的基础上生成内容，从而发展创造力。 GitHub 已构建面向全行业的共享流程和工具。 现在，社区中心将直接在 Configuration Manager 控制台中利用这些工具，作为推动新社区发展的基础组件。 在初始版本中，社区中心内提供的内容将仅由 Microsoft 上传。 将来，IT 管理员将能够使用其自己的 GitHub 帐户自行上传内容。

> [!Note]  
> 社区中心是一项可选的基于云的功能。 2020 年 6 月首次推出此功能。 有关如何选择加入社区中心的信息，请参阅[可选功能](install-in-console-updates.md#bkmk_options)。

## <a name="about-community-hub"></a>关于社区中心

社区中心支持以下对象：

- CMPivot 查询
- 应用程序
- 任务序列
- 配置项目
- PowerShell 脚本
- 报表

## <a name="prerequisites"></a>必备条件

- 用于访问社区中心且运行 Configuration Manager 控制台的设备必须安装以下各项：
   - .NET Framework 版本 4.6 或更高版本
   - Windows 10 版本 17110 或更高版本
      - Windows Server 不受支持，因此需要在与站点服务器不同的 Windows 10 设备上安装 Configuration Manager 控制台。
   - 登录的用户帐户不能是内置管理员帐户

- Configuration Manager 中的[管理服务](../../../develop/adminservice/set-up.md)需要进行设置才能正常运行。

- 如果组织使用防火墙或代理设备限制与 Internet 的网络通信，你必须允许 Configuration Manager 控制台访问 Internet 终结点。 有关详细信息，请参阅 [Internet 访问要求](../../plan-design/network/internet-endpoints.md#community-hub)。

## <a name="permissions"></a>权限

- 若要导入脚本：需要 SMS_Scripts 类的“创建”权限。
- 若要导入报告：需要完全权限管理员安全角色。


## <a name="use-the-community-hub"></a>使用社区中心

1. 转到“社区”工作区中的“社区中心”节点。
1. 选择要下载的项。
1. 必须在 Configuration Manager 站点中拥有适当权限，才能从此中心下载对象并将它们导入站点。
    - 若要导入脚本：需要 SMS_Scripts 类的“创建”权限。
    - 若要导入报告：需要完全权限管理员安全角色。
1. 下载的报告部署到 Reporting Services 点上名为“中心”的报告文件夹中。 可转到“运行脚本”节点来查看下载的脚本。
1. 单击“社区中心”节点中的“你的下载”，查看组织从中心下载的所有项目 。

[![从社区中心下载的所有项目](./media/3555935-community-hub-downloads.png)](./media/3555935-community-hub-downloads.png#lightbox)


## <a name="direct-links-to-community-hub-items"></a><a name="bkmk_deeplink"></a> 指向社区中心项的直接链接
<!--4224406-->
（在版本 2006 中引入）可以使用直接链接轻松转到并引用 Configuration Manager 控制台“社区中心”节点内的项。 此功能的目的是为了更轻松地进行协作，并且能够与同事共享指向社区中心项的链接。 这些深层链接当前仅用于控制台的社区中心节点中的项。

### <a name="prerequisites-for-direct-links"></a>直接链接的先决条件

- Configuration Manager 控制台版本 2006 或更高版本
- 在打开社区中心链接时，无法使用本地内置管理员帐户。

### <a name="sharing-and-opening-direct-links"></a>共享和打开直接链接

若要共享项，请执行以下操作：
1. 转到中心内的项，然后选择“共享”。
1. 粘贴所复制的链接，然后与其他人共享。

若要打开共享的链接，请执行以下操作：
1. 在安装了 Configuration Manager 控制台的计算机上单击链接。
   - 例如，使用此链接共享[配置边缘自动更新脚本](https://communityhub.microsoft.com/item/7200) (`https://communityhub.microsoft.com/item/7200`)。
1. 出现提示时，选择“启动社区中心”。
1. 控制台将直接打开到社区中心中的脚本。

## <a name="known-issues"></a><a name="bkmk_known"></a> 已知问题

### <a name="unable-to-access-community-hub-node-when-running-console-as-a-different-user"></a>当以其他用户身份运行控制台时，无法访问“社区中心”节点
<!--7826897-->
如果你以权限较低的用户身份登录，并选择“以其他用户身份运行”来打开 Configuration Manager 控制台，可能无法访问“社区中心”节点。

### <a name="downloaded-reports-dont-get-removed-from-your-downloads-page"></a>下载的报表不会从“下载”页中删除
<!--7851305-->
如果你从“监视” > “报表”节点中删除了下载的报表，此报表不会从“社区中心” > “你的下载”页中删除，但你无法再次下载此报表。 

## <a name="next-steps"></a>后续步骤

详细了解如何创建和使用以下对象：

- [创建并运行 PowerShell 脚本](../../../apps/deploy-use/create-deploy-scripts.md)
- [报表简介](introduction-to-reporting.md)
- [创建和管理任务序列](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md)
- [创建和部署应用程序](../../../apps/get-started/create-and-deploy-an-application.md)
- [创建配置项目](../../../compliance/deploy-use/create-configuration-items.md)