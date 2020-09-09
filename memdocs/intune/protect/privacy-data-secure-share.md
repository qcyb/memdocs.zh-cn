---
title: Intune 中的数据安全性和数据共享
titleSuffix: Microsoft Intune
description: 了解 Intune 中如何保护和共享个人数据。
keywords: 隐私, 数据
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 09/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 68921fd6-5f50-456c-a3af-83d7bc4b134b
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 34e99a53165afdccd5ee9a2f3f190c78f673a507
ms.sourcegitcommit: 15450a1e92d9f67f74ae619ffe192c15948107c5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/08/2020
ms.locfileid: "89516250"
---
# <a name="data-security-and-sharing-in-intune"></a>Intune 中的数据安全性和数据共享


## <a name="data-security"></a>数据安全性

Microsoft Intune 是 Microsoft 企业移动性 + 安全性套件云服务产品的重要组成部分。 为了支持[数据管理策略](https://www.microsoft.com/en-us/TrustCenter/Security/default.aspx)，所有 Microsoft 云服务均采用 [Microsoft 隐私](https://www.microsoft.com/en-us/trustcenter/privacy)和 [Microsoft 安全性](https://www.microsoft.com/en-us/trustcenter/security/)方法进行开发。  

Microsoft Intune 与 Microsoft Azure 服务团队采用相同的技术和组织措施来抵御数据泄露进程。

有关详细信息，请参阅[服务信任门户](https://www.microsoft.com/en-us/TrustCenter/stp)。

### <a name="data-breach-reporting"></a>数据泄露报告

发现可报告客户安全事件 (CRSI) 时，客户会收到通知。 此过程包括与 Microsoft 365 团队合作，向使用 Intune 的任何 Microsoft 365 客户下达泄露通知。

## <a name="data-sharing"></a>数据共享

当租户管理员打开某些功能（如 Apple 设备注册计划）时，即表示管理员允许 Microsoft Intune 与相应的第三方共享数据。 在此情况下，Intune 可能与以下各方共享个人数据：

- 充当 Microsoft 代理的第三方。
- 不充当 Microsoft 代理的第三方（仅限租户管理员显式授予 Intune 执行此操作的权限时）。

作为 Microsoft 代理的所有第三方都包含在[联机服务分包商列表](https://aka.ms/Online_Serv_Subcontractor_List)中。

与此类实体共享数据是为了对客户和技术支持提供帮助，进行服务维护及其他操作。

租户与第三方签订的合同用于管理第三方服务中保留的 Intune 个人数据。 该合同还为 Intune 授予将数据传输到第三方服务的权限。  

有关与特定第三方共享的数据的信息，请参阅以下文章：
- [Intune 向 Apple 发送的数据](data-intune-sends-to-apple.md)
- [Intune 向 Google 发送的数据](data-intune-sends-to-google.md)
- [Apple 发送到 Intune 的数据](data-apple-sends-to-intune.md)
- [Google 发送到 Intune 的数据](data-google-sends-to-intune.md)
- [Jamf Pro 向 Intune 发送的数据](data-jamf-sends-to-intune.md)

### <a name="microsoft-endpoint-configuration-manager-data-sharing"></a>Microsoft Endpoint Configuration Manager 数据共享

Microsoft Intune 不与 Configuration Manager 共享任何数据。 Configuration Manager 是由客户直接部署、管理和运行的本地产品。 Configuration Manager 收集的诊断和使用情况数据仅用于改进将来版本的安装体验、质量和安全性。

有关详细信息，请参阅 [Configuration Manager 的诊断和使用情况数据](/configmgr/core/plan-design/diagnostics/diagnostics-and-usage-data)。 


## <a name="next-steps"></a>后续步骤

了解如何在 Intune 中[查看和更正](privacy-data-view-correct.md)个人数据。
