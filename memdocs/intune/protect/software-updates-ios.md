---
title: 使用 Microsoft Intune 配置 iOS/iPadOS 软件更新策略 - Azure | Microsoft Docs
description: 使用 Microsoft Intune 创建或添加配置策略，以限制软件更新在 iOS/iPadOS 设备上自动安装的时间。 可以选择不安装更新的日期和时间。 还可以将此策略分配给组、用户或设备，并检查是否存在任何安装故障。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0a81e0e59eca03c9c15d7553376ea0c524251a18
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914848"
---
# <a name="add-iosipados-software-update-policies-in-intune"></a>使用 Intune 添加 iOS/iPadOS 软件更新策略

软件更新策略可强制受监督的 iOS/iPadOS 设备自动安装 OS 更新。 受监督的设备是使用 Apple Business Manager 或 Apple School Manager 注册的设备。 配置部署更新策略时，可以执行以下操作：

- 选择部署可用的“最新更新”，如果不想部署最新更新，请选择按更新版本号部署较旧的更新。 如果选择部署较旧的更新，则还必须设置设备配置策略，以限制软件更新可见性。
- 指定一个计划，确定安装更新的时间。 计划可以非常简单，例如在下一次设备签入时安装更新，或者创建安装更新或阻止安装更新的日期和时间范围。

此功能适用于：

- iOS 10.3 及更高版本（受监督）
- iPadOS 13.0 及更高版本（受监督）

默认情况下，设备会通过 Intune 大约每 8 小时签入一次。 如果通过更新策略提供更新，则该设备会下载该更新。 然后，设备会在下一次在计划配置中签入时安装更新。 尽管更新过程通常不涉及到任何用户交互，但如果设备有密码，则用户必须输入密码才能启动软件更新。 配置文件无法阻止用户手动更新操作系统。 可以阻止用户使用设备配置策略手动更新 OS，以限制软件更新可见性。

