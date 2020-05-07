---
title: 关于应用程序部署客户端组件的技术参考
titleSuffix: Configuration Manager
description: 用于在 Configuration Manager 中排除应用程序部署故障的客户端组件。
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 701a3456-9dd6-4aaa-9c5a-37c1e1773216
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 35b54bd5868197d607a15ab1d4759d03968b9892
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688845"
---
# <a name="understanding-application-deployment-client-components"></a>了解应用程序部署客户端组件

适用范围：  Configuration Manager (Current Branch)

应用程序部署评估和强制操作由客户端上的 DCM 代理和 CI 代理组件处理。 本文介绍了典型 DCM 和 CI 代理作业的工作原理。

## <a name="dcm-agent"></a>DCM 代理

DCM 代理是负责评估配置项目（包括应用程序）的高级客户端组件。 在激活或强制部署后，会创建 DCM 代理作业，用于读取分配策略，并确定需要执行的操作。 可以使用 DCM 代理作业 ID（可通过查找应用程序唯一 ID 来识别）在客户端上的 DCMAgent.log  中跟踪此活动。

### <a name="device-deployments"></a>设备部署

- 对于必需  部署，DCMAgent.log 会显示适用的操作。 这些操作可能会因部署截止时间是否已过去而异。

    ```text
    # Evaluation Job example:
    DCMAgentJob({A9E850E2-91B0-4122-94FD-D14EDF925AF7}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/RequiredApplication_fc76ef0a-3ab0-4110-8cce-1addc36d0225 version:3 with actions: Evaluation, Content Download

    # Enforcement Job example:
    DCMAgentJob({4C8A9F6E-390B-450E-B505-B5698DB68EDD}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/RequiredApplication_fc76ef0a-3ab0-4110-8cce-1addc36d0225 version:3 with actions: Evaluation, Install, Uninstall, Update, Look-ahead Install, Look-ahead Uninstall, Look-ahead Update
    ```

- 对于可用  部署，DCMAgent.log 会显示部署 `is not mandatory`。 对于此类部署，会完成应用程序评估，但会跳过强制部署，除非用户启动了安装。

    ```text
    # Evaluation Job example:
    DCMAgentJob({E353BF94-D7ED-4ADD-AF0F-9273F6A67FC1}): CDCMAgentJob::PopulateCIsFromAssignment - [SCAN] CI policy Id :ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/RequiredApplication_fc76ef0a-3ab0-4110-8cce-1addc36d0225 version:3 - Assignment:{3AC57DFE-3F87-4C59-930B-B9F57CB41B91} is not mandatory.

    # Enforcement Job (user initiated) example:
    Request to enforce application ConfigMgr Toolkit(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/Application_fc76ef0a-3ab0-4110-8cce-1addc36d0225.3) immediately for target: machine with action(s): Evaluation, Install, Update
    CDCMAgentJobMgr::CreateInteractiveJob - Queuing new job: {D331249E-F7DE-481B-A497-8E8B5E7B91C3}

    ```

### <a name="user-deployments"></a>用户部署

- 对于必需  部署，DCMAgent.log 会显示适用的操作。 这些操作可能会因部署截止时间是否已过去而异。

    ```text
    # Evaluation Job example:
    DCMAgentJob({65D9688D-1781-4DA3-B07A-193D481251C6}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98 version:2 with actions: Evaluation, Content Download

    # Enforcement Job example:
    DCMAgentJob({2B0DA272-FC65-4F31-9557-C4D840D650F1}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98 version:2 with actions: Evaluation, Install, Uninstall, Update, Look-ahead Install, Look-ahead Uninstall, Look-ahead Update
    ```

