---
title: 管理客户端
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中管理客户端。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3986a992-c175-4b6f-922e-fc561e3d7cb7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2d7697f8b5a2017aa732c52512bf31598c070fbc
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696075"
---
# <a name="how-to-manage-clients-in-configuration-manager"></a>如何在 Configuration Manager 中管理客户端

适用范围：  Configuration Manager (Current Branch)

在设备上安装 Configuration Manager 客户端并将其成功分配到站点后，你将在“设备”  节点的“资产和符合性”  工作区中看到设备，并在“设备集合”  节点中看到一个或多个集合。 选择设备或集合，然后运行管理操作。 但是，也可以使用其他方式来管理客户端，其中可能涉及控制台中的其他工作区或控制台未涉及的任务。  

> [!NOTE]  
> 如果已安装 Configuration Manager 客户端但尚未成功分配到站点，则该客户端可能不会显示在控制台中。 在客户端分配到站点后，更新集合成员身份，然后刷新控制台视图。  
>
> 在未安装 Configuration Manager 客户端时，设备也可能显示在控制台中。 如果站点发现了设备，但未安装和分配客户端，则可能发生此情况。
>
> 通过 [Exchange Server 连接器](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)或[本地 MDM](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) 管理的移动设备不会安装 Configuration Manager 客户端。  
>
> 若要从控制台管理设备，请使用“设备”节点中的“客户端”列来确定是否安装了客户端   。  

## <a name="manage-clients-from-the-devices-node"></a><a name="BKMK_ManagingClients_DevicesNode"></a> 通过“设备”节点管理客户端   

根据设备类型，其中某些选项可能不可用。  

1. 在 Configuration Manager 控制台中，转到“资产和符合性”工作区，并选择“设备”节点   。  

2. 选择一台或多台设备，然后从功能区中选择以下其中一个客户端管理任务。 还可以右键单击该设备。）  

### <a name="import-user-device-affinity"></a>导入用户设备相关性

配置用户和设备之间的关联，以便高效地向用户部署软件。  

有关详细信息，请参阅[将用户和设备与用户设备相关性进行链接](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)。

### <a name="import-computer-information"></a>导入计算机信息

启动导入计算机信息向导，将新计算机信息导入 Configuration Manager 数据库  。 可使用文件导入多台计算机，或指定单台计算机的信息。

### <a name="add-selected-items"></a>添加所选项

提供下列选项：

- **将所选项目添加到现有设备集合**：打开“选择集合”  对话框。 选择要向其添加此设备的集合。 使用“直接”成员身份规则可将该设备包括在此集合中  。  

- **将所选项目添加到新的设备集合**：将打开“创建设备集合向导”，可以在其中创建新的集合  。 使用“直接”成员身份规则可将所选集合包括在此集合中  。  

有关详细信息，请参阅[如何创建集合](collections/create-collections.md)。

### <a name="install-client"></a>安装客户端

将打开“安装客户端向导”  。 此向导使用客户端请求安装在所选设备上安装或重新安装 Configuration Manager 客户端。