> [!NOTE]
> 如果使用[自治单应用模式 (ASAM)](../configuration/device-restrictions-ios.md#autonomous-single-app-mode-asam)，则应考虑操作系统更新的影响，因为可能由此产生不良行为。
考虑进行测试，评估操作系统更新对你在 ASAM 中运行的应用的影响。

## <a name="configure-the-policy"></a>配置策略

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“设备” > “适用于 iOS/iPadOS 的更新策略” > “创建配置文件”  。
3. 在“基本信息”选项卡上，为该策略指定名称并指定描述（可选），然后选择“下一步” 。

   ![“基本信息”选项卡](./media/software-updates-ios/basics-tab.png)

4. 在“更新策略设置”选项卡上，配置以下设置：

   1. 选择要安装的版本。 可以选择：

      - 最新更新：这会为 iOS/iPadOS 部署最近发布的更新。
      - 下拉框中提供的任何早期版本。 如果选择早期版本，则还必须部署设备配置策略，以延迟显示软件更新。

   2. **计划类型**：配置该策略的计划：

      - 下次签入时更新：更新将在设备下一次通过 Intune 签入时进行安装。 这是最简单的选项，无需其他配置。
      - 在计划时间内更新：可以配置一个或多个时间段，在此期间将在签入时安装更新。
      - 在计划时间外更新：可以配置一个或多个时间段，在此期间将不会在签入时安装更新。

   3. **每周计划**：如果选择的计划类型不是“下次签入时更新”，请配置以下选项：

      ![选择在计划时间更新的示例](./media/software-updates-ios/scheduled-time.png)

      - **时区**：选择时区。
      - **时间范围**：定义一个或多个限制更新安装时间的时间段。 以下选项的效果取决于所选的计划类型。 通过使用开始日期和结束日期，将支持长段时间。 选项包括：

        - **开始日期**：选择计划时段开始的日期。
        - **开始时间**：选择计划时段开始的时间。 例如，如果选择“凌晨 5 点”，并选择计划类型为“在计划时间内更新”，则会在凌晨 5 点开始安装更新。 如果选择计划类型为“在计划时间之外更新”，则不会在凌晨 5 点开始安装更新。
        - **结束日期**：选择计划时段结束的日期。
        - **结束时间**：选择计划时段结束的时间。 例如，如果选择“凌晨 1 点”，并选择计划类型为“在计划时间内更新”，则凌晨 1 点不再安装更新。 如果选择计划类型为“在计划时间之外更新”，则凌晨 1 点会开始安装更新。

       如果未配置开始时间或结束时间，则配置不会产生限制，随时都可以安装更新。  

       > [!NOTE]
       > 可在[设备限制](../configuration/device-restrictions-ios.md#general)中配置设置，使更新于一段时间内在受监管的 iOS/iPadOS 设备上对设备用户不可见。 通过限制期，可在更新可供用户安装之前对其进行测试。 设备限制期限到期后，用户便可看到该更新。 然后，用户可选择安装更新，否则软件更新策略可能会在不久后自动安装它。
       >
       > 使用设备限制隐藏更新时，请查看软件更新策略，确保它们不会在该限制期间结束之前计划安装更新。 软件更新策略会根据自己的计划来安装更新，而不管更新对设备用户是隐藏的还是可见的。

   配置“更新策略设置”之后，选择“下一步”。

5. 若要将标记应用于更新策略，请在“作用域标记”选项卡上，选择“+ 选择作用域标记”以打开“选择标记”窗格 。

   - 在 **“选择标记”** 窗格中，选择一个或多个标记，然后单击 **“选择”** 以将其添加到策略，然后返回 *“作用域标记”* 窗格。

   准备就绪后，选择“下一步”，转到“分配”。

6. 在“分配”选项卡上，选择“+ 选择要包括的组”，然后将更新策略分配到一个或多个组 。 使用“+ 选择要排除的组”对分配进行相应调整。 准备就绪后，选择“下一步”继续操作。

   需对策略目标用户所用的设备进行更新符合性评估。 此策略还支持无用户设备。

7. 在“查看 + 创建”选项卡中，查看设置，然后在已准备好保存 iOS/iPadOS 更新策略时选择“创建” 。 新策略显示在 iOS/iPadOS 更新策略列表中。

如需 Intune 支持团队的指导，请参阅[在 Intune 中为受监督的设备延迟软件更新可见性](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Delaying-visibility-of-software-updates-in-Intune-for-supervised/ba-p/345753)。

> [!NOTE]
> Apple MDM 不允许强制设备在特定时间或日期前安装更新。 无法使用 Intune 软件更新策略来降低设备上的操作系统版本级别。

## <a name="edit-a-policy"></a>编辑策略

可以编辑现有策略，包括更改限制时间：

1. 选择“设备” > “适用于 iOS 的更新策略”。 选择要编辑的策略。

2. 在查看策略“属性”时，为要修改的策略页面选择“编辑” 。

   ![编辑策略](./media/software-updates-ios/edit-policy.png)

3. 进行更改后，选择“查看 + 保存” > “保存”，保存所做的修改，然后返回策略“属性” 。

> [!NOTE]
> 如果“开始时间”和“结束时间”都设为凌晨 12 点，则 Intune 不会检查有关更新安装时间的限制 。 这意味着将忽略已有的任何“选择阻止安装更新的时间”配置，结果是可以随时安装更新。

## <a name="monitor-device-installation-failures"></a>监视设备安装故障

<!-- 1352223 -->
“软件更新” > “iOS/iPadOS 设备安装故障”列出了虽是策略更新目标，但尝试更新后却未能成功更新的受监督 iOS 设备 。 可以查看每个设备的状态，了解该设备未自动更新的原因。 运行正常的最新版本设备不会显示在该列表中。 “最新版本”设备包括设备本身支持的最新更新。

## <a name="next-steps"></a>后续步骤

[监视其状态](../configuration/device-profile-monitor.md)。