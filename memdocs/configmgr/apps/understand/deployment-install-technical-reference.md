---
title: 关于应用程序安装的技术参考
titleSuffix: Configuration Manager
description: 关于应用程序安装的 Configuration Manager 故障排除技术参考。
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 2af4f9c3-16b8-4691-a59d-aea6241d288e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 13c96e9ad4f0608084d87bed3973221730cb2d5f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688815"
---
# <a name="application-installation"></a>应用程序安装

适用范围：  Configuration Manager (Current Branch)

继续操作前，请先查阅[应用程序部署客户端组件](client-components-technical-reference.md)，以了解 DCM 和 CI 代理作业处理。

如果强制部署，应用程序安装由 DCM 代理和 CI 代理组件执行。 可用部署和必需部署的强制时间不同。 若要了解何时强制分配，请参阅[将应用程序部署到设备集合](device-deployment-technical-reference.md)或[将应用程序部署到用户集合](user-deployment-technical-reference.md)文章。

## <a name="enforcement-initiation"></a>启动强制

应用程序安装由客户端上的 CI 代理组件在 StateEnforcingCIs  阶段启动。 无论应用程序是部署到设备集合，还是部署到用户集合，此过程都是相同的。

- 对于可用  部署，应用程序在用户从软件中心启动应用程序安装时安装。
- 对于必需  部署，应用程序在部署截止时间安装。 不过，用户可以在截止时间前从软件中心启动安装。

启动应用程序安装时，CI 代理会创建由 CI 任务管理器组件处理的任务。 然后，CI 任务管理器会启动安装。 可以使用部署类型唯一 ID 在 CITaskMgr.log  中跟踪此活动。

<pre><code class="lang-text"><b>Initiating task Enforce</b> for CI ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44.2 (ConfigMgr Toolkit - Windows Installer (*.msi file)) for target: , consumer: {9BC3154A-98F1-4595-A967-173D536A3F94}
Initiated application enforcement. : CITask(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44.2..Install.Enforce)
</code></pre>

## <a name="application-enforcement"></a>应用程序强制

启动应用程序强制后，客户端会再次执行应用程序检测，以确保应用程序尚未安装。 在确定应用程序未安装后，便会启动应用程序安装。 可以使用部署类型唯一 ID 在客户端上的 AppEnforce.log  中跟踪此活动。

```text
+++ Starting Install enforcement for App DT "ConfigMgr Toolkit - Windows Installer (*.msi file)" ApplicationDeliveryType - ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, Revision - 2, ContentPath - C:\WINDOWS\ccmcache\2, Execution Context - System
    Executing Command line: "C:\WINDOWS\system32\msiexec.exe" /i "ConfigMgrTools.msi" /q /qn with user context
    Process 7292 terminated with exitcode: 0
Status is switching to Success
```

## <a name="installation-verification"></a>验证安装

在应用程序安装后，会再次使用应用程序检测方法，以确保应用程序检测为“已安装”。

<pre><code class="lang-text">Performing detection of app deployment type ConfigMgr Toolkit - Windows Installer (*.msi file)(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, revision 2) for system.
+++ <b>Discovered MSI application</b> [AppDT Id: ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, Revision: 2, MSI Product code: {4FFF7ECC-CCF7-4530-B938-E7812BB91186}, MSI Product version: ]
++++++ <b>App enforcement completed</b> (3 seconds) for App DT "ConfigMgr Toolkit - Windows Installer (*.msi file)" [ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44], Revision: 2, User SID: ] ++++++
</code></pre>

最后，在强制完成后，CI 代理会收到任务完成通知，CI 代理作业会转到下一阶段。

<pre><code class="lang-text">CIAgentJob({2BF84225-C9E8-49A6-A308-A160C4B799D3}): CAgentJob::HandleEvent(<b>Event=CITaskComplete, CurrentState=StateEnforcingCIs</b>)
</code></pre>

## <a name="next-steps"></a>后续步骤

[排除应用程序部署故障](../deploy-use/troubleshoot-application-deployment.md)
