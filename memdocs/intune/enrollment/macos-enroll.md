---
title: 设置 macOS 设备注册
titleSuffix: Microsoft Intune
description: 了解如何在 Intune 中设置 macOS 设备注册。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 12/16/2019
ms.topic: conceptual
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
ms.openlocfilehash: 7538cce4b116098db21e89d491476e8e0cd7f4e5
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/21/2020
ms.locfileid: "80086079"
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

你还可以向用户发送联机注册步骤的链接：[在 Intune 中注册 macOS 设备](https://docs.microsoft.com/mem/intune/user-help/enroll-your-device-in-intune-macos-cp)。

有关其他最终用户任务的信息，请参阅以下文章：

- [有关 Microsoft Intune 最终用户体验的资源](../fundamentals/end-user-educate.md)
- [通过 Intune 使用 macOS 设备](../user-help/enroll-your-device-in-intune-macos-cp.md)

## <a name="company-owned-macos-devices"></a>公司拥有的 macOS 设备
对于为用户购买设备的组织，Intune 还支持以下公司自有的 macOS 设备注册方法：
- [Apple 设备注册计划 (DEP)](device-enrollment-program-enroll-macos.md)：组织可以通过 Apple 设备注册计划 (DEP) 购买 macOS 设备。 DEP 允许用户通过“无线方式”部署注册配置文件以对设备进行管理。
- [设备注册管理员 (DEM)](device-enrollment-manager-enroll.md)：最多可以使用 DEM 帐户注册 1,000 台设备。

## <a name="block-macos-enrollment"></a>阻止 macOS 注册
默认情况下，Intune 允许注册 macOS 设备。 若要阻止 macOS 注册设备，请参阅[设置设备类型限制](enrollment-restrictions-set.md)。

## <a name="enroll-virtual-macos-machines-for-testing"></a>注册用于测试的虚拟 macOS 计算机

> [!NOTE]
> macOS 虚拟机只支持用于测试。 不应将 macOS 虚拟机用作最终用户的生产设备。 

可以使用 Parallels Desktop 或 VMware Fusion 注册用于测试的 macOS 虚拟机。 

对于 Parallels Desktop，需要设置虚拟机的硬件类型和序列号，使 Intune 能够识别它们。 按照 Parallels 的设置硬件类型和[序列号](http://kb.parallels.com/123455)说明进行操作，设置测试所必需的设置。 建议运行虚拟机的设备的硬件类型与要创建的虚拟机的硬件类型相匹配。 可通过“Apple 菜单” > “关于此 Mac” > “系统报告” > “模型标识符”找到此硬件类型     。 

对于 VMware Fusion，需要[编辑 .vmx 文件](https://kb.vmware.com/s/article/1014782)，设置虚拟机的硬件模型和序列号。 建议运行虚拟机的设备的硬件类型与要创建的虚拟机的硬件类型相匹配。 可通过“Apple 菜单” > “关于此 Mac” > “系统报告” > “模型标识符”找到此硬件类型     。 

## <a name="user-approved-enrollment"></a>用户已批准注册
用户批准的 MDM 注册是一种可用于管理某些安全敏感设置的 macOS 注册类型。 有关详细信息，请参阅 [Apple 的支持文档](https://support.apple.com/HT208019)。  
 
在 BYOD 注册过程中，将要求用户手动批准 Apple 管理配置文件。 适用于 macOS 的公司门户应用提供了说明。 尽管无需批准此管理配置文件即可完成注册，但 Intune 建议经过用户批准完成注册。 若在注册过程中用户未批准此配置文件，用户可以转到“系统首选项”   > “配置文件”，  选择管理配置文件，然后选择“批准”。     

### <a name="find-out-if-a-device-is-user-approved"></a>查明设备是否处于“用户已批准”状态
1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“设备” > “所有设备”，再依次选择相关设备和“硬件”    。
3. 选中  “用户已批准注册”字段。


## <a name="next-steps"></a>后续步骤

注册 macOS 设备后，可[为 macOS 设备创建自定义设置](../configuration/custom-settings-macos.md)。
