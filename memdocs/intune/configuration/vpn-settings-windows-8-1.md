---
title: 在 Microsoft Intune 中配置 Windows 8.1 设备上的 VPN 设置 - Azure | Microsoft Docs
description: 使用虚拟专用网络 (VPN) 配置设置添加或创建 VPN 配置文件，包括运行 Windows 8.1 的设备上的连接详细信息和代理设置（其中包括 IP 或 FQDN 地址以及 Microsoft Intune 中的 TCP 端口）。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f0f242f336fadf9dd31641849462a5dd24c09e3f
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556347"
---
# <a name="add-vpn-settings-on-windows-81-devices-in-microsoft-intune"></a>在 Microsoft Intune 中为 Windows 8.1 设备添加 VPN 设置

本文介绍可用于在运行 Windows 8.1 的设备上配置 VPN 连接的 Intune 设置。

下表中并非所有值都可配置，具体取决于所选择的设置。

## <a name="before-you-begin"></a>在开始之前

[创建 Windows 8.1 VPN 设备配置文件](vpn-settings-configure.md)。

## <a name="base-vpn-settings"></a>基础 VPN 设置

- **连接名称**：为此连接输入名称。 用户在他们的设备上浏览可用 VPN 连接的列表时会看到此名称。 例如，输入 `Contoso VPN`。
- **服务器**：添加设备连接到的一个或多个 VPN 服务器。 添加服务器时，输入以下信息：
  - **描述**：为服务器输入一个描述性名称，例如“Contoso VPN 服务器”。
  - **IP 地址或 FQDN**：输入设备连接到的 VPN 服务器的 IP 地址或完全限定的域名 (FQDN)。 例如，输入 `192.168.1.1` 或 `vpn.contoso.com`。
  - **默认服务器**：**True** 将此服务器设置为设备用于建立连接的默认服务器。 只将一台服务器设置为默认服务器。
  - **导入**：浏览到以逗号分隔的文件，该文件包含以下格式的服务器列表：描述、IP 地址或 FQDN、默认服务器。 选择“确定”，将这些服务器导入到“服务器”列表 。
  - **导出**：将服务器列表导出到逗号分隔值 (csv) 文件。

- **连接类型**：选择 VPN 连接类型。 选项包括：
  - **Check Point Capsule VPN**
  - **SonicWall Mobile Connect**
  - **F5 Edge Client**
  - **Pulse Secure**

<!--- **Fingerprint** (Check Point Capsule VPN only): Specify a string (for example, "Contoso Fingerprint Code") that will be used to verify that the VPN server can be trusted. A fingerprint can be sent to the client so it knows to trust any server that presents the same fingerprint when connecting. If the device doesn't already have the fingerprint, it will prompt the user to trust the VPN server that they are connecting to while showing the fingerprint. (The user manually verifies the fingerprint and chooses **trust** to connect.) --->

- **登录组或域**（仅限 SonicWall Mobile Connect）：输入想要连接到的登录组或域的名称。

- **角色**（仅限 Pulse Secure）：输入可访问此连接的用户角色的名称。 用户角色用于定义个人设置和选项，并启用或禁用某些访问功能。

- **领域**（仅限 Pulse Secure）：输入想要使用的身份验证领域的名称。 身份验证领域是“Pulse Secure”连接类型使用的身份验证资源的分组。

- **自定义 XML**：输入配置 VPN 连接的任何自定义 XML 命令。

  **Pulse Secure 示例**：

  ```xml
  <pulse-schema><isSingleSignOnCredential>true</isSingleSignOnCredential></pulse-schema>
  ```

  **CheckPoint Mobile VPN 示例**：

  ```xml
  <CheckPointVPN port="443" name="CheckPointSelfhost" sso="true" debug="3" />
  ```

  **SonicWALL Mobile Connect 示例**：

  ```xml
  <MobileConnect><Compression>false</Compression><debugLogging>True</debugLogging><packetCapture>False</packetCapture></MobileConnect>
  ```

  **F5 Edge Client 示例**：

  ```xml
  <f5-vpn-conf><single-sign-on-credential /></f5-vpn-conf>
  ```

  有关编写自定义 XML 的详细信息，请参阅制造商的 VPN 文档。

- **拆分隧道**：“启用”此设置，让设备根据流量确定使用哪个连接。 例如，旅馆中的用户使用 VPN 连接来访问工作文件，但使用旅馆的标准网络进行常规的 Web 浏览。 如果想要让所有流量在 VPN 连接处于活动状态时使用 VPN 隧道，则设置为“禁用”。

## <a name="proxy-settings"></a>代理设置

- **自动配置脚本**：使用文件配置代理服务器。 输入包含配置文件的“代理服务器 URL”。 例如，输入 `http://proxy.contoso.com`。
- **地址**：输入代理服务器地址，例如 IP 地址或 `vpn.contoso.com`。
- **端口号**：输入代理服务器使用的 TCP 端口号。
- **自动检测代理设置**：如果 VPN 服务器要求使用代理服务器进行连接，请选择是否希望设备自动检测连接设置。 选项包括：
  - **未配置**（默认）：Intune 不会更改或更新此设置。
  - **启用**：自动检测连接设置。
  - **禁用**：不会自动检测连接设置。
- **绕过本地地址的代理**：选择为本地地址使用代理服务器。 选项包括：
  - **未配置**（默认）：Intune 不会更改或更新此设置。
  - **启用**：不为本地地址使用代理服务器。
  - **禁用**：为本地地址使用代理服务器。

## <a name="next-steps"></a>后续步骤

[分配配置文件](device-profile-assign.md)并[监视其状态](device-profile-monitor.md)。

在 [Android](vpn-settings-android.md)、[Android Enterprise](vpn-settings-android-enterprise.md)、[macOS](vpn-settings-macos.md) 和 [Windows 10](vpn-settings-windows-10.md) 设备上配置 VPN 设置。
