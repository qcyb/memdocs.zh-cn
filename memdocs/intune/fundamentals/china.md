---
title: Intune 由世纪互联在中国运营
titleSuffix: ''
description: Intune 由世纪互联在中国运营。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: ''
ms.reviewer: amsaeedi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: f82664cbc9f6970d494945cfdf6fc72e8d95ae8b
ms.sourcegitcommit: b90d51f7ce09750e024b97baf6950a87902a727c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86022341"
---
# <a name="intune-operated-by-21vianet-in-china"></a>Intune 由世纪互联在中国运营  

由世纪互联运营的 Intune 旨在满足在中国提供安全、可靠和可缩放的云服务的需求。 作为服务的 Intune 基于 Microsoft Azure 构建。 由世纪互联运营的 Microsoft Azure 是位于中国的独立云服务提供商。 它由世纪互联独立运营和交易。 该服务由 Microsoft 向世纪互联授权的技术提供支持。

Microsoft 不亲自参与该服务的运营。 由世纪互联运营、提供和管理该服务的交付。 世纪互联是中国一家互联网数据中心服务提供商。 它提供托管、托管网络服务和云计算基础结构服务。 世纪互联通过授权 Microsoft 技术来运营本地数据中心，使你能够在使用 Intune 服务的同时将你的数据保留在中国。 世纪互联还提供订阅、计费和支持服务。

[!INCLUDE [GDPR-related guidance](../includes/gdpr-dsr-and-stp-note.md)]

## <a name="feature-differences-in-intune-operated-by-21vianet"></a>由世纪互联运营的 Intune 中的功能差异

由于中国境内的服务由中国境内的合作伙伴运营，因此在 Intune 中存在一些功能差异。 

- 由世纪互联运营的 Intune 仅支持独立部署。 目前正在开发对 System Center Configuration Manager 中的共同管理的支持。
- 不支持从公有云迁移到主权云。 有兴趣迁移到由世纪互联运营的 Intune 的客户必须手动迁移。
- 目前不支持租户附加功能（无需注册即可将设备同步到 Intune 以支持云控制台方案）。
- 由世纪互联运营的 Intune 不支持 Intune 代理，因此不支持旧式电脑管理。
- 通过使用现代 MDM 渠道支持 Windows 10 的管理。
- 由世纪互联运营的 Intune 不支持本地 Exchange Connector。
- Windows Autopilot 和企业应用商店功能当前不可用。
- 由于 Google 移动服务在中国不可用，因此由世纪互联运营的 Intune 中的客户无法使用需要 Google 移动服务的功能。 这些功能包括：
  - Google Play 保护机制功能（如 SafetyNet 设备证明）。
  - 从 Google Play 商店管理应用。
  - Android Enterprise 功能。 有关详细信息，请参阅此 [Google 文档](https://support.google.com/work/android/answer/6270910?hl=en)。
- Android 版 Intune 公司门户应用使用 Google 移动服务与 Microsoft Intune 服务进行通信。 由于 Google Play 服务在中国不可用，因此某些任务最长可能需要 8 小时才能完成。 有关详细信息，请参阅此[文章](https://docs.microsoft.com/mem/intune/apps/manage-without-gms#limitations-of-intune-device-administrator-management-when-gms-is-unavailable)。 
- 为了遵守本地法规和提供改进的功能，Intune 客户端体验（公司门户应用）在中国可能有所不同。
- 隔离不可用。
- 移动应用管理 (MAM) 的可用性取决于这些应用在中华人民共和国的可用性。

## <a name="you-control-customer-data"></a>由你控制客户数据

在由世纪互联运营的 Microsoft Azure、Intune、Office 365 和 Power BI 中，你可以完全控制你的数据：
- 你知道客户数据的位置。
- 你可以控制对客户数据的访问。
- 如果离开服务，你可以控制客户数据。
- 你可以选择控制客户数据的安全性。

在由世纪互联运营的 Microsoft Azure、Intune、Office 365 和 Power BI 中，你是数据的所有者：
- 世纪互联不会将客户数据用于广告宣传。
- 你可以控制谁有权访问客户数据。
- 我们使用逻辑隔离来隔离每个客户的数据。
- 我们提供简单透明的数据使用策略，并获得独立审核。
- 我们的分包商受合同约束，必须合同满足我们的隐私要求。

## <a name="data-subject-requests"></a>数据主体请求

由世纪互联运营的 Intune 的租户管理员角色可以通过以下方式请求数据主体的数据：

- 使用 Azure Active Directory 管理中心，租户管理员可以从 Azure Active Directory 和相关服务中永久删除数据主体。 有关详细信息，请参阅 [Azure 数据主体请求 - 删除](https://docs.microsoft.com/microsoft-365/compliance/gdpr-dsr-azure?view=o365-worldwide#step-5-delete)
- 由世纪互联运营的 Microsoft 服务的系统生成的日志可以由租户管理员使用“数据日志导出”将其导出。 有关详细信息，请参阅 [Azure 数据主体请求 - 导出](https://docs.microsoft.com/microsoft-365/compliance/gdpr-dsr-azure?view=o365-worldwide#step-6-export)。

## <a name="next-steps"></a>后续步骤

[了解有关 Intune 支持的配置的详细信息](supported-devices-browsers.md)