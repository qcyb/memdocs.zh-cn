---
title: Windows Autopilot 设备指南
ms.reviewer: ''
manager: laurawi
description: 了解有关 Windows Autopilot 部署的硬件、固件和软件最佳实践的全部信息。
keywords: mdm, 设置, windows, windows 10, oobe, 管理, 部署, autopilot, ztd, 零接触, 合作伙伴, msfb, intune
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
ms.openlocfilehash: eb591206ad61878bc2637bf1a10c2a1cec17ddba
ms.sourcegitcommit: 41e6e6b7f5c2a87aaf7f23d90d0f175dd63c0579
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89057359"
---
# <a name="windows-autopilot-device-guidelines"></a>Windows Autopilot 设备指南

**适用于**

- Windows 10

## <a name="hardware-and-firmware-best-practice-guidelines-for-windows-autopilot"></a>适用于 Windows Autopilot 的硬件和固件最佳实践指南

使用 Windows Autopilot 的所有设备都应满足适用于 Windows 10 的 [最低硬件要求](/windows-hardware/design/minimum/minimum-hardware-requirements-overview) 。  

以下最佳做法确保在 Windows Autopilot 部署过程中可以轻松地设置设备： 
- TPM 2.0 已启用并处于良好状态 (不在适用于 Windows Autopilot 自行部署模式的设备上) **缩减功能模式** 。
- OEM 应在 [SMBIOS 字段](/windows-hardware/drivers/bringup/smbios)中预配以下任何信息。 此信息应遵循 Microsoft 规范 (制造商、产品名称和存储在 SMBIOS 类型 1 04h 中的序列号，键入 1 05h 并键入 1 07h) 。
    - 唯一元组信息 (SmbiosSystemManufacturer，SmbiosSystemProductName，SmbiosSystemSerialNumber) 
    - PKID + SmbiosSystemSerialNumber
- 在将设备寄送到 Autopilot 客户或渠道合作伙伴之前，OEM 应使用 CBR 报表向 Microsoft 上传4K 的硬件哈希。 应使用 OA3 工具 RS3 + 在完整操作系统上使用审核模式运行哈希。
- Microsoft 要求 OEM 发运驱动程序在 CBR 提交日期30天内发布到 Windows 更新。 在14天内，系统固件和驱动程序更新将发布到 Windows 更新。
- OEM 确保在 SMBIOS 中预配的 PKID 传递到通道。

## <a name="software-best-practice-guidelines-for-windows-autopilot"></a>适用于 Windows Autopilot 的软件最佳做法指南

- 应仅使用 Windows 10 基本映像和驱动程序预安装 Windows Autopilot 设备。
- 可以预安装 Office 的许可版本，如 Microsoft 365 适用 [于企业的应用程序](/deployoffice/about-office-365-proplus-in-the-enterprise)。
- 除非客户明确请求，否则不应包含任何其他预安装软件。
  - 每个 OEM 策略都不应禁用或删除 Windows 10 功能（包括内置应用）。

## <a name="next-steps"></a>后续步骤

[Windows Autopilot 客户许可](registration-auth.md)<br>
[主板更换方案指南](autopilot-mbr.md)<br>