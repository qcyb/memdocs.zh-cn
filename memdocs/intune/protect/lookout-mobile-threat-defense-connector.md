---
title: Lookout MTD 连接器与 Microsoft Intune
titleSuffix: Microsoft Intune
description: 了解如何将 Intune 与 Lookout 移动威胁防御 (MTD) 相集成以控制移动设备对公司资源的访问。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/09/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 3a730a5d-2a90-42b0-aa28-aadfc7a18788
ms.reviewer: davera
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 17b120faa0021a1fc044d7831b4b81ea88f404a7
ms.sourcegitcommit: bbb63f69ff8a755a2f2d86f2ea0c5984ffda4970
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "79526574"
---
# <a name="lookout-mobile-endpoint-security-connector-with-intune"></a>Lookout 移动终结点安全连接器与 Intune

可根据 Lookout 给出的风险评估，控制移动设备对公司资源的访问，Lookout 是与 Microsoft Intune 集成的移动威胁防御解决方案。 基于通过 Lookout 服务从设备收集的遥测评估风险，包括：
- 操作系统漏洞
- 安装的恶意应用
- 恶意网络配置文件

可以基于通过注册设备的 Intune 合规性策略启动的 Lookout 风险评估配置条件访问策略，从而根据检测到的威胁允许或阻止不符合设备访问公司资源。 对于未注册设备，可使用应用保护策略根据检测到的威胁强制执行阻止或选择性擦除操作。

## <a name="how-do-intune-and-lookout-mobile-endpoint-security-help-protect-company-resources"></a>Intune 和 Lookout 移动终结点安全如何帮助保护公司资源？

在移动设备上安装并运行 Lookout 移动应用 Lookout for work  。 此应用可捕获文件系统、网络堆栈以及设备和应用程序遥测（如果有），然后将其发送到 Lookout 云服务，评估设备的移动威胁风险。 可在 Lookout 控制台中更改威胁的风险等级分类以满足你的需求。

- 支持已注册设备  - Intune 设备符合性策略包括移动威胁防御 (MTD) 规则，该规则可以使用 Lookout for work 中的风险评估信息。 启用 MTD 规则后，Intune 将评估设备是否符合已启用的策略。 如果发现设备不符合，将阻止用户访问 Exchange Online 和 SharePoint Online 等公司资源。 用户还可以通过安装在其设备上的 Lookout for work 应用获取指导以解决问题并重新访问公司资源。 若要支持将 Lookout for work 与已注册设备一起使用，请执行以下操作：
  - [将 MTD 应用添加到设备](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md)
  - [创建支持 MTD 的设备合规性策略](../protect/mtd-device-compliance-policy-create.md)
  - [在 Intune 中启用 MTD 连接器](../protect/mtd-connector-enable.md)

- **支持未注册设备** - 在使用 Intune 应用保护策略时，Intune 可以在未注册的设备上使用 Lookout for work 应用的风险评估数据。 管理员可以使用此组合帮助保护[受 Microsoft Intune 保护的应用](../apps/apps-supported-intune-apps.md)中的公司数据，管理员还可以对未注册设备上的公司数据发出阻止或选择性擦除。 若要支持将 Lookout for work 与未注册设备一起使用，请执行以下操作：
  - [将 MTD 应用添加到未注册设备](../protect/mtd-add-apps-unenrolled-devices.md)
  - [创建移动威胁防御应用保护策略](../protect/mtd-app-protection-policy.md)
  - [为未注册设备启用移动 MTD 连接器](../protect/mtd-enable-unenrolled-devices.md)

## <a name="supported-platforms"></a>受支持的平台

在 Intune 中注册时，Lookout 支持以下平台：

- **Android 4.1 及更高版本**  
- **iOS 8 及更高版本**  

有关平台和语言支持的其他相关信息，请访问 [Lookout 网站](https://personal.support.lookout.com/hc/articles/114094140253)。  

## <a name="prerequisites"></a>必备条件

- Lookout Mobile EndPoint Security 企业订阅  
- Microsoft Intune 订阅
- Azure Active Directory Premium
- 企业移动性和安全性 (EMS) E3 或 E5，并向用户分配许可证。  

有关详细信息，请参阅 [Lookout Mobile Endpoint Security](https://www.lookout.com/products/mobile-endpoint-security)

## <a name="sample-scenarios"></a>示例方案

以下是结合使用 Lookout 移动终结点安全与 Intune 的常见情形。

### <a name="control-access-based-on-threats-from-malicious-apps"></a>基于来自恶意应用的威胁来控制访问

在设备上检测到恶意应用（如恶意软件）时，可阻止进行以下操作，直到解决威胁：

- 连接到公司电子邮件
- 使用 OneDrive for Work 应用同步企业文件
- 访问公司应用

*检测到恶意应用时对其进行阻止：*

> [!div class="mx-imgBorder"]
> ![由于检测到恶意应用而阻止访问的策略概念图](./media/lookout-mobile-threat-defense-connector/malicious-apps-blocked.png)

*修正后授予访问权限：*

> [!div class="mx-imgBorder"]
> ![显示在修正后授予访问权限的概念图](./media/lookout-mobile-threat-defense-connector/malicious-apps-unblocked.png)

### <a name="control-access-based-on-threat-to-network"></a>根据网络威胁控制访问权限

检测中间人攻击等网络威胁，并基于设备风险保护对 WiFi 网络的访问。

*阻止通过 Wi-Fi 访问网络*

> [!div class="mx-imgBorder"]
> ![根据网络威胁阻止 WiFi 访问的示意图](./media/lookout-mobile-threat-defense-connector/network-wifi-blocked.png)

*修正后授予访问权限：*

> [!div class="mx-imgBorder"]
> ![允许修正后访问的条件访问概念图](./media/lookout-mobile-threat-defense-connector/network-wifi-unblocked.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>根据网络威胁控制对 SharePoint Online 的访问

检测到中间人攻击等网络威胁时，根据设备风险阻止对公司文件进行同步。

*检测到网络威胁时阻止 SharePoint Online：*

> [!div class="mx-imgBorder"]
> ![阻止对 SharePoint Online 的访问的概念图](./media/lookout-mobile-threat-defense-connector/network-spo-blocked.png)

*修正后授予访问权限：*

> [!div class="mx-imgBorder"]
> ![在解除网络威胁后允许访问的概念图](./media/lookout-mobile-threat-defense-connector/network-spo-unblocked.png)

### <a name="control-access-on-unenrolled-devices-based-on-threats-from-malicious-apps"></a>基于来自恶意应用的威胁控制对未注册设备的访问

Lookout Mobile Threat Defense 解决方案认为设备受到感染时：
> [!div class="mx-imgBorder"]
> ![应用保护策略由于检测到恶意软件而阻止访问](./media/lookout-mobile-threat-defense-connector/lookout-app-policy-block.png)

修正后授予访问权限：

> [!div class="mx-imgBorder"]
> ![应用保护策略在修正后授予访问权限](./media/lookout-mobile-threat-defense-connector/lookout-app-policy-remediated.png)

## <a name="next-steps"></a>后续步骤

以下是实现此解决方案必须执行的主要步骤：

- [设置 Lookout 集成](lookout-mtd-connector-integration.md)
- [在 Intune 中启用移动终结点安全](mtd-connector-enable.md)
- [添加和分配 Lookout for Work 应用](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [配置 Lookout 设备符合性策略](mtd-device-compliance-policy-create.md)
- [创建 MTD 应用保护策略](mtd-app-protection-policy.md)
