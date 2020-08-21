---
title: 管理 VDI 客户端
titleSuffix: Configuration Manager
description: 在虚拟桌面基础结构 (VDI) 中管理 Configuration Manager 客户端。
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: abd45393-d84e-4583-bc80-74bbb3709577
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1d79edb5ad1a60c5876163281ec5c1d1c17eff0a
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692802"
---
# <a name="manage-configuration-manager-clients-in-a-virtual-desktop-infrastructure-vdi"></a>在虚拟桌面基础结构 (VDI) 中管理 Configuration Manager 客户端

适用范围：  Configuration Manager (Current Branch)

Configuration Manager 支持在以下虚拟桌面基础结构 (VDI) 方案中安装 Configuration Manager 客户端：

- 个人虚拟机：虚拟机 (VM) 保留会话之间的用户数据和设置。

- 远程桌面服务会话：在集中式服务器上托管多个并发客户端会话。 用户连接到会话，然后在此服务器上运行应用程序。

- 共用虚拟机：VM 不保留会话之间的用户数据和设置。 当用户关闭会话时，虚拟环境会放弃所有数据和设置。 当无法使用远程桌面服务时，共用虚拟机就非常有用。 例如，当所需的应用程序无法在托管客户端会话的 Windows Server 上运行时。

- Windows 虚拟桌面：在 Microsoft Azure 上运行的桌面和应用虚拟化服务。 从版本 1906 开始，可以使用 Configuration Manager 管理在 Azure 中运行 Windows 的这些虚拟设备。

## <a name="personal-vms"></a>个人 VM

Configuration Manager 将个人 VM 视为物理计算机。 可以在 VM 映像上预安装 Configuration Manager 客户端，也可以在预配它后再安装。

有关详细信息，请参阅[对虚拟化环境的支持](../../../plan-design/configs/support-for-virtualization-environments.md)。

## <a name="remote-desktop-services"></a>远程桌面服务

你不会为单个远程桌面会话安装 Configuration Manager 客户端。 在托管远程桌面服务的服务器上安装一次。 可以在远程桌面服务服务器上使用所有 Configuration Manager 客户端功能。

有关详细信息，请参阅[欢迎使用远程桌面服务](/windows-server/remote/remote-desktop-services/welcome-to-rds)。

## <a name="pooled-vms"></a>共用 VM

如果你解除共用虚拟机授权，就会丢失 Configuration Manager 所做的任何更改。

由于 VM 可能只能运行很短的时间，因此一些 Configuration Manager 功能可能不会返回相关数据。 例如，硬件清单、软件清单和软件计数。 不妨从清单任务中排除共用 VM。

## <a name="windows-virtual-desktop"></a>Windows 虚拟桌面

有关详细信息，请参阅[客户端和设备支持的操作系统](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop)。

## <a name="other-considerations"></a>其他注意事项

因为虚拟化支持在同一台物理计算机上运行多个 Configuration Manager 客户端，所以许多客户端操作都对计划性操作有内置的随机化延迟。 例如，硬件和软件清单、反恶意软件扫描、软件安装和软件更新扫描。 对于包含多个运行 Configuration Manager 客户端的 VM 的服务器，这种延迟有助于分配 CPU 处理和数据传输。

除了处于维护服务模式的 Windows Embedded 客户端之外，不在虚拟化环境中的 Configuration Manager 客户端也使用这种随机化延迟。 此行为有助于避免网络带宽出现峰值。 它还减少了站点系统（如管理点和站点服务器）上的 CPU 处理。 延迟间隔因 Configuration Manager 功能而异。 例如，请参阅[关于客户端设置 - 禁用截止时间随机化](../about-client-settings.md#disable-deadline-randomization)。

为了帮助在支持多个用户会话的虚拟环境中提高 Configuration Manager 客户端性能，它在默认情况下禁用了用户策略。 自版本 1910 起，可以在此方案中启用用户策略。 有关详细信息，请参阅[关于客户端设置 - 为多个用户会话启用用户策略](../about-client-settings.md#enable-user-policy-for-multiple-user-sessions)。