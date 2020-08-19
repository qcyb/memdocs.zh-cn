---
title: 在 Microsoft Intune 中向 Windows Phone 8.1 设备添加自定义设置 - Azure | Microsoft Docs
titleSuffix: ''
description: 在 Microsoft Intune 中为运行 Windows Phone 8.1 的设备添加或创建自定义配置文件，以使用 OMA-URI 设置。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/11/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ROBOTS: NOINDEX
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 839130f11da41d8b3bd417e8ec3ff3f6301811ed
ms.sourcegitcommit: 8999e197f10fb72d1b82f30a599d1e588db237b7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88146365"
---
# <a name="use-custom-settings-for-windows-phone-81-devices-in-intune"></a>在 Intune 中使用适用于 Windows Phone 8.1 设备的自定义设置

[!INCLUDE [windows-phone-81-windows-10-mobile-support](../includes/windows-phone-81-windows-10-mobile-support.md)]

借助 Microsoft Intune，可以使用“自定义配置文件”添加或创建适用于 Windows Phone 8.1 设备的自定义设置。 自定义配置文件是 Intune 中的一项功能。 这项功能用于添加未内置到 Intune 的设备设置和功能。

Windows Phone 8.1 自定义配置文件使用开放移动联盟统一资源标识符 (OMA-URI) 设置配置不同的功能。 移动设备制造商通常使用这些设置来控制设备上的功能。 [Windows Phone 8.1 MDM 协议文档](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-phone/dn499787(v=technet.10))列出了设置。

本文介绍如何创建适用于 Windows Phone 8.1 设备的自定义配置文件。 

## <a name="before-you-begin"></a>在开始之前

[创建 Windows Phone 8.1 自定义配置文件](custom-settings-configure.md)。

## <a name="custom-oma-uri-settings"></a>自定义 OMA-URI 设置

- **OMA-URI 设置**：添加以下设置：

  - **名称**：输入 OMA-URI 设置的唯一名称，以帮助你在设置列表中识别它。
  - **描述**：输入设置的简要说明以及有助于找到该配置文件的其他所有相关信息。
  - **OMA-URI**（区分大小写）：输入要用作设置的 OMA-URI。
  - **数据类型**：选择用于此 OMA-URI 设置的数据类型。 选项包括：

    - 字符串
    - 字符串（XML 文件）
    - 日期和时间
    - 整数
    - 浮点
    - 布尔值
    - Base64（文件）

  - **值**：输入要与已输入的 OMA-URI 关联的数据值。 值取决于所选的数据类型。 例如，如果选择了“日期和时间”，则从日期选取器中选择值。

  添加一些设置后，可以选择“导出”。 “导出”将创建逗号分隔值 (.csv) 文件中添加的所有值的列表。

## <a name="example"></a>示例

在以下示例中，当 Windows Phone 8.1 设备超出运营商覆盖区域时，会阻止设备更改手机网络。

- **名称**：允许手机网络数据漫游
- **描述**：允许或禁止手机网络数据漫游
- OMA-URI（区分大小写）：./Vendor/MSFT/PolicyManager/My/Connectivity/AllowCellularDataRoaming
- **数据类型**：整数
- **值**：0

## <a name="next-steps"></a>后续步骤

[分配配置文件](device-profile-assign.md)并[监视其状态](device-profile-monitor.md)。

在 [Windows 10 设备上创建自定义配置文件](custom-settings-windows-10.md)。
