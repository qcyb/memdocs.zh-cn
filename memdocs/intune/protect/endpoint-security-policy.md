---
title: 在 Microsoft Intune 中管理终结点安全策略 | Microsoft Docs
description: 了解安全管理员如何使用终结点安全策略和配置文件来关注 Microsoft Endpoint Manager 中设备的安全配置。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/15/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 071cab69b652193b835282603e187e4f3d0c7b0d
ms.sourcegitcommit: 97f150f8ba8be8746aa32ebc9b909bb47e22121c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84879731"
---
# <a name="manage-device-security-with-endpoint-security-policies-in-microsoft-intune"></a>使用 Microsoft Intune 中的终结点安全策略管理设备安全

作为安全管理员，使用 Intune 终结点安全中的安全策略来配置设备安全，而不必在设备配置配置文件和安全基线中浏览内容更多的正文和更大范围的设置。

每个策略类型支持一个或多个配置文件。 配置文件用于配置设置，你可以在其中为不同的平台或更大策略区域中的不同重点区域进行分组设置。

可在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)“终结点安全”节点中的“管理”下查找这些策略。

![管理策略](./media/endpoint-security-policy/endpoint-security-policies.png)

以下是每个终结点安全策略类型的简要说明。 要了解有关它们的更多信息，包括每个策略类型的可用策略，请单击指向每种策略类型专用内容的链接：

- [防病毒](../protect/endpoint-security-antivirus-policy.md) - 防病毒策略可帮助安全管理员专注于受管理设备的独立防病毒设置组。 若要使用防病毒策略，请将 Intune 与 Microsoft Defender 高级威胁防护 (Microsoft Defender ATP) 集成为移动威胁防御解决方案。

- [磁盘加密](../protect/endpoint-security-disk-encryption-policy.md) - 终结点安全磁盘加密配置文件只关注与设备内置加密方法（如 FileVault 或 BitLocker）相关的设置。 此举可使安全管理员轻松管理磁盘加密设置，而不必浏览大量不相关的设置。

- [防火墙](../protect/endpoint-security-firewall-policy.md) - 使用 Intune 中的终结点安全防火墙策略为运行 macOS 和 Windows 10 的设备配置设备内置防火墙。 

- [终结点检测和响应](../protect/endpoint-security-edr-policy.md) - 将 Microsoft Defender ATP 与 Intune 集成时，请使用油管终结点检测和响应 (EDR) 的终结点安全策略来管理 EDR 设置并将设备加入 Microsoft Defender ATP。

- [攻击面减少](../protect/endpoint-security-asr-policy.md) - 在 Windows 10 设备上使用 Defender 防病毒时，可以使用 Intune 终结点安全策略来减少攻击面，以管理设备的这些设置。

- [帐户保护](../protect/endpoint-security-account-protection-policy.md) - 帐户保护策略可帮助你保护用户的身份和帐户。 帐户保护策略侧重于 Windows Hello 和 Credential Guard 的设置，这是 Windows 身份和访问管理的一部分。

以下部分适用于所有终结点安全策略。

## <a name="create-an-endpoint-security-policy"></a>创建终结点安全策略

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 选择“终结点安全”，然后选择要配置的策略类型，然后选择“创建策略” 。 从以下策略类型中进行选择：
   - 防病毒
   - 磁盘加密
   - 防火墙
   - 终结点检测和响应
   - 攻击面减少
   - 帐户保护

3. 输入以下属性：
   - **平台**：选择要为之创建策略的平台。 可用的选项取决于你选择的策略类型：
     - macOS
     - Windows 10 及更高版本
   - **配置文件**：从所选平台的可用配置文件中进行选择。 有关配置文件的信息，请参阅本文中有关所选策略类型的专用部分。

4. 选择“创建”。

5. 在“基本信息”页上，输入配置文件的名称和说明，然后选择“下一步” 。

6. 在“配置设置”页面上，展开每个设置组，然后配置要使用此配置文件管理的设置。

   完成配置设置后，选择“下一步”。

7. 在“作用域标记”页上，选择“选择作用域标记”以打开“选择标记”窗格，将作用域标记分配给配置文件 。
  
   选择“下一步”继续操作。

8. 在“分配”页上，选择将接收此配置文件的组。 有关分配配置文件的详细信息，请参阅[分配用户和设备配置文件](../configuration/device-profile-assign.md)。

   选择“下一步”。

9. 完成后，在“查看 + 创建”页上，选择“创建” 。 为创建的配置文件选择策略类型时，新配置文件将显示在列表中。

## <a name="duplicate-a-policy"></a>复制策略

终结点安全策略支持复制以创建原始策略的副本。 如果需要将类似的策略分配给不同的组，但不希望手动重新创建整个策略，那么复制策略将很有用。 在这种情况下，只需复制原始策略，然后仅引入新策略所需的更改。 你只能更改特定设置以及分配了策略的组。

创建副本时，将为副本命名。 复制的副本具有与原基线相同的配置和作用域标记，但不具有任何分配。 稍后需要编辑新策略才能创建分配。  

以下策略类型支持复制：

- 防病毒
- 磁盘加密
- 防火墙
- 终结点检测和响应
- 攻击面减少
- 帐户保护

创建新策略后，查看并编辑该策略以更改其配置。

### <a name="to-duplicate-a-policy"></a>复制策略

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择要复制的策略。 接下来，选择“复制”，或选择策略右侧的省略号（“…”），然后选择“复制”  。
3. 为策略提供“新名称”，然后选择“保存” 。

### <a name="to-edit-a-policy"></a>编辑策略

1. 选择新策略，然后选择“属性”。
2. 选择“设置”，展开策略中的配置设置列表。 在此视图中，将无法修改设置，但可以查看它们的配置方式。
3. 要修改策略，请为要更改的每个类别选择“编辑”：
   - 基本
   - 分配
   - 作用域标记
   - 配置设置
4. 更改后，选择“保存”，保存编辑。  必须先保存对一个类别的编辑，然后才能将编辑引入其他类别。

## <a name="manage-conflicts"></a>管理冲突

通过终结点安全策略（以下简称安全策略）管理的许多设备设置都可以通过 Intune 中的其他策略类型管理。 这些其他策略类型包括设备配置策略和安全基线 。 由于可以使用多个不同的策略类型或同一策略类型的多个实例来管理设置，因此如果设备不符合你所期望的配置，请做好识别和解决策略冲突的准备。

- 安全基线可为设备设置生成一个非默认值，以符合基线要求的建议配置。
- 其他策略类型（包括终结点安全策略）将默认值设置为“未配置”。 这些其他策略类型要求你在策略中显式配置设置。

无论使用何种策略方法，通过多个策略类型或通过同一策略类型的多个实例在同一设备上管理同一设置都可能导致冲突，而这些冲突应该避免。

以下链接中的信息可帮助你识别和解决冲突：

- [在 Intune 中对策略和配置文件进行故障排除](../configuration/troubleshoot-policies-in-microsoft-intune.md)
- [监视安全基线](../protect/security-baselines-monitor.md#troubleshoot-using-per-setting-status)

## <a name="next-steps"></a>后续步骤

[在 Intune 中管理终结点安全性](../protect/endpoint-security.md)
