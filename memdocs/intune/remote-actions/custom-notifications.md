---
title: 使用 Microsoft Intune 向用户发送自定义通知
titleSuffix: Microsoft Intune
description: 使用 Intune 创建自定义推送通知并将其发送给使用 iOS/iPadOS 和 Android 设备的用户
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 02/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: jinyoon
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0ef8989c9f4de0211a7636c747ff9a01111842f6
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2020
ms.locfileid: "80325316"
---
# <a name="send-custom-notifications-in-intune"></a>使用 Intune 发送自定义通知

使用 Microsoft Intune 向使用托管 iOS/iPadOS 和 Android 设备的用户发送自定义通知。 这些消息在用户设备上显示为来自公司门户应用和 Microsoft Intune 应用的标准推送通知，就像设备上显示的来自其他应用程序的通知一样。 Windows 和 macOS 设备不支持 Intune 自定义通知。

自定义通知消息包括短标题和不超过 500 个字符的消息正文。 可以出于任何常规通信目的自定义这些消息。

### <a name="what-the-notification-looks-like-on-an-iosipados-device"></a>iOS/iPadOS 设备上通知的外观

如果在 iOS/iPadOS 设备上打开公司门户应用，则通知将类似于以下屏幕截图：

> [!div class="mx-imgBorder"]
> ![公司门户 iOS/iPadOS 测试通知](./media/custom-notifications/105046-1.png)

如果设备被锁定，通知将类似于以下屏幕截图：

> [!div class="mx-imgBorder"]
> ![锁定设备 iOS/iPadOS 测试通知](./media/custom-notifications/105046-2.png)

### <a name="what-the-notification-looks-like-on-an-android-device"></a>Android 设备上通知的外观

如果在 Android 设备上打开公司门户应用，则通知将类似于以下屏幕截图：

> [!div class="mx-imgBorder"]
> ![Android 测试通知](./media/custom-notifications/105046-3.png)

## <a name="common-scenarios-for-sending-custom-notifications"></a>发送自定义通知的常见方案  

- 通知所有员工关于时间表中发生的更改，例如因恶劣天气导致的办公楼关闭。
- 向单个设备的用户发送通知，以传达紧急请求，如重启设备以完成更新安装。

## <a name="considerations-for-using-custom-notifications"></a>使用自定义通知的注意事项

**设备配置**

- 设备必须安装公司门户应用或 Microsoft Intune 应用，用户才可以接收自定义通知。 它们还必须配置权限，以允许公司门户应用或 Microsoft Intune 应用发送推送通知。 如有必要，公司门户应用和 Microsoft Intune 应用会提示用户允许通知。
- 在 Android 上，Google Play Services 是必备依赖项。
- 设备必须已注册 MDM。

**权限**：

- 帐户必须在 Intune 中拥有以下 RBAC 权限，才可向组发送通知：  组织 > 更新  。
- 帐户必须在 Intune 中拥有以下 RBAC 权限，才可向设备发送通知：  远程任务 > 发送自定义通知  。

**创建通知**：
 
