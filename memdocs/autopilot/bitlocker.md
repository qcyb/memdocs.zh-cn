---
title: 设置 Autopilot 设备的 BitLocker 加密算法
ms.reviewer: ''
manager: laurawi
description: Microsoft Intune 提供了一组全面的配置选项来管理 Windows 10 设备上的 BitLocker。
keywords: Autopilot，BitLocker，加密，256位，Windows 10
ms.prod: w10
ms.mktglfcycl: deploy
ms.sitesec: library
ms.pagetype: deploy
ms.localizationpriority: medium
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: 8ea2e0de96887e8f7d97633a041721462b81d6c8
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88908295"
---
# <a name="setting-the-bitlocker-encryption-algorithm-for-autopilot-devices"></a>设置 Autopilot 设备的 BitLocker 加密算法

**适用于**

-   Windows 10

在 Windows Autopilot 中，你可以将 BitLocker 加密设置配置为在开始自动加密之前应用。 这可以确保在不需要此设置时不会自动应用默认加密算法。 在自动 BitLocker 加密开始之前，必须在加密之前应用的其他 BitLocker 策略也可以提供。 

Bitlocker 加密算法在第一次启用 BitLocker 时使用，并设置应进行全卷加密的强度。 可用的加密算法包括： AES-CBC 128 位、AES-CBC 256 位、XTS-AES 128 位或 XTS-AES 256 位加密。 默认值为 XTS-AES 128 位加密。 有关建议使用的加密算法的信息，请参阅 [BITLOCKER CSP](/windows/client-management/mdm/bitlocker-csp) 。

若要确保在 Autopilot 设备进行自动加密之前设置所需的 BitLocker 加密算法：

1. 在 Windows 10 终结点保护配置文件中配置[加密方法设置](/intune/endpoint-protection-windows-10#windows-encryption)以得到所需的加密算法。 
2. [将策略分配](/intune/device-profile-assign)到 Autopilot 设备组。 
    - **重要提示**：加密策略必须分配给组中的**设备**，而非用户。
3. 对这些设备启用 Autopilot [注册状态页](enrollment-status.md) (ESP)。 
    - **重要提示**：如果未启用 ESP，加密开始之前不会应用该策略。

下面显示了 Microsoft Intune Windows 加密设置的示例。

   ![BitLocker 加密设置](images/bitlocker-encryption.png)

**注意**：自动加密的设备在更改加密算法之前需要进行解密。

这些设置在 "设备配置-> 配置文件-> 创建配置文件-> 平台 = Windows 10 及更高版本，配置文件类型 = Endpoint protection-> 配置-> Windows 加密-> BitLocker 基本设置，" 配置加密方法 = 启用 "下提供。

**注意**：也建议设置 windows 加密 > windows 设置-> Encryption = **需要**。

## <a name="requirements"></a>要求

Windows 10 版本1809或更高版本。

## <a name="see-also"></a>请参阅

[BitLocker 概述](/windows/security/information-protection/bitlocker/bitlocker-overview)