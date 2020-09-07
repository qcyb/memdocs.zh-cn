---
title: 无需设备管理的 Exchange
titleSuffix: Microsoft Intune
description: 使用 Microsoft Intune 为员工提供访问其 Microsoft 365 Exchange Online 电子邮件的权限，而无需设置设备管理系统。
keywords: Microsoft 365 Exchange 电子邮件访问权限
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/31/2017
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.topic: archived
ms.technology: ''
ms.assetid: 88a0d3b9-2622-403b-8374-1396afd8066e
ms.reviewer: pchacon
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8491d716751a4d370003583059546f17b689657e
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88996123"
---
# <a name="protect-microsoft-365-exchange-online-without-requiring-device-management"></a>无需设备管理即可保护 Microsoft 365 Exchange Online

可以向员工提供对其工作电子邮件的访问权限，而无需设置设备管理系统。 可通过 Intune 提供对 Microsoft 365 Exchange Online 的访问权限。 为了完成必要步骤，请确认你拥有 Microsoft 365 或 Azure Active Directory Premium 和 Intune 的许可证。 员工需要拥有[受支持的 iOS/iPadOS 或 Android 设备](../fundamentals/supported-devices-browsers.md)。 

如果决定设置设备管理系统，也可以进行设置。 这种类型的应用保护独立于设备管理。 

## <a name="action-plan"></a>操作计划

1. [了解条件访问](conditional-access.md)。 
2. [了解基于应用的条件访问](app-based-conditional-access-intune.md)。
3. [创建用于 Exchange Online 的基于应用的条件访问策略](app-based-conditional-access-intune-create.md)。
4. [阻止无法管理的应用](app-modern-authentication-block.md)，尤其是未使用 Azure Active Directory 身份验证库 (ADAL) 或 Microsoft 身份验证库 (MSAL) 的应用。
5. （可选）[创建用于 SharePoint Online 的基于应用的条件访问策略](app-based-conditional-access-intune-create.md)。 这些策略会阻止通过无法管理和保护的应用访问公司数据。 这些策略还会限制通过 SharePoint 移动应用进行访问。 

## <a name="what-to-tell-employees-and-students"></a>应告知员工和学生的事项

* 要求员工和学生从 Apple App Store 下载并安装适用于 iOS/iPadOS 的 Microsoft Outlook 或 Microsoft SharePoint，或者从 Google Play 商店下载适用于 Android 的 Microsoft Outlook 或 Microsoft SharePoint。 
* 如果阻止访问未使用新式验证的应用，请告知员工和学生此限制。 

## <a name="next-steps"></a>后续步骤

你已使用基于应用的条件访问来提高公司数据的安全性。 在后续步骤中，可详细了解增强公司数据保护的其他方式，包括： 

* [在 Active Directory 和 Azure Active Directory 中创建基于设备合规性、设备风险、位置和用户属性的条件访问](/azure/active-directory/active-directory-conditional-access-azure-portal)。  
* 设置应用保护策略，帮助防止出现有意或无意的公司数据泄露。 
* 利用 Azure 信息保护来保护网络外部的公司数据。 

需要有关启用此方案或者其他 EMS 或 Microsoft 365 方案的帮助？ 对于 Microsoft 365、企业移动性 + 安全性或 Azure Active Directory Premium，如果你拥有至少 150 个许可证，请使用 [FastTrack 权益](/enterprise-mobility-security/solutions/enterprise-mobility-fasttrack-program)。
