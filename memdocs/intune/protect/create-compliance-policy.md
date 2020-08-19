---
title: 在 Microsoft Intune 中创建设备符合性策略 - Azure | Microsoft Docs
description: 在 Microsoft Intune 中：创建设备符合性策略，状态和严重性级别概述，使用 InGracePeriod 状态，使用条件访问，处理不具有分配策略的设备，以及 Azure 门户和经典门户中的符合性的差别
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/14/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9c1431105bdba9731bda4599e310889bfbf86a2c
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252248"
---
# <a name="create-a-compliance-policy-in-microsoft-intune"></a>在 Microsoft Intune 中创建符合性策略

使用 Intune 保护组织的资源时，设备符合性策略是一项关键功能。 在 Intune 中，可以创建规则和设置，设备必须满足这些设置（例如最低操作系统版本）才能被视为符合策略。 如果设备不符合，则可使用[条件访问](conditional-access.md)阻止对数据和资源的访问。

此外，还可针对不符合的情况采取措施，例如向用户发送通知电子邮件。 有关符合性策略的作用以及使用方式的概述，请参阅[设备符合性入门](device-compliance-get-started.md)。

本文：

- 列出了创建符合性策略的先决条件和步骤。
- 介绍如何将策略分配给用户和设备组。
- 介绍其他功能，包括用于“筛选”策略的作用域标记，以及可对不符合策略的设备采取的措施。
- 列出设备接收策略更新时的签入刷新周期时间。

## <a name="before-you-begin"></a>在开始之前

若要使用设备符合性策略，请务必：

