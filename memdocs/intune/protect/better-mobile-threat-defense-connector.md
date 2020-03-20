---
title: 通过 Intune 启用 Better Mobile Threat Defense 连接器
titleSuffix: Intune on Azure
description: 使用 Intune 设置 Better Mobile Threat Defense 连接器。
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
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 05dec05cdc5a16078328d736d2f622cea1b2aa00
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79353978"
---
# <a name="better-mobile-threat-defense-connector-with-intune"></a>通过 Intune 启用 Better Mobile Threat Defense 连接器

可根据 Better Mobile 进行的风险评估，使用条件访问控制移动设备对公司资源的访问，Better Mobile 是与 Microsoft Intune 集成的 Mobile Threat Defense (MTD) 解决方案。 基于从运行 Better Mobile 应用的设备收集的遥测评估风险。

可以基于通过已注册设备的 Intune 设备合规性策略启动的 Better Mobile 风险评估配置条件访问策略，从而根据检测到的威胁允许或阻止非合规设备访问公司资源。 对于未注册设备，可使用应用保护策略根据检测到的威胁强制执行阻止或选择性擦除操作。

## <a name="how-do-intune-and-better-mobile-help-protect-your-company-resources"></a>Intune 和 Better Mobile 如何帮助你保护公司资源？

在移动设备上安装并运行 Better Mobile 应用。 此应用可捕获文件系统、网络堆栈、设备和应用程序遥测（如果有），然后将数据发送到 Better Mobile 云服务，以评估设备的移动威胁风险。

- **支持已注册设备** - Intune 设备合规性策略包括移动威胁防御 (MTD) 规则，该规则可以使用 Better Mobile 中的风险评估信息。 启用 MTD 规则后，Intune 将评估设备是否符合已启用的策略。 如果发现设备不符合，将阻止用户访问 Exchange Online 和 SharePoint Online 等公司资源。 用户还可通过安装在设备上的 Better Mobile 应用获取指导，以便解决问题并重新访问公司资源。 若要支持将 Better Mobile 与已注册的设备一起使用，请执行以下操作：
  - [将 MTD 应用添加到设备](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md)
  - [创建支持 MTD 的设备合规性策略](../protect/mtd-device-compliance-policy-create.md)
  - [在 Intune 中启用 MTD 连接器](../protect/mtd-connector-enable.md)

- **支持未注册设备** - 在使用 Intune 应用保护策略时，Intune 可以在未注册的设备上使用 Better Mobile 应用的风险评估数据。 管理员可以使用此组合帮助保护[受 Microsoft Intune 保护的应用](../apps/apps-supported-intune-apps.md)中的公司数据，管理员还可以对未注册设备上的公司数据发出阻止或选择性擦除。 若要支持将 Better Mobile 与未注册的设备一起使用，请执行以下操作：
  - [将 MTD 应用添加到未注册设备](../protect/mtd-add-apps-unenrolled-devices.md)
  - [创建移动威胁防御应用保护策略](../protect/mtd-app-protection-policy.md)
  - [为未注册设备启用移动 MTD 连接器](../protect/mtd-enable-unenrolled-devices.md)

## <a name="supported-platforms"></a>受支持的平台

- **Android 4.1 及更高版本**

- **iOS 8.0 及更高版本**

## <a name="prerequisites"></a>必备条件

- Azure Active Directory Premium

- Microsoft Intune 订阅

- Better Mobile Threat Defense 订阅

  - 有关详细信息，请参阅[网站](https://www.better.mobi/)。

## <a name="sample-scenarios"></a>示例方案

以下是一些常见方案。

### <a name="control-access-based-on-threats-from-malicious-apps"></a>基于来自恶意应用的威胁来控制访问

在设备上检测到恶意应用（如恶意软件）时，可阻止进行以下操作，直到解决威胁：

- 连接到公司电子邮件

- 使用 OneDrive for Work 应用同步企业文件

- 访问公司应用

检测到恶意应用时对其进行阻止：

![检测到恶意应用的示意图](./media/better-mobile-threat-defense-connector/better-mobile-maliciousapps-blocked.png)

修正后授予访问权限：

![检测到恶意应用，授予访问权限](./media/better-mobile-threat-defense-connector/better-mobile-maliciousapps-unblocked.png)

### <a name="control-access-based-on-threat-to-network"></a>根据网络威胁控制访问权限

检测“中间人”攻击等网络威胁，并基于设备风险保护对 WiFi 网络的访问  。

阻止通过 Wi-Fi 访问网络：

![阻止通过 Wi-Fi 访问网络](./media/better-mobile-threat-defense-connector/better-mobile-network-wifi-blocked.png)

修正后授予访问权限：

![修正后授予访问权限的示意图](./media/better-mobile-threat-defense-connector/better-mobile-network-wifi-unblocked.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>根据网络威胁控制对 SharePoint Online 的访问

基于设备风险检测对网络的威胁，如“中间人”攻击和阻止同步企业文件  。

检测到网络威胁时阻止 SharePoint Online：

![检测到网络威胁时阻止 SharePoint Online](./media/better-mobile-threat-defense-connector/better-mobile-network-spo-blocked.png)

威胁解除后授予访问权限：

![Sharepoint 的威胁解除后授予访问权限示例](./media/better-mobile-threat-defense-connector/better-mobile-network-spo-unblocked.png)

### <a name="control--access-on-unenrolled-devices-based-on-threats-from-malicious-apps"></a>基于来自恶意应用的威胁控制对未注册设备的访问

BETTER Mobile 移动威胁防御解决方案认为设备会受到感染时：![应用保护策略由于检测到恶意软件而阻止访问](./media/better-mobile-threat-defense-connector/better-mobile-app-policy-block.png)

修正后授予访问权限：

![应用保护策略在修正后授予访问权限](./media/better-mobile-threat-defense-connector/better-mobile-app-policy-remediated.png)

## <a name="next-steps"></a>后续步骤

- [将 Better Mobile 与 Intune 集成](better-mobile-mtd-connector-integration.md)

- [设置 Better Mobile 应用](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [创建 Better Mobile 设备符合性策略](mtd-device-compliance-policy-create.md)

- [启用 Better Mobile MTD 连接器](mtd-connector-enable.md)

- [创建 MTD 应用保护策略](mtd-app-protection-policy.md) 
