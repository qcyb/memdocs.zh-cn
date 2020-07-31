---
title: 在 Microsoft Intune 中为 macOS 设备配置有线网络设置 - Azure | Microsoft Docs
titleSuffix: ''
description: 为 macOS 设备创建或添加有线网络设备配置文件。 查看不同的设置，添加证书，选择 EAP 类型以及在 Microsoft Intune 中选择身份验证方法。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 07/28/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1da738611dd5fe114054645170d2b49ef12f0523
ms.sourcegitcommit: e8076576f5c0ea7e72358d233782f8c38c184c8f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "87334600"
---
# <a name="add-wired-network-settings-for-macos-devices-in-microsoft-intune"></a>添加 Microsoft Intune 中适用于 macOS 设备的有线网络设置

可以使用特定的有线网络设置创建配置文件，然后将此配置文件部署到 macOS 设备。 Microsoft Intune 提供多种功能，包括对网络进行身份验证、添加 SCEP 证书等。

本文介绍可以配置的设置。

## <a name="before-you-begin"></a>在开始之前

[创建有线网络设备配置文件](wired-networks-configure.md)。

> [!NOTE]
> 这些设置适用于所有注册类型。 有关注册类型的详细信息，请参阅 [macOS 注册](../enrollment/macos-enroll.md)。

## <a name="wired-network"></a>有线网络

- **网络接口**：根据服务顺序优先级，选择配置文件应用到的设备上的网络接口。 选项包括：
  
  - **第一个活动以太网**（默认）
  - **第二个活动以太网**
  - **第三个活动以太网**
  - **第一个以太网**
  - **第二个以太网**
  - **第三个以太网**
  - **任何以太网**

  标题中具有“活动”的选项使用在设备上积极工作的接口。 如果没有活动接口，则配置服务顺序优先级中的下一个接口。 默认情况下，会选择“第一个活动以太网”，这也是 macOS 配置的默认设置。

- **EAP 类型**：选择用于对安全有线连接进行身份验证的可扩展身份验证协议 (EAP) 类型。 选项包括：

  - **EAP-FAST**：输入“受保护的访问凭据(PAC)设置”。 此选项使用受保护的访问凭据来创建客户端和身份验证服务器之间经过身份验证的隧道。 选项包括：
    - 不使用 (PAC)
    - **使用 (PAC)** ：如果存在现有 PAC 文件，则使用它。
    - **使用和预配 PAC**：创建 PAC 文件并将其添加到设备中。
    - **匿名使用和预配 PAC**：创建 PAC 文件并将其添加到设备中，无需对服务器进行身份验证。

  - **EAP-TLS**：此外请输入：

    - 服务器信任 - 证书服务器名称： “添加”由受信任的证书颁发机构 (CA) 颁发的证书中使用的一个或多个常用名称。 输入此信息时，则可在用户设备连接到此网络时，绕过该设备上显示的动态信任窗口。
    - **用于服务器验证的根证书**：选择现有受信任的根证书配置文件。 客户端连接到网络时向服务器显示此证书。 它用于对连接进行身份验证。
    - “客户端身份验证” - “证书” ：选择也部署到设备的 SCEP 客户端证书配置文件。 此证书是由设备呈现给服务器以用于对连接进行身份验证的标识。 不支持 PKCS 证书。
    - 标识隐私（外部标识）  ：输入为响应 EAP 标识请求而发送的文本。 此文本可以是任何值，例如 `anonymous`。 在身份验证过程中，将首先发送此匿名标识，然后在安全隧道内发送真实标识。

  - **EAP-TTLS**：此外请输入：

    - 服务器信任 - 证书服务器名称： “添加”由受信任的证书颁发机构 (CA) 颁发的证书中使用的一个或多个常用名称。 输入此信息时，则可在用户设备连接到此网络时，绕过该设备上显示的动态信任窗口。
    - **用于服务器验证的根证书**：选择现有受信任的根证书配置文件。 客户端连接到网络时向服务器显示此证书。 它用于对连接进行身份验证。
    - **客户端身份验证**：选择“身份验证方法”。 选项包括：
      - **用户名和密码**：提示用户输入验证连接所需的用户名和密码。 此外请输入：
        - **非 EAP 方法(内部标识)** ：选择连接验证方法。 请确保选择在你的网络上配置同一协议。 选项包括：
          - **未加密的密码 (PAP)**
          - **质询握手身份验证协议 (CHAP)**
          - **Microsoft CHAP (MS-CHAP)**
          - **Microsoft CHAP 版本 2 (MS-CHAP v2)**
      - **证书**：选择也部署到设备的 SCEP 客户端证书配置文件。 此证书是由设备呈现给服务器以用于对连接进行身份验证的标识。 不支持 PKCS 证书。
      - 标识隐私（外部标识）  ：输入为响应 EAP 标识请求而发送的文本。 此文本可以是任何值，例如 `anonymous`。 在身份验证过程中，将首先发送此匿名标识，然后在安全隧道内发送真实标识。

  - **LEAP**

  - **PEAP**：此外请输入：

    - 服务器信任 - 证书服务器名称： “添加”由受信任的证书颁发机构 (CA) 颁发的证书中使用的一个或多个常用名称。 输入此信息时，则可在用户设备连接到此网络时，绕过该设备上显示的动态信任窗口。
    - **用于服务器验证的根证书**：选择现有受信任的根证书配置文件。 客户端连接到网络时向服务器显示此证书。 它用于对连接进行身份验证。
    - **客户端身份验证**：选择“身份验证方法”。 选项包括：
      - **用户名和密码**：提示用户输入验证连接所需的用户名和密码。
      - **证书**：选择也部署到设备的 SCEP 客户端证书配置文件。 此证书是由设备呈现给服务器以用于对连接进行身份验证的标识。 不支持 PKCS 证书。
      - 标识隐私（外部标识）  ：输入为响应 EAP 标识请求而发送的文本。 此文本可以是任何值，例如 `anonymous`。 在身份验证过程中，将首先发送此匿名标识，然后在安全隧道内发送真实标识。

## <a name="next-steps"></a>后续步骤

此时，配置文件创建完成，但它可能未执行任何操作。 请务必[分配此配置文件](device-profile-assign.md)，并[监视配置文件状态](device-profile-monitor.md)。
