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
ms.openlocfilehash: 171070e1560796763f3c3851afe239237098f756
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87756106"
---
# <a name="overview-of-windows-autopilot"></a>Windows Autopilot 概述

**适用于**

-   Windows 10

Windows Autopilot 是一组用于设置和预配置新设备以让它们可供高效使用的技术。 你还可以使用 Windows Autopilot 来重置、恢复设备并重新调整其用途。 此解决方案可以让 IT 部门通过轻松简单的流程，在几乎不需要管理基础结构的情况下实现上述目标。

Windows Autopilot 旨在为 IT 和最终用户简化 Windows 设备生命周期的各个部分，从初始部署一直到生命的最终结束。 它利用基于云的服务，通过减少 IT 用于部署、管理和停用设备的时间和需要维护的基础结构量来减少这些过程的总体成本，同时还可为所有类型的最终用户确保易用性。 请参阅以下视频和关系图：

&nbsp;

> [!video https://www.microsoft.com/videoplayer/embed/RE4C7G9?autoplay=false]

![过程概述](images/image1.png)

初次部署新的 Windows 设备时，Windows Autopilot 利用设备上预安装的 OEM 优化版本的 Windows 10，使组织能够为所使用的每个设备型号维护自定义映像和驱动程序。 你的现有 Windows 10 安装可以转换为 "企业就绪" 状态、应用设置和策略、安装应用，甚至更改正在 (使用的 Windows 10 版本（例如从 Windows 10 专业版到 Windows 10 企业版) ，以支持高级功能），而不是对设备重新进行映像。

部署后，Windows 10 设备可以通过工具进行管理，例如 Microsoft Intune、Windows 更新 for Business、Microsoft Endpoint Configuration Manager 和其他类似工具。 Windows Autopilot 还可用于通过利用 Windows Autopilot Reset 为新用户快速准备设备，或通过中断/修复方案使设备快速恢复到业务就绪状态，来重新使用设备。

借助 Windows Autopilot，你可以：
* 将设备自动加入到 Azure Active Directory (Azure AD) 或 Active Directory（通过混合 Azure AD 联接）。  有关这两个加入选项之间的差异的详细信息，请参阅 [Azure Active Directory 中的设备管理简介](https://docs.microsoft.com/azure/active-directory/device-management-introduction)。
* 自动将设备注册到 MDM 服务（如 Microsoft Intune ([*需要 Azure AD Premium 订阅才能配置*](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-Identity/Windows-10-Azure-AD-and-Microsoft-Intune-Automatic-MDM/ba-p/244067)) 。
* 限制管理员帐户的创建。
* 根据设备的配置文件创建设备并将其自动分配到配置组。
* 自定义特定于组织的 OOBE 内容。

## <a name="benefits-of-windows-autopilot"></a>Windows Autopilot 的优势

IT 专业人员通常会花费大量时间生成和自定义稍后将部署到设备的图像。 Windows Autopilot 引入了新方法。

从用户的角度来看，只需几个简单操作便可以使其设备准备就绪，以供使用。

从 IT 专业人员的角度来看，最终用户所需的交互将只有连接到网络并验证其凭据。 这一切都是自动化的。

## <a name="requirements"></a>要求

使用 Windows Autopilot 需要 Windows 10 半年频道的[受支持版本](https://docs.microsoft.com/windows/release-information/)。 还支持 Windows 10 Enterprise LTSC 2019。 有关软件、配置、网络和许可要求的详细信息，请参阅[Windows Autopilot 的要求](windows-autopilot-requirements.md)。

## <a name="related-topics"></a>相关主题

[使用 Windows Autopilot 在 Intune 中注册 Windows 设备](https://docs.microsoft.com/intune/enrollment-autopilot)<br>
[Windows Autopilot 方案和功能](windows-autopilot-scenarios.md)
