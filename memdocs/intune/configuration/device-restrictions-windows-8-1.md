---
title: Microsoft Intune 中的 Windows 8.1 设备限制设置 - Azure | Microsoft Docs
titleSuffix: ''
description: 了解可用于控制运行 Windows 8.1 的设备中设备设置和功能的 Intune 设置。
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
ms.openlocfilehash: 36a74e503f15fe982eeaf1addfed40d0c599cb2c
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556228"
---
# <a name="microsoft-intune-windows-81-device-restriction-settings"></a>Microsoft Intune Windows 8.1 设备限制设置

本文介绍可为运行 Windows 8.1 的设备配置的 Microsoft Intune 设备限制设置。

## <a name="before-you-begin"></a>在开始之前

[创建 Windows 8.1 设备限制配置文件](device-restrictions-configure.md#create-the-profile)。

## <a name="general"></a>常规

- **共享使用情况数据**：设置为“阻止”将阻止设备向 Microsoft 提交诊断和使用情况遥测信息。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。
- **防火墙**：设置为“需要”将要求 Windows 防火墙处于打开状态。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。
- **用户帐户控制**：配置用户帐户控制 (UAC)。 选择如何就设备上的更改通知用户。 选项包括：
  - **未配置**（默认）：Intune 不会更改或更新此设置。
  - **始终通知**
  - **通知应用更改**
  - **通知应用更改，但不使桌面变暗**
  - **从不通知**

## <a name="password"></a>Password

- **所需的密码类型**：选择用户是否必须输入密码才能访问设备。 选项包括：
  - **未配置**（默认）：Intune 不会更改或更新此设置。
  - **字母数字**：密码必须是数字和字母的混合。
  - **数字**：密码必须仅为数字。
- **最短密码长度**：输入所需的最小字符数，范围为 6-16 个。 例如，输入 `6` 可要求密码长度至少为六个数字或字符。
- **擦除设备前的登录失败次数**：输入设备擦除前允许的错误密码数，范围为 1-14 个。
- **屏幕锁定前的最长非活动分钟数(分钟)** ：输入设备在屏幕自动锁定前必须处于空闲状态的时间长度，范围为 1-60 分钟。 例如，输入 `5 Minutes` 可在空闲 5 分钟后锁定设备。 设置为“未配置”时，Intune 不会更改或更新此设置。
- **密码过期(天)** ：输入在用户必须更改设备密码之前密码保持有效的天数（介于 1-255 天之间）。 例如，要使密码在 90 天后过期，请输入 `90`。 如果该值为空，Intune 不会更改或更新此设置。
- **防止重用以前的密码**：输入以前用过的不能重用的密码数，从 1 到 24。 例如，输入 `5` 意味着用户不能将其新密码设置为当前密码或以前四个密码中的任何一个。 如果该值为空，Intune 不会更改或更新此设置。
- **图片密码和 PIN**：图片密码允许用户使用图片上的手势登录。 PIN 允许用户使用 4 位代码快速登录。

  设置为“阻止”将阻止使用图片或 PIN 作为密码。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。

- **加密**：设置为“需要”将需要对设备进行加密，包括文件。 并非所有设备都支持加密。 设置为“未配置”时，Intune 不会更改或更新此设置。

  若要配置此设置并正确报告合规性，还需要配置：

  - **所需的密码类型**：设置为“至少包含数字”。
  - **最短密码长度**：设置为至少包含 `6`。

  若要在运行 Windows 8.1 的设备上强制加密，必须在每台设备上安装 [用于 Windows 的 December 2014 MDM 客户端更新](https://support.microsoft.com/kb/3013816) 。

  如果对 Windows 8.1 设备启用此设置，则该设备的所有用户必须都具有 Microsoft 帐户。

  为了使加密有效，设备必须满足 Microsoft [InstantGo](https://blogs.windows.com/windowsexperience/2014/06/19/instantgo-a-better-way-to-sleep/#IBHULcTfI4PokO8X.97) 硬件认证要求。

  在设备上强制加密时，恢复密钥仅可从用户的 Microsoft 帐户（从用户的 OneDrive 帐户访问）进行访问。 无法为用户恢复此密钥。

## <a name="browser"></a>浏览器

- **自动填充**：设置为“阻止”将阻止用户更改浏览器中的自动完成设置，以及阻止自动填充表单字段。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。 默认情况下，OS 可能允许自动填充。
- **欺诈警告**：设置为“需要”将在浏览器中显示潜在欺诈网站的欺诈警告。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。
- **Microsoft Edge SmartScreen**：设置为“阻止”将关闭 Microsoft Defender SmartScreen。 SmartScreen 在访问站点和文件下载时查找潜在的仿冒骗局和恶意软件。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。 默认情况下，OS 可能会打开 SmartScreen。
- **允许 JavaScript**：设置为“阻止”将阻止脚本（如 JavaScript）在浏览器中运行。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。 默认情况下，OS 可能允许 JavaScript。
- **弹出窗口**：设置为“阻止”将打开弹出窗口阻止程序，以阻止 Web 浏览器中的弹出窗口。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。
- **do-not-track 标头**：设置为“阻止”将阻止设备将 do-not-track 标头发送到请求跟踪信息的网站。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。
- **插件**：设置为“阻止”将阻止用户在 Internet Explorer 中添加插件。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。
- **在 Intranet 站点上使用单字条目**：单字输入允许用户通过输入单个字（如 `hr` 或 `benefits`）进入 Intranet 站点。 “阻止”则阻止此功能。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。
- **自动检测 Intranet 站点**：设置为“阻止”将阻止浏览器自动检测 Intranet 站点。 将阻止 Intranet 映射规则。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。
- **Internet 安全级别**：设置 Internet 站点的安全级别。 选项包括：
  - **未配置**（默认）：Intune 不会更改或更新此设置。
  - **高**
  - **中-高**
  - **中等**
- **Intranet 安全级别**：设置 Intranet 站点的安全级别。 选项包括：
  - **未配置**（默认）：Intune 不会更改或更新此设置。
  - **低**
  - **中-低**
  - **中等**
  - **中-高**
  - **高**
- **受信任的站点安全级别**：配置受信任的站点区域的安全级别。 选项包括：
  - **未配置**（默认）：Intune 不会更改或更新此设置。
  - **低**
  - **中-低**
  - **中等**
  - **中-高**
  - **高**
- **对受限站点实施高安全性**：配置受限制的站点区域的安全级别。 设置为“已配置”将对受限站点强制实施高安全性。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。
- **企业模式菜单访问**：设置为“阻止”将阻止用户访问 Internet Explorer 中的企业模式菜单选项。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。

  当设置为“未配置”时，还请输入：

  - **记录报告位置 URL**：输入 URL 位置，从中获取显示已启用企业模式访问的网站的报告。

- **企业模式站点列表位置(仅限桌面)** ：输入可以在企业模式下打开的网站列表的位置。

## <a name="cellular"></a>移动电话

- **数据漫游**：设置为“阻止”将阻止在设备使用蜂窝网络时进行数据漫游。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。

## <a name="cloud-and-storage"></a>云和存储

- **工作文件夹 URL**：输入工作文件夹的 URL，以允许文档跨设备同步。 设置为“未配置”（默认）或保留为空时，Intune 不会更改或更新此设置。
- **不使用 Microsoft 帐户时访问 Windows 邮件应用**：设置为“阻止”将阻止在没有 Microsoft 帐户的情况下访问 Windows 邮件应用程序。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。

## <a name="next-steps"></a>后续步骤

在 [Windows 10 和更高版本](device-restrictions-windows-10.md)上创建设备限制配置文件。
