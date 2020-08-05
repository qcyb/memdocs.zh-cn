---
title: Windows Autopilot 方案和功能
description: 请遵循几个典型的 Windows Autopilot 部署方案，如在业务就绪状态下重新部署设备。
keywords: mdm, 设置, windows, windows 10, oobe, 管理, 部署, autopilot, ztd, 零接触, 合作伙伴, msfb, intune
ms.reviewer: mniehaus
manager: laurawi
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
ms.openlocfilehash: 063d791b4b2373f195625c996c6b4a1667015ad3
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87756107"
---
# <a name="windows-autopilot-scenarios-and-capabilities"></a>Windows Autopilot 方案和功能

**适用于： Windows 10**

## <a name="scenarios"></a>方案

Windows Autopilot 支持不断增长的方案列表，旨在支持常见的组织需求。 这些需求取决于组织的类型，并将其进度转移到 Windows 10 并[过渡到新式管理](https://docs.microsoft.com/windows/client-management/manage-windows-10-in-your-organization-modern-management)。

本指南中介绍了以下 Windows Autopilot 方案：

| 场景 | 详细信息 |
| --- | --- |
| 部署将由组织的成员设置并为该人员配置的设备 | [Windows Autopilot 用户驱动模式](user-driven.md) |
| 部署将自动配置为以共享方式使用、作为展台或数字告示设备进行配置的设备。| [Windows Autopilot 自部署模式](self-deploying.md) |
| 重新部署处于企业就绪状态的设备。| [Windows Autopilot 重置](windows-autopilot-reset.md) |
| 使用最新的应用程序、策略和设置预先设置设备。| [白色手套](white-glove.md) |
| 在现有的 Windows 7 或8.1 设备上部署 Windows 10 | [面向现有设备的 Windows Autopilot](existing-devices.md) |

以下视频概述了这些方案。

&nbsp;

> [!video https://www.microsoft.com/videoplayer/embed/RE4Ci1b?autoplay=false]

## <a name="windows-autopilot-capabilities"></a>Windows Autopilot 功能

### <a name="windows-autopilot-is-self-updating-during-oobe"></a>Windows Autopilot 在 OOBE 期间自行更新

从 Windows 10 开始，版本1903、Autopilot 功能和关键更新将在设备连接到网络后，在 OOBE 期间自动开始下载，并在[关键驱动程序和 Windows 零天修补程序 (ZDP) 更新](https://docs.microsoft.com/windows-hardware/customize/desktop/windows-updates-during-oobe)已完成。 用户或 IT 管理员无法选择退出这些 Autopilot 更新，因为 Windows Autopilot 部署需要它们才能正常运行。  Windows 将提醒用户设备正在检查、下载和安装更新。

有关详细信息，请参阅[Windows Autopilot 更新](autopilot-update.md)。

### <a name="cortana-voiceover-and-speech-recognition-during-oobe"></a>OOBE 期间 Cortana voiceover 和语音识别

在 Windows 10 中，默认情况下，对所有 Windows 10 专业版、教育版和企业版 Sku 禁用了版本1903及更高版本的 Cortana voiceover 和语音识别。

还可以通过创建以下注册表项，在 OOBE 期间启用 Cortana voiceover 和语音识别。 默认情况下，此项不存在：

HKLM\Software\Microsoft\Windows\CurrentVersion\OOBE\EnableVoiceForAllEditions

键值为 DWORD， **0** = 禁用， **1** = 已启用。

| 值 | 说明 |
| --- | --- |
| 0 | Cortana voiceover 已禁用 |
| 1 | 已启用 Cortana voiceover |
| 无值 | 设备将回退到版本的默认行为 |

若要更改此密钥值，请使用 WCD 工具创建，如[此处](https://docs.microsoft.com/windows/configuration/wcd/wcd-oobe#nforce)所述。

### <a name="bitlocker-encryption"></a>BitLocker 加密

在 Windows Autopilot 中，你可以将 BitLocker 加密设置配置为在开始自动加密之前应用。 有关详细信息，请参阅[设置适用于 Autopilot 设备的 BitLocker 加密算法](bitlocker.md)

## <a name="related-topics"></a>相关主题

[Windows Autopilot：新增功能](windows-autopilot-whats-new.md)
