---
title: 什么是 Microsoft Intune - Azure | Microsoft Docs
description: 了解 Microsoft Intune 如何成为企业移动性 + 安全性解决方案的移动设备管理 (MDM) 和移动应用管理 (MAM) 组件，以及它如何帮助保护公司数据。
keywords: 什么是 Intune
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 06/23/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 3b4e778d-ac13-4c23-974f-5122f74626bc
ms.reviewer: pmay
ms.suite: ems
search.appverid: MET150
ms.custom: get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6e8fa8db5e7a960677eeafaf03ca43662da9b8d3
ms.sourcegitcommit: d6cbd1a1c2926064e074e3431471534eb142c905
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90012640"
---
# <a name="microsoft-intune-is-an-mdm-and-mam-provider-for-your-devices"></a>Microsoft Intune 是适用于设备的 MDM 和 MAM 提供程序

Microsoft Intune 是一项基于云的服务，关注移动设备管理 (MDM) 和移动应用程序管理 (MAM)。 可以控制如何使用组织的设备，包括移动电话、平板电脑和笔记本电脑。 还可以配置特定策略来控制应用程序。 例如，可以阻止电子邮件发送给组织外部人员。 Intune 还可便于组织中的人员在学校或工作中使用个人设备。 在个人设备上，Intune 有助于确保组织数据始终受到保护，并能将组织数据与个人数据隔离开来。

