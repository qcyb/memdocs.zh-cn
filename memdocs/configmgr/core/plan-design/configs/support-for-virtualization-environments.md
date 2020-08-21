---
title: 支持虚拟化
titleSuffix: Configuration Manager
description: 在虚拟化环境中安装 Configuration Manager 客户端和站点系统角色的要求。
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1098e8c5-9676-4c2b-841b-ec88bd04e495
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f7d774d620916f3d735a3545db5fe1e41988731d
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126675"
---
# <a name="support-for-virtualization-environments-with-configuration-manager"></a>Configuration Manager 支持虚拟化环境

适用范围：  Configuration Manager (Current Branch)

Configuration Manager 支持在受支持的操作系统上安装客户端和站点系统角色，这些操作系统在某些虚拟化环境中作为虚拟机 (VM) 运行。 即使不支持虚拟主机（虚拟化环境）作为客户端或站点服务器，也存在这种支持。

例如，使用 Microsoft Hyper-V Server 2016 来托管运行 Windows Server 2019 的 VM。 可以在运行 Windows Server 2019 的 VM 上安装客户端或站点系统角色。 无法在运行 Microsoft Hyper-V Server 2016 的主机上安装客户端。

## <a name="virtualization-environments"></a>虚拟化环境

- Windows Server 2019  
- Windows Server 2016<sup>[注 1](#bkmk_note1)</sup>  
- Microsoft Hyper-V Server 2016<sup>[注 1](#bkmk_note1)</sup>  
- Windows Server 2012 R2  
- Microsoft Hyper-V Server 2012  
- Windows Server 2012  

<a name="bkmk_note1"></a>

> [!NOTE]
> Configuration Manager 不支持[嵌套虚拟化](https://docs.microsoft.com/windows-server/virtualization/hyper-v/What-s-new-in-Hyper-V-on-Windows#nested-virtualization-new)，这是 Windows Server 2016 的新增功能。

### <a name="virtualization-environment-support"></a>虚拟化环境支持

每台虚拟计算机都需要与物理 Configuration Manager 计算机相同或 更多的硬件和软件要求。

若要验证 Configuration Manager 是否支持虚拟化环境，请使用服务器虚拟化验证计划。 其中包括联机的“虚拟化计划支持策略向导”。 有关详细信息，请参阅 [Windows 服务器虚拟化验证计划](https://www.windowsservercatalog.com/svvp.aspx)。

Configuration Manager 无法管理脱机的 VM。 主计算机上的 Configuration Manager 客户端无法管理脱机的 VM 映像。 例如，它无法安装软件更新或收集硬件清单。

通常，Configuration Manager 不会特别考虑 VM。 例如，如果你停止一个 VM，并且没有保存它的状态，Configuration Manager 可能无法确定是否必须重新安装软件更新。

为了帮助在支持多个用户会话的虚拟环境中提高 Configuration Manager 客户端性能，它在默认情况下禁用了用户策略。 自版本 1910 起，可以在此方案中启用用户策略。 有关详细信息，请参阅[关于客户端设置 - 为多个用户会话启用用户策略](../../clients/deploy/about-client-settings.md#enable-user-policy-for-multiple-user-sessions)。

## <a name="microsoft-azure-vms"></a><a name="bkmk_Azure"></a> Microsoft Azure VM

Configuration Manager 可以在 Azure 中的 VM 上运行，就像它在数据中心内本地运行一样。 在以下方案中，将 Configuration Manager 用于 Azure VM：

- **方案 1**：在 Azure VM 中运行 Configuration Manager。 使用它来管理其他 Azure VM 上的客户端。

- **方案 2**：在 Azure VM 中运行 Configuration Manager。 使用它来管理不在 Azure 上运行的客户端。

- **方案 3**：在 Azure VM 中运行不同的 Configuration Manager 站点系统角色。 在本地数据中心内运行其他角色（已正确连接到 Azure）。

对于网络、受支持的配置和硬件的 Configuration Manager 要求也适用于 Azure VM。

有关详细信息，请参阅 [Azure 上的 Configuration Manager](../../understand/configuration-manager-on-azure.md)。

> [!IMPORTANT]
> 在 Azure VM 中运行的 Configuration Manager 站点和客户端与本地安装遵循相同的许可证要求。

## <a name="windows-virtual-desktop"></a>Windows 虚拟桌面

[Windows 虚拟桌面](https://docs.microsoft.com/azure/virtual-desktop/)是在 Microsoft Azure 上运行的桌面和应用虚拟化服务。 从版本 1906 开始，可以使用 Configuration Manager 管理在 Azure 中运行 Windows 的这些虚拟设备。 有关详细信息，请参阅[客户端和设备支持的操作系统](supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop)。

## <a name="next-steps"></a>后续步骤

[在虚拟桌面基础结构 (VDI) 中管理 Configuration Manager 客户端](../../clients/deploy/plan/considerations-for-managing-clients-in-a-vdi.md)