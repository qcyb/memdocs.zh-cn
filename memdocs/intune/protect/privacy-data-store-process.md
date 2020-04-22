---
title: Intune 中的数据存储和处理
titleSuffix: Microsoft Intune
description: 了解如何在 Intune 中存储和处理个人数据。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/18/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: edb07842-6a16-482e-8c1d-541a29e169a8
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 525389e2f1cec207389bc37816ea4fc5399c99b4
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "79351391"
---
# <a name="data-storage-and-processing-in-intune"></a>Intune 中的数据存储和处理

Intune [收集数据](privacy-data-collect.md)后，将执行数据存储和处理，详情如下。

## <a name="storing-personal-data"></a>存储个人数据

收集的所有非遥测数据都通过 Intune 服务进行处理，并存储在以下一个或多个存储位置中： 

- SQLAzure 
- 可靠集合 (Service Fabric)  
- Azure 存储 

遥测数据（服务日志、性能日志、错误等）对于监视和提供稳定服务有关键作用，将发送到 Microsoft 的遥测数据存储中。

### <a name="storage-locations"></a>存储位置

Microsoft 在全球许多地区提供和运营 Intune 服务。 Intune 遵从客户数据管理员做出的存储位置选择。

有关详细信息，请参阅[数据位于何处？](https://www.microsoft.com/trust-center/privacy/data-location)

### <a name="personal-data-retention"></a>个人数据保留

一般情况下，Intune 将保留个人数据，直到将用户从 Intune 管理中删除 30 天后。

在 Intune 使用过程中收集到的遥测数据最多保留 30 天。

审核日志最多保留一年。

## <a name="processing-personal-data"></a>处理个人数据

Intune 使用 ISO 认证系统处理个人数据。 有关详细信息，请参阅[服务信任门户](https://www.microsoft.com/en-us/TrustCenter/stp)。

### <a name="profiling-and-marketing"></a>分析和营销

Microsoft Intune 不会将提供服务期间收集到的任何个人数据用于分析或营销目的。 

### <a name="restrict-processing-of-personal-data"></a>限制处理个人数据

若要对处理用户个人数据进行限制，可按以下方式删除用户帐户：
1. 导出用户个人数据的电子副本，包括
    - 帐户
    - 服务数据
    - 关联日志
2. 从 Intune 中删除用户帐户和关联数据。

## <a name="next-steps"></a>后续步骤

详细了解 Intune 如何[保护和共享](privacy-data-secure-share.md)个人数据。 
