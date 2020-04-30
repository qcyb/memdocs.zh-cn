---
title: 应用程序评估技术参考
titleSuffix: Configuration Manager
description: 关于应用程序评估的 Configuration Manager 故障排除技术参考。
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: a7035223-d7bd-47b4-896f-08de3416a4eb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fdeec54489adfc0d2a5cceb99c7e7587ce1a41ab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688835"
---
# <a name="application-deployment-evaluation"></a>应用程序部署评估

适用范围：  Configuration Manager (Current Branch)

在继续之前，请查看[应用程序部署客户端组件](client-components-technical-reference.md)以了解 DCM 和 CI 代理作业处理。

部署激活后，DCM 代理和 CI 代理组件将执行应用程序评估。 若要了解何时激活分配，请参阅[应用程序部署到设备集合](device-deployment-technical-reference.md)或[应用程序部署到用户集合](user-deployment-technical-reference.md)文章。

## <a name="application-detection-and-evaluation"></a>应用程序检测和评估

应用程序评估在 CI 代理作业的“InvokingSdmMethod”阶段执行  。 在此阶段，客户端会评估为应用程序定义的检测方法，以确认设备上是否安装了应用程序。 可以使用“部署类型唯一 ID”或“部署类型名称”在“AppDiscovery.log”中跟踪此活动  。

```text
Performing detection of app deployment type ConfigMgr Toolkit - Windows Installer (*.msi file)(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, revision 2) for system.
+++ Did not detect app deployment type ConfigMgr Toolkit - Windows Installer (*.msi file)(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, revision 2) for system.
```

> [!NOTE]
> 以上示例显示了对 MSI 应用程序的检测操作，其中，检测是通过检查设备上是否安装了 MSI 产品代码来完成的。 对于使用其他检测方法的应用程序，会使用适当的检测方法来检查是否安装了应用程序。

接下来，客户端根据部署目的评估应用程序的所需状态。 此步骤还包括检测应用程序是否有任何依赖关系或需要遵守的取代规则。 可以使用“应用程序和部署类型唯一 ID”在“AppIntentEval.log”中跟踪此活动  。

<pre><code class="lang-text"># Available Application Deployment

[Application or DT Unique ID] :- <b>Current State = NotInstalled, Applicability = Applicable, ResolvedState = Available</b>, ConfigureState = NotNeeded, Title = [Application or DT Name]

# Required Application Deployment

[Application or DT Unique ID] :- <b>Current State = NotInstalled, Applicability = Applicable, ResolvedState = Installed</b>, ConfigureState = NotNeeded, Title = [Application or DT Name]

# Requirement Rules Not Met

[Application or DT Unique ID] :- <b>Current State = NotInstalled, Applicability = NotApplicable, ResolvedState = None</b>, ConfigureState = NotNeeded, Title = [Application or DT Name]
</code></pre>

在以上的日志条目中，“当前状态”指示设备上当前是否安装了应用程序  。 “适用性”根据定义的要求规则指示应用程序是否适用  。 “ResolvedState”根据部署目的指示应用程序的所需状态  。

> [!TIP]
> 使用[部署监视工具](../../core/support/deployment-monitoring-tool.md)查看应用程序状态、适用性状态和要求违规情况。

## <a name="next-steps"></a>后续步骤

- [应用程序下载](deployment-download-technical-reference.md)
