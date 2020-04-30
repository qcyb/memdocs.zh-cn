---
title: 不符合要求的 Microsoft Intune 操作及相关消息 - Azure | Microsoft Docs
description: 创建通知电子邮件，发送到不符合的设备。 在设备被标记为“不符合”后添加操作，例如添加宽限期以符合要求，或创建计划用于阻止访问在满足符合要求之前进行访问。 在 Azure 中使用 Microsoft Intune 完成此操作。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/17/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.reviewer: samyada
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b8b8bde6b7979cfe3b936a08630e23e19fc7e5a0
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81615053"
---
# <a name="configure-actions-for-noncompliant-devices-in-intune"></a>为 Intune 中不符合要求的设备配置操作

对于不满足符合性策略或规则的设备，可添加针对非符合性的操作  。 此功能会配置一系列按时间顺序排列的操作，例如向最终用户发送电子邮件等。

## <a name="overview"></a>概述

默认情况下，每个符合性策略都包括针对不符合性的操作（即“将设备标记为不符合”），计划为零 (0) 天   。 此默认设置使得在 Intune 检测到不符合的设备时，会立即将它标记为“不符合”。 然后，Azure Active Directory (AD) [条件访问](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)会阻止设备。

通过配置针对不符合性的操作，你可灵活决定如何处理不符合的设备以及何时处理  。 例如，你可选择不立即阻止设备，并给予用户宽限期以使其符合要求。

对于可设置的每个操作，都可配置一个计划，该计划根据将设备标记为“不符合”后的天数来确定该操作何时生效。 你还可配置一个操作的多个实例。 在策略中设置一个操作的多个实例时，如果设备仍然不符合要求，则该操作将在稍后的计划时间再次运行。

并非所有操作都适用于所有平台。

## <a name="available-actions-for-noncompliance"></a>可用于处理不符合性的操作

下面是可用于处理不符合性的操作。 除非另有说明，否则每个操作都可用于 Intune 支持的所有平台：

- **将设备标记为不符合**：默认情况下，此操作针对每个符合性策略进行设置，且计划为零 (0) 天，也就是立即将设备标记为“不符合”  。

  更改默认计划时，会提供一个宽限期。在此期间，用户可修正问题，或者变得符合要求而不是被标记为“不符合”。

