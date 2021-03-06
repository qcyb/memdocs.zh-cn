---
title: Microsoft Intune 中适用于 Android 设备管理员的自定义每应用 VPN 配置文件 - Azure | Microsoft Docs
description: 在 Microsoft Intune 中将自定义配置文件用于使用 Pulse Secure 或 Citrix VPN 连接类型的 Android 设备管理员的每应用 VPN 配置文件。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 07/22/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d035ebf5-85f4-4001-a249-75d24325061a
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3c8e09b6010f7fc846fd81281053eaaa722e5ef4
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "87262789"
---
# <a name="use-a-microsoft-intune-custom-profile-to-create-a-per-app-vpn-profile-for-android-devices"></a>使用 Microsoft Intune 自定义配置文件为 Android 设备创建每应用 VPN 配置文件

可为由 Intune 管理的 Android 5.0 及更高版本设备创建每应用 VPN 配置文件。 首先，创建使用 Pulse Secure 或 Citrix 连接类型的 VPN 配置文件。 然后，创建将 VPN 配置文件与特定应用关联的自定义配置策略。

此功能适用于：

- Android 设备管理员

若要在 Android Enterprise 设备上使用每应用 VPN，请使用[应用配置策略](../apps/app-configuration-vpn-ae.md)。 应用配置策略支持更多 VPN 客户端应用。 在 Android Enterprise 设备上，可以使用本文中的步骤。 但我们不建议这样做，并且仅限于 Pulse Secure 和 Citrix VPN 连接。

将策略分配给 Android 设备或用户组后，用户应启动 Pulse Secure 或 Citrix VPN 客户端。 然后，VPN 客户端将仅允许来自指定应用的流量使用打开的 VPN 连接。

> [!NOTE]
>
> Android 设备管理员仅支持 Pulse Secure 和 Citrix 连接类型。 在 Android Enterprise 设备上，使用[应用配置策略](../apps/app-configuration-vpn-ae.md)。

## <a name="step-1-create-a-vpn-profile"></a>步骤 1：创建 VPN 配置文件

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“设备” > “配置文件” > “创建配置文件”。
3. 输入以下属性：

    - **平台**：选择“Android 设备管理员”。
    - **配置文件**：选择“VPN”。

4. 选择“创建”。
5. 在“基本信息”中，输入以下属性：

    - **名称**：输入配置文件的描述性名称。 为配置文件命名，以便稍后可以轻松地识别它们。 例如，配置文件名称最好是“整个公司的 Android 设备管理员每应用 VPN 配置文件”。
    - **描述**：输入配置文件的说明。 此设置是可选的，但建议进行。

6. 选择“下一步”  。
7. 在“配置设置”中，配置想要包含在配置文件中的设置：

    - [适用于 Android 设备管理员设备的 VPN 设置](vpn-settings-android.md)。

    记录创建 VPN 配置文件时输入的“连接名称”值。 在下一步中会用到此名称。 在此示例中，连接名称为 MyAppVpnProfile。

8. 选择“下一步”，然后继续创建配置文件。 有关详细信息，请参阅[创建 VPN 配置文件](vpn-settings-configure.md#create-the-profile)。

## <a name="step-2-create-a-custom-configuration-policy"></a>步骤 2:创建自定义配置策略

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“设备” > “配置文件” > “创建配置文件”。
3. 输入以下属性：

    - **名称**：输入自定义配置文件的描述性名称。 为配置文件命名，以便稍后可以轻松地识别它们。 例如，配置文件名称最好是“整个公司的自定义 OMA-URI Android VPN 配置文件”。
    - **描述**：输入配置文件的说明。 此设置是可选的，但建议进行。
    - **平台**：选择“Android 设备管理员”。
    - **配置文件类型**：选择“自定义”。

4. 选择“设置” > “配置”。
5. 在“自定义 OMA-URI 设置”窗格上，选择“添加”。
    - **名称**：输入设置的名称。
    - **描述**：输入配置文件的说明。 此设置是可选的，但建议进行。
    - **OMA-URI**：输入 `./Vendor/MSFT/VPN/Profile/*Name*/PackageList`，其中“Name”是在步骤 1 中记下的连接名称。 在此示例中，字符串是 `./Vendor/MSFT/VPN/Profile/MyAppVpnProfile/PackageList`。
    - **数据类型**：输入“String”。
    - **值**：输入与配置文件相关联的包列表，其中此列表以分号进行分隔。 例如，如果你希望 Excel 和 Google Chrome 浏览器使用 VPN 连接，输入 `com.microsoft.office.excel;com.android.chrome`。

    :::image type="content" source="./media/android-pulse-secure-per-app-vpn/android_per_app_vpn_oma_uri.png" alt-text="Microsoft Intune 中的 Android 设备管理员每应用 VPN 自定义策略":::

### <a name="set-your-blocked-and-allowed-app-list-optional"></a>设置阻止和允许的应用列表（可选）

使用“BLACKLIST”值，可输入将无法使用 VPN 连接的应用列表。 所有其他应用将通过 VPN 连接。 或者，使用“WHITELIST”值来输入可以使用 VPN 连接的应用列表。 不在列表中的应用不会通过 VPN 连接。

1. 在“自定义 OMA-URI 设置”窗格上，选择“添加”。
2. 输入设置名称。
3. 在“OMA-URI”中，输入 `./Vendor/MSFT/VPN/Profile/*Name*/Mode`，其中“Name”是在步骤 1 中记下的 VPN 配置文件名称。 在此示例中，字符串是 `./Vendor/MSFT/VPN/Profile/MyAppVpnProfile/Mode`
4. 在“数据类型”中，输入“String”。
5. 在**值**中，输入**黑名单**或**白名单**。

## <a name="step-3-assign-both-policies"></a>步骤 3：分配这两个策略

向所需用户或设备[分配两个设备配置文件](device-profile-assign.md)。

## <a name="next-steps"></a>后续步骤

- 有关所有 Android 设备管理员 VPN 设置的列表，请参阅[用于配置 VPN 的 Android 设备设置](vpn-settings-android.md)。
- 要了解 VPN 设置和 Intune 的详细信息，请参阅[在 Microsoft Intune 中配置 VPN 设置](vpn-settings-configure.md)。
