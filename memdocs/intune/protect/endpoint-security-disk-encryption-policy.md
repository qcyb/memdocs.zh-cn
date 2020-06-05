---
title: 在 Microsoft Intune 中使用终结点安全性策略管理磁盘加密 | Microsoft Docs
description: 在 Microsoft Endpoint Manager 中为使用终结点安全性磁盘加密策略管理的设备配置和部署策略。
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
ms.openlocfilehash: b988e4ddeb306c7da290c87e8a32fa0571627257
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431665"
---
# <a name="disk-encryption-policy-for-endpoint-security-in-intune"></a>Intune 中的终结点安全性磁盘加密策略

终结点安全性磁盘加密配置文件只关注与设备内置加密方法（如 FileVault 或 BitLocker）相关的设置。 此举可使安全管理员轻松管理磁盘加密设置，而不必浏览大量不相关的设置。

尽管可以通过使用“Endpoint Protection”配置文件进行设备配置，以配置相同的设备设置，但设备配置文件包含其他类别的设置。 这些额外设置与磁盘加密无关，并且可能使仅配置磁盘加密的任务复杂化。

在 [Microsoft endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)的“终结点安全性”节点中的“管理”下查找用于磁盘加密策略的终结点安全性策略。

## <a name="prerequisites-for-disk-encryption-policy"></a>磁盘加密策略的先决条件

- **macOS** - macOS 10.13 或更高版本
- **Windows** - Windows 10 或更高版本

## <a name="disk-encryption-profiles"></a>磁盘加密配置文件

**macOS 配置文件**：

- **FileVault** - FileVault 为 macOS 设备提供了内置的完整磁盘加密。

  管理用于 macOS 的 [FileVault 设置](../protect/endpoint-security-disk-encryption-profile-settings.md#filevault)。

  若要创建 FileVault 配置文件，请参阅[使用用于 macOS 的 FileVault 磁盘加密](../protect/encrypt-devices-filevault.md)。

**Windows 10 配置文件**：

- **BitLocker** - BitLocker 驱动器加密是一种数据保护功能，它与操作系统相集成，以解决因计算机丢失、被盗或停止使用不当而造成的数据盗窃或暴露威胁

  管理用于 Windows 10 的 [BitLocker 设置](../protect/endpoint-security-disk-encryption-profile-settings.md#bitlocker)。

  若要创建 BitLocker 配置文件，请参阅[使用用于 Windows 10 的 BitLocker 磁盘加密](../protect/encrypt-devices.md)。

## <a name="manage-device-encryption"></a>管理设备加密

部署策略以加密设备磁盘后，请参阅以下文章，了解有关管理加密的信息：

- [管理 BitLocker](../protect/encrypt-devices.md#manage-bitlocker)
- [管理 FileVault](../protect/encrypt-devices-filevault.md#manage-filevault)
- [监视设备加密](../protect/encryption-monitor.md)

## <a name="next-steps"></a>后续步骤

- [要创建 FileVault 配置文件](../protect/encrypt-devices-filevault.md#create-an-endpoint-security-policy-for-filevault)
- [要创建 BitLocker 配置文件](../protect/encrypt-devices.md#create-an-endpoint-security-policy-for-bitlocker)