- **向最终用户发送电子邮件**：此操作将向用户发送电子邮件通知。
启用此操作时：

  - 选择此操作发送的通知消息模板  。 必须[创建通知消息模板](#create-a-notification-message-template)，然后才能将其分配给此操作。 创建自定义通知时，可自定义主题和邮件正文，还可包含公司徽标、公司名称和其他联系信息。
  - 通过选择一个或多个 Azure AD 组，选择将邮件发送给其他收件人。

发送电子邮件时，Intune 会在电子邮件通知中附上不符合设备的详细信息。

- **远程锁定不符合要求的设备**：使用此操作可发出设备的远程锁定指令。 然后提示用户输入 PIN 或密码以解锁设备。 [远程锁定](../remote-actions/device-remote-lock.md)功能的详细信息。

- **停用不符合要求的设备**：此操作将从设备中删除所有公司数据并从 Intune 管理中删除设备。 为防止意外擦除设备，此操作支持的最短计划时间为 30 天  。

  以下平台支持此操作：
  - Android
  - iOS
  - macOS
  - Windows 10 移动版
  - Windows Phone 8.1 及更高版本

  了解有关[停用设备](../remote-actions/devices-wipe.md#retire)的详细信息。

- **向最终用户发送推送通知**：配置此操作，以通过设备上的公司门户应用或 Intune 应用向该设备发送有关不符合性的推送通知。

  以下平台支持此操作：
  - Android：
    - Android 设备管理员
    - Android Enterprise 设备所有者
    - Android Enterprise 工作配置文件
  - iOS/iPadOS

  设备首次向 Intune 签入并被发现不遵守符合性性策略时，系统会发送推送通知。 当用户选择通知时，公司门户应用或 Intune 应用会打开并显示不符合原因的相关信息。 用户随后可采取操作来解决问题。 有关不符合性的消息详细信息由 Intune 生成，无法自定义。

  > [!IMPORTANT]
  > Intune、公司门户应用和 Microsoft Intune 应用无法保证发送推送通知。 通知可能会延迟几小时后显示（若有）。 例如，如果用户关闭了推送通知，则可能会延迟。
  >
  > 不要依靠这种通知方法来获取紧急消息。

  操作的每个实例一次发送一个通知。 若要从策略再次发送相同的通知，请在该策略中配置该操作的其他实例，每个实例具有不同的计划。
  
  例如，你可将第一个操作计划为零天，然后添加该操作的第二个实例并将其计划设为三天。 在第二次通知之前出现的这种延迟会给用户几天时间来解决问题，从而避免第二次通知。

  为了避免向用户发送过多的重复消息，请检查哪些符合性策略包括关于不符合性的推送通知并进行简化，同时检查计划，避免过于频繁地就同一问题发送重复通知。

  请注意以下几点：
  - 如果一个策略的多个实例设为同一天发送推送通知，则当天只发送一则通知。

  - 如果多个符合性策略包含相同的符合性条件，并包含具有相同计划的推送通知操作，则会在同一天向同一台设备发送多个通知。

## <a name="before-you-begin"></a>在开始之前

可在配置设备符合性策略时[添加针对不符合性的操作为](#add-actions-for-noncompliance)，也可稍后通过编辑策略来添加操作。 可向每个策略添加额外的操作来满足你的需求。 请记住，每个符合性策略都自动包含针对不符合性的默认操作（即“将设备标记为不符合”），计划设置为零天。

若要使用设备符合性策略来阻止设备使用公司资源，必须设置 Azure AD 条件访问。 请参阅 [Azure Active Directory 中的条件访问](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)或[使用 Intune 条件访问的常见方式](conditional-access-intune-common-ways-use.md)以获取指南。

要创建设备符合性策略，请查看下面的平台特定指南：

- [Android](compliance-policy-create-android.md)
- [Android 工作配置文件](compliance-policy-create-android-for-work.md)
- [iOS](compliance-policy-create-ios.md)
- [macOS](compliance-policy-create-mac-os.md)
- [Windows](compliance-policy-create-windows.md)

## <a name="create-a-notification-message-template"></a>创建通知邮件模板

要向用户发送电子邮件，请创建通知消息模板。 设备不符合要求时，在模板中输入的详细信息将显示在发送给用户的电子邮件中。

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“设备”   > “符合性策略”   > “通知”   > “创建通知”  。
3. 在“基本”  下，指定以下信息：

   - **Name**
   - **主题**
   - **Message**

4. 此外，在“基本”  下，配置以下通知选项，这些选项都默认为“启用”  ：

   - **电子邮件标头 – 包括公司徽标**
   - **电子邮件页脚 – 包括公司名称**
   - **电子邮件页脚 – 包括联系人信息**

   作为公司门户品牌的一部分上传的徽标可用于电子邮件模板。 有关公司门户品牌的详细信息，请参阅[公司标识品牌自定义](../apps/company-portal-app.md#customizing-the-user-experience)。

   ![Intune 中符合性通知邮件的示例](./media/actions-for-noncompliance/actionsfornoncompliance-1.PNG)

   选择“下一步”继续操作  。

5. 在“查看 + 创建”  下，查看你的配置以确保通知消息模板已准备就绪可供使用。 选择“创建”  以成功创建通知。

> [!NOTE]
> 你还可以选择之前创建的现有通知模板，并选择“编辑”  来编辑其信息以更新模板。

## <a name="add-actions-for-noncompliance"></a>添加针对非符合性的操作

创建设备符合性策略时，Intune 会自动为非符合性创建操作。 如果设备不满足符合性策略的要求，此操作会将设备标记为不符合。 可自定义将设备标记为不符合的时长。 此操作不可撤消。

还可在创建符合性策略或更新现有策略时添加可选操作。

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 选择“设备”   > “符合性策略”   > “策略”  ，选择其中一个策略，然后选择“属性”  。

   尚没有策略？ 创建 [Android](compliance-policy-create-android.md)、[iOS](compliance-policy-create-ios.md)、[Windows](compliance-policy-create-windows.md) 或其他平台策略。

   > [!NOTE]
   > 此时，JAMF 设备和面向设备组的设备无法接收符合性操作。

3. 选择“针对非符合性的操作” > “添加”   。

4. 选择“操作”： 

   - **向最终用户发送电子邮件**：当设备不符合要求时，选择给用户发送电子邮件。 此外：
     - 选择此前创建的“消息模板” 
     - 通过选择组输入任何“其他收件人” 

   - **远程锁定不符合要求的设备**：当设备不符合要求时，锁定设备。 该操作会强制用户输入 PIN 或密码来解锁设备。

   - **停用不符合要求的设备**：当设备不符合要求时，从设备中删除所有公司数据并从 Intune 管理中删除设备。 为防止意外擦除设备，此操作支持的最短计划时间为 30 天  。

   - **向最终用户发送推送通知**：配置此操作，以通过设备上的公司门户应用或 Intune 应用向该设备发送有关不符合性的推送通知。

5. 配置计划  :输入非符合性状态触发用户设备操作之后的宽限天数（0 到 365 天）。 （停用不合规的设备  支持的最短时间为 30 天。）在此宽限期后，可以强制执行[条件访问](conditional-access-intune-common-ways-use.md)策略。 如果输入“0”（零）天，则条件访问将立即生效   。 例如，如果设备不合规，请使用条件访问来立即阻止对电子邮件、SharePoint 和其他组织资源的访问。

   在你创建合规性策略时，“标记不合规设备”  操作会自动创建，并自动设置为“0”  天（即立即执行）。 通过此操作，当设备签入时，系统会立即将设备评估为不合规。 如果还使用条件访问，条件访问会立即生效。 若要给予宽限期，请更改“标记不合规设备”  操作中的“计划”  。

   在合规性策略中，假设还想要通知用户。 可以添加“向最终用户发送电子邮件”  操作。 在此“发送电子邮件”  操作中，将“计划”  设置为“2”天。 如果设备或最终用户在第 2 天仍被评估为不合规，系统就会在第 2 天发送电子邮件。 若要在被评估为不合规的第 5 天再次向用户发送电子邮件，请添加另一个操作，并将“计划”  设置为“5”天。

  若要详细了解合规性和内置操作，请参阅[合规性概述](device-compliance-get-started.md)。

6. 完成后，选择“添加” > “确定”，保存所做更改   。

## <a name="next-steps"></a>后续步骤

[监视策略](compliance-policy-monitor.md)。
