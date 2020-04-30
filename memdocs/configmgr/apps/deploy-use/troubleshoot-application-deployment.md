---
title: 应用部署的故障排除提示
titleSuffix: Configuration Manager
description: 有关排除 Configuration Manager 中的应用程序部署问题的提示
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 4e8b46a3-3e11-475f-a4d7-6bf9ddf14145
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4723a85c55a2a5f7a4fbd0a99a14fbf31e7511c6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689965"
---
# <a name="troubleshooting-tips-for-application-deployments"></a>应用程序部署的故障排除提示

适用范围：  Configuration Manager (Current Branch)

应用程序部署的典型问题属于以下类别之一：

- 应用程序下载失败

- 应用程序部署合规性一直为 0%

如果遇到上述任一问题，本文提供了一些可用于排除故障的步骤。 有关故障排除的详细信息，请参阅[应用程序部署排除故障技术参考](../understand/app-deployment-technical-reference.md)。


## <a name="download-failures"></a>下载失败

应用程序下载失败包括以下问题：

- 客户端无法下载应用程序

- 客户端无法下载应用程序内容

- 下载应用程序时客户端的进度一直为 0%

遇到应用程序下载失败的问题时，要检查的第一项是缺失或配置错误的边界和边界组。 例如，如果客户端位于 Intranet 上且未配置为仅限 Internet 的客户端管理，则其网络位置必须位于已配置的边界中。 还必须为此边界分配边界组，以便客户端下载内容。 有关详细信息，请参阅[定义站点边界和边界组](../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md)。

如果无法为客户端配置边界，或者特定边界组不能是另一个边界组的成员：

1. 在 Configuration Manager 控制台中，打开“部署类型”的属性  。  

1. 切换到“内容”选项卡  。

1. 在使用来自相邻边界组或默认站点边界组的分发点的部分中，将“部署选项”更改为“从分发点下载内容并本地运行”   。 （默认情况下，此设置为“不下载内容”  。）

如果客户端无法下载应用程序内容，请确保将其分发到分发点。 若要验证此配置，请使用控制台中的功能来监视分发点的内容分发。 有关详细信息，请参阅[监视分发的内容](../../core/servers/deploy/configure/monitor-content-you-have-distributed.md)。  


## <a name="compliance-stuck-at-0"></a>合规性一直为 0%

当应用程序的部署合规性为 0% 时，请在“部署”节点下的“监视”工作区中检查应用程序的部署状态   。

- **正在进行**：客户端可能无法[下载内容](#download-failures)

- **错误**：有关如何解决此问题的更多信息，请参见以下博客文章：[提示和技巧：如何对报告失败部署的资产执行操作](https://techcommunity.microsoft.com/t5/Configuration-Manager-Archive/Tips-and-Tricks-How-to-Take-Action-on-Assets-That-Report-a/ba-p/273019)

- **未知**：此状态通常表示客户端尚未收到策略。 请手动刷新客户端策略以查看客户端是否收到它。 有关详细信息，请参阅[启动 Configuration Manager 客户端的策略检索](../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval)。
  
如果这些操作无法解决问题，请检查客户端状态。 客户端可能存在更深层次的潜在问题。 有关详细信息，请参阅[如何监视客户端](../../core/clients/manage/monitor-clients.md)。


## <a name="next-steps"></a>后续步骤

- [监视应用程序](monitor-applications-from-the-console.md)
- [部署应用程序](deploy-applications.md)
- [应用程序的管理任务](management-tasks-applications.md)
- [应用程序部署排除故障技术参考](../understand/app-deployment-technical-reference.md)
