---
title: 通过网络将 PXE 用于 OSD
titleSuffix: Configuration Manager
description: 使用启动了 PXE 的操作系统部署来刷新计算机的操作系统或在新计算机上安装新版本的 Windows。
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: da5f8b61-2386-4530-ad54-1a5c51911f07
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7d2d467a053689edad1dcf62fa9bb140d5f259d9
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124612"
---
# <a name="use-pxe-to-deploy-windows-over-the-network-with-configuration-manager"></a>使用 PXE 和 Configuration Manager 通过网络部署 Windows

适用范围：  Configuration Manager (Current Branch)

如果 Configuration Manager 中的 OS 部署启动了预启动执行环境 (PXE)，则客户端可通过网络发出请求和部署操作系统。 对于这种部署方法，你将 OS 映像和启动映像发送到已启用 PXE 的分发点。

> [!NOTE]
> 当创建一个仅针对 x64 BIOS 计算机的 OS 部署时，x64 启动映像和 x86 启动映像都必须在分发点上可用。

可以在以下方案中使用启动了 PXE 的 OS 部署：

- [使用新版的 Windows 刷新现有的计算机](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [在新计算机（裸机）上安装新版的 Windows](install-new-windows-version-new-computer-bare-metal.md)

完成其中一个 OS 部署方案中的步骤，然后使用本文中的内容来准备启动了 PXE 的部署。

> [!WARNING]
> 如果使用 PXE 部署，并在配置设备硬件时将网络适配器作为第一个启动设备，则这些设备可以自动启动 OS 部署任务序列而无需用户交互。 [部署验证](../../core/servers/manage/settings-to-manage-high-risk-deployments.md)不会管理此配置。 尽管此配置可以简化流程并减少用户交互，但它会增加设备意外重置映像的风险。

自版本 2006 起，基于 PXE 的任务序列可以下载基于云的内容。 已启用 PXE 的分发点仍需要启动映像，并且设备需要与管理点建立 Intranet 连接。 然后，它可以从已启用内容的云管理网关 (CMG) 或云分发点获取其他内容。<!--6209223--> 有关详细信息，请参阅[支持基于云的内容](use-bootable-media-to-deploy-windows-over-the-network.md#support-for-cloud-based-content)。

## <a name="configure-distribution-points-for-pxe"></a><a name="BKMK_Configure"></a> 为分发点配置 PXE

要将操作系统部署到发出 PXE 启动请求的 Configuration Manager 客户端，请配置一个或多个分发点以接受 PXE 请求。 然后，此分发点会响应 PXE 启动请求，并确定适当的部署操作。 有关详细信息，请参阅[安装或修改分发点](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe)。

> [!NOTE]
> 当你配置一个已启用 PXE 的分发点来支持多个子网时，不支持使用 DHCP 选项。 若要允许网络将客户端 PXE 请求转发到已启用 PXE 的分发点，请在路由器上配置 IP 帮助程序。

在版本 1810 中，不支持在同时运行 DHCP 服务器的服务器上使用不含 WDS 的 PXE 响应程序。

自版本 1902 起，如果你对分发点启用不含 Windows 部署服务的 PXE 响应程序，它现在与 DHCP 服务位于同一服务器上。<!--3734270, SCCMDocs-pr #3416--> 添加以下设置以支持此配置：

- 将以下注册表项中的 DWord 值 DoNotListenOnDhcpPort 设置为 `1`：`HKLM\Software\Microsoft\SMS\DP` 。
- 将 DHCP 选项 60 设置为 `PXEClient`。
- 重启服务器上的 SCCMPXE 和 DHCP 服务。

## <a name="prepare-a-pxe-enabled-boot-image"></a>准备 PXE 启用的启动映像

若要使用 PXE 来部署 OS，请将已启用 PXE 的 x86 和 x64 启动映像同时分发到一个或多个已启用 PXE 的分发点。

- 要在启动映像上启用 PXE，请从启动映像属性中的“数据源”  选项卡中，选择“从已启用 PXE 的分发点部署此启动映像”  。

- 在更改启动映像的属性后，请更新启动映像，并将它再分发到分发点。 有关详细信息，请参阅[分发内容](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)。

## <a name="manage-duplicate-hardware-identifiers"></a>管理重复的硬件标识符

如果有多台计算机具有重复的 SMBIOS 属性或使用的是共享的网络适配器，Configuration Manager 可能会将它们识别为同一个设备。 请通过管理层次结构设置中的重复硬件标识符来缓解这些问题。 有关详细信息，请参阅[管理重复硬件标识符](../../core/clients/manage/manage-clients.md#manage-duplicate-hardware-identifiers)。

## <a name="create-an-exclusion-list-for-pxe-deployments"></a><a name="BKMK_PXEExclusionList"></a> 创建 PXE 部署的排除列表

> [!NOTE]
> 在某些情况下，[管理重复硬件标识符](../../core/clients/manage/manage-clients.md#manage-duplicate-hardware-identifiers)的过程可能更方便。<!-- SCCMDocs issue 802 -->
>
> 在一些场景中，每个行为可能会导致不同的结果。 排除列表无论如何也不会启动列出了 MAC 地址的客户端。
>
> 重复的 ID 列表不会使用 MAC 地址查找客户端的任务序列策略。 如果它与 SMBIOS ID 匹配，或者如果存在未知计算机的任务序列策略，则仍会启动客户端。

使用 PXE 部署操作系统时，可以在每个分发点上创建一个排除列表。 将 MAC 地址添加到你希望分发点忽略的计算机的排除列表中。 列出的计算机将不接收 Configuration Manager 用于 PXE 部署的部署任务序列。

1. 在已启用 PXE 的分发点上，创建一个文本文件。 例如，将此文件命名为 pxeExceptions.txt。

1. 使用纯文本编辑器（如记事本）来编辑此文件。 添加已启用 PXE 的分发点应忽略的计算机的 MAC 地址。 用冒号分隔 MAC 地址值，每行输入一个地址。 例如：`01:23:45:67:89:ab`

1. 在已启用 PXE 的分发点上，保存此文本文件。 可以将它保存到服务器上的任何位置。

1. 在已启用 PXE 的分发点上，编辑注册表。 转到以下注册表路径：`HKLM\Software\Microsoft\SMS\DP`。 创建 MACIgnoreListFile 字符串值。 在已启用 PXE 的分发点上，添加此文本文件的完整路径。

    > [!WARNING]
    > 如果不正确地使用注册表编辑器，可能会导致也许需要你重新安装 Windows 的严重问题。 Microsoft 不保证能够解决因注册表编辑器使用不当而导致的问题。 你自行承担使用注册表编辑器的风险。

1. 在进行此注册表更改后，请重启 WDS 服务或 PXE 响应者服务。 无需重启服务器。<!--512129-->

## <a name="ramdisk-tftp-block-size-and-window-size"></a><a name="BKMK_RamDiskTFTP"></a> RamDisk TFTP 块大小和窗口大小

可以为启用 PXE 的分发点自定义 RamDisk TFTP 块大小和窗口大小。 如果已自定义网络，较大的块或窗口可能会导致启动映像下载由于超时错误而失败。 通过 RamDisk TFTP 块大小和窗口大小自定义，可以在使用 PXE 时优化 TFTP 流量，以满足特定网络要求。 若要确定最高效的设置，请在环境中测试自定义设置。 有关详细信息，请参阅[在启用 PXE 的分发点上自定义 RamDisk TFTP 块大小和窗口大小](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP)。

## <a name="configure-deployment-settings"></a>配置部署设置

若要使用启动了 PXE 的 OS 部署，必须配置该部署以使 OS 对 PXE 启动请求可用。 在部署属性中的“部署设置”选项卡上配置可用的操作系统  。 对于“可用于以下项目”  设置，请选择以下选项之一：

- Configuration Manager 客户端、媒体和 PXE

- 仅媒体和 PXE

- 仅媒体和 PXE（隐藏）

## <a name="option-82-during-pxe-dhcp-handshake"></a>在 PXE DHCP 握手期间使用选项 82

自版本 1906 起，Configuration Manager 在使用没有 WDS 的 PXE 响应者进行 PXE DHCP 握手期间支持选项 82。 如果需要选项 82，请务必使用没有 WDS 的 PXE 响应者。 Configuration Manager 不支持将选项 82 用于 WDS。

## <a name="deploy-the-task-sequence"></a><a name="BKMK_Deploy"></a> 部署任务序列

将 OS 部署到目标集合。 有关详细信息，请参阅 [Deploy a task sequence](deploy-a-task-sequence.md)。 当使用 PXE 部署操作系统时，你可以将部署配置为必需或可用。

- **所需部署**：所需的部署使用 PXE，无需任何用户干预。 用户无法绕过 PXE 启动。 但是，如果用户在分发点响应之前取消 PXE 启动，则不会部署 OS。

- **可用部署**：可用部署要求用户在目标计算机旁。 用户必须按 F12 键继续执行 PXE 启动过程  。 如果由于用户不在场而未按 F12，则计算机将启动到当前 OS，或者将从下一个可用启动设备启动计算机  。

通过清除分配给 Configuration Manager 集合或计算机的上一个 PXE 部署的状态，可以重新部署所需的 PXE 部署。 有关清除所需的 PXE 部署  操作的详细信息，请参阅[管理客户端](../../core/clients/manage/manage-clients.md#BKMK_ManagingClients_DevicesNode)或[管理集合](../../core/clients/manage/collections/manage-collections.md#bkmk_device)。 此操作将重置该部署的状态并重新安装最新的所需部署。

> [!IMPORTANT]
> PXE 协议不安全。 请确保 PXE 服务器和 PXE 客户端位于物理上安全的网络（如数据中心）内，以防对站点进行未经授权的访问。

## <a name="how-the-boot-image-is-selected-for-pxe"></a>如何为 PXE 选择启动映像

当客户端通过 PXE 启动时，Configuration Manager 会提供一个启动映像给该客户端使用。 Configuration Manager 使用体系结构精确匹配的启动映像。 如果没有可用的体系结构精确匹配的启动映像，则 Configuration Manager 会使用具有兼容体系结构的启动映像。

以下列表详细介绍了如何为通过 PXE 启动的客户端选择启动映像：  

1. Configuration Manager 会在站点数据库中查找与尝试启动的客户端的 MAC 地址或 SMBIOS 相匹配的系统记录。  

    > [!NOTE]  
    > 如果分配到站点的计算机启动了另一站点的 PXE，则策略对该计算机不可见。 例如，如果已将客户端分配到站点 A，则站点 B 的管理点和分发点将不能从站点 A 访问策略，且客户端无法成功进行 PXE 启动。  

2. Configuration Manager 会查找部署到步骤 1 中找到的系统记录中的任务序列。  

3. 在步骤 2 中找到的任务序列列表中，Configuration Manager 会查找与尝试启动的客户端体系结构相匹配的启动映像。 如果找到具有相同体系结构的启动映像，则会使用该启动映像。  

    如果发现多个启动映像，则会使用排名位置最高或最新的任务序列部署 ID  。 如果是多站点层次结构，排名位置较高  字母的站点将优先列入该字符串比较。 例如，如果它们同时匹配，则会选择站点 ZZZ 中的一年期部署，而不是站点 AAA 中昨天的部署。<!-- SCCMDocs issue 877 -->  

4. 如果找不到具有相同体系结构的启动映像，Configuration Manager 会查找与客户端体系结构兼容的启动映像。 它查找在步骤 2 中发现的任务序列列表。 例如，64 位 BIOS/MBR 客户端与 32 位和 64 位启动映像兼容。 32 位 BIOS/MBR 客户端仅与 32 位启动映像兼容。 UEFI 客户端仅与匹配的体系结构兼容。 64 位的 UEFI 客户端仅与 64 位的启动映像兼容，而 32 位的 UEFI 客户端仅与 32 位的启动映像兼容。

## <a name="next-steps"></a>后续步骤

[有关操作系统部署的用户体验](../understand/user-experience.md#pxe)
