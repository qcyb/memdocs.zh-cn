---
title: 优化 Windows 10 更新传递
titleSuffix: Configuration Manager
description: 了解如何使用 Configuration Manager 管理更新内容以及时了解 Windows 10 动态。
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: b670cfaf-96a4-4fcb-9caa-0f2e8c2c6198
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 6c42015880cae09be48feff9c42b6b2a0d2c8544
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129308"
---
# <a name="optimize-windows-10-update-delivery-with-configuration-manager"></a>使用 Configuration Manager 优化 Windows 10 更新传递

适用范围：Configuration Manager (Current Branch)

对于许多客户而言，使用 Configuration Manager 获取且及时了解 Windows 10 月度更新的成功途径从良好的内容分发策略开始。 月度质量更新的大小可能是大型组织关心的一个原因。 某些技术旨在帮助降低带宽和网络负载以优化更新传递。 本文将介绍这些技术，对它们进行比较，并提供帮助你决定使用哪种技术的建议。  
 
Windows 10 提供了几种类型的更新。 有关详细信息，请参阅 [Windows Update for Business 中的更新类型](/windows/deployment/update/waas-manage-updates-wufb#types-of-updates-managed-by-windows-update-for-business)。 本文重点介绍 Windows 10 质量更新和 Configuration Manager。 


## <a name="express-update-delivery"></a>快速更新传递

Windows 10 质量更新下载文件可能很大。 每个包都包含以前发布的所有修复程序，以确保一致性和简单性。 Microsoft 已经能够通过名为“快速”的功能减少每个客户端下载的 Windows 10 更新内容的大小。 如今，数百万设备使用“快速”功能直接从 Windows 更新服务中拉取更新，并大大降低了下载文件大小。 对于未直接从 Windows 更新服务下载的客户端，客户也可以使用此优势。 

Configuration Manager 在版本 1702 中添加了对 Windows 10 质量更新的[快速安装文件](manage-express-installation-files-for-windows-10-updates.md)的支持。 但是，为获得最佳体验，建议使用 Configuration Manager 版本 1802 或更高版本。 为了获得最佳下载速度，还建议使用 Windows 10 版本 1703 或更高版本。 

> [!NOTE]  
> 快速版本内容比完整文件版本大得多。 快速安装文件包含要更新的每个文件的所有可能变体。 因此，在 Configuration Manager 中启用 快速支持时，更新包源和分发点上的更新所需的磁盘空间会增加。 即使分发点上的磁盘空间需求增加，客户端从这些分发点下载的内容大小也会减少。 客户端仅下载他们需要的位（增量），不会下载完整更新。


## <a name="peer-to-peer-content-distribution"></a>对等内容分发

即使客户端仅下载了所需内容的部分内容，也可以通过利用对等内容分发来加速环境中的 Windows 更新。 利用对等作为质量更新的下载源可能对远程办公室中不存在本地分发点的环境有益。 此行为避免了所有客户端跨慢速 WAN 链接从远程分发点下载内容的需要。 当客户端回退到 Windows 更新服务时，使用对等也很有用。 在将更新内容提供给其他设备之前，只需一个对等即可从云中下载更新内容。

Configuration Manager 支持许多对等技术，包括：
- Windows 传递优化
- Configuration Manager 对等缓存
- Windows BranchCache  

下一节将提供有关这些技术的更多信息。

### <a name="windows-delivery-optimization"></a>Windows 传递优化

[传递优化](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization)是 Windows 10 中内置的主要下载技术和对等分发方法。 Windows 10 客户端可以从下载相同更新的本地网络上的其他设备获取内容。 使用 [Windows 传递优化选项](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-reference#delivery-optimization-options)，你可以配置客户端以进行分组。 此分组允许组织标识可能满足对等请求的最佳候选设备。 传递优化显著降低了用于使设备保持最新的总体带宽，同时缩短了下载时间。

> [!NOTE]  
> 传递优化是一种云托管解决方案。 要利用其对等功能，需具有对传递优化云服务的 Internet 访问。 有关所需的 Internet 终结点的信息，请参阅[有关传递优化的常见问题](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions)。 

为获得最佳结果，你可能需要将传递优化[下载模式](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-reference#download-mode)设置为组 (2) 并定义组 ID。 在组模式下，对等可以跨属于同一组的设备之间的内部子网，包括远程办公室中的设备。 使用[组 ID 选项](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-reference#select-the-source-of-group-ids)创建独立于域和 AD DS 站点的自己的自定义组。 对于希望通过传递优化实现最佳带宽优化的大多数组织，建议使用组下载模式。

当客户端在不同网络中漫游时，手动配置这些组 ID 很有挑战性。 Configuration Manager 版本 1802 添加了一项新功能，即通过[将边界组与传递优化集成](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization)来简化此过程的管理。 当唤醒某个客户端后，它会与其管理点进行通信以获取策略，并提供其网络和边界组信息。 Configuration Manager 为每个边界组创建唯一 ID。 该站点使用客户端的位置信息，通过 Configuration Manager 边界 ID 自动配置客户端的传递优化组 ID。 当客户端漫游到其他边界组时，它会与其管理点进行通信，并使用新的边界组 ID 自动重新配置。 通过此集成，传递优化可以利用 Configuration Manager 边界组信息查找从中下载更新的对等。

### <a name="delivery-optimization-starting-in-version-1910"></a><a name="bkmk_DO-1910"></a>传递优化（从版本 1910 开始）
<!--4699118-->
自 Configuration Manager 版本 1910 起，可以为运行 Windows 10 版本 1709 或更高版本的客户端对分发的所有 Windows 更新内容（而不只是快速安装文件）使用传递优化。

若要对所有 Windows 更新安装文件使用传递优化，请启用以下[软件更新客户端设置](../../core/clients/deploy/about-client-settings.md#software-updates)：

- “在有可用内容时，允许客户端下载增量内容”设置为“是” 。
- “客户端用于接收增量内容请求的端口”设置为 8005（默认值）或自定义端口号。

> [!IMPORTANT]
> - 必须启用（默认情况）且不能绕过传递优化。 有关详细信息，请参阅 [Windows 传递优化参考](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-reference)。
> - 针对增量内容更改[软件更新客户端设置](../../core/clients/deploy/about-client-settings.md#software-updates)时，请验证[传递优化客户端设置](../../core/clients/deploy/about-client-settings.md#delivery-optimization)。
> - 如果 Office COM 已启用，则无法将传递优化用于 Microsoft 365 Apps 客户端更新。 Configuration Manager 使用 Office COM 来管理 Microsoft 365 Apps 客户端更新。 可以通过取消注册 Office COM 来允许将传递优化用于 Microsoft 365 Apps 更新。 在 Office COM 被禁用后，Microsoft 365 Apps 软件更新由默认 Office 自动更新 2.0 计划性任务进行管理。 也就是说，Configuration Manager 不会命令或监视 Microsoft 365 Apps 更新的安装过程。 Configuration Manager 会继续收集硬件清单中的信息，以便在控制台中填充 Office 365 客户端管理仪表板。 若要了解如何取消注册 Office COM，请参阅[启用 office 365 客户端以从 OFFICE CDN（而不是 Configuration Manager）接收更新](https://docs.microsoft.com/deployoffice/manage-office-365-proplus-updates-with-configuration-manager#enable-office-365-clients-to-receive-updates-from-the-office-cdn-instead-of-configuration-manager)。
> - 如果对内容存储使用 CMG，且[客户端设置](../../core/clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available)“下载增量内容(若有)”已启用，那么第三方更新的内容不会下载到客户端。 <!--6598587-->


### <a name="configuration-manager-peer-cache"></a>Configuration Manager 对等缓存

[对等缓存](../../core/plan-design/hierarchy/client-peer-cache.md)是 Configuration Manager 的一项功能，使客户端可以直接从其本地 Configuration Manager 缓存与其他客户端共享内容。 对等缓存不会取代 Windows BranchCache 等其他对等缓存解决方案的使用。 它可与其他解决方案结合使用，为扩展传统内容部署解决方案提供更丰富的方案，例如分发点。 对等缓存不依赖于 BranchCache。 即使未启用或使用 BranchCache，对等缓存仍能正常运行。

> [!NOTE]  
> 客户端只能下载来自其当前边界组中的对等缓存客户端中的内容。  


### <a name="windows-branchcache"></a>Windows BranchCache
[BranchCache](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache) 是 Windows 中的带宽优化技术。 每个客户端都具有缓存，并用作内容的备用源。 同一网络上的设备可以请求此内容。 [Configuration Manager 可以使用 BranchCache](../../core/plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache) 以允许对等方互相提供内容，而不必总是联系分发点。 使用 BranchCache，文件缓存在每个单独的客户端上，其他客户端可以根据需要检索它们。 这种方法分发缓存而不是进行单点检索。 此行为可节省大量带宽，同时减少客户端接收所请求内容的时间。



## <a name="selecting-the-right-peer-caching-technology"></a>选择正确的对等缓存技术

为快速安装文件选择正确的对等缓存技术取决于环境和要求。 尽管 Configuration Manager 支持上述所有对等技术，但应该使用对环境最有意义的技术。 对于大多数客户而言，假设客户端可以满足传递优化的 Interne 要求，使用传递优化的 Windows 10 内置对等缓存应该就足够了。 如果客户端无法满足这些 Internet 要求，请考虑使用 Configuration Manager 对等缓存功能。 如果当前正在将 BranchCache 与 Configuration Manager 一起使用并且该操作满足你的所有需求，那么使用具有 BranchCache 的快速文件可能是你的正确选择。 

### <a name="peer-cache-comparison-chart"></a>对等缓存比较图


| 功能  | 传递优化  | 对等缓存  | BranchCache  |
|---------|---------|---------|---------|
| 支持跨子网 | 是 | 是 | 否 |
| 带宽限制 | 是（本机） | 是（通过 BITS） | 是（通过 BITS） |
| 支持部分内容 | 是，适用于此列的下一行中列出的所有受支持的内容类型。 | 只适用于 Microsoft 365 Apps 和快速更新 | 是，适用于此列的下一行中列出的所有受支持的内容类型。 |
| 支持的内容类型 | **通过 ConfigMgr：** </br> -快速更新 </br> -所有 Windows 更新（自版本 1910 起）。 这不包括 Microsoft 365 Apps 更新。</br> </br> **通过 Microsoft 云：**</br> - Windows 和安全更新</br> - 驱动程序</br> - Windows 应用商店应用</br> - 适用于企业的 Windows 应用商店应用 | 所有 ConfigMgr 内容类型，包括在 [Windows PE](../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md) 中下载的映像 | 所有 ConfigMgr 内容类型，映像除外 |
| 控制磁盘上的缓存大小 | 是 | 是 | 是 |
| 发现对等源 | 自动 | 手动（客户端代理设置） | 自动 |
| 对等发现 | 通过传递优化云服务（需要 Internet 访问） | 通过管理点（基于客户端边界组） | 多播 |
| 报表 | 是（使用桌面分析） | ConfigMgr 客户端数据源仪表板 | ConfigMgr 客户端数据源仪表板 |
| WAN 使用控制 | 是（本机，可通过组策略设置控制） | 边界组 | 仅限子网支持 |
| 通过 ConfigMgr 管理 | 部分（客户端代理设置） | 是（客户端代理设置） | 是（客户端代理设置） |



## <a name="conclusion"></a>结论

Microsoft 建议根据需要使用带有快速安装文件和对等缓存技术的 Configuration Manager 优化 Windows 10 质量更新传递。 此方法应该可以解决与 Windows 10 设备下载大量内容以安装质量更新相关的挑战。 此外，还建议通过每月部署质量更新来使 Windows 10 设备保持最新。 这种做法减少了设备每月所需的质量更新内容的增量。 减少此内容增量会导致从分发点或对等源下载较少的内容。 

由于快速安装文件的性质，其内容比传统自包含文件大得多。 这会导致从 Windows 更新服务到 Configuration Manager 站点服务器的更新下载时间变长。 站点服务器和分发点所需的磁盘空间也会增加。 下载和分发质量更新所需的总时间可能会更长。 但是，在 Windows 10 设备下载和安装质量更新期间设备端优势应显而易见。 有关详细信息，请参阅[使用快速安装文件](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc708456(v=ws.10)?#using-express-installation-files)。

如果较大更新的服务器端权衡是采用快速支持的阻止程序，但设备端优势对你的业务和环境至关重要，Microsoft 建议通过 Configuration Manager 使用[适用于企业的 Windows 更新](integrate-windows-update-for-business-windows-10.md)。 适用于企业的 Windows 更新提供了快速更新的所有优势，无需在整个环境中下载、存储和分发快速安装文件。 客户端直接从 Windows 更新服务下载内容，因此仍可使用传递优化。



## <a name="frequently-asked-questions"></a><a name="bkmk_faq"></a>常见问题

#### <a name="how-do-windows-express-downloads-work-with-configuration-manager"></a>Windows 快速下载如何与 Configuration Manager 一起使用？

Windows 更新代理 (WUA) 首先请求快速内容。 如果无法安装快速更新，则可以回退到完整文件更新。  

1. Configuration Manager 客户端告知 WUA 下载更新内容。 当 WUA 发起快速下载时，它首先下载一个存根（例如，`Windows10.0-KB1234567-<platform>-express.cab`），该存根是快速包的一部分。  

2. WUA 将此存根传递给 Windows 更新安装程序 - 基于组件的服务 (CBS)。 CBS 使用存根来执行本地清单，将设备上文件的增量与获取所提供文件的最新版本所需的增量进行比较。  

3. 然后，CBS 要求 WUA 从一个或多个快速 .psf 文件下载所需的范围。  

4. 如果“传递优化”已启用，且发现对等节点具有所需的范围，那么客户端会独立于 ConfigMgr 客户端从对等节点下载这些范围。 如果“传递优化”已禁用，或没有对等节点具有所需的范围，那么 ConfigMgr 客户端会从本地分发点（或对等节点/Microsoft 更新）下载这些范围。 这些范围传递给 Windows 更新代理，这样 CBS 就可以使用它们来应用这些范围。


#### <a name="why-are-the-express-files-psf-so-large-when-stored-on-configuration-manager-peer-sources-in-the-ccmcache-folder"></a>为什么快速文件 (.psf) 存储在 ccmcache 文件夹的 Configuration Manager 对等源上时如此之大？

快速文件 (.psf) 是稀疏文件。 要确定文件在磁盘上实际使用的空间，请检查文件的“占用空间”属性。 “占用空间”属性应远小于大小值。  


#### <a name="does-configuration-manager-support-express-installation-files-with-windows-10-feature-updates"></a>Configuration Manager 是否支持使用 Windows 10 功能更新的快速安装文件？

不支持，Configuration Manager 当前仅支持使用 Windows 10 质量更新的快速安装文件。  


#### <a name="how-much-disk-space-is-needed-per-quality-update-on-the-site-server-and-distribution-points"></a>站点服务器和分发点上的每个质量更新需要占用多少磁盘空间？

视情况而定。 对于每个质量更新，更新的完整文件版本和快速版本都存储在服务器上。 Windows 10 质量更新是累积性的，因此这些文件的大小每个月都会增加。 计划每种语言每个更新至少为 5 GB。 


#### <a name="do-configuration-manager-clients-still-benefit-from-express-installation-files-when-falling-back-to-the-windows-update-service"></a>在回退到 Windows 更新服务后，Configuration Manager 客户端是否仍然可以从快速安装文件中受益？

是。 如果使用以下软件更新部署选项，则客户端在回退到云服务时仍会使用快速更新和传递优化：  

如果软件更新在当前、相邻或站点组中的分发点上不可用，请从 Microsoft 更新下载内容


#### <a name="why-is-express-file-content-not-downloaded-for-existing-updates-after-i-enable-express-file-support"></a>我启用快速文件支持后，为什么未下载现有更新的快速文件内容？ 

这些更改仅对启用支持后同步和部署的任何新更新生效。


#### <a name="is-there-any-way-to-see-how-much-content-is-downloaded-from-peers-using-delivery-optimization"></a>有没有办法查看使用传递优化从对等下载了多少内容？
Windows 10 版本 1703（及更高版本）包括两个新的 PowerShell cmdlet：Get-DeliveryOptimizationPerfSnap 和 Get-DeliveryOptimizationStatus。 这些 cmdlet 可以更深入地了解传递优化和缓存使用情况。 有关详细信息，请参阅[适用于 Windows 10 更新的传递优化](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#the-cloud-service-doesnt-see-other-peers-on-the-network)


#### <a name="how-do-clients-communicate-with-delivery-optimization-over-the-network"></a>客户端如何通过网络与传递优化进行通信？
有关防火墙的网络端口、代理要求和主机名的详细信息，请参阅[传递优化常见问题解答](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions)。

## <a name="log-files"></a>日志文件

使用以下日志文件监视增量下载：

- WUAHandler.log
- DeltaDownload.log

## <a name="next-steps"></a>后续步骤

- [部署软件更新](deploy-software-updates.md)
- [自动部署软件更新](automatically-deploy-software-updates.md)