- 若要创建消息，请使用分配有 Intune 角色（包括前面“权限”部分所述的正确权限）的帐户  。 若要为用户分配权限，请参阅[角色分配](../fundamentals/role-based-access-control.md#role-assignments)。
- 自定义通知的标题最多允许 50 个字符，其消息最多允许 500 个字符。  
- Intune 不会保存以前发送的自定义通知中的文本。 若要重新发送消息，必须重新创建该消息。  
- 每小时最多只能向组发送 25 条消息。 此限制仅针对租户级别。 此限制不适用于向单个设备发送通知。
- 向单个设备发送消息时，每小时最多只可以向同一台设备发送 10 条消息。
- 可以向组内用户发送通知。 向组内用户发送通知时，每个通知都可以直接面向最多 25 个组。 嵌套组不计入此总数。 向单个组发送通知时，消息仅以该组中的用户为目标，并发送到用户已注册的每个 iOS/iPadOS 或 Android 设备。 如果以通知为目标，则将忽略该组中的设备。
- 可以向单个设备发送通知。 选择一个设备，然后使用远程[设备操作](device-management.md#available-device-actions)发送自定义通知，而非使用组。

**发送**：

- Intune 将消息发送到用户的公司门户应用或 Microsoft Intune 应用，然后创建推送通知。 用户无需登录应用，即可在设备上推送通知，但是设备必须经由目标用户注册完成。
- Intune、公司门户应用和 Microsoft Intune 应用无法保证发送自定义通知。 自定义通知可能会在几个小时的延迟后显示（如果有的话），因此它们不应用于紧急消息。
- 来自 Intune 的自定义通知消息在设备上显示为标准推送通知。 如果公司门户应用在收到通知后在 iOS/iPadOS 设备上处于打开状态，则通知将在应用中显示，而不在推送通知中显示。  
- 自定义通知可以在 iOS/iPadOS 和 Android 设备的锁屏界面上显示，具体取决于设备设置。  
- 在 Android 设备上，其他应用可能可以访问自定义通知中的数据。 请勿将其用于敏感通信。  
- 最近未注册设备的用户或从组中删除的用户可能仍会收到之后发送到该组的自定义通知。  同样，如果在向组发送自定义通知后将用户添加到组，则新添加的用户可能会收到之前发送的通知消息。  

## <a name="send-a-custom-notification-to-groups"></a>向组发送自定义通知

1. 使用有权创建和发送通知的帐户登录 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，然后转至“租户管理” > “自定义通知”   。  

2. 在“基本信息”选项卡上，指定以下各项，然后选择“下一步”以继续  。  
   - **标题** - 指定此通知的标题。 标题最多允许 50 个字符。  
   - **正文** - 指定消息。 消息最多允许 500 个字符。

   ![创建自定义通知](./media/custom-notifications/custom-notifications.png)  

3. 在“分配”选项卡上，选择要向其发送此自定义通知的组，然后选择“下一步”以继续  。 向组发送通知将仅以该组的用户为目标；通知将发送到该用户注册的所有 iOS/iPadOS 和 Android 设备。

4. 在“查看 + 创建”选项卡上查看信息，并在准备好发送通知后，选择“创建”   。  

Intune 会立即处理你创建的消息。 消息已发送的唯一确认就是确认已发送自定义通知的 Intune 通知。  

![发送通知确认](./media/custom-notifications/notification-sent.png)  

Intune 不会跟踪你发送的自定义通知，并且设备不会在设备的通知中心之外记录回执。 如果用户在公司门户或 Intune 应用内请求支持，则可以将通知内容包含在临时诊断日志中。

## <a name="send-a-custom-notification-to-a-single-device"></a>向单个设备发送自定义通知

1. 使用可以创建和发送通知的帐户登录 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，然后转至“设备” > “所有设备”   。

2. 双击要向其发送通知的受管理设备的名称，以打开该设备的“概述”  页。

3. 在该设备的“概述”页上，选择“发送自定义通知”设备操作，打开“发送自定义通知”窗格    。 如果此选项不可用，请从页面右上角选择“...”  （省略号）选项，然后选择“发送自定义通知”  。

4. 在“发送自定义通知”  窗格上，指定以下消息详细信息：  

   - **标题** - 指定此通知的标题。 标题最多允许 50 个字符。  
   - **正文** - 指定消息。 消息最多允许 500 个字符。  

5. 选择“发送”，向设备发送自定义通知。  与向组发送的通知不同，在发送消息前，不配置分配或查看消息。  

Intune 会立即处理该消息。 消息已发送的唯一确认方式是将从控制台收到的 Intune 通知，它将显示所发送的消息文本。  

## <a name="receive-a-custom-notification"></a>接收自定义通知

用户可以在设备上看到作为标准推送通知由 Intune 从公司门户应用或 Microsoft Intune 应用发送的自定义通知消息。 这些通知类似于用户从设备上的其他应用接收的推送通知。  

在 iOS/iPadOS 设备上，如果在收到通知时公司门户应用处于打开状态，则通知将在应用中显示，而不在推送通知中显示。  

通知将一直保留，除非用户将其关闭。  

## <a name="next-steps"></a>后续步骤

[管理设备](device-management.md)
