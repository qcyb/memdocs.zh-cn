---
title: 诊断和使用情况数据的常见问题解答
titleSuffix: Configuration Manager
description: 有关 Configuration Manager 的诊断和使用情况数据的常见问题
ms.date: 01/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3fe32aa2-d594-4ad0-a291-b8f5395ac50b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: eb14f909238e86a7aa4a87493b17a218a21f0909
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700191"
---
# <a name="frequently-asked-questions-about-diagnostics-and-usage-data"></a>有关诊断和使用情况数据的常见问题

适用范围：  Configuration Manager (Current Branch)

本文解答有关 Configuration Manager 中的诊断和使用情况数据的常见问题。

## <a name="can-i-turn-off-diagnostic-and-usage-data"></a><a name="bkmk_off"></a> 能否关闭诊断和使用情况数据？

为了帮助管理站点何时发送数据，请在脱机模式下使用服务连接点。 然后，使用服务连接工具手动发送数据。 有关详细信息，请参阅以下文章：

- [关于服务连接点](../../servers/deploy/configure/about-the-service-connection-point.md)
- [使用服务连接工具](../../servers/manage/use-the-service-connection-tool.md)

为了支持 Windows 10 的新版本和 Microsoft Intune 等云服务，需要定期更新 Configuration Manager 的当前分支。 Microsoft 需要至少基本级别的诊断和使用情况数据。 此数据用于使产品保持最新状态、改进更新体检以及提高产品的质量和安全性。

当服务连接点处于脱机模式时，没有数据发送到服务。 切换到联机模式或使用服务连接工具时，它会将数据发送到服务以检查更新。

你还可以选择 Configuration Manager 收集的数据级别。 有关详细信息，请参阅[诊断使用情况数据的级别](levels-overview.md)。

## <a name="what-is-the-data-retention-period"></a><a name="bkmk_retention"></a>数据保留期为多久？

Microsoft 将 Configuration Manager 诊断和使用情况数据存储一年。

## <a name="is-diagnostics-and-usage-data-sent-when-setup-runs"></a><a name="bkmk_update"></a> 安装程序运行时是否发送了诊断和使用情况数据？

不是。 仅当安装站点且可对其进行操作之后，才发送诊断和使用情况数据。

## <a name="how-frequently-is-the-data-sent"></a><a name="bkmk_frequency"></a>发送数据的频率为多少？

SQL 存储过程每七天（自安装站点之日起）运行一次。

- 在联机模式下，服务连接点在查询运行后上传数据。

- 在脱机模式下，使用服务连接工具上传数据。 （安装站点后的七天内，数据不可脱机使用。）  

## <a name="can-the-data-be-used-to-form-a-network-map"></a><a name="bkmk_network"></a>可否将数据用于形成网络映射？

不是。 此数据不包括任何网络详细信息，例如 IP 地址或详细的地理位置信息。 有关详细信息，请参阅[诊断使用情况数据的级别](levels-overview.md#bkmk_versions)，并找到有关你所用版本的更多详细信息。

数据包括每个站点的时区信息。 此信息使你能够深入了解层次结构中站点广泛的地理位置和全球分布。

## <a name="can-you-see-data-in-custom-sql-tables"></a><a name="bkmk_tables"></a> 你们可以看到自定义 SQL 表中的数据吗？

不是。 Configuration Manager 通过 SQL 存储过程收集诊断和使用情况数据。 这些存储过程针对数据库中的默认产品表运行。 所有这些 SQL 表的前缀都为“TEL_”****。 作为 SQL 架构检测查询的一部分，对所有表名称进行了哈希处理，以便与已知默认值进行比较。 此行为确定数据库中存在自定义表。 若存在自定义表，则 Microsoft 可知你已从默认架构扩展了数据库架构。 它不包含这些表中存储的任何数据。

## <a name="can-you-see-other-databases"></a><a name="bkmk_databases"></a> 你们可以看到其他数据库吗？

不是。 用于收集数据的存储过程仅限于 Configuration Manager 站点数据库。 Microsoft 无法看到其他数据库的名称或其他数据库中的数据。

## <a name="is-any-data-sent-to-other-integrated-cloud-services"></a><a name="bkmk_cloud"></a> 是否将任何数据发送到其他集成云服务？

是的，当你将这些服务与 Configuration Manager 集成时。 在与任何云服务交互的过程中，Configuration Manager 会将一些数据发送到该服务。 此数据特定于该云服务，不同于 Configuration Manager 诊断和使用情况数据。 有关与其他云服务交互时使用的特定数据的详细信息，请参阅该服务的文档。

例如，以下云服务是 Microsoft 终结点管理器的一部分：

- [桌面分析数据隐私](../../../desktop-analytics/privacy.md)
- [Intune 中的隐私和个人数据](/intune/protect/privacy-personal-data)
- [Windows Autopilot 要求](/windows/deployment/windows-autopilot/windows-autopilot-requirements)

## <a name="does-configuration-manager-collect-any-personal-data"></a><a name="bkmk_personal"></a> Configuration Manager 是否收集任何个人数据？

不是。 Configuration 不收集或传输任何个人数据或客户数据。 它是你直接部署、管理和操作的本地产品。 Microsoft 收集的诊断和使用情况数据用于改进未来版本的安装体验、质量和安全性。

有关 Configuration Manager 数据的详细信息，请参阅[诊断使用情况数据的级别](levels-overview.md)。