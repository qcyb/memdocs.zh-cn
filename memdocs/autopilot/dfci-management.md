---
title: DFCI 管理
ms.reviewer: ''
manager: laurawi
description: 使用 Windows Autopilot Deployment 和 Intune，你可以在通过使用设备固件配置接口 () DFCI 来注册 UEFI (BIOS) 设置。
keywords: Autopilot，DFCI，UEFI，Windows 10
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
ms.openlocfilehash: df49fb939b709c15f2b01b3577f7fc7ced60140d
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88908342"
---
# <a name="dfci-management"></a>DFCI 管理

**适用于**

-   Windows 10

使用 Windows Autopilot Deployment 和 Intune，你可以在 (UEFI) 设置注册后，使用设备固件配置界面 (DFCI) 来管理统一可扩展固件接口。  DFCI [使 Windows 可以将管理命令](/windows/client-management/mdm/uefi-csp) 从 Intune 传递到 UEFI，并将其传递到 Autopilot 部署的设备。 这允许您限制最终用户对 BIOS 设置的控制。 例如，你可以锁定启动选项，以防止用户启动其他 OS （例如不具有相同安全功能的 OS）。

如果用户重新安装了以前的 Windows 版本，请安装单独的操作系统或格式化硬盘驱动器，它们不能替代 DFCI 管理。 此功能还可防止恶意软件与 OS 进程进行通信，包括提升的操作系统进程。 DFCI 的信任链使用公钥加密，而不依赖于本地 UEFI 密码安全。 此安全层阻止本地用户从设备的 UEFI 菜单访问托管设置。

有关 DFCI 权益、方案和先决条件的概述，请参阅 [设备固件配置界面 (DFCI) 简介](https://microsoft.github.io/mu/dyn/mu_plus/DfciPkg/Docs/Dfci_Feature/)。

## <a name="dfci-management-lifecycle"></a>DFCI 管理生命周期

可以将 DFCI 管理生命周期视为 UEFI 集成、设备注册、配置文件创建、注册、管理、停用和恢复。 请参阅下图。

   ![生命周期](images/dfci.png)

## <a name="requirements"></a>要求

- 需要 Windows 10 版本1809或更高版本以及支持的 UEFI。
- 设备制造商必须在生产过程中将 DFCI 添加到其 UEFI 固件，或添加为你安装的固件更新。 与设备供应商合作，确定 [支持 DFCI 的制造商](#oems-that-support-dfci)，或使用 DFCI 所需的固件版本。
- 设备必须通过 Microsoft Intune 进行管理。 有关详细信息，请参阅 [使用 Windows Autopilot 在 Intune 中注册 Windows 设备](/intune/enrollment/enrollment-autopilot)。
- 设备必须由 [Microsoft 云解决方案提供商 (CSP) 合作伙伴](https://partner.microsoft.com/membership/cloud-solution-provider)注册为 Windows Autopilot，或由 OEM 直接注册。 

>[!IMPORTANT]
>对于 Autopilot (手动注册的设备（例如通过 [从 csv 文件导入](/intune/enrollment/enrollment-autopilot#add-devices)) 不允许使用 DFCI）。 DFCI 管理默认需要通过 OEM 或 Microsoft CSP 合作伙伴注册 Windows Autopilot 来对设备的商业采购进行外部认证。 注册设备后，其序列号将显示在 Windows Autopilot 设备列表中。

## <a name="managing-dfci-profile-with-windows-autopilot"></a>通过 Windows Autopilot 管理 DFCI 配置文件

通过 Windows Autopilot 管理 DFCI 配置文件有四个基本步骤：

1. 创建 Autopilot 配置文件
2. 创建注册状态页配置文件
3. 创建 DFCI 配置文件
4. 分配配置文件

有关详细信息，请参阅 [创建配置文件](/intune/configuration/device-firmware-configuration-interface-windows#create-the-profiles) 和 [分配配置文件](/intune/configuration/device-firmware-configuration-interface-windows#assign-the-profiles-and-reboot) 。

你还可以更改正在使用的设备上 [现有的 DFCI 设置](/intune/configuration/device-firmware-configuration-interface-windows#update-existing-dfci-settings) 。 在现有的 DFCI 配置文件中，更改设置并保存更改。 由于已分配了配置文件，因此新的 DFCI 设置将在下一次设备同步或设备重新启动时生效。

## <a name="oems-that-support-dfci"></a>支持 DFCI 的 Oem

- [Microsoft Surface](/surface/surface-manage-dfci-guide)

其他 Oem 处于挂起状态。

## <a name="see-also"></a>请参阅

[Microsoft DFCI 方案](https://microsoft.github.io/mu/dyn/mu_plus/DfciPkg/Docs/Scenarios/DfciScenarios/)<br>
[Windows Autopilot 和 Surface 设备](/surface/windows-autopilot-and-surface-devices)<br>