---
title: 设置 macOS 设备注册
titleSuffix: Microsoft Intune
description: 了解如何在 Intune 中设置 macOS 设备注册。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/12/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 46429114-2e26-4ba7-aa21-b2b1a5643e01
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7f2b2826e8eaf1cf1c1c8680743b582203199aed
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88906831"
---
# <a name="set-up-enrollment-for-macos-devices-in-intune"></a>在 Intune 中设置 macOS 设备注册

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Intune 可以管理 macOS 设备以允许用户访问公司电子邮件和应用。

作为 Intune 管理员，可以为公司拥有的 macOS 设备和个人拥有的 macOS 设备（“自带设备办公”或 BYOD）设置注册。 

## <a name="prerequisites"></a>必备条件

设置 macOS 设备注册之前请先完成以下先决条件：

- [确保设备符合 Apple 设备注册的条件](https://support.apple.com/en-us/HT204142#eligibility)。
- [配置域](../fundamentals/custom-domain-name-configure.md)
- [设置 MDM 机构](../fundamentals/mdm-authority-set.md)
- [创建组](../fundamentals/groups-add.md)
- [配置公司门户](../apps/company-portal-app.md)
- 在 [Microsoft 365 管理中心](https://go.microsoft.com/fwlink/p/?LinkId=698854)分配用户许可证
- [获取 Apple MDM Push Certificate](../enrollment/apple-mdm-push-certificate-get.md)

## <a name="user-owned-macos-devices-byod"></a>用户拥有的 macOS 设备 (BYOD)

可以让用户将其个人设备注册到 Intune 管理。 这称为“自带设备办公”或简称 BYOD。 完成先决条件并分配用户许可证后，用户可以通过以下方式注册其设备：
- 转到[公司门户网站](https://portal.manage.microsoft.com)或
- 在 [aka.ms/EnrollMyMac](https://aka.ms/EnrollMyMac) 下载 Mac 公司门户应用。

你还可以向用户发送联机注册步骤的链接：[在 Intune 中注册 macOS 设备](../user-help/enroll-your-device-in-intune-macos-cp.md)。

有关其他最终用户任务的信息，请参阅以下文章：

- [有关 Microsoft Intune 最终用户体验的资源](../fundamentals/end-user-educate.md)
- [通过 Intune 使用 macOS 设备](../user-help/enroll-your-device-in-intune-macos-cp.md)

## <a name="company-owned-macos-devices"></a>公司拥有的 macOS 设备
对于为用户购买设备的组织，Intune 还支持以下公司自有的 macOS 设备注册方法：
- [Apple 的自动设备注册 (ADE)](device-enrollment-program-enroll-macos.md)：组织可以通过 ADE 购买 macOS 设备。 ADE 允许用户通过“无线方式”部署注册配置文件以对设备进行管理。
- [设备注册管理员 (DEM)](device-enrollment-manager-enroll.md)：最多可以使用 DEM 帐户注册 1,000 台设备。
- [直接注册](device-enrollment-direct-enroll-macos.md)：直接注册不会擦除设备。

## <a name="block-macos-enrollment"></a>阻止 macOS 注册
默认情况下，Intune 允许注册 macOS 设备。 若要阻止 macOS 注册设备，请参阅[设置设备类型限制](enrollment-restrictions-set.md)。

## <a name="enroll-virtual-macos-machines-for-testing"></a>注册用于测试的虚拟 macOS 计算机

> [!NOTE]
> macOS 虚拟机只支持用于测试。 不应将 macOS 虚拟机用作最终用户的生产设备。 

可以使用 Parallels Desktop 或 VMware Fusion 注册用于测试的 macOS 虚拟机。 

对于 Parallels Desktop，需要设置虚拟机的硬件类型和序列号，使 Intune 能够识别它们。 按照 Parallels 的设置硬件类型和[序列号](http://kb.parallels.com/123455)说明进行操作，设置测试所必需的设置。 建议运行虚拟机的设备的硬件类型与要创建的虚拟机的硬件类型相匹配。 可通过“Apple 菜单” > “关于此 Mac” > “系统报告” > “模型标识符”找到此硬件类型   。 

对于 VMware Fusion，需要[编辑 .vmx 文件](https://kb.vmware.com/s/article/1014782)，设置虚拟机的硬件模型和序列号。 建议运行虚拟机的设备的硬件类型与要创建的虚拟机的硬件类型相匹配。 可通过“Apple 菜单” > “关于此 Mac” > “系统报告” > “模型标识符”找到此硬件类型   。 

## <a name="user-approved-enrollment"></a>用户已批准注册

用户批准的 MDM 注册是一种可用于管理某些安全敏感设置的 macOS 注册类型。 有关详细信息，请参阅 [Apple 的支持文档](https://support.apple.com/HT208019)。  
 
从 2020 年 6 月起，Intune 中的所有新 macOS MDM 注册（包括不是通过自动设备注册 (ADE) 完成的注册）都视为已获用户批准。  最终用户必须在“系统首选项” > “配置文件”中手动安装管理配置文件，从而为管理配置文件提供批准。 针对 BYOD macOS 用户从公司门户应用自动启动系统首选项。 公司门户应用中提供了[有关安装管理配置文件的说明](../user-help/enroll-your-device-in-intune-macos-cp.md)。     

 如果最终用户未在“系统首选项” > “配置文件”中手动提供管理配置文件的批准，则在 2020 年 6 月之前的 BYOD macOS MDM 注册可能未获用户批准。 对于 2020 年 6 月之后的 BYOD 注册，公司门户应用为用户启动“系统首选项”，用户将需要选择“安装”。 若在注册过程中用户未批准该管理配置文件，用户可以转到“系统首选项” > “配置文件”，选择管理配置文件，然后选择“批准”在稍后批准配置文件。

### <a name="find-out-if-a-device-is-user-approved"></a>查明设备是否处于“用户已批准”状态
1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“设备” > “所有设备”，再依次选择相关设备和“硬件”  。
3. 选中“用户已批准注册”字段。


## <a name="next-steps"></a>后续步骤

注册 macOS 设备后，可[为 macOS 设备创建自定义设置](../configuration/custom-settings-macos.md)。