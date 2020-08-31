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
ms.openlocfilehash: f72410d0570e1b9ebbc324f26a288100e744f422
ms.sourcegitcommit: 41e6e6b7f5c2a87aaf7f23d90d0f175dd63c0579
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89056986"
---
# <a name="setting-the-bitlocker-encryption-algorithm-for-autopilot-devices"></a>设置 Autopilot 设备的 BitLocker 加密算法

**适用于**

-  Windows 10

在 Windows Autopilot 中，你可以将 BitLocker 加密设置配置为在自动加密开始之前应用。 此配置可确保不会自动应用默认加密算法。 还可以在自动 BitLocker 加密开始之前应用其他 BitLocker 策略。 

Bitlocker 加密算法在第一次启用 BitLocker 时使用。 该算法设置用于整卷加密的强度。 可用的加密算法包括： AES-CBC 128 位、AES-CBC 256 位、XTS-AES 128 位或 XTS-AES 256 位加密。 默认值为 XTS-AES 128 位加密。 有关建议使用的加密算法的信息，请参阅 [BITLOCKER CSP](/windows/client-management/mdm/bitlocker-csp) 。

若要确保在 Autopilot 设备进行自动加密之前，请设置所需的 BitLocker 加密算法：

1. 将 Windows 10 Endpoint Protection 配置文件中的 [加密方法设置](/intune/endpoint-protection-windows-10#windows-encryption) 配置为所需的加密算法。 
2. [将策略分配](/intune/device-profile-assign)到 Autopilot 设备组。 必须将加密策略分配给组中的 **设备** ，而不是用户。
3. 对这些设备启用 Autopilot [注册状态页](enrollment-status.md) (ESP)。 如果未启用 ESP，则在开始加密之前不会应用该策略。

下面显示了 Microsoft Intune Windows 加密设置的示例。

![BitLocker 加密设置](images/bitlocker-encryption.png)

自动加密的设备在更改加密算法之前需要进行解密。

这些设置在 "**设备配置**" "配置文件" "  >  **Profiles**  >  **创建配置**文件  >  **平台**= Windows 10 及更高版本" 下提供，配置文件类型 = Endpoint protection >**配置**  >  **Windows 加密**  >  **BitLocker 基本设置**，配置加密方法 = 启用。

建议设置**windows 加密**  >  **windows Settings**Encryption  >  **Encrypt** = 要求。

## <a name="requirements"></a>要求

Windows 10 版本1809或更高版本。

## <a name="next-steps"></a>后续步骤

[BitLocker 概述](/windows/security/information-protection/bitlocker/bitlocker-overview)