---
title: Windows Autopilot 新增功能
ms.reviewer: ''
manager: laurawi
description: 阅读有关最新更新和过去版本的 Windows Autopilot 的新闻和资源。
keywords: mdm, 设置, windows, windows 10, oobe, 管理, 部署, autopilot, ztd, 零接触, 合作伙伴, msfb, intune
ms.technology: windows
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: 736e01696cf503b63762c32a9acee3cb68c1e241
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/09/2020
ms.locfileid: "89606563"
---
# <a name="windows-autopilot-whats-new"></a>Windows Autopilot：新增功能

**适用于**

- Windows 10

## <a name="windows-autopilot-update-history"></a>Windows Autopilot 更新历史记录

以下 [Windows Autopilot 更新](autopilot-update.md) 可用。 **注意**： Windows Autopilot 部署过程中会自动下载和应用更新。 

尚无可用更新。 日后可回来查看以了解详细信息。

## <a name="new-in-windows-10-version-2004"></a>Windows 10 中的新增版本2004版

在此版本中，你可以配置 Windows Autopilot [用户驱动](user-driven.md) 的混合 AZURE ACTIVE DIRECTORY 结合 VPN 支持。 此支持也向后移植 Windows 10 版本1909和1903。

如果在 Autopilot 配置文件中配置了语言设置并且设备已连接到以太网，则所有方案现在都将跳过语言、区域设置和键盘页。 在以前的版本中，仅支持自部署配置文件。

## <a name="new-in-windows-10-version-1903"></a>Windows 10 中的新增版本1903版

[Windows Autopilot for 白色手套部署](white-glove.md) 是 windows 10 版本1903中的新增项。 请参阅以下视频：

<br>

> [!VIDEO https://www.youtube.com/embed/nE5XSOBV0rI]

在此版本的 Windows 中也有新内容：
- Intune 注册状态页 (ESP) 立即跟踪 Intune 管理扩展。
- 默认情况下，对于所有 Windows 10 专业教育版和 Enterprise Sku，禁用了[OOBE 期间 Cortana voiceover 和语音识别](windows-autopilot-scenarios.md#cortana-voiceover-and-speech-recognition-during-oobe)。
- [Windows Autopilot 在 OOBE 期间自我更新](windows-autopilot-scenarios.md#windows-autopilot-is-self-updating-during-oobe)。 从 Windows 10 开始，版本 1903 Autopilot 功能和关键更新将在 OOBE 期间自动开始下载。
- Windows Autopilot 会在运行 Windows 10 1903 版或更高版本的设备上的 OOBE 期间将诊断数据级别设置为 Full。 

## <a name="new-in-windows-10-version-1809"></a>Windows 10 中的新增版本1809版

Windows Autopilot [自助部署模式](self-deploying.md) 是零触控设备预配过程。 只需打开设备，连接到以太网，Autopilot 会自动配置设备。 在部署过程中，最终用户无需按 "下一步" 按钮。 

可以使用 Windows Autopilot self 部署模式将设备注册到 AAD 租户、注册组织的 MDM 提供程序，以及预配策略和应用程序。 不需要用户身份验证或用户交互。

>[!NOTE]
>Windows 10 版本1903或更高版本需要使用自部署模式，因为 Windows 10 版本1809中的 TPM 设备证明有问题。

## <a name="related-topics"></a>相关主题

[Microsoft Intune 新增功能](/intune/whats-new)<br>
[Windows 10 中的新增功能](/windows/whats-new/)