Intune 属于 Microsoft [企业移动性 + 安全性 (EMS) 套件](https://www.microsoft.com/microsoft-365/enterprise-mobility-security)。 Intune 与 Azure Active Directory (Azure AD) 集成，以控制谁有权可以访问什么。 它还与 Azure 信息保护集成，以实现数据保护。 它可以与 Microsoft 365 产品套件配合使用。 例如，可以将 Microsoft Teams、OneNote 和其他 Microsoft 365 应用部署到设备。 借助此功能，组织中的人员可以在自己的所有设备上高效工作，同时使用你创建的策略来保护组织的信息。

[![Intune 体系结构示意图](./media/what-is-intune/intunearch_sm.png )](./media/what-is-intune/intunearchitecture.svg#lightbox)

通过 Intune，还可以：

- 选择使用 Intune 的 100% 云，或与 Configuration Manager 和 Intune [共同托管](/configmgr/comanage/overview)。
- 设置规则并在个人拥有的设备和组织拥有的设备上配置设置以访问数据和网络。
- 在设备（本地和移动）上部署应用并对其进行身份验证。
- 通过控制用户访问和共享信息的方式来保护公司信息。
- 确保设备和应用符合安全要求。

## <a name="manage-devices"></a>管理设备

在 Intune 中，使用适合你的方法来管理设备。 对于组织拥有的设备，你可能希望完全控制设备，包括设置、功能和安全性。 在此方法中，设备和这些设备的用户在 Intune 中“注册”。 注册后，他们通过 Intune 中配置的策略接收规则和设置。 例如，可以设置密码和 PIN 要求，创建 VPN 连接，设置威胁防护等。

对于个人设备或自带设备办公 (BYOD)，用户可能不希望其组织管理员拥有完全控制权限。 在此方法中，为用户提供选项。 例如，如果用户需要拥有对组织资源的完全访问权限，则[注册](../enrollment/device-enrollment.md)其设备。 或者，如果这些用户只想访问电子邮件或 Microsoft Teams，则使用需要多重身份验证 (MFA) 才能使用这些应用的应用保护策略。

在 Intune 中注册和管理设备时，管理员可以：

- 查看已注册的设备，并获取访问组织资源的设备的清单。
- 配置设备，使其满足安全和运行状况标准。 例如，你可能想要阻止已越狱的设备。
- 将证书推送到设备，以便用户可以轻松访问 Wi-Fi 网络，或使用 VPN 连接到网络。
- 查看有关符合和不符合要求的用户和设备的报表。
- 如果设备丢失、被盗或不再使用，则删除组织数据。

**联机资源**：

- [什么是设备注册？](../enrollment/device-enrollment.md)

- [对使用设备配置文件的设备应用功能和设置](../configuration/device-profiles.md)

- [使用 Microsoft Intune 保护设备](../protect/device-protect.md)

### <a name="try-the-interactive-guide"></a>尝试交互式指南
[使用 Microsoft Endpoint Manager 管理设备](https://mslearn.cloudguides.com/guides/Manage%20devices%20with%20Microsoft%20Endpoint%20Manager)交互式指南将引导你浏览 Microsoft Endpoint Manager 管理中心，并展示如何管理和保护移动和桌面应用程序。</br></br>

<div align=”center”>
<iframe allowfullscreen width="95%" height="450" src="https://mslearn.cloudguides.com/guides/Manage%20devices%20with%20Microsoft%20Endpoint%20Manager" frameborder="0" scrolling="no" loading="lazy" importance="low"/></iframe>
</div>

## <a name="manage-apps"></a>管理应用

Intune 中的移动应用程序管理 (MAM) 设计为在应用程序级别（包括自定义应用和应用商店应用）保护组织数据。 可以在组织拥有的设备和个人设备上使用应用管理。

在 Intune 中管理应用时，管理员可以：

- 添加移动应用并将其分配给用户组和设备，包括特定组中的用户、特定组中的设备等。
- 将应用配置为启用特定设置后启动或运行，并更新设备上的现有应用。
- 查看有关使用哪些应用的报表，并跟踪其使用情况。
- 通过仅从应用中删除组织数据进行选择性擦除。

Intune 提供移动应用安全的一种方法是通过[应用保护策略](../apps/app-protection-policy.md)。 应用保护策略：

- 使用 Azure AD 标识将组织数据与个人数据隔离。 因此，个人信息与组织 IT 识别隔离。 使用组织凭据访问的数据被授予其他安全保护。
- 通过限制用户可执行的操作（例如复制和粘贴、保存以及查看）来帮助保护个人设备上的访问权限。
- 可以在已在 Intune 中注册的设备、已在其他 MDM 服务中注册的设备或未在任何 MDM 服务中注册的设备上创建和部署。 在已注册的设备上，应用保护策略可以添加额外的保护层。

例如，用户使用其组织凭据登录到设备。 使用组织标识可以访问被其个人标识拒绝的数据。 用户使用该组织数据时，应用保护策略会控制数据的保存方式和共享方式。 当用户使用其个人标识登录时，不会应用这些相同的保护。 这样，IT 能够控制组织数据，而最终用户可以保持对其个人数据的控制性和私密性。

此外，还可以将 Intune 与 EMS 中的其他服务结合使用。 此功能提供了操作系统和任何应用不包括的组织移动应用安全性。 使用 EMS 管理的应用可以访问更多的移动应用和数据保护功能。

![显示应用管理数据安全级别的图片](./media/what-is-intune/managing-mobile-apps.png)

## <a name="compliance-and-conditional-access"></a>符合性和条件访问

通过与 Azure AD 集成，Intune 实现了一系列广泛的访问控制方案。 例如，在访问网络资源（如电子邮件或 SharePoint）之前，要求移动设备符合 Intune 中定义的组织标准。 同样，可以将服务锁定到特定的一组移动应用。 例如，可以锁定 Exchange Online，只允许由 Outlook 或 Outlook Mobile 进行访问。

**联机资源**：

- [在设备上设置规则以允许访问组织资源](../protect/device-compliance-get-started.md)

- [使用 Intune 条件访问的常见方式](../protect/conditional-access-intune-common-ways-use.md)

## <a name="how-to-get-intune"></a>如何获取 Intune

Intune 可用：

- 作为独立的 [Azure 服务](https://go.microsoft.com/fwlink/?linkid=2090973)
- 包括 [Microsoft 365](https://www.microsoft.com/microsoft-365/enterprise-mobility-security/microsoft-intune) 和 [Microsoft 365 政府版](https://www.microsoft.com/microsoft-365/government)
- 作为 [Microsoft 365 中的移动设备管理](https://support.office.com/article/Set-up-Mobile-Device-Management-MDM-in-Office-365-dd892318-bc44-4eb1-af00-9db5430be3cd)，其中包含一些有限的 Intune 功能

Intune 用于许多扇区，包括[政府版](/enterprise-mobility-security/solutions/ems-govt-service-description)、[教育版](https://www.microsoft.com/en-us/education/intune)、用于制造和零售的[展台或专用设备](../configuration/kiosk-settings.md)等。

## <a name="next-steps"></a>后续步骤

- 阅读一些 [Intune 可帮助解决的常见业务问题](common-scenarios.md)。
- 开始使用 [Intune 30 天试用版](free-trial-sign-up.md)。
- 计划[到 Azure 的迁移](migration-guide.md)。
- 使用免费试用版或订阅，逐步完成[快速入门：创建适用于 iOS 的电子邮件设备配置文件](../configuration/quickstart-email-profile.md)中的步骤创建适用于 iOS 设备的测试设备配置文件。