---
title: Intune 中适用于 Windows 安全体验的 Windows 10 防病毒策略设置 | Microsoft Docs
description: Microsoft Intune 中适用于 Windows 安全应用的终结点安全防病毒策略设置
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 089303b76f674d47767afdff72341d09f7f227d4
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431730"
---
# <a name="settings-for-the-windows-security-experience-profile-in-microsoft-intune"></a>Microsoft Intune 中适用于 Windows 安全体验配置文件的设置

查看可以在 Microsoft Intune 中为 Windows 10 的 Windows 安全体验配置文件配置的防病毒策略设置，这些设置可以作为[终结点安全策略](../protect/endpoint-security-policy.md)的一部分。

**Windows 安全**

- **启用篡改防护以防止禁用 Microsoft Defender**  
  [通过篡改防护防止对安全设置进行更改](https://go.microsoft.com/fwlink/?linkid=2066083)

  - **未配置**（默认）- 当客户端上存在“启用”或“禁用”状态时，部署“未配置”对设置没有影响   。 
  - **启用** - 启用篡改防护限制。 若要更改“已启用”或“已禁用”状态，请部署相反的设置以使其生效。
  - **禁用** - 禁用篡改防护限制。 若要更改“已启用”或“已禁用”状态，请部署相反的设置以使其生效。

- **在 Windows 安全应用中隐藏病毒和威胁防护区域**  
  CSP：[DisableVirusUI](https://go.microsoft.com/fwlink/?linkid=873662)

  - **未配置**（默认）- 设置将还原为客户端默认设置，即允许用户访问和通知。
  - **是** - 对最终用户隐藏 Windows 安全应用中的病毒和威胁防护区域。 将禁止与病毒和威胁防护相关的通知。

  - **隐藏 Windows 安全应用中的勒索软件数据恢复选项**  
    CSP：[](https://go.microsoft.com/fwlink/?linkid=873664)

  - **未配置**（默认）- 设置将还原为客户端默认设置，即允许用户访问和通知。
  - **是** - 对最终用户隐藏 Windows 安全应用中的勒索软件数据恢复区域。 将禁止与勒索软件相关的通知。

- **在 Windows 安全应用中隐藏帐户保护区域**  
  CSP：[DisableAccountProtectionUI](https://go.microsoft.com/fwlink/?linkid=873666)

  - **未配置**（默认）- 设置将还原为客户端默认设置，即允许用户访问和通知。
  - **是** - 对最终用户隐藏 Windows 安全应用中的帐户保护区域。 将禁止与帐户保护相关的通知。

- **隐藏 Windows 安全应用中的防火墙和网络保护区域**  
  CSP：[DisableNetworkUI](https://go.microsoft.com/fwlink/?linkid=873668)

  - **未配置**（默认）- 设置将还原为客户端默认设置，即允许用户访问和通知。
  - **是** - 对最终用户隐藏 Windows 安全应用中的防火墙和网络保护区域。 将禁止与防火墙和网络保护相关的通知。

- **隐藏 Windows 安全应用中的应用和浏览器控制区域**  
  CSP：[DisableAppBrowserUI](https://go.microsoft.com/fwlink/?linkid=873669)

  - **未配置**（默认）- 设置将还原为客户端默认设置，即允许用户访问和通知。
  - **是** - 对最终用户隐藏 Windows 安全中的应用和浏览器控制区域。 将禁止与应用和浏览器控制相关的通知。

- **隐藏 Windows 安全应用中的设备安全区域**  
  CSP：[DisableDeviceSecurityUI](https://go.microsoft.com/fwlink/?linkid=873670)

  - **未配置**（默认）- 设置将还原为客户端默认设置，即允许用户访问和通知。
  - **是** - 对最终用户隐藏 Windows 安全应用中的硬件保护区域。 将禁止与硬件保护相关的通知。
  
- **隐藏 Windows 安全应用中的设备性能和运行状况区域**  
  CSP：[DisableHealthUI](https://go.microsoft.com/fwlink/?linkid=873671)

  - **未配置**（默认）- 设置将还原为客户端默认设置，即允许用户访问和通知。
  - **是** - 对最终用户隐藏 Windows 安全应用中的设备性能和运行状况区域。 将禁止与设备性能和运行状况相关的通知

- **隐藏 Windows 安全应用中的产品系列选项区域**  
  CSP：[DisableFamilyUI](https://go.microsoft.com/fwlink/?linkid=873673)

  - **未配置**（默认）- 设置将还原为客户端默认设置，即允许用户访问和通知。
  - **是** - 对最终用户隐藏 Windows 安全应用中的产品系列选项区域。 此外，将禁止与产品系列选项相关的通知。

- **Windows 安全应用通知**  
  CSP：[](https://go.microsoft.com/fwlink/?linkid=873675)

  使用此设置可针对上述所有功能，阻止向用户发送 Windows 安全通知。 或者，你可以使用上述设置来管理每项功能的 Windows 安全应用通知。

  - **未配置**（默认）- 允许不受其他设置控制的所有 Windows 安全应用通知。
  - **阻止非关键通知** - 阻止扫描完成等通知。
  - **阻止所有通知** - 针对所有 Windows 安全功能阻止关键通知和非关键通知。

- **在通知区域中隐藏 Windows 安全图标**  
  CSP：[HideWindowsSecurityNotificationAreaControl](https://go.microsoft.com/fwlink/?linkid=2114313&clcid=0x409)

  用户需要注销再重新登录或者重启计算机才能使此设置生效。
  - **未配置**（默认）- 设置将还原为客户端默认设置，即显示图标。
  - **是** - 在用户系统栏中隐藏 Windows 安全图标。
  
- **禁用 Windows 安全应用中的“清除 TPM”选项**  
  CSP：[DisableClearTpmButton](https://go.microsoft.com/fwlink/?linkid=2114125&clcid=0x409)

  - **未配置**（默认）- 设置将还原为客户端默认设置，即允许访问按钮。
  - **是** - 禁用对 Windows 安全应用中“清除 TPM”按钮的访问。

- **发现漏洞时提示用户更新 TPM 固件**  
  CSP：[DisableTpmFirmwareUpdateWarning](https://go.microsoft.com/fwlink/?linkid=2114212&clcid=0x409)

  - **未配置**（默认）- 设置将还原为客户端默认设置，即不会提示用户。
  - **是** - 允许 Windows 在其 TPM 固件中发现潜在漏洞时提示最终用户。 然后，建议他们运行固件更新以解决该漏洞。

- **组织的支持联系人信息**  
  CSP：[EnableCustomizedToasts](https://go.microsoft.com/fwlink/?linkid=873676)

  声明希望在 Windows 安全应用和通知中显示 IT 组织信息的位置。
  - **未配置**（默认）
  - **在应用和通知中显示**
  - **仅在应用中显示**
  - **仅在通知中显示**