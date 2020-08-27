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
ms.openlocfilehash: 326901cef5b337a505d85dc6c5706109ad9cbc1f
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88908538"
---
# <a name="windows-autopilot-device-guidelines"></a>Windows Autopilot 设备指南

**适用于**

- Windows 10

## <a name="hardware-and-firmware-best-practice-guidelines-for-windows-autopilot"></a>适用于 Windows Autopilot 的硬件和固件最佳实践指南

与 Windows Autopilot 一起使用的所有设备都应满足 Windows 10 的 [最低硬件要求](/windows-hardware/design/minimum/minimum-hardware-requirements-overview) 。  

以下最佳做法确保在 Windows Autopilot 部署过程中可以轻松地设置设备： 
- 请确保 TPM 2.0 已启用且处于良好状态 (不在适用于 Windows Autopilot 自部署模式的设备上) **缩减功能模式下** 运行。
- OEM 将唯一的元组信息 (SmbiosSystemManufacturer、SmbiosSystemProductName、SmbiosSystemSerialNumber) 或 PKID + SmbiosSystemSerialNumber 预配到每个 Microsoft 规范的 [smbios 字段](/windows-hardware/drivers/bringup/smbios) 中 (制造商、产品名称和存储在 smbios 类型 1 04h 中的序列号，键入1个05H 并键入1个 07h) 。
- OEM 上传4K 的硬件哈希使用 OA3 工具 RS3 + 在将设备寄送到 Autopilot 客户或渠道合作伙伴之前，在完整操作系统上通过 CBR 报表以审核模式运行。
- Microsoft 要求将 OEM 发货驱动程序发布到提交的30天内的 Windows 更新。 在14天内，系统固件和驱动程序更新将发布到 Windows 更新。
- OEM 确保在 SMBIOS 中预配的 PKID 传递到通道。

## <a name="software-best-practice-guidelines-for-windows-autopilot"></a>适用于 Windows Autopilot 的软件最佳做法指南

- 应仅使用 Windows 10 基本映像和驱动程序预安装 Windows Autopilot 设备。
- 可以预安装 Office 的许可版本，如 Microsoft 365 适用 [于企业的应用程序](/deployoffice/about-office-365-proplus-in-the-enterprise)。
- 除非客户明确请求，否则不应包含任何其他预安装软件。
  - 根据 OEM 策略，不应禁用或删除 Windows 10 的功能，包括内置应用。

## <a name="related-topics"></a>相关主题

[Windows Autopilot 客户许可](registration-auth.md)<br>
[主板更换方案指南](autopilot-mbr.md)<br>