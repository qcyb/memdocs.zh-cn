---
title: 在 Microsoft Intune 中管理适用于 Android 设备的 Microsoft Defender ATP Web 保护 - Azure | Microsoft Docs
description: 在 Intune 中配置适用于 Android 的 Microsoft Defender 高级威胁防护 (Microsoft Defender ATP) Web 保护。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/23/2020
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
ms.openlocfilehash: 49423d1d1b887aaf3ed3323ff36678bb7319b1ad
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88909459"
---
# <a name="configure-microsoft-defender-atp-on-android-devices-you-manage-with-intune"></a>在通过 Intune 管理的 Android 设备上配置 Microsoft Defender ATP

集成 Microsoft Intune 和 Microsoft Defender 高级威胁防护 (ATP) 时，可以使用设备配置文件来修改 Android 设备上 Microsoft Defender ATP 的某些设置。

在继续之前，必须成功地[在 Intune 中配置 Microsoft Defender ATP](../protect/advanced-threat-protection-configure.md)，并将 Android 设备载入 Microsoft Defender ATP。

## <a name="configure-web-protection-on-devices-that-run-android"></a>在运行 Android 的设备上配置 Web 保护

默认情况下，适用于 Android 的 Microsoft Defender ATP 包含并启用了 Web 保护功能。 [Web 保护](/windows/security/threat-protection/microsoft-defender-atp/web-protection-overview)有助于保护设备免受 Web 威胁，并保护用户免受钓鱼网站攻击。

虽然默认是启用的，但在某些 Android 设备上有正当的理由禁用此保护。 例如，你可以选择仅使用 Microsoft Defender ATP 应用扫描功能，或在 Web 保护扫描到有害 URL 时阻止使用 VPN。

Intune 支持关闭全部或部分 Web 保护功能。 你使用的方法和可禁用的功能取决于 Android 设备向 Intune 注册的方式：

- **Android 设备管理员**：使用配置文件在设备上设置自定义 OMA-URI 设置以禁用整个 Web 保护功能或仅禁用对 VPN 的使用。 有关 Android 设备自定义设置的常规信息，请参阅[自定义设置](../configuration/custom-settings-android.md)。

- **Android Enterprise 工作配置文件**：使用应用配置文件和配置设计器禁用 Web 保护。 此方法和注册类型支持禁用所有 Web 保护功能，但不支持仅禁用对 VPN 的使用。 有关应用配置策略的常规信息，请参阅[使用配置设计器](../apps/app-configuration-policies-use-android.md#use-the-configuration-designer)。

若要在设备上配置 Web 保护，请使用以下过程创建和部署适用的配置。

### <a name="disable-web-protection-for-android-device-administrator"></a>禁用 Android 设备管理员的 Web 保护

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 选择“设备” > “配置文件” > “创建配置文件”。

3. 输入以下设置：

   - **平台**：选择“Android 设备管理员”
   - **配置文件**：选择“自定义”

   选择“创建”。

4. 在“基本信息”上，输入以下详细信息：

   - **名称**：输入配置文件的描述性名称。 为配置文件命名，以便稍后可以轻松地识别它们。 例如，适用于Microsoft Defender ATP Web 保护的 Android 自定义配置文件
   - **描述**：输入配置文件的说明。 此设置是可选的，但建议设置。

5. 在“配置设置”中，选择“添加” 。

   指定要部署的配置的设置：

   - **禁用 Web 保护**：
     - **名称**：输入 OMA-URI 设置的唯一名称，便于轻松查找。 例如，禁用 Microsoft Defender ATP Web 保护
     - **描述**：（可选）输入包含设置概述以及其他所有重要详细信息的说明。
     - **OMA-URI**：输入“./Vendor/MSFT/DefenderATP/AntiPhishing”
     - **数据类型**：使用下拉菜单，然后选择“整数”
     - **值**：输入“0”以禁用 Web 保护，包括基于 VPN 的扫描。
       > [!NOTE]
       > 输入“1”以启用 Web 保护，这是 Web 保护的默认设置。

   - **通过 Web 保护仅禁用对 VPN 的使用：**
     - **名称**：输入 OMA-URI 设置的唯一名称，便于轻松查找。 例如，禁用 Microsoft Defender ATP Web 保护 VPN
     - **描述**：（可选）输入包含设置概述以及其他所有重要详细信息的说明。
     - **OMA-URI**：输入“./Vendor/MSFT/DefenderATP/Vpn”
     - **数据类型**：使用下拉菜单，然后选择“整数”
     - **值**：输入“0”以禁用基于 VPN 的扫描。
       > [!NOTE]
       > 输入“1”以启用 Web 保护，这是 Web 保护的默认设置。

   选择“添加”保存 OMA-URI 设置配置，然后选择“下一步”继续 。

6. 在“分配”中，指定将接收此配置文件的组。 有关分配配置文件的详细信息，请参阅[分配用户和设备配置文件](../configuration/device-profile-assign.md)。

7. 完成后，在“查看 + 创建”上，选择“创建” 。 为创建的配置文件选择策略类型时，新配置文件将显示在列表中。

### <a name="disable-web-protection-for-android-enterprise-work-profile"></a>禁用 Android Enterprise 工作配置文件的 Web 保护

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 选择“应用” > “应用配置策略” > “添加”，然后选择受管理设备  。

3. 在“基本信息”上，输入以下详细信息：

   - **名称**：输入配置文件的描述性名称。 为配置文件命名，以便稍后可以轻松地识别它们。 例如，适用于 Microsoft Defender ATP Web 保护的 Android 应用配置。
   - **描述**：输入配置文件的说明。 此设置是可选的，但建议设置。
   - **平台**：选择“Android Enterprise”
   - **配置文件类型**：选择“仅工作配置文件”
   - **目标应用**：单击“选择应用”。

4. 在“关联应用”上，找到并选择“Defender ATP”，然后选择“确定” > “下一步”   。

5. 在“设置”上，使用“配置设置格式”的下拉列表，选择“使用配置设计器”，然后单击“添加”   。 此时会打开 JSON 编辑器。

6. 找到并选择“Web 保护”，然后选择“确定”，返回到“设置”页面  。

7. 对于“配置值”，输入“0”以禁用 Web 保护 。

   > [!NOTE]
   > 输入“1”以启用 Web 保护，这是 Web 保护的默认设置。

   选择“下一步”继续操作。

8. 在“分配”中，指定将接收此配置文件的组。 有关分配配置文件的详细信息，请参阅[分配用户和设备配置文件](../configuration/device-profile-assign.md)。

9. 完成后，在“查看 + 创建”上，选择“创建” 。 为创建的配置文件选择策略类型时，新配置文件将显示在列表中。

## <a name="next-steps"></a>后续步骤

- [监视风险级别的合规性](../protect/advanced-threat-protection-monitor.md)
- [使用带有 ATP 漏洞管理的安全任务来修复设备上的问题](../protect/atp-manage-vulnerabilities.md)

有关详细信息，请参阅 Microsoft Defender ATP 文档：

- [Microsoft Defender ATP 条件访问](/windows/security/threat-protection/microsoft-defender-atp/conditional-access)
- [Microsoft Defender ATP 风险仪表板](/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard)