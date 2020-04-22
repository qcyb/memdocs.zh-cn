---
title: 在 Microsoft Intune 中为 macOS 设备配置 Wi-Fi 设置 - Azure | Microsoft Docs
titleSuffix: ''
description: 为 macOS 设备创建或添加 WiFi 设备配置文件。 请参阅不同的设置，包括添加证书、选择 EAP 类型以及在 Microsoft Intune 中选择身份验证方法。
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
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0e878294a9af6b80358aa495aa4d10ac6ed93404
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "80086348"
---
# <a name="add-wi-fi-settings-for-macos-devices-in-microsoft-intune"></a>添加 Microsoft Intune 中适用于 macOS 设备的 Wi-Fi 设置

可以使用特定的 WiFi 设置创建配置文件，然后将此配置文件部署到 macOS 设备。 Microsoft Intune 提供多种功能，包括对网络进行身份验证，添加 PKS 或 SCEP 证书等。

这些 Wi-Fi 设置分为两类：基本设置和企业级设置。

本文将介绍这些设置。

## <a name="before-you-begin"></a>在开始之前

[创建设备配置文件](wi-fi-settings-configure.md)。

> [!NOTE]
> 这些设置适用于所有注册类型。 有关注册类型的详细信息，请参阅 [macOS 注册](../enrollment/macos-enroll.md)。

## <a name="basic-profiles"></a>基本配置文件

- Wi-Fi 类型  ：选择“基本”  。
- 网络名称  ：输入此 Wi-Fi 连接的名称。 该值是用户在其设备上浏览可用连接列表时看到的名称。
- SSID  ：服务集标识符的英文缩写  。 该属性是设备连接到的无线网络的真实名称。 但是，用户在选择连接时只会看到你之前配置的网络名称。
- 自动连接  ：选择“启用”  将在设备处于范围内时自动连接到此网络。 选择“禁用”  以防止设备自动连接。
- 隐藏网络  ：选择“启用”  以在设备上的可用网络列表中隐藏此网络。 不广播 SSID。 选择“禁用”  以在设备上的可用网络列表中显示此网络。
- 安全类型  ：选择要用于对 Wi-Fi 网络进行身份验证的安全协议。 选项包括：

  - 开放(无身份验证)：仅在网络未受保护的情况下使用此选项  。
  - WPA/WPA2 - 个人  ：在预共享密钥中输入此密码  。 设置或配置组织的网络后，还要配置密码或网络密钥。 输入此密码或网络密钥作为 PSK 值。
  - **WEP**

- 代理设置  ：选项包括：
  - 无：不配置任何代理设置  。
  - 手动  ：输入代理服务器地址  作为 IP 地址及其端口号  。
  - 自动  ：使用文件配置代理服务器。 输入包含配置文件的代理服务器 URL  （例如 `http://proxy.contoso.com`）。

## <a name="enterprise-profiles"></a>企业配置文件

- Wi-Fi 类型  ：选择“企业”  。
- SSID  ：服务集标识符的英文缩写  。 该属性是设备连接到的无线网络的真实名称。 但是，用户在选择连接时只会看到你之前配置的网络名称。
- 自动连接  ：选择“启用”  将在设备处于范围内时自动连接到此网络。 选择“禁用”  以防止设备自动连接。
- 隐藏网络  ：选择“启用”  以在设备上的可用网络列表中隐藏此网络。 不广播 SSID。 选择“禁用”  以在设备上的可用网络列表中显示此网络。

