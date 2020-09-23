---
title: 条件访问方案
titleSuffix: Microsoft Intune
description: 了解 Intune 条件访问通常如何用于基于设备和基于应用的条件访问。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: a0b8e55e-c3d8-4599-be25-dc10c1027b62
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6d062af4859dcca6c762bf401e1007a9fc9af126
ms.sourcegitcommit: fdd6d3c4b906e895ebec2856ebc38b0656296d2c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/22/2020
ms.locfileid: "91002658"
---
# <a name="what-are-common-ways-to-use-conditional-access-with-intune"></a>通过 Intune 使用条件访问的常见方式有哪些？

使用 Intune 的条件访问有两种：基于设备的条件访问和基于应用的条件访问。 需要配置相关的符合性策略，以驱动组织中的条件访问符合性。 条件访问通常用于执行以下操作：允许或阻止对 Exchange 的访问、控制网络访问权限、与 Mobile Threat Defense 解决方案集成等。
 
本文中的信息有助于了解如何使用 Intune 移动设备符合性功能和 Intune 移动应用程序管理 (MAM) 功能   。 

> [!NOTE]
> 条件访问是 Azure Active Directory Premium 许可证附带的 Azure Active Directory 功能。 Intune 通过向解决方案添加移动设备符合性和移动应用管理来增强此功能。 从 Intune 访问的条件访问节点与从 Azure AD 访问的节点相同   。  

## <a name="device-based-conditional-access"></a>基于设备的条件访问

配合使用 Intune 和 Azure Active Directory，可确保只有合规的托管设备才能访问电子邮件、Microsoft 365 服务、软件即服务 (SaaS) 应用和[本地应用](/azure/active-directory/active-directory-application-proxy-get-started)。 此外，可在 Azure Active Directory 中设置策略，以仅允许加入域的计算机或在 Intune 中注册的移动设备访问 Microsoft 365 服务。

Intune 提供了设备符合性策略功能，可评估设备的符合性状态。 在用户尝试访问公司资源时，符合性状态会报告给 Azure Active Directory，用于强制执行在 Azure Active Directory 中创建的条件访问策略。

Exchange Online 和其他 Microsoft 365 产品的基于设备的条件访问策略通过 [Azure 门户](../fundamentals/what-is-intune.md)进行配置。

- 了解有关[需要具有 Azure Active Directory 中条件访问权限的受管理设备](/azure/active-directory/conditional-access/require-managed-devices)的详细信息。

- 了解有关 [Intune 设备符合性](device-compliance-get-started.md)的详细信息。

- 了解有关 [Azure Active Directory 中通过条件访问使用受支持的浏览器](/azure/active-directory/conditional-access/technical-reference#supported-browsers)的详细信息。

> [!NOTE]
> 在 Android 设备上为 SharePoint Online 或对 Exchange Online 的基于浏览器的访问启用基于设备的访问时，用户必须在注册的设备上打开“启用浏览器访问”选项，如下所示：
> 1. 启动“公司门户应用”  。
> 2. 从三个点 (…) 或硬件菜单按钮转到“设置”  页。
> 3. 按“启用浏览器访问”  按钮。 
> 4. 在 Chrome 浏览器中退出 Microsoft 365，然后重启 Chrome。

### <a name="conditional-access-based-on-network-access-control"></a>基于网络访问控制的条件性访问

基于 Intune 注册和设备符合性状态，Intune 与 Cisco ISE、Aruba Clear Pass 以及 Citrix NetScaler 等合作伙伴集成，以提供访问控制。

根据用户使用的设备是否受管理以及是否符合 Intune 设备符合性策略，可以允许或拒绝他们访问企业 Wi-Fi 或 VPN 资源。

- 详细了解 [NAC 与 Intune 的集成](network-access-control-integrate.md)。

### <a name="conditional-access-based-on-device-risk"></a>基于设备风险的条件性访问

Intune 与移动威胁防护供应商合作提供安全性解决方案，以检测恶意软件、木马以及移动设备上的其他威胁。

#### <a name="how-the-intune-and-mobile-threat-defense-integration-works"></a>Intune 和移动威胁防御集成的工作方式

在移动设备安装了移动威胁防御代理后，一旦发现移动设备自身存在威胁，代理即将符合性状态消息发送回 Intune 报告。

在基于设备风险的条件访问决策中，Intune 和移动威胁防御集成发挥着重要的作用。

- 了解 [Intune 移动威胁防御](mobile-threat-defense.md)的详细信息。

### <a name="conditional-access-for-windows-pcs"></a>Windows 电脑的条件访问

适用于电脑的条件访问提供与移动设备可用的类似功能。 让我们介绍一下使用 Intune 管理电脑时，你可以使用条件性访问的方式。

#### <a name="corporate-owned"></a>公司拥有的设备

- **已联接混合 Azure AD：** 此选项通常适用于已经非常习惯通过 AD 组策略或 Configuration Manager 管理 PC 的组织。

- **Azure AD 域加入和 Intune 管理：** 此方案适用于希望云优先（即主要使用云服务，以减少使用本地基础结构）或仅使用云（无本地基础结构）的组织。 Azure AD 联接非常适用于混合环境，可以借助它访问云和本地应用及资源。 设备要加入 Azure AD 并在 Intune 中注册，可以将此用作访问公司资源的条件访问条件。

#### <a name="bring-your-own-device-byod"></a>自带设备办公 (BYOD)

- **工作区加入和 Intune 管理：** 用户可以加入自己的个人设备，以访问公司资源和服务。 你可以使用工作区将设备加入并注册到 Intune MDM 以接收设备级别的策略，这是评估条件访问标准的另一个选项。

了解有关 [Azure Active Directory 中的设备管理](/azure/active-directory/devices/overview)的详细信息。

## <a name="app-based-conditional-access"></a>基于应用的条件性访问

配合使用 Intune 和 Azure Active Directory，可确保只有托管应用才能访问公司电子邮件或其他 Microsoft 365 服务。

- 了解[使用 Intune 且基于应用的条件性访问](app-based-conditional-access-intune.md)的详细信息。

### <a name="intune-conditional-access-for-exchange-on-premises"></a>本地 Exchange 的 Intune 条件访问

基于设备符合性策略和注册状态，条件性访问可用于允许或阻止访问 **Exchange 内部部署**。 结合使用条件性访问与设备符合性策略时，仅允许合规的设备访问 Exchange 内部部署。

你可以在条件性访问中配置高级设置，以进行更精细的控制，例如：

- 允许或阻止某些平台。

- 立即阻止不受 Intune 管理的设备。

应用设备符合性和条件性访问策略时，检查用于访问 Exchange 内部部署的任何设备的符合性。

设备不满足设置的条件时，指导最终用户完成设备注册流程，以修复导致设备不符合的问题。

> [!NOTE]
> 从 2020 年 7 月开始，已弃用对 Exchange Connector 的支持，并已替换为 Exchange [新式混合身份验证](/office365/enterprise/hybrid-modern-auth-overview) (HMA)。 使用 HMA 不需要 Intune 设置和使用 Exchange Connector。 进行此更改后，用于配置和管理 Intune Exchange Connector 的 UI 也将从 Microsoft Endpoint Manager 管理中心删除，除非你已在订阅中使用 Exchange Connector。
>
> 如果你的环境中设置了 Exchange Connector，则仍支持你的 Intune 租户使用该连接器，并且你有权继续访问支持其配置的 UI。 有关更多详细信息，请参阅[安装 Exchange 内部部署连接器](../protect/exchange-connector-install.md)。 你可以继续使用该连接器，或者配置 HMA 后卸载你的连接器。
>
> 混合新式身份验证提供的功能之前 Intune Exchange Connector 也曾提供：设备标识到其 Exchange 记录的映射。  现在，此映射发生在你在 Intune 中进行的配置之外，或者要求 Intune 连接器桥接 Intune 和 Exchange。 使用 HMA，不再要求使用“Intune”特定配置（连接器）。


<!-- Deprecated with change from the connector to Exchange hybrid modern authentication)

