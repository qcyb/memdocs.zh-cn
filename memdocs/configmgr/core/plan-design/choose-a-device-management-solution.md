---
title: 选择设备管理解决方案
titleSuffix: Configuration Manager
description: 了解 Microsoft 提供的用于管理电脑、服务器和设备的解决方案。
ms.date: 01/24/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 24633725-791a-4df7-8dce-2c24c1a19a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d36e29f0f915c0f2a35070c667525853e5981564
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702265"
---
# <a name="choose-a-device-management-solution"></a>选择设备管理解决方案

Microsoft 提供用于管理电脑、服务器和设备的不同解决方案。 这些解决方案可在本地、基于云或两者的结合中使用。 请选择适合贵组织业务需求的解决方案。 可以根据进行管理所需的设备平台和所需的管理功能来决定选择哪种解决方案。

## <a name="overview"></a>“概述”

在不同的情景中，提供几种可能最适合的 Microsoft 解决方案。 不需要只选择一个。

- 对于小型组织，诸如 Windows 管理中心这样的工具可能非常合适。
- 大约 75% 的 IT 组织使用 Configuration Manager 来管理其设备。
- Microsoft Azure 通过 Azure Stack 提供来自云或本地的各种解决方案，这些解决方案主要针对服务器管理。
- Microsoft Intune 提供客户端的云管理。
- 可以将 Configuration Manager 和 Intune 与共同管理结合使用。

使用下表来帮助比较这些管理技术：

|  | 仅限云 | 云附加 | 内部 | 已断开连接 |
|---------|---------|---------|---------|---------|
| **Hyper-V 主机** | Not applicable | - Azure Stack<br/> - Windows 管理中心<br/> - Virtual Machine Manager | - Azure Stack<br/> - Windows 管理中心<br/> - Virtual Machine Manager | - Azure Stack<br/> - Windows 管理中心<br/> - Virtual Machine Manager |
| **Windows Server** | - Azure 管理<br/> - Configuration Manager | - Azure 管理<br/> - Configuration Manager | - Azure 管理<br/> - Configuration Manager | 配置管理器 |
| **Linux 服务器** | Azure 管理 | Azure 管理 | Azure 管理 |  |
| **Windows 10** | - Intune<br/> - Configuration Manager | - Intune<br/> - Configuration Manager | - Intune<br/> - Configuration Manager | 配置管理器 |
| **Windows 7 或 8.1** | 配置管理器 | 配置管理器 | 配置管理器 | 配置管理器 |
| **Windows 虚拟桌面** | 配置管理器 | Not applicable | Not applicable | Not applicable |

有关详细信息，请参阅下列文章：

