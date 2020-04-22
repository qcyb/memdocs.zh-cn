---
title: 在 Microsoft Intune 中添加对 macOS 的终结点保护 - Azure | Microsoft Docs
description: 在 macOS 设备上，使用网关守卫来确定安装应用的位置，包括 Mac App Store。 此外，还可以使用 Microsoft Intune 启用或配置防火墙，以允许使用特定应用、阻止使用特定应用、使用隐藏模式，甚至阻止特定类型的传入连接。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/24/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5e857cdd7028851f14f607739ba7e37c744fa2f1
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "80359468"
---
# <a name="macos-endpoint-protection-settings-in-intune"></a>Intune 中的 macOS 终结点保护设置  

本文介绍可为运行 macOS 的设备配置的终结点保护设置。 在 Intune 中使用 [Endpoint Protection](endpoint-protection-configure.md) 的 macOS 设备配置文件配置这些设置。  

## <a name="before-you-begin"></a>在开始之前

[创建 macOS Endpoint Protection 配置文件](endpoint-protection-configure.md)。

## <a name="gatekeeper"></a>网关守卫  

- **允许从以下位置下载应用**  
  限制设备可启动的应用，具体取决于应用的下载位置。 其目的是保护设备免受恶意软件侵扰，仅允许使用来自信任来源的应用。  

  - 未配置   
  - **Mac App Store**  
  - **Mac App Store 和已识别的开发人员**  
  - **任何来源**  

  **默认值**：未配置  

- **用户可以替代 Gatekeeper**  
  可以防止用户重写网关守卫设置，并能防止用户通过按住 Control 键并单击安装应用。 启用时，用户可以通过按住 Control 键并单击安装任何应用。  
 
  - **未配置** - 用户可通过按住 Ctrl 并单击来安装应用。  
  - **阻止** - 阻止用户通过按住 Ctrl 并单击来安装应用。  

  **默认值**：未配置  

## <a name="firewall"></a>防火墙  

使用防火墙按每个应用程序（而不是按每个端口）控制连接。 按每个应用程序进行设置能更轻松地享受防火墙保护的优点。 它还有助于防止某些应用意外占用为合理应用打开的网络端口。  

**常规**
- **防火墙**  
  启用防火墙，配置环境对传入连接的处理方式。  
  - 未配置   
  - **启用**  

  **默认值**：未配置  

- **传入连接**  
  阻止所有传入连接，DHCP、Bonjour 和 IPSec 等基本 Internet 服务需要的连接除外。 此功能还会阻止所有共享服务，例如文件共享和屏幕共享。 如果需要使用共享服务，请让此设置保持“未配置”状态  。  
  - 未配置   
  - **阻止**  

  **默认值**：未配置  

**允许或阻止特定应用的传入连接。**  

  - **允许的应用**  
    选择显式允许接收传入连接的应用。  

  - **已阻止的应用**  
    选择应阻止传入连接的应用。  

  - **隐藏模式**  
    若要防止计算机对探测请求做出响应，请启用隐藏模式。 设备会继续回应已授权应用的传入请求。 意外的请求将被忽略，如 ICMP (ping)。  
    - 未配置   
    - **启用**  

    **默认值**：未配置  

## <a name="filevault"></a>FileVault  
有关 Apple FileVault 设置的详细信息，请参阅 Apple 开发人员内容中的 [FDEFileVault](https://developer.apple.com/documentation/devicemanagement/fdefilevault)。 

> [!IMPORTANT]  
> 自 macOS 10.15 起，FileVault 配置要求用户批准的 MDM 注册。 

- **FileVault**  
  可以在运行 macOS 10.13 和更高版本的设备上通过 FileVault 使用 XTS-AES 128 启用全磁盘加密  。  
  - 未配置   
  - **启用**  

  **默认值**：未配置  

  - **恢复密钥类型**  
    为设备创建个人恢复密钥  。 为个人密钥配置以下设置。  

    - **个人恢复密钥的位置** - 向用户指定一条简短消息，说明他们如何以及在何处检索个人恢复密钥。 如果忘记了密码，则在系统提示你输入个人恢复密钥时，请将此文本插入用户在其登录屏幕上看到的消息。  

    - **个人恢复密钥轮替** - 指定设备的个人恢复密钥轮替的频率。 可以选择默认的“未配置”，或选择 1 到 12 个月其中一个值    。  

  - **禁止在注销时提示**  
    禁止在用户注销时提示他们启用 FileVault。如果设置为“禁用”，则会禁止在用户注销时提示，而在用户登录时提示。  
    - 未配置   
    - **禁用** - 禁止在注销时提示。

    **默认值**：未配置  

  - **允许的免验证次数**  
  设置在系统要求用户提供 FileVault 才能登录之前用户可忽略“启用 FileVault”提示的次数。 

    - **未配置** - 需要在设备上进行加密，才能允许下次登录。  
    - 1 到 10 - 允许用户在要求对设备进行加密之前忽略 1 到 10 次的提示   。  
    - **无限制，始终提示** - 系统会提示用户启用 FileVault，但绝不要求加密。  
 
    **默认值**：变化不定 - 将“禁止在注销时提示”设置为“未配置”时，此设置默认为“未配置”     。 如果将“禁止在注销时提示”设置为“禁用”，则此设置默认为“1”，而不可选择“未配置”值     。

有关 Intune 的 FileVault 的详细信息，请参阅 [FileVault 恢复密钥](encryption-monitor.md#filevault-recovery-keys)。

## <a name="next-steps"></a>后续步骤

[分配配置文件](../configuration/device-profile-assign.md)并[监视其状态](../configuration/device-profile-monitor.md)。

还可以在 [Windows 10 和更高版本设备](endpoint-protection-windows-10.md)上配置 Endpoint Protection。
