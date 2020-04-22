---
title: 技术预览版
titleSuffix: Configuration Manager
description: 了解可测试 Configuration Manager 中的新功能和新特性的技术预览分支。
ms.date: 03/31/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ec49f9931240e17218c125f1fa514088c83c55fd
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701835"
---
# <a name="technical-preview-for-configuration-manager"></a>Configuration Manager 的技术预览版

适用范围：*Configuration Manager（技术预览版分支）*

本文提供了有关 Configuration Manager 的每月技术预览分支的详细信息。 技术预览版介绍 Microsoft 正在开发的新功能。 它介绍 Configuration Manager 当前分支中尚未包含的新功能。 这些功能可能最终会包含在当前分支的更新中。 在我们最终发布这些功能前，我们希望你试用这些功能并向我们提供反馈。

由于此版本是技术预览版，因此详细信息和功能可能有所更改。

此信息适用于 Configuration Manager 技术预览分支的所有版本。 本文列出了每个新功能以及该功能首次出现所在的技术预览版。 例如，版本 2001 为 2020 年 (`20`) 的 1 月 (`01`)  。 单独的文章专用于详细介绍每个预览版的单独功能。

有关 Configuration Manager 的当前版本  中新增功能的信息，请参阅 [Configuration Manager 增量版本中的新增功能](../plan-design/changes/whats-new-incremental-versions.md)。

> [!Tip]
> 若要在此页面更新时收到通知，请将以下 URL 复制并粘贴到 RSS 源阅读器中：`https://docs.microsoft.com/api/search/rss?search=%22technical+preview+releases+-+Configuration+Manager%22&locale=en-us`

## <a name="requirements-and-limitations"></a><a name="bkmk_reqs"></a>要求和限制

> [!IMPORTANT]
> 技术预览版仅授权用于实验室环境。 Microsoft 可能无法提供支持服务，技术预览中某些功能可能不可用。 此外，相对于面向市场提供的软件，技术预览软件可能采用简化的或不同的安全性、隐私性、可访问性、可用性和可靠性标准。

有关大多数产品的先决条件，请使用[支持的配置](../plan-design/configs/supported-configurations.md)中的信息。 以下是适用于技术预览分支的例外情况：

- 每次安装在活动状态 90 天后变为非活动状态。

- 英语是唯一受支持的语言。

- 它仅支持以下安装命令行参数：

  - `/silent`
  - `/testdbupgrade`

- 服务连接点安装为联机模式。 它不支持脱机模式。

- 每个特定版本的 Technical Preview 的单独文章中包括其他限制或要求（如果适用）。

- 以下功能在技术预览分支中不受支持：

  - [迁移](../migration/migrate-data-between-hierarchies.md)到此预览分支或从此预览分支迁移。

  - [升级](../servers/deploy/install/upgrade-to-configuration-manager.md)到此预览分支。

  - cd.latest 文件夹中的[站点恢复](../servers/manage/recover-sites.md)。<!--507106-->

