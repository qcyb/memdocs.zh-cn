---
title: 应用程序下载技术参考
titleSuffix: Configuration Manager
description: 为 Configuration Manager 提供故障排除应用程序下载技术参考。
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 41c29a07-9bf6-4ec4-b3f2-1c05e001eff7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: effa8115a5023a8e0611f6bc4245a101b3a47e38
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688855"
---
# <a name="application-download-in-configuration-manager"></a>Configuration Manager 中的应用程序下载

适用范围：  Configuration Manager (Current Branch)

在继续之前，请查看[应用程序部署客户端组件](client-components-technical-reference.md)，了解 DCM 和 CI 代理作业处理过程。

## <a name="download-initiation"></a>启动下载

应用程序内容下载由客户端上的 CI 代理组件在 StateDownloadingContents 阶段启动  。 无论应用程序是部署到设备集合还是用户集合，此过程都是相同的。

- 对于“可用”部署，当用户从软件中心启动应用程序安装时，将下载应用程序内容  。
- 对于“必需”部署，当激活分配并在评估后认为应用程序可用时，下载应用程序内容  。 若要了解何时激活分配，请参阅[应用程序部署到设备集合](device-deployment-technical-reference.md)或[应用程序部署到用户集合](user-deployment-technical-reference.md)文章。

CI 代理启动内容下载时，它将创建由 CI 任务管理器组件处理的任务。 然后，CI 任务管理器启动内容下载。 可以使用“部署类型唯一 ID”在 CITaskMgr.log 中跟踪此活动  。

<pre><code class="lang-text"><b>Initiating task ContentDownload</b> for CI ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44.2 (ConfigMgr Toolkit - Windows Installer (*.msi file)) for target: , consumer: {53EA65C2-D596-4215-83E4-F7007B78E18C}
</code></pre>

## <a name="distribution-point-location"></a>分发点位置

所有下载任务都由负责管理客户端缓存的内容访问组件处理。 创建下载任务后，内容访问组件将检查内容在客户端缓存中是否已可用。 如果内容不可用，则将创建位置请求，以便得到要从中获取内容的分发点的列表。 可以在 CAS.log 和 LocationServices.log 使用“内容唯一 ID”在客户端上跟踪此活动   。

```text
Requesting locations synchronously for content Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1 with priority Foreground
ContentLocationRequest : <Request XML Body>
Reply Message Body : <Reply XML Body>
```

> [!IMPORTANT]
> 尽管定位服务组件会管理位置请求，但它不会直接从管理点请求位置。 所有发送到管理点的请求通常会经过 CCM 消息传递组件的处理，该组件会在 CcmMessaging.log  中记录信息。

位置回复 XML 包含基于客户端边界组的分发点列表。 根据[内容源优先级](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#content-source-priority)，此列表在客户端上的 WMI 中进行解析并保留。 可以通过使用“内容唯一 ID”和查找 `Persisted location` 在 ContentTransferManager.log 中查看此活动  。 

如果位置回复 XML 不包含任何分发点，ContentTransferManager.log 将显示 `Received empty location update`，客户端在下载应用程序时进度可能会卡在 0%  。 导致发生此回复的原因通常是边界组配置问题。 有关详细信息，请参阅[下载失败](../deploy-use/troubleshoot-application-deployment.md#download-failures)。

## <a name="content-download"></a>内容下载

获取分发点位置后，内容访问组件将创建内容传输作业。 可以使用内容唯一 ID 在 CAS.log 中跟踪此活动  。

<pre><code class="lang-text">Submitted CTM job <b>{6D0EA720-EB4E-4893-8395-8B27470A6CFB}</b> to download Content <b>Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1</b> under context System
</code></pre>

然后，内容传输管理器创建数据传输服务作业以执行内容下载。 可以使用内容唯一 ID 在客户端上的 ContentTransferManager.log 中对该活动进行跟踪  。

<pre><code class="lang-text">CTM job <b>{6D0EA720-EB4E-4893-8395-8B27470A6CFB}</b> (corresponding DTS job <b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b>) started download from '<Distribution Point URL>/<b>Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1</b>' for full content download.
</code></pre>

> [!NOTE]
> 此日志项目可用于标识 CTM 和 DTS 作业 ID，分别用于在 ContentTransferManager.log 和 DataTransferService.log 中跟踪内容传输进度   。

数据传输服务通过创建后台智能传输服务 (BITS) 作业并等待下载完成来执行应用程序内容的下载。 可以使用从 ContentTransferService.log 获取的 DTS 作业 ID 在客户端上的 DataTransferService.log 中跟踪此活动   。

<pre><code class="lang-text">Starting BITS job '{40263E01-2EDD-462F-ABBA-A5E892CB9229}' for DTS job '<b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b>' under user 'S-1-5-18'.
DTSJob <b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b> in state 'DownloadingData'.
DTS job <b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b> has completed
</code></pre>

下载完成后，将通知内容访问组件。 然后，内容访问组件验证下载的内容，以确保内容在下载过程中未被更改。 可以使用内容唯一 ID 在 CAS.log 中跟踪此活动  。

```text
Hash verification succeeded for content Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1 downloaded under context System
```

最后，在验证内容后，CI 代理将收到任务完成通知，CI 代理作业将进入下一阶段。

<pre><code class="lang-text">CIAgentJob({2BF84225-C9E8-49A6-A308-A160C4B799D3}): CAgentJob::HandleEvent(<b>Event=CITaskComplete, CurrentState=StateDownloadingContents</b>)
</code></pre>

## <a name="next-steps"></a>后续步骤

- [应用程序安装](deployment-install-technical-reference.md)
