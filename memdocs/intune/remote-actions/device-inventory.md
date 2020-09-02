---
title: 使用 Microsoft Intune 查看设备详细信息 - Azure | Microsoft Docs
description: 查看设备的详细信息，包括操作系统、存储空间、制造商和型号。 在 Azure 的 Microsoft Intune 中获取已安装应用的列表、检查符合性策略和设置 TeamViewer。 类似于查看管理设备的清单。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/12/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: e71c6bdb-d75c-404f-8e38-24a663be81c2
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: e6aa3c887a22c468d8d482ce2d4ba0da8202fceb
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88906814"
---
# <a name="see-device-details-in-intune"></a>在 Intune 中查看设备详细信息

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

“设备”功能可提供管理设备的其他详细信息，包括其硬件和已安装的应用。

本文介绍如何在 Azure 门户中查看所有设备及其属性。

## <a name="view-the-device-details"></a>查看设备详细信息

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
3. 选择“设备” > “所有设备”，然后选择某个列出的设备以打开其详细信息 ：

   - “概述”显示设备名称，并列出设备的某些关键属性，例如该设备是个人设备还是公司设备、序列号、主要用户等。 可以在设备上执行以下操作：
      - [停用](devices-wipe.md#retire)
      - [擦除](devices-wipe.md#wipe)
      - [删除](devices-wipe.md#delete-devices-from-the-intune-portal)
      - [远程锁定](device-remote-lock.md)
      - [同步](device-sync.md)
      - [重置密码](device-passcode-reset.md)
      - [重启](device-restart.md)（仅限 Windows）
      - [重新开始](device-fresh-start.md)（仅限 Windows）
      - [Autopilot 重置](/windows/deployment/windows-autopilot/windows-autopilot-reset#reset-devices-with-remote-windows-autopilot-reset)（仅限 Windows）
      - [快速扫描](../configuration/device-restrictions-windows-10.md)（仅限 Windows 10）
      - [完全扫描](../configuration/device-restrictions-windows-10.md)（仅限 Windows 10）
      - [更新 Windows Defender 安全智能](/windows/security/threat-protection/microsoft-defender-antivirus/manage-protection-updates-microsoft-defender-antivirus)
      - [BitLocker 密钥轮换](../protect/encrypt-devices.md#to-rotate-the-bitlocker-recovery-key)
      - [重命名设备](device-rename.md)
      - [新远程协助会话](./teamviewer-support.md)
   - 使用“属性”可以将设备分配到[你创建的设备类别](../enrollment/device-group-mapping.md)，并将设备的所有权更改为个人设备或公司设备。
   - “硬件”包括有关设备的详细信息，例如设备 ID、操作系统和版本、存储空间等详细信息。
   - “发现的应用”列出 Intune 发现的安装在设备上的所有应用以及应用版本。 有关详细信息，请参阅 [Intune 发现的应用](../apps/app-discovered-apps.md)。
   - “设备符合性”列出分配到的所有符合性策略，以及设备是否符合要求。
   - “设备配置”显示分配给该设备的所有设备配置策略，以及该策略成功还是失败。
   - **应用配置** 
   - **终结点安全配置**
   - “恢复密钥”显示找到了设备的可用 BitLocker 密钥
   - “托管应用”列出了 Intune 配置并部署到设备的所有托管应用。 

## <a name="hardware-device-details"></a>硬件设备详细信息
根据设备使用的运营商，可能并不会收集所有详细信息

> [!Note]  
> 硬件和软件清单每 7 天在 Intune 服务中刷新一次。

|详情|说明|平台| 
|--------------|----------------------|----|  
|名称|设备的名称。|Windows、iOS|
|管理名称|仅在控制台中使用的设备名。 更改此名称不会更改设备上的名称。|Windows、iOS|
|UDID|设备的唯一设备标识符。|Windows、iOS|
|Intune 设备 ID|用于唯一标识设备的 GUID。|Windows、iOS|
|序列号|制造商提供的设备序列号。|Windows、iOS|
|共享设备|如果为“是”，设备将被多个用户共享。|Windows、iOS|
|用户已批准注册|如果为“是”，则设备具有用户已批准注册，可让管理员管理设备上的某些安全设置。|Windows、iOS|
|操作系统|设备上使用的操作系统。|Windows、iOS|
|操作系统版本|设备上的操作系统版本。|Windows、iOS|
|操作系统语言|设备上为操作系统设置的语言。|Windows、iOS|
|内部版本号|操作系统的内部版本号。|Android|
|安全修补程序级别|设备的安全修补程序级别。|Android|
|总存储空间|设备上的总存储空间（以千兆字节为单位）。|Windows、iOS|
|可用存储空间|设备上未使用的存储空间（以千兆字节为单位）。|Windows、iOS|
|IMEI|设备的国际移动设备识别。|Windows、iOS/iPadOS、Android|
|MEID|设备的移动设备标识符。|Windows、iOS/iPadOS、Android|
|制造商|设备制造商。|Windows、iOS/iPadOS、Android|
|型号|设备型号。|Windows、iOS/iPadOS、Android|
|电话号码|分配给设备的电话号码。|Windows、iOS/iPadOS、Android*|
|订阅运营商|设备的无线运营商。|Windows、iOS/iPadOS、Android|
|蜂窝技术|设备使用的无线系统。|Windows、iOS/iPadOS、Android|
|Wi-Fi MAC|设备的媒体访问控制地址。|Windows、iOS/iPadOS、Android|
|ICCID|集成电路卡标识符，即 SIM 卡的唯一标识号。|Windows、iOS/iPadOS、Android|
|注册日期|设备在 Intune 中注册的日期和时间。|Windows、iOS/iPadOS、Android|
|上次联系|设备上次连接到 Intune 的日期和时间。|Windows、iOS/iPadOS、Android|
|激活锁旁路代码|可用于禁用激活锁的代码。|iOS|
|已注册 Azure AD|如果为“是”，则设备已向 Azure Directory 注册。|Windows、iOS/iPadOS、Android|
|已注册 Intune|如果为“是”，则设备已向 Intune 注册。|Windows、iOS/iPadOS、Android|
|合规性|设备的符合性状态。|Windows、iOS/iPadOS、Android|
|已激活 EAS|如果为“是”，则设备已于 Exchange 邮箱同步。|Windows、iOS/iPadOS、Android|
|EAS 激活 ID|设备的 Exchange ActiveSync 标识符。|Windows、iOS/iPadOS、Android|
|受到监督|如果为“是”，管理员对设备的控制增强。|Windows、iOS/iPadOS、Android|
|已加密|如果为“是”，则设备上存储的数据已加密。|Windows、iOS/iPadOS、Android|

> [!Note]  
> Android Enterprise 专用设备或完全托管设备上未列出电话号码清单。

## <a name="next-steps"></a>后续步骤
了解使用 Intune [管理设备](device-management.md)还可以执行哪些操作。