- [什么是 Azure Stack？](https://docs.microsoft.com/azure-stack/operator/azure-stack-overview)
- [什么是 Windows 管理中心？](https://docs.microsoft.com/windows-server/manage/windows-admin-center/understand/what-is)
- [什么是 Virtual Machine Manager？](https://docs.microsoft.com/system-center/vmm/overview)
- [Azure 管理产品](https://docs.microsoft.com/azure/)
- [什么是 Windows 虚拟桌面？](https://docs.microsoft.com/azure/virtual-desktop/overview)

有关 Configuration Manager 和 Intune 解决方案的详细信息，请继续阅读下一节。

## <a name="client-management"></a>客户端管理

本节将以下四个客户端管理解决方案进行了比较：

- [Configuration Manager 客户端](#bkmk_sccm)
- [通过 Configuration Manager 实现本地移动设备管理 (MDM)](#bkmk_opmdm)
- [使用 Microsoft Intune 进行共同管理](#bkmk_comanage)
- [Microsoft Exchange](#bkmk_opmdm)

可以使用这些解决方案本身或彼此之间相互结合使用。 例如，使用基于客户端的管理方法来管理组织中的计算机和服务器，同时使用共同管理来管理基于 Internet 的笔记本电脑。 通过这样的组合方法，可以满足所有设备管理需求。  

还提供两个表，根据以下因素对管理解决方案进行比较：

- [根据支持的平台进行比较](#bkmk_comp1)
- [根据管理功能进行比较](#bkmk_comp2)

### <a name="configuration-manager-client"></a><a name="bkmk_sccm"></a> Configuration Manager 客户端  

此选项要求在设备上安装 Configuration Manager 客户端。 它提供管理你环境中的电脑、服务器和其他设备的大多数功能。

有关详细信息，请参阅[客户端安装方法](../clients/deploy/plan/client-installation-methods.md)。  

### <a name="on-premises-mdm"></a><a name="bkmk_opmdm"></a> 本地 MDM  

此选项使用内置于 Windows 10 的设备管理功能。 尽管没有基于客户端管理的功能全面，但本地 MDM 可提供更轻松的触点方法来进行管理。 它使用本地 Configuration Manager 资源来管理设备。  

有关详细信息，请参阅[使用本地基础结构管理移动设备](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)。  

### <a name="co-management-with-microsoft-intune"></a><a name="bkmk_comanage"></a>使用 Microsoft Intune 进行共同管理

共同管理是将现有 Configuration Manager 部署附加到 Microsoft 365 云的主要方式之一。 它使你能够使用 Configuration Manager 和 Microsoft Intune 同时管理 Windows 10 设备。 借助共同管理，可以通过添加新功能在 Configuration Manager 中云附加现有投资。

有关详细信息，请参阅[什么是共同管理？](../../comanage/overview.md)  

### <a name="microsoft-exchange"></a><a name="bkmk_exchange"></a> Microsoft Exchange  

此选项使用 Exchange Server 连接器将多个 Exchange 服务器连接到 Configuration Manager。 这可集中管理连接到 Exchange ActiveSync 的设备。 你可以在 Configuration Manager 控制台中配置 Exchange 移动设备管理功能。 示例功能包括针对多个 Exchange 服务器的远程设备擦除和设置控制。

有关详细信息，请参阅[使用 Configuration Manager 和 Exchange 管理移动设备](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)。  

### <a name="compare-solutions-by-supported-platforms"></a><a name="bkmk_comp1"></a> 按支持的平台比较解决方案  

|平台|Configuration Manager 客户端|本地 MDM|带 Exchange 的 Configuration Manager| Intune |
|--------|----------------------------|---------------|-----------------------------------|--------|
|Android| | |“是”| “是” |
|iOS| | |“是”| “是” |
|Mac OS X|“是”| |“是”| “是” |
|Windows 10|“是”|“是”|“是”| “是” |
|Windows 10 移动版| |“是”|“是”| “是” |
|Windows（以前版本）|“是”| |“是”|  |
|Windows Server|“是”| |“是”|  |
|Windows Embedded|“是”| | |  |

关于支持平台的完整列表，请参阅以下文章：

- [Configuration Manager 的客户端和设备支持的操作系统](configs/supported-operating-systems-for-clients-and-devices.md)
- [Intune 支持的配置](https://docs.microsoft.com/intune/supported-devices-browsers)

Microsoft 建议使用 Intune 来管理 Android、iOS 和 Windows 10 移动设备。 有关更多信息，请参阅[什么是 Microsoft Intune？](https://docs.microsoft.com/intune/what-is-intune)。

### <a name="compare-solutions-by-management-functionality"></a><a name="bkmk_comp2"></a>根据管理功能比较解决方案  

|管理功能|Configuration Manager 客户端|本地 MDM|带 Exchange 的 Configuration Manager|  
|--------|----------------------------|---------------|-----------------------------------|  
|基于证书的相互身份验证|“是”|“是”| |
|客户端安装|“是”| | |
|通过 Internet 提供的支持|“是”| | |
|发现|“是”| |“是”|
|硬件清单|“是”|“是”|“是”|
|软件清单|“是”| |“是”|
|设置|“是”|“是”|“是”|
|软件部署|“是”|“是”| |
|软件更新管理|“是”| | |
|OS 部署|“是”| | |
|通过 Configuration Manager 进行阻止|“是”|“是”| |
|通过 Exchange Server 和 Configuration Manager 进行隔离和阻止| | |“是”|
|远程擦除| |“是”|“是”|
