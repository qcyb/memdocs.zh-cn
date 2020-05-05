---
title: 设备操作故障排除
titleSuffix: Configuration Manager
description: 排查 Configuration Manager 的设备操作技术参考
ms.date: 04/01/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 44c2eb8a-3ccc-471f-838b-55d7971bb79e
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 72da589a3f4213fb64b4123d5580cb1be945de0e
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "82140272"
---
# <a name="troubleshooting-device-actions-for-configuration-manager-devices"></a>Configuration Manager 设备的设备操作故障排除

适用范围：  Configuration Manager (Current Branch)

从 Configuration Manager 2002 开始，Configuration Manager 客户端可以同步到 Microsoft 终结点管理器管理中心。 在同步的客户端上，可以从 Microsoft 终结点管理器管理中心运行一些客户端操作。

可用的操作包括：
- 同步计算机策略
- 同步用户策略
- 应用评估周期


[![Microsoft 终结点管理器管理中心中的设备概述](./media/3555758-device-overview-actions.png)](./media/3555758-device-overview-actions.png#lightbox)
  
当管理员从 Microsoft 终结点管理器管理中心运行某一操作时，通知请求会转发到 Configuration Manager 站点，并从该站点转发到客户端。

## <a name="configuration-manager-components"></a>Configuration Manager 组件

- **SMS_SERVICE_CONNECTOR**：使用网关通知辅助角色从 Microsoft 终结点管理器管理中心处理通知。
- **SMS_NOTIFICATION_SERVER**：获取通知并创建客户端通知。
- **BgbAgent**：客户端获取任务并运行请求的操作。

## <a name="sms_service_connector"></a>SMS_SERVICE_CONNECTOR

当从 Microsoft 终结点管理器管理中心启动操作时， **CMGatewayNotificationWorker**将处理该请求。  

```text
Received new notification. Validating basic notification details...
Validating device action message content...
Authorized to perform client action. TemplateID: RequestMachinePolicy TenantId: a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2 AADUserID:     a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2
Forwarded BGB remote task. TemplateID: 1 TaskGuid: a43dd1b3-a006-4604-b012-5529380b3b6f TaskParam: TargetDeviceIDs: 1  
```
 
1. 从 Microsoft 终结点管理器管理中心收到通知。

   ```text
   Received new notification. Validating basic notification details..
   ```

1. 验证用户和设备操作。

   ```text
   Validating device action message content... 
   Authorized to perform client action. TemplateID: RequestMachinePolicy TenantId: a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2 AADUserID:     a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2
   ```

1. 远程任务将转发到 SMS_NOTIFICATION_SERVER。

    ```text
   Forwarded BGB remote task. TemplateID: 1 TaskGuid: a43dd1b3-a006-4604-b012-5529380b3b6f TaskParam: TargetDeviceIDs: 1  
    ```


## <a name="sms_notification_server"></a>SMS_NOTIFICATION_SERVER

将消息发送到 SMS_NOTIFICATION_SERVER 后，会将任务从管理点发送到相应的客户端。 在管理点上的**bgbserver.log**中会显示以下内容：

```text
Get one push message from database.
Starting to send push task (PushID: 7 TaskID: 8 TaskGUID: A43DD1B3-A006-4604-B012-5529380B3B6F TaskType: 1 TaskParam: ) to 1 clients  with throttling (strategy: 1 param: 42)
```

## <a name="bgbagent"></a>BgbAgent

最后一步出现在客户端上，可在**CcmNotificationAgent**中查看。 一旦接收到任务，它将请求计划程序执行该操作。 执行操作时，将显示一条确认消息：

```text
Receive task from server with pushid=7, taskid=8, taskguid=A43DD1B3-A006-4604-B012-5529380B3B6F, tasktype=1 and taskParam=

Send Task response message <BgbResponseMessage TimeStamp="2020-01-21T15:43:43Z"><PushID>8</PushID><TaskID>9</TaskID><ReturnCode>1</ReturnCode></BgbResponseMessage> successfully.
```

## <a name="common-issues"></a>常见问题

如果管理员在 Configuration Manager 中没有所需的权限，你将在`Unauthorized` **CMGatewayNotificationWorker**中看到一个响应。

```text
Received new notification. Validating basic notification details..
Validating device action message content...
Unauthorized to perform client action. TemplateID: RequestMachinePolicy TenantId: a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2 AADUserID: 3a1e89e6-e190-4615-9d38-a208b0eb1c78
```  

确保从 Microsoft 终结点管理器管理中心运行操作的用户在 Configuration Manager 站点上具有所需的权限。 有关详细信息，请参阅[Microsoft 终结点管理器租户附加必备组件](device-sync-actions.md#prerequisites)。

## <a name="next-steps"></a>后续步骤

[启用共同管理](../comanage/overview.md)，以获取其他云驱动功能，如条件性访问。
