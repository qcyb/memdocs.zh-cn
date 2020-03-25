---
title: 适用于 Android Enterprise 和展台设备的 Wi-Fi 设置 - Microsoft Intune | Microsoft Docs
description: 为 Android Enterprise 和 Android 展台创建或添加 WiFi 设备配置文件。 请参阅不同的设置，包括添加证书、选择 EAP 类型以及在 Microsoft Intune 中选择身份验证方法。 对于展台设备，还要输入网络的预共享密码。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/19/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: maholdaa
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 38c3c4adb7029303eaad34b1d5a9fdef774c0f00
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/21/2020
ms.locfileid: "80086436"
---
# <a name="add-wi-fi-settings-for-android-enterprise-dedicated-and-fully-managed-devices-in-microsoft-intune"></a>在 Microsoft Intune 中为 Android Enterprise 专用和完全托管设备添加 Wi-Fi 设置

可以使用特定的 Wi-Fi 设置创建配置文件，然后将此配置文件部署到 Android Enterprise 完全托管和专用的设备。 Microsoft Intune 提供多种功能，包括对网络进行身份验证，使用预共享密钥等。

本文将说明这些设置。 [在设备上使用 Wi-Fi](wi-fi-settings-configure.md) 详细介绍了 Microsoft Intune 中的 Wi-Fi 功能。

## <a name="before-you-begin"></a>在开始之前

[创建设备配置文件](wi-fi-settings-configure.md)。

## <a name="device-owner-only"></a>仅设备所有者

如果要部署到 Android Enterprise 专用或完全托管设备，请选择此选项。  Android Enterprise 专用和完全托管设备目前支持 SCEP 证书部署，但不支持 PKCS。

### <a name="basic"></a>基本

- **Wi-Fi 类型**：选择“基本”  。
- **网络名称**：输入此 Wi-Fi 连接的名称。 最终用户在浏览其设备的可用 Wi-FI 连接时将看到此名称。 例如，输入 Contoso WiFi  。
- **SSID**：输入“服务集标识符”，它是设备连接到的无线网络的真实名称  。 但是，用户在选择连接时只会看到你已配置的网络名称  。
- **隐藏的网络**：选择“启用”  可以在设备上的可用网络列表中隐藏此网络。 不广播 SSID。 选择“禁用”  以在设备上的可用网络列表中显示此网络。
- **Wi-Fi 类型**：选择用于对 Wi-Fi 网络进行身份验证的安全协议。 选项包括：

  - **开放(无身份验证)** ：仅在网络未受保护的情况下使用此选项。
  - **WEP 预共享密钥**：在“预共享密钥”  中输入密码。 设置或配置组织的网络后，还要配置密码或网络密钥。 输入此密码或网络密钥作为 PSK 值。
  - **WPA 预共享密钥**：在“预共享密钥”  中输入密码。 设置或配置组织的网络后，还要配置密码或网络密钥。 输入此密码或网络密钥作为 PSK 值。

### <a name="enterprise"></a>企业

- **Wi-Fi 类型**：选择“企业”  。
- **SSID**：输入“服务集标识符”，它是设备连接到的无线网络的真实名称  。 但是，用户在选择连接时只会看到你已配置的网络名称  。
- **隐藏的网络**：选择“启用”  可以在设备上的可用网络列表中隐藏此网络。 不广播 SSID。 选择“禁用”  以在设备上的可用网络列表中显示此网络。
- **EAP 类型**：选择用于验证安全无线连接的可扩展身份验证协议 (EAP) 类型。 选项包括：

  - **EAP-TLS**：此外请输入：

    - **服务器信任** - **用于服务器验证的根证书**：选择现有受信任的根证书配置文件。 当客户端连接到网络时，此证书向服务器显示，并对连接进行身份验证。

    - **客户端身份验证** - **用于客户端身份验证的客户端证书（标识证书）** ：选择同时被部署到设备的 SCEP 客户端证书配置文件。 此证书是由设备呈现给服务器以用于对连接进行身份验证的标识。

    - **标识隐私(外部标识)** ：输入为响应 EAP 标识请求而发送的文本。 此文本可以是任何值，例如 `anonymous`。 在身份验证过程中，将首先发送此匿名标识，然后在安全隧道内发送真实标识。

  - **EAP-TTLS**：此外请输入：

    - **服务器信任** - **用于服务器验证的根证书**：选择现有受信任的根证书配置文件。 当客户端连接到网络时，此证书向服务器显示，并对连接进行身份验证。

    - **客户端身份验证**：选择身份验证方法  。 选项包括：

      - **用户名和密码**：提示用户输入验证连接所需的用户名和密码。 此外请输入：
        - **非 EAP 方法(内部标识)** ：选择连接验证方法。 请确保选择在你的 Wi-Fi 网络上配置同一协议。 选项包括：

          - **未加密的密码 (PAP)**
          - **Microsoft CHAP (MS-CHAP)**
          - **Microsoft CHAP 版本 2 (MS-CHAP v2)**

      - **证书**：选择同时被部署到设备的 SCEP 客户端证书配置文件。 此证书是由设备呈现给服务器以用于对连接进行身份验证的标识。

      - **标识隐私(外部标识)** ：输入为响应 EAP 标识请求而发送的文本。 此文本可以是任何值，例如 `anonymous`。 在身份验证过程中，将首先发送此匿名标识，然后在安全隧道内发送真实标识。

  - **PEAP**：此外请输入：

    - **服务器信任** - **用于服务器验证的根证书**：选择现有受信任的根证书配置文件。 当客户端连接到网络时，此证书向服务器显示，并对连接进行身份验证。

    - **客户端身份验证**：选择身份验证方法  。 选项包括：

      - **用户名和密码**：提示用户输入验证连接所需的用户名和密码。 此外请输入：
        - **非 EAP 身份验证方法(内部标识)** ：选择连接验证方法。 请确保选择在你的 Wi-Fi 网络上配置同一协议。 选项包括：

          - **无**
          - **Microsoft CHAP 版本 2 (MS-CHAP v2)**

      - **证书**：选择同时被部署到设备的 SCEP 客户端证书配置文件。 此证书是由设备呈现给服务器以用于对连接进行身份验证的标识。

      - **标识隐私(外部标识)** ：输入为响应 EAP 标识请求而发送的文本。 此文本可以是任何值，例如 `anonymous`。 在身份验证过程中，将首先发送此匿名标识，然后在安全隧道内发送真实标识。

## <a name="work-profile-only"></a>仅工作配置文件

### <a name="basic"></a>基本

- **Wi-Fi 类型**：选择“基本”  。
- **SSID**：输入“服务集标识符”，它是设备连接到的无线网络的真实名称  。 但是，用户在选择连接时只会看到你已配置的网络名称  。
- **隐藏的网络**：选择“启用”  可以在设备上的可用网络列表中隐藏此网络。 不广播 SSID。 选择“禁用”  以在设备上的可用网络列表中显示此网络。

### <a name="enterprise"></a>企业

