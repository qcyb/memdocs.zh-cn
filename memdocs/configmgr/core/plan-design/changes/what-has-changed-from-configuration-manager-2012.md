---
title: 相较于 2012 版本的更改
titleSuffix: Configuration Manager
description: 识别 Configuration Manger 中相较于 System Center 2012 Configuration Manager 的更改内容和新增功能。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3ae68fa6-8b30-45dd-9d12-50bb67cb4a9d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0cd49eac95d9789fd11ba2bf1ca01b68b236628d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704435"
---
# <a name="whats-changed-from-system-center-2012-configuration-manager"></a>自 System Center 2012 Configuration Manager 以来的更改内容

适用范围：  Configuration Manager (Current Branch)

Configuration Manager Current Branch 引入了自 System Center 2012 Configuration Manager 以来的重要更改。 本文确定了 Configuration Manager Current Branch 的原始基线版本 1511 中的显著更改和新增功能。 若要了解有关 Configuration Manager 最新更新中引入的更改，请参阅 [Configuration Manager 增量版本中的新增功能](whats-new-incremental-versions.md)。

> [!NOTE]
> 从版本 1910 开始，Configuration Manager 现在是 Microsoft Endpoint Manager 的一部分。 有关详细信息，请参阅 [Microsoft Endpoint Configuration Manager](whats-new-in-version-1910.md#bkmk_mem)。

2015 年 12 月发布的 Configuration Manager（版本 1511）是 Microsoft 发布的当前 Configuration Manager 产品的初始版本。 它通常被称为 Configuration Manager Current Branch。 Current Branch  表明此版本支持产品增量更新。 它还提供区分 Configuration Manager 此发布版本和早期版本的方法。  

Configuration Manager Current Branch：  

- 不在产品名称中使用年份或产品标识符，与 Configuration Manager 2007 或 System Center 2012 Configuration Manager 等旧版本不同。  

- 支持增量产品内更新，也称为更新版本。 初始版本是版本 1511。 一年发布几次作为控制台内更新的更高版本，如版本 1910。  

- 使用基线版本安装。 1511 是原始基线版本，而新的基线版本也会不定期发布，如 2002。 基线版本可用于安装新的 Configuration Manager 站点和层次结构，或从 System Center 2012 Configuration Manager 支持的版本升级。  

## <a name="in-console-updates"></a><a name="bkmk_updates"></a> 控制台内更新

Configuration Manager 使用称为“更新和服务”的控制台内服务方法，该方法可轻松找到并安装建议的更新  。  

某些版本仅可用作 Configuration Manager 控制台内对现有站点的更新。 不能使用这些更新来安装新的 Configuration Manager 站点。 例如，仅可从 Configuration Manager 控制台获取 1910 更新。 它用于更新已运行 Configuration Manager 受支持版本的站点。

我们还会定期发布更新版本作为新的基线版本  。 例如，更新版本 2002 也是基线版本。 使用基线版本安装新站点或层次结构。 不要从较旧的基线版本（如 1802）开始，而要升级到当前版本。 始终使用最新的基线。

有关详细信息，请参阅下列文章：

- [Configuration Manager 的更新](../../servers/manage/updates.md)
- [基准和更新版本](../../servers/manage/updates.md#bkmk_Baselines)

## <a name="service-connection-point"></a><a name="bkmk_servicepoint"></a>服务连接点  

Configuration Manager Current Branch 包含新的站点系统角色，即“服务连接点”  ：  

- 许多支持云的功能的联系点

- 下载站点的更新

- 将站点的诊断和使用情况数据上传到 Microsoft 云

此站点系统角色支持联机和脱机操作模式。 有关详细信息，请参阅[关于服务连接点](../../servers/deploy/configure/about-the-service-connection-point.md)。  

## <a name="diagnostics-and-usage-data"></a><a name="bkmk_usage"></a> 诊断和使用情况数据

Configuration Manager 收集站点和基础结构的诊断和使用情况数据。 编译此信息并通过服务连接点将其提交给 Microsoft 云服务。 Configuration Manager 需要此数据来下载适用于你的环境的更新。 设置服务连接点时，可以指定收集到的数据级别，以及是自动（联机）还是手动（脱机）提交数据。

有关详细信息，请参阅[诊断和使用情况数据](../diagnostics/diagnostics-and-usage-data.md)。  

## <a name="deprecated-functionality"></a><a name="bkmk_out"></a> 弃用的功能  

[对基于 Intel 主动管理技术 (AMT) 的计算机的本机支持](#bkmk_AMT)等一些功能从 Configuration Manager 控制台中删除。 网络访问保护等另一些功能遭完全删除。 此外，不再支持一些旧版 Microsoft 产品，如 Windows Vista、Windows Server 2008 和 SQL Server 2008。  

有关已弃用功能列表，请参阅[已删除项和已弃用项](deprecated/removed-and-deprecated.md)。  

若要详细了解受支持的产品、操作系统和配置，请参阅[受支持的配置](../configs/supported-configurations.md)。  

### <a name="support-for-intel-active-management-technology-amt"></a><a name="bkmk_AMT"></a> Intel 主动管理技术 (AMT) 的支持  

Configuration Manager Current Branch 已从 Configuration Manager 控制台中删除对基于 AMT 的计算机的本机支持。 使用[适用于 Microsoft Configuration Manager 的 Intel SCS 外接程序](https://www.intel.com/content/www/us/en/software/setup-configuration-software.html)时，基于 AMT 的计算机保持完全托管。 使用外接程序可以在 Configuration Manager 能够合并这些更改之前使用用于管理 AMT 的最新功能，同时删除引入的限制。  

带外管理随适用于 Configuration Manager 的集成 AMT 一起删除。 带外管理点站点系统角色不再可用。  

> [!Note]
> 此更改不会影响 System Center 2012 Configuration Manager 中的带外管理。

## <a name="changes-in-functionality"></a>功能中的更改

以下部分总结了 System Center 2012 R2 Configuration Manager 与版本 1511 的 Configuration Manager Current Branch 之间功能区域中的一些重大更改。 有关功能的最新更改的详细信息，请参阅[增量版本中的新增功能](whats-new-incremental-versions.md)。

### <a name="client-deployment"></a>客户端部署  

Configuration Manager 引入了新功能，用于在使用新软件升级站点的其余部分之前，测试 Configuration Manager 客户端的新版本。 可以设置在其中试验新客户端的预生产集合。 对预生产中的新客户端软件感到满意后，便能将客户端提升为使用新版本自动升级站点的其余部分。  

若要详细了解如何测试客户端，请参阅[如何在预生产集合中测试客户端升级](../../clients/manage/upgrade/test-client-upgrades.md)。  

### <a name="os-deployment"></a>OS 部署  

请注意以下 OS 部署变更：

- 在“创建任务序列向导”中，新增以下任务序列类型：通过升级包升级操作系统  。 它创建将计算机从 Windows 7 或 Windows 8.1 升级到 Windows 10 的步骤。 有关详细信息，请参阅[将 Windows 升级到最新版本](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md)。  

- 现在可以在部署操作系统时使用 Windows PE 对等缓存。 如果运行任务序列来部署 OS，计算机可使用 Windows PE 对等缓存从对等缓存源中获取内容，而无需从分发点下载内容。 此行为有助于最大限度减小没有本地分发点的分支机构方案中的 WAN 流量。 有关信息，请参阅[准备 Windows PE 对等缓存来减少 WAN 流量](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md)。  

- 现在可将 Windows 的状态作为环境中的一种服务进行查看。 还可以通过创建服务计划来形成部署环，并确保在新内部版本发布时 Windows 10 Current Branch 计算机为最新。 此外，还可以在对 Windows 10 客户端内部版本的支持即将结束时查看警报。 有关详细信息，请参阅[管理 Windows 即服务](../../../osd/deploy-use/manage-windows-as-a-service.md)。  

### <a name="application-management"></a>应用程序管理  

请注意对应用程序管理进行的以下更改：

- 借助 Configuration Manager，可以为运行 Windows 10 及更高版本的设备部署通用 Windows 平台 (UWP) 应用。 有关详细信息，请参阅[创建 Windows 应用](../../../apps/get-started/creating-windows-applications.md)。  

- 软件中心具有富有现代感的全新外观。 用户可用应用之前仅出现在应用目录中，现在出现在软件中心内的“应用”选项卡下。此行为让这些部署更易于被发现，并免去了用户参考单独的应用目录的麻烦。 此外，不再必须使用已启用 Silverlight 的浏览器了。 有关详细信息，请参阅[规划和配置应用程序管理](../../../apps/plan-design/plan-for-and-configure-application-management.md)。  

- 通过 MDM 的新 Windows Installer 安装程序类型让你可以创建基于 Windows Installer 的应用并将其部署到运行 Windows 10 的已注册 PC 上。 有关详细信息，请参阅[创建 Windows 应用](../../../apps/get-started/creating-windows-applications.md)。  

- 在 Configuration Manager 2012 中，若要在 Windows 应用商店中指定应用的链接，可以直接指定该链接，或者浏览到安装有该应用的远程计算机。 在 Configuration Manager Current Branch 中，虽仍能直接输入链接，但现在可以直接在 Configuration Manager 控制台中浏览应用商店以查找应用，而不用转到引用计算机。  

### <a name="software-updates"></a>软件更新  

请注意对软件更新进行的以下更改：

- Configuration Manager 现在可以为计算机检测软件更新管理方法差异。 具体而言，它可以区分连接到适用于企业的 Windows 更新 (WUfB) 的 Windows 10 计算机和连接到 WSUS 的计算机。 **UseWUServer** 属性为新属性，它指定了计算机是否由 WUfB 管理。 你可以在集合中使用此设置从软件更新管理中删除这些计算机。 有关详细信息，请参阅 [Integration with Windows Update for Business in Windows 10](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md)。  

- 现在可从 Configuration Manager 控制台计划和运行 WSUS 清理任务。 在“软件更新点组件”  属性中，如果你选择运行 WSUS 清理任务，它便会在下一次软件更新同步时运行。 过期的软件更新被设置为，在 WSUS 服务器上处于拒绝状态，计算机上的 Windows 更新代理不再扫描这些软件更新。 有关详细信息，请参阅 [Schedule and run the WSUS clean up task](../../../sum/deploy-use/software-updates-maintenance.md)。  

### <a name="compliance-settings"></a>符合性设置  

请注意对符合性设置进行的以下更改：

- Configuration Manager 改进了用于创建配置项目的工作流。 现在，当创建配置项目并选择受支持的平台时，只有与该平台相关的设置才可用。 请参阅[符合性设置入门](../../../compliance/get-started/get-started-with-compliance-settings.md)。  

- **创建配置项目**向导现在可以更轻松地选择你想要创建的配置项目类型。 此外，新的和更新的配置项目可用于：  

    - 使用 Configuration Manager 客户端管理的 Windows 10 设备  

    - 使用 Configuration Manager 客户端管理的 Mac OS X 设备  

    - 使用 Configuration Manager 客户端管理的 Windows 台式计算机和服务器计算机  

    - 未使用 Configuration Manager 客户端管理的 Windows 8.1 和 Windows 10 设备  

    有关详细信息，请参阅[如何创建配置项目](../../../compliance/deploy-use/create-configuration-items.md)。  

- 支持在 Mac OS X 计算机上管理设置，这些计算机不使用 Configuration Manager 客户端进行管理。

### <a name="on-premises-mobile-device-management"></a>本地移动设备管理  

现在可以使用本地 Configuration Manager 基础结构管理移动设备。 所有设备和管理数据都在本地处理，并且不属于 Microsoft Intune 或其他云服务。 此类设备管理不需要客户端软件。 Configuration Manager 使用设备 OS 内置的功能来管理设备。  

有关详细信息，请参阅[使用本地基础结构管理移动设备](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)。

## <a name="next-steps"></a>后续步骤

[增量版本中的新增功能](whats-new-incremental-versions.md)