- 使用以下订阅：

  - Intune
  - 如果使用条件访问，则需要 Azure Active Directory (AD) Premium 版本。 [Azure Active Directory 定价](https://azure.microsoft.com/pricing/details/active-directory/)列出了购买不同版本可获得的功能。 Intune 符合性不需要 Azure AD。

- 使用支持的平台：

  - Android 设备管理员
  - Android Enterprise
  - iOS
  - macOS
  - Windows 10
  - Windows 8.1

- 在 Intune 中注册设备（用于查看符合性状态）

- 向一个用户设备注册，或在没有主要用户的情况下注册。 不支持向多个用户注册设备。

## <a name="create-the-policy"></a>创建策略

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 选择“设备” > “符合性策略” > “策略” > “创建策略”。

3. 从以下选项中选择此策略的“平台”：
   - *Android 设备管理员*
   - *Android Enterprise*
   - *iOS/iPadOS*
   - *macOS*
   - *Windows 8.1 及更高版本*
   - *Windows 10 及更高版本*

    对于“Android Enterprise”，还可以选择一种“策略类型”：
     - Android 公司拥有的完全托管式专用工作配置文件策略
     - Android 工作配置文件合规性策略

    然后，选择“创建”以打开“创建策略”配置窗口。

4. 在“基本信息”选项卡上，指定“名称”，以便稍后识别它们。 例如，策略名称最好为“将已越狱的 iOS/iPadOS 设备标记为不合规策略”。

   还可以选择指定“说明”。
  
5. 在“合规性设置”选项卡上，展开可用类别，并为策略配置设置。  下面的文章介绍了每个平台的设置：
   - [Android 设备管理员](compliance-policy-create-android.md)
   - [Android Enterprise](compliance-policy-create-android-for-work.md)
   - [iOS/iPadOS](compliance-policy-create-ios.md)
   - [macOS](compliance-policy-create-mac-os.md)
   - [Windows 8.1 及更高版本](compliance-policy-create-windows-8-1.md)
   - [Windows 10 及更高版本](compliance-policy-create-windows.md)  

6. 在“位置”选项卡上，可以根据设备位置强制实施合规性。 从现有位置进行选择。 如果尚无可用位置，请参阅[使用位置（网络围墙）](use-network-locations.md)提供的指南。
   > [!TIP]
   > 位置仅适用于 Android 设备管理员平台。

7. 在“对不合规项的操作”选项卡上，指定一系列操作，以自动应用于不符合此合规性策略的设备。

   可以添加多个操作，并为某些操作配置计划和其他详细信息。 例如，可以将默认操作“标记不合规设备”的计划更改为一天后执行。 然后，可以添加一个操作，以便在设备不合规时向用户发送电子邮件，向他们通知此状态。 还可以添加操作以锁定或停用仍然不合规的设备。

   有关可以配置的操作的信息，请参阅[添加针对不合规设备的操作](actions-for-noncompliance.md)，包括了解如何创建通知电子邮件并发送给用户。

   另一个示例涉及位置的使用，可以至少向合规性策略添加一个位置。 在这种情况下，选择至少一个位置时，将应用针对不合规项的默认操作。 如果设备未连接到所选的任何位置，则被视为不合规。 可以配置计划，为用户提供宽限期（例如，一天）。

8. 在“范围标记”选项卡上，选择标记以帮助筛选特定组的策略，如 `US-NC IT Team` 或 `JohnGlenn_ITDepartment`。 添加设置后，还可以向符合性策略添加作用域标记。 

   有关使用范围标记的信息，请参阅[使用范围标记筛选策略](../fundamentals/scope-tags.md)。

9. 在“分配”选项卡上，向组分配策略。  

   选择“+ 选择要包括的组”，然后将策略分配给一个或多个组。 在下一步后保存策略时，策略将应用于这些组。 

10. 在“查看 + 创建”选项卡中，查看设置，然后在准备好保存合规性策略时选择“创建” 。  

    当策略所面向的用户或设备使用 Intune 签入时，会对其进行评估以确定是否满足合规性要求。

<!-- Evaluate option  - pending details as to its fate with this new Full Screen UI udpate  

### Evaluate how many users are targeted

When you assign the policy, you can also **Evaluate** how many users are affected. This feature calculates users; it doesn't calculate devices.

1. In Intune, select **Devices** > **Compliance policies** > **Policies**.

2. Select a *policy* > **Assignments** > **Evaluate**. A message shows you how many users are targeted by this policy.

If the **Evaluate** button is grayed out, make sure the policy is assigned to one or more groups.
-->

## <a name="refresh-cycle-times"></a>刷新周期时间

Intune 使用不同的刷新周期来检查符合性策略的更新。 如果设备是最近注册的，则会增加运行签入的频率。 [策略和配置文件刷新周期](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned)列出了估计的刷新时间。

用户可以随时打开公司门户应用，并同步设备以立即检查策略更新。

### <a name="assign-an-ingraceperiod-status"></a>分配 InGracePeriod 状态

符合性策略的 InGracePeriod 状态是一个值。 该值由设备的宽限期和设备针对该合规性策略的实际状态共同确定。

具体而言，如果设备的已分配符合性策略为“不符合”状态，且：

- 设备未分配到宽限期，则符合性策略的指定值为“不符合”
- 设备具有已到期的宽限期，则符合性策略的指定值为“不符合”
- 设备具有将来的宽限期，则符合性策略的指定值为“InGracePeriod”

下表概述了这些情况：

|实际符合性状态|指定的宽限期的值|有效符合性状态|
|---------|---------|---------|
|不符合 |未指定宽限期 |不符合 |
|不符合 |过去的日期|不符合|
|不符合 |将来的日期|InGracePeriod|

有关监视设备符合性策略的详细信息，请参阅[监视 Intune 设备符合性策略](compliance-policy-monitor.md)。

### <a name="assign-a-resulting-compliance-policy-status"></a>分配生成的符合性策略状态

如果设备具有多个符合性策略，且该设备分配到的两个或多个符合性策略的符合性状态各不相同，则系统会分配单个生成的符合性状态。 此分配基于向每个符合性状态指定的概念严重性级别。 每个符合性状态均包含以下严重性级别：

|状态  |严重性  |
|---------|---------|
|Unknown     |1|
|不适用     |2|
|合规|3|
|InGracePeriod|4|
|不符合|5|
|错误|6|

设备具有多个符合性策略时，系统会为该设备分配所有策略中的最高严重性级别。

例如，某台设备分配有三个符合性策略：一个处于“未知”状态（严重性 = 1），一个处于“符合”状态（严重性 = 3），还有一个处于 InGracePeriod 状态（严重性 = 4）。 InGracePeriod 状态具有最高的严重性级别。 因此，所有三个策略都处于 InGracePeriod 符合性状态。

## <a name="next-steps"></a>后续步骤

[监视策略](compliance-policy-monitor.md)。