> [!TIP]  
> 可通过多种不同的方式来安装 Configuration Manager 客户端。 尽管客户端请求向导提供一种通过控制台实现的便捷客户端安装方法，但此方法有许多依赖关系，并且并非适合所有环境。 有关依赖关系的详细信息，请参阅[将客户端部署到 Windows 计算机的先决条件](../deploy/prerequisites-for-deploying-clients-to-windows-computers.md#client-push-installation)。 有关其他客户端安装方法的详细信息，请参阅[客户端安装方法](../deploy/plan/client-installation-methods.md)。

有关详细信息，请参阅[如何使用客户端请求安装 Configuration Manager 客户端](../deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush)。

### <a name="run-script"></a>运行脚本

打开“运行脚本”向导，在所选设备上运行 PowerShell 脚本  。

有关详细信息，请参阅[创建和运行 PowerShell 脚本](../../../apps/deploy-use/create-deploy-scripts.md)。

### <a name="install-application"></a>安装应用程序

在设备上实时安装应用程序。 此功能有助于减少对每个应用程序的单独集合的需求。

有关详细信息，请参阅[为设备安装应用程序](../../../apps/deploy-use/install-app-for-device.md)。

### <a name="reassign-site"></a>重新分配站点

将一个或多个客户端（包括被管理的移动设备）重新分配到层次结构中的另一个主站点。 可逐个重新分配客户端，也可以选择多个客户端以进行批量重新分配。  

### <a name="client-settings---resultant-client-settings"></a>客户端设置 - 生成的客户端设置

如果已将多个客户端设置部署到同一设备，则设置的优先顺序和组合会很复杂。 使用此选项查看部署到此设备的生成的客户端设置集合。

有关详细信息，请参阅[如何配置客户端设置](../deploy/configure-client-settings.md)。

### <a name="start"></a>启动

- 运行资源浏览器，从 Windows 客户端查看硬件和软件清单信息  。 有关详细信息，请参阅下列文章：

  - [如何使用资源浏览器来查看硬件清单](inventory/use-resource-explorer-to-view-hardware-inventory.md)

  - [如何使用资源浏览器来查看软件清单](inventory/use-resource-explorer-to-view-software-inventory.md)

- 使用远程控制、远程协助或远程桌面客户端对设备进行远程管理    。 有关详细信息，请参阅[如何远程管理 Windows 客户端计算机](remote-control/remotely-administer-a-windows-client-computer.md)。

### <a name="approve"></a>批准

客户端使用 HTTP 和自签名证书与站点系统通信时，必须批准这些客户端以将其标识为受信任计算机。 默认情况下，站点配置会自动批准同一 Active Directory 林和受信任林中的客户端。 此默认行为意味着不必手动批准每个客户端。 手动批准你信任的工作组计算机，以及你信任但未获批准的任何其他计算机。

> [!IMPORTANT]  
> 尽管某些管理功能可能适合于未批准的客户端，但 Configuration Manager 不支持这种情况。  

不必批准始终使用 HTTPS 与站点系统通信的客户端，或在通过 HTTP 与站点系统通信时使用 PKI 证书的客户端。 这些客户端通过使用 PKI 证书建立信任。

### <a name="block-or-unblock"></a>阻止或解除阻止

阻止不再受信任的客户端。 阻止操作可以阻止客户端接收策略，阻止站点系统与客户端进行通信。  

> [!IMPORTANT]  
> 阻止客户端的操作只会阻止从客户端到 Configuration Manager 站点系统的通信， 不会阻止与其他设备的通信。 客户端通过使用 HTTP（而不是 HTTPS）与站点系统通信时，还有一些安全限制。  

也可以取消阻止已阻止的客户端。

有关详细信息，请参阅[确定是否阻止客户端](../deploy/plan/determine-whether-to-block-clients.md)。

<!-- Change Category is a hybrid action -->

### <a name="clear-required-pxe-deployments"></a>清除所需的 PXE 部署

通过清除分配给 Configuration Manager 集合或计算机的上一个 PXE 部署的状态，可以重新部署所需的 PXE 部署。 此操作将重置该部署的状态并重新安装最新的所需部署。

有关详细信息，请参阅[使用 PXE 通过网络部署 Windows](../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md)。

### <a name="client-notification"></a>客户端通知

有关详细信息，请参阅[客户端通知](client-notification.md#client-notification)。

### <a name="endpoint-protection"></a>Endpoint Protection

有关详细信息，请参阅[客户端通知](client-notification.md#endpoint-protection)。

### <a name="edit-primary-users"></a>编辑主要用户

查看此设备在过去 90 天内的用户，或指定此设备的主要用户。

有关详细信息，请参阅[将用户和设备与用户设备相关性进行链接](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)。

### <a name="wipe-a-mobile-device"></a>擦除移动设备

你可以擦除支持擦除命令的移动设备。 此操作会永久删除移动设备上的所有数据，包括个人设置和个人数据。 通常，此操作会将移动设备重置回出厂默认值。 在移动设备不再受信任时将其擦除。 例如设备丢失或被盗的情况。  

> [!TIP]  
> 请检查制造商的文档以了解有关移动设备如何处理远程擦除命令的详细信息。  

移动设备收到擦除命令之前通常会有延迟：  

- 如果移动设备是通过 Configuration Manager 注册的，则客户端会在下载客户端策略时收到命令。

- 如果通过 Exchange Server 连接器管理移动设备，则移动设备会在其与 Exchange 同步时收到命令。  

若要监视设备何时收到擦除命令，可使用“擦除状态”列  。 设备将擦除确认发送到 Configuration Manager 之前，可以取消擦除命令。  

### <a name="retire-a-mobile-device"></a>停用移动设备

只有本地 MDM 注册的移动设备才支持“停用”选项  。  

有关详细信息，请参阅[使用远程擦除、远程锁定或密码重置功能帮助保护数据](../../../mdm/deploy-use/wipe-lock-reset-devices.md)。

### <a name="change-ownership"></a>更改所有权

如果设备未加入域并且未安装 Configuration Manager 客户端，则可以使用此选项将所有权更改为“公司”或“个人”   。  

可在应用程序要求中使用此值来控制部署，以及控制从用户设备中收集的清单数量。  

可能需要右键单击任意列标题并选择“设备所有者”  列，将此列添加到视图中。

### <a name="delete"></a>删除

> [!WARNING]  
> 如果要卸载 Configuration Manager 客户端或将其从集合中移除，请不要删除客户端。  

“删除”操作会从 Configuration Manager 数据库中手动删除客户端记录  。 仅使用此操作来解决问题。 如果删除了对象，但是依然安装了客户端并与站点进行通信，检测信号发现会重新创建客户端记录。 客户端记录会重新出现在 Configuration Manager 控制台中，然而客户端历史记录和以前的所有关联都会丢失。  
> [!NOTE]  
> 删除 Configuration Manager 注册的移动设备客户端时，此操作还会撤销颁发的 PKI 证书。 即使 IIS 不检查证书吊销列表 (CRL)，管理点也会拒绝此证书。
>
> 在删除这些客户端时，不会吊销移动设备旧客户端上的证书。

要卸载客户端，请参阅[卸载 Configuration Manager 客户端](#BKMK_UninstalClient)。  

要将客户端分配到新的主站点，请参阅[如何将客户端分配到站点](../deploy/assign-clients-to-a-site.md)。

要从集合中删除客户端，请重新配置集合属性。 有关详细信息，请参阅[如何管理集合](collections/manage-collections.md)。

### <a name="refresh"></a>刷新

用数据库中的最新数据刷新控制台视图。 例如，设备显示在发现列表中，但未显示为已安装。 安装客户端并确保将其分配给站点后，请选择“刷新”  。

### <a name="properties"></a>属性

查看发现数据和针对客户端的部署。

也可以配置任务序列用于将 OS 部署到设备的变量。 有关详细信息，请参阅[为设备和集合创建任务序列变量](../../../osd/understand/using-task-sequence-variables.md#bkmk_set-coll-var)。


## <a name="manage-clients-from-the-device-collections-node"></a><a name="BKMK_ManagingClients_DeviceCollectionsNode"></a> 通过“设备集合”节点管理客户端 

许多在“设备”  节点中的设备上可用的任务在集合上也可用。 控制台会将操作自动应用于集合中的所有合格设备。 此操作对整个集合生成附加的网络数据包，并提高站点服务器上的 CPU 使用率。  

在运行集合级别任务之前，请考虑以下问题。 开始后则无法从控制台停止任务。

- 集合中有多少设备？
- 是否通过低带宽网络连接进行设备连接？
- 在所有设备上完成此任务需要多少时间？

有关详细信息，请参阅[如何管理集合](collections/manage-collections.md)。


## <a name="restart-clients"></a>重新启动客户端

使用 Configuration Manager 控制台来标识需要重启的客户端。 然后使用客户端通知操作进行重启。

> [!Tip]
> 启用自动客户端升级，以更轻松的方式使客户端保持最新状态。 有关详细信息，请参阅[关于自动客户端升级](upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate)。

若要标识正在等待重启的设备，请转到 Configuration Manager 控制台中的“资产和符合性”  工作区，并选择“设备”  节点。 然后可以在名为“等待重启”  的新列的详细信息窗格中查看每个设备的状态。 每个设备都具有以下一个或多个值：

- **No**：没有正在等待的重启
- **Configuration Manager**：此值源于客户端重新启动处理协调器组件 (RebootCoordinator.log)
- **File rename**：此值源于 Windows 报告挂起的文件重命名操作 (HKLM\SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations)
- **Windows Update**：此值源于 Windows 更新代理报告由于一个或多个更新而需要挂起的重启 (HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired)
- **Add or remove feature**：此值源于 Windows 基于组件的服务报告由于添加或删除一种 Windows 功能而需要重启 (HKLM\Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\Reboot Pending)

### <a name="create-the-client-notification-to-restart-a-device"></a>创建要重启设备的客户端通知

1. 在控制台的“设备集合”节点，选择集合中要重启的设备  。
2. 在功能区中，选择“客户端通知”，然后选择“重启”   。 会打开一个有关重启的信息窗口。 选择“确定”确认重启请求  。

当客户端收到通知时，将打开“软件中心”  通知窗口以通知用户重启。 默认情况下，重启会在 90 分钟后发生。 可以通过配置[客户端设置](../deploy/configure-client-settings.md)来修改重启时间。 重启行为的设置可在默认设置的[“计算机重启”](../deploy/about-client-settings.md#computer-restart)选项卡上找到。


## <a name="configure-the-client-cache"></a><a name="BKMK_ClientCache"></a> 配置客户端缓存

客户端缓存会存储客户端安装应用程序和程序时的临时文件。 软件更新也使用客户端缓存，但始终尝试在不考虑大小设置的情况下将内容下载到缓存中。 可以在手动安装客户端时、使用客户端请求安装时或在安装之后配置客户端缓存设置，例如大小和位置。

可使用 Configuration Manager 控制台中的客户端设置来指定缓存文件夹的大小。 有关详细信息，请参阅[客户端缓存设置](../deploy/about-client-settings.md#client-cache-settings)。

Configuration Manager 客户端缓存的默认位置为 `%windir%\ccmcache`，默认磁盘空间为 5120 MB。  

> [!IMPORTANT]  
> 不要对用于客户端缓存的文件夹进行加密。 Configuration Manager 无法将内容下载到加密的文件夹。  

### <a name="about-the-client-cache"></a>关于客户端缓存  

Configuration Manager 客户端会在接收部署之后立即下载所需软件的内容，但会等到部署计划时间之后才会运行。 在计划的时间，Configuration Manager 客户端将检查以确定缓存中是否有内容。 如果内容位于缓存中且版本正确，则客户端会使用该缓存内容。 如果内容的所需版本发生了更改或者客户端已将内容删除以便为另一个包腾出空间，客户端则会将内容再次下载到缓存。  

如果客户端尝试下载的程序或应用程序内容大小超出缓存的大小，则部署将因缓存大小不足而失败。 客户端会生成缓存大小不足的状态消息 10050。 如果稍后增加了缓存大小，则会出现以下结果：  

- 对于所需程序：客户端不会自动重试下载内容。 将包和程序重新部署到客户端。  
- 对于所需应用程序：客户端会在下载其客户端策略时自动重试下载内容。  

如果客户端尝试下载的包小于缓存大小，但缓存已满，则所有必需的部署将一直重试，直到满足以下条件为止  ：

- 缓存空间可用
- 下载超时
- 重试次数达到限制

如果稍后增加了缓存大小，则客户端将尝试在下一次重试间隔期间再次下载该包。 客户端将每隔四小时尝试下载内容一次，直至尝试 18 次为止。  

系统不会自动删除缓存内容。 在客户端使用缓存内容后，该内容至少在缓存中保留一天。 如果将包属性配置为包含将内容保留在客户端缓存中的选项，则客户端不会自动将其删除。 如果缓存空间由最近 24 小时内下载的包占用，并且客户端必须下载新包，则可以增加缓存大小，或选择选项以删除保留的缓存内容。  

使用以下过程在手动客户端安装过程中或在安装客户端之后配置客户端缓存。  

### <a name="configure-the-cache-during-manual-client-installation"></a>在客户端手动安装过程中配置缓存  

从安装源位置运行 CCMSetup.exe 命令，并指定所需的以下属性，用空格分隔：  

- DISABLECACHEOPT  

  - SMSCACHEDIR  

  - SMSCACHEFLAGS  

  - SMSCACHESIZE  

    > [!NOTE]
    > 请使用 Configuration Manager 控制台中“客户端设置”的可用缓存大小设置，而不是 SMSCACHESIZE  。 有关详细信息，请参阅[客户端缓存设置](../deploy/about-client-settings.md#client-cache-settings)。

有关如何使用 CCMSetup.exe 的这些命令行属性的详细信息，请参阅[关于客户端安装属性](../deploy/about-client-installation-properties.md)。

### <a name="configure-the-cache-during-client-push-installation"></a>在客户端请求安装过程中配置缓存  

1. 在 Configuration Manager 控制台中，转到“管理”  工作区，展开“站点配置”  ，然后选择“站点”  节点。  

2. 选择适当的站点。 在功能区的“主页”选项卡上的“设置”组中，依次选择“客户端安装设置”、“客户端请求安装”     。 切换到“安装属性”选项卡  。  

3. 指定以下属性，并使用空格分隔：  

   - DISABLECACHEOPT  

   - SMSCACHEDIR  

   - SMSCACHEFLAGS  

   - SMSCACHESIZE  

     > [!NOTE]
     > 请使用 Configuration Manager 控制台中“客户端设置”的可用缓存大小设置，而不是 SMSCACHESIZE  。 有关详细信息，请参阅[客户端缓存设置](../deploy/about-client-settings.md#client-cache-settings)。

     有关如何使用 CCMSetup.exe 的这些命令行属性的详细信息，请参阅[关于客户端安装属性](../deploy/about-client-installation-properties.md)。  

### <a name="configure-the-cache-on-the-client-computer"></a>配置客户端计算机上的缓存  

1. 在客户端计算机上，打开“Configuration Manager”控制面板  。  

2. 切换到“缓存”选项卡  。设置空间和位置属性。 默认位置为 `%windir%\ccmcache`。  

3. 若要删除缓存文件夹中的文件，请选择“删除文件”  。  

### <a name="configure-client-cache-size-in-client-settings"></a>在客户端设置中配置客户端缓存大小

在无需重新安装客户端的情况下调整客户端缓存的大小。 请使用 Configuration Manager 控制台中“客户端设置”的可用缓存大小设置  。 有关详细信息，请参阅[客户端缓存设置](../deploy/about-client-settings.md#client-cache-settings)。


## <a name="uninstall-the-client"></a><a name="BKMK_UninstalClient"></a> 卸载客户端

可通过将 CCMSetup.exe 与 /Uninstall 属性一起使用从计算机卸载 Configuration Manager 客户端软件   。 在单独的计算机上从命令提示符运行 CCMSetup.exe，或部署包以便为计算机集合卸载客户端。  

> [!NOTE]  
> 无法从移动设备中卸载 Configuration Manager 客户端。 如果必须从移动设备中删除 Configuration Manager 客户端，则必须擦除设备，从而删除移动设备上的所有数据。  

1. 以管理员身份打开 Windows 命令提示符。 将文件夹更改到 CCMSetup.exe 所在的位置，如 `cd %windir%\ccmsetup`

2. 运行以下命令：`CCMSetup.exe /uninstall`

> [!TIP]  
> 卸载过程不会在屏幕上显示结果。 要验证客户端是否已成功卸载，请查看以下日志文件：`%windir%\ccmsetup\logs\CCMSetup.log`  
>
> 如果需要等待卸载过程完成，才能执行其他操作，请在 PowerShell 中运行 `Wait-Process CCMSetup`。 此命令可以暂停脚本，直到 CCMSetup 过程完成。


## <a name="manage-conflicting-records"></a><a name="BKMK_ConflictingRecords"></a> 管理冲突的记录

Configuration Manager 使用硬件标识符来尝试标识可能重复的客户端，并发出有关冲突的记录的警报。 例如，如果重新安装计算机，则硬件标识符将相同，但 Configuration Manager 使用的 GUID 可能已更改。  

通过 Configuration Manager，可以使用计算机帐户的 Windows 身份验证或来自受信任来源的 PKI 证书自动解决冲突。 如果 Configuration Manager 无法解决重复硬件标识符冲突，则由层次结构设置决定行为。

### <a name="change-the-hierarchy-setting-for-managing-conflicting-records"></a>更改用于管理冲突记录的层次结构设置  

1. 在 Configuration Manager 控制台中，转到“管理”  工作区，展开“站点配置”  ，然后选择“站点”  节点。

1. 在功能区中，选择“层次结构设置”  。

1. 切换到“客户端批准和冲突的记录”选项卡，并选择下列选项之一  ：

    - 自动解决冲突的记录 
    - 手动解决冲突的记录 

### <a name="manually-resolve-conflicting-records"></a>手动解决冲突的记录  

1. 在 Configuration Manager 控制台中，转到“监视”工作区，展开“系统状态”，然后选择“冲突的记录”节点    。  

1. 选择一个或多个冲突的记录，然后选择“冲突的记录”  。  

1. 选择下列选项之一：  

    - 合并  ：合并新检测到的记录和现有客户端记录。  

    - 新建  ：为冲突的客户端记录创建新记录。  

    - **阻止**：为冲突的客户端记录创建新记录，但将其标记为已阻止。  


## <a name="manage-duplicate-hardware-identifiers"></a>管理重复的硬件标识符

可以提供 Configuration Manager 为实现 PXE 启动和客户端注册，而忽略的硬件标识符列表。 此列表可帮助解决两个常见问题：

1. 许多新设备不包括板载以太网端口。 为部署 OS，技术人员会使用 USB 转以太网适配器来建立有线连接。 出于成本和一般可用性的考虑，这些适配器通常会共享使用。 站点使用此适配器的 MAC 地址来标识设备。 因此，如果每次部署之间没有其他管理员操作，则重复使用适配器的操作会出现问题。 若要重复使用此方案中的适配器，请排除其 MAC 地址。

2. SMBIOS 属性应唯一，某些特殊硬件设备具有重复标识符。 排除此重复标识符，并依赖于每个设备的唯一 MAC 地址。

通过以下过程，添加 Configuration Manager 要忽略的硬件标识符：

1. 在 Configuration Manager 控制台中，转到“管理”  工作区，展开“站点配置”  ，然后选择“站点”  节点。

2. 在功能区“主页”选项卡的“站点”组中，选择“层次结构设置”    。

3. 切换到“客户端批准和冲突的记录”选项卡  。若要添加新的硬件标识符，在“复制硬件标识符”部分中选择“添加”   。

> [!TIP]
> 自版本 1910 开始，使用以下 PowerShell cmdlet 自动管理重复的硬件标识符：<!-- 4852819 -->
>
> - New-CMDuplicateHardwareIdGuid
> - Remove-CMDuplicateHardwareIdGuid
> - New-CMDuplicateHardwareIdMacAddress
> - Remove-CMDuplicateHardwareIdMacAddress


## <a name="start-policy-retrieval"></a><a name="BKMK_PolicyRetrieval"></a> 启动策略检索

Configuration Manager 客户端按配置为客户端设置的计划下载其客户端策略。 还可以从客户端启动按需策略检索。 例如，用于故障排除或测试的情况。  

- [客户端通知](#bkmk_policy-notify)
- [客户端控制面板](#bkmk_policy-manual)
- [支持中心](#bkmk_policy-support)
- [脚本](#bkmk_policy-script)

### <a name="start-client-policy-retrieval-with-client-notification"></a><a name="bkmk_policy-notify"></a> 通过客户端通知启动客户端策略检索  

1. 在 Configuration Manager 控制台中，转到“资产和符合性”工作区，并选择“设备”   。  

1. 选择要下载策略的设备。 在功能区“主页”选项卡上的“设备”组中，选择“客户端通知”，然后选择“下载计算机策略”     。  

    > [!NOTE]  
    > 还可以使用客户端通知来为集合中的所有设备启动策略检索。  

### <a name="start-client-policy-retrieval-from-the-configuration-manager-client-control-panel"></a><a name="bkmk_policy-manual"></a> 从 Configuration Manager 客户端控制面板中启动客户端策略检索

1. 打开计算机上的“Configuration Manager”控制面板  。  

2. 切换到“操作”选项卡  。选择“计算机策略检索和评估周期”以启动计算机策略，然后选择“立即运行”   。  

3. 选择“确定”，确认提示  。  

4. 对任何其他操作，重复前面的步骤。 例如，对用户客户端设置，选择“用户策略检索和评估周期”  。  

### <a name="start-client-policy-retrieval-with-support-center"></a><a name="bkmk_policy-support"></a> 通过支持中心启动客户端策略检索

使用支持中心来请求和查看客户端策略。 有关详细信息，请参阅[支持中心参考](../../support/support-center-ui-reference.md#bkmk_support-policy)。

### <a name="start-client-policy-retrieval-by-script"></a><a name="bkmk_policy-script"></a> 使用脚本启动客户端策略检索  

1. 打开脚本编辑器，如记事本或 Windows PowerShell ISE。  

2. 复制以下示例 PowerShell 代码并将其插入<!-- SCCMDocs#1591 --> 到文件中：  

    ```PowerShell
    $trigger = "{00000000-0000-0000-0000-000000000021}"
    Invoke-WmiMethod -Namespace root\ccm -Class sms_client -Name TriggerSchedule $trigger
    ```  

    > [!TIP]
    > 有关计划 ID 的详细信息，请参阅[消息 ID](../../support/send-schedule-tool.md#bkmk_sendschedule-guids)。

3. 以 .ps1 扩展名保存文件。  

4. 在客户端上运行脚本。
