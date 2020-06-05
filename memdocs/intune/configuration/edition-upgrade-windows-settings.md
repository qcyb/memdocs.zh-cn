---
title: Microsoft Intune 中的 Windows 10 升级设置和 S 模式设置 - Azure | Microsoft Docs
description: 查看在设备上使用 Microsoft Intune 中的设备配置文件升级 Windows 10 版本或启用 S 模式时所有设置及其用途的列表。
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
ms.assetid: ''
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: a91a84ece833bf893395e494a0e99fa675f14c2a
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429658"
---
# <a name="windows-10-and-newer-device-settings-to-upgrade-editions-or-enable-s-mode-in-intune"></a>Intune 中用于升级版本或启用 S 模式的 Windows 10（及更高版本）设备设置

Microsoft Intune 包含许多有助于管理和保护设备的设置。 本文列出并介绍了用于在 Windows 10 设备上升级版本或启用 S 模式的设置。 这些设置是在 Intune 中的升级配置文件中创建，随后被推送或部署到设备。

作为移动设备管理 (MDM) 解决方案的一部分，请使用这些设置控制 Windows 10 设备的版本选项和 S 模式选项。

若要详细了解此功能，请参阅[升级 Windows 10 版本或启用 S 模式](edition-upgrade-configure-windows-10.md)。

## <a name="before-you-begin"></a>在开始之前

[创建配置文件](edition-upgrade-configure-windows-10.md#create-the-profile)。

## <a name="edition-upgrade"></a>版本升级

- **要升级到的版本**：选择要升级到的 Windows 10 版本。 将该策略针对的设备升级到所选版本。
- **产品密钥**：输入从 Microsoft 收到的产品密钥。 创建包含产品密钥的策略后，无法更新该密钥，并出于安全原因隐藏该密钥。 要更改产品密钥，请再次输入完整密钥。
- **许可证文件**：对于 Windows 10 Holographic for Business 或 Windows 10 移动版，请选择“浏览”，以选择从 Microsoft 收到的许可证文件。 此许可证文件包含要将设备升级到的版本的许可证信息。

## <a name="mode-switch"></a>模式切换

- **切出 S 模式**：将设备切换退出 S 模式。 选项包括：

  - **无配置**：Intune 不会更改或更新此设置。 默认情况下，S 模式设备可能保持 S 模式。 用户可将设备切出 S 模式。
  - **保持 S 模式**：阻止用户将设备切出 S 模式。
  - **切换**：允许用户将设备切出 S 模式。

## <a name="next-steps"></a>后续步骤

[分配配置文件](device-profile-assign.md)并[监视其状态](device-profile-monitor.md)。

还可以为 [Windows Holographic for Business](holographic-upgrade.md) 设备创建版本升级配置文件。
