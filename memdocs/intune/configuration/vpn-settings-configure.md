---
title: 在 Microsoft Intune 中向设备添加 VPN 设置 - Azure | Microsoft Docs
description: 对于 Android 设备管理员、Android Enterprise、iOS、iPadOS、macOS 和 Windows 设备，请使用内置设置在 Microsoft Intune 中创建虚拟专用网 (VPN) 连接。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/11/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 649b9417f349509e4d1630d0cfecfe8e5b6b1430
ms.sourcegitcommit: 8999e197f10fb72d1b82f30a599d1e588db237b7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88146484"
---
# <a name="create-vpn-profiles-to-connect-to-vpn-servers-in-intune"></a>在 Intune 中创建 VPN 配置文件以连接到 VPN 服务器

虚拟专用网络 (VPN) 可让用户安全远程访问你的组织网络。 设备使用 VPN 连接配置文件来启动与 VPN 服务器的连接。 Microsoft Intune 中的“VPN 配置文件”将 VPN 设置分配到你组织中的用户和设备。 使用这些设置，用户能够轻松安全地连接到你的组织网络。

例如，你希望用连接到组织网络上的文件共享所需的设置来配置所有 iOS/iPadOS 设备。 创建包含这些设置的 VPN 配置文件。 然后，将此配置文件分配到拥有 iOS/iPadOS 设备的所有用户。 用户能在可用网络的列表中看到 VPN 连接，并可以轻松连接。

> [!NOTE]
> iOS/iPadOS 和 macOS 的用户注册仅支持[每应用 VPN](vpn-setting-configure-per-app.md)。

> [!NOTE]
> 可使用 [Intune 自定义配置策略](custom-settings-configure.md)为以下平台创建 VPN 配置文件：
>
> * Android 4 及更高版本
> * 运行 Windows 8.1 和更高版本的已注册设备
> * 运行 Windows 10 桌面版的已注册设备
> * Windows Holographic for Business

## <a name="vpn-connection-types"></a>VPN 连接类型

可以使用以下连接类型创建 VPN 配置文件：

- 自动
  - Windows 10

- Check Point Capsule VPN
  - Android 设备管理员
  - Android 企业工作配置文件
  - Android Enterprise 完全托管和公司拥有的工作配置文件：使用[应用配置策略](../apps/app-configuration-vpn-ae.md)
  - iOS/iPadOS
  - macOS
  - Windows 10
  - Windows 8.1

- Cisco AnyConnect
  - Android 设备管理员
  - Android 企业工作配置文件
  - Android Enterprise 完全托管和公司拥有的工作配置文件
  - iOS/iPadOS
  - macOS

- Cisco (IPSec)
  - iOS/iPadOS

- Citrix SSO
  - Android 设备管理员
  - Android Enterprise 工作配置文件：使用[应用配置策略](../apps/app-configuration-vpn-ae.md)
  - Android Enterprise 完全托管和公司拥有的工作配置文件：使用[应用配置策略](../apps/app-configuration-vpn-ae.md)
  - iOS/iPadOS
  - Windows 10

- 自定义 VPN
  - iOS/iPadOS
  - macOS

  要使用 URI 设置创建自定义 VPN 配置文件，请参阅[创建具有自定义设置的配置文件](custom-settings-configure.md)。

- F5 Access
  - Android 设备管理员
  - Android 企业工作配置文件
  - Android Enterprise 完全托管和公司拥有的工作配置文件
  - iOS/iPadOS
  - macOS
  - Windows 10
  - Windows 8.1

- IKEv2
  - iOS/iPadOS
  - Windows 10

- L2TP
  - Windows 10

- 帕洛阿尔托网络全局保护
  - Android Enterprise 工作配置文件：使用[应用配置策略](../apps/app-configuration-vpn-ae.md)
  - Android Enterprise 完全托管和公司拥有的工作配置文件：使用[应用配置策略](../apps/app-configuration-vpn-ae.md)
  - iOS/iPadOS
  - Windows 10

- PPTP
  - Windows 10

- 脉冲安全
  - Android 设备管理员
  - Android 企业工作配置文件
  - Android Enterprise 完全托管和公司拥有的工作配置文件
  - iOS/iPadOS
  - Windows 10
  - Windows 8.1

- SonicWall Mobile Connect
  - Android 设备管理员
  - Android 企业工作配置文件
  - Android Enterprise 完全托管和公司拥有的工作配置文件
  - iOS/iPadOS
  - macOS
  - Windows 10
  - Windows 8.1

