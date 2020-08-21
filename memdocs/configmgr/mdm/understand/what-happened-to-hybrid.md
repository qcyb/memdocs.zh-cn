---
title: 混合 MDM 发生了什么情况？
titleSuffix: Configuration Manager
description: 了解 (MDM) 的混合移动设备管理的弃用 Configuration Manager
ms.date: 12/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e9e0da6d-bd5a-48d9-930a-e74b34b9286c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 95ac4160895394eb075589ed18a317923f317b45
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695386"
---
# <a name="what-happened-to-hybrid-mdm"></a>混合 MDM 发生了什么情况？

适用范围：  Configuration Manager (Current Branch)

> [!WARNING]
> 从2019年9月1日起，Microsoft 停用了混合 MDM 服务产品/服务。 任何剩余的混合 MDM 设备都不会接收策略、应用或安全更新。

## <a name="remove-hybrid-mdm"></a>删除混合 MDM

如果 Configuration Manager 站点具有 Microsoft Intune 订阅，则需要将其删除。

1. 在 Configuration Manager 控制台中，转到“管理”工作区。 展开“云服务”****，然后选择“Microsoft Intune 订阅”**** 节点。 删除现有的 Intune 订阅。

1. 在 " **删除 Microsoft Intune 订阅" 向导**中，选择 " **从 Configuration Manager 中删除 Microsoft Intune 订阅**" 选项，然后单击 " **下一步**"。

1. 完成向导。

## <a name="deprecation-announcement"></a>弃用公告

下面是原始弃用公告：

> [!NOTE]  
> 截至 2018 年 8 月 14 日，混合移动设备管理已是一项[弃用功能](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)。 自 1902 Intune 服务版本起，预计在 2019 年 2 月底，新客户便无法新建混合连接。
> <!--Intune feature 2683117-->  
> 自从一年多前在 Azure 上推出以来，Intune 已经增加了数百个客户要求和市场领先的新服务功能。 Intune 现在提供的功能远远超过了混合移动设备管理 (MDM)。 Azure 上的 Intune 为你的企业移动需求提供了更深入集成的简化管理体验。
>
> 因此，大多数客户选择 Azure 上的 Intune 而不是混合 MDM。 随着越来越多的客户迁移到云，使用混合 MDM 的客户数量持续减少。 因此，Microsoft 将在 2019 年 9 月 1 日停用混合 MDM 服务产品。
>
> 此更改不会影响本地 Configuration Manager 或[适用于 Windows 10 设备的共同管理](../../comanage/overview.md)。 如果不确定是否使用混合 MDM，请进入 Configuration Manager 控制台的 " **管理** " 工作区，展开 " **云服务**"，然后选择 " **Microsoft Intune 订阅**"。 如果设置了 Microsoft Intune 订阅，那么你的租户已针对混合 MDM 进行了配置。
>
> **这会对我产生哪些影响？**
>
> - Microsoft 将在明年支持使用混合 MDM。 该功能将继续接收主要 bug 修复。 Microsoft 将支持新版本操作系统上的现有功能，例如在 iOS 12 上注册。 将不再为混合 MDM 提供新功能。  
>
> - 如果在混合 MDM 产品/服务结束之前迁移到 Azure 上的 Intune，则不会对最终用户产生任何影响。  
>
> - 2019 年 9 月 1 日，任何剩余的混合 MDM 设备将不再接收策略、应用或安全更新。  
>
> - 许可将保持不变。 混合 MDM 中随附 Azure 上的 Intune 许可证。  
>
> - Configuration Manager 中的本地 MDM 功能不会弃用。 从 Configuration Manager 版本1810开始，你可以在不使用 Intune 连接的情况下使用本地 MDM。 有关详细信息，请参阅 [新的本地 MDM 部署不再需要 Intune 连接](../../core/plan-design/changes/whats-new-in-version-1810.md#bkmk_opmdm)。
>
> - 混合 MDM 还弃用了 Configuration Manager 的本地条件访问功能。 如果对使用 Configuration Manager 客户端管理的设备使用条件访问，请在迁移之前确保它们受到保护。
>     1. 在 Azure 中设置条件性访问策略
>     2. 在 Intune 门户中设置合规性策略
>     3. 完成混合迁移，并将 MDM 机构设置为 Intune
>     4. 启用共同管理
>     5. 将合规性策略共同管理工作负荷转移到 Intune
>
>     有关详细信息，请参阅[启用共同管理的条件访问](../../comanage/quickstart-conditional-access.md)。
>
> **我需要如何准备应对此项变化？**
>
> - 开始为 MDM 规划从 ConfigMgr 控制台迁移到 Azure。 包括 Microsoft IT 在内的许多客户都执行了这一迁移过程。 有关详细信息，请参阅 [Microsoft 案例研究](https://aka.ms/Intune_MSFT)。  
>
> - 请联系你的名义伙伴或 FastTrack 以获取帮助。 [适用于 Microsoft 365 的 FastTrack](https://aka.ms/hybrid_fasttrack) 可以帮助你从混合 MDM 迁移到 Azure 上的 Intune。
>
> 有关详细信息，请参阅 [Intune 支持博客文章](https://aka.ms/hybrid_notification)。

## <a name="next-steps"></a>后续步骤

有关支持的管理 MDM 设备功能的详细信息，请参阅以下文章：

- [什么是 Microsoft Intune？](/intune/what-is-intune)
- [什么是本地 MDM？](manage-mobile-devices-with-on-premises-infrastructure.md)
- [使用 Exchange 管理设备](../deploy-use/manage-mobile-devices-with-exchange-activesync.md)