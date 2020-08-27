---
title: Windows Autopilot 概述
description: Windows Autopilot 是一组用于设置和预配置新设备以让它们可供高效使用的技术。
keywords: mdm, 设置, windows, windows 10, oobe, 管理, 部署, autopilot, ztd, 零接触, 合作伙伴, msfb, intune
ms.reviewer: mniehaus
manager: laurawi
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
ms.openlocfilehash: 8c339e2a55fd8876ce8a144bb72c7c0a37de8346
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88907831"
---
# <a name="overview-of-windows-autopilot"></a>Windows Autopilot 概述

**适用于**

-  Windows 10

Windows Autopilot 是一组用于设置和预配置新设备以让它们可供高效使用的技术。 你还可以使用 Windows Autopilot 重置、重新使用和恢复设备。 此解决方案可以让 IT 部门通过轻松简单的流程，在几乎不需要管理基础结构的情况下实现上述目标。

Windows Autopilot 为 IT 用户和最终用户简化了 Windows 设备生命周期，从初始部署到生命周期。 使用基于云的服务，Windows Autopilot：
- 减少部署、管理和注销设备所花费的时间。
- 减少维护设备所需的基础结构。
- 最大程度地提高了所有类型的最终用户的易用性。

请参阅以下视频和关系图：

&nbsp;

> [!video https://www.microsoft.com/videoplayer/embed/RE4C7G9?autoplay=false]

![过程概述](images/image1.png)

初次部署新的 Windows 设备时，Windows Autopilot 使用 OEM 优化版本的 Windows 10。 此版本预安装在设备上，因此无需为每个设备型号维护自定义映像和驱动程序。 你的现有 Windows 10 安装可以转换为 "企业就绪" 状态，而不是重新映像设备，可以：
- 应用设置和策略
- 安装应用
- 更改使用的 Windows 10 版本 (例如，从 Windows 10 专业版到 Windows 10 企业版) ，以支持高级功能。

部署后，你可以通过以下方式管理 Windows 10 设备：
- Microsoft Intune
- Windows Update for Business
- Microsoft Endpoint Configuration Manager
- 或其他类似工具。

使用 Windows Autopilot，你可以使用 Windows Autopilot Reset 为新用户快速准备设备。 你还可以在中断/修复方案中使用 "重置" 以快速将设备恢复到业务就绪状态。

借助 Windows Autopilot，你可以：
* 将设备自动加入到 Azure Active Directory (Azure AD) 或 Active Directory（通过混合 Azure AD 联接）。 有关这两个联接选项之间的差异的详细信息，请参阅 [Azure Active Directory 中的设备管理简介](/azure/active-directory/device-management-introduction)。
* 自动将设备注册到 MDM 服务（如 Microsoft Intune ([*需要 Azure AD Premium 订阅才能配置*](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-Identity/Windows-10-Azure-AD-and-Microsoft-Intune-Automatic-MDM/ba-p/244067)) 。
* 限制管理员帐户的创建。
* 根据设备的配置文件创建设备并将其自动分配到配置组。
* 自定义特定于组织的 OOBE 内容。

## <a name="benefits-of-windows-autopilot"></a>Windows Autopilot 的优势

通常，IT 专业人员花费大量时间来构建和自定义以后将部署到设备的映像。 Windows Autopilot 引入了新方法。

从用户的角度来看，只需几个简单操作便可以使其设备准备就绪，以供使用。

从 IT 专业人员的角度来看，最终用户所需的交互将只有连接到网络并验证其凭据。 这一切都是自动化的。

## <a name="requirements"></a>要求

使用 Windows Autopilot 需要 Windows 10 半年频道的 [受支持版本](/windows/release-information/) 。 还支持 Windows 10 Enterprise LTSC 2019。 有关详细信息，请参阅 [Windows Autopilot software](software-requirements.md)、 [网络](networking-requirements.md)、 [配置](configuration-requirements.md)和 [许可](licensing-requirements.md) 要求。

## <a name="related-topics"></a>相关主题

[使用 Windows Autopilot 在 Intune 中注册 Windows 设备](/intune/enrollment-autopilot)<br>
[Windows Autopilot 方案和功能](windows-autopilot-scenarios.md)