- Zscaler
  - Android Enterprise 工作配置文件：使用[应用配置策略](../apps/app-configuration-vpn-ae.md)
  - Android Enterprise 完全托管和公司拥有的工作配置文件：使用[应用配置策略](../apps/app-configuration-vpn-ae.md)
  - iOS/iPadOS

> [!IMPORTANT]
> 在你能够使用已分配到设备的 VPN 配置文件之前，必须安装适用于该配置文件的 VPN 应用。 若要使用 Intune 分配应用，请参阅[什么是 Microsoft Intune 中的应用管理？](../apps/app-management.md)。  

## <a name="create-the-profile"></a>创建配置文件

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“设备” > “配置文件” > “创建配置文件”。
3. 输入以下属性：

    - **平台**：选择设备平台。 选项包括：
      - **Android 设备管理员**
      - **Android Enterprise** > **公司拥有的完全托管式专用工作配置文件**
      - **Android Enterprise** > **工作配置文件**
      - **iOS/iPadOS**
      - **macOS**
      - **Windows 10 及更高版本**
      - **Windows 8.1 及更高版本**
    - **配置文件**：选择“VPN”。

4. 选择“创建”。
5. 在“基本信息”中，输入以下属性：

    - **名称**：输入配置文件的描述性名称。 为配置文件命名，以便稍后可以轻松地识别它们。 例如，配置文件名称最好是“整个公司的 VPN 配置文件”。
    - **描述**：输入配置文件的说明。 此设置是可选的，但建议进行。

6. 选择“下一步”。
7. 在“配置设置”中，根据所选择的平台，可配置的设置有所不同。 选择平台，进行详细设置：

    - [Android 设备管理员](vpn-settings-android.md)
    - [Android Enterprise](vpn-settings-android-enterprise.md)
    - [iOS/iPadOS](vpn-settings-ios.md)
    - [macOS](vpn-settings-macos.md)
    - [Windows 10](vpn-settings-windows-10.md)（包括 Windows Holographic for Business）
    - [Windows 8.1](vpn-settings-windows-8-1.md)

8. 选择“下一步”。
9. 在“作用域标记”（可选）中，分配一个标记以将配置文件筛选到特定 IT 组（如 `US-NC IT Team` 或 `JohnGlenn_ITDepartment`）。 有关范围标记的详细信息，请参阅[将 RBAC 和范围标记用于分布式 IT](../fundamentals/scope-tags.md)。

    选择“下一步”。

10. 在“分配”中，选择将接收配置文件的用户或组。 有关分配配置文件的详细信息，请参阅[分配用户和设备配置文件](device-profile-assign.md)。

    选择“下一步”。

11. 在“查看并创建”中查看设置。 选择“创建”时，将保存所做的更改并分配配置文件。 该策略也会显示在配置文件列表中。

## <a name="secure-your-vpn-profiles"></a>保护 VPN 配置文件

VPN 配置文件可以使用来自不同制造商的多种不同的连接类型和协议。 这些连接通常通过以下方法进行保护。

### <a name="certificates"></a>证书

在创建 VPN 配置文件时，选择之前已在 Intune 中创建的 SCEP 或 PKCS 证书配置文件。 该配置文件又称为身份证书。 用于对你创建的受信任的身份证书配置文件（或根证书）进行身份验证，以允许用户的设备进行连接。 受信任的证书会分配到对 VPN 连接（通常是 VPN 服务器）进行身份验证的计算机。

如果对 VPN 配置文件使用基于证书的身份验证，请将 VPN 配置文件、证书配置文件和受信任的根配置文件部署到同一组。 此分配可确保每台设备都能识别证书颁发机构的合法性。

有关如何在 Intune 中创建和使用证书配置文件的详细信息，请参阅[如何使用 Microsoft Intune 配置证书](../protect/certificates-configure.md)。

> [!NOTE]
> VPN 身份验证不支持使用“PKCS 导入的证书”配置文件类型添加的证书。 VPN 身份验证支持使用“PKCS 证书”配置文件类型添加的证书。


### <a name="user-name-and-password"></a>用户名和密码

用户通过提供用户名和密码向 VPN 服务器进行身份验证。

## <a name="next-steps"></a>后续步骤

配置文件已创建，但它尚未起到任何作用。 下一步，向某些设备[分配配置文件](device-profile-assign.md)并[监视其状态](device-profile-monitor.md)。

也可以在 [Android 设备管理员/Android Enterprise](android-pulse-secure-per-app-vpn.md) 和 [iOS/iPadOS](vpn-setting-configure-per-app.md) 设备上创建并使用每应用 VPN。