- **Wi-Fi 类型**：选择“企业”  。
- **SSID**：输入“服务集标识符”，它是设备连接到的无线网络的真实名称  。 但是，用户在选择连接时只会看到你已配置的网络名称  。
- **隐藏的网络**：选择“启用”  可以在设备上的可用网络列表中隐藏此网络。 不广播 SSID。 选择“禁用”  以在设备上的可用网络列表中显示此网络。
- **EAP 类型**：选择用于验证安全无线连接的可扩展身份验证协议 (EAP) 类型。 选项包括：

  - **EAP-TLS**：此外请输入：

    - **服务器信任** - **用于服务器验证的根证书**：选择现有受信任的根证书配置文件。 当客户端连接到网络时，此证书向服务器显示，并对连接进行身份验证。

    - **客户端身份验证** - **用于客户端身份验证的客户端证书（标识证书）** ：选择也被部署到设备的 SCEP 或 PKCS 客户端证书配置文件。 此证书是由设备呈现给服务器以用于对连接进行身份验证的标识。

    - **标识隐私(外部标识)** ：输入为响应 EAP 标识请求而发送的文本。 此文本可以是任何值，例如 `anonymous`。 在身份验证过程中，将首先发送此匿名标识，然后在安全隧道内发送真实标识。

  - **EAP-TTLS**：此外请输入：

    - **服务器信任** - **用于服务器验证的根证书**：选择现有受信任的根证书配置文件。 当客户端连接到网络时，此证书向服务器显示，并对连接进行身份验证。

    - **客户端身份验证**：选择身份验证方法  。 选项包括：

      - **用户名和密码**：提示用户输入验证连接所需的用户名和密码。 此外请输入：
        - **非 EAP 方法(内部标识)** ：选择连接验证方法。 请确保选择在你的 Wi-Fi 网络上配置同一协议。 选项包括：

          - **未加密的密码 (PAP)**
          - **Microsoft CHAP (MS-CHAP)**
          - **Microsoft CHAP 版本 2 (MS-CHAP v2)**

      - **证书**：选择也被部署到设备的 SCEP 或 PKCS 客户端证书配置文件。 此证书是由设备呈现给服务器以用于对连接进行身份验证的标识。

      - **标识隐私(外部标识)** ：输入为响应 EAP 标识请求而发送的文本。 此文本可以是任何值，例如 `anonymous`。 在身份验证过程中，将首先发送此匿名标识，然后在安全隧道内发送真实标识。

  - **PEAP**：此外请输入：

    - **服务器信任** - **用于服务器验证的根证书**：选择现有受信任的根证书配置文件。 当客户端连接到网络时，此证书向服务器显示，并对连接进行身份验证。

    - **客户端身份验证**：选择身份验证方法  。 选项包括：

      - **用户名和密码**：提示用户输入验证连接所需的用户名和密码。 此外请输入：
        - **非 EAP 身份验证方法(内部标识)** ：选择连接验证方法。 请确保选择在你的 Wi-Fi 网络上配置同一协议。 选项包括：

          - **无**
          - **Microsoft CHAP 版本 2 (MS-CHAP v2)**

      - **证书**：选择也被部署到设备的 SCEP 或 PKCS 客户端证书配置文件。 此证书是由设备呈现给服务器以用于对连接进行身份验证的标识。

      - **标识隐私(外部标识)** ：输入为响应 EAP 标识请求而发送的文本。 此文本可以是任何值，例如 `anonymous`。 在身份验证过程中，将首先发送此匿名标识，然后在安全隧道内发送真实标识。

- **代理设置**：指定你组织使用的代理配置。 选项包括：

  - **无** - 不使用代理服务器。
  - **自动** – 选择此选项以使代理服务器 URL 设置可用，该设置用于指定代理服务器或包含代理服务器列表的代理自动配置 (PAC) 文件  。

- **代理服务器 URL**：将“代理设置”设置为“自动”时，此设置可用   。 指定下列选项之一，以将设备定向到代理服务器：

  - IP 地址。 例如 `10.0.0.11`
  - URL。 例如，`http://proxyserver.contoso.com`。
  - 代理自动配置 (PAC) 文件 URL。 例如： `http://proxy.contoso.com/proxy.pac`。

  有关 PAC 文件的详细信息，请参阅[代理自动配置 (PAC) 文件](https://developer.mozilla.org/docs/Web/HTTP/Proxy_servers_and_tunneling/Proxy_Auto-Configuration_(PAC)_file)（将打开非 Microsoft 网站）。

## <a name="next-steps"></a>后续步骤

配置文件已创建，但未执行任何操作。 下一步是[分配此配置文件](device-profile-assign.md)，并[监视配置文件状态](device-profile-monitor.md)。

此外，还可以为 [Android](wi-fi-settings-android.md)、[iOS/iPadOS](wi-fi-settings-ios.md)、[macOS](wi-fi-settings-macos.md)、[Windows 10](wi-fi-settings-windows.md) 和 [Windows 8.1](wi-fi-settings-import-windows-8-1.md) 设备创建 Wi-Fi 配置文件。