- EAP 类型  ：选择用于对安全无线连接进行身份验证的可扩展身份验证协议 (EAP) 类型。 选项包括：

  - EAP-FAST  ：输入受保护的访问凭据 (PAC) 设置  。 此选项使用受保护的访问凭据来创建客户端和身份验证服务器之间经过身份验证的隧道。 选项包括：
    - 不使用 (PAC) 
    - 使用 (PAC)  ：如果存在现有 PAC 文件，则使用它。
    -  使用和预配 PAC：创建 PAC 文件并将其添加到设备中。
    - 匿名使用和预配 PAC  ：创建 PAC 文件并将其添加到你的设备，无需对服务器进行身份验证。

  - **EAP-SIM**

  - EAP-TLS  ：此外请输入：

    - 服务器信任   - 证书服务器名称  ：添加  由受信任的证书颁发机构 (CA) 颁发的证书中使用的一个或多个常用名称。 输入此信息时，可在用户设备连接到此 Wi-Fi 网络时，绕过该设备上显示的动态信任窗口。
    - 用于服务器验证的根证书  ：选择现有的受信任根证书配置文件。 当客户端连接到网络时，将向服务器显示此证书，并被用于对连接进行身份验证。

    - 客户端身份验证   - 用于客户端身份验证的客户端证书（标识证书）  ：选择同时被部署到设备的 SCEP 或 PKCS 客户端证书配置文件。 此证书是由设备呈现给服务器以用于对连接进行身份验证的标识。

  - EAP-TTLS  ：此外请输入：

    - 服务器信任   - 证书服务器名称  ：添加  由受信任的证书颁发机构 (CA) 颁发的证书中使用的一个或多个常用名称。 输入此信息时，可在用户设备连接到此 Wi-Fi 网络时，绕过该设备上显示的动态信任窗口。
    - 用于服务器验证的根证书  ：选择现有的受信任根证书配置文件。 当客户端连接到网络时，将向服务器显示此证书，并被用于对连接进行身份验证。

    - 客户端身份验证  - 选择一种身份验证方法  。 选项包括：

      - 用户名和密码  ：提示用户输入用户名和密码以对连接进行身份验证。 此外请输入：
        - 非 EAP 方法（内部标识）  ：选择验证连接的方式。 请确保选择在你的 Wi-Fi 网络上配置同一协议。

          选项包括：未加密的密码 (PAP)  、质询握手身份验证协议 (CHAP)  、Microsoft CHAP (MS-CHAP)  或 Microsoft CHAP 版本 2 (MS-CHAP v2) 

      - 证书  ：选择同时被部署到设备的 SCEP 或 PKCS 客户端证书配置文件。 此证书是由设备呈现给服务器以用于对连接进行身份验证的标识。

      - 标识隐私（外部标识）  ：输入为响应 EAP 标识请求而发送的文本。 此文本可以是任何值，例如 `anonymous`。 在身份验证过程中，将首先发送此匿名标识，然后在安全隧道内发送真实标识。

  - **LEAP**

  - PEAP  ：此外请输入：

    - 服务器信任   - 证书服务器名称  ：添加  由受信任的证书颁发机构 (CA) 颁发的证书中使用的一个或多个常用名称。 输入此信息时，可在用户设备连接到此 Wi-Fi 网络时，绕过该设备上显示的动态信任窗口。
    - 用于服务器验证的根证书  ：选择现有的受信任根证书配置文件。 当客户端连接到网络时，将向服务器显示此证书，并被用于对连接进行身份验证。

    - 客户端身份验证  - 选择一种身份验证方法  。 选项包括：

      - 用户名和密码  ：提示用户输入用户名和密码以对连接进行身份验证。 

      - 证书  ：选择同时被部署到设备的 SCEP 或 PKCS 客户端证书配置文件。 此证书是由设备呈现给服务器以用于对连接进行身份验证的标识。

      - 标识隐私（外部标识）  ：输入为响应 EAP 标识请求而发送的文本。 此文本可以是任何值，例如 `anonymous`。 在身份验证过程中，将首先发送此匿名标识，然后在安全隧道内发送真实标识。

- 代理设置  ：选项包括：
  - 无：不配置任何代理设置  。
  - 手动  ：输入代理服务器地址  作为 IP 地址及其端口号  。
  - 自动  ：使用文件配置代理服务器。 输入包含配置文件的代理服务器 URL  （例如 `http://proxy.contoso.com`）。

## <a name="next-steps"></a>后续步骤

配置文件已创建，但未执行任何操作。 下一步是[分配此配置文件](device-profile-assign.md)，并[监视配置文件状态](device-profile-monitor.md)。

在 [Android](wi-fi-settings-android.md)、[Android Enterprise](wi-fi-settings-android-enterprise.md)、[iOS/iPadOS](wi-fi-settings-ios.md) 和 [Windows 10](wi-fi-settings-windows.md) 设备上配置 Wi-Fi 设置。
