---
title: 设置 Check Point SandBlast MTD
titleSuffix: Microsoft Intune
description: 了解如何将 Intune 与 Check Point SandBlast Mobile Threat Defense 相集成以控制移动设备对公司资源的访问。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 706a4228-9bdf-41e0-b8d1-64c923dd2d2b
ms.reviewer: davidra
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: e9c1450af064caa1f7572da0ab4753e9db68484c
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989254"
---
# <a name="check-point-sandblast-mobile-threat-defense-connector-with-intune"></a>Check Point SandBlast 移动威胁防御连接器与 Intune

可根据 Check Point SandBlast Mobile 给出的风险评估，使用条件访问控制移动设备对公司资源的访问，Check Point SandBlast Mobile 是与 Microsoft Intune 集成的移动威胁防御解决方案。 基于从运行 Check Point SandBlast Mobile 应用的设备收集的遥测评估风险。

可以基于通过 Intune 设备符合性策略启用的 Check Point SandBlast Mobile 风险评估配置条件访问策略，从而根据检测到的威胁允许或阻止不符合设备访问公司资源。

> [!NOTE]
> 未注册的设备不支持此移动威胁防御供应商。

## <a name="supported-platforms"></a>受支持的平台

- **Android 4.1 及更高版本**

- **iOS 8 及更高版本**

## <a name="pre-requisites"></a>先决条件

- Azure Active Directory Premium

- Microsoft Intune 订阅

- Check Point SandBlast Mobile 威胁防御订阅
  - 有关详细信息，请参阅 [CheckPoint SandBlast 网站 ](https://www.checkpoint.com/)。

## <a name="how-do-intune-and-check-point-sandblast-mobile-help-protect-your-company-resources"></a>Intune 和 Check Point SandBlast Mobile 如何帮助你保护公司资源？

适用于 Android 或 iOS/iPadOS 的 Check Point Sandblast Mobile 应用可捕获文件系统、网络堆栈，以及设备和应用程序遥测（如果有），然后将遥测数据发送到 Check Point Sandblast 云服务，评估设备的移动威胁风险。

Intune 设备符合性策略包括基于 Check Point SandBlast 风险评估的 Check Point SandBlast Mobile 威胁防御规则。 启用此规则后，Intune 将评估设备是否符合已启用的策略。 如果发现设备不符合，将阻止用户访问 Exchange Online 和 SharePoint Online 等公司资源。 用户还可通过安装在设备上的 Check Point Sandblast Mobile 应用获取指导，以便解决问题并重新访问公司资源。

以下是一些常见方案：

### <a name="control-access-based-on-threats-from-malicious-apps"></a>基于来自恶意应用的威胁来控制访问

在设备上检测到恶意应用（如恶意软件）时，可阻止设备，直到解除威胁：

- 连接到公司电子邮件

- 使用 OneDrive for Work 应用同步企业文件

- 访问公司应用

*检测到恶意应用时对其进行阻止：*

> [!div class="mx-imgBorder"]
> ![Check Point MTD 检测到恶意应用时对其进行阻止](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-2.PNG)

*修正后授予访问权限：*

> [!div class="mx-imgBorder"]
> ![Check Point MTD 授予访问权限](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-3.PNG)

### <a name="control-access-based-on-threat-to-network"></a>基于对网络的威胁来控制访问

检测**中间人**等网络威胁，并基于设备风险保护对 WiFi 网络的访问。

*阻止通过 Wi-Fi 访问网络：*

> [!div class="mx-imgBorder"]
> ![Check Point MTD 阻止通过 Wi-Fi 访问网络](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-4.PNG)

*修正后授予访问权限：*

> [!div class="mx-imgBorder"]
> ![Check Point MTD 授予 Wi-Fi 访问权限](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-5.PNG)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>根据网络威胁控制对 SharePoint Online 的访问

检测**中间人**等网络威胁，根据设备风险阻止公司文件的同步。

*检测到网络威胁时阻止 SharePoint Online：*

> [!div class="mx-imgBorder"]
> ![Check Point MTD 阻止 SharePoint Online 访问](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-6.PNG)

*修正后授予访问权限：*

> [!div class="mx-imgBorder"]
> ![Check Point MTD 授予 SharePoint Online 访问权限](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-7.PNG)

<!-- ### Control access on unenrolled devices based on threats from malicious apps

When the Check Point Sandblast Mobile Threat Defense solution considers a device to be infected:
> [!div class="mx-imgBorder"]
> ![App protection policy blocks due to detected malware](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/sandblast-app-policy-block.png)

Access is granted on remediation:

> [!div class="mx-imgBorder"]
> ![Access is granted on remediation for App protection policy](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/sandblast-app-policy-remediated.png)
-->

## <a name="next-steps"></a>后续步骤

- [将 CheckPoint SandBlast 与 Intune 集成](checkpoint-sandblast-mobile-mtd-connector-integration.md)

- [设置 CheckPoint SandBlast Mobile 应用](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [创建 CheckPoint SandBlast Mobile 设备符合性策略](mtd-device-compliance-policy-create.md)

- [启用 CheckPoint SandBlast Mobile MTD 连接器](mtd-connector-enable.md)
