---
title: 社区中心和 GitHub
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中启用和使用社区中心
ms.date: 07/27/2020
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 88cead9a-64fe-471e-b57c-81707cefe46c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c0b812fa3b373d6bd5bd2bebed8b1540ceb7bdd6
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "87262075"
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


## <a name="next-steps"></a>后续步骤

详细了解如何创建和使用以下对象：

- [创建并运行 PowerShell 脚本](../../../apps/deploy-use/create-deploy-scripts.md)
- [报表简介](introduction-to-reporting.md)
- [创建和管理任务序列](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md)
- [创建和部署应用程序](../../../apps/get-started/create-and-deploy-an-application.md)
- [创建配置项目](../../../compliance/deploy-use/create-configuration-items.md)