- 不支持从此预览分支更新到当前分支。

    > [!Note]
    > 更新可用于预览版本时，仍从 Configuration Manager 控制台的“更新与维护服务”  节点查找并安装它们。 有关控制台中升级过程的视频，请观看 youtube.com 上的[安装 Configuration Manager 更新包](https://www.youtube.com/embed/KBd_EGFbUT8)。

- 它仅支持独立主站点。 不支持管理中心站点、多个主站点或辅助站点。

Configuration Manager 的技术预览分支支持以下产品和技术：

- 它仅支持 SQL Server  的以下版本：

  - SQL Server 2017（带累积更新 2 或更高版本）
  - SQL Server 2016（不带服务包或更高版本）
  - SQL Server 2014（含服务包 1 或更高版本）
  - SQL Server 2012（含服务包 3 或更高版本）

- 站点最多支持 10 个客户端，客户端可以运行任何[受支持的客户端 OS 版本](../plan-design/configs/supported-operating-systems-for-clients-and-devices.md)。<!-- SCCMDocs#1656 -->

> [!Note]
> 在此内容中包含这些产品并不意味着支持超出其支持生命周期以外的版本。 Configuration Manager 不支持超出其支持生命周期以外的产品。 有关详细信息，请参阅 [Microsoft 生命周期策略](https://go.microsoft.com/fwlink/p/?LinkId=208270)。

## <a name="install-and-update"></a><a name="bkmk_install"></a>安装和更新

供实验室使用的 Configuration Manager 技术预览分支与供生产使用的 Configuration Manager 当前分支有所不同。

首先安装技术预览分支的基线版本。 安装基线版本之后，使用控制台内更新来升级此内部版本，以便使用最新预览版使你的安装程序保持最新。 通常，每个月都会提供新版本的技术预览版。

Microsoft 将支持每个技术预览版，直到三个连续的版本可用为止。 例如，版本 1908 发布后，版本 1904 便不再受支持。 版本 1905、1906 和 1907 仍受支持。 当某个基线版本不受支持后，它仍支持安装新的技术预览版站点（假设你立即更新到支持的版本）。 较旧的基线版本将继续受支持，直到有新的可用的基线版本为止。 从基线版本更新到最新可用版本，然后重复更新过程，直到安装最新技术预览版为止。

> [!TIP]
> 向 Technical Preview 安装更新后，即可将 Preview 安装更新到这个新的 Technical Preview 版本。 技术预览版安装永远不会有升级到当前分支安装的选项。 它也永远不会接收来自当前分支版本的更新。
>
> 技术预览分支和当前分支版本在一年中有几次使用相同的版本号。 例如，有一个技术预览版 1910 和一个当前分支版本 1910。

### <a name="active-baseline-versions"></a>活动基线版本

在基线版本发布后的 1 年内安装此基线版本。 在安装新技术预览版站点时，请使用最新的基准版本。

- **技术预览版 2002**：Configuration Manager 技术预览分支版本 2002 可同时用作控制台内更新和新基线版本。

从 [TechNet 评估中心](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview)下载基线版本。

## <a name="providing-feedback"></a><a name="BKMK_TPFeedback"></a> 提供反馈

欢迎提供有关技术预览版新功能的反馈。 有关详细信息，请参阅[产品反馈](../understand/find-help.md#product-feedback)。

如果你对于想要看到的新功能有任何想法，请告诉我们！ 提交新的想法并对其他人的想法进行投票：[Configuration Manager UserVoice](https://configurationmanager.uservoice.com)。

<!--
## <a name="bdmk_tpknownissues"></a> General changes introduced in technical preview branch

<!-- (explanatory comment)
Enable this section if needed to include any broad change to the tech preview branch
-->

## <a name="features-in-the-most-recent-version"></a><a name="bkmk_tpCaps"></a> 最新版本中的功能

<!-- (explanatory comment)
This is the full list of new features in the latest TP release

bullet format:
<!-- - [title](2020/technical-preview-2003.md#bkmk_anchor) <!--ID-->

以下是最新 Configuration Manager 技术预览版中提供的功能：

### <a name="technical-preview-version-2003"></a>技术预览版 2003

- [通过 Microsoft Endpoint Manager 控制台将 Configuration Manager 客户端加入 Microsoft Defender ATP](2020/technical-preview-2003.md#bkmk_atp) <!--5691658-->
- [跟踪配置项目修正](2020/technical-preview-2003.md#bkmk_track) <!--4261411 in 2002-->
- [显示设备的边界组](2020/technical-preview-2003.md#bkmk_boundary) <!--6521835 in 2002-->
- [新反馈向导](2020/technical-preview-2003.md#bkmk_feedback) <!--3180826-->
- [对 Microsoft Edge 管理仪表板的改进](2020/technical-preview-2003.md#bkmk_edge) <!--5907383-->
- [对 CMPivot 的改进](2020/technical-preview-2003.md#bkmk_cmpivot) <!--6518631-->
- [针对发送给 Microsoft 的反馈的查询](2020/technical-preview-2003.md#bkmk_smile) <!--6488450-->
- [任务序列进度的新 SDK 方法](2020/technical-preview-2003.md#bkmk_tsapi) <!--6448458-->
- [对 OS 部署的改进](2020/technical-preview-2003.md#bkmk_osd) <!--6452769-->

> [!NOTE]
> 某个旧版技术预览中可用的功能在其后的版本中仍然可用。 同样，已添加到 Configuration Manager 当前分支的功能在技术预览分支中仍然可用。

<!-- temp remove for 2002 CB ## Features in recent technical previews -->

<!-- (explanatory comment)
This is the full list of new features in the past TP releases since the last CB release.
Each month, add features from the list above to a new H3 section at the top of this section.
When there's a new CB, add any features not in that CB to the table in H2 "Features in previous technical previews"
-->

<!--temp remove for 2002 CB  The following features were released with previous versions of the Configuration Manager technical preview branch since current branch version 1910: -->

> [!TIP]
> 当新的分支版本可用时，会在最新的“新增功能”一文中列出该版本中可用的功能  。 有关详细信息，请参阅[增量版本中的新增功能](../plan-design/changes/whats-new-incremental-versions.md#supported-versions)。

<!-- ### Technical preview version 2003 -->

## <a name="features-in-previous-technical-previews"></a>旧版技术预览版中的功能

<!-- (explanatory comment)
This is the list of individual features that are still in TP (not in CB). 
Copy from the lists above any individual features that are still in TP and add to the top of this list
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

以下是旧版 Configuration Manager 技术预览分支发布的功能。 这些功能在更高版本中保持可用，但在当前分支中不可用。

| 功能        | 技术预览版 |
|----------------|---------------------------|
| 将文件附加到反馈 <!--3556011--> | [技术预览版 1910](2019/technical-preview-1910.md#attach-files-to-feedback) |
| 对已启用多播的分发点的改进 <!--3785535--> | [技术预览版 1908.2](2019/technical-preview-1908-2.md#bkmk_multicast) |
| 分阶段部署模板 <!--4961086--> | [技术预览版 1908](2019/technical-preview-1908.md#phased-deployment-templates) |
| 使用云管理网关随时随地进行远程控制 <!--4575930--> | [技术预览版 1906](2019/technical-preview-1906.md#remote-control-anywhere-using-cloud-management-gateway) |
| 对社区中心的改进 <!--3555935--> | [技术预览版 1906](2019/technical-preview-1906.md#bkmk_hub) |
| 对社区中心的改进 <!--4224401--> | [技术预览版 1905](2019/technical-preview-1905.md#bkmk_hub) |
| 社区中心和 GitHub <!--3555935--> | [Tech Preview 1904](2019/technical-preview-1904.md#community-hub-and-github) |
| 云服务成本估算器 <!--3555774--> | [Tech Preview 1903](2019/technical-preview-1903.md#bkmk_cmg) |
| 从社区中心下载报表 <!--3555936--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_hub) |
| 社区中心 <!--3556020, fka 1357766--> | [技术预览版 1807](capabilities-in-technical-preview-1807.md#bkmk_hub) |
| 基于客户端的 PXE 响应者服务 <!--3556018, fka 1357148--> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
| PXE 网络启动对 IPv6 的支持 <!--3601254, fka 1269793--> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
| 使用 Azure Active Directory <!--3607315, fka 1322145--> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
| 对资产智能的改进 <!--3601024, fka 1307390--> | [Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence) |

## <a name="see-also"></a>另请参阅

有关详细信息，请参阅下列文章：

- [在实验室中评估 Configuration Manager](evaluate-with-lab-environment.md)
- [Configuration Manager 增量版本中的新增功能](../plan-design/changes/whats-new-incremental-versions.md)
- [Configuration Manager 简介](../understand/introduction.md)

> [!Tip]
> 若要详细了解需要同意才能启用的当前分支功能，请参阅[预发布功能](../servers/manage/pre-release-features.md)。
>
> 若要详细了解必须先启用的当前分支功能，请参阅[启用更新中的可选功能](../servers/manage/install-in-console-updates.md#bkmk_options)。
