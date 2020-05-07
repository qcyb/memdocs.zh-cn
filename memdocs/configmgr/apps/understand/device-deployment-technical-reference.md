---
title: 关于将应用程序部署到设备集合的技术参考
titleSuffix: Configuration Manager
description: 关于将应用程序部署到设备集合的 Configuration Manager 故障排除技术参考。
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 4e62b04d-fe56-42ed-87dc-e673cf061d52
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1965029a1933793057dc5768bacb391afd645404
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688785"
---
# <a name="application-deployment-for-device-collections"></a>将应用程序部署到设备集合

适用范围：  Configuration Manager (Current Branch)

将应用程序部署到设备集合时，策略定目标到集合中的所有设备，而不考虑部署目的。 本文介绍了客户端上的策略下载和部署处理。

> [!TIP]
> 若要获取审阅客户端日志所必需的全部信息，可以运行[“开始前”](app-deployment-technical-reference.md#before-you-begin)部分中引用的 SQL 查询。

## <a name="policy-download"></a>策略下载

在应用程序部署策略定目标到客户端后，客户端会在下一个策略轮询周期下载策略。 下载策略时，客户端除了下载部署策略外，还下载相关策略。 这些相关策略包括应用程序策略、部署类型策略、全局条件策略等。可以使用应用程序或分配唯一 ID 在客户端上的 PolicyAgent.log  中跟踪策略下载活动。

<pre><code class="lang-text">Download of policy CCM_Policy_Policy5.PolicyID="{<b>3AC57DFE-3F87-4C59-930B-B9F57CB41B91</b>}",PolicySource="SMS:PS1",PolicyVersion="1.00" completed (DTS Job ID: {AE88E639-0E59-40D7-AAA9-4403AAE6EE82})
Policy state for [CCM_Policy_Policy5.PolicyID="{<b>3AC57DFE-3F87-4C59-930B-B9F57CB41B91</b>}",PolicySource="SMS:PS1",PolicyVersion="1.00"] is currently [Active]
</code></pre>

当策略下载到客户端上后，计划程序组件创建部署激活和强制计划。

## <a name="deployment-activation"></a>部署激活

在部署激活后，应用程序评估便会启动。 计划程序组件创建在部署中配置的可用时间激活分配的计划。 可以使用应用程序分配唯一 ID 在客户端上的 Scheduler.log  中跟踪此活动。

- 对于必需  部署，会创建激活计划，但会有最长为两个小时的延迟，以免站点服务器和分发点上发生资源争用。 延迟有助于避免争用，因为如果根据定义的要求规则应用程序是适用的，可能会在评估过程中下载应用程序内容。

    <pre><code class="lang-text">SMSTrigger '15AF8C4000080000' for scheduler '<b>Machine/{5F2FA409-C9B2-4100-8BC8-051820311DE1}</b>' will fire at 08/15/2019 01:44:00 PM with randomization.
    </code></pre>

- 对于可用  部署，会创建在部署中配置的可用时间触发的激活计划。

    <pre><code class="lang-text">SMSTrigger '1E4F8C4000080001' for scheduler '<b>Machine/{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}</b>' will fire at 08/15/2019 01:13:33 PM without randomization.
    </code></pre>

到了计划时间，计划程序组件会向 DCM 代理发送激活消息，以执行应用程序评估。

<pre><code class="lang-text">Sending message for schedule '<b>Machine/{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}</b>' (Target: 'direct:DCMAgent', Name: '')
</code></pre>

DCM 代理会收到激活消息，并创建应用程序评估作业。

```text
CDCMAgent::HandleMessage - Message received for machine: '<?xml version='1.0' ?><CIAssignmentMessage MessageType='Activation'><AssignmentID>{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}</AssignmentID></CIAssignmentMessage>'
```

## <a name="deployment-enforcement"></a>部署强制

如果强制部署，则会启动应用程序安装。

- 对于必需  部署，计划程序会在策略下载后创建截止时间计划，用于在部署截止时间强制部署应用程序。 默认情况下，截止时间计划并不是随机选择的。 可以通过[“禁用截止时间随机选择”](../../core/clients/deploy/about-client-settings.md#disable-deadline-randomization)客户端设置来控制激活的随机选择行为。

    <pre><code class="lang-text">SMSTrigger '15EF8C4000080000' for scheduler '<b>Machine/DEADLINE:{5F2FA409-C9B2-4100-8BC8-051820311DE1}</b>' will fire at 08/15/2019 03:05:00 PM without randomization.
    </code></pre>

    到了截止时间，计划程序组件会向 DCM 代理发送截止时间消息。 

    <pre><code class="lang-text">Sending message for schedule '<b>Machine/DEADLINE:{5F2FA409-C9B2-4100-8BC8-051820311DE1}</b>' (Target: 'direct:DCMAgent', Name: '')
    </code></pre>

    DCM 代理会收到截止时间消息，并创建应用程序部署强制作业。
  
    ```text
    CDCMAgent::HandleMessage - Message received for machine: '<?xml version='1.0' ?><CIAssignmentMessage MessageType='EnforcementDeadline'><AssignmentID>{5F2FA409-C9B2-4100-8BC8-051820311DE1}</AssignmentID></CIAssignmentMessage>'
    ```

    > [!NOTE]
    > 对于截止时间已过去的部署，应用程序会立即由执行评估、下载和安装操作的同一 DCM 代理作业来激活并强制部署。

- 对于可用  部署，并没有截止时间计划，因为当用户从软件中心启动应用程序安装时就会强制部署。 当用户开始安装时，会创建 DCM 代理作业，用于执行应用程序评估、下载和安装。 可以在客户端上的 DCMAgent.log  中跟踪此活动。

## <a name="next-steps"></a>后续步骤

- [了解应用程序部署客户端组件](client-components-technical-reference.md)
