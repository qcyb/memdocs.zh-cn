---
title: 不符合性代码
titleSuffix: Configuration Manager
description: 关于可能从不符合 BitLocker 策略的 Configuration Manager 客户端返回的代码的技术参考
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 6c28fa29-fc97-49ef-9fc3-cb062bdba908
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e8ee130929605f8087eb7fbef55e8a27618c3aed
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705955"
---
# <a name="non-compliance-codes"></a>不符合性代码

适用范围：  Configuration Manager (Current Branch)

<!--3601034-->

客户端上的 WMI 返回以下不符合性代码。 它还描述了特定设备报告为不符合的原因。

查看 WMI 的方法有多种。 例如，使用以下 PowerShell 命令：

``` PowerShell
(Get-WmiObject -Class mbam_Volume -Namespace root\microsoft\mbam).ReasonsForNoncompliance
```

> [!TIP]
> 如果设备符合，此命令不返回任何内容。
>
> 也可以查看此类的 `Compliant` 属性：如果设备符合，属性值为 `1`。

|不符合性代码|不符合的原因|
|--- |--- |
|0|密码长度不是 AES 256。|
|1|BitLocker 策略要求对此卷进行加密，但此卷没有加密。|
|2|BitLocker 策略要求不  对此卷进行加密，但此卷已加密。|
|3|BitLocker 策略要求此卷使用 TPM 保护程序，但它没有。|
|4|BitLocker 策略要求此卷使用 TPM+PIN 保护程序，但它没有。|
|5|BitLocker 策略不允许非 TPM 计算机报告为符合。|
|6|卷有 TPM 保护程序，但 TPM 不可见。|
|7|BitLocker 策略要求此卷使用密码保护程序，但它没有。|
|8|BitLocker 策略要求此卷不  使用密码保护程序，但它使用了。|
|9|BitLocker 策略要求此卷使用自动解锁保护程序，但它没有。|
|10|BitLocker 策略要求此卷不  使用自动解锁保护程序，但它使用了。|
|11|BitLocker 检测到策略冲突，这会阻止它将此卷报告为符合。|
|12|需要系统卷来加密 OS 卷，但没有系统卷。|
|13|卷保护已暂停。|
|14|自动解锁保护程序并不安全，除非 OS 卷已加密。|
|15|策略要求的最低密码强度为 XTS-AES-128 位，但实际密码强度较弱。|
|16|策略要求的最低密码强度为 XTS-AES-256 位，但实际密码强度较弱。|