#### How conditional access for Exchange on-premises works

Conditional access for Exchange on-premises works differently than Azure Conditional Access based policies. You install the Intune Exchange on-premises connector to directly interact with Exchange server. The Intune Exchange connector pulls in all the Exchange Active Sync (EAS) records that exist at the Exchange server so Intune can take these EAS records and map them to Intune device records. These records are devices enrolled and recognized by Intune. This process allows or blocks e-mail access.

If the EAS record is new and Intune isn't aware of it, Intune issues a cmdlet (pronounced "command-let") that directs the Exchange server to block access to e-mail. Following are more details on how this process works:

![Exchange on-premises with CA flow-chart](./media/conditional-access-intune-common-ways-use/ca-intune-common-ways-1.png)

1. User tries to access corporate email, which is hosted on Exchange on-premises 2010 SP1 or later.

2. If the device is not managed by Intune, access to email will be blocked. Intune sends a block notification to the EAS client.

3. EAS receives the block notification, moves the device to quarantine, and sends the quarantine email with remediation steps that contain links so the users can enroll their devices.

4. The Workplace join process happens, which is the first step to have the device managed by Intune.

5. The device gets enrolled into Intune.

6. Intune maps the EAS record to a device record, and saves the device compliance state.

7. The EAS client ID gets registered by the Azure AD Device Registration process, which creates a relationship between the Intune device record, and the EAS client ID.

8. The Azure AD Device Registration saves the device state information.

9. If the user meets the conditional access policies, Intune issues a cmdlet through the Intune Exchange connector that allows the mailbox to sync.

10. Exchange server sends the notification to EAS client so the user can access e-mail.
-->

#### <a name="whats-the-intune-role"></a>什么是 Intune 角色？

Intune 评估并管理设备状态。

#### <a name="whats-the-exchange-server-role"></a>什么是 Exchange Server 角色？

Exchange Server 提供了 API 和基础结构，可将设备移至隔离区域。

> [!IMPORTANT]
> 请注意，使用设备的用户必须将符合性配置文件和 Intune 许可证分配到该设备中，以便对其进行符合性评估。 如果未向用户部署合规性策略，该设备将被视为合规且不会对其应用任何访问限制。

## <a name="next-steps"></a>后续步骤

[如何在 Azure Active Directory 中配置条件访问](/azure/active-directory/active-directory-conditional-access-azure-portal)

[设置基于应用的条件访问策略](app-based-conditional-access-intune-create.md)

[如何为本地 Exchange 创建条件访问策略](conditional-access-exchange-create.md)
