---
title: Windows Autopilot 配置要求
ms.reviewer: ''
manager: laurawi
description: 自行通知 Windows Autopilot 部署的配置要求。
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
ms.openlocfilehash: 8731532ff052c626514d9f1a80e3a93c0cbde6dc
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88908315"
---
# <a name="windows-autopilot-configuration-requirements"></a>Windows Autopilot 配置要求

**适用于： Windows 10**

在可以使用 Windows Autopilot 之前，需要执行一些配置任务来支持常见的 Autopilot 方案。 

- 配置 Azure Active Directory 自动注册。 有关 Microsoft Intune，请参阅 [启用 Windows 10 自动注册](/intune/windows-enroll#enable-windows-10-automatic-enrollment) 以获取详细信息。 如果使用不同的 MDM 服务，请与供应商联系，以了解这些服务所需的特定 Url 或配置。
- 配置 Azure Active Directory 自定义品牌。 若要显示组织特定的登录页，必须使用要显示的图像和文本配置 Azure Active Directory。 有关详细信息，请参阅 [Azure AD 中的快速入门：将公司品牌添加到登录页](/azure/active-directory/fundamentals/customize-branding)。 Autopilot 的关键元素包括 "方形徽标"、"登录页文本" 和 "Azure Active Directory 租户名称"。 租户名称分别在 Azure AD 租户属性中进行配置。
- 可选：若要从 Windows 10 专业版自动单步执行到 Windows 10 企业版，请启用 [Windows 订阅激活](/windows/deployment/windows-10-enterprise-subscription-activation)。

具体方案将具有其他要求。 通常有两个特定任务：

- 设备注册。 必须将设备添加到 Windows Autopilot 以支持大多数 Windows Autopilot 方案。 有关详细信息，请参阅向 [Windows Autopilot 添加设备](add-devices.md)。
- 配置文件配置。 在将设备添加到 Windows Autopilot 后，需要将设置的配置文件应用于每个设备。 有关详细信息，请参阅 [配置 Autopilot 配置文件](profiles.md) 。  Microsoft Intune 可以自动执行此配置文件分配。 有关详细信息，请参阅 [创建 Autopilot 设备组](/intune/enrollment-Autopilot#create-an-Autopilot-device-group) 和 [将 Autopilot 部署配置文件分配到设备组](/intune/enrollment-Autopilot#assign-an-Autopilot-deployment-profile-to-a-device-group)。

有关详细信息，请参阅 [Windows Autopilot 方案](windows-Autopilot-scenarios.md)。

有关部分和相关步骤的演练，请观看此视频：

</br>

<iframe width="560" height="315" src="https://www.youtube.com/embed/KYVptkpsOqs" frameborder="0" allow="accelerometer; autoplay; encrypted-media" gyroscope; picture-in-picture" allowfullscreen></iframe>


除了[运行 Windows 10 的要求](https://www.microsoft.com/windows/windows-10-specifications)之外，使用 Windows 10 Autopilot 时没有其他硬件要求。

**后续步骤**

[Windows Autopilot 概述](windows-autopilot.md)