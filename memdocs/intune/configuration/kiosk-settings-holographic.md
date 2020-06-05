---
title: Microsoft Intune 中适用于 Windows Holographic for Business 的展台设置 - Azure | Microsoft Docs
description: 使用 Microsoft Intune 将 Windows Holographic for Business 设备配置为单应用和多应用展台、自定义开始菜单、添加应用、显示任务栏，以及配置 Web 浏览器。
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
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3d54e02c7bb88354ec59a9a8ce780ff559377466
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556092"
---
# <a name="windows-holographic-for-business-device-settings-to-run-as-a-kiosk-in-intune"></a>使用 Intune 将 Windows Holographic for Business 设备作为展台运行的设置

在 Windows Holographic for Business 设备上，可将这些设备配置为以单应用展台模式或多应用展台模式运行。 在 Windows Holographic for Business 上不支持某些功能。

本文列出并介绍了可以在 Windows Holographic for Business 设备上控制的各种设置。 作为移动设备管理 (MDM) 解决方案的一部分，请使用这些设置将 Windows Holographic for Business 设备配置为在展台模式下运行。

作为 Intune 管理员，可以创建这些设置，并将它们分配到设备。

若要详细了解 Intune 中的 Windows 展台功能，请参阅[配置展台设置](kiosk-settings.md)。

## <a name="before-you-begin"></a>在开始之前

- [创建 Windows 10 展台设备配置文件](kiosk-settings.md#create-the-profile)。

  创建 Windows 10 展台设备配置文件时，设置数超过本文中所列的设置数。 Windows Holographic for Business 设备支持本文中的设置。

- 此展台配置文件与使用 [Microsoft Edge 展台设置](device-restrictions-windows-holographic.md#microsoft-edge-browser)创建的设备限制配置文件直接相关。 总结：

  1. 创建此展台配置文件以在展台模式下运行设备。
  2. 创建[设备限制配置文件](device-restrictions-windows-holographic.md#microsoft-edge-browser)，并配置可在 Microsoft Edge 中使用的特定功能和设置。

> [!IMPORTANT]
> 请务必将此展台配置文件和 [Microsoft Edge 配置文件](device-restrictions-windows-holographic.md#microsoft-edge-browser)分配给相同设备。

## <a name="single-app-full-screen-kiosk"></a>单个应用、全屏展台

只能在设备上运行一个应用。 用户登录时，将启动一个特定应用。 此模式还会限制用户打开新应用或更改正在运行的应用。

- **用户登录类型**：选择运行应用的帐户类型。 选项包括：

  - **自动登录（Windows 10 版本 1803 及更高版本）** ：在 Windows Holographic for Business 上不支持。
  - **本地用户帐户**：输入本地（对设备而言）用户帐户。 或者，输入与展台应用相关联的 Microsoft 帐户 (MSA)。 输入的帐户会在展台中登录。

    对于公众环境中的展台，应使用具有最低权限的用户类型。

- **应用程序类型**：选择“添加应用商店应用”。

  - **要在展台模式下运行的应用**：从列表中选择应用。

    未列出任何应用？ 使用[客户端应用](../apps/apps-add.md)中的步骤添加一些应用。

## <a name="multi-app-kiosk"></a>多应用展台

在此模式下，可从开始菜单使用应用。 其中仅包含用户可以打开的应用。 如果某应用在另一应用上有依赖项，则这两者都必须包含在“允许的应用”列表中。

- **在 S 模式设备中定位 Windows 10**：选择“否”。 Windows Holographic for Business 上不支持 S 模式。

- **用户登录类型**：添加一个或多个可以使用所添加的应用的用户帐户。 选项包括：

  - **自动登录（Windows 10 版本 1803 及更高版本）** ：在 Windows Holographic for Business 上不支持。
  - **本地用户帐户**：“添加”本地（对设备而言）用户帐户。 输入的帐户会在展台中登录。
  - **Azure AD 用户或组（Windows 10 版本 1803 及更高版本）** ：需要用户凭据才能登录到设备。 选择“添加”以从列表中选择 Azure AD 用户或组。 你可以选择多个用户和组。 选取“选择”，保存所做的更改。
  - **HoloLens 访问者**：访问者帐户是来宾帐户，不需要任何用户凭据或身份验证，如[共享电脑模式概念](https://docs.microsoft.com/windows/configuration/set-up-shared-or-guest-pc#shared-pc-mode-concepts)中所述。

- **浏览器和应用程序**：添加要在展台设备上运行的应用。 请记住，可以添加多个应用。

  - **浏览器**
    - **添加 Microsoft Edge**：Microsoft Edge 会添加到应用网格中，且所有应用程序均可在此展台上运行。 选择 Microsoft Edge 展台模式类型：

      - **正常模式(Microsoft Edge 完整版)** ：使用所有浏览功能运行完整版 Microsoft Edge。 会话期间会保存用户数据和状态。
      - **公共浏览(InPrivate)** ：运行多选项卡版本的 Microsoft Edge InPrivate，为全屏模式下运行的展台提供量身定制的体验。

      要详细了解这些选项，请参阅[部署 Microsoft Edge 展台模式](https://docs.microsoft.com/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-configuration-types)。

      > [!NOTE]
      > 此设置会在设备上启用 Microsoft Edge 浏览器。 要配置 Microsoft Edge 专属设置，请创建设备限制配置文件（“设备” > “配置文件” > “创建配置文件” > “Windows 10”（针对平台），再选择“设备限制” > “Microsoft Edge 浏览器”     ）。 [Microsoft Edge 浏览器](device-restrictions-windows-holographic.md#microsoft-edge-browser)列出并介绍了可用的 Holographic for Business 设置。

    - **添加展台浏览器**：在 Windows Holographic for Business 上不支持。

  - **应用程序**
    - **添加应用商店应用**：将已添加或部署到 Intune 的现有应用选择为[客户端应用](../apps/apps-add.md)，包括 LOB 应用。 如果未列出任何应用，Intune 将支持[添加到 Intune](../apps/store-apps-windows.md) 的多种[应用类型](../apps/apps-add.md)。
    - **添加 Win32 应用**：在 Windows Holographic for Business 上不支持。
    - **按 AUMID 添加**：使用此选项可添加收件箱 Windows 应用，如记事本或计算器。 输入以下属性：

      - **应用程序名称**：必需。 输入应用程序的名称。
      - **应用程序用户模型 ID (AUMID)** ：必需。 输入 Windows 应用的应用程序用户模型 ID (AUMID)。 若要获取此 ID，请参阅[查找已安装应用的应用程序用户模型 ID](https://docs.microsoft.com/windows-hardware/customize/enterprise/find-the-application-user-model-id-of-an-installed-app)。

    - **自动登录**：可选。 添加应用和浏览器后，选择一个应用或浏览器，以便在用户登录时自动打开。 只会自动启动一个应用或浏览器。
    - **磁贴大小**：必需。 添加应用后，选择“小”、“中”、“宽”或“大”应用磁贴尺寸。

- **使用可选“开始”屏幕布局**：选择“是”，输入一个 XML 文件，用于描述应用在“开始”菜单上的显示方式，包括应用的顺序。 如果在开始菜单中需要更多自定义，请使用此选项。 [自定义和导出开始布局](https://docs.microsoft.com/hololens/hololens-kiosk#start-layout-for-hololens)提供了一些指导，并包含适用于 Windows Holographic for Business 设备的特定 XML 文件。

- **Windows 任务栏**：在 Windows Holographic for Business 上不支持。
- **允许访问 Downloads 文件夹**：在 Windows Holographic for Business 上不支持。
- **针对应用重启指定维护时段**：在 Windows Holographic for Business 上不支持。

## <a name="next-steps"></a>后续步骤

[分配配置文件](device-profile-assign.md)并[监视其状态](device-profile-monitor.md)。

还可以为 [Android](device-restrictions-android.md#kiosk)、[Android Enterprise](device-restrictions-android-for-work.md#dedicated-devices) 和 [Windows 10 及更高版本](kiosk-settings-windows.md)设备创建展台配置文件。
