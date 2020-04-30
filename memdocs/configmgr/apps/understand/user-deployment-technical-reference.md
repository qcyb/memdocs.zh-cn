---
title: 有关用户应用部署的技术参考
titleSuffix: Configuration Manager
description: 关于将应用程序部署到用户的 Configuration Manager 故障排除技术参考。
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: b8e9dbfe-a046-4e06-8dec-cf0bc41ba095
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b44aad1db96b4191b9c9537acea4e64b1d30fde6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690265"
---
# <a name="application-deployment-policy-for-users"></a>用户应用程序部署策略

适用范围：  Configuration Manager (Current Branch)

将应用程序部署到用户集合时，仅为“必需”的部署创建部署策略。 对于“可用”部署，在用户尝试从软件中心安装应用程序时创建策略。 本文介绍“必需”和“可用”部署的部署过程。

> [!TIP]
> 若要查看客户端日志，可以通过运行[开始之前](app-deployment-technical-reference.md#before-you-begin)部分中提到的 SQL 查询来获取所有必要的相关信息。

## <a name="required-deployments"></a>“必需”部署

在部署创建后，有关将“必需”应用程序部署到用户集合的策略适用于集合中的所有用户。 这些部署的客户端处理过程与必需的设备集合部署相似。 部署激活发生在定义的“可用时间”，强制执行发生在定义的“截止时间”。 有关详细信息，请参阅[应用程序部署到设备集合](device-deployment-technical-reference.md)。

## <a name="available-deployments"></a>可用部署

采用“可用部署”方式部署到用户集合的应用程序的行为有所不同。 此行为上的不同使管理员不仅能向用户提供应用程序，还不会导致策略的资源争用。 当用户启动软件中心时，会从管理点实时查询用户可用的应用程序列表。 此请求对管理点上的 `CMUserService_WindowsAuth` 虚拟目录发出，可以在客户端上的“SCClient_[UserName].log”中看到  。

```text
Using endpoint Url: https://MP.CONTOSO.COM:443/CMUserService_WindowsAuth, Windows authentication
```

当管理点接收到此请求时，它通过执行 `usp_GetApplicationPropertyValuesFiltered` 存储过程来查询用户可用的应用程序列表。 可在管理点上的“UserService.log”中跟踪此活动  。

```text
GetFilteredApplications, startItem = 0, max rows = 60, search text = '', filter = '', user = CONTOSO\UserName, api = 4.0, source = UserService_WinAuth_SoftwareCenter, platform = <OSPlatform>
GetFilteredApplications: returned 1 rows out of 1 total
```

软件中心接收到列表并显示用户可以安装的应用程序。 当用户单击应用程序时，将从管理点查询有关该应用程序的其他信息，这涉及 usp_GetApplicationInfo、usp_getappmodelsapplicationsupersedence、usp_GetDeploymentTypeForAnApp 等存储过程的执行。

当用户选择应用程序并单击“安装”按钮时，将激活部署，并创建一个 DCM 代理作业来评估应用程序  。 如果应用程序可用，会创建另一个 DCM 代理作业来下载和执行应用程序。 可以在客户端的“DCMAgent.log”中跟踪此活动  。

## <a name="next-steps"></a>后续步骤

- [了解应用程序部署客户端组件](client-components-technical-reference.md)
