---
title: 使用 Microsoft Intune 在 macOS 设备上配置 Endpoint Protection | Microsoft Docs
description: 使用 Intune 配置 macOS 设备，使其使用内置防火墙以允许或阻止特定应用，或者使其使用隐藏模式，使用 Gatekeeper 确定应用的安装位置，以及使用 FileVault 磁盘加密。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/19/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 506bb4672b84423204df5fce1401748ffbce0484
ms.sourcegitcommit: 3217778ebe7fd0318810696e8931e427a85da897
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2020
ms.locfileid: "85107512"
---
# <a name="macos-endpoint-protection-settings-in-intune"></a>Intune 中的 macOS 终结点保护设置

本文介绍可为运行 macOS 的设备配置的终结点保护设置。 在 Intune 中使用 [Endpoint Protection](endpoint-protection-configure.md) 的 macOS 设备配置文件配置这些设置。

## <a name="before-you-begin"></a>在开始之前

[创建 macOS Endpoint Protection 配置文件](endpoint-protection-configure.md)。

## <a name="firewall"></a>防火墙

使用防火墙按每个应用程序（而不是按每个端口）控制连接。 按每个应用程序进行设置能更轻松地享受防火墙保护的优点。 它还有助于防止某些应用意外占用为合理应用打开的网络端口。

- **启用防火墙**

  在 macOS 上启用防火墙，然后配置在环境中处理传入连接的方式。

  - **未配置**（默认）
  - **是**

- **阻止所有传入连接**

  阻止所有传入连接，DHCP、Bonjour 和 IPSec 等基本 Internet 服务需要的连接除外。 此功能还会阻止所有共享服务，例如文件共享和屏幕共享。 如果需要使用共享服务，请让此设置保持“未配置”状态。

  - **未配置**（默认）
  - **是**

  如果将“阻止所有传入连接”设置为“未配置”，则可以配置可以或不能接收传入连接的应用 。

  **允许的应用**：配置允许接收传入连接的应用列表。

  - **按程序包 ID 添加应用**：输入应用的[程序包 ID](../configuration/bundle-ids-built-in-ios-apps.md)。 可在 Apple 网站上查看[内置的 Apple 应用](https://support.apple.com/HT208094)列表。
  - **添加应用商店应用**：选择以前添加在 Intune 中的存储应用。 有关详细信息，请参阅[将应用添加到 Microsoft Intune](../apps/apps-add.md)。

  **阻止的应用**：配置阻止传入连接的应用列表。

  - **按程序包 ID 添加应用**：输入应用的[程序包 ID](../configuration/bundle-ids-built-in-ios-apps.md)。 可在 Apple 网站上查看[内置的 Apple 应用](https://support.apple.com/HT208094)列表。
  - **添加应用商店应用**：选择以前添加在 Intune 中的存储应用。 有关详细信息，请参阅[将应用添加到 Microsoft Intune](../apps/apps-add.md)。

- **启用隐藏模式**

  若要防止计算机对探测请求做出响应，请启用隐藏模式。 设备会继续回应已授权应用的传入请求。 意外的请求将被忽略，如 ICMP (ping)。

  - **未配置**（默认）
  - **是**

## <a name="gatekeeper"></a>网关守卫

- **允许从以下位置下载应用**

  限制设备可启动的应用，具体取决于应用的下载位置。 其目的是保护设备免受恶意软件侵扰，仅允许使用来自信任来源的应用。

  - **未配置**（默认）
  - **Mac App Store**
  - **Mac App Store 和已识别的开发人员**
  - **任何来源**

- **不允许用户替代 Gatekeeper**

  可以防止用户重写网关守卫设置，并能防止用户通过按住 Control 键并单击安装应用。 启用时，用户可以通过按住 Control 键并单击安装任何应用。

  - **未配置**（默认）- 用户可通过按住 Ctrl 并单击来安装应用。
  - **是** - 阻止用户通过按住 Ctrl 并单击来安装应用。

## <a name="filevault"></a>FileVault

有关 Apple FileVault 设置的详细信息，请参阅 Apple 开发人员内容中的 [FDEFileVault](https://developer.apple.com/documentation/devicemanagement/fdefilevault)。

> [!IMPORTANT]
> 自 macOS 10.15 起，FileVault 配置要求用户批准的 MDM 注册。

- **启用 FileVault**  

  可以在运行 macOS 10.13 和更高版本的设备上通过 FileVault 使用 XTS-AES 128 启用全磁盘加密。

  - **未配置**（默认）
  - **是**

  当“启用 FileVault”设置为“是”时，可配置以下设置 ：

  - **恢复密钥类型**

    为设备创建个人恢复密钥。 为个人密钥配置以下设置。

  - **个人恢复密钥的托管位置说明**

    指定一条发给用户的简短消息，向他们说明如何以及在何处检索个人恢复密钥。 如果忘记了密码，则在系统提示你输入个人恢复密钥时，请将此文本插入用户在其登录屏幕上看到的消息。

  - **个人恢复密钥轮替**

    指定设备的个人恢复密钥的轮替频率。 可以选择默认的“未配置”，或选择 1 到 12 个月其中一个值  。

  - **隐藏恢复密钥**

    选择在 FileVault 2 加密过程中对设备用户隐藏个人密钥。

    - **未配置**（默认）- 在加密过程中，个人密钥对设备用户可见。
    - **是** - 在加密过程中，个人密钥对设备用户是隐藏的。

    加密后，设备用户可以从以下位置查看加密 macOS 设备的个人恢复密钥：
    - iOS/iPadOS 公司门户应用
    - Intune 应用
    - 公司门户网站
    - Android 公司门户应用

    若要查看密钥，请从应用或网站转到已加密 macOS 设备的设备详细信息，然后选择“获取恢复密钥”。

  - **禁止在注销时提示**

    禁止在用户注销时提示他们启用 FileVault。如果设置为“禁用”，则会禁止在用户注销时提示，而在用户登录时提示。

    - **未配置**（默认）
    - **是** - 禁止在注销时提示。

  - **允许的免验证次数**

    设置在系统要求用户提供 FileVault 才能登录之前用户可忽略“启用 FileVault”提示的次数。

    - **未配置** - 需要在设备上进行加密，才能允许下次登录。
    - **0** - 要求设备在用户下次登录到该设备时进行加密。
    - 1 到 10 - 允许用户在要求对设备进行加密之前忽略 1 到 10 次的提示 。
    - **无限制，始终提示** - 系统会提示用户启用 FileVault，但绝不要求加密。

    此设置的默认值取决于“禁止在注销时提示”的配置。如果“禁止在注销时提示”设置为“未配置”，此设置默认为“未配置” 。 如果将“禁止在注销时提示”设置为“是”，则此设置默认为“1”，而不可选择“未配置”值  。

## <a name="next-steps"></a>后续步骤

[分配配置文件](../configuration/device-profile-assign.md)并[监视其状态](../configuration/device-profile-monitor.md)。

还可以在 [Windows 10 和更高版本设备](endpoint-protection-windows-10.md)上配置 Endpoint Protection。
