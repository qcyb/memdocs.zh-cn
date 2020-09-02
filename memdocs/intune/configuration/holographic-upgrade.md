---
title: 在 Microsoft Intune 中升级到 Windows Holographic for Business - Azure | Microsoft Docs
description: 在 Microsoft Intune 中使用设备配置文件升级到 Windows 10 Holographic for Business。
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
ms.openlocfilehash: 65a45b13a91671c1de9bcf04f23156d75313285f
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88907763"
---
# <a name="upgrade-devices-running-windows-holographic-to-windows-holographic-for-business"></a>将运行 Windows Holographic 的设备升级到 Windows Holographic for Business

Microsoft Intune 包含许多有助于管理和保护设备的设置。 本文列出并介绍了用于将 Windows Holographic 设备升级为 Windows Holographic for Business 的设置。

作为移动设备管理 (MDM) 解决方案的一部分，请使用这些设置升级 Windows Holographic 设备。 对于 Microsoft HoloLens，可以通过购买商业套件来获得升级所需的许可证。 有关详细信息，请参阅[解锁 Windows Holographic for Business 功能](/hololens/hololens1-upgrade-enterprise)。

作为 Intune 管理员，可以创建这些设置，并将它们分配到设备。

若要详细了解此功能，请参阅[升级 Windows 10 版本或启用 S 模式](edition-upgrade-configure-windows-10.md)。

## <a name="before-you-begin"></a>在开始之前

[创建 Windows 10 版本升级和模式切换设备配置文件](edition-upgrade-configure-windows-10.md#create-the-profile)。

创建 Windows 10 版本升级和模式切换设备配置文件时，设置数超过本文中所列的设置。 Windows Holographic for Business 设备支持本文中的设置。

## <a name="edition-upgrade"></a>版本升级

- **要升级到的版本**：选择“Windows 10 Holographic for Business”。
- **许可证文件**：转到并选择系统提供的 XML 许可证文件。

  :::image type="content" source="./media/holographic-upgrade/Holographic-edition-upgrade.png" alt-text="在 Intune 中，输入包含 Holographic for Business 许可证信息的 XML 文件名。":::

## <a name="next-steps"></a>后续步骤

[分配配置文件](device-profile-assign.md)并[监视其状态](device-profile-monitor.md)。

还可以为 [Windows 10 及更高版本](edition-upgrade-windows-settings.md)设备创建版本升级配置文件。