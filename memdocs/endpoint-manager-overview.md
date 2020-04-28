---
title: Microsoft Endpoint Manager 概述 - Azure | Microsoft Docs
description: Endpoint Manager 包括 Intune、Configuration Manager、共同管理、桌面分析、Windows Autopilot 和管理中心，用户可以使用这些功能管理所有设备，包括本地设备。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/23/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: ''
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 939224776199407abb6a508f25bf5dadbacb882f
ms.sourcegitcommit: 795e8a6aca41e1a0690b3d0d55ba3862f8a683e7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/24/2020
ms.locfileid: "82135984"
---
# <a name="microsoft-endpoint-manager-overview"></a>Microsoft Endpoint Manager 概述

Microsoft Endpoint Manager 有助于提供现代工作场所和新式管理，用于确保数据安全，无论是在云端还是本地环境都是如此。 Endpoint Manager 包含一系列服务和工具，可用于管理和监视移动设备、桌面计算机、虚拟机、嵌入式设备和服务器。

Endpoint Manager 结合了你可能已知并已在使用的服务，包括 Microsoft Intune、Configuration Manager、桌面分析、共同管理和 Windows Autopilot。 这些服务是 Microsoft 365 堆栈的一部分，有助于确保访问安全、保护数据，以及应对和管理风险。

首先观看以下 Microsoft 365 公司副总裁 Brad Anderson 发布的两分钟视频：

> [!VIDEO https://www.youtube.com/embed/GS7oNPInFuw]

## <a name="what-you-get"></a>提供的服务

Endpoint Manager 包括以下服务：

- Microsoft Intune  ：Intune 是适用于应用和设备的完全基于云的移动设备管理 (MDM) 和移动应用管理 (MAM) 提供程序。 使用它，用户可以控制 Android、Android Enterprise、iOS/iPadOS、macOS 和 Windows 10 设备上的功能和设置。 它可与其他服务集成，包括 Azure Active Directory (AD)、移动威胁防御程序、ADMX 模板、Win32 和自定义 LOB 应用等。

  如果你有本地基础结构（如 Exchange 或 Active Directory），还可以使用 Intune 连接器：

  - 适用于 Active Directory 的 Intune 连接器  将条目添加到使用 Windows Autopilot 注册的计算机的本地 Active Directory 域中。 有关详细信息，请参阅[部署已加入混合 Azure AD 的设备](/mem/intune/enrollment/windows-autopilot-hybrid)。
  - 如果设备已在 Intune 中注册并符合你的策略要求，则 Intune Exchange 连接器  允许（或阻止）设备访问 Exchange 服务器。 有关详细信息，请参阅[设置本地 Intune Exchange 连接器](/mem/intune/protect/exchange-connector-install)。
  - Intune 证书连接器  处理来自使用证书进行身份验证和 S/MIME 电子邮件加密的设备的证书请求。 有关详细信息，请参阅[使用证书进行身份验证](/mem/intune/protect/certificates-configure)。

  作为 Endpoint Manager 的一部分，使用 Intune 创建和检查合规性，并使用云将应用、功能和设置部署到设备。

  有关详细信息，请参阅[什么是 Microsoft Intune](https://docs.microsoft.com/intune/fundamentals/what-is-intune)。

- **Configuration Manager**：Configuration Manager 是一种本地管理解决方案，用于管理网络上的或基于 Internet 的台式机、服务器和笔记本电脑。 可以在云中启用它，以便与 Intune、Azure AD、Microsoft Defender ATP 和其他云服务集成。 使用 Configuration Manager 可以部署应用、软件更新和操作系统。 还可以监视合规性，实时查询客户端并对其进行操作，还可以执行更多操作。

  作为 Endpoint Manager 的一部分，继续像往常一样使用 Configuration Manager。 如果已准备好将某些任务移至云中，请考虑使用[共同管理](https://docs.microsoft.com/configmgr/comanage/)。

  有关详细信息，请参阅[什么是 Configuration Manager？](https://docs.microsoft.com/configmgr/core/understand/introduction)。

-  共同管理：共同管理使用 Intune 和其他 Microsoft 365 云服务将你现有的本地 Configuration Manager 投入与云结合起来。 可以选择将 Configuration Manager 或 Intune 作为七个不同工作负荷组的管理机构。

  作为 Endpoint Manager 的一部分，共同管理使用云功能，包括条件访问。 可以将一些任务保留在本地，同时在云中使用 Intune 运行其他任务。

  有关详细信息，请参阅[什么是共同管理？](https://docs.microsoft.com/configmgr/comanage/overview)

-  桌面分析：桌面分析是一项基于云的服务，可与 Configuration Manager 集成。 它为你提供见解和情报，让你可以就 Windows 客户端的更新就绪情况做出更明智的决定。 此服务将组织中的数据与从数百万台连接到 Microsoft 云的设备中聚合得到的数据进行组合。 它提供有关组织中的安全更新、应用和设备的信息，并确定与应用和驱动程序之间的兼容性问题。 将最有可能为整个组织的资产提供最佳见解的设备作为试点。

  作为 Endpoint Manager 的一部分，使用云助力的桌面分析见解使 Windows 10 设备保持最新状态。

  有关详细信息，请参阅[什么是桌面分析？](https://docs.microsoft.com/configmgr/desktop-analytics/overview)。

-  Windows Autopilot：Windows Autopilot 设置并预先配置新设备，使其可供使用。 它旨在为 IT 和最终用户简化 Windows 设备的生命周期流程，即从初始部署到生命周期结束。

  作为 Endpoint Manager 的一部分，使用 Autopilot 预先配置设备，并自动在 Intune 中注册设备。 还可以将 Autopilot 与 Configuration Manager 集成在一起，并进行共同管理，实现更复杂的设备配置（处于预览状态）。

  有关详细信息，请参阅 [Windows Autopilot 概述](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot)和[在 Intune 中注册 Windows 设备](/mem/intune/enrollment/enrollment-autopilot)。

-  Azure AD Premium：Endpoint Manager 将 Azure AD 用于设备、用户、组、动态组、自动注册、多重身份验证和条件访问。 这些功能是保护设备、应用和数据的关键所在。

  有关详细信息，请参阅[添加用户](/mem/intune/fundamentals/users-add)、[设置自动注册](/mem/intune/enrollment/windows-enroll)和[关于条件访问](/mem/intune/protect/conditional-access)。

- Endpoint Manager 管理中心  ：[管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)是一个一站式网站，用于创建策略和管理设备。 它嵌入了其他关键设备管理服务，包括组、安全性、条件访问和报告。 此管理中心还显示由 Configuration Manager 和 Intune 管理的设备（处于预览状态）。

## <a name="choose-whats-right-for-you"></a>选择适合的服务

有几种方法可以确定适合组织的服务。 后续步骤取决于组织执行的操作。 请考虑要实现的目标。

例如：

- 如果持续预配新设备，可以先使用 Windows Autopilot。
- 如果为用户、应用和设备添加规则和控制设置，那就从 Intune 开始吧。
- 如果目前使用 Configuration Manager 来部署应用，并希望根据安全要求使用条件访问，则从使用共同管理开始。
- 如果目前使用的是 Configuration Manager，并负责使 Windows 10 设备保持最新状态，可以先使用桌面分析。
- 如果你刚开始使用 MDM 和 MAM，或者使用 ADMX 模板来控制 Office、Microsoft Edge 和 Windows 设置，那就从 Intune 开始吧。

也可以从三个方面使用 Endpoint Manager：云、本地以及云 + 本地：

- 云  ：所有数据都存储在 Azure 中。 并且没有数据中心。 这种方法提供了云的移动性优势，以及 Azure 的安全优势。

- 本地  ：如果你有一个包含 Configuration Manager 的本地基础架构；或者还没有准备好使用云，那么可以保留现有系统。

- 云 + 本地  ：许多环境混合在一起，并使用云附加方法。 这意味着结合使用云和本地。 对于新设备，请使用 Intune 的优势功能来访问和保护数据。 如果使用 Configuration Manager，请连接到云以获取其他功能和分析。 如果要将一些工作负载迁移到云中，那么共同管理是一个不错的选择。

## <a name="what-you-need-to-get-started"></a>入门所需操作

如果你目前使用 Configuration Manager，则还需要使用 Microsoft Intune 来共同管理 Windows 设备。 对于其他平台，例如 iOS/iPadOS 和 Android，则需要单独的 Intune 许可证。

在大多数情况下，Microsoft 365 可能是最理想的选择，因为它提供了 Endpoint Manager 和 Office 365。

有关详细信息，请参阅 [Microsoft 365](https://www.microsoft.com/licensing/product-licensing/microsoft-365-enterprise)。

## <a name="next-steps"></a>后续步骤

[利用云智能的强大功能简化和加速 IT 以及向现代工作场所的转变](https://www.microsoft.com/microsoft-365/blog/2019/11/04/use-the-power-of-cloud-intelligence-to-simplify-and-accelerate-it-and-the-move-to-a-modern-workplace/)

[Microsoft Endpoint Manager](https://www.microsoft.com/microsoft-365/microsoft-endpoint-manager)

[教程：Microsoft Endpoint Manager 中的 Intune 演练](/intune/fundamentals/tutorial-walkthrough-endpoint-manager)

[什么是 Microsoft 365？了解模块](https://docs.microsoft.com/learn/modules/what-is-m365/index)