- 对于可用  部署，DCM 代理作业在用户启动了应用程序安装时创建，用于评估和强制部署。

    ```text
    # Evaluation Job example:
    DCMAgentJob({FBB44C84-DB06-41F7-8DC1-D9BA368F0C20}): CDCMAgentJob::PopulateCIsFromAssignment - [SCAN] CI policy Id :ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98 version:2 - Assignment:{7EA17128-EB4F-448A-88A7-B865E7DA228C} is not mandatory.

    # Enforcement Job example:
    CAppMgmtSDK::EnforceAppPolicy ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98.
    CDCMAgentJobMgr::CreateInteractiveJob - Queuing new job: {7936D7F3-24B0-401D-BADD-59EB5B49C2C2}
    ```

## <a name="ci-agent"></a>CI 代理

CI 代理是负责评估和修正配置项目的客户端组件。 DCM 代理读取分配策略，并为 CI 代理组件创建作业来执行请求的操作。 DCMAgent.log  记录了 CI 代理作业 ID，此 ID 可用于在客户端上的 CIAgent.log  中跟踪 CI 代理活动。

<pre><code class="lang-text">DCMAgentJob({E353BF94-D7ED-4ADD-AF0F-9273F6A67FC1}): CDCMAgent::InitiateCIAgentJob - <b>Starting CI Agent Job</b> {57AF6FA1-3482-4469-9881-A63F41D18406} for target: machine. Refer to this CI agent job ID in ciagent.log for more details
</code></pre>

典型 CI 代理作业会经历多个阶段，可以按 CI 代理作业 ID 筛选 CIAgent.log  并查找 `TransitionState` 来识别。 应用程序部署 CI 代理作业的部分关键阶段为：

- DownloadingCIs 
  - 在此阶段中，下载评估应用程序所需的应用程序元数据。 元数据包括检测方法、要求规则、全局条件等。可以在 CIDownloader.log  和 DataTransferService.log  中跟踪此活动。 对于可用  部署，此过程在第一次评估应用程序期间发生。 不过，对于必需  部署，此过程在策略下载后立即发生。

- InvokingSdmMethod 
  - 在此阶段中，使用应用程序检测方法来检查是否安装了应用程序并确定了所需状态。 可以在 AppDiscovery.log  和 AppIntentEval.log  中跟踪此活动。 若要详细了解此阶段，请参阅[应用程序评估](deployment-evaluation-technical-reference.md)。

- StateDownloadingContents 
  - 在此阶段中，下载应用程序内容（如果需要）。 可以在 CAS.log  、ContentTransferManager.log  、LocationServices.log  和 DataTransferService.log  中跟踪此活动。 若要详细了解此阶段，请参阅[应用程序下载](deployment-download-technical-reference.md)。

- StateEnforcingCIs 
  - 在此阶段中，启动应用程序安装。 可以在 AppEnforce.log  中跟踪此活动。 若要详细了解此阶段，请参阅[应用程序安装](deployment-install-technical-reference.md)。

- StateEnforcementReporting 
  - 在此阶段中，记录应用程序安装状态，以便向管理点报告。 可以在 StateMessage.log  中跟踪此活动。

虽然 CI 代理作业经历所有阶段，但也会跳过不是必需的阶段。 例如，对于可用  部署，除非用户尝试从软件中心安装应用程序，否则会跳过 StateDownloadingContents 和 StateEnforcingCIs 阶段。 不过，对于必需  部署，StateDownloadingContents 阶段会在分配激活时下载应用程序内容（如果需要），但如果截止时间是未来时间，则会跳过 StateEnforcingCIs 阶段。 通过按 CI 代理作业 ID 筛选并查找 `Skipping policy`，可以在 CIAgent.log 中观察到此行为。

```text
{57AF6FA1-3482-4469-9881-A63F41D18406} - Skipping policy CI <CI Unique ID> and all dependents for ContentDownload task since CI action was not requested.
{57AF6FA1-3482-4469-9881-A63F41D18406} - Skipping policy CI <CI Unique ID> and all dependents for Enforce task since CI action was not requested.
```

## <a name="next-steps"></a>后续步骤

- [应用程序评估](deployment-evaluation-technical-reference.md)
- [应用程序下载](deployment-download-technical-reference.md)
- [应用程序安装](deployment-install-technical-reference.md)
