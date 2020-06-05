---
title: Windows Holographic for Business 设备设置 - Microsoft Intune - Azure | Microsoft Docs
description: 阅读了解在 Microsoft Intune 中配置适用于 Windows Holographic for Business 的设备限制的相关信息并进行配置。 控制取消注册、地理位置、密码、从应用商店安装应用、Microsoft Edge 中的 Cookie 和弹出窗口、Microsoft Defender、搜索、云和存储、蓝牙连接、系统时间，以及使用情况数据。
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
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 301cdd9403b0bb3e2d64c8707782ecbc639dc044
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556041"
---
# <a name="windows-holographic-for-business-device-settings-to-allow-or-restrict-features-using-intune"></a>便于使用 Intune 允许或限制功能的 Windows Holographic for Business 设备设置

本文列出并介绍了可以在 Windows Holographic for Business 设备（如 Microsoft Hololens）上控制的各种设置。 在移动设备管理 (MDM) 解决方案中，使用这些设置可允许或禁用功能、控制安全等。

作为 Intune 管理员，可以创建这些设置，并将它们分配到设备。

## <a name="before-you-begin"></a>在开始之前

[创建 Windows 10 设备限制配置文件](device-restrictions-configure.md#create-the-profile)。

创建 Windows 10 设备限制配置文件时，设置数超过本文中所列的设置数。 Windows Holographic for Business 设备支持本文中的设置。

## <a name="app-store"></a>App Store

- **自动更新来自应用商店的应用**：选择“阻止”可阻止自动安装来自 Microsoft Store 的更新。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。 默认情况下，OS 可能允许自动更新从 Microsoft Store 安装的应用。

  [ApplicationManagement/AllowAppStoreAutoUpdate CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowappstoreautoupdate)

- **受信任的应用安装**：选择是否可以安装非 Microsoft Store 应用，也称为旁加载。 安装旁加载，然后运行或测试未经 Microsoft Store 认证的应用。 例如，仅适用于公司内部的应用。 选项包括：
  - **未配置**（默认）：Intune 不会更改或更新此设置。
  - **阻止**：阻止旁加载。 无法安装非 Microsoft Store 应用程序。
  - **允许**：允许旁加载。 可以安装非 Microsoft Store 应用程序。

  [ApplicationManagement/AllowAllTrustedApps CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowalltrustedapps)

- **开发人员解锁**：允许 Windows 开发人员设置，如允许用户修改已旁加载的应用。 选项包括：
  - **未配置**（默认）：Intune 不会更改或更新此设置。
  - **阻止**：阻止开发人员模式和旁加载应用。
  - **允许**：允许开发人员模式和旁加载应用。

  [ApplicationManagement/AllowDeveloperUnlock CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowdeveloperunlock)

## <a name="cellular-and-connectivity"></a>手机网络和连接性

- **蓝牙**：选择“阻止”可阻止用户启用蓝牙。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。 默认情况下，OS 可能允许在设备上使用蓝牙。

  [Connectivity/AllowBluetooth CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-connectivity#connectivity-allowbluetooth)

- **蓝牙可发现性**：选择“阻止”可阻止其他已启用蓝牙的设备发现此设备。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。 默认情况下，OS 可能允许其他支持蓝牙的设备（如耳机）发现该设备。

  [Bluetooth/AllowDiscoverableMode CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowdiscoverablemode)

- **蓝牙广告**：选择“阻止”可阻止设备发送蓝牙广告。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。 默认情况下，OS 可能允许设备发送蓝牙播发。

  [Bluetooth/AllowAdvertising CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowadvertising)

## <a name="cloud-and-storage"></a>云和存储

- **Microsoft 帐户**：设置为“阻止”可阻止用户将 Microsoft 帐户与设备关联。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。 默认情况下，OS 可能允许添加和使用 Microsoft 帐户。

  [Accounts/AllowMicrosoftAccountConnection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-accounts#accounts-allowmicrosoftaccountconnection)

## <a name="control-panel-and-settings"></a>控制面板和设置

- **系统时间修改**：选择“阻止”可阻止用户更改设备上的日期和时间设置。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。 默认情况下，OS 可能允许用户更改这些设置。

  [Settings/AllowDateTime CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-settings#settings-allowdatetime)

## <a name="general"></a>常规

- **手动取消注册**：选择“阻止”可阻止用户使用设备上的工作区控制面板删除工作区帐户。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。

  [Experience/AllowManualMDMUnenrollment CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowmanualmdmunenrollment)

- **地理位置**：选择“阻止”可阻止用户打开设备上的位置服务。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。

  [Experience/AllowFindMyDevice CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowfindmydevice)

- **Cortana**：选择“阻止”可禁用设备上的 Cortana 语音助手。 Cortana 关闭时，用户仍然可以搜索设备上的条目。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。 默认情况下，OS 可能允许使用 Cortana。

  [Experience/AllowCortana CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowcortana)

## <a name="microsoft-edge-browser"></a>Microsoft Edge 浏览器

- **启动体验** > **允许弹出窗口**：选择“是”（默认）可允许在 Web 浏览器中弹出窗口。 选择“否”可阻止在浏览器中弹出窗口。

  [Browser/AllowPopups CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpopups)

- **收藏夹和搜索** > **显示搜索建议**：选择“是”（默认）可允许搜索引擎在你在地址栏中键入搜索短语时建议站点。 选择“否”则阻止此功能。

  [Browser/AllowSearchSuggestionsinAddressBar CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar)

- **隐私和安全** > **允许密码管理器**：选择“是”（默认）可允许 Microsoft Edge 自动使用密码管理器，其允许用户在设备上保存和管理密码。 选择“否”可阻止 Microsoft Edge 使用密码管理器。

  [Browser/AllowPasswordManager CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)

- **隐私和安全** > **Cookie**：选择在 Web 浏览器中处理 Cookie 的方式。 选项包括：
  - **允许**：Cookie 存储在设备上。
  - **阻止所有 cookie**：Cookie 不会存储在设备上。
  - **仅阻止第三方 cookie**：第三方或合作伙伴 cookie 不会存储在设备上。

  [Browser/AllowCookies CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowcookies)

- **隐私和安全** > **发送 do-not track 标头**：选择“是”可向请求跟踪信息的网站发送 do-not-track 标头（推荐）。 选择“否”（默认）不会发送允许网站跟踪用户的标头。 用户可以配置此设置。

  [Browser/AllowDoNotTrack CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack)

## <a name="microsoft-defender-smartscreen"></a>Microsoft Defender SmartScreen

- **Microsoft Edge SmartScreen**：选择“需要”可打开 Microsoft Defender SmartScreen，并阻止用户将其关闭。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。 默认情况下，操作系统会打开 SmartScreen，并允许用户打开和关闭它。

  [Browser/AllowSmartScreen CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

## <a name="password"></a>Password

- **密码**：设置为“需要”时，强制用户输入密码才能访问设备。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。 默认情况下，OS 可能允许访问设备而无需输入密码。 仅适用于本地帐户。 域帐户密码仍由 Active Directory (AD) 和 Azure AD 配置。

  [DeviceLock/DevicePasswordEnabled CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordenabled)

- **必须提供密码才能让设备从空闲状态恢复**：设置为“需要”时，强制用户输入密码才能在空闲后解锁设备。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。 默认情况下，设备空闲后 OS 可能不要求输入 PIN 或密码。

  [DeviceLock/AllowIdleReturnWithoutPassword CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-allowidlereturnwithoutpassword)

## <a name="reporting-and-telemetry"></a>报告和遥测

- **共享使用情况数据**：选择已提交的诊断数据的级别。 选项包括：

  - **未配置**（默认）：Intune 不会更改或更新此设置。 不强制任何设置。 用户选择提交的级别。 默认情况下，OS 可能不会共享任何数据。
  - **安全性**：为帮助使 Windows 更安全所需要的信息，包括有关“已连接的用户体验和遥测”组件设置、恶意软件删除工具和 Microsoft Defender 的数据
  - **基本**：基本设备信息，包括质量相关数据、应用兼容性、应用使用情况数据和来自安全级别的数据
  - **增强**：其他见解，包括 Windows、Windows Server、System Center 和应用的使用方式、执行方式、高级可靠性数据以及来自基本级别和安全级别的数据
  - **全部**：识别和帮助解决问题所需的所有数据，以及来自安全级别、基本级别和增强级别的数据。

  [System/AllowTelemetry CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-system#system-allowtelemetry)

## <a name="search"></a>搜索

- **搜索位置**：选择“阻止”可阻止 Windows 搜索使用该位置。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。 默认情况下，OS 可能允许使用此功能。

  [Search/AllowSearchToUseLocation CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search#search-allowsearchtouselocation)

## <a name="next-steps"></a>后续步骤

[分配配置文件](device-profile-assign.md)并[监视其状态](device-profile-monitor.md)。
