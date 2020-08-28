---
title: Windows Autopilot 许可要求
ms.reviewer: ''
manager: laurawi
description: 自行通知 Windows Autopilot 部署的许可要求。
keywords: mdm，安装程序，windows，windows 10，oobe，管理，部署，Autopilot，ztd，0-touch，合作伙伴，msfb，intune
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.custom:
- CI 116757
- CSSTroubleshooting
ms.openlocfilehash: 22f9b5f8e93339bc41403b2acf6e4ce53395a139
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88993774"
---
# <a name="windows-autopilot-licensing-requirements"></a>Windows Autopilot 许可要求

**适用于： Windows 10**

Windows Autopilot 取决于 Windows 10 和 Azure Active Directory 中提供的特定功能。 它还需要一个 MDM 服务，如 Microsoft Intune。 可以通过各种版本和订阅计划获得这些功能：

若要提供所需的 Azure Active Directory (自动 MDM 注册和公司品牌功能) 和 MDM 功能，需要以下订阅之一：
- [Microsoft 365 商业版高级订阅](https://www.microsoft.com/microsoft-365/business)
- [Microsoft 365 F1 或 F3 订阅](https://www.microsoft.com/microsoft-365/enterprise/firstline)
- [Microsoft 365 学术 A1、A3 或 A5 订阅](https://www.microsoft.com/education/buy-license/microsoft365/default.aspx)
- [Microsoft 365 企业版 E3 或 E5 订阅](https://www.microsoft.com/microsoft-365/enterprise)，其中包括所有 Windows 10、MICROSOFT 365 和 EM + S 功能 (Azure AD 和 Intune) 。
- [企业移动性 + 安全性 E3 或 E5 订阅](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)，其中包括所有所需的 Azure AD 和 Intune 功能。
- [Intune for Education 订阅](/intune-education/what-is-intune-for-education)，其中包括所有所需的 Azure AD 和 Intune 功能。
- [Azure Active Directory Premium P1 或 P2](https://azure.microsoft.com/services/active-directory/) 和 [Microsoft Intune 订阅](https://www.microsoft.com/cloud-platform/microsoft-intune) (或其他 MDM 服务) 。

> [!NOTE]
> 即使使用 Microsoft 365 订阅，仍需要向 [用户分配 Intune 许可证](/intune/fundamentals/licenses-assign)。

此外，还建议使用以下 (但不是必需的) ：
- [Microsoft 365 适用于企业的应用](https://www.microsoft.com/p/office-365-proplus/CFQ7TTC0K8R0)，可通过 Intune (或其他 MDM 服务) 轻松部署。
- [Windows 订阅激活](/windows/deployment/windows-10-enterprise-subscription-activation)，将设备从 Windows 10 专业版自动单步执行到 Windows 10 企业版。

**后续步骤**

[Windows Autopilot 配置要求](configuration-requirements.md)