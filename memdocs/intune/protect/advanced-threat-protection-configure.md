---
title: 在 Microsoft Intune 中配置 Microsoft Defender ATP - Azure | Microsoft Docs
description: 在 Intune 中配置 Microsoft Defender 高级威胁防护 (Microsoft Defender ATP)，包括连接到 ATP、载入设备、为风险级别分配合规性和条件访问策略。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/12/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: a9c3e456722d0b747a07c3f7040edc2cdf28f264
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88909578"
---
# <a name="configure-microsoft-defender-atp-in-intune"></a>在 Intune 中配置 Microsoft Defender ATP

本文中的信息和过程将帮助你配置 Microsoft Defender ATP 与 Intune 的集成。 配置包括下列常规步骤：

- 为租户启用 Microsoft Defender ATP
- 载入运行 Windows 和 Android 的设备
- 使用合规性策略设置设备风险级别
- 使用条件访问策略来阻止超出预期风险级别的设备

在开始之前，你的环境必须满足[先决条件](../protect/advanced-threat-protection.md#prerequisites)，才能将 Microsoft Defender ATP 与 Intune 配合使用。

## <a name="enable-microsoft-defender-atp-in-intune"></a>在 Intune 中启用 Microsoft Defender ATP

第一步是在 Intune 和 Microsoft Defender ATP 之间设置服务到服务连接。 设置需要对 Microsoft Defender 安全中心和 Intune 的管理访问权限。

只需为每个租户启用一次 Microsoft Defender ATP。

### <a name="to-enable-microsoft-defender-atp"></a>启用 Microsoft Defender ATP

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 选择“终结点安全” > “Microsoft Defender ATP”，然后选择“打开 Microsoft Defender 安全中心”。

   ![选择打开 Microsoft Defender 安全中心](./media/advanced-threat-protection-configure/atp-device-compliance-open-microsoft-defender.png)

3. 在“Microsoft Defender 安全中心”中：
   1. 选择“设置” > “高级功能”。
   2. 对于“Microsoft Intune 连接”，选择“启用”：

      ![启用到 Intune 的连接](./media/advanced-threat-protection-configure/atp-security-center-intune-toggle.png)

   3. 选择“保存首选项”。

4. 返回到 Microsoft Endpoint Manager 管理中心的“Microsoft Defender ATP”。 在“MDM 符合性策略设置”下，根据组织的需求：
   - 将“将 Windows 设备版本 10.0.15063 及更高版本连接到 Microsoft Defender ATP”设置为“启用”
   - 将“将 Android 设备版本 6.0.0 及更高版本连接到 Microsoft Defender ATP”设置为“启用”

5. 选择“保存”。

> [!TIP]
> 如果你将新应用集成到 Intune Mobile Threat Defense，并启用与 Intune 的连接，Intune 会在 Azure Active Directory 中创建经典条件访问策略。 集成的每个 MTD 应用（包括 [Microsoft Defender ATP](advanced-threat-protection.md) 或其他任何 [MTD 合作伙伴](mobile-threat-defense.md#mobile-threat-defense-partners)）都会新建经典条件访问策略。 可以忽略这些策略，但不能对其进行编辑、删除或禁用。
>
> 如果删除了经典策略，你将需要删除负责创建它的 Intune 的连接，然后重新设置。 此过程将重新创建经典策略。 不支持将 MTD 应用的经典策略迁移到新的条件访问策略类型。
>
> MTD 应用的经典条件访问策略：
>
> - 供 Intune MTD 使用，以要求在 Azure AD 中注册设备，这样它们就在与 MTD 合作伙伴通信前有设备 ID 了。 此 ID 是必需的，以便设备可以成功向 Intune 报告其状态。
> - 不会影响其他任何云应用或资源。
> - 此策略与可能创建的用于帮助管理 MTD 的条件访问策略不同。
> - 默认情况下，该策略与用于评估的其他条件访问策略不交互。
>
> 要查看经典条件访问策略，请转到 [Azure](https://portal.azure.com/#home) 中的“Azure Active Directory” > “条件访问” > “经典策略”  。

## <a name="onboard-devices"></a>加入设备

在 Intune 中启用对 Microsoft Defender ATP 的支持后，可以在 Intune 和 Microsoft Defender ATP 之间建立服务到服务连接。 然后，可以将通过 Intune 管理的设备载入 Microsoft Defender ATP，这将启用有关设备风险级别的数据收集。

### <a name="onboard-windows-devices"></a>载入 Windows 设备

在 Intune 和 Microsoft Defender ATP 之间建立连接后，Intune 会接收到来自 Microsoft Defender ATP 的 Microsoft Defender ATP 载入配置包。 使用 Microsoft Defender ATP 的设备配置文件将此配置包部署到 Windows 设备。

配置包将设备配置为与 [Microsoft Defender ATP 服务](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)进行通信以扫描文件和检测威胁。 设备还可配置为根据你创建的合规性策略向 Microsoft Defender ATP 报告设备风险级别。

使用配置包载入设备后，不需要再次执行本操作。 还可以使用[组策略或 Microsoft Endpoint Configuration Manager](/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints) 载入设备。

### <a name="create-the-device-configuration-profile-to-onboard-windows-devices"></a>创建设备配置文件以载入 Windows 设备

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“设备” > “配置文件” > “创建配置文件”。
3. 在“平台”中，选择“Windows 10 及更高版本”
4. 对于“配置文件类型”，请选择“Microsoft Defender ATP (Windows 10 桌面版)”，然后选择“创建”。
5. 在“基本信息”页上，输入配置文件的“名称”和“说明”（可选） ，然后选择“下一步”。
6. 在“配置设置”页面上，配置下列设置：

   - Microsoft Defender ATP 客户端配置包类型：选择“载入”将配置包添加到配置文件。 选择“卸载”，从配置文件中删除配置包。
  
     > [!NOTE]
     > 如果你已正确建立与 Microsoft Defender ATP 的连接，Intune 会自动为你载入配置文件，且“Microsoft Defender ATP 客户端配置包类型”设置将不可用。
  
   - **所有文件的示例共享**：选择“启用”可收集示例，并与 Microsoft Defender ATP 共享示例。 例如，如果看到可疑文件，可以将其提交至 Microsoft Defender ATP 进行深入分析。 选择“未配置”不会向 Microsoft Defender ATP 共享任何示例。
   - **加快遥测报告频率**：对于处于高风险的设备，选择“启用”此设置，可以更频繁地向 Microsoft Defender ATP 服务报告遥测。

     有关这些 Microsoft Defender ATP 设置的详细信息，请参阅[使用 Microsoft Endpoint Configuration Manager 载入 Windows 10 计算机](/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints-sccm)。

7. 选择“下一步”以打开“作用域标记”页。 作用域标记是可选的。 选择“下一步”继续操作。

8. 在“分配”页上，选择将接收此配置文件的组。 有关分配配置文件的详细信息，请参阅[分配用户和设备配置文件](../configuration/device-profile-assign.md)。

   选择“下一步”。

9. 完成后，在“查看 + 创建”页上，选择“创建” 。 为创建的配置文件选择策略类型时，新配置文件将显示在列表中。
 选择“确定”，然后“创建”保存更改，此操作将创建配置文件。

### <a name="onboard-android-devices"></a>载入 Android 设备

在 Intune 和 Microsoft Defender ATP 之间建立服务到服务连接之后，可以将 Android 设备载入到 Microsoft Defender ATP。 载入将设备配置为与 Defender ATP 进行通信，然后收集有关设备风险级别的数据。

与 Windows 设备不同的是，没有运行 Android 的设备的配置包。 有关适用于 Android 的先决条件和载入说明，请参阅 Microsoft Defender ATP 文档中[适用于 Android 的 Microsoft Defender ATP 概述](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-android)。

对于运行 Android 的设备，你还可以使用 Intune 策略修改 Android 上 Microsoft Defender ATP。 有关详细信息，请参阅 [Microsoft Defender ATP Web 保护](../protect/advanced-threat-protection-manage-android.md)。

## <a name="create-and-assign-compliance-policy-to-set-device-risk-level"></a>创建并分配合规性策略以设置设备风险级别

对于 Windows 和 Android 设备，合规性策略确定设备可接受的风险级别。

如果对创建合规性策略不熟悉，请参考在 Microsoft Intune 中创建合规性策略一文中的[创建策略](../protect/create-compliance-policy.md#create-the-policy)过程。 以下信息具体介绍如何将 Microsoft Defender ATP 配置为合规性策略的一部分。

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 选择“设备” > “符合性策略” > “策略” > “创建策略”。

3. 对于“平台”，请使用下拉框选择以下选项之一：
   - **Windows 10 及更高版本**
   - **Android 设备管理员**
   - **Android Enterprise**

   接下来，选择“创建”以打开“创建策略”配置窗口 。

4. 指定“名称”以帮助你稍后识别此策略。 还可以选择指定“说明”。
  
5. 在“合规性设置”选项卡上，展开“Microsoft Defender ATP”组并将选项“要求设备不高于计算机风险评分”设置为首选级别  。

   威胁级别分类[由 Microsoft Defender ATP 确定](/windows/security/threat-protection/microsoft-defender-atp/alerts-queue)。

   - **清除**：此级别是最安全的。 设备不能存在任何威胁，且仍可访问公司资源。 如果发现了任何威胁，设备都会被评估为不符合。 （Microsoft Defender ATP 使用“安全”值。）
   - **低**：如果只有低级别威胁，设备符合策略。 具有中等级别或高级别威胁的设备不符合策略。
   - **中**：如果有低级别或中等级别威胁，设备符合策略。 如果检测到高级别威胁，则设备会被确定为不合规。
   - **高**：此级别最不安全，允许所有威胁级别。 存在高、中等或低级别威胁的设备被视为合规。

6. 完成策略的配置，包括将策略分配给适用的组。


## <a name="create-a-conditional-access-policy"></a>创建条件访问策略

条件访问策略可以使用来自 Microsoft Defender ATP 的数据阻止设备访问超过威胁级别的资源。 可以阻止设备访问公司资源，如 SharePoint 或 Exchange Online。

> [!TIP]
> 条件访问是一项 Azure Active Directory (Azure AD) 技术。 在 Microsoft Endpoint Manager 管理中心中找到的条件访问节点是 Azure AD 中的节点 。

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 选择“终结点安全” > “条件访问” > “新策略”。

3. 输入策略“名称”，然后选择“用户和组”。 使用“包括”或“排除”选项来添加策略的组，然后选择“完成”。

4. 选择“云应用”，然后选择要保护的应用。 例如，选取“选择应用”，然后选择“Office 365 SharePoint Online”和“Office 365 Exchange Online”。

   选择“完成”，保存所做的更改。

5. 选择“条件” > “客户端应用”，将策略应用到应用和浏览器。 例如，选择“是”，然后启用“浏览器”和“移动应用和桌面客户端”。

   选择“完成”，保存所做的更改。

6. 选择“授予”，应用基于设备符合性的条件访问。 例如，选择“授予访问权限” > “要求设备标记为符合策略”。

    选取“选择”，保存所做的更改。

7. 选择“启用策略”，然后选择“创建”以保存更改。

## <a name="next-steps"></a>后续步骤

- [在 Android 上配置 Microsoft Defender ATP 设置](../protect/advanced-threat-protection-manage-android.md)
- [监视风险级别的合规性](../protect/advanced-threat-protection-monitor.md)

有关详细信息，请参阅 Intune 文档：

- [使用带有 ATP 漏洞管理的安全任务来修复设备上的问题](atp-manage-vulnerabilities.md)
- [设备符合性策略入门](device-compliance-get-started.md)

有关详细信息，请参阅 Microsoft Defender ATP 文档：

- [Microsoft Defender ATP 条件访问](/windows/security/threat-protection/microsoft-defender-atp/conditional-access)
- [Microsoft Defender ATP 风险仪表板](/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard)