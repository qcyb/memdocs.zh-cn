---
title: Microsoft Intune 中的 Surface Hub Windows 10 协同版设备限制 - Azure | Microsoft Docs
titleSuffix: ''
description: 使用 Intune 添加或配置运行 Windows 10 协同版的 Surface Hub 设备设置。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/14/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b57bc0b7c76a6b67a26c7b1fdacb7880173a055c
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429694"
---
# <a name="windows-10-team-settings-to-allow-or-restrict-features-on-surface-hub-devices-using-intune"></a>便于使用 Intune 允许或限制 Surface Hub 设备上的功能的 Windows 10 协同版设置

本文介绍可为运行 Windows 10 协同版的设备（包括 Surface Hub 设备）配置的 Microsoft Intune 设备限制设置。

## <a name="before-you-begin"></a>在开始之前

[创建设备配置文件](device-restrictions-configure.md#create-the-profile)。

## <a name="apps-and-experience"></a>应用和体验

这些设置使用 [SurfaceHub CSP](https://docs.microsoft.com/windows/client-management/mdm/surfacehub-csp)。

- **有人在房间内时唤醒屏幕**：“阻止”将阻止设备在其传感器检测到房间内有人时自动唤醒屏幕。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。
- **显示在“欢迎”屏幕上的会议信息**：选择“欢迎”屏幕的“会议”磁贴上显示的信息。 选项包括：
  - **未配置**（默认）：Intune 不会更改或更新此设置。
  - **仅显示组织者和时间**
  - **组织者、时间和主题(私人会议隐藏主题)**
- **欢迎屏幕背景图像 URL**：输入 .png 图像的 URL，该图像将作为 Windows 10 协同版设备上“欢迎”屏幕上的自定义背景。 图片必须为 PNG 格式，并且 URL 必须以 `https://` 开头。
- ：“阻止”将阻止 Connect 应用在投影启动时自动打开。 如果已阻止，用户可从 Hub 的设置中手动启动 Connect 应用。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。
- **签到建议**：“阻止”禁用将计划会议中的受邀者自动填充到签到对话框的功能。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。
- **我的会议和文件**：“阻止”将禁用“开始”菜单中的“我的会议和文件”功能 。 此功能显示 Office 365 中已登录用户的会议和文件。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。

## <a name="azure-operational-insights"></a>Azure Operational Insights

- **Azure 操作见解**：“启用”使用 Azure 操作见解来收集、存储和分析 Windows 10 Team 设备中的日志数据。 Azure 操作见解是 Microsoft Operations Manager 套件的一部分。 输入“工作区 ID”和“工作区密钥”以连接到 Azure 操作见解 。

  设置为“未配置”（默认）时，Intune 不会更改或更新此设置。 默认情况下，OS 可能不收集此数据。

## <a name="maintenance"></a>维护

这些设置使用 [SurfaceHub CSP](https://docs.microsoft.com/windows/client-management/mdm/surfacehub-csp)。

- **更新的维护时段**：“启用”将在可安装更新时创建维护时段。 输入维护时段的“开始时间”和“持续小时数”（1-5 小时） 。

  设置为“未配置”（默认）时，Intune 不会更改或更新此设置。

## <a name="session"></a>会话

这些设置使用 [SurfaceHub CSP](https://docs.microsoft.com/windows/client-management/mdm/surfacehub-csp)。

- **音量**：输入新会话的默认音量值 (0-100)。 如果留空，Intune 将不会更改或更新此设置。 默认情况下，OS 可能会将音量设置为 45。
- **屏幕超时**：输入 Hub 屏幕关闭前的分钟数。
- **会话超时**：输入会话超时前的分钟数。
- **睡眠超时**：输入 Hub 进入睡眠模式前的分钟数。
- **会话继续**：“阻止”将阻止用户在会话超时后恢复会话。设置为“未配置”（默认）时，Intune 不会更改或更新此设置。

## <a name="wireless-projection"></a>无线投影

这些设置使用 [SurfaceHub CSP](https://docs.microsoft.com/windows/client-management/mdm/surfacehub-csp)。

- **用于无线投影的 PIN**：“必填”强制用户输入 PIN，然后才能在设备上使用无线投影功能。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。
- **Miracast 无线投影**：“阻止”将阻止使用启用了 Miracast 的设备进行投影。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。
- **Miracast 无线投影通道**：选择 Miracast 通道以建立连接。

## <a name="next-steps"></a>后续步骤

有关详细信息，请参阅[如何配置设备限制设置](device-restrictions-configure.md)。

[分配配置文件](device-profile-assign.md)并[监视其状态](device-profile-monitor.md)。
