---
title: Microsoft Intune 基本设置
description: 本文提供设置 Microsoft Intune 所需的步骤。
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 03/04/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 60cfa440-0723-4ea0-bacf-3c5d26f9a1d3
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3b7784d4ad86e3418259f85ca1c4577d2289dc86
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79358151"
---
# <a name="basic-setup"></a>基本设置

评估环境后，即可设置 Microsoft Intune。

## <a name="external-dependencies-for-an-intune-deployment"></a>Intune 部署的外部依赖关系

### <a name="identity"></a>标识

Intune 要求 Azure Active Directory (AAD) 作为标识和用户分组提供者。 了解详细信息：

- [身份要求](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview#design-considerations-overview)

- [目录同步路线图](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-directory-sync-requirements)

- [多重身份验证 (MFA)](https://docs.microsoft.com/azure/active-directory/authentication/concept-mfa-howitworks)

- [规划用户和设备组](users-add.md)

- [如何创建用户和设备组](groups-get-started.md)

如果组织已在使用 Office 365，则 Intune 必须使用相同的 Azure Active Directory 环境。

### <a name="pki-optional"></a>PKI（可选）

如果打算将针对 VPN、Wi-Fi 或电子邮件配置文件的基于证书的身份验证与 Intune 结合使用，需确保具有受支持的 [PKI 基础结构](../protect/certificates-configure.md)，并准备好创建和部署证书配置文件。 有关在 Intune 中配置证书的详细信息，请参阅：

- [如何配置 SCEP 证书基础结构](/intune/certificates-scep-configure)

- [如何配置 PFX 证书基础结构](/intune/certficates-pfx-configure)。

## <a name="task-list-for-an-intune-setup"></a>Intune 设置的任务列表

### <a name="task-1-intune-subscription"></a>任务 1：Intune 订阅

迁移到 Intune 之前，首先需要 [Intune 订阅](account-sign-up.md)。

### <a name="task-2-assign-intune-user-licenses"></a>任务 2：分配 Intune 用户许可证

- 了解[如何分配 Intune 用户许可证](licenses-assign.md)。

- 如果你已创建新的 Azure Active Directory 租户，可以了解[如何从本地 Active Directory (AD) 中创建新的用户或同步用户。](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)

### <a name="task-3-set-your-mdm-authority-to-intune"></a>任务 3：将 MDM 机构设置为 Intune

建议使用 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)来管理 Intune。

将 MDM 机构设置为 Intune  。 使用不同的 MDM 机构以使 Intune 将 MDM 管理传输到备用 Microsoft 管理控制台。 这种情况并不常见。

> [!IMPORTANT]
> 如果你是第一次将移动设备管理传输到 Intune，则应将 MDM 机构设置为 Intune。

了解[如何设置移动管理机构](mdm-authority-set.md)。

## <a name="next-step"></a>下一步

配置[设备和应用管理策略](migration-guide-configure-policies.md